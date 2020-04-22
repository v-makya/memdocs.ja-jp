---
title: ソフトウェア センターのアプリケーションを共有する
titleSuffix: Configuration Manager
description: Configuration Manager でソフトウェア センターのアプリケーションのリンクを共有します。
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689240"
---
# <a name="share-an-application-from-software-center"></a>ソフトウェア センターからのアプリケーションの共有

*適用対象:Configuration Manager (Current Branch)* <!-- 1706 -->

アプリケーションの詳細ビューで、![[共有]](media/share15.png) **[共有]** ボタンを使用して、ソフトウェア センターのアプリケーションのハイパーリンクをコピーすることができます。 共有できるのはアプリケーションのハイパーリンクのみです。 アプリケーションが使用できなくなった場合は、ハイパーリンクによって、アプリケーションの利用不可メッセージを含むウィンドウが開きます。

1. **[アプリケーション]** を選択し、アプリケーションを選択します。
2. ![[共有]](media/share15.png) **[共有]** ボタンをクリックします。
3. ウィンドウ内の **[コピー]** をクリックします。
4. メールに URL を貼り付けて、アプリケーションを共有します。  

> [!TIP]  
>  Outlook 電子メールでリンクを作成するには、**Ctrl** + **K** キーを押して、URL を貼り付けます。  
>  
> 既定では、受信者がリンクをクリックすると、ソフトウェア センターのプロトコルに関するセキュリティ アラートが Outlook に表示されます。 お使いの環境でこれを防ぐには、信頼されているプロトコル キーをレジストリに追加します。 たとえば、 `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:` と記述します。  
