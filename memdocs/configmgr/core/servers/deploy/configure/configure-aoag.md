---
title: 可用性グループを構成する
titleSuffix: Configuration Manager
description: Configuration Manager で SQL Server Always On 可用性グループを設定して管理する
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e85b36d0caeb6ceb99f56220e271774dc0db0f6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699247"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configuration Manager の SQL Server Always On 可用性グループを構成する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager で使用する可用性グループを構成して管理するには、この記事の情報を使用します。

始める前に  

- 「[System Center Configuration Manager の高可用性サイト データベースの SQL Server AlwaysOn](sql-server-alwayson-for-a-highly-available-site-database.md)」の内容を理解しておいてください。
- 可用性グループの使用方法と関連する手順を説明した SQL Server ドキュメントを理解しておいてください。 ドキュメントの情報は、以下のシナリオを完了するために必要になります。


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> 可用性グループを作成して構成する

可用性グループを作成し、サイト データベースのコピーをその可用性グループに移動するには、次の手順を実行します。

1. Configuration Manager サイトを停止するには、次のコマンドを使用します。

    `preinst.exe /stopsite`

    詳細については、[階層のメンテナンス ツール](../../manage/hierarchy-maintenance-tool-preinst.exe.md)に関するページを参照してください。

2. サイト データベースのバックアップ モデルを、**SIMPLE** から **FULL** に変更します。

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    可用性グループでは、FULL バックアップ モデルのみがサポートされます。 詳細については、[データベースの復旧モデルの表示または変更](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)に関するページを参照してください。

3. SQL Server を使用してサイト データベースの完全バックアップを作成します。 次のいずれかのオプションを選択します。

    - **可用性グループのメンバーにする**:可用性グループの最初のプライマリ レプリカ メンバーとしてこのサーバーを使用する場合、グループ内のこのサーバーまたは別のサーバーにサイト データベースのコピーを復元する必要はありません。 データベースは既にプライマリ レプリカに配置されています。 SQL Server では、後の手順でデータベースをセカンダリ レプリカにレプリケートします。  

    - **可用性グループのメンバーにしない**:グループのプライマリ レプリカをホストするサーバーに、サイト データベースのコピーを復元します。

    詳細については、SQL Server のドキュメントの次の記事を参照してください。

    - [データベースの完全バックアップの作成](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [SSMS を使用してデータベース バックアップを復元する](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > 既存のレプリカで可用性グループからスタンドアロンに移行する予定の場合は、まず、可用性グループからデータベースを削除します。

4. グループの最初のプライマリ レプリカをホストするサーバーで、[新しい可用性グループ ウィザード](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio)を使用して可用性グループを作成します。 ウィザード:

    - **[データベースの選択]** ページで、Configuration Manager サイトのデータベースを選択します。  

    - **[レプリカの指定]** ページで次のように構成します。

        - **レプリカ:** セカンダリ レプリカをホストするサーバーを指定します。

        - **リスナー**: **[リスナーの DNS 名]** を完全な DNS 名 (たとえば、`<listener_server>.fabrikam.com`) として指定します。 可用性グループのデータベースを使用するように Configuration Manager を構成すると、この名前が使用されます。

    - **[最初のデータの同期を選択]** ページで、 **[完全]** を選びます。 ウィザードでは、可用性グループが作成された後に、プライマリ データベースおよびトランザクション ログがバックアップされます。 それから、セカンダリ レプリカをホストする各サーバーで復元されます。

        > [!Note]  
        > この手順を使用しない場合は、セカンダリ レプリカをホストする各サーバーにサイト データベースのコピーを復元します。 その後、そのデータベースを手動でグループに参加させます。

5. 各レプリカで構成を確認します。

    1. サイト サーバーのコンピューター アカウントが、可用性グループのメンバーである各コンピューターのローカル**管理者**グループのメンバーであることを確認します。  

    2. [検証スクリプト](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites)を実行し、各レプリカのサイト データベースが正しく構成されていることを確認します。

    3. セカンダリ レプリカで構成を設定する必要がある場合は、続行する前に、プライマリ レプリカをセカンダリ レプリカに手動でフェールオーバーします。 構成できるのはプライマリ レプリカのデータベースだけです。 詳細については、SQL Server ドキュメントの「[可用性グループの計画的な手動フェールオーバーの実行](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server)」を参照してください。

6. すべてのレプリカが要件を満たすようになったら、Configuration Manager で可用性グループを使用する準備は完了です。


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> 可用性グループを使用するようにサイトを構成する

[可用性グループを作成して構成](#bkmk_create)した後、Configuration Manager サイトのメンテナンスを使用して、可用性グループでホストされているデータベースを使用するようにサイトを構成します。

可用性グループのデータベースを使用して新しいサイトをインストールすることはサポートされていません。 たとえば、ベースライン メディアを使用する場合は、SQL Server の単一のインスタンスを使用してサイトをインストールします。 サイトのインストール後に、サイト データベースを可用性グループに移動します。

1. Configuration Manager サイトのインストール フォルダーから **Configuration Manager セットアップ** (`\BIN\X64\setup.exe`) を実行します。

2. **[はじめに]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** を選択し、 **[次へ]** を選びます。

3. **[SQL Server の構成を変更する]** を選択してから、 **[次へ]** を選びます。

4. サイト データベースの次の設定を再構成します。

    - **SQL Server 名**:可用性グループ *リスナー*の仮想名を入力します。 可用性グループの作成時にリスナーを構成しました。 仮想名は、`<Listener_Server>.fabrikam.com` のような、完全 DNS 名である必要があります。  

    - **インスタンス:** 可用性グループの*リスナー*の既定のインスタンスを指定するには、この値を空白にする必要があります。 現在のサイト データベースが名前付きインスタンスで実行されている場合は、現在の名前付きインスタンスをクリアします。

    - **データベース:** 表示される名前のままにします。 この名前は、現在のサイト データベースです。

5. 新しいデータベースの場所の情報を入力した後、通常のプロセスと構成でセットアップを完了します。


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> 同期レプリカ メンバー  

可用性グループでサイト データベースがホストされている場合、次の手順で同期レプリカ メンバーの追加と削除を行います。 サポートされているレプリカの種類と数の詳細については、[可用性グループの構成](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations)に関するページを参照してください。

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a> 新しい同期レプリカ メンバーを追加する

<!--3127336-->
バージョン 1906 以降では、Configuration Manager セットアップを実行して、新しい同期レプリカ メンバーを追加します。

1. SQL Server の手順を使ってセカンダリ レプリカを追加します。

    1. [Always On 可用性グループにセカンダリ レプリカを追加します](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)。

    1. SQL Management Studio でステータスを監視します。 可用性グループが完全な正常性に戻るまで待ちます。

1. Configuration Manager セットアップを実行し、サイトを変更するオプションを選択します。

1. データベース名として可用性グループ リスナーの名前を指定します。 リスナーで標準以外のネットワーク ポートが使用されている場合、それも指定します。 この操作によって、各ノードが正しく構成されます。 また、データベースの復旧プロセスが開始されます。

Configuration Manager セットアップでは、SQL データベースの移動操作を使用し、ノードが正しく構成されていることを確認します。

バージョン 1902 以前でこのプロセスを手動で実行する方法の詳細については、「[ConfigMgr 1702:既存の SQL AO AG に新しいノード (セカンダリ レプリカ) を追加する](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960)」を参照してください。

### <a name="remove-a-replica-member"></a>レプリカ メンバーを削除する

バージョン 1906 以降では、Configuration Manager セットアップを使用して、レプリカ メンバーを削除することができます。 同じプロセスを使用して、[新しい同期レプリカ メンバーを追加](#bkmk_sync-add)します。

バージョン 1902 以前でこのプロセスを手動で実行する方法の詳細については、[可用性グループからのセカンダリ レプリカの削除](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server)に関するページを参照してください。  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> 非同期レプリカ

Configuration Manager で使用する可用性グループでは、非同期レプリカを利用できます。 同期レプリカの構成に必要な構成スクリプトを実行する必要はありません。これは、サイト データベースで非同期レプリカがサポートされていないためです。

### <a name="configure-an-asynchronous-commit-replica"></a>非同期コミット レプリカを構成する

詳細については、[可用性グループへのセカンダリ レプリカの追加](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)に関するページを参照してください。

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>非同期レプリカを使用してサイトを回復する

非同期レプリカを使用してサイト データベースを回復します。

1. アクティブなプライマリ サイトを停止して、サイト データベースへの追加の書き込みを防止します。 サイトを停止するには、[階層のメンテナンス ツール](../../manage/hierarchy-maintenance-tool-preinst.exe.md) (`preinst.exe /stopsite`) を使用します

1. サイトを停止した後、[手動で回復したデータベース](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered)ではなく、非同期レプリカを使用します。


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a> 可用性グループの使用を停止する

可用性グループでサイト データベースをホストする必要がなくなったときには、次の手順に従います。 このプロセスでは、サイト データベースを SQL Server の単一インスタンスに戻します。

1. `preinst.exe /stopsite` コマンドを使用して、Configuration Manager サイトを停止します。 詳細については、[階層のメンテナンス ツール](../../manage/hierarchy-maintenance-tool-preinst.exe.md)に関するページを参照してください。

2. SQL Server を使用して、プライマリ レプリカからサイト データベースの完全バックアップを作成します。 詳細については、[データベースの完全バックアップの作成](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)に関するページを参照してください。

3. SQL Server を使用して、サイト データベースをホストするサーバーにサイト データベースのバックアップを復元します。 詳細については、「[SSMS を使用してデータベース バックアップを復元する](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)」を参照してください。

    > [!Note]  
    > 可用性グループのプライマリ レプリカ サーバーでサイト データベースの単一インスタンスをホストする場合は、この手順をスキップします。

4. サイト データベースをホストするサーバーで、サイト データベースのバックアップ モデルを **FULL** から **SIMPLE** に変更します。 詳細については、[データベースの復旧モデルの表示または変更](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)に関するページを参照してください。

5. Configuration Manager サイトのインストール フォルダーから **Configuration Manager セットアップ** (`\BIN\X64\setup.exe`) を実行します。

6. **[はじめに]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** を選択し、 **[次へ]** を選びます。  

7. **[SQL Server の構成を変更する]** を選択してから、 **[次へ]** を選びます。  

8. サイト データベースの次の設定を再構成します。

    - **SQL Server 名:** サイト データベースを現在ホストするサーバーの名前を入力します。

    - **インスタンス:** サイト データベースをホストする名前付きインスタンスを指定します。 データベースが既定のインスタンスにある場合は、このフィールドを空白のままにします。

    - **データベース:** 表示される名前のままにします。 この名前は、現在のサイト データベースです。

9. 新しいデータベースの場所の情報を入力した後、通常のプロセスと構成でセットアップを完了します。 セットアップが完了すると、サイトが再起動され、新しいデータベースの場所の使用が開始されます。

10. 可用性グループのメンバーだったサーバーをクリーンアップする場合は、[可用性グループの削除](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server)に関するページのガイダンスに従ってください。