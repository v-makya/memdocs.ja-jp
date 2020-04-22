---
title: クライアント設定を構成する
titleSuffix: Configuration Manager
description: Configuration Manager でクライアント設定を選択します。
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c64895c7945b972821a1dee1702047e61b740026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694240"
---
# <a name="how-to-configure-client-settings-in-configuration-manager"></a>Configuration Manager でクライアント設定を構成する方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のすべてのクライアント設定は、 **[管理]**  >  **[クライアント設定]** から管理できます。 カスタム設定が適用されていない、階層内のすべてのユーザーおよびデバイスの設定を構成する場合は、既定の設定を変更します。 別の設定を一部のユーザーまたはデバイスのみに適用する場合は、カスタム設定を作成してコレクションに展開します。  

各クライアント設定の詳細については、[クライアント設定について](../../../core/clients/deploy/about-client-settings.md)に関するページを参照してください。

> [!NOTE]  
>  クライアントを管理する構成項目を使用して、デバイスの構成対応の評価、追跡、および修復を行うことができます。 詳細については、「[System Center Configuration Manager でのデバイス コンプライアンスの確認](../../../compliance/understand/ensure-device-compliance.md)」を参照してください。  

##  <a name="configure-the-default-client-settings"></a>既定のクライアント設定を構成する    

1. Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]**  >  **[既定のクライアント設定]** の順に選択します。  

2. **[ホーム]** タブで **[プロパティ]** を選択します。  

3. ナビゲーション ウィンドウで、各設定のグループのクライアント設定を表示および構成します。  

   クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始するには、[クライアントを管理する方法](../../../core/clients/manage/manage-clients.md)に関するページで [Configuration Manager クライアントのポリシーの取得開始](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)をご覧ください。  

##  <a name="create-and-deploy-custom-client-settings"></a>カスタム クライアント設定を作成および展開する  
これらのカスタム設定を展開すると、既定のクライアント設定がオーバーライドされます。 この手順を始める前に、これらのカスタム クライアント設定を必要とするユーザーまたはデバイスを含むコレクションがあることを確認します。  

1. Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]** の順に選択します。  

2. **[ホーム]** タブの **[作成]** グループで、 **[カスタム クライアント設定の作成]** を選択してから、次のいずれかを選択します。  

   -   **カスタム クライアント デバイス設定の作成**  

   -   **カスタム クライアント ユーザー設定の作成**  

3. 一意の名前と、必要に応じて説明を指定します。  

4. 設定のグループが表示されているチェック ボックスのうち 1 つまたは複数をオンにします。  

5. ナビゲーション ウィンドウの各設定のグループを選択し、利用可能な設定を構成して **[OK]** をクリックします。   

6. 作成したカスタム クライアント設定を選択します。 **[ホーム]** タブの **[クライアント設定]** グループで、 **[展開]** を選択します。  

7. **[コレクションの選択]** ダイアログ ボックスで適切なコレクションを選択し、 **[OK]** を選択します。 選択したコレクションを確認するには、詳細ウィンドウで **[展開]** タブをクリックします。  

8. 作成したカスタム クライアント設定の順序を表示します。 複数のカスタム クライアント設定がある場合は、順序番号に従って適用されます。 競合がある場合は、順序番号が一番小さい設定によってその他の設定がオーバーライドされます。 順序番号を変更するには、 **[ホーム]** タブの **[クライアント設定]** グループで、 **「Move Item Up」 (項目を上に移動)** または **「Move Item Down」 (項目を下に移動)** を選択します。  

   クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始するには、[クライアントを管理する方法](../../../core/clients/manage/manage-clients.md)に関するページで [Configuration Manager クライアントのポリシーの取得開始](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)をご覧ください。  



##  <a name="view-client-settings"></a>クライアント設定を表示する  
 同じデバイス、ユーザー、またはユーザー グループに複数のクライアント設定を展開すると、優先順位と設定が複雑になることがあります。 クライアント設定を表示するには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[デバイス]**  >  **[ユーザー]** または **[ユーザー コレクション]** の順に選択します。  

3.  **[クライアント設定]** グループで、デバイス、ユーザー、または、ユーザー グループを選択して、 **[クライアントの設定の結果]** を選択します。  

4.  左ウィンドウからクライアント設定を選択すると、設定が表示されます。 この表示では、設定は読み取り専用です。 

    > [!NOTE]  
    >  クライアント設定を表示するには、クライアント設定に対する読み取りアクセス権を持っている必要があります。  

    
