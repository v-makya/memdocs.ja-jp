---
title: Exchange Connector をインストールする
titleSuffix: Configuration Manager
description: ActiveSync を使用してモバイルデバイスを管理するには、Configuration Manager 用の Exchange connector をインストールして構成します。
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3d854e4b70a59a364b8611947feea89d4678e7e6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724846"
---
# <a name="install-and-configure-the-exchange-connector"></a>Exchange connector をインストールして構成する

*適用対象:Configuration Manager (Current Branch)*

モバイルデバイスを管理するように Exchange Server コネクタをインストールして構成するには、次の手順に従います。 Configuration Manager では、1 つの Exchange 組織に設定できるコネクタは 1 つのみです。

Configuration Manager 用の Exchange Server コネクタをインストールする前に、必要なアクセス許可とバージョンがあることを確認してください。 詳細については、「 [Exchange と Configuration Manager でのデバイス管理](manage-mobile-devices-with-exchange-activesync.md#prerequisites)」を参照してください。

## <a name="exchange-connection-account"></a>Exchange 接続アカウント

どのアカウントを Exchange クライアント アクセス サーバーに接続しモバイル デバイスを管理するかを判断します。 アカウントは、サイト サーバーのコンピューター アカウントでも、Windows ユーザー アカウントでも構いません。

次に、exchange の役割グループでこのアカウントを構成して、次の Exchange Server コマンドレットを実行します。

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Get-Mailbox**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Get-ユーザー**  

- **Set-ActiveSyncOrganizationSettings**  

次の Exchange Server の管理の役割にはこれらのコマンドレットが含まれます。

- 受信者管理
- 表示のみの組織管理
- Server Management

詳細については、Exchange Server 2013 のドキュメントの「[管理ロールグループ](https://docs.microsoft.com/exchange/understanding-management-role-groups-exchange-2013-help)について」を参照してください。

> [!TIP]  
> 必要なコマンドレットなしで Exchange Server コネクタをインストールまたは使用しようとすると、サイトサーバーコンピューター `Invoking cmdlet <cmdlet> failed`の easdisc .log ファイルに次のエラーが表示されます。

## <a name="install-the-connector"></a>コネクタをインストールする

1. Configuration Manager コンソールで、[**管理**] ワークスペースにアクセスし、[**階層の構成**] を展開して、[ **Exchange Server コネクタ**] を選択します。

1. リボンの [**ホーム**] タブの [**作成**] グループで、[ **Exchange Server の追加**] を選択します。

1. Exchange Server の追加ウィザードの [**全般**] ページで、exchange server 環境の1つを選択します。

    - **オンプレミスの Exchange server**: Active Directory サイトごとに1台のサーバーまたはクライアントアクセスサーバーの配列を指定します。

        サーバーまたはアレイがオフラインの場合は、Configuration Manager が使用するクライアント アクセス サーバーを検出しようとします。 失敗した場合、Configuration Manager はメール ボックス サーバーの使用にフォールバックして、クライアント アクセス サーバーに接続します。 接続を再試行すると、サイトサーバーコンピューター `Failed to open runspace for site <site_name>`の easdisc .log ファイルに次の警告が記録されます。

    - **ホスト型 Exchange サーバー**: exchange Online 環境のサーバーアドレスを指定します。

    次に、Exchange Server コネクタを実行するプライマリサイトを選択します。

1. [**アカウント**] ページで、Exchange サーバーに接続するアカウントを指定します。 詳細については、「 [Exchange の接続アカウント](#exchange-connection-account)」を参照してください。

1. [**検出**] ページで、デバイスを検索するための同期スケジュールとルールを構成します。

1. [**設定**] ページで、次のグループのモバイルデバイス設定を構成します。

    - **全般**
    - **パスワード**
    - **電子メール管理**
    - **Security**
    - **Application**

    詳細については、「 [Exchange connector の設定](manage-mobile-devices-with-exchange-activesync.md#policies)」を参照してください。

    [オンプレミスの MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md)Configuration Manager を使用してモバイルデバイスを登録する場合は、[**外部のモバイルデバイス管理を許可**する] オプションを有効にします。 この設定により、これらのモバイルデバイスは Configuration Manager 登録した後も Exchange から電子メールを受信し続けることができます。

1. ウィザードを完了します。

## <a name="verify-and-monitor"></a>確認と監視

Exchange Server コネクタがステータスメッセージとログファイルと共にインストールされていることを確認します。

- サイトコンポーネントマネージャー Exchange Server コネクタが正常にインストールされたことを確認します。 **SMS_EXCHANGE_CONNECTOR**コンポーネントから、メッセージの状態 ID **1015**を探します。

    指定されたクライアントアクセスサーバーがオフラインの場合、インストールは失敗する可能性があります。 Configuration Manager がコネクタを正常にインストールできない場合は、Configuration Manager 60 分ごとにインストールを再試行します。 インストールが成功するか、Exchange Server コネクタを削除するまで、再試行は続行されます。

- サイトサーバーコンピューターで、次のエントリについて**Sitecomp .log**を確認`Component SMS_EXCHANGE_CONNECTOR flagged for installation`します。 次のテキストを使用して、インストールが成功`STATMSG: ID=1015`したことをログに記録します。

インストールが完了したら、コネクタによって検出および管理されるモバイルデバイスを監視します。 モバイルデバイスのコレクションを表示し、モバイルデバイスのレポートを使用します。

> [!NOTE]  
> Configuration Manager は、検出されたモバイルデバイスの名前を生成します。 *ユーザー名*_*デバイスの種類*の形式を使用します。 たとえば、 **jdoe_WindowsPhone**のようにします。 あるユーザーが同じ種類のモバイル デバイスを複数持っているときは、それらのモバイル デバイスについて、Configuration Manager はコンソールおよびレポートに同じ名前を表示します。  

## <a name="see-also"></a>関連項目

- [構成クライアントとサイトシステムで使用されるポート](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [プロキシ サーバーのサポート](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [モバイルデバイスのセキュリティに関する推奨事項](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Exchange Server コネクタで管理されているモバイルデバイスのプライバシー情報](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)
