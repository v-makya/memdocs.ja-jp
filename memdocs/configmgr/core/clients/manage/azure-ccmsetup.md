---
title: Azure AD の認証ワークフロー
titleSuffix: Configuration Manager
description: Azure Active Directory 認証を使用した Windows 10 デバイスへの Configuration Manager クライアントのインストール プロセスの詳細
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695000"
---
# <a name="azure-ad-authentication-workflow"></a>Azure AD の認証ワークフロー

*適用対象:Configuration Manager (Current Branch)*

この記事は、Azure Active Directory (Azure AD) に参加している Windows 10 デバイスへの Configuration Manager クライアントのインストール プロセスに関するテクニカル リファレンスです。 デバイスの認証とクライアントのインストールのためのワークフロー プロセスについて詳しく説明します。  
 

## <a name="azure-ad-token-request-workflow"></a>Azure AD トークン要求ワークフロー

![Azure AD CCMSetup のワークフロー図](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1.Azure AD トークン要求

Windows 10 Azure AD ドメインに参加しているクライアントは、Azure AD パラメーターを使用してトークンを要求します。 次のエントリが **ccmsetup.log** に記録されます。

- Azure AD デバイス トークンを要求します。

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- デバイス トークンを取得できない場合は、Azure AD ユーザー トークンが要求されます。

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> クライアントは、Azure AD に参加するときにワークプレース参加 (WPJ) 証明書を取得する必要があります。 ワークプレース参加証明書が見つからない場合、クライアントでは、セキュリティ トークン サービス通信チャネル (CCM_STS) を使用した要求の作成が試行されません。 この動作は、クライアントで Azure AD トークンを要求に追加できないためです。 クライアントが Azure AD に正しく参加していない場合、通常、デバイスにはこの証明書がありません。
>
> さらに、トークンが無効な場合、クラウド管理ゲートウェイ (CMG) から内部サイトの役割にその要求は転送されません。 テナントが Configuration Manager にクラウド管理サービスとして登録されていない場合、トークンは無効になる可能性があります。


### <a name="2-configuration-manager-client-token-request"></a>2.Configuration Manager クライアント トークン要求

クライアントでは、Azure AD トークンを取得すると、Configuration Manager クライアント (CCM) トークンを要求します。

次のエントリが CMG 仮想マシンの **ccmsetup.log** に記録されます。

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 CMG で要求を受け取る

次のエントリが **IIS.log** に記録されます。

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 CMG で要求を CMG 接続ポイントに転送する

次のエントリが **CMGService.log** に記録されます。

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 CMG 接続ポイントで CMG クライアント要求を管理ポイント クライアント要求に変換する

次のエントリが **SMS_CLOUD_PROXYCONNECTOR.log** に記録されます。

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 管理ポイントでサイト データベースのユーザー トークンを確認する

次のエントリが **CCM_STS.log** に記録されます。

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>コンテンツの場所の要求

クライアントでは、CCM トークンで応答を受け取ると、それをキャッシュして使用し、CMG を介してサイト情報とコンテンツの場所を要求します。 次のエントリが **ccmsetup.log** に記録されます。

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>クライアントのインストール

デバイスでは、クライアント コンテンツをダウンロードしてインストールを開始します。

### <a name="communication-validation"></a>通信の検証

- CMG では、CMG、CMG 接続ポイントと HTTP(S)、および管理ポイント データベース要求を介してクライアント トークンを検証します。
- クライアントで CMG サービス証明書または管理証明書を検証する
- CMG サービス証明書の PKI:クライアントには、ローカル ストア上の CMG 証明書のルート証明機関 (CA) が必要です
- サードパーティの CMG サービス証明書:クライアントによって、インターネット上で公開されているルート CA を使って証明書が自動的に検証されます


## <a name="common-issues"></a>一般的な問題

- ルート CA が存在しない
- CRL チェックを有効にする: CRL をインターネット上に公開するか、コマンド ラインで **/NoCRLcheck** オプションを使用します
- WPJ 証明書が見つからない: クライアントは Azure AD に登録されていますが、Azure AD に参加していません

/NoCRLCheck の使用は、ccmsetup ブートストラップにのみ適しています。 クライアントが完全に機能するには、インターネット上に CRL を公開する必要があります。 回避策として、サイトのクライアント通信構成で CRL チェックを無効にすることができます。 それ以外の場合、セキュリティ設定がロケーション サービスによって更新された後、クライアントはサーバーとの通信を停止します。


## <a name="client-registration"></a>クライアントの登録

![Azure AD の登録ワークフロー図](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1.Configuration Manager クライアント要求の登録

次のエントリが **ClientIDManagerStartup.log** に記録されます。

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2.クライアントを登録するための Configuration Manager 要求の Azure AD トークン

次のエントリが **ADALOperationProvider.log** に記録されます。

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2.1 Configuration Manager クライアントが登録される  

次のエントリが **ClientIDManagerStartup.log** に記録されます。

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> クライアントの登録中は、証明書の検証が常に実行されます。 クライアントの登録に Azure AD の認証方法を使っている場合でも、この処理が実行されます。


### <a name="3-configuration-manager-client-token-request"></a>3.Configuration Manager クライアント トークン要求

サイトによりクライアントが登録されると、クライアントによって CCM トークンが要求されます。 CCM トークンはローカル システム アカウント (S-1-5-18) 用に暗号化され、8 時間キャッシュされます。 8 時間経過するとトークンの有効期限が切れ、クライアントによりトークンの更新が要求されます。

次のエントリが **ClientIDManagerStartup.log** に記録されます。

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3.1 CMG で要求を受け取る

次のエントリが **IIS.log** に記録されます。

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3.2 CMG により要求が CMG 接続ポイントに転送される

次のエントリが **CMGService.log** に記録されます。

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3.3 CMG 接続ポイントにより CMG クライアント要求が管理ポイント クライアント要求に変換される

次のエントリが **SMS_CLOUD_PROXYCONNECTOR.log** に記録されます。

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3.4 管理ポイントでサイト データベースのユーザー トークンを確認する

次のエントリが **CCM_STS.log** に記録されます。

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
