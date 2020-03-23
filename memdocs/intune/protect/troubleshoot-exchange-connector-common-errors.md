---
title: Intune Exchange コネクタに関する一般的なエラーのトラブルシューティング
titleSuffix: Microsoft Intune
description: オンプレミスの Microsoft Intune Exchange コネクタに関する一般的なエラーをトラブルシューティングして解決します。
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb35fdc400c89c64b689f4695a48d201e50fc617
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350656"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>Intune Exchange コネクタでのよくあるエラーを解決する

この記事は、Intune 管理者が Intune Exchange コネクタの操作に関する特定のエラーとメッセージを解決するのに役立ちます。  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>構成が失敗し、エラー コード 0x0000001 が返される

**問題**:  
Microsoft Intune Exchange Connector を構成しようとすると、次のエラー メッセージが表示されます。

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

この問題は、インターネット プロキシの設定が正しく構成されていない場合に発生する可能性があります。

**解決方法**:  
プロキシ設定の構成:
1. ローカル ネットワーク管理者に問い合わせて、プロキシ設定が正しく構成されていることを確認します。 
2. **Netsh winhttp** コマンドを使用してプロキシ サーバーを構成し、必要な除外リストを追加します。 次に例を示します。  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>構成が失敗し、エラー コード 0x000000b が返される   

**問題**:  
Microsoft Intune Exchange コネクタを構成しようとすると、次のエラー メッセージが表示されます。  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
Intune へのサインインに使用したアカウントが、Intune のグローバル管理者アカウントではない場合、この問題が発生する可能性があります。

**解決方法**:  
グローバル管理者であるアカウントを使用して Intune にサインインするか、お使いのアカウントをグローバル管理者グループに追加します。 詳細については、「[Microsoft Intune でのロール ベースの管理制御 (RBAC)](../fundamentals/role-based-access-control.md)」を参照してください。

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>構成が失敗し、エラー コード 0x0000006 が返される

**問題**:  
Microsoft Intune Exchange コネクタを構成しようとすると、次のエラー メッセージが表示されます。  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
このエラーは、インターネットへの接続にプロキシ サーバーが使用されていて、それにより Intune サービスへのトラフィックがブロックされている場合に、発生する可能性があります。 プロキシが使用されているかどうかを確認するには、 **[コントロール パネル]**  >  **[インターネット オプション]** に移動し、 **[接続]** タブを選択して、 **[LAN の設定]** をクリックします。

**解決方法**:  

- **オプション 1** - プロキシの設定を削除し、プロキシを経由せずにコンピューターがインターネットに接続できるようにします。  

- **オプション 2** - 「[Intune Exchange Connector の要件](exchange-connector-install.md#intune-exchange-connector-requirements)」に記載されているように、Intune サービスとの通信を許可するようにプロキシ サーバーを構成します。



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>イベント 7000 または 7041: Microsoft Intune Exchange Connector サービスが開始しません

**問題**:  
Intune での iOS デバイスの登録が失敗し、次のいずれかのエラー メッセージが生成されます。  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
この問題は、**WIEC_User** アカウントにローカル ポリシーでの**サービスとしてログオン** ユーザー権利がない場合に、発生する可能性があります。

**解決方法**:  
Intune Exchange コネクタが実行されているコンピューターで、**サービスとしてログオン** ユーザー権利を、**WIEC_User** サービス アカウントに割り当てます。 コンピューターがクラスター内のノードである場合は、"*サービスとしてログオン*" ユーザー権利を、クラスター内のすべてのノードのクラスター サービス アカウントに割り当てます。  

**サービスとしてログオン** ユーザー権利をコンピューターの **WIEC_User** サービス アカウントに割り当てるには、次の手順のようにします。

1. 管理者として、または Administrators グループのメンバーとして、コンピューターにログオンします。
2. **secpol.msc** を実行し、ローカル セキュリティ ポリシーを開きます。
3. **[セキュリティの設定]**  >  **[ローカル ポリシー]** に移動し、 **[ユーザー権利の割り当て]** を選択します。
4. 右のウィンドウで、 **[サービスとしてログオン]** をダブルクリックします。
5. **[ユーザーまたはグループの追加]** を選択し、**WIEC_USER** をポリシーに追加して、 **[OK]** を 2 回クリックします。

**サービスとしてログオン** ユーザー権利を **WIEC_User** に割り当てた後で削除した場合は、ドメイン管理者に連絡して、グループ ポリシー設定で上書きされているかどうかを確認します。  

## <a name="next-steps"></a>次のステップ  

次の記事は、特定のエラーの解決に役立ちます。
- [Intune Exchange コネクタでの一般的な問題を解決する](troubleshoot-exchange-connector-common-problems.md)。 

サポートまたは Intune コミュニティから支援を受けます。
- Intune コンソールを使用して問題のトラブルシューティングを行う方法、または Microsoft のサポート ケースを開く方法については、[サポートの利用](../fundamentals/get-support.md)に関するページを参照してください。 
- [Microsoft Intune フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod)に問題を投稿してください。  
