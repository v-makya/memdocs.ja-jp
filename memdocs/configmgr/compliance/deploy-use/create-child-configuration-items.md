---
title: 子構成項目を作成する
titleSuffix: Configuration Manager
description: Configuration Manager での子構成項目を作成します。
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 319f673200244d4451b957dcb778ce378f9569fa
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240322"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Configuration Manager での子構成項目の作成方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の子構成項目は構成項目のコピーであり、元の構成項目への関係を保持しています。したがって、子構成項目は親構成項目から元の構成を継承しています。  

Configuration Manager コンソールで子構成項目のプロパティを表示したときに、独自の検証条件を持つ継承されたオブジェクトと設定は編集できません。 ただし、子構成項目に検証条件を追加してから、その検証条件を編集することはできます。また、新しいオブジェクトや設定を子構成項目に追加することもできます。
子構成項目を作成および編集する例としては、元の構成項目をビジネス要件に合わせることがあります。  

> [!NOTE]  
>  子構成項目は、種類が **Windows デスクトップおよびサーバー (カスタム)** の構成項目からのみ作成できます。  

## <a name="to-create-a-child-configuration-item"></a>子構成項目を作成するには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[コンプライアンス設定]**  >  **[構成項目]** の順にクリックします。  

3.  **構成項目** 一覧で、子構成項目を作成するため、次の構成項目を選択、 **ホーム** ] タブで、 **構成項目** グループで、[ **子構成項目の作成**です。  

4.  **全般** のページ、 **子の構成項目の作成ウィザード**, 、親の特定のバージョンを使用して、子を作成する構成項目を選択できます。 このウィザードのほかの手順は、標準の構成項目を作成する場合に使用する手順と同じです。 詳細については、｢[System Center Configuration Manager クライアントを使用して管理されている Windows デスクトップおよびサーバー コンピューターのカスタム構成項目を作成する方法](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)｣を参照してください。  

5.  ウィザードを完了します。 新しい子構成項目は、 **[構成項目]** 一覧に表示されます。  
