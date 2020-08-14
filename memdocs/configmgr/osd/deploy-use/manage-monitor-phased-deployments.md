---
title: 段階的な展開の管理と監視
titleSuffix: Configuration Manager
description: Configuration Manager でソフトウェアの段階的な展開を管理および監視する方法について説明します。
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66f31983e34ff37cd2df8532cd9d45d372ef1f3b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125102"
---
# <a name="manage-and-monitor-phased-deployments"></a>段階的な展開の管理と監視

この記事では、段階的な展開を管理および監視する方法について説明します。 管理タスクには、手動で次のフェーズを開始することと、フェーズを中断または再開することが含まれます。 

まず、段階的な展開を作成する必要があります。 
- [アプリケーション](create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)。  
- [ソフトウェア更新プログラム](create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [タスク シーケンス](create-phased-deployment-for-task-sequence.md)  



## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> 次のフェーズに移行する

設定 **[Manually begin the second phase of deployment]\(展開の第 2 フェーズを手動で開始する\)** を選択すると、成功の条件に基づいて自動的に次のフェーズが開始されません。 段階的な展開を次のフェーズに移行する必要があります。  

1. このアクションを開始する方法は、展開されているソフトウェアの種類に応じて変わります。  

    - **アプリケーション** (バージョン 1806 以降のみ): **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** を選択します。   

    - **ソフトウェアの更新プログラム** (バージョン 1810 以降のみ): **[ソフトウェア ライブラリ]** ワークスペースに移動して、次のいずれかのノードを選択します。    
        - ソフトウェア更新プログラム  
            - **すべてのソフトウェア更新プログラム**  
            - **ソフトウェア更新プログラム グループ**   
        - Windows 10 サービス、**すべての Windows 10 更新プログラム**  
        - Office 365 クライアント管理、**Office 365 の更新プログラム**  

    - **タスク シーケンス**: **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[オペレーティング システム]** を展開して、 **[タスク シーケンス]** を選択します。   

2. 段階的な展開を使用するソフトウェアを選択します。  

3. 詳細ウィンドウで、 **[段階的な展開]** タブに切り替えます。  

4. 段階的な展開を選択し、リボンの **[次のフェーズに移動]** をクリックします。  

    ![段階的な展開に関するアクションが表示された右クリック メニュー](media/Suspend-phased-deployment.PNG)



## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> フェーズの中断と再開 

段階的な展開は、手動で中断または再開できます。 たとえば、タスク シーケンスの段階的な展開を作成するとします。 パイロット グループのフェーズを監視している間、多数の障害が発生していることに気づきます。 そこで段階的な展開を中断し、以降、デバイスのタスク シーケンスの実行を停止します。 問題を解決したら、段階的な展開を再開してロールアウトを続行します。 

1. このアクションを開始する方法は、展開されているソフトウェアの種類に応じて変わります。  

    - **アプリケーション** (バージョン 1806 以降のみ): **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** を選択します。   

    - **ソフトウェアの更新プログラム** (バージョン 1810 以降のみ): **[ソフトウェア ライブラリ]** ワークスペースに移動して、次のいずれかのノードを選択します。    
        - ソフトウェア更新プログラム  
            - **すべてのソフトウェア更新プログラム**  
            - **ソフトウェア更新プログラム グループ**   
        - Windows 10 サービス、**すべての Windows 10 更新プログラム**  
        - Office 365 クライアント管理、**Office 365 の更新プログラム**  

    - **タスク シーケンス**: **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[オペレーティング システム]** を展開して、 **[タスク シーケンス]** を選択します。 既存のタスク シーケンスを選択して、リボンの **[段階的な展開の作成]** をクリックします。  

2. 段階的な展開を使用するソフトウェアを選択します。  

3. 詳細ウィンドウで、 **[段階的な展開]** タブに切り替えます。  

4. 段階的な展開を選択し、リボンの **[中断]** または **[再開]** をクリックします。 

> [!NOTE]
> 2020 年 4 月 21 日以降、Office 365 ProPlus は、**Microsoft 365 Apps for enterprise** に名前が変更されます。 詳細については、「[Office 365 ProPlus の名前の変更](https://docs.microsoft.com/deployoffice/name-change)」を参照してください。 コンソールの更新中は、Configuration Manager 製品やドキュメントに古い名前が表示される場合があります。 

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="monitor"></a><a name="bkmk_monitor"></a> 監視
<!--1358577-->
バージョン 1902 以降では、段階的展開が独自の専用監視ノードを持つことで、作成した段階的展開が識別しやすくなり、段階的展開の監視ビューに移動しやすくなりました。 **[監視]** ワークスペースから、 **[段階的展開]** を選択し、状態を確認する段階的展開のいずれかをダブルクリックします。 <!--3555949-->

Configuration Manager 1806 および 1810 では、段階的展開用のネイティブの監視エクスペリエンスを確認できます。 **[監視]** ワークスペースの **[展開]** ノードから段階的な展開を選択し、リボンで **[段階的な展開の状態]** をクリックします。

![2 つのフェーズの状態を示す段階的な展開の状態ダッシュボード](media/1358577-phased-deployment-status.png)

このダッシュボードには、展開の各フェーズに対して次の情報が表示されます。  

- **[合計デバイス数]** または **[リソースの合計]** :このフェーズの対象となるデバイスの数。  

- **状態**: このフェーズの現在の状態。 各フェーズは次の状態のいずれかになります。  

    - **展開の作成完了**:段階的な展開によって、このフェーズのコレクションにソフトウェアの展開が作成されました。 このソフトウェアではアクティブにクライアントを対象とします。  

    - **待機中**:前のフェーズは、このフェーズに引き続き展開するための成功基準にまだ達していません。  

    - **中断**:管理者が展開を中断しました。  

- **進行状況**:クライアントからの色分けされた展開の状態。 次に例を示します。成功、実行中、エラー、要件が満たされていません、不明。 

#### <a name="success-criteria-tile"></a>[成功の条件] タイル

**[Select Phase]\(フェーズの選択\)** ドロップダウン リストを使用して、 **[成功の条件]** タイルの表示を変更します。 このタイルには、 **[Phase Goal]\(フェーズ目標\)** と展開の現在のコンプライアンスとの比較が表示されます。 既定の設定では、フェーズ目標は 95% です。 この値は、展開が次のフェーズに移行するには 95% のコンプライアンスが必要であることを意味します。

この例では、フェーズ目標は 65% であり、現在のコンプライアンスは 66.7% です。 第 1 段階が成功の条件を満たしていたため、段階的な展開は自動的に第 2 段階に移行しました。  

   ![目標が 65% の段階的な展開状況の [成功の条件] タイルの例](media/pod-status-success-criteria-tile.png)

フェーズ目標は、*次の*フェーズの [フェーズの設定] の **[展開の成功率]** と同じです。 段階的な展開が次の段階を開始するために、この第 2 段階で第 1 段階の成功の条件を定義します。 この設定を表示するには: 

1. ソフトウェアの段階的な展開オブジェクトに移動し、[段階的な展開のプロパティ] を開きます。  

2. **[フェーズ]** タブに切り替えます。 **[フェーズ 2]** を選択し、 **[表示]** をクリックします。  

3. フェーズの [プロパティ] ウィンドウで、 **[フェーズの設定]** タブに切り替えます。  

4. *[前のフェーズが成功したかどうかの基準]* グループの **[展開の成功率]** の値を確認します。  

たとえば、以下のプロパティは、前述した条件が 65% の [成功の条件] タイルと同じフェーズのプロパティです。  
![フェーズのプロパティの [プロパティの設定] タブ](media/phase-properties-phase-settings.png)

