---
title: ラボ環境での評価
titleSuffix: Configuration Manager
description: 組織で使用するために Configuration Manager を評価するラボ環境を作成します。
ms.date: 02/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd238319ba064f57911eee58e1299e17a2ce5b60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694600"
---
# <a name="evaluate-configuration-manager-by-building-your-own-lab-environment"></a>独自のラボ環境を構築して Configuration Manager を評価する

*適用対象:Configuration Manager (Current Branch)*

 組織で使用するために Configuration Manager を評価するラボ環境を作成する方法について説明します。  

 Configuration Manager は、ユーザー、デバイス、ソフトウェアを管理するための複雑で強力なツールです。 概念の理解を現場での実践に結び付けることができるように、完全な展開の前に Configuration Manager の詳細な評価をすることをお勧めします。  

 このガイドは、主に、企業環境内で Configuration Manager の使用を評価する次のような管理者を対象にしています。  

-   PC、サーバー、およびモバイル デバイスを完全に管理するソリューションを必要とする管理者  

-   オンプレミス デバイス管理のセキュリティと、クラウドベースのデバイス管理の柔軟性を必要とする高セキュリティ業界の管理者  

-   オンプレミス サーバー アーキテクチャのスケールアップの管理を必要とする管理者  

## <a name="what-this-lab-does"></a>このラボの実行内容  
 このラボ環境を作成する主な目的は、Configuration Manager の使用を開始するための一般的な知識を提供すること、および Configuration Manager についての理解を深めることです。 次の 2 台のサーバーを使用して、最新バージョンの Configuration Manager の簡易化した構成を使って説明します。  

-   Active Directory、ドメイン コントローラー、および DNS サーバーをホストするサーバー  

-   Configuration Manager と、関連するすべての SQL Server コンポーネントをホストするサーバー  

クライアント コンピューターは Hyper-V 内にインストールされます。 ラボ自体は、単一のサーバーで完全に仮想化されたシステムとして実行することもできます。  

## <a name="what-this-lab-does-not-do"></a>このラボで実行しないこと  
 このラボでは、Configuration Manager のすべてのシナリオについて説明しません。 すぐにアクティブな環境に移行することは想定されていません。  

 このラボを構築すると、機能し、作業できる環境が整います。 ただし、この環境は、システム パフォーマンス、ハード ディスク領域の管理、SQL Server の記憶域などの要因に対して最適化されません。  

##  <a name="recommended-reading-before-you-build-the-lab"></a><a name="BKMK_EvalRec"></a>ラボを構築する前の推奨資料  
 「[Configuration Manager のドキュメント](https://docs.microsoft.com/sccm/)」には豊富なコンテンツがあります。 ラボを構築する前に、このライブラリから次のトピックを読むことをお勧めします。  

-   「[Configuration Manager の概要](../../core/understand/introduction.md)」。Configuration Manager コンソール、エンドユーザー ポータル、シナリオ例の主要な概念について説明しています。  

-   「[Configuration Manager の特徴と機能](../../core/plan-design/changes/features-and-capabilities.md)」。Configuration Manager の主な管理機能について説明しています。  

-   「[Configuration Manager の基本](../../core/understand/fundamentals.md)」。知識を強化します。  

-   「[Configuration Manager のロール ベース管理の基礎](../../core/understand/fundamentals-of-role-based-administration.md)」。セキュリティ ロールの重要性について説明しています。  

-   「[System Center Configuration Manager でのコンテンツ管理の基本的な概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)」。コンテンツ管理について説明しています。  

-   「[クライアントが Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」。展開全体での日常のタスクを適切にサポートする方法を説明しています。  
