---
title: 前提条件の確認
titleSuffix: Configuration Manager
description: Configuration Manager の更新プログラムに関する特定の前提条件の確認のリファレンス。
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5bdf2adbf4ba5f02869ba5058da84ee7738e0ce2
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608080"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Configuration Manager の前提条件の確認の一覧

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager のインストール時または更新時に行われる前提条件の確認について詳しく説明します。 詳細については、[前提条件チェッカー](prerequisite-checker.md)に関するページを参照してください。  



## <a name="errors"></a>エラー

### <a name="active-migration-mappings-on-the-target-primary-site"></a>ターゲット プライマリ サイトにアクティブな移行へのマッピング

*適用対象:中央管理サイト*

プライマリ サイトにアクティブな移行へのマッピングがありません。

### <a name="active-replica-mp"></a>アクティブなレプリカ MP

*適用対象:プライマリ サイト*

アクティブな管理ポイントのレプリカがあります。

### <a name="administrative-rights-on-expand-primary-site"></a>展開プライマリ サイトの管理者権限

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、セットアップを実行するユーザー アカウントに、スタンドアロン プライマリ サイト サーバーに対する**管理者**権限があります。

### <a name="administrative-rights-on-site-system"></a>サイト システムの管理者権限

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

Configuration Manager セットアップを実行するユーザー アカウントに、サイト サーバーに対する**管理者**権限があります。

### <a name="administrator-rights-on-central-administration-site"></a>中央管理サイトの管理者権限

*適用対象:プライマリ サイト*

Configuration Manager セットアップを実行するユーザー アカウントに、中央管理サイト サーバーに対する**管理者**権限があります。

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>展開プライマリ サイトの資産インテリジェンス同期ポイント

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、スタンドアロン プライマリ サイトで資産インテリジェンス同期ポイントの役割がインストールされていません。

### <a name="bits-enabled"></a>BITS 対応

*適用対象:管理ポイント*

管理ポイントにバックグラウンド インテリジェント転送サービス (BITS) がインストールされています。 次のいずれかの理由で、この確認が失敗する場合があります。

- BITS がインストールされていない  

- IIS 7.0 用の IIS 6.0 WMI 互換性コンポーネントが、サーバーまたはリモート IIS ホストにインストールされていない  

- セットアップでリモート IIS 設定を確認できなかった。 IIS の共通コンポーネントがサイト サーバーにインストールされていない。  

### <a name="case-insensitive-collation-on-sql-server"></a>SQL Server の照合順序の大文字と小文字の区別

*適用対象:サイト データベース サーバー*

SQL Server のインストールで、**SQL_Latin1_General_CP1_CI_AS** などの大文字と小文字が区別されない照合順序が使用されています。

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>展開プライマリ サイトに対する中央管理サイト サーバーの管理者権限

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、中央管理サイト サーバーのコンピューター アカウントに、スタンドアロン プライマリ サイト サーバーに対する**管理者**権限があります。

### <a name="client-version-on-management-point-computer"></a>管理ポイント コンピューター上のクライアントのバージョン

*適用対象:管理ポイント*

別のバージョンの Configuration Manager クライアントがインストールされていないサーバーに、管理ポイントをインストールします。

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>展開プライマリ サイトのクラウド管理ゲートウェイ

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開するときに、スタンドアロン プライマリ サイトにクラウド管理ゲートウェイの役割がインストールされていません。

### <a name="connection-to-sql-server-on-central-administration-site"></a>中央管理サイトの SQL Server への接続

*適用対象:プライマリ サイト*

既存の階層に含めるプライマリ サイトで Configuration Manager セットアップを実行するユーザー アカウントに、中央管理サイトの SQL Server インスタンスに対する **sysadmin** の役割があります。

### <a name="custom-client-agent-settings-have-nap-enabled"></a>NAP が有効になっているカスタムのクライアント エージェント設定

*適用対象:中央管理サイト、プライマリ サイト*

ネットワーク アクセス保護 (NAP) を有効にするカスタム クライアント設定がありません。

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>展開プライマリ サイトのデータ ウェアハウス サービス ポイント

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開するときに、スタンドアロン プライマリ サイトにデータ ウェアハウス サービス ポイントの役割がインストールされていません。

### <a name="dedicated-sql-server-instance"></a>専用の SQL Server インスタンス

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

Configuration Manager サイト データベースをホストするように SQL Server の専用インスタンスを構成しています。

別のサイトでインスタンスを使用する場合は、新しいサイト用に別のインスタンスを選択する必要があります。 別のサイトをアンインストールすることも、そのデータベースを SQL Server の別のインスタンスに移動することもできます。

### <a name="default-client-agent-settings-have-nap-enabled"></a>NAP が有効になっている既定のクライアント エージェント設定

*適用対象:中央管理サイト、プライマリ サイト*

既定のクライアント設定では、ネットワーク アクセス保護 (NAP) は有効にされません。

### <a name="domain-membership-error"></a>ドメインのメンバーシップ (エラー)

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、SMS プロバイダー、SQL Server*

Configuration Manager コンピューターが Windows ドメインのメンバーです。

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>展開プライマリ サイトの Endpoint Protection ポイント

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、スタンドアロン プライマリ サイトに Endpoint Protection ポイントの役割がインストールされていません。

### <a name="existing-configuration-manager-server-components-on-server"></a>サーバー上の既存の Configuration Manager サーバー コンポーネント

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイトのインストール用に選択されたサーバーに、サイト サーバーやサイト システムの役割がまだインストールされていません。

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>既存のスタンドアロン プライマリ サイトのバージョンとサイト コード

*適用対象:中央管理サイト、プライマリ サイト*

展開を計画しているプライマリ サイトがスタンドアロン プライマリ サイトです。 Configuration Manager のバージョンは同じですが、サイト コードがインストールする中央管理サイトとは異なっています。

### <a name="firewall-exception-for-sql-server"></a>SQL Server 用のファイアウォールの例外

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、管理ポイント*

Windows ファイアウォールが無効になっている、または適切な Windows ファイアウォールの例外が SQL Server に対して存在します。

Sqlservr.exe または必要な TCP ポートへのリモート アクセスを許可します。 既定では、SQL Server は TCP ポート 1433 でリッスンし、SQL Server Service Broker (SSB) は TCP ポート 4022 を使用します。

### <a name="free-disk-space-on-site-server"></a>サイト サーバーの空きディスク領域

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイト サーバーをインストールするには、少なくとも 15 GB の空きディスク領域が必要です。 同じサーバー上に SMS プロバイダーをインストールする場合は、さらに 1 GB の空き領域が必要です。

### <a name="iis-service-running"></a>IIS サービス実行中

*適用対象:管理ポイント、配布ポイント*

管理ポイントまたは配布ポイント用のサーバーに IIS がインストールされ、実行されています。

### <a name="incompatible-collection-references"></a>互換性のないコレクション参照

*適用対象:中央管理サイト*

アップグレード中に、コレクションで同じ種類の他のコレクションのみが参照されます。

### <a name="match-collation-of-expand-primary-site"></a>展開プライマリ サイトの照合順序の一致

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、スタンドアロン プライマリ サイトのサイト データベースの照合順序が、中央管理サイトのサイト データベースと同じになっています。

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性グループのテキスト レプリケーションの最大サイズ

*適用対象:サイト データベース サーバー*

SQL Server Always On を使用している場合、**テキスト レプリケーションの最大サイズ**設定を適切に構成する必要があります。 詳細については、「[Configuration Manager で SQL Server Always On 可用性グループを使用するための準備](../configure/sql-server-alwayson-for-a-highly-available-site-database.md)」を参照してください。

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>展開プライマリ サイトの Microsoft Intune コネクタ

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、スタンドアロン プライマリ サイトに Microsoft Intune コネクタの役割がインストールされていません。

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>登録されている Microsoft Remote Differential Compression (RDC) ライブラリ

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

RDC ライブラリが、Configuration Manager サイト サーバーに登録されています。

### <a name="microsoft-windows-installer"></a>Microsoft Windows インストーラー

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

Windows インストーラーのバージョンを確認します。

この確認が失敗した場合、セットアップでバージョンを確認できなかったか、インストールされたバージョンが Windows インストーラーの最小要件である 4.5 を満たしていません。

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Configuration Manager コンソールに最低限必要な .NET Framework のバージョン

*適用対象:Configuration Manager コンソール*

Microsoft .NET Framework 4.0 が Configuration Manager コンソール コンピューターにインストールされています。

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Configuration Manager サイト サーバーに最低限必要な .NET Framework のバージョン

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

Configuration Manager サイト サーバーで .NET Framework 3.5 がインストールされているか、有効になっています。

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Configuration Manager セカンダリ サイト用 SQL Server Express エディションのインストールに最低限必要な .NET Framework のバージョン

*適用対象:セカンダリ サイト*

Configuration Manager セカンダリ サイト サーバーで .NET Framework 4.0 がインストールされているか、有効になっています。 このバージョンは SQL Server Express で必要です。

### <a name="parent-database-collation"></a>親データベースの照合順序

*適用対象:プライマリ サイト、セカンダリ サイト*

サイト データベースの照合順序が、親サイトのデータベースの照合順序と一致しています。 階層内のすべてのサイトが同じデータベース照合順序を使用する必要があります。

### <a name="parent-site-replication-status"></a>親サイトのレプリケーション ステータス

*適用対象:中央管理サイト、プライマリ サイト*

親サイトのレプリケーション ステータスが **[レプリケーションはアクティブ]** (状態 **125**) です。

### <a name="pending-system-restart"></a>システムの再起動を保留しています

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

セットアップを実行する前に、別のプログラムでサーバーを再起動することが要求されます。

バージョン 1810 以降では、この確認で回復力が高まります。 コンピューターが再起動の保留状態であるかどうかを確かめるために、次のレジストリの場所が確認されます。<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>プライマリ FQDN

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、サイト データベース サーバー*

コンピューターの NetBIOS 名が、完全修飾ドメイン名 (FQDN) のローカル ホスト名と一致しています。

### <a name="read-only-domain-controller"></a>読み取り専用のドメイン コントローラー

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイト データベース サーバーとセカンダリ サイト サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。

詳細については、Microsoft サポート記事の「[Problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911)」(ドメイン コントローラーに SQL Server をインストールすると問題が発生する) を参照してください。

### <a name="required-sql-server-collation"></a>SQL Server の必須の照合順序

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

SQL Server のインスタンスが、**SQL_Latin1_General_CP1_CI_AS** 照合順序を使用するように構成されています。

Configuration Manager サイト データベースが既にインストールされている場合、この確認はデータベースにも適用されます。 SQL Server インスタンスとデータベースの照合順序の変更方法の詳細については、[SQL の照合順序と Unicode サポート](/sql/relational-databases/collations/collation-and-unicode-support)に関するページを参照してください。

中国語の OS を使用しており、GB18030 のサポートが必要な場合、この確認は適用されません。 GB18030 サポートの有効化の詳細については、「[International support](../../../plan-design/hierarchy/international-support.md)」(インターナショナル サポート) を参照してください。

### <a name="server-service-is-running"></a>サーバー サービスが実行されている

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サーバー サービスが開始され、実行されています。

### <a name="setup-source-folder"></a>セットアップ ソース フォルダー

*適用対象:セカンダリ サイト*

セカンダリ サイトのコンピューター アカウントに、セットアップ ソース フォルダーおよび共有に対する次のアクセス許可があります。

- NTFS ファイル システムの**読み取り**アクセス許可  

- 共有の**読み取り**アクセス許可  

> [!Note]  
> 管理用共有 (C$ や D$ など) を使用する場合、セカンダリ サイトのコンピューター アカウントはサーバーの**管理者**でなければなりません。  

### <a name="setup-source-version"></a>セットアップ ソースのバージョン

*適用対象:セカンダリ サイト*

セカンダリ サイトのインストール用に指定されたソース フォルダーの Configuration Manager バージョンが、プライマリ サイトの Configuration Manager バージョンに一致しています。

### <a name="site-code-in-use"></a>使用中のサイト コード

*適用対象:プライマリ サイト*

指定されたサイト コードが、Configuration Manager 階層内でまだ使用されていません。 このサイトの一意のサイト コードを指定します。

### <a name="site-server-computer-account-administrative-rights"></a>サイト サーバー コンピューター アカウントの管理者権限

*適用対象:プライマリ サイト、サイト データベース サーバー*

サイト サーバー コンピューター アカウントに、SQL サーバーと管理ポイントに対する**管理者**権限があります。

### <a name="site-server-fqdn-length"></a>サイト サーバーの FQDN の長さ

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイト サーバーの FQDN の長さ。

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>展開済みプライマリ サイト上のパッシブ モードのサイト サーバー

*適用対象:中央管理サイト*

階層にプライマリ サイトを展開するときに、スタンドアロン プライマリ サイトにパッシブ モードのサイト サーバーの役割がインストールされていません。

### <a name="sms-provider-in-same-domain-as-site-server"></a>サイト サーバーと同じドメイン内の SMS プロバイダー

*適用対象:SMS プロバイダー*

SMS プロバイダーのすべてのインスタンスが、サイト サーバーと同じドメインにあります。

### <a name="software-update-point-in-nlb-configuration"></a>NLB 構成でのソフトウェアの更新ポイント

*適用対象:ソフトウェアの更新ポイント*

サイトでアクティブなソフトウェアの更新ポイントへの仮想の場所を持つネットワーク負荷分散 (NLB) が使用されていません。

### <a name="software-update-point-using-a-load-balancer"></a>ロード バランサーを使用するソフトウェアの更新ポイント

*適用対象:ソフトウェアの更新ポイント*

Configuration Manager では、ネットワーク負荷分散 (NLB) またはハードウェア負荷分散 (HLB) でのソフトウェアの更新ポイントをサポートしていません。

### <a name="sql-server-always-on-availability-groups"></a>SQL Server の Always On 可用性グループ

*適用対象:サイト データベース サーバー*

SQL Server Always On を使用している場合、可用性グループをホストする最小要件を満たしている必要があります。 詳細については、「[Configuration Manager で SQL Server Always On 可用性グループを使用するための準備](../configure/sql-server-alwayson-for-a-highly-available-site-database.md)」を参照してください。

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>読み取り可能セカンダリが構成された SQL Server 可用性グループ

*適用対象:サイト データベース サーバー*

SQL Server Always On を使用している場合、可用性グループのレプリカのセカンダリ読み取り状態を確認します。

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>手動フェールオーバーが構成された SQL Server 可用性グループ

*適用対象:サイト データベース サーバー*

SQL Server Always On を使用している場合、可用性グループのレプリカで手動フェールオーバーが構成されます。

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>既定のインスタンス上の SQL Server 可用性グループのレプリカ

*適用対象:サイト データベース サーバー*

SQL Server Always On を使用している場合、可用性グループのレプリカは既定のインスタンスにあります。

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>SQL 可用性グループ レプリカのシード処理モードはすべて同じでなければなりません

<!-- SCCMDocs-pr#3899 -->
*適用対象:サイト データベース サーバー*

バージョン 1906 以降で SQL Server Always On を使用する場合は、同じ[シード処理モード](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)で可用性グループ レプリカを構成する必要があります。

### <a name="sql-availability-group-replicas-must-be-healthy"></a>SQL 可用性グループ レプリカが正常である必要があります

<!-- SCCMDocs-pr#3899 -->
*適用対象:サイト データベース サーバー*

バージョン 1906 以降で SQL Server Always On を使用する場合は、可用性グループのレプリカが正常な状態になります。

### <a name="sql-server-configuration-for-site-upgrade"></a>サイトのアップグレードのための SQL Server 構成

*適用対象:サイト データベース サーバー*

SQL Server はサイトのアップグレードの最小要件を満たしています。 詳細については、[サポートされている SQL Server のバージョン](../../../plan-design/configs/support-for-sql-server-versions.md)に関するページを参照してください。

### <a name="sql-server-edition"></a>SQL Server のエディション

*適用対象:サイト データベース サーバー*

サイトの SQL Server が SQL Server Express ではありません。

### <a name="sql-server-express-on-secondary-site"></a>セカンダリ サイトの SQL Server Express

*適用対象:セカンダリ サイト*

SQL Server Express をセカンダリ サイト サーバーに正常にインストールできます。

### <a name="sql-server-on-the-secondary-site-server"></a>セカンダリ サイト サーバー上の SQL Server

*適用対象:セカンダリ サイト*

SQL Server がセカンダリ サイト サーバーにインストールされています。 セカンダリ サイト用のリモート サイトに、SQL Server をインストールすることはできません。

> [!Warning]  
> この確認は、セットアップで SQL Server の既存のインスタンスを使用するように選択した場合にのみ適用されます。  

### <a name="sql-server-service-running-account"></a>SQL Server サービスの実行アカウント

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

SQL Server サービスのサインイン アカウントが、ローカル ユーザー アカウントや**ローカル サービス**ではありません。

有効なドメイン アカウント、**ネットワーク サービス**、または**ローカル システム**を使用するように SQL Server サービスを構成します。

### <a name="sql-server-site-database-consistency"></a>SQL Server サイト データベースの整合性

*適用対象:サイト データベース サーバー*

データベースの整合性を検証します。

### <a name="sql-server-sysadmin-rights"></a>SQL Server の sysadmin 権限

*適用対象:サイト データベース サーバー*

Configuration Manager セットアップを実行するユーザー アカウントに、サイト データベースのインストール用に選択した SQL Server インスタンスに対する **sysadmin** の役割があります。 この確認は、アクセス許可の確認のためにセットアップが SQL Server のインスタンスにアクセスできない場合も失敗します。

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>基準サイト用の SQL Server sysadmin 権限

*適用対象:サイト データベース サーバー*

Configuration Manager セットアップを実行するユーザー アカウントに、基準サイトのデータベースとして選択した SQL Server の役割インスタンスに対する **sysadmin** の役割があります。 SQL Server の役割アクセス許可 **sysadmin** は、サイト データベースを変更するために必要です。

### <a name="sql-server-tcp-port"></a>SQL Server の TCP ポート

*適用対象:サイト データベース サーバー*

TCP が SQL Server インスタンスに対して有効になっており、静的ポートを使用するように設定されています。

### <a name="sql-server-version"></a>SQL Server バージョン

*適用対象:サイト データベース サーバー*

指定されたサイト データベース サーバーに、サポートされているバージョンの SQL Server がインストールされています。

詳細については、「[Support for SQL Server versions](../../../plan-design/configs/support-for-sql-server-versions.md)」(SQL Server バージョンのサポート) を参照してください。

### <a name="unsupported-os-for-configuration-manager-console"></a>Configuration Manager コンソールのサポートされていない OS

*適用対象:Configuration Manager コンソール*

サポートされる OS のバージョンを実行するコンピューターに、Configuration Manager コンソールをインストールします。

詳細については、「[Supported OS versions for the Configuration Manager console](../../../plan-design/configs/supported-operating-systems-consoles.md)」 (Configuration Manager コンソールでサポートされる OS バージョン) を参照してください。

### <a name="unsupported-os-for-site-server"></a>サイト サーバーのサポートされていない OS

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、Configuration Manager コンソール、管理ポイント、配布ポイント*

サーバーで、サポートされている OS バージョンが実行されています。

詳細については、[Configuration Manager サイト システム サーバーでサポートされる OS バージョン](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)に関するページを参照してください。

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>サポートされていないサイト システムの役割: 帯域外サービス ポイント

*適用対象:プライマリ サイト*

帯域外サービス ポイントのサイト システムの役割はインストールされません。

### <a name="unsupported-site-system-role-system-health-validation-point"></a>サポートされていないサイト システムの役割: システム正常性検証ポイント

*適用対象:プライマリ サイト*

システム正常性検証ポイントのサイト システムの役割はインストールされていません。

### <a name="unsupported-upgrade-path"></a>サポートされていないアップグレードのパス

*適用対象:中央管理サイト、プライマリ サイト*

階層内のすべてのサイト サーバーが、アップグレードに必要な Configuration Manager 最小バージョンを満たしています。

### <a name="usmt-installed"></a>USMT のインストール

*適用対象:中央管理サイト、プライマリ サイト (スタンドアロンのみ)*

Windows 用 Windows アセスメント & デプロイメント キット (ADK) のユーザー状態移行ツール (USMT) コンポーネントがインストールされています。

### <a name="validate-fqdn-of-sql-server"></a>SQL Server FQDN の検証

*適用対象:サイト データベース サーバー*

SQL Server コンピューターの有効な FQDN を指定しています。

### <a name="verify-central-administration-site-version"></a>中央管理サイトのバージョンの確認

*適用対象:プライマリ サイト*

中央管理サイトの Configuration Manager のバージョンが同じです。

### <a name="verify-database-consistency"></a>データベースの整合性の検証

*適用対象:中央管理サイト、プライマリ サイト*

SQL Server でサイト データベースの整合性を検証します。  

### <a name="windows-deployment-tools-installed"></a>インストールされている Windows 展開ツール

*適用対象:SMS プロバイダー*

Windows ADK の Windows 展開ツール コンポーネントがインストールされています。

### <a name="windows-failover-cluster"></a>Windows フェールオーバー クラスター

*適用対象:サイト サーバー、管理ポイント、配布ポイント*

サイト サーバー、管理ポイント、または配布ポイントの役割を持つサーバーが、Windows クラスターの一部ではありません。

バージョン 1810 以降では、Configuration Manager セットアップ プロセスで、フェールオーバー クラスタリング用の Windows の役割でコンピューターにサイト サーバーの役割がインストールされるのがブロックされなくなりました。 SQL Always On では、このロールが必要なため、以前はサイト サーバーにサイト データベースを同時に配置できませんでした。 この変更により、SQL Always On とパッシブ モードのサイト サーバーを使用して、少ないサーバー数で高可用性サイトを作成できます。 詳細については、[高可用性オプション](../configure/high-availability-options.md)に関するページを参照してください。 <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE のインストール

*適用対象:SMS プロバイダー*

Windows ADK の Windows プレインストール環境 (PE) コンポーネントがインストールされています。



## <a name="warnings"></a>警告

### <a name="active-directory-domain-functional-level"></a>Active Directory ドメインの機能レベル

*適用対象:中央管理サイト、プライマリ サイト*

Active Directory のドメインとフォレストの機能レベルは、少なくとも Windows Server 2008 R2 です。 詳細については、「[Active Directory ドメインのサポート](../../../plan-design/configs/support-for-active-directory-domains.md)」をご覧ください。

### <a name="administrative-rights-on-distribution-point"></a>配布ポイントの管理者権限

*適用対象:配布ポイント*

セットアップを実行するユーザー アカウントに、配布ポイントに対する**管理者**権限があります。

### <a name="administrative-rights-on-management-point"></a>管理ポイントの管理者権限

*適用対象:管理ポイント、配布ポイント*

サイト サーバーのコンピューター アカウントに、管理ポイントと配布ポイントに対する**管理者**権限があります。

### <a name="administrative-share-site-system"></a>管理用共有 (サイト システム)

*適用対象:管理ポイント*

サイト システム コンピューターに必要な管理用共有があります。

### <a name="application-compatibility"></a>アプリケーションの互換性

*適用対象:中央管理サイト、プライマリ サイト*

現在のアプリケーションがアプリケーション スキーマに対応しています。

### <a name="backlogged-inboxes"></a>バックログされた受信トレイ

*適用対象:中央管理サイト、プライマリ サイト*

サイト サーバーは重要な受信トレイを指定時間内に処理しています。 受信トレイには、2 日以上経過したファイルはありません。

次の受信トレイ フォルダーが確認されます。

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

この警告を解決するには、デスプーラーとスケジューラー サイト システムのコンポーネントが実行されているかどうかを確認します。

### <a name="bits-installed"></a>BITS のインストール

*適用対象:管理ポイント*

IIS でバックグラウンド インテリジェント転送サービス (BITS) がインストールされており、有効になっています。

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>サイトで Upgrade Readiness クラウド サービス コネクタが使用されているかどうかを確認します

*適用対象:中央管理サイト、プライマリ サイト*

Upgrade Readiness サービスは、2020 年 1 月 31 日をもって廃止されています。 詳細については、[KB 4521815:Windows Analytics の廃止 (2020 年 1 月 31 日)](https://support.microsoft.com/help/4521815/windows-analytics-retirement) に関するページをご確認ください。

Desktop Analytics が Windows Analytics の進化版です。 詳細については、「[Desktop Analytics とは](../../../../desktop-analytics/overview.md)」を参照してください。

Configuration Manager サイトが Upgrade Readiness に接続されている場合は、それを削除し、クライアントを再構成する必要があります。 詳細については、「[Upgrade Readiness 接続を削除する](../../../clients/manage/upgrade-readiness.md#bkmk_remove)」を参照してください。

この前提条件の警告を無視すると、Configuration Manager セットアップによって Upgrade Readiness コネクタが自動的に削除されます。<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>クラウド管理ゲートウェイには、トークン ベース認証または HTTPS 管理ポイントのいずれかが必要です

*適用対象:クラウド管理ゲートウェイ*

Configuration Manager の一部のバージョンでは、クラウド管理ゲートウェイ (CMG) で HTTP 管理ポイントを使用できません。 HTTPS の CMG を構成するか、拡張 HTTP のサイトを構成します。 詳細については、「[クラウド管理ゲートウェイの計画](../../../clients/manage/cmg/plan-cloud-management-gateway.md)」を参照してください。

### <a name="configuration-for-sql-server-memory-usage"></a>SQL Server のメモリ使用量の構成

*適用対象:サイト データベース サーバー*

SQL Server がメモリ使用制限なしに構成されています。 SQL Server のメモリに上限を構成します。

### <a name="distribution-point-package-version"></a>配布ポイントのパッケージ バージョン

*適用対象:配布ポイント*

サイト内のすべての配布ポイントに最新バージョンのソフトウェア配布パッケージが適用されています。

### <a name="domain-membership-warning"></a>ドメインのメンバーシップ (警告)

*適用対象:管理ポイント、配布ポイント*

Configuration Manager コンピューターが Windows ドメインのメンバーです。

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>SQL Server のファイアウォールの例外 (スタンドアロン プライマリ サイト)

*適用対象:プライマリ サイト (スタンドアロンのみ)*

Windows ファイアウォールが無効になっている、または SQL Server に対して適切な Windows ファイアウォールの例外が存在します。

Sqlservr.exe または必要な TCP ポートへのリモート アクセスを許可します。 既定で、SQL Server では TCP ポート 1433 でリッスンし、Server Service Broker (SSB) では TCP ポート 4022 を使用します。

### <a name="firewall-exception-for-sql-server-for-management-point"></a>管理ポイントに関する SQL Server 用のファイアウォールの例外

*適用対象:管理ポイント*

Windows ファイアウォールが無効になっている、または SQL Server に対して適切な Windows ファイアウォールの例外が存在します。

### <a name="iis-https-configuration"></a>IIS の HTTPS 構成

*適用対象:管理ポイント、配布ポイント*

IIS Web サイトに HTTPS 通信プロトコル用のバインドがあります。

HTTPS を必要とするサイトの役割をインストールする場合は、有効な公開キー基盤 (PKI) 証明書を使用して、指定されたサーバーで IIS サイト バインドを構成します。

### <a name="invalid-discovery-records"></a>無効な探索レコード

*適用対象: 中央管理サイト*

無効になっている探索レコードがあります。 これらのレコードは削除対象としてマークされます。

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60)

*適用対象: 中央管理サイト、プライマリ サイト、セカンダリ サイト、Configuration Manager コンソール、管理ポイント、配布ポイント*

MSXML 6.0 以降のバージョンがインストールされていることを確認します。

### <a name="network-access-protection-nap-is-no-longer-supported"></a>ネットワーク アクセス保護 (NAP) はサポートされなくなりました

*適用対象:プライマリ サイト*

NAP に使用できるソフトウェア更新プログラムはありません。

### <a name="ntfs-drive-on-site-server"></a>サイト サーバー上の NTFS ドライブ

*適用対象:プライマリ サイト*

ディスク ドライブが NTFS ファイル システムでフォーマットされています。 セキュリティを強化するには、NTFS ファイル システムでフォーマットされたディスク ドライブにサイト サーバー コンポーネントをインストールします。

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a> 保留中の構成アイテム ポリシーの更新プログラム

<!--SCCMDocs-pr issue 2814-->

*適用対象:プライマリ サイト*

バージョン 1806 以降では、バージョン 1706 以降から更新する場合、アプリケーションの展開数が多く、そのうち少なくとも 1 つで承認が必要であると、この警告が表示されることがあります。

次の 2 つのオプションがあります。  

- 警告を無視して、更新を続行する。 この操作によって、更新中のポリシーを処理する際に、サイト サーバーに高い負荷がかかります。 更新後の管理ポイント上でも、プロセッサの負荷が増える可能性があります。  

- 要件がない、あるいは特定の OS 要件があるアプリケーションのいずれかを変更する。 その時点でのサイト サーバー上の一部の負荷を事前に処理します。 **objreplmgr.log** を確認し、管理ポイント上のプロセッサを監視します。 処理が完了したら、サイトを更新します。 更新後もさらに処理が発生する可能性がありますが、最初のオプションで警告を無視した場合よりは少なくなります。  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>リモート SQL Server でシステムの再起動が保留中です

*適用対象:バージョン 1902 以降、リモート SQL Server*

セットアップを実行する前に、別のプログラムでサーバーを再起動することが要求されます。

コンピューターが再起動の保留状態であるかどうかを確かめるために、次のレジストリの場所が確認されます。<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>サイト サーバーの PowerShell 2.0

*適用対象:Exchange コネクタを使用するプライマリ サイト*

Configuration Manager Exchange Connector 用のサイト サーバーに、Windows PowerShell 2.0 以降のバージョンがインストールされています。

### <a name="remote-connection-to-wmi-on-secondary-site"></a>セカンダリ サイトの WMI へのリモート接続

*適用対象:セカンダリ サイト*

セットアップで、セカンダリ サイト サーバーの WMI へのリモート接続を確立できます。

### <a name="schema-extensions"></a>スキーマ拡張

*適用対象:中央管理サイト、プライマリ サイト*

Active Directory スキーマが拡張されています。 拡張されている場合は、使用されたスキーマ拡張のバージョン。

Configuration Manager では、サイト サーバーのインストールに Active Directory スキーマ拡張は必要ありません。 Microsoft では、すべての Configuration Manager 機能を十分活用するためにこれをお勧めします。 スキーマ拡張の詳細については、「[サイト発行のために Active Directory を準備する](../../../plan-design/network/extend-the-active-directory-schema.md)」を参照してください。

### <a name="share-name-in-package"></a>パッケージでの共有名

*適用対象:中央管理サイト、プライマリ サイト*

パッケージには、共有名に無効な文字 (`#` など) が含まれていません。

### <a name="site-system-to-sql-server-communication"></a>サイト システムから SQL Server への通信

*適用対象:セカンダリ サイト、管理ポイント*

サイト データベース インスタンスの SQL Server サービスの実行用に構成したアカウントに、Active Directory Domain Services で有効なサービス プリンシパル名 (SPN) があります。 Kerberos 認証をサポートするには、Active Directory で有効な SPN を登録します。

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a> SQL Server 変更追跡のクリーンアップ

*適用対象:サイト データベース サーバー*

バージョン 1810 以降では、サイト データベースに SQL 変更追跡データのバックログがあるかどうかを確認します。<!--SCCMDocs-pr issue 3023-->  

サイト データベースで診断ストアド プロシージャを実行することで、この確認を手動で検証します。 最初に、サイト データベースへの[診断接続](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators)を作成します。 最も簡単な方法は、SQL Server Management Studio のデータベース エンジン クエリ エディターを使用して、`admin:<instance name>` に接続することです。

専用管理者接続クエリ ウィンドウで、次のコマンドを実行します。

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

データベースのサイズやバックログのサイズに応じて、このストアド プロシージャは数分または数時間実行される場合があります。 クエリが完了すると、バックログに関連するデータの 2 つのセクションが表示されます。 最初に、**CT_Days_Old** を確認します。 この値は、syscommittab テーブル内の最も古いエントリの経過期間 (日数) を示しています。 これは、Configuration Manager の既定値である、5 日になっているはずです。 この既定値は変更しないでください。 負荷の大きいデータの処理時またはレプリケーション時に、syscommittab の最も古いエントリが 5 日を超える場合があります。 この値が 7 日を超える場合は、変更追跡データの手動クリーンアップを実行します。  

変更追跡データをクリーンアップするには、専用管理接続で次のコマンドを実行します。

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

このコマンドでは、syscommittab と関連付けられている側のテーブルのすべてのクリーンアップを開始します。 これは数分または数時間実行される場合があります。 その進行状況を監視するには、**vLogs** ビューのクエリを実行します。 現在の進行状況を表示するには、次のクエリを実行します。

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 SQL Server Native Client を更新するには、再起動が必要な場合があります。これは、サイトのインストール プロセスに影響する可能性があります。

このチェックでは、サイト サーバーに SQL Native Client のサポートされているバージョンがあることを確認します。 前提条件の確認では、リモート サイト システムの SQL Native Client のバージョンは確認されません。

最小バージョンは SQL 2012 SP4 (`11.*.7001.0`) です。 この SQL Native Client のバージョンでは、TLS 1.2 をサポートします。 詳細については、以下の記事を参照してください。

- [Microsoft SQL Server 用の TLS 1.2 のサポート](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Configuration Manager で TLS 1.2 を有効にする方法](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager では、次のサイト システムの役割で SQL Server Native Client を使用します。<!-- SCCMDocs issue 1150 -->

- サイト データベース サーバー
- サイト サーバー: 中央管理サイト、プライマリ サイト、またはセカンダリ サイト
- 管理ポイント
- デバイス管理ポイント
- 状態移行ポイント
- SMS プロバイダー
- ソフトウェアの更新ポイント
- マルチキャスト対応の配布ポイント
- 資産インテリジェンスの更新サービス ポイント
- レポート サービス ポイント
- アプリケーション カタログ Web サービス
- 登録ポイント
- Endpoint Protection ポイント
- [サービス接続ポイント]
- 証明書登録ポイント
- データ ウェアハウス サービス ポイント

### <a name="sql-server-process-memory-allocation"></a>SQL Server プロセスのメモリの割り当て

*適用対象:サイト データベース サーバー*

SQL Server で、中央管理サイトとプライマリ サイト用に少なくとも 8 GB、セカンダリ サイト用に少なくとも 4 GB のメモリが予約されています。

詳細については、「[[SQL Server Management Studio] を利用してメモリ オプションを構成する方法](/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-)」を参照してください。

> [!NOTE]  
> この確認は、セカンダリ サイトの SQL Server Express には適用できません。 このエディションでは、予約メモリが 1 GB に制限されます。  

### <a name="sql-server-security-mode"></a>SQL Server のセキュリティ モード

*適用対象:サイト データベース サーバー*

Windows 認証セキュリティ用に SQL Server が構成されています。

### <a name="unsupported-site-system-os-version-for-upgrade"></a>アップグレードでサポートされていないサイト システムの OS バージョン

*適用対象:プライマリ サイト、セカンダリ サイト*

配布ポイント以外のサイト システムの役割が、Windows Server 2012 以降を実行しているサーバーにインストールされています。

詳細については、「[Configuration Manager サイト システム サーバーでサポートされるオペレーティング システム](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)」を参照してください。

> [!NOTE]  
> この確認では、Azure にインストールされているサイト システムの役割や、Microsoft Intune によって使用されるクラウド ストレージ用のサイト システムの役割の状態を解決できません。 これらの役割に対する誤検知としての警告は無視します。

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>Upgrade Assessment Toolkit はサポートされていません

*適用対象:中央管理サイト、プライマリ サイト*

Upgrade Assessment Toolkit はインストールされません。 詳細については、[削除された機能と非推奨の機能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Active Directory に発行するためのサイト サーバーのアクセス許可の確認

*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイト サーバーのコンピューター アカウントに、Active Directory ドメイン内の **System Management** コンテナーに対する**フル コントロール** アクセス許可があります。

詳細については、「[サイト発行のために Active Directory を準備する](../../../plan-design/network/extend-the-active-directory-schema.md)」を参照してください。

> [!NOTE]  
> アクセス許可を手動で確認する場合、この警告は無視できます。

### <a name="windows-remote-management-winrm-v11"></a>Windows Remote Management (WinRM) v1.1

*適用対象:プライマリ サイト、Configuration Manager コンソール*

帯域外管理コンソールを実行するために、プライマリ サイト サーバーまたは Configuration Manager コンソール コンピューターに WinRM 1.1 がインストールされています。

WinRM は、現在サポートされているあらゆるバージョンの Windows と共に自動的にインストールされます。 詳細については、「[Windows リモート管理のためのインストールと構成](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management)」をご覧ください。

### <a name="wsus-on-site-server"></a>サイト サーバー上の WSUS

*適用対象:中央管理サイト、プライマリ サイト*

サポートされているバージョンの Windows Server Update Services (WSUS) がサイト サーバーにインストールされています。

サイト サーバー以外のサーバーでソフトウェアの更新ポイントを使用する場合は、サイト サーバーに WSUS 管理コンソールをインストールする必要があります。 WSUS の詳細については、「[Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)」を参照してください。