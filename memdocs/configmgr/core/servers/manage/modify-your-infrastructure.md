---
title: インフラストラクチャの変更
titleSuffix: Configuration Manager
description: Configuration Manager のインフラストラクチャに影響する、変更やアクションを実行します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694360"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Configuration Manager インフラストラクチャの変更

*適用対象:Configuration Manager (Current Branch)*

1 つ以上のサイトをインストールした後は、インフラストラクチャに影響を与える構成の変更やアクションの実行が必要になることがあります。

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a> SMS プロバイダーを管理する

SMS プロバイダーは、1 つ以上の Configuration Manager コンソールに、管理用の接続ポイントを提供します。 複数の SMS プロバイダーをインストールすると、サイトや階層を管理するための接続ポイントに冗長性を提供できます。

各 Configuration Manager サイトでは、以下の目的でセットアップを再実行できます。

- SMS プロバイダーのインスタンスを追加します。 追加する SMS プロバイダーの各インスタンスは、別個のコンピューターに配置する必要があります。

- SMS プロバイダーのインスタンスを削除します。 サイトの最後の SMS プロバイダーを削除するには、サイトをアンインストールする必要があります。

SMS プロバイダーのインストールや削除は、セットアップを実行したサイト サーバーのルート フォルダーにある **ConfigMgrSetup.log** を表示して監視します。

サイトの SMS プロバイダーを変更する前に、「[SMS プロバイダーの計画](../../plan-design/hierarchy/plan-for-the-sms-provider.md)」を参照してください。

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>サイトの SMS プロバイダーの構成を管理する  

1. Configuration Manager サイトのインストール フォルダーにある `\BIN\X64\setup.exe` から **Configuration Manager セットアップ**を実行します。

1. **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** を選択します。

1. **[サイトのメンテナンス]** ページで、 **[SMS プロバイダーの構成を変更する]** を選択します。

1. **[SMS プロバイダーの管理]** ページで、以下のオプションのいずれかを選択します。

    - **新しい SMS プロバイダーを追加する**:現在ホストしていない SMS プロバイダーをホストするためのコンピューターの FQDN を指定します。

    - **指定した SMS プロバイダーをアンインストールする**:SMS プロバイダーを削除するコンピューターの名前を選択します。

    > [!TIP]  
    > 2 台のコンピューター間で SMS プロバイダーを移動するには、まず、新しいコンピューターにそのプロバイダーをインストールします。 次に、元の場所からそれを削除します。 コンピューター間で SMS プロバイダーを移動するオプションはありません。

セットアップ ウィザードを終了すると、SMS プロバイダーの構成は完了です。 サイトの **[プロパティ]** の **[全般]** タブで、サイトの SMS プロバイダーがインストールされているコンピューターを確認します。

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a> Configuration Manager コンソールを管理する

以下のタスクは、Configuration Manager コンソールの管理に役立ちます。

- Configuration Manager コンソールに表示される言語を変更するには、「[Configuration Manager コンソールの言語を管理する](#BKMK_ManageConsoleLanguages)」セクションを参照してください。

- 追加のコンソールをインストールするには、「[Configuration Manager コンソールのインストール](../deploy/install/install-consoles.md)」を参照してください。

- サイト サーバーからリモートにあるコンソールを有効にするために DCOM アクセス許可を構成するには、「[リモートからの Configuration Manager コンソールに対する DCOM アクセス許可を構成する](#BKMK_ConfigDCOMforRemoteConsole)」を参照してください。

- 管理アクセス許可を変更し、コンソールでどのユーザーが何を表示して実行できるかを制限するには、「[管理ユーザーの管理スコープの変更](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)」を参照してください。

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a> Configuration Manager コンソールの言語を管理する

サイト サーバーのインストール中に、Configuration Manager コンソールのインストール ファイルおよびサイトでサポートされる言語パックが、サイト サーバーの Configuration Manager インストール パスの `\Tools\ConsoleSetup` サブフォルダーにコピーされます。

- サイト サーバーのこのフォルダーから Configuration Manager コンソールのインストールを開始すると、Configuration Manager コンソールとサポートされる言語パックのファイルがコンピューターにコピーされます。

- コンピューターの現在の言語設定用の言語パックが提供されている場合、Configuration Manager コンソールは、その言語で開かれます。

- Configuration Manager コンソールに関連付けられた言語パックが提供されていない場合は、Configuration Manager コンソールは英語 (米国) で開かれます。

たとえば、英語、ドイツ語、およびフランス語をサポートしているサイト サーバーから Configuration Manager コンソールをインストールします。 フランス語の言語設定のコンピューターでは、Configuration Manager コンソールもフランス語で開きます。 構成された言語が日本語のコンピューターで Configuration Manager コンソールを開いた場合、日本語の言語パックが提供されていないため、コンソールは英語で開かれます。  

Configuration Manager コンソールが開かれるたびに、以下が行われます。

- そのコンピューターに対して構成されている言語設定を特定します
- Configuration Manager コンソールに関連付けられている言語パックが提供されているかどうかを確認します
- 適切な言語パックを使用してコンソールが開かれます

コンピューターで構成されている言語設定に関係なく、Configuration Manager コンソールを英語で開きたい場合は、そのコンピューター上の言語パック ファイルを削除するか、名前を変更します。

コンピューターのロケール設定に関係なく Configuration Manager コンソールが常に英語で開くようにするには、次の手順に従います。  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Configuration Manager コンソールの英語専用バージョンをコンピューターにインストールする  

1. Windows エクスプローラーで、Configuration Manager インストールパスの `\Tools\ConsoleSetup\LanguagePack` に移動します。

1. **.msp** ファイルと **.mst** ファイルの名前を変更します。 たとえば、 **&lt;ファイル名\>.MSP** を **&lt; ファイル名\>.MSP.disabled** に変更します。

1. Configuration Manager コンソールをコンピューターにインストールします。

    > [!IMPORTANT]
    > サイト サーバーで新しいサーバー言語が構成された場合は、.msp ファイルと .mst ファイルが **LanguagePack** フォルダーに再びコピーされるため、上記の手順を繰り返して、英語専用の新しい Configuration Manager コンソールをインストールする必要があります。  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>既存の Configuration Manager コンソールのインストールでコンソール言語を一時的に無効にする

1. Configuration Manager コンソールを実行しているコンピューターで、Configuration Manager コンソールを閉じます。

1. エクスプローラーで、Configuration Manager コンソール コンピューターの &lt;*コンソールのインストール パス*>\Bin\ に移動します。  

1. コンピューターで設定されている言語のフォルダーの名前を変更します。 たとえば、コンピューターでドイツ語が設定されている場合は、 **[de]** フォルダーの名前を「 **de.disabled**」に変更します。  

1. コンピューターで設定されている言語で Configuration Manager コンソールを開くには、フォルダーを元の名前に戻します。 たとえば、「 **de.disabled** 」を「 **de**」に変更します。  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a> リモート コンソールのために DCOM アクセス許可を構成する

Configuration Manager コンソールを実行するユーザー アカウントには、SMS プロバイダーを使用してサイト データベースにアクセスするためのアクセス許可が必要です。 ただし、リモート Configuration Manager コンソールを使用する管理ユーザーには、次の場所での **リモート アクティブ化** DCOM アクセス許可も必要となります。

- サイト サーバー コンピューター

- SMS プロバイダーのインスタンスをホストする各コンピューター

**SMS Admins** という名前のセキュリティ グループは、コンピューター上の SMS プロバイダーへのアクセスを付与します。このグループは、必要な DCOM アクセス許可を付与するためにも使用できます。 このグループは、SMS プロバイダーがメンバー サーバーで実行されているときには、コンピューターに対してローカルです。 SMS プロバイダーがドメイン コントローラーで実行されているときには、ドメイン ローカル グループです。

> [!IMPORTANT]
> Configuration Manager コンソールでは WMI を使用して SMS プロバイダーに接続し、WMI では内部的に DCOM が使用されます。 Configuration Manager コンソールが SMS プロバイダー以外のコンピューターで実行されている場合、SMS プロバイダーのコンピューターで DCOM サーバーをアクティブにするためのアクセス許可が必要です。 既定では、リモートでアクティブにするためのアクセス許可は、組み込みの管理者グループのメンバーにのみ付与されます。
>
> SMS Admins グループに、リモート アクティブ化のアクセス許可を持つことを許可すると、このグループのメンバーは SMS プロバイダーのコンピューターに対して DCOM 攻撃を試みることができます。 また、この構成ではコンピューターの脆弱性が増します。 この脅威を軽減するには、SMS 管理者グループのメンバーシップを慎重に監視します。

以下の手順に従って、各中央管理サイト (CAS)、プライマリ サイト サーバー、および SMS プロバイダーがインストールされている各コンピューターを構成し、リモートからの Configuration Manager コンソールによるアクセスを管理ユーザーに付与します。

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>リモートからの Configuration Manager コンソール接続に対する DCOM アクセス許可の構成

1. ターゲット コンピューターの管理者として、`Dcomcnfg.exe` を実行して **[コンポーネント サービス]** を開きます。

1. **[コンポーネント サービス]** 、 **[コンピューター]** の順に展開し、 **[マイ コンピューター]** を選択します。 **[操作]** メニューの **[プロパティ]** を選択します。

1. **マイ コンピューターの [プロパティ]** ウィンドウで、 **[COM セキュリティ]** タブに切り替えます。 **[起動とアクティブ化のアクセス許可]** セクションで、 **[制限の編集]** を選択します。

1. **[起動とアクティブ化のアクセス許可]** ウィンドウで、 **[追加]** を選択します。

1. **[ユーザー、コンピューター、サービス アカウントまたはグループの選択]** ウィンドウで、 **[選択するオブジェクト名を入力してください]** ボックスに「`SMS Admins`」と入力し、 **[OK]** をクリックします。

   > [!TIP]
   > SMS Admins グループを見つけるために、次の設定を変更することが必要になる場合があります: **[場所の指定]** 。 このグループは、SMS プロバイダーがメンバー サーバーで実行されている場合は、そのコンピューターに対してローカルであり、SMS プロバイダーがドメイン コントローラーで実行されている場合は、ドメイン ローカル グループとなります。

1. **[SMS 管理者のアクセス許可]** セクションで、リモート アクティブ化を許可するために **[リモートからのアクティブ化]** 行の **[許可]** 列を選択します。

1. **[OK]** を選択して変更を保存し、すべてのウィンドウを閉じます。

SMS 管理者グループのメンバーに対して、リモートの Configuration Manager コンソールからのアクセスを許可するようにコンピューターが構成されました。

リモートの Configuration Manager コンソールをサポートする各 SMS プロバイダーのコンピューターで、この手順を繰り返します。

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a> サイト データベースの構成を変更する

サイトをインストールした後で、サイト データベースとサイト データベース サーバーの構成を変更することができます。 CAS サーバーまたはプライマリ サイト サーバーで Configuration Manager セットアップを実行し、変更を加えます。 サイト データベースは、同じコンピューター上の SQL Server の新しいインスタンス、またはサポートされているバージョンの SQL Server を実行する別のコンピューターに移動できます。 これらの変更は、セカンダリ サイトのデータベースの構成についてはサポートされません。

サポートの制限について詳しくは、「 [Configuration Manager 環境での手動によるデータベース変更のサポート ポリシー](https://support.microsoft.com/kb/3106512)」をご覧ください。  

> [!NOTE]
> サイトのデータベース構成を変更すると、Configuration Manager はサイト サーバー、およびそのデータベースと通信するリモート サイト システム サーバー上の Configuration Manager サービスを再起動または再インストールします。

### <a name="modify-the-database-configuration"></a>データベースの構成を変更する

サイト サーバーで Configuration Manager セットアップを実行し、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** オプションを選択します。 次に、 **[SQL Server の構成を変更する]** オプションを選択します。 次のサイト データベースの構成を変更することができます。

- データベースをホストする Windows ベースのサーバー。

- SQL Server データベースをホストするサーバーで使用されている SQL Server のインスタンス。

- データベース名。

- Configuration Manager によって使用中の SQL Server のポート。

- Configuration Manager によって使用中の SQL Server Service Broker のポート。

### <a name="move-the-site-database"></a>サイト データベースを移動する

サイト データベースを移動する場合は、以下の構成も確認してください。

- サイト データベースを新しいコンピューターに移動する場合は、SQL Server を実行するコンピューターのローカル **Administrators** グループに、サイト サーバーのコンピューター アカウントを追加します。 サイト データベースのために SQL Server クラスターを使用する場合は、各 Windows Server クラスター ノード コンピューターのローカル **Administrators** グループにコンピューター アカウントを追加します。

- データベースを SQL Server 上の新しいインスタンス、または新しい SQL Server コンピューターに移動する場合は、共通言語ランタイム (CLR) 統合を有効にします。 サイト データベースをホストする SQL Server のインスタンスに接続するには、**SQL Server Management Studio** を使用します。 その後、次のストアド プロシージャをクエリとして実行します: `sp_configure 'clr enabled',1; reconfigure`

- 新しい SQL Server がバックアップの場所にアクセスできることを確認します。 サイト データベースのバックアップを格納するために UNC を使っている場合は、データベースを新しいサーバーに移動した後で、新しい SQL Server のコンピューター アカウントが、UNC の場所への**書き込み**アクセス許可を持っていることを確認します。 この構成には、SQL Server AlwaysOn 可用性グループまたは SQL Server クラスターに移動する場合が含まれます。

> [!IMPORTANT]
> 管理ポイントのデータベース レプリカが 1 つ以上あるデータベースを移動する前に、まずデータベース レプリカを削除します。 データベースの移動が完了したら、データベースのレプリカを再構成できます。 詳細については、「[管理ポイントのデータベース レプリカ](../deploy/configure/database-replicas-for-management-points.md)」を参照してください。

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a> サイト データベース サーバーの SPN を管理する

サイト データベースのために SQL サービスを実行するアカウントを選択できます。

- コンピューターのシステム アカウントを使用してサービスが実行されると、サービス プリンシパル名 (SPN) が自動的に登録されます。

- ドメイン ローカル ユーザー アカウントでサービスを実行する場合は、SPN を手動で登録します。 SPN を使用すると、SQL クライアントおよびその他のサイトシステムで、Kerberos を使用した認証が可能です。 Kerberos 認証を使用しない場合、データベースへの通信は失敗する可能性があります。

SPN と Kerberos 接続の詳細については、[「Kerberos 接続用のサービス プリンシパル名の登録](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections)」を参照してください。

サイト データベース サーバーの SQL Server サービス アカウントのためには、**Setspn** ツールを使用して SPN を登録します。 SQL Server と同じドメイン内のコンピューターで、ドメイン管理者として Setspn を実行します。

以下の手順は、SQL Server サービス アカウントのための SPN を管理する方法の例です。 Setspn の詳細については、[SetSPN の概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\))に関するページを参照してください。

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>SQL Server サービス アカウントのためにドメイン ユーザーの SPN を手動で作成する

1. コマンド プロンプトを管理者として開きます。

1. 有効なコマンドを入力し、NetBIOS 名と FQDN の両方の SPN を作成します。

    > [!IMPORTANT]
    > クラスター化された SQL Server の SPN を作成するときは、SQL Server クラスターの仮想名を、SQL Server のコンピューター名として指定します。

    - NetBIOS 名: `setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        例: `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - FQDN: `setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        例: `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > SQL Server の名前付きインスタンスの SPN を登録するコマンドは、既定のインスタンスの SPN を登録するときに使用するコマンドと同じです。 唯一の例外は、ポート番号が、名前付きインスタンスが使用するポートと一致している必要があることです。

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>ドメイン ユーザーの SPN が正しく登録されていることを確認する

1. コマンド プロンプトを管理者として開きます。

1. 次のコマンドを入力します。`setspn -L <domain\SQL service account>`

    例: `setspn -L contoso\sqlservice`

1. 登録された **ServicePrincipalName** を調べます。 SQL Server 用の有効な SPN を作成したことを確認します。

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>SQL Server サービス アカウントをローカル システムからドメイン ユーザー アカウントに変更する

1. SQL Server サービス アカウントとして使用するドメインまたはローカルのシステム ユーザー アカウントを作成または選択します。

1. **[SQL Server 構成マネージャー]** を開きます。

1. **[SQL Server のサービス]** をクリックしてから、 **[SQL Server&lt;インスタンス名\>]** を開きます。

1. **[ログオン]** タブに切り替えます。 **[このアカウント]** を選択したら、手順 1. で指定したドメイン ユーザー アカウントのユーザー名とパスワードを入力します。

1. サービス アカウントの変更を確認し、SQL Server サービスを再起動します。

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a> サイト リセットを実行する

CAS またはプライマリ サイトでサイト リセットを実行すると、サイトでは以下が行われます。

- 既定の Configuration Manager ファイルおよびレジストリ アクセス許可を再適用する

- すべてのサイト コンポーネントとすべてのサイト システムの役割を再インストールする

セカンダリ サイトでは、サイト リセットはサポートされていません。

手動でサイトをリセットすることができます。 サイトの構成を変更した後に、自動的に実行することもできます。 次に例を示します。

- Configuration Manager コンポーネントによって使用されるアカウントに対して変更があった場合、手動でのサイト リセットを検討してください。 この操作により、新しいアカウントの詳細を使用するようにサイト コンポーネントが更新されます。

- サイトのクライアントまたはサーバーの言語を変更した場合、Configuration Manager によって自動的にサイト リセットが実行されます。 サイトで新しい言語を使用するためにはリセットが必要です。

> [!NOTE]
> サイト リセットでは、Configuration Manager 以外のオブジェクトに対するアクセス許可はリセットされません。

### <a name="what-happens-during-a-site-reset"></a>サイト リセット中の動作

サイト リセットの実行時には、以下が行われます。

1. セットアップでは、 **SMS_SITE_COMPONENT_MANAGER** サービスと、 **SMS_EXECUTIVE** サービスのスレッド コンポーネントを停止してから再起動します。

1. セットアップにより、ローカル コンピューターおよびリモート サイト システム コンピューター上にある、サイト システムの共有フォルダーと **SMS Executive** コンポーネントが、削除され、再作成されます。

1. セットアップにより **SMS_SITE_COMPONENT_MANAGER** サービスが再起動され、このサービスによって **SMS_EXECUTIVE** サービスと **SMS_SQL_MONITOR** サービスがインストールされます。

サイト リセットでは、以下のオブジェクトが復元されます。

- **SMS** または **NAL** のレジストリ キー、またはこれらのキーの既定のサブキー。

- Configuration Manager ファイル ディレクトリ ツリー、およびこのファイル ディレクトリ ツリー内の既定のファイルまたはサブディレクトリ。

### <a name="prerequisites-for-site-reset"></a>サイト リセットの前提条件

サイトをリセットするのに使用するアカウントには、以下のアクセス許可が必要です。

- CAS をリセットするには:

  - CAS サーバーのローカル**管理者**

  - **完全な権限を持つ管理者**のロール ベース管理のセキュリティ ロールと同等の特権

- プライマリ サイトをリセットするには:

  - プライマリ サイト サーバーのローカル**管理者**

  - **完全な権限を持つ管理者**のロール ベース管理のセキュリティ ロールと同等の特権
  
  - CAS がある階層内にプライマリ サイトがある場合、このアカウントも、CAS サーバーのローカル**管理者**である必要があります。

### <a name="limitations-for-a-site-reset"></a>サイト リセットに関する制限事項

[運用前コレクションでのクライアント アップグレードのテスト](../../clients/manage/upgrade/test-client-upgrades.md)をサポートするように階層が構成されている場合、サイト リセットを使用して、サイトのサーバーまたはクライアント言語パックを変更することはできません。

### <a name="run-a-site-reset"></a>サイト リセットの実行

1. 以下のいずれかの方法を使用して、サイト サーバーで Configuration Manager のセットアップを開始します。

    - **[開始]** メニューで、 **[Configuration Manager のセットアップ]** を選択します。

    - Configuration Manager の*インストール メディア*のディレクトリで、`\SMSSETUP\BIN\X64\setup.exe` を開きます。 このバージョンがサイトのバージョンと同じであることを確認します。

    - Configuration Manager が*インストールされている*ディレクトリで、`\BIN\X64\setup.exe` を開きます。

1. **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** を選択します。

1. **[サイトのメンテナンス]** ページで、 **[構成を変更せずにサイトをリセットする]** を選択します。

1. **[はい]** を選択してサイト リセットを開始します。

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a> サイトの言語パックを管理する

サイトをインストールした後、使用中のサーバーおよびクライアントの言語パックを変更することができます。

### <a name="server-language-packs"></a>サーバー言語パック

*適用対象:Configuration Manager コンソールのインストール、適用可能なサイト システムの役割の新規インストール*

サイトのサーバー言語パックを更新した後は、言語パックのサポートを Configuration Manager コンソールに追加できます。

サーバー言語パックのサポートを Configuration Manager コンソールに追加するには、サイト サーバー上にある、使用する言語パックが含まれる **ConsoleSetup** フォルダーから Configuration Manager コンソールをインストールします。 Configuration Manager コンソールが既にインストールされている場合、新しいインストールを有効にしてサポートされる言語パックの最新の一覧を特定するには、まず既存のコンソールをアンインストールする必要があります。

### <a name="client-language-packs"></a>クライアント言語パック

クライアント言語パックを変更すると、クライアント インストール ソース ファイルが更新されます。 新しいクライアントのインストールとアップグレードでは、クライアント言語の更新された一覧のサポートが追加されます。

サイトのクライアント言語パックを更新したら、クライアント言語パックが含まれるソース ファイルを使用して、言語パックを使用する各クライアントをインストールします。

Configuration Manager でサポートされているクライアントとサーバーの言語の詳細については、[言語パック](../deploy/install/language-packs.md)に関するページを参照してください。

### <a name="modify-the-supported-language-packs-at-a-site"></a>サイトでサポートされる言語パックを変更する

1. 以下のいずれかの方法を使用して、サイト サーバーで Configuration Manager のセットアップを開始します。

    - **[開始]** メニューで、 **[Configuration Manager のセットアップ]** を選択します。

    - Configuration Manager の*インストール メディア*のディレクトリで、`\SMSSETUP\BIN\X64\setup.exe` を開きます。 このバージョンがサイトのバージョンと同じであることを確認します。

    - Configuration Manager が*インストールされている*ディレクトリで、`\BIN\X64\setup.exe` を開きます。

1. **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** を選択します。

1. **[サイトのメンテナンス]** ページで、 **[言語構成を変更する]** を選択します。

1. **[必須ファイルのダウンロード]** ページで、次のいずれかのオプションを選択します。

    - **必須ファイルをダウンロードする**:言語パックに対する更新プログラムを取得します。

    - **ダウンロード済みのファイルを使用する**:サイトに追加する言語パックが含まれる、以前にダウンロードしたファイルを使用します。

1. **[サーバーの言語の選択]** ページで、このサイトでサポートされるサーバー言語を選択します。

1. **[クライアント言語の選択]** ページで、このサイトでサポートされるクライアント言語を選択します。

1. ウィザードを完了し、サイトの言語サポートを変更します。

    > [!NOTE]
    > Configuration Manager でサイトのリセットが開始され、サイトのすべてのサイト システムの役割も再インストールされます。

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a> データベース サーバーのアラートしきい値を変更する

Configuration Manager では、既定で、サイト データベース サーバーの空きディスク領域が少ないとアラートが生成されます。

- 空きディスク領域が 10 GB 以下の場合に警告を生成する
- 空きディスク領域が 5 GB 以下の場合に重大なアラートを生成する

サイトごとに、これらの値を変更したり、アラートを無効にしたりすることができます。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。

1. 構成するサイトを選択します。 リボンで、 **[プロパティ]** を選択します。

1. **[アラート]** タブに切り替えてから、設定を編集します。

## <a name="uninstall-sites-and-hierarchies"></a>サイトと階層のアンインストール

Configuration Manager サイト システムの役割、サイト、または階層をアンインストールする必要が生じることがあります。 詳細については、[役割、サイト、および階層のアンインストール](../deploy/install/uninstall-sites-and-hierarchies.md)に関するページを参照してください。

バージョン 2002 以降では、階層から CAS を削除しても、プライマリ サイトを保持することもできます。 詳細については、[CAS の削除](../deploy/install/remove-central-administration-site.md)に関するページを参照してください。
