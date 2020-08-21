---
title: ソフトウェア センターを使用したネットワーク経由での Windows の展開
titleSuffix: Configuration Manager
description: OS をソフトウェア センターから展開して、既存のコンピューターを新しいバージョンの Windows に更新したり、Windows を最新バージョンにアップグレードしたりします。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124603"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager でソフトウェア センターを使用したネットワーク経由での Windows の展開

*適用対象:Configuration Manager (Current Branch)*

OS をインストールするタスク シーケンスをソフトウェア センターで使用できるようにすることができます。 ユーザーは、次の OS 展開シナリオで、ソフトウェア センターからタスク シーケンスを実行できます。

- [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md)

- [OS 以外の展開用タスク シーケンスの作成](create-a-task-sequence-for-non-operating-system-deployments.md)

これらの OS の展開シナリオのいずれかで手順を完了します。 その後で、次のセクションを使用して、ソフトウェア センターで使用可能な展開を準備します。

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> タスク シーケンスの展開

ターゲット コレクションにタスク シーケンスを展開します。 詳細については、「 [Deploy a task sequence](deploy-a-task-sequence.md)」をご覧ください。

展開の **[展開の設定]** ページの **[利用できるようにする項目]** の設定で、次のいずれかのオプションを選択します。

- Configuration Manager クライアントのみ

- Configuration Manager クライアント、メディア、PXE

また、展開が必要か使用可能かを構成します。

- 必要な展開: 必要な展開により、タスク シーケンスがソフトウェア センターで使用できるようになります。 構成された期限に自動的に開始します。

- 利用可能な展開: タスク シーケンスは、ソフトウェア センターで使用可能であり、ユーザーはオンデマンドでこれをインストールできます。

展開を作成した後、ターゲット コレクションのクライアントにより、タスク シーケンスがソフトウェア センターに表示されます。

## <a name="next-steps"></a>次のステップ

[OS 展開のユーザー エクスペリエンス](../understand/user-experience.md#software-center)
