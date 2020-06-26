---
title: 共同管理ワークロードを切り替える
titleSuffix: Configuration Manager
description: Configuration Manager で現在管理されているワークロードを Microsoft Intune に切り替える方法について説明します。
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: how-to
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 88c8b34437ba52e700ef97885aafed40734a0f32
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776958"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Configuration Manager のワークロードを Intune に切り替える方法

共同管理の利点の 1 つは、Configuration Manager から Microsoft Intune に切り替えることです。 Windows 10 デバイスに Configuration Manager クライアントがあり、Intune に登録されている場合は、両方のサービスの恩恵を受けられます。 ワークロードがある場合、そのワークロードを制御して、機関を Configuration Manager から Intune に切り替えます。 Configuration Manager では、Intune に切り替えないワークロードを含む、他のすべてのワークロードと、共同管理でサポートされない Configuration Manager の他のすべての機能が引き続き管理されます。

ワークロードを Intune に切り替えても、後で気が変わった場合は、Configuration Manager に戻すことができます。

サポートされているワークロードの詳細については、「[ワークロード](workloads.md)」を参照してください。

## <a name="switch-workloads-starting-in-version-1906"></a>バージョン 1906 以降でのワークロードの切り替え
<!--3555750 FKA 1357954 -->
バージョン 1906 以降では、各共同管理ワークロードに対してさまざまなパイロット コレクションを構成できるようになります。 さまざまなパイロット コレクションを使用できれば、ワークロードをシフトするとき、さらに詳細な手法が可能になります。 共同管理を有効にするとき、あるいはその後、準備ができたとき、ワークロードを切り替えることができます。 共同管理を有効にしていない場合、まず有効にしてください。 詳細については、「[How to enable co-management](how-to-enable.md)」 (共同管理を有効にする方法) を参照してください。 共同管理を有効にした後、共同管理プロパティの設定を変更します。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[共同管理]** を選択します。  
2. 共同管理オブジェクトを選択してから、リボンで **[プロパティ]** を選択します。  
3. **[ワークロード]** タブに切り替えます。既定では、すべてのワークロードは **[Configuration Manager]** 設定に設定されています。 ワークロードを切り替えるには、そのワークロードのスライダー コントロールを目的の設定まで動かします。  

    ![共同管理プロパティ ページの [ワークロード] タブのスクリーンショット](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**:Configuration Manager では引き続きこのワークロードが管理されます。  

    - **パイロット Intune**:パイロット コレクション内のデバイスに対してのみこのワークロードを切り替えます。 共同管理プロパティ ページの **[ステージング]** タブで **[パイロット コレクション]** を変更できます。  

    - **Intune**:共同管理に登録されているすべての Windows 10 デバイスに対してこのワークロードを切り替えます。  

4. **[ステージング]** タブに移動し、必要に応じて、ワークロードの **[パイロット コレクション]** を変更します。
  
   ![共同管理プロパティ ページの [ワークロード] タブのスクリーンショット](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - ワークロードを切り替える前に、それに対応するワークロードが Intune で適切に構成され、展開されていることを確認します。 デバイス用の管理ツールのいずれかでワークロードが常に管理されていることを確認します。
> - Configuration Manager バージョン 1806 以降では、共同管理ワークロードを切り替えるときに、共同管理されたデバイスで自動的に Microsoft Intune から MDM ポリシーが同期されます。 この同期は、Configuration Manager コンソールのクライアント通知から**コンピューター ポリシーのダウンロード**操作を開始するときにも行われます。 詳細については、「[クライアント通知を使用してクライアント ポリシーの取得を開始する](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」を参照してください。 <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>バージョン 1902 以前でのワークロードの切り替え

共同管理を有効にするとき、あるいはその後、準備ができたとき、ワークロードを切り替えることができます。 共同管理を有効にしていない場合、まず有効にしてください。 詳細については、「[How to enable co-management](how-to-enable.md)」 (共同管理を有効にする方法) を参照してください。 共同管理を有効にした後、共同管理プロパティの設定を変更します。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[共同管理]** を選択します。  

2. 共同管理オブジェクトを選択してから、リボンで **[プロパティ]** を選択します。
   - Azure AD にサインインするように求められます。 このプロンプトによってオンボードの更新がブロックされることはありません。 ただし、サインインを実行するまでは、 **[プロパティ]** ページを開くたびにプロンプトが表示されます。

3. **[ワークロード]** タブに切り替えます。既定では、すべてのワークロードは **[Configuration Manager]** 設定に設定されています。 ワークロードを切り替えるには、そのワークロードのスライダー コントロールを目的の設定まで動かします。  

    ![共同管理プロパティ ページの [ワークロード] タブのスクリーンショット](media/properties-workloads.png)

    - **Configuration Manager**:Configuration Manager では引き続きこのワークロードが管理されます。  

    - **パイロット Intune**:パイロット コレクション内のデバイスに対してのみこのワークロードを切り替えます。 共同管理プロパティ ページの **[ステージング]** タブで **[パイロット コレクション]** を変更できます。  

    - **Intune**:共同管理に登録されているすべての Windows 10 デバイスに対してこのワークロードを切り替えます。  

4. 共同管理プロパティ ページの **[ステージング]** タブで、必要に応じてワークロードの **[パイロット コレクション]** を変更します。

5. **[OK]** をクリックし、共同管理プロパティを保存して終了します。

> [!Important]  
> - ワークロードを切り替える前に、それに対応するワークロードが Intune で適切に構成され、展開されていることを確認します。 デバイス用の管理ツールのいずれかでワークロードが常に管理されていることを確認します。 
> - Configuration Manager バージョン 1806 以降では、共同管理ワークロードを切り替えるときに、共同管理されたデバイスで自動的に Microsoft Intune から MDM ポリシーが同期されます。 この同期は、Configuration Manager コンソールのクライアント通知から**コンピューター ポリシーのダウンロード**操作を開始するときにも行われます。 詳細については、「[クライアント通知を使用してクライアント ポリシーの取得を開始する](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」を参照してください。 <!--1357377-->

## <a name="next-steps"></a>次のステップ

[共同管理の監視](how-to-monitor.md)
