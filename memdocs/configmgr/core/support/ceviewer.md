---
title: Collection Evaluation Viewer
titleSuffix: Configuration Manager
description: Collection Evaluation Viewer を使用すると、Configuration Manager のコレクション評価のプロセスを参照したり、トラブルシューティングできます。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707890"
---
# <a name="collection-evaluation-viewer"></a>Collection Evaluation Viewer

*適用対象:Configuration Manager (Current Branch)*

Collection Evaluation Viewer は、[Configuration Manager のツール](tools.md)の 1 つです。 これを使用すると、プライマリ サイト サーバーのコレクション評価のプロセスを参照したり、トラブルシューティングすることができます。

このツールには、次の情報が示されます。  

- 完全および増分コレクション評価用の履歴およびライブ情報の両方  

- 評価キューの状態  

- コレクション評価の完了時間  

- 現在評価されているコレクション  

- コレクションの評価が開始および完了する推定時間  



## <a name="about-collection-evaluation"></a>コレクション評価について

コレクション評価のプロセスは、そのメンバーを更新するために、コレクションのメンバーシップの規則を評価することによって実行されます。 サイトは、評価しているコレクションを 4 つの異なるいずれかのキューに配置します。  

- **Manual Queue (手動キュー)** :管理者がコンソールからの評価用に手動で選択したコレクション用  

- **新しいキュー**:新規に作成されたコレクション用  

- **Full Queue (完全なキュー)** :完全評価を行う予定のコレクション用  

- **Incremental Queue (増分キュー)** :増分評価を行うコレクション用  

上述のキューで、コレクションを評価するために実行されるスレッドは 4 つあります。 各キューには一連の配列が含まれ、各配列には評価するコレクションが含まれています。 キュー用に実行されているスレッドは、配列からコレクションを選択し、評価を実行します。 キューの長さは、キュー内の配列数を示します。



## <a name="requirements"></a>要件

- サイト サーバーでツールを実行する  

- 少なくとも**読み取り専用アナリスト** ロールを持つ管理者ユーザーがツールを実行する  

- ユーザーには、SQL のサイト データベースの**読み取り**権限も必要です



## <a name="usage"></a>使用方法

**CEViewer.exe** を実行します。 このツールのメイン メニューには、次のタブがあります。 

- [接続](#bkmk_connect): プライマリ サイト サーバーおよび SQL Server への最初の接続を確立します  

- [Full Evaluation (完全な評価)](#bkmk_full-eval):過去のすべての完全な評価の詳細な情報が一覧されます   

- [Incremental evaluation (増分評価)](#bkmk_incremental-eval):過去のすべての増分評価の詳細な情報が一覧されます  

- [All Queues (すべてのキュー)](#bkmk_all-q):4 つのすべてのキューの現在のコレクションの評価がまとめられます  

- [Manual Queue (手動キュー)](#bkmk_manual-q):手動キュー内の現在のコレクション評価の詳細な情報が一覧されます  

- [新しいキュー](#bkmk_new-q):新しいキューの現在のコレクション評価の詳細な情報が一覧されます  

- [Full Queue (完全なキュー)](#bkmk_full-q):完全なキューの現在のコレクション評価の詳細な情報が一覧されます  

- [Incremental Queue (増分キュー)](#bkmk_incremental-q):増分キューの現在のコレクション評価の詳細な情報が一覧されます  


### <a name="connect-tab"></a><a name="bkmk_connect"></a> [接続] タブ

このタブを使用すると、プライマリ サイト サーバーへの最初の接続を確立できます。 このツールは、サイト データベースをホストする SQL サーバーへの接続も確立します。

現在のサインイン ユーザー資格情報は、プライマリ サイト サーバーおよび SQL サーバーの両方への接続で使用されます。 中央管理サイトまたはセカンダリ サイトへの接続はサポートされていません。 それらのサイトでは、コレクションの評価プロセスは実行されません。

ツールによって接続が一度確立されると、ツールが SQL サーバーに接続されたことを確認する通知が Collection Evaluation Viewer の下部に表示されます。 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a> [Full Evaluation]\(完全な評価\) タブ

過去の完全コレクション評価に関する詳細な情報が表示されます。 次の 8 つの列があります。  

- **コレクション名**:コレクションの名前  

- **サイト ID**:コレクションのサイト ID   

- **実行時間**:過去のコレクションの秒での実行時間  

- **Last Evaluation Completion Time (最終評価の完了時間)** :最終評価の完了時間  

- **Next Evaluation Time (次回の評価時間)** :次回の完全な評価の開始時間  

- **Member Changes (メンバー変更)** :コレクションの最終評価時のメンバー変更。 これらの変更は、プラス (メンバーの追加) またはマイナス (メンバーの削除) のいずれかです。  

- **Last Member Change Time (メンバーの最終変更時間)** :コレクション評価でメンバーシップの変更があった最終時間  

- **Percent (パーセント)** :合計 (すべてのコレクション) の評価時間に対するこのコレクションの評価時間のパーセンテージ  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a> [Incremental evaluation]\(増分評価\) タブ

過去の増分コレクション評価に関する詳細な情報が表示されます。 次の 7 つの列があります。  

- **コレクション名**:コレクションの名前  

- **サイト ID**:コレクションのサイト ID   

- **実行時間**:過去のコレクションの秒での実行時間  

- **Last Evaluation Completion Time (最終評価の完了時間)** :最終評価の完了時間  

- **Member Changes (メンバー変更)** :コレクションの最終評価時のメンバー変更。 これらの変更は、プラス (メンバーの追加) またはマイナス (メンバーの削除) のいずれかです。  

- **Last Member Change Time (メンバーの最終変更時間)** :コレクション評価でメンバーシップの変更があった最終時間  

- **Percent (パーセント)** :合計 (すべてのコレクション) の評価時間に対するこのコレクションの評価時間のパーセンテージ  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a> [All Queues]\(すべてのキュー\) タブ

4 つのすべてのキューのライブ コレクションの評価がまとめられます。 これには 6 つのセクションがあります。  

- **Summary (概要)** :4 つのすべてのキューのすべてのコレクションのコレクションの合計数と、キューの長さが一覧されます  

- **Running Evaluation (実行中の評価)** :各キューでどのコレクションが現在評価されており、それがどのくらいの時間実行されているかを示します  

- **Manual Update (手動更新)** :評価されているコレクションの簡単な概要と、見込み完了時間、手動キューの評価順序を示します  

- **New Collection (新しいコレクション)** :評価されているコレクションの簡単な概要と、見込み完了時間、新しいコレクション キューの評価順序を示します  

- **Full Evaluation (完全な評価)** :評価されているコレクションの簡単な概要と、見込み完了時間、完全な評価キューの評価順序を示します  

- **Incremental evaluation (増分評価)** :評価されているコレクションの簡単な概要と、見込み完了時間、増分評価キューの評価順序を示します  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a> [Manual Queue]\(手動キュー\) タブ

現在評価されている、手動のコレクション評価に関する情報が表示されます。 リスト内の順序は、コレクションが評価される順序です。 これには 4 つの列があります。  

- **コレクション名**:コレクションの名前  

- **サイト ID**:コレクションのサイト ID   

- **Estimated Completion Time (推定完了時間)** :評価の推定完了時間  

- **予想実行時間**:評価に予想される、日:時間:分:秒の形式での時間  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a> [新しいキュー] タブ

現在評価されている、新しいコレクション評価に関するライブ情報が表示されます。 リスト内の順序は、コレクションが評価される順序です。 これには 4 つの列があります。  

- **コレクション名**:コレクションの名前  

- **サイト ID**:コレクションのサイト ID   

- **Estimated Completion Time (推定完了時間)** :評価の推定完了時間  

- **予想実行時間**:評価に予想される、日:時間:分:秒の形式での時間  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a> [Full Queue]\(完全なキュー\) タブ

現在評価されている、完全コレクション評価に関する情報が表示されます。 リスト内の順序は、コレクションが評価される順序です。 これには 4 つの列があります。  

- **コレクション名**:コレクションの名前  

- **サイト ID**:コレクションのサイト ID   

- **Estimated Completion Time (推定完了時間)** :評価の推定完了時間  

- **予想実行時間**:評価に予想される、日:時間:分:秒の形式での時間  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a> [Incremental Queue]\(増分キュー\) タブ

現在評価されている、増分コレクション評価に関する情報が表示されます。 リスト内の順序は、コレクションが評価される順序です。 これには 4 つの列があります。  

- **コレクション名**:コレクションの名前  

- **サイト ID**:コレクションのサイト ID   

- **Estimated Completion Time (推定完了時間)** :評価の推定完了時間  

- **予想実行時間**:評価に予想される、日:時間:分:秒の形式での時間  



