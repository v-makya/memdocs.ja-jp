---
title: 電源管理を構成する
titleSuffix: Configuration Manager
description: Configuration Manager の電源管理を設定します。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696600"
---
# <a name="configure-power-management-in-configuration-manager"></a>Configuration Manager の電源管理を構成する

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager で電源管理を設定する方法について説明します。

## <a name="enable-and-configure-client-settings"></a>クライアント設定を有効にして構成する

この手順では、電源管理の*既定のクライアント設定*を構成します。 階層にあるすべてのコンピューターに適用されます。

これらの設定を一部のコンピューターにのみ適用する場合は、*カスタムのデバイス クライアント設定*を作成します。 次にそれを、電源管理対象のコンピューターが含まれるコレクションに割り当てます。 詳しくは、「[クライアント設定を構成する方法](../../deploy/configure-client-settings.md)」をご覧ください。  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[クライアント設定]** ノードを選択し、 **[既定のクライアント設定]** を選択します。

1. リボンの **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** を選択します。  

1. **[電源管理]** グループを選択します。  

1. **デバイスの電源管理を許可する**ようにクライアント設定を有効にします。

1. 必要な追加のクライアント設定を構成します。 詳細については、[電源管理のクライアント設定](../../deploy/about-client-settings.md#power-management)に関するページを参照してください。  

クライアントでは、次回クライアント ポリシーをダウンロードしたとき、これらの設定が構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「[クライアントを管理する方法](../manage-clients.md#BKMK_PolicyRetrieval)」を参照してください。  

## <a name="exclude-computers"></a>コンピューターを除外する

コンピューターに電源管理設定が適用されるのを防ぐことができます。 コンピューターが電源管理設定から除外される*あらゆる*コレクションのメンバーである場合、そのコンピューターでは電源管理設定が適用されません。 この動作は、電源管理設定を適用する別のコレクションに属している場合も当てはまります。  

次の理由から、コンピューターを電源管理から除外することがあります。  

- 事業の必要性からコンピューターを常時オンにしておく必要がある場合  

- 電源管理設定を適用しないコンピューターの制御コレクションを作成した場合  

- 一部のコンピューターに、電源管理設定を適用する機能が備わっていない場合  

- Windows Server を実行しているコンピューターを電源管理から除外する場合  

> [!NOTE]  
> クライアント設定で **[ユーザーがデバイスを電源管理対象から外せるようにする]** が構成されていると、ユーザーはソフトウェア センターを使用し、自分のコンピューターを電源管理から除外できます。  

電源管理から除外されているコンピューターを見つけるには、 **[除外されているコンピューター]** レポートを実行してください。 このレポートの詳細は、[電源管理を監視して計画する方法](monitor-and-plan-for-power-management.md#BKMK_Excluded)に関するページを参照してください。  

> [!IMPORTANT]  
> 電源管理からコンピューターを除外すると、すべての電源設定が元の値に戻ります。 個々の電源設定をその元の値に戻すことはできません。  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>コンピューターのコレクションを電源管理から除外する方法  

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス コレクション]** ノードを選択します。  

1. 電源管理から除外するコレクションを選択します。 リボンの **[ホーム]** タブの **[プロパティ]** グループで **[プロパティ]** を選択します。  

1. **[電源管理]** タブに切り替え、 **[このコレクションのコンピューターに電源管理設定を適用しない]** を選択します。  

## <a name="next-steps"></a>次のステップ

[電源プランを作成して適用する方法](create-and-apply-power-plans.md)

[電源管理を監視して計画する方法](monitor-and-plan-for-power-management.md)
