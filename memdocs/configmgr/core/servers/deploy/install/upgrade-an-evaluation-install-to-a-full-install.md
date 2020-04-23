---
title: 評価版インストールのアップグレード
titleSuffix: Configuration Manager
description: 評価版の Configuration Manager を製品版にアップグレードする方法について説明します。
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8a42b2538ff1baaceb6895d371081ac2a444c5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700460"
---
# <a name="upgrade-an-evaluation-installation-of-configuration-manager-to-a-full-installation"></a>評価版の Configuration Manager を製品版にアップグレードする方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager を評価版としてインストールすると、180 日後に Configuration Manager コンソールが読み取り専用になります。ライセンス認証するには、セットアップの **[サイトのメンテナンス]** ページでプロダクト キーを入力する必要があります。 この 180 日の前または後のいつでも、評価版を製品版にアップグレードできます。  

> [!NOTE]  
>  Configuration Manager コンソールを Configuration Manager の評価版に接続すると、コンソールのタイトル バーに、評価版が期限切れになるまでの日数が表示されます。 ただし、この日数は自動的に更新されず、サイトに新しく接続した場合だけ更新されます。  

 評価版インストールを実行している次のサイトをアップグレードできます。  

-   中央管理サイト  
-   プライマリ サイト  

セカンダリ サイトは評価版としては処理されないため、親プライマリ サイトを製品版にアップグレードした後で、セカンダリ サイトを変更する必要はありません。  

ライセンスのある製品版に評価版をアップグレードするための前提条件:  

-   アップグレード中に使用する正しい製品が必要です。  
-   アカウントには、サイトがインストールされているコンピューターの**管理者**権限が必要です。  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Configuration Manager の評価版をライセンスのある製品版にアップグレードするには  

1.  サイト サーバーで、インストール フォルダー ( **%path%\BIN\X64**) から **SETUP.exe** (Configuration Manager のセットアップ) を実行します。 インストール メディアからセットアップを実行した場合はサイトのメンテナンス オプションを利用できないため、サイト サーバーの Configuration Manager フォルダーにある Setup のコピーを実行する必要があります。  
2.  **[開始する前に]** ページで、 **[次へ]** を選択します。  
3.  **[はじめに]** ページで **[Perform site maintenance or reset the Site (サイトのメンテナンスを実施するか、このサイトをリセットする)]** を選択し、 **[次へ]** を選択します。  
4.  **[サイトのメンテナンス]** ページで、 **[Upgrade the evaluation edition to a licensed edition (評価版を製品版にアップグレードする)]** を選び、正しいプロダクト キーを入力して、 **[次へ]** をクリックします。  
5.  **[マイクロソフト ソフトウェア ライセンス条項]** ページで、ライセンス条項を読んで同意し、 **[次へ]** を選択します。  
6.  **[構成]** ページで **[閉じる]** を選択してウィザードを終了します。  

    > [!NOTE]  
    >  アップグレードしたサイトに Configuration Manager コンソールを接続したままの場合は、サイトに接続し直さないと、コンソールのタイトル バーに評価版と表示される可能性があります。  
