---
title: Technical Preview 1602 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1602 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 65c8feb6381c59cc1fef3fb07a3ad8c33fc67e65
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705690"
---
# <a name="capabilities-in-technical-preview-1602-for-configuration-manager"></a>Configuration Manager の Technical Preview 1602 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1602 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。  

 このバージョンでお試しいただける新機能を次に示します。  

##  <a name="improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a> モバイル デバイス管理の機能強化  

### <a name="ios-activation-lock"></a>iOS のアクティベーション ロック  
 Configuration Manager は、iOS 7.1 以降のデバイス向けの iPhone を探すアプリの機能である iOS のアクティベーション ロックを管理するために役立ちます。 iPhone を探すアプリをデバイスで使用すると、アクティブ化ロックが自動的に有効になります。 有効になると、ユーザーの Apple ID とパスワードを入力しない限り、以下の操作を実行できなくなります。  

- iPhone を探すアプリをオフにする  

- デバイスを消去する  

- ディスクを再アクティブ化する  

  Configuration Manager では、iOS 7.1 以降を実行している監視対象と監視対象外の両方のデバイスのアクティベーション ロックの状態を要求できます。 監視対象のデバイスの場合、Intune では、アクティベーション ロックのバイパス コードを取得し、直接デバイスに発行できます。  

##  <a name="improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a> バージョン 1602 でのソフトウェア センターの機能強化  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>ソフトウェア センターから PC コンピューターとユーザーのポリシーを更新する  
 新しいオプションである **同期ポリシー** が、ソフトウェア センターの **[オプション]**  >  **[コンピューターのメンテナンス]** ページに追加されました。これにより、PC では Configuration Manager コンピューターとユーザーのポリシーが更新されます。  

##  <a name="improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a> Windows 10 サービスの機能強化  
 1602 Technical Preview では、次の Windows 10 サービスの機能が追加されました。  

-   サービス プランの新しいフィルター オプション。  **言語**、**必須**、**タイトル**ごとにフィルター処理できるようになりました。 指定された条件を満たすアップグレードだけが、関連付けられている展開に追加されます。  

-   ソフトウェア更新プログラムの同期の**アップグレード**の分類を選ぶと、ソフトウェア更新プログラムが正常に同期され、Windows 10 サービスが適切に動作するためには、WSUS [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) が必要なことを通知する警告ダイアログが表示されます。  このダイアログから、修正プログラムのサポート技術情報の記事に移動できます。  

-   利用可能な Windows 10 アップグレードは、Configuration Manager コンソールの **[Windows 10 のサービス]**  \  **[すべての Windows 10 更新プログラム]** ノードにのみ表示されるようになりました。 これらの更新プログラムは、[**ソフトウェア更新プログラム** \ **すべてのソフトウェアの更新**] ノードには表示されなくなりました。  

-   Windows 10 Upgrade パッケージを開始するエンド ユーザーには、オペレーティング システムがアップグレードされることを通知するダイアログが表示されます。  
