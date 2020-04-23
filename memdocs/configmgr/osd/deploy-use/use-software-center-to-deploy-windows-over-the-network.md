---
title: ソフトウェア センターを使用したネットワーク経由での Windows の展開
titleSuffix: Configuration Manager
description: オペレーティング システムをソフトウェア センターに展開して、既存のコンピューターを新しいバージョンの Windows に更新したり、Windows を最新バージョンにアップグレードしたりできます。
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709030"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager でソフトウェア センターを使用したネットワーク経由での Windows の展開

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager でオペレーティング システムをインストールするタスク シーケンスは、ソフトウェア センターで使用可能にすることができます。 次のオペレーティング システムの展開シナリオでは、オペレーティング システムをソフトウェア センターに展開することができます。

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md)

いずれかのオペレーティング システムの展開シナリオの手順を実行します。 その後で、次のセクションを使用して、ソフトウェア センターで使用可能な展開を準備します。

## <a name="configure-deployment-settings"></a>展開の設定の構成  
オペレーティング システムの展開をソフトウェア センターで使用できるようにするには、展開を構成します。 展開は、ソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで構成することができます。 **[利用できるようにする項目]** 設定で、 **[Configuration Manager クライアントのみ]** または **[Configuration Manager クライアント、メディア、PXE]** のいずれかを構成します。 システムでオペレーティング システムが展開された後、オペレーティング システムは、ソフトウェア センターにターゲット コレクションのメンバーとして表示されます。

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> コンピューターへのタスク シーケンスの展開  
オペレーティング システムをターゲット コレクションに展開します。 詳細については、「 [Deploy a task sequence](deploy-a-task-sequence.md)」をご覧ください。 ソフトウェア センターでオペレーティング システムを展開するとき、展開が必須か使用可能かを設定することができます。

-   **必要な展開**:必須の展開では、ソフトウェア センターでオペレーティング システムが利用可能になりますが、構成された割り当てスケジュールで自動的に開始されます。

-   **利用可能な展開**:オペレーティング システムはソフトウェア センターで使用可能になり、ユーザーはオンデマンドでインストールすることができます。
