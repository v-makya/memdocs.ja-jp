---
title: ログ ファイルのリファレンス
titleSuffix: Configuration Manager
description: Configuration Manager のクライアント、サーバー、および依存コンポーネントのすべてのログ ファイルのリファレンス。
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f8ad6827a1aa72c3aaa51e21fecbf639fbb405
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715579"
---
# <a name="log-file-reference"></a>ログ ファイルのリファレンス

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、クライアント コンポーネントとサイト サーバー コンポーネントによって、処理情報が個々のログ ファイルに記録されます。 ログに記録された情報を、発生した問題を解決するときの参考にしてください。 既定では、Configuration Manager ではクライアント コンポーネントとサーバー コンポーネントのログ記録が有効になっています。

Configuration Manager のログ ファイルに関するより一般的な情報については、「[ログ ファイルについて](about-log-files.md)」を参照してください。 この記事には、使用するツール、ログの構成方法、およびその検索場所に関する情報が含まれています。

次のセクションに、各ログ ファイルの説明を示します。 操作の詳細に関する Configuration Manager のクライアントとサーバーのログを監視し、エラーの情報を表示して問題のトラブルシューティングを行います。  

- [クライアント ログ ファイル](#BKMK_ClientLogs)  

  - [クライアントによる処理](#BKMK_ClientOpLogs)  

  - [クライアントのインストール](#BKMK_ClientInstallLog)  

  - [Linux および UNIX 用のクライアント](#BKMK_LogFilesforLnU)  

  - [Mac コンピューター用のクライアント](#BKMK_LogfilesforMac)  

- [サーバー ログ ファイル](#BKMK_ServerLogs)  

  - [サイト サーバーとサイト システム](#BKMK_SiteSiteServerLog)  

  - [サイト サーバーのインストール](#BKMK_SiteInstallLog)

  - [データ ウェアハウス サービス ポイント](#BKMK_DataWarehouse)

  - [フォールバック ステータス ポイント](#BKMK_FSPLog)  

  - [管理ポイント](#BKMK_MPLog)  

  - [サービス接続ポイント](#BKMK_WITLog)  

  - [ソフトウェアの更新ポイント](#BKMK_SUPLog)  

- [機能別ログ ファイル](#BKMK_FunctionLogs)  

  - [アプリケーション管理](#BKMK_AppManageLog)  

  - [資産インテリジェンス](#BKMK_AILog)  

  - [バックアップと回復](#BKMK_BnRLog)  

  - [証明書の登録](#BKMK_CertificateEnrollment)

  - [クライアント通知](#BKMK_BGB)

  - [クラウド管理ゲートウェイ](#cloud-management-gateway)

  - [コンプライアンス設定と会社のリソースへのアクセス](#BKMK_CompSettingsLog)  

  - [Configuration Manager コンソール](#BKMK_ConsoleLog)  

  - [コンテンツ管理](#BKMK_ContentLog)  

  - [Desktop Analytics](#desktop-analytics)

  - [探索](#BKMK_DiscoveryLog)  

  - [Endpoint Protection](#BKMK_EPLog)  

  - [拡張機能](#BKMK_Extensions)  

  - [インベントリ](#BKMK_InventoryLog)  

  - [移行](#BKMK_MigrationLog)  

  - [モバイル デバイス](#BKMK_MDMLog)  

  - [OS の展開](#BKMK_OSDLog)  

  - [電源管理](#BKMK_PowerMgmtLog)  

  - [リモート コントロール](#BKMK_RCLog)  

  - [レポート](#BKMK_ReportLog)  

  - [役割に基づいた管理](#BKMK_RBALog)  

  - [ソフトウェア使用状況測定](#BKMK_MeteringLog)  

  - [ソフトウェア更新プログラム](#BKMK_SU_NAPLog)  

  - [Wake On LAN](#BKMK_WOLLog)  

  - [Windows 10 サービス](#BKMK_WindowsServicingLog)

  - [Windows 更新エージェント](#BKMK_WULog)  

  - [WSUS サーバー](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a> クライアント ログ ファイル

次のセクションでは、クライアントによる処理が記録されるログ ファイルと、クライアントのインストール時に記録されるログ ファイルについて説明します。  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a> クライアントによる処理

次の表に、Configuration Manager クライアントにあるログ ファイルを示します。  

|ログの名前|[説明]|  
|--------------|-----------------|  
|ADALOperationProvider.log|Azure Active Directory (Azure AD) Authentication Library (ADAL) を使用したクライアント認証トークン要求に関する情報。|
|BitLockerManagementHandler.log|BitLocker 管理ポリシーに関する情報を記録します。|
|CAS.log|コンテンツ アクセス サービス。 クライアントのローカル パッケージのキャッシュを管理します。|  
|Ccm32BitLauncher.log|クライアントにある *run as 32 bit* とマークされたアプリケーションの起動を記録します。|  
|CcmEval.log|Configuration Manager クライアント ステータスを評価するときの処理と、Configuration Manager クライアントが必要とするコンポーネントの詳細を記録します。|  
|CcmEvalTask.log|スケジュールに従って開始される Configuration Manager クライアント ステータスの評価に関する処理を記録します。|  
|CcmExec.log|クライアントと SMS Agent Host サービスによって行われる処理を記録します。 ウェイクアップ プロキシの有効化と無効化に関する情報も記録します。|  
|CcmMessaging.log|クライアントと管理ポイント間の通信に関連する処理を記録します。|  
|CCMNotificationAgent.log|クライアント通知操作に関連する処理を記録します。|  
|Ccmperf.log|メンテナンス操作、およびクライアントのパフォーマンス カウンターに関連するデータの取得操作を記録します。|  
|CcmRestart.log|クライアント サービスの再開を記録します。|  
|CCMSDKProvider.log|クライアントの SDK インターフェイスで行われる処理を記録します。|  
|ccmsqlce.log|クライアントに使用される SQL Compact Edition のアクティビティを記録します。 このログは、通常、デバッグ ログを有効にする場合またはコンポーネントに問題がある場合にのみ使用されます。 通常、クライアント正常性タスク (ccmeval) によってこのコンポーネントの問題は自己修正されます。|
|CertificateMaintenance.log|Active Directory ドメイン サービスと管理ポイントの証明書を管理するときに使用します。|  
|CIDownloader.log|構成項目の定義のダウンロードの詳細を記録します。|  
|CITaskMgr.log|コンテンツのダウンロードとインストールや、アンインストール アクションなど、アプリケーションと展開の種類ごとにタスクを記録します。|  
|ClientAuth.log|クライアントの署名と認証処理を記録します。|  
|ClientIDManagerStartup.log|クライアント GUID を作成して維持し、クライアントの登録および割り当て時にタスクを識別します。|  
|ClientLocation.log|クライアント サイトの割り当てに関連する操作を記録します。|  
|CMHttpsReadiness.log|Configuration Manager の HTTPS 使用準備ができているかどうかを評価するツールの実行結果を記録します。 このツールは、Configuration Manager で使用できる公開キー基盤 (PKI) クライアント認証証明書がコンピューターにあるかどうかをチェックします。|  
|CmRcService.log|リモート コントロール サービスの情報を記録します。|  
|CoManagementHandler.log|クライアント上での共同管理をトラブルシューティングするために使用します。|
|ContentTransferManager.log|バックグラウンド インテリジェント転送サービス (BITS)、またはサーバー メッセージ ブロック (SMB) でパッケージをダウンロード、またはパッケージにアクセスするスケジュールの情報を含みます。|  
|DataTransferService.log|ポリシーまたはパッケージにアクセスするために行われた、BITS による通信をすべて記録します。|  
|DeltaDownload.log|配信の最適化を使用してダウンロードされた高速更新プログラムと更新プログラムのダウンロードに関する情報が記録されます。|  
|Diagnostics.log|クライアント診断操作の状態を記録します。|
|EndpointProtectionAgent|System Center Endpoint Protection クライアントのインストール、およびそのクライアントへのマルウェア対策ポリシーの適用に関する情報を記録します。|  
|execmgr.log|クライアントで実行されたパッケージとタスク シーケンスの詳細を記録します。|  
|ExpressionSolver.log|"詳細" または "デバッグ" レベルのログ記録が有効になっているときに使用される検出方法の詳細を記録します。|  
|ExternalEventAgent.log|Endpoint Protection のマルウェア検出とクライアント ステータスに関連するイベントの履歴を記録します。|  
|FileBITS.log|SMB によるパッケージへのアクセスをすべて記録します。|  
|FileSystemFile.log|Windows Management Instrumentation (WMI) プロバイダーによって行われるソフトウェア インベントリとファイルの収集処理を記録します。|  
|FSPStateMessage.log|クライアントによってフォールバック ステータス ポイントに送信されるステータス メッセージを記録します。|  
|InternetProxy.log|クライアントのネットワーク プロキシの構成と使用状況を記録します。|  
|InventoryAgent.log|クライアントで行われるハードウェア インベントリ、ソフトウェア インベントリ、定期探索を記録します。|  
|LocationCache.log|クライアントの位置情報のキャッシュの使用状況とメンテナンス情報を記録します。|  
|LocationServices.log|クライアントで管理ポイント、ソフトウェア更新ポイント、配布ポイントを見つけるために行われた操作を記録します。|  
|M365AHandler.log|Desktop Analytics 設定ポリシーに関する情報|
|MaintenanceCoordinator.log|クライアントの一般的なメンテナンス作業を記録します。|  
|Mifprovider.log|管理情報フォーマット (MIF) ファイルの WMI プロバイダーの活動を記録します。|  
|mtrmgr.log|ソフトウェア使用状況測定プロセスを記録します。|  
|PolicyAgent.log|データ転送サービスを使用して行われたポリシーの要求を記録します。|  
|PolicyAgentProvider.log|ポリシーに加えられた変更を記録します。|  
|PolicyEvaluator.log|ソフトウェア更新プログラムのポリシーを含む、クライアント コンピューターのポリシーの評価の詳細を記録します。|  
|PolicyPlatformClient.log|ファイル プロバイダーを除く、Program Files\Microsoft Policy Platform にあるすべてのプロバイダーの修正プロセスとコンプライアンス対応プロセスを記録します。|  
|PolicySdk.log|ポリシー システム SDK のインターフェイスによる操作を記録します。|  
|Pwrmgmt.log|ウェイクアップ プロキシのクライアント設定の有効化と無効化、および構成に関する情報を記録します。|  
|PwrProvider.log|WMI サービスでホストされている電源管理プロバイダー (PWRInvProvider) による処理を記録します。 このプロバイダーは、サポートされているすべてのバージョンの Windows で、ハードウェアのインベントリ中にコンピューターの現在の設定を列挙し、電源プランの設定を適用します。|  
|SCClient_&lt;*domain*\>@&lt;*username*\>_1.log|クライアント コンピューターの特定のユーザーがソフトウェア センターで行った操作を記録します。|  
|SCClient_&lt;*domain*\>@&lt;*username*\>_2.log|クライアント コンピューターの特定のユーザーがソフトウェア センターで行った操作の履歴を記録します。|  
|Scheduler.log|クライアントのスケジュールが設定されている処理をすべて記録します。|  
|SCNotify_&lt;*domain*\>@&lt;*username*\>_1.log|特定のユーザーに送信したソフトウェアに関する通知を記録します。|  
|SCNotify_&lt;*domain*\>@&lt;*username*\>_1-&lt;*date_time*>.log|特定のユーザーに送信したソフトウェアに関する通知の履歴を記録します。|  
|setuppolicyevaluator.log|WMI による構成とインベントリ ポリシーの作成を記録します。|  
|SleepAgent_&lt;*domain*\>@SYSTEM_0.log|ウェイクアップ プロキシのメイン ログ ファイルです。|  
|smscliui.log|コントロール パネルで Configuration Manager クライアントがどのように使用されたかを記録します。|  
|SrcUpdateMgr.log|Windows インストーラーを使ってインストールされたアプリケーションが、現在の配布ポイントにあるソースでどのように更新されたかを記録します。|  
|StatusAgent.log|クライアント コンポーネントによって作成されたステータス メッセージを記録します。|  
|SWMTRReportGen.log|使用状況測定エージェントによる、使用状況レポート生成用データの収集を記録します。 このデータは、Mtrmgr.log に記録されます。|  
|UserAffinity.log|ユーザーとデバイスのアフィニティの詳細を記録します。|  
|VirtualApp.log|Application Virtualization (App-V) 展開の評価に特有の情報を記録します。|  
|Wedmtrace.log|Windows Embedded クライアントの書き込みフィルターに関連する処理を記録します。|  
|wakeprxy-install.log|ウェイクアップ プロキシを有効にするクライアント設定オプションをクライアントが受信したときに、インストール情報を記録します。|  
|wakeprxy-uninstall.log|ウェイクアップ プロキシが以前に有効になっていた場合、ウェイクアップ プロキシを無効にするクライアント設定オプションをクライアントが受信したときに、ウェイクアップ プロキシのアンインストールに関する情報を記録します。|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a> クライアントのインストール

次の表に、Configuration Manager クライアントのインストールに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|  
|--------------|-----------------|  
|ccmsetup.log|クライアントのセットアップ、クライアントのアップグレード、およびクライアントの削除に関する ccmsetup.exe のタスクを記録します。 クライアントのインストールのトラブルシューティングに使用できます。|  
|ccmsetup-ccmeval.log|クライアントのステータスと修復に関する ccmsetup.exe のタスクを記録します。|  
|CcmRepair.log|クライアント エージェントの修復処理を記録します。|  
|client.msi.log|client.msi によって行われた設定タスクを記録します。 クライアントのインストールまたは削除に関する問題の解消に利用できます。|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a> Linux および UNIX 用のクライアント

> [!Important]  
> バージョン 1902 以降の Configuration Manager では、Linux または UNIX クライアントはサポートされていません。
>
> Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。

Linux および UNIX 用の Configuration Manager クライアントでは、次のログ ファイルに情報を記録します。  

> [!TIP]
> Linux および UNIX 用のクライアントのログ ファイルを表示するには、CMTrace を使用します。

|ログの名前|詳細|
|-------------------|-----------------------------------------------------------------|
|Scxcm.log| Linux および UNIX 用の Configuration Manager クライアントのコア サービス (ccmexec.bin) のログ ファイルです。 このログ ファイルには、ccmexec.bin のインストールと実行中の処理に関する情報が含まれます。 既定でこのログ ファイルは **/var/opt/microsoft/scxcm.log** にあります ログ ファイルの場所を変更するには、 **/opt/microsoft/configmgr/etc/scxcm.conf** を編集して **[パス]** フィールドを変更します。 変更を有効にするために、クライアント コンピューターやサービスを再起動する必要はありません。 ログ レベルを 4 種類の設定のいずれかに設定できます。 |
| Scxcmprovider.log |Linux および UNIX 用の Configuration Manager クライアントの CIM サービス (omiserver.bin) のログ ファイルです。 このログ ファイルには、nwserver.bin の実行中の処理に関する情報が含まれます。 このログは `/var/opt/microsoft/configmgr/scxcmprovider.log` にあります。 ログ ファイルの場所を変更するには、 **/opt/microsoft/omi/etc/scxcmprovider.conf** を編集して **[パス]** フィールドを変更します。 変更を有効にするために、クライアント コンピューターやサービスを再起動する必要はありません。 ログ レベルを 3 つの設定のいずれかに設定できます。|

両方のログ ファイルは、いくつかのレベルのログ記録をサポートします。  

- **scxcm.log**。 ログ レベルを変更するには、 **/opt/microsoft/configmgr/etc/scxcm.conf** を編集し、 **[モジュール]** タグの各インスタンスを必要なログ レベルに変更します。  

  - エラー:注意が必要な問題を示します。  

  - 警告:クライアントの処理で発生した可能性がある問題を示します。  

  - 情報:クライアントのさまざまなイベントのステータスを示す、さらに詳細なログ記録です。  

  - トレース: 問題の診断に通常使用する、詳細なログ記録です。  

- **scxcmprovider.log**。 ログ レベルを変更するには、 **/opt/microsoft/omi/etc/scxcmprovider.conf** を編集し、タグ **[モジュール]** の各インスタンスを必要なログ レベルに変更します。  

  - エラー:注意が必要な問題を示します。  

  - 警告:クライアントの処理で発生した可能性がある問題を示します。

  - 情報:クライアントのさまざまなイベントのステータスを示す、さらに詳細なログ記録です。  

通常の動作条件では、エラーのログ レベルを使用します。 このログ レベルでは、最小限のログ ファイルが作成されます。 ログ レベルがエラーから警告、情報、トレースへと上がるにつれて、ログ ファイルにさらに多くのデータが書き込まれるため、作成されるログ ファイルが大きくなります。  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a> Linux および UNIX 用のクライアントのログ ファイルを管理する

Linux および UNIX 用のクライアントでは、クライアント ログ ファイルの最大サイズが制限されていません。 また、.log ファイルの内容が、.lo_ ファイルなどの別のファイルに自動的にコピーされることもありません。 ログ ファイルの最大サイズを制御する場合、Linux および UNIX 用の Configuration Manager クライアントとは独立して、ログ ファイルを管理する手順を実行します。  

たとえば、標準の Linux および UNIX コマンド「**logrotate**」を使用して、クライアント ログ ファイルのサイズとローテーションを管理できます。 Linux および UNIX 用の Configuration Manager クライアントには、ログのローテーションがいつ完了するのかをクライアントに **logrotate** で知らせるインターフェイスが用意されています。これにより、クライアントはログ ファイルへのログの記録を再開できるようになります。  

**logrotate**の詳細については、ご使用の Linux および UNIX ディストリビューションのドキュメントを参照してください。  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a> Mac コンピューター用のクライアント

Mac コンピューター用の Configuration Manager クライアントでは、Mac コンピューター上の次のログ ファイルに情報が記録されます。  

|ログの名前|詳細|場所|
|--------------|-------------|-------------|
|CCMClient-&lt;*date_time*>.log|アプリケーション管理、インベントリ、エラー記録などの、Mac クライアントの操作に関連する処理が記録されます。| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent-&lt;*date_time*>.log|ユーザーのサインインとサインアウト操作、Mac コンピューターの処理など、クライアントの操作に関連する情報を記録します。| `~/Library/Logs`|  
|CCMNotifications-&lt;*date_time*>.log|Mac コンピューターに表示された Configuration Manager の通知に関連する処理を記録します。| `~/Library/Logs`|  
|CCMPrefPane-&lt;*date_time*>.log|全般的なステータスやエラー記録などの、Mac コンピューターの Configuration Manager の設定ダイアログ ボックスに関連する処理を記録します。| `~/Library/Logs`|  

サイト システム サーバーのログ ファイル **SMS_DM.log** には、モバイル デバイスおよび Mac コンピューター用に設定された管理ポイントと Mac コンピューター間の通信も記録されます。  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a> サーバー ログ ファイル

次のセクションでは、サイト サーバーにあるログ ファイルと、各種サイト システムの役割に関係のあるログ ファイルについて説明します。  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a> サイト サーバーとサイト システム

次の表に、Configuration Manager のサイト サーバーとサイト システム サーバーにあるログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|adctrl.log|登録操作を記録します。|サイト サーバー|  
|ADForestDisc.log|Active Directory フォレストの探索操作を記録します。|サイト サーバー|  
|adminservice.log|SMS プロバイダーの管理サービス REST API のアクションを記録します|SMS プロバイダーのあるコンピューター|
|ADService.log|Active Directory のアカウントの作成とセキュリティ グループの詳細を記録します。|サイト サーバー|  
|adsgdis.log|Active Directory グループの探索の処理を記録します。|サイト サーバー|  
|adsysdis.log|Active Directory システムの探索操作を記録します。|サイト サーバー|  
|adusrdis.log|Active Directory ユーザーの探索操作を記録します。|サイト サーバー|  
|BusinessAppProcessWorker.log|ビジネス向け Microsoft Store アプリの処理を記録します。|サイト サーバー|
|ccm.log|クライアント プッシュ インストールの処理を記録します。|サイト サーバー|  
|CertMgr.log|サイト内通信用の証明書に関する操作を記録します。|サイト システム サーバー|  
|chmgr.log|クライアントの正常性マネージャーによる処理を記録します。|サイト サーバー|  
|Cidm.log|クライアント インストール データ マネージャー (CIDM) によるクライアント設定の変更を記録します。|サイト サーバー|  
|CollectionAADGroupSyncWorker.log | バージョン 2002 以降では、コレクション メンバーシップの結果を Azure Active Directory に同期するログ ファイルです。 バージョン 1910 以前では、この機能のログ記録は SMS_AZUREAD_DISCOVERY_AGENT.log に統合されていました。 | サイト サーバー|
|colleval.log|コレクション エバリュエーターによるコレクションの生成、変更、削除の詳細を記録します。|サイト サーバー|  
|compmon.log|サイト サーバーの監視されているコンポーネント スレッドのステータスを記録します。|サイト システム サーバー|  
|compsumm.log|コンポーネントのステータスの要約操作を記録します。|サイト サーバー|  
|ComRegSetup.log|サイト サーバーの初期インストール時の COM 登録結果を記録します。|サイト システム サーバー|  
|dataldr.log|Configuration Manager データベースの MIF ファイルとハードウェア インベントリの処理に関する情報を記録します。|サイト サーバー|  
|ddm.log|探索データ マネージャーによる処理を記録します。|サイト サーバー|  
|despool.log|他のサイトからの通信を受信したことを記録します。|サイト サーバー|  
|distmgr.log|パッケージの作成、圧縮、差分レプリケーション、情報の更新を記録します。 また、配布マネージャー コンポーネントの他のアクティビティを含めることもできます。 たとえば、配布ポイントのインストール、接続試行、コンポーネントのインストールなどです。 このログを使用する他の機能の詳細については、「[サービス接続ポイント](#BKMK_WITLog)」と「[OS の展開](#BKMK_OSDLog)」を参照してください。|サイト サーバー|  
|EPCtrlMgr.log|Endpoint Protection ポイントのサイト システムの役割のサーバーにあるマルウェア情報と Configuration Manager データベースの同期に関する情報を記録します。|サイト サーバー|  
|EPMgr.log|Endpoint Protection ポイントのサイト システムの役割のステータスを記録します。|サイト システム サーバー|  
|EPSetup.log|Endpoint Protection ポイントのサイト システムの役割のインストールに関する情報を含みます。|サイト システム サーバー|  
|EnrollSrv.log|登録サービス プロセスの処理を記録します。|サイト システム サーバー|  
|EnrollWeb.log|登録 Web サイト プロセスによる処理を記録します。|サイト システム サーバー|  
|fspmgr.log|フォールバック ステータス ポイントのサイト システムの役割による処理を記録します。|サイト システム サーバー|  
|hman.log|サイトの構成の変更と、Active Directory Domain Services でのサイト情報の発行を記録します。|サイト サーバー|  
|Inboxast.log|管理ポイントから、サイトサーバーの対応する受信トレイ フォルダーに移動したファイルを記録します。|サイト サーバー|  
|inboxmgr.log|受信トレイ フォルダー間のファイルの移動を記録します。|サイト サーバー|  
|inboxmon.log|受信トレイにあるファイルの処理とパフォーマンス カウンターの更新を記録します。|サイト サーバー|  
|invproc.log|セカンダリ サイトから親サイトへの MIF ファイルの転送を記録します。|サイト サーバー|  
|migmctrl.log|移行処理に関する情報 (移行ジョブ、共有配布ポイント、配布ポイントのアップグレード) を記録します。|Configuration Manager 階層の最上位サイトと、それぞれの子プライマリ サイト 階層にプライマリ サイトが複数ある場合は、中央管理サイトで作成されたログ ファイルを使用してください。|  
|mpcontrol.log|Windows インターネット ネーム サービス (WINS) に管理ポイントの登録を記録します。 管理ポイントの可用性を 10 分おきに記録します。|サイト システム サーバー|  
|mpfdm.log|管理ポイント コンポーネントによる、クライアント ファイルの、サイト サーバーの対応する受信トレイ フォルダーへの移動処理を記録します。|サイト システム サーバー|  
|mpMSI.log|管理ポイントのインストールの詳細を記録します。|サイト サーバー|  
|MPSetup.log|管理ポイントのインストール ラッパー プロセスを記録します。|サイト サーバー|  
|netdisc.log|ネットワーク探索操作を記録します。|サイト サーバー|  
|NotiCtrl.log|アプリケーションの要求通知。|サイト サーバー|  
|ntsvrdis.log|サイト システム サーバーの探索操作を記録します。|サイト サーバー|  
|Objreplmgr|レプリケーションによるオブジェクトの変更通知の処理を記録します。|サイト サーバー|  
|offermgr.log|開示通知の更新を記録します。|サイト サーバー|  
|offersum.log|展開のステータス メッセージの要約処理を記録します。|サイト サーバー|  
|OfflineServicingMgr.log|オペレーティング システム イメージ ファイルへの更新プログラムの適用を記録します。|サイト サーバー|  
|outboxmon.log|送信トレイにあるファイルの処理とパフォーマンス カウンターの更新を記録します。|サイト サーバー|  
|PerfSetup.log|パフォーマンス カウンターのインストール結果を記録します。|サイト システム サーバー|  
|PkgXferMgr.log|SMS_Executive コンポーネントによる、プライマリ サイトからリモート配布ポイントへのコンテンツの送信処理を記録します。|サイト サーバー|  
|policypv.log|クライアントの設定または展開の変更を反映した、クライアント ポリシーの更新を記録します。|プライマリ サイト サーバー|  
|rcmctrl.log|階層にあるサイト間のデータベースのレプリケーションを記録します。|サイト サーバー|  
|replmgr.log|サイト サーバー コンポーネントとスケジューラ コンポーネント間のファイルのレプリケーションを記録します。|サイト サーバー|  
|ResourceExplorer.log|リソース エクスプローラーの実行時に発生したエラーと警告、および実行に関する情報を記録します。|Configuration Manager コンソールを実行しているコンピューター|  
|RESTPROVIDERSetup.log|SMS プロバイダーの管理サービス REST API のインストール|SMS プロバイダーのあるコンピューター|
|ruleengine.log|自動展開規則に関する情報 (確認、コンテンツのダウンロード、およびソフトウェア更新プログラム グループと展開の作成) を記録します。|サイト サーバー|  
|schedule.log|サイト間のジョブとファイルのレプリケーションに関する情報を記録します。|サイト サーバー|  
|sender.log|サイト間のファイルベースのレプリケーションによって転送されるファイルを記録します。|サイト サーバー|  
|sinvproc.log|サイト データベースに格納されるソフトウェアのインベントリ データの処理に関する情報を記録します。|サイト サーバー|  
|sitecomp.log|サイトのすべてのサイト システム サーバーにインストールされているサイト コンポーネントのメンテナンスに関する詳細を記録します。|サイト サーバー|  
|sitectrl.log|データベースのサイト コントロール オブジェクトに加えられたサイト設定の変更を記録します。|サイト サーバー|  
|sitestat.log|すべてのサイト システムの可用性とディスク領域の監視プロセスを記録します。|サイト サーバー|
|SMS_AZUREAD_DISCOVERY_AGENT.log| Azure Active Directory (Azure AD) ユーザーとユーザー グループの探索のログ ファイル。 バージョン 1910 以前では、コレクション メンバーシップの結果の Azure AD への同期も含まれていました。| サイト サーバー|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|ビジネス向け Microsoft Store からアプリを同期するコンポーネントのログ ファイルです。|サイト サーバー|
|SMS_ISVUPDATES_SYNCAGENT.log| サードパーティのソフトウェア更新プログラムを同期するためのログ ファイルです。| Configuration Manager 階層内の最上位のソフトウェア更新ポイント。|
|SMS_OrchestrationGroup.log| オーケストレーション グループのログ ファイル|サイト サーバー|
|SMS_PhasedDeployment.log| 段階的展開のログ ファイル|Configuration Manager 階層の最上位サイト|
|SMS_REST_PROVIDER.log|証明書情報を含む、SMS プロバイダー管理サービス REST API のサービス正常性状態|SMS プロバイダーのあるコンピューター|
|SmsAdminUI.log|Configuration Manager コンソール アクティビティを記録します。|Configuration Manager コンソールを実行しているコンピューター|  
|SMSAWEBSVCSetup.log|アプリケーション カタログ Web サービスのインストール処理を記録します。|サイト システム サーバー|  
|smsbkup.log|サイトのバックアップ プロセスの出力を記録します。|サイト サーバー|  
|smsdbmon.log|データベースの変更を記録します。|サイト サーバー|  
|SMSENROLLSRVSetup.log|登録 Web サービスのインストール操作を記録します。|サイト システム サーバー|  
|SMSENROLLWEBSetup.log|登録 Web サイトのインストール操作を記録します。|サイト システム サーバー|  
|smsexec.log|すべてのサイト サーバー コンポーネント スレッドの処理を記録します。|サイト サーバーまたはサイト システム サーバー|  
|SMSFSPSetup.log|フォールバック ステータス ポイントのインストールによって生成されたメッセージを記録します。|サイト システム サーバー|  
|SMSPORTALWEBSetup.log|アプリケーション カタログ Web サイトのインストール処理を記録します。|サイト システム サーバー|  
|SMSProv.log|WMI プロバイダーからのサイト データベースへのアクセスを記録します。|SMS プロバイダーのあるコンピューター|  
|srsrpMSI.log|MSI によるレポート ポイントのインストール プロセスの出力結果を含みます。|サイト システム サーバー|  
|srsrpsetup.log|レポート ポイントのインストール プロセスの結果を記録します。|サイト システム サーバー|  
|statesys.log|ステート システムのメッセージの処理を記録します。|サイト サーバー|  
|statmgr.log|データベースに書き込まれたすべてのステータス メッセージを記録します。|サイト サーバー|  
|swmproc.log|ファイルの使用状況測定と設定の処理を記録します。|サイト サーバー|  

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a> サイト サーバーのインストール

次の表に、サイトのインストールに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|前提条件コンポーネントの評価とインストール操作を記録します。|サイト サーバー|  
|ConfigMgrSetup.log|サイト サーバーのセットアップからの詳しい出力を記録します。|サイト サーバー|  
|ConfigMgrSetupWizard.log|セットアップ ウィザードによる処理に関係のある情報を記録します。|サイト サーバー|  
|SMS_BOOTSTRAP.log|セカンダリ サイトのインストール プロセスの進行状況を記録します。 実際のセットアップ プロセスの詳細は、ConfigMgrSetup.log に記録されます。|サイト サーバー|  
|smstsvc.log|Windows サービスのインストール、使用、および削除に関する情報を記録します。 Windows では、サーバー間のネットワーク接続とアクセス許可をテストするためにこのサービスが使用されます。 接続を作成するサーバーのコンピューター アカウントが使用されます。|サイト サーバーとサイト システム サーバー|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a> データ ウェアハウス サービス ポイント

次の表に、データ ウェアハウス サービス ポイントに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|DWSSMSI.log|データ ウェアハウス サービス ポイントのインストールによって生成されたメッセージを記録します。|サイト システム サーバー|  
|DWSSSetup.log|データ ウェアハウス サービス ポイントのインストールによって生成されたメッセージを記録します。|サイト システム サーバー|  
|Microsoft.ConfigMgrDataWarehouse.log|サイト データベースとデータ ウェアハウス データベースの間のデータ同期に関する情報を記録します。|サイト システム サーバー|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a> フォールバック ステータス ポイント

次の表に、フォールバック ステータス ポイントのインストールに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|FspIsapi|モバイル デバイス レガシ クライアントとクライアント コンピューターからのフォールバック ステータス ポイントへの通信に関する詳細を記録します。|サイト システム サーバー|  
|fspMSI.log|フォールバック ステータス ポイントのインストールによって生成されたメッセージを記録します。|サイト システム サーバー|  
|fspmgr.log|フォールバック ステータス ポイントのサイト システムの役割による処理を記録します。|サイト システム サーバー|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a> 管理ポイント

次の表に、管理ポイントのインストールに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|エンドポイントでのクライアント メッセージの送受信に関する情報を記録します。|サイト システム サーバー|
|CCM_STS.log|Azure Active Directory またはサイト発行のクライアント トークンからの認証トークンのアクティビティを記録します。|サイト システム サーバー|
|ClientAuth.log|署名および認証アクティビティを記録します。|サイト システム サーバー|
|MP_CliReg.log|管理ポイントによって処理されるクライアントの登録を記録します。|サイト システム サーバー|  
|MP_Ddr.log|クライアントの XML レコードの DDR への変換と、変換されたレコードのサイト サーバーへのコピーを記録します。|サイト システム サーバー|  
|MP_Framework.log|コア管理ポイントとクライアント フレームワーク コンポーネントの動作を記録します。|サイト システム サーバー|  
|MP_GetAuth.log|クライアントの認証を記録します。|サイト システム サーバー|  
|MP_GetPolicy.log|クライアント コンピューターからのポリシーの要求を記録します。|サイト システム サーバー|  
|MP_Hinv.log|クライアントの XML 形式のハードウェア インベントリ レコードの変換と、変換されたファイルのサイト サーバーへのコピーを記録します。|サイト システム サーバー|  
|MP_Location.log|クライアントからの場所の要求と、それに対する応答を記録します。|サイト システム サーバー|  
|MP_OOBMgr.log|クライアントからの OTP 受信に関連する、管理ポイントの動作を記録します。|サイト システム サーバー|  
|MP_Policy.log|ポリシーの通信を記録します。|サイト システム サーバー|  
|MP_RegistrationManager.log|証明書、CRL、トークンの検証など、クライアントの登録に関連する処理を記録します。|サイト システム サーバー|
|MP_Relay.log|クライアントから収集されたファイルの転送を記録します。|サイト システム サーバー|  
|MP_Retry.log|ハードウェア インベントリの再試行プロセスを記録します。|サイト システム サーバー|  
|MP_Sinv.log|クライアントの XML 形式のソフトウェア インベントリ レコードの変換と、変換されたファイルのサイト サーバーへのコピーを記録します。|サイト システム サーバー|  
|MP_SinvCollFile.log|ファイルの収集の詳細を記録します。|サイト システム サーバー|  
|MP_Status.log|クライアントからの XML 形式のステータス メッセージ ファイルの変換と、変換されたファイルのサイト サーバーへのコピーを記録します。|サイト システム サーバー|
|mpcontrol.log|管理ポイントの WINS への登録を記録します。 管理ポイントの可用性を 10 分おきに記録します。|サイト サーバー|  
|mpfdm.log|管理ポイント コンポーネントによる、クライアント ファイルの、サイト サーバーの対応する受信トレイ フォルダーへの移動処理を記録します。|サイト システム サーバー|  
|mpMSI.log|管理ポイントのインストールの詳細を記録します。|サイト サーバー|  
|MPSetup.log|管理ポイントのインストール ラッパー プロセスを記録します。|サイト サーバー|  
|UserService.log|ソフトウェア センターからのユーザー要求を記録し、ユーザーが利用できるアプリケーションをサーバーから取得/インストールします。|サイト システム サーバー|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a> サービス接続ポイント

次の表に、サービス接続ポイントに関連する情報を含むログ ファイルを一覧表示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|証明書とプロキシ アカウントの情報を記録します。|サイト サーバー|  
|colleval.log|コレクション エバリュエーターによるコレクションの生成、変更、削除の詳細を記録します。|プライマリ サイトと中央管理サイト|  
|Cloudusersync.log|ユーザーのライセンス有効化を記録します。|サービス接続ポイントのあるコンピューター|  
|dataldr.log|MIF ファイルの処理に関する情報を記録します。|サイト サーバー|  
|ddm.log|探索データ マネージャーによる処理を記録します。|サイト サーバー|  
|distmgr.log|コンテンツ配布要求に関する情報を記録します。|最上位のサイト サーバー|  
|Dmpdownloader.log|Microsoft Intune からのダウンロードに関する情報を記録します。|サービス接続ポイントのあるコンピューター|  
|Dmpuploader.log|Microsoft Intune へのデータベースの変更のアップロードに関する情報を記録します。|サービス接続ポイントのあるコンピューター|  
|hman.log|メッセージの転送に関する情報を記録します。|サイト サーバー|  
|MSfBSyncWorker.log|ビジネス向け Microsoft Store との通信に関する情報を記録します。|サービス接続ポイントのあるコンピューター|
|objreplmgr.log|ポリシーと割り当ての処理を記録します。|プライマリ サイト サーバー|  
|policypv.log|すべてのポリシーのポリシー生成を記録します。|サイト サーバー|  
|outgoingcontentmanager.log|Microsoft Intune にアップロードされたコンテンツを記録します。|サービス接続ポイントのあるコンピューター|  
|sitecomp.log|サービス接続ポイントのインストールの詳細を記録します。|サイト サーバー|  
|SmsAdminUI.log|Configuration Manager コンソール アクティビティを記録します。|Configuration Manager コンソールを実行しているコンピューター|  
|SMS_CLOUDCONNECTION.log|クラウド サービスに関する情報を記録します。|サービス接続ポイントのあるコンピューター|
|SMSProv.log|SMS プロバイダーのアクティビティを記録します。 Configuration Manager コンソールの操作では、SMS プロバイダーが使用されます。|SMS プロバイダーのあるコンピューター|  
|SrvBoot.log|サービス接続ポイントのインストーラー サービスに関する詳細を記録します。|サービス接続ポイントのあるコンピューター|  
|Statesys.log|モバイル デバイス管理メッセージの処理を記録します。|プライマリ サイトと中央管理サイト|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a> ソフトウェアの更新ポイント

次の表に、ソフトウェアの更新ポイントのインストールに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|ソフトウェアの更新の通知ファイルの親サイトから子サイトへのレプリケーションに関する詳細を記録します。|サイト サーバー|  
|PatchDownloader.log|更新プログラムのソースから、ソフトウェア更新プログラムをサイト サーバーにダウンロードするプロセスの詳細を記録します。|更新プログラムを手動でダウンロードするとき、このファイルは、コンソールを使用するコンピューターの `%temp%` ディレクトリにあります。 自動展開規則では、Configuration Manager クライアントがサイト サーバーにインストールされている場合、このファイルはサイト サーバーの `%windir%\CCM\Logs` にあります。|  
|ruleengine.log|自動展開規則に関する情報 (確認、コンテンツのダウンロード、およびソフトウェア更新プログラム グループと展開の作成) を記録します。|サイト サーバー|
|SMS_ISVUPDATES_SYNCAGENT.log| サードパーティのソフトウェア更新プログラムを同期するためのログ ファイルです。| Configuration Manager 階層内の最上位のソフトウェア更新ポイント。|
|SUPSetup.log|ソフトウェアの更新ポイントのインストールに関する詳細を記録します。 ソフトウェアの更新ポイントのインストールが完了すると、このログ ファイルに「 **Installation was successful** 」と書き込まれます。|サイト システム サーバー|  
|WCM.log|ソフトウェアの更新ポイントの構成に関する情報、およびサブスクライブ済みの更新カテゴリ、分類、言語のための WSUS サーバーへの接続に関する情報を記録します。|WSUS サーバーに接続するサイト サーバー|  
|WSUSCtrl.log|サイトの WSUS サーバーの構成、データベース接続、正常性に関する詳細を記録します。|サイト システム サーバー|  
|wsyncmgr.log|ソフトウェア更新プログラムの同期プロセスの詳細を記録します。|サイト システム サーバー|  
|WUSSyncXML.log|Microsoft 更新プログラム用インベントリ ツールの同期プロセスに関する情報を記録します。|Microsoft 更新プログラム用インベントリ ツールの同期ホストとして構成されているクライアント コンピューター|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a> 機能別ログ ファイル

次のセクションでは、Configuration Manager の機能に関連するログ ファイルについて説明します。  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a> アプリケーション管理

次の表に、アプリケーション管理に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|アプリケーションの現在の状態と意図していた状態、適用性、要件を満たしているかどうか、展開の種類、依存関係を記録します。|クライアント|  
|AppDiscovery.log|クライアント コンピューターでのアプリケーションの探索または検出に関する情報を記録します。|クライアント|  
|AppEnforce.log|クライアントでアプリケーションに対して実行された強制実行処理 (インストールとアンインストール) に関する情報を記録します。|クライアント|  
|AppGroupHandler.log|バージョン 1906 以降の、アプリケーション グループの検出と強制実行に関する情報|クライアント|
|awebsctl.log|アプリケーション カタログ Web サービス ポイントのサイト サーバーの役割の監視操作を記録します。|サイト システム サーバー|  
|awebsvcMSI.log|アプリケーション カタログ Web サービス ポイントのサイト サーバーの役割のインストールに関する詳細を記録します。|サイト システム サーバー|  
|BusinessAppProcessWorker.log|ビジネス向け Microsoft Store アプリの処理を記録します。|サイト サーバー|
|CCMSDKProvider.log|アプリケーション管理 SDK による処理を記録します。|クライアント|  
|colleval.log|コレクション エバリュエーターによるコレクションの生成、変更、削除の詳細を記録します。|サイト システム サーバー|  
|ConfigMgrSoftwareCatalog.log|Silverlight の使用を含む、アプリケーション カタログの動作を記録します。|クライアント|  
|MSfBSyncWorker.log|ビジネス向け Microsoft Store との通信に関する情報を記録します。|サービス接続ポイントのあるコンピューター|
|NotiCtrl.log|アプリケーションの要求通知。|サイト サーバー|  
|portlctl.log|アプリケーション カタログ Web サイト ポイントのサイト サーバーの役割の監視操作を記録します。|サイト システム サーバー|  
|portlwebMSI.log|アプリケーション カタログ Web サイトの役割の MSI によるインストール操作を記録します。|サイト システム サーバー|  
|PrestageContent.log|事前設定されたリモート配布ポイントの ExtractContent.exe の使用に関する詳細を記録します。 このツールは、ファイルにエクスポートされているコンテンツを抽出します。|サイト システム サーバー|  
|ServicePortalWebService.log|アプリケーション カタログ Web サービスの動作を記録します。|サイト システム サーバー|  
|ServicePortalWebSite.log|アプリケーション カタログ Web サイトの動作を記録します。|サイト システム サーバー|  
|SettingsAgent.log|特定のアプリケーションの強制実行、アプリケーション グループの評価のオーケストレーション、および共同管理ポリシーの詳細を記録します。|クライアント|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|ビジネス向け Microsoft Store からアプリを同期するコンポーネントのログ ファイルです。|サイト サーバー|
|SMS_CLOUDCONNECTION.log|クラウド サービスに関する情報を記録します。|サービス接続ポイントのあるコンピューター|
|SMSdpmon.log|配布ポイントで構成されている、スケジュールに従った配布ポイントの正常性の監視タスクの詳細を記録します。|サイト サーバー|  
|SoftwareCatalogUpdateEndpoint.log|ソフトウェア センターに表示されるアプリケーション カタログの URL の管理操作を記録します。|クライアント|  
|SoftwareCenterSystemTasks.log|ソフトウェア センターの前提条件コンポーネントの検証に関連する活動を記録します。|クライアント|  
|TSDTHandler.log|タスク シーケンスの展開の種類の場合。 アプリの適用 (インストールまたはアンインストール) からタスク シーケンスの起動までのプロセスを記録します。 AppEnforce.log と smsts.log と共に使用します。|クライアント|<!-- MEMDocs#336 -->

#### <a name="packages-and-programs"></a>パッケージとプログラム

次の表に、パッケージとプログラムの展開に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|colleval.log|コレクション エバリュエーターによるコレクションの生成、変更、削除の詳細を記録します。|サイト サーバー|  
|execmgr.log|実行されたパッケージとタスク シーケンスの詳細を記録します。|クライアント|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a> 資産インテリジェンス

次の表に、資産インテリジェンスに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|資産インテリジェンスのインベントリ操作を記録します。|クライアント|  
|aikbmgr.log|資産インテリジェンス カタログを更新するための、受信トレイの XML ファイルの処理に関する詳細を記録します。|サイト サーバー|  
|AIUpdateSvc.log|資産インテリジェンス同期ポイントとクラウド サービスのやり取りを記録します。|サイト システム サーバー|  
|AIUSMSI.log|資産インテリジェンス同期ポイントのサイト システムの役割のインストールに関する詳細を記録します。|サイト システム サーバー|  
|AIUSSetup.log|資産インテリジェンス同期ポイントのサイト システムの役割のインストールに関する詳細を記録します。|サイト システム サーバー|  
|ManagedProvider.log|ソフトウェアの探索に関する情報を、関連付けられたソフトウェア識別タグと共に記録します。 ハードウェア インベントリに関連する処理も記録します。|サイト システム サーバー|  
|MVLSImport.log|インポートされたライセンス ファイルの処理の詳細を記録します。|サイト システム サーバー|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a> バックアップと回復

次の表に、バックアップと回復操作 (サイトのリセットと SMS プロバイダーの変更を含む) に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Configuration Manager のサイトをバックアップから回復するときのセットアップと回復操作に関する情報を記録します。|サイト サーバー|  
|smsbkup.log|サイトのバックアップ操作の詳細を記録します。|サイト サーバー|  
|smssqlbkup.log|サイト サーバーではないサーバーに SQL Server がインストールされている場合に、サイト データベースのバックアップ プロセスからの出力を記録します。|サイト データベース サーバー|  
|Smswriter.log|バックアップ プロセスで使用される Configuration Manager VSS ライターの状態に関する情報を記録します。|サイト サーバー|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a> 証明書の登録

次の表は、証明書の登録に関係のある情報を含む Configuration Manager ログ ファイルの一覧です。 証明書の登録では、ネットワーク デバイス登録サービス (NDES) を実行しているサーバー上の Configuration Manager ポリシー モジュールと証明書登録ポイントを使用します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|Crp.log|登録活動を記録します。|証明書登録ポイント|  
|Crpctrl.log|証明書登録ポイントの動作の正常性を記録します。|証明書登録ポイント|  
|Crpsetup.log|証明書登録ポイントのインストールと構成に関する詳細を記録します。|証明書登録ポイント|  
|Crpmsi.log|証明書登録ポイントのインストールと構成に関する詳細を記録します。|証明書登録ポイント|  
|NDESPlugin.log|チャレンジの検証と証明書登録の活動を記録します。|Configuration Manager ポリシー モジュールとネットワーク デバイス登録サービス|  

Configuration Manager のログ ファイルに加えて、ネットワーク デバイス登録サービスを実行するサーバーと、証明書登録ポイントをホストするサーバーで、イベント ビューアーの Windows アプリケーションのログを確認します。 たとえば、 **NetworkDeviceEnrollmentService** ソースからのメッセージを探します。

次のログ ファイルも使用できます。  

- ネットワーク デバイス登録サービスの IIS ログ ファイル: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- 証明書登録ポイントの IIS ログ ファイル: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- ネットワーク デバイス登録ポリシーのログ ファイル: **mscep.log**  

    > [!NOTE]  
    > このファイルは、NDES アカウント プロファイルのフォルダー (たとえば、C:\Users\SCEPSvc) にあります。 NDES ログを有効にする方法の詳細については、NDES Wiki の[ログの有効化](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging)に関するセクションを参照してください。  

### <a name="client-notification"></a><a name="BKMK_BGB"></a> クライアント通知

次の表に、クライアント通知に関連する情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|クライアント通知タスクに関連するサイト サーバーの処理に関する情報と、オンライン ステータス ファイルとタスク ステータス ファイルを処理するサイト サーバーの処理に関する情報を記録します。|サイト サーバー|  
|BGBServer.log|クライアントとサーバー間の通信やクライアントへのタスクのプッシュなどの、通知サーバーの処理を記録します。 また、サイト サーバーに送信されるオンライン ステータス ファイルとタスク ステータス ファイルの生成情報も記録します。|管理ポイント|  
|BgbSetup.log|インストール時とアンインストール時の通知サーバーのインストール ラッパー プロセスの処理を記録します。|管理ポイント|  
|bgbisapiMSI.log|通知サーバーのインストールとアンインストールに関する情報を記録します。|管理ポイント|  
|BgbHttpProxy.log|HTTP を使用して通知サーバーとの間でクライアントのメッセージをリレーしたときに、通知 HTTP プロキシの処理を記録します。|クライアント|  
|CCMNotificationAgent.log|クライアントとサーバー間の通信などの通知エージェントの処理、および受信して他のクライアント エージェントにディスパッチされたタスクに関する情報を記録します。|クライアント|  

### <a name="cloud-management-gateway"></a>クラウド管理ゲートウェイ

次の表に、クラウド管理ゲートウェイに関係のある情報を含むログ ファイルを示します。

|ログの名前|[説明]|ログ ファイルのあるコンピューター|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|クラウド管理ゲートウェイ サービスの展開、進行中のサービスの状態、およびサービスに関連する使用状況データについての情報を記録します。 ログ レベルを構成するには、レジストリ キー `HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER` の **[ログ レベル]** 値を編集します。|プライマリ サイト サーバーまたは CAS の *installdir* フォルダー。|
|CMGSetup.log <sup>[注 1](#bkmk_note1)</sup>|クラウド管理ゲートウェイ展開 (Azure のローカル展開) の 2 番目のフェーズに関する詳細を記録します。 ログ レベルを構成するには、 **[Azure portal] の [Cloud services configuration]\(クラウド サービスの構成\)** タブで **[トレース レベル]** ( **[情報]** (既定値)、 **[詳細]** 、 **[エラー]** ) の設定を使用します。|Azure サーバーの **[%approot%\logs]** 、またはサイト システム サーバーの [SMS/ログ] フォルダー|
|CMGService.log <sup>[注 1](#bkmk_note1)</sup>|Azure のクラウド管理ゲートウェイ サービスのコア コンポーネントの詳細を記録します。 ログ レベルを構成するには、 **[Azure portal] の [Cloud services configuration]\(クラウド サービスの構成\)** タブで **[トレース レベル]** ( **[情報]** (既定値)、 **[詳細]** 、 **[エラー]** ) の設定を使用します。|Azure サーバーの **[%approot%\logs]** 、またはサイト システム サーバーの [SMS/ログ] フォルダー|
|SMS_Cloud_ProxyConnector.log|クラウド管理ゲートウェイ サービスとクラウド管理ゲートウェイ接続ポイントの間の接続の設定に関する詳細を記録します。|サイト システム サーバー|
|CMGContentService.log <sup>[注 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->Azure ストレージからコンテンツも提供するように CMG を有効にすると、このログにそのサービスの詳細が記録されます。|Azure サーバーの **[%approot%\logs]** 、またはサイト システム サーバーの [SMS/ログ] フォルダー|

- 展開のトラブルシューティングの場合は、**CloudMgr.log** および **CMGSetup.log** を使用します。
- サービス正常性のトラブルシューティングの場合は、**CMGService.log** および **SMS_Cloud_ProxyConnector.log** を使用します。
- クライアントのトラフィックのトラブルシューティングの場合は、**CMGHttpHandler.log**、**CMGService.log**、および **SMS_Cloud_ProxyConnector.log** を使用します。

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a> 注 1:Azure から同期されたログ

これらは、クラウド サービス マネージャーによって Azure Storage から 5 分ごとに同期されるローカルの Configuration Manager ログ ファイルです。 クラウド管理ゲートウェイは、Azure Storage に 5 分おきにログをプッシュします。 そのための最大遅延時間は 10 分です。 [詳細] に切り替えると、ローカルとリモートの両方のログに影響します。 実際のファイル名には、サービス名とロール インスタンスの識別子が含まれます。 例: CMG-*ServiceName*-*RoleInstanceID*-CMGSetup.log

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a> コンプライアンス設定と会社のリソースへのアクセス

次の表に、コンプライアンス設定と会社のリソースへのアクセスに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|コンプライアンス設定、ソフトウェア更新プログラム、およびアプリケーション管理による修復とコンプライアンス対応プロセスの詳細を記録します。|クライアント|  
|CITaskManager.log|構成項目のタスクのスケジュール設定に関する情報を記録します。|クライアント|  
|DCMAgent.log|構成項目とアプリケーションの評価、競合の報告、修復の全般的な情報を記録します。|クライアント|  
|DCMReporting.log|ポリシー プラットフォームによるポリシー施行結果を構成項目の状態メッセージとしてレポートする処理に関する情報を記録します。|クライアント|  
|DcmWmiProvider.log|WMI からの構成項目の同期プログラムの読み取りに関する情報を記録します。|クライアント|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Configuration Manager コンソール

次の表に、Configuration Manager コンソールに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Configuration Manager コンソールのインストールを記録します。|Configuration Manager コンソールを実行しているコンピューター|  
|SmsAdminUI.log|Configuration Manager コンソールの操作に関する情報を記録します。|Configuration Manager コンソールを実行しているコンピューター|  
|SMSProv.log|SMS プロバイダーのアクティビティを記録します。 Configuration Manager コンソールの操作では、SMS プロバイダーが使用されます。|サイト サーバーまたはサイト システム サーバー|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a> コンテンツ管理

次の表に、コンテンツの管理に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|特定のクラウド ベースの配布ポイントの詳細 (記憶域とコンテンツのアクセスに関する情報など) を記録します。|サイト システム サーバー|  
|CloudMgr.log|コンテンツのプロビジョニング、記憶域と帯域幅の統計の収集、クラウド ベースの配布ポイントを実行するクラウド サービスを停止または開始した管理者による操作に関する情報を記録します。|サイト システム サーバー|  
|DataTransferService.log|ポリシーまたはパッケージにアクセスするために行われた、BITS による通信をすべて記録します。 このログは、プル配布ポイントでのコンテンツ管理にも使用されます。|プル配布ポイントとして構成されているコンピューター|  
|PullDP.log|プル配布ポイントがソース配布ポイントから転送した、コンテンツに関する情報を記録します。|プル配布ポイントとして構成されているコンピューター|  
|PrestageContent.log|事前設定されたリモート配布ポイントの ExtractContent.exe の使用に関する詳細を記録します。 このツールは、ファイルにエクスポートされているコンテンツを抽出します。|サイト システムの役割|  
|SMSdpmon.log|配布ポイントで構成されている、スケジュールに従った配布ポイントの正常性の監視タスクの詳細を記録します。|サイト システムの役割|  
|smsdpprov.log|プライマリ サイトから受け取った圧縮ファイルの抽出に関する詳細を記録します。 このログは、リモート配布ポイントの WMI プロバイダーによって生成されます。|サイト サーバーに併置されていない配布ポイント コンピューター|  
|smsdpusage.log|実行されて配布ポイントの使用状況の概要レポート用のデータを収集する smsdpusage.exe に関する詳細を記録します。|サイト システムの役割|  

### <a name="desktop-analytics"></a>Desktop Analytics

次のログ ファイルを使って、Configuration Manager と統合された Desktop Analytics の問題のトラブルシューティングに役立ててください。

サービス接続ポイントのログ ファイルは、ディレクトリ `%ProgramFiles%\Configuration Manager\Logs\M365A` にあります。
Configuration Manager クライアント上のログ ファイルは、ディレクトリ `%WinDir%\CCM\logs` にあります。

| ログ | [説明] |ログ ファイルのあるコンピューター|
|---------|---------|---------|
| M365ADeploymentPlanWorker.log | Desktop Analytics クラウド サービスからオンプレミスの Configuration Manager への展開計画の同期に関する情報 |[サービス接続ポイント]|
| M365ADeviceHealthWorker.log | Configuration Manager から Microsoft クラウドへのデバイス正常性のアップロードに関する情報 |[サービス接続ポイント]|
| M365AHandler.log | Desktop Analytics 設定ポリシーに関する情報 |クライアント|
| M365AUploadWorker.log | Configuration Manager から Microsoft クラウドへのコレクションおよびデバイスのアップロードに関する情報 |[サービス接続ポイント]|
| SmsAdminUI.log | Azure クラウド サービスの構成など、Configuration Manager コンソールのアクティビティに関する情報  |[サービス接続ポイント]|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a> 探索

次の表に、探索に関係のある情報を含むログ ファイルをリストします。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Active Directory セキュリティ グループの探索操作を記録します。|サイト サーバー|  
|adsysdis.log|Active Directory システムの探索操作を記録します。|サイト サーバー|  
|adusrdis.log|Active Directory ユーザーの探索操作を記録します。|サイト サーバー|  
|ADForestDisc.log|Active Directory フォレストの探索操作を記録します。|サイト サーバー|  
|ddm.log|探索データ マネージャーによる処理を記録します。|サイト サーバー|  
|InventoryAgent.log|クライアントで行われるハードウェア インベントリ、ソフトウェア インベントリ、定期探索を記録します。|クライアント|  
|netdisc.log|ネットワーク探索操作を記録します。|サイト サーバー|  

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection

次の表に、Endpoint Protection に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Endpoint Protection クライアントのインストール、およびそのクライアントへのマルウェア対策ポリシーの適用に関する詳細を記録します。|クライアント|  
|EPCtrlMgr.log|Endpoint Protection ポイントのサイト システムの役割のサーバーにあるマルウェア情報と Configuration Manager データベースの同期に関する詳細を記録します。|サイト システム サーバー|  
|EPMgr.log|Endpoint Protection ポイントのサイト システムの役割のステータスを記録します。|サイト システム サーバー|  
|EPSetup.log|Endpoint Protection ポイントのサイト システムの役割のインストールに関する情報を含みます。|サイト システム サーバー|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a> 拡張機能

次の表に、拡張機能に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Microsoft からの拡張機能のダウンロードとすべての拡張機能のインストールとアンインストールに関する情報を記録します。|Configuration Manager コンソールを実行しているコンピューター|  
|FeatureExtensionInstaller.log|Configuration Manager コンソールで有効または無効にしたときの個々の拡張機能のインストールと削除に関する情報を記録します。|Configuration Manager コンソールを実行しているコンピューター|  
|SmsAdminUI.log|Configuration Manager コンソール アクティビティを記録します。|Configuration Manager コンソールを実行しているコンピューター|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a> インベントリ

次の表に、インベントリ データの処理に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Configuration Manager データベースの MIF ファイルとハードウェア インベントリの処理に関する情報を記録します。|サイト サーバー|  
|invproc.log|セカンダリ サイトから親サイトへの MIF ファイルの転送を記録します。|セカンダリ サイト サーバー|  
|sinvproc.log|サイト データベースに格納されるソフトウェアのインベントリ データの処理に関する情報を記録します。|サイト サーバー|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a> 測定

次の表に、使用状況測定に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|ソフトウェア使用状況測定プロセスを記録します。|クライアント|  
|SWMTRReportGen.log|使用状況測定エージェントによる、使用状況レポート生成用データの収集を記録します。 このデータは、Mtrmgr.log に記録されます。|クライアント|
|swmproc.log|ファイルの使用状況測定と設定の処理を記録します。|サイト サーバー|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a> 移行

次の表に、移行に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|移行処理に関する情報 (移行ジョブ、共有配布ポイント、配布ポイントのアップグレード) を記録します。|Configuration Manager 階層の最上位サイトと、それぞれの子プライマリ サイト 階層にプライマリ サイトが複数ある場合は、中央管理サイトで作成されたログ ファイルを使用してください。|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a> モバイル デバイス

このセクションでは、モバイル デバイスの管理に関係のあるログ ファイルについて説明します。  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a> 登録

次の表に、モバイル デバイスの登録に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|モバイル デバイス管理が有効になっている管理ポイントとそのエンドポイント間の通信を記録します。|サイト システム サーバー|  
|dmpmsi.log|Windows インストーラーで管理ポイントのモバイル デバイス管理を有効にするときの構成データを記録します。|サイト システム サーバー|  
|DMPSetup.log|モバイル デバイスに対して有効になっている場合に管理ポイントの構成を記録します。|サイト システム サーバー|  
|enrollsrvMSI.log|Windows インストーラーで登録ポイントを構成するときのデータを記録します。|サイト システム サーバー|  
|enrollmentweb.log|モバイル デバイスと登録プロキシ ポイント間の通信を記録します。|サイト システム サーバー|  
|enrollwebMSI.log|Windows インストーラーで登録プロキシ ポイントを構成するときのデータを記録します。|サイト システム サーバー|  
|enrollmentservice.log|登録プロキシ ポイントと登録ポイント間の通信を記録します。|サイト システム サーバー|  
|SMS_DM.log|モバイル デバイス、Mac コンピューター、およびモバイル デバイスと Mac コンピューターに有効になっている管理ポイント間の通信を記録します。|サイト システム サーバー|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Exchange Server コネクタ

次のログには、Exchange Server コネクタに関係のある情報が含まれます。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Exchange Server コネクタの動作とステータスを記録します。|サイト サーバー|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a> モバイル デバイス レガシ

次の表に、モバイル デバイス レガシ クライアントに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|モバイル デバイス レガシ クライアントの証明書登録データの詳細を記録します。|クライアント|  
|DMCertResp.htm|モバイル デバイス レガシ クライアントの登録プログラムが証明書サーバーに PKI 証明書を要求したときのサーバーからの HTML 応答を記録します。|クライアント|  
|DmClientHealth.log|モバイル デバイス管理が有効になっている管理ポイントと通信するすべてのモバイル デバイス レガシ クライアントの GUID を記録します。|サイト システム サーバー|  
|DmClientRegistration.log|モバイル デバイス レガシ クライアントからの登録要求とその応答を記録します。|サイト システム サーバー|  
|DmClientSetup.log|モバイル デバイス レガシ クライアントのクライアント セットアップ データを記録します。|クライアント|  
|DmClientXfer.log|モバイル デバイス レガシ クライアントと ActiveSync によるクライアント データの転送を記録します。|クライアント|  
|DmCommonInstaller.log|モバイル デバイス レガシ クライアントの転送ファイルのインストールを記録します。|クライアント|  
|DmInstaller.log|モバイル デバイス レガシ クライアントの DMInstaller が正しく DmClientSetup を呼び出したかどうかと、DmClientSetup が正常に終了したかどうかを記録します。|クライアント|  
|DmpDatastore.log|モバイル デバイス管理が有効になっている管理ポイントからのサイト データベースへの接続とクエリをすべて記録します。|サイト システム サーバー|  
|DmpDiscovery.log|モバイル デバイス管理が有効になっている管理ポイントのモバイル デバイス レガシ クライアントの探索データをすべて記録します。|サイト システム サーバー|  
|DmpHardware.log|モバイル デバイス管理が有効になっている管理ポイントのモバイル デバイス レガシ クライアントのハードウェア インベントリ データをすべて記録します。|サイト システム サーバー|  
|DmpIsapi.log|モバイル デバイス レガシ クライアントの、モバイル デバイス管理が有効になっている管理ポイントとの通信を記録します。|サイト システム サーバー|  
|dmpmsi.log|Windows インストーラーで管理ポイントのモバイル デバイス管理を有効にするときの構成データを記録します。|サイト システム サーバー|  
|DMPSetup.log|モバイル デバイスに対して有効になっている場合に管理ポイントの構成を記録します。|サイト システム サーバー|  
|DmpSoftware.log|モバイル デバイス管理が有効になっている管理ポイントのモバイル デバイス レガシ クライアントのソフトウェア配布データをすべて記録します。|サイト システム サーバー|  
|DmpStatus.log|モバイル デバイス管理が有効になっている管理ポイントのモバイル デバイス レガシ クライアントのステータス メッセージ データをすべて記録します。|サイト システム サーバー|  
|DmSvc.log|モバイル デバイス レガシ クライアントからの、モバイル デバイス管理が有効になっている管理ポイントへのクライアント接続を記録します。|クライアント|  
|FspIsapi.log|モバイル デバイス レガシ クライアントとクライアント コンピューターからのフォールバック ステータス ポイントへの通信に関する詳細を記録します。|サイト システム サーバー|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a> OS の展開

次の表に、OS の展開に関係のある情報を含むログ ファイルをリストします。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|CAS.log|配布ポイントで参照コンテンツが検出されたときに詳細情報を記録します。|クライアント|  
|ccmsetup.log|クライアントのセットアップ、クライアントのアップグレード、およびクライアントの削除に関する ccmsetup のタスクを記録します。 クライアントのインストールのトラブルシューティングに使用できます。|クライアント|  
|CreateTSMedia.log|タスク シーケンス メディアの作成の詳細を記録します。|Configuration Manager コンソールを実行しているコンピューター|  
|Dism.log|オフライン サービス用のドライバーのインストールまたは更新プログラムの適用操作を記録します。|サイト システム サーバー|  
|distmgr.log|配布ポイントをブート前実行環境 (PXE) 用に有効にする構成の詳細を記録します。|サイト システム サーバー|  
|DriverCatalog.log|ドライバー カタログにインポートされているデバイス ドライバーの詳細を記録します。|サイト システム サーバー|  
|mcsisapi.log|マルチキャスト パッケージの転送とクライアント要求への応答に関する情報を記録します。|サイト システム サーバー|  
|mcsexec.log|正常性チェック、名前空間、セッションの作成、証明書の確認操作を記録します。|サイト システム サーバー|  
|mcsmgr.log|構成、セキュリティ モード、可用性の変化を記録します。|サイト システム サーバー|  
|mcsprv.log|マルチキャスト プロバイダーと Windows 展開サービス (WDS) のやり取りを記録します。|サイト システム サーバー|  
|MCSSetup.log|マルチキャスト サーバーの役割のインストールの詳細を記録します。|サイト システム サーバー|  
|MCSMSI.log|マルチキャスト サーバーの役割のインストールの詳細を記録します。|サイト システム サーバー|  
|Mcsperf.log|マルチキャスト パフォーマンス カウンターの更新の詳細を記録します。|サイト システム サーバー|  
|MP_ClientIDManager.log|タスク シーケンスで PXE またはブート メディアから開始される、クライアント ID 要求への管理ポイントの応答を記録します。|サイト システム サーバー|  
|MP_DriverManager.log|ドライバーの自動適用を要求するタスク シーケンス アクションへの管理ポイントの応答を記録します。|サイト システム サーバー|  
|OfflineServicingMgr.log|オフライン サービスのスケジュールと、オペレーティング システムの Windows Imaging Format (WIM) ファイルへの更新プログラムの適用操作を記録します。|サイト システム サーバー|  
|Setupact.log|Windows Sysprep とセットアップのログの詳細を記録します。 詳細については、[ログ ファイル](https://docs.microsoft.com/windows/deployment/upgrade/log-files)に関するページを参照してください。|クライアント|  
|Setupapi.log|Windows Sysprep とセットアップのログの詳細を記録します。|クライアント|  
|Setuperr.log|Windows Sysprep とセットアップのログの詳細を記録します。|クライアント|  
|smpisapi.log|クライアントの状態のキャプチャと復元操作、およびしきい値の詳細を記録します。|クライアント|  
|Smpmgr.log|状態移行ポイントの正常性チェックの結果と構成の変更の詳細を記録します。|サイト システム サーバー|  
|smpmsi.log|状態移行ポイントのインストールと構成の詳細を記録します。|サイト システム サーバー|  
|smpperf.log|状態移行ポイントのパフォーマンス カウンターの更新を記録します。|サイト システム サーバー|  
|smspxe.log|PXE ブートを使用するクライアントへの応答と、ブート イメージとブート ファイルの展開の詳細を記録します。|サイト システム サーバー|  
|smssmpsetup.log|状態移行ポイントのインストールと構成の詳細を記録します。|サイト システム サーバー|
| SMS_PhasedDeployment.log| 段階的展開のログ ファイル|Configuration Manager 階層の最上位サイト|
|Smsts.log|タスク シーケンスによる操作を記録します。|クライアント|  
|TSAgent.log|タスク シーケンス開始前の依存関係の解決結果を記録します。|クライアント|  
|TaskSequenceProvider.log|タスク シーケンスがインポート、エクスポート、または編集されたときの詳細を記録します。|サイト システム サーバー|  
|loadstate.log|ユーザー状態移行ツール (USMT)、およびユーザー状態データの回復の詳細を記録します。|クライアント|  
|scanstate.log|ユーザー状態移行ツール (USMT)、およびユーザー状態データのキャプチャの詳細を記録します。|クライアント|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a> 電源管理

次の表に、電源管理に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|クライアント コンピューターの電源管理操作の詳細を記録します。これには、電源管理クライアント エージェントによる電源管理設定の監視と適用が含まれます。|クライアント|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a> リモート コントロール

次の表に、リモート コントロールに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|リモート コントロール ビューアーの処理に関する情報を記録します。|リモート コントロール ビューアーを実行するコンピューターの %temp% フォルダー|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a> レポート

次の表に、レポートに関係のある情報を含む Configuration Manager ログ ファイルを一覧します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|srsrp.log|レポート サービス ポイントの動作とステータスに関する情報を記録します。|サイト システム サーバー|  
|srsrpMSI.log|MSI によるレポート サービス ポイントのインストール プロセスの出力結果を含みます。|サイト システム サーバー|  
|srsrpsetup.log|レポート サービス ポイントのインストール プロセスの結果を記録します。|サイト システム サーバー|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a> 役割に基づいた管理

次の表に、役割に基づいた管理に関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|hman.log|サイトの構成の変更と、Active Directory Domain Services でのサイト情報の発行を記録します。|サイト サーバー|  
|SMSProv.log|WMI プロバイダーからのサイト データベースへのアクセスを記録します。|SMS プロバイダーのあるコンピューター|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a> ソフトウェア使用状況測定

次の表に、ソフトウェア使用状況測定に関連する情報を含むログ ファイルをリストします。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|ソフトウェア使用状況測定プロセスを記録します。|サイト サーバー|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a> ソフトウェア更新プログラム

次の表に、ソフトウェアの更新プログラムに関連する情報を含むログ ファイルを一覧表示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|AlternateHandler.log|Microsoft 365 Apps for enterprise クライアントの更新プログラムをダウンロードしてインストールするために、クライアントで Office クイック実行 COM インターフェイスが呼び出されたときに詳細を記録します。 Windows 更新プログラムをダウンロードしてインストールするために Windows Update エージェント API を呼び出すときの、WuaHandler の使用と似ています。<!-- SCCMDocs#888 -->|クライアント|
|Ccmperf.log|メンテナンス操作、およびクライアントのパフォーマンス カウンターに関連するデータの取得操作を記録します。|クライアント|
|DeltaDownload.log|配信の最適化を使用してダウンロードされた高速更新プログラムと更新プログラムのダウンロードに関する情報が記録されます。|クライアント|  
|PatchDownloader.log|更新プログラムのソースから、ソフトウェア更新プログラムをサイト サーバーにダウンロードするプロセスの詳細を記録します。|更新プログラムを手動でダウンロードする場合、このログ ファイルは、コンソールを実行しているコンピューターでコンソールを実行しているユーザーの %temp% ディレクトリに配置されます。 自動展開規則では、ConfigMgr クライアントがサイト サーバーにインストールされている場合、このログ ファイルはサイト サーバーの %windir%\CCM\Logs に配置されます。|  
|PolicyEvaluator.log|ソフトウェア更新プログラムのポリシーを含む、クライアント コンピューターのポリシーの評価の詳細を記録します。|クライアント|  
|RebootCoordinator.log|ソフトウェア更新プログラムがインストールされた後のシステムの再起動の調整に関する詳細を記録します。|クライアント|  
|ScanAgent.log|ソフトウェア更新プログラムのスキャン要求、WSUS の場所、および関連する操作の詳細を記録します。|クライアント|  
|SdmAgent.log|コンプライアンス対応状態と修復の追跡情報を記録します。 ただし、ソフトウェア更新プログラムのログ ファイル (Updateshandler.log) に、コンプライアンス対応に必要なソフトウェア更新プログラムのインストールのより詳しい情報が記録されます。 このログ ファイルは、コンプライアンス設定で共有されます。|クライアント|  
|ServiceWindowManager.log|メンテナンス期間の評価の詳細を記録します。|クライアント|
|SMS_ISVUPDATES_SYNCAGENT.log| サードパーティのソフトウェア更新プログラムを同期するためのログ ファイルです。| Configuration Manager 階層内の最上位のソフトウェア更新ポイント。|
|SMS_OrchestrationGroup.log| オーケストレーション グループのログ ファイル|サイト サーバー|
|SmsWusHandler.log|Microsoft 更新プログラム用インベントリ ツールのスキャン プロセスの詳細を記録します。|クライアント|  
|StateMessage.log|作成されて管理ポイントに送信されたソフトウェア更新プログラムの状態メッセージの詳細を記録します。|クライアント|  
|SUPSetup.log|ソフトウェアの更新ポイントのインストールに関する詳細を記録します。 ソフトウェアの更新ポイントのインストールが完了すると、このログ ファイルに「 **Installation was successful** 」と書き込まれます。|サイト システム サーバー|  
|UpdatesDeployment.log|ソフトウェア更新プログラムのクライアントへの展開の詳細 (アクティブ化と評価、強制実行など) を記録します。 ログ記録のレベルを "詳細" にしている場合は、クライアント ユーザー インターフェイスとの相互動作に関する情報も含まれます。|クライアント|  
|UpdatesHandler.log|ソフトウェア更新プログラムのコンプライアンス スキャン、およびソフトウェア更新プログラムのダウンロードとクライアントへのインストールの詳細を記録します。|クライアント|  
|UpdatesStore.log|コンプライアンス スキャンで評価された更新プログラムとのコンプライアンス対応状態の詳細を記録します。|クライアント|  
|WCM.log|ソフトウェアの更新ポイントの構成に関する情報、およびサブスクライブ済みの更新カテゴリ、分類、言語のための WSUS サーバーへの接続に関する情報を記録します。|サイト サーバー|  
|WSUSCtrl.log|サイトの WSUS サーバーの構成、データベース接続、正常性に関する詳細を記録します。|サイト システム サーバー|  
|wsyncmgr.log|ソフトウェア更新プログラムの同期プロセスの詳細を記録します。|サイト サーバー|  
|WUAHandler.log|クライアントの Windows 更新エージェントによるソフトウェア更新プログラムの検索に関する詳細を記録します。|クライアント|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a> Wake On LAN

次の表に、Wake On LAN の使用に関係のある情報を含むログ ファイルを示します。  

> [!NOTE]  
> ウェイクアップ プロキシを使用して Wake On LAN を補うと、この処理がクライアントに記録されます。 たとえば、この記事の「[クライアントによる処理](#BKMK_ClientOpLogs)」セクションの CcmExec.log と SleepAgent_<*domain*\>@SYSTEM_0.log をご覧ください。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|ウェイクアップ パケットの送信先クライアント、送信したウェイクアップ パケットの数、ウェイクアップ パケット送信の再試行回数を記録します。|サイト サーバー|  
|wolmgr.log|ウェイクアップ手順 (Wake On LAN 用に構成されている展開の開始日時など) の詳細を記録します。|サイト サーバー|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a> Windows 10 サービス

次の表に、Windows 10 サービスに関係のある情報を含むログ ファイルの一覧を示します。  
サービスにはソフトウェア更新プログラムと同じインフラストラクチャとプロセスが使用されます。 サービス シナリオに適用できるその他のログについては、「[ソフトウェア更新プログラム](#BKMK_SU_NAPLog)」を参照してください。

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|CBS.log|Windows Update またはロールと機能の変更に関連したサービスのエラーを記録します。|クライアント|
|DISM.log|DISM を使用するすべてのアクションを記録します。 必要に応じて、詳細情報について DISM.log から CBS.log が示されます。|クライアント|
|setupact.log|Windows インストール プロセス中に発生するほとんどのエラーのプライマリ ログ ファイルです。 このログ ファイルは、%windir%\$Windows.~BT\sources\panther フォルダーにあります。|クライアント|

詳細については、「[Online Servicing-Related Log Files (オンライン サービス関連のログ ファイル)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files)」を参照してください。

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a> Windows 更新エージェント

次の表に、Windows 更新エージェントのインストールに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Windows 更新エージェントが、いつ WSUS サーバーに接続してコンプライアンス評価用のソフトウェア更新プログラムを取得したかと、エージェント コンポーネントの更新プログラムがあるかどうかを記録します。|クライアント|  

詳細については、「[Windows Update のログ ファイル](https://docs.microsoft.com/windows/deployment/update/windows-update-logs)」を参照してください。

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a> WSUS サーバー

次の表に、WSUS サーバーに関係のある情報を含むログ ファイルを示します。  

|ログの名前|[説明]|ログ ファイルのあるコンピューター|  
|--------------|-----------------|----------------------------|  
|Change.log|WSUS サーバーのデータベース情報の変更を記録します。|WSUS サーバー|  
|SoftwareDistribution.log|構成済みの更新プログラムのソースから、WSUS サーバーのデータベースと同期された更新プログラムの詳細を記録します。|WSUS サーバー|  

これらのログ ファイルは、`%ProgramFiles%\Update Services\LogFiles` フォルダーにあります。

## <a name="see-also"></a>関連項目

- [ログ ファイルについて](about-log-files.md)

- [サポート センターの OneTrace](../../support/support-center-onetrace.md)

- [サポート センター ログ ファイル ビューアー](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
