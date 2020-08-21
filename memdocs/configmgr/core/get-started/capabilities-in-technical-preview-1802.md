---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1802 で使用できる機能について説明します。
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 1f8af5975d623161e05e168192ee102bd0d072dc
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694391"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Configuration Manager の Technical Preview 1802 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1802 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 

このバージョンの Technical Preview をインストールする前に、「[Configuration Manager の Technical Preview](technical-preview.md)」を確認してください。 この記事により、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、フィードバックを提供する方法についての理解を深めることができます。     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>この Technical Preview の既知の問題
- **サイト サーバーがパッシブ モードの場合、新しいプレビュー バージョンへの更新に失敗します**。 [プライマリ サイト サーバーがパッシブ モード](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)の場合は、この新しいプレビュー バージョンに更新する前にパッシブ モードのサイト サーバーをアンインストールする必要があります。 パッシブ モードのサイト サーバーは、サイトの更新を完了したあとに再インストールできます。

  パッシブ モードのサイト サーバーをアンインストールするには、次の手順を実行します。
  1. Configuration Manager コンソールで **[管理]**  >  **[概要]**  >  **[サイトの構成]**  >  **[サーバーとサイト システムの役割]** の順に移動し、パッシブ モードのサイト サーバーを選択します。
  2. **[サイト システムの役割]** ウィンドウで、 **[サイト サーバー]** の役割を右クリックし、 **[役割の削除]** を選択します。
  3. パッシブ モードのサイト サーバーを右クリックし、 **[削除]** を選択します。
  4. サイト サーバーのアンインストール後に、アクティブなプライマリ サイト サーバーで **CONFIGURATION_MANAGER_UPDATE** のサービスを再起動します。
  <!--sms 489412-->


</br>

**このバージョンでお試しいただける新機能を次に示します。**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>共同管理を使用して Intune に Endpoint Protection ワークロードを移行する    
<!-- 1357365 -->
このリリースでは、共同管理を有効にした後に、Configuration Manager から Intune に Endpoint Protection ワークロードを移行できるようになります。 Endpoint Protection ワークロードを移行するには、共同管理のプロパティ ページに移動し、スライダー バーを Configuration Manager から **[パイロット]** または **[すべて]** に移動します。 詳細については、「[Windows 10 デバイスの共同管理](../../comanage/overview.md)」をご覧ください。


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configuration Manager 境界グループを使用するように Windows の配信の最適化を構成する
<!-- 1324696 -->
Configuration Manager の境界グループを使って、企業ネットワークおよびリモート オフィスへのコンテンツ配布を定義して調整します。 [Windows の配信最適化](/windows/deployment/update/waas-delivery-optimization)は、Windows 10 デバイス間でコンテンツを共有するための、クラウド ベースのピア ツー ピア テクノロジです。 このリリース以降、ピア間でコンテンツを共有するときは、境界グループを使うように配信の最適化を構成します。 新しいクライアント設定は、クライアントでの配信最適化グループ識別子として境界グループ識別子を適用します。 クライアントは、配信の最適化クラウド サービスと通信するとき、この識別子を使って目的のコンテンツを含むピアを探します。 

### <a name="prerequisites"></a>[前提条件]
- 配信の最適化は Windows 10 クライアントでのみ利用できます

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 その後、 **[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

1. Configuration Manager コンソールの **[管理]** ワークスペースの **[クライアント設定]** ノードで、カスタム クライアント デバイス設定ポリシーを作成します。
2. 新しい**配信の最適化**グループを選びます。
3. 設定 **[配信の最適化グループ ID の Configuration Manager 境界グループを使用します。]** を有効にします。

詳細については、[配信の最適化のオプション](/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization)に関するページの**グループ**配信モード オプションを参照してください。



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>クラウド管理ゲートウェイ経由での Windows 10 一括アップグレード タスク シーケンス
<!-- 1357149 -->

Windows 10 の[一括アップグレード タスク シーケンス](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)で、[クラウド管理ゲートウェイ](../clients/manage/cmg/plan-cloud-management-gateway.md)を通して管理されるインターネット ベースのクライアントへの展開がサポートされるようになります。 この機能により、リモート ユーザーはいっそう簡単に Windows 10 にアップグレードできるようになり、企業ネットワークに接続しなくてもよくなります。 

一括アップグレード タスク シーケンスによって参照されているすべてのコンテンツが、[クラウド配布ポイント](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)に配布されることを確認します。 配布されないと、デバイスはタスク シーケンスを実行できません。

アップグレード タスク シーケンスを展開するときは、次の設定を使います。
- 展開の [ユーザー エクスペリエンス] タブの **[クライアントのタスク シーケンスをインターネット上で実行できるようにする]** 。
- 展開の [配布ポイント] タブの **[タスク シーケンスを開始する前にすべてのコンテンツをローカルにダウンロードする]** 。 **[実行中のタスク シーケンスでコンテンツが必要になったときにローカルにダウンロードする]** などの他のオプションは、このシナリオでは機能しません。 タスク シーケンス エンジンは、現在、クラウド配布ポイントからコンテンツを取得できません。 Configuration Manager クライアントは、タスク シーケンスを開始する前に、クラウド配布ポイントからコンテンツをダウンロードする必要があります。
- (*省略可能*) 展開の [全般] タブの **[このタスク シーケンスのコンテンツを事前にダウンロードする]** 。 詳細については、「[コンテンツの事前キャッシュを構成する](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content)」を参照してください。



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 一括アップグレード タスク シーケンスの機能強化
<!-- 1357425 -->
Windows 10 の一括アップグレード用の既定のタスク シーケンス テンプレートに、アップグレード プロセスの前後に追加する推奨アクションを含む追加グループが含まれるようになりました。 これらのアクションは、Windows 10 にデバイスを正常にアップグレードしている多くのユーザーに共通するものです。 

### <a name="new-groups-under-prepare-for-upgrade"></a>**[アップグレードの準備]** の新しいグループ
- **バッテリのチェック**:このグループにステップを追加して、コンピューターがバッテリまたは有線の電源を使用しているかどうかを確認します。 このアクションには、このチェックを実行するためのカスタム スクリプトまたはユーティリティが必要です。
- **ネットワーク接続およびワイヤード接続のチェック**:コンピューターがネットワークに接続されているか、またワイヤレス接続を使っていないかどうかを確認するには、このグループにステップを追加します。 このアクションには、このチェックを実行するためのカスタム スクリプトまたはユーティリティが必要です。
- **互換性のないアプリケーションを削除する**:このグループにステップを追加して、この Windows 10 のバージョンと互換性のないすべてのアプリケーションを削除します。 アプリケーションをアンインストールする方法はさまざまです。 アプリケーションが Windows インストーラーを使っている場合は、アプリケーションの Windows インストーラー展開の種類プロパティの **[プログラム]** タブから、 **[アンインストール プログラム]** コマンド ラインをコピーします。 そして、アンインストール プログラムのコマンド ラインの **[コマンド ラインの実行]** ステップを、このグループに追加します。 次に例を示します。 </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **互換性のないドライバーを削除する**:このグループにステップを追加して、この Windows 10 のバージョンと互換性のないすべてのドライバーを削除します。
- **サード パーティ セキュリティの削除/停止**:このグループにステップを追加して、サード パーティ セキュリティ プログラム (ウイルス対策など) を削除または停止します。
   - サード パーティのディスク暗号化プログラムを使っている場合は、 **/ReflectDrivers** [コマンド ライン オプション](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)で、Windows セットアップにその暗号化ドライバーを提供します。 [[タスク シーケンス変数の設定]](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) ステップを、このグループのタスク シーケンスに追加します。 タスク シーケンス変数を **OSDSetupAdditionalUpgradeOptions** に設定します。 値をドライバーへのパス **/ReflectDriver** に設定します。 この[タスク シーケンス アクション変数](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS)をタスク シーケンスで使われる Windows セットアップ コマンド ラインに追加します。 このプロセスの他のガイダンスについては、ソフトウェアの製造元にお問い合わせください。

### <a name="new-groups-under-post-processing"></a>**[後処理]** の新しいグループ
- **セットアップ ベースのドライバーを適用する**:このグループにステップを追加して、パッケージからセットアップ ベースのドライバー (.exe) をインストールします。
- **サード パーティ セキュリティのインストール/有効化**:このグループにステップを追加して、サード パーティ セキュリティ プログラム (ウイルス対策など) をインストールまたは有効にします。 
- **Windows の既定のアプリと関連付けを設定する**このグループにステップを追加して、Windows の既定のアプリとファイルの関連付けを設定します。 最初に、必要なアプリの関連付けで参照コンピューターを準備します。 それから、次のコマンドを実行してエクスポートします。 </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>XML ファイルをパッケージに追加します。 [[コマンド ラインの実行]](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) ステップをこのグループに追加します。 XML ファイルを含むパッケージを指定し、次のコマンド ラインを指定します。 </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> 詳細については、「[Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)」(既定のアプリケーションの関連付けをエクスポートまたはインポートする) を参照してください。
- **カスタマイズと個人用設定を適用する**:このグループにステップを追加して、[スタート] メニューのカスタマイズ (プログラム グループの整理など) を適用します。 詳細については、「[Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen)」(スタート画面をカスタマイズする) を参照してください。

### <a name="additional-recommendations"></a>その他の推奨事項
- Windows のドキュメント「[Windows 10 のアップグレード エラーの解決](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)」を参照してください。 この記事には、アップグレード プロセスに関する詳細情報も含まれています。
- 既定の **[準備の確認]** ステップで、 **[最小空きディスク容量 (MB) を満たすことを確認する]** を有効にします。 値を、32 ビット OS のアップグレード パッケージの場合は **16384** (16 GB) 以上、64 ビットの場合は **20480** (20 GB) 以上に設定します。 
- **SMSTSDownloadRetryCount** [組み込みタスク シーケンス変数](../../osd/understand/task-sequence-variables.md)を使って、ポリシーのダウンロードを再試行します。 現在の既定では、クライアントは 2 回再試行します。この変数は 2 に設定されます。 クライアントが企業ネットワークに有線接続されていない場合は、再試行回数を増やすと、クライアントがポリシーを取得するのに役立ちます。 この変数を使っても、ポリシーをダウンロードできない場合の障害の遅延以外に、悪影響はありません。<!-- 501016 --> また、**SMSTSDownloadRetryDelay** 変数を既定値の 15 秒から増やします。
- インラインの互換性評価を実行します。 
   - **[アップグレードの準備]** グループの早い段階に、第 2 の **[オペレーティング システムのアップグレード]** ステップを追加します。 その名前を "*アップグレード評価*" にします。 同じアップグレード パッケージを指定し、 **[アップグレードを開始せずに Windows セットアップの互換性スキャンを実行する]** オプションを有効にします。 [オプション] タブで **[エラー時に続行する]** を有効にします。 
   - この "*アップグレード評価*" ステップの直後に、 **[コマンド ラインの実行]** ステップを追加します。 次のコマンド ラインを指定します。</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>**[オプション]** タブで、次の条件を追加します。 </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>このリターン コードは MOSETUP_E_COMPAT_SCANONLY (0xC1900210) に相当する 10 進数で、互換性スキャンが成功して問題がなかったことを示します。 "*アップグレード評価*" ステップが成功してこのコードを返した場合、このステップはスキップされます。 評価ステップが他のリターン コードを返した場合、このステップは Windows セットアップ互換性スキャンからのリターン コードでタスク シーケンスを失敗させます。
   - 詳細については、「[オペレーティング システムのアップグレード](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS)」を参照してください。
- このタスク シーケンスの間にデバイスを BIOS から UEFI に変更する場合は、「[インプレース アップグレード時に BIOS から UEFI に変換する](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)」を参照してください。

これら以外に推奨事項や提案がある場合は、リボンの **[ホーム]** タブから**フィードバック**をお送りください。



## <a name="improvements-to-pxe-enabled-distribution-points"></a>PXE 対応の配布ポイントの機能強化
<!-- 1357580 -->
Technical Preview バージョン 1706 で初めて導入された[新しい PXE の機能](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)の動作がはっきりわかるように、 **[Support IPv6]\(IPv6 のサポート\)** オプションの名前を変更しました。 配布ポイントのプロパティの **[PXE]** タブで、 **[Windows 展開サービスなしで PXE レスポンダーを有効にする]** をオンにします。 

このオプションは、配布ポイントで PXE レスポンダーを有効にし、Windows 展開サービス (WDS) を必要としません。 既に PXE が有効になっている配布ポイントでこの新しいオプションを有効にした場合、Configuration Manager は WDS サービスを一時停止させます。 この新しいオプションを無効にした場合、 **[クライアントの PXE サポートを有効にする]** がまだ指定されていると、配布ポイントは WDS を再び有効にします。

WDS が必要ないため、Windows Server Core などのクライアントまたはサーバー オペレーティング システムを、PXE が有効な配布ポイントにすることができます。 この新しい PXE レスポンダー サービスは、IPv6 を引き続きサポートするだけでなく、リモート オフィスの PXE が有効な配布ポイントの柔軟性も向上させます。

> [!NOTE]
> このサービスは、Technical Preview バージョン 1712 の[クライアント ベースの PXE レスポンダー サービス](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service)と同じ基本テクノロジを使っています。 この機能では、配布ポイントの役割のオーバーヘッドは必要ありません。

### <a name="multicast"></a>マルチキャスト
配布ポイントのプロパティの **[マルチキャスト]** タブでマルチキャストを有効にして構成するには、配布ポイントが WDS を使っている必要があります。 
- **[クライアントの PXE サポートを有効にする]** と **[複数のクライアントに同時にデータを送信するマルチキャストを有効にする]** を指定する場合は、 **[Windows 展開サービスなしで PXE レスポンダーを有効にする]** を指定できません。
- **[クライアントの PXE サポートを有効にする]** と **[Windows 展開サービスなしで PXE レスポンダーを有効にする]** を指定する場合は、 **[複数のクライアントに同時にデータを送信するマルチキャストを有効にする]** を指定できません。



## <a name="deployment-templates-for-task-sequences"></a>タスク シーケンスの展開テンプレート
<!-- 1357391 -->
タスク シーケンスの展開ウィザードは、展開テンプレートを作成できるようになりました。 展開テンプレートを保存して、展開を作成する既存または新規のタスク シーケンスに適用できます。 

### <a name="try-it-out"></a>試してみましょう。  
タスクを実行してみます。 その後、 **[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。 

 **新しいタスク シーケンスの展開用に展開テンプレートを作成する** <br/> 
1. **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、 **[タスク シーケンス]** を選択します。
2. タスク シーケンスを右クリックし、 **[展開]** を選びます。 
3. **[全般]** タブで、 **[展開テンプレートの選択]** オプションが追加されていることに注意してください。 
4. **ソフトウェアの展開ウィザード**の指示に従い、タスク シーケンスの展開設定を選びます。 
5. **ソフトウェアの展開ウィザード**の **[概要]** タブが表示されたら、 **[テンプレートとして保存]** をクリックします。
6. テンプレートに名前を付けて、テンプレートに保存する設定を選びます。 
7. **[Save]** (保存) をクリックします。 **[展開テンプレートの選択]** オプションからテンプレートを使えるようになります。



## <a name="product-lifecycle-dashboard"></a>製品ライフサイクル ダッシュボード
<!--1319632-->
新しい[製品ライフサイクル ダッシュボード](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)には、Configuration Manager で管理されているデバイスにインストールされている Microsoft 製品の Microsoft 製品ライフサイクル ポリシーの状態が表示されます。 このダッシュボードでは、環境内にある Microsoft 製品についての情報、サポート可能性の状態、およびサポート終了日が提供されます。 このダッシュボードを使って、各製品のサポートを利用できるかどうかを理解することができます。 

Configuration Manager コンソールのライフサイクル ダッシュボードにアクセスするには、 **[資産とコンプライアンス]**  > **[資産インテリジェンス]**  > **[製品のライフサイクル]** の順に移動します。



## <a name="improvements-to-reporting"></a>レポートの機能強化
<!--1357653-->
[ユーザーからのフィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and)の結果として、 **[特定のコレクションに対する Windows 10 サービスの詳細]** という新しいレポートが追加されました。 このレポートには、リソース ID、NetBIOS 名、OS 名、OS リリース名、ビルド、OS ブランチ、および Windows 10 デバイスのサービス状態が表示されます。 このレポートにアクセスするには、 **[監視]**  > **[レポート]**  > **[レポート]**  > **[オペレーティング システム]**  > **[特定のコレクションに対する Windows 10 サービスの詳細]** の順に移動します。



## <a name="improvements-to-software-center"></a>ソフトウェア センターの機能強化
<!--1357592-->
[ユーザーからのフィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid)の結果として、インストールされているアプリケーションをソフトウェア センターで非表示にできるようになりました。 このオプションを有効にすると、既にインストールされているアプリケーションが、[アプリケーション] タブに表示されなくなります。 

### <a name="try-it-out"></a>試してみましょう。
ソフトウェア センターのクライアント設定で、 **[インストールされたアプリケーションをソフトウェア センターで非表示にする]** 設定を有効にします。 エンド ユーザーがアプリケーションをインストールするときに、ソフトウェア センターで動作を確認してください。



## <a name="improvements-to-run-scripts"></a>スクリプトの実行の改善
<!--1236459-->
[スクリプトの実行](../../apps/deploy-use/create-deploy-scripts.md)機能が、JSON 形式を使ってスクリプトの出力を返すようになりました。 この形式は、読み取り可能なスクリプトの出力を一貫して返します。 スクリプトの実行が失敗した場合、出力が返されないことがあります。 



## <a name="boundary-group-fallback-for-management-points"></a>管理ポイントに対する境界グループのフォールバック
<!-- 1324594 -->
このリリースから、[境界グループ](../servers/deploy/configure/boundary-groups.md)間の管理ポイントのフォールバック関係を構成できるようになりました。 この動作では、クライアントが使う管理ポイントをいっそうきめ細かく制御できます。 境界グループのプロパティの **[関係]** タブに、管理ポイント用の新しい列があります。 新しいフォールバック境界グループを追加するとき、現在は、管理ポイントのフォールバック時間が常にゼロ (0) になります。 この動作は、サイトの既定の境界グループの **[既定の動作]** でも同じです。

これまでは、セキュリティで保護されたネットワークに保護された管理ポイントがあると、一般的な問題が発生します。 メインの企業ネットワーク上のクライアントは、ファイアウォールを経由してこの保護された管理ポイントと通信できない場合でも、保護された管理ポイントを含むポリシーを受け取ります。 この問題に対処するには、 **[フォールバックしない]** オプションを使って、クライアントが通信できる管理ポイントに対してのみフォールバックするようにします。

サイトをこのバージョンにアップグレードするとき、Configuration Manager は、インターネットに接続していないすべての管理ポイントを、サイトの既定の境界グループに追加します。 このアップグレード動作により、古いバージョンのクライアントが引き続き管理ポイントと通信できることが保証されます。 この機能を最大限に活用するには、管理ポイントを目的の境界グループに移動します。

管理ポイントの境界グループのフォールバックにより、クライアントのインストール (ccmsetup) 中の動作が変わることはありません。 コマンド ラインで /MP パラメーターを使って初期管理ポイントを指定しないと、新しいクライアントは、利用可能な管理ポイントの完全な一覧を受け取ります。 初期ブートストラップ プロセスでは、クライアントはアクセスできる最初の管理ポイントを使います。 クライアントがサイトに登録した後、クライアントはこの新しい動作で正しく並べ替えられた管理ポイントの一覧を受け取ります。 

### <a name="prerequisites"></a>[前提条件]
- [優先管理ポイント](../servers/deploy/configure/boundary-groups.md#bkmk_preferred)を有効にします。 Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[サイトの構成]** を展開し、 **[サイト]** を選びます。 リボンの **[階層設定]** をクリックします。 **[全般]** タブで、 **[クライアントは境界グループで指定された管理ポイントの使用を優先]** をオンにします。 

### <a name="known-issues"></a>既知の問題
- オペレーティング システムの展開プロセスは、境界グループを認識しません。

### <a name="troubleshooting"></a>トラブルシューティング
**LocationServices.log** に新しいエントリが追加されます。 **Locality** 属性は、次のいずれかの状態を示します。
- 0:Unknown
- 1:指定された管理ポイントは、フォールバックに対するサイトの既定の境界グループにのみ存在します
- 2:指定された管理ポイントは、リモート境界グループまたは近隣の境界グループに存在します。 管理ポイントが近隣の境界グループとサイトの既定の境界グループの両方に存在する場合、ローカリティは 2 です。
- 3:指定された管理ポイントは、ローカル境界グループまたは現在の境界グループに存在します。 管理ポイントが現在の境界グループと共に、近隣の境界グループまたはサイトの既定の境界グループのどちらかに存在する場合、ローカリティは 3 です。 階層設定で優先管理ポイントの設定を有効にしていない場合は、管理ポイントが存在する境界グループに関係なく、ローカリティは常に 3 です。

クライアントは、最初にローカル管理ポイント (ローカリティ 3)、次にリモート (ローカリティ 2)、最後にフォールバック (ローカリティ 1) を使います。 

クライアントは、10 分間に 5 個のエラーを受け取り、現在の境界グループ内の管理ポイントとの通信に失敗した場合、近隣の境界グループまたはサイトの既定の境界グループの管理ポイントに接続しようとします。 現在の境界グループの管理ポイントが後でオンラインに戻った場合、クライアントは次の更新サイクルでローカル管理ポイントに戻ります。 更新サイクルは、24 時間または Configuration Manager エージェント サービスが再起動するときです。



## <a name="improved-support-for-cng-certificates"></a>CNG 証明書のサポートの強化
<!-- 1357314 -->
Configuration Manager (Current Branch) バージョン 1710 では、[Cryptography:Next Generation (CNG) 証明書](../plan-design/network/cng-certificates-overview.md)がサポートされています。 バージョン 1710 では、一部のシナリオでクライアント証明書のサポートに制限があります。 

この Technical Preview リリース以降、以下の HTTPS が有効なサーバーの役割には CNG 証明書を使ってください。
- 管理ポイント
- 配布ポイント
- ソフトウェアの更新ポイント

[サポートされないシナリオ](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios)の一覧は変わりません。



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Azure Resource Manager に対するクラウド管理ゲートウェイのサポート
<!-- 1324735 -->
[クラウド管理ゲートウェイ](../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) のインスタンスを作成するとき、**Azure Resource Manager の展開**を作成するためのオプションがウィザードで提供されるようになりました。 [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) は、[リソース グループ](/azure/azure-resource-manager/resource-group-overview#resource-groups)と呼ばれる単一のエンティティとしてすべてのソリューション リソースを管理するための最新のプラットフォームです。 Azure Resource Manager で CMG を展開するとき、サイトは Azure Active Directory (Azure AD) を使って必要なクラウド リソースの認証と作成を行います。 この最新の展開では、従来の Azure 管理証明書は必要ありません。  

CMG ウィザードでは、Azure 管理証明書を使う**従来のサービス展開**のためのオプションがまだ提供されています。 リソースの展開と管理を簡単にするため、すべての新しい CMG インスタンスに Azure Resource Manager デプロイ モデルを使うことをお勧めします。 可能であれば、Resource Manager で既存の CMG インスタンスを再展開してください。

Configuration Manager では、既存の従来の CMG インスタンスが Azure Resource Manager デプロイ モデルに移行されることはありません。 Azure Resource Manager の展開を使って新しい CMG インスタンスを作成した後、従来の CMG インスタンスを削除します。 

> [!IMPORTANT]
> この機能では、Azure クラウド サービス プロバイダー (CSP) のサポートは有効になりません。 Azure Resource Manager での CMG の展開では引き続き従来のクラウド サービスが使われ、CSP はこれをサポートしません。 詳細については、「[Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)」(Azure CSP で使用可能な Azure サービス) を参照してください。  

### <a name="prerequisites"></a>[前提条件]
- [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md) との統合。 Azure AD のユーザー探索は必要ありません。
- Azure 管理証明書を除き、同じ[クラウド管理ゲートウェイの要件](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements)。

### <a name="try-it-out"></a>試してみましょう。  
 タスクを実行してみます。 その後、 **[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

1. Configuration Manager コンソールの **[管理]** ワークスペースで、 **[クラウド サービス]** を展開して、 **[クラウド管理ゲートウェイ]** を選びます。 リボンの **[クラウド管理ゲートウェイの作成]** をクリックします。 
2. **[全般]** ページで、 **[Azure Resource Manager の展開]** を選びます。 **[サインイン]** をクリックし、Azure サブスクリプション管理者アカウントで認証を行います。 ウィザードは、統合の前提条件の間に格納された Azure AD サブスクリプション情報から、残りのフィールドを自動的に設定します。 複数のサブスクリプションを所有している場合は、使う適切なサブスクリプションを選びます。 **[次へ]** をクリックします。  
3. **[設定]** ページで、サーバーの PKI 証明書ファイルを通常どおりに提供します。 この証明書では、Azure での CMG サービス名が定義されています。 **[領域]** を選び、リソース グループ オプションとして **[新規作成]** または **[既存のものを使用]** を選びます。 新しいリソース グループ名を入力するか、ドロップダウン リストから既存のリソース グループを選びます。 
4. ウィザードを完了します。

> [!NOTE] 
> 選んだ Azure AD サーバー アプリについて、Azure でサブスクリプションに**共同作成者**アクセス許可が割り当てられます。 

サービス接続ポイントの **cloudmgr.log** で、サービス展開の進行状況を監視します。



## <a name="approve-application-requests-for-users-per-device"></a>デバイスごとにユーザーのアプリケーション要求を承認する
<!-- 1357015 -->
このリリース以降では、承認を必要とするアプリケーションをユーザーが要求したとき、特定のデバイス名が要求の一部になります。 管理者が要求を承認した場合、ユーザーはそのデバイスにのみアプリケーションをインストールできます。 別のデバイスにアプリケーションをインストールするには、ユーザーは別の要求を送信する必要があります。 

> [!NOTE]
> この機能はオプションです。 このリリースを更新するときに、更新ウィザードでこの機能を有効にします。 または、後からコンソールで機能を有効にします。 詳細については、「[Enable optional features from updates](../servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。

### <a name="prerequisites"></a>[前提条件]
- Configuration Manager クライアントを最新バージョンにアップグレードします。
- [[コンピューター エージェント]](../clients/deploy/about-client-settings.md#computer-agent) グループで、クライアント設定 **[新しいソフトウェア センターを使用する]** を有効にします。

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 その後、 **[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

1. 使用できるアプリケーションをユーザー コレクションに展開します。
2. **[展開の設定]** ページで、オプション **[管理者は、デバイス上のこのアプリケーションへの要求を承認する必要があります]** を有効にします。
3. 対象のユーザーは、ソフトウェア センターを使ってアプリケーションの要求を送信します。 
4. Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** の **[承認要求]** を確認します。 各要求のリストに、 **[デバイス]** 列が追加されています。 要求に対するアクションを実行するとき、[アプリケーションの要求] ダイアログ ボックスには、ユーザーが要求を送信したデバイスの名前も表示されます。



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>ソフトウェア センターを使用してユーザーが利用できるアプリケーションを参照し、Azure AD に参加しているデバイスにインストールする
<!-- 1322613 -->
ユーザーが利用できるようにアプリケーションを展開した場合、ユーザーは Azure Active Directory (Azure AD) デバイスのソフトウェア センターでアプリケーションを参照してインストールできるようになりました。  

### <a name="prerequisites"></a>[前提条件]
- 管理ポイントで HTTPS を有効にします。
- サイトを [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md) と統合します
- ユーザー コレクションに利用可能なアプリケーションを展開します
- アプリケーション コンテンツを[クラウド配布ポイント](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)に配布します
- [[コンピューター エージェント]](../clients/deploy/about-client-settings.md#computer-agent) グループで、クライアント設定 **[新しいソフトウェア センターを使用する]** を有効にします。
- クライアントは次の条件を満たしている必要があります。 
   - Windows 10
   - Azure AD に参加していること (クラウド ドメイン参加とも呼ばれます)
- インターネット ベースのクライアントをサポートするには:
    - [クラウド管理ゲートウェイ](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - クライアント設定 **[インターネット クライアントからのユーザー ポリシー要求を有効にする]** を [[クライアント ポリシー]](../clients/deploy/about-client-settings.md#client-policy) グループで有効にします。
- 企業ネットワーク上のクライアントをサポートするには:
    - クライアントによって使われる境界グループに、クラウド配布ポイントを追加します
    - クライアントは、HTTPS が有効な管理ポイントの完全修飾ドメイン名 (FQDN) を解決できる必要があります



## <a name="report-on-windows-autopilot-device-information"></a>Windows AutoPilot のデバイス情報についてのレポート
<!-- 1351442 -->
Windows AutoPilot は、最新の方法で新しい Windows 10 デバイスをオンボーディングおよび構成するためのソリューションです。 詳細については、「[Windows AutoPilot の概要](/windows/deployment/windows-autopilot/windows-10-autopilot)」を参照してください。 既存のデバイスを Windows AutoPilot に登録する 1 つの方法は、ビジネス向け Microsoft Store および教育機関向け Microsoft Store にデバイスの情報をアップロードすることです。 この情報には、デバイスのシリアル番号、Windows 製品識別子、およびハードウェア ID が含まれます。 Configuration Manager を使って、このデバイス情報を収集およびレポートします。 

### <a name="prerequisites"></a>[前提条件]
- このデバイス情報は、Windows 10 バージョン 1703 以降のクライアントにのみ適用されます。

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 その後、 **[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

1. Configuration Manager コンソールの **[監視]** ワークスペースで、 **[レポート]** ノード、 **[レポート]** の順に展開し、 **[ハードウェア - 全般]** ノードを選びます。
2. 新しいレポート **[Windows AutoPilot デバイス情報]** を実行し、結果を表示します。 
3. レポート ビューアーで **[エクスポート]** アイコンをクリックして、 **[CSV (コンマ区切り)]** オプションを選びます。
4. ファイルを保存した後、ビジネス向け Microsoft Store および教育機関向け Microsoft Store にデータをアップロードします。 詳細については、[ビジネス向け Microsoft Store および教育機関向け Microsoft Store でのデバイスの追加](/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile)に関するページを参照してください。 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Windows Defender Exploit Guard に対する Configuration Manager ポリシーの機能強化
<!-- 1356220 -->
攻撃の回避およびフォルダー アクセスの制御コンポーネントに対する新しいポリシー設定が、[Windows Defender Exploit Guard](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) 用に Configuration Manager に追加されました。

**フォルダー アクセスの制御の新しい設定**<br/>
フォルダー アクセスの制御を構成するときのオプションとして、 **[ディスク セクターのみをブロックする]** と **[ディスク セクターのみを監査する]** の 2 つが新しく追加されました。 これら 2 つの設定を使うと、ブート セクターに対してだけフォルダー アクセスの制御を有効にし、特定のフォルダーまたは既定の保護されたフォルダーの保護を有効にしないことができます。 

**攻撃の回避の新しい設定**
- ランサムウェアに対して高度な保護を使います。
- Windows ローカル セキュリティ機関サブシステムからの資格情報の盗難をブロックします。 
- 普及、経過時間、または信頼されたリストの条件を満たしていない実行可能ファイルの実行をブロックします。 
- USB から実行された信頼されていない署名なしのプロセスをブロックします。



## <a name="microsoft-edge-browser-policies"></a>Microsoft Edge ブラウザーのポリシー
<!-- 1357310 -->
Windows 10 クライアントで [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) Web ブラウザーを使うユーザーは、Configuration Manager のコンプライアンス設定ポリシーを作成して、Microsoft Edge の一部の設定を構成できるようになりました。 現在、このポリシーには次の設定が含まれます。
- **[Set Microsoft Edge browser as default]\(Microsoft Edge ブラウザーを既定として設定する\)** : Windows 10 既定アプリの設定で、Web ブラウザーを Microsoft Edge に構成します
- **アドレス バーのドロップダウンを許可する**:Windows 10 バージョン 1703 以降が必要です。 詳細については、[AllowAddressBarDropdown ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)に関する説明を参照してください。
- **Microsoft のブラウザー間でお気に入りの同期を許可する**:Windows 10 バージョン 1703 以降が必要です。 詳細については、[SyncFavoritesBetweenIEAndMicrosoftEdge ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)に関する説明を参照してください。
- **終了時に閲覧データをクリアすることを許可する**:Windows 10 バージョン 1703 以降が必要です。 詳細については、[ClearBrowsingDataOnExit ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)に関する説明を参照してください。
- **トラッキング拒否ヘッダーを許可する**:詳細については、[AllowDoNotTrack ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)に関する記事を参照してください。
- **オートコンプリートを使用する**:詳細については、[AllowAutofill ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)に関する記事を参照してください。
- **Cookie を使用する**:詳細については、[AllowCookies ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)に関する記事を参照してください。
- **ポップアップ ブロックを許可する**:詳細については、[AllowPopups ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)に関する記事を参照してください。
- **アドレス バーで検索候補を許可する**:詳細については、[AllowSearchSuggestionsinAddressBar ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)に関する記事を参照してください。
- **Internet Explorer へのイントラネット トラフィックの送信を許可する**:詳細については、[SendIntranetTraffictoInternetExplorer ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)に関する記事を参照してください。
- **Password Manager を許可する**:詳細については、[AllowPasswordManager ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)に関する記事を参照してください。
- **開発者ツールを許可する**:詳細については、[AllowDeveloperTools ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)に関する記事を参照してください。
- **拡張機能を許可する**:詳細については、[AllowExtensions ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)に関する記事を参照してください。

### <a name="prerequisites"></a>[前提条件]
- Azure Active Directory に参加している Windows 10 クライアント。 

### <a name="known-issues"></a>既知の問題
- このリリースでは、オンプレミスのドメイン参加デバイスにはこのポリシーを適用できません。 この問題は、ハイブリッドのドメイン参加デバイスにも関係します。

### <a name="try-it-out"></a>試してみましょう。  
 タスクを実行してみます。 その後、 **[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

**ポリシーを作成する**
1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動します。 **[コンプライアンス設定]** を展開し、新しい **[Microsoft Edge ブラウザーのプロファイル]** ノードを選びます。 リボンの **[Microsoft Edge ブラウザー ポリシーの作成]** オプションをクリックします。
2. ポリシーの **[名前]** を指定し、必要に応じて **[説明]** を入力してから、 **[次へ]** をクリックします。
3. **[設定]** ページで、このポリシーに含める設定の値を **[構成済み]** に変更して、 **[次へ]** をクリックします。
4. **[サポートされているプラットフォーム]** ページで、このポリシーを適用するオペレーティング システムのバージョンとアーキテクチャを選び、 **[次へ]** をクリックします。 
5. ウィザードを完了します。

**ポリシーを展開する**
1. ポリシーを選び、リボンのオプション **[展開]** をクリックします。
2. **[参照]** をクリックして、ポリシーを展開するユーザー コレクションまたはデバイス コレクションを選びます。 
3. 必要に応じて、追加のオプションを選びます。 ポリシーに準拠していない場合は、アラートを生成します。 クライアントがこのポリシーについてデバイスのコンプライアンスを評価するスケジュールを設定します。
4. **[OK]** をクリックして展開を作成します。

他のコンプライアンス設定ポリシーと同様に、クライアントは指定されたスケジュールで設定を修復します。 Configuration Manager コンソールで、[デバイスのコンプライアンス対応を監視およびレポート](../../compliance/deploy-use/monitor-compliance-settings.md)します。



## <a name="report-for-default-browser-counts"></a>既定のブラウザー数についてのレポート
<!-- 1357830 -->
特定の Web ブラウザーが Windows の既定値になっているクライアントの数を表示する新しいレポートが追加されました。 

### <a name="known-issues"></a>既知の問題
- 最初にレポートを開いたときは、数だけが表示され、BrowserProgID は表示されません。 この問題を回避するには、レポートのクエリを次の構文に編集します。  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>試してみましょう。  
 タスクを実行してみます。 その後、 **[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。
1. **Configuration Manager** コンソールの **[監視]** ワークスペースで、 **[レポート]** 、 **[レポート]** の順に展開し、 **[ソフトウェア - 会社と製品]** を選びます。
2. **[既定のブラウザーの数]** レポートを実行します。

一般的な BrowserProgID については以下をご覧ください。
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**:Microsoft Edge
- **IE.HTTP**:Microsoft Internet Explorer
- **ChromeHTML**:Google Chrome
- **OperaStable**:Opera Software
- **FirefoxURL-308046B0AF4A39CB**:Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Windows 10 ARM64 デバイスのサポート
<!-- 1353704 -->
このリリースから、Configuration Manager クライアントは Windows 10 ARM64 デバイスでサポートされるようになりました。 既存のクライアント管理機能は、これらの新しいデバイスで動作します。 たとえば、ハードウェアとソフトウェアのインベントリ、ソフトウェア更新プログラム、アプリケーション管理などです。 オペレーティング システムの展開は現在はサポートされていません。 

## <a name="changes-to-phased-deployments"></a>段階的展開に対する変更
<!-- 1357405 -->
段階的展開は、複数のコレクションでのソフトウェアの調整および順序付けされたロールアウトを自動化します。 この Technical Preview バージョンでは、管理コンソールでタスク シーケンスの段階的展開ウィザードを実行でき、展開が作成されます。 ただし、1 番目のフェーズの成功条件が満たされた後、2 番目のフェーズは自動的に開始しません。 2 番目のフェーズは、SQL ステートメントを使って手動で開始できます。   

### <a name="try-it-out"></a>試してみましょう。  
  タスクを実行してみます。 その後、 **[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。
 
**タスク シーケンスの段階的展開の作成** </br>
1. **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、 **[タスク シーケンス]** を選択します。
2. 既存のタスク シーケンスを右クリックして、 **[Create Phased Deployment]\(段階的展開の作成\)** を選択します。 
3. **[全般]** タブで、段階的展開の名前と説明 (省略可能) を入力し、 **[既定の 2 つの段階の展開を自動的に作成する]** を選びます。 
4. **[最初のコレクション]** フィールドと **[2 番目のコレクション]** フィールドを設定します。 **[次へ]** を選択します。
5. **[設定]** タブで、スケジュール設定ごとに 1 つのオプションを選択し、完了したら **[次へ]** を選択します。 
6. **[Phases]\(フェーズ\)** タブで、必要に応じて、フェーズのいずれかを編集してから **[次へ]** をクリックします。
7. **[概要]** タブで選択内容を確認してから、 **[次へ]** をクリックして続行します。
8. 第 1 のフェーズの成功基準に到達したら、指示に従って SQL ステートメントで第 2 のフェーズを開始します。
 
**SQL ステートメントで第 2 のフェーズを開始する**
1. 次の SQL クエリで、作成した展開の PhasedDeploymentID を示します。<br/> `Select * from PhasedDeployment`
2. 次のステートメントを実行して、運用フェーズを開始します。<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。