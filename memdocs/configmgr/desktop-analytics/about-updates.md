---
title: Desktop Analytics の更新プログラム
titleSuffix: Configuration Manager
description: Desktop Analytics のセキュリティおよび機能の更新プログラムについて説明します。
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 96a014f4919480854b57bae82e982ce783f5f59b
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590968"
---
# <a name="updates-in-desktop-analytics"></a>Desktop Analytics の更新プログラム

Desktop Analytics ポータルで、セキュリティおよび機能の更新プログラムの状態を確認します。 Desktop Analytics メイン メニューの [監視] グループでこれらのノードを選択します。 これらのノードから、環境内のこれらの更新プログラムの状態に関する分析情報が得られます。

<!--7362999-->

> [!IMPORTANT]
> Desktop Analytics には、Desktop Analytics ワークスペースに関連付けられている商用 ID を持つデバイスのセキュリティと機能更新プログラムの状態が表示されます。 この動作は、デバイスを Configuration Manager に登録したかどうかに関係なく発生します。 これらのタイルの合計デバイス数が、[**接続済みサービス**](monitor-connection-health.md#commercial-id-configuration)に登録されているデバイスの数と一致しない可能性があります。

## <a name="security-updates"></a>セキュリティ更新プログラム

セキュリティ更新プログラムの現在の状態を確認するには、Desktop Analytics の **[監視]** セクションで **[セキュリティ更新プログラム]** を選択します。

![Desktop Analytics の [セキュリティ更新プログラム] ノード](media/security-updates.png)

このビューには、Windows 10 を実行しているデバイスの "*セキュリティ*" 更新プログラムの概要が表示されます。 横棒グラフには、デバイスが次のラベル別に分類されます。

#### <a name="latest"></a>最新

デバイスでは、そのバージョンとチャネル用の最新のセキュリティ更新プログラムが実行されています。

#### <a name="latest-1"></a>最新-1

デバイスでは、そのチャネルで利用可能な最新の更新プログラムよりも 1 つ古いバージョンのセキュリティ更新プログラムが実行されています。

#### <a name="older"></a>それより以前

デバイスでは、"最新-1" よりも古いセキュリティ更新プログラムが実行されています。

#### <a name="not-measured"></a>測定なし

Desktop Analytics でデバイスが評価されていません。 この状態には、Windows Insider プログラムに登録された Windows 7、Windows 8.1、または Windows 10 を実行しているデバイスが含まれます。  

セキュリティ更新プログラムの導入動向を確認するには、特定のバージョンの Windows について **[View More]\(詳細の表示\)** を選択します。 積み上げ面グラフでは、時間の経過と共にインストールされたセキュリティ更新プログラムごとにデバイスが分類されます。

セキュリティ更新プログラムの展開状態を確認するには、 **[すべて表示]** を選択します。 このビューには、デバイスが次のカテゴリで一覧表示されます。

- 未開始
- 進行中
- Completed
- 要注意 - デバイス (デバイス名で並べ替え)
- 要注意 - 問題 (問題の種類で並べ替え)

新しい情報がサービスがまだ処理中であるデバイスを表示するには、 **[最近のデータを表示]** を選択します。 次の完全なデータ更新後に、Desktop Analytics にこの情報が表示されます。

  > [!IMPORTANT]
  > **[最近のデータを表示]** の Desktop Analytics のオプションは非推奨です。 このアクションは、Desktop Analytics サービスの今後のリリースで削除される予定です。 詳しくは、「[非推奨の機能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)」をご覧ください。<!--7080949-->  

## <a name="feature-updates"></a>機能更新プログラム

機能更新プログラムの現在の状態を確認するには、Desktop Analytics の **[監視]** セクションで **[機能更新プログラム]** を選択します。

![Desktop Analytics の [機能更新プログラム] ノード](media/feature-updates.png)

このビューには、Windows 10 を実行しているデバイスの "*機能*" 更新プログラムの概要が表示されます。

サービス期間の詳細については、「[Windows ライフサイクルのファクト シート](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)」を参照してください。  

横棒グラフには、デバイスが次のラベル別に分類されます。

#### <a name="in-service"></a>サービス中

デバイスでは、そのバージョンとチャネル用の最新の機能更新プログラムが実行されています。  

#### <a name="near-end-of-service"></a>サービス終了間近

デバイスでは、90 日以内にサービス期間が終了する機能更新プログラムが実行されています。

#### <a name="end-of-service"></a>サービス終了

デバイスでは、サービス終了日を過ぎた機能更新プログラムが実行されています。 これらの日付は、Windows の Enterprise および Education エディションに固有のものです。 Home、Pro、Pro Education の各エディション、または Pro for Workstations エディションには適用されません。 詳細については、「[Windows ライフサイクルのファクト シート](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)」を参照してください。

#### <a name="not-measured"></a>測定なし

Desktop Analytics でデバイスが評価されていません。 この状態には、Windows Insider プログラムに登録された Windows 7、Windows 8.1、または Windows 10 を実行しているデバイスが含まれます。

タイルを選択すると、機能更新プログラムの導入動向が表示されます。 積み上げ面グラフでは、時間の経過と共にインストールされた機能更新プログラムごとにデバイスが分類されます。

## <a name="next-steps"></a>次のステップ

- [Desktop Analytics の資産の詳細](about-assets.md): デバイス、ドライバー、およびアプリ  

- [展開計画の詳細情報](about-deployment-plans.md)  
