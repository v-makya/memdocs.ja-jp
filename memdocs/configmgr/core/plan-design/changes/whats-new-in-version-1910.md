---
title: バージョン 1910 の新機能
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch のバージョン 1910 で導入された変更点および新機能について説明します。
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 849dd0bdb0f6583d525df8af3f6d46f8a4a9aecf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904668"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch のバージョン 1910 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1910 はコンソール内の更新プログラムとして利用できます。 バージョン 1806 以降が実行されているサイトで、この更新プログラムを適用します。 <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> この記事では、Configuration Manager バージョン 1910 での変更点と新機能をまとめます。

この更新プログラムをインストールするための最新のチェックリストを常に確認してください。 詳細については「[更新プログラム 1910 をインストールするためのチェックリスト](../../servers/manage/checklist-for-installing-update-1910.md)」を参照してください。 サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist)に関するページも確認してください。

Configuration Manager の新機能をすべて利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

> [!TIP]
> このページが更新されたときに通知を受け取るには、次の URL をコピーして RSS フィード リーダーに貼り付けます。`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a> Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager は Microsoft Endpoint Manager の一部になりました。

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager は、すべてのデバイスを管理するための統合ソリューションです。 Microsoft は、ライセンスを簡素化して、Configuration Manager と Intune を統合しました。 既存の Configuration Manager の投資を引き続き活用しながら、Microsoft クラウドの機能をご自分のペースで利用できます。

次の Microsoft 管理ソリューションはすべて Microsoft Endpoint Manager ブランドの一部になりました。

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- [デバイス管理の管理コンソール](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)に含まれるその他の機能

詳細については、Microsoft 365 担当の Microsoft コーポレート バイス プレジデントである Brad Anderson による次の投稿を参照してください。

- [お知らせのブログ投稿](https://aka.ms/cmannounce)
- [ビジョン ペーパー](https://aka.ms/MEMVisionPaper)
- [お知らせの概要ビデオ](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Microsoft Endpoint Manager での Configuration Manager の変更点は何ですか。

バージョン 1910 では、名前の変更を除けば、Configuration Manager は引き続き同じように機能します。 名前の変更の一部は、次のコンポーネントの使用に影響を与えることがあります。

- **Configuration Manager コンソール**:Windows [スタート] メニューの **[Microsoft Endpoint Manager]** フォルダーでコンソールと**リモート コントロール ビューアー**のショートカットを見つけます。

- **ソフトウェア センター**:Windows [スタート] メニューの **[Microsoft Endpoint Manager]** フォルダーで、ソフトウェア センターのショートカットを見つけます。

![[スタート] メニューの Microsoft Endpoint Manager のアイコン](media/microsoft-endpoint-manager-start-menu.png)

保守管理している内部ドキュメントがあれば、これらの新しい場所が含まれるように更新してください。

> [!TIP]
> Windows 10 の場合、[スタート] メニューを開き、名前の入力を始めるとアイコンが見つかります。 たとえば、「`Configuration Manager`」や「`Software Center`」と入力します。

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> サイトのインフラストラクチャ

### <a name="reclaim-sedo-lock"></a>SEDO ロックの再利用

<!--4786915-->

[Current Branch バージョン 1906](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences) 以降では、タスク シーケンスのロックを解除できました。 これで Configuration Manager コンソールでオブジェクトのロックを解除できるようになりました。

詳細については、「[Configuration Manager コンソールの使用](../../servers/manage/admin-console.md#bkmk_sedo)」を参照してください。

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>オンプレミスのサイトを拡張して Microsoft Azure に移行する
<!--3556022-->

この新しいツールは、Configuration Manager 用の Azure 仮想マシン (VM) をプログラムで作成するのに役立ちます。 パッシブ サイト サーバー、管理ポイント、配布ポイントなど、既定の設定のサイトの役割を使用してインストールできます。 新しい役割を検証したら、高可用性に向けた追加のサイト システムとしてそれらを使用します。 また、オンプレミスのサイト システムの役割を削除し、Azure VM の役割のみを保持することもできます。

詳細については、「[オンプレミスのサイトを拡張して Microsoft Azure に移行する](../../support/azure-migration-tool.md)」を参照してください。

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

Desktop Analytics クラウド サービスの毎月の変更については、「[Desktop Analytics の新機能](../../../desktop-analytics/whats-new.md)」を参照してください。

## <a name="real-time-management"></a><a name="bkmk_real"></a> リアルタイムの管理

### <a name="optimizations-to-the-cmpivot-engine"></a>CMPivot エンジンに対する最適化
<!--3197353-->
CMPivot エンジンがさらに大幅に最適化されました。 これで、より多くの処理を ConfigMgr クライアントにプッシュすることができます。 最適化によって、CMPivot クエリの実行に必要なネットワークとサーバーの CPU 負荷が大幅に削減されます。 これらの最適化を利用して、数ギガバイトのクライアント データをリアルタイムで処理できるようになりました。 

詳細については、「[CMPivot エンジンに対する最適化](../../servers/manage/cmpivot.md#bkmk_optimization)」を参照してください。

### <a name="additional-cmpivot-entities-and-enhancements"></a>追加の CMPivot エンティティと拡張機能
<!--5410930-->
トラブルシューティングとハンティングを支援するために、いくつかの新しい CMPivot エンティティとエンティティの拡張機能が追加されました。 クエリを実行する次のエンティティを含めています。

- Windows イベント ログ ([WinEvent](../../servers/manage/cmpivot.md#bkmk_WinEvent))
- ファイルの内容 ([FileContent](../../servers/manage/cmpivot.md#bkmk_File))
- プロセスによって読み込まれた DLL ([ProcessModule](../../servers/manage/cmpivot.md#bkmk_ProcessModule))
- Azure Active Directory 情報 ([AADStatus](../../servers/manage/cmpivot.md#bkmk_AadStatus))
- エンドポイント保護の状態 ([EPStatus](../../servers/manage/cmpivot.md#bkmk_EPStatus))

このリリースには、CMPivot に対する[その他の拡張機能](../../servers/manage/cmpivot.md#bkmk_Other)もいくつか追加されています。 詳細については、「[バージョン 1910 以降の CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot1910)」を参照してください。

## <a name="content-management"></a><a name="bkmk_content"></a> コンテンツ管理

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Microsoft Connected Cache の Intune Win32 アプリのサポート

<!--5032900-->

Configuration Manager 配布ポイントで Microsoft Connected Cache を有効にすると、Microsoft Intune Win32 アプリを共同管理クライアントに提供できるようになります。

詳細については、「[Configuration Manager における Microsoft の接続済みキャッシュ](../hierarchy/microsoft-connected-cache.md#bkmk_intune)」を参照してください。

> [!NOTE]
> Configuration Manager の Current Branch バージョン 1906 には、Windows Server にインストールされる、まだ開発中のアプリケーションである [Delivery Optimization In-Network Cache](../hierarchy/microsoft-connected-cache.md) (DOINC) が含まれていました。 Current Branch バージョン 1910 以降では、この機能は、Microsoft Connected Cache と呼ばれるようになりました。
>
> Connected Cache を Configuration Manager の配布ポイントにインストールすると、[配信の最適化] サービスのトラフィックがローカル ソースにオフロードされます。 Connected Cache では、コンテンツをバイト範囲レベルで効率的にキャッシュすることによって、この動作を行います。

## <a name="client-management"></a><a name="bkmk_client"></a> クライアント管理

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>コンプライアンス ポリシー評価の一部としてカスタム構成基準を含める
<!--3608345-->

コンプライアンス ポリシー評価の規則として、カスタム構成基準の評価を追加できるようになりました。 構成基準を作成または編集するとき、 **[コンプライアンス ポリシー評価の一部としてこの基準を評価する]** オプションを使用できるようになりました。 コンプライアンス ポリシー ルールを追加または編集するとき、 **[コンプライアンス ポリシーの評価に構成済みのベースラインを含める]** という条件があります。

共同管理デバイスの場合、全体のコンプライアンス対応状態の一部として Configuration Manager コンプライアンス評価の結果を受け取るように Intune を設定すると、この情報は Azure Active Directory に送信されます。 その後、Office 365 リソースに対する条件付きアクセスで利用できます。

詳細については、「[コンプライアンス ポリシー評価の一部としてカスタム構成基準を含める](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)」を参照してください。

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Windows 10 Enterprise マルチセッションのユーザー ポリシーを有効にする

<!--4737447-->

Configuration Manager Current Branch バージョン 1906 では、[Windows 仮想デスクトップ](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)のサポートが導入されました。 この Microsoft Azure 環境ではいくつかの OS バージョンがサポートされますが、その一部では複数のアクティブ ユーザー セッションを同時に実行できます。 たとえば、Windows 10 Enterprise マルチセッションは、これらの OS バージョンの 1 つです。

このマルチセッション デバイスでユーザー ポリシーが必要であり、パフォーマンスに影響する可能性を受け入れる場合、クライアント設定を構成してユーザー ポリシーを有効にできるようになりました。 **[クライアント ポリシー]** グループで、 **[複数のユーザー セッションに対してユーザー ポリシーを有効にします]** の設定を構成できます。

詳しくは、「[クライアント設定を構成する方法](../../clients/deploy/configure-client-settings.md)」をご覧ください。


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a> アプリケーション管理

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Microsoft Edge バージョン 77 以降の展開
<!--4561024-->
まったく新しい Microsoft Edge をビジネスにご利用いただけます。 Microsoft Edge バージョン 77 以降をユーザーに展開できるようになりました。 管理者は、展開する Microsoft Edge クライアントのバージョンと共に Beta、Dev、または安定チャンネルを選択できます。

詳細については、「[Microsoft Edge バージョン 77 以降の展開](../../../apps/deploy-use/deploy-edge.md)」を参照してください。

### <a name="improvements-to-application-groups"></a>アプリケーション グループの機能強化

<!--4760058-->

Current Branch バージョン 1906 以降では、1 つの展開としてデバイス コレクションに送信できるアプリケーションのグループを作成できます。 このリリースでは、この機能が向上しています。

- ユーザーは、ソフトウェア センターでアプリ グループを**アンインストール**できません。
- **ユーザー コレクション**にアプリ グループを展開できます。

全般情報については、「[アプリケーション グループの作成](../../../apps/deploy-use/create-app-groups.md)」をご覧ください。


## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS の展開

### <a name="improvements-to-the-task-sequence-editor"></a>タスク シーケンス エディターの向上

 タスク シーケンス エディターには次の改善が含まれています。

- **タスク シーケンス エディターの検索:**<!--4621085--> 多くのグループとステップが含まれる大規模なタスク シーケンスがある場合、特定のステップを見つけるのが難しいことがあります。 タスク シーケンス エディター内で検索できるようになりました。 これにより、タスク シーケンス内のステップをすばやく検索できるようになります。
- **タスク シーケンスの条件のコピーと貼り付け:**<!--4621098--> あるタスク シーケンス ステップの条件を別のタスク シーケンス ステップに再利用する場合は、タスク シーケンス エディター内で条件をコピーして貼り付けることができます。

詳細については、[タスク シーケンス エディターを使用する](../../../osd/understand/task-sequence-editor.md)方法に関する新しい記事を参照してください。

### <a name="task-sequence-performance-improvements-power-plans"></a>タスク シーケンスのパフォーマンス向上: 電源プラン

<!--3555926-->

高パフォーマンスの電源プランを使用してタスク シーケンスを実行できるようになりました。 このオプションを選択すると、タスク シーケンスの全体的な速度が向上します。 組み込みの高パフォーマンスの電源プランを使用するように Windows が構成されるので、電力消費の増加と引き換えに最大のパフォーマンスを実現できます。

詳細については、「[電源プランのパフォーマンスの向上](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf)」を参照してください。

### <a name="task-sequence-download-on-demand-over-the-internet"></a>インターネット経由でのタスク シーケンスのオン デマンド ダウンロード

<!--3601238-->

タスク シーケンスを使用して、クラウド管理ゲートウェイ (CMG) 経由で Windows 10 一括アップグレードを展開できます。 ただし、その場合の展開では、すべてのコンテンツをローカルにダウンロードしてからタスク シーケンスを開始する必要があります。

このリリース以降、タスク シーケンス エンジンでは、コンテンツが有効な CMG またはクラウド配布ポイントから、オンデマンドでパッケージをダウンロードできるようになりました。 この変更により、インターネット ベースのデバイスへの Windows 10 インプレース アップグレードの展開に、さらなる柔軟性が提供されます。

詳細については、「[CMG を通して Windows 10 の一括アップグレードを展開する](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)」を参照してください。

### <a name="improvements-to-os-deployment"></a>OS 展開の機能強化

このリリースには、OS 展開に対する次の機能強化が含まれています。

#### <a name="boot-image-keyboard-layout"></a>ブート イメージ キーボード レイアウト

<!--4910348-->

ブート イメージの既定のキーボード レイアウトを構成します。 ブート イメージの **[カスタマイズ]** タブで、新しい **[WinPE の既定のキーボード レイアウトを設定する]** オプションを使用します。 en-us 以外の言語を選択した場合でも、Configuration Manager によって、使用可能な入力ロケールに en-us が含められます。 デバイス上の初期のキーボード レイアウトは選択されたロケールですが、ユーザーは必要に応じてデバイスを en-us に切り替えることができます。

詳細については、「[ブート イメージの管理](../../../osd/get-started/manage-boot-images.md#customization)」をご覧ください。

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>OS アップグレード パッケージの 1 つのインデックスをインポートする

<!--4931110-->

OS アップグレード パッケージをインポートするときに、 **[選択したアップグレード パッケージの install.wim ファイルから、特定のイメージ インデックスを抽出する]** オプションを使用できます。 この動作は、[OS イメージ](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages)の場合と似ていますが、OS アップグレード パッケージ内の既存の install.wim が上書きされる点で異なります。 イメージ インデックスが一時的な場所に抽出された後、元のソース ディレクトリに移動されます。

詳しくは、[OS のアップグレード パッケージの管理](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs)に関するページをご覧ください。

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>タスク シーケンス中にコマンド ラインの実行ステップの結果を変数に出力する

<!--user story 4977616/bug 4798352-->

**[コマンドラインの実行]** ステップに **[タスク シーケンス変数に出力]** オプションが含まれるようになりました。 このオプションを有効にすると、タスク シーケンスによって、指定したカスタム タスク シーケンス変数にコマンドからの出力が保存されます。

詳細については、「[コマンド ラインの実行](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)」を参照してください。

#### <a name="improvements-to-task-sequence-debugger"></a>タスク シーケンス デバッガーの機能強化

このリリースでは、タスク シーケンス デバッガーが次の点で改善されています。

- 新しいタスク シーケンス変数 **TSDebugOnError** を使って、タスク シーケンスでエラーが返されたときに自動的にデバッガーを起動できます。<!-- 5012536 -->
- デバッガーでブレークポイントを作成した後、タスク シーケンスによってコンピューターが再起動された場合、再起動後もデバッガーによってそのブレークポイントが保持されます。<!-- 5012509 -->

詳しくは、[タスク シーケンスのデバッグ](../../../osd/deploy-use/debug-task-sequence.md)に関するページと「[タスク シーケンス変数 - TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError)」をご覧ください。

#### <a name="improved-language-support-in-task-sequence"></a>タスク シーケンスでの言語サポートの強化

<!--5411057, 5138936-->

このリリースでは、OS 展開中に言語構成をさらに細かく制御できるようになります。 これらの言語設定を既に適用している場合は、この変更によって OS 展開のタスク シーケンスを簡略化することができます。 言語ごとに複数のステップを使ったり、個別のスクリプトを使ったりする代わりに、組み込みの **[Windows 設定の適用]** ステップのインスタンスを、言語につき 1 つ、その言語の条件と共に使います。

**[Windows 設定の適用]** タスク シーケンス ステップを使用すると、次の新しい設定を構成できます。

- 入力ロケール (既定のキーボード レイアウト)
- システム ロケール
- UI 言語
- UI 言語のフォールバック
- ユーザー ロケール

詳細については、「[Windows 設定の適用](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings)」を参照してください。

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Windows 10 一括アップグレード用の新しい変数

<!--4680263-->

Windows セットアップが完了したときに、高パフォーマンスのデバイスで Windows 10 の一括アップグレード タスク シーケンスに発生するタイミングの問題に対処する目的で、新しいタスク シーケンス変数 **SetupCompletePause** を設定できるようになりました。 この変数に秒単位の値を割り当てると、Windows セットアップ プロセスにより、タスク シーケンスが開始されるまでの時間がその分だけ遅延されます。 このタイムアウトにより、Configuration Manager クライアントでは初期化にさらに時間がかかるようになります。

詳しくは、「[タスク シーケンス変数 - SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause)」をご覧ください。

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> ソフトウェア更新プログラム

### <a name="additional-options-for-third-party-update-catalogs"></a>サード パーティの更新プログラム カタログの追加オプション
<!--4469002-->
サードパーティの更新プログラム カタログの同期を今までより細かく制御できるようになりました。 Configuration Manager バージョン 1910 以降、他に依存せず、カタログ別に同期スケジュールを構成できるようになりました。 分類された更新プログラムを含むカタログを使用するとき、特定の更新プログラム カテゴリのみを含めるように同期を構成し、カタログ全体の同期を回避できます。 分類されたカタログを使用すると、あるカテゴリを展開することがわかっているとき、それを自動的にダウンロードし、Windows Server Update Services (WSUS) に発行するよう構成できます。

詳細については、「[Enable third-party updates](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910)」 (サードパーティ製更新プログラムを有効にする) を参照してください。

### <a name="use-delivery-optimization-for-all-windows-updates"></a>すべての Windows 更新プログラムに配信の最適化を使用する
<!--4699118-->
以前は、配信の最適化は、高速更新に対してのみ利用できました。 Configuration Manager バージョン 1910 では、Windows 10 バージョン 1709 以降を実行しているクライアントに対するすべての Windows Update コンテンツの配布に配信の最適化を使用できるようになりました。

詳細については、次をご覧ください。
- [Windows 10 更新プログラムの配信の最適化](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [ソフトウェア更新プログラムのクライアントの設定](../../clients/deploy/about-client-settings.md#software-updates)
- [配信の最適化のためのクライアント設定](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>ADR 用の追加のソフトウェア更新プログラム フィルター
<!--4852033-->
自動展開規則 (ADR) の更新フィルターとして **[展開済み]** を使用できるようになりました。 このフィルターは、パイロット コレクションまたはテスト コレクションへの展開が必要となる可能性がある新しい更新プログラムを識別するのに役立ちます。

詳細については、「[ソフトウェア更新プログラムの自動展開](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)」を参照してください。

## <a name="office-management"></a><a name="bkmk_o365"></a> Office 管理


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>[Office 365 ProPlus Pilot と正常性] ダッシュボード
<!--4488272, 4488301-->

Office 365 ProPlus のパイロットと正常性ダッシュボードでは、Office 365 ProPlus を計画し、試作し、展開できます。 このダッシュボードからは、Office 365 ProPlus がインストールされたデバイスの正常性に関する分析情報が提供され、展開計画に影響を与える可能性のある問題の特定に役立ちます。 Office 365 ProPlus Pilot と正常性ダッシュボードには、アドイン インベントリに基づくパイロット デバイスの推奨事項が表示されます。

詳細については、「[Office 365 ProPlus のパイロットと正常性ダッシュボード](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot)」を参照してください。

## <a name="protection"></a><a name="bkmk_protect"></a> 保護

### <a name="bitlocker-management"></a>BitLocker の管理

<!--3601034-->

Configuration Manager からは、BitLocker ドライブ暗号化の次の管理機能が提供されます。

- BitLocker クライアントをマネージド Windows デバイスに展開する
- デバイスの暗号化ポリシーを管理する
- コンプライアンス レポートを生成する
- キー回復用 Web サイトの管理と監視を使用する
- ユーザー セルフサービス ポータルにアクセスする

詳細については、「[BitLocker 管理の計画](../../../protect/plan-design/bitlocker-management.md)」を参照してください。

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager コンソール

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>コンソール接続を使用してアクティブなコンソールとメッセージ管理者を表示する
<!--4923997-->
**コンソール接続**に関して、次のような機能強化が行われました。

- Microsoft Teams を通じて他の Configuration Manager 管理者にメッセージを送信する機能。
- **[最終接続時刻]** が **[最後のコンソール ハートビート]** 列に置き換えられました。
  - フォアグラウンドで開いているコンソールから 10 分ごとにハートビートが送信されるので、現在アクティブになっているコンソール接続を判断するときに役立ちます。

詳細については、「[最近接続されたコンソールを表示する](../../servers/manage/admin-console.md#bkmk_viewconnected)」と[メッセージ管理者](../../servers/manage/admin-console.md#bkmk_message)に関するページを参照してください。

### <a name="client-diagnostics-actions"></a>クライアント診断アクション

<!--4433455-->

Configuration Manager コンソールの **[クライアント診断]** には新しいデバイス アクションがあります。

- **詳細ログ記録を有効にする:** CCM コンポーネントのグローバル ログ レベルを "*詳細に変更*" し、デバッグ ログ記録を有効にします。
- **詳細なログ記録を無効にする**: グローバル ログ レベルを "*既定*" に変更し、デバッグ ログ記録を無効にします。

詳細については、[クライアント診断](../../clients/manage/client-notification.md#client-diagnostics)に関するページを参照してください。

### <a name="improvements-to-console-search"></a>コンソール検索の機能強化
<!--4640570-->

このリリースでは、Configuration Manager コンソールの検索が次の点で機能強化されています。

- **[ドライバー パッケージ]** ノードと **[クエリ]** ノードから、 **[すべてのサブフォルダー]** 検索オプションを使用できるようになりました。<!--2841181,5424892-->
- 検索で 1,000 件を超える結果が返された場合は、通知バーで **[OK]** を選択すると、さらに結果を表示できます。<!--4640570-->

## <a name="other-updates"></a>その他の更新内容

Configuration Manager 向け Windows PowerShell コマンドレットの変更に関する詳細については、[PowerShell バージョン 1910 のリリース ノート](https://docs.microsoft.com/powershell/sccm/1910-release-notes?view=sccm-ps)を参照してください。

管理サービスの REST API の変更に関する詳細については、[管理サービスのリリース ノート](../../../develop/adminservice/release-notes.md#bkmk_1910)を参照してください。

このリリースには、新機能に加え、バグ修正などの追加の変更も含まれています。 詳細については、「[バージョン 1910 の現在のブランチでの変更の概要](https://support.microsoft.com/help/4535776)」を参照してください。

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
2020 年 2 月 18 日以降、コンソールで次の更新プログラムのロールアップ (4537079) を利用できるようになりました:[Microsoft Endpoint Configuration Manager Current Branch バージョン 1910 の更新プログラムのロールアップ](https://support.microsoft.com/help/4537079)。



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>次のステップ

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
2019 年 12 月 20 日より、バージョン 1910 は全世界のすべてのユーザーがインストールできるようになります。

このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラムのインストール](../../servers/manage/updates.md)に関する記事および「[1910 に更新するためのチェックリスト](../../servers/manage/checklist-for-installing-update-1910.md)」をご覧ください。

> [!TIP]
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用します。
>
> 詳細については、下記のリンクをクリックしてください。
>
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md) 
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines) 

既知の重大な問題については、[リリース ノート](../../servers/deploy/install/release-notes.md)を参照してください。

サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist)に関するページも確認してください。
