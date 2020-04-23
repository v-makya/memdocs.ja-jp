---
title: Run Meter Summarization Tool
titleSuffix: Configuration Manager
description: Run Meter Summarization Tool を使用して、Configuration Manager でソフトウェア使用状況測定の概要作成タスクをトリガーします。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707540"
---
# <a name="run-meter-summarization-tool"></a>Run Meter Summarization Tool

*適用対象:Configuration Manager (Current Branch)*

Run Meter Summarization Tool は、[Configuration Manager ツール](tools.md)の 1 つです。 このツールを使用すると、プライマリ サイトでソフトウェア使用状況測定の概要作成のメンテナンス タスクをすぐにトリガーできます。 既定で、これらのタスクは**サイトのメンテナンス** タスクのスケジュールに従って実行され、毎日午前 12:00 から開始されます。 

これらのタスクは、**MeterData** SQL テーブルのデータの概要を作成し、その概要の結果を **FileUsageSummary** テーブルと **MonthlyUsageSummary** テーブルに書き込みます。 概要の結果は、ソフトウェア使用状況測定レポートに表示されます。 プライマリ サイト データベースに接続できるすべての Configuration Manager 管理ユーザーは、このツールを使用して概要作成を実行できます。 

このツールは、ソフトウェア使用状況測定データの概要作成タスクである **[ファイルの使用状況の概要]** と **[月ごとの使用状況の概要]** を実行します。 このツールは、通常の 12 時間の待機時間なしで、既存の使用状況データすべての概要を作成します。 このツールは、サイト データベースをホストする SQL サーバー上で実行されます。 概要作成が成功すると、終了コードは `0` に設定されます。 エラーがあった場合、終了コードは `1` に設定されます。



## <a name="usage"></a>使用方法

### <a name="command-line"></a>コマンド ライン

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>オプション

#### <a name="database-name"></a>データベース名
SQL Server 上のサイト データベースの名前。

#### <a name="delay-in-hours-for-summarization"></a>概要作成の遅延 (時間単位)
このツールは、遅延前に生成されたソフトウェア使用状況測定の概要を作成します。 既定で、この遅延はゼロです。


### <a name="example"></a>例

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>12 時間前に生成されたソフトウェア使用状況測定の概要を作成する

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>関連項目

- [メンテナンス タスク](../servers/manage/maintenance-tasks.md)
- [ソフトウェア使用状況測定でアプリの使用状況を監視する](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
