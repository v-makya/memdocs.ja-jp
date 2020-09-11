---
title: サポートされている SQL Server のバージョン
titleSuffix: Configuration Manager
description: Configuration Manager サイト データベースをホストするための SQL Server のバージョンおよび構成要件を取得します。
ms.date: 06/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5043967a640b937784c22ea2b74269a2f2043ba9
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607627"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Configuration Manager のサポートされている SQL Server バージョン

*適用対象:Configuration Manager (Current Branch)*

それぞれの Configuration Manager サイトには、サイト データベースをホストするためにサポートされている SQL Server バージョンおよび構成が必要です。  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server インスタンスと場所

### <a name="central-administration-site-and-primary-sites"></a>中央管理サイトとプライマリ サイト

サイト データベースは SQL Server のフル インストールを使用する必要があります。  

SQL Server は次の場所に配置できます。  

- サイト サーバー コンピューター。  
- サイト サーバーから離れたコンピューター。  

次のインスタンスがサポートされています。  

- SQL Server の既定のインスタンスまたは名前付きインスタンス。  
- 複数インスタンス構成。  
- SQL Server クラスター。 「[SQL Server クラスターを使用したサイト データベースのホスティング](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)」を参照してください。
- SQL Server AlwaysOn 可用性グループ。 詳しくは、「[高可用性サイト データベースの SQL Server AlwaysOn](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)」をご覧ください。

### <a name="secondary-sites"></a>セカンダリ サイト

サイト データベースは SQL Server または SQL Server Express のフル インストールの既定のインスタンスを使用できます。  

SQL Server はサイト サーバー コンピューターに配置する必要があります。  

### <a name="limitations-to-support"></a>サポートの制限事項

次の構成はサポートされていません。

- ネットワーク負荷分散 (NLB) クラスター構成の SQL Server クラスター
- クラスター共有ボリューム (CSV) 上の SQL Server クラスター
- SQL Server のデータベース ミラーリング テクノロジとピア ツー ピア レプリケーション

SQL Server のトランザクション レプリケーションは、[データベース レプリカ](../../servers/deploy/configure/database-replicas-for-management-points.md)を使用するように構成されている管理ポイントにオブジェクトをレプリケートする場合にのみサポートされます。  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> サポートされている SQL Server のバージョン

複数のサイトを含む階層では、それぞれのサイトが異なるバージョンの SQL Server を使用してサイト データベースをホストできます。 ただし、次の条件が満たされる場合です。

- Configuration Manager によってサポートされている SQL Server のバージョンを使用していること。
- 使用する SQL Server のバージョンが、Microsoft によって引き続きサポートされていること。
- SQL Server で、SQL Server の 2 つのバージョン間のレプリケーションをサポートしていること。 詳しくは、[SQL Serverレプリケーションの旧バージョンとの互換性](/sql/relational-databases/replication/replication-backward-compatibility)に関する記事をご覧ください。

SQL Server 2016 以前では、SQL の各バージョンと Service Pack は、[Microsoft ライフサイクル ポリシー](https://aka.ms/sqllifecycle)に従ってサポートされています。 特定の SQL Server Service Pack のサポートには、基本の Service Pack バージョンへの後方互換性が失われる場合を除き、累積的な更新プログラムが含まれます。 SQL Server 2017 以降では、Service Pack は[最新のサービス モデル](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)に従うようになるためリリースされません。 SQL Server チームは引き続き、利用可能になった[累積的な更新プログラムを事前にインストールする](/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism)ことをお勧めします。

特に指定のない限り、次のバージョンの SQL Server はすべてのアクティブ バージョンの Configuration Manager でサポートされます。 SQL Server の新しいバージョンのサポートが追加されている場合、そのサポートが追加される Configuration Manager のバージョンが示されます。 同様に、サポートが非推奨とされる場合は、Configuration Manager の影響を受けるバージョンの詳細を確認してください。

> [!IMPORTANT]  
> 中央管理サイトでデータベース用に SQL Server Standard を使用する場合、階層でサポートできるクライアントの合計数が制限されます。 「 [サイジングとスケールの数値](size-and-scale-numbers.md)」をご覧ください。

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019:Standard、Enterprise

Configuration Manager バージョン 1910 以降では、お使いの累積的な更新プログラムのバージョンが SQL のライフサイクルでサポートされている限り、累積的な更新プログラム 5 (CU5) 以降でこのバージョンを使用できます。 CU5 は、SQL Server 2019 の最小要件です。これによって[スカラー UDF のインライン化](/sql/relational-databases/user-defined-functions/scalar-udf-inlining)に関する問題が解決されるためです。

このバージョンの SQL は、次のサイトで使用できます。

- 中央管理サイト
- プライマリ サイト
- セカンダリ サイト

<!--
#### Known issue with SQL Server 2019

There's a known issue<!--6436234 with the new [scalar UDF inlining](/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature in SQL 2019. To work around this issue and disable UDF lining, run the following script on the SQL 2019 server:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

While not always necessary, you may need to restart the SQL server after you run this script. For more information, see [Disabling Scalar UDF Inlining without changing the compatibility level](/sql/relational-databases/user-defined-functions/scalar-udf-inlining#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

You can safely disable this SQL feature for the site database server because Configuration Manager doesn't use it.

If you don't disable scalar UDF inlining in SQL 2019, the site server will randomly fail to query the site database. For example, you'll see the following errors in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

You may see similar errors in other logs, such as **SmsAdminUI.log**.

SQL Server version 2019 logs the following error:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

You'll also see crash dumps (`.mdump` files) from SQL in its log directory, which by default is `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.
-->

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard、Enterprise

お使いの累積的な更新プログラムのバージョンが SQL のライフサイクルでサポートされている限り、[累積的な更新プログラム バージョン 2](https://support.microsoft.com/help/4052574) 以降でこのバージョンを使用できます。 このバージョンの SQL は、次のサイトで使用できます。

- 中央管理サイト  
- プライマリ サイト  
- セカンダリ サイト  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard、Enterprise  
<!--514985-->
このバージョンは、SQL のライフサイクルでサポートされている最小の Service Pack と累積的な更新プログラムで使用できます。 このバージョンの SQL は、次のサイトで使用できます。

- 中央管理サイト  
- プライマリ サイト  
- セカンダリ サイト  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: Standard、Enterprise

このバージョンは、SQL のライフサイクルでサポートされている最小の Service Pack と累積的な更新プログラムで使用できます。 このバージョンの SQL は、次のサイトで使用できます。

- 中央管理サイト  
- プライマリ サイト  
- セカンダリ サイト

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: Standard、Enterprise

このバージョンは、SQL のライフサイクルでサポートされている最小の Service Pack と累積的な更新プログラムで使用できます。 このバージョンの SQL は、次のサイトで使用できます。

- 中央管理サイト  
- プライマリ サイト  
- セカンダリ サイト  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

お使いの累積的な更新プログラムのバージョンが SQL のライフサイクルでサポートされている限り、[累積的な更新プログラム バージョン 2](https://support.microsoft.com/help/4052574) 以降でこのバージョンを使用できます。 このバージョンの SQL は、次のサイトで使用できます。

- セカンダリ サイト
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

このバージョンは、SQL のライフサイクルでサポートされている最小の Service Pack と累積的な更新プログラムで使用できます。 このバージョンの SQL は、次のサイトで使用できます。

- セカンダリ サイト

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

このバージョンは、SQL のライフサイクルでサポートされている最小の Service Pack と累積的な更新プログラムで使用できます。 このバージョンの SQL は、次のサイトで使用できます。

- セカンダリ サイト  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

このバージョンは、SQL のライフサイクルでサポートされている最小の Service Pack と累積的な更新プログラムで使用できます。 このバージョンの SQL は、次のサイトで使用できます。

- セカンダリ サイト  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> SQL Server の必須構成

SQL Server Express など、サイト データベースに使用する SQL Server のすべてのインストールで、次の構成が必要です。 Configuration Manager が SQL Server Express をセカンダリ サイト インストールの一部としてインストールするときには、これらの構成は自動的に作成されます。  

### <a name="sql-server-architecture-version"></a>SQL Server アーキテクチャのバージョン

Configuration Manager には、サイト データベースをホストするために 64 ビット版の SQL Server が必要です。  

### <a name="database-collation"></a>データベース照合順序

各サイトで、そのサイトに使用される SQL Server のインスタンスとサイト データベースの両方が次の照合順序を使用する必要があります: **SQL_Latin1_General_CP1_CI_AS**。  

Configuration Manager は、中国の GB18030 規格についてこの照合順序に対する 2 つの例外をサポートしています。 詳細については、「[インターナショナル サポート](../hierarchy/international-support.md)」をご覧ください。  

### <a name="database-compatibility-level"></a>データベース互換性レベル

Configuration Manager では、サイト データベースの互換性レベルがご利用の Configuration Manager バージョンでサポートされている最小の SQL Server バージョン以上である必要があります。 たとえば、バージョン 1702 以降では、[データベースの互換性レベル](/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database)が 110 以上である必要があります。 <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server の機能

各サイト サーバーに必要な機能は、 **データベース エンジン サービス** 機能のみです。  

Configuration Manager データベース レプリケーションは、**SQL Server レプリケーション**機能を必要としません。 ただし、[管理ポイントのデータベース レプリカ](../../servers/deploy/configure/database-replicas-for-management-points.md)を使うときは、この SQL Server の構成が必要です。  

### <a name="windows-authentication"></a>Windows 認証

Configuration Manager は、データベースへの接続を検証するために、**Windows 認証**を必要とします。  

### <a name="sql-server-instance"></a>SQL Server インスタンス

サイトごとに専用の SQL Server のインスタンスを使用します。 インスタンスには、**名前付きインスタンス** か**既定のインスタンス**を使用できます。  

### <a name="sql-server-memory"></a>SQL Server のメモリ

SQL Server Management Studio を使用して SQL Server のメモリを予約します。 **[サーバー メモリ オプション]** の下の **[最小サーバー メモリ]** を設定します。 この設定を構成する方法について詳しくは、[SQL Server メモリに関するサーバー構成オプション](/sql/database-engine/configure-windows/server-memory-server-configuration-options)に関するページをご覧ください。  

- **データベース サーバーをサイト サーバーと同じコンピューターにインストールする場合**: SQL Server 用のメモリをアドレス指定可能なシステム メモリの 50% から 80% に制限します。  

- **サイト サーバーからリモートにある専用データベース サーバーの場合**: SQL Server 用のメモリをアドレス指定可能なシステム メモリの 80% から 90% に制限します。  

- **使用中の各 SQL Server インスタンスのバッファー プール用のメモリ予約の場合**:  

  - 中央管理サイトの場合: 8 GB 以上に設定します。  
  - プライマリ サイトの場合: 8 GB 以上に設定します。  
  - セカンダリ サイトの場合: 4 GB 以上に設定します。  

### <a name="sql-nested-triggers"></a>SQL の入れ子になったトリガー

SQL の入れ子になったトリガーを有効にする必要があります。 詳細については、「[nested triggers サーバー構成オプションの構成](/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)」をご覧ください。

### <a name="sql-server-clr-integration"></a>SQL Server の CLR 統合

サイト データベースには、SQL Server 共通言語ランタイム (CLR) を有効にする必要があります。 このオプションは、Configuration Manager のインストール時に自動的に有効になります。 CLR の詳細については、「[SQL Server の CLR 統合の概要](/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)」をご覧ください。  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

SQL Server Service Broker は、サイト間レプリケーションと単一のプライマリ サイトの両方に必要です。

### <a name="trustworthy-setting"></a>TRUSTWORTHY 設定

Configuration Manager により、SQL [TRUSTWORTHY データベース プロパティ](/sql/relational-databases/security/trustworthy-database-property)が自動的に有効になります。 このプロパティは、Configuration Manager が**オン**になっている場合に必要です。

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> SQL Server のオプション構成

以下の構成は、SQL Server の完全インストールを使用する各データベースのオプションです。  

### <a name="sql-server-service"></a>SQL Server サービス

SQL Server サービスを、以下のものを使用して実行するように構成できます。  

- *権限の低いドメイン ユーザー* アカウント:  

  - この構成はベスト プラクティスであり、アカウントのサービス プリンシパル名 (SPN) を手動で登録しなければならない場合があります。  

- SQL Server を実行しているコンピューターの**ローカル システム** アカウント:  

  - ローカル システム アカウントを使用すると、構成プロセスが簡単になります。  
  - ローカル システム アカウントを使用すると、Configuration Manager によって自動的に SQL Server サービスの SPN が登録されます。  
  - SQL Server サービスにローカル システム アカウントを使用することは、SQL Server のベスト プラクティスではありません。  

SQL Server を実行するコンピューターが、ローカル システム アカウントを使用して SQL Server サービスを実行していない場合、SQL Server サービスを実行するアカウントの SPN を Active Directory Domain Services で構成します。 (システム アカウントを使用する場合、SPN が自動的に登録されます)。

サイト データベースの SPN について詳しくは、「[サイト データベース サーバーの SPN の管理](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN)」をご覧ください。  

SQL Server サービスで使用されるアカウントを変更する方法について詳しくは、「[SCM サービス - サービス開始アカウントを変更する](/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account)」をご覧ください。  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

レポートを実行できるようにするレポート サービス ポイントをインストールするには、SQL Server Reporting Services が必要です。 Configuration Manager では、レポート用に、サイト データベースの場合と同じバージョンの SQL Server がサポートされています。

詳細については、「[Configuration Manager のレポートの前提条件](../../servers/manage/prerequisites-for-reporting.md)」をご覧ください。

> [!IMPORTANT]  
> 以前のバージョンから SQL Server をアップグレードした後に、次のエラーが表示されることがあります:*Report Builder Does Not Exist* (レポート ビルダーが存在しません)。  
> このエラーを解決するには、レポート サービス ポイント サイト システムの役割を再インストールする必要があります。  

### <a name="data-warehouse-service-point"></a>データ ウェアハウス サービス ポイント

データ ウェアハウスでは、個別のデータベースが使用されます。 これは、サイト データベース サーバーで、または別の SQL Server でホストすることができます。 詳細については、「[Configuration Manager のデータ ウェアハウス サービス ポイント](../../servers/manage/data-warehouse.md)」をご覧ください。

### <a name="sql-server-ports"></a>SQL Server のポート

SQL Server データベース エンジンとの通信、およびサイト間のレプリケーションには、SQL Server の既定ポート構成を使用することも、カスタム ポートを指定することもできます。  

- **サイト間の通信** には SQL Server Service Broker が使用され、既定ではポート TCP 4022 が使用されます。  
- SQL Server データベース エンジンとさまざまな Configuration Manager サイト システムの役割の間の**サイト内通信**では、既定でポート TCP 1433 が使用されます。 次のサイト システムの役割は、SQL Server データベースと直接通信します。  

  - 管理ポイント  
  - SMS プロバイダー コンピューター  
  - レポート サービス ポイント  
  - サイト サーバー  

SQL Server を実行しているコンピューターが複数のサイトからデータベースをホストする場合、各データベースは個別の SQL Server インスタンスを使用する必要があります。 さらに、各インスタンスは一意のポート セットを使用するように構成されている必要があります。  

> [!WARNING]  
> Configuration Manager は、動的ポートをサポートしていません。 SQL Server 名前付きインスタンスの既定動作では、データベース エンジンへの接続に動的ポートが使用されるため、名前付きインスタンスの使用時に、サイト内通信に使用する静的ポートを手動で構成する必要があります。  

SQL Server を実行しているコンピューターのファイアウォールが有効に設定されている場合は、展開で使用されているポートと、SQL Server と通信するコンピューター間のネットワーク上のあらゆる場所にあるポートを許可するように構成してください。  

特定のポートを使用する SQL Server を構成する方法の例については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)」をご覧ください。  

## <a name="upgrade-options-for-sql-server"></a>SQL Server のアップグレード オプション

使用している SQL Server のバージョンをアップグレードする必要がある場合は、次の方法のいずれかを使用します (簡単な方法から順に示されています)。  

- [SQL Server をインプレースでアップグレードします](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (推奨)  

- 新しいコンピューターに新しいバージョンの SQL Server をインストールしてから、Configuration Manager セットアップの[データベースの移動オプションを使用](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig)して、サイト サーバーを新しい SQL Server にポイントします  

- [バックアップと回復](../../servers/manage/backup-and-recovery.md)を使用します。 SQL アップグレード シナリオに対するバックアップと回復の使用がサポートされています。 「[サイトを回復する前の注意事項](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site)」を確認するとき、SQL のバージョンの要件は無視してかまいません。