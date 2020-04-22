---
title: SQL レプリケーション
titleSuffix: Configuration Manager
description: この図を使用して、Configuration Manager サイト間での SQL レプリケーションのトラブルシューティングを開始します。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699860"
---
# <a name="sql-replication"></a>SQL レプリケーション

複数サイト階層では、Configuration Manager は SQL レプリケーションを使用してサイト間でデータを転送します。 詳細については、「[データベース レプリケーション](../../../plan-design/hierarchy/database-replication.md)」を参照してください。

次の図を使用して、リンクが失敗したときの SQL レプリケーションのトラブルシューティングを開始します。

![SQL レプリケーションをトラブルシューティングする図](media/sql-replication.svg)

## <a name="queries"></a>クエリ

この図では次のクエリが使用されます。

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>レプリケーション グループのリンクが低下または失敗の状態になっていないかを確認する

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>レプリケーション グループ リンクが最近計算されたかどうかを確認する

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>SQL メンテナンス モードを確認する

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>次のステップ

- [SQL レプリケーションの再初期化](sql-replication-reinit.md)
- [SQL パフォーマンス](sql-performance.md)
- [SQL の構成](sql-configuration.md)
