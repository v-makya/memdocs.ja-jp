---
title: 再初期化の不明メッセージ
titleSuffix: Configuration Manager
description: この図を使用して、Configuration Manager で SQL レプリケーション再初期化の不明メッセージのトラブルシューティングを開始します。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703980"
---
# <a name="reinit-missing-message"></a>再初期化の不明メッセージ

複数サイト階層では、Configuration Manager は SQL レプリケーションを使用してサイト間でデータを転送します。 詳細については、「[データベース レプリケーション](../../../plan-design/hierarchy/database-replication.md)」を参照してください。

次の図を使用して、SQL レプリケーション再初期化での不足メッセージのトラブルシューティングを開始します。

![再初期化の不足メッセージをトラブルシューティングする図](media/reinit-missing-message.svg)

## <a name="queries"></a>クエリ

この図では次のクエリが使用されます。

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>サイト レプリケーションによる再初期化が完了していないかどうかを確認する

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>サブスクライバー サイトの TrackingGuid と状態を取得する

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>発行サイトの TrackingGuid と状態を取得する

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>修復処理

### <a name="version-1902-and-later"></a>バージョン 1902 以降

問題を検出して再初期化するには、[レプリケーション リンク アナライザー](../monitor-replication.md#BKMK_RLA)を実行します。

### <a name="version-1810-and-earlier"></a>バージョン 1810 以前

次の SQL クエリを実行して `ReplicationGroupID` を取得します。

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

その後、次の値を指定して、`InitializeData` メソッドを `SMS_ReplicationGroup` WMI クラスに対して使用します。

- ReplicationGroupID: 上記の SQL クエリから
- SiteCode1: 親サイト
- SiteCode2: 子サイト

詳細については、「[クラス SMS_ReplicationGroup の InitializeData メソッド](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md)」を参照してください。

#### <a name="example"></a>例

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>次のステップ

- [SQL レプリケーションの再初期化](sql-replication-reinit.md)
