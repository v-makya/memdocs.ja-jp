---
title: 既存のコンピューターの置き換えと設定の転送
titleSuffix: Configuration Manager
description: Configuration Manager で、起動可能なメディア、マルチキャスト、またはソフトウェア センターなどの展開方法から選択して、既存のコンピューターを新しいコンピューターに置き換えます。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 860ee3aeb255921ccd8bf3b1695a9647b514752f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124870"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Configuration Manager で既存のコンピューターを置き換え、設定を転送する

*適用対象:Configuration Manager (Current Branch)*

このトピックでは、Configuration Manager で既存のコンピューターを新しいコンピューターに置き換える一般的な手順を示します。 このシナリオでは、起動可能なメディア、マルチキャスト、またはソフトウェア センターなどのさまざまな展開方法から選択できます。 また、状態移行ポイントをインストールして設定を保存し、新しいオペレーティング システムをインストールした後、そこに復元することもできます。 適切なオペレーティング システムの展開シナリオがわからない場合は、「[エンタープライズ オペレーティング システムを展開するシナリオ](scenarios-to-deploy-enterprise-operating-systems.md)」を参照してください。  

 Windows の新しいバージョンで既存のコンピューターを更新する場合は、次のセクションを参考にします。  

##  <a name="plan"></a><a name="BKMK_Plan"></a> プラン  

-   **インフラストラクチャの要件の計画と実装**  

     オペレーティング システムを展開する前に解決しなければならないインフラストラクチャの要件として、Windows ADK、ユーザー状態移行ツール (USMT)、Windows 展開サービス (WDS)、サポートされているハード ディスクの構成などがあります。詳細については、「[オペレーティング システムの展開のインフラストラクチャ要件](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)」を参照してください。  

-   **状態移行ポイントのインストール (設定を転送する場合にのみ必要)**  

     既存のコンピューターから設定をキャプチャし、新しいオペレーティング システムにその設定を復元するときは、状態移行ポイントをインストールする必要があります。 詳細については、「[状態移行ポイント](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)」を参照してください。  

##  <a name="configure"></a><a name="BKMK_Configure"></a> 構成  

1.  **ブート イメージの準備**  

     ブート イメージは、Windows PE 環境 (コンポーネントやサービスが制限された最小オペレーティング システム) でコンピューターを起動して、完全な Windows オペレーティング システムをコンピューターにインストールできるようにします。 オペレーティング システムを展開する場合は、使用するブート イメージを選択し、配布ポイントにそのイメージを配布する必要があります。 ブート イメージを準備するには、次のものを使用します。  

    -   イメージの詳細については、「[ブート イメージの管理](../get-started/manage-boot-images.md)」を参照してください。  

    -   ブート イメージをカスタマイズする方法の詳細については、「[ブート イメージのカスタマイズ](../get-started/customize-boot-images.md)」を参照してください。  

    -   配布ポイントへブート イメージを配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)」をご覧ください。  

2.  **オペレーティング システム イメージの準備**  

     オペレーティング システム イメージには、セットアップ先のコンピューターにオペレーティング システムをインストールするために必要なファイルが含まれています。 オペレーティング システム イメージを準備するには、次のものを使用します。  

    -   オペレーティング システム イメージを作成する方法の詳細については、「[オペレーティング システム イメージを管理する](../get-started/manage-operating-system-images.md)」を参照してください。  

    -   オペレーティング システム イメージを配布ポイントに配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)」をご覧ください。  

3.  **オペレーティング システムをネットワーク経由で展開するためのタスク シーケンスの作成**  

     ネットワーク経由でのオペレーティング システムのインストールを自動化するタスク シーケンスを使用します。 「[オペレーティング システムをインストールするタスク シーケンスの作成](create-a-task-sequence-to-install-an-operating-system.md)」の手順でオペレーティング システムを展開するためのタスク シーケンスを作成します。 選択した展開方法に応じて、タスク シーケンスに追加の考慮事項があります。  

    > [!NOTE]  
    >  このシナリオでは、ユーザー設定とファイルをキャプチャして復元する場合、状態移行ポイントを使用するか、またはファイルをローカルに保存するかのいずれかを選択できます。 詳細については、「[ユーザー状態の管理](../get-started/manage-user-state.md)」を参照してください。  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> デプロイ  

-   オペレーティング システムを展開するには、次の展開方法のいずれかを使用します。  

    -   [ソフトウェア センターを使用したネットワーク経由での Windows の展開](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [起動可能なメディアを使用したネットワーク経由での Windows の展開](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [マルチキャストを使用した、ネットワーク経由での Windows の展開](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [工場出荷時の OEM 用、または現地保管場所用のイメージの作成](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>モニター  

-   **タスク シーケンスの展開の監視**  

     オペレーティング システムをインストールするために、タスク シーケンスの展開を監視するには、「[オペレーティング システムの展開の監視](monitor-operating-system-deployments.md)」を参照してください。  
