---
title: サポート センターをカスタマイズする
titleSuffix: Configuration Manager
description: サポート センターの構成ファイルをカスタマイズします。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1436f40dc989202725d7b83d551d318b970f9b5d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707440"
---
# <a name="customize-support-center"></a>サポート センターをカスタマイズする

*適用対象:Configuration Manager (Current Branch)*

[サポート センター](support-center.md) ツールには、カスタマイズ可能な構成ファイルが含まれます。 既定では、サポート センターをインストールすると、このファイルはパス `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config` にあります。 構成ファイルを使用してプログラムの動作を変更します。

- [データ収集をカスタマイズする](#bkmk_datacoll):データ収集時に含めることができるレジストリ キーと WMI 名前空間のセットを編集します  

- [ログ グループをカスタマイズする](#bkmk_loggroups):正規表現を使用してログ ファイルの新しいグループを定義します。 また、ログ グループに他のログ ファイルを追加します。  

- [ワイルドカードを使用して収集するログ ファイルを追加する](#bkmk_wildcards):ワイルドカード検索を使用して、追加のログ ファイルを収集します  

これらの変更を行うには、サポート センターをインストールしたクライアントでのローカル管理アクセス許可が必要です。 これらのカスタマイズを行うには、メモ帳や Visual Studio などのテキスト エディターまたは XML エディターを使います。

> [!Important]  
> サポート センターの構成ファイルは、XML 形式のファイルです。 サポート センターの動作には不可欠です。 このファイルの編集は、XML と正規表現に精通しているユーザーのみに推奨されます。  

サポート センターの構成ファイルをカスタマイズする前に、元のバックアップを保存します。 このバックアップにより、誤ってファイルを編集してしまった場合に、元のサポート センターの機能を回復できます。 バックアップを作成していなくて、構成ファイルの変更後にサポート センターが正しく機能しない場合は、サポート センターを再インストールします。 サポート センターの別のインストールから、構成ファイルをコピーすることもできます。



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a> データ収集をカスタマイズする

クライアントでのデータの収集をカスタマイズするには、`<dataCollectorSettings>` 要素に含まれる XML 要素を使用してサポート センターの構成ファイルを変更します。


### <a name="wmi-data-collection"></a>WMI データの収集

`<CcmWmiDataCollector>` 要素には、`<collectionScopes>` 要素が含まれます。 この要素を使用して、サポート センターがデータを収集する WMI 名前空間を変更できます。 また、`<ignoreScopes>` 要素も含まれています。 この要素を使用すると、`<collectionScopes>` 要素で定義されている名前空間でのデータ収集から除外する部分を指定できます。  
    
#### <a name="example"></a>例
既定の構成ファイルでは、`root\ccm` 名前空間からデータが収集されます。 このパスは、`<collectionScopes>` 内の `<add/>` 要素に含まれます。 

また、この名前空間の `\cimodels`、`\invagt`、 `\events`、および `\policy` パスの下にあるものはすべて無視されます。 これらのパスは、`<ignoreScopes>` 内の `<add/>` 要素に含まれます。

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>レジストリ データの収集

`<RegistryDataCollector>` 要素には `<registryKeys>` 要素が含まれます。 サポート センターが `HKEY_LOCAL_MACHINE` パスの下で収集するレジストリ キーとサブキーを変更するには、この要素を使用します。 サポート センターでは、他のルート レジストリ パスからのレジストリ データの収集はサポートされていません。

#### <a name="example"></a>例
デバイスにインストールされているクラシック プログラム用のレジストリ キーを収集するには、次の `<add/>` 要素を `<registryKeys>` 要素に追加します。`<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a> ログ ファイル グループをカスタマイズする

サポート センターで収集されるログ ファイル、および**ログ グループ**の一覧でのそれらの表示方法をカスタマイズするには、`<logGroups>` 要素内の要素を使用します。 サポート センターを開始すると、構成ファイルのこのセクションがスキャンされます。 その後、`<logGroups>` 要素に含まれる `<add/>` 要素で検出された一意のキー属性値ごとに、**ログ グループ**の一覧にグループが作成されます。

- **コンポーネント ログ グループ**:`<componentLogGroup>` 要素では、キー属性を使用して、一覧に表示されるログ グループの名前を定義します。 また、正規表現 (regex) を含む値属性も使用されます。 この正規表現を使用して、関連するログ ファイルのセットが収集されます。  

- **静的ログ グループ**:`<staticLogGroup>` 要素では、キー属性を使用して、一覧に表示されるログ グループの名前を定義します。 また、ログ ファイル名が定義されている値属性も使用されます。  

`<componentLogGroup>` 要素と `<staticLogGroup>` 要素両方の `<add/>` 要素で同じキー属性値を使用すると、1 つのグループが作成されます。 このグループには、同じキーを使用する両方の要素で定義されているログ ファイルが含まれます。

#### <a name="example"></a>例
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a> ワイルドカードを使用して収集するログ ファイルを追加する

収集するログ ファイルを追加するには、ファイル パスまたはファイル名でワイルドカードを使用します。 これらのワイルドカードには `%WINDIR%` などのシステム全体の環境変数は含まれますが、`%USERPROFILE%` のようなユーザー スコープの環境変数は除外されます。 この非再帰的なログ ファイル検索を使用して追加のログ ファイルを収集するには、`<additionalLogFiles>` 要素内に `<add/>` 要素を使用します。 

以下の例では、サポート センターにより既定の構成ファイルでのこの機能が使用される方法を示します。

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>例 1:Windows ディレクトリ内のすべての Windows Update ログ ファイルを収集する
次の要素では、Windows ディレクトリにある `WindowsUpdate.log` という名前のファイルがすべて収集されます。 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>例 2:Windows ログ ディレクトリ内のすべてのログ ファイルを収集する
次の要素では、Windows ログ ディレクトリにある末尾が `.log` のすべてのファイルが収集されます。 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>XML の完全な例
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
