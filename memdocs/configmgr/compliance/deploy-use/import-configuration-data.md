---
title: 構成データのインポート
titleSuffix: Configuration Manager
description: 構成データは、キャビネット ファイル形式であり、サポートされている Service Modeling Language スキーマに準拠している場合にインポートできます。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 4f70a956051858fce5b4ba5f519c7e1035600793
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692410"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Configuration Manager による構成データのインポート

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager コンソールで構成基準と構成項目を作成するほか、構成項目がキャビネット (cab) ファイル形式で、サポートされる Service Modeling Language (SML) スキーマに準拠している場合は、構成データをインポートできます。 構成データのインポート元:  

- Microsoft または他のソフトウェア ベンダー サイトからダウンロードしたベスト プラクティス構成データ (構成パック)。  

- System Center 2012 Configuration Manager 以降からエクスポートされた構成データ。  

- 外部で作成され、SML スキーマに従う構成データ。  

  System Center 2012 Configuration Manager サイト サーバーの役割のコンプライアンスを管理するのに役立つ構成パックの例については、 [System Center 2012 Configuration Manager 構成パック](https://www.microsoft.com/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all)に関するページを参照してください。  

構成基準をインポートするとき、構成基準で参照される一部またはすべての構成項目をキャビネット ファイルにも含める必要がある場合があります。 インポート処理中に、Configuration Manager は、構成基準で参照されるすべての構成項目がキャビネット ファイルにも含まれているかどうかや、既に Configuration Manager に存在するかどうかを確認します。 構成基準のインポートを試みたときに、その構成基準が参照する構成データが見つからない場合は、そのインポート処理は失敗します。  

その他にも、次のようなシナリオでインポート処理が失敗することがあります。  

-   構成データが参照する構成データを、Configuration Manager が自身のデータベースおよびキャビネット ファイル自体から見つけられない。  

-   Configuration Manager データベース内に、同じ名前で同じ構成データ バージョンの構成データが既に存在しているが、コンテンツ バージョンが異なる。  

-   Configuration Manager データベース内に、同じコンテンツ バージョンの構成データが既に存在するが、ハッシュ計算では異なるデータとして識別される。  

-   Configuration Manager データベース内に、同じ名前で新しいバージョンの構成データが既に存在するか、最近削除された。  

-   マルチサイト Configuration Manager 階層で、構成データが最初に親サイトからインポートされた。 その構成データは、子サイトではなく、同じサイトから更新する必要があります。  

### <a name="import-configuration-data"></a>構成データのインポート  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[構成アイテム]** または **[構成基準]** の順にクリックします。
2.  **[ホーム]** タブの **[作成]** グループで、 **[構成データのインポート]** をクリックします。  
3.  **ファイルの選択** のページ、 **構成データのインポート ウィザード**, 、 をクリックして **追加**, 、し、次に、 **開く**  ダイアログ ボックスで、インポートする .cab ファイルを選択します。  
4.  Configuration Manager コンソールでインポートした構成データを編集可能にする場合は、 **[インポートする構成項目と構成基準を含む新しいファイルを作成する]** チェックボックスをオンにします。  
5.  **[概要]** ページで、実行される操作を確認し、ウィザードを完了します。  

インポートされた構成データは、 **[資産とコンプライアンス]** ワークスペースの **[コンプライアンス設定]** ノードに表示されます。  
