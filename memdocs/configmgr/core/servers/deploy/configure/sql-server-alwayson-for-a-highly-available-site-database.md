---
title: SQL Server AlwaysOn
titleSuffix: Configuration Manager
description: Configuration Manager で SQL Server Always On 可用性グループの使用を計画します
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eef375cad028a6903a0fa28d1cc3f7562bcebf6f
ms.sourcegitcommit: 2339c927b6576db8878f34f167a9a45c5dc9f58d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90689414"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Configuration Manager で SQL Server Always On 可用性グループを使用するための準備

*適用対象:Configuration Manager (Current Branch)*

この記事では、SQL Server Always On 可用性グループを使用するように Configuration Manager を準備します。 この機能では、サイト データベースに対して高可用性とディザスター リカバリー ソリューションが提供されます。  

Configuration Manager では、次の場所での可用性グループの使用がサポートされます。

- プライマリ サイトと中央管理サイト。
- オンプレミス、または Microsoft Azure。

Microsoft Azure で可用性グループを使用する場合は、*Azure 可用性セット*を使用することで、サイト データベースの可用性をさらに向上できます。 Azure 可用性セットの詳細については、「 [仮想マシンの可用性管理](/azure/virtual-machines/windows/manage-availability)」を参照してください。

> [!Important]
> 作業を続行する前に、SQL Server と SQL Server 可用性グループの構成に慣れておいてください。 以下の情報では、SQL Server ドキュメント ライブラリと手順を示します。


## <a name="supported-scenarios"></a>サポートされるシナリオ

Configuration Manager で可用性グループを使用する場合にサポートされるシナリオを以下に示します。 各シナリオの詳細と手順については、「[Configuration Manager の SQL Server Always On 可用性グループを構成する](configure-aoag.md)」をご覧ください。

- [Configuration Manager で使用する可用性グループを作成する](configure-aoag.md#bkmk_create)  
- [可用性グループを使用するようにサイトを構成する](configure-aoag.md#bkmk_configure)  
- [サイト データベースをホストする可用性グループで同期レプリカ メンバーを追加または削除する](configure-aoag.md#bkmk_sync)  
- [非同期コミット レプリカからサイトを構成または復旧する](configure-aoag.md#bkmk_async)  
- [サイト データベースを、可用性グループから、スタンドアロン SQL Server の指定したインスタンスまたは既定のインスタンスに移動する](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>[前提条件]

すべてのシナリオに以下の必要条件が適用されます。 追加の必要条件が特定のシナリオに適用される場合は、そのシナリオで詳しく説明します。

### <a name="configuration-manager-accounts-and-permissions"></a>Configuration Manager のアカウントとアクセス許可

#### <a name="installation-account"></a>インストール アカウント

Configuration Manager セットアップの実行に使用するアカウントは、次のものである必要があります。

- 可用性グループのメンバーである各コンピューターのローカル**管理者**グループのメンバー。
- サイト データベースをホストする各 SQL Server インスタンスの **sysadmin**。

#### <a name="site-server-to-replica-member-access"></a>サイト サーバーからレプリカ メンバーへのアクセス

サイト サーバーのコンピューター アカウントは、可用性グループのメンバーである各コンピューターのローカル**管理者**グループのメンバーである必要があります。

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>バージョン

可用性グループの各レプリカは、使用しているバージョンの Configuration Manager でサポートされるバージョンの SQL Server を実行する必要があります。 SQL Server でサポートされる場合、可用性グループの別々のノードで、異なるバージョンの SQL Server を実行できます。 詳細については、「[Configuration Manager のサポートされている SQL Server バージョン](../../../plan-design/configs/support-for-sql-server-versions.md)」を参照してください。<!--SCCMDocs issue 656-->

#### <a name="edition"></a>エディション

SQL Server の *Enterprise* エディションを使用します。

#### <a name="account"></a>アカウント

SQL Server の各インスタンスは、ドメイン ユーザー アカウント (**サービス アカウント**) またはドメイン以外のアカウントで実行できます。 グループ内の各レプリカは別の構成を持つことができます。

- できるだけアクセス許可が制限されたアカウントを使用します。 詳しくは、「[SQL Server インストールにおけるセキュリティの考慮事項](/sql/sql-server/install/security-considerations-for-a-sql-server-installation)」をご覧ください。  

- SQL Server 用のサービス アカウントとアクセス許可の構成について詳しくは、「[Windows サービス アカウントと権限の構成](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions)」をご覧ください。  

- ドメイン以外のアカウントを使用するには、証明書を使用する必要があります。 詳しくは、「[データベース ミラーリング エンドポイントでの証明書の使用 (Transact-SQL)](/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql)」をご覧ください。  

- 詳しくは、[Always On 可用性グループのデータベース ミラーリング エンドポイントの作成](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell)に関するページを参照してください。  


### <a name="database"></a>データベース

#### <a name="configure-the-database-on-a-new-replica"></a>新しいレプリカでデータベースを構成する

各レプリカのデータベースを次の設定のように構成します。  

- **CLR 統合**を有効にします。

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    詳しくは、「[CLR integration](/sql/relational-databases/clr-integration/clr-integration-enabling)」(CLR の統合) をご覧ください。  

- **テキスト レプリケーションの最大サイズ**を `2147483647` に設定します。  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- データベース所有者を *SA アカウント* に設定します。 このアカウントを有効にする必要はありません。

- **TRUSTWORTHY** の設定を **ON** にします。

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    詳しくは、「[TRUSTWORTHY データベース プロパティ](/sql/relational-databases/security/trustworthy-database-property)」をご覧ください。

- **Service Broker** を有効にします。  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > 既に可用性グループの一部であるデータベースでは、Service Broker オプションを有効にすることはできません。 可用性グループに追加する前に、そのオプションを有効にする必要があります。<!-- SCCMDocs#1432 -->

- Service Broker の優先度を構成します。

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

これらの構成はライマリ レプリカでのみ行います。 セカンダリ レプリカを構成するには、最初にプライマリをセカンダリにフェールオーバーします。 これにより、セカンダリが新しいプライマリ レプリカになります。

#### <a name="database-verification-script"></a>データベース検証スクリプト

次の SQL スクリプトを実行して、プライマリとセカンダリ両方のレプリカのデータベース構成を検証します。 セカンダリ レプリカに関する問題を修正するには、そのセカンダリ レプリカをプライマリ レプリカに変更します。

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>可用性グループの構成

#### <a name="replica-members"></a>レプリカ メンバー

- 可用性グループには、1 つのプライマリ レプリカを含める必要があります。  

- 可用性グループでは、お使いのバージョンの SQL Server でサポートされているのと同じ数と種類のレプリカを使用します。

- 同期レプリカを復旧するために非同期コミット レプリカを使用できます。 詳しくは、[サイト データベースの回復オプション](../../manage/recover-sites.md#site-database-recovery-options)に関するページをご覧ください。  

    > [!Warning]  
    > Configuration Manager では、非同期コミット レプリカをサイト データベースとして使用するための "*フェールオーバー*" はサポートされていません。 詳しくは、「[Failover and failover modes (Always On availability groups)](/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups)」(フェールオーバーとフェールオーバー モード (AlwaysOn 可用性グループ)) をご覧ください。  

Configuration Manager では、最新であることを確認するための非同期コミット レプリカの状態の検証は行われません。 非同期コミット レプリカをサイト データベースとして使用すると、サイトとデータの整合性が危険にさらされる場合があります。 設計上、このレプリカは同期しなくなる可能性があります。 詳しくは、[SQL Server Always On 可用性グループの概要](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)に関するページを参照してください。

各レプリカ メンバーは次のように構成されている必要があります。

- "*既定のインスタンス*" または "*名前付きインスタンス*" を使用します  

- **[プライマリ ロールでの接続]** 設定は **[すべての接続を許可]** です  

- **[読み取り可能なセカンダリ]** の設定は **[はい]** です  

- **[手動フェールオーバー]** を有効にします

    > [!Note]
    > バージョン 1902 以前では、手動フェールオーバー用に SQL Server ですべての可用性グループを構成する必要があります。 この構成は、サイト データベースをホストしていない場合でも必要です。
    >
    > バージョン 1906 以降では、 **[自動フェールオーバー]** に設定されている場合、Configuration Manager で可用性グループ同期レプリカの使用がサポートされます。 次のときは**手動フェールオーバー**を設定します。
    >
    > - Configuration Manager のセットアップを実行して、可用性グループでのサイト データベースの使用を指定する。  
    > - Configuration Manager にすべての更新プログラムをインストールする (サイト データベースに適用される更新プログラムだけでなく)。  

- すべてのメンバーが同じ[シード処理モード](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)を必要とします。<!-- SCCMDocs-pr#3899 --> Configuration Manager セットアップには、インストールまたは復元を使用してデータベースを作成するときにこの構成を検証するための前提条件の確認が含まれます。

    > [!Note]  
    > セットアップでデータベースを作成し、**自動**シード処理を構成する場合は、可用性グループにデータベースを作成する権限が必要です。 この要件は、新しいデータベースと回復の両方に適用されます。 詳細については、「[セカンダリ レプリカの自動シード処理](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security)」を参照してください。<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>レプリカ メンバーの場所

すべてのレプリカを、オンプレミスまたは Microsoft Azure どちらかの可用性グループでホストします。 オンプレミス メンバーと Azure のメンバーを 1 つのグループに含めることはサポートされていません。

> [!NOTE]
> SQL Server に Azure 仮想マシンを使用している場合は、**floating IP** を有効にします。 詳細については、「[Azure Virtual Machines に SQL Server Always On 可用性グループのロード バランサーを構成する](/azure/azure-sql/virtual-machines/windows/availability-group-load-balancer-portal-configure)」を参照してください。<!-- SCCMDocs#1928 -->

Configuration Manager セットアップでは、各レプリカに接続する必要があります。 Azure で可用性グループをセットアップし、グループが内部または外部ロード バランサーの背後にある場合、次の既定ポートを開きます。

- RPC エンドポイント マッパー:**TCP 135**

- SQL Server Service Broker:**TCP 4022**  

- SQL over TCP:**TCP 1433**

セットアップの完了後も、これらのポートを Configuration Manager とレプリケーション リンク アナライザー用に開けておく必要があります。<!-- MEMDocs#375 -->

これらの構成ではカスタム ポートを使用することができます。 エンドポイントと、可用性グループ内のすべてのレプリカで、同じカスタム ポートを使用します。

SQL によってデータをサイト間でレプリケートするには、Azure ロード バランサーのポートごとに負荷分散規則を作成します。 詳細については、「[内部ロード バランサー用の高可用性ポートの構成](/azure/load-balancer/load-balancer-configure-ha-ports)」を参照してください。<!-- MEMDocs#252 -->

#### <a name="listener"></a>リスナー

可用性グループには、少なくとも 1 つの *可用性グループ リスナー*が必要です。 可用性グループのサイト データベースを使用するように Configuration Manager を構成するときは、このリスナーの仮想名が使用されます。 可用性グループに複数のリスナーを含めることはできますが、Configuration Manager で使用できるのは 1 つだけです。 詳しくは、「[可用性グループ リスナーの作成または構成 (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server)」をご覧ください。

#### <a name="file-paths"></a>ファイル パス

可用性グループ内のデータベースを使用するようにサイトを構成するために Configuration Manager セットアップを実行するときには、各セカンダリ レプリカ サーバーに、現在のプライマリ レプリカ上のサイト データベース ファイルのファイル パスと同じ SQL Server ファイル パスが存在する必要があります。 同じパスが存在しない場合、セットアップでは、サイト データベースの新しい場所として可用性グループのインスタンスを追加できません。  

ローカル SQL Server サービス アカウントは、このフォルダーに対する**フル コントロール** アクセス許可を持っている必要があります。

Configuration Manager のセットアップを使用して可用性グループのデータベース インスタンスを指定するときに、セカンダリ レプリカ サーバーではこのファイルのパスのみが必要です。 可用性グループのサイト データベースの構成が完了したら、セカンダリ レプリカ サーバーから未使用のパスを削除できます。

たとえば、次の場合を考えてください。

- 3 つの SQL Server を使用する可用性グループを作成するとします。  

- プライマリ レプリカ サーバーは、SQL Server 2014 の新規インストールです。 既定では、データベースの .MDF および .LDF ファイルが `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` に格納されます。  

- 両方のセカンダリ レプリカ サーバーを以前のバージョンから SQL Server 2014 にアップグレードしました。 アップグレードでは、これらのサーバーはデータベース ファイルを格納するための元のファイル パス `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA` を保持します。  

- サイト データベースをこの可用性グループに移動する前に、各セカンダリ レプリカ サーバーで、ファイル パス `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` を作成します。 このパスはプライマリ レプリカで使用されているパスの複製であり、セカンダリ レプリカがこのファイルの場所を使用しない場合でも作成します。  

- 次に、各セカンダリ レプリカ上の SQL Server サービス アカウントに、そのサーバーの新規作成されたファイルの場所に対するフル コントロール アクセス許可を付与します。  

- この時点で Configuration Manager セットアップを正常に実行し、可用性グループ内のサイト データベースを使用するようにサイトを構成できます。  

#### <a name="multi-subnet-failover"></a>マルチサブネット フェールオーバー

<!-- SCCMDocs-pr#3734 -->
バージョン 1906 以降では、SQL Server で [MultiSubnetFailover 接続文字列キーワード](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover)を有効にすることができます。 また、サイト サーバーの Windows レジストリに次の値を手動で追加する必要もあります。

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> [サイト サーバーの高可用性](site-server-high-availability.md)と SQL Server Always On をマルチサブネット フェールオーバーと共に使用しても、ディザスター リカバリーのシナリオでは自動フェールオーバーのすべての機能が提供されるわけではありません。

リモートの場所にあるメンバーを使用して可用性グループを作成する必要がある場合は、最も短いネットワーク待機時間に基づいて優先順位を設定します。 ネットワーク待機時間が長いと、レプリケーションが失敗する可能性があります。<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>制限事項と既知の問題

すべてのシナリオに以下の制限事項が適用されます。

### <a name="unsupported-sql-server-options-and-configurations"></a>サポートされていない SQL Server のオプションと構成

- **基本的な可用性グループ**:SQL Server 2016 Standard エディションで導入された基本的な可用性グループでは、セカンダリ レプリカに対する読み取りアクセスがサポートされていません。 構成にはこのアクセスが必要です。 詳しくは、[基本的な SQL Server 可用性グループ](/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups)に関するページをご覧ください。  

- **フェールオーバー クラスター インスタンス**:フェールオーバー クラスター インスタンスは、Configuration Manager で使用するレプリカではサポートされていません。 詳しくは、「[AlwaysOn フェールオーバー クラスター インスタンス (SQL Server)](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server)」をご覧ください。  

- **MultiSubnetFailover**:バージョン 1902 以前では、Configuration Manager でマルチサブネット構成の可用性グループを使用することはサポートされていません。 [MutliSubnetFailover](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) キーワードを含む接続文字列も使用できません。

    この構成をサポートするには、Configuration Manager をバージョン 1906 以降に更新します。 詳細については、[マルチサブネット フェールオーバー](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover)の前提条件に関するページを参照してください。

### <a name="sql-servers-that-host-additional-availability-groups"></a>追加の可用性グループをホストする SQL Server

<!--SCCMDocs issue 649-->
Configuration Manager で使用する可用性グループに加え、SQL Server で 1 つ以上のグループをホストしている場合、Configuration Manager セットアップの実行時に特定の設定が必要になります。 これらの設定は、Configuration Manager に対する更新プログラムをインストールするときにも必要です。 各可用性グループ内の各レプリカでは、次の構成が必要です。

- 手動フェールオーバー  
- 読み取り専用接続を許可  

> [!Note]
> バージョン 1902 以前では、手動フェールオーバー用に SQL Server ですべての可用性グループを構成する必要があります。 この構成は、サイト データベースをホストしていない場合でも必要です。
>
> バージョン 1906 以降では、 **[自動フェールオーバー]** に設定されている場合、Configuration Manager で可用性グループ同期レプリカの使用がサポートされます。 次のときは**手動フェールオーバー**を設定します。
>
> - Configuration Manager のセットアップを実行して、可用性グループでのサイト データベースの使用を指定する。  
> - Configuration Manager にすべての更新プログラムをインストールする (サイト データベースに適用される更新プログラムだけでなく)。  

### <a name="unsupported-database-use"></a>サポートされていないデータベースの使用

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager で可用性グループ内のサイト データベースのみがサポートされている

次のデータベースは、SQL Server Always On 可用性グループの Configuration Manager でサポートされていません。  

- レポート データベース  
- WSUS データベース  

#### <a name="pre-existing-database"></a>既存のデータベース

レプリカで作成された新しいデータベースを使用することはできません。 可用性グループを構成するときは、既存の Configuration Manager データベースのコピーをプライマリ レプリカに復元します。  

#### <a name="distributed-views"></a>分散ビュー

<!-- SCCMDocs-pr#3792 -->
バージョン 1902 以前では、SQL Server Always On 可用性グループでサイト データベースをホストしている場合、データベース レプリケーションの[分散ビュー](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep)を有効にすることはできません。 この構成をサポートするには、バージョン 1906 以降に更新します。


### <a name="setup-errors-in-configmgrsetuplog"></a>ConfigMgrSetup.log のセットアップ エラー

Configuration Manager のセットアップを実行してサイト データベースを可用性グループに移動すると、可用性グループのセカンダリ レプリカでデータベース ロールの処理が試みられます。 **ConfigMgrSetup.log** ファイルでは次のエラーが示されます。  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

このようなエラーは無視してもかまいません。

### <a name="site-expansion"></a>サイトの拡張

<!--SCCMDocs issue 568-->
スタンドアロン プライマリ サイト用のサイト データベースを、SQL Always On を使用するように構成する場合は、中央管理サイトを含むようにサイトを拡張できません。 この処理を行おうとすると失敗します。 サイトを拡張するには、可用性グループからプライマリ サイト データベースを一時的に削除します。

セカンダリ サイトを追加するときに、構成を変更する必要はありません。


## <a name="changes-for-site-backup"></a>サイト バックアップの変更

### <a name="backup-database-files"></a>データベース ファイルのバックアップ
  
サイト データベースが可用性グループを使用しているときは、組み込み**バックアップ サイト サーバー** メンテナンス タスクを実行して、Configuration Manager の一般的な設定とファイルをバックアップします。 そのバックアップで作成された .MDF ファイルや .LDF ファイルは使用しないでください。 代わりに、SQL Server を使用して、これらのデータベース ファイルの直接バックアップを作成します。

### <a name="transaction-log"></a>トランザクション ログ  

サイト データベースの復旧モデルを**完全**に設定します。 可用性グループで Configuration Manager を使用するには、このように構成する必要があります。 サイト データベース トランザクション ログのサイズを監視および維持するための計画を立てます。 完全復旧モデルでは、データベースまたはトランザクション ログの完全バックアップが作成されるまで、トランザクションは書き込まれません。 詳しくは、「[SQL Server データベースのバックアップと復元](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases)」をご覧ください。


## <a name="changes-for-site-recovery"></a>サイトの回復の変更

可用性グループの 1 つ以上のノードがまだ機能している場合は、サイトの回復オプション **[データベースの回復をスキップする (このオプションは、サイト データベースが障害の影響を受けていない場合に選択してください)]** を使用します。

バージョン 1906 以降では、サイトの回復で SQL Always On グループにデータベースを再作成できます。 このプロセスは、手動と自動の両方のシード処理で機能します。<!-- SCCMDocs-pr#3846 -->

> [!TIP]
> セットアップまたは回復ウィザードを実行すると、 **[新しい可用性グループ データベース]** ページは手動のシード処理構成にのみ適用されます。 自動シード処理の場合、共有されるデータベース バックアップが存在しないため、ウィザードのそのページは表示されません。<!-- SCCMDocs #2242 -->

バージョン 1902 以前では、可用性グループのすべてのノードが失われた場合、サイトを回復するには、まず、可用性グループを再作成します。 Configuration Manager では可用性ノードの再構築や復元はできません。 グループを再作成し、バックアップを復元して、SQL を再構成します。 その後、サイト回復オプション **[データベースの回復をスキップする (このオプションは、サイト データベースが障害の影響を受けていない場合に選択してください)]** を使用します。

詳細については、「[バックアップと回復](../../manage/backup-and-recovery.md)」を参照してください。


## <a name="changes-for-reporting"></a>レポートの変更

### <a name="install-the-reporting-service-point"></a>レポート サービス ポイントをインストールする

レポート サービス ポイントでは、可用性グループのリスナー仮想名の使用はサポートされていません。 また、SQL Server Always On 可用性グループでのデータベースのホストもサポートされていません。  

- 既定では、レポート サービス ポイントのインストールで **[サイト データベース サーバー名]** がリスナーとして指定されている仮想名に設定されます。 この設定を変更し、可用性グループ内のレプリカのコンピューター名とインスタンスを指定します。  

- レポート作成の負荷を軽減し、レプリカ ノードがオフラインのときの可用性を向上させるには、各レプリカ ノードで追加のレポート サービス ポイントをインストールすることを検討します。 独自のコンピューター名を使用するように、各レポート サービス ポイントを構成します。 可用性グループの各レプリカでレポート サービス ポイントをインストールする場合、レポート作成時にアクティブなレポート ポイント サーバーにいつでも接続できます。  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>コンソールで使用されるレポート サービス ポイントを切り替える

1. Configuration Manager コンソールで、 **[監視]** ワークスペースに移動して、 **[レポート]** を展開し、 **[レポート]** ノードを選択します。

1. リボンで、 **[レポート オプション]** を選択します。  

1. [レポート オプション] ダイアログ ボックスで、使用するレポート サービス ポイントを選択します。  


## <a name="next-steps"></a>次のステップ

この記事では、可用性グループを使用するときに Configuration Manager で必要な一般的なタスクに関する前提条件、制限事項、および変更について説明します。 可用性グループを使用するようにサイトを設定および構成する手順については、「[可用性グループを構成する](configure-aoag.md)」をご覧ください。