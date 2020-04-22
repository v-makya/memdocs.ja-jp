---
title: SQL レプリケーションの再初期化
titleSuffix: Configuration Manager
description: この図を使用して、Configuration Manager サイト間での SQL レプリケーションの再初期化のトラブルシューティングを開始します。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0e48f2c04e218a7f0eba1b7f06dec768edc8af4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699880"
---
# <a name="sql-replication-reinit"></a>SQL レプリケーションの再初期化

複数サイト階層では、Configuration Manager は SQL レプリケーションを使用してサイト間でデータを転送します。 詳細については、「[データベース レプリケーション](../../../plan-design/hierarchy/database-replication.md)」を参照してください。

次の図を使用して、SQL レプリケーションの再初期化のトラブルシューティングを開始します。

![SQL レプリケーションの再初期化をトラブルシューティングする図](media/sql-replication-reinit.svg)

## <a name="queries"></a>クエリ

この図では次のクエリが使用されます。

### <a name="check-if-site-is-in-maintenance-mode"></a>サイトがメンテナンス モードかどうかを確認する

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>再初期化を完了していないレプリケーショング ループを確認する

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>グローバル データを確認する

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>サイト データを確認する

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>次のステップ

- [グローバル データの再初期化](global-data-reinit.md)
- [サイト データの再初期化](site-data-reinit.md)
- [SQL の構成](sql-configuration.md)
