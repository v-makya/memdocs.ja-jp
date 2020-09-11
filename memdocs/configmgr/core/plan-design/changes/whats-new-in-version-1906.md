---
title: バージョン 1906 の新機能
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch のバージョン 1906 で導入された変更点および新機能について説明します。
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d28d3ed697097b177ef9e2849fbcd6003505594c
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607802"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch のバージョン 1906 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1906 はコンソール内の更新プログラムとして利用できます。 バージョン 1802 以降が実行されているサイトで、この更新プログラムを適用します。 <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> この記事では、Configuration Manager バージョン 1906 での変更点と新機能をまとめます。  

この更新プログラムをインストールするための最新のチェックリストを常に確認してください。 詳細については「[更新プログラム 1906 をインストールするためのチェックリスト](../../servers/manage/checklist-for-installing-update-1906.md)」を参照してください。 サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist)に関するページも確認してください。

Configuration Manager の新機能をすべて利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

> [!Tip]  
> このページが更新されたときに通知を受け取るには、次の URL をコピーして RSS フィード リーダーに貼り付けます。`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>要件の変更

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>バージョン 1906 のクライアントでは、SHA-2 コード署名のサポートが必要です

<!--SCCMDocs-pr#3404-->
SHA-1 アルゴリズムの弱点と業界標準への整合性のため、Microsoft は、より安全な SHA-2 アルゴリズムを使用した Configuration Manager のバイナリにのみ署名するようになりました。 次の Windows OS バージョンでは、SHA-2 コード署名をサポートするための更新が必要です。

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

詳しくは、「[Windows クライアントの前提条件](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2)」をご覧ください。


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> サイトのインフラストラクチャ

### <a name="site-server-maintenance-task-improvements"></a>サイト サーバーのメンテナンス タスクの機能強化

<!--3555894-->
サイト サーバーのメンテナンス タスクを、サイト サーバーの詳細ビューでそれぞれのタブから表示し、編集できるようになりました。 新しい **[メンテナンス タスク]** タブには、次の情報があります。

- タスクが有効になっているかどうか
- タスク スケジュール
- 最後の開始時刻
- 最後の完了時間
- タスクが正常に完了したかどうか

![サイト サーバーの詳細ビューのメンテナンス タスク用の新しいタブ](./media/3555894-maintenance-tasks.png)

詳細については、[メンテナンス タスク](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906)に関するページを参照してください。

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Configuration Manager 更新時のデータベース アップグレード監視

<!--4200581-->
Configuration Manager 更新プログラムを適用するとき、インストール状況ウィンドウで **ConfigMgr データベースのアップグレード** タスクの状況を確認できるようになりました。

- データベースのアップグレードがブロックされている場合、 **[In progress, needs attention]\(処理中、要注意\)** という警告が表示されます。
   - cmupdate.log により、データベース アップグレードをブロックしている SQL からのプログラム名とセッション ID がログに記録されます。
- データベース アップグレードのブロックが終わると、ステータスが **[処理中]** または **[完了]** にリセットされます。
   - データベース アップグレードがブロックされると、データベースがまだブロックされているかどうか 5 分ごとに確認されます。

   ![インストール中のデータベース アップグレード監視](./media/4200581-database-upgrade-monitoring.png)

詳細については、[コンソール内の更新プログラムのインストール](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install)に関するページを参照してください。

### <a name="management-insights-rule-for-ntlm-fallback"></a>NTLM フォールバックの管理分析情報規則

<!--4572953-->
管理分析情報には、サイトにとって安全性が低い NTLM 認証フォールバック手法が有効になっているかどうかを検出する新しい規則、**NTLM のフォールバックが有効**が含まれます。

詳細については、[管理分析情報](../../servers/manage/management-insights.md#security)に関するページを参照してください。

### <a name="improvements-to-support-for-sql-always-on"></a>SQL Always On のサポートの強化

- セットアップから新しい同期レプリカを追加する<!--3127336-->:既存の SQL Always On 可用性グループに新しいセカンダリ レプリカ ノードを追加できるようになりました。 手動プロセスの代わりに、Configuration Manager 設定を使用し、この変更を行います。 詳しくは、[SQL Server Always On 可用性グループの構成](../../servers/deploy/configure/configure-aoag.md#bkmk_sync)に関するページを参照してください。

- マルチサブネット フェールオーバー<!-- SCCMDocs-pr#3734 -->:SQL Server で [MultiSubnetFailover 接続文字列キーワード](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover)を有効にできるようになりました。 サイト サーバーを手動で構成する必要もあります。 詳細については、[マルチサブネット フェールオーバー](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover)の前提条件に関するページを参照してください。

- 分散ビューのサポート<!-- SCCMDocs-pr#3792 -->:サイト データベースを SQL Server Always On 可用性グループでホストすることができ、データベース レプリケーション リンクでの[分散ビュー](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep)の使用を有効にすることができます。

    > [!Note]  
    > この変更は、SQL Server クラスターには適用されません。

- Site Recovery によって、SQL Always On グループにデータベースを再作成できます。 このプロセスは、手動と自動の両方のシード処理で機能します。<!-- SCCMDocs-pr#3846 -->

- 新しいセットアップの前提条件の確認:<!-- SCCMDocs-pr#3899 -->  

    - SQL 可用性グループ レプリカのシード処理モードはすべて同じでなければなりません
    - SQL 可用性グループ レプリカが正常である必要があります

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> クラウド接続の管理

### <a name="azure-active-directory-user-group-discovery"></a>Azure Active Directory ユーザー グループの探索

<!--3611956-->

Azure Active Directory (Azure AD) からユーザー グループとそのメンバーを検出できるようになりました。 サイトで以前に検出されていない Azure AD グループで見つかったユーザーは、Configuration Manager にユーザー リソースとして追加されます。 グループがセキュリティ グループのとき、ユーザー グループ リソース レコードが作成されます。 この機能は[プレリリース版の機能](../../servers/manage/pre-release-features.md)であり、有効にする必要があります。

詳しくは、[探索方法の構成](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)に関する記事をご覧ください。

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>コレクションのメンバーシップの結果の Azure Active Directory グループとの同期

<!--3607475-->

コレクション メンバーと Azure Active Directory (Azure AD) グループの同期が可能になりました。 この同期は、プレリリース機能です。 これを有効にする場合は、「[プレリリース機能](../../servers/manage/pre-release-features.md)」を参照してください。

同期により、コレクション メンバーシップの結果に基づいて Azure AD グループのメンバーシップを作成して、クラウドで既存のオンプレミスのグループ化規則を使用することができます。 Azure Active Directory レコードを持つデバイスのみが Azure AD に反映されます。 Hybrid Azure AD 参加済みデバイスと Azure Active Directory 参加済みデバイスの両方がサポートされます。

詳細については、[コレクションの作成](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)に関するページを参照してください。


## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

### <a name="readiness-insights-for-desktop-apps"></a>デスクトップ アプリの対応性に関する分析情報

<!-- 4021225 -->

基幹業務アプリを含むデスクトップ アプリケーションの詳細な分析情報を得ることができるようになりました。 以前の App Health Analyzer ツールキットは、Configuration Manager クライアントと統合されました。 この統合により、Desktop Analytics ポータルでのアプリ対応性分析情報の展開と管理が簡単になります。

詳しくは、「[Desktop Analytics での互換性評価](../../../desktop-analytics/compat-assessment.md#advanced-insights)」をご覧ください。


### <a name="dalogscollector-tool"></a>DALogsCollector ツール

<!--4622989-->
Desktop Analytics のトラブルシューティングを行うには、Configuration Manager のインストール ディレクトリの DesktopAnalyticsLogsCollector.ps1 ツールを使います。 いくつかの基本的なトラブルシューティング手順が実行され、関連するログが 1 つの作業ディレクトリに収集されます。

詳しくは、[ログ コレクター](../../../desktop-analytics/log-collector.md)に関する記事をご覧ください。


## <a name="real-time-management"></a><a name="bkmk_real"></a> リアルタイムの管理

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>CMPivot で結合、追加の演算子、およびアグリゲーターを追加する

<!--4054074-->

CMPivot では、新しい算術演算子、アグリゲーター、およびレジストリとファイルの併用などのクエリを結合する機能が追加されています。

詳細については、[CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1906) に関するページを参照してください。

### <a name="cmpivot-standalone"></a>CMPivot スタンドアロン

<!--3555890, 4619340, 4692885 -->

CMPivot をスタンドアロン アプリとして使用できるようになりました。 CMPivot スタンドアロンは、**プレリリース機能**で、英語でのみ利用できます。 CMPivot を Configuration Manager コンソールの外で実行して、環境内にあるデバイスの状態をリアルタイムで表示することができます。 この変更により、最初にコンソールをインストールしなくてもデバイスで CMPivot を使用できます。

CMPivot の機能を、ヘルプデスクやセキュリティ管理者など、コンソールをコンピューターにインストールしていない他のユーザーと共有できます。 他のユーザーは今まで使用していた他のツールと共に CMPivot を使用し、Configuration Manager にクエリを実行できます。 この充実した管理データを共有することで、職務をまたぐビジネス上の問題を同僚と共に事前解決できます。

詳しくは、[CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) に関する記事および「[プレリリース機能](../../servers/manage/pre-release-features.md#bkmk_table)」をご覧ください。

### <a name="added-permissions-to-the-security-administrator-role"></a>セキュリティ管理者ロールに追加されたアクセス許可

<!--4683130-->

次のアクセス許可が、Configuration Manager の組み込みの[**セキュリティ管理者**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles)ロールに追加されています。

- SMS スクリプトの読み取り
- コレクションでの CMPivot の実行
- インベントリ レポートの読み取り

詳細については、[CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot_secadmin1906) に関するページを参照してください。


## <a name="content-management"></a><a name="bkmk_content"></a> コンテンツ管理

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>クライアント データ ソース ダッシュボードでの配信最適化ダウンロード データ

<!--3555759-->
クライアント データ ソース ダッシュボードに[配信の最適化](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)が含まれるようになりました。 このダッシュボードを使用すると、クライアントが環境内のどこからコンテンツを取得しているのかを理解できます。

詳しくは、「[クライアント データ ソース ダッシュボード](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)」をご覧ください。

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>配信最適化のネットワーク内キャッシュ サーバーとして配布ポイントを使用する

<!--3555764-->
自分の配布ポイントで配信の最適化のネットワーク内キャッシュ サーバーをインストールできるようになりました。 このコンテンツをオンプレミスでキャッシュすることによって、クライアントは配信の最適化機能から恩恵を受けることができますが、お客様が WAN リンクを保護するのに役立てることができます。

このキャッシュ サーバーは、配信の最適化によってダウンロードされたコンテンツに対して、オンデマンドの透過型キャッシュとして機能します。 クライアント設定を使用して、このサーバーがローカルの Configuration Manager 境界グループのメンバーにのみ提供されるようにします。

詳細については、「[Configuration Manager の配信の最適化ネットワーク内キャッシュ サーバー](../hierarchy/microsoft-connected-cache.md)」を参照してください。


## <a name="client-management"></a><a name="bkmk_client"></a> クライアント管理

### <a name="support-for-windows-virtual-desktop"></a>Windows Virtual Desktop のサポート

<!--3556025-->
[Windows Virtual Desktop](/azure/virtual-desktop/) は Microsoft Azure と Microsoft 365 のプレビュー機能です。 Configuration Manager を使用し、Azure で Windows を実行しているこれらの仮想デバイスを管理できるようになりました。

ターミナル サーバーと同様に、これらの仮想デバイスでは、アクティブ ユーザーの同時実行セッションが複数許可されます。 クライアントのパフォーマンスを支援する目的で、Configuration Manager では、このような複数のユーザー セッションを許可するあらゆるデバイスでユーザー ポリシーが無効になりました。 ユーザー ポリシーを有効にした場合でも、Windows Virtual Desktop やターミナル サーバーを含む、これらのデバイスでは、クライアントによって既定でポリシーが無効化されます。

詳しくは、[クライアントとデバイスに対してサポートされる OS のバージョン](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers)に関する記事をご覧ください。

### <a name="support-center-onetrace-preview"></a>サポート センターの OneTrace (プレビュー)

<!--3555962-->
OneTrace は、サポート センターの新しいログ ビューアーです。 CMTrace と同様に機能しますが、以下の点が改善されています。

- タブ付きビュー
- ドッキング可能なウィンドウ
- 改善された検索機能
- ログ ビューを終了せずにフィルターを有効にする機能
- エラーのクラスターを素早く特定できるスクロールバーのヒント
- 大きなファイルの高速ログ オープン処理

![OneTrace ログ ビューアーのスクリーンショット](./media/3555962-onetrace.png)

詳しくは、「[サポート センターの OneTrace](../../support/support-center-onetrace.md)」をご覧ください。

### <a name="configure-client-cache-minimum-retention-period"></a>クライアントのキャッシュの最小保持期間の構成

<!--4485509-->
キャッシュされたコンテンツを Configuration Manager クライアントで維持する最小時間を指定できるようになりました。 このクライアント設定では、より多くの領域が必要な場合に、Configuration Manager エージェントがキャッシュからコンテンツを削除できるようになる前に待機する必要がある最小時間を定義します。 クライアント設定の **[クライアント キャッシュの設定]** グループで、 **[Minimum duration before cached content can be removed (minutes)]\(キャッシュされたコンテンツを削除できるようになるまでの最小期間 (最小)\)** を設定します。

> [!Note]  
> 同じクライアント設定グループで、 **[完全な OS 上の Configuration Manager クライアントでコンテンツを共有できるようにする]** ための既存の設定の名前が **[Enable as peer cache source]\(ピア キャッシュ ソースとして有効にする\)** に変更されました。 設定の動作は変更されません。  

詳細については、「[クライアントのキャッシュ設定](../../clients/deploy/about-client-settings.md#client-cache-settings)」を参照してください。


## <a name="co-management"></a><a name="bkmk_comgmt"></a> 共同管理

### <a name="improvements-to-co-management-auto-enrollment"></a>共同管理の自動登録の機能強化

- 新しい共同管理デバイスが、その Azure Active Directory (Azure AD) "*デバイス*" トークンに基づいて、Microsoft Intune サービスに自動的に登録されるようになりました。 自動登録を開始するのに、ユーザーがデバイスにサインインするのを待機する必要はありません。 この変更により、[登録状態](../../../comanage/how-to-monitor.md#co-management-enrollment-status)が "*ユーザー サインインの保留中*" のデバイスの数を減らすことができます。<!-- 4454491 -->

- 既に共同管理に登録されているデバイスがあるお客様の場合は、前提条件を満たせば、新しいデバイスがすぐに登録されるようになりました。 たとえば、デバイスが Azure AD に参加され、Configuration Manager クライアントがインストールされている場合などです。<!--4321130-->

詳しくは、[共同管理の有効化](../../../comanage/how-to-enable.md)に関する記事をご覧ください。

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>共同管理ワークロードの複数のパイロット グループ

<!--3555750-->
共同管理ワークロードごとに異なるパイロット コレクションを構成できるようになりました。 さまざまなパイロット コレクションを使うと、ワークロードをシフトするときに、さらに詳細な手法を利用できます。

- **[Enablement]\(有効化\)** タブで、 **[Intune Auto Enrollment]\(Intune 自動登録\)** コレクションを指定できるようになりました。
    - **[Intune Auto Enrollment]\(Intune 自動登録\)** コレクションには、共同管理に取り入れるすべてのクライアントを含める必要があります。 基本的には、その他すべてのステージング コレクションのスーパーセットになります。

- **[ステージング]** タブで、すべてのワークロードに 1 つのパイロット コレクションを使用する代わりに、ワークロード別にコレクションを選択できるようになりました。

    ![共同管理の [ステージング] タブでは、ワークロードごとにコレクションを選択できます](./media/3555750-co-management-staging-tab.png)

これらのオプションは、最初に共同管理を有効にするときにも利用できます。

詳しくは、[共同管理の有効化](../../../comanage/how-to-enable.md)に関する記事をご覧ください。

### <a name="co-management-support-for-government-cloud"></a>政府クラウド向けの共同管理のサポート

<!--4075452-->
米国政府機関のお客様は、Azure U.S. Government Cloud (portal.azure.us) で共同管理を使用できるようになりました。 詳しくは、[共同管理の有効化](../../../comanage/how-to-enable.md)に関する記事をご覧ください。


## <a name="application-management"></a><a name="bkmk_app"></a> アプリケーション管理

### <a name="filter-applications-deployed-to-devices"></a>デバイスに展開されたアプリケーションをフィルター処理する

<!--4451056-->
デバイスを対象としたアプリケーションの展開のユーザー カテゴリが、ソフトウェア センターでフィルターとして表示されるようになりました。 アプリケーションのプロパティの**ソフトウェア センター** ページで**ユーザー カテゴリ**を指定します。 次に、ソフトウェア センターでアプリを開き、使用可能なフィルターを確認します。

詳細については、「[アプリケーションの情報を手動で指定する](../../../apps/deploy-use/create-applications.md#bkmk_manual-app)」を参照してください。

### <a name="application-groups"></a>アプリケーション グループ

<!--3555907-->
1 つの展開としてユーザーまたはデバイス コレクションに送信できるアプリケーションのグループを作成します。 アプリ グループについて指定したメタデータは、ソフトウェア センターでは 1 つのエンティティとして表示されます。 アプリがクライアントに特定の順序でインストールされるように、グループ内のアプリに順序を付けることができます。

この機能はプレリリースです。 これを有効にする場合は、「[プレリリース機能](../../servers/manage/pre-release-features.md)」を参照してください。

詳しくは、「[アプリケーション グループの作成](../../../apps/deploy-use/create-app-groups.md)」をご覧ください。

### <a name="retry-the-install-of-pre-approved-applications"></a>事前承認済みアプリケーションのインストールの再試行

<!--4336307-->
ユーザーまたはデバイスに対して以前に承認したアプリのインストールを再試行できるようになりました。 承認オプションは、使用できる展開専用です。 ユーザーがアプリをアンインストールした場合、または初期インストール プロセスが失敗した場合、Configuration Manager ではその状態の再評価と再インストールは行われません。 この機能を使用すると、サポート技術者は、サポートを求めるユーザーのためにアプリのインストールをすばやく再試行できます。

詳しくは、「[Approve applications](../../../apps/deploy-use/app-approval.md)」(アプリケーションの承認) をご覧ください。

### <a name="install-an-application-for-a-device"></a>デバイスにアプリケーションをインストールする

<!--4402180-->
Configuration Manager コンソールから、アプリケーションをデバイスにリアルタイムでインストールできるようになりました。 この機能により、アプリケーションごとにコレクションを用意する必要性が減ります。

詳しくは、「[デバイスへのアプリケーションのインストール](../../../apps/deploy-use/install-app-for-device.md)」をご覧ください。

### <a name="improvements-to-app-approvals"></a>アプリの承認の機能強化

<!--4224910-->
このリリースには、アプリの承認に対する次の機能改善が含まれています。

- コンソールでアプリ要求を承認してから拒否した場合は、再度承認できるようになりました。 承認すると、アプリはクライアントに再インストールされます。  

- Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースの **[アプリケーション管理]** で、 **[承認要求]** ノードの名前が **[アプリケーションの要求]** に変更されています。<!-- SCCMDocs-pr#4028 -->

- アプリ承認要求を削除する新しい WMI メソッドの **DeleteInstance** があります。 このアクションでデバイスのアプリがアンインストールされることはありません。 まだインストールされていない場合、ユーザーはソフトウェア センターからアプリをインストールできません。

- **CreateApprovedRequest** API を呼び出して、デバイス上のアプリに対する事前承認済み要求を作成します。 クライアントにアプリが自動的にインストールされないようにするには、**AutoInstall** パラメーターを `FALSE` に設定します。 ソフトウェア センターにはアプリが表示されますが、自動的にはインストールされません。

詳しくは、「[Approve applications](../../../apps/deploy-use/app-approval.md)」(アプリケーションの承認) をご覧ください。


## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS の展開

### <a name="task-sequence-debugger"></a>タスク シーケンス デバッガー

<!--3612274-->
タスク シーケンス デバッガーは新しいトラブルシューティング ツールです。 デバッグ モードでタスク シーケンスを 1 つのデバイスのコレクションに展開します。 これで、制御された方法でタスク シーケンスをステップ実行し、トラブルシューティングと調査に利用できるようになります。

![タスク シーケンス デバッガーのスクリーンショット](./media/3612274-tsdebug.png)

この機能はプレリリースです。 これを有効にする場合は、「[プレリリース機能](../../servers/manage/pre-release-features.md)」を参照してください。

詳細については、「[タスク シーケンスのデバッグ](../../../osd/deploy-use/debug-task-sequence.md)」をご覧ください。

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>タスク シーケンス中にクライアント キャッシュからアプリのコンテンツを消去する

<!--4485675-->
**アプリケーションのインストール** タスク シーケンス ステップで、ステップの実行後、クライアント キャッシュからアプリのコンテンツを削除できるようになりました。

詳しくは、[タスク シーケンスのステップ](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication)に関する記事をご覧ください。

> [!Important]  
> この新しい機能をサポートするには、ターゲット クライアントを最新バージョンに更新します。

### <a name="reclaim-sedo-lock-for-task-sequences"></a>タスク シーケンスの SEDO のロックを再要求する

<!--3699337-->
Configuration Manager コンソールが応答しなくなった場合は、タスク シーケンスをそれ以上変更できないようにロックされている可能性があります。 ロックされているタスク シーケンスにアクセスしようとすると、**変更を破棄**して、オブジェクトの編集を続けられるようになりました。

詳細については、「[タスク シーケンス エディターを使用する](../../../osd/understand/task-sequence-editor.md#bkmk_sedo)」を参照してください。

### <a name="pre-cache-driver-packages-and-os-images"></a>ドライバー パッケージと OS イメージの事前キャッシュ

<!--4224642-->
タスク シーケンスの事前キャッシュに含まれるコンテンツの種類が増えました。 事前キャッシュ コンテンツは以前、OS アップグレード パッケージにのみ適用されていました。 それが今、事前キャッシュを使用し、以下のものによる帯域幅使用を減らすことができるようになりました。

- OS イメージ
- ドライバー パッケージ
- パッケージ

詳細については、「[コンテンツの事前キャッシュを構成する](../../../osd/deploy-use/configure-precache-content.md)」を参照してください。

### <a name="improvements-to-os-deployment"></a>OS 展開の機能強化

このリリースには、OS 展開に対する次の機能改善が含まれています。

- 次の 2 つの PowerShell コマンドレットを使用して、[タスク シーケンスの実行](../../../osd/understand/task-sequence-steps.md#child-task-sequence)ステップを作成および編集します。<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- タスク シーケンスを実行するときの変数の編集が簡単になりました。 タスク シーケンス ウィザード ウィンドウでタスク シーケンスを選択すると、タスク シーケンス変数を編集するページに **[編集]** ボタンが含まれるようになります。<!-- 4668846 --> 詳しくは、「[How to use task sequence variables](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz)」(タスク シーケンス変数の使い方) をご覧ください。

- **BitLocker の無効化**タスク シーケンス ステップに新しい再起動カウンターが追加されました。 このオプションを使用することで、BitLocker の無効状態を維持する再起動数を指定できます。 この変更により、タスク シーケンスを簡略化できます。 このステップの複数のインスタンスを追加する代わりに、1 つのステップを使用できます。 <!--4512937--> 詳細については、「[BitLocker の無効化](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker)」を参照してください。

- 新しいタスクシーケンス変数 **SMSTSRebootDelayNext** を、既存の [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) 変数と共に使います。 初回とは異なるタイムアウトで、後で再起動する場合は、この新しい変数を秒単位の別の値に設定します。 <!--4447680--> 詳しくは、[SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext) に関する記事をご覧ください。

- タスク シーケンスでは、新しい読み取り専用変数 **_SMSTSLastContentDownloadLocation** が設定されます。 この変数には、タスク シーケンスがダウンロードされた、またはコンテンツのダウンロードが試行された最後の場所が含まれています。 クライアントのログを解析する代わりに、この変数を検査します。<!-- 2840337 -->

- タスク シーケンス メディアを作成する場合、Configuration Manager によって autorun.inf ファイルが追加されることはありません。 通常、このファイルはマルウェア対策製品によってブロックされます。 自分のシナリオに必要な場合は、引き続きこのファイルを含めることができます。<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>PXE の改善

PXE DHCP ハンドシェイク中のオプション 82 が、WDS を使用せずに PXE レスポンダーでサポートされるようになりました。 オプション 82 は WDS ではサポートされません。


## <a name="software-center"></a><a name="bkmk_userxp"></a> ソフトウェア センター

### <a name="improvements-to-software-center-tab-customizations"></a>ソフトウェア センター タブのカスタマイズの機能強化

<!--4063773-->
ソフトウェア センターで最大 5 つのカスタム タブを追加できるようになりました。 ソフトウェア センターにこれらのタブが表示される順序も編集できます。

詳細については、[ソフトウェア センターのクライアント設定](../../clients/deploy/about-client-settings.md#software-center)に関するページを参照してください。

### <a name="software-center-infrastructure-improvements"></a>ソフトウェア センターのインフラストラクチャの改善

<!--3555950-->

このリリースには、ソフトウェア センターの次のインフラストラクチャ機能改善が含まれています。

- ユーザーが入手できるアプリについては、ソフトウェア センターで管理ポイントと通信できるようになりました。 今後、アプリケーション カタログは使用されません。 この変更により、サイトからアプリケーション カタログを簡単に削除できるようになりました。

- 以前は、ソフトウェア センターによって、利用できるサーバーの一覧から最初の管理ポイントが選択されました。 このリリース以降、クライアントにより使用されるものと同じ管理ポイントが使用されます。 この変更により、割り当てられたプライマリ サイトからの管理ポイントでクライアントのものと同じ管理ポイントをソフトウェア センターで使用できるようになりました。

> [!Important]  
> ソフトウェア センターと管理ポイントがこのように繰り返し改善されるのは、アプリケーション カタログの役割を廃止する目的で行われます。
>
> - Silverlight ユーザー エクスペリエンスは Current Branch バージョン 1806 以降、サポートされません。
> - バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。
> - アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  

詳しくは、「[アプリケーション カタログの削除](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)」および「[ソフトウェア センターの計画](../../../apps/plan-design/plan-for-software-center.md)」をご覧ください。

### <a name="redesigned-notification-for-newly-available-software"></a>新しく利用可能になったソフトウェアの再設計された通知

<!--3555904-->
**[新しいソフトウェアを利用できます]** 通知は、特定のアプリケーションとリビジョンでユーザーに対して 1 回のみ表示されます。 ユーザーがサインインするたびに表示されることはなくなりました。 アプリケーションが変更または再展開された場合にのみ、アプリケーションに対する別の通知が表示されます。

詳細については、「[アプリケーションの作成と展開](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience)」を参照してください。

### <a name="more-frequent-countdown-notifications-for-restarts"></a>再起動時のカウントダウンの通知頻度を上げる

<!--3976435-->

カウントダウンを周期的に通知することで、再起動の保留をエンド ユーザーに通知する頻度が増えました。 **[コンピューターの再起動]** ページの **[クライアントの設定]** で、間欠的な通知の間隔を定義できます。 最後のカウントダウン通知が発生するまで、保留中の再起動についてユーザーに通知する頻度を構成するには、 **[コンピューターの再起動のカウントダウン通知を再通知する期間を指定する (分)]** の値を変更します。

さらに、 **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)]** の最大値が、1440 分 (24 時間) から 20160 分 (2 週間) に増えました。

詳しくは、[デバイス再起動通知](../../clients/deploy/device-restart-notifications.md)および[クライアントの設定](../../clients/deploy/about-client-settings.md#computer-restart)に関する記事をご覧ください。

### <a name="direct-link-to-custom-tabs-in-software-center"></a>ソフトウェア センターのカスタム タブへの直接リンク

<!--4655176-->

ソフトウェア センターの[カスタム タブ](../../clients/deploy/about-client-settings.md#software-center-tab-visibility)への直接リンクをユーザーに提供できるようになりました。

ソフトウェア センターを開いて特定のタブに移動するには、次の URL 形式を使用します。

`softwarecenter:page=CustomTab1`

文字列 `CustomTab1` は、カスタム タブの順序の 1 番目です。

たとえば、Windows の **[実行]** ウィンドウにこの URL を入力します。

この構文を使用して、ソフトウェア センターの既定のタブを開くこともできます。

|コマンド ライン  |タブ  |
|---------|---------|
|`AvailableSoftware`|アプリケーション|
|`Updates`|更新プログラム|
|`OSD`|オペレーティング システム|
|`InstallationStatus`|インストールのステータス|
|`Compliance`|デバイスのポリシー準拠|
|`Options`|オプション|

詳しくは、「[ソフトウェア センターのタブの表示](../../clients/deploy/about-client-settings.md#software-center-tab-visibility)」をご覧ください。

## <a name="software-updates"></a><a name="bkmk_sum"></a> ソフトウェア更新プログラム

### <a name="additional-options-for-wsus-maintenance"></a>WSUS メンテナンスの追加オプション

<!--4110109-->
Configuration Manager を実行して正常なソフトウェア更新ポイントを維持できる WSUS メンテナンス タスクが追加されました。 WSUS のメンテナンスは、各同期後に行われます。 WSUS で更新が期限切れになる事態を減らすだけでなく、Configuration Manager では次のことができるようになりました。

- WSUS データベースから古い更新プログラムを削除します。
- WSUS データベースに非クラスター化インデックスを追加して、WSUS のクリーンアップのパフォーマンスを向上させます。

詳細については、「[ソフトウェア更新プログラムのメンテナンス](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906)」を参照してください。

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>ソフトウェア更新プログラムの既定の最大実行時間の構成

<!--3734426-->

ソフトウェア更新プログラムのインストール完了までの最長時間を指定できるようになりました。 ソフトウェアの更新ポイントの **[最長実行時間]** タブでは、次の項目を指定できます。

- **Windows の機能更新プログラムの最長実行時間 (分)**
- **Office 365 更新プログラムおよび Windows の機能以外の更新プログラムの最長実行時間 (分)**

詳細については、[ソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime)に関するページを参照してください。

### <a name="configure-dynamic-update-during-feature-updates"></a>機能の動的更新を設定する

<!--4062619-->

新しいクライアント設定を使用して、Windows 10 の機能更新プログラムのインストールの間に[動的更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)を構成します。 動的更新を設定すると、Windows セットアップ中に言語パック、オンデマンド機能、ドライバー、累積された更新プログラムをインストールできます。これは、クライアントに対して更新プログラムをインターネットからダウンロードするよう指示することで行われます。

詳しくは、[ソフトウェア更新プログラムのクライアント設定](../../clients/deploy/about-client-settings.md#software-updates)および [サービスとしての Windows の管理](../../../osd/deploy-use/manage-windows-as-a-service.md)に関する記事をご覧ください。

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Windows 10 バージョン 1903 以降の新しい製品カテゴリ

<!--4682946-->

**Windows 10 バージョン 1903 以降**は、以前のバージョンのように **Windows 10** の一部としてではなく、独自の製品として Microsoft Update に追加されました。 この変更により、クライアントでこれらの更新プログラムが確実に表示されるようにするための多くの手動のステップが発生しました。 弊社では、新製品のために実行する必要がある手動のステップの数の削減を支援してきました。

Configuration Manager バージョン 1906 に更新し、同期のために **Windows 10** 製品が選択されていると、次のアクションが自動的に行われます。

- **Windows 10 バージョン 1903 以降**の製品が同期のために追加されます。
- **Windows 10** 製品を含む自動展開規則が、**Windows 10 バージョン 1903 以降**が含まれるように更新されます。
- **Windows 10 バージョン 1903 以降**の製品を含めるため、サービス プランが更新されます。

詳しくは、「[同期する分類と製品の構成](../../../sum/get-started/configure-classifications-and-products.md)」、[サービス プラン](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)に関する記事、および[自動展開規則](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)に関する記事をご覧ください。

### <a name="drill-through-required-updates"></a>必要な更新プログラムをドリルスルーする

<!--4224414-->
特定のソフトウェア更新プログラムが必要なデバイスを確認するため、コンプライアンスに関する統計情報をドリルダウンできるようになりました。 デバイスの一覧を表示するには、更新プログラムとデバイスが属するコレクションを表示するアクセス許可が必要です。 デバイスの一覧にドリルダウンするには、更新プログラムの **[概要]** タブの円グラフの横にある **[必須項目の表示]** ハイパーリンクを選択します。 ハイパーリンクをクリックすると、更新プログラムが必要なデバイスを確認できる **[デバイス]** の下の一時ノードに移動されます。

**[必須項目の表示]** ハイパーリンクは、次の場所で使用できます。

   - **[ソフトウェア ライブラリ]**  >  **[ソフトウェア更新プログラム]**  >  **[すべてのソフトウェア更新プログラム]**
   - **[ソフトウェア ライブラリ]**  >  **[Windows 10 のサービス]**  >  **[すべての Windows 10 更新プログラム]**
   - **[ソフトウェア ライブラリ]**  >  **[Office 365 クライアント管理]**  >  **[Office 365 の更新プログラム]**

詳細については、[ソフトウェア更新プログラムの監視](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates)、[サービスとしての Windows の管理](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates)、[Microsoft 365 Apps の更新プログラムの管理](../../../sum/deploy-use/manage-office-365-proplus-updates.md)に関する記事をご覧ください。


## <a name="office-management"></a><a name="bkmk_o365"></a> Office 管理

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Office 365 ProPlus アップグレードの準備ダッシュボード

<!--4021125-->

Microsoft 365 Apps for enterprise へのアップグレードの準備ができているデバイスを特定するために、新しい準備ダッシュボードが用意されています。 これには、Configuration Manager の Current Branch バージョン 1902 でリリースされた **[Office 365 ProPlus upgrade readiness]\(Office 365 ProPlus アップグレード準備\)** タイルが含まれています。 Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[Office 365 クライアント管理]** を展開し、 **[Office 365 ProPlus Upgrade Readiness]\(Office 365 ProPlus アップグレード準備\)** ノードを選択します。

ダッシュボード、前提条件、このデータを使用方法について詳しくは、「[Office 365 ProPlus 準備の統合](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash)」をご覧ください。


## <a name="protection"></a><a name="bkmk_protect"></a> 保護

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Windows Defender Application Guard のファイルの信頼基準

<!--3555858-->

通常は Windows Defender Application Guard (WDAG) で開くファイルをユーザーが信頼できるようにする新しいポリシー設定があります。 正常に完了すると、WDAG ではなく、ホスト デバイスでファイルが開きます。

詳しくは、「[Windows Defender Application Guard ポリシーの作成と展開](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM)」をご覧ください。


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager コンソール

### <a name="role-based-access-for-folders"></a>フォルダーのロール ベースのアクセス

<!--3600867-->

フォルダーにセキュリティ スコープを設定できるようになりました。 フォルダー内のオブジェクトへのアクセス許可が与えられていても、フォルダーにアクセスできない場合、そのオブジェクトを表示できません。 同様に、フォルダーへのアクセス許可が与えられていても、その中のオブジェクトにアクセスできない場合、そのオブジェクトは表示できません。 フォルダーを右クリックし、 **[セキュリティ スコープの設定]** を選択して、適用するセキュリティ スコープを選びます。

詳しくは、[Configuration Manager コンソールのヒント](../../servers/manage/admin-console-tips.md)と[ロールベース管理の構成](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder)に関する記事をご覧ください。

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>デバイスおよびデバイス コレクション ノードに SMBIOS GUID 列を追加する

<!--4526580-->
**[デバイス]** および **[デバイス コレクション]** の両方のノードで、**SMBIOS GUID** の新しい列を追加できるようになりました。 この値は、[システム リソース] クラスの **[BIOS GUID]** プロパティと同じです。 これはデバイス ハードウェアの一意の識別子です。

### <a name="administration-service-support-for-security-nodes"></a>セキュリティ ノードに対する管理サービスのサポート

<!--4223683-->
Configuration Manager コンソールのいくつかのノードで管理サービスを使用できるようになりました。 この変更により、コンソールが WMI 経由の代わりに HTTPS 経由で SMS プロバイダーと通信できるようになります。

詳細については、「[管理サービス](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)」をご覧ください。

> [!Note]
> バージョン 1906 以降では、サイトのプロパティの **[クライアントコンピューターの通信方法]** タブは、 **[Communication Security]\(通信のセキュリティ\)** という名前になりました。<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>デバイス ノードの [コレクション] タブ

<!--4616810-->
**[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノードに移動し、デバイスを選択します。 詳細ウィンドウで、新しい **[コレクション]** タブに切り替えます。このタブには、このデバイスを含むコレクションが一覧表示されます。

> [!Note]  
> - 現在、このタブは **[デバイス コレクション]** ノード以下のデバイス サブノードからは使用できません。 たとえば、コレクションで **[メンバーの表示]** のオプションを選択した場合です。
> - このタブはユーザーによっては想定通りに設定されないことがあります。 デバイスが属しているコレクションの完全な一覧を表示するには、**完全な権限を持つ管理者**のセキュリティ ロールが必要です。 これは既知の問題です。 <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>アプリケーション ノードの [タスク シーケンス] タブ

<!--4616810-->
**[ソフトウェア ライブラリ]** ワークスペースの **[アプリケーション管理]** を展開し、 **[アプリケーション]** ノードに移動し、アプリケーションを選択します。 詳細ウィンドウで、新しい **[タスク シーケンス]** タブに切り替えます。このタブには、このアプリケーションを参照するタスク シーケンスが一覧表示されます。

### <a name="show-collection-name-for-scripts"></a>スクリプトのコレクション名を表示する

<!--4616810-->
**[監視]** ワークスペースで、 **[スクリプトのステータス]** ノードを選択します。 ID に加え、 **[コレクション名]** も表示されます。

### <a name="real-time-actions-from-device-lists"></a>デバイス一覧からのリアルタイム アクション

<!--4616810-->
**[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノード以下にデバイスの一覧を表示するには、さまざまな方法があります。

- **[資産とコンプライアンス]** ワークスペースで、 **[デバイス コレクション]** ノードを選択します。 デバイス コレクションを選択して、 **[メンバーの表示]** のアクションを選択します。 このアクションで、そのコレクションのデバイス一覧が表示される **[デバイス]** ノードのサブノードが開きます。  

  - コレクションのサブノードを選択すると、リボンの [コレクション] グループから **[CMPivot]** を開始できるようになります。  

- **[監視]** ワークスペースで、 **[展開]** ノードを選択します。 展開を選択し、リボンの **[状態の表示]** アクションを選択します。 展開の状態ウィンドウで、総資産をダブルクリックすると、デバイス一覧まで展開して表示されます。  

  - この一覧のデバイスを選択すると、リボンの [デバイス] グループから **[CMPivot]** と **[スクリプトの実行]** を開始できます。  

### <a name="order-by-program-name-in-task-sequence"></a>タスク シーケンスのプログラム名順

<!--4616810-->
**[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、 **[タスク シーケンス]** ノードを選択します。 タスク シーケンスを編集し、[[パッケージのインストール]](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) 手順を選択または追加します。 パッケージに複数のプログラムがある場合、ドロップダウン リストにはプログラムがアルファベット順に表示されます。

### <a name="correct-names-for-client-operations"></a>クライアント操作の正しい名前

<!--4616810-->
**[監視]** ワークスペースで **[クライアントの操作]** を選択します。 **[次のソフトウェアの更新ポイントに切り替える]** 操作が正しい名前になります。


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> 非推奨の機能とオペレーティング システム

[削除された項目と非推奨の項目](deprecated/removed-and-deprecated.md)で実装される前のサポートに関する変更点について説明します。

バージョン 1906 では、次の機能のサポートが廃止されます。  

- 新しいアプリケーション カタログの役割をインストールできなくなります。 更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 詳細については、[ソフトウェア センターの計画](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)に関するセクションを参照してください。

バージョン 1906 では、次の製品のサポートが非推奨になります。  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>その他の更新内容

このバージョンでは、次の機能はプレリリースではなくなりました。

- [SMS プロバイダーの管理サービス](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Windows Defender アプリケーション制御の管理](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

このリリースには、新機能に加え、バグ修正などの追加の変更も含まれています。 詳細については、「[Configuration Manager Current Branch バージョン 1906 での変更の概要](https://support.microsoft.com/help/4514258)」を参照してください。

Configuration Manager 向け Windows PowerShell コマンドレットの変更に関する詳細については、[PowerShell バージョン 1906 のリリース ノート](/powershell/sccm/1906-release-notes)を参照してください。

2019 年 10 月 1 日以降、コンソールで次の更新プログラムのロールアップ (4517869) を利用できるようになりました:[Configuration Manager Current Branch バージョン 1906 の更新プログラムのロールアップ](https://support.microsoft.com/help/4517869)。

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>次のステップ

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
2019 年 8 月 16 日より、バージョン 1906 は全世界のすべてのユーザーがインストールできるようになります。

このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラムのインストール](../../servers/manage/updates.md)に関する記事および「[1906 に更新するためのチェックリスト](../../servers/manage/checklist-for-installing-update-1906.md)」をご覧ください。

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用します。  
>
> 詳細については、下記のリンクをクリックしてください。
>
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md)  
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)  

既知の重大な問題については、[リリース ノート](../../servers/deploy/install/release-notes.md)を参照してください。

サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist)に関するページも確認してください。
