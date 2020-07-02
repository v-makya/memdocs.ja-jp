---
title: バージョン 1606 の新機能
titleSuffix: Configuration Manager
description: Configuration Manager のバージョン 1606 で導入された変更点および新機能について説明します。
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 070c616ed8411bcd90b2d3edb12b04edd57241e1
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590475"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Configuration Manager のバージョン 1606 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の更新プログラム 1606 は、以前にインストール済みで、バージョン 1511 または 1602 を実行するサイトを対象とする、コンソール内の更新プログラムとして使用可能な更新プログラムです。 バージョン 1511 は、新しい Configuration Manager サイトのインストールに使用する初期の基準バージョンです。
> [!TIP]  
> 詳細については、下記のリンクをクリックしてください。  
>   
> - [新しいサイトをインストールする](../../servers/deploy/install/prepare-to-install-sites.md) (1511 などの基準バージョンを使用)  
> - [サイトで更新プログラムをインストールする](../../servers/manage/updates.md) (更新プログラム 1602 または 1606 など)  

 以降のセクションでは、Configuration Manager のバージョン 1606 の変更点および導入された新機能について詳しく説明します。  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>更新プログラムとサービス

### <a name="changes-for-the-updates-and-servicing-node"></a>更新プログラムとサービス ノードの変更
Configuration Manager コンソールの [更新とサービス] ノードの変更点を次に示します。
> [!NOTE]
> これらの変更点は、バージョン 1606 をインストールするまで利用できません。

- **ノード名の変更:**

    **[監視]** ワークスペースで、 **[サイト サービスの状態]** ノードの名前が **[更新とサービスの状態]** に変更されました。
- **追加のインストール状態の詳細:**

    サイトの更新プログラムのインストールの状態を表示すると、次の操作の詳細がコンソールで個別に表示されるようになりました。
    - **ダウンロード** (これは、サービス接続ポイントのサイト システムの役割がインストールされている最上位層のサイトにのみ適用されます)
    - **Replication**
    - **前提条件の確認**
    - **インストール**

  さらに、各手順のより詳細な情報 (詳細な情報を表示できるログ ファイルなど) が追加されています。  
-   **前提条件のエラーを再試行する新しいオプション:**

    **[管理]** ワークスペースと **[監視]** ワークスペースの両方で、 **[更新とサービス]** ノードのリボンに **[前提条件チェックの警告を無視する]** という名前の新しいボタンが含まれています。

    前提条件チェックの警告を無視する オプションを使用せずに更新プログラムを (更新ウィザードから) インストールし、その更新プログラムのインストールが警告状態になって停止した場合は、後でリボンから **前提条件チェックの警告を無視する** を選択できます。 これにより、更新プログラムのインストールの自動継続がトリガーされます。  



- **より見やすくなった更新プログラムのビュー:**

    **[更新とサービス]** ノードに、最近インストールされた更新プログラムと、インストール可能な新しい更新プログラムのみが表示されるようになりました。 以前にインストールされた更新プログラムを表示するには、リボンに表示される新しい **[履歴]** ボタンをクリックします。  

-   **実稼働前の名前変更されたオプション:**

    **[更新とサービス]** ノードで、 **[クライアント オプション]** という名前だったボタンが **[実稼働前クライアントの昇格]** に変更されました。


###  <a name="pre-release-features"></a>プレリリース機能
1606 以降では、Configuration Manager のプレリリース機能を使用することに同意して初めて、そのプレリリース機能を選択し、有効にして使用するようにできます。 詳細については、「[更新プログラムからプレリリース機能を使用する](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)」を参照してください。

### <a name="new-distribution-point-update-behavior"></a>新しい配布ポイントの更新プログラムの動作
更新プログラム 1606 には、今後の更新プログラムをインストールする際に配布ポイントの可用性を向上させる変更が導入されています。

更新プログラム 1606 がインストールされた後、そのサイトで次回に更新プログラムをインストールする際に、標準およびプル配布ポイントのサイト システムの役割を自動的に再インストールする必要がある場合、すべての配布ポイントが同時にオフラインで更新されることはなくなります。 代わりに、サイト サーバーはサイトのコンテンツ配布設定を利用し、一度に一部の配布ポイントに更新プログラムを配布します。 結果として、一部の配布ポイントだけがオフラインになり、更新プログラムをインストールします。 この方法により、更新をまだ開始していない、あるいは更新を完了した配布ポイントがオンラインにとどまり、コンテンツをクライアントに提供できます。



## <a name="accessibility"></a><a name="accessibility"></a> ユーザー補助
ノード名の最初の文字することで、ワークスペースのさまざまなノード間を移動できるようになりました。 キーを押すたびに、その文字で始まる次のノードにカーソルが移動します。 スクリーン リーダーを使用している場合は、リーダーがそのノードの名前を読み上げます。 ユーザー補助機能の詳細については、[ユーザー補助機能](../../../core/understand/accessibility-features.md)についての記事を参照してください。

## <a name="administration"></a><a name="administration"></a>管理
Configuration Manager コンソールの [管理] の変更点を次に示します。
### <a name="oms-connector"></a>OMS コネクタ

Configuration Manager を Configuration Manager のコレクションとして [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/articles/operations-management-suite-overview/) に接続できるようになりました。 これにより、Configuration Manager 展開のコレクションなどのデータを OMS に表示できるようになります。 [Configuration Manager から Microsoft Operations Management Suite へのデータの同期については、こちら](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)をご覧ください。

OMS コネクタは、プレリリースの機能です。 有効にするには、「[更新プログラムからのプレリリース機能の使用](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)」をご覧ください。

### <a name="support-for-cache-size-in-client-settings"></a>[クライアント設定] でのキャッシュ サイズのサポート

Configuration Manager コンソールの **[クライアント設定]** で、クライアント コンピューターのキャッシュ フォルダーのサイズを構成できるようになりました。 以前は、クライアント ソフトウェアのインストールまたは再インストール時にのみ、クライアント キャッシュ サイズを設定することができました。 キャッシュ サイズをクライアント設定として指定し (既定またはカスタム)、クライアントの再インストールを必要とせずに、次回のポリシー更新時にその設定をクライアントに適用できるようになりました。 詳細については、「 [Configuration Manager クライアントにクライアントキャッシュを構成する](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache)」を参照してください。

## <a name="on-premises-mobile-device-management"></a>オンプレミス モバイル デバイス管理

### <a name="support-for-multiple-device-management-points"></a>複数のデバイス管理ポイントのサポート

オンプレミスのモバイル デバイス管理 (MDM) で、複数のデバイス管理ポイントが使用できるように登録済みのデバイスを自動的に構成する Windows 10 Anniversary Update の新機能がサポートされました。 この機能により、通常使用しているデバイスの管理ポイントが使用できない場合に、デバイスが別のデバイス管理ポイントにフォールバックすることができます。 この機能は、Windows 10 Anniversary Update がインストールされている PC およびデバイスでのみ機能します。


## <a name="application-management"></a>アプリケーション管理

### <a name="manage-apps-from-the-windows-store-for-business"></a>ビジネス向け Windows ストアからのアプリの管理

[ビジネス向け Windows ストア](https://www.microsoft.com/business-store)は、組織向けの Windows アプリを検索して、個別に、または一括で購入できる場所です。 Configuration Manager にストアを接続することで、購入したアプリのリストを Configuration Manager と同期し、それらを Configuration Manager コンソールで表示し、他のアプリと同様に展開できます。

詳細については、[Configuration Manager でのビジネス向け Microsoft Store のアプリの管理](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)に関する記事を参照してください。

### <a name="manage-ios-volume-purchased-apps"></a>iOS ボリューム購入アプリの管理

ボリューム購入した iOS アプリを管理して Configuration Manager でこれらのアプリを展開するためのワークフローが改善されました。


### <a name="software-center-user-interface"></a>ソフトウェア センターのユーザー インターフェイス

ソフトウェア センターのユーザー インターフェイスが簡素化されて検索が容易になりました。
*  **[インストールのステータス]** タブと **[インストール済みソフトウェア]** タブが、1 つの **[インストールのステータス]** タブに統合されました。
*  **[更新プログラム]** 、 **[オペレーティング システム]** 、および **[アプリケーション]** が 3 つのタブに分割されました。
* 一度に複数の更新プログラムを選択してインストールすることも、 **[すべてをインストール]** をクリックして一度にすべての更新プログラムをインストールすることもできます。

### <a name="content-status-links"></a>コンテンツのステータスのリンク
アプリケーションまたはパッケージのプロパティに、そのオブジェクトのステータスに移動するリンクが追加されました。

## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Office 365 のクライアント エージェントを管理するクライアント設定
構成マネージャー クライアントの設定を使用して Office 365 のクライアント エージェントを管理できるようになりました。 これを設定し、Office 365 の更新プログラムを展開すると、Configuration Manager クライアント エージェントは、Office 365 のクライアント エージェントと連携して、配布ポイントから Office 365 の更新プログラムをダウンロードしてインストールします。

詳細については、「[Configuration Manager での Office 365 ProPlus の更新プログラムの管理](../../../sum/deploy-use/manage-office-365-proplus-updates.md)」をご覧ください。

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>手動でのクライアントの新しいソフトウェアの更新ポイントへの切り替え
アクティブなソフトウェアの更新ポイントに問題がある場合に、Configuration Manager クライアントが新しいソフトウェアの更新ポイントに切り替えるためのオプションを有効にできるようになりました。 有効にすると、クライアントは次のスキャンにおいて他のソフトウェア更新ポイントを探します。

詳細については、「[Configuration Manager でのソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs)」をご覧ください。

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Windows 10 クライアントにおけるソフトウェア更新プログラムのインストール後の再起動オプション
再起動の必要なソフトウェア更新プログラムが Configuration Manager により展開され、コンピューターにインストールされた場合、再起動が保留中としてスケジュールされます。 再起動ダイアログ ボックスも表示されます。 Configuration Manager バージョン 1606 から、Configuration Manager ソフトウェアの更新のために再起動が保留中となっているときはいつでも **[更新と再起動]** および **[更新とシャットダウン]** のオプションを利用できるようになりました。 これらは、Windows 10 コンピューターの Windows の電源オプションで使用できます。 これらのオプションのいずれかを使用した場合、コンピューターの再起動後に再起動ダイアログ ボックスは表示されません。

詳細については、[ソフトウェア更新プログラムの監視](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions)に関する記事を参照してください。

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>クライアントがソフトウェアをインストールして再起動した直後に、ソフトウェア更新プログラムのコンプライアンス対応スキャンを実行する
クライアントがソフトウェアをインストールして再起動した直後に、ソフトウェア更新プログラムのコンプライアンス対応スキャンを実行できるようになりました。 展開に対してこれを設定するには、ソフトウェア更新プログラムの展開ウィザードの **[ユーザー エクスペリエンス]** ページで、 **[この展開の更新プログラムでシステムの再起動が必要な場合は、再起動後に更新プログラムの展開評価サイクルを実行する]** をオンにします。 これにより、クライアントは、クライアントの再起動後に適用可能になる追加のソフトウェア更新プログラムをチェックして、同じメンテナンス期間中にそれらをインストール (およびコンプライアンスに準拠) できます。 詳細については、「[ソフトウェア更新プログラムの自動展開](../../../sum/deploy-use/automatically-deploy-software-updates.md)」または「[ソフトウェア更新プログラムの手動展開](../../../sum/deploy-use/manually-deploy-software-updates.md)」を参照してください。

## <a name="operating-system-deployment"></a>オペレーティング システムの展開

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>タスク シーケンス ステップの向上:ソフトウェア更新プログラムのインストール
**[キャッシュされているスキャン結果からソフトウェア更新プログラムを評価する]** という新しい設定により、キャッシュされたスキャン結果を使用する代わりに、ソフトウェア更新プログラムのフル スキャンを実行するオプションを利用できるようになりました。 詳細については、「[Task sequence steps](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)」(タスク シーケンスのステップ) を参照してください。

また、新しいタスク シーケンス変数 **SMSTSSoftwareUpdateScanTimeout** が使用できるようになりました。 この変数を使用すると、ソフトウェア更新プログラムのインストール タスク シーケンスのステップ中に、ソフトウェア更新プログラムのスキャンのタイムアウトを制御することができます。 既定値は 30 分です。 詳細については、[タスク シーケンスの組み込み変数](../../../osd/understand/task-sequence-variables.md)に関する記事を参照してください。

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>OSDPreserveDriveLetter タスク シーケンス変数は非推奨とされました
OSDPreserveDriveLetter タスク シーケンス変数は非推奨とされました。 Configuration Manager バージョン 1606 以降、Windows セットアップにより、オペレーティング システムの展開中に使用する最適なドライブ文字 (通常は C:) が既定で決定されます。

詳細については、[タスク シーケンスの組み込み変数](../../../osd/understand/task-sequence-variables.md)に関する記事を参照してください。

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>PXE 対応配布ポイントの RamDisk TFTP ウィンドウ サイズのカスタマイズ
PXE 対応配布ポイントの RamDisk ウィンドウ サイズをカスタマイズできるようになりました。 ネットワークをカスタマイズしている場合、ウィンドウ サイズが大きすぎるために、ブート イメージのダウンロードがタイムアウト エラーで失敗する可能性があります。 RamDisk 簡易ファイル転送プロトコル (TFTP) ウィンドウ サイズのカスタマイズにより、特定のネットワーク要件に対応する PXE を使用する場合に、TFTP トラフィックを最適化できます。

詳細については、「[Configuration Manager で OS 展開用のサイト システムの役割を準備する](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)」を参照してください。

## <a name="compliance-settings"></a>コンプライアンス設定

### <a name="smart-lock-setting-for-android-devices"></a>Android デバイスの Smart Lock 設定
**[Smart Lock やその他の信頼できるエージェントを許可する]** という新しい設定が、Android および Samsung KNOX Standard 構成項目に追加されました。

この設定により、互換性のある Android デバイスで Smart Lock 機能を制御できるようになります。 "信頼エージェント" とも呼ばれるこの電話機能では、信頼できる場所にある場合、デバイスのロック画面のパスワードを無効化またはバイパスすることができます。 たとえば、デバイスが特定の Bluetooth デバイスに接続されているときや NFC タグの近くにある場合などは信頼できる場所にあると考えられます。 この設定を使用して、ユーザーが Smart Lock を構成することを禁止できます。


## <a name="device-configuration-and-protection"></a>デバイスの構成と保護

### <a name="product-name-changes"></a>製品名の変更

* Microsoft Passport for Work は、**Windows Hello for Business** という名前になりました。
* エンタープライズ データ保護は、**Windows Information Protection** という名前になりました。

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Windows Hello for Business (Passport for Work) の展開

構成マネージャー クライアントで管理されたドメインに参加している Windows 10 デバイスに Windows Hello for Business ポリシーを展開できるようになりました。

これらの変更を反映するように、Configuration Manager コンソールが更新されました。

### <a name="ios-activation-lock"></a>iOS のアクティベーション ロック
Configuration Manager は、iOS 7.1 以降のデバイス向けの iPhone を探すアプリの機能である iOS のアクティベーション ロックを管理するために役立ちます。 アクティベーション ロックを有効にすると、ユーザーの Apple ID とパスワードを入力しない限り、以下の操作を実行できなくなります。
* iPhone を探すアプリをオフにする。
* デバイスを消去する。
* ディスクを再アクティブ化する。

Configuration Manager を使ってアクティベーション ロックを管理するには、次の 2 つの方法があります。

- 監視対象のデバイスでアクティベーション ロックを有効にする。
- 監視対象のデバイスでアクティベーション ロックをバイパスする。


### <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection を使用して、Microsoft Defender Advanced Threat Protection (ATP) を管理および監視することができます。 Microsoft Defender ATP は、企業が自社のネットワークに対する高度な攻撃を検出して調査し、対応するのに役立つ新しいサービスです。 Configuration Manager ポリシーは、Windows 10 バージョン 1607 (ビルド 14328) 以降を実行しているマネージド コンピューターの登録と監視に役立ちます。

詳細については、「[Microsoft Defender Advanced Threat Protection](../../../protect/deploy-use/defender-advanced-threat-protection.md)」を参照してください。

### <a name="device-categories"></a>デバイス カテゴリ
Microsoft Intune と Configuration Manager を使用している場合に、デバイス コレクションにデバイスを自動的に配置するために使用できるデバイス カテゴリを作成することができます。 ユーザーは Intune にデバイスを登録するときに、デバイス カテゴリの選択を求められます。 Configuration Manager コンソールから、デバイスのカテゴリを変更することもできます。

詳細については、[Configuration Manager でデバイスを自動的にコレクションごとに分類する方法](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md)に関する記事を参照してください。

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>IMEI または iOS シリアル番号によるデバイスの事前宣言

会社所有のデバイスの International station Mobile Equipment Identity (IMEI) 番号または iOS シリアル番号をインポートすることで、それらのデバイスを識別できます。 デバイスの IMEI 番号を含むコンマ区切り値 (.csv) ファイルをアップロードするか、デバイス情報を手動で入力することができます。 インポートされた情報によって登録するデバイスの所有権が、デバイスの一覧で "企業" として設定されます。 Intune ライセンスも、サービスにアクセスする各ユーザーに必要です。

### <a name="on-premises-health-attestation-service-communication"></a>オンプレミスの正常性構成証明サービスの通信

オンプレミスのインフラストラクチャのみを使用して Windows 10 PC の正常性構成証明サービスの監視を有効にして、インターネットにアクセスできないコンピューターでもデバイス正常性構成証明 (DHA) を報告できるようになりました。

詳細については、「[System Center Configuration Manager の正常性構成証明書](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers)」を参照してください。  

## <a name="remote-control"></a>リモート コントロール
リモート コントロール セッションで共有クリップボードからコンテンツを転送する前に、ユーザーはファイル転送を許可するかどうかを選択できます。 ユーザーはセッションごとに一度アクセス許可を与えるだけで済みます。ビューアーはファイル転送を続行するためのアクセス許可を自身に与えることはできません。 この新しい設定は、**管理**ワークスペースにあります。 **[クライアント設定]** に移動し、 **[既定の設定]** で、 **[リモート ツール]** パネルを開きます。
