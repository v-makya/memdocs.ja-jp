---
title: 階層の監視
titleSuffix: Configuration Manager
description: Configuration Manager コンソールの [監視] ワークスペースを使用して、Configuration Manager のインフラストラクチャを監視します。
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 504943df58c0471a0ef821a269cc22b2d12d76d8
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068040"
---
# <a name="monitor-the-hierarchy"></a>階層の監視

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の階層を監視するには、Configuration Manager コンソールの **[監視]** ワークスペースを使用します。  

> [!NOTE]  
> サイトを移行する場合、この場所に関して例外があります。 **[管理]** ワークスペースの **[移行]** ノードでこのプロセスを監視します。 詳細については、「[Configuration Manager Current Branch に移行するための操作](../../migration/operations-for-migration.md)」を参照してください。  

監視のために Configuration Manager コンソールを使用すると共に、次の機能を使用します。

- [レポートの概要](introduction-to-reporting.md)
- [ログ ファイル](../../plan-design/hierarchy/log-files.md).  

サイトを監視するときは、問題発生の兆候があるかどうかに注意します。 次に例を示します。  

- サイト サーバーとサイト システムにあるファイルのバックログ  

- エラーまたは問題を示すステータス メッセージ  

- サイト間の通信障害  

- サーバーのシステム イベント ログのエラー メッセージと警告メッセージ  

- Microsoft SQL Server エラー ログのエラー メッセージと警告メッセージ  

- 状態を長期間レポートしていないサイトまたはクライアント  

- SQL Server データベースの応答の遅延  

- ハードウェア障害の兆候  

監視タスクによって問題の兆候が明らかになった場合は、問題の原因を調査してください。 その後、サイト障害のリスクを最小限に抑えるために、迅速に修復します。  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a> 一般的な管理タスクの監視

Configuration Manager コンソールには監視機能が組み込まれています。

### <a name="alerts"></a>アラート

詳細については、「[アラートを監視する](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts)」を参照してください。  

### <a name="compliance-settings"></a>コンプライアンス設定

詳細については、「[コンプライアンス設定を監視する方法](../../../compliance/deploy-use/monitor-compliance-settings.md)」をご覧ください。

### <a name="content"></a>Content

コンテンツ監視に関する一般的な情報については、[コンテンツ インフラストラクチャとコンテンツの管理](../deploy/configure/manage-content-and-content-infrastructure.md)に関するページを参照してください。  

特定の種類のコンテンツの監視については、以下を参照してください。

- [アプリケーションの監視](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [パッケージとプログラムを監視する](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [ソフトウェア更新プログラムのコンテンツを監視する](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [OS デプロイのコンテンツを監視する](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Endpoint Protection

詳細については、[Endpoint Protection の監視方法](../../../protect/deploy-use/monitor-endpoint-protection.md)に関するページを参照してください。  

### <a name="os-deployment"></a>OS の展開

詳細については、[OS デプロイの監視](../../../osd/deploy-use/monitor-operating-system-deployments.md)に関するページを参照してください。

### <a name="monitor-power-management"></a>電源管理の監視

「[電源管理を監視して計画する方法](../../clients/manage/power/monitor-and-plan-for-power-management.md)」を参照してください。  

### <a name="monitor-software-metering"></a>ソフトウェア使用状況測定の監視

詳細については、[ソフトウェア使用状況測定によるアプリの使用状況の監視](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)に関するページを参照してください。  

### <a name="monitor-software-updates"></a>ソフトウェア更新プログラムの監視

詳細については、「[Monitor software updates](../../../sum/deploy-use/monitor-software-updates.md)」 (ソフトウェア更新プログラムの監視) を参照してください。  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a> サイト階層の監視

**[監視]** ワークスペースの **[サイト階層]** ノードには、Configuration Manager の階層とサイト間のリンクの概要が表示されます。 

**[サイト階層]** ノードを使用して、各サイトの正常性を監視します。 サイト間レプリケーション リンクや、外的な要因 (地理的な場所など) との関係も監視します。  

サイトの状態とサイト間リンクの状態は、グローバル データではなくサイト データとしてレプリケートされます。 Configuration Manager コンソールを子プライマリ サイトに接続すると、他のプライマリ サイトやその子セカンダリ サイトのサイトの状態またはリンクの状態は表示されません。 たとえば、複数のプライマリ サイトを含む階層では、コンソールをプライマリサイトに接続すると、子セカンダリ サイト、プライマリ サイト、および中央管理サイトの状態を表示できます。 このビューでは、中央管理サイトの下にある他のサイトの状態を確認することはできません。  

**[サイト階層]** ノードの表示を制御するには、**[設定の構成]** アクションを使用します。 階層によって、このノードで構成する設定がレプリケートされます。  

### <a name="hierarchy-diagram"></a>階層図

階層図は、サイトをトポロジ マップで表示します。 サイトを選択すると、そのサイトのステータス メッセージの概要が表示されます。 ドリルスルーしてステータス メッセージを表示し、サイトの **[プロパティ]** にアクセスします。  

サイトまたはサイト間のレプリケーション リンクの状態の概要を表示するには、オブジェクト上にマウス ポインターを置きます。 レプリケーション リンクの状態はグローバルにレプリケートされません。 階層内のすべてのプライマリ サイト間のレプリケーション リンクの詳細を表示するには、コンソールを中央管理サイトに接続します。  

次のオプションを使用すると、階層図が変更されます。  

#### <a name="groups"></a>グループ

階層図の変更を引き起こすプライマリ サイトとセカンダリ サイトの数を構成します。 表示のこの変更により、複数のサイトが 1 つのオブジェクトに結合されます。 このとき、サイトの合計数、ステータス メッセージのロールアップの概要、およびサイトの状態が表示されます。

#### <a name="favorite-sites"></a>お気に入りサイト

お気に入りサイトにする個々のサイトを指定します。 階層図内の星形のアイコンはお気に入りサイトを示します。 グループを使用するとき、お気に入りサイトは他のサイトと結合されません。 それらは常に個別に表示されます。  

### <a name="geographical-view"></a>地図

> [!IMPORTANT]
> 2020 年 8 月以降、この機能は非推奨となりました。 **[階層図]** オプションを使用してください。<!--8116777-->

地図は、各サイトの場所を地図上に表示します。 場所を指定して構成したサイトのみが表示されます。 このビューでサイトを選択すると、親サイトまたは子サイトへのレプリケーション リンクが表示されます。 階層図ビューとは異なり、このビューにサイトのステータス メッセージまたはレプリケーション リンクの詳細を表示することはできません。  

> [!NOTE]  
> 地図を使用するには、Configuration Manager コンソールを接続するコンピューターに Internet Explorer がインストールされていて、HTTP プロトコルを使用して Bing Maps にアクセスできる必要があります。  

次のオプションを使用すると、地図が変更されます。  

#### <a name="site-location"></a>サイトの場所

次のいずれかの種類を使用して、各サイトの地理的な場所を指定します。

- 番地
- 地名 (市の名前など)
- 緯度と経度の座標

たとえば、ワシントン州レドモンドの緯度と経度を使用する場合、**N 47 40 26.3572 W 122 7 17.4432** をサイトの場所として指定します。 緯度や経度の度、分、または秒を示す記号を指定する必要はありません。 Configuration Manager では、Bing Maps を使って地図上に場所が表示されます。 その後、地理的な場所を使用して階層を表示できます。 このビューでは、特定のサイトまたはサイト間レプリケーションに影響する可能性がある地理的な問題の分析情報が提供されます。  

場所を指定する場合、[場所] ボックスを使用して、階層内の特定のサイトを検索できます。 **** サイトを選択した状態で、 **[場所]** 列に都市名または住所で場所を入力します。 Configuration Manager は Bing Maps を使用して場所を見つけます。  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>次のステップ

[データベース レプリケーションの監視](monitor-replication.md)
