---
title: リモート コントロール使用状況の監査
titleSuffix: Configuration Manager
description: Configuration Manager のリモート コントロール使用状況を監査します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2cda087867f3ebbd6695a0f4d368bbe2c5e06664
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696490"
---
# <a name="how-to-audit-remote-control-usage-in-configuration-manager"></a>Configuration Manager でのリモート コントロール使用状況の監査方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のレポートを使用して、リモート コントロールの監査情報を表示することができます。  

 Configuration Manager でのレポートの構成方法について詳しくは、[レポートの概要](../../../servers/manage/introduction-to-reporting.md)に関する記事をご覧ください。  

 **[ステータス メッセージ - 監査]** のカテゴリでは次の 2 つのレポートが使用できます。  

-   **リモート コントロール - 特定のユーザーによりリモートで制御されるコンピューターすべて** – 特定のユーザーが開始したリモート コントロール操作の概要が表示されます。  

-   **リモート コントロール - リモート コントロール情報すべて** – クライアント コンピューターのリモート コントロールに関するステータス メッセージの概要が表示されます。  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>[リモート コントロール - 特定のユーザーによりリモートで制御されるコンピューターすべて] レポートを実行するには  

1.  Configuration Manager コンソールで、 **[監視]** をクリックします。  

2.  **[監視]** ワークスペースで、 **[レポート]** を展開し、 **[レポート]** をクリックします。  

3.  **レポート** ノードをクリックして、 **カテゴリ** レポートを並べ替え、カテゴリのレポートをより簡単に見つけられるように列 **ステータス メッセージ - 監査**です。  

4.  レポートを選択して **リモート_コントロール - 特定のユーザーによって制御されるすべてのリモートのコンピューター**, 、、 **ホーム**  タブで、 **レポート グループ**, 、 をクリックして **実行**です。  

5.  **ユーザー名** の一覧、 **リモート_コントロール - 特定のユーザーによって制御されるすべてのリモートのコンピューター**, 、クリックして、監査情報をレポートするユーザー指定 **レポートの表示**です。  

6.  レポートのデータの確認が終わったら、レポート ウィンドウを閉じます。  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>[リモート コントロール - リモート コントロール情報すべて] レポートを実行するには  

1.  Configuration Manager コンソールで、 **[監視]** をクリックします。  

2.  **[監視]** ワークスペースで、 **[レポート]** を展開し、 **[レポート]** をクリックします。  

3.  **[レポート]** ノードで、 **[カテゴリ]** 列をクリックしてレポートを並べ替え、 **[ステータス メッセージ - 監査]** カテゴリのレポートを簡単に見つけられるようにします。  

4.  レポートを選択 **リモート_コントロール - リモート_コントロール情報すべて**, 、、 **ホーム**  タブで、 **レポート グループ**, 、 をクリックして **実行** を開くには、 **リモート_コントロール - リモート_コントロール情報すべて** ウィンドウです。  

5.  レポートのデータの確認が終わったら、レポート ウィンドウを閉じます。  
