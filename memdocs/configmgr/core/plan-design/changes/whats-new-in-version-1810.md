---
title: バージョン 1810 の新機能
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch のバージョン 1810 で導入された変更点および新機能について説明します。
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6a9770dca209669659abf6e4fc9c23d5e6972981
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073553"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch のバージョン 1810 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1810 はコンソール内の更新プログラムとして利用できます。 バージョン 1710、1802、1806 を実行しているサイトでこの更新プログラムを適用します。 <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> この記事では、Configuration Manager バージョン 1810 での変更点と新機能をまとめます。  

この更新プログラムをインストールするための最新のチェックリストを常に確認してください。 詳細については「[更新プログラム 1810 をインストールするためのチェックリスト](../../servers/manage/checklist-for-installing-update-1810.md)」を参照してください。 サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist)に関するページも確認してください。

Configuration Manager の新機能を利用するには、最初にクライアントを最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> このページが更新されたときに通知を受け取るには、次の URL をコピーして RSS フィード リーダーに貼り付けます。`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> 非推奨の機能とオペレーティング システム

[削除された項目と非推奨の項目](deprecated/removed-and-deprecated.md)で実装される前のサポートに関する変更点について説明します。

2018 年 8 月 14 日以降、ハイブリッド モバイル デバイス管理機能は非推奨です。 詳細については、「[ハイブリッド MDM はどうなりましたか?](../../../mdm/understand/what-happened-to-hybrid.md)」を参照してください。<!--Intune feature 2683117-->  

Mac と Linux (すべてのバージョン) の System Center Endpoint Protection (SCEP) のサポートは 2018 年 12 月 31 日で終了します。 Mac 用の SCEP および Linux 用の SCEP の新しいウイルスの定義の可用性は、サポートの終了後に停止される可能性があります。 詳しくは、[サポートの終了ブログ投稿](https://go.microsoft.com/fwlink/?linkid=870182)をご覧ください。

Configuration Manager において Azure の従来のサービスのデプロイは非推奨です。 クラウド管理ゲートウェイおよびクラウド配布ポイント用の Azure Resource Manager の展開の使用を開始します。 詳細については、[CMG の計画](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)に関するページを参照してください。



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> サイトのインフラストラクチャ

### <a name="support-for-windows-server-2019"></a>Windows Server 2019 のサポート

<!--1359195-->
Configuration Manager は、サイト システムとして Windows Server 2019 と Windows Server バージョン 1809 をサポートするようになりました。

詳細については、[サイト システム サーバーでサポートされるオペレーティング システム](../configs/supported-operating-systems-for-site-system-servers.md)に関するページを参照してください。


### <a name="hierarchy-support-for-site-server-high-availability"></a>サイト サーバーの高可用性に対する階層のサポート

<!--3607755, fka 1358224-->
中央管理サイトと子プライマリ サイトでは、パッシブ モードで追加のサイト サーバーを使用できるようになりました。

詳細については、[サイト サーバーの高可用性](../../servers/deploy/configure/site-server-high-availability.md)に関するページを参照してください。


### <a name="improvements-to-setup-prerequisites"></a>セットアップの前提条件の機能強化

バージョン 1810 のインストールまたはバージョン 1810 への更新では、Configuration Manager のセットアップで次の前提条件チェックが追加または改良されました。

- **保留中のシステム再起動**:この前提条件チェックは回復性が強化されました。 Windows 機能の追加のレジストリ キーが確認されます。 詳しくは、「[保留中のシステムの再起動](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart)」をご覧ください。 <!--SCCMDocs-pr issue 3010-->  

- **SQL 変更追跡のクリーンアップ**:サイト データベースに SQL 変更追跡データのバックログがあるかどうかの新しい確認です。 このバックログの確認とクリーンアップの手順など、詳しくは、「[SQL 変更追跡のクリーンアップ](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking)」をご覧ください。 <!--SCCMDocs-pr issue 3023-->  

- **SQL Native Client バージョン**:この前提条件の確認は、TLS 1.2 をサポートする SQL Native Client のバージョン用に更新されています。 最小バージョンは [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402) です。 詳細については、[SQL Native Client バージョン](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)に関するトピックを参照してください。 <!--SCCMDocs-pr issue 3094-->  

- **Windows クラスター ノード上のサイト システム**:Configuration Manager の設定手順では、フェールオーバー クラスタリング用の Windows ロールで、コンピューターにサイト サーバー ロールがインストールされるのをブロックしなくなりました。 SQL Always On では、このロールが必要なため、以前はサイト サーバーにサイト データベースを同時に配置できませんでした。 この変更により、SQL Always On とパッシブ モードのサイト サーバーを使用して、少ないサーバー数で高可用性サイトを作成できます。 詳しくは、「[Windows フェールオーバー クラスター](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster)」をご覧ください。 <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>クライアント通知アクションの新しいアクセス許可

<!--SCCMDocs-pr issue #2972-->
クライアント通知アクションでは、SMS_Collection クラスに対する**リソースの通知**アクセス許可が必要になりました。 次の組み込みロールには、既定でこのアクセス許可があります。

- 完全な権限を持つ管理者  
- インフラストラクチャ管理者  

クライアント通知アクションを使用する必要があるカスタム ロールには、このアクセス許可を追加してください。

詳しくは、「[Client notifications](../../clients/manage/client-notification.md)」(クライアント通知) をご覧ください。



## <a name="content-management"></a><a name="bkmk_content"></a> コンテンツ管理

### <a name="new-boundary-group-options"></a>新しい境界グループのオプション

<!--1358749-->
境界グループに、環境内のコンテンツ配布をより細かく制御するための、以下の追加設定が含められました。

- **同じサブネット内のピアの配布ポイントより優先**:管理ポイントは、既定で、コンテンツの場所の一覧の最上位にピア キャッシュ ソースを順位付けします。 この設定は、ピア キャッシュ ソースと同じサブネット内にあるクライアントのその優先順位を入れ替えます。  

- **配布ポイントよりクラウドの配布ポイントを優先**:より高速なインターネット リンクが使用されている支店がある場合、クラウドのコンテンツを優先できるようになりました。  

詳細については、「[ピアのダウンロードの境界グループのオプション](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)」を参照してください。


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>ピア キャッシュ ソースのクライアントのバージョンに関するマネジメントの分析情報の規則

<!-- 1358008 -->
**[マネジメントの分析情報]** ノードには、ピア キャッシュ ソースとして機能しているにもかかわらず、1806 より前のクライアント バージョンからアップグレードされていないクライアントを識別するための、新しい規則があります。 新しい規則は **[ピア キャッシュのソースを、Configuration Manager クライアントの最新バージョンにアップグレードします]** であり、新しい **[プロアクティブ メンテナンス]** 規則グループに含まれます。 1806 より前のクライアントは、1806 以降のバージョンを実行するクライアントに対するピア キャッシュ ソースとして使用できません。 **[対応策を取る]** を選択して、クライアントの一覧が表示されるデバイス ビューを開きます。

詳細については、[管理分析情報](../../servers/manage/management-insights.md)に関するページを参照してください。



## <a name="client-management"></a><a name="bkmk_client"></a> クライアント管理

### <a name="new-client-notification-action-to-wake-up-device"></a>デバイスを復帰させる新しいクライアント通知アクション

<!--1317364-->
クライアントとサイト サーバーのサブネットが異なる場合でも、Configuration Manager コンソールからクライアントを復帰させることができるようになりました。 メンテナンスを実行したり、デバイスにクエリを実行したりする必要がある場合、スリープ状態にあるリモート クライアントで制限されることがありません。 サイト サーバーでは、クライアント通知チャネルを利用し、同じリモート サブネット上で起動状態にある別のクライアントが識別されます。 その後、復帰したクライアントは、Wake On LAN 要求 (マジック パケット) を送信します。

詳細については、[Wake On LAN の構成](../../clients/deploy/configure-wake-on-lan.md)に関するページと[クライアントをウェイク アップする方法](../../clients/deploy/plan/plan-wake-up-clients.md)に関するページを参照してください。

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>デバイス ノードからクライアント通知を実行する新しいオプション

<!--1317364-->
1810 まで、 **[クライアント通知]** オプションは、デバイス コレクション ノードから利用できるか、またはデバイス コレクションのメンバーシップを表示するときに利用できるだけでした。 **[デバイス]** ノードから **[クライアント通知]** を直接実行できるようになりました。 コレクション メンバーシップ ビュー内に要件は存在しなくなりました。

詳細については、[クライアント通知](../../clients/manage/client-notification.md)に関するページをご覧ください。


### <a name="improvements-to-collection-evaluation"></a>コレクションの評価の機能強化

<!--3607726, fka 1358981-->
コレクションの評価の動作における次の変更により、サイトのパフォーマンスが向上します。  

- 以前は、クエリ ベースのコレクションでスケジュールを構成すると、コレクションの設定 **[このコレクションの完全な更新をスケジュールする]** が有効かどうかにかかわらず、サイトではクエリの評価が続けられました。 スケジュールを完全に無効にするには、スケジュールを **[なし]** に変更する必要がありました。 現在は、この設定を無効にすると、サイトはスケジュールをクリアします。 コレクション評価のスケジュールを指定するには、オプション **[このコレクションの完全な更新をスケジュールする]** を有効にします。  

- **すべてのシステム**のような組み込みコレクションの評価を無効にすることはできませんが、スケジュールを構成できるようになりました。 この動作により、ビジネス要件を満たしているときはこの操作をカスタマイズできます。

詳しくは、「[コレクションを作成する方法](../../clients/manage/collections/create-collections.md#bkmk_create)」をご覧ください。


### <a name="improvement-to-client-installation"></a>クライアント インストールの改善

<!--1358840-->
構成マネージャー クライアントをインストールするとき、ccmsetup プロセスにより管理ポイントが接触され、必要なコンテンツが検索されます。 このプロセスでは以前、管理ポイントは、クライアントの現在の境界グループにある配布ポイントが返されるだけでした。 コンテンツが利用できない場合、セットアップ プロセスはフォールバックし、管理ポイントからコンテンツをダウンロードします。 必要なコンテンツがあるかもしれない他の境界グループにある配布ポイントにフォールバックするオプションはありません。 今回、管理ポイントにより境界グループの構成に基づいて配布ポイントが返されるようになりました。

詳細については、[境界グループの構成](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)に関するページを参照してください。



## <a name="co-management"></a><a name="bkmk_comgmt"></a> 共同管理

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>共同管理デバイスに必要なアプリ コンプライアンス ポリシー

<!--1358196-->
必要なアプリケーションに対して、Configuration Manager でコンプライアンス ポリシー ルールを定義します。 このアプリ評価は、共同管理デバイスについて Microsoft Intune に送信される全体的コンプライアンス状態に含まれます。

詳細については、「[共同管理ワークロード](../../../comanage/workloads.md)」を参照してください。


### <a name="improvement-to-co-management-dashboard"></a>共同管理ダッシュボードの改善

<!--1358980-->
共同管理ダッシュボードが機能強化され、以下の情報がさらに詳しくなりました。  

- **[共同管理の登録ステータス]** タイルに状態が追加されました

- 新しい **[共同管理の状態]** タイルにはじょうごグラフが付き、登録プロセスの状態が表示されます

- **登録エラー**のカウントが付いた新しいタイル

![共同管理ダッシュボードのスクリーンショット。上の 4 つのタイルを確認できます。](media/1358980-comgmt-dashboard.png)

詳しくは、「[共同管理ダッシュボード](../../../comanage/how-to-monitor.md#co-management-dashboard)」をご覧ください。


### <a name="improvements-to-internet-based-client-setup"></a>インターネット ベースのクライアント セットアップの機能強化

<!--3607731, fka 1359181-->
このリリースでは、インターネット上のクライアントに対する Configuration Manager のクライアント セットアップ プロセスがさらに簡単になります。 サイトでは、クラウド管理ゲートウェイ (CMG) に対して Azure Active Directory (Azure AD) の追加情報が公開されます。 Azure AD に参加しているクライアントは、ccmsetup プロセスの間に、参加している同じテナントを使用して、CMG からこの情報を取得します。 この動作により、複数の Azure AD テナントがある環境での共同管理に対するデバイスの登録がさらに簡略化されます。 必要な ccmsetup プロパティは、**CCMHOSTNAME** と **SMSSiteCode** の 2 つだけになります。

詳細については、「[How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)」 (共同管理用にインターネット ベースのデバイスを準備する方法) を参照してください。



## <a name="application-management"></a><a name="bkmk_app"></a> アプリケーション管理

### <a name="convert-applications-to-msix"></a>アプリケーションを MSIX に変換する

<!--3607729, fka 1359029-->
バージョン 1806 以降の Configuration Manager では、Windows 10 の新しいアプリ パッケージ (.msix) 形式の展開がサポートされています。 既存の Windows インストーラー (.msi) アプリケーションを MSIX 形式に変換できるようになりました。

詳しくは、「[Windows アプリケーションを作成する](../../../apps/get-started/creating-windows-applications.md#bkmk_msix)」をご覧ください。  


### <a name="repair-applications"></a>アプリケーションの修復

<!--1357866-->
Windows インストーラーおよびスクリプト インストーラーの展開の種類で、修復コマンド ラインを指定します。 その後、展開でオプションを有効にすると、ソフトウェア センターでアプリケーションを**修復**するための新しいボタンを使用できます。 修復プログラムでアプリケーションを構成するときに、ユーザーはソフトウェア センターからコマンドを開始できます。

詳しくは、「[アプリケーションの作成](../../../apps/deploy-use/create-applications.md#bkmk_dt-content)」と「[アプリケーションの展開](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)」をご覧ください。


### <a name="approve-application-requests-via-email"></a>電子メールでアプリケーション要求を承認する

<!--1321550-->
アプリケーションの承認を要求する電子メール通知を構成します。 ユーザーがアプリケーションを要求すると、管理者はメールを受け取ります。 メールのリンクをクリックして、要求を承認または拒否できます。Configuration Manager コンソールは必要ありません。

詳しくは、「[Approve applications](../../../apps/deploy-use/app-approval.md)」(アプリケーションの承認) をご覧ください。


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>検出方法で Windows PowerShell プロファイルを読み込まない

<!--3607762, fka 1359239-->
構成項目のアプリケーションと設定で検出方法に対して Windows PowerShell スクリプトを使用できます。 これらのスクリプトがクライアントで実行されるとき、Configuration Manager クライアントが `-NoProfile` パラメーターで PowerShell を呼び出すようになりました。 このオプションでは、プロファイルなしで PowerShell が起動されます。

PowerShell プロファイルは、PowerShell の開始時に実行されるスクリプトです。 PowerShell プロファイルを作成して、環境をカスタマイズし、開始するすべての PowerShell セッションにセッション固有の要素を追加できます。

> [!Note]  
> この動作の変更は、[スクリプト](../../../apps/deploy-use/create-deploy-scripts.md)または [CMPivot](../../servers/manage/cmpivot.md) には適用されません。 これらの機能はどちらも既にこの PowerShell パラメーターを使用しています。  

詳細については、[アプリケーションの作成](../../../apps/deploy-use/create-applications.md)と[カスタム構成項目の作成](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)に関する記事を参照してください。



## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS の展開

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>既存デバイス向けの Windows Autopilot のタスク シーケンスのサポート

<!--3607717, fka 1358333-->
[既存デバイス向けの Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) を、Windows 10 バージョン 1809 以降で利用できるようになりました。 この新しい機能を使用すると、単一のネイティブな Configuration Manager タスク シーケンスを使用して、[Windows Autopilot ユーザー駆動モード](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven)用に Windows 7 デバイスを再イメージ化およびプロビジョニングできます。

詳細については、「[Windows Autopilot for existing devices](../../../osd/deploy-use/windows-autopilot-for-existing-devices.md)」 (既存のデバイス向け Windows Autopilot) を参照してください。


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>オフライン OS イメージ サービス用のドライブを指定する

<!--1358924-->
OS イメージおよび OS アップグレード パッケージにソフトウェア更新プログラムを追加するときに、Configuration Manager が使用するドライブを指定するようになりました。 このプロセスでは一時ファイルによって大量のディスク領域が使用される可能性があり、このオプションでは使用するドライブを柔軟に選択できます。

詳しくは、「[OS イメージの管理](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive)」および「[OS アップグレード パッケージの管理](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive)」をご覧ください。


### <a name="task-sequence-support-for-boundary-groups"></a>境界グループのタスク シーケンス サポート

<!--1359025-->
デバイスでタスク シーケンスが実行され、コンテンツを取得する必要があるとき、構成マネージャー クライアントに似た境界グループの動作が使用されるようになりました。

詳細については、「[境界グループ](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd)」を参照してください。


### <a name="improvements-to-driver-maintenance"></a>ドライバーのメンテナンスの機能強化

<!--3607716, fka 1358270-->
ドライバー パッケージに、**製造元**と**モデル**のメタデータ フィールドが追加されました。 これらのフィールドを使用して、一般的なハウスキーピングに役立つ情報、または削除できる古くて重複するドライバーを識別する情報で、ドライバー パッケージにタグを付けます。

詳細については、「[Manage drivers](../../../osd/get-started/manage-drivers.md)」(ドライバーの管理) を参照してください。

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Windows 10 サービス プラン フィルターの機能強化

<!--3098809, 3113836, 3204570 -->
Windows 10 サービス プランに追加のフィルターが追加されました。 **[アーキテクチャ]** 、 **[製品カテゴリ]** 、およびアップグレードが **[優先]** かどうかでフィルター処理できるようになりました。

詳細については、「[Windows 10 サービス プラン](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan)」をご覧ください。

### <a name="new-task-sequence-variable-for-last-action-name"></a>最後のアクション名に対する新しいタスク シーケンス変数

<!--SCCMDocs-pr issue #2964-->
タスク シーケンス変数 _SMSTSLastActionRetCode と共に、タスク シーケンスでは新しい変数 **_SMSTSLastActionName** も設定されます。 また、この値は smsts.log ファイルに記録されます。 この新しい変数は、タスク シーケンスのトラブルシューティングを行うときに役立ちます。 ステップが失敗した場合、カスタム スクリプトにリターン コードと共にステップ名を含めることができます。

詳しくは、「[タスク シーケンス変数](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName)」をご覧ください。



## <a name="software-updates"></a><a name="bkmk_sum"></a> ソフトウェア更新プログラム

### <a name="phased-deployment-of-software-updates"></a>ソフトウェア更新プログラムの段階的展開

<!--1358146-->
ソフトウェア更新プログラムの段階的な展開を作成します。 段階的な展開を使用すると、カスタマイズ可能な条件およびグループに基づいて、調整およびシーケンス化されたソフトウェアの展開をまとめることができます。

詳しくは、「[段階的展開の作成](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)」をご覧ください。


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>ソフトウェア更新プログラムのメンテナンス期間の改善

<!--vso2839307-->
メンテナンス期間におけるソフトウェア更新プログラムのインストール動作を制御するための次のクライアント設定が、 **[ソフトウェア更新プログラム]** グループにあります。 **[Enable installation of updates in "All deployments" maintenance window when "Software update" maintenance window is available]\([ソフトウェア更新プログラム] のメンテナンス期間が利用可能な場合、[すべての展開] のメンテナンス期間の更新プログラムのインストールを有効にします\)**

既存の動作と一貫性を保つため、このオプションは既定で **[いいえ]** に設定されています。 **[はい]** に変更すると、クライアントが他の利用可能なメンテナンス期間を使用して、ソフトウェア更新プログラムをインストールできるようになります。

詳細については、[ソフトウェア更新プログラムのクライアント設定](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint)に関する記事をご覧ください。


### <a name="improvement-to-software-updates-maintenance"></a>ソフトウェア更新プログラムのメンテナンスの強化

<!--2839349-->
WSUS クリーンアップ タスクがセカンダリ サイトで実行されるようになりました。 有効期限が切れた更新プログラムの WSUS クリーンアップが実行され、WSUS で置き換えられた更新プログラムはセカンダリ サイトで拒否されます。

詳細については、「[バージョン 1810 以降の WSUS クリーンアップ動作](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)」を参照してください

### <a name="improvement-to-software-update-supersedence-rules"></a>ソフトウェア更新プログラムの置き換え規則の機能強化

<!--3098809, 2977644-->
機能の更新プログラム用の置き換え規則を、機能以外の更新プログラムとは別に指定できるようになりました。 つまり、Windows 10 クライアントのサービスが完了する前に Configuration Manager からアップグレードが削除されることはありません。

詳細については、「 [置き換え規則](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules)」を参照してください。

## <a name="reporting"></a><a name="bkmk_report"></a> レポート

### <a name="improvement-to-lifecycle-dashboard"></a>ライフサイクル ダッシュボードの改善

<!--1358702-->
製品ライフサイクル ダッシュボードに、**System Center 2012 Configuration Manager 以降**の情報が含まれるようになりました。

また、新しいレポート**ライフサイクル 05A - 製品ライフサイクル ダッシュボード**があります。 コンソール内のダッシュボードと同様の情報が含まれます。

このダッシュボードの詳細については、[製品ライフサイクル ダッシュボードの使用](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)に関するページを参照してください。


### <a name="improvement-to-data-warehouse"></a>データ ウェアハウスの機能強化

<!--1358870-->
サイト データベースからより多くのテーブルをデータ ウェアハウスに同期できるようになりました。 この変更により、お客様のビジネス要件に基づいてより多くのレポートを作成することができます。

詳細については、「[データ ウェアハウス](../../servers/manage/data-warehouse.md)」を参照してください。



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager コンソール

### <a name="configuration-manager-administrator-authentication"></a>Configuration Manager 管理者の認証

<!--1357013-->
Configuration Manager サイトにアクセスする管理者の最低限の認証レベルを指定できるようになりました。 この機能では、Windows にサインインする管理者には必要なレベルを持つことが強制されます。 この設定は、 **[階層設定]** の **[認証]** タブで構成します。

詳細については、「[SMS プロバイダーの計画](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)」を参照してください。


### <a name="support-center"></a>サポート センター

<!--1357489-->
クライアントの問題を解決する場合、リアルタイムのログを表示する場合、または後で分析するために Configuration Manager クライアント コンピューターの状態をキャプチャする場合は、サポート センターを使用します。 サポート センターは、多くの管理者用トラブルシューティング ツールを結合する 1 つのツールです。 サイト サーバー上の **cd.latest\SMSSETUP\Tools\SupportCenter** フォルダー内にあるサポート センターのインストーラーを探します。

詳しくは、「[Support Center](../../support/support-center.md)」(サポート センター) をご覧ください。


### <a name="management-insights-dashboard"></a>管理分析情報ダッシュボード

<!--1357979-->
**管理分析情報**ノードにグラフィック ダッシュボードが追加されました。 このダッシュボードにはルールの状態の概要が表示されるので、進捗状況を簡単に表示できます。 ダッシュボードには次のタイルが含まれています。

- **管理分析情報インデックス**:管理分析情報ルールの全体的進捗状況を追跡記録します。 インデックスは加重平均です。 クリティカル ルールが最も重要です。 このインデックスは、任意のルールに最も軽い重みを与えます。  

- **管理分析情報グループ**:各グループのルールがパーセント表示されます。  

- **管理分析情報の優先順位**:優先順位別のルールがパーセント表示されます。  

- **すべての分析情報**:優先順位と状態を含む、分析情報のテーブル。  

![管理分析情報ダッシュボードのスクリーンショット](media/1357979-management-insights-dashboard.png)

詳細については、[管理分析情報](../../servers/manage/management-insights.md)に関するページを参照してください。


### <a name="improvements-to-cmpivot"></a>CMPivot の改善

<!--1359068-->
CMPivot には次の改善が含まれています。

- **お気に入り**クエリの保存  

- [クエリ概要] タブで、エラーが発生したデバイスまたはオフラインのデバイスを選択し、**コレクションを作成する**オプションを選択します。

CMPivot のパフォーマンスとトラブルシューティングの改善の詳細については、「[スクリプトの改善](#bkmk_scripts)」を参照してください。

CMPivot の詳細については、[CMPivot](../../servers/manage/cmpivot.md) に関するページを参照してください。


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a> スクリプトの改善

<!--1358239-->
詳細なスクリプトの出力を、手が加えられていない形式または構造化された JSON 形式で表示できるようになりました。 この書式設定を行うと、出力の読み取りと分析が容易になります。

CMPivot とスクリプトの両方に、次のパフォーマンス改善とトラブルシューティング改善が適用されます。

- 更新後のクライアントでは、高速の通信チャネルでサイトに 80 KB 未満の出力が返されます。 この変更により、スクリプトまたはクエリの出力を表示するパフォーマンスが上がります。  

- トラブルシューティングのための追加のログ  

詳細については、以下の記事を参照してください。  

- [Configuration Manager コンソールから PowerShell スクリプトを作成して実行する](../../../apps/deploy-use/create-deploy-scripts.md)  

- [CMPivot のトラブルシューティング](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>SMS プロバイダー API

<!--3607711, fka 1321523-->
SMS プロバイダーで、WMI over HTTPS に対する読み取り専用の API 相互運用性アクセスが提供されるようになりました (**管理サービス**と呼ばれます)。 この REST API をカスタム Web サービスの代わりに使って、サイトからの情報にアクセスできます。

**SMS プロバイダー**は、クラウド管理ゲートウェイ経由で通信できるオプションを持つロールとして表示されます。 この設定の現在の用途は、リモート デバイスからメール経由でアプリケーションを承認できるようにすることです。

詳細については、「[SMS プロバイダーの計画](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)」を参照してください。



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> オンプレミス MDM

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>新しいオンプレミスの MDM 展開に Intune 接続は不要になった

<!--1359124-->
新しい展開では、Microsoft Intune サブスクリプションを構成するというオンプレミス MDM の前提条件は必要なくなりました。 組織では、この機能を使用するにはまだ Intune ライセンスが必要です。 現時点では、既存のオンプレミスの MDM 展開から Intune 接続を削除することはできません。 詳細については、[Intune サポートのブログ投稿](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)をご覧ください。



## <a name="other-updates"></a>その他の更新内容

このリリースには、新機能に加え、バグ修正などの追加の変更も含まれています。 詳細については、「[Summary of changes in Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4482169)」(Configuration Manager Current Branch バージョン 1810 での変更の概要) をご覧ください。

Configuration Manager 向け Windows PowerShell コマンドレットの変更に関する詳細については、[PowerShell バージョン 1810 のリリース ノート](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps)を参照してください。

2019 年 3 月 25 日以降、コンソールで次の更新プログラムのロールアップ (4488598) を利用できるようになりました: [Configuration Manager Current Branch バージョン 1810 の更新プログラムのロールアップ 2](https://support.microsoft.com/help/4488598)。 これは、以前の更新プログラムのロールアップ KB 4486457 に代わるものです。


### <a name="hotfixes"></a>修正プログラム

次の追加の修正プログラムは、特定の問題を解決するために利用できます。

| ID | タイトル | 日付 | コンソール内 |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune のコネクタ証明書が Configuration Manager で更新されない | 2019 年 1 月 18 日 | はい |
| [4490434](https://support.microsoft.com/help/4490434) | Configuration Manager でユーザーの探索列が重複して作成される | 2019 年 2 月 22 日 | はい |
| [4490575](https://support.microsoft.com/help/4490575) | Configuration Manager バージョン 1810 で、更新プログラムのインストールが応答しないまたは完了が表示されない | 2019 年 2 月 22 日 | はい |


## <a name="next-steps"></a>次のステップ

このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラムのインストール](../../servers/manage/updates.md)および[更新プログラム 1810 をインストールするためのチェックリスト](../../servers/manage/checklist-for-installing-update-1810.md)に関するページをご覧ください。

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用します。  
>
> 詳細については、下記のリンクをクリックしてください。
>
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md)  
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)  

既知の重大な問題については、[リリース ノート](../../servers/deploy/install/release-notes.md)を参照してください。

サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist)に関するページも確認してください。
