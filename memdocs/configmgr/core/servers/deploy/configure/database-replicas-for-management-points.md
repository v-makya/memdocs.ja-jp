---
title: 管理ポイントのデータベース レプリカ
titleSuffix: Configuration Manager
description: 管理ポイントがサイト データベース サーバーに加えられた CPU 負荷を軽減するように、データベース レプリカを使用します。
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e647672b02c0122709b3c80fc012ed1fb82b1519
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696431"
---
# <a name="database-replicas-for-management-points-for-configuration-manager"></a>Configuration Manager の管理ポイントのデータベース レプリカ

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager プライマリ サイトでは、データベース レプリカを使用して、管理ポイントがクライアントからの要求を処理することでサイト データベース サーバーに加えられた CPU 負荷を軽減することができます。  

-   管理ポイントでデータベース レプリカを使用すると、その管理ポイントはサイト データベース サーバーではなく、データベース レプリカをホストする SQL Server コンピューターにデータを要求します。  

-   これにより、クライアントに関連して頻繁に発生する処理タスクの負荷を軽減し、サイト データベース サーバーの CPU 処理要件を減らすことができます。  クライアントの頻繁な処理タスクの例として、クライアント ポリシーのために頻繁に要求を行うクライアントがサイトに多数存在する場合が挙げられます。  


##  <a name="prepare-to-use-database-replicas"></a><a name="bkmk_Prepare"></a> データベース レプリカを使用するための準備  
**管理ポイントのデータベース レプリカについて**  

-   レプリカは、SQL Server の別のインスタンスにレプリケートされるサイト データベースの部分的なコピーです。  

    -   プライマリ サイトは、サイトの各管理ポイントの専用のデータベース レプリカをサポートします (セカンダリ サイトではデータベース レプリカはサポートされません)。  

    -   同一サイトの複数の管理ポイントで 1 つのデータベース レプリカを使用できます。  

    -   SQL Server は、各データベース レプリカが SQL Server の別のインスタンスで実行されている限り、異なる管理ポイントでの複数データベース レプリカの使用をホストできます。  

-   レプリカは、サイト データベース サーバーが同期用に発行したデータとサイト データベースのコピーを、決められたスケジュールに従って同期します。  

-   管理ポイントをインストールするとき、またはインストール済みの管理ポイントを後で再構成するときに、データベース レプリカを使用するように構成できます。  

-   サイト データベース サーバーおよび各データベース レプリカ サーバーを定期的に監視し、それらの間でレプリケーションが実行されていること、データベース レプリカ サーバーのパフォーマンスがサイトとクライアントで必要とされるパフォーマンスに対して十分であることを確認します。  

**データベース レプリカの前提条件:**  

-   **SQL Server の要件:**  

    -   データベース レプリカをホストする SQL Server は、サイト データベース サーバーと同じ要件を満たしている必要があります。 ただし、レプリカ サーバーで実行する SQL Server のバージョンとエディションは、サポートされている SQL Server のバージョンとエディションであれば、サイト データベース サーバーと同じでなくてもかまいません。 詳細については、「[Configuration Manager の SQL Server バージョンのサポート](../../../../core/plan-design/configs/support-for-sql-server-versions.md)」をご覧ください。  

    -   レプリカ データベースをホストするコンピューターの SQL Server サービスを、 **System** アカウントとして実行する必要があります。  

    -   サイト データベースをホストする SQL Server とデータベース レプリカをホストする SQL Server の両方に、 **SQL Server レプリケーション** がインストールされている必要があります。  

    -   サイト データベースはデータベース レプリカを **発行** する必要があります。また、リモートの各データベース レプリカ サーバーは、発行されたデータを **サブスクライブ** する必要があります。  

    -   サイト データベースをホストする SQL Server とデータベース レプリカをホストする SQL Server の両方を、2 GB の **テキスト レプリケーションの最大サイズ** をサポートするように構成する必要があります。 SQL Server 2012 でこれを構成する方法の例については、「 [max text repl size サーバー構成オプションの構成](/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option?view=sql-server-ver15)」をご覧ください。  

-   **自己署名証明書:** データベース レプリカを構成するには、データベース レプリカ サーバー上で自己署名証明書を作成して、そのデータベース レプリカ サーバーを使用する各管理ポイントでこの証明書を利用できるようにする必要があります。  

    -   データベース レプリカ サーバーにインストールされている管理ポイントでは、この証明書が自動的に利用できるようになります。  

    -   この証明書をリモート管理ポイントが利用できるようにするには、証明書をエクスポートして、リモート管理ポイントの **信頼されたユーザー** 証明書ストアに追加する必要があります。  

-   **クライアント通知:** 管理ポイントのデータベース レプリカを使用したクライアント通知をサポートするためには、**SQL Server Service Broker** のためにサイト データベース サーバーとデータベース レプリカ サーバー間の通信を構成する必要があります。 そのためには、次の操作が必要です。  

    -   他方のデータベースに関する情報を使用して各データベースを構成します。  

    -   セキュリティ保護された通信を行うため、2 つのデータベース間で証明書を交換します。  

**データベース レプリカを使用する場合の制限事項:**  

-   データベース レプリカを発行するようにサイトが構成されている場合は、通常のガイダンスの代わりに次の手順を使用する必要があります。  

    -   [データベースのレプリカを発行するサイト サーバーのアンインストール](#BKMK_DBReplicaOps_Uninstall)  

    -   [データベースのレプリカを発行するサイト サーバー データベースの移動](#BKMK_DBReplicaOps_Move)  

-   **Configuration Manager Current Branch にアップグレードする**:サイトを System Center 2012 Configuration Manager から Configuration Manager Current Branch にアップグレードする前、または Configuration Manager Current Branch を最新リリースに更新する前に、管理ポイントのデータベース レプリカを無効にする必要があります。  サイトをアップグレードしたら、管理ポイントのデータベース レプリカを再構成できます。  

-   **単一 SQL Server 上の複数レプリカ:** 管理ポイントの複数のデータベース レプリカをホストするようにデータベース レプリカ サーバーを構成する場合 (各レプリカは別々のインスタンス上にある必要があります)、変更した構成スクリプト (次のセクションの手順 4 から) を使用して、そのサーバー上の以前に構成されたデータベース レプリカで使用されている自己署名入り証明書が上書きされないようにする必要があります。  

- ソフトウェア センターでのユーザー展開は、SQL レプリカを使用する管理ポイントに対しては機能しません。 <!--sccmdocs-1011-->

##  <a name="configure-database-replicas"></a><a name="BKMK_DBReplica_Config"></a> データベース レプリカの構成  
データベース レプリカを構成して使用するには、次の手順を実行する必要があります。  

-   [手順 1 - データベース レプリカを発行するようにサイト データベース サーバーを構成する](#BKMK_DBReplica_ConfigSiteDB)  

-   [手順 2 - データベース レプリカ サーバーの構成](#BKMK_DBReplica_ConfigSrv)  

-   [手順 3 - データベース レプリカを使用するための管理ポイントの構成](#BKMK_DBReplica_ConfigMP)  

-   [手順 4 - データベース レプリカ サーバーの自己署名入り証明書の構成](#BKMK_DBReplica_Cert)  

-   [手順 5 - データベース レプリカ サーバーでの SQL Server Service Broker の構成](#BKMK_DBreplica_SSB)  

###  <a name="step-1---configure-the-site-database-server-to-publish-the-database-replica"></a><a name="BKMK_DBReplica_ConfigSiteDB"></a> 手順 1 - データベース レプリカを発行するようにサイト データベース サーバーを構成する  
 データベースのレプリカを発行するように Windows Server 2008 R2 上のサイト データベース サーバーを構成するには、次の手順に従います。 別のオペレーティング システムのバージョンを使用している場合は、使用しているオペレーティング システムのドキュメントを参照し、必要に応じてこの手順のステップを調整してください。  

##### <a name="to-configure-the-site-database-server"></a>サイト データベース サーバーを構成するには  

1.  サイト データベース サーバーで、SQL Server エージェントが自動的に開始されるように設定します。  

2.  サイト データベース サーバーで、 **ConfigMgr_MPReplicaAccess**という名前のローカルのユーザー グループを作成します。 このサイトで使用する各データベース レプリカ サーバーのコンピューター アカウントをこのグループに追加して、それらのデータベース レプリカ サーバーが発行されたデータベース レプリカと同期できるようにする必要があります。  

3.  サイト データベース サーバーで、 **ConfigMgr_MPReplica**という名前のファイル共有を構成します。  

4.  次のアクセス許可を **[ConfigMgr_MPReplica]** 共有に追加します。  

    > [!NOTE]  
    >  SQL Server エージェントがローカルのシステム アカウント以外のアカウントを使用する場合は、次のリストの SYSTEM をそのアカウント名に置き換えます。  

    -   **共有のアクセス許可**:  

        -   SYSTEM:**書き込み**  

        -   ConfigMgr_MPReplicaAccess:**読み取り**  

    -   **NTFS アクセス許可**:  

        -   SYSTEM:**フル コントロール**  

        -   ConfigMgr_MPReplicaAccess:**読み取り**、**読み取りと実行**、**フォルダーの内容の一覧表示**  

5.  **SQL Server Management Studio** を使用して、サイト データベースに接続し、ストアド プロシージャ **spCreateMPReplicaPublication**をクエリとして実行します。  

ストアド プロシージャが完了すると、サイト データベース サーバーはデータベースのレプリカを発行するように構成されています。  

###  <a name="step-2---configuring-the-database-replica-server"></a><a name="BKMK_DBReplica_ConfigSrv"></a> 手順 2 - データベース レプリカ サーバーの構成  
データベース レプリカ サーバーは、SQL Server を実行するコンピューターであり、管理ポイントが使用するサイト データベースのレプリカをホストします。 データベース レプリカ サーバーは、サイト データベース サーバーによって発行されたデータベースのレプリカとそれ自体のデータベースのコピーを固定されたスケジュールで同期します。  

データベース レプリカ サーバーは、サイト データベース サーバーと同じ要件を満たしている必要があります。 ただし、データベース レプリカ サーバーは、サイト データベース サーバーが使用している SQL Server と別のエディションまたはバージョンの SQL Server を実行できます。 サポートされている SQL Server のバージョンの詳細については、「[Configuration Manager の SQL Server バージョンのサポート](../../../../core/plan-design/configs/support-for-sql-server-versions.md)」トピックを参照してください。  

> [!IMPORTANT]  
>  レプリカ データベースをホストするコンピューターの SQL Server Service を、System アカウントとして実行する必要があります。  

Windows Server 2008 R2 コンピューターにデータベース レプリカ サーバーを構成するには、次の手順に従います。 別のオペレーティング システムのバージョンを使用している場合は、使用しているオペレーティング システムのドキュメントを参照し、必要に応じてこの手順のステップを調整してください。  

##### <a name="to-configure-the-database-replica-server"></a>データベース レプリカ サーバーを構成するには  

1. データベース レプリカ サーバーで、SQL Server エージェントが自動的に開始されるように設定します。  

2. データベース レプリカ サーバーで、 **SQL Server Management Studio** を使用してローカル サーバーに接続し、 **レプリケーション** フォルダーを参照して、ローカル サブスクリプション をクリックし、 **新規サブスクリプション** を選択します。これで、 **サブスクリプションの新規作成ウィザード**が開始されます。  

   1. **[パブリケーション]** ページの **[発行元]** リスト ボックスで、 **[SQL Server 発行元の検索]** を選択し、サイトのデータベース サーバーの名前を入力してから、 **[接続]** をクリックします。  

   2. **ConfigMgr_MPReplica**を選択し、 **[次へ]** をクリックします。  

   3. **[配布エージェントの場所]** ページで、 **[サブスクライバーで各エージェントを実行する (プル サブスクリプション)]** を選択し、 **[次へ]** をクリックします。  

   4. **[サブスクライバー]** ページで、次のいずれかの操作を行います。  

      -   データベースのレプリカに使用するデータベース レプリカ サーバーから既存のデータベースを選択して、 **[OK]** をクリックします。  

      -   **[新しいデータベース]** を選択して、データベースのレプリカの新しいデータベースを作成します。 **[新しいデータベース]** ページで、データベースの名前を指定し、 **[OK]** をクリックします。  

   5. **[次へ]** をクリックして、続行します。  

   6. 「**ディストリビューション エージェント セキュリティ**」ページで、ダイアログ ボックスの "サブスクライバー接続" 行のプロパティ ボタン **(....)** をクリックしてから、接続のセキュリティ設定を構成します。  

      > [!TIP]  
      >  プロパティ ボタン **(....)** は、表示ボックスの 4 列目にあります。  

      **セキュリティ設定:**  

      - 配布エージェント処理を実行するアカウント (プロセスのアカウント) を構成します。  

        -   SQL Server エージェントをローカル システムとして実行する場合は、 **[SQL Server エージェント サービスのアカウントで実行する (これは推奨されるセキュリティのベスト プラクティスではありません)]** を選択します。  

        -   SQL Server エージェントを別のアカウントを使用して実行する場合は、 **[次の Windows アカウントで実行する]** を選択して、そのアカウントを構成します。 Windows アカウントまたは SQL Server アカウントを指定できます。  

        > [!IMPORTANT]  
        >  配布エージェントを実行するアカウントに、発行元へのアクセス許可をプル サブスクリプションとして付与する必要があります。 これらのアクセス許可の構成について詳しくは、「[ディストリビューション エージェント セキュリティ](/sql/relational-databases/replication/distribution-agent-security?view=sql-server-ver15)」をご覧ください。  

      - **[ディストリビューターに接続]** で、 **[プロセスのアカウントを借用する]** を選択します。  

      - **[サブスクライバーに接続]** で、 **[プロセスのアカウントを借用する]** を選択します。  

        接続のセキュリティ設定を構成したら、 **[OK]** をクリックして設定を保存してから、 **[次へ]** をクリックします。  

   7. **[同期スケジュール]** ページの **[エージェント スケジュール]** リスト ボックスで、 **[スケジュールの定義]** を選択し、 **[新しいジョブ スケジュール]** を構成します。 ジョブを行う頻度を **[毎日]** に、繰り返す間隔を **[5 分]** に設定し、期間に **終了日がない**ように設定します。 **[次へ]** をクリックしてスケジュールを保存してから、もう一度 **[次へ]** をクリックします。  

   8. **[ウィザードのアクション]** ページで、 **[サブスクリプションの作成]** チェック ボックスを選択してから、 **[次へ]** をクリックします。  

   9. **[ウィザードの完了]** ページで、 **[完了]** 、 **[閉じる]** の順にクリックしてウィザードを完了します。  

3. サブスクリプションの新規作成ウィザードの完了の直後に、 **SQL Server Management Studio** を使用してデータベース レプリカ サーバーのデータベースに接続し、次のクエリを実行して TRUSTWORTHY データベース プロパティを有効にします。  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. 同期ステータスを確認して、サブスクリプションが成功したことを検証します。  

   -   サブスクライバーのコンピューターで:  

       -   **SQL Server Management Studio**で、データベース レプリカ サーバーに接続し、 **[レプリケーション]** を展開します。  

       -   **[ローカル サブスクリプション]** を展開してサイト データベース パブリケーションに対するサブスクリプションを右クリックし、 **[同期の状態の表示]** を選択します。  

   -   発行元のコンピューターで:  

       -   **SQL Server Management Studio**で、サイト データベース コンピューターに接続し、 **[レプリケーション]** フォルダーを右クリックして **[レプリケーション モニターの起動]** を選択します。  

5. データベースのレプリカで共通言語ランタイム (CLR) 統合を有効にするには、**SQL Server Management Studio** を使用して、データベース レプリカ サーバーのデータベースのレプリカに接続し、ストアド プロシージャ **exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE**をクエリとして実行します  

6. データベース レプリカ サーバーを使用する各管理ポイントで、管理ポイントのコンピューター アカウントをそのデータベース レプリカ サーバーのローカルの **[Administrators]** グループに追加します。  

   > [!TIP]  
   >  この手順は、データベース レプリカ サーバーで実行する管理ポイントでは必要ありません。  

   管理ポイントでデータベースのレプリカを使用できるようになりました。  

###  <a name="step-3---configure-management-points-to-use-the-database-replica"></a><a name="BKMK_DBReplica_ConfigMP"></a> 手順 3 - データベース レプリカを使用するための管理ポイントの構成  
 管理ポイントの役割をインストールするときに、データベースのレプリカを使用するようにプライマリ サイトの管理ポイントを構成できます。または、既存の管理ポイントがデータベースのレプリカを使用するように再構成できます。  

 次の情報を使用して、管理ポイントがデータベースのレプリカを使用するように構成します。  

-   新しい管理ポイントを構成**するには:** 管理ポイントをインストールするためのウィザードの **[管理ポイントのデータベース]** ページで、 **[データベースのレプリカを使用する]** を選択してから、データベースのレプリカをホストするコンピューターの FQDN を指定します。 次に、 **[ConfigMgr サイト データベース名]** で、そのコンピューターのデータベースのレプリカのデータベース名を指定します。  

-   **以前にインストールした管理ポイントを構成するには**: 管理ポイントのプロパティ ページを開き、 **[管理ポイントのデータベース]** タブ、 **[データベースのレプリカを使用する]** の順に選択してから、データベースのレプリカをホストするコンピューターの FQDN を指定します。 次に、 **[ConfigMgr サイト データベース名]** で、そのコンピューターのデータベースのレプリカのデータベース名を指定します。  

-   **データベースのレプリカを使用する各管理ポイント**では、管理ポイント サーバーのコンピューター アカウントをデータベース レプリカの **db_datareader** ロールに手動で追加する必要があります。  

データベース レプリカ サーバーを使用する管理ポイントを構成するだけでなく、管理ポイントの **IIS** で **Windows 認証** を有効にする必要もあります。  

1.  **[インターネット インフォメーション サービス (IIS) マネージャー]** を開きます。  

2.  管理ポイントが使用する Web サイトを選択して、 **[認証]** を開きます。  

3.  **[Windows 認証]** を **[有効]** に設定してから、 **[インターネット インフォメーション サービス (IIS) マネージャー]** を閉じます。  

###  <a name="step-4--configure-a-self-signed-certificate-for-the-database-replica-server"></a><a name="BKMK_DBReplica_Cert"></a> 手順 4 - データベース レプリカ サーバーの自己署名入り証明書の構成  
 データベース レプリカ サーバーで自己署名入り証明書を作成して、そのデータベース レプリカ サーバーを使用する各管理ポイントがこの証明書を利用できるようにする必要があります。  

 データベース レプリカ サーバーにインストールされている管理ポイントでは、この証明書が自動的に利用できるようになります。 ただし、この証明書をリモート管理ポイントが利用できるようにするには、証明書をエクスポートして、リモート管理ポイントの信頼されたユーザー証明書ストアに追加する必要があります。  

 Windows Server 2008 R2 コンピューター上のデータベース レプリカ サーバーに自己署名入り証明書を構成するには、次の手順に従います。 別のオペレーティング システムのバージョンを使用している場合は、使用しているオペレーティング システムのドキュメントを参照し、必要に応じてこれらの手順のステップを調整してください。  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>データベース レプリカ サーバーに自己署名入り証明書を構成するには  

1.  データベース レプリカ サーバーで、管理者特権で PowerShell コマンド プロンプトを開いて、コマンド **set-executionpolicy UnRestricted**を実行します:  

2.  次の PowerShell スクリプトをコピーし、 **CreateMPReplicaCert.ps1**という名前のファイルとして保存します。 このファイルのコピーを、データベース レプリカ サーバーのシステム パーティションのルート フォルダーに配置します。  

    > [!IMPORTANT]  
    >  1 つの SQL Server に複数のデータベース レプリカを構成する場合は、後で構成する各レプリカについて、この手順で変更済みのこのスクリプトを使用する必要があります。 「  [単一の SQL Server 上の追加データベース レプリカ用の補足スクリプト](#bkmk_supscript)」をご覧ください。  

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  データベース レプリカ サーバーで、SQL Server の構成を適用する次のコマンドを実行します。  

    -   SQL Server の既定のインスタンスの場合:**CreateMPReplicaCert.ps1** ファイルを右クリックして **[PowerShell で実行]** を選択します。 スクリプトを実行すると、自己署名入り証明書が作成され、SQL Server がその証明書を使用するように構成されます。  

    -   SQL Server の名前付きインスタンスの場合:PowerShell を使用して、コマンド **%path%\CreateMPReplicaCert.ps1 xxxxxx** を実行します。ここで、**xxxxxx** は SQL Server インスタンスの名前です。  

    -   スクリプトが完了したら、SQL Server エージェントが実行されていることを確認します。 実行されていない場合は、SQL Server エージェントを再起動します。  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>リモート管理ポイントがデータベース レプリカ サーバーの自己署名入り証明書を使用するように構成するには  

1.  データベース レプリカ サーバーで次の手順を実行して、サーバーの自己署名入り証明書をエクスポートします。  

    1.  **[スタート]** 、 **[実行]** の順にクリックし、「 **mmc.exe**」と入力します。 空のコンソールで、 **[ファイル]** をクリックし、次に **[スナップインの追加と削除]** をクリックします。  

    2.  **[スナップインの追加と削除]** ダイアログ ボックスで、 **[利用できるスナップイン]** リストから **[証明書]** を選択し、 **[追加]** をクリックします。  

    3.  **[証明書スナップイン]** ダイアログボックスで **[コンピューター アカウント]** を選択し、 **[次へ]** をクリックします。  

    4.  **[コンピューターの選択]** ダイアログ ボックスで、 **[ローカル コンピューター: (このコンソールを実行しているコンピューター)]** が選択されていることを確認して、 **[完了]** をクリックします。  

    5.  **[スナップインの追加と削除]** ダイアログ ボックスで、 **[OK]** をクリックします。  

    6.  コンソール ウィンドウで  **証明書 (ローカル コンピューター)** 、**個人** の順に展開して、**証明書** を選択します。  

    7.  **ConfigMgr SQL Server 識別証明書**のフレンドリ名の付いた証明書を右クリックして **[すべてのタスク]** をクリックし、 **[エクスポート]** を選択します。  

    8.  既定のオプションを使用して、 **証明書のエクスポート ウィザード** を完了し、 **.cer** ファイル名拡張子を使用して証明書を保存します。  

2.  管理ポイントのコンピューターで次の手順を実行し、データベース レプリカ サーバーの自己署名入り証明書を管理ポイントの信頼されたユーザー証明書ストアに追加します。  

    1.  上記の手順 1.a から 1.e を繰り返し、管理ポイントのコンピューターに [証明書] スナップイン MMC を構成します。 管理ポイントのコンピューターに **[証明書]** スナップイン MMC を構成します。  

    2.  コンソールで、 **[証明書 (ローカル コンピューター)]** 、 **[信頼されたユーザー]** の順に展開し、 **[証明書]** を右クリックして、 **[すべてのタスク]** 、 **[インポート]** の順に選択して、 **証明書のインポート ウィザード**を開始します。  

    3.  **[インポートするファイル]** ページで、手順 1.h で保存した証明書を選択し、 **[次へ]** をクリックします。  

    4.  **[証明書ストア]** ページで **[証明書をすべて次のストアに配置する]** を選択し、 **[証明書ストア]** を **[信頼されたユーザー]** に設定して、 **[次へ]** をクリックします。  

    5.  **[完了]** をクリックし、ウィザードを閉じて、管理ポイントへの証明書の構成を完了します。  

###  <a name="step-5---configure-the-sql-server-service-broker-for-the-database-replica-server"></a><a name="BKMK_DBreplica_SSB"></a> 手順 5 - データベース レプリカ サーバーでの SQL Server Service Broker の構成  
管理ポイントのデータベース レプリカを使用したクライアント通知をサポートするためには、SQL Server Service Broker にサイト データベース サーバーとデータベース レプリカ サーバー間の通信を構成する必要があります。 そのためには、他のデータベースの情報を使って各データベースを構成し、通信をセキュリティで保護するために 2 つのデータベース間で証明書を交換する必要があります。  

> [!NOTE]  
>  以下の手順を実行する前に、データベース レプリカ サーバーでサイト データベース サーバーとの最初の同期が正常に完了する必要があります。  

 以下の手順を実行しても、サイト データベース サーバーまたはデータベース レプリカ サーバーの SQL Server に構成されているサービス ブローカー ポートは変更されません。 代わりに、この手順で、正しいサービス ブローカー ポートを使って他のデータベースと通信するように、各データベースが構成されます。  

 サイト データベース サーバーとデータベース レプリカ サーバーにサービス ブローカーを構成するには、次の手順を実行します。  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>データベースのレプリカにサービス ブローカーを構成するには  

1. **SQL Server Management Studio** を使用して、データベース レプリカ サーバーのデータベースに接続してから、次のクエリを実行してデータベース レプリカ サーバーでサービス ブローカーを有効にします。**ALTER DATABASE &lt;レプリカ データベース名\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2. 次に、データベース レプリカ サーバーで、クライアント通知を行うようにサービス ブローカーを構成し、サービス ブローカーの証明書をエクスポートします。 これを行うには、サービス ブローカーを構成する SQL Server ストアド プロシージャを実行して、証明書を 1 回の操作でエクスポートします。 ストアド プロシージャを実行するときに、データベース レプリカ サーバーの FQDN、データベースのレプリカのデータベース名、および証明書ファイルをエクスポートする場所を指定する必要があります。  

    次のクエリを実行して、必要な情報をデータベース レプリカ サーバーに構成し、データベース レプリカ サーバーの証明書をエクスポートします。**EXEC sp_BgbConfigSSBForReplicaDB '&lt;レプリカ SQL Server の FQDN\>'、'&lt;レプリカ データベース名\>'、'&lt;証明書バックアップ ファイルのパス\>'**  

   > [!NOTE]  
   >  データベース レプリカ サーバーが SQL Server の既定のインスタンスに配置されていない場合は、この手順で、レプリカ データベース名に加えてインスタンス名も指定する必要があります。 それには、 **&lt;レプリカ データベース名\>** を **&lt;インスタンス名\\レプリカ データベース名\>** に置き換えます。  

    データベース レプリカ サーバーから証明書をエクスポートしたら、証明書のコピーをプライマリ サイトのデータベース サーバーに配置します。  

3. **SQL Server Management Studio** を使用して、プライマリ サイトのデータベースに接続します。 プライマリ サイトのデータベースに接続したら、クエリを実行して証明書をインポートし、データベース レプリカ サーバーで使用するサービス ブローカー ポート、データベース レプリカ サーバーの FQDN、およびデータベースのレプリカのデータベース名を指定します。 これにより、サービス ブローカーを使用してデータベース レプリカ サーバーのデータベースと通信するように、プライマリ サイトのデータベースが構成されます。  

    次のクエリを実行してデータベース レプリカ サーバーから証明書をインポートし、必要な情報を指定します。**EXEC sp_BgbConfigSSBForRemoteService 'REPLICA'、'&lt;SQL のサービス ブローカー ポート\>'、'&lt;証明書のファイル パス\>'、'&lt;レプリカの SQL Server の FQDN\>'、'&lt;レプリカ データベース名\>'**  

   > [!NOTE]  
   >  データベース レプリカ サーバーが SQL Server の既定のインスタンスに配置されていない場合は、この手順で、レプリカ データベース名に加えてインスタンス名も指定する必要があります。 それには、 **&lt;レプリカ データベース名\>** を **\インスタンス名\\レプリカ データベース名\>** に置き換えます。  

4. 次に、サイト データベース サーバーで、次のコマンドを実行してサイト データベース サーバーの証明書をエクスポートします。**EXEC sp_BgbCreateAndBackupSQLCert '&lt;証明書のバックアップ ファイル パス\>'**  

    サイト データベース サーバーから証明書をエクスポートしたら、証明書のコピーをデータベース レプリカ サーバーに配置します。  

5. **SQL Server Management Studio** を使用して、データベース レプリカ サーバーのデータベースに接続します。 データベース レプリカ サーバーのデータベースに接続したら、クエリを実行して証明書をインポートし、プライマリ サイトのサイト コードと、サイト データベース サーバーで使用するサービス ブローカー ポートを指定します。 これにより、サービス ブローカーを使用してプライマリ サイトのデータベースと通信するように、データベース レプリカ サーバーが構成されます。  

    次のクエリを実行して、サイト データベース サーバーから証明書をインポートします。**EXEC sp_BgbConfigSSBForRemoteService '&lt;サイト コード\>'、'&lt;SQL のサービス ブローカー ポート\>'、'&lt;証明書のファイル パス\>'**  

   サイト データベースとデータベースのレプリカ データベースの構成を完了して数分すると、プライマリ サイトの通知マネージャーによって、プライマリ サイト データベースからデータベースのレプリカへのクライアント通知を行うための Service Broker メッセージ交換が設定されます。  

###  <a name="supplemental-script-for-additional-database-replicas-on-a-single-sql-server"></a><a name="bkmk_supscript"></a> 単一の SQL Server 上の追加データベース レプリカ用の補足スクリプト  
 手順 4 のスクリプトを使用して、引き続き使用するデータベース レプリカが既に存在する SQL Server 上のデータベース レプリカ サーバーの自己署名入り証明書を構成する場合、元のスクリプトの変更済みバージョンを使用する必要があります。 次の変更を行うと、スクリプトはサーバー上の既存の証明書を削除することなく、一意のフレンドリ名を持つ後続の証明書を作成します。  次のように、元のスクリプトを編集します。  

-   スクリプト エントリ **# Delete existing cert if one exists** と **# Create the new cert**の間の各行をコメントに (実行されないように) します。コメントにするには、該当する各行の先頭に文字  **#**  を追加します。  

-   この証明書を使用して構成する後続のデータベース レプリカごとに、証明書のフレンドリ名を更新します。  これを行うには、 **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** の行を編集し、 **ConfigMgr SQL Server Identification Certificate** を新しい名前 (  **ConfigMgr SQL Server Identification Certificate1**など) に置き換えます。  

##  <a name="manage-database-replica-configurations"></a><a name="BKMK_DBReplicaOps"></a> データベースのレプリカの構成の管理  
 サイトでデータベースのレプリカを使用する場合は、データベースのレプリカのアンインストール、データベースのレプリカを使用するサイトのアンインストール、または SQL Server の新しいインストールへのサイト データベースの移動を行うための補足する手順として、以下のセクションの情報を参照してください。 以下のセクションの情報を参照してパブリケーションを削除する場合は、データベースのレプリカに使用しているバージョンの SQL Server のトランザクション レプリケーションを削除する手順に従ってください。 詳細については、「[パブリケーションの削除](/sql/relational-databases/replication/publish/delete-a-publication?view=sql-server-ver15)」を参照してください。  

> [!NOTE]  
>  データベースのレプリカ用に構成されたサイト データベースを復元した後で、データベースのレプリカを使用するためには、データベースの各レプリカを再構成して、パブリケーションとサブスクリプションの両方を再作成する必要があります。  

###  <a name="uninstall-a-database-replica"></a><a name="BKMK_UninstallDbReplica"></a> データベースのレプリカのアンインストール  
 管理ポイントにデータベースのレプリカを使用する場合、データベースのレプリカをしばらくの間アンインストールしてから、使用するには再構成することが必要になる可能性があります。 たとえば、Configuration Manager サイトを新しいサービス パックにアップグレードする前に、データベースのレプリカを削除する必要があります。 サイトのアップグレードが完了した後で、データベースのレプリカを復元して使用することができます。  

 データベースのレプリカをアンインストールするには、次の手順を実行します。  

1.  Configuration Manager コンソールの **[管理]** ワークスペースで、 **[サイトの構成]** を展開して **[サーバーとサイト システムの役割]** を選択します。それから、詳細ウィンドウで、アンインストール対象のデータベース レプリカを使用している管理ポイントをホストしているサイト システム サーバーを選択します。  

2.  **[サイト システムの役割]** ウィンドウで、 **[管理ポイント]** を右クリックして **[プロパティ]** を選択します。  

3.  **[管理ポイントのデータベース]** タブで **[サイト データベースを使用する]** を選択し、データベースのレプリカではなくサイト データベースを使用する管理ポイントを構成します。 次に、 **[OK]** をクリックして構成を保存します。  

4.  **SQL Server Management Studio** を使用して、次のタスクを実行します。  

    -   サイト サーバー データベースからデータベースのレプリカのパブリケーションを削除する。  

    -   データベース レプリカ サーバーからデータベースのレプリカのサブスクリプションを削除する。  

    -   データベース レプリカ サーバーからレプリカ データベースを削除する。  

    -   サイト データベース サーバーでパブリッシングとディストリビューションを無効にする。 パブリッシングとディストリビューションを無効にするには、Replication フォルダーを右クリックしてから、 **[パブリッシングおよびディストリビューションを無効にする]** をクリックします。  

5.  サイト データベース サーバーでパブリケーション、サブスクリプション、レプリカ データベースを削除し、パブリッシングを無効にすると、データベースのレプリカがアンインストールされます。  

###  <a name="uninstall-a-site-server-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Uninstall"></a> データベースのレプリカを発行するサイト サーバーのアンインストール  
 データベースのレプリカを発行するサイトをアンインストールする前に、次の手順に従って、パブリケーションおよびサブスクリプションをクリーンアップします。  

1.  **SQL Server Management Studio** を使用して、サイト サーバー データベースからデータベースのレプリカのパブリケーションを削除します。  

2.  **SQL Server Management Studio** を使用して、このサイトのデータベースのレプリカをホストする各リモート SQL Server から、データベースのレプリカのサブスクリプションを削除します。  

3.  サイトをアンインストールします。  

###  <a name="move-a-site-server-database-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Move"></a> データベースのレプリカを発行するサイト サーバー データベースの移動  
 サイト データベースを新しいコンピューターに移動する場合は、次の手順に従います。  

1.  **SQL Server Management Studio** を使用して、サイト サーバー データベースからデータベースのレプリカのパブリケーションを削除します。  

2.  **SQL Server Management Studio** を使用して、このサイトの各データベース レプリカ サーバーから、データベースのレプリカのサブスクリプションを削除します。  

3.  データベースを新しい SQL Server コンピューターに移動します。 詳細については、「[Configuration Manager インフラストラクチャの変更](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig)」トピックの「[サイト データベース構成の変更](../../../../core/servers/manage/modify-your-infrastructure.md)」セクションをご覧ください。  

4.  サイト データベース サーバーにデータベースのレプリカのパブリケーションを再作成します。 詳細については、このトピックの「 [手順 1 - データベース レプリカを発行するようにサイト データベース サーバーを構成する](#BKMK_DBReplica_ConfigSiteDB) 」をご覧ください。  

5.  各データベース レプリカ サーバーにデータベースのレプリカのサブスクリプションを再作成します。 詳細については、このトピックの「 [手順 2 - データベース レプリカ サーバーの構成](#BKMK_DBReplica_ConfigSrv) 」をご覧ください。