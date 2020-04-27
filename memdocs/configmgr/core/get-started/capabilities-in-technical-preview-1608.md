---
title: Technical Preview 1608 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1608 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074182"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Configuration Manager の Technical Preview 1608 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1608 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。      このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    


**このバージョンでお試しいただける新機能を次に示します。**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>ConfigMgr クライアントのキャプチャの準備タスク シーケンス ステップの向上  
ConfigMgr クライアントの準備手順で、キー情報だけではなく、Configuration Manager クライアントが完全に削除されるようになりました。 タスク シーケンスでキャプチャしたオペレーティング システム イメージを展開すると、毎回新しい Configuration Manager クライアントがインストールされます。  


## <a name="improvements-to-software-center"></a>ソフトウェア センターの機能強化
* ソフトウェア センターの **[アプリケーション]** 、 **[更新]** 、 **[オペレーティング システム]** の各タブに、最近追加されたソフトウェアが表示されるようになりました。 ナビゲーション ウィンドウ内の数字は、各タブ内の新しいソフトウェアの数を示します。
* ユーザーはアプリケーションの承認を要求して、要求の履歴をソフトウェア センターの **[アプリケーションの詳細]** ビューで確認できるようになりました。 **[アプリケーションの詳細]** の **[要求]** ボタンは、Web ベースのアプリケーション カタログにリダイレクトしなくなりました。

## <a name="improvements-to-asset-intelligence"></a>資産インテリジェンスの改善
他のソフトウェアと親子の関係を設定できるように、インベントリされたソフトウェアのプロパティにフィールドを追加しました。 [インベントリされたソフトウェア] の一覧で、任意のソフトウェアの親を表示したり、すべての子ソフトウェアを非表示したりすることもできます。

### <a name="configure-a-parent-to-child-relationship"></a>親子のリレーションシップを構成する
  1. 親ソフトウェアを設定するには、インベントリされたソフトウェア ノードの**インベントリされたソフトウェア** 一覧でソフトウェア項目を右クリックし、**プロパティ** を選択します。
  2. 表示されたダイアログ ボックスで、最初の選択の親ソフトウェアとして設定するソフトウェアを選択します。

### <a name="filter-the-software-display"></a>ソフトウェアの表示をフィルター処理する
親子のリレーションシップを定義すると、ビューをフィルターして、親ソフトウェアまたは定義済みのリレーションシップがないソフトウェアのみを表示することができます。 これにより、別のインベントリされたソフトウェアの子として設定されているすべてのソフトウェアが非表示になります。 これを実行するには、次のようにします。
   1. 検索バーの場合は、 **[条件の追加]** を選びます。
   2. **[親ソフトウェア]** を選び、条件値を **[が空]** に変更してから **[検索]** をクリックします。

表示には、親ソフトウェア アイテム、または定義済みのリレーションシップがないソフトウェアのみが表示されます。 別のタイトルの子のみのソフトウェアは表示されません。

## <a name="remote-control-keyboard-translation"></a>リモート コントロール キーボードの変換
以前は、Configuration Manager は、キーの位置をビューアーの場所から共有先の場所に転送していました。 これは、ビューアーと共有先でキーボードの構成が異なる場合に問題がありました。 たとえば、英語キーボードを使用しているビューアーが「A」を入力しても、共有先のフランス語キーボードでは「Q」となってしまいます。 文字そのものがビューアーのキーボードから共有先に送信され、ビューアーが入力したものが共有先に届くように、既定の動作を変更しています。

共有先のキーボードの配置に従って入力する場合には、ビューアーでこの動作を無効にできます。 動作を変更するには、 **[Configuration Manager のリモート コントロール]** で **[アクション]** を選択し、 **[キーボード変換を有効にする]** を選択してキーの位置を送信します。

> [!NOTE]
>
> ~!#@$% などの特殊なキーは、正しく変換されません。
