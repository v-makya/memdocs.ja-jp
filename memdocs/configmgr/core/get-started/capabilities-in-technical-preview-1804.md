---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview バージョン 1804 で利用できる新しい機能について説明します。
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b30386745244900e7f525f8f45b25a598628bf43
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078738"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Configuration Manager の Technical Preview 1804 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1804 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Technical Preview サイトに追加できます。 

この更新プログラムをインストールする前に、[Technical Preview](technical-preview.md) に関する記事を確認してください。 この記事により、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、フィードバックを提供する方法についての理解を深めることができます。     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>この Technical Preview の既知の問題

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a> 更新プログラムのダウンロードのリンクのセットアップが機能しない
<!--514334-->
メディアからセットアップを実行する場合に、最初のページに **[最新の Configuration Manager 更新プログラムの取得]** というリンクが表示されますが、このリリースではこのリンクが機能しません。 このリンクは、セットアップに必要なファイルをダウンロードするためのものです。

#### <a name="workaround"></a>回避策
セットアップに必要なファイルをダウンロードするには、セットアップ ウィザードを実行します。 [必須ファイルのダウンロード] ページで、 **[必須ファイルをダウンロードする]** オプションを使用します。 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a> アプリケーション カタログ Web サービス ポイントを HTTPS 対応にすることができません。
<!--512637-->
アプリケーション カタログ Web サービス ポイントが HTTPS 対応の場合:

- ユーザーが使用できるように展開されたアプリケーションがソフトウェア センターに表示されません  

- awebsctl.log に次のエラーが表示されます。  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>回避策
HTTP 接続を使用して通信するようにアプリケーション カタログ Web サービス ポイントを再構成します。  




</br>

**このバージョンでお試しいただける新機能を次に示します。**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>サイト サーバーのリモート コンテンツ ライブラリを構成する  
<!--1357525-->
プライマリ サイト サーバー上のハード ドライブ領域を解放するために、[コンテンツ ライブラリ](../plan-design/hierarchy/the-content-library.md)を別の保存場所に移動します。 コンテンツ ライブラリは、サイト サーバー上の別のドライブ、別のサーバー、または記憶域ネットワーク (SAN) 内のフォールトトレラント ディスクに移動できます。 変化するコンテンツの要件に合わせて、時間の経過と共に拡張または縮小する弾力性記憶域の機能があるので、SAN をお勧めします。 

このリモート コンテンツ ライブラリは、[サイト サーバー ロールの高可用性](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)に対応するための新しい前提条件です。 

> [!Note]  
> この操作では、サイト サーバー上のコンテンツ ライブラリのみを移動します。 配布ポイント上のコンテンツ ライブラリの場所には影響しません。 

### <a name="prerequisites"></a>[前提条件]  
- サイト サーバー コンピューター アカウントには、コンテンツ ライブラリの移動先であるネットワーク パスに対して**読み取り**および**書き込み**のアクセス許可が必要です。 リモート システムにコンポーネントはインストールされません。 

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに切り替えます。 **[サイトの構成]** を展開し、 **[サイト]** を選びます。 詳細ウィンドウの下部にある **[概要]** タブに **[コンテンツ ライブラリ]** の新しい列が表示されます。  

2. リボンの **[コンテンツ ライブラリの管理]** をクリックします。  

3. **[On a network share]\(ネットワーク共有上\)** を選択し、有効なネットワーク パスを入力します。 このパスは、サイトがコンテンツ ライブラリを移動する先の場所です。 **[OK]** をクリックします。  

4. 詳細ウィンドウの [コンテンツ ライブラリ] 列の **[状態]** プロパティに注目してください。 コンテンツ ライブラリの移動時には、サイトの進行状況に合わせて更新されます。 進行中は完了率が表示されます。 エラー状態がある場合、エラーが表示されます。 一般的なエラーには `access denied` や `disk full` があります。 完了すると、`OK` と表示されます。 詳細については、**distmgr.log** を参照してください。 詳細については、「[サイト サーバーとサイト システムのログ ファイル](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog)」を参照してください。  

コンテンツ ライブラリをサイト サーバーに戻す必要がある場合は、このプロセスを繰り返しますが、オプションは **[Local to the site server]\(ローカルからサイト サーバーへ\)** を選択します。  

> [!Tip]  
> コンテンツをサイト サーバー上の別のドライブに移動するには、**Content Library Transfer** ツールを使用します。 詳細については、「[Configuration Manager Toolkit](#configuration-manager-toolkit)」を参照してください。  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a> Configuration Manager コンソールからフィードバックを送信する  
<!--1357542-->

[気に入った機能の報告] を使ってみましょう。 Configuration Manager チームに使用感を直接伝えることができるようになりました。 フィードバックは、Configuration Manager コンソールから簡単に送信できます。 称賛、問題、提案など、あらゆるフィードバックを歓迎します。  

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の**フィードバック**をお送りください。  

1. Configuration Manager コンソールで、リボンの右上にあるスマイル ボタンをクリックします。  

2. ドロップダウン リストを使用して、使用できるオプションのいずれかを選択します。  

   - **気に入った機能の報告**:気に入った機能があったら、 このオプションでフィードバックの詳細を入力してください。 必要に応じてスクリーンショットとメール アドレスを含めることができます。  

   - **問題点、改善点の報告**:コンソールに問題が発生した場合、または何かが期待どおりに機能しなかった場合は、 このオプションで製品の問題の可能性について詳しく入力してください。 必要に応じてスクリーンショット、メール アドレス、診断データを含めることができます。  

   - **提案の送信**:Configuration Manager を変更して改善するアイデアがある場合は、 このオプションを選択してください。Web ブラウザーに [UserVoice](https://configurationmanager.uservoice.com) サイトが表示されます。  

このフィードバックは、Configuration Manager の Microsoft 製品チームに直接送られます。 Windows 10 フィードバック ハブも使用できますが、コンソール内のフィードバック機能を使用することをお勧めします。  

コンテキストに関するフィードバックには、次の匿名情報が常に含まれています。  

- Configuration Manager コンソールのバージョンと言語  

- Configuration Manager サイトのバージョン  

- サポート ID (階層 ID とも呼ばれます)  

- コンソールが動作しているシステムの OS バージョンと言語  

- コンソール内でスマイルをクリックした正確な位置  

このデータは、診断データと使用状況データの収集と一致しています。 詳細については、「[診断結果と使用状況データ](../plan-design/diagnostics/diagnostics-and-usage-data.md)」を参照してください。

### <a name="known-issues"></a>既知の問題

インターネットにアクセスできないデバイスからフィードバックを送信しようとすると、アプリケーションが予期せず終了することがあります。 気に入った機能、問題点、改善点を送信するには、デバイスが petrol.office.microsoft.com にアクセスできることを確認してください。



## <a name="support-center"></a>サポート センター
<!--1357489-->

クライアントの問題を解決する場合、リアルタイムのログを表示する場合、または後で分析するために Configuration Manager クライアント コンピューターの状態をキャプチャする場合は、サポート センターを使用します。 サポート センターは、多くの管理者用トラブルシューティング ツールを統合する 1 つのツールです。 バグの修正、改善、新しいログ ビューアーのプレビューを含む最新バージョンのサポート センターのプレビューは、Technical Preview で利用できます。 サイト サーバー上の **cd.latest\SMSSETUP\Tools\SupportCenter** フォルダー内にあるサポート センターのインストーラーを探します。

 > [!Tip]  
 > サポート センターの既存の機能に関する以前のドキュメントは、[TechNet](https://technet.microsoft.com/library/dn688621.aspx) を参照してください。 関連する情報は docs.microsoft.com ライブラリに移行中です。  

### <a name="new-support-center-features"></a>新しいサポート センターの機能  

- 新しいログ ビューアー OneTrace が追加されました。 CMTrace と似た機能ですが、タブ付きビューやドッキング可能なウィンドウなどの点が改善されています。  

- 新しいデータ コレクター機能では、ローカルまたはリモートの Configuration Manager クライアントから診断ログが収集されます。 インベントリのリアルタイム診断機能 (Client Spy を置き換える機能)、ポリシー機能 (Policy Spy を置き換える機能)、クライアント キャッシュ機能があります。  



## <a name="configuration-manager-toolkit"></a>Configuration Manager Toolkit
<!--1357145-->

Configuration Manager のサーバー ツールとクライアント ツールが Technical Preview に含まれるようになりました。 これらのツールは、サイト サーバー上の **cd.latest\SMSSETUP\Tools** フォルダーにあります。 追加でインストールする必要はなくなりました。

#### <a name="server-tools"></a>サーバー ツール  

- **DP Job Manage**:配布ポイントに対するコンテンツ配布ジョブの問題を解決します  

- **Collection Evaluation Viewer**:コレクション評価の詳細を表示します  

- **Content Library Explorer**:コンテンツ ライブラリの単一インスタンス ストアのコンテンツを表示します  

- **Content Library Transfer**:ドライブ間でコンテンツ ライブラリを転送します  

- **Content Ownership Tool**:孤立したパッケージの所有権を変更します。 これらのパッケージは、所有するサイト サーバーがないサイトに存在します。  

- **Role-based Administration and Auditing Tool**:管理者の監査ロールの構成を支援します  

#### <a name="client-tools"></a>クライアント ツール

- **CMTrace**:ログを表示します  

- **Deployment Monitoring Tool**:アプリケーション、更新プログラム、およびベースラインの展開の問題を解決します  

- **Policy Spy**:ポリシーの割り当てを表示します  

- **Power Viewer Tool**:電源管理機能の状態を表示します  

- **Send Schedule Tool**:DCM ベースラインのスケジュールと評価をトリガーします  

> [!Important]  
> [サポート センター](#support-center)には、次のツールと同じ機能または改善された機能が含まれているので、ほとんどのユース ケースにお勧めします。  
> - Client Spy
> - CMTrace<sup>1</sup> 
> - Deployment Monitoring Tool
> - Policy Spy
> - Send Schedule Tool
> 
> <sup>1</sup> CMTrace は .NET または Windows Presentation Foundation (WPF) に依存していないため、Windows PE のブート イメージでも使用されます。

### <a name="known-issues"></a>既知の問題
一部のクライアント ツールやサーバー ツールは、起動時に突然終了することがあります。 この問題は、メディアにファイルが見つからないためです。 この問題を回避するには、**Microsoft.Diagnostics.Tracing.EventSource.dll** ファイルを AdminConsole\bin ディレクトリから SMSSETUP\Tools\ClientTools ディレクトリと ServerTools ディレクトリの両方にコピーします。 このファイルは、Configuration Manager コンソールで使用されているものと同じバージョンである必要があります。 他のバージョンでは動作しない可能性があります。 <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>承認を取り消したときにアプリケーションをアンインストールする
<!--1357891-->

アプリケーションの承認を取り消したときの動作が変更されました。 アプリケーションの要求を拒否すると、クライアントによってユーザーのデバイスからアプリケーションがアンインストールされます。 

### <a name="prerequisites"></a>[前提条件]
- **[デバイスごとにユーザーのアプリケーション要求を承認します]** 機能を有効にします。

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、承認を必要とするアプリケーションをユーザーに展開します。 展開の **[展開設定]** タブで、 **[管理者は、デバイス上のこのアプリケーションへの要求を承認する必要があります]** オプションをオンにします。  

2. ソフトウェア センターの Configuration Manager クライアントで、ユーザーはアプリケーションのインストールの承認を要求します。  

3. Configuration Manager コンソールで、このユーザーがデバイスにアプリケーションをインストールする要求を承認します。 アプリケーション承認要求は、 **[ソフトウェア ライブラリ]** ワークスペースの **[アプリケーション管理]** の下にある **[承認要求]** ノードに表示されます。  

4. ソフトウェア センターのクライアントで、ユーザーがアプリケーションをインストールします。  

5. Configuration Manager コンソールで、デバイス上のアプリケーションに対するユーザーの要求を拒否します。  

### <a name="known-issues"></a>既知の問題
- ユーザーがクライアントにアプリケーションをインストールしたら、ユーザー ポリシーを更新します。 ソフトウェア センターで **[オプション]** タブに切り替え、 **[コンピューターのメンテナンス]** を展開して **[同期ポリシー]** をクリックします。<!--480609-->  

- アプリケーション カタログ Web サービス ポイントは HTTP である必要があります。 詳細については、[この Technical Preview の既知の問題](#bkmk_appcathttps)を参照してください。<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>探索から Active Directory コンテナーを除外する
<!--1358143-->
探索されるオブジェクト数を減らすために、Active Directory システム探索から特定のコンテナーを除外できるようになりました。 この機能は、[UserVoice のフィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery)の結果です。

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[階層の構成]** を展開し、 **[探索方法]** を選択します。 **[Active Directory システム探索]** を選択し、リボンの **[プロパティ]** をクリックします。  

2. [新規] アイコンをクリックし、新しい Active Directory コンテナーを指定します。   

3. [Active Directory コンテナー] ダイアログ ボックスの [場所] セクションで、 **[パス]** を参照または入力して探索を開始します。  

4. [検索のオプション] セクションで、オプション **[Active Directory の子コンテナーを反復検索する]** を有効にします。 次に **[追加]** をクリックし、この探索から除外するサブコンテナーを選択します。  

5. [新しいコンテナーの選択] ダイアログ ボックスで、除外する子コンテナーを選択します。 **[OK]** をクリックし、[新しいコンテナーの選択] ダイアログ ボックスを閉じます。  

6. **[OK]** をクリックし、[Active Directory コンテナー] ダイアログ ボックスを閉じます。  

7. [Active Directory システム探索のプロパティ] ウィンドウで、探索を開始する Active Directory コンテナーのパスを確認します。 **[再帰]** 列には **[はい]** が表示されます。また、新しい **[除外あり]** 列にも **[はい]** が表示されます。 **[OK]** をクリックし、[Active Directory システム探索のプロパティ] ウィンドウを閉じます。  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>ソフトウェア センターのアプリケーション カタログ Web サイト リンクの表示を指定する
<!--1358214-->

ソフトウェア センターの **[インストール状態]** ノードに **[アプリケーション カタログ Web サイトを開く]** のリンクを表示するかどうかを制御できるようになりました。  

> [!Note]  
> アプリケーション カタログの Web サイトでのユーザー エクスペリエンスは、2018 年 6 月 1 日以降にリリースされる最初の更新プログラムでサポートが終了します。 詳細については、[削除された機能と非推奨の機能](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。  

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールの **[管理]** ワークスペースの **[クライアント設定]** ノードで、カスタム クライアント デバイス設定ポリシーを作成します。  

2. **[ソフトウェア センター]** グループを選択します。  

3. **[ソフトウェア センターの設定]** では、 **[カスタマイズ]** をクリックします。  

4. オプション **[Hide the Application Catalog web site link in Software Center]\(ソフトウェア センターでアプリケーション カタログ Web サイトのリンクを非表示にする\)** を有効にします。   

クライアント設定の構成については、[クライアント設定の構成](../clients/deploy/configure-client-settings.md)に関するページを参照してください。




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>ソフトウェア更新アーキテクチャを使用した自動展開規則のフィルター処理
 <!--1322266-->
自動展開規則をフィルター処理して、Itanium や ARM64 などのアーキテクチャを除外できるようになりました。

### <a name="try-it-out"></a>試してみましょう。
タスクを実行してみます。 試した結果の[フィードバック](#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに切り替えます。 **[ソフトウェア更新プログラム]** を展開し、 **[自動展開規則]** を選択します。 リボンの **[自動展開規則の作成]** を選択します。  

2. **[全般]** タブと **[展開設定]** タブに適切な設定を入力します。  

3. **[ソフトウェア更新プログラム]** タブで **[アーキテクチャ]** を選択し、 **[検索条件]** の **[<検索する項目>]** をクリックします。  

4. 自動展開規則に含めるアーキテクチャを選択します。  

5. **[次へ]** をクリックし、自動展開規則の作成を続行します。  

> [!IMPORTANT]  
> 64 ビット (x64) システム上で動作する 32 ビット (x86) アプリケーションとコンポーネントがあることに注意してください。 x86 が不要なことが確実ではない場合は、x64 を選択するときも x86 を有効にしてください。  

### <a name="known-issues"></a>既知の問題
アーキテクチャの条件を追加すると、自動展開規則のプロパティ ページの検索条件に、 **[タイトル]** が表示されます。 自動展開規則は引き続き期待どおりに機能するので、正しいソフトウェア更新プログラムを選択します。 ただし、現時点では、 **[アーキテクチャ]** と **[タイトル]** の両方の条件を含めることはできません。 <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>OS 展開の機能強化
OS の展開について、次のような機能拡張を行いました。一部は皆さまからのフィードバックに基づくものです。  

- [タスク シーケンス変数に格納されている機密データをマスキングする](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed):[[タスク シーケンス変数の設定]](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) 手順で **[この値を表示しない]** という新しいオプションを選択します。 たとえば、パスワードを指定するときに使用します。<!--1358330--> このオプションを有効にすると、次の動作が適用されます。
  - 変数の値は smsts.log に表示されません。
  - Configuration Manager コンソールと SMS プロバイダーは、この値をパスワードなど他のシークレットと同じように扱います。
  - タスク シーケンスをエクスポートするときに、この値は含まれません。
  - タスク シーケンス エディターは、このステップを編集するときにこの値を読み取りません。 変更するには、値全体を再入力します。

  > [!Important]  
  > 変数とその値は、タスク シーケンスと共に XML 形式で保存され、データベース内で難読化されます。 クライアントが管理ポイントからタスク シーケンス ポリシーを要求すると、送信中とクライアント上の保存時には暗号化されます。 ただし、クライアント上での実行中、メモリ内のタスク シーケンス環境では、すべての変数値はプレーン テキストです。 タスク シーケンスに変数の値を出力するステップがある場合、この出力はプレーン テキストです。 この動作には、管理者がこのようなステップを含める明示的なアクションが必要です。 


- [タスク シーケンスのコマンドの実行ステップ中にプログラム名をマスキングする](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed):機密性が高い可能性のあるデータが表示または記録されないようにするには、タスク シーケンス変数 **OSDDoNotLogCommand** を `TRUE` に設定します。 この変数は、[[コマンド ラインの実行]](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) タスク シーケンス ステップ中に smsts.log のプログラム名をマスキングします。 <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager コンソールの機能拡張
- **[資産とコンプライアンス]** 、 **[デバイス コレクション]** でコレクションのメンバーを表示するときに、プライマリ ユーザー情報が表示されるようになりました。<!--510252-->  



## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。    
