---
title: Technical Preview 1806.2
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview バージョン 1806.2 で利用できる新しい機能について説明します。
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 426767b65e0fd770a9a41ce9463948007a524c41
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078755"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Configuration Manager の Technical Preview 1806.2 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1806.2 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Technical Preview サイトに追加できます。 

この更新プログラムをインストールする前に、[Technical Preview](technical-preview.md) に関する記事を確認してください。 この記事により、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、フィードバックを提供する方法についての理解を深めることができます。     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## <a name="known-issues-in-this-technical-preview"></a>この Technical Preview の既知の問題

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a> クライアントが自動的に更新されない
<!--518760-->
バージョン 1806.2 に更新するとき、サイトは SQL Native Client も更新しますが、これによってサイト サーバー上で再起動が保留される場合があります。 この遅延が原因で特定のファイルが更新されなくなり、クライアントの自動アップグレードに影響が及びます。

#### <a name="workarounds"></a>回避策
この問題を回避するには、Configuration Manager をバージョン 1806.2 に "*更新する前に*"、SQL Native Client を手動でアップグレードします。 詳細については、[SQL Server 2012 Native Client 用の最新のサービス更新](https://www.microsoft.com/download/details.aspx?id=50402)に関するページをご覧ください。

サイトを既に更新している場合、自動のクライアント アップグレードとクライアント プッシュは機能しません。 クライアントを、完全テストの最新機能に更新する必要があります。 次のプロセスに従って、Technical Preview クライアントを手動で更新します。  

1. サイト サーバー上の Configuration Manager のインストール ディレクトリの **CMUClient** フォルダーで、クライアント ソース ファイルを探します。 たとえば、 `C:\Program Files\Configuration Manager\CMUClient` と記述します。  

2. クライアント デバイスに CMUClient フォルダー全体をコピーします。 たとえば、 `C:\Temp\CMUClient` と記述します。  

    クライアントからアクセスできるネットワーク共有をこの場所に指定することができます。  

3. 管理者特権のコマンド プロンプトで、次のコマンド ラインを実行します: `C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Technical Preview バージョン 1806.2 のサイトに新しいクライアントをインストールしている場合は、この同じプロセスを使用します。 

> [!Important]  
> このシナリオでは `/MP` コマンドライン パラメーターを使用しないでください。 このパラメーターは `/source` よりも優先されるため、ccmsetup で管理ポイントまたは配布ポイントからクライアント コンテンツがダウンロードされます。
> 
> SMSSITECODE や CCMLOGLEVEL などのコマンドライン プロパティを使用しても構いませんが、既存のクライアントをアップグレードする場合は必要ありません。 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a> Configuration Manager のバージョン情報でバージョン 1806.2 がバージョン 1806 と表示される
<!--518148-->
テクニカル プレビュー バージョン 1806.2 にアップグレードした後、コンソールの左上隅から **[Configuration Manager のバージョン情報]** ウィンドウを開いても、表示が**バージョン 1806** のままです。 

#### <a name="workaround"></a>回避策
**サイトのバージョン** プロパティを使用して、1806 と 1806.2 を区別します。

| サイトのバージョン  | バージョン
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**このバージョンでお試しいただける新機能を次に示します。**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a> 段階的な展開の機能強化

このリリースには、[段階的な展開](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)に対する次の機能改善が含まれています。
- [段階的な展開の状態](#bkmk_pod-monitor)
- [アプリケーションの段階的な展開](#bkmk_pod-app)
- [段階的な展開中の段階的なロールアウト](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a> 段階的な展開の状態
<!--1358577-->
段階的な展開に、ネイティブの監視機能が追加されました。 **[監視]** ワークスペースの **[展開]** ノードから段階的な展開を選択し、リボンで **[段階的な展開の状態]** をクリックします。

![2 つのフェーズの状態を示す段階的な展開の状態ダッシュボード](media/1358577-phased-deployment-status.png)

このダッシュボードには、展開の各フェーズに対して次の情報が表示されます。  

- **デバイスの総数**:このフェーズの対象となるデバイスの数。  

- **状態**: このフェーズの現在の状態。 各フェーズは次の状態のいずれかになります。  

    - **展開の作成完了**:段階的な展開によって、このフェーズのコレクションにソフトウェアの展開が作成されました。 このソフトウェアではアクティブにクライアントを対象とします。  

    - **待機中**:前のフェーズは、このフェーズに引き続き展開するための成功基準にまだ達していません。  

    - **中断**:管理者が展開を中断しました。  

- **進行状況**:クライアントからの色分けされた展開の状態。 次に例を示します。成功、実行中、エラー、要件が満たされていません、不明。 


#### <a name="known-issue"></a>既知の問題
段階的な展開の状態ダッシュボードでは、同じフェーズの行が複数表示される場合があります。<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a> アプリケーションの段階的な展開
<!--1358147-->
アプリケーションの段階的な展開を作成します。 段階的な展開を使用すると、カスタマイズ可能な条件およびグループに基づいて、調整およびシーケンス化されたソフトウェアの展開をまとめることができます。

Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** に移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** を選択します。 アプリケーションを選択して、リボンで **[段階的な展開の作成]** をクリックします。 

アプリケーションの段階的な展開の動作は、タスク シーケンスの場合と同じです。 詳細については、[タスク シーケンスの段階的展開の作成](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)に関するページをご覧ください。

#### <a name="prerequisite"></a>前提条件
段階的な展開を作成する前に、アプリケーションのコンテンツを配布ポイントに配布します。<!--518293-->

#### <a name="known-issue"></a>既知の問題
アプリケーションのフェーズを手動で作成できません。 ウィザードでは、アプリケーションの展開のフェーズが 2 つ自動的に作成されます。


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a> 段階的な展開中の段階的なロールアウト
<!--1358578-->
段階的な展開中、各フェーズのロールアウトが段階的に発生するようになりました。 この動作は展開に関する問題のリスクを軽減するのに役立ち、クライアントへのコンテンツの配布によるネットワークの負荷を減少させます。 サイトは、各フェーズの構成に基づいて、ソフトウェアを段階的に利用可能にしていくことができます。 フェーズ内の各クライアントには、ソフトウェアが利用可能になった時間に基づく期限が設定されます。 利用可能時間と期限の間の時間枠は、フェーズ内のすべてのクライアントで同じです。 

段階的な展開を作成し、フェーズを手動で構成する場合、[フェーズを追加] ウィザードの **[フェーズの設定]** ページ、または [段階的な展開の作成] ウィザードの **[設定]** ページで、 **[この期間 (日数) の間、このソフトウェアを段階的に利用できるようにする]** オプションを構成します。 この設定の既定値は **0** です。したがって、既定では展開は調整されません。

> [!Note]  
> 現在、このオプションは、タスク シーケンスの段階的な展開でのみ利用できます。  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a> 新しい Windows アプリケーション パッケージ形式のサポート
<!--1357427-->
Configuration Manager は、新しい Windows 10 アプリ パッケージ (.msix) とアプリ バンドル (.msixbundle) 形式の展開をサポートするようになりました。 現在、最新の [Windows Insider Preview](https://insider.windows.com/) のビルドでは、これらの新しい形式がサポートされています。

MSIX の概要については、「[A closer look at MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/)」(MSIX を詳しく調べる) をご覧ください。

新しい MSIX アプリを作成する方法については、「[MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376)」(Insider ビルド 17682 で導入された MSIX のサポート) をご覧ください。

### <a name="prerequisites"></a>[前提条件]
- 最低でも Windows Insider Preview のビルド 17682 を実行している Windows 10 クライアント
- MSIX 形式の Windows アプリケーション パッケージ

### <a name="try-it-out"></a>試してみましょう。
タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、[アプリケーションを作成します](../../apps/deploy-use/create-applications.md)。 
2. アプリケーション インストール ファイルの **[種類]** として **[Windows アプリケーション パッケージ (\*.appx、\*.appxbundle、\*.msix、\*.msixbundle)]** を選択します。
3. 最新の Windows Insider Preview ビルドを実行しているクライアントに[アプリケーションを展開](../../apps/deploy-use/deploy-applications.md)します。



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a> クライアント プッシュ セキュリティの機能改善
<!--1358204-->
構成マネージャー クライアントをインストールする[クライアント プッシュ](../clients/deploy/plan/client-installation-methods.md#client-push-installation) メソッドを使用する場合、サイト サーバーでは、インストールを開始するクライアントへのリモート接続が作成されます。 このリリース以降、サイトでは、接続を確立する前の NTLM へのフォールバックを許可しないことによって、Kerberos の相互認証を要求できます。 この機能強化は、サーバーとクライアント間の通信をセキュリティで保護するのに役立ちます。 

セキュリティ ポリシーによっては、お客様の環境は既に以前の NTLM 認証よりも Kerberos に適している場合、または Kerberos を必要としている場合があります。 これらの認証プロトコルに関するセキュリティの考慮事項について詳しくは、[NTLM を制限する Windows セキュリティ ポリシーの設定](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations)に関するページをご覧ください。


### <a name="prerequisite"></a>前提条件

この機能を使用するには、信頼された Active Directory フォレスト内にクライアントがいる必要があります。 Windows の Kerberos は、相互認証を Active Directory に依存しています。 


### <a name="try-it-out"></a>試してみましょう。

タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

このサイトをアップグレードしても、既存の動作は継続します。 クライアント プッシュ インストールのプロパティを*開く*と、サイトでは自動的に Kerberos のチェックが有効になります。 必要に応じて、安全性の低い NTLM 接続を使用するフォールバックへの接続を許可することができます (非推奨)。 

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** を選択します。 対象のサイトを選択してください。 リボンで **[クライアント インストール設定]** をクリックし、 **[クライアント プッシュ インストール]** を選択します。  

2. これで、サイトでクライアント プッシュの Kerberos チェックが有効になりました。 **[OK]** をクリックして、ウィンドウを閉じます。  

3. 環境の必要に応じて、[クライアント プッシュ インストールのプロパティ] ウィンドウの **[全般]** タブで、 **[NTLM への接続フォールバックを許可する]** オプションを確認します。 既定では、このオプションは無効になっています。 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a> プロアクティブ メンテナンスの管理分析情報
<!--1352184,et al-->
このリリースには、潜在的な構成上の問題を明らかにする、管理分析情報が追加されています。 新しい**プロアクティブ メンテナンス** グループの次のルールを確認してください。  

- **未使用の構成項目**: 構成基準の一部ではなく、30 日以上経過している構成項目。  

- **未使用のブート イメージ**: PXE ブートまたはタスク シーケンスの使用のために参照されていないブート イメージ。  

- **割り当てられたサイト システムがない境界グループ**: 割り当てられたサイト システムがない境界グループは、サイトの割り当てにのみ使用できます。  

- **メンバーを持たない境界グループ**: メンバーを持たない境界グループは、サイトの割り当てやコンテンツ ルックアップに適用されません。  

- **コンテンツをクライアントに提供していない配布ポイント**: 過去 30 日以内にクライアントにコンテンツを提供していない配布ポイント。 このデータは、クライアントからのダウンロード履歴のレポートに基づきます。  

- **[Expired updates found]\(期限切れの更新プログラムがある\)** :期限切れの更新プログラムは展開に適用されません。   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a> 共同管理されたデバイスのモバイル アプリ ワークロードの移行
<!--1357892-->
Windows デスクトップ アプリケーションを展開するために引き続き Configuration Manager を使用しながら、Microsoft Intune でモバイル アプリを管理できます。 モダン アプリのワークロードを移行するには、共同管理のプロパティ ページに移動します。 スライダー バーを、[Configuration Manager] から [パイロット] または [すべて] に移動します。 

このワークロードを移行すると、Intune から展開された使用可能なアプリが、すべてポータル サイトで使用可能になります。 Configuration Manager から展開するアプリは、ソフトウェア センターで使用できます。 

詳細については、以下の記事を参照してください。  

- [Windows 10 デバイスの共同管理](../../comanage/overview.md)  

- [Microsoft Intune アプリの管理とは](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a> ピアのダウンロードの境界グループのオプション
<!--1356193-->
環境内のコンテンツ配布をより細かく制御できるように、境界グループに追加の設定が設けられました。 このリリースでは、次のオプションが追加されます。  

- **この境界グループのピアのダウンロードを許可する**:既定では、この設定は有効になっています。 管理ポイントでは、ピア ソースを含むコンテンツの場所のリストがクライアントに提供されます。 <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    このオプションの無効化を検討する必要がある一般的なシナリオが 2 つあります。  

    - VPN など、地理的に分散した場所からの境界を含む境界グループがある場合。 VPN を介して接続されるため同じ境界グループ内にある 2 つのクライアントが、コンテンツのピアの共有に適さないほど遠く離れた場所に位置している可能性があります。  

    - サイトの割り当てに、配布ポイントを参照しない、1 つの大規模な境界グループを使用する場合。  

- **ピアのダウンロード中に、同じサブネット内のピアのみを使用する**:この設定は、上記のいずれかに依存します。 このオプションを有効にした場合、管理ポイントのコンテンツの場所のリストには、クライアントと同じサブネット内にあるピア ソースのみが含まれます。

    このオプションを有効にする一般的なシナリオを次に示します。

    - コンテンツの配布のための境界グループの設計に、その他の小さい境界グループと重複する 1 つの大規模な境界グループが含まれている場合。 この新しい設定では、管理ポイントがクライアントに提供するコンテンツ ソースのリストには同じサブネットからのピア ソースのみが含まれます。

    - リモート オフィス内のすべての場所のために 1 つの大規模な境界グループがある場合。 このオプションを有効にすると、クライアントは、場所の間でコンテンツを共有するリスクを負う代わりに、リモート オフィス内の場所にあるサブネット内でのみコンテンツを共有します。


### <a name="known-issue"></a>既知の問題
ピア ソースのクライアントが複数の IP アドレス (IPv4、IPv6、またはその両方) を所有している場合、ピア キャッシュが機能しません。 ピア ソースに複数の IP アドレスがある場合、新しいオプション (**ピアのダウンロード中に、同じサブネット内のピアのみを使用する**) が機能しません。<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a> カスタム カタログ用のサード パーティ製ソフトウェアの更新プログラムのサポート
<!--1358714-->
皆さまからの [UserVoice フィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)を反映し、このリリースではサード パーティのソフトウェア更新プログラムのサポートをさらに繰り返し行います。 [Technical Preview バージョン 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) では、"*パートナー カタログ*" (ソフトウェア ベンダーが登録したカタログ) のサポートが提供されます。 自身で提供する、Microsoft に登録されていないカタログを、*カスタム カタログ*と呼びます。 Configuration Manager コンソールでカスタム カタログを追加します。  


### <a name="prerequisites"></a>[前提条件] 

- [サード パーティ製ソフトウェアの更新プログラム](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)を設定します。 「フェーズ 1:機能を有効にして設定する」を完了します。   

- デジタル署名されているソフトウェア更新プログラムを含む、デジタル署名されているカスタム カタログ。  

- 管理者には次のアクセス許可が必要です。  

    - サイト:作成、変更  


### <a name="try-it-out"></a>試してみましょう。

タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[ソフトウェア更新プログラム]** を展開して、 **[サード パーティのソフトウェア更新プログラムのカタログ]** ノードを選択します。 リボンで **[Add Custom Catalog]\(カスタム カタログの追加\)** をクリックします。  

2. **[全般]** ページで、次の詳細を指定します。  

    - **[ダウンロード URL]** :カスタム カタログの有効な HTTPS アドレス。  

    - **[発行者]** :カタログを発行している組織の名前。  

    - **名前**:Configuration Manager コンソールに表示されるカタログの名前。  

    - **説明**:カタログの説明。  

    - **サポート URL** (省略可能):カタログのヘルプを取得するための Web サイトの有効な HTTPS アドレス。  

    - **サポートの連絡先** (省略可能):カタログのヘルプを得るための連絡先情報。  

3. ウィザードを完了します。 ウィザードによって、新しいカタログがサブスクライブされていない状態で追加されます。  

4. 既存の **[カタログのサブスクライブ]** アクションを使用して、カスタム カタログをサブスクライブします。 詳細については、「[フェーズ 2:サード パーティのカタログをサブスクライブして更新プログラムを同期する](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates)」をご覧ください。  

> [!Note]  
> 同じダウンロード URL のカタログを追加することはできません。また、カタログのプロパティを編集することはできません。 カスタム カタログの正しくないプロパティを指定する場合は、もう一度追加する前に、カタログを削除します。  


#### <a name="unsubscribe-from-a-catalog"></a>カタログのサブスクライブを解除する
カタログのサブスクライブを解除するには、一覧から目的のカタログを選択し、リボンで **[Unsubscribe Catalog]\(カタログのサブスクライブ解除\)** をクリックします。 カタログのサブスクライブを解除すると、次のアクションと動作が発生します。 
- サイトは、新しい更新プログラムの同期を停止します。 
- サイトは、カタログの署名とコンテンツの更新のために関連付けられている証明書をブロックします。 
- 既存の更新プログラムは削除されませんが、それらを発行または展開できない場合があります。

#### <a name="delete-a-custom-catalog"></a>カスタム カタログの削除
コンソールの同じノードからカスタム カタログを削除します。 "*サブスクライブされていない*" 状態のカスタム カタログを選択し、 **[Delete Custom Catalog]\(カスタム カタログの削除\)** をクリックします。 カタログを既にサブスクライブしている場合は、削除する前にまずサブスクライブ解除します。 パートナー カタログを削除することはできません。 削除したカスタム カタログは、カタログの一覧から削除されます。 このアクションは、ソフトウェアの更新ポイントに発行したソフトウェア更新プログラムには影響しません。


### <a name="known-issue"></a>既知の問題
カスタム カタログの削除アクションが灰色表示されるため、コンソールからカスタム カタログを削除することができません。 この問題を回避するには、サイト サーバーの **wbemtest** ツールを使用します。 削除するインスタンスに対して、名前かダウンロード URL を使用してクエリを実行します。例: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`。 クエリの結果ウィンドウで、オブジェクトを選択し、 **[削除]** をクリックします。<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a> クラウド管理機能の改善

このリリースには、次の機能改善が含まれています。  

- 次の機能で Azure 米国政府機関クラウドの使用がサポートされました。<!--511980-->  

    - [Azure サービス](../servers/deploy/configure/azure-services-wizard.md) を使用した**クラウド管理**のためのサイトのオンボード  

    - [Azure Resource Manager を使用するクラウド管理ゲートウェイ](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)の展開  

    - [Azure Resource Manager を使用するクラウド配布ポイント](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)の展開  

- ユーザーは、Windows AutoPilot を使用して、オンプレミス ネットワークに接続された、Azure Active Directory に参加しているデバイスに Windows 10 をプロビジョニングしています。 これらのデバイスで Configuration Manager クライアントをインストールまたはアップグレードするために、**クライアントに匿名接続を許可する**ために構成したクラウド配布ポイントやオンプレミスの配布ポイントが必要なくなりました。 代わりに、**HTTP サイト システム用に Configuration Manager で生成された証明書を使用する**サイトのオプションを有効にします。これにより、クラウド ドメイン参加しているクライアントが、オンプレミスの HTTP が有効な配布ポイントと通信できるようになります。 詳細については、「[改善されたセキュアなクライアント通信](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications)」をご覧ください。<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a> 新しいソフトウェア更新プログラムのコンプライアンス レポート
<!--1357775-->
ソフトウェア更新プログラムのコンプライアンス レポートの従来の表示には、最近サイトに接続していないクライアントからのデータが含まれていました。 新しいレポートでは、特定のソフトウェア更新プログラム グループのコンプライアンス結果を、"正常な" クライアントでフィルター処理できます。 このレポートでは、環境内のアクティブなクライアントの、より現実的なコンプライアンスの状態が表示されます。 
 
レポートを表示するには、 **[監視]** ワークスペースに移動し、 **[レポート]** を展開し、 **[レポート]** を展開し、 **[ソフトウェア更新プログラム - A コンプライアンス]** を展開して、 **[コンプライアンス 9 - 全体的な正常性とコンプライアンス]** を選択します。 **[グループの更新]** 、 **[コレクション名]** 、 **[クライアントのヘルス]** 状態を指定します。

レポートには、次の部分が含まれます。
- **[正常なクライアント対合計クライアント]** :この棒グラフでは、指定した期間にサイトと通信した "正常な" クライアントと、指定したコレクション内のクライアントの合計数が比較されます。
- **[Compliance Overview]\(コンプライアンスの概要\)** :この円グラフでは、指定したコレクション内のアクティブなクライアントでの、特定のソフトウェア更新プログラム グループの全体的なコンプライアンスの状態が示されます。
- **[Top 5 Non-Compliant by Article ID]\(アーティクル ID 別非準拠トップ 5\)** :この棒グラフでは、指定したコレクション内のアクティブなクライアントで準拠していない、指定したグループ内の上位 5 つのソフトウェア更新プログラムが表示されます。
- レポートの下部には、さらなる詳細のテーブルがあります。ここでは、指定したグループ内のソフトウェア更新プログラムが一覧表示されます。



## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。    
