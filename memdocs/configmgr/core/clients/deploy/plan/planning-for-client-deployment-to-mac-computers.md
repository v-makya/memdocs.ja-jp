---
title: Mac コンピューターへのクライアント展開の計画
titleSuffix: Configuration Manager
description: Configuration Manager での Mac コンピューターへのクライアント展開の計画。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693720"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Configuration Manager での Mac コンピューターへのクライアント展開の計画

*適用対象:Configuration Manager (Current Branch)*

Mac OS X オペレーティング システムを実行する Mac コンピューターに Configuration Manager クライアントをインストールして、次の管理機能を使用できます。  

- **ハードウェア インベントリ**  

   Configuration Manager ハードウェア インベントリを使用して、Mac コンピューターのハードウェアと、インストールされているアプリケーションに関する情報を収集できます。 この情報を Configuration Manager コンソールのリソース エクスプローラーで確認し、コレクション、クエリ、レポートの作成に使用できます。 詳細については、[リソース エクスプローラーを使用してハードウェア インベントリを表示する方法](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)に関するページをご覧ください。  

   Configuration Manager は、Mac コンピューターから次のハードウェア情報を収集します。  

  -   プロセッサ  

  -   コンピューター システム  

  -   ディスク ドライブ  

  -   ディスク パーティション  

  -   ネットワーク アダプター  

  -   オペレーティング システム  

  -   サービス  

  -   プロセス  

  -   インストール済みソフトウェア  

  -   コンピューター システム製品  

  -   USB コントローラー  

  -   USB デバイス  

  -   CD-ROM ドライブ  

  -   ビデオ コントローラー  

  -   デスクトップ モニター  

  -   ポータブル バッテリー  

  -   物理メモリ  

  -   プリンター  

  > [!IMPORTANT]  
  >  ハードウェア インベントリ時に Mac コンピューターから収集されるハードウェア情報を拡張することはできません。  

- **コンプライアンス設定**  

   Configuration Manager コンプライアンス設定を使用して、コンプライアンスを確認し、Mac OS X 環境設定 (.plist) の設定を修復できます。 たとえば、Safari Web ブラウザーのホーム ページの設定を強制したり、Apple ファイアウォールを有効にしたりできます。 また、シェル スクリプトを使用して、Mac OS X の設定を監視、修復することもできます。  

- **アプリケーション管理**  

   Configuration Manager は、Mac コンピューターにソフトウェアを展開できます。 Mac コンピューターには、次のソフトウェア形式を展開できます。  

  -   Apple Disk Image (.DMG)  

  -   Meta Package File (.MPKG)  

  -   Mac OS X Installer Package (.PKG)  

  -   Mac OS X Application (.APP)  

  Mac コンピューターに Configuration Manager クライアントをインストールする場合、Windows ベースのコンピューターにインストールされた Configuration Manager クライアントでサポートされる次の管理機能を使用できません。  

- クライアント プッシュ インストール  

- オペレーティング システムの展開  

- ソフトウェア更新プログラム  

  > [!NOTE]  
  >  必要な Mac OS X ソフトウェア更新プログラムを Mac コンピューターに展開するには、Configuration Manager アプリケーション管理を使用します。 また、コンプライアンス設定を使用して、必要なソフトウェア更新プログラムを常にコンピューターに適用することもできます。  

- メンテナンス期間  

- リモート コントロール  

- 電源管理  

- クライアント ステータスのクライアント チェックと修復  

  Configuration Manager Mac クライアントのインストールおよび構成方法の詳細については、「[Mac にクライアントを展開する方法](../../../../core/clients/deploy/deploy-clients-to-macs.md)」を参照してください。
