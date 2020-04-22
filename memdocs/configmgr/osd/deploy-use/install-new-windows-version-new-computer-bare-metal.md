---
title: 新しいコンピューターに Windows をインストールする
titleSuffix: Configuration Manager
description: Configuration Manager で PXE、OEM、またはスタンドアロン メディアを使用して、新しいコンピューター (ベア メタル) にオペレーティング システムをインストールします。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a70269839b4a550fbef4dc5cab1b7ff3d426d87
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690670"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Configuration Manager を使用して、新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする

*適用対象:Configuration Manager (Current Branch)*

このトピックでは、Configuration Manager で新しいコンピューターにオペレーティング システムをインストールする一般的な手順を示します。 このシナリオでは、PXE、OEM、スタンドアロン メディアなど、展開のさまざまな方法の中から選択することができます。 適切なオペレーティング システムの展開シナリオがわからない場合は、「[エンタープライズ オペレーティング システムを展開するシナリオ](scenarios-to-deploy-enterprise-operating-systems.md)」を参照してください。  

Windows の新しいバージョンで既存のコンピューターを更新する場合は、次のセクションを参考にします。  

##  <a name="plan"></a><a name="BKMK_Plan"></a> プラン  

-   **インフラストラクチャの要件の計画と実装**  

     オペレーティング システムを展開する前に解決しなければならないインフラストラクチャの要件として、Windows ADK、Windows 展開サービス (WDS)、Windows 展開サービス (WDS)、サポートされているハード ディスクの構成などがあります。詳細については、「[オペレーティング システムの展開のインフラストラクチャ要件](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)」を参照してください。

##  <a name="configure"></a><a name="BKMK_Configure"></a> 構成  

1.  **ブート イメージの準備**  

     ブート イメージは、Windows PE 環境 (コンポーネントやサービスが制限された最小オペレーティング システム) でコンピューターを起動して、完全な Windows オペレーティング システムをコンピューターにインストールできるようにします。   オペレーティング システムを展開する場合は、使用するブート イメージを選択し、配布ポイントにそのイメージを配布する必要があります。 ブート イメージを準備するには、次のものを使用します。  

    -   イメージの詳細については、「[ブート イメージの管理](../get-started/manage-boot-images.md)」を参照してください。  

    -   ブート イメージをカスタマイズする方法の詳細については、「[ブート イメージのカスタマイズ](../get-started/customize-boot-images.md)」を参照してください。  

    -   配布ポイントへブート イメージを配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)」をご覧ください。  

2.  **オペレーティング システム イメージの準備**  

     オペレーティング システム イメージには、セットアップ先のコンピューターにオペレーティング システムをインストールするために必要なファイルが含まれています。 オペレーティング システム イメージを準備するには、次のものを使用します。  

    -   オペレーティング システム イメージを作成する方法の詳細については、「[オペレーティング システム イメージを管理する](../get-started/manage-operating-system-images.md)」を参照してください。

    -   オペレーティング システム イメージを配布ポイントに配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)」をご覧ください。  

    > [!NOTE]
    > Windows の新規インストールは、インストール ソース ファイルから OS アップグレード パッケージを使って実行することもできますが、代わりに **install.wim** などの OS イメージを使ってください。
    >
    > OS アップグレード パッケージを使った Windows の新規インストールの展開は、引き続きサポートされますが、この方法と互換性があるドライバーに依存しています。 OS アップグレード パッケージから Windows をインストールする場合、ドライバーは、単純に Windows PE にいる間に挿入されるのと比較して、Windows PE にいる間にインストールされます。 一部のドライバーは、Windows PE にいる間にインストールすることはできません。 ドライバーが Windows PE にいる間のインストールと互換性がない場合は、代わりに OS イメージを使います。  

3.  **オペレーティング システムをネットワーク経由で展開するためのタスク シーケンスの作成**  

     ネットワーク経由でのオペレーティング システムのインストールを自動化するタスク シーケンスを使用します。 「[オペレーティング システムをインストールするタスク シーケンスの作成](create-a-task-sequence-to-install-an-operating-system.md)」の手順でオペレーティング システムを展開するためのタスク シーケンスを作成します。 選択した展開方法に応じて、タスク シーケンスに追加の考慮事項があります。  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> デプロイ  

-   オペレーティング システムを展開するには、次の展開方法のいずれかを使用します。  

    -   [PXE を使用したネットワーク経由での Windows の展開](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [マルチキャストを使用した、ネットワーク経由での Windows の展開](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [工場出荷時の OEM 用、または現地保管場所用のイメージの作成](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [ネットワークではなくスタンドアロン メディアを使用した Windows の展開](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [起動可能なメディアを使用したネットワーク経由での Windows の展開](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>モニター  

-   **タスク シーケンスの展開の監視**  

     オペレーティング システムをインストールするために、タスク シーケンスの展開を監視するには、「[オペレーティング システムの展開の監視](monitor-operating-system-deployments.md)」を参照してください。  
