---
title: Desktop Analytics の更新プログラム
titleSuffix: Configuration Manager
description: Desktop Analytics のセキュリティおよび機能の更新プログラムについて説明します。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec510414f11aa312e6c1a7d1d5bfa8126f473fe3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706580"
---
# <a name="updates-in-desktop-analytics"></a>Desktop Analytics の更新プログラム

Desktop Analytics ポータルで、セキュリティおよび機能の更新プログラムの状態を確認します。 Desktop Analytics メイン メニューの [監視] グループでこれらのノードを選択します。 これらのノードから、環境内のこれらの更新プログラムの状態に関する分析情報が得られます。


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

Windows 10 デバイスが Microsoft アカウントによる "*認証を受けていない*" 場合、Windows からはこのデータが報告されません。 通常、この認証は、Windows セットアップの組み込みエクスペリエンス (OOBE) の一部として完了しています。<!-- 5148153 -->


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

Windows 10 デバイスが Microsoft アカウントによる "*認証を受けていない*" 場合、Windows からはこのデータが報告されません。 通常、この認証は、Windows セットアップの組み込みエクスペリエンス (OOBE) の一部として完了しています。<!-- 5148153 -->


## <a name="next-steps"></a>次のステップ

- [Desktop Analytics の資産の詳細](about-assets.md): デバイス、ドライバー、およびアプリ  

- [展開計画の詳細情報](about-deployment-plans.md)  
