---
title: マルチキャストを使用した、ネットワーク経由での Windows の展開
titleSuffix: Configuration Manager
description: 複数のコンピューターで OS イメージを同時にダウンロードできるように、Configuration Manager 環境内でマルチキャストを使用します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124707"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager でマルチキャストを使用したネットワーク経由での Windows の展開

*適用対象:Configuration Manager (Current Branch)*

マルチキャストは、複数のクライアントが同じ OS イメージを同時にダウンロードすることが多い場合に使用できるネットワーク最適化の方法です。 マルチキャストを使用すると、OS イメージが配布ポイントによってマルチキャストされるので、複数のコンピューターで同時にダウンロードされます。 この動作は、各クライアントが配布ポイントから別の接続を介してイメージのコピーをダウンロードすることの代わりです。

次の OS の展開シナリオでは、マルチキャストを使用してネットワーク経由でオペレーティング システムを展開します。

- [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)

いずれかの OS の展開シナリオの手順を完了します。 その後、次のセクションを使用して、マルチキャストをサポートします。

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a> マルチキャスト用の配布ポイントを構成する

マルチキャストを使用するには、1 つ以上の配布ポイントをマルチキャストをサポートするように構成します。 詳細については、[配布ポイントのインストールと構成](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)に関するページを参照してください。

マルチキャストをサポートするために必要なポートの一覧については、「[ポート](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2)」を参照してください。

## <a name="prepare-an-os-image-for-multicast"></a>マルチキャスト用に OS イメージを準備する

マルチキャストをサポートするように、OS イメージを構成する必要があります。 詳細については、「[マルチキャスト展開用に OS イメージを準備する](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast)」を参照してください。

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> タスク シーケンスの展開

ターゲット コレクションに OS を展開します。 詳細については、「 [Deploy a task sequence](deploy-a-task-sequence.md)」をご覧ください。

## <a name="next-steps"></a>次のステップ

[OS 展開のユーザー エクスペリエンス](../understand/user-experience.md)
