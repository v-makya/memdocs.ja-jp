---
title: ヘルプの検索
titleSuffix: Configuration Manager
description: Configuration Manager の詳細情報に関するリソースを見つけます。
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bae98a8df1d8b8ff843bd333083c4c6ad68848c
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343186"
---
# <a name="find-help-for-using-configuration-manager"></a>Configuration Manager の使用に関するヘルプの検索

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager の使用に関するヘルプを検索するための複数のリソースで以下のセクションを提供します。  

- [製品ドキュメント](#bkmk_Info)  

- [製品に関するフィードバックの共有](#product-feedback)  

- [Configuration Manager チームのブログをフォローする](#BKMK_ProductGroupBlog)  

- [サポート オプションとコミュニティ リソース](#BKMK_SupportOptions)  

製品のユーザー補助機能のヘルプについては、[ユーザー補助機能](accessibility-features.md)に関するページをご覧ください。  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a> 製品ドキュメント  

最新の製品ドキュメントにアクセスするには、[ライブラリのインデックス](https://docs.microsoft.com/sccm/)から開始します。  

<a name="BKMK_SearchTips"></a>  

検索、フィードバックの提供、および製品ドキュメントの使用の詳細に関するヒントについては、「[ドキュメントの使用方法](use-docs.md)」をご覧ください。  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a> バージョン 1806 以降の製品に関するフィードバック

Configuration Manager バージョン 1806 以降では、コンソールから直接、製品に関するフィードバックを送信できます。 ログを添付する必要がある場合は、[フィードバック ハブ](#BKMK_FeedbackHub)を使用します。 次の操作を行うことができます。 <!--1357542-->

- **気に入った機能の報告**:気に入ったもののフィードバックを送信します。
- **問題点、改善点の報告**:気に入らなかったもののフィードバックを送信します。
- **提案の送信**:アイデアを共有するために [UserVoice の Web サイト](https://configurationmanager.uservoice.com/)に移動します。

  ![Configuration Manager 1806 でフィードバックを送信する](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>気に入った機能または問題点、改善点の報告

気に入ったもののフィードバックを送信するには、次の手順に従います。

1. コンソールの右上隅で、スマイル マークをクリックします。
2. ドロップダウン メニューで、 **[気に入った機能の報告]** または **[問題点、改善点の報告]** を選択します。
3. テキスト ボックスを使用して、気に入った点または気に入らなかった点を説明します。 
4. 自分の電子メール アドレスとスクリーンショットを共有するかどうかを選択します。
5. **[フィードバックの送信]** をクリックします。
     - インターネット接続がない場合は、下部にある **[保存]** ボタンをクリックします。 「[後で送信するために保存したフィードバックを送信する](#BKMK_NoInternet)」セクションに記載されている手順に従って、マイクロソフトにフィードバックを送信します。 

![Configuration Manager 1806 でフィードバック フォームを送信する](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>気に入った機能の報告のステータス メッセージ
<!--5891852-->
Configuration Manager 2002 以降、**気に入った機能の報告**または**問題点、改善点の報告**を行う場合、フィードバックの送信時にステータス メッセージが作成されます。 この機能強化により、次のレコードが提供されます。
- フィードバックが送信された日時
- フィードバックを送信したユーザー
- フィードバック ID
- フィードバックの送信が成功したかどうか
   - 送信に成功した場合のメッセージ ID は 53900 です。
   - 送信に失敗した場合のメッセージ ID は 53901 です。

**[監視]**  >  **[システム ステータス]**  >  **[ステータス メッセージ クエリ]** でステータス メッセージを表示できます。 **[すべてのステータスメッセージを ]** クエリを開始して、時間枠を選択します。 メッセージが読み込まれたら、 **[メッセージのフィルター]** ボタンをクリックし、メッセージ ID 53900 または 53901 をフィルター処理します。

[後で送信するために保存したフィードバックを送信する](find-help.md#BKMK_NoInternet)場合、ステータス メッセージは作成されません。

[![フィードバックが正常に送信された場合のステータ スメッセージ](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>提案の送信

**提案を送信**する場合、アイデアを共有するために [UserVoice](https://configurationmanager.uservoice.com/) (サード パーティの Web サイト) にリダイレクトされます。 Configuration Manager 製品チームでは、次の UserVoice の状態の値を使用します。

- **Noted (記録済み)** - 要求を理解しており、この要求は意味を成します。 バックログに追加しました。
- **計画済み** - この機能のコーディングを開始しており、今後数か月以内にテクニカル プレビュー ビルドに表示される予定です。
- **開始** - 現在、機能はテクニカル プレビュー段階にあります。 確認して、フィードバックを送信してください。 機能が正しい方向に向かっているかどうかをお知らせください。 その他のユーザーが表示してコメントするために、元の要求のコメント セクションに追加のフィードバックを入力します。 Microsoft はその内容を確認し、フィードバックを使用して機能を改善しようとします。
- **完了** - 機能の最初のバージョンが実稼働ビルドになっています。 この状態は、この機能が 100% 完了しており、これ以上改善することはないという意味ではありません。 しかし、機能の v1 が実稼働ビルドにあり、実際に使用を開始できるということを意味します。 完了にしている理由は次のとおりです。
  - 機能を実稼働で利用できる準備ができていることを知ってもらう必要があります。
  - 他の項目で使用できるように、UserVoice で投票を返してもらう必要があります。
  - お客様はこの機能に新しい設計変更要求を提出し、Microsoft がこの機能について次に最も重要な改善を知るのに役立てることができます。

### <a name="information-sent-with-feedback"></a>フィードバックで送信される情報

**気に入った機能を報告**したり、**問題点、改善点を報告**したりするときに、次の情報がフィードバックと共に送信されます。

- OS ビルド情報
- Configuration Manager 階層 ID
- 製品のビルド情報
- 言語情報
- デバイスの識別子 
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a> 後で送信するために保存したフィードバックを送信する

1. **[フィードバックの提供]** ウィンドウの下部で **[保存]** をクリックします。 
2. .zip ファイルを保存します。 ローカル コンピューターにインターネット アクセスがない場合は、インターネットに接続されているコンピューターにファイルをコピーします。 
3. 必要に応じて、`cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\` にある UploadOfflineFeedback フォルダーをコピーします。
    - cd.latest フォルダーの詳細については、[CD.Latest フォルダー](../servers/manage/the-cd.latest-folder.md)に関するページを参照してください。

4. インターネット接続されているコンピューターで、コマンド プロンプトを開きます。 
5. 次のコマンドを実行します。`UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - 必要に応じて、次のパラメーターを指定できます。
        -  `-t, --timeout` データ送信のタイムアウト (秒)。 0 は制限なしです。 既定値は 30 です。
        - `-s --silent` コンソールにログを記録しない (--verbose との組み合わせは不可)
        - `-v, --verbose` 詳細なログをコンソールに出力する (--silent との組み合わせは不可)
        - `--help` ヘルプ画面の表示
    
    - バージョン 1910 以降では、UploadOfflineFeedback ユーティリティでのプロキシ サーバーの使用がサポートされています。 次のパラメーターを指定できます。
        - `-x, --proxy` インターネットに接続するプロキシ サーバーを指定します。
        - `-o, --port` インターネットに接続するプロキシ サーバー用のポートを指定します。
        - `-u, --user` インターネットに接続するプロキシ サーバー用のユーザー名を指定します。
        - `-w, --password` インターネットに接続するプロキシ サーバー用のパスワードを指定します。 パスワード用のプロンプトを生成するには、アスタリスク (&#42;) を入力します。 パスワードは、パスワード用プロンプトで入力した場合は表示されません。 コマンド ライン上のプレーン テキストは安全性が低くなるため、アスタリスク (&#42;) を使用してパスワード入力用のプロンプトを生成することを強くお勧めします。
        - `-i` 接続チェックのスキップ:ネットワークの接続チェックをスキップし、指定した設定でフィードバックのアップロードだけを行います。

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a> コンソール フィードバックの確認

<!--3556010-->
バージョン 1902 以降では、Configuration Manager コンソールまたは UploadOfflineFeedback.exe からフィードバックを送信するときに、確認メッセージが表示されます。 このメッセージに含まれる**フィードバック ID** を、追跡識別子として Microsoft に渡すことができます。

- **フィードバック ID** をコピーするには、ID の横にあるコピー アイコンを選択するか、**Ctrl** + **C** ショートカット キーを使用します。
  - この ID はコンピューターに保存されないので、ウィンドウを閉じる前にコピーしてください。
- **[今後このメッセージを表示しない]** をクリックすると、このダイアログ ボックスは非表示になり、今後表示されなくなります。

   ![Configuration Manager 1902 のコンソールからのフィードバックの確認](media/1902-feedback-id-example.png)
- **UploadOfflineFeedback** コマンド ツールでは、-s または --silent が使用されない限り、**FeedbackID** がコンソールに表示されます。

  ![Configuration Manager 1902 の UploadOfflineFeedback.exe からのフィードバックの確認](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a> バージョン 1802 以前の製品に関するフィードバック

製品の潜在的な欠陥は、Windows 10 に組み込まれている[フィードバック ハブ アプリ](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)を通じて報告してください。 **新しいフィードバックを追加する**場合は、必ず、 **[エンタープライズ管理]** カテゴリを選択してから、以下のサブカテゴリのいずれかを選択してださい。
- Configuration Manager クライアント
- Configuration Manager コンソール
- Configuration Manager OS の展開
- Configuration Manager サーバー

Configuration Manager の新しい機能のアイデアについて投票する場合は、引き続き [UserVoice ページ](https://configurationmanager.uservoice.com/)をご利用ください。 Configuration Manager 製品チームでは、次の UserVoice の状態の値を使用します。

- **Noted (記録済み)** - 要求を理解しており、この要求は意味を成します。 バックログに追加しました。
- **計画済み** - この機能のコーディングを開始しており、今後数か月以内にテクニカル プレビュー ビルドに表示される予定です。
- **開始** - 現在、機能はテクニカル プレビュー段階にあります。 確認して、フィードバックを送信してください。 機能が正しい方向に向かっているかどうかをお知らせください。 その他のユーザーが表示してコメントするために、元の要求のコメント セクションに追加のフィードバックを入力します。 Microsoft はその内容を確認し、フィードバックを使用して機能を改善しようとします。
- **完了** - 機能の最初のバージョンが実稼働ビルドになっています。 この状態は、この機能が 100% 完了しており、これ以上改善することはないという意味ではありません。 しかし、機能の v1 が実稼働ビルドにあり、実際に使用を開始できるということを意味します。 完了にしている理由は次のとおりです。
  - 機能を実稼働で利用できる準備ができていることを知ってもらう必要があります。
  - 他の項目で使用できるように、UserVoice で投票を返してもらう必要があります。
  - お客様はこの機能に新しい設計変更要求を提出し、Microsoft がこの機能について次に最も重要な改善を知るのに役立てることができます。

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a> Configuration Manager チームのブログ  

Configuration Manager のエンジニアリング チームとパートナー チームは、[Enterprise Mobility + Security ブログ](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager)を使用して、Configuration Manager と関連技術に関する技術情報やその他のニュースを提供しています。 ブログの記事は、製品ドキュメントとサポート情報を補足するものです。  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a> サポート オプションとコミュニティ リソース  

次のリンクは、サポート オプションとコミュニティ リソースに関する情報を提供します。  

-   [Microsoft サポート](https://aka.ms/cmcbsupport)  

-   [Configuration Manager コミュニティ:Configuration Manager (Current Branch) サバイバル ガイド](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Configuration Manager フォーラム ページ](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
