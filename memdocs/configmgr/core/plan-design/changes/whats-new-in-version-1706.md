---
title: 新バージョン 1706
titleSuffix: Configuration Manager
description: Configuration Manager のバージョン 1706 で導入された変更点および新機能について説明します。
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f6087011a0390997d704278af6ffd5e6071bf031
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129020"
---
# <a name="what39s-new-in-version-1706-of-configuration-manager"></a>Configuration Manager のバージョン 1706 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1706 は、バージョン 1606、1610、または 1702 を実行しているインストール済みのサイトで、コンソール内の更新プログラムとして利用可能です。

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用する必要があります。  
>
> 詳細については、下記のリンクをクリックしてください。    
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md)  
> - [サイトで更新プログラムをインストールする](../../servers/manage/updates.md)  
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)  

以降のセクションでは、Configuration Manager のバージョン 1706 の変更点および導入された新機能について詳しく説明します。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>サイトのインフラストラクチャ

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>クライアント ピア キャッシュで、Windows 10 と Office 365 の高速インストール ファイルに対応  
<!-- 1352486 -->
今回のリリースから、ピア キャッシュで、Windows 10 のコンテンツ高速インストール ファイルと Office 365 の更新ファイルを配信できるようになりました。 この変更サポートするために追加の構成は必要ありません。

### <a name="updates-for-the-data-warehouse"></a>データ ウェアハウスの更新
<!-- 1277922 -->
データ ウェアハウスは、プレリリース版の機能ではなくなりました。 さらに、SQL Server Always On 可用性グループとフェールオーバー クラスターのデータベースのサポートを含めるように前提条件を更新しました。 詳細については、「[データ ウェアハウス サービス ポイント](../../servers/manage/data-warehouse.md)」を参照してください。

### <a name="accessibility-improvements"></a>アクセシビリティの機能強化
<!-- 1253000 -->
Configuration Manager コンソールのユーザー補助機能の機能強化を追加しました。 詳細については、「[ユーザー補助機能](../../understand/accessibility-features.md)」を参照してください。

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性グループの機能強化
<!-- 1352094 -->
このリリースでは、Configuration Manager で使用する SQL Server Always On 可用性グループで非同期コミット レプリカを使用できるようになりました。 これにより、オフサイトの (リモート) バックアップとして使用する追加のレプリカを可用性グループに追加して、それらをディザスター リカバリー シナリオで使用することができます。  
- Configuration Manager は、同期レプリカを復旧するために非同期コミット レプリカの使用をサポートしています。 これを実行する方法については、バックアップと回復に関するトピックで[サイト データベースの回復オプション](../../servers/manage/recover-sites.md#site-database-recovery-options)を参照してください。
- このリリースでは、非同期コミット レプリカをサイト データベースとして使用するためのフェールオーバーはサポートされていません。
詳細については、「[Configuration Manager で SQL Server Always On 可用性グループを使用するための準備](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)」を参照してください。

### <a name="update-reset-tool"></a>更新のリセット ツール
<!-- 1324589 -->
バージョン 1706 以降、Configuration Manager のプライマリ サイトと中央管理サイトには、Configuration Manager 更新のリセット ツール **CMUpdateReset.exe** が含まれています。 Current Branch のいずれかのバージョンでこのツールを使用し、コンソール内の更新のダウンロードをまたはレプリケーションの問題がある場合に問題を修正します。 詳細については、「[更新のリセット ツール](../../servers/manage/update-reset-tool.md)」を参照してください。

### <a name="high-dpi-console-support"></a>高 DPI コンソールのサポート  
<!-- 1353476 -->
このリリースでは、高 DPI デバイス (Surface Book など) で表示したときに、Configuration Manager コンソールのスケーリング方法と、UI のさまざまな部分を表示する方法に修正すべき問題があります。

### <a name="improved-boundary-groups-for-software-update-points"></a>ソフトウェアの更新ポイントのための境界グループの改善
<!-- 1324591 -->
このリリースでは、ソフトウェアの更新ポイントでの境界グループの使用方法が改善されています。 新しいフォールバック動作を次にまとめます。
- ソフトウェアの更新ポイントのフォールバックで、近隣境界グループへのフォールバックに時間構成を使用するようになりました。
- フォールバックの構成に関係なく、クライアントは、使用した最後のソフトウェアの更新ポイントへの到達を 120 分間試行します。 120 分以内にそのサーバーに到達できない場合は、新しいサーバーを見つけるため、クライアントは利用可能なソフトウェアの更新ポイントのプールをチェックします。
- 2 時間で元のサーバーに到達できない場合、クライアントは、新しいソフトウェアの更新ポイントに接続するためにより短いサイクルに切り替えます。 つまり、クライアントは新しいサーバーとの接続に失敗すると、使用可能なサーバー プールからすぐに次のサーバーを選択して、接続を試行します。

詳細については、Current Branch の境界グループに関するトピックの[ソフトウェアの更新ポイント](../../servers/deploy/configure/boundary-groups.md#bkmk_sup)の記述を参照してください。

### <a name="azure-ad-integration-with-configuration-manager"></a>Azure AD と Configuration Manager の統合
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
このリリースでは、Configuration Manager と Azure Active Directory (Azure AD) の統合を改善しました。  この改善により、Configuration Manager で使用する Azure サービスの構成方法を効率化し、Azure AD を介して認証するクライアントとユーザーの管理を容易にすることができます。

改善された統合により以下のことが可能になります。  
- Azure サービス ウィザード - このウィザードは、Configuration Manager で使用する以下の Azure サービスを設定するための個々のワークフローに代わる、共通の構成エクスペリエンスを提供します。
  - **クラウド管理**Azure Active Directory (Azure AD) を利用し、クライアントの認証を有効にします。 Azure AD ユーザー探索を構成することもできます。
  - **Log Analytics コネクタ** Azure Log Analytics に接続してコレクション データを同期します。
  - **Upgrade Readiness** Upgrade Readiness に接続し、クライアント アップグレード互換性データを表示します。
  - **Windows Store for Business** Windows Store for Business のオンライン ストアに接続し、Configuration Manager でデプロイできるアプリを組織のために入手します。


  このエクスペリエンスは、これまで、新しい Configuration Manager のコンポーネントや Azure のサービスを設定するたびに入力していたサブスクリプションや構成の詳細を提供する [Azure サーバー Web アプリ](/azure/app-service/app-service-authentication-overview)によって実現されます。 詳細については、「[Azure サービス ウィザード](../../servers/deploy/configure/azure-services-wizard.md)」を参照してください。

- Configuration Manager サイトにアクセスするには、Azure AD を使用してインターネット上のクライアントを認証します。 Azure AD を使用すると、クライアント認証証明書を構成して使用する必要がなくなります。 これには、クラウド管理ゲートウェイ サイト システムの役割が必要です。 詳細については、「[認証のため Azure AD を使用して、インターネットから Configuration Manager クライアントをインストールして割り当てる](../../clients/deploy/deploy-clients-cmg-azure.md)」を参照してください。

- Configuration Manager クライアントをインターネットに配置されているコンピューターにインストールして管理します。 これには、クラウド管理ゲートウェイ サイト システムの役割を使用する必要があります。 詳細については、「[認証のため Azure AD を使用して、インターネットから Configuration Manager クライアントをインストールして割り当てる](../../clients/deploy/deploy-clients-cmg-azure.md)」を参照してください。

- Azure AD ユーザー探索を構成する  Azure サービス ウィザードを使用して、この新しい探索方法を構成します。 この新しい方法は、Azure AD でユーザー データのクエリを行い、従来の探索データと併用することができます。  完全と差分の両方の同期がサポートされています。  詳細については、「[Azure AD ユーザー探索](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)」を参照してください。

### <a name="peer-cache-improvements"></a>ピア キャッシュの改善
<!-- 1252345 -->
ピア キャッシュはピアからのダウンロード要求を認証するためにネットワーク アクセス アカウントを使用しなくなりました。 クライアントで引き続きアカウントは必要な場合、1 つの注意事項があります。 これにより、WinPE で起動し、ピア キャッシュ ソースからコンテンツにアクセスするクライアントの要件が残ります。 詳細については、「[ピア キャッシュの要件と考慮事項](../hierarchy/client-peer-cache.md#requirements)」を参照してください。


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>コンプライアンス設定

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Configuration Manager クライアントを使用して管理されていない Windows 10 デバイスの新しい構成設定
<!-- 1354715 -->
このリリースでは、Intune に登録されるか、Configuration Manager でオンプレミスで管理されている Windows 10 デバイス用の新しい構成項目設定が追加されました。 設定は、次のとおりです。

- **パスワード**
  - デバイスの暗号化
- **デバイス**
  - 地域の設定の変更 (デスクトップのみ)
  - 電源とスリープの設定の変更
  - 言語の設定の変更
  - システム時刻の変更
  - デバイス名の変更
- **ストア**
  - ストア アプリの自動更新
  - プライベート ストアのみを使用する
  - ストアから配信されたアプリの起動
- **Microsoft Edge**
  - About Flags へのアクセスをブロック
  - SmartScreen のプロンプトのオーバーライド
  - ファイルに対する SmartScreen プロンプトのオーバーライド
  - WebRtc localhost IP アドレス
  - 既定の検索エンジン
  - OpenSearch XML URL
  - ホームページ (デスクトップのみ)

Windows 10 の設定の詳細については、「[Configuration Manager クライアントを使用せずに管理されている Windows 8.1 デバイスと Windows 10 デバイスの構成項目を作成する方法](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)」を参照してください。

### <a name="new-device-compliance-policy-rules"></a>新しいデバイス コンプライアンス ポリシー ルール

* **必要なパスワードの種類**。 ユーザーが英数字のパスワードまたは数字のパスワードのどちらを使用する必要があるかを指定します。 英数字のパスワードの場合、パスワードに最低限必要な文字セットの数も指定します。 次の 4 つの文字セットがあります。小文字、大文字、記号、および数字です。

  **以下でサポートされています。**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
  <br></br>
* **デバイスでの USB デバッグをブロックする**。 USB デバッグは Android for Work デバイスでは既に無効になっているため、この設定を構成する必要はありません。

  **以下でサポートされています。**
  * Android 4.0 以降
  * Samsung KNOX Standard 4.0+
  <br></br>
* **提供元不明のアプリをブロックする**。 デバイスが不明なソースからのアプリのインストールを許可しないことが必要です。 Android for Work デバイスでは、不明なソースからのインストールは常に制限されるため、この設定を構成する必要はありません。

  **以下でサポートされています。**
  * Android 4.0 以降
  * Samsung KNOX Standard 4.0+
  <br></br>
* **アプリの脅威のスキャンが必要**。 この設定は、デバイスでアプリの確認機能が有効になっていることを指定します。

  **以下でサポートされています。**
  * Android 4.2 から 4.4
  * Samsung KNOX Standard 4.0+


## <a name="application-management"></a>アプリケーション管理

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Configuration Manager コンソールから PowerShell スクリプトを実行する
<!-- 1236459 -->

Configuration Manager では、パッケージとプログラムを使用してクライアント デバイスにスクリプトを展開することができます。 このリリースでは、次の操作を実行するための新機能が追加されました。

- PowerShell スクリプトを Configuration Manager にインポートする
- Configuration Manager コンソールからスクリプトを編集する (署名されていないスクリプトのみ)
- セキュリティを強化するため、スクリプトを承認または拒否としてマークする
- Windows クライアント コンピューターのコレクションおよびオンプレミスの管理対象 Windows PC でスクリプトを実行する。 スクリプトを展開しない代わりに、スクリプトはクライアント デバイスでほぼリアルタイムで実行されます。
- Configuration Manager コンソールで、スクリプトによって返される結果を確認する

詳細については、「[Configuration Manager コンソールから PowerShell スクリプトを作成して実行する](../../../apps/deploy-use/create-deploy-scripts.md)」を参照してください。

### <a name="new-mobile-application-management-policy-settings"></a>新しいモバイル アプリケーション管理ポリシーの設定    
<!--1324760-->
このリリースから、3 つの新しいモバイル アプリケーション管理 (MAM) ポリシー設定が使用できます。

- **画面キャプチャの禁止 (Android デバイスのみ):** このアプリを使用するときに、デバイスの画面キャプチャ機能をブロックするように指定します。


## <a name="operating-system-deployment"></a>オペレーティング システムの展開

### <a name="hardware-inventory-collects-secure-boot-information"></a>ハードウェア インベントリでのセキュア ブート情報の収集
ハードウェア インベントリは、クライアントでセキュア ブートが有効になっているかどうかの情報を収集します。 この情報は、**SMS_Firmware** クラス (バージョン 1702 で導入) に格納されており、ハードウェア インベントリでは既定で有効になっています。 ハードウェア インベントリの詳細については、[ハードウェア インベントリを構成する方法](../../clients/manage/inventory/configure-hardware-inventory.md)に関する記事を参照してください。

### <a name="collapsible-task-sequence-groups"></a>折りたたみ可能なタスク シーケンス グループ
このバージョンでは、タスク シーケンス グループを展開および折りたたむ機能が導入されています。 個々のグループを展開または折りたたんだり、すべてのグループを一度に展開または折りたたんだりすることができます。

### <a name="reload-boot-images-with-current-windows-pe-version"></a>最新バージョンの Windows PE を使用してブート イメージを再読み込みする
選択したブート イメージ上で **[配布ポイントの更新]** を実行した場合、そのブート イメージ内の (Windows ADK インストール ディレクトリにある) 最新バージョンの Windows PE を再読み込みできます。 詳細については、「[Update distribution points with the boot image](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)」(ブートイメージによる配布ポイントの更新) を参照してください。

## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="improvements-to-express-update-download-time"></a>Express Update のダウンロード時間の短縮
このリリースでは、Express Update のダウンロードにかかる時間を大幅に短縮しました。 詳細については、「[Windows 10 更新プログラムに対する高速インストール ファイルの管理](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md)」を参照してください。

### <a name="manage-microsoft-surface-driver-updates"></a>Microsoft Surface ドライバーの更新プログラムの管理
<!-- 1098490 -->
Configuration Manager を使用して、Microsoft Surface ドライバーの更新プログラムを管理できるようになりました。    


#### <a name="prerequisites"></a>[前提条件]
- すべてのソフトウェアの更新ポイントで Windows Server 2016 を実行している必要があります。    
- これは、使用するために有効にする必要があるプレリリース機能です。 詳細については、「[更新プログラムからプレリリース機能を使用する](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)」を参照してください。

#### <a name="to-manage-surface-driver-updates"></a>Surface ドライバーの更新プログラムを管理するには

1. Microsoft Surface ドライバーの同期を有効にします。 [分類と製品の構成](../../../sum/get-started/configure-classifications-and-products.md)の手順を使用して、 **[分類]** タブで **[Microsoft Surface のドライバーとファームウェアの更新プログラムを含める]** チェックボックスをオンにして、Surface ドライバーを有効にします。
2. [Microsoft Surface ドライバーを同期します](../../../sum/get-started/synchronize-software-updates.md)。
3. [同期した Microsoft Surface ドライバーを展開します](../../../sum/deploy-use/deploy-software-updates.md)。

### <a name="configure-windows-update-for-business-deferral-policies"></a>Windows Update for Business 遅延ポリシーの構成
<!-- 1290890 -->
Windows Update for Business によって直接管理されている Windows 10 デバイスの Windows 10 機能更新プログラムまたは品質更新プログラムに対し、遅延ポリシーを構成できるようになりました。 遅延ポリシーの管理は、 **[ソフトウェア ライブラリ]**  >  **[Windows 10 のサービス]** の下の新しい **[Windows Update for Business ポリシー]** ノードでできます。

詳細については、「[Windows 10 における Windows Update for Business との統合](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies)」を参照してください。

### <a name="improved-user-notifications-for-office-365-updates"></a>Office 365 更新プログラムのユーザーへの通知の改善
クライアントが Office 365 更新プログラムをインストールする場合に、Office クイック実行ユーザー エクスペリエンスを活用するように改善されました。 これには、ポップアップとアプリ内通知、およびカウントダウン エクスペリエンスが含まれます。 詳細については、「[Office 365 の更新プログラムの動作とクライアント通知を再起動する](../../../sum/deploy-use/manage-office-365-proplus-updates.md)」

## <a name="reporting"></a>レポート

### <a name="use-windows-analytics-with-configuration-manager"></a>Configuration Manager で Windows Analytics を使用する
<!-- 1318608 -->
Windows Analytics は、環境の現在の状態に関する有益な分析情報が得られるソリューションのセットです。 環境内のデバイスでは、Windows の利用統計情報がレポートされます。 データには、Azure portal からアクセスできます。 Upgrade Readiness の場合は、データは、Configuration Manager コンソールの監視ノードで直接使用できます。


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>モバイル デバイス管理

### <a name="updates-to-android-for-work-sharing-configuration"></a>Android for Work の共有構成の更新
<!-- 1338403 -->
このリリースでは、 **[仕事用プロファイル]** 設定グループの **[仕事用プロファイルと個人プロファイル間でのデータ共有を許可する**] 設定の値が更新されました。 仕事用プロファイルと個人用プロファイルの間のコピーおよび貼り付けをブロックするユーザー設定も追加されました。


### <a name="android-and-ios-enrollment-restrictions"></a>Android および iOS の登録制限
<!-- 1290826 -->
このリリースでは、管理者は、ユーザーが個人の Android または iOS デバイスを登録できないことを指定できるようになりました。 新しいデバイス制限の設定を使用して、Android デバイスの登録を、事前に宣言されたデバイスに制限できます。 iOS デバイスの場合は、Apple の Device Enrollment Program、Apple Configurator、または Intune のデバイス登録マネージャー アカウントを使用して登録されているデバイスを除くすべてのデバイスの登録をブロックできます。

## <a name="protect-devices"></a>デバイスを保護する

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Device Guard ポリシーに特定のファイルとフォルダーの信頼を含める
<!--1324676-->
このリリースでは、Device Guard ポリシー管理に機能が追加されています。

必要に応じて、Device Guard ポリシー内のフォルダーの特定のファイルに信頼を追加できるようになりました。 これにより、次のことが可能になります。

- 管理されたインストーラーの動作で問題を解決する
- Configuration Manager で展開できない基幹業務アプリを信頼する
- オペレーティング システムの展開イメージに含まれているアプリを信頼する

詳細については、「[Configuration Manager を使用した Device Guard 管理](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)」を参照してください。
