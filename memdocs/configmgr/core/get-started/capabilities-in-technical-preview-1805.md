---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview バージョン 1805 で利用できる新しい機能について説明します。
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 88234bb3117850bc3280242671ae459308a5262e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696030"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Configuration Manager の Technical Preview 1805 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1805 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Technical Preview サイトに追加できます。 

この更新プログラムをインストールする前に、[Technical Preview](technical-preview.md) に関する記事を確認してください。 この記事により、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、フィードバックを提供する方法についての理解を深めることができます。     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**このバージョンでお試しいただける新機能を次に示します。**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>タスク シーケンスに手動で構成されたフェーズを使用して段階的展開を作成する
<!--1358148-->
タスク シーケンスに手動で構成されたフェーズを使用して、[段階的展開を作成](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)できます。 [Create Phased Deployment]\(段階的展開の作成\) ウィザードの **[フェーズ]** タブから、最大 10 個のフェーズを追加できます。 


### <a name="try-it-out"></a>試してみましょう。
手動ですべてのフェーズを構成する段階的展開を作成するには、次の手順に従います。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。 

1. **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、 **[タスク シーケンス]** を選択します。  

2. 既存のタスク シーケンスを右クリックして、 **[Create Phased Deployment]\(段階的展開の作成\)** を選択します。  

3. **[全般]** タブで、段階的展開の名前と説明 (省略可能) を入力し、 **[Manually configure all phases]\(すべてのフェーズを手動で構成する\)** を選択します。  

4. **[フェーズ]** タブで、 **[追加]** をクリックします。  

5. フェーズの **[名前]** を指定して、対象の **[フェーズのコレクション]** を参照します。  

6. **[フェーズの設定]** タブで、各スケジュール設定に対して以下のいずれか 1 つのオプションを選択し、完了したら **[次へ]** を選択します。  

    - 前のフェーズの成功基準 (このオプションは、最初のフェーズでは無効になっています)
        - **[展開の成功率]** :前のフェーズの成功基準に対して展開を正常に完了したデバイスの割合を指定します。  

    - 前のフェーズが成功した後に展開のこのフェーズを開始するための条件  
        - **[この段階は遅延期間 (日数) の後、自動的に開始する]** :前の段階が成功した後に次の段階を開始するまでに待機する日数を選択します。 
        - **[この段階の展開を手動で開始する]** :前の段階が成功した後に自動的にこの段階を開始しません。  

    - デバイスが対象になったら、ソフトウェアをインストールする
        - **直ちに**: デバイスがターゲットになったらすぐに、デバイスへのインストール期限を設定します。
        - **[期限 (デバイスが対象となった時点からの時間)]** :デバイスがターゲットになってから一定の日数後にインストールの期限を設定します。  
     
7. フェーズの設定ウィザードを完了します。

8. [Create Phased Deployment]\(段階的展開の作成\) ウィザードの **[フェーズ]** タブで、この展開のフェーズを追加、削除、並べ替え、または編集できるようになりました。  

9. [Create Phased Deployment]\(段階的展開の作成\) ウィザードを完了します。  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Azure Resource Manager のためのクラウド配布ポイントのサポート
<!--1322209-->
[クラウド配布ポイント](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) のインスタンスを作成するとき、**Azure Resource Manager の展開**を作成するためのオプションがウィザードで提供されるようになりました。 [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) は、[リソース グループ](/azure/azure-resource-manager/resource-group-overview#resource-groups)と呼ばれる単一のエンティティとしてすべてのソリューション リソースを管理するための最新のプラットフォームです。 Azure Resource Manager でクラウド配布ポイントを展開するとき、サイトは Azure Active Directory (Azure AD) を使って必要なクラウド リソースの認証と作成を行います。 この最新の展開では、従来の Azure 管理証明書は必要ありません。  

クラウド配布ポイント ウィザードでは、Azure 管理証明書を使う**従来のサービス展開**のためのオプションがまだ提供されています。 リソースの展開と管理を簡単にするため、すべての新しいクラウド配布ポイントに Azure Resource Manager デプロイ モデルを使うことをお勧めします。 可能であれば、Resource Manager で既存のクラウド配布ポイントを再展開してください。

Configuration Manager では、既存の従来のクラウド配布ポイントが Azure Resource Manager デプロイ モデルに移行されることはありません。 Azure Resource Manager の展開を使用して新しいクラウド配布ポイントを作成してから、従来のクラウド配布ポイントを削除してください。 

> [!IMPORTANT]  
> この機能では、Azure クラウド サービス プロバイダー (CSP) のサポートは有効になりません。 Azure Resource Manager でのクラウド配布ポイントの展開では引き続き従来のクラウド サービスが使われ、CSP はこれをサポートしません。 詳細については、「[Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)」(Azure CSP で使用可能な Azure サービス) を参照してください。  


### <a name="prerequisites"></a>[前提条件]  
- [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md) との統合。 Azure AD のユーザー探索は必要ありません。  

- Azure 管理証明書を除く、同じ[クラウド配布ポイントの要件](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements)。  


### <a name="try-it-out"></a>試してみましょう。  
 タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールの **管理** ワークスペースで、**クラウド サービス** を展開して、**クラウド配布ポイント** を選択します。 リボンにある **[クラウド配布ポイントの作成]** をクリックします。   

2. **[全般]** ページで、 **[Azure Resource Manager の展開]** を選びます。 **[サインイン]** をクリックし、Azure サブスクリプション管理者アカウントで認証を行います。 ウィザードは、統合の前提条件の間に格納された Azure AD サブスクリプション情報から、残りのフィールドを自動的に設定します。 複数のサブスクリプションを所有している場合は、使う適切なサブスクリプションを選びます。 **[次へ]** をクリックします。  

3. **[設定]** ページで、サーバーの PKI **証明書ファイル**を通常どおりに提供します。 この証明書では、Azure によって使用される、クラウド配布ポイントの**サービスの FQDN** を定義しています。 **[領域]** を選び、リソース グループ オプションとして **[新規作成]** または **[既存のものを使用]** を選びます。 新しいリソース グループ名を入力するか、ドロップダウン リストから既存のリソース グループを選びます。  

4. ウィザードを完了します。  

> [!NOTE]  
> 選んだ Azure AD サーバー アプリについて、Azure でサブスクリプションに**共同作成者**アクセス許可が割り当てられます。  

サービス接続ポイントの **cloudmgr.log** で、サービス展開の進行状況を監視します。



## <a name="take-actions-based-on-management-insights"></a>管理の洞察に基づいて対策する
<!--1357930-->
[管理の洞察](../servers/manage/management-insights.md)のいくつかで、対策を行うことが可能になりました。 ルールに応じて、この対策は次の動作のいずれかになります。  

- コンソールで、さらに詳細な対策を行うことが可能なノードへ、自動的に移動する。 たとえば、管理の洞察によって、クライアント設定の変更が推奨された場合、[クライアント設定] ノードへの移動という対策を行います。 既定またはカスタムのクライアント設定オブジェクトを変更することで、さらに詳細な対策を行うことができます。  

- クエリに基づいてフィルター処理されたビューに移動する。 たとえば、空のコレクション ルールに対して対策を行うと、単にコレクションの一覧にこれらのコレクションが表示されるようになります。 ここで、コレクションの削除やメンバーシップ ルールの変更など、さらに詳細な対策を行うことができます。  

このリリースでは、次に示す管理の洞察ルールに対策が用意されています。
- セキュリティ
    - サポートされていないバージョンのマルウェア対策クライアント
- ソフトウェア センター
    - ソフトウェア センターの新しいバージョンを使用する
- アプリケーション
    - 展開のないアプリケーション
- 簡素化された管理
    - CB 以外のクライアント バージョン
- コレクション
    - 空のコレクション 
- クラウド サービス
    - クライアントを最新の Windows 10 バージョンに更新する



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>共同管理を使用して Intune にデバイス構成ワークロードを移行する
<!--1357903-->

共同管理を有効にした後に、Configuration Manager から Intune にデバイス構成ワークロードを移行できるようになりました。 このワークロードを移行することで、アプリケーションの展開に Configuration Manager を引き続き使用したうえで、Intune を使用して MDM ポリシーを展開できるようになります。 

このワークロードを移行するには、共同管理プロパティ ページに移動して、スライド バーを Configuration Manager から**パイロット**または**すべて**に移動します。 詳細については、「[Windows 10 デバイスの共同管理](../../comanage/overview.md)」を参照してください。

> [!Note]  
> また、このワークロードを移行すると、デバイス構成ワークロードのサブセットである**リソース アクセス**と **Endpoint Protection** のワークロードも移動されます。

このワークロードを移行する場合、Intune がデバイス構成機関であっても、Configuration Manager から共同管理デバイスに引き続き設定を展開できます。 この例外は、組織で必要とされる設定を構成するために使用できるかもしれませんが、Intune ではまだ利用できません。 この例外は、Configuration Manager の構成基準で指定します。 ベースラインを作成するとき、または既存のベースラインのプロパティの **[全般]** タブ上で、 **[Always apply this baseline even for co-managed clients]\(共同管理クライアントにもこのベースラインを常に適用する\)** のオプションを有効にします。 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>ネットワークの輻そう制御を使用する配布ポイントを有効にする
<!--1358112-->

Windows Low Extra Delay Background Transport (LEDBAT) は、バックグラウンド ネットワーク転送を管理するための Windows Server の機能です。 サポートされている Windows Server のバージョンで実行される配布ポイントに対して、ネットワーク トラフィックを調整するオプションを有効にできます。 クライアントは利用可能な場合のみ、ネットワーク帯域幅を使用します。 

Windows LEDBAT の詳細については、「[New transport advancements](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/)」(新しいトランスポートの発展) ブログ投稿を参照してください。


### <a name="prerequisites"></a>[前提条件]
- Windows Server、バージョン 1709 での配布ポイント。  

- クライアントの前提条件はありません。<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[配布ポイント]** ノードを選択します。 対象となる配布ポイントを選び、リボンにある **[プロパティ]** を選択します。  

2. **[全般]** タブで、 **[Adjust the download speed to use the unused network bandwidth (Windows LEDBAT)]\(未使用のネットワーク帯域幅を使用するようにダウンロード速度を調整する (Windows LEDBAT)\)** のオプションを有効にします。  



## <a name="cloud-management-dashboard"></a>クラウド管理ダッシュボード
<!--1358461-->
新しい**クラウド管理ダッシュ ボード**では、クラウド管理ゲートウェイ (CMG) 使用量を一元化したビューを提供します。 Azure AD でサイトがオンボードになっている場合、クラウド ユーザーおよびデバイスに関するデータも表示します。  

次のスクリーンショットは、利用可能な 2 つのタイルを表示したクラウド管理ダッシュ ボードの一部です。  
![クラウド管理ダッシュボード タイルの CMG トラフィックと現在のオンライン クライアント](media/1358461-cmg-dashboard.png)

また、この機能には、トラブルシューティングを支援するリアルタイム検証のための **CMG 接続アナライザー**も含まれます。 コンソール内ユーティリティは、サービスの状態と、CMG 接続ポイント経由で CMG トラフィックを許可する任意の管理ポイントへの通信チャネルをチェックします。


### <a name="prerequisites"></a>[前提条件]
- インターネット ベース クライアントによって使用される、アクティブな[クラウド管理ゲートウェイ](../clients/manage/cmg/plan-cloud-management-gateway.md)。  

- クラウド管理のために [Azure サービス](../servers/deploy/configure/azure-services-wizard.md)にオンボードされているサイト。  


### <a name="try-it-out"></a>試してみましょう。
タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

#### <a name="cloud-management-dashboard"></a>クラウド管理ダッシュボード

Configuration Manager コンソールで、 **[監視]** ワークスペースに移動します。 **[クラウド管理]** ノードを選択して、ダッシュボード タイルを表示します。  

#### <a name="cmg-connection-analyzer"></a>CMG 接続アナライザー

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[クラウド サービス]** を展開し、 **[クラウド管理ゲートウェイ]** を選択します。  

2. 対象となる CMG インスタンスを選択して、リボンにある **[接続アナライザー]** を選択します。  

3. [CMG connection analyzer]\(CMG 接続アナライザー\) ウィンドウで、サービスを認証するための次のいずれかのオプションを選択します。  

     1. **Azure AD のユーザー**: このオプションを使用して、Azure AD に参加している Windows 10 デバイスにログオン済みのクラウド ベースのユーザー ID と同じ通信をシミュレートします。 **[サインイン]** をクリックして、この Azure AD ユーザー アカウントのための資格情報を安全に入力します。  

     2. **クライアント証明書**: このオプションを使用して、[クライアント認証証明書](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth)を使用した Configuration Manager クライアントと同じ通信をシミュレートします。  

4. **[開始]** をクリックして、分析を開始します。 結果は、アナライザー ウィンドウに表示されます。 エントリを選択すると、[説明] フィールドにさらに詳しい詳細が表示されます。  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager では、レポートを目的として顧客が使用する、デバイス データの大規模な一元化ストアを常に提供しています。 ただし、データは、クライアントから最後に収集された時点までの精度です。 

CMPivot は、お使いの環境でリアルタイム状態のデバイスへのアクセスを提供する、新しいコンソール内ユーティリティです。 対象となるコレクション内の現在接続されているすべてのデバイス上で直ちにクエリを実行して、結果を返します。 ツール内で、このデータのフィルター処理およびグループ化が可能です。 オンライン クライアントからリアルタイム データを提供することで、業務上の質問に迅速に回答し、問題をトラブルシューティングし、セキュリティの問題に対応できます。

たとえば、[予測実行によるサイド チャネルの脆弱性を緩和する](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)場合、 システムの BIOS の更新が要件の 1 つになっています。 CMPivot を使用して、システム BIOS 情報に対して迅速にクエリを実行し、コンプライアンスにはないクライアントを検索できます。 

このスクリーンショットでは、CMPivot は、デバイス数がそれぞれ 1 の独立した 2 つの BIOS バージョンを表示しています。 CMPivot を試行する場合は、このサンプル クエリを使用できます。  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![BIOSVersion のサンプル クエリを示したCMPivot ウィンドウ](media/1358456-cmpivot-biosversion.png)

デバイス数をクリックすると、詳細へ移動して特定のデバイスを確認できます。 CMPivot でデバイスを表示する場合、デバイスを右クリックして、以下の[クライアント通知アクション](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)を選択します。
- スクリプトを実行する
- リモート コントロール
- リソース エクスプローラー

特定のデバイスを右クリックすると、特定のデバイスのビューを次のいずれかの属性へピボットすることもできます。
- 自動開始コマンド
- インストールされている製品
- プロセス数
- サービス
- Users
- アクティブな接続
- 不足している更新プログラム

### <a name="prerequisites"></a>[前提条件]
- 対象クライアントは、最新バージョンに更新する必要があります。  

- Configuration Manager の管理者には、スクリプトを実行するためのアクセス許可が必要です。 詳細については、[スクリプトのセキュリティ ロール](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles)に関するセクションを参照してください。  

### <a name="try-it-out"></a>試してみましょう。
タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス コレクション]** を選択します。 対象となるコレクションを選択し、リボンにある **[Start CMPivot]\(CMPivot の開始\)** をクリックして、ツールを起動します。  

2. インターフェイスでは、ツールの使用に関する詳細情報を提供しています。 
     - 最上部でクエリ文字列を手動入力したり、インライン ドキュメントのリンクをクリックしたりすることも可能です。
     - いずれかの**エントリ**をクリックして、クエリ文字列にそのエントリを追加します。 
     - **テーブル演算子**、**集計関数**、および**スカラー関数**へのリンクでは、Web ブラウザーの言語リファレンス ドキュメントが開かれます。 CMPivot では、[Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/)と同じクエリ言語を使用します。



## <a name="improved-secure-client-communications"></a>改善されたセキュアなクライアント通信
<!--1356889,1358228,1358460-->
HTTPS 通信の使用は、すべての Configuration Manager 通信パスで推奨されていますが、PKI 証明書の管理のオーバーヘッドが原因で、一部の顧客にとっては、この使用が困難な課題になってしまう場合があります。 Azure Active Directory (Azure AD) の統合を導入することで、一部は軽減されますが、証明書要件のすべてには対応できません。 

このリリースでは、クライアントがシステム クライアントと通信する方法を強化しました。 これらの強化の主な目的は、以下の 2 つです。  

- PKI サーバー認証証明書を必要とせずにクライアント通信を保護できる。  

- クライアントは、ネットワーク アクセス アカウントを必要とせずに、配布ポイントからコンテンツに安全にアクセスできる。  

> [!Note]  
> PKI 証明書は、この証明書を使用したい顧客にとって引き続き有効なオプションです。  


### <a name="scenarios"></a><a name="bkmk_token"></a> シナリオ
これらの強化によって、次のシナリオでの動作が向上しました。  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a> シナリオ 1:管理ポイントに対するクライアント
<!--1356889-->
[Azure AD に参加したデバイス](/azure/active-directory/devices/concept-azure-ad-join)は、HTTP 用に構成された管理ポイントを使用して、クラウド管理ゲートウェイ (CMG) 経由で通信できます。 サイト サーバーは、管理ポイントに対する証明書を生成して、安全なチャネル経由での通信を可能にします。   

> [!Note]  
> この動作は、このシナリオに HTTPS を有効化した管理ポイントを必要とする Configuration Manager の現在のブランチ バージョン 1802 から変更されました。 詳細については、「[HTTPS 用の管理ポイントを有効にする](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)」を参照してください。  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a> シナリオ 2:配布ポイントに対するクライアント
<!--1358228-->
ワークグループまたは Azure AD に参加しているクライアントは、HTTP 用に構成されている配布ポイントから安全なチャネル経由でコンテンツをダウンロードできます。   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a> シナリオ 3 Azure AD デバイス ID 
<!--1358460-->
Azure AD に参加している、または[ハイブリッドの Azure AD デバイス](/azure/active-directory/devices/concept-azure-ad-join-hybrid)は、ログインしている Azure AD ユーザーがいない場合、割り当てられているサイトと安全に通信できます。 現在は、CMG および管理ポイントで認証するには、クラウドベースのデバイス ID で十分になりました。  


### <a name="prerequisites"></a>[前提条件]  

- HTTP クライアント接続用に構成された管理ポイント。 サイトのシステム ロール プロパティの **[全般]** タブで、このオプションを設定します。  

- HTTP クライアント接続用に構成された配布ポイント。 サイトのシステム ロール プロパティの **[全般]** タブで、このオプションを設定します。 **[Allow clients to connect anonymously]\(クライアントに匿名での接続を許可する\)** のオプションを有効にしないでください。  

- クラウド管理ゲートウェイ。  

- クラウド管理のために、サイトを Azure AD にオンボードします。  

    - 既にサイトでこの前提条件を満たしている場合は、Azure AD アプリケーションを更新する必要があります。 Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[クラウド サービス]** を展開して **[Azure Active Directory テナント]** を選択します。 Azure AD テナントを選択し、 **[アプリケーション]** ウィンドウで Web アプリケーションを選択して、リボンにある **[Update application setting]\(アプリケーション設定の更新\)** をクリックします。  

- Windows 10 バージョン 1803 を実行し、Azure AD に参加しているクライアント (この要件は技術上、[シナリオ 3](#bkmk_token3) のみに適用されます)。 


### <a name="try-it-out"></a>試してみましょう。
タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** を選択します。 サイトを選択して、リボンにある **[プロパティ]** をクリックします。  

2. **[クライアント コンピューターの通信方法]** タブに切り替えます。 **[HTTPS or HTTP]\(HTTPS または HTTP\)** のオプションを選択してから、 **[Use Configuration Manager-generated certificates for HTTP site systems]\(HTTP サイト システム用に Configuration Manager で生成された証明書を使用する\)** の新しいオプションを有効にします。  

検証するには、前記の[シナリオ一覧](#bkmk_token)を確認してください。

> [!Tip]
> このリリースでは、管理ポイントがサイトから新しい証明書を受信して構成するまで、最大 30 分待機します。

Configuration Manager コンソールでこれらの証明書を確認できます。 **[管理]** ワークスペースに移動して、 **[セキュリティ]** を展開し、 **[証明書]** ノードを選択します。 SMS 発行ルートによって発行されたサイト サーバー ロール証明書と共に、**SMS 発行**ルート証明書を検索します。


### <a name="known-issues"></a>既知の問題
- 対象になっている利用可能なすべてのアプリケーションが、ソフトウェア センターでユーザーに表示されるわけではありません。  

- OS 展開シナリオには、引き続きネットワーク アクセス アカウントが必要です。  

- **[Use Configuration Manager-generated certificates for HTTP site systems]\(HTTP サイト システム用に Configuration Manager で生成された証明書を使用する\)** のオプションを短い期間で繰り返し有効/無効にすると、証明書がサイト システム ロールに正しくバインドされない可能性があります。 "SMS 発行" 証明書によって発行された証明書は、Windows Server Internet Information Services (IIS) の Web サイトにバインドされません。 この問題を回避するには、Windows の **SMS** 証明書ストアから "SMS 発行" によって発行されたすべての証明書を削除してから、smsexec サービスを再起動します。



## <a name="improvements-for-enabling-third-party-software-update-support"></a>サード パーティ製のソフトウェア更新プログラムのサポートを有効にするための機能強化
<!--1357605-->
[[サード パーティ製のソフトウェア更新プログラムのサポートを有効にする]](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co) に寄せられるUserVoice フィードバックの結果として、このリリースでは、System Center Updates Publisher (SCUP) との統合において、さらにイテレーション機能を強化しました。 Configuration Manager Technical Preview [バージョン 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) では、サードパーティ製更新プログラムのために WSUS から証明書を読み取り、その証明書をクライアントに展開する機能が追加されました。 しかし、以前と同様に、サードパーティ製ソフトウェア更新プログラムに署名するために、SCUP ツールを使用して証明書を作成および管理する必要がありました。

このリリースでは、自動的に証明書を構成する Configuration Manager サイトを有効にできます。 サイトは、WSUS と通信して、この目的に合った証明書を生成します。 Configuration Manager は、続けてその証明書をクライアントに展開します。 このイテレーション機能によって、SCUP ツールを使用して証明書を作成および管理する必要がなくなりました。 

SCUP ツールの一般的な用途の詳細については、「[System Center Updates Publisher](../../sum/tools/updates-publisher.md)」を参照してください。

### <a name="prerequisites"></a>[前提条件]
- **[ソフトウェア更新プログラム]** グループのクライアント設定 **[サード パーティ製のソフトウェア更新プログラムを有効にする]** を有効化して展開している。
- WSUS がソフトウェアの更新ポイントとは別のサーバー上にある場合は、リモート WSUS サーバー上で次のいずれかを行う。
    - Windows でリモート レジストリ サービスを有効にする  
    または
    - レジストリ キー `HKLM\Software\Microsoft\Update Services\Server\Setup` に、値 `1` が設定された **EnableSelfSignedCertificates** という新しい DWORD を作成する 

### <a name="try-it-out"></a>試してみましょう。
タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[サイトの構成]** を展開し、 **[サイト]** を選びます。 最上位のサイトを選択して、リボンにある **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** を選択します。  

2. **[サード パーティ製の更新プログラム]** タブに切り替えます。 **[サード パーティ製のソフトウェア更新プログラムを有効にする]** のオプションを選択してから、 **[Configuration Manager automatically manages the certificate]\(Configuration Manager が自動的に証明書を管理する\)** を選択します。

3. サードパーティ製ソフトウェア更新プログラムのカタログをインポートするために、一般的な SCUP ワークフローの残りの部分を続行してから、更新プログラムをクライアントに展開します。



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 一括アップグレード タスク シーケンスの機能強化
<!--1358500-->

Windows 10 の一括アップグレード用の既定のタスク シーケンス テンプレートに、アップグレード プロセスが失敗した場合に追加する推奨アクションを備えた、新しい別のグループが含まれるようになりました。 これらのアクションによって、トラブルシューティングが容易になりました。

### <a name="new-groups-under-run-actions-on-failure"></a>**[Run actions on failure]\(エラー時にアクションを実行する\)** にある新しいグループ
- **ログの収集**:クライアントからログを収集するには、このグループに手順を追加します。 
    - 通常は、ログ ファイルをネットワーク共有にコピーします。 この接続を確立するには、[ネットワーク フォルダーへの接続](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)の手順を使用します。 
    - コピー操作を実行するには、「[コマンド ラインの実行](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)」または「[PowerShell スクリプトの実行](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)」の手順のどちらかに従って、カスタム スクリプトまたはユーティリティを使用します。
    - 収集するファイルには、次のログ ファイルが含まれる可能性があります。  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - setupact.log および他の Windows Setup ログ ファイルの詳細については、[Windows 設定ログ ファイル](/windows/deployment/upgrade/log-files)に関するページをご覧ください。
    - Configuration Manager クライアント ログ ファイルの詳細については、「[Configuration Manager クライアントのログ ファイル](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs)」セクションをご覧ください。
    - _SMSTSLogPath および他の便利な変数の詳細については、[タスク シーケンス組み込み変数](../../osd/understand/task-sequence-variables.md)に関するページをご覧ください。

- **診断ツールの実行**:追加の診断ツールを実行するには、このグループで手順を追加します。 これらのツールは、エラー発生後できるだけすぐに、システムから追加情報を収集するために、自動化される必要があります。
    - このようなツールの 1 つが、Windows の [SetupDiag](/windows/deployment/upgrade/setupdiag) です。 これは、Windows 10 がアップグレードに失敗した詳細な理由の取得に使用できる、スタンドアロンの診断ツールです。
         - Configuration Manager で、ツールの[パッケージを作成](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program)します。
         - [コマンド ラインの実行](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)手順を、タスク シーケンスのこのグループに追加します。 **[パッケージ]** オプションを使用して、ツールを参照します。 次の文字列は、**コマンド ライン**のサンプルです。  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>クライアントと共にインストールされる CMTrace
<!--1357971-->

CMTrace ログ表示ツールが、Configuration Manager クライアントと共に自動的にインストールされるようになりました。 このツールは、クライアント インストール ディレクトリ (既定では、`%WinDir%\ccm\cmtrace.exe`) に追加されます。

> [!Note]  
> .log ファイル拡張子を開くために、CMTrace が Windows で自動登録されることは "*ありません*"。



## <a name="improvement-to-the-configuration-manager-console"></a>Configuration Manager コンソールの機能強化
<!--1358202-->
Configuration Manager コンソールに次の機能強化を行いました。

- [資産とコンプライアンス]、[デバイス] の下の [デバイス] 一覧に既定で、現在ログオンしているユーザーが表示されるようになりました。 この値は、現在の[クライアント ステータス](../clients/manage/monitor-clients.md#bkmk_indStatus)を示します。 ユーザーがログオフすると、値はクリアされます。 ログオンしているユーザーがいない場合、値は空白になります。 

### <a name="known-issues"></a>既知の問題
[デバイス] ノードで、または [デバイス コレクション] ノード下のデバイス一覧を表示した場合に、現在ログオンしているユーザーの値が空白になる。 この問題を回避するには、この [SQL スクリプト](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c)をダウンロードします。 サイトのデータベース サーバー上で sp_BgbUpdateLiveData.sql を実行してから、管理ポイント上で smsexec および sms_notification_server サービスを再起動してください。<!--514471-->



## <a name="improvements-to-console-feedback"></a>コンソール フィードバックの機能強化
<!--1357542-->
このリリースでは、Configuration Manager コンソールの新しい[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)機構に対して、次の機能強化を行いました。  

- フィードバック ダイアログで、選択したオプションや自分の電子メール アドレスなど、以前の設定を記憶できるようになりました。  

- オフラインのフィードバックがサポートされるようになりました。 コンソールから自分のフィードバックを保存して、インターネット接続システムから Microsoft にアップロードしてください。 `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe` に配置されている新しいオフライン フィードバック アップロード ツールを使用してください。 使用可能および必須のコマンド ライン オプションを確認するには、`--help` オプションを指定してツールを実行します。 接続されたシステムでは、**petrol.office.microsoft.com** へのアクセスが必要になります。

### <a name="known-issues"></a>既知の問題
インターネットに接続されたコンピューターのコンソールから **[気に入った機能の報告]** または **[問題点、改善点の報告]** を使用すると、次のメッセージが返される場合があります。"フィードバックの送信中にエラーが発生しました。" **[詳細]** をクリックすると、「`{"Message":""}`」というテキストが表示されます。 このエラーは、バックエンドのフィードバック システムの応答に関連する既知の問題が原因で発生します。 このエラーは無視できます。 Microsoft では、引き続きお客様のフィードバックも受信しています。 (詳細で別のメッセージが表示される場合は、オフラインのフィードバック オプションを使用して、後でフィードバックを送信し直してください。)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>PXE 対応の配布ポイントの機能強化
<!--1357580-->

このリリースでは、配布ポイントで [ **[Windows 展開サービスなしで PXE レスポンダーを有効にする]** ](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) のオプションを使用する場合に、次のような機能強化を行いました。  

- このオプションを有効にすると、Windows ファイアウォールの規則が自動的に作成される  
- コンポーネント ログ記録の機能強化



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>大きな整数値でのハードウェア インベントリの機能強化
<!--1357880-->
ハードウェア インベントリには現在、 4,294,967,296 (2^32) を超える整数値に対して制限があります。 この制限は、バイト単位のハード ドライブ サイズなどの属性も対象になる場合があります。 管理ポイントはこの制限を超える整数値を処理せず、そのため、値がデータベースに格納されません。 このリリースでは、制限が 18,446,744,073,709,551,616 (2^64) に引き上げられました。 

合計ディスク サイズなど、値が変更されないプロパティの場合は、サイトのアップグレード後に、すぐに値を確認することはできません。 ほとんどのハードウェア インベントリは、累計レポートです。 クライアントは、変更された値のみを送信します。 この動作を回避するには、同じクラスにもう 1 つのプロパティを追加します。 これにより、クライアントでは、変更されたクラス内のすべてのプロパティを更新するようになります。 



## <a name="improvement-to-wsus-maintenance"></a>WSUS メンテナンスの機能強化
<!--1357898-->

WSUS クリーンアップ ウィザードでは、有効期限が切れてているか、または置き換え規則に従って置き換えられた更新プログラムを拒否するようになりました。 これらの規則は、ソフトウェアの更新ポイントのコンポーネント プロパティで定義されています。

### <a name="try-it-out"></a>試してみましょう。
タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[サイトの構成]** を展開し、 **[サイト]** を選びます。 最上位のサイトを選択して、リボンにある **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** を選択します。  

2. **[置き換えの規則]** タブに切り替えます。 **[WSUS クリーンアップ ウィザードを実行します]** のオプションを有効にします。 目的の置き換え動作を指定します。  

3. WSyncMgr.log ファイルを確認します。



## <a name="improvement-to-support-for-cng-certificates"></a>CNG 証明書のサポートの強化
<!--1357314-->
このリリースでは、HTTPS が有効な以下の追加のサーバー役割に [CNG 証明書](../plan-design/network/cng-certificates-overview.md)を使用します。  
- Configuration Manager ポリシー モジュールを使った NDES サーバーを含む、証明書登録ポイント



## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。    
