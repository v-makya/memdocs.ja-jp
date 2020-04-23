---
title: 移行対象を選択する
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch に移行できるデータと移行できないデータについて説明します。
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701770"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Configuration Manager Current Branch にデータを移行するかどうかを判断する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の移行では、作成したデータと構成を、サポートされているバージョンの Configuration Manager から新しい階層に転送するためのプロセスが提供されます。  これを使用して、次の操作を実行できます。  

-   複数の階層を 1 つに統合する。  

-   データと構成をラボの展開から運用環境の展開に移動する。

-   Configuration Manager Current Branch へのアップグレード パスのない Configuration Manager 2007 などの以前のバージョンの Configuration Manager、または System Center 2012 Configuration Manager (Configuration Manager Current Branch へのアップグレード パスがサポートされている) からデータと構成を移動します。  

配布ポイント サイト システムの役割と、配布ポイントをホストするコンピューターを除き、階層間で移行、転送、または共有できるインフラストラクチャ (サイト、サイト システムの役割、またはサイト システムの役割をホストするコンピューターを含む) はありません。  

 サーバー インフラストラクチャは移行できませんが、階層間で構成マネージャー クライアントを移行することはできます。 クライアントの移行には、ソース階層でクライアントが使用するデータを対象の階層に移行する処理と、クライアントが新しい階層にレポートするようにクライアント ソフトウェアのインストールまたは再割り当てを行う処理が必要です。

クライアントを新しい階層にインストールし、クライアントがそのデータを送信した後は、Configuration Manager で一意の Configuration Manager ID を使用して、以前に移行したデータを各クライアント コンピューターに関連付けることができます。  

 移行によって提供される機能は、構成と展開にこれまで投資してきた資産を維持しながら、(System Center 2012 Configuration Manager で最初に導入され、Configuration Manager に引き継がれている) 主要な変更点を最大限に活用するのに役立ちます。 これらの変更点には、より少ないサイトとリソースを使用するように簡素化された Configuration Manager 階層、64 ビット ハードウェア上で実行されるネイティブ 64 ビット コードの使用により強化されたプロセッシング機能などが含まれます。  

 移行がサポートされている Configuration Manager のバージョンの詳細については、「[移行の前提条件](../../core/migration/prerequisites-for-migration.md)」をご覧ください。  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a> Configuration Manager Current Branch に移行できるデータ

移行により、サポートされる Configuration Manager 階層間で大部分のオブジェクトを移行できます。 サポートされるバージョンの Configuration Manager 2007 のオブジェクトによっては、System Center 2012 Configuration Manager のスキーマとオブジェクト形式に準拠するように、移行されるインスタンスを変更する必要があります。

この変更は、ソース サイトのデータベース内のデータには影響しません。 サポートされているバージョンの System Center 2012 Configuration Manager または Configuration Manager Current Branch から移行されたオブジェクトは、変更する必要がありません。  

ソース階層の Configuration Manager のバージョンに基づいて移行できるオブジェクトを次に示します。 クエリと同様に、一部のオブジェクトは移行されません。 このような移行されないオブジェクトを引き続き使用するには、新しい階層で再作成する必要があります。 一部のクライアント データを含む、他のオブジェクトは、新しい階層でクライアントを管理するときに自動的に再作成されます。  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>System Center 2012 Configuration Manager または Configuration Manager Current Branch の現在のブランチから移行できるオブジェクト

-   System Center 2012 Configuration Manager およびそれ以降のバージョン用のアプリケーション  

-   System Center 2012 Configuration Manager およびそれ以降のバージョンの App-V 仮想環境  

-   資産インテリジェンスのカスタマイズ設定  

-   境界  

-   コレクション:サポートされているバージョンの System Center 2012 Configuration Manager または Configuration Manager Current Branch からコレクションを移行するには、オブジェクトの移行ジョブを使用します。  

-   コンプライアンス設定:  

    -   構成基準  

    -   構成項目  

-   展開  

-   オペレーティング システムの展開:  

    -   ブート イメージ  

    -   ドライバー パッケージ  

    -   ドライバー  

    -   画像  

    -   パッケージ  

    -   タスク シーケンス  

-   検索結果:保存された検索条件  

-   ソフトウェア更新プログラム:  

    -   展開  

    -   展開パッケージ  

    -   テンプレート  

    -   ソフトウェア更新プログラム一覧  

-   ソフトウェアの配布パッケージ  

-   ソフトウェア使用状況測定規則 (旧称「ソフトウェア メータリング規則」)  

-   仮想アプリケーション パッケージ  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Configuration Manager 2007 SP2 から移行できるオブジェクト

-   開示通知 (旧称「提供情報」)  

-   System Center 2012 Configuration Manager およびそれ以降のバージョン用のアプリケーション  

-   System Center 2012 Configuration Manager およびそれ以降のバージョンの App-V 仮想環境  

-   資産インテリジェンスのカスタマイズ設定  

-   境界  

-   コレクション:コレクションの移行ジョブを使用して、サポートされるバージョンの Configuration Manager 2007 からコレクションを移行します。  

-   コンプライアンス設定 (Configuration Manager 2007 では必要な構成管理とも呼ばれます):  

    -   構成基準  

    -   構成項目  

-   オペレーティング システムの展開:  

    -   ブート イメージ  

    -   ドライバー パッケージ  

    -   ドライバー  

    -   画像  

    -   パッケージ  

    -   タスク シーケンス  

-   検索結果:検索フォルダー  

-   ソフトウェア更新プログラム:  

    -   展開  

    -   展開パッケージ  

    -   テンプレート  

    -   ソフトウェア更新プログラム一覧  

-   ソフトウェアの配布パッケージ  

-   ソフトウェア使用状況測定規則 (旧称「ソフトウェア メータリング規則」)  

-   仮想アプリケーション パッケージ  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a> Configuration Manager Current Branch に移行できないデータ

次の種類のオブジェクトは移行できません。  

-   AMT クライアントのプロビジョニング情報  

-   次のような、クライアント上のファイル:  

    -   クライアント インベントリおよび履歴データ  

    -   クライアントのキャッシュ内のファイル  

-   クエリ  

-   サイトとオブジェクトの Configuration Manager 2007 セキュリティ権限とインスタンス  

-   SQL Server Reporting Services の Configuration Manager 2007 レポート  

-   Configuration Manager 2007 の Web レポート  

-   System Center 2012 Configuration Manager と Configuration Manager Current Branch のレポート  

-   System Center 2012 Configuration Manager と Configuration Manager Current Branch のロール ベース管理:  

    -   セキュリティ ロール  

    -   セキュリティ スコープ  
