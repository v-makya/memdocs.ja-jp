---
title: 新バージョン 1610
titleSuffix: Configuration Manager
description: Configuration Manager のバージョン 1610 で導入された変更点および新機能について説明します。
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d154dc0ba681a37ebb2155bfa1bcdb6d8734965f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073961"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Configuration Manager のバージョン 1610 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1610 は、バージョン 1511、1602、または 1606 を実行しているインストール済みのサイトで、コンソール内の更新プログラムとして利用可能です。


> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用する必要があります。  
>
> 詳細については、下記のリンクをクリックしてください。    
> - [新しいサイトのインストール](https://technet.microsoft.com/library/mt590197.aspx)  
> - [サイトで更新プログラムをインストールする](https://technet.microsoft.com/library/mt607046.aspx)  
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)

以降のセクションでは、Configuration Manager のバージョン 1610 の変更点および導入された新機能について詳しく説明します。  


## <a name="in-console-monitoring-of-update-installation-status"></a>更新プログラムのインストール状態をコンソール内で監視する  
バージョン 1610 以降、更新プログラム パックをインストールし、コンソールでインストールを監視すると、 **[インストール後]** という新しいフェーズが表示されるようになります。 このフェーズには、主要なサービスの再起動、レプリケーション監視の初期化など、タスクの状態が含まれます (このフェーズを使用するには、サイトをバージョン 1610 に更新する必要があります)。更新プログラムのインストール状態の詳細については、「[Install in-console updates](../../servers/manage/install-in-console-updates.md#bkmk_install)」(コンソール内の更新プログラムのインストール) を参照してください。


## <a name="exclude-clients-from-automatic-upgrade"></a>自動アップグレードからクライアントを除外する
新しいバージョンのクライアント ソフトウェアで、自動アップグレードから Windows クライアントを除外することができます。 除外するには、アップグレードから除外するように指定したコレクションにクライアント コンピューターを含めます。 除外されるコレクションのクライアントは、クライアント ソフトウェアを更新する要求を無視します。  詳細については、「[Exclude Windows clients from upgrades](../../clients/manage/upgrade/exclude-clients-windows.md)」(アップグレードから Windows クライアントを除外する) を参照してください。


## <a name="improvements-for-boundary-groups"></a>境界グループの機能強化
バージョン 1610 では、境界グループとそれらが配布ポイントを扱う方法に重要な変更が加えられています。 これらの変更によって、コンテンツ インフラストラクチャの設計が単純化されると共に、クライアントがいつどのようにフォールバックしてコンテンツ ソースの場所となる他の配布ポイントを検索するかをより細かく制御することができます。 これには、オンプレミスとクラウド ベースの配布ポイントの両方が含まれます。
従来からある概念や動作は、これらの機能強化によって一新されます (配布ポイントの [高速] と [低速] の構成など)。 セットアップとメンテナンスは、新しいモデルによって省力化されると考えられます。 これらの変更も、境界グループに関連付けるその他のサイト システムの役割を向上させる将来の変更のための基礎です。

バージョン 1610 への更新時に、これらの変更が既存のコンテンツの配布の構成を妨げないように、アップグレードによって現在の境界グループ構成が新しいモデルに適合するように変換されます。

詳細については、「[境界グループ](../../servers/deploy/configure/boundary-groups.md)」を参照してください。


## <a name="peer-cache-for-content-distribution-to-clients"></a>クライアントへのコンテンツ配布のピア キャッシュ
バージョン 1610 より、クライアントの**ピア キャッシュ**をリモート クライアントへのコンテンツ展開の管理に使用できるようになりました。 クライアントがローカル キャッシュから直接他のクライアントとコンテンツを共有するための組み込みの Configuration Manager ソリューションである、ピア キャッシュです。

ピア キャッシュを有効にするクライアント設定をコレクションに展開すると、そのコレクションのメンバーは同じ境界グループ内の他のクライアントのピア コンテンツ ソースとして動作できます。

また、新しい**クライアント データ ソース** ダッシュボードを使用して、環境内のピア キャッシュ コンテンツ ソースの使用状況を把握することもできます。

> [!TIP]  
> バージョン 1610 では、ピア キャッシュとクライアント データ ソースのダッシュボードは、プレリリース機能です。 有効にするには、「[更新プログラムからのプレリリース機能の使用](../../servers/manage/install-in-console-updates.md#bkmk_prerelease)」をご覧ください。

詳細については、「[Configuration Manager クライアントのピア キャッシュ](../hierarchy/client-peer-cache.md)」と「[クライアント データ ソース ダッシュボード](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)」を参照してください。


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>複数の共有配布ポイントを同時に移行する
**配布ポイントを再割り当てする**オプションを利用し、Configuration Manager に、最大 50 の共有配布ポイントの同時再割り当てを並列処理させることができます。 このリリースの前のバージョンでは、再割り当てされた配布ポイントは、同時に処理されていました。 詳細については、「[複数の共有配布ポイントを同時に移行する](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time)」を参照してください。

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>インターネットベースのクライアントを管理するためのクラウド管理ゲートウェイ

クラウド管理ゲートウェイは、インターネット上で Configuration Manager クライアントを管理する簡単な方法を提供します。 Microsoft Azure にデプロイされ、Azure サブスクリプションを必要とするクラウド管理ゲートウェイ サービスは、クラウド管理ゲートウェイ接続ポイントと呼ばれる新しい役割を使用して、オンプレミスの Configuration Manager インフラストラクチャに接続します。 完全にデプロイされ、構成されると、クライアントは内部のプライベート ネットワークに接続しているかどうか、またはインターネット上にあるかどうかに関係なく、オンプレミスの Configuration Manager サイト システムの役割およびクラウドベースの配布ポイントと通信できるようになります。 詳細と、クラウド管理ゲートウェイがインターネットベースのクライアント管理を比較する方法については、「[Manage clients on the Internet](../../clients/manage/manage-clients-internet.md)」(インターネット上のクライアントの管理) を参照してください。

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Windows 10 のエディションのアップグレード ポリシーの改善
このリリースでは、次の機能強化がこのポリシーの種類に加えられています。

- Microsoft Intune に登録された Windows 10 PC に加え、Configuration Manager クライアントを実行している Windows 10 PC で、エディションのアップグレード ポリシーを使用できるようになりました。
- Windows 10 Professional から、ハードウェアと互換性がある、ウィザードのプラットフォームのいずれかにアップグレードすることができます。

## <a name="manage-hardware-identifiers"></a>ハードウェア ID の管理
PXE ブートとクライアント登録で Configuration Manager が無視するハードウェア ID の一覧を指定できるようになりました。 それにより 2 つの一般的な問題に対処できます。

1. Surface Pro 3 など、デバイスの多くにオンボード イーサネット ポートが含まれません。 オペレーティング システムの展開で有線接続を確立するとき、一般的に USB/イーサネット アダプターが使用されます。 しかしながら、コストや汎用性に起因し、多くの場合、共有アダプターになります。 そのアダプターの MAC アドレスを利用してデバイスを識別するため、展開ごとに管理者による追加措置がないと、アダプターの再利用が問題になります。 Configuration Manager Version 1610 では、このアダプターの MAC アドレスを除外できます。そのため、このシナリオで簡単に再利用できます。
2. SMBIOS ID は一意のハードウェア識別子ですが、専門的なハードウェア デバイスには ID が重複するものもあります。 この問題は、前述の USB/イーサネット アダプターのシナリオほどよく起こることではありませんが、除外するハードウェア ID の一覧を使用することによって解決できます。

詳細については、「[Manage duplicate hardware identifiers](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)」(重複するハードウェア識別子を管理する) を参照してください。

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>ビジネス向け Windows ストアと Configuration Manager のとの統合の強化
このリリースの変更点:
- 以前は、ビジネス向け Windows ストアから無料のアプリの展開のみができました。 さらに、Configuration Manager で有償のオンライン ライセンス付きアプリ (Intune に登録されているデバイスのみ) も展開できるようになりました。
- ビジネス向け Windows ストアと Configuration Manager との即時同期を開始できるようになりました。
- Azure Active Directory から取得したクライアントの秘密鍵を変更できるようになりました。
- ストアに対するサブスクリプションを削除できるようになりました。

詳細については、[Configuration Manager でのビジネス向け Microsoft Store のアプリの管理](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)に関する記事を参照してください。


## <a name="policy-sync-for-intune-enrolled-devices"></a>Intune に登録されたデバイスのポリシー同期
デバイス自体のポータル サイト アプリから同期を要求するのではなく、Configuration Manager コンソールから Intune に登録されたデバイスのポリシー同期を要求できるようになりました。 同期要求の状態に関する情報は、デバイス ビュー内に 「**Remote Sync State**」 (リモート同期の状態) と呼ばれる新しい列として表示されます。 この情報は、各デバイスの **[プロパティ]** ダイアログ ボックスの [探索データ] セクションにも表示されます。


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>コンプライアンス設定を使用して Windows Defender 設定を構成する
Configuration Manager コンソールの構成項目を使用して、Intune に登録されている Windows 10 コンピューターで Windows Defender クライアント設定を構成できるようになりました。
詳細については、[Configuration Manager クライアントを使用せずに管理されている Windows 8.1 デバイスと Windows 10 デバイスの構成項目の作成](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)に関する記事の「**Windows Defender**」セクションを参照してください。



## <a name="general-improvements-to-software-center"></a>ソフトウェア センターの全般的な機能強化
- ユーザーは、ソフトウェア センターだけでなく、アプリケーション カタログからアプリを要求できるようになりました。
- 新規のソフトウェアと関連性のあるソフトウェアを把握しやすくなりました。

## <a name="new-columns-in-device-collection-views"></a>デバイス コレクション ビューの新しい列
デバイス コレクション ビューで **IMEI** と**シリアル番号** (iOS デバイス) の列を表示できるようになりました。

## <a name="customizable-branding-for-software-center-dialogs"></a>ソフトウェア センター ダイアログにおけるカスタマイズ可能なブランド
ソフトウェア センターのカスタム ブランド設定は、Configuration Manager バージョン 1602 で導入されました。 バージョン 1610 では、ソフトウェア センターのユーザーにより一貫性のあるエクスペリエンスを提供するため、このブランド設定が関連するすべてのダイアログ ボックスに拡張されています。

ソフトウェア センターのカスタム ブランド設定は、次の規則に従って適用されます。

- アプリケーション カタログ Web サイトのポイント サイト サーバーの役割がインストールされていない場合は、 **[ソフトウェア センターに表示される組織名]** という **[コンピューター エージェント]** クライアント設定で指定された組織名がソフトウェア センターに表示されます。 手順については、「[クライアント設定を構成する方法](../../clients/deploy/configure-client-settings.md)」をご覧ください。

- アプリケーション カタログ Web サイトのポイント サイト サーバーの役割がインストールされている場合は、アプリケーション カタログ Web サイトのポイント サイト サーバーの役割プロパティに指定されている組織名と色がソフトウェア センターに表示されます。 詳細については、「[Configuration options for Application Catalog website point](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)」(アプリケーション カタログ Web サイト ポイントの構成オプション) をご覧ください。

- Microsoft Intune サブスクリプションが構成されていて Configuration Manager 環境に接続されている場合は、Intune サブスクリプションのプロパティに指定されている組織名、色、および会社のロゴがソフトウェア センターに表示されます。


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>必要なアプリケーションとソフトウェア更新プログラムを展開するための適用猶予期間
場合によっては、必要なアプリケーション展開またはソフトウェア更新プログラムをインストールできるように、設定期限よりも長い時間をユーザーに与える必要があります。 これは、たとえばコンピューターが長期間オフになっていて、多数のアプリケーションや更新プログラムの展開をインストールする必要がある場合に必要になります。 たとえば、エンド ユーザーが休暇から戻って来たばかりの場合、期限切れのアプリケーションの展開がインストールされるまで、長時間待たなければならない場合があります。 この問題を解決するため、Configuration Manager クライアント設定をコレクションに展開することで、適用猶予期間を定義できるようになりました。 

猶予期間を設定するには、次の操作を実行します。
1. クライアント設定の **[コンピューター エージェント]** ページで、新しいプロパティ **[展開期限後の実施の猶予期間 (時間)]** の値を **1** ～ **120** 時間で設定します。
2. 新しい必須アプリケーションの展開または既存の展開のプロパティの **[スケジュール]** ページで、 **[Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings (ユーザー設定に従い、クライアント設定で定義された猶予期間が終了するまでこの展開の実施を延期する)]** チェック ボックスをオンにします。 このチェック ボックスがオンになっていて、クライアント設定も展開するデバイスを対象としているすべての展開が、適用猶予期間を使用します。

適用猶予期間を構成し、チェック ボックスをオンにすると、アプリケーションのインストール期限になると、ユーザーがその猶予期間までに設定した最初の非ビジネス ウィンドウで、アプリケーションがインストールされます。 ただし、ユーザーはソフトウェア センターを開いて、いつでもアプリケーションをインストールすることもできます。 猶予期間が切れると、適用は期限切れの展開に対する通常の動作に戻ります。 ソフトウェア更新プログラムの展開ウィザード、自動展開規則の作成ウィザード、およびプロパティ ページに、同様のオプションが追加されています。



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>必要なソフトウェアに関するダイアログ ボックスで改善された機能
ユーザーが必要なソフトウェアを受け取ったときに、 **[次の時間が経過したら再通知する]** 設定で、次のドロップダウン リストから値を選択できます。 
- **[後で]** : クライアント エージェント設定で構成されている通知の設定に基づいて通知をスケジュールすることを指定します。
- **[定時]** : 選択した時間後にもう一度通知を表示するように指定します (30 分後など)。

![クライアント エージェント設定の [コンピューター エージェント] ページ](media/client-notification-settings.png)

最大の再通知時間は、クライアント エージェント設定で構成された値に基づきます。 たとえば、[コンピューター エージェント] ページで **[Deployment deadline greater than 24 hours, remind users every (hours) (展開期限まで 24 時間以上の場合に、ユーザーに通知する間隔 (時間))]** 設定が 10 時間に設定されていて、期限まで 24 時間以上ある場合は、ユーザーに最大で 10 時間以内の再通知を設定するオプションが表示されます。 期限が近づくにつれ、展開タイムラインの各コンポーネントに関連するクライアント エージェント設定に合わせて、選択できるオプションが減っていきます。

さらに、オペレーティング システムを展開するタスク シーケンスなど、危険度の高い展開に対しては、ユーザー通知のエクスペリエンスがより煩わしいものになりました。 一時的なタスク バーの代わりに、重要なソフトウェア メンテナンスが必要なことがユーザーに通知されるたび、次のようなダイアログ ボックスがユーザーのコンピューターに表示されます。

![必要なソフトウェアのダイアログ](media/client-toast-notification.png)


詳細情報:
- [危険度の高い展開を管理するための設定](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [クライアント設定を構成する方法](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>ソフトウェア更新プログラム ダッシュボード
新しいソフトウェア更新プログラム ダッシュボードを使用すると、組織内にあるデバイスの現在のコンプライアンス状態を確認し、データをすばやく分析して危険な状態のデバイスを確認できます。 ダッシュボードを表示するには、 **[監視]**  >  **[概要]**  >  **[セキュリティ]**  >  **[ソフトウェア更新プログラム ダッシュボード]** に移動します。

詳細については、「[Monitor software updates](../../../sum/deploy-use/monitor-software-updates.md)」(ソフトウェア更新プログラムの監視) を参照してください。


## <a name="improvements-to-the-application-request-process"></a>アプリケーション要求プロセスの改善
アプリケーションのインストールを承認した後は、要求を拒否するには、Configuration Manager コンソールで **[拒否]** をクリックします。 以前は、承認後にこのボタンが淡色表示されていました。

この操作で、アプリケーションがデバイスからアンインストールされることはありませんが、 ユーザーはソフトウェア センターからアプリケーションの新しいコピーをインストールできなくなります。

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>自動展開規則でコンテンツのサイズでフィルター処理する
自動展開規則でソフトウェア更新プログラムのコンテンツのサイズでフィルター処理できるようになりました。 たとえば、2 MB 未満のソフトウェア更新プログラムだけをダウンロードするには、 **[コンテンツ サイズ (KB)]** フィルターを **[< 2048]** に設定します。 ネットワーク帯域幅が制限されている場合に、下位レベルの簡素化された Windows サービスのよりよいサポートのため、このフィルターを使用して、サイズの大きいソフトウェア更新プログラムが自動的にダウンロードされるのを防止します。 詳細については、以下を参照してください。
- [Configuration Manager と下位レベルのオペレーティング システムでの簡素化された Windows サービス](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [ソフトウェア更新プログラムの自動展開](../../../sum/deploy-use/automatically-deploy-software-updates.md)

**[コンテンツ サイズ (KB)]** フィールドを構成するには、次のいずれかを実行します。
- 自動展開規則を作成するときに、自動展開規則の作成ウィザードの **[ソフトウェア更新プログラム]** ページにアクセスします。
- 既にある自動展開規則のプロパティの **[ソフトウェア更新プログラム]** タブにアクセスします。

## <a name="office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボード
Configuration Manager コンソールで Office 365 クライアント管理ダッシュボードを使用できるようになりました。 このダッシュボードを表示するには、 **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[Office 365 クライアント管理]** に移動します。

ダッシュボードには、次のチャートが表示されます。

- Office 365 クライアントの数
- Office 365 クライアントのバージョン
- Office 365 クライアントの言語
- Office 365 クライアントのチャネル     

詳細については、[Office 365 ProPlus の更新プログラムの管理](../../../sum/deploy-use/manage-office-365-proplus-updates.md)に関するページを参照してください。

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>BIOS からUEFI への変換を管理するためのタスク シーケンス手順
**コンピューターの再起動**のステップで、UEFI に移行するためにハード ドライブに FAT32 パーティションを準備するため、新しい変数 TSUEFIDrive を使用して、オペレーティング システムの展開タスク シーケンスをカスタマイズできるようになりました。 次の手順では、タスク シーケンスのステップを作成して BIOS からUEFI への変換のためにハード ドライブを準備する方法の例を示します。 詳細については、「[BIOS から UEFI への変換を管理するためのタスク シーケンス手順](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md)」を参照してください。

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>タスク シーケンス ステップの向上:Prepare ConfigMgr Client for Capture  
ConfigMgr クライアントの準備手順で、キー情報だけではなく、Configuration Manager クライアントが完全に削除されるようになりました。 タスク シーケンスでキャプチャしたオペレーティング システム イメージを展開すると、毎回新しい Configuration Manager クライアントがインストールされます。 詳細については、「[Task sequence steps](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)」(タスク シーケンスのステップ) を参照してください。



## <a name="intune-compliance-policy-charts"></a>Intune コンプライアンス ポリシー グラフ
Configuration Manager コンソールの **[監視]** ワークスペースで新しいチャートを使用して、デバイスの全体の準拠と非準拠の主な理由をすばやく表示することができるようになりました。 いずれかのチャートのセクションをクリックすると、そのカテゴリ内のデバイスのリストまでドリル ダウンすることができます。 詳細については、「[Monitor the compliance policy](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)」(コンプライアンス ポリシーの監視) を参照してください。


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>iOS デバイスと Android デバイスを保護するハイブリッド実装のための Lookout 統合
Microsoft は、デバイス上のマルウェアやリスクの高いアプリなどを検出して iOS および Android モバイル デバイスを保護するため、Lookout のモバイル脅威保護ソリューションに統合しています。 Lookout のソリューションにより、構成可能な脅威レベルを決定できます。 Lookout によるリスク評価に基づいてデバイスのコンプライアンスを判断するためのコンプライアンス ポリシー規則を、Configuration Manager に作成できます。 条件付きアクセス ポリシーを使用すると、デバイスのコンプライアンス状態に基づいて、会社のリソースへのアクセスを許可したりブロックしたりできます。

コンプライアンスを満たしていない iOS デバイスのユーザーには登録が求められます。 会社のデータへのアクセス権を得るにはデバイスへの Lookout for Work アプリのインストール、アプリのアクティブ化、Lookout for Work アプリケーションで報告された脅威の修復が必要となります。


## <a name="new-compliance-settings-for-configuration-items"></a>構成アイテムの新しいコンプライアンス設定
さまざまなデバイス プラットフォームの構成アイテムで使用できる多くの新しい設定が追加されました。 これらの設定は、以前はスタンドアロン構成での Microsoft Intune にありましたが、Intune を Configuration Manager で使用する際にも使用できるようになりました。
詳細については、「[Configuration Manager クライアントを使用せずに管理されているデバイスの構成項目](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)」を参照してください。

### <a name="new-settings-for-android-devices"></a>Android デバイス向けの新しい設定
#### <a name="password-settings"></a>パスワードの設定
- **パスワードの履歴を記憶する**
- **指紋によるロック解除を使用する**

#### <a name="security-settings"></a>セキュリティ設定
- **メモリ カードの暗号化を必要とする**
- **画面のキャプチャを許可する**
- **診断データの送信を使用する**

#### <a name="browser-settings"></a>ブラウザーの設定
- **Web ブラウザーを許可する**
- **オートコンプリートを使用する**
- **ポップアップ ブロックを使用する**
- **Cookie を使用する**
- **アクティブ スクリプティングを使用する**

#### <a name="app-settings"></a>アプリの設定
- **Google Play ストアを使用する**

#### <a name="device-capability-settings"></a>デバイスの機能の設定
- **リムーバブル記憶域を許可する**
- **Wi-Fi テザリングを許可する**
- **位置情報を許可する**
- **NFC を許可する**
- **Bluetooth を許可する**
- **音声通話ローミングを許可する**
- **データ ローミングを許可する**
- **SMS/MMS メッセージングを許可する**
- **音声アシスタントを使用する**
- **音声による発信を使用する**
- **コピーと貼り付けを許可する**

### <a name="new-settings-for-ios-devices"></a>iOS デバイスの新しい設定
#### <a name="password-settings"></a>パスワードの設定
- **パスワードに必要な複雑な文字の数**
- **単純なパスワードを許可する**
- **パスワードが必要になるまでの非アクティブ状態の時間 (分)**
- **パスワードの履歴を記憶する**

### <a name="new-settings-for-mac-os-x-devices"></a>Mac OS X デバイスの新しい設定
#### <a name="password-settings"></a>パスワードの設定
- **パスワードに必要な複雑な文字の数**
- **単純なパスワードを許可する**
- **パスワードの履歴を記憶する**
- **スクリーンセーバーがアクティブになるまでの非アクティブな時間 (分)**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Windows 10 デスクトップおよびモバイル デバイスの新しい設定
#### <a name="password-settings"></a>パスワードの設定
- **文字セットの最小数**
- **パスワードの履歴を記憶する**
- **デバイスがアイドル状態から戻るときにパスワードを必須とする**

#### <a name="security-settings"></a>セキュリティ設定
- **モバイル デバイスの暗号化を要求する**
- **手動での登録解除を許可する**

#### <a name="device-capability-settings"></a>デバイスの機能の設定
- **移動体通信で VPN を許可する**
- **移動体通信で VPN ローミングを許可する**
- **電話リセットを許可する**
- **USB 接続を許可する**
- **Cortana を許可する**
- **アクション センターの通知を許可する**

### <a name="new-settings-for-windows-10-team-devices"></a>Windows 10 Team デバイスの新しい設定
#### <a name="device-settings"></a>デバイスの設定
- **Azure Operational Insights を有効にする**
- **Miracast ワイヤレス投影を有効にする**
- **[ようこそ] 画面に表示される会議の情報を選択する**
- **ロック画面の背景画像 URL**

### <a name="new-settings-for-windows-81-devices"></a>Windows 8.1 デバイスの新しい設定
#### <a name="applicability-settings"></a>適用性の設定
- **Windows 10 にすべての構成を適用する**

#### <a name="password-settings"></a>パスワードの設定
- **必要なパスワードの種類**
- **文字セットの最小数**
- **最小のパスワードの長さ**
- **デバイスをワイプするまでの連続サインイン エラーの数**
- **画面がオフになるまでの非アクティブな時間 (分)**
- **パスワードの有効期限 (日)**
- **パスワードの履歴を記憶する**
- **前のパスワードの再利用を防止**
- **ピクチャ パスワードと PIN を許可する**

#### <a name="browser-settings"></a>ブラウザーの設定
- **イントラネット ネットワークの自動検出を使用する**

### <a name="new-settings-for-windows-phone-81-devices"></a>Windows Phone 8.1 デバイスの新しい設定
#### <a name="applicability-settings"></a>適用性の設定
- **Windows 10 にすべての構成を適用する**

#### <a name="password-settings"></a>パスワードの設定
- **文字セットの最小数**
- **単純なパスワードを許可する**
- **パスワードの履歴を記憶する**

#### <a name="device-capability-settings"></a>デバイスの機能の設定
- **無料 Wi-Fi スポットへの自動接続を許可する**
