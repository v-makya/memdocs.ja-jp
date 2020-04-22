---
title: SQL の構成
titleSuffix: Configuration Manager
description: この図を使用して、Configuration Manager の SQL 構成のトラブルシューティングを開始します。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707620"
---
# <a name="sql-configuration"></a>SQL の構成

複数サイト階層では、Configuration Manager は SQL レプリケーションを使用してサイト間でデータを転送します。 詳細については、「[データベース レプリケーション](../../../plan-design/hierarchy/database-replication.md)」を参照してください。

次の図を使用して、SQL Service Broker に関連する SQL 構成のトラブルシューティングを開始します。

![SQL 構成をトラブルシューティングする図](media/sql-configuration.svg)

## <a name="queries"></a>クエリ

この図には、次のクエリとアクションが含まれます。

### <a name="check-if-sql-can-deliver-ssb-messages"></a>SQL が SSB メッセージを配信できるかどうかを確認する

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>修復処理

### <a name="remediate-the-issues-reported-from-transmission_status"></a>transmission_status から報告された問題を修復する

一般的な問題:

- ファイアウォールの構成
- ネットワークの構成
- SSB 証明書の間違った構成

### <a name="run-sql-profiler-to-trace-ssb-events"></a>SQL プロファイラーを実行して SSB イベントをトレースする

CA とプライマリ サイト データベースで SQL プロファイラーを実行して、SQL Service Broker に関連するイベントをトレースします。

- **Audit Broker Login**
- **Audit Broker Conversation**
- **Broker** カテゴリのイベント
