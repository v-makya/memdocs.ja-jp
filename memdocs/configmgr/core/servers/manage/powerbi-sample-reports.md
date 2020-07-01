---
title: Power BI サンプル レポートのインストール
titleSuffix: Configuration Manager
description: Power BI サンプル レポートを Configuration Manager にインストールする方法について説明します
ms.date: 06/25/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 39bec7e8b01b35a8411400399a74eb352406c023
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383191"
---
# <a name="install-power-bi-sample-reports"></a>Power BI サンプル レポートのインストール
<!--5679791-->
*適用対象:Configuration Manager (Current Branch)*

バージョン 2002 以降では、[Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started) を Configuration Manager レポートと統合できるようになりました。 Configuration Manager にインストールできる、ダウンロード可能なサンプル レポートがあります。 この記事では、Power BI サンプル レポートを Configuration Manager にインストールする方法について説明します。

## <a name="prerequisites"></a>[前提条件]

- [Power BI Report Server が統合された](powerbi-report-server.md) Configuration Manager レポート サービス ポイント
- [Microsoft Power BI Desktop (Power BI Report Server 向けに最適化 - 2019 年 9 月)](https://www.microsoft.com/download/details.aspx?id=57271) 以降

    > [!IMPORTANT]
    > - [Microsoft ダウンロード センター](https://www.microsoft.com/download/)の Power BI Desktop バージョンのみを使用し、Microsoft Store のバージョンは使用しないでください。
    > - [**Power BI Report Server 用に最適化済み**と記載されている Power BI Desktop](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop) のバージョンのみを使用してください。

## <a name="download-the-sample-reports"></a>サンプル レポートをダウンロードする

> [!IMPORTANT]
> 現在、サンプル レポートをダウンロードすることはできません。 報告された問題を修正するために、一時的に削除されました。

サンプル レポートをダウンロードするには:

1. Power BI サンプル レポートをダウンロードします<!-- from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=101452)-->。
1. `ConfigMgrSamplePowerBIReports.exe` ファイルを保存します。 
1. 別のデバイスからダウンロードした場合は、Microsoft Power BI Desktop (Power BI Report Server 向けに最適化) がインストールされているコンピューターにファイルを移動します。
1. `ConfigMgrSamplePowerBIReports.exe` ファイルを実行して、.pbit ファイルを抽出します。

## <a name="install-the-sample-reports"></a>サンプル レポートをインストールする

サンプル レポートをインストールするには:

1. Power BI Report Server 上で、Configuration Manager レポートのルート フォルダーに `Sample Reports` という名前の新しいフォルダーを作成します。
   
   :::image type="content" source="media/create-sample-reports-folder.png" alt-text="Configuration Manager レポートのルート フォルダーにサンプル レポート フォルダーを作成する" lightbox="media/create-sample-reports-folder.png":::


1. Microsoft Power BI Desktop (Power BI Report Server 向けに最適化) を起動します。
1. **[ファイル]** 、 **[開く]** の順に選択し、抽出した .pbit ファイルを保存した場所に移動します。
1. `ConfigMgrSamplePowerBIReports.exe` ファイルから抽出した .pbit ファイルのいずれかを選択します。
1. メッセージが表示されたら Configuration Manager データベース名とデータベース サーバー名を指定し、 **[読み込み]** を選択します。
   - データ モデルの読み込み時または適用時は、エラーが発生しても無視します。
   
    :::image type="content" source="media/sample-report-database.png" alt-text="データベースとデータベース サーバーの名前を指定する" lightbox="media/sample-report-database.png":::

1. レポート データが読み込まれたら、 **[ファイル]**  >  **[名前を付けて保存]** を選択した後、 **[Power BI Report Server]** を選択します。
   
   :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Power BI Report Server として保存する" lightbox="media/save-powerbi-report-server.png":::

1. レポート ポイント上に作成した `Sample Reports` フォルダーにレポートを保存します。
     
   :::image type="content" source="media/save-sample-report.png" alt-text="サンプル レポート フォルダーに保存する" lightbox="media/save-sample-report.png":::

1. その他のサンプル レポートについてもこの手順を繰り返します。 完了したら、Microsoft Power BI Desktop (Power BI Report Server 向けに最適化) を閉じます。
1. Configuration Manager コンソールで、 **[監視]**  >  **[Power BI レポート]**  >  **[サンプル レポート]** の順に移動します。
1. レポートの 1 つを右クリックし、 **[ブラウザーで実行]** を選択してレポートを起動します。

   :::image type="content" source="media/view-powerbi-report.png" alt-text="Configuration Manager コンソールからサンプル レポートを実行する" lightbox="media/view-powerbi-report.png":::

## <a name="next-steps"></a>次のステップ

[Power BI Report Server との統合](powerbi-report-server.md)
