---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview Branch バージョン 1807 で利用できる新しい機能について説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ace27e9035af6696e455382a32365be0e3824d65
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905197"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Configuration Manager Technical Preview バージョン 1807 の機能 

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1807 で利用できる機能について説明します。 このバージョンをインストールすると、Technical Preview サイトが更新され、新機能が追加されます。 

この更新プログラムをインストールする前に、[Technical Preview](technical-preview.md) に関する記事を確認してください。 この記事により、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、フィードバックを提供する方法についての理解を深めることができます。     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>既知の問題 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a> Office 365 のソフトウェア更新プログラムに関する問題
<!--521365-->
Technical Preview Branch バージョン 1806 および 1806.2 を使用して Office 365 の更新プログラムを管理すると、クライアントでのインストールが失敗する可能性があります。 

#### <a name="workaround"></a>回避策
- Office 365 の既存の展開パッケージとソフトウェア更新プログラム グループを削除します。  

- 2018 年 7 月 31 日以降は、Office 365 のソフトウェア更新プログラムを同期し、最新の更新プログラムのみを展開します。  



</br>

**次のセクションでは、このバージョンの新機能について説明します。**  


## <a name="community-hub"></a><a name="bkmk_hub"></a> コミュニティ ハブ
<!--1357766-->

コミュニティ ハブは、Configuration Manager の役立つオブジェクトを他のユーザーと共有するための一元的な場所です。 Configuration Manager コンソールで新しい **[コミュニティ]** ワークスペースを表示し、 **[ハブ]** ノードを選択します。 コミュニティ ハブを使用して、次の種類の Configuration Manager オブジェクトをダウンロードします。 
- スクリプト
- 構成項目

![Configuration Manager コンソール、コミュニティ ワークスペース、ハブ ノード](media/1357766-hub.png)

使用可能な項目に関する詳細を見るには、ハブで項目をクリックします。 詳細ページから **[ダウンロード]** をクリックして、項目を取得します。 ハブから項目をダウンロードすると、サイトに自動的に追加されます。 

![Configuration Manager コンソール、コミュニティ ワークスペース、ハブ ノード、詳細ページ](media/1357766-hub-details.png)

**[コミュニティ]** ワークスペースには、次のノードも含まれています。

- **ドキュメント**:Configuration Manager の[ドキュメント ライブラリ](https://docs.microsoft.com/sccm/)が表示されます。  

- **フィードバック**:Configuration Manager の [UserVoice サイト](https://configurationmanager.uservoice.com/)が表示されます  


### <a name="prerequisites"></a>[前提条件]

- クライアント OD で Configuration Manager コンソールを使用します。  

    - 推奨されない代替方法: サーバー OS で、[Internet Explorer のセキュリティ強化構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10))を無効にします。

- コンソールを使用するコンピューターは、インターネットにアクセスし、次のサイトに接続できる必要があります。  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>既知の問題

ハブへの項目の寄与は、このバージョンでは現在使用できません。 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a> オフライン OS イメージ サービス用のドライブを指定する  
<!--1358924-->

[UserVoice のフィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive)に基づき、OS イメージのオフライン サービス中に Configuration Manager が使用するドライブを指定するようになりました。 このプロセスでは一時ファイルによって大量のディスク領域が使用される可能性があり、このオプションでは使用するドライブを柔軟に選択できます。 


### <a name="try-it-out"></a>試してみましょう。

タスクを実行してみます。 その後、[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)で機能についてのご意見をお寄せください。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。 リボンの **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** を選択します。  

2. **[Offline Servicing]\(オフライン サービス\)** タブに切り替えて、 **[イメージのオフライン サービスで使用するローカル ドライブ]** のオプションを指定します。  

この設定の既定値は **[自動]** です。 この値では、Configuration Manager がインストール対象のドライブを選択します。 

オフライン サービス中、Configuration Manager は一時ファイルをフォルダー `<drive>:\ConfigMgr_OfflineImageServicing` に格納します。 また、このフォルダー内の OS イメージをマウントします。 

**OfflineServicingMgr.log** ログ ファイルを確認してください。 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a> Intune での共同管理されたデバイス同期アクティビティ
<!--1358565-->

Configuration Manager コンソールに、共同管理されたデバイスが Microsoft Intune でアクティブになっているかどうかが表示されます。 この状態は、[Intune データ ウェアハウス](https://docs.microsoft.com/intune/reports-nav-create-intune-reports)のデータに基づきます。 Configuration Manager コンソールの **[クライアントのステータス]** ダッシュボードには、 **[Intune を使用する非アクティブなクライアント]** が表示されます。 この新しいカテゴリは、Configuration Manager では非アクティブでも、過去 1 週間以内に Intune サービスと同期されている、共同管理されたデバイスに関するものです。


### <a name="try-it-out"></a>試してみましょう。

タスクを実行してみます。 その後、[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)で機能についてのご意見をお寄せください。

共同管理用にサイトを既に設定してある場合: 

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[共同管理]** を選択します。 リボンで **[プロパティ]** をクリックします。  

2. **[レポート]** タブに切り替えます。 **[サインイン]** をクリックして認証を行います。 **[更新]** をクリックして、Intune データ ウェアハウスに対する読み取りアクセス許可を有効にします。  

3. Intune とサイトを同期した後、 **[監視]** ワークスペースに移動し、 **[クライアント ステータス]** ノードを選択します。 **[全体のクライアント ステータス]** セクションで、 **[Intune を使用する非アクティブなクライアント]** の行を確認します。  

共同管理の有効化について詳しくは、「[Windows 10 デバイスの共同管理](../../comanage/overview.md)」をご覧ください。



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a> アプリケーションの修復
<!--1357866-->

[UserVoice のフィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application)に基づき、Windows インストーラーおよびスクリプト インストーラーの展開の種類で、修復コマンド ラインを指定できるようになりました。 


### <a name="try-it-out"></a>試してみましょう。

タスクを実行してみます。 その後、[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)で機能についてのご意見をお寄せください。

1. Configuration Manager コンソールで、Windows インストーラーまたはスクリプト インストーラーの展開の種類のプロパティを開きます。  

2. **[プログラム]** タブに切り替えます。 **[プログラム修復]** コマンドを指定します。  

3. アプリを展開します。 展開の **[展開の設定]** タブで、 **[エンド ユーザーがこのアプリケーションの修復を試すことを許可する]** オプションを有効にします。  


### <a name="known-issue"></a>既知の問題

ユーザーがアプリを**修復**するためのソフトウェア センターの新しいボタンは、このバージョンでは表示されません。  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a> 電子メールでアプリケーション要求を承認する
<!--1321550-->

アプリケーションの承認を要求する電子メール通知を構成します。 ユーザーがアプリケーションを要求すると、管理者はメールを受け取ります。 メールのリンクをクリックして、要求を承認または拒否できます。Configuration Manager コンソールは必要ありません。


### <a name="prerequisites"></a>[前提条件]

#### <a name="to-send-email-notifications"></a>メール通知を送信するには
- [オプション機能](../servers/manage/install-in-console-updates.md#bkmk_options)の **[デバイスごとにユーザーのアプリケーション要求を承認します]** を有効にします。  

- [アラートのメール通知](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts)を構成します。  

#### <a name="to-approve-or-deny-requests-from-email"></a>メールから要求を承認または拒否するには
これらの前提条件を構成しない場合、サイトから送信されるアプリケーション要求のメール通知には、要求を承認または拒否するリンクが含まれません。  

- サイトのプロパティで、 **[このサイトのすべてのプロバイダー ロールの REST エンドポイントを有効にして、Configuration Manager のクラウド管理ゲートウェイ トラフィックを許可する]** を選択します。 詳しくは、「[OData エンドポイントのデータ アクセス](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)」をご覧ください。  

    - REST エンドポイントを有効にした後、SMS_EXEC サービスを再起動します

- [クラウド管理ゲートウェイ](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- **クラウド管理**のために [Azure サービス](../servers/deploy/configure/azure-services-wizard.md)にサイトをオンボードします  

    - [Azure AD ユーザー探索](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)を有効にします  

    - Azure AD でこのネイティブ アプリの次の設定を手動で構成します。  

        - **リダイレクト URI**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`。 クラウド管理ゲートウェイ (CMG) サービスの完全修飾ドメイン名 (FQDN) を使用します (例: GraniteFalls.Contoso.com)。   

        - **マニフェスト**: **oauth2AllowImplicitFlow** を true に設定します。`"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>試してみましょう。

タスクを実行してみます。 その後、[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)で機能についてのご意見をお寄せください。

1. Configuration Manager コンソールで、ユーザー コレクションに使用できるようにアプリケーションを展開します。 **[展開の設定]** ページで、承認に対して有効にします。 通知を受け取る "*1 つの*" メール アドレスを入力します。  

     > [!Note]  
     > Azure AD 組織内でメールを受け取るすべてのユーザーが、要求を承認できます。 他のユーザーにアクションを実行させるのでない限り、他のユーザーにメールを転送しないでください。  

2. ユーザーが、ソフトウェア センターでアプリケーションを要求します。  

3. 管理者は、次の例のようなメール通知を受け取ります。  

![アプリケーション承認のメール通知の例](media/1321550-email.png)

> [!Note]  
> 承認または拒否のためのリンクは、1 回しか使用できません。 たとえば、通知を受け取るためのグループの別名を構成します。 あるユーザーが要求を承認します。 その場合、別のユーザーは要求を拒否できません。  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a> スクリプトの出力の改良
<!--1236459-->

詳細なスクリプトの出力を、手が加えられていない形式または構造化された JSON 形式で表示できるようになりました。 この書式設定を行うと、出力の読み取りと分析が容易になります。 スクリプトが有効な JSON 形式のテキストを返す場合は、詳細な出力を **JSON 出力**または**未フォーマット出力**として表示できます。 それ以外の場合は、 **[スクリプトの出力]** が唯一のオプションです。 

#### <a name="example-script-output-is-valid-json"></a>例:スクリプト出力が有効な JSON である
コマンド: `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>例:スクリプト出力が有効な JSON ではない
コマンド: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>試してみましょう。

タスクを実行してみます。 その後、[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)で機能についてのご意見をお寄せください。

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス コレクション]** ノードを選択します。 コレクションを右クリックして、 **[スクリプトの実行]** を選択します。 スクリプトの作成と実行について詳しくは、「[Configuration Manager コンソールから PowerShell スクリプトを作成して実行する](../../apps/deploy-use/create-deploy-scripts.md)」をご覧ください。  

2. ターゲット コレクションでスクリプトを実行します。  

3. スクリプトの実行ウィザードの **[スクリプトのステータスの監視]** ページで、下部にある **[サマリー]** タブを選択します。 上部にある 2 つのドロップダウン リストを、 **[スクリプトの出力]** と **[データ テーブル]** に変更します。 その後、結果の行をダブルクリックして、 **[Detailed Output]\(詳細出力\)** ダイアログ ボックスを開きます。  

4. スクリプトの実行ウィザードの **[スクリプトのステータスの監視]** ページで、下部にある **[実行の詳細]** タブを選択します。 結果の行をダブルクリックして、そのデバイスの [Detailed Output]\(詳細出力\) ダイアログ ボックスを開きます。  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a> サード パーティ製ソフトウェアの更新プログラムの改良
<!--1358714-->

カスタム カタログのプロパティを変更できるようになりました。

詳しくは、「[カスタム カタログ用のサード パーティ製ソフトウェアの更新プログラムのサポート](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)」をご覧ください。



## <a name="next-steps"></a>次のステップ

Technical Preview Branch のインストールまたは更新について詳しくは、[Technical Preview](technical-preview.md)に関するページをご覧ください。    

Configuration Manager のさまざまなブランチについて詳しくは、「[適切な Configuration Manager のブランチを選択する](../understand/which-branch-should-i-use.md)」をご覧ください。
