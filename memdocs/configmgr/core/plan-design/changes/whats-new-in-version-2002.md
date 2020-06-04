---
title: バージョン 2002 の新機能
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch のバージョン 2002 で導入された変更点および新機能について説明します。
ms.date: 05/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: afdcc608133d306042c9c6dc817396bb2fc3f387
ms.sourcegitcommit: b0ae4a9972bac3518d0d4f33e033ac492eefe3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84126483"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch のバージョン 2002 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 2002 はコンソール内の更新プログラムとして利用できます。 バージョン 1810 以降が実行されているサイトで、この更新プログラムを適用します。 <!-- baseline only statement:-->新しいサイトをインストールするときにも基準のバージョンとしても利用できます。 この記事では、Configuration Manager バージョン 2002 での変更点と新機能をまとめます。

この更新プログラムをインストールするための最新のチェックリストを常に確認してください。 詳細については「[更新プログラム 2002 をインストールするためのチェックリスト](../../servers/manage/checklist-for-installing-update-2002.md)」を参照してください。 サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist)に関するページも確認してください。

Configuration Manager の新機能をすべて利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

> [!TIP]
> このページが更新されたときに通知を受け取るには、次の URL をコピーして RSS フィード リーダーに貼り付けます。`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a>Microsoft Endpoint Manager テナントのアタッチ

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a>デバイスの同期とデバイスのアクション
<!--3555758-->
Microsoft Endpoint Manager は、すべてのデバイスを管理するための統合ソリューションです。 Microsoft は、Configuration Manager と Intune を、**Microsoft Endpoint Manager 管理センター**と呼ばれる 1 つのコンソールに統合します。 このリリース以降、ご利用の Configuration Manager デバイスをクラウド サービスにアップロードし、管理センターの **[デバイス]** ブレードからアクションを実行できるようになります。

詳細については、「[Microsoft Endpoint Manager テナントのアタッチ](../../../tenant-attach/device-sync-actions.md)」を参照してください。

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> サイトのインフラストラクチャ

### <a name="remove-a-central-administration-site"></a>中央管理サイトを削除する
<!-- 3607277 -->

階層が中央管理サイト (CAS) と 1 つの子プライマリ サイトで構成されている場合、CAS を削除できるようになりました。 この操作により、Configuration Manager インフラストラクチャが 1 つのスタンドアロンのプライマリ サイトに簡素化されます。 これにより、サイト間レプリケーションの複雑さが解消され、管理タスクが 1 つのプライマリ サイトに集中されます。

詳細については、「[CAS を削除する](../../servers/deploy/install/remove-central-administration-site.md)」を参照してください。

### <a name="new-management-insight-rules"></a>新しい管理分析情報ルール

このリリースには、次の管理分析情報ルールが含まれています。

- Microsoft Premier Field Engineering による **Configuration Manager 評価**グループの 9 つのルール。 これらのルールは、Microsoft Premier によって Services Hub で提供される多くのチェックのサンプルです。<!-- 3607758 -->

  - Active Directory セキュリティ グループ探索があまりに頻繁に実行されるように構成されている
  - Active Directory システム探索があまりに頻繁に実行されるように構成されている
  - Active Directory ユーザー探索があまりに頻繁に実行されるように構成されている
  - コレクションがすべてのシステムまたはすべてのユーザーに制限されている
  - 定期探索が無効になっている
  - 増分更新に対して実行時間の長いコレクション クエリが有効になっている
  - 配布ポイントのアプリケーションとパッケージの数を減らす
  - セカンダリ サイトのインストール問題
  - すべてのサイトを同じバージョンに更新する

- セキュリティで保護された HTTPS 通信を追加するためにご利用のサイトを構成するのに役立つ **Cloud Services** グループの 2 つの追加ルール。<!-- 6268489 -->

  - HTTPS 構成が適切でないサイト
  - Azure AD にアップロードされないデバイス

詳細については、[管理分析情報](../../servers/manage/management-insights.md)に関するページを参照してください。

### <a name="improvements-to-administration-service"></a>管理サービスの改善

<!-- 5728365 -->

管理サービスは、SMS プロバイダー向けの REST API です。 以前は、次のいずれかの依存関係を実装する必要がありました。

- サイト全体に拡張 HTTP を有効にする
- SMS プロバイダーのロールをホストするサーバー上で IIS に PKI ベースの証明書を手動でバインドする

このリリースから、管理サービスでサイトの自己署名証明書が自動的に使用されるようになりました。 この変更により、管理サービスをより簡単に使用できるようになります。 サイトでは常にこの証明書が生成されます。 拡張 HTTP サイトの設定 **[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** は、サイト システムでそれを使用するかどうかのみを制御します。 管理サービスでは他のサイト システムが拡張 HTTP を使用していない場合でも、常にサイトの証明書が使用されるため、このサイト設定は無視されるようになりました。 PKI ベースのサーバー認証証明書を引き続き使用することもできます。

詳細については、以下の新しい記事を参照してください。

- [管理サービスとは何ですか](../../../develop/adminservice/overview.md)
- [管理サービスを設定する方法](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Azure Active Directory の検出とグループの同期に対するプロキシのサポート

<!-- 5913817 -->

サイト システムのプロキシ設定 (認証を含む) が、以下によって使用されるようになりました。

- Azure Active Directory (Azure AD) ユーザー探索
- Azure AD ユーザー グループの探索
- コレクション メンバーシップの結果の Azure Active Directory グループへの同期

詳細については、「[プロキシ サーバーのサポート](../network/proxy-server-support.md#bkmk_other)」を参照してください。

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> クラウド接続の管理

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>必要なエンドポイントへのサーバー接続エラーを示すクリティカルなステータス メッセージ

<!-- 5566763 -->

Configuration Manager サイト サーバーがクラウド サービスに必要なエンドポイントへの接続に失敗すると、クリティカルなステータス メッセージ ID 11488 が生成されます。 サイト サーバーがサービスに接続できない場合、SMS_SERVICE_CONNECTOR コンポーネントのステータスがクリティカルに変わります。 Configuration Manager コンソールのコンポーネントのステータス ノードに、詳細なステータスが表示されます。

### <a name="token-based-authentication-for-cloud-management-gateway"></a>クラウド管理ゲートウェイのトークン ベース認証

<!-- 5686290 -->

クラウド管理ゲートウェイ (CMG) では多くの種類のクライアントがサポートされていますが、たとえ拡張 HTTP であっても、これらのクライアントにはクライアント認証証明書が必要です。 この証明書の要件は、内部ネットワークに接続することがあまりなく、Azure Active Directory (Azure AD) に参加できず、PKI によって発行された証明書をインストールする方法を持たない、インターネットベースのクライアントでは、プロビジョニングするのが困難な場合があります。

Configuration Manager では、次の方法でデバイスのサポートが拡張されます。

- 一意のトークンのために内部ネットワークに登録する
- インターネットベースのデバイス用の一括登録トークンを作成する

詳細については、[CMG のトークンベースの認証](../../clients/deploy/deploy-clients-cmg-token.md)に関する記事をご覧ください。

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Microsoft Endpoint Configuration Manager のクラウド機能

<!--5834830-->

Microsoft Endpoint Manager admin center や、オンプレミスの Config Manager インストール用の他の接続クラウド サービスでクラウドベースの新しい機能が使用できるようになると、Configuration Manager コンソールでこれらの新しい機能をオプトインできるようになります。 Configuration Manager コンソールで機能を有効にする方法の詳細については、「[更新プログラムのオプション機能の有効化](../../servers/manage/install-in-console-updates.md#bkmk_options)」を参照してください。

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

Desktop Analytics クラウド サービスの毎月の変更については、「[Desktop Analytics の新機能](../../../desktop-analytics/whats-new.md)」を参照してください。

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>[接続の正常性] ダッシュボードにクライアントの接続の問題が表示される

Configuration Manager で Desktop Analytics の [接続の正常性] ダッシュボードを使用して、クライアントの接続状態を監視します。 次の 2 つの領域でクライアント プロキシの構成に関する問題をより簡単に特定できるようになりました。

- **エンドポイント接続チェック**:必要なエンドポイントにクライアントが接続できない場合に、ダッシュボードに構成アラートが表示されます。 プロキシの構成に問題があるためにクライアントが接続できないエンドポイントを表示するには、ドリルダウンします。<!-- 4963230 -->

- **接続性の状態**:クライアントが Desktop Analytics クラウド サービスへのアクセスにプロキシ サーバーを使用している場合、Configuration Manager によって、クライアントからのプロキシ認証の問題が表示されるようになりました。 ドリルダウンして、プロキシ認証が原因で登録できないクライアントを表示します。<!-- 4963383 -->

詳細については、「[接続の正常性の監視](../../../desktop-analytics/monitor-connection-health.md)」をご覧ください。

## <a name="real-time-management"></a><a name="bkmk_real"></a> リアルタイムの管理

### <a name="improvements-to-cmpivot"></a>CMPivot の改善

<!-- 5870934 -->

CMPivot エンティティの移動が容易になりました。 CMPivot エンティティを検索できるようになりました。 エンティティとエンティティ オブジェクトの種類を簡単に区別できるように、新しいアイコンも追加されました。

詳細については、[CMPivot](../../servers/manage/cmpivot.md#bkmk_2002) に関するページを参照してください。

## <a name="content-management"></a><a name="bkmk_content"></a> コンテンツ管理

### <a name="exclude-certain-subnets-for-peer-content-download"></a>ピア コンテンツのダウンロードで特定のサブネットを除外する

<!-- 3555777 -->

境界グループには、次のようなピア ダウンロード オプションがあります。**ピアのダウンロード中に、同じサブネット内のピアのみを使用する**。 このオプションを有効にした場合、管理ポイントのコンテンツの場所のリストには、クライアントと同じサブネットと境界グループ内にあるピア ソースのみが含まれます。 ネットワークの構成によっては、特定のサブネットを除外して一致させることができるようになりました。 たとえば、境界は含めて、特定の VPN サブネットは除外することができます。

詳細については、[境界グループ オプション](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)に関するセクションを参照してください。

### <a name="proxy-support-for-microsoft-connected-cache"></a>Microsoft 接続キャッシュのプロキシ サポート

<!-- 5856396 -->

ご利用の環境で、インターネット アクセスのために、認証されていないプロキシ サーバーを使用している場合、Microsoft 接続キャッシュで Configuration Manager 配布ポイントを有効にすると、プロキシ通して通信できます。 詳細については、[Microsoft 接続済みキャッシュ](../hierarchy/microsoft-connected-cache.md)に関するページを参照してください。

## <a name="client-management"></a><a name="bkmk_client"></a> クライアント管理

### <a name="client-log-collection"></a>クライアント ログの収集

<!-- 4226618 -->

Configuration Manager コンソールからクライアント通知アクションを送信することによって、クライアント デバイスに対してそのクライアント ログをサイト サーバーにアップロードするようにトリガーできるようになりました。

詳細については、[クライアント通知](../../clients/manage/client-notification.md#client-diagnostics)に関するページをご覧ください。

### <a name="wake-up-a-device-from-the-central-administration-site"></a>中央管理サイトからデバイスをウェイク アップする

<!-- 6030715 -->

中央管理サイト (CAS) の [デバイス] または [デバイス コレクション] ノードで、クライアント通知アクションを使用して、デバイスの [ウェイク アップ] を実行できるようになりました。 このアクションは、以前はプライマリ サイトからしか使用できませんでした。

詳細については、[Wake On LAN を構成する方法](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810)に関するページを参照してください。

### <a name="improvements-to-support-for-arm64-devices"></a>ARM64 デバイスのサポートの強化

<!--5954175-->

**すべての Windows 10 (ARM64)** プラットフォームが、要件の規則や適用性の一覧があるオブジェクトでサポートされている OS バージョンの一覧に示されます。

> [!NOTE]
> 以前にトップ レベルの **Windows 10** プラットフォームを選択した場合、このアクションは**すべての Windows 10 (64 ビット)** と**すべての Windows 10 (32 ビット)** の両方に自動的に選択されます。 この新しいプラットフォームは自動的には選択されません。 **すべての Windows 10 (ARM64)** を追加する場合は、一覧から手動で選択します。

ARM64 デバイスに対する Configuration Manager のサポートの詳細については、「[ARM64 上での Windows 10](../configs/support-for-windows-10.md#bkmk_arm64)」を参照してください。

### <a name="track-configuration-item-remediations"></a>構成アイテムの修復の追跡
<!--4261411-->
構成アイテムのコンプライアンス規則で**サポートされている場合に修復履歴を追跡**できるようになりました。 このオプションを有効にすると、構成アイテムに対してクライアントで行われた修復によって状態メッセージが生成されます。 履歴は、Configuration Manager データベースに格納されます。

この設定の詳細については、[Configuration Manager クライアントを使用して管理されている Windows デスクトップおよびサーバー コンピューターのカスタム構成項目の作成](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track)に関する記事を参照してください。

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a> アプリケーション管理

### <a name="microsoft-edge-management-dashboard"></a>Microsoft Edge の管理ダッシュボード

<!-- 3871913 -->

Microsoft Edge の管理ダッシュボードを使用すると、Microsoft Edge やその他のブラウザーの使用状況に関する分析情報を得ることができます。 このダッシュボードでは、次のことができます。

- Microsoft Edge がインストールされているデバイスの数を確認する
- 異なるバージョンの Microsoft Edge がインストールされているクライアントの数を確認する
- デバイス全体のインストールされているブラウザーを確認する
- デバイス別の優先ブラウザーを確認する

[ソフトウェア ライブラリ] ワークスペースで、[Microsoft Edge の管理] をクリックしてダッシュボードを表示します。 グラフ データのコレクションを変更するには、[参照] をクリックし、別のコレクションを選択します。 既定では、最も大きい 5 つのコレクションがドロップダウン リストに表示されます。 リストにないコレクションを選択すると、新しく選択されたコレクションがドロップダウン リストの下の方に移動します。

詳細については、[Microsoft Edge の管理](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash)に関するページを参照してください。

### <a name="improvements-to-microsoft-edge-management"></a>Microsoft Edge の管理の機能強化

<!-- 4561024 -->

自動更新を無効にするのではなく、自動更新を受信するように設定された Microsoft Edge アプリケーションを作成できるようになりました。 この変更により、Configuration Manager を使用して Microsoft Edge の更新プログラムを管理するか、Microsoft Edge による自動更新を許可するかを選択できます。 アプリケーションを作成するときに、[Microsoft Edge の設定] ページの [Allow Microsoft Edge to automatically update the version of the client on the end user's device]\(エンド ユーザーのデバイス上で Microsoft Edge によるクライアントのバージョンの自動更新を許可する\) を選択します。

詳細については、[Microsoft Edge の管理](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate)に関するページを参照してください。

### <a name="task-sequence-as-an-app-model-deployment-type"></a>アプリ モデルの展開の種類としてのタスク シーケンス

<!-- 3555953 -->

アプリケーション モデルを使用したタスク シーケンスを使用して、複雑なアプリケーションをインストールできるようになりました。 アプリのインストールまたはアンインストールに、タスク シーケンスである展開の種類をアプリに追加します。 この機能には、次のメリットがあります。

- ソフトウェア センターにアイコンでアプリ タスク シーケンスを表示する。 ユーザーは、このアイコンによってアプリ タスク シーケンスを見つけて識別しやすくなります。

- ローカライズされた情報を含むアプリ タスク シーケンスのメタデータを追加で定義する

詳しくは、「[Windows アプリケーションを作成する](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)」をご覧ください。

## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS の展開

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>クライアント登録の直後にタスク シーケンスをブートストラップする

<!-- 5526972 -->

新しい Configuration Manager クライアントをインストールして登録し、さらにそのクライアントにタスク シーケンスを展開すると、登録後にタスク シーケンスが実行されるまでの時間を決定することが困難になります。 このリリースでは、新しいクライアント セットアップ プロパティが導入されています。これを使用すると、タスク シーケンスがサイトに正常に登録されたら、それをクライアントで開始することができます。

詳しくは、[クライアント インストールのプロパティ - PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts) に関するページをご覧ください。

### <a name="improvements-to-check-readiness-task-sequence-step"></a>準備の確認タスク シーケンス ステップの改善

<!-- 6005561 -->

**準備の確認**タスク シーケンス ステップで、より多くのデバイス プロパティを確認できるようになりました。 タスク シーケンスでこのステップを使用して、ターゲット コンピューターが前提条件を満たしていることを確認します。

- 現在の OS のアーキテクチャ
- 最小 OS バージョン
- 最大 OS バージョン
- クライアントの最小バージョン
- 現在の OS の言語
- AC 電源の接続
- ネットワーク アダプターが接続され、ワイヤレスではない

詳しくは、[タスク シーケンスのステップ - 準備の確認](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness)に関する記事をご覧ください。

### <a name="improvements-to-task-sequence-progress"></a>タスク シーケンスの進行状況の改善

<!-- 5932692 -->

タスク シーケンスの進行状況ウィンドウには次の改善が取り込まれています。

- これを有効にすることにより、現在のステップ番号、ステップの合計数、完了率を表示できます
- 組織名を 1 行により適切に表示するためのより広いスペースを確保できるようにウィンドウの幅を大きくしました

詳細については、「[OS 展開のユーザー エクスペリエンス](../../../osd/understand/user-experience.md#task-sequence-progress)」をご覧ください。

### <a name="improvements-to-os-deployment"></a>OS 展開の機能強化

このリリースには、OS 展開に対する次の機能改善が含まれています。

- タスク シーケンス環境に新しい読み取り専用変数 `_TSSecureBoot` が含まれました。<!--5842295--> UEFI 対応デバイスでセキュア ブートの状態を確認するには、この変数を使用します。 詳細については、「[_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot)」を参照してください。

- タスク シーケンス変数を設定して、**コマンド ラインの実行**と **PowerShell スクリプトの実行**ステップのユーザー コンテキストを構成します。<!-- 5573175 --> 詳細については、「[SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser)」と「[SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser)」を参照してください。

- **[PowerShell スクリプトの実行]** ステップで、**Parameters** プロパティを変数に設定できます。<!-- 5690481 --> 詳細については、「[PowerShell スクリプトの実行](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)」を参照してください。

- Configuration Manager の PXE レスポンダーにより、サイト サーバーにステータス メッセージが送信されるようになりました。 この変更により、このサービスを使用する OS 展開のトラブルシューティングが容易になります。<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> ソフトウェア更新プログラム

### <a name="orchestration-groups"></a>オーケストレーション グループ

<!-- 3098816 -->

オーケストレーション グループを作成して、デバイスへのソフトウェア更新プログラムの展開をより細かく制御します。 多くのサーバー管理者は、特定のワークロードの更新プログラムを慎重に管理し、中間の動作を自動化する必要があります。

オーケストレーション グループを使用すると、割合や特定の数値、または明示的な順序に基づいて、デバイスを柔軟に更新できます。 また、デバイスで更新プログラムの展開を実行する前後に、PowerShell スクリプトを実行することもできます。

サーバーだけでなく、任意の Configuration Manager クライアントをオーケストレーション グループのメンバーにすることができます。 オーケストレーション グループのルールは、オーケストレーション グループのメンバーを含むすべてのコレクションに対する、すべてのソフトウェア更新プログラムの展開について、デバイスに適用されます。 その他の展開の動作も引き続き適用されます。 たとえば、メメンテナンス期間や展開スケジュールなどです。

詳細については、[オーケストレーション グループ](../../../sum/deploy-use/orchestration-groups.md)に関するページを参照してください。

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>サービス スタックの更新後にソフトウェア更新プログラムを評価する

<!-- 4639943 -->

Configuration Manager では、サービス スタックの更新プログラム (SSU) が複数の更新プログラムのインストールに含まれているかどうかが検出されるようになりました。 SSU が検出されると、それが最初にインストールされます。 SSU のインストール後、ソフトウェア更新プログラムの評価サイクルが実行され、残りの更新プログラムがインストールされます。 この変更により、依存する累積的な更新プログラムを、サービス スタックの更新プログラムの後にインストールできるようになります。 インストール間にデバイスを再起動する必要はなく、追加のメンテナンス期間を作成する必要はありません。 SSU が最初にインストールされるのは、ユーザー以外がインストールを開始した場合のみです。 たとえば、ユーザーがソフトウェア センターから複数の更新プログラムのインストールを開始した場合は、SSU が最初にインストールされないことがあります。

詳細については、[ソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu)に関するページを参照してください。

### <a name="office-365-updates-for-disconnected-software-update-points"></a>切断されたソフトウェアの更新ポイント用の Office 365 更新プログラム

<!-- 4065163 -->

新しいツールを使用して、インターネットに接続されている WSUS サーバーから、切断された Configuration Manager 環境に Office 365 更新プログラムをインポートすることができます。 以前は、更新されたソフトウェアのメタデータをエクスポートし、切断された環境にインポートした場合、Office 365 更新プログラムを展開できませんでした。 Office 365 更新プログラムには Office API と Office CDN からダウンロードした追加のメタデータが必要ですが、これは、切断された環境では不可能です。

詳細については、「[切断されているソフトウェアの更新ポイントからの Office 365 更新プログラムの同期](../../../sum/get-started/synchronize-office-updates-disconnected.md)」を参照してください。

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a> 保護

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Microsoft Defender Advanced Threat Protection (ATP) のオンボードを拡張する

<!-- 5229962 -->
Configuration Manager では、デバイスを Microsoft Defender ATP にオンボードするためのサポートが拡張されました。 詳細については、「[Microsoft Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md#onboard-devices)」をご覧ください。

## <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Microsoft エンドポイント マネージャー管理センターを使用し構成マネージャー クライアントを Microsoft Defender ATP にオンボードする
<!--5691658-->
Microsoft Defender ATP エンドポイント検出と応答 (EDR) のオンボード ポリシーを、Configuration Manager 管理対象クライアントに展開できるようになりました。 これらのクライアントは Azure AD や MDM の登録を必要とせず、ポリシーは Azure AD グループではなく ConfigMgr コレクションを対象としています。

この機能により、お客様は、Microsoft エンドポイント マネージャー管理センターという単一の管理エクスペリエンスから、Intune MDM と構成マネージャー クライアント EDR/ATP のオンボードの両方を管理できます。 詳細については、[Intune におけるエンドポイント セキュリティのエンドポイント検出と応答ポリシー](../../../../intune/protect/endpoint-security-edr-policy.md)に関するページを参照してください。

> [!Important]
> この機能を使用するには、環境にインストールされている修正プログラム ロールアップ [KB4563473](https://support.microsoft.com/help/4563473) が必要です。

### <a name="improvements-to-bitlocker-management"></a>BitLocker 管理の機能強化

- BitLocker 管理ポリシーには、固定ドライブとリムーバブル ドライブ用のポリシーなど、新しい設定が追加されています。<!-- 5925683 --> 詳細については、「[BitLocker 設定リファレンス](../../../protect/tech-ref/bitlocker/settings.md)」を参照してください。

- Configuration Manager Current Branch バージョン 1910 で、BitLocker 回復サービスを統合するには、管理ポイントの HTTPS を有効にする必要がありました。 HTTPS 接続は、ネットワーク経由で Configuration Manager クライアントから管理ポイントへの回復キーを暗号化するために必要です。 多くのお客様にとって、HTTPS 用に管理ポイントとすべてのクライアントを構成することは困難です。

    このバージョン以降、HTTPS の要件は、管理ポイントの役割全体ではなく、回復サービスをホストする IIS Web サイトに対するものになります。 この変更により、証明書の要件が緩和され、転送中の回復キーは引き続き暗号化されます。<!-- 5925660 --> 詳細については、「[回復データの暗号化](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md)」を参照してください。

## <a name="reporting"></a><a name="bkmk_report"></a> レポート

### <a name="integrate-with-power-bi-report-server"></a>Power BI Report Server との統合

<!-- 3721603 -->

Power BI Report Server を Configuration Manager レポートと統合できるようになりました。 この統合により、最新の視覚化とパフォーマンスの向上が実現します。 SQL Server Reporting Services に既に存在するものと同様の Power BI レポートのコンソールのサポートが追加されます。

詳細については、「[Power BI Report Server との統合](../../servers/manage/powerbi-report-server.md)」を参照してください。

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager コンソール

### <a name="show-boundary-groups-for-devices"></a>デバイスの境界グループを表示する

<!--6521835-->

境界グループを使用したデバイスの動作のより適切なトラブルシューティングに役立てるために、特定のデバイスの境界グループを表示できるようになりました。 **[デバイス]** ノードで、または**デバイス コレクション**のメンバーを表示するときに、新しい **[Boundary Group(s)]\(境界グループ\)** 列をリスト ビューに追加します。

詳細については、「[境界グループ](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary)」を参照してください。

### <a name="send-a-smile-improvements"></a>気に入った機能の報告の機能強化

<!-- 5891852 -->

気に入った機能の報告または問題点、改善点の報告を行う場合、フィードバックの送信時にステータス メッセージが作成されます。 この機能強化により、次のレコードが提供されます。

- フィードバックが送信された日時
- フィードバックを送信したユーザー
- フィードバック ID
- フィードバックの送信が成功したかどうか

ステータス メッセージの ID が 53900 の場合、送信は成功です。53901 の場合、送信は失敗です。

詳細については、「[製品に関するフィードバック](../../understand/find-help.md#BKMK_1806Feedback)」を参照してください。

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>構成アイテムと構成基準でのすべてのサブフォルダーの検索

<!--5891241-->

以前のリリースでの改善と同様に、 **[構成アイテム]** ノードと **[構成基準]** ノードから **[すべてのサブフォルダー]** 検索オプションを使用できるようになりました。

## <a name="tools"></a><a name="bkmk_tools"></a>ツール

### <a name="onetrace-log-groups"></a>OneTrace ログ グループ

<!-- 5559993 -->

OneTrace では、サポート センターの機能に似たカスタマイズ可能なログ グループがサポートされるようになりました。 ログ グループを使用すると、1 つのシナリオのすべてのログ ファイルを開くことができます。 OneTrace には、現在、次のシナリオ向けのグループが含まれています。

- アプリケーション管理
- コンプライアンス設定 (Desired Configuration Management とも呼ばれます)
- ソフトウェア更新プログラム

詳しくは、「[サポート センターの OneTrace](../../support/support-center-onetrace.md)」をご覧ください。

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a> "Microsoft Azure へのオンプレミス サイトの拡張と移行" の改善
<!--5665775, 6307931-->
Microsoft Azure へのオンプレミス サイトの拡張と移行を行うツールでは、1 つの Azure 仮想マシンに複数のサイト システムの役割をプロビジョニングできるようになりました。 最初の Azure 仮想マシンの展開が完了した後、サイト システムの役割を追加できます。

詳細については、「[オンプレミスのサイトを拡張して Microsoft Azure に移行する](../../support/azure-migration-tool.md#bkmk_add_role)」を参照してください。

## <a name="other-updates"></a>その他の更新内容

このバージョンでは、次の機能は[プレリリース](../../servers/manage/pre-release-features.md)ではなくなりました。

- [Azure Active Directory ユーザー グループの探索](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [コレクションのメンバーシップの結果の Azure Active Directory グループとの同期](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [CMPivot スタンドアロン](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [共同管理デバイス向けのクライアント アプリ](../../../comanage/workloads.md#client-apps) (以前の名称は *共同管理デバイス向けのモバイル アプリ*でした)<!-- 1357892/3600959 -->

Configuration Manager 向け Windows PowerShell コマンドレットの変更に関する詳細については、[PowerShell バージョン 2002 のリリース ノート](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps)を参照してください。

管理サービスの REST API の変更に関する詳細については、[管理サービスのリリース ノート](../../../develop/adminservice/release-notes.md#bkmk_2002)を参照してください。

このリリースには、新機能に加え、バグ修正などの追加の変更も含まれています。 詳細については、「[Configuration Manager Current Branch バージョン 2002 での変更の概要](https://support.microsoft.com/help/4556203)」を参照してください。

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>次のステップ

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

2020 年 5 月 11 日以降、全世界のすべてのユーザーがバージョン 2002 をインストールできます。

このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラムのインストール](../../servers/manage/updates.md)に関する記事および「[2002 に更新するためのチェックリスト](../../servers/manage/checklist-for-installing-update-2002.md)」をご覧ください。

> [!TIP]
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用します。
>
> 詳細については、下記のリンクをクリックしてください。
>
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md)
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)

既知の重大な問題については、[リリース ノート](../../servers/deploy/install/release-notes.md)を参照してください。

サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist)に関するページも確認してください。
