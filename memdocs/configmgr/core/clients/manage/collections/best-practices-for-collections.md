---
title: コレクションのベスト プラクティス
titleSuffix: Configuration Manager
description: Configuration Manager でコレクションとコレクションの評価を構成する際の推奨事項について説明します。
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ee640a70eea9f2e8470e852409911d28e542bc2
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663377"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Configuration Manager のコレクションのベスト プラクティス

*適用対象:Configuration Manager (Current Branch)*

一部のコレクション管理ガイダンスは矛盾する場合があります。 たとえば、パフォーマンス上の理由から、更新頻度の高いコレクションの数を制限する必要があります。 ただし、Configuration Manager のほとんどの機能はコレクションに依存しているため、コレクションを頻繁に更新すると便利です。 コレクションとコレクションの評価を設計および構成する際には、パフォーマンスへの影響とビジネス要件の両方を慎重に検討してください。

Configuration Manager のコレクションに関する以下のベスト プラクティスを使用してください。  

## <a name="configure-maintenance-window-for-updates"></a>更新プログラムのメンテナンス期間を構成する

デバイス コレクションのメンテナンス期間を構成して、Configuration Manager がソフトウェアをそれらのデバイスにインストールできる時間を制限することができます。 メンテナンス期間の構成で十分な時間が確保されていない場合、クライアントは重要なソフトウェア更新プログラムをインストールできない可能性があり、その結果、更新プログラムによって緩和される問題に対してクライアントが脆弱なままになります。

メンテナンス期間を計画するときに注意する必要がある重要な考慮事項は次のとおりです。

- 既定のソフトウェア更新プログラムの最長実行時間は 60 分です。
- 更新プログラムをインストールできるかどうかが Configuration Manager によって計算される場合、再起動のために、最大実行時間に 5 分が加えられます。
- メンテナンス期間の残りの期間は、ソフトウェア更新プログラムの最長実行時間に 5 分を加えた時間よりも長くする必要があります。

## <a name="avoid-frequent-collection-evaluation"></a>コレクションの評価を頻繁に行わない

完全なコレクションの評価を行うと、対象のコレクションだけでなく、更新が発生した場合にそのコレクションによって制限されているすべてのコレクションも評価されます。 また、限定コレクションが更新されると、スケジュールのないコレクションも評価されます。 そのため、一部のコレクションは想定よりも頻繁に評価される可能性があります。

ビジー状態の Configuration Manager 環境では、コレクションの評価が繰り返されないようにスケジュールを縮小することにより、コレクションの評価のパフォーマンスを向上させることができます。 階層の深いツリーでは、高位のコレクションの評価によって下位のコレクションの評価もトリガーされるので、ツリーの下位にあるコレクションほど、コレクションの評価頻度を減らすことができます。

## <a name="understand-the-collection-evaluation-graph"></a>コレクション評価グラフの概要

コレクション評価グラフのしくみに注意して、適切なコレクション構造を設計してください。 完全なコレクションの評価を使ってすべてのコレクションを常に更新することは避けてください。 増分更新コレクションがスケジュールに従って更新される場合、増分更新が有効になっていない参照元のコレクションは更新されない場合があります。 増分評価中に更新が発生すると、完全な評価ではコレクションが更新されず、そのサイクルのコレクション評価グラフが終了する場合があります。 この場合、参照元のコレクション評価は行われません。 詳細については、「[コレクション評価グラフ](collection-evaluation.md#collection-evaluation-graph)」を参照してください。

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a> 増分更新を制限する

多数のコレクションに対して増分更新を有効にすると、評価の遅延が発生する可能性があります。 増分更新されるコレクションの数を 200 に制限することをお勧めします。 具体的な数は以下によって変わります。

- コレクションの総数
- 階層内で、リソースが新しく追加または変更される頻度
- 階層内のクライアントの数
- 階層内のコレクション メンバーシップ規則の複雑さ

増分評価サイクルにかかる時間が構成された更新頻度よりも長くなる場合、Configuration Manager では常にコレクションの評価が処理されることになり、システム パフォーマンスに影響する可能性があります。 増分更新されるコレクションの数を減らすか、増分評価サイクル間の時間を長くしてください。

増分コレクションの影響の可能性を考慮して、コレクションを作成し、更新スケジュールを割り当てるためのポリシーまたは手順を用意することが重要です。 ポリシーに関する考慮事項の例を次に示します。

- セキュリティ スコープ、クライアント設定、およびメンテナンス期間に使用されるコレクションには、増分更新のみを使用します。 このようなコレクションの更新は、クライアントのリソースに対する動作とアクセスに影響します。
- ライセンスが承認されていないアプリケーションの場合は、アプリケーションを既存のコレクションにアドバタイズし、グローバル条件を使用して可用性を制限します。
- 完全なコレクションの更新がスケジュールされている他のコレクションについて、適切な期間の概要を作成します。

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>CAS からの大規模なツリーの評価を避ける

Configuration Manager 環境の中央管理サイト (CAS) では、コレクションのメンバーシップが評価されません。 コレクションを評価する唯一のサイトはプライマリ サイトです。 セカンダリ サイトは、プライマリ サイトからレプリケートしたデータのみを使用するプロキシとして機能します。

コレクションの更新を要求するために、CAS から各プライマリ サイトに要求が送信されます。 プライマリ サイトでは、コレクションが評価され、結果が CAS に送り返されます。 すべてのコレクションの評価手順がすべてのサイトにレプリケートされ、すべてのサイトですべてのコレクションが評価され、すべてのデータが CAS に返され、統合された後にのみ、コレクションの評価結果が表示されます。

次の図は、CAS から手動のコレクション更新が要求された場合のフローを示しています。

![CAS からのコレクションの手動更新](media/manual-collection-update-from-cas.png)

複数のプライマリ サイトがある CAS からのコレクションの更新には時間がかかることがあります。 コレクションが適切なタイミングで評価されない場合は、要求を繰り返したくなるものです。

コレクションの評価スレッドが始まり、評価グラフが読み込まれると、コレクション評価グラフが空になるまで評価は続行されます。 その後、スレッドが終了すると、次の評価に使用できるようになります。 ただし、スレッドでコレクションが評価されている間に別のコレクションの評価サイクルがキューに入ると、スレッドでは、"実行されなかった" サイクルの評価の試行がすぐに再開されます。

各評価メソッドは、それ自体のスレッドで実行されます。 スレッド内で、Configuration Manager によって同じコレクションのグラフ化が複数回試行される可能性があります。 この場合、Configuration Manager では 2 つ目以降の要求がドロップされます。

このようなシナリオを回避するには、特に複数のサイトがある CAS から作業する場合は、大規模なツリーの手動によるコレクションの評価を避けてください。

## <a name="consider-collection-depth-and-cross-referencing"></a>コレクションの深さと相互参照を考慮する

ビジネス要件とパフォーマンスのバランスをとるには、作成するコレクション構造と、他のコレクションに対する依存関係を理解することが重要です。 他のコレクションも参照する 1 つ以上のコレクションを参照する規則を使用してコレクションを作成すると、それらすべてのコレクションが評価され、コレクションのメンバーシップが作成されます。

Configuration Manager のコレクションの包含規則と除外規則を使用すると、カスタムの WQL クエリを作成するよりもコレクションを簡単に参照できます。 ただし、コレクションの包含と除外を使用した結果、パフォーマンスのコストが高くなる場合は、代わりに WQL クエリ メソッドを使用できます。

包含:

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

除外:

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>CEViewer を使用してコレクションの評価を監視する

[Collection Evaluation Viewer (CEViewer)](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer) を使用すると、評価されているコレクションの数と、各コレクションの更新にかかる時間を監視できます。 CEViewer は、サイト サーバー上の *CD.Latest* フォルダーにあります。

SQL で同様のチェックを手動で実行するには、次のクエリを使用できます。

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```


