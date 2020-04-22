---
title: グローバル データの再初期化
titleSuffix: Configuration Manager
description: この図を使用して、Configuration Manager 階層でのグローバル データの SQL レプリケーション再初期化のトラブルシューティングを開始します。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694300"
---
# <a name="troubleshoot-global-data-reinit"></a>グローバル データの再初期化をトラブルシューティングする

複数サイト階層では、Configuration Manager は SQL レプリケーションを使用してサイト間でデータを転送します。 詳細については、「[データベース レプリケーション](../../../plan-design/hierarchy/database-replication.md)」を参照してください。

次の図を使用して、Configuration Manager 階層でのグローバル データの SQL レプリケーション再初期化のトラブルシューティングを開始します。

![グローバル データの再初期化をトラブルシューティングする図](media/global-data-reinit.svg)

## <a name="queries"></a>クエリ

この図では次のクエリが使用されます。

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>サイト レプリケーションによる再初期化が完了していないかどうかを確認する

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>プライマリ サイトの TrackingGuid と状態を取得する

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>CAS の TrackingGuid と状態を取得する

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>追跡 ID の要求の状態を確認する

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>次のステップ

- [再初期化の不明メッセージ](reinit-missing-message.md)
