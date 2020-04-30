---
title: アプリケーション展開をシミュレートする
titleSuffix: Configuration Manager
description: アプリケーションをインストールすることなく、展開の種類に関する検出方法、要件、および依存関係を評価します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689980"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Configuration Manager でアプリケーションの展開をシミュレートする

*適用対象:Configuration Manager (Current Branch)*

アプリケーションをインストールまたはアンインストールしないでアプリケーションの展開をテストするには、シミュレートされた展開を使用できます。 シミュレートされた展開は、展開の種類に関する検出方法、要件、および依存関係を評価します。 結果は、 **[監視]** ワークスペースの **[展開]** ノードでレポートされます。 Configuration Manager でアプリケーションの展開をシミュレーションするときは、このトピックの手順を使用します。  

> [!NOTE]  
> モバイル デバイスのコレクションには、展開シミュレーションを使用できません。  
>   
> アプリケーションの展開シミュレーションがアクティブな場合は、展開目的が **[アンインストール]** のアプリケーション展開を行うことはできません。  

## <a name="configure-a-simulated-application-deployment"></a>シミュレートされたアプリケーションの展開を構成する

1.  Configuration Manager コンソールで、次のいずれかを選択します。  
    -   ユーザーのコレクション  
    -   デバイスのコレクション  
    -   Configuration Manager アプリケーション  

2.  **[ホーム]** タブの **[展開]** グループで、 **[展開のシミュレーション]** を選択します。  

3.  アプリケーション展開のシミュレーション ウィザードで、シミュレートされた展開に次の詳細を設定します。  

    -   **[アプリケーション]** 。 **[参照]** を選択し、展開のシミュレーションを作成するアプリケーションを選択します。  

    -   **[コレクション]** 。 **[参照]** を選択し、シミュレーションされた展開に使うコレクションを選択します。  

    -   **[操作]** 。 ドロップダウン リストから、選択したアプリケーションのインストールをシミュレーションするか、アンインストールをシミュレーションするかを選択します。  

    -   **[ユーザーのログインに関係なく自動的に展開する]** 。 このオプションをオンにすると、クライアントがログインしているかどうかにかかわらず、クライアントはシミュレーションされた展開を評価します。  

4.  **[次へ]** をクリックし、 **[概要]** ページで情報を確認して、ウィザードを終了し、シミュレーションされたアプリケーション展開を作成します。  

5.  シミュレーションされるアプリケーションは、 **[監視]** ワークスペースの **[展開]** ノードに、 **[シミュレート]** の目的で表示されます。 アプリケーション展開の監視方法の詳細については、「[Configuration Manager でのアプリケーションの監視方法](../../apps/deploy-use/monitor-applications-from-the-console.md)」を参照してください。  
