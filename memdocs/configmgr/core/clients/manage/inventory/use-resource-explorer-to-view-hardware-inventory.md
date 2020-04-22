---
title: リソース エクスプローラーの使用方法
titleSuffix: Configuration Manager
description: Configuration Manager でリソース エクスプローラーを使用して、ハードウェア インベントリを表示します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690100"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Configuration Manager でリソース エクスプローラーを使用して、ハードウェア インベントリを表示する方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager でリソース エクスプローラーを使用して、ハードウェア インベントリに関する情報を表示します。 サイトでは、階層内のクライアントからこの情報が収集されます。  

> [!Tip]  
>  接続するクライアントでハードウェア インベントリ サイクルが実行されるまで、リソース エクスプローラーではデータが表示されません。  



## <a name="overview"></a>概要

リソース エクスプローラーには、ハードウェア インベントリに関する次のセクションが含まれます。  

- **ハードウェア**:指定したクライアント デバイスから収集された、最新のハードウェア インベントリが表示されます。  

    - **[ワークステーションのステータス]** ノードには、デバイスからの最後のハードウェア インベントリの時刻と日付が表示されます。  

- **ハードウェア履歴**:最後のハードウェア インベントリ サイクル以降に変更されたインベントリ項目の履歴。  

    - 項目を展開して、**現在**のノードと、過去の日付の 1 つ以上のノードを表示します。 現在のノードの情報と、履歴ノードの 1 つを比較して、変更された項目を確認します。  

> [!NOTE]  
> 既定では、90 日間非アクティブだったハードウェア インベントリが Configuration Manager によって削除されます。 **[期限切れのインベントリ履歴の削除]** サイト メンテナンス タスクでこの日数を調整します。 詳細については、[メンテナンス タスク](../../../servers/manage/maintenance-tasks.md)に関するページを参照してください。  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a> リソース エクスプローラーを開く方法   

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス]** ノードを選択します。 **[デバイス コレクション]** ノードで任意のコレクションを選択することもできます。  

2.  デバイスを選択します。 リボンの **[ホーム]** タブにある **[デバイス]** グループで、 **[開始]** をクリックして **[リソース エクスプローラー]** を選択します。   

> [!Tip]  
> リソース エクスプローラーで、追加アクションの右側の結果ウィンドウにある項目を右クリックします。 **[プロパティ]** をクリックして、別の形式でその項目を表示します。  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a> 大きな整数値の使用
<!--1357880-->
Configuration Manager バージョン 1802 以前の場合、ハードウェア インベントリには、4,294,967,296 (2^32) より大きな整数に対して制限があります。 この制限は、バイト単位のハード ドライブ サイズなどの属性も対象になる場合があります。 管理ポイントではこの制限を超える整数値が処理されないため、値がデータベースに格納されません。 

バージョン 1806 以降では、制限が 18,446,744,073,709,551,616 (2^64) に引き上げられました。 

合計ディスク サイズなど、値が変更されないプロパティの場合は、サイトのアップグレード後に、すぐに値を確認することはできません。 ほとんどのハードウェア インベントリは、累計レポートです。 クライアントは、変更された値のみを送信します。 この動作を回避するには、同じクラスにもう 1 つのプロパティを追加します。 これにより、クライアントでは、変更されたクラス内のすべてのプロパティを更新するようになります。 



## <a name="see-also"></a>関連項目

Linux および UNIX を実行するクライアントからハードウェア インベントリを表示する方法については、[Linux および UNIX サーバーのクライアントを監視する方法](../monitor-clients-for-linux-and-unix-servers.md)に関するページを参照してください。  

リソース エクスプローラーにはソフトウェア インベントリも表示されます。 詳細については、[リソース エクスプローラーを使用してソフトウェア インベントリを表示する方法](use-resource-explorer-to-view-software-inventory.md)に関するページを参照してください。
