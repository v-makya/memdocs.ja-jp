---
title: バージョン 1902 の新機能
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch のバージョン 1902 で導入された変更点および新機能について説明します。
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f758456ad75c4acde1b050be75d653cc0e1dcfa1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700369"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch のバージョン 1902 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1902 はコンソール内の更新プログラムとして利用できます。 バージョン 1802、1806、1810 を実行しているサイトでこの更新プログラムを適用します。 <!-- baseline only statement:-->新しいサイトをインストールするときにも基準のバージョンとしても利用できます。 この記事では、Configuration Manager バージョン 1902 での変更点と新機能をまとめます。  

この更新プログラムをインストールするための最新のチェックリストを常に確認してください。 詳細については「[更新プログラム 1902 をインストールするためのチェックリスト](../../servers/manage/checklist-for-installing-update-1902.md)」を参照してください。 サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist)に関するページも確認してください。

Configuration Manager の新機能をすべて利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> このページが更新されたときに通知を受け取るには、次の URL をコピーして RSS フィード リーダーに貼り付けます。`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> 非推奨の機能とオペレーティング システム

[削除された項目と非推奨の項目](deprecated/removed-and-deprecated.md)で実装される前のサポートに関する変更点について説明します。

- Azure からコンテンツを共有するための実装が変更されました。 コンテンツが有効なクラウド管理ゲートウェイを使用します。その場合、 **[CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする]** オプションを有効にします。 今後は、従来のクラウド配布ポイントを作成できなくなります。

バージョン 1902 では、次の製品のサポートが廃止されます。  

- クライアントとしての Linux および UNIX。 廃止は[バージョン 1802](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support) で発表されました。 Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> サイトのインフラストラクチャ

### <a name="client-health-dashboard"></a>クライアントの正常性ダッシュボード

<!--3599209-->
ご利用の環境を保護するのに役立つ、ソフトウェア更新プログラムとその他のアプリをデプロイします。しかし、これらのデプロイで到達できるのは正常なクライアントのみです。 異常な Configuration Manager クライアントは、全体的なコンプライアンスに悪影響を及ぼします。 管理のスコープに含める必要があるデバイスの合計数など、分母によっては、クライアントの正常性の判断が困難な場合があります。 たとえば、Active Directory からすべてのシステムを検出した場合、それらのレコードの一部が使用を中止したコンピューターに対するものであっても、このプロセスによって分母が増加します。

環境内の Configuration Manager クライアントの正常性に関する情報を含むダッシュボードを表示できるようになりました。 クライアントの正常性、シナリオのヘルス、および一般的なエラーを表示します。 ビューをいくつかの属性でフィルター処理し、OS とクライアントのバージョンごとに潜在的な問題を表示します。

Configuration Manager コンソールで、 **[監視]** ワークスペースに移動します。 **[クライアント ステータス]** を展開し、 **[クライアントの正常性ダッシュボード]** ノードを選択します。

![クライアントの正常性ダッシュボードのスクリーンショット](media/3599209-client-health-dashboard.png)

詳細については、[クライアントを監視する方法](../../clients/manage/monitor-clients.md#bkmk_health)に関するページを参照してください。

### <a name="new-management-insight-rules"></a>新しい管理分析情報ルール

管理分析情報機能には、次の新しいルールがあります。

- コレクションの管理に関する複数のルールと推奨事項。 これらの分析情報を使用すると、管理を簡略化し、パフォーマンスを向上させることができます。 これらの新しいルールは **[コレクション]** グループで確認します。<!--3555752-->  

- **[単純化された管理]** グループの **[クライアントをサポート対象の Windows 10 バージョンに更新する]** ルール。 このルールでは、サポートされなくなった Windows 10 のバージョンを実行しているクライアントについて報告されます。 また、サービスの終了が近い (3 か月間) Windows 10 のバージョンを使用しているクライアントも含まれます。<!--3897268-->  

詳細については、[管理分析情報](../../servers/manage/management-insights.md)に関するページを参照してください。

### <a name="improvement-to-enhanced-http"></a>拡張 HTTP の改善

<!--3798957-->

拡張 HTTP をプライマリ サイトごとに、または中央管理サイトで有効にできるようになりました。

中央管理サイトのプロパティで、 **[HTTP サイト システムに Configuration Manager によって生成された証明書を使用します]** オプションを有効にします。 この設定は、中央管理サイトのサイト システムの役割にのみ適用されます。 階層のグローバル設定ではありません。

詳細については、「[拡張 HTTP](../hierarchy/enhanced-http.md)」を参照してください。

### <a name="improvement-to-setup-prerequisites"></a>セットアップの前提条件の機能強化

バージョン 1902 のインストールまたはバージョン 1902 への更新では、Configuration Manager のセットアップで次の前提条件チェックが追加されました。

- **リモート SQL Server でシステムの再起動が保留中です**: この前提条件チェックは、**保留中のシステム再起動**ルールに似ていますが、リモートの SQL Server がチェックされます。 詳細については、[前提条件の確認の一覧](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server)を参照してください。 <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> クラウド接続の管理

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>しきい値を超えたときにクラウド サービスを停止する

<!--3735092-->
Configuration Manager では、データ転送の合計が制限を超えたときに、クラウド管理ゲートウェイ (CMG) サービスを停止できるようになりました。 CMG では常に、使用量が警告レベルまたは重大レベルに達したときに通知をトリガーするために、アラートが表示されていました。 この新しいオプションではクラウド サービスを無効にすることができ、使用量の急増による予期しない Azure コストを削減するのに役立ちます。

詳細については、「[Stop CMG when it exceeds threshold (しきい値を超えた場合に CMG を停止する)](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop)」を参照してください。

### <a name="use-azure-resource-manager-for-cloud-services"></a>クラウド サービスに Azure Resource Manager を使用する

<!--3605704-->
バージョン 1810 以降では、Configuration Manager での Azure の従来のサービス展開の使用は非推奨になりました。 これらの Azure 展開の作成がサポートされるのは、そのバージョンが最後になります。

既存の展開は引き続き機能します。 この Current Branch バージョン以降、クラウド管理ゲートウェイとクラウド配布ポイントの新しいインスタンスに対しては、Azure Resource Manager が唯一の展開メカニズムです。

詳細については、[クラウド管理ゲートウェイに対する Azure Resource Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager) に関するページを参照してください。

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>クラウド管理ゲートウェイを境界グループに追加する

<!--3640932-->
クラウド管理ゲートウェイ (CMG) を境界グループに関連付けることができるようになりました。 クライアントにこの構成を使用すると、境界グループのリレーションシップに従って、クライアント通信に対して CMG を既定に設定したり、それにフォールバックしたりすることができます。 この動作は、ブランチ オフィスと VPN のシナリオで特に役立ちます。 クライアント トラフィックに高価で低速な WAN リンクを使用せず、代わりに Microsoft Azure への高速インターネット リンクを使用できます。

詳細については、[CMG 階層設計](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design)と [CMG の設定](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups)に関するページを参照してください。


## <a name="real-time-management"></a><a name="bkmk_real"></a> リアルタイムの管理

### <a name="run-cmpivot-from-the-central-administration-site"></a>中央管理サイトから CMPivot を実行する

<!--3610960-->
Configuration Manager で、階層内の中央管理サイトから CMPivot を実行できるようになりました。 まだ、プライマリ サイトでクライアントへの通信が処理されます。 中央管理サイトから CMPivot を実行するとき、高速メッセージ サブスクリプション チャネル経由でプライマリ サイトとの通信が行われます。 この通信では、サイト間の標準の SQL レプリケーションは利用されません。

詳細については、[リアルタイム データに対する CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1902) に関するページをご覧ください。

### <a name="edit-or-copy-powershell-scripts"></a>PowerShell スクリプトの編集またはコピー

<!--3705507-->
スクリプトの実行機能で使用される既存の PowerShell スクリプトを **[編集]** または **[コピー]** できるようになりました。 変更する必要があるスクリプトを再作成するのではなく、直接編集できるようになりました。 どちらのアクションでも、新しいスクリプトを作成するときと同じウィザード エクスペリエンスが使われます。 スクリプトを編集またはコピーするときに、Configuration Manager では承認状態が保持されません。

詳細については、「[スクリプトの実行](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit)」を参照してください。


## <a name="content-management"></a><a name="bkmk_content"></a> コンテンツ管理

### <a name="distribution-point-maintenance-mode"></a>配布ポイント メンテナンス モード

<!--3555754-->

メンテナンス モードで配布ポイントを設定できるようになりました。 ソフトウェア更新プログラムをインストールするとき、またはサーバーのハードウェアを変更するときに、メンテナンス モードを有効にします。

配布ポイントがメンテナンス モードの間の動作は、次のようになります。

- サイトからそれに対してコンテンツは何も配布されません。  

- 管理ポイントからクライアントに、この配布ポイントの場所は返されません。

- サイトを更新すると、メンテナンス モードの配布ポイントも更新されます。

- 配布ポイントのプロパティは読み取り専用です。 たとえば、証明書を変更したり、境界グループを追加したりすることはできません。  

- コンテンツの検証などのすべてのスケジュールされたタスクは、同じスケジュールで引き続き実行されます。

この機能の詳細については、[メンテナンス モード](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint)に関する記事を参照してください。

Configuration Manager SDK を使用してこのプロセスを自動化する方法の詳細については、[クラス SMS_DistributionPointInfo の SetDPMaintenanceMode メソッド](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md)に関する記事を参照してください。


## <a name="client-management"></a><a name="bkmk_client"></a> クライアント管理

### <a name="client-provisioning-mode-timeout"></a>クライアント プロビジョニング モードのタイムアウト

<!--3197824-->
タスク シーケンスでは、クライアントをプロビジョニング モードにするときに、タイムスタンプが設定されます。 プロビジョニング モードのクライアントでは、60 分ごとにタイムスタンプからの経過時間が確認されます。 48 時間より長くプロビジョニング モードになっている場合、クライアントは自動的にプロビジョニング モードを終了し、そのプロセスを再起動します。

詳細については、「[Provisioning mode (プロビジョニング モード)](../../../osd/understand/provisioning-mode.md)」を参照してください。

### <a name="view-first-screen-only-during-remote-control"></a>リモート制御中にのみ最初の画面を表示する

<!--3231732-->
2 台以上のモニターを使用してクライアントに接続すると、Configuration Manager リモート制御ビューアーでそのすべてを表示することが難しくなる可能性があります。 リモート ツール オペレーターでは、 **[すべての画面]** を表示するか **[最初の画面]** のみを表示するかを選択できるようになりました。

詳細については、「[Windows クライアント コンピューターをリモート管理する方法](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)」を参照してください。

### <a name="specify-a-custom-port-for-peer-wakeup"></a>ピア ウェイクアップ用のカスタム ポートを指定する

<!--3605925-->
ウェイクアップ プロキシ用のカスタム ポート番号を指定できるようになりました。 クライアント設定の **[電源管理]** グループで、 **[Wake On LAN ポート番号 (UDP)]** の設定を構成します。  

詳細については、[Wake On LAN を構成する方法](../../clients/deploy/configure-wake-on-lan.md)に関するページを参照してください。


## <a name="application-management"></a><a name="bkmk_app"></a> アプリケーション管理

### <a name="improvements-to-application-approvals-via-email"></a>電子メールを使用したアプリケーション承認の改善

<!--3594063-->
このバージョンには、アプリケーションの要求のメール通知を受信するための機能強化が含まれています。 ユーザーは、ソフトウェア センターから要求にコメントをいつでも追加することができます。 このコメントは、Configuration Manager コンソールのアプリケーションの要求に表示されます。 このコメントも電子メールに表示されるようになりました。 電子メールにこのコメントを含めると、承認者が要求を承認するか拒否するかをより適切に判断するのに役立ちます。

詳細については、[メール通知](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)に関する記事を参照してください。

### <a name="improvements-to-package-conversion-manager"></a>パッケージ変換マネージャーの改善

<!-- SCCMDocs-pr issue #3357 -->
このバージョンには、[パッケージ変換マネージャー](../../../apps/pcm/package-conversion-manager.md)に対する次の改善が含まれています。

- スケジュールされたパッケージの分析は、既定では 7 日ごとに実行されます
- パッケージを分析および変換するための PowerShell コマンドレット
- 一般的なバグ修正と改善


## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS の展開

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>インプレース アップグレード タスク シーケンスの進行状況

<!--3747129-->
Windows 10 のインプレース アップグレード タスク シーケンス中に表示される進行状況バーがより詳細になりました。 このバーには Windows セットアップの進行状況が表示され、それ以外の場合は、タスク シーケンス中に表示はされません。 ユーザーは下層で進行中の状況をある程度把握できるようになりました。 進行状況が表示されないためにアップグレード プロセスが中断しているのではないかという心配が解消されます。  

![Windows のアップグレードの進行状況に関するタスク シーケンスの進行状況の例](media/3747129-installation-progress.png)

この機能は、Windows 10 でサポートされるすべてのバージョンの、インプレース アップグレード タスク シーケンスでのみ動作します。

### <a name="improvements-to-task-sequence-media-creation"></a>タスク シーケンス メディアの作成の改善

<!--3556027, fka 1359388-->
このバージョンには、タスク シーケンス メディアの作成と管理が向上する複数の機能強化が含まれます。 詳細については、特定のメディアの種類に対する以下の記事を参照してください。

- [スタンドアロン メディアの作成](../../../osd/deploy-use/create-stand-alone-media.md)
- [事前設定されたメディアの作成](../../../osd/deploy-use/create-prestaged-media.md)
- [起動可能なメディアの作成](../../../osd/deploy-use/create-bootable-media.md)
- [キャプチャ メディアを作成する](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>一時記憶域を指定する

タスク シーケンス メディアを作成するときに、データの一時記憶域用にサイトが使用する場所をカスタマイズできるようになりました。 このプロセスでは、多くの一時ドライブの領域が必要になる場合があります。 この変更により、これらの一時ファイルを格納する場所をより柔軟に選択できるようになります。

**タスク シーケンス メディアの作成ウィザード**で、**ステージング フォルダー**の場所を指定します。 既定では、この場所は次のようなパスになります。`%UserProfile%\AppData\Local\Temp`

#### <a name="add-a-label-to-the-media"></a>メディアにラベルを追加する

タスク シーケンス メディアにラベルを追加できるようになりました。 このラベルは、作成したメディアを識別しやすくするのに役立ちます。 **タスク シーケンス メディアの作成ウィザード**で、**メディア ラベル**を指定します。

### <a name="import-a-single-index-of-an-os-image"></a>OS イメージの 1 つのインデックスをインポートする

<!--3719699-->
Configuration Manager に Windows イメージ (WIM) ファイルをインポートするとき、ファイル内のすべてのイメージ インデックスではなく、1 つのインデックスを自動的にインポートするよう指定できるようになりました。 このオプションには次のようなメリットがあります。

- より小さいイメージ ファイル  
- より速いオフライン サービス  
- イメージ サービスを最適化する (オフライン サービスの後に小さいイメージ ファイルに対して)

OS イメージをインポートするときに、 **[指定された WIM ファイルから特定のイメージ インデックスを抽出する]** オプションをオンにします。 その後、一覧からイメージのインデックスを選択します。  

詳細については、「[Add an OS image (OS イメージの追加)](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages)」を参照してください。

### <a name="optimized-image-servicing"></a>最適化されたイメージ サービス

<!--3555951-->
OS イメージにソフトウェア更新プログラムを適用するときに、置き換えられた更新プログラムを削除することによって出力を最適化するための新しいオプションがあります。 オフライン サービスに対する最適化は、単一インデックスのイメージにのみ適用されます。

OS イメージ更新スケジュールを作成するときに、 **[イメージが更新された後、置き換えられた更新プログラムを削除する]** オプションをオンにします。

詳しくは、「[ソフトウェア更新プログラムをイメージに適用](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase)」をご覧ください。

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>PowerShell スクリプトの実行タスク シーケンス ステップの改善

<!--3556028, fka 1359389-->
**PowerShell スクリプトの実行**タスク シーケンス ステップに次の機能強化が行われました。  

- このステップで、Windows PowerShell コードを直接入力できるようになりました。 この変更により、最初にスクリプトを使用してパッケージを作成して配布しなくても、タスク シーケンス中に PowerShell コマンドを実行することができます。

- **[Enter a PowerShell script]\(PowerShell スクリプトの入力\)** オプションを選択したときに、 **[スクリプトの編集]** を選択します。 新しい PowerShell スクリプト ウィンドウでは、次のアクションが提供されます。  

    - スクリプトを直接編集する  

    - ファイルから既存のスクリプトを開く  

    - Configuration Manager で既存の承認されたスクリプトを参照する

- スクリプトの出力をカスタム タスク シーケンス変数に保存します。  

- スクリプトのパラメーターをタスク シーケンス ログに含めるには、タスク シーケンス変数 **OSDLogPowerShellParameters** を **TRUE** に設定します。 既定では、ログ内にパラメーターはありません。  

- [[コマンド ラインの実行]](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) ステップと同様の機能を提供するその他の改善。 たとえば、代わりのユーザー資格情報を指定するか、またはタイムアウトを指定します。

> [!Important]  
> Configuration Manager のこの新機能を利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

詳細については、「[PowerShell スクリプトの実行](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)」を参照してください。

### <a name="other-improvements-to-os-deployment"></a>OS 展開のその他の機能強化

<!--3633146,3641475,3654172,3734270-->
このバージョンでは、OS の展開に関して次の機能強化が行われています。

- タスク シーケンスで **[ビュー]** に新しい既定のアクションがあります。 <!--3633146-->  

- タスク シーケンスのエラー ダイアログ ウィンドウに表示される詳細情報が追加されています。 失敗したタスク シーケンス ステップの名前が表示されます。 <!--3641475-->  

- **OSDDoNotLogCommand** タスク シーケンス変数を true に設定すると、ログ ファイルの "コマンド ラインの実行" ステップからのコマンド ラインも表示されなくなりました。 以前は、smsts.log の "パッケージのインストール" ステップからのプログラム名のみがマスクされました。<!--3654172-->  

- Windows 展開サービスのない配布ポイントで PXE レスポンダーを有効にするときは、DHCP サービスと同じサーバーでもかまわなくなりました。 <!--3734270--> 詳細については、「[PXE 要求を許可するために少なくとも 1 つの配布ポイントを構成する](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure)」を参照してください。


## <a name="software-center"></a><a name="bkmk_userxp"></a> ソフトウェア センター

### <a name="replace-toast-notifications-with-dialog-window"></a>ダイアログ ウィンドウでトースト通知を置き換える

<!--3555947-->
再起動や必須の展開に関する Windows のトースト通知が表示されないことがあります。 また、リマインダーを再通知するエクスペリエンスが表示されません。 クライアントが期限に達すると、この動作が原因でユーザー エクスペリエンスが低下する可能性があります。

展開で再起動が必要な場合、またはソフトウェアの変更が必要な場合、より頻繁に表示されるダイアログ ウィンドウを使用できるようになりました。

詳細については、[ソフトウェア センターの計画](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)に関するセクションを参照してください。

### <a name="configure-user-device-affinity-in-software-center"></a>ソフトウェア センターでのユーザーとデバイスのアフィニティの構成

<!--3485366-->
バージョン 1806 以降の[ソフトウェア センターのインフラストラクチャの改善](whats-new-in-version-1806.md#software-center-infrastructure-improvements)により、ほとんどのシナリオでアプリケーション カタログのサイト サーバーの役割が必要なくなりました。 ユーザーがユーザーとデバイスのアフィニティに自身のプライマリ デバイスを設定できるようにするため、一部のお客様は、引き続きアプリケーション カタログに依存します。

これでユーザーがソフトウェア センターで自身のプライマリ デバイスを設定できます。 この操作により、ユーザーが Configuration Manager 内のデバイスのプライマリ ユーザーになります。

詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。

### <a name="configure-default-views-in-software-center"></a>ソフトウェア センターで既定のビューを構成する

<!--3612112-->
このバージョンの Configuration Manager では、ソフトウェア センターのカスタマイズ方法が繰り返し使用されます。

- アプリケーションの既定レイアウトをタイル形式またはリスト形式で設定する  

    - ユーザーがこの構成を変更すると、ソフトウェア センターでは以降もユーザーの設定が保持されます。  

- 既定のアプリケーション フィルターをすべてのアプリまたは必要なアプリのみに設定する  

    - ソフトウェア センターでは常に既定の設定が使用されます。 ユーザーはこのフィルターを変更できますが、ソフトウェア センターではその設定が保持されません。

クライアント設定の **[ソフトウェア センター]** グループでこれらの設定を指定します。

詳細については、「[クライアント設定について](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults)」を参照してください。


## <a name="software-updates"></a><a name="bkmk_sum"></a> ソフトウェア更新プログラム

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Windows 10 サービスで機能更新プログラムの優先順位を指定する

<!--3734525-->
クライアントが [Windows 10 サービス](../../../osd/deploy-use/manage-windows-as-a-service.md)で機能更新プログラムをインストールする優先順位を調整します。 既定では、クライアントは処理優先順位の高い機能更新プログラムからインストールするようになりました。

クライアント設定を使用して、このオプションを構成します。 **[ソフトウェア更新プログラム]** グループで、次の設定を構成します: **[機能更新プログラムのスレッドの優先度を指定してください]** 。

詳細については、「[クライアント設定について](../../clients/deploy/about-client-settings.md#software-updates)」を参照してください。


## <a name="office-management"></a><a name="bkmk_o365"></a> Office 管理

### <a name="redirect-windows-known-folders-to-onedrive"></a>Windows の既知のフォルダーを OneDrive にリダイレクト

<!--3556021-->
Configuration Manager を使用して、Windows の既知のフォルダーを OneDrive for Business に移動します。 これらのフォルダーには、デスクトップ、ドキュメント、およびピクチャが含まれます。 Windows 10 へのアップグレードを簡単にするために、タスク シーケンスを展開する前にこれらの設定を Windows 7 クライアントに展開します。

OneDrive for Business のこの機能の詳細については、「[Windows の既知のフォルダーを OneDrive にリダイレクトして移動する](/onedrive/redirect-known-folders)」を参照してください。

最初に、[Office 365 テナント ID を確認します](/onedrive/find-your-office-365-tenant-id)。 次に、OneDrive 同期クライアント バージョン 18.111.0603.0004 以降を展開します。 詳細については、「[Configuration Manager を使用した OneDrive アプリの展開](/onedrive/deploy-on-windows)」を参照してください。  

OneDrive for Business プロファイルを作成して展開するには、Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動します。 **[コンプライアンス設定]** を展開し、 **[OneDrive for Business プロファイル]** ノードを選びます。  

詳細については、「[OneDrive for Business プロファイル](../../../compliance/deploy-use/onedrive-profile.md)」の記事の「Windows の既知のフォルダーを OneDrive にリダイレクト」セクションをご覧ください。

### <a name="integration-for-office-365-proplus-readiness"></a>Office 365 ProPlus の準備の統合

<!--3735402-->
Office 365 ProPlus へのアップグレードの準備ができている信頼性の高いデバイスを特定するには、Configuration Manager を使用します。 統合により、環境内で使用されている Office のアドインとマクロの潜在的な互換性の問題の分析情報が得られます。 そして、Configuration Manager を使用して Office を展開し、デバイスを準備します。

既存の Office 365 クライアント管理ダッシュボードに、 **[Office 365 ProPlus Upgrade Readiness]** という新しいタイルが追加されました。

詳細については、[Office 365 クライアント管理ダッシュボード](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness)に関するページをご覧ください。

### <a name="additional-languages-for-office-365-updates"></a>Office 365 更新プログラムの追加言語

<!--3555955-->
Office 365 クライアント更新プログラムでサポートされるすべての言語が Configuration Manager でサポートされるようになりました。 更新のワークフローでは、**Office 365 クライアント更新**での多数の言語に対して、**Windows Update** では 38 の言語に分割されています。

詳しくは、[Office 365 更新の管理](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang)に関するページをご覧ください。

### <a name="office-products-on-lifecycle-dashboard"></a>ライフサイクル ダッシュボードでの Office 製品

<!--3556026-->
製品ライフサイクル ダッシュボードに、Office 2003 から Office 2016 までのインストールされているバージョンに関する情報が含まれるようになりました。 サイトで 24 時間ごとのライフサイクル概要作成タスクが実行された後、データが表示されます。

詳細については、[製品ライフサイクル ダッシュボードの使用](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)に関するページを参照してください。


## <a name="phased-deployments"></a><a name="bkmk_pod"></a> 段階的展開

### <a name="dedicated-monitoring-for-phased-deployments"></a>段階的な展開に対する専用の監視

<!--3555949-->
段階的展開に専用の監視ノードが作成されました。 このノードを使用すると、作成した段階的展開を簡単に識別し、段階的展開の監視ビューに移動できます。 Configuration Manager コンソールで、 **[監視]** ワークスペースに移動して、 **[段階的な展開]** ノードを選択します。 段階的な展開の一覧が表示されます。

詳細については、[段階的な展開の監視ビュー](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor)に関する記事を参照してください。

### <a name="improvement-to-phased-deployment-success-criteria"></a>段階的な展開における成功の判断基準の強化

<!--3555946-->
段階的な展開におけるフェーズの成功の判断基準を追加します。 この基準を、割合だけでなく、展開が成功したデバイスの数とすることができるようになりました。 このオプションは、コレクションの数が変動し、次のフェーズに移る前に特定の数の成功したデバイスを示す必要がある場合に役立ちます。

タスク シーケンス、ソフトウェア更新プログラム、またはアプリケーションの段階的な展開を作成します。 その後、ウィザードの設定ページで、最初のフェーズの成功の基準として次のオプションを選択します。**正常に展開されたデバイスの数**。

詳しくは、「[段階的展開の作成](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)」をご覧ください。


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager コンソール

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a> Configuration Manager コンソールの機能拡張

<!--3594151-->
Midwest Management Summit (MMS) Desert Edition 2018 でのお客様のフィードバックに基づき、このバージョンには Configuration Manager コンソールに対する次の機能強化が含まれています。

- アプリケーション検出方法のレジストリ参照ウィンドウの最大化
- アプリケーションの展開からコレクションに移動
- 監視状態からコンテンツの削除
- **[監視]** ワークスペースの **[展開]** ノードの整数値によるビューの並べ替え
- 多数の結果に対する警告を移動

詳細については、[Configuration Manager コンソールのヒント](../../servers/manage/admin-console-tips.md)に関する記事を参照してください。

### <a name="configuration-manager-console-notifications"></a>Configuration Manager コンソールの通知

<!--3556016, fka 1318035-->
適切な対応ができるように十分な情報が得られるようにするため、Configuration Manager コンソールで次のイベントが通知されるようになりました。

- Configuration Manager 自体の更新プログラムが利用可能になったとき
- ライフサイクルおよびメンテナンス イベントが環境で発生したとき

この通知は、コンソール ウィンドウの上部のリボンの下のバーに表示されます。 これにより Configuration Manager の更新プログラムが利用可能になったときに、以前のエクスペリエンスが置き換えられます。 これらのコンソール内通知には引き続き重要な情報が表示されますが、コンソールでの作業には干渉しません。 重要な通知は消去できません。 コンソールのタイトル バーの新しい通知領域に、すべての通知が表示されます。

詳細については、「[Configuration Manager コンソールの通知](../../servers/manage/admin-console-notifications.md)」を参照してください。

### <a name="confirmation-of-console-feedback"></a>コンソール フィードバックの確認

<!--3556010-->
Configuration Manager コンソールで[フィードバック](../../understand/find-help.md#product-feedback)を送信するときに、確認メッセージが表示されるようになりました。 このメッセージに含まれる**フィードバック ID** を、追跡識別子として Microsoft に渡すことができます。

詳細については、「[製品に関するフィードバック](../../understand/find-help.md#bkmk_feedbackid)」を参照してください。

### <a name="view-recently-connected-consoles"></a>最近接続されたコンソールを表示する

<!--3699367-->
Configuration Manager コンソールの最新の接続を表示できるようになりました。 ビューには、アクティブな接続と最近接続されたコンソールが含まれます。 Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[セキュリティ]** を展開して **[コンソール接続]** ノードを選択します。

詳細については、「[Configuration Manager コンソールの使用](../../servers/manage/admin-console.md#bkmk_viewconnected)」を参照してください。

### <a name="in-console-documentation-dashboard"></a>コンソール内ドキュメント ダッシュボード

<!--3556019, fka 1357546-->
新しい **[コミュニティ]** ワークスペースには新しい **[ドキュメント]** ノードがあります。 このノードには、Configuration Manager のドキュメントとサポート記事に関する最新情報が含まれています。

詳細については、「[Configuration Manager コンソールの使用](../../servers/manage/admin-console.md#bkmk_doc-dashboard)」を参照してください。

### <a name="search-device-views-using-mac-address"></a>MAC アドレスを使用してデバイス ビューを検索する

<!--3600878-->
Configuration Manager コンソールのデバイス ビューで MAC アドレスを検索できるようになりました。 このプロパティは、OS の展開管理者が PXE ベースの展開のトラブルシューティングを行うときに役立ちます。 デバイスの一覧を表示するには、ビューに **[MAC アドレス]** 列を追加します。 検索フィールドを使用して、**MAC アドレス**の検索条件を追加します。

詳細については、[Configuration Manager コンソールのヒント](../../servers/manage/admin-console-tips.md)に関する記事を参照してください。

### <a name="use-net-47-for-improved-console-accessibility"></a>コンソールのユーザー補助機能向上のために .NET 4.7 を使用する

<!-- SCCMDocs-pr issue #3228 -->
Configuration Manager コンソールのユーザー補助機能向上のため、コンソールが実行されているコンピューターの .NET がバージョン 4.7 以降に更新されます。

詳細については、[Configuration Manager のユーザー補助機能](../../understand/accessibility-features.md)に関する記事を参照してください。

### <a name="changes-to-console-setup-process"></a>コンソールのセットアップ プロセスへの変更

<!-- 3612513 -->
Configuration Manager コンソールをインストールするときに必要となる新しいコンポーネントがあります。 他のコンピューターにコンソールをインストールするためのパッケージを作成する場合は、パッケージに次のファイルが含まれていることを確認します。

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

サイト サーバーをインストールまたは更新するときに、これらのインストール ファイル、およびサイト用にサポートされている言語パックが **Tools\ConsoleSetup** サブフォルダーにコピーされます。 詳細については、「[System Center Configuration Manager コンソールをインストールする](../../servers/deploy/install/install-consoles.md)」を参照してください。


## <a name="other-updates"></a>その他の更新内容

このリリースには、新機能に加え、バグ修正などの追加の変更も含まれています。 詳細については、「[Summary of changes in Configuration Manager current branch, version 1902 (Configuration Manager Current Branch バージョン 1902 での変更の概要)](https://support.microsoft.com/help/4498910)」をご覧ください。

Configuration Manager 向け Windows PowerShell コマンドレットの変更に関する詳細については、[PowerShell バージョン 1902 のリリース ノート](/powershell/sccm/1902-release-notes?view=sccm-ps)を参照してください。

2019 年 6 月 17 日以降、コンソールで次の更新プログラムのロールアップ (4500571) を利用できるようになりました: [Configuration Manager Current Branch バージョン 1902 の更新プログラムのロールアップ](https://support.microsoft.com/help/4500571)。

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>次のステップ

このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラムのインストール](../../servers/manage/updates.md)および[更新プログラム 1902 をインストールするためのチェックリスト](../../servers/manage/checklist-for-installing-update-1902.md)に関するページをご覧ください。

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用します。  
>
> 詳細については、下記のリンクをクリックしてください。    
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md)  
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)  

既知の重大な問題については、[リリース ノート](../../servers/deploy/install/release-notes.md)を参照してください。

サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist)に関するページも確認してください。