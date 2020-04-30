---
title: 1610 のチェックリスト
titleSuffix: Configuration Manager
description: Configuration Manager バージョン 1610 に更新する前に、実行するアクションについて説明します。
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 25d0302c4c35f2c66ce06febde63809b4a11116c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688780"
---
# <a name="checklist-for-installing-update-1610-for-configuration-manager"></a>Configuration Manager の更新プログラム 1610 をインストールするためのチェックリスト

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の Current Branch を使用している場合、バージョン 1610 のコンソール内の更新プログラムをインストールし、階層をバージョン 1606 から更新できます。 階層でバージョン 1511、1602、1606 を実行している場合、バージョン 1610 に更新できます。

バージョン 1610 の更新プログラムを得るには、階層の最上位サイトでサービス接続ポイントのサイト システムの役割を利用する必要があります。 これはオンラインまたはオフライン モードで可能です。 階層で Microsoft からダウンロードした更新プログラム パッケージは、 **[管理] &gt; [概要] &gt; [クラウド サービス] &gt; [更新とサービス]** にあります。

-   更新プログラムが**利用可能**として掲載されているとき、インストールできます。 バージョン 1610 のインストール前に、[更新プログラム 1610 のインストールに関する](#about-installing-update-1610)次の情報と更新プログラムを開始する前に実行するアクションの[チェックリスト](#checklist)を確認します。

-   更新プログラムに**ダウンロード中**と表示され、変化がない場合、**hman.log** と **dmpdownloader.log** でエラーを確認してください。

    -   通常、サイト サーバーで **SMS_Executive** サービスを再起動し、更新プログラムの再配布ファイルのダウンロードを再開することもできます。

    -   別の一般的なダウンロード問題は、 `silverlight.dlservice.microsoft.com` と `download.microsoft.com` からのダウンロードがプロキシ サーバーの設定で禁止されているときに発生するものです。

更新プログラムのインストールの詳細については、「[コンソール内の更新プログラムとサービス](updates.md#bkmk_inconsole)」を参照してください。

Current Branch バージョンの詳細については、「[Configuration Manager の更新プログラム](updates.md)」の「[基準バージョンと更新プログラムのバージョン](updates.md#bkmk_Baselines)」を参照してください。

## <a name="about-installing-update-1610"></a>更新プログラム 1610 のインストールについて

**サイト:**  
更新プログラム 1610 は、階層の最上位サイトのみにインストールすることができます。 つまり、中央管理サイトがある場合はそこからインストールを開始します。そうでない場合は、スタンドアロン プライマリ サイトからインストールを開始します。 更新プログラムを最上位サイトでインストールすると、子サイトで次の更新動作が行われます。

-   中央管理サイトが更新プログラムのインストールを完了したら、子プライマリ サイトが更新を自動的に開始します。 サービス期間を使用して、サイトが更新プログラムをインストールするタイミングを制御することができます。 バージョン 1606 より前では、サービス期間はメンテナンス期間と呼ばれました。 詳細については、「[サイト サーバーのサービス ウィンドウ](service-windows.md)」を参照してください。

-   プライマリ親サイトが更新プログラムのインストールを完了したら、Configuration Manager コンソール内からセカンダリ サイトを手動で更新する必要があります。 セカンダリ サイト サーバーの自動更新はサポートされていません。

**サイト システムの役割:**  
サイト サーバーが更新プログラムをインストールすると、サイト サーバーにインストールされたサイト システムの役割と、リモート コンピューターにインストールされたサイト システムの役割が自動的に更新されます。 したがって、更新プログラムをインストールする前に、各サイト システム サーバーが新しい更新プログラムのバージョンの操作の新しい前提条件をすべて満たしていることを確認してください。

**Configuration Manager コンソール:**    
更新の完了後に Configuration Manager コンソールを初めて使用する場合、そのコンソールの更新を求められます。 これを行うには、コンソールをホストするコンピューターで Configuration Manager セットアップを実行し、コンソールを更新するオプションを選択する必要があります。 コンソールへの更新プログラムのインストールを遅らせないことをお勧めします。



## <a name="checklist"></a>チェックリスト

**すべてのサイトで、Configuration Manager のサポート対象のバージョンが実行されている:** 更新プログラム 1610 のインストールを始めるには、階層内の各サイトが、同じバージョンの Configuration Manager (バージョン 1511、1602、または 1606 のいずれか) を実行している必要があります。

**ソフトウェア アシュアランスまたは同等のサブスクリプション権利の状態を確認する:**    
更新プログラム 1610 をインストールするには、ソフトウェア アシュアランス (SA) 契約が必要です。 バージョン 1610 をインストールすると、**ソフトウェア アシュアランスの有効期限**を確認するためのオプションが **[ライセンス]** タブに表示されます。

この任意の値は、ライセンスの有効期限を知らせるリマインダーとして指定できるので便利です。将来、更新プログラムをインストールするときに表示されます。 バージョン 1606 構成基準メディアから Configuration Manager をインストールした場合、セットアップ中に、あるいはサイトのインストール後に **[階層設定]** の **[ライセンス]** タブで、この値を指定している可能性があります。

詳細については、「[Configuration Manager のライセンスとブランチ](../../understand/learn-more-editions.md)」を参照してください。

**サイト システム サーバーにインストールされた Microsoft .NET のバージョンを確認する:** サイトで更新プログラム 1610 がインストールされると、Configuration Manager によって、次のいずれかのサイト システムの役割をホストする各コンピューターに .NET Framework 4.5.2 が自動的にインストールされます (.NET Framework 4.5 以降がまだインストールされていない場合)。

-   登録プロキシ ポイント
-   登録ポイント
-   管理ポイント
-   サービス接続ポイント

このインストールにより、サイト システム サーバーが再起動保留中の状態になり、Configuration Manager コンポーネント ステータス ビューアーにエラーが報告される場合があります。 さらに、サーバーが再起動されるまで、サーバー上の .NET アプリケーションでランダムにエラーが発生する場合があります。

詳細については、「[サイトとサイト システムの前提条件](../../plan-design/configs/site-and-site-system-prerequisites.md)」をご覧ください。

**サイトと階層の状態を確認して、未解決の問題がないことを確認する:** サイトを更新する前に、サイト サーバー、サイト データベース サーバー、およびリモート コンピューターにインストールされているサイト システムの役割で、運用上のすべての問題を解決します。 運用上の問題があると、サイトの更新が失敗する可能性があります。

詳細については、「[Configuration Manager のアラートとステータス システムの使用](use-alerts-and-the-status-system.md)」を参照してください。

**サイト間でファイルとデータのレプリケーションを確認する:** サイト間のファイルとデータベースのレプリケーションが機能していて最新の状態であることを確認します。 遅延またはバックログにより、円滑で正常な更新が行われない場合があります。
データベース レプリケーションには、更新プログラムを開始する前に問題を解決するために、レプリケーション リンク アナライザーを使用できます。

詳細は、「[データベース レプリケーションの監視](monitor-replication.md)」トピックの「[レプリケーション リンク アナライザー](monitor-replication.md#BKMK_RLA)」を参照してください。

**サイト、サイト データベース サーバー、リモートのサイト システムの役割をホストするコンピューターのオペレーティング システムに適用できる、重要な更新プログラムすべてをインストールする:** Configuration Manager 用の更新プログラムをインストールする前に、該当する各サイト システムに重要な更新プログラムをインストールします。 更新のインストール時に再起動が必要な場合は、Configuration Manager の更新を開始する前に該当するコンピューターを再起動します。

**プライマリ サイトの管理ポイントのデータベース レプリカを無効にする:**    
Configuration Manager では、管理ポイントのデータベース レプリカが有効になっているプライマリ サイトを正常に更新することはできません。 データベースのレプリケーションを無効にしてから、Configuration Manager の更新プログラムをインストールしてください。

詳しくは、「[Configuration Manager の管理ポイントのデータベース レプリカ](../deploy/configure/database-replicas-for-management-points.md)」をご覧ください。

**SQL Server AlwaysOn 可用性グループを手動フェールオーバーに設定する:**    
バージョン 1610 などの更新プログラムをインストールする前に、可用性グループで手動フェールオーバーを必ず設定してください。 サイト更新後に、自動フェールオーバーに復元できます。 詳細については、[サイト データベースの SQL Server AlwaysOn](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) に関するページを参照してください。

**NLB を使用するソフトウェアの更新ポイントを再構成する:**    
Configuration Manager では、ネットワーク負荷分散 (NLB) クラスターを使用してソフトウェアの更新ポイントをホストしているサイトは、更新できません。

ソフトウェアの更新ポイントに NLB クラスターを使用している場合、Windows PowerShell を使用して NLB クラスターを削除してください。
詳細については、[ソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md)に関するページを参照してください。

**サイトの更新インストール時に各サイトですべてのサイト メンテナンス タスクを無効にする:**    
更新プログラムをインストールする前に、更新プロセスがアクティブになっている間にそのサイトで実行される可能性があるサイトのメンテナンス タスクをすべて無効にします。 次のタスクが含まれますが、これらのタスクに限定されません。

-   サイト サーバーのバックアップ
-   期限切れのクライアント操作を削除
-   期限切れの探索データの削除

更新プログラムのインストール中にサイト データベースのメンテナンス タスクを実行すると、更新プログラムのインストールが失敗することができます。 タスクを無効にする前に、更新プログラムをインストールした後で構成を復元できるように、タスクのスケジュールを記録してください。

詳細については、「[Configuration Manager のメンテナンス タスク](maintenance-tasks.md)」および「[Configuration Manager のメンテナンス タスクのリファレンス](reference-for-maintenance-tasks.md)」を参照してください。

**Configuration Manager サーバー上でウイルス対策ソフトウェアを一時的に停止する:** サイトを更新する前に、Configuration Manager サーバー上でウイルス対策ソフトウェアを確実に停止します。 <!--SMS.503481-->

**中央管理サイトとプライマリ サイトのサイト データベースのバックアップを作成する:** サイトを更新する前に、サイト データベースをバックアップして、ディザスター リカバリーに使用する正常なバックアップを確実に作成できるようにします。

詳細については、[Configuration Manager のバックアップと回復](backup-and-recovery.md)に関するページを参照してください。

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**クライアントのパイロット運用を計画する:**    
クライアントを更新する更新プログラムをインストールすると、すべてのアクティブなクライアントを展開してアップグレードする前に、実稼働前環境でその新しいクライアントの更新プログラムをテストできます。

このオプションを活用するには、更新プログラムのインストールを開始する前に、実稼働前環境の自動アップグレードをサポートするサイトを構成する必要があります。

詳細については、「[クライアントをアップグレードする](../../clients/manage/upgrade/upgrade-clients.md)」および「[System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストする方法](../../clients/manage/upgrade/test-client-upgrades.md)」を参照してください。

**サービス期間を使用する計画を立て、サイトが更新プログラムをインストールするタイミングを制御する:**    
サイト サーバーに対する更新プログラムをインストールできる期間は、サービス期間を使用して定義することができます。

これは、階層内のサイトが更新プログラムをインストールするタイミングの制御に役立ちます。 バージョン 1606 より前では、サービス期間はメンテナンス期間と呼ばれました。 詳細については、「[サイト サーバーのサービス ウィンドウ](service-windows.md)」を参照してください。

**セットアップ前提条件チェッカーを実行する:**    
更新プログラムが**利用可能**としてコンソールに表示されているとき、更新プログラムのインストール前に、前提条件チェッカーを別個に実行できます。 (サイトへの更新プログラムのインストール時に、前提条件チェッカーが再度実行されます。)

前提条件の確認をコンソールから実行するには、 **[管理]、[概要]、[クラウド サービス]、[更新とサービス]** の順に選択します。 次に、 **[Configuration Manager 1610 update package (Configuration Manager 1610 更新プログラム パッケージ)]** を右クリックし、 **[前提条件チェックを実行]** を選択します。

前提条件チェックを開始して監視する方法の詳細については、「**手順 3:更新プログラムをインストールする前の前提条件チェッカーの実行**」 (トピック「[Configuration Manager のコンソール内更新プログラムのインストール](install-in-console-updates.md)」内) を参照してください。

> [!IMPORTANT]  
> 前提条件チェッカーを更新プログラムの一部として、または単独で実行すると、サイト メンテナンス タスクに使用される一部の製品ソース ファイルが更新されます。 このため、前提条件チェッカーを実行した後で、1610 更新プログラムをインストールする前に、サイト メンテナンス タスクを実行する必要がある場合は、サイト サーバーの CD.Latest フォルダーから **Setupwpf.exe** (Configuration Manager セットアップ) を実行する必要があります。

**サイトを更新する:** 階層の更新プログラムのインストールを開始する準備が整いました。 更新プログラムのインストールに関する情報については、「[コンソール内の更新プログラムのインストール](install-in-console-updates.md#bkmk_install)」を参照してください。

更新プログラムをインストールするプロセス、およびサイトのコンポーネントとサイト システムの役割を再インストールするアクションが業務に及ぼす影響が少ない場合は、各サイトの通常業務時間外に更新プログラムをインストールする計画を立てることをお勧めします。

詳細については、 [Configuration Manager の更新プログラム](updates.md)に関するページをご覧ください。
