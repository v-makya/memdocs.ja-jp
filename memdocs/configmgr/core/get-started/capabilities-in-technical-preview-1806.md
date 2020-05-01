---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview バージョン 1806 で利用できる新しい機能について説明します。
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 522e01b0d811d768d4f239bc917c2e3db08e05ef
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210079"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Configuration Manager の Technical Preview 1806 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1806 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Technical Preview サイトに追加できます。 

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

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a> サイトでリモート コンテンツ ライブラリを使用してアップグレードできない
<!--514642-->
**cmupdate.log** に示される以下のエラーが発生し、サイトでアップグレードできません。  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

コンテンツ ライブラリがリモートの場所にある場合、このリリースでこの問題が発生します。

#### <a name="workaround"></a>回避策
コンテンツ ライブラリを、サイト サーバーに対してローカルのドライブに移動します。 詳細については、「[サイト サーバーのリモート コンテンツ ライブラリを構成する](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)」を参照してください。 



</br>

**このバージョンでお試しいただける新機能を次に示します。**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a> サード パーティのソフトウェア更新プログラム
<!--1352101-->
皆さまからの [UserVoice フィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)を反映し、このリリースではサード パーティのソフトウェア更新プログラムのサポートをさらに繰り返し行います。 いくつかの一般的なシナリオでは、System Center Updates Publisher (SCUP) を使用する必要がなくなりました。 Configuration Manager コンソールの新しい **[サード パーティのソフトウェア更新プログラムのカタログ]** ノードでは、サード パーティのカタログをサブスクライブし、更新プログラムをソフトウェア更新ポイントに発行してからクライアントに展開できます。 

このリリースでは、次のサード パーティのソフトウェア更新プログラムのカタログを利用できます。

 | 発行者 | カタログ名 |
 |--------|---------------------|
 | HP | HP クライアント更新プログラム カタログ |

SCUP では引き続き、他のカタログとシナリオがサポートされます。 Configuration Manager コンソールの [サード パーティのソフトウェア更新プログラムのカタログ] ノードのカタログ リストは動的であり、追加のカタログが利用でき、サポートされる場合は更新されます。


### <a name="prerequisites"></a>[前提条件]
- HTTPS が有効なソフトウェア更新ポイントで、ソフトウェア更新管理を設定します。 詳細については、「[Prepare for software updates management](../../sum/get-started/prepare-for-software-updates-management.md)」 (ソフトウェア更新管理の準備) を参照してください。  
  - このリリースのこの機能を利用するには、ソフトウェア更新ポイントがサイト サーバー上にある必要があります。 <!--515810--> 

    > [!Tip]  
    > ソフトウェアの更新ポイントでは HTTPS が必要です。これは、署名証明書を処理するために使用される WSUS API の前提条件だからです。 クライアントが HTTPS 対応である必要はありません。 WSUS での HTTPS の有効化の詳細については、次の記事を参照してください。  
    > - [Secure Sockets Layer (SSL) プロトコルを使用して WSUS をセキュリティで保護する](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 
    > - [WSUS サポートのブログ記事](https://blogs.technet.microsoft.com/sus/2011/05/09/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names/)

- ソフトウェア更新ポイントの WSUSContent フォルダーに、サード パーティのソフトウェア更新プログラムのソース バイナリ コンテンツを格納するのに十分なディスク領域がある必要があります。 必要な記憶域の容量は、ベンダー、更新プログラムの種類、および展開のために発行する特定の更新プログラムによって異なります。 WSUSContent フォルダーを、空き領域がより多い別のドライブに移動する必要がある場合は、WSUS サポート チームのブログ記事「[How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/)」 (WSUS で更新プログラムをローカルに格納する場所を変更する方法) を参照してください。  

- **[ソフトウェア更新プログラム]** グループのクライアント設定 [[サード パーティ製のソフトウェア更新プログラムを有効にする]](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) を有効化して展開している。  

- サイト サーバーでは、HTTPS ポート 443 経由での download.microsoft.com へのインターネット アクセスが必要です。 サード パーティのソフトウェア更新プログラムの同期サービスは、現在、サイト サーバーで実行されています。 このサービスでは、利用可能なサード パーティ カタログのリストを更新し、サブスクライブ時にカタログをダウンロードし、発行時に更新プログラムをダウンロードします。 必要に応じて、サイト サーバー コンピューターのサイト システムの役割プロパティの **[プロキシ]** タブで、インターネット プロキシ設定を構成します。  


### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。


#### <a name="phase-1-enable-and-set-up-the-feature"></a>フェーズ 1:機能を有効にして設定する
*階層ごとに 1 回*、次の手順を実行して、機能を使用できるように設定します。  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[サイトの構成]** を展開し、 **[サイト]** ノードを選択します。  

2. 階層の最上位サイトを選択します。 リボンの **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** を選択します。  

3. **[サード パーティ製の更新プログラム]** タブに切り替えます。 **[サード パーティ製のソフトウェア更新プログラムを有効にする]** というオプションを選択します。 証明書のオプションの詳細については、「[サード パーティ製のソフトウェア更新プログラムのサポートを有効にするための機能強化](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)」を参照してください。  

   > [!Note]  
   > Configuration Manager の既定のオプションを使用して、この証明書を管理する場合、 **[管理]** ワークスペースの **[セキュリティ]** の下にある **[証明書]** ノードに、**サード パーティの WSUS 署名**という種類の新しい証明書が作成されます。  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>フェーズ 2:サード パーティのカタログをサブスクライブして更新プログラムを同期する
サブスクライブする*サード パーティのカタログごと*に、次の手順を実行します。  

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動します。 **[ソフトウェア更新プログラム]** を展開し、 **[サード パーティのソフトウェア更新プログラムのカタログ]** ノードを選択します。  

2. サブスクライブするカタログを選択し、リボンの **[カタログのサブスクライブ]** をクリックします。   

3. カタログの証明書を確認して承認します。  

   > [!Note]  
   > サード パーティのソフトウェア更新プログラム カタログをサブスクライブすると、ウィザードで確認して承認した証明書がサイトに追加されます。 この証明書の種類は、**サード パーティ製のソフトウェア更新プログラム カタログ**です。 これは、 **[管理]** ワークスペースの **[セキュリティ]** の下にある **[証明書]** ノードから管理できます。  

4. ウィザードを完了します。  

   > [!Tip]  
   > 初期サブスクリプションの後、すぐにカタログのダウンロードが開始されます。 その後、このリリースでは 24 時間ごとに再同期が行われます。 カタログが自動的にダウンロードされるまで待機しない場合は、リボンの **[今すぐ同期]** をクリックします。  
   > 
   > カタログがダウンロードされた後、製品のメタデータがソフトウェア更新ポイントに同期される必要があります。 このプロセスと、手動による開始方法の詳細については、「[ソフトウェア更新プログラムの同期](../../sum/get-started/synchronize-software-updates.md)」を参照してください。 この時点で、 **[すべての更新プログラム]** ノードでサード パーティの更新プログラムを確認できます。 

5. 次に、サブスクライブするサード パーティのカタログ用にソフトウェア更新ポイントの **[製品]** を構成します。 詳細については、「[同期する分類と製品の構成](../../sum/get-started/configure-classifications-and-products.md)」を参照してください。 製品の条件が変更された後に、もう一度ソフトウェア更新プログラムを同期する必要があります。

クライアントからのコンプライアンス結果を表示するには、更新プログラムをスキャンして評価する必要があります。 **ソフトウェア更新プログラムのスキャン サイクル**操作を実行することで、クライアントの Configuration Manager コンソール パネルからこのサイクルを手動でトリガーできます。 プロセスの詳細については、「[Software updates introduction](../../sum/understand/software-updates-introduction.md)」 (ソフトウェア更新プログラムの概要) を参照してください。


#### <a name="phase-3-deploy-third-party-software-updates"></a>フェーズ 3:サード パーティのソフトウェア更新プログラムを展開する
クライアントに展開する*すべてのサード パーティのソフトウェア更新プログラム*について、次の手順を実行します。  

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動します。 **[ソフトウェア更新プログラム]** を展開し、 **[すべてのソフトウェア更新プログラム]** ノードを選択します。  

   > [!Tip]  
   > **[条件の追加]** をクリックして、更新プログラムのリストをフィルター処理します。 たとえば、Adobe からのすべての更新プログラムを表示する場合は、**Adobe Systems, Inc. **の**ベンダー**を追加します。  

2. クライアントに必要な更新プログラムを選択します。 **[Publish Third-Party Software Update Content]\(サード パーティ製のソフトウェア更新プログラムのコンテンツを発行する\)** をクリックし、SMS_ISVUPDATES_SYNCAGENT.log で進行状況を確認します。 この操作で、ベンダーからの更新プログラム バイナリがダウンロードされ、ソフトウェア更新ポイントの WSUSContent フォルダーに格納されます。 また、更新プログラムの状態が、メタデータのみからコンテンツありおよび展開可能に変わります。  

   > [!Note]  
   > サード パーティ製のソフトウェア更新プログラムのコンテンツを発行するときに、コンテンツの署名に使用されるすべての証明書がサイトに追加されます。 これらの証明書の種類は、**サード パーティ製のソフトウェア更新プログラムのコンテンツ**です。 これらは、 **[管理]** ワークスペースの **[セキュリティ]** の下にある **[証明書]** ノードから管理できます。  

3. 既存のソフトウェア更新プログラムの管理プロセスを使用して、更新プログラムを展開します。 詳細については、「[ソフトウェアの更新の展開方法](../../sum/deploy-use/deploy-software-updates.md)」を参照してください。 ソフトウェア更新プログラムの展開ウィザードの **[ダウンロード場所]** ページで、 **[インターネットからソフトウェア更新プログラムをダウンロードする]** という既定のオプションを選択します。 このシナリオでは、展開パッケージのコンテンツのダウンロードに使用される、ソフトウェア更新ポイントにコンテンツが既に発行されています。


### <a name="monitoring-progress-of-third-party-software-updates"></a>サード パーティのソフトウェア更新プログラムの進行状況の監視
サード パーティのソフトウェア更新プログラムの同期は、サイト サーバー上の SMS_ISVUPDATES_SYNCAGENT コンポーネントによって処理されます。 このコンポーネントからステータス メッセージを表示したり、SMS_ISVUPDATES_SYNCAGENT.log でより詳細な状態を確認したりすることができます。 このログは、サイト サーバー上のサイト インストール ディレクトリの **Logs** サブフォルダーにあります。 既定では、このパスは `C:\Program Files\Microsoft Configuration Manager\Logs` です。 一般的なソフトウェア更新プログラム管理プロセスの監視の詳細については、「[ソフトウェア更新プログラムの監視](../../sum/deploy-use/monitor-software-updates.md)」を参照してください。


### <a name="known-issues"></a>既知の問題
- サード パーティのソフトウェア更新プログラムの同期サービスでは、**WSUS サーバー接続アカウント**を使用するように構成されたソフトウェアの更新ポイントはサポートされません。 このアカウントが [ソフトウェアの更新ポイントのプロパティ] ページの **[Proxy and Account Settings]\(プロキシとアカウントの設定\)** タブで構成されている場合は、SMS_ISVUPDATES_SYNCAGENT.log に次のエラーが表示されます。  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
このアカウントの詳細については、「[ソフトウェアの更新ポイントの接続アカウント](../plan-design/hierarchy/accounts.md#software-update-point-connection-account)」を参照してください。<!--515492-->  

- SCUP などの他のツールを、この新しい統合されたサード パーティのソフトウェア更新プログラム機能と一緒に使用しないでください。 サード パーティのソフトウェア更新プログラムの同期サービスでは、SCUP などの別のアプリケーション、ツール、またはスクリプトで WSUS に追加されたメタデータのみの更新プログラムにコンテンツを発行することはできません。 これらの更新プログラムに対する**サード パーティ製のソフトウェア更新プログラムのコンテンツを発行する**操作は失敗します。 この機能でまだサポートされていないサード パーティの更新プログラムを展開する必要がある場合は、完全に既存のプロセスを使用して更新プログラムを展開してください。<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Microsoft Edge 用に Windows Defender SmartScreen 設定を構成する
<!--1353701-->
このリリースでは、[Microsoft Edge ブラウザー コンプライアンスの設定ポリシー](../../compliance/deploy-use/browser-profiles.md)に、[Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) の 3 つの設定が追加されています。 ポリシーには、 **[SmartScreen の設定]** ページの次の追加設定が含まれるようになりました。
- **SmartScreen を許可する**:Windows Defender SmartScreen を許可するかどうかを指定します。 詳細については、[AllowSmartScreen ブラウザー ポリシー](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)に関するページを参照してください。
- **サイトの SmartScreen プロンプトをユーザーがオーバーライドできる**:悪意のある可能性がある Web サイトに関する Windows Defender SmartScreen フィルターの警告をユーザーがオーバーライドできるかどうかを指定します。 詳細については、[PreventSmartScreenPromptOverride ブラウザー ポリシー](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)に関するページを参照してください。
- **ファイルの SmartScreen プロンプトをユーザーがオーバーライドできる**:確認されていないファイルのダウンロードに関する Windows Defender SmartScreen フィルターの警告をユーザーがオーバーライドできるかどうかを指定します。 詳細については、[PreventSmartScreenPromptOverrideForFiles ブラウザー ポリシー](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)に関するページを参照してください。



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>共同管理されたデバイスのために MDM ポリシーを Microsoft Intune から同期する
<!--1357377-->
このリリース以降、[共同管理ワークロードを切り替える](../../comanage/how-to-switch-workloads.md)ときに、共同管理されたデバイスで自動的に Microsoft Intune から MDM ポリシーが同期されます。 この同期は、Configuration Manager コンソールのクライアント通知から**コンピューター ポリシーのダウンロード**操作を開始するときにも行われます。 詳細については、「[クライアント通知を使用してクライアント ポリシーの取得を開始する](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」を参照してください。



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>共同管理を使用して Intune に Office 365 ワークロードを移行する
<!--1357841-->
共同管理を有効にした後に、Configuration Manager から Microsoft Intune に Office 365 ワークロードを移行できるようになりました。 このワークロードを移行するには、共同管理プロパティ ページに移動して、スライド バーを Configuration Manager から [パイロット] または [すべて] に移動します。 詳細については、「[Windows 10 デバイスの共同管理](../../comanage/overview.md)」を参照してください。

**Office 365 アプリケーションがデバイス上の Intune で管理されているか**という新しいグローバル条件もあります。 この条件は、新しい Office 365 アプリケーションの要件として既定で追加されます。 このワークロードを移行すると、共同管理されたクライアントでアプリケーションの要件が満たされなくなるため、Configuration Manager で展開される Office 365 がインストールされません。

### <a name="known-issue"></a>既知の問題
- 現在、このワークロードの移行は Office 365 の展開にのみ適用されます。 Configuration Manager では引き続き Office 365 の更新プログラムが管理されます。<!--510876--> 可能な回避策を含む詳細については、Configuration Manager バージョン 1802 のリリース ノート「[Office 365 クライアント設定の変更が適用されない](../servers/deploy/install/release-notes.md)」を参照してください。



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager は統合ツールとなりました。これを使用して、従来の Configuration Manager 2007 パッケージを Configuration Manager の現在のブランチのアプリケーションに変換することができます。 その後、依存関係、要件の規則、およびユーザーとデバイスのアフィニティなど、アプリケーションの機能を使用することができます。

> [!Tip]  
> Package Conversion Manager の既存の機能に関する以前のドキュメントについては、[TechNet](https://technet.microsoft.com/library/hh531519.aspx) を参照してください。 関連する情報は docs.microsoft.com ライブラリに移行中です。

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

> [!Important]  
> 古いバージョンの Package Conversion Manager を以前にインストールした場合は、まず、それをアンインストールしてからサイトをアップグレードします。 新しい統合されたバージョンをインストールする必要はありませんが、既存のバージョンと競合する可能性があります。  

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動します。 **[アプリケーション管理]** を展開し、 **[パッケージ]** を選択します。  
2. パッケージを選択します。 リボンの **[Package Conversion]\(パッケージ変換\)** グループで、次の 3 つのオプションを使用できます。  
     - **パッケージの分析**:パッケージを分析して、変換プロセスを開始します。
     - **Convert Package\(パッケージ変換\)** :一部のパッケージは、この操作でアプリケーションに簡単に変換することができます。
     - **修正と変換**:一部のパッケージでは、アプリケーションに変換する前に問題を修正する必要があります。  

   これらの操作の詳細については、[パッケージを分析および変換する方法](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29)に関するページを参照してください。  

3. **[監視]** ワークスペースに移動して、 **[Package Conversion Status]\(パッケージ変換の状態\)** を選択します。 この新しいダッシュボードには、サイトでのパッケージの全体的な分析と変換の状態が示されます。 新しいバックグラウンド タスクでは、分析データの概要が自動的に示されます。  

   > [!Tip]  
   > Package Conversion Manager では、パッケージの分析のスケジュールを設定する必要はありません。 この操作は、統合された概要タスクで処理されるようになりました。  

![パッケージ変換の状態ダッシュボードのスクリーンショット](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>コンテンツなしのソフトウェア更新プログラムの展開
<!--1357933-->
最初にソフトウェア更新プログラムのコンテンツをダウンロードして配布ポイントに配布することなく、ソフトウェア更新プログラムをデバイスに展開できるようになりました。 この機能は、非常に大きい更新プログラムのコンテンツを処理する場合や、常にクライアントで Microsoft Update クラウド サービスからコンテンツを取得する場合に役立ちます。 このシナリオのクライアントでは、既に必要なコンテンツがあるピアからコンテンツをダウンロードすることもできます。 Configuration Manager クライアントで引き続きコンテンツのダウンロードが管理されるため、Configuration Manager のピア キャッシュ機能や、配信の最適化などの他のテクノロジを利用することができます。 この機能では、Windows および Office の更新プログラムを含む、Configuration Manager ソフトウェア更新プログラム管理でサポートされるすべての更新プログラムの種類がサポートされます。 

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. 通常どおり、ソフトウェアの更新の展開を開始します。 詳細については、「[ソフトウェアの更新の展開方法](../../sum/deploy-use/deploy-software-updates.md)」を参照してください。
2. ソフトウェアの更新の展開ウィザードの **[展開パッケージ]** ページで、 **[展開パッケージなし]** の新しいオプションを選択します。

### <a name="known-issues"></a>既知の問題
- この設定で展開された更新のアイコンが誤って表示され、更新が無効である場合と同じように赤色の X が示されます。 詳細については、「[ソフトウェア更新プログラムに使用されるアイコン](../../sum/understand/software-updates-icons.md)」を参照してください。 <!--515556-->  
- この設定は、ソフトウェアの更新の展開ウィザードにのみ統合されます。 現在、自動展開規則では使用できません。 <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office 365 インストーラーと Office カスタマイズ ツールの統合
<!--1358149-->
Office カスタマイズ ツールが、Configuration Manager コンソールの Office 365 インストーラーと統合されました。 Office 365 の展開を作成するときに、最新の Office の管理容易性設定を動的に構成できるようになりました。 Office カスタマイズ ツールは、Office 365 の新しいビルドのリリースと同時に更新されます。 Office 365 の新しい管理容易性設定は、使用可能になるとすぐに利用できるようになりました。 

### <a name="prerequisites"></a>[前提条件]
- Configuration Manager コンソールを実行しているコンピューターには、HTTPS ポート 443 経由のインターネット アクセスが必要です。 Office 365 クライアント インストール ウィザードでは、Windows の標準的な Web ブラウザー API を使用して https://config.office.com を開きます。 インターネット プロキシが使用されている場合、ユーザーはこの URL にアクセスできる必要があります。

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[Office 365 クライアント管理]** ノードを選択します。
2. ダッシュボードの **[Office 365 インストーラー]** タイルをクリックして、Office 365 クライアント インストール ウィザードを起動します。 詳細については、「[Office 365 アプリを展開する](../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps)」を参照してください。
3. **[Office の設定]** ページで、 **[Go To Office Web Page]\(Office Web ページへ移動\)** をクリックします。 オンラインの Office カスタマイズ ツールを使用して、この展開の設定を指定します。 
4. 完了したら、右上隅にある **[送信]** をクリックします。 Office 365 クライアントのインストール ウィザードを終了します。



## <a name="improvements-to-cloud-management-gateway"></a>クラウド管理ゲートウェイの機能改善
このリリースでは、クラウド管理ゲートウェイ (CMG) が次の点で機能強化されています。

### <a name="simplified-client-bootstrap-command-line"></a>簡略化されたクライアント ブートストラップ コマンド ライン
<!--1358215-->
CMG を介してインターネット上に Configuration Manager クライアントをインストールするときに、必要なコマンド ライン プロパティが少なくなりました。 このシナリオの 1 つの例の詳細については、共同管理の準備を行う場合の「[Configuration Manager クライアントをインストールするためのコマンド ライン](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)」を参照してください。 

すべてのシナリオで次のコマンド ライン プロパティが必要になります。
- CCMHOSTNAME  
- SMSSITECODE  

PKI ベースのクライアント認証証明書ではなく、クライアント認証で Azure AD を使用する場合は、次のプロパティが必要です。
- AADCLIENTAPPID  
- AADRESOURCEURI  

クライアントがイントラネットに再度ローミングされる場合は、次のプロパティが必要です。
- SMSMP  

次の例には、上記のプロパティのすべてが含まれます。   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

詳細については、「[クライアント インストールのプロパティ](../clients/deploy/about-client-installation-properties.md)」を参照してください。

### <a name="download-content-from-a-cmg"></a>CMG からコンテンツをダウンロードする
<!--1358651-->
これまでは、別の役割として、クラウド配布ポイントと CMG を展開する必要がありました。 このリリースでは、CMG でクライアントにコンテンツを提供できるようにもなりました。 この機能により、Azure VM の必要な証明書とコストが削減されます。 この機能を有効にするには、CMG プロパティの **[設定]** タブで **[Allow CMG to function as a cloud distribution point and serve content from Azure storage]\(CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする\)** という新しいオプションを有効にします。 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Azure AD では信頼されたルート証明書が必要ない
<!--503899-->
CMG を作成するときに、[設定] ページで[信頼されたルート証明書](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot)を指定する必要はなくなりました。 クライアント認証で Azure Active Directory (Azure AD) を使用するときにこの証明書は必要ありませんが、ウィザードで必要な場合は使用されます。

> [!Important]  
> PKI クライアント認証証明書を使用する場合は、引き続き信頼されたルート証明書を CMG に追加する必要があります。



## <a name="improvements-to-secure-client-communications"></a>セキュアなクライアント通信の改善
<!--1358278,1358279-->
このリリースでは引き続き、ネットワーク アクセス アカウントの追加の依存関係を削除することで、[セキュアなクライアント通信の改善](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)を繰り返し行います。 **[Use Configuration Manager-generated certificates for HTTP site systems]\(HTTP サイト システム用に Configuration Manager で生成された証明書を使用する\)** という新しいサイト オプションを有効にする場合、次のシナリオでは、配布ポイントからコンテンツをダウンロードするためのネットワーク アクセス アカウントは必要ありません。  

- ブート メディアまたは PXE から実行されているタスク シーケンス
- ソフトウェア センターから実行されているタスク シーケンス  

これらのタスク シーケンスは、OS の展開用またはカスタム用の場合があります。 ワークグループ コンピューターでもサポートされます。



## <a name="software-center-infrastructure-improvements"></a>ソフトウェア センターのインフラストラクチャの改善
<!--1358309-->
ユーザーが利用できるアプリケーションをソフトウェア センターに表示するのにアプリケーション カタログの役割は必要なくなりました。 この変更は、ユーザーにアプリケーションを配布するために必要なサーバー インフラストラクチャを減らすのに役立ちます。 ソフトウェア センターは、この情報を取得するために管理ポイントに依存するようになりました。より大規模な環境を、[境界グループ](../servers/deploy/configure/boundary-groups.md#management-points)に割り当てることでより適切にスケーリングすることができます。

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. サイトからアプリケーション カタログの役割をすべて削除します。 これらの役割には、アプリケーション カタログ Web サービス ポイントおよびアプリケーション カタログ Web サイト ポイントが含まれます。
2. 使用できるアプリケーションをユーザー コレクションに展開します。
3. 対象ユーザーとしてソフトウェア センターを使用して、アプリケーションの参照、要求、インストールを行います。

### <a name="known-issue"></a>既知の問題
- この機能で Azure Active Directory に参加しているクライアントを使用する場合は、サイトを **HTTP サイト システム用に Configuration Manager で生成された証明書を使用する**ように構成しないでください。 それは現在、この機能と競合しています。<!--515846--> この設定の詳細については、「[改善されたセキュアなクライアント通信](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)」を参照してください。



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>デバイス上のすべてのユーザーに対して Windows アプリ パッケージをプロビジョニングする
<!--1358310-->
デバイス上のすべてのユーザーに対して、Windows アプリ パッケージを含むアプリケーションをプロビジョニングできるようになりました。 このシナリオの 1 つの一般的な例では、ある学校の生徒が使用するすべてのデバイスに、Minecraft:Education Edition などの、ビジネス向け Microsoft Store および教育機関向け Microsoft Store からアプリをプロビジョニングします。 これまでは、Configuration Manager では、これらのアプリケーションのユーザーごとのインストールのみがサポートされていました。 新しいデバイスにサインインした後、学生はアプリにアクセスするまで待機する必要があります。 これからは、すべてのユーザー用のデバイスにアプリがプロビジョニングされている場合、より迅速に生産性を高めることができます。

> [!Important]  
> 予期しない結果になる場合があるため、1 つのデバイス上で同じ Windows アプリ パッケージの異なるバージョンのインストール、プロビジョニング、および更新を行う際には注意してください。 この動作は、Configuration Manager を使用してアプリをプロビジョニングするが、ユーザーに Microsoft Store からのアプリの更新を許可する場合に発生する可能性があります。 詳細については、[ビジネス向け Microsoft Store からアプリを管理する](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)場合の「次のステップ」のガイダンスを参照してください。  

オフライン ライセンス付きアプリをプロビジョニングする場合、Configuration Manager では、Windows での Microsoft Store からの自動更新は許可されません。  

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 試した結果の[フィードバック](capabilities-in-technical-preview-1804.md#bkmk_feedback)をお送りください。

1. 新しいアプリケーションを作成します。 このアプリは、Windows アプリケーション パッケージからのものであるか、あるいはビジネス向け Microsoft Store および教育機関向け Microsoft Store から同期した、オフライン ライセンス付きアプリである必要があります。  

2. アプリケーションの作成ウィザードの **[一般情報]** ページで、 **[Provision this application for all users on the device]\(このアプリケーションをデバイス上のすべてのユーザーにプロビジョニングする\)** というオプションを有効にします。  

   > [!Tip]  
   > 既存のアプリケーションを変更する場合、この設定はアプリケーション プロパティの **[ユーザー エクスペリエンス]** タブにあります。  

3. デバイス コレクションにアプリケーションを展開します。  

4. 別のユーザー アカウントで対象のデバイスにサインインして、アプリケーションを起動します。  

> [!Note]  
> ユーザーが既にサインオンしているデバイスからプロビジョニングされたアプリケーションをアンインストールする必要がある場合は、2 つのアンインストール展開を作成する必要があります。 1 つ目のアンインストール展開は、デバイスを含むデバイス コレクションを対象とします。 2 つ目のアンインストール展開は、アプリケーションがプロビジョニングされているデバイスに既にサインオンしているユーザーを含むユーザー コレクションを対象とします。 デバイスのプロビジョニングされているアプリをアンインストールしても、Windows では、現在、そのユーザーのアプリはアンインストールされません。 



## <a name="improvements-to-the-surface-dashboard"></a>Surface ダッシュボードの改善
<!--1358654-->
このリリースでは、[Surface ダッシュボード](../clients/manage/surface-device-dashboard.md)が次の点で改善されています。
- Surface ダッシュボードに、グラフ セクションが選択されたときに関連するデバイスのリストが表示されるようになりました。
   - **[Surface デバイスの割合]** タイルをクリックすると、Surface デバイスのリストが開きます。
   - **[上位 5 つのファームウェアのバージョン]** タイルのバーをクリックすると、その特定のファームウェアのバージョンを示す Surface デバイスのリストが開きます。
- Surface ダッシュボードからこれらのデバイス リストを表示した場合、デバイスを右クリックして、一般的な操作を実行できます。



## <a name="hardware-inventory-default-unit-revision"></a>ハードウェア インベントリの既定の単位のリビジョン
<!--514442-->
[Configuration Manager バージョン 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure) では、多くのレポート ビューで使用される既定の単位が、メガバイト (MB) からギガバイト (GB) に変更されました。 [より大きな整数値のハードウェア インベントリの機能強化](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)により、また、お客様からのフィードバックに基づき、この既定の単位が再度 MB になりました。



## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。    
