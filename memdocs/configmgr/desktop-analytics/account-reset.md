---
title: アカウントをリセットする方法
titleSuffix: Configuration Manager
description: Desktop Analytics アカウントをリセットする方法について説明します。
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 29f108254e3201925917a0546dd96d36a19763b6
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268880"
---
# <a name="how-to-reset-your-account"></a>アカウントをリセットする方法

<!-- 3733897 -->

お使いの環境に Desktop Analytics を設定したが、オンボードと登録をやり直す場合は、このプロセスを使用してアカウントをリセットします。

## <a name="prerequisites"></a>[前提条件]

**グローバル管理者**だけが、Azure portal でアカウントをリセットできます。

## <a name="behaviors"></a>動作

- このプロセスによって、既存の Azure AD ユーザー、アプリ、またはアクセス許可が変更されることはありません。

- 新しいワークスペースを追加することを選択した場合は、資産に関する次のユーザー入力はすべて保持されません。
    - 重要度
    - Owner
    - アップグレードの決定
    - 修復メモ

## <a name="process"></a>プロセス

1. Microsoft 365 デバイス管理で、**グローバル管理者**ロールを持つユーザーとして、[Desktop Analytics ポータル](https://aka.ms/desktopanalytics)を開きます。

1. **[グローバル設定]** メニューで、 **[接続済みサービス]** を選択します。 [デバイスの登録] セクションで、 **[リセット]** オプションを選択します。

1. 続行すると、アカウントがリセットされます。 Desktop Analytics をもう一度設定する必要があります。

## <a name="next-steps"></a>次のステップ

リセットしたら、ページを更新し、オンボード プロセスを再実行します。 詳しくは、「[Desktop Analytics をセットアップする方法](set-up.md)」をご覧ください。

このプロセス中に問題が発生した場合は、Microsoft サポートにお問い合わせください。
