---
title: マルチキャストを使用した、ネットワーク経由での Windows の展開
titleSuffix: Configuration Manager
description: Configuration Manager 環境内でマルチキャストを使用すると、複数のコンピューターがオペレーティング システム イメージを同時にダウンロードできるようになります。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f81b23d3783d397d83a3925b98c0c8f601fa4012
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703490"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager でマルチキャストを使用したネットワーク経由での Windows の展開

*適用対象:Configuration Manager (Current Branch)*

マルチキャストは、複数のクライアントで同じオペレーティング システム イメージを同時にダウンロードすることの多い Configuration Manager 環境で使用できる、ネットワーク最適化の方法です。 マルチキャストを使用すると、配布ポイントがデータのコピーを各々のクライアントに別々の接続で送信する代わりに、マルチキャストしますので、複数のコンピューターが同時にオペレーティング システム イメージをダウンロードすることになります。  

 次に挙げるオペレーティング システムの展開シナリオでは、マルチキャストを使用してネットワーク経由でオペレーティング システムを展開できます。  

- [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

  いずれかのオペレーティング システムの展開シナリオのステップを完了させてから、次のセクションを参照して、マルチキャストをサポートします。  

##  <a name="configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> マルチキャストをサポートする配布ポイントの構成  
 オペレーティング システムを展開するときにマルチキャストを使用するには、マルチキャストをサポートするように配布ポイントを構成する必要があります。 詳細については、[配布ポイントのインストールと構成](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)に関するページを参照してください。 マルチキャストをサポートするために必要なポートの一覧については、「[ポート](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2)」を参照してください。  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>マルチキャスト展開用のオペレーティング システム イメージの準備  
 マルチキャストをサポートするようにオペレーティング システム イメージ パッケージを構成するには、「[マルチキャスト展開用のオペレーティング システム イメージを準備する](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast)」を参照してください。  

##  <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> タスク シーケンスの展開  
 オペレーティング システムをターゲット コレクションに展開します。 詳細については、「 [Deploy a task sequence](deploy-a-task-sequence.md)」をご覧ください。  
