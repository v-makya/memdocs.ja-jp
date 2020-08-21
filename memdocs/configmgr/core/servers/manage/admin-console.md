---
title: Configuration Manager コンソール
titleSuffix: Configuration Manager
description: Configuration Manager コンソールでの移動について学習します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126497"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Configuration Manager コンソールの使用方法

*適用対象:Configuration Manager (Current Branch)*

管理者は Configuration Manager コンソールを利用し、Configuration Manager 環境を管理します。 この記事では、コンソールを移動するときの基礎について説明します。  

## <a name="open-the-console"></a><a name="bkmk_open"></a> コンソールを開く

Configuration Manager コンソールは、常にすべてのサイト サーバーにインストールされます。 また、他のコンピューターにインストールすることもできます。 詳細については、「[System Center Configuration Manager コンソールをインストールする](../deploy/install/install-consoles.md)」を参照してください。

Windows 10 コンピューターでコンソールを開く最も簡単な方法は、 **[スタート]** を押して「`Configuration Manager console`」と入力し始めることです。 Windows では、最適な一致を見つけるために文字列全体を入力する必要がない場合があります。

[スタート] メニューを参照する場合は、 **[Microsoft Endpoint Manager]** グループの **[Configuration Manager コンソール]** アイコンを探します。

![[スタート] メニューの Microsoft Endpoint Manager のアイコン](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> [スタート] メニューのパスはバージョン 1910 で変更されました。 バージョン 1906 以前では、フォルダー名は **System Center** です。 Configuration Manager をバージョン 1910 以降に更新する場合は、この新しい場所を含むように、保守しているすべての内部ドキュメントを更新してください。

## <a name="connect-to-a-site-server"></a>サイト サーバーに接続する

コンソールは、中央管理サイトまたはプライマリ サイト サーバーに接続されます。 Configuration Manager コンソールをセカンダリ サイトに接続することはできません。 インストール時、コンソールが接続するサイト サーバーの完全修飾ドメイン名 (FQDN) を指定しています。

別のサイト サーバーに接続するには、次の手順を実行します。

1. [リボン](#ribbon)上部の矢印をクリックし、 **[新しいサイトに接続]** を選択します。  

    ![コンソールを新しいサイトに接続する](media/connect-to-a-new-site.png)  

2. サイト サーバーの FQDN を入力します。 サイト サーバーに以前接続したことがある場合は、ドロップダウン リストからサーバーを選択します。  

    ![[サイトの接続] ウィンドウで、サイト サーバーの FQDN を入力する](media/site-server-fqdn.png)  

3. **[接続]** を選択します。  

バージョン 1810 以降では、Configuration Manager サイトにアクセスする管理者の最低限の認証レベルを指定することができます。 この機能では、Windows にサインインする管理者には必要なレベルを持つことが強制されます。 詳細については、「[SMS プロバイダーの計画](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)」を参照してください。 <!--1357013-->  

## <a name="navigation"></a>ナビゲーション

割り当てられているセキュリティ ロールによっては、コンソールの一部の領域が表示されない場合があります。 ロールの詳細については、[ロール ベース管理の基礎](../../understand/fundamentals-of-role-based-administration.md)に関するページを参照してください。

### <a name="workspaces"></a>ワークスペース

Configuration Manager コンソールには、**ワークスペース**が 4 つあります。  

- **資産とコンプライアンス**  

- **ソフトウェア ライブラリ**  

- **監視**  

- **管理**  

![Configuration Manager のワークスペースとコンテキスト メニュー](media/configuration-manager-workspaces.png)  

下向き矢印を選択し、 **[ナビゲーション ペイン オプション]** を選択して、ワークスペースのボタンの順序を再変更します。 **[上へ移動]** または **[下へ移動]** する項目を選択します。 **[リセット]** を選択して、ボタンを既定の順序に戻します。  

![ワークスペースの順序を変更する [ナビゲーション ペイン オプション] ウィンドウ](media/navigation-pane-options.png)  

**[表示するボタンを減らす]** を選択して、ワークスペースのボタンを最小化します。 リストの最後のワークスペースが最初に最小化されます。 最小化されたボタンを選択して、 **[表示するボタンを増やす]** を選択すると、ボタンは元のサイズに戻ります。

![Configuration Manager コンソール内で最小化されたワークスペース](media/workspace-buttons.png)  

### <a name="nodes"></a>ノード

ワークスペースとは、**ノード**のコレクションです。 ノードの一例として、**ソフトウェア ライブラリ** ワークスペースの**ソフトウェア更新プログラム グループ** ノードがあります。

そのノードに移動したら、矢印を選択してナビゲーション ウィンドウを最小化できます。  

![ノードの例と強調表示された最小化矢印](media/software-update-groups-node.png)  

ナビゲーション ウィンドウを最小化した場合は、**ナビゲーション バー**を使用してコンソール内を移動します。  

![Configuration Manager の最小化されているナビゲーション ウィンドウ](media/minimized-navigation-pane.png)  

コンソールで、ノードはフォルダーに分類される場合があります。 フォルダーを選択すると、通常、**ナビゲーション インデックス**または**ダッシュボード**が表示されます。  

![Configuration Manager のソフトウェア更新プログラムの機能一覧](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>リボン

リボンは、Configuration Manager コンソールの上部にあります。 リボンにはタブが 1 つ以上あり、右の矢印を使用して最小化することができます。 リボンのボタンは、ノードによって変わります。 リボンのほとんどのボタンは、コンテキスト メニューでも使用することができます。  

![複数のタブと最小化矢印が強調表示されたリボンの例](media/ribbon.png)

### <a name="details-pane"></a>詳細ウィンドウ

項目の追加情報は、詳細ウィンドウで確認できます。 詳細ウィンドウには、タブが 1 つ以上あります。 このタブはノードによって異なります。  

![Configuration Manager の詳細ウィンドウの例](media/details-pane.png)

### <a name="columns"></a>列

列は、追加、削除、順序変更、サイズ変更することができます。 これらのアクションでは、お好みのデータを表示することができます。 使用できる列はノードによって異なります。 ビューに列を追加またはビューから列を削除するには、既存の列見出しを右クリックし、項目を選択します。 お好きな場所に列見出しをドラッグし、列を並べ替えます。  

![Configuration Managers での列の追加](media/add-columns.png)  

列のコンテキスト メニューの下部で、列を並べ替えたりグループ化できます。 また、列の見出しを選択して並べ替えることもできます。  

![Configuration Manager での列でグループ化](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a> オブジェクトを編集するためにロックを再利用する

<!--4786915-->

Configuration Manager コンソールが応答しなくなった場合は、30 分後にロックの期限が切れるまで、さらに変更を加えられないようにロックされることがあります。 このロックは、Configuration Manager SEDO (分散オブジェクトでの編集のシリアル化) システムの一部です。 詳細については、「[Configuration Manager SEDO](../../../develop/core/understand/sedo.md)」を参照してください。

[Current Branch バージョン 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences) 以降では、タスク シーケンスのロックを解除できました。 バージョン 1910 以降では、Configuration Manager コンソール内の任意のオブジェクトのロックを解除できます。

このアクションは、サイトがロックを付与できる同じデバイス上で、ロックされている自分のユーザー アカウントにのみ適用されます。 ロックされているオブジェクトにアクセスしようとすると、**変更を破棄**して、オブジェクトの編集を続けられるようになりました。 これらの変更は、ロックの期限が切れたときに、いずれにしても失われます。

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a> 最近接続されたコンソールを表示する

<!--3699367-->
バージョン 1902 以降では、Configuration Manager コンソールの最新の接続を表示できます。 ビューには、アクティブな接続と最近接続された接続が含まれます。 常に、リストに現在のコンソール接続が表示され、Configuration Manager コンソールからの接続のみが表示されます。 PowerShell または SMS プロバイダーへのその他の SDK ベースの接続は表示されません。 サイトでは、30 日を経過したインスタンスがリストから削除されます。

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a> 接続されたコンソールを表示するための前提条件

- お使いのアカウントに **SMS_Site** オブジェクトに対する**読み取り**アクセス許可が必要です

- 管理サービスの REST API を構成します。 詳細については、「[管理サービスとは何ですか](../../../develop/adminservice/overview.md)」をご覧ください。

### <a name="view-connected-consoles"></a>接続されたコンソールを表示する

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。  

2. **[セキュリティ]** を展開し、 **[コンソール接続]** ノードを選択します。  

3. 次のプロパティを使用して、最近の接続を表示します。  

    - ユーザー名
    - コンピューター名
    - 接続したサイト コード
    - コンソール バージョン
    - 最終接続時刻:ユーザーが最後にコンソールを*開いた* 時刻
    - バージョン 1910 以降では、 **[最終接続時刻]** が **[最後のコンソール ハートビート]** 列に置き換えられました。 <!--4923997-->
       - フォアグラウンドで開いているコンソールでは、10 分ごとにハートビートが送信されます。

![Configuration Manager コンソール接続を表示する](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a> コンソール接続から Microsoft Teams チャットを開始する
<!--4923997-->
*(バージョン 1910 で導入)*

バージョン 1910 以降では、Microsoft Teams を使用して、 **[コンソール接続]** ノードから他の Configuration Manager 管理者にメッセージを送信することができます。 管理者を指定して **[Microsoft Teams チャットの開始]** を選択すると、Microsoft Teams が起動し、そのユーザーとのチャットが開始されます。

### <a name="prerequisites"></a>[前提条件]

- 管理者とチャットを開始するには、チャット相手のアカウントが [Azure AD または AD ユーザー探索](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)で検出されている必要があります。
- コンソールを実行するデバイスにインストールされている Microsoft Teams。
注意
- [接続されたコンソールを表示するためのすべての前提条件](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Microsoft Teams チャットの開始

1. **[管理]**  >  **[セキュリティ]**  >  **[コンソール接続]** にアクセスします。
1. ユーザーのコンソール接続を右クリックし、 **[Microsoft Teams チャットの開始]** を選択します。
    - 選択した管理者のユーザー プリンシパル名が見つからない場合、 **[Microsoft Teams チャットの開始]** はグレー表示になります。
    - コンソールを実行するデバイスに Microsoft Teams がインストールされていない場合は、ダウンロード リンクを含むエラー メッセージが表示されます。
    - コンソールを実行するデバイスに Microsoft Teams がインストールされている場合は、ユーザーとのチャットが開きます。

### <a name="known-issues"></a>既知の問題

次のレジストリ キーが存在しない場合、Microsoft Teams がインストールされていないことを通知するエラー メッセージは表示されません。

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

この問題を回避するには、レジストリ キーを手動で作成します。

## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a> コンソール内ドキュメント ダッシュボード

<!--3556019 FKA 1357546-->
Configuration Manager バージョン 1902 以降、新しい **[コミュニティ]** ワークスペースには **[ドキュメント]** ノードがあります。 このノードには、Configuration Manager のドキュメントとサポート記事に関する最新情報が含まれています。 次のセクションが含まれています。  

### <a name="product-documentation-library"></a>製品ドキュメント ライブラリ

- **推奨**: 手動でまとめた重要な記事の一覧です。
- **トレンド**: 過去 1 か月の最も人気があった記事。
- **最近の更新**: 過去 1 か月に改訂された記事。

### <a name="support-articles"></a>サポート技術情報

- **トラブルシューティング記事**: Configuration Manager のコンポーネントと機能のトラブルシューティングに役立つガイド付きチュートリアル。
- **新規および更新のサポートに関する記事**: 過去 2 か月間の新規または更新のサポートに関する記事。

### <a name="troubleshooting-connection-errors"></a>接続エラーのトラブルシューティング
**[ドキュメント]** ノードには明示的なプロキシ構成はありません。 **[インターネット オプション]** コントロール パネル アプレットにある OS 定義のプロキシが使用されます。 接続エラーの後で再試行するには、 **[ドキュメント]** ノードを最新の情報に更新します。


## <a name="command-line-options"></a>コマンド ライン オプション

Configuration Manager コンソールには次のコマンド ライン オプションがあります。

|オプション|[説明]|  
|------------|-----------------|  
|`/sms:debugview=1`|ビューが指定されているすべての ResultView に DebugView を含めます。 DebugView では、生のプロパティ (名前と値) が示されます。|  
|`/sms:NamespaceView=1`|コンソールに名前空間ビューを表示します。|  
|`/sms:ResetSettings`|コンソールでは、ユーザーの永続的な接続状態とビューの状態は無視されます。 ウィンドウのサイズはリセットされません。|  
|`/sms:IgnoreExtensions`|Configuration Manager のすべての拡張機能を無効にします。|  
|`/sms:NoRestore`|コンソールでは、前に永続化されていたノードのナビゲーションは無視されます。|  


## <a name="next-steps"></a>次のステップ

- [コンソール通知](admin-console-notifications.md)
- [コンソール ヒント](admin-console-tips.md)
- [ユーザー補助機能](../../understand/accessibility-features.md)
- [タスク シーケンス エディター](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
