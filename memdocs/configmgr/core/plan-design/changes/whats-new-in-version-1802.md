---
title: 新バージョン 1802
titleSuffix: Configuration Manager
description: Configuration Manager のバージョン 1802 で導入された変更点および新機能について説明します。
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0165488946dda924484a53e0e6832ce1d60acded
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702300"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Configuration Manager のバージョン 1802 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1802 はコンソール内の更新プログラムとして利用できます。 バージョン 1702、1706、1710 を実行しているサイトでこの更新プログラムを適用します。 <!-- baseline only statement: -->新しいサイトをインストールするときにも基準のバージョンとしても利用できます。

このリリースには、新機能に加え、バグ修正などの追加の変更も含まれています。 詳細については、「[Configuration Manager Current Branch バージョン 1802 での変更の概要](https://support.microsoft.com/help/4101375)」を参照してください。

このリリースでは、次の追加の更新プログラムも利用できるようになりました。
- [Configuration Manager Current Branch バージョン 1802 の更新プログラムのロールアップ](https://support.microsoft.com/help/4163547)

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用する必要があります。  
>
> 詳細については、下記のリンクをクリックしてください。    
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md)  
> - [サイトで更新プログラムをインストールする](../../servers/manage/updates.md)  
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)

次の各セクションでは、Configuration Manager のバージョン 1802 の変更点と新機能について説明します。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>サイトのインフラストラクチャ

### <a name="reassign-distribution-point"></a>配布ポイントの再割り当て
<!-- 1306937 -->
多くのお客様が大きな Configuration Manager インフラストラクチャを持っており、環境を簡素化するためにプライマリ サイトまたはセカンダリ サイトを減らしています。 それでも、管理されたクライアントにコンテンツを提供するためにブランチ オフィスの所在地で配布ポイントを保持する必要があります。 多くの場合、これらの配布ポイントには数テラバイト以上のコンテンツが含まれています。 これらのリモート サーバーに配布するための時間とネットワーク帯域幅を考えると、このコンテンツにはコストがかかります。 この機能を使用することで、コンテンツを再配布せずに配布ポイントを別のプライマリ サイトに再割り当てできます。 この操作により、サーバー上のすべてのコンテンツを保持したままで、サイト システムの割り当てが更新されます。 詳細については、[配布ポイントの再割り当て](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign)に関するページを参照してください。

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configuration Manager 境界グループを使用するように Windows の配信の最適化を構成する
<!-- 1324696 -->
Configuration Manager の境界グループを使って、企業ネットワークおよびリモート オフィスへのコンテンツ配布を定義して調整します。 [Windows の配信最適化](/windows/deployment/update/waas-delivery-optimization)は、Windows 10 デバイス間でコンテンツを共有するための、クラウド ベースのピア ツー ピア テクノロジです。 このリリース以降、ピア間でコンテンツを共有するときは、境界グループを使うように配信の最適化を構成します。 新しいクライアント設定は、クライアントでの配信最適化グループ識別子として境界グループ識別子を適用します。 クライアントは、配信の最適化クラウド サービスと通信するとき、この識別子を使って目的のコンテンツを含むピアを探します。 詳しくは、「[コンテンツ管理の基本的な概念](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)」を参照してください。

### <a name="support-for-windows-10-arm64-devices"></a>Windows 10 ARM64 デバイスのサポート
<!-- 1353704 -->
このリリースから、Configuration Manager クライアントは Windows 10 ARM64 デバイスでサポートされるようになりました。 既存のクライアント管理機能は、これらの新しいデバイスで動作します。 たとえば、ハードウェアとソフトウェアのインベントリ、ソフトウェア更新プログラム、アプリケーション管理などです。 オペレーティング システムの展開は現在はサポートされていません。 

### <a name="improved-support-for-cng-certificates"></a>CNG 証明書のサポートの強化
<!-- 1357314 -->
Configuration Manager (Current Branch) バージョン 1710 では、[Cryptography:Next Generation (CNG) 証明書](../network/cng-certificates-overview.md)がサポートされています。 バージョン 1710 では、一部のシナリオでクライアント証明書のサポートに制限があります。 

このリリース以降、以下の HTTPS が有効なサーバーの役割には CNG 証明書を使ってください。
- 管理ポイント
- 配布ポイント
- ソフトウェアの更新ポイント
- 状態移行ポイント  


### <a name="boundary-group-fallback-for-management-points"></a>管理ポイントに対する境界グループのフォールバック
<!-- 1324594 -->
[境界グループ](../../servers/deploy/configure/boundary-groups.md)間の管理ポイントのフォールバック関係を構成します。 この動作では、クライアントが使う管理ポイントをいっそうきめ細かく制御できます。 詳細については、[境界グループの構成](../../servers/deploy/configure/boundary-groups.md#management-points)に関するページを参照してください。


### <a name="cloud-distribution-point-site-affinity"></a>クラウド配布ポイントのサイト アフィニティ
<!--503719-->
この機能は、クラウド配布ポイントを利用し、複数のサイトを階層にして地理的に分散している顧客にとって便利です。 インターネットベースのクライアントがコンテンツを探すとき、以前は、クライアントが受け取るクラウド配布ポイントの一覧に指示がありませんでした。 この動作の結果、インターネットベースのクライアントが地理的な離れたクラウド配布ポイントからコンテンツを受け取ることがありました。 そのような離れた場所にあるサーバーからコンテンツをダウンロードすると、近くにあるサーバーからダウンロードする場合に比べ、通常は遅くなります。
 
クラウド配布ポイントのサイト アフィニティを利用すれば、インターネットベースのクライアントは順序付きの一覧を受け取ります。 この一覧では、クライアントに割り当てられたサイトからのクラウド配布ポイントに優先順位が付けられています。 この動作によって、サイト リソースからコンテンツをダウンロードするときの管理者の設計意図が維持されます。
 

## <a name="management-insights"></a>管理分析情報
<!-- 1353967 -->
Configuration Manager のマネジメント インサイトからは、環境の現状に関する情報が提供されます。 この情報は、サイト データベースからのデータの分析に基づきます。 分析情報を利用することで、ご利用の環境についての理解を深め、その情報に基づいてアクションを実行できます。 詳細は、[管理分析情報](../../servers/manage/management-insights.md)に関するページを参照してください。

Configuration Manager 1802 では、次の分析情報を利用できます。
- アプリケーション:
    - 展開のないアプリケーション
- クラウド サービス: <!--1356412-->
    - 共同管理の準備状態を評価する 
    - デバイスをハイブリッド Azure Active Directory に参加できるようにする
    - ID を最新化し、インフラストラクチャを評価する
    -  Windows 10、バージョン 1709 以降にクライアントをアップグレードする 
- コレクション:
    - 空のコレクション
- 簡素化された管理:  <!--1355148-->
    - 旧式のクライアント バージョン  
- ソフトウェア センター: 
    - アプリケーション カタログの代わりにソフトウェア センターにユーザーを誘導する  
    - ソフトウェア センターの新しいバージョンを使用する 
- Windows 10: <!--1357421-->
    - Windows のテレメトリと商用 ID キーを構成する 
    - Configuration Manager と Upgrade Readiness の接続 
   
<!-- ## Migration  -->



## <a name="client-management"></a>クライアント管理

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Azure Resource Manager に対するクラウド管理ゲートウェイのサポート
<!-- 1324735 -->
[クラウド管理ゲートウェイ](../../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) のインスタンスを作成するとき、**Azure Resource Manager の展開**を作成するためのオプションがウィザードで提供されるようになりました。 [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) は、[リソース グループ](/azure/azure-resource-manager/resource-group-overview#resource-groups)と呼ばれる単一のエンティティとしてすべてのソリューション リソースを管理するための最新のプラットフォームです。 Azure Resource Manager で CMG を展開するとき、サイトは Azure Active Directory (Azure AD) を使って必要なクラウド リソースの認証と作成を行います。 この最新の展開では、従来の Azure 管理証明書は必要ありません。 詳細については、[CMG トポロジ設計](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)に関するページを参照してください。

> [!IMPORTANT]
> この機能では、Azure クラウド サービス プロバイダー (CSP) のサポートは有効になりません。 Azure Resource Manager での CMG の展開では引き続き従来のクラウド サービスが使われ、CSP はこれをサポートしません。 詳細については、「[Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)」 (Azure CSP で使用可能な Azure サービス) を参照してください。  

### <a name="improvements-to-cloud-management-gateway"></a>クラウド管理ゲートウェイの機能改善  

- このリリースから、**クラウド管理ゲートウェイ**はプレリリース機能ではなくなりました。  

- 機能文書が改訂され、改善されています。 詳細については、以下の記事を参照してください。
    - [クラウド管理ゲートウェイの計画](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [クラウド管理ゲートウェイのサイズとスケールの数値](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [クラウド管理ゲートウェイのセキュリティとプライバシー](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [クラウド管理ゲートウェイについてよくあるご質問](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [クラウド管理ゲートウェイの証明書](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [Set up cloud management gateway](../../clients/manage/cmg/setup-cloud-management-gateway.md) (クラウド管理ゲートウェイの設定)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>255 文字以上の文字列を収集するようにハードウェア インベントリを構成する
<!-- 1357389 -->
ハードウェア インベントリ プロパティに対して、文字列の長さを 255 文字以上に構成できます。 この変更は、新しく追加されたクラスと、キーではないハードウェア インベントリ プロパティに対してのみ適用されます。 詳細については、[ハードウェア インベントリの拡張](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255)に関する記事を参照してください。 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Linux と Unix のクライアント サポートの廃止告知
 <!--510139-->
Microsoft は、今からおよそ 1 年のうちに、Configuration Manager での Linux と UNIX のクライアント サポートを非推奨とする方針を立てています。2019 年の早期に予定されているバージョン 1902 には Linux と UNIX のクライアントが含まれません。 2018 年の後半に予定されている Configuration Manager 1810 リリースが Linux クライアントと UNIX クライアントを含む最後のリリースになります。Configuration Manager 1810 のライフサイクル全体でサポートされる予定です。 Configuration Manager 1810 以降、ユーザーは Linux サーバーを管理するために Microsoft Azure 管理を検討する必要があります。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。

### <a name="surface-device-dashboard"></a>Surface デバイス ダッシュボード
<!--1355788-->
Surface デバイス ダッシュボードには、お使いの環境内で見つかった Surface デバイスに関する情報が表示されます。 コンソールでは、 **[監視]**  >  **[Surface Devices]\(Surface デバイス\)** の順に進みます。 次のような項目を表示できます。
- Surface の割合
- Surface モデルの割合
- 上位 5 つのファームウェアのバージョン

詳細については、[Surface ダッシュボード](../../clients/manage/surface-device-dashboard.md)に関する記事を参照してください。

### <a name="change-in-the-configuration-manager-client-install"></a>Configuration Manager クライアント インストールにおける変更
<!--1356195-->
このリリース以降、Silverlight はクライアント デバイスに自動インストールされません。 詳細については、[Windows コンピューターにクライアントを展開するための前提条件](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies)に関するページを参照してください。

## <a name="co-management"></a>共同管理

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>共同管理を使用して Intune に Endpoint Protection ワークロードを移行する
<!-- 1357365 -->
 共同管理を有効にした後、Endpoint Protection のワークロードを Intune に移行できます。 Endpoint Protection ワークロードを移行するには、共同管理のプロパティ ページに移動し、スライダー バーを Configuration Manager から **[パイロット]** または **[すべて]** に移動します。 ワークロードの詳細については、[共同管理ワークロード](../../../comanage/workloads.md)に関するページを参照してください。 共同管理の詳細については、「[Windows 10 デバイスの共同管理](../../../comanage/overview.md)」を参照してください。
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Configuration Manager の共同管理ダッシュボード
<!--1356648-->
このリリースより、共同管理に関する情報をダッシュボードに表示できます。 ダッシュボードを利用すれば、お使いの環境で共同管理しているコンピューターを確認できます。 各種グラフを見ることで、対処が必要なデバイスを特定できます。 詳細については、[共同管理ダッシュボード](../../../comanage/how-to-monitor.md#co-management-dashboard)に関する記事を参照してください。 


## <a name="compliance-settings"></a>コンプライアンス設定

### <a name="microsoft-edge-browser-policies"></a>Microsoft Edge ブラウザーのポリシー
<!-- 1357310 -->
Windows 10 クライアントで [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web ブラウザーを使用する場合、Configuration Manager のコンプライアンス設定ポリシーを作成し、Microsoft Edge の一部の設定を構成します。 詳細については、[Microsoft Edge ブラウザー プロファイルの作成](../../../compliance/deploy-use/browser-profiles.md)に関するページを参照してください。 



## <a name="application-management"></a>アプリケーション管理

### <a name="allow-user-interaction-when-installing-an-application"></a>アプリケーションをインストールするときに、ユーザー操作を許可する
<!-- 1356976 -->
タスク シーケンスの実行中にアプリケーションのインストールと対話することをエンド ユーザーに許可します。 たとえば、さまざまなオプションの入力をエンド ユーザーに求めるセットアップ プロセスを実行します。 一部のアプリケーション インストーラーでは、ユーザー プロンプトを消せなかったり、インストール プロセスでユーザーだけが知っている特定の構成値が求められたりする場合があります。 この機能では、これらのインストール シナリオを処理することができます。 詳細については、「[展開の種類のユーザー エクスペリエンス オプションを指定する](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux)」を参照してください。

### <a name="do-not-automatically-upgrade-superseded-applications"></a>置き換えられたアプリケーションを自動的にアップグレードしない
<!-- 1351266 -->
置き換えられるバージョンを自動的にアップグレードしないように、アプリケーションの展開を構成します。 展開を作成する際に、**ソフトウェアの展開ウィザード**の **[展開設定]** ページで、**利用可能な**インストールのために、 **[このアプリケーションの置き換えられるバージョンを自動的にアップグレードする]** のオプションを有効または無効にできるようになりました。 詳細については、「[展開の設定を指定する](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)」をご覧ください。

### <a name="approve-application-requests-for-users-per-device"></a>デバイスごとにユーザーのアプリケーション要求を承認する
<!-- 1357015 -->
このリリース以降では、承認を必要とするアプリケーションをユーザーが要求したとき、特定のデバイス名が要求の一部になります。 管理者が要求を承認した場合、ユーザーはそのデバイスにのみアプリケーションをインストールできます。 別のデバイスにアプリケーションをインストールするには、ユーザーは別の要求を送信する必要があります。 詳細については、「[展開の設定を指定する](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)」をご覧ください。

 > [!Note]  
 > これはオプション機能です。 詳細については、「[Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。  


### <a name="run-scripts-improvements"></a>スクリプト実行の機能強化 
<!-- 1236459 -->
 このリリースから、**スクリプトの実行**はプレリリース機能ではなくなりました。 スクリプト出力が JSON 書式設定を利用して返されるようになりました。 詳細については、「[Configuration Manager コンソールから PowerShell スクリプトを作成して実行する](../../../apps/deploy-use/create-deploy-scripts.md)」を参照してください。


## <a name="operating-system-deployment"></a>オペレーティング システムの展開

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>クラウド管理ゲートウェイ経由での Windows 10 一括アップグレード タスク シーケンス
<!-- 1357149 -->
Windows 10 の[一括アップグレード タスク シーケンス](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)で、[クラウド管理ゲートウェイ](../../clients/manage/cmg/plan-cloud-management-gateway.md)を通して管理されるインターネット ベースのクライアントへの展開がサポートされるようになります。 この機能により、リモート ユーザーはいっそう簡単に Windows 10 にアップグレードできるようになり、企業ネットワークに接続しなくてもよくなります。 詳細については、「 [Deploy a task sequence](../../../osd/deploy-use/deploy-a-task-sequence.md)」をご覧ください。

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 一括アップグレード タスク シーケンスの機能強化
<!-- 1357425 -->
Windows 10 の一括アップグレード用の既定のタスク シーケンス テンプレートに、アップグレード プロセスの前後に追加する推奨アクションを含む追加グループが含まれるようになりました。 これらのアクションは、Windows 10 にデバイスを正常にアップグレードしている多くのユーザーに共通するものです。 詳細については、「[OS をアップグレードするタスク シーケンスの作成](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade)」を参照してください。

### <a name="improvements-to-operating-system-deployment"></a>オペレーティング システムの展開に関する機能拡張
このリリースでは、オペレーティング システムの展開が次の点で改善されています。
- Windows PE では、cmtrace.exe の起動時に、このプログラムをログ ファイルの既定のビューアーにするかどうかを選択するように求められることがなくなりました。 <!-- SMS 500897 -->
- タスク シーケンス ステップの[パッケージ コンテンツのダウンロード](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent)にブート イメージを追加します。
- [タスク シーケンスの実行](../../../osd/understand/task-sequence-steps.md#child-task-sequence)ステップの機能強化: <!-- 1261338 -->   
  - ソフトウェア センター、PXE、およびメディアからのすべてのオペレーティング システムの展開シナリオのサポート。
  - オブジェクトの削除中にコピー、インポート、エクスポート、および警告などのコンソール操作の改善。
  - [[事前定義済みコンテンツ ファイルの作成]](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) ウィザードのサポート。
  - 展開の検証との統合。 詳細については、[危険度の高いタスク シーケンスの展開](../../../osd/deploy-use/deploy-a-task-sequence.md)に関するページを参照してください。 
  - タスク シーケンスの実行ステップが、単一の親子関係だけでなく、タスク シーケンスの複数のレベル間で使用できるようになりました。 複数レベルの関係は複雑さが増すため、注意して使用してください。 これらの関係は引き続き循環参照がチェックされます。

### <a name="deployment-templates-for-task-sequences"></a>タスク シーケンスの展開テンプレート
<!-- 1357391 -->
[タスク シーケンスの展開ウィザード](../../../osd/deploy-use/deploy-a-task-sequence.md)は、展開テンプレートを作成できるようになりました。 展開テンプレートを保存して、展開を作成する既存または新規のタスク シーケンスに適用できます。 

### <a name="phased-deployments-for-task-sequences"></a>タスク シーケンスの段階的展開
<!--1356837-->
 段階的な展開は[プレリリース機能](../../servers/manage/pre-release-features.md)です。 段階的展開は、複数のコレクションでのタスク シーケンスの調整および順序付けされたロールアウトを自動化します。 既定の 2 段階で[段階的展開を作成](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)するか、複数の段階を手動で構成できます。 タスク シーケンスの段階的展開は、PXE またはメディア インストールに対応していません。




## <a name="software-center"></a>ソフトウェア センター

### <a name="install-multiple-applications-in-software-center"></a>ソフトウェア センターで複数のアプリケーションをインストールする
<!-- 1357126 -->
エンド ユーザーまたはデスクトップ技術者がデバイスに複数のアプリケーションをインストールする必要がある場合、ソフトウェア センターで複数の選択されたアプリケーションのインストールがサポートされるようになりました。 この動作では、1 つのインストールが完了するのを待ってから次のインストールを開始するのではないため、ユーザーの効率を上げることができます。 詳細については、新しいソフトウェア センター ユーザー ガイドで[複数のアプリケーションのインストール](../../understand/software-center.md#install-multiple-applications)に関するセクションを参照してください。

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>ソフトウェア センターを使用してユーザーが利用できるアプリケーションを参照し、Azure AD に参加しているデバイスにインストールする
<!-- 1322613 -->
ユーザーが利用できるようにアプリケーションを展開した場合、ユーザーは Azure Active Directory (Azure AD) デバイスのソフトウェア センターでアプリケーションを参照してインストールできるようになりました。 詳細については、[Azure AD 参加デバイスにユーザーが利用できるアプリケーションを展開する方法](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)に関するページを参照してください。

### <a name="hide-installed-applications-in-software-center"></a>ソフトウェア センターでインストール済みのアプリケーションを非表示にする
<!--1357592-->
インストールされているアプリケーションをソフトウェア センターで非表示にできるようになりました。 クライアント設定でこのオプションを有効にすると、既にインストールされているアプリケーションが、[アプリケーション] タブに表示されなくなります。 Configuration Manager 1802 をインストールすると、あるいはこのバージョンにアップグレードすると、このオプションが既定として設定されます。  インストールされているアプリケーションは、[インストールの状態] タブで引き続き確認できます。「[ソフトウェア センターでインストール済みのアプリケーションを非表示にする](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled)」に詳細があります。   

### <a name="hide-unapproved-applications-in-software-center"></a>ソフトウェア センターで承認されていないアプリケーションを非表示にする
 <!--1355146-->
このクライアント設定オプションを有効にすると、承認を必要とするユーザーの使用可能なアプリケーションがソフトウェア センターでは非表示になります。  「[ソフトウェア センターで承認されていないアプリケーションを非表示にする](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved)」に詳細があります。  

### <a name="software-center-shows-user-additional-compliance-information"></a>ソフトウェア センターにユーザーの追加のコンプライアンス情報が表示される
<!-- 1235616 -->
 会社のリソースに対する条件付きアクセスのコンプライアンス ポリシー ルールとしてデバイス正常性構成証明ステータスを使用すると、システム センターに、ポリシーに準拠していないデバイス正常性構成証明書設定が表示されるようになりました。


 ## <a name="software-updates"></a>ソフトウェア更新プログラム 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>基準日からのオフセットを指定して自動展開規則の評価をスケジュールします。 
<!--1357133-->
自動展開規則の評価は、基本の日からのオフセットを指定してスケジュールできます。 つまり、火曜日のパッチが実際には水曜日になる場合、1 日オフセットし、評価スケジュールを月の第 2 火曜日に設定できます。 詳細については、「[ソフトウェア更新プログラムの自動展開](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule)」をご覧ください。 



## <a name="reporting"></a>レポート

### <a name="report-for-default-browser-counts"></a>既定のブラウザー数についてのレポート
<!-- 1357830 -->
特定の Web ブラウザーが Windows の既定値になっているクライアントの数を表示する新しいレポートが追加されました。 **ソフトウェア - 会社と製品**レポート グループの**既定のブラウザー カウント** レポートを参照してください。 詳細については、[レポートの一覧](../../servers/manage/list-of-reports.md#software---companies-and-products)を参照してください。

### <a name="report-on-windows-autopilot-device-information"></a>Windows Autopilot のデバイス情報についてのレポート
<!-- 1351442 -->
Windows Autopilot は、最新の方法で新しい Windows 10 デバイスをオンボーディングおよび構成するためのソリューションです。 詳細については、「[Windows Autopilot の概要](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot)」を参照してください。 既存のデバイスを Windows Autopilot に登録する 1 つの方法は、ビジネス向け Microsoft Store および教育機関向け Microsoft Store にデバイスの情報をアップロードすることです。 この情報には、デバイスのシリアル番号、Windows 製品識別子、およびハードウェア ID が含まれます。 Configuration Manager を利用し、**ハードウェア - 全般**レポート ノードの新しいレポート、**Windows Autopilot デバイス情報**でこのデバイスの情報を収集し、報告します。 詳細については、共同管理の準備での「[How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#windows-autopilot)」 (共同管理用のインターネット ベースのデバイスを準備する方法) を参照してください。

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>特定のコレクションに対する Windows 10 サービスの詳細を報告する
<!--1357653-->
**特定のコレクションに対する Windows 10 サービスの詳細**レポートには、特定のコレクションに対する Windows 10 サービスに関する全般情報が表示されます。 このレポートには、リソース ID、NetBIOS 名、OS 名、OS リリース名、ビルド、OS ブランチ、および Windows 10 デバイスのサービス状態が表示されます。 詳細については、[レポートの一覧](../../servers/manage/list-of-reports.md#operating-system)を参照してください。



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>デバイスを保護する

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Windows Defender Exploit Guard に対する Configuration Manager ポリシーの機能強化
<!-- 1356220 -->
[攻撃の回避](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR)および[フォルダー アクセスの制御](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA)コンポーネントに対する新しいポリシー設定が、[Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction) 用に Configuration Manager に追加されました。

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Windows Defender Application Guard の新しいホスト対話設定
<!-- 1356256 -->
Windows 10 バージョン 1709 以降のデバイスには、[Windows Defender Application Guard](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS) の新しい 2 つのホスト対話設定があります。 
- Web サイトに、ホストの仮想グラフィック プロセッサへのアクセスを許可することができます。 
- コンテナー内にダウンロードされたファイルをホストで保持することができます。 




## <a name="configuration-manager-console"></a>Configuration Manager コンソール

### <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager コンソールの機能拡張 
このリリースでは、Configuration Manager コンソールが次の点で機能強化されています。
- [資産とコンプライアンス]、[デバイス] の下の [デバイス] リストに既定でプライマリ ユーザーが表示されるようになりました。 この列は [デバイス] ノードでのみ表示されます。 最後にログオンしたユーザーを省略可能な列として追加することもできます。<!-- 1357280 --> サイトのクライアント設定、[[ユーザーとデバイスのアフィニティ]](../../clients/deploy/about-client-settings.md#user-and-device-affinity) を有効にして、プライマリ ユーザーとデバイスを関連付けます。
- コレクションが別のコレクションのメンバーである場合、その名前を変更すると、メンバーシップの規則に従って新しい名前が更新されます。<!--1357282--> 
- DPI スケールが異なる複数のモニターでクライアントをリモート制御しているとき、マウスのカーソルがモニター間で正しくマッピングされるようになりました。 <!--433170-->
- [Office 365 クライアント管理ダッシュボード](../../../sum/deploy-use/office-365-dashboard.md)に、グラフ セクションが選択されたときに関連するデバイスのリストが表示されます。 <!--1357281 --> 



## <a name="next-steps"></a>次のステップ
このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラム](../../servers/manage/updates.md)に関するページを参照してください。
