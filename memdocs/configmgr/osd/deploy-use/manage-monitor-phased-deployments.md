---
title: 段階的な展開の管理と監視
titleSuffix: Configuration Manager
description: Configuration Manager でソフトウェアの段階的な展開を管理および監視する方法について説明します。
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 631a2fc3cb7df01eed1a5a6af80dd87f84455bdc
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606335"
---
# <a name="manage-and-monitor-phased-deployments"></a>段階的な展開の管理と監視

この記事では、段階的な展開を管理および監視する方法について説明します。 管理タスクには、手動で次のフェーズを開始することと、フェーズを中断または再開することが含まれます。

まず、段階的な展開を作成する必要があります。

- [アプリケーション](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)。  
- [ソフトウェア更新プログラム](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [タスク シーケンス](create-phased-deployment-for-task-sequence.md)  

## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> 次のフェーズに移行する

設定 **[Manually begin the second phase of deployment]\(展開の第 2 フェーズを手動で開始する\)** を選択すると、成功の条件に基づいて自動的に次のフェーズが開始されません。 段階的な展開を次のフェーズに移行する必要があります。  

1. このアクションを開始する方法は、展開されているソフトウェアの種類に応じて変わります。  

    - **アプリケーション**: **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** を選択します。

    - **ソフトウェア更新プログラム**: **[ソフトウェア ライブラリ]** ワークスペースに移動して、次のいずれかのノードを選択します。
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

バージョン 2002 以降では、次の Windows PowerShell コマンドレットを使用してこのタスクを実行できます。[Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext)。

## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> フェーズの中断と再開

段階的な展開は、手動で中断または再開できます。 たとえば、タスク シーケンスの段階的な展開を作成するとします。 パイロット グループのフェーズを監視している間、多数の障害が発生していることに気づきます。 そこで段階的な展開を中断し、以降、デバイスのタスク シーケンスの実行を停止します。 問題を解決したら、段階的な展開を再開してロールアウトを続行します。

1. このアクションを開始する方法は、展開されているソフトウェアの種類に応じて変わります。  

    - **アプリケーション**: **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** を選択します。

    - **ソフトウェア更新プログラム**: **[ソフトウェア ライブラリ]** ワークスペースに移動して、次のいずれかのノードを選択します。
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
> 2020 年 4 月 21 日以降、Office 365 ProPlus は、**Microsoft 365 Apps for enterprise** に名前が変更されます。 詳細については、「[Office 365 ProPlus の名前の変更](/deployoffice/name-change)」を参照してください。 コンソールの更新中は、Configuration Manager 製品やドキュメントに古い名前が表示される場合があります。

バージョン 2002 以降では、次の Windows PowerShell コマンドレットを使用してこのタスクを実行できます。

- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)

## <a name="monitor"></a><a name="bkmk_monitor"></a> 監視
<!--1358577-->

段階的な展開には独自の専用監視ノードがあるため、作成した段階的な展開の特定や、段階的な展開の監視ビューへの移動を容易に行えます。 **[監視]** ワークスペースから、 **[段階的展開]** を選択し、状態を確認する段階的展開のいずれかをダブルクリックします。 <!--3555949-->

![2 つのフェーズの状態を示す段階的な展開の状態ダッシュボード](media/1358577-phased-deployment-status.png)

このダッシュボードには、展開の各フェーズに対して次の情報が表示されます。  

- **[合計デバイス数]** または **[リソースの合計]** :このフェーズの対象となるデバイスの数。  

- **状態**: このフェーズの現在の状態。 各フェーズは次の状態のいずれかになります。  

  - **展開の作成完了**:段階的な展開によって、このフェーズのコレクションにソフトウェアの展開が作成されました。 このソフトウェアではアクティブにクライアントを対象とします。  

  - **待機中**:前のフェーズは、このフェーズに引き続き展開するための成功基準にまだ達していません。  

  - **中断**:管理者が展開を中断しました。  

- **進行状況**:クライアントからの色分けされた展開の状態。 次に例を示します。成功、実行中、エラー、要件が満たされていません、不明。

### <a name="success-criteria-tile"></a>[成功の条件] タイル

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

## <a name="powershell"></a>PowerShell

段階的な展開を管理するには、次の Windows PowerShell コマンドレットを使用します。

### <a name="automatically-create-phased-deployments"></a>段階的な展開を自動で作成する

- [New-CMApplicationAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmapplicationautophaseddeployment)
- [New-CMSoftwareUpdateAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdateautophaseddeployment)
- [New-CMTaskSequenceAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequenceautophaseddeployment)

### <a name="manually-create-phased-deployments"></a>段階的な展開を手動で作成する

- [New-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/new-cmsoftwareupdatephase)
- [New-CMSoftwareUpdateManualPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatemanualphaseddeployment)
- [New-CMTaskSequencePhase](/powershell/module/configurationmanager/new-cmtasksequencephase)
- [New-CMTaskSequenceManualPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequencemanualphaseddeployment)

### <a name="get-existing-phased-deployment-objects"></a>既存の段階的な展開オブジェクトを取得する

- [Get-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/get-cmapplicationphaseddeployment)
- [Get-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/get-cmsoftwareupdatephaseddeployment)
- [Get-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/get-cmtasksequencephaseddeployment)
- [Get-CMPhase](/powershell/module/configurationmanager/get-cmphase)

### <a name="monitor-phased-deployment-status"></a>段階的な展開の状態を監視する

- [Get-CMPhasedDeploymentStatus](/powershell/module/configurationmanager/get-cmphaseddeploymentstatus)

### <a name="manage-existing-phased-deployments"></a>既存の段階的な展開を管理する

- [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)
- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)

### <a name="modify-existing-phased-deployments"></a>既存の段階的な展開を変更する

- [Set-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/set-cmapplicationphaseddeployment)
- [Set-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/set-cmsoftwareupdatephase)
- [Set-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/set-cmsoftwareupdatephaseddeployment)
- [Set-CMTaskSequencePhase](/powershell/module/configurationmanager/set-cmtasksequencephase)
- [Set-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/set-cmtasksequencephaseddeployment)
- [Remove-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/remove-cmapplicationphaseddeployment)
- [Remove-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/remove-cmsoftwareupdatephaseddeployment)
- [Remove-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/remove-cmtasksequencephaseddeployment)
