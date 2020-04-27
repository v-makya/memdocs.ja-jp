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
ms.openlocfilehash: f6207ed4eeeef892de38c85096d2cc80189214d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078560"
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

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>再初期化を完了していないレプリケーション グループを確認する

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
