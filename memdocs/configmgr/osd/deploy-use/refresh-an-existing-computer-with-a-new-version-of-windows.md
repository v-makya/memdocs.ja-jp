---
title: 既存のコンピューターの OS を更新する
titleSuffix: Configuration Manager
description: Configuration Manager でいくつかの方法を使用して、既存のコンピューターのパーティション分割とフォーマットを行い、そのコンピューターに新しい OS をインストールすることができます。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5972f930e0f8026f0ca1004d797bf34605af201e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697842"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>新しいバージョンの Windows で既存のコンピューターを更新する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager を使用すると、既存のコンピューターのパーティション分割とフォーマットを行い、新しい OS をインストールできます。 このプロセスは、*再イメージ化*または*ワイプおよび読み込み*と呼ばれることがあります。 このシナリオでは、PXE、起動可能なメディア、またはソフトウェア センターなど、多数のさまざまな展開方法を選べます。 また、状態移行ポイントを使用して設定を保存し、その設定を新しい OS に復元することもできます。

適切な OS 展開シナリオを選択するには、「[エンタープライズ オペレーティング システムを展開するシナリオ](scenarios-to-deploy-enterprise-operating-systems.md)」をご覧ください。  

## <a name="plan"></a><a name="BKMK_Plan"></a> プラン  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>インフラストラクチャの要件の計画と実装

OS を展開する前に、いくつかのインフラストラクチャ要件を満たす必要があります。 要件としては、Windows ADK、ユーザー状態移行ツール (USMT)、Windows 展開サービス (WDS) などがあります。 詳細については、[OS 展開のインフラストラクチャ要件](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)に関するページを参照してください。  

### <a name="install-a-state-migration-point"></a>状態移行ポイントのインストール

既存のコンピューターから設定をキャプチャし、新しい OS にその設定を復元する場合、状態移行ポイントの使用を検討します。 詳細については、「[状態移行ポイント](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)」を参照してください。  

## <a name="configure"></a><a name="BKMK_Configure"></a> 構成  

### <a name="prepare-a-boot-image"></a>ブート イメージの準備

ブート イメージによって、Windows PE 環境でコンピューターが起動されます。 Windows PE は最小限の OS であり、限られたコンポーネントとサービスが含まれています。 Windows PE から、Configuration Manager でコンピューターにフル Windows OS をインストールできます。

詳細については、以下の記事を参照してください。

- [ブート イメージの管理](../get-started/manage-boot-images.md)

- [ブート イメージのカスタマイズ](../get-started/customize-boot-images.md)

- [コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>OS イメージの準備

OS イメージには、対象コンピューターに OS をインストールするために必要なファイルが含まれています。

詳細については、以下の記事を参照してください。

- [OS イメージの管理](../get-started/manage-operating-system-images.md)

- [コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>OS を展開するためのタスク シーケンスの作成

タスク シーケンスを使用すると、OS のインストールを自動化できます。 選択した展開方法に応じて、タスク シーケンスに追加の考慮事項があります。

詳細については、以下の記事を参照してください。

- [OS をインストールするタスク シーケンスの作成](create-a-task-sequence-to-install-an-operating-system.md)

- [ユーザー状態の管理](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a> デプロイ

- OS を展開するには、次の展開方法のいずれかを使用します。  

  - [PXE を使用したネットワーク経由での Windows の展開](use-pxe-to-deploy-windows-over-the-network.md)  

  - [マルチキャストを使用した、ネットワーク経由での Windows の展開](use-multicast-to-deploy-windows-over-the-network.md)  

  - [工場出荷時の OEM 用、または現地保管場所用のイメージの作成](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [ネットワークではなくスタンドアロン メディアを使用した Windows の展開](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [起動可能なメディアを使用したネットワーク経由での Windows の展開](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [ソフトウェア センターを使用したネットワーク経由での Windows の展開](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>モニター  

詳細については、[OS デプロイの監視](monitor-operating-system-deployments.md)に関するページを参照してください。  

> [!Note]
> UEFI デバイスを再イメージ化すると、Windows ブート マネージャーによってブート ローダーに新しいエントリが作成されます。 この動作は、テスト環境や学生ラボなどで、デバイスを繰り返し再イメージ化する場合に最も顕著になります。 一般に、デバイスのパフォーマンスや使用状況には影響しません。 一覧が大きくなりすぎると、一部の特定のハードウェア デバイスで機能上の問題が発生する可能性があります。 たとえば、外部 USB ドライブを起動すること、つまり、一覧から現在のブート エントリを選択できなくなります。 Windows **bcdedit** コマンドを使用すると、未使用のブート エントリをクリアできます。 詳細については、「[BCDEdit/deletevalue](/windows-hardware/drivers/devtest/bcdedit--deletevalue)」を参照してください。<!-- 2841926 -->