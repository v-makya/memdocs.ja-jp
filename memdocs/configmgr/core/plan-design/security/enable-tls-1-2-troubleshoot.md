---
title: トランスポート層セキュリティ (TLS) 1.2 を有効にしたときの一般的な問題
titleSuffix: Configuration Manager
description: トランスポート層セキュリティ (TLS) 1.2 を有効にしたときの一般的な問題について説明します
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 316387bc42ed51dd9b581a25208091ed93cad1d1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699757"
---
# <a name="common-issues-when-enabling-tls-12"></a>TLS 1.2 を有効にしたときの一般的な問題

この記事では、Configuration Manager で TLS 1.2 のサポートを有効にしたときに発生する一般的な問題について説明します。

## <a name="unsupported-platforms"></a>サポートされていないプラットフォーム

次のクライアント プラットフォームは、Configuration Manager によってサポートされていますが、TLS 1.2 環境ではサポートされていません。

- Windows CE
- Apple OS X
- オンプレミス MDM で管理されている Windows 10 デバイス

## <a name="reports-dont-show-in-the-console"></a>コンソールにレポートが表示されない

Configuration Manager コンソールにレポートが表示されない場合は、コンソールを実行しているコンピューターを必ず更新してください。 [.NET Framework を更新](enable-tls-1-2-client.md#bkmk_net)し、強力な暗号化を有効にします。

## <a name="fips-security-policy-enabled"></a>FIPS セキュリティ ポリシーが有効

クライアント、サーバーのいずれかに対して FIPS セキュリティ ポリシーの設定を有効にした場合、セキュリティで保護されたチャネル (Schannel) のネゴシエーションによりそれらで TLS 1.0 が使われるようになる場合があります。 この動作は、レジストリでプロトコルを無効にした場合でも発生します。

調べるには、セキュリティで保護されたチャネルのイベント ログを有効にしてから、システム ログで Schannel イベントを確認します。 詳細については、「[Schannel.dll で特定の暗号アルゴリズムおよびプロトコルの使用を制限する方法](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)」をご覧ください。

## <a name="sql-server-communication-failure"></a>SQL Server の通信エラー

SQL Server の通信が失敗し、**SslSecurityError** エラーが返される場合は、以下の設定を確認します。

- [.NET Framework を更新](enable-tls-1-2-server.md#bkmk_net)し、各コンピューター上で強力な暗号化を有効にする
- ホスト サーバー上の [SQL Server を更新する](enable-tls-1-2-server.md#bkmk_sql)
- SQL と通信するすべてのシステム上で [SQL クライアント コンポーネントを更新する](enable-tls-1-2-server.md#bkmk_sql-client)。 例: サイト サーバー、SMS プロバイダー、サイトの役割サーバー。

## <a name="configuration-manager-client-communication-failures"></a>Configuration Manager クライアントの通信エラー

Configuration Manager クライアントがサイトの役割と通信していない場合は、WinHTTP を使ってクライアントとサーバー間の通信で TLS 1.2 をサポートするように [Windows を更新した](enable-tls-1-2-client.md#bkmk_winhttp)ことを確認します。 一般的なサイトの役割としては、配布ポイント、管理ポイント、状態移行ポイントなどがあります。

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>レポート サービス ポイントが失敗し、予期されるエラーが返される

レポート サービス ポイントでレポートが構成されていない場合は、**SRSRP.log** で次のエラー エントリを確認します。

`The underlying connection was closed:`
`An expected error occurred on a receive.`

この問題を解決するには、次の手順を実行します。

1. [.NET Framework を更新](enable-tls-1-2-client.md#bkmk_net)し、関連するすべてのコンピューター上で強力な暗号化を有効にします。

1. いずれかの更新プログラムをインストールしたら、SMS_Executive サービスを再起動します。

## <a name="application-catalog-doesnt-initialize"></a>アプリケーション カタログが初期化されない

> [!Important]  
> アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。 詳細については、[削除された機能と非推奨の機能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。

アプリケーション カタログが初期化されない場合は、**ServicePortalWebSite.svclog** ファイルで次のエラー エントリを確認します。

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

この問題を解決するには、次の手順を実行します。

1. [.NET Framework を更新](enable-tls-1-2-client.md#bkmk_net)し、関連するすべてのコンピューター上で強力な暗号化を有効にします。

1. アプリケーション カタログ サーバーの `%WinDir%\System32\InetSrv` フォルダー内に、以下の内容を含む **W2SP.exe.config** ファイルを作成します。

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > このファイルは、アプリケーションが .NET Framework 4.6.3 を使用してビルドされた場合に作成される既定のファイルです。

1. アプリケーション カタログの役割には HTTPS トランスポート セキュリティを使用します。

    > [!Important]
    > アプリケーション カタログの役割に HTTP メッセージ セキュリティを使用する場合、SSL 3.0 と TLS 1.0 のみを使用するように WCF がハードコーディングされます。 これによって TLS 1.2 の使用が妨げられます。

1. 何らかの変更を加えた場合は、コンピューターを再起動します。

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>ソフトウェア センターまたはブラウザーがアプリケーション カタログと通信しない

> [!Important]  
> アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。 詳細については、[削除された機能と非推奨の機能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。

TLS 1.2 が有効なサイト内で、ソフトウェア センターがユーザーが利用できるアプリと連携できるようにするための最善の方法は、アプリケーション カタログの役割を削除することです。 そして、ソフトウェア センターが管理ポイントと直接通信できるようにします。 詳細については、「[アプリケーション カタログの削除](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)」を参照してください。

アプリケーション カタログとソフトウェア センター間の通信エラーを解決する必要がある場合は、次の条件を確認します。

- [.NET Framework を更新](enable-tls-1-2-client.md#bkmk_net)し、各コンピューター上で強力な暗号化を有効にする。

- 変更を行った後、影響を受けたすべてのコンピューターを再起動する。

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>サービス接続ポイントのアップロード エラー

サービス接続ポイントから SCCMConnectedService にデータがアップロードされない場合は、[.NET Framework を更新](enable-tls-1-2-server.md#bkmk_net)し、各コンピューター上で強力な暗号化を有効にします。 変更を加えたら、そのコンピューターを再起動することを忘れないようにします。

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager コンソールに Intune のオンボード ダイアログ ボックスが表示される

コンソールで Intune ポータルに接続しようとすると、Intune のオンボード ダイアログ ボックスが表示される場合は、[.NET Framework を更新](enable-tls-1-2-client.md#bkmk_net)し、各コンピューター上で強力な暗号化を有効にします。 変更を加えたら、そのコンピューターを再起動することを忘れないようにします。

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Configuration Manager コンソールに Azure へのサインイン エラーが表示される

Azure Active Directory (Azure AD) でアプリケーションを作成しようとしたとき、 **[サインイン]** を選択した直後に Azure サービスのオンボード ダイアログ ボックスが失敗する場合は、[.NET Framework を更新](enable-tls-1-2-server.md#bkmk_net)し、強力な暗号化を有効にします。 変更を加えたら、そのコンピューターを再起動することを忘れないようにします。

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager のクラウド サービスと TLS 1.2

クラウド管理ゲートウェイとクラウド配布ポイントで使用される Azure 仮想マシンでは、TLS 1.2 がサポートされています。 サポートされているクライアント バージョンでは、TLS 1.2 が自動的に使用されます。

**SMSAdminui.log** に、次の例のようなエラーが記録される場合があります。

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

System の EventLog に、次の説明と共に SChannel EventID 36874 が記録される場合があります: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>その他のリソース

- [.NET Framework でのトランスポート層セキュリティ (TLS) のベスト プラクティス](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244:Microsoft SQL Server 用の TLS 1.2 のサポート](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [暗号化コントロールのテクニカル リファレンス](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>次のステップ

- [クライアントで TLS 1.2 を有効にする](enable-tls-1-2-client.md)
- [サイト サーバーとリモート サイト システムで TLS 1.2 を有効にする](enable-tls-1-2-server.md)