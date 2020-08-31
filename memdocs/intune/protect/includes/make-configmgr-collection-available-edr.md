---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823495"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. 最上位サイトに接続されている Configuration Manager コンソールで、Microsoft Endpoint Manager admin center に同期するデバイス コレクションを右クリックし、 **[プロパティ]** を選択します。

2. **[Cloud Sync]\(クラウド同期\)** タブで、 **[Make this collection available to assign Endpoint security policies from Microsoft Endpoint Manager admin center]\(このコレクションを Microsoft エンドポイント マネージャー管理センターからエンドポイント セキュリティ ポリシーを割り当てるために使用できるようにする\)** のオプションを有効にします。

   - Configuration Manager 階層がテナントにアタッチされていない場合は、このオプションを選択することはできません。
   - このオプションに使用できるコレクションは、[テナントのアタッチのアップロード対象に選択されたコレクション スコープ](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit)に制限されます。 <!--CM7423168-->
  
   ![クラウドの同期を構成する](../media/tenant-attach-intune/cloud-sync.png)

3. **[OK]** を選択して構成を保存します。

   このコレクションのデバイスは、Microsoft Defender ATP を使用してオンボードできます。また、Intune エンドポイント セキュリティ ポリシーの使用をサポートしています。
