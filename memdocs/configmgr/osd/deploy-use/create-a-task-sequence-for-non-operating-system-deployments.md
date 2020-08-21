---
title: OS 以外の展開用タスク シーケンスの作成
titleSuffix: Configuration Manager
description: ソフトウェアの配布やタスクの自動化など、OS を展開する以外のタスク シーケンスを作成する
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fcae4d520b1e81d0ef3470cd12ee68488b4f589
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125528"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>OS 以外の展開用タスク シーケンスの作成

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のタスク シーケンスは、お客様の環境でさまざまなタスクを自動化するために使用されます。 これらのタスクは、主にオペレーティング システムの展開のために設計され、テストされます。 Configuration Manager には、次のシナリオで使用する主要なテクノロジとなる機能が他にもたくさんあります。

- [アプリケーションのインストール](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > バージョン 2002 以降では、アプリケーション モデルを介してタスク シーケンスを使用し、複雑なアプリケーションをインストールできます。 アプリのインストールまたはアンインストールに、タスク シーケンスである展開の種類をアプリに追加します。 詳しくは、「[Windows アプリケーションを作成する](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)」をご覧ください。<!-- 3555953 -->

- [ソフトウェア更新プログラムのインストール](../../sum/understand/software-updates-introduction.md)

- [構成の設定](../../compliance/understand/ensure-device-compliance.md)

[Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) や [Service Management Automation](https://docs.microsoft.com/system-center/sma/) など、Microsoft System Center の他の自動化テクノロジもご検討ください。  

タスク シーケンスの能力は、その柔軟性と使用方法にあります。 クライアント設定の構成、ソフトウェアの配布、ドライバーの更新、ユーザー状態の編集、および OS の展開とは独立したその他のタスクの実行を行うことができます。 カスタム タスク シーケンスを作成して、タスクをいくつでも追加できます。 Configuration Manager では、OS 以外の展開用のカスタム タスク シーケンスの使用がサポートされています。 ただし、タスク シーケンスで好ましくない結果や矛盾する結果が生じる場合は、操作を簡略化する方法を考えてください。

- より単純なステップを使用する
- 操作を複数のタスク シーケンスに分割する
- 段階的な方法でタスク シーケンスを作成してテストする

## <a name="supported-steps"></a>サポートされているステップ

OS 以外の展開用のカスタム タスク シーケンスでは、以下のステップの使用がサポートされています。  

- [準備の確認](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [ネットワーク フォルダーへの接続](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [パッケージ コンテンツのダウンロード](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [アプリケーションのインストール](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [パッケージのインストール](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [ソフトウェア更新プログラムのインストール](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [コンピューターの再起動](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [コマンド ラインの実行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [Powershell スクリプトの実行](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [タスク シーケンスの実行](../understand/task-sequence-steps.md#child-task-sequence)  

- [動的変数の設定](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [タスク シーケンス変数の設定](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>次のステップ

[カスタム タスク シーケンスの作成](create-a-custom-task-sequence.md)