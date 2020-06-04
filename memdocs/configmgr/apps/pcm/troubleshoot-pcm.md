---
title: パッケージ変換マネージャーのトラブルシューティング
titleSuffix: Configuration Manager
description: Configuration Manager のパッケージ変換マネージャーに関する問題をトラブルシューティングする方法について説明します。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877621"
---
# <a name="troubleshoot-package-conversion-manager"></a>パッケージ変換マネージャーのトラブルシューティング

*適用対象:Configuration Manager (Current Branch)*

<!--1357861-->

パッケージ変換マネージャーを使用する際の問題をトラブルシューティングするには、この記事の情報を参考にします。



## <a name="sms-provider"></a>SMS プロバイダー

パッケージ変換マネージャーでは SMS プロバイダーを使用します。 詳細については、「[SMS プロバイダーの計画](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)」を参照してください。

SMS プロバイダーが正しく動作していない場合、パッケージ変換マネージャーを含む Configuration Manager コンソールは機能しません。



## <a name="package-readiness"></a>パッケージの準備

パッケージをアプリケーションに変換する前に、パッケージ変換マネージャーの**分析**機能を使用してパッケージを分析します。 分析が完了したら、Configuration Manager コンソールの **[パッケージ]** ノードで **[変換準備]** 列を追加します。 パッケージの一覧には、分析したパッケージの準備状態として次のいずれかが表示されます。

- **自動**:**変換**機能を使用して、パッケージを直接変換できます。      

  > [!NOTE]  
  > 自動変換では WQL クエリはアプリケーション要求には変換されません。 これらのクエリを変換するには、**修正と変換**プロセスを使用してください。  

- **手動**:**修正と変換**機能を使用してパッケージを変換する前に、パッケージにいくつかの追加または変更を加える必要があります。  

- **該当なし**:パッケージは変換に適していません。 パッケージで問題を解決するか、パッケージとして展開する必要があります。  

- **エラー**: パッケージにはエラーが含まれています。 パッケージを分析して変換する前に、これらのエラーを手動で修正してください。  

Configuration Manager コンソールの **[パッケージ]** ノードの詳細ウィンドウには準備上の問題が表示されます。 パッケージを選択して、詳細ウィンドウで **[概要]** タブを選択します。



## <a name="log-files"></a>ログ ファイル

### <a name="enable-logging"></a>ログを有効にする

パッケージ変換マネージャーでログを有効にすると、アクション、例外、およびエラーがすべて記録されます。

Configuration Manager でこのコンポーネントのログを有効にするには、**Microsoft.ConfigurationManagement.exe.Config** を変更します。既定では、この構成ファイルは次のパスにあります。  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> バージョン 1910 以降、このパスは `Microsoft Endpoint Manager` フォルダーを使用するように変更されました。 別のフォルダーに存在する可能性がある古いバージョンのファイルを使用しないようにしてください。

**system.diagnostics** 要素にある最後の **sources** 要素の後に、次に示す XML 要素 **switches** および **trace** を挿入します。

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

このサンプルでは **PCMTrace.log** ファイルを使用します。 このログは、Configuration Manager コンソールを実行しているコンピューター上の次のパスにあります。  
`%UserProfile%\AppData\Local\Temp`

詳細レベルを構成するには、**PcmLogging** トレース スイッチの設定を変更します。 この値を、詳細度最低の `1` から詳細度最高の `4` まで、4 段階の詳細レベルに設定します。


### <a name="smsprovlog"></a>SMSProv.log

場合によっては、パッケージ変換プロセスのトラブルシューティングに関する情報が **SMSProv.log** ファイルで見つかることがあります。 このファイルは、Configuration Manager の SMS プロバイダーから情報をキャプチャします。

既定では、このログ ファイルは Configuration Manager サイト サーバーの次のパスにあります。  
`C:\Program Files\Microsoft Configuration Manager\Logs`

次に示すいずれかのエラー メッセージが表示された場合、**SMSProv.log** ファイルには、関連するトラブルシューティング情報が含まれている可能性があります。

- `The SMS Provider reported an error`

- `Generic Failure`

これらのエラー メッセージは通常、エラーがサイト サーバーに起こったこと、およびエラー情報が Configuration Manager コンソールに送信されなかったことを示しています。

詳細については、「[Technical reference for Package Conversion Manager error messages](error-messages.md)」(パッケージ変換マネージャーのエラー メッセージのテクニカル リファレンス) を参照してください。



## <a name="changing-package-attributes-after-analysis"></a>分析後のパッケージの属性の変更

パッケージを分析し、その準備状態が **[自動]** または **[手動]** の場合は、関連する属性が変更されると、変換プロセスが失敗する可能性があります。

たとえば、パッケージを分析して、その準備状態が **[自動]** であるとします。 続いて、別のプログラムをパッケージに追加します。 この場合、パッケージの変換が失敗する可能性があります。

分析後にパッケージを変更する必要がある場合は、変換前に分析を再実行してください。 



## <a name="see-also"></a>関連項目

[Technical reference for Package Conversion Manager error messages](error-messages.md) (パッケージ変換マネージャーのエラー メッセージのテクニカル リファレンス)
