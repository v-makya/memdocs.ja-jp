---
title: Endpoint Protection 用 Windows ファイアウォール ポリシー
titleSuffix: Configuration Manager
description: System Center 2012 Configuration Manager で Endpoint Protection のファイアウォール ポリシーを作成および展開する方法を説明します。
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c017e750e175e09a67deb4651cf7e8eb98f1bc1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696960"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager で Endpoint Protection の Windows ファイアウォール ポリシーを作成および展開する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager で Endpoint Protection のファイアウォール ポリシーを使用すると、階層内のクライアント コンピューターで、基本的な Windows ファイアウォール構成タスクと保守タスクを実行できます。 Windows ファイアウォール ポリシーを使用して以下のタスクを実行できます。  

-   Windows ファイアウォールの有効化と無効化を制御する。  

-   着信接続をクライアント コンピューターに許可するかどうかを制御する。  

-   Windows ファイアウォールが新しいプログラムをブロックしたときにユーザーに通知するかどうかを制御する。  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** をクリックします。  

2.  **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、 **[Windows ファイアウォール ポリシー]** をクリックします。  

3.  **[ホーム]** タブの **[作成]** グループで、 **[Windows ファイアウォール ポリシーの作成]** をクリックします。  

4.  **Windows ファイアウォール ポリシーの作成ウィザード** の **[全般]** ページで、このファイアウォール ポリシーの名前とオプションの説明を指定し、 **[次へ]** をクリックします。  

5.  ウィザードの **[プロファイルの設定]** ページで、ネットワーク プロファイルごとに以下の設定を構成します。  

    > [!NOTE]  
    >  ネットワーク プロファイルの詳細については、Windows のドキュメントを参照してください。  

    -   **[Windows ファイアウォールを有効にする]**  

        > [!NOTE]  
        >  **[Windows ファイアウォールを有効にする]** が有効になっていない場合は、ウィザードのこのページの他の設定を利用できません。  

    -   **許可されたプログラムの一覧にあるプログラムからの接続も含み、すべての着信をブロックする**  

    -   **Windows ファイアウォールが新しいプログラムをブロックしたときにユーザーに通知する**  

6.  ウィザードの **[概要]** ページで、実行される操作を確認してから、ウィザードを完了します。  

7.  **[Windows ファイアウォール ポリシー]** の一覧に表示される新しい Windows ファイアウォール ポリシーを確認します。  

##  <a name="to-deploy-a-windows-firewall-policy"></a><a name="BKMK_Assign"></a> Windows ファイアウォール ポリシーを展開するには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** をクリックします。  

2.  **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、 **[Windows ファイアウォール ポリシー]** をクリックします。  

3.  **[Windows ファイアウォール ポリシー]** の一覧で、展開する Windows ファイアウォール ポリシーを選択します。  

4.  **[ホーム]** タブの **[展開]** グループで、 **[展開]** をクリックします。  

5.  **[Windows ファイアウォール ポリシーの展開]** ダイアログ ボックスで、このWindows ファイアウォール ポリシーを割り当てるコレクションを指定して、割り当てスケジュールを指定します。 Windows ファイアウォール ポリシーは、このスケジュールとクライアントの Windows ファイアウォール設定を使用して対応を評価し、Windows ファイアウォール ポリシーと一致するように再構成します。  

6.  **[OK]** をクリックし、 **[Windows ファイアウォール ポリシーの展開]** ダイアログ ボックスを閉じて Windows ファイアウォール ポリシーを展開します。  

    > [!IMPORTANT]  
    >  Windows ファイアウォール ポリシーをコレクションに展開すると、ネットワークに大きな負荷がかかるのを避けるため、このポリシーは 2 時間かけてランダムな順序でコンピューターに適用されます。
