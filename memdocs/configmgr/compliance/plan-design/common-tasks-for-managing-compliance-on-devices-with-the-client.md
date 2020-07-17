---
title: 一般的なコンプライアンス管理のタスク
titleSuffix: Configuration Manager
description: いくつかの一般的なシナリオを使用して、Configuration Manager のコンプライアンス設定について説明します。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 5920229331bca8d2a47b0bf1ab663530ef63c51e
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240662"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Configuration Manager クライアントでデバイスのコンプライアンスを管理するための一般的なタスク

*適用対象:Configuration Manager (Current Branch)*

この記事では、よく発生する一般的なシナリオに従ってガイドすることで、Configuration Manager のコンプライアンス設定を使用する方法の概要を説明します。  

 コンプライアンス設定に関する知識を既にお持ちの場合は、[Configuration Manager クライアントを使用して管理されているデバイスの構成アイテム](../../compliance/deploy-use/create-configuration-items.md)に関する記事に、お客様が使用するすべての機能に関する詳細情報が記載されています。  

 開始する前に、コンプライアンス設定の基本について、[コンプライアンス設定の概要](../../compliance/get-started/get-started-with-compliance-settings.md)に関するページ参照してください。 必要な前提条件については、[コンプライアンス設定の計画と構成](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)に関するページをご覧ください。  

## <a name="general-information-for-each-scenario"></a>各シナリオ共通の情報  
 各シナリオでは、特定のタスクを実行する構成項目を作成します。 構成アイテムの作成 ウィザードを開いて作業を開始するには、次のステップを実行します。  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[コンプライアンス設定]**  >  **[構成アイテム]** の順に選択します。  

1.  **[ホーム]** タブの **[作成]** グループで、 **[構成アイテムの作成]** を選択します。  

1.  次のスクリーンショットで表示されている構成アイテムの作成ウィザードの **[全般]** ページで、構成アイテムの名前と説明を入力します。 次に、この記事の各シナリオに適した構成アイテムの種類を選択します。  

     ![構成アイテムの作成ウィザードの [全般] ページ](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>シナリオ:Windows 10 デバイスで Bluetooth を無効にする

 このシナリオでは、デバイス上の Bluetooth 機能を使って会社の機密情報が社外で送信される可能性がある、とお客様のセキュリティ部門が判断したとします。 最近、すべてのコンピューターを Windows 10 にアップグレードしました。 これらのデバイスで Bluetooth を無効にすることを決定しました。  

1. 構成アイテムの作成ウィザードの **[全般]** ページで、構成アイテムの種類として **[Windows 10]** を選択してから、 **[次へ]** を選択します。  

2. ウィザードの **[サポートされているプラットフォーム]** ページで、すべての Windows 10 プラットフォームを選択します。  

3. **[デバイス設定]** ページで、 **[デバイス]** を選択し、 **[次へ]** を選択します。  

4. **[デバイス]** ページで、 **[Bluetooth]** の値として **[禁止]** を選択します。  

5. **[対応していない設定を修復する]** を選択して、変更がすべての Windows 10 デバイスに確実に適用されるようにします。  

6. ウィザードを完了して構成項目を作成します。  

 これで、「[Configuration Manager での構成基準の作成と展開に関する一般的なタスク](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)」の記事に記載されている情報を使って、作成した構成をデバイスに簡単に展開できるようになりました。  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>シナリオ:Windows デスクトップ コンピューターで正しくないレジストリ値を修復する

> [!NOTE] 
> Configuration Manager クライアントを実行している Mac コンピューターでは、コンプライアンスを評価するためのオプションが 2 つあります。  
> - Mac OS X の設定 (plist) ファイルを評価します。
> - カスタム スクリプトを使用し、そのスクリプトから返される結果を評価します。  
>
>詳細については、「[Configuration Manager クライアントを使用して管理されている Mac OS X デバイスの構成項目を作成する方法](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)」を参照してください。  

 このシナリオでは、 管理対象の一部の Windows 8.1 コンピューターで、重要な基幹業務アプリが正しく実行されていないことを発見したとします。 あなたは、**HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** という名前のレジストリ キーの値が、一部のコンピューター上で **0** に設定されていることがこの原因であると判断しました。 この基幹業務アプリを正常に実行させるには、この値を **1** に設定する必要があります。  

 この手順では、レジストリ キーの値を監視し、正しくない値が見つかった場合には自動的に修復する構成アイテムを作成します。  

1. 構成アイテムの作成ウィザードの **[全般]** ページで、構成アイテムの種類として **[Windows デスクトップおよびサーバー (カスタム)]** を選択してから、 **[次へ]** を選択します。  

2. ウィザードの **[サポートされているプラットフォーム]** ページで、 **[Windows 8.1]** を選択します (構成アイテムが対象のコンピューターにのみ適用されるようにするため)。  

3. **[設定]** ページで、 **[新規]** を選択して新しい設定を作成します。  

4. **[設定の作成]** ダイアログ ボックスの **[全般]** タブで、次の設定を構成します。  

   -   **[名前]**  >  **[設定例]**  

   -   **[設定の種類]**  >  **[レジストリ値]**  

   -   **[データ型]**  >  **[整数]** (値に数値のみが含まれているため)  

   -   **[ハイブ]**  > **HKEY_LOCAL_MACHINE**  

   -   **[キー]**  > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **[値]**  > **1** (必須の値)  

5. **[設定の作成]** ダイアログ ボックスの **[コンプライアンスの規則]** タブで、 **[新規]** を選択します。 **[規則の作成]** ダイアログ ボックスで、次の設定を構成します。  

   -   **[名前]**  >  **[規則の例]**  

   -   **[選択した設定]** > 選択した設定が **[設定例]** であることを確認します。

   -   **[規則の種類]**  >  **[値]**  

   -   **[この設定は次の規則に対応する必要があります]** > 設定名が正しいことを確認して、設定値が **[1]** に等しくなければならないことを指定するオプションを構成します。  

   -   **[サポートされている場合は対応していない規則を修復する]** > レジストリ キー値が正しくない場合に Configuration Manager によってこれが正しい値にリセットされるようにするには、このチェック ボックスをオンにします。  

6. ウィザードを完了して構成項目を作成します。  

 これで、[構成基準の作成と展開に関する一般的なタスク](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)に関する記事に記載されている情報を使って、作成した構成をデバイスに簡単に展開できるようになりました。  

## <a name="next-steps"></a>次のステップ

[構成基準を展開する](common-tasks-for-creating-and-deploying-configuration-baselines.md)
