---
title: エンドポイント分析のプレビュー
titleSuffix: Configuration Manager
description: エンドポイント分析のプレビューの手順です。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 6f481fa54a8018137a4b45bc62f6fde9c1f1165b
ms.sourcegitcommit: 7b224e138c0618e978be59832b3486f3745abacc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83381582"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a> エンドポイント分析のプレビュー

> [!Note]  
> この情報は、製品版のリリース前に大幅に変更される可能性があるプレビュー機能に関連します。 Microsoft は、ここで提供される情報に関して、明示または黙示を問わず、いかなる保証も行いません。 
>
> エンドポイント分析の変更点の詳細については、「[エンドポイント分析の新機能](whats-new-endpoint-analytics.md)」を参照してください。 
>
>エンドポイント分析のプライベート プレビューに参加したい場合は、詳細を[この形式で](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9-ZzmlTlbJMh03eDDHtO81UOERLUkMzNFZKSlBaNFNFUVhFSlE0MzNYMS4u)入力してください。 テナントは、プレビューの初公開が展開されるとフライト化されます。


## <a name="endpoint-analytics-overview"></a>エンドポイント分析の概要

エンド ユーザーにとって、長いブート時間やその他の中断を経験することは珍しいことではありません。 このような中断は、次の組み合わせが原因で発生する可能性があります。

- レガシ ハードウェア
- エンド ユーザーのエクスペリエンスに最適化されていないソフトウェア構成
- 構成の変更および更新に起因する問題

これらの問題やエンド ユーザーのエクスペリエンスに関するその他の問題が持続する原因は、IT 部門がエンド ユーザーのエクスペリエンスを十分に把握できていないためです。 一般に、このような問題を把握するための唯一の方法は低速でコストのかかるサポート チャネルであり、通常、それによって、何を最適化するべきかについて明確な情報が提供されることはありません。 このような問題のコストを負担するのは、IT サポートだけではありません。 インフォメーション ワーカーが問題を処理するのに使う時間にも、高いコストがかかります。 ユーザーの生産性を低下させるパフォーマンス、信頼性、サポートに関する問題は、組織の最終的な収益にも大きな影響を与える可能性があります。

**エンドポイント分析**は、ユーザー エクスペリエンスに関する分析情報を提供することで、ユーザーの生産性を向上させ、IT サポートのコストを削減することを目的としています。 IT 部門は、この分析情報を使用して、プロアクティブなサポートによりエンド ユーザー エクスペリエンスを最適化したり、構成変更がもたらすユーザーへの影響を評価して、ユーザー エクスペリエンスの低下を検知したりすることができます。

この最初のリリースでは、次の 3 つの点に焦点を当てています。

- [**推奨されるソフトウェア**](#bkmk_uea_rs):最適なユーザー エクスペリエンスを実現するための推奨事項
- [**プロアクティブな修復スクリプト**](#bkmk_uea_prs):エンド ユーザーが問題に気付く前に、一般的なサポートの問題を修正します
- [**スタートアップ パフォーマンス**](#bkmk_uea_bp):ユーザーが、長いブート時間やサインインの遅延なしで、電源オンから作業開始まですばやく移行できるようにするために、IT 部門の役に立ちます

このリリースはほんの出発点に過ぎません。 他の重要なユーザー エクスペリエンスに関する新しい分析情報は、最初のリリースの直後から、迅速にロールアウトしていく予定です。 エンドポイント分析の変更点の詳細については、「[エンドポイント分析の新機能](whats-new-endpoint-analytics.md)」を参照してください。

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a> はじめに

エンドポイント分析の使用を開始するには、前提条件を確認してから、データ収集を開始します。 

### <a name="technical-prerequisites"></a>技術的な前提条件

このプレビューでは、Configuration Manager または Microsoft Intune を使用してデバイスを登録できます。 

Intune を使用してデバイスを登録するには、このプレビューでは次のものが必要です。
- Windows 10 を稼働している Intune に登録されたデバイス
- スタートアップ パフォーマンスの分析情報は、Windows 10 Enterprise のバージョン 1903 以降を実行しているデバイスでのみ使用できます (Home および Pro エディションは現在サポートされていません)。また、デバイスが Azure AD または Hybrid Azure AD に参加している必要があります。 ワークプレースに参加しているコンピューターは現在サポートされていません。
- デバイスから Microsoft パブリック クラウドへのネットワーク接続。 詳しくは、「[エンドポイント](#bkmk_uea_endpoints)」をご覧ください。
- [データの収集を開始する](#bkmk_uea_start)には、[Intune サービス管理者ロール](https://docs.microsoft.com/intune/fundamentals/role-based-access-control)が必要です。
   - **[開始]** をクリックすると、ご自分が Microsoft Intune テナントをプロビジョニングしたときに選択した場所の外部に顧客データが保存される可能性があることに同意し、承認したものと見なされます。
   - データ収集の **[開始]** をクリックすると、他の読み取り専用ロールでデータを表示できるようになります。

Configuration Manager を使用してデバイスを登録するには、このプレビューでは次のものが必要です。
- Configuration Manager バージョン 2002 以降
- バージョン 2002 以降にアップグレードされたクライアント
- [Microsoft Endpoint Manager テナントのアタッチ](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions)。北米またはヨーロッパの Azure テナントの場所で有効になっています (間もなく他のリージョンに展開される予定です)

Intune または Configuration Manager を使用してデバイスを登録するかどうかは、[**プロアクティブな修復スクリプト**](#bkmk_uea_prs)に次の要件があります。
- デバイスが Azure AD または Hybrid Azure AD に参加している必要があり、次のいずれかの条件を満たしている必要があります。
- Intune によって管理される Windows 10 Enterprise、Professional、または Education デバイス
- Intune を示す[クライアント アプリ ワークロード](../../comanage/workloads.md#client-apps)が含まれる、Windows 10 Enterprise バージョン 1607 以降が実行されている[共同管理された](../../comanage/overview.md)デバイス。
- Configuration Manager を示す[クライアント アプリ ワークロード](../../comanage/workloads.md#client-apps)が含まれる、Windows 10 Enterprise バージョン 1903 以降が実行されている[共同管理された](../../comanage/overview.md)デバイス。

### <a name="licensing-prerequisites"></a>ライセンスの前提条件

エンドポイント分析は、次のプランに含まれています。 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) 以降
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) 以降。

プロアクティブな修復には、マネージド デバイスに次のいずれかのライセンスも必要です。
- Windows 10 Enterprise E3 または E5 (Microsoft 365 F3、E3、または E5 に含まれます)
- Windows 10 Education A3 または A5 (Microsoft 365 A3 または A5 に含まれます)
- Windows Virtual Desktop Access E3 または E5

### <a name="permissions"></a>アクセス許可

#### <a name="endpoint-analytics-permissions"></a>エンドポイント分析のアクセス許可

エンドポイント分析には、次のアクセス許可が使用されます。
- **デバイス構成**カテゴリの **[読み取り]** 。
- **組織**カテゴリの**読み取り**。 <!--temporary for pp-->
- **エンドポイント分析**カテゴリでのユーザーのロールに適したアクセス許可。

読み取り専用ユーザーには、**デバイス構成**カテゴリと**エンドポイント分析**カテゴリの両方で、**読み取り**アクセス許可のみが必要です。 Intune 管理者には、通常、すべてのアクセス許可が必要です。

#### <a name="proactive-remediations-permissions"></a>プロアクティブな修復のアクセス許可

プロアクティブな修復の場合、ユーザーには、**デバイスの構成**カテゴリのロールに適したアクセス許可が必要です。  ユーザーがプロアクティブ修復のみを使用する場合、**エンドポイント分析**カテゴリのアクセス許可は必要ありません。

## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a> データ収集の開始
- Intune で管理されたのみを登録する場合は、「[エンドポイント分析ポータルでのオンボード](#bkmk_uea_onboard)」セクションに進んでください。

- Configuration Manager によって管理されるデバイスを登録する場合は、次の手順を実行する必要があります。
   - [Configuration Manager でエンドポイント分析データ コレクションを有効にする](#bkmk_uea_cm_enroll)
   - [Configuration Manager でデータのアップロードを有効にする](#bkmk_uea_cm_upload)
   - [エンドポイント分析ポータルでのオンボード](#bkmk_uea_onboard)  

### <a name="enroll-devices-managed-by-configuration-manager"></a><a name="bkmk_uea_cm_enroll"></a> Configuration Manager によって管理されるデバイスを登録する
<!--6051638, 5924760-->
Configuration Manager デバイスを登録する前に、[Microsoft Endpoint Manager テナントのアタッチ](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions)の有効化を含む[前提条件](#bkmk_uea_prereq)を確認してください。 Intune で管理されたのみを登録する場合は、「[エンドポイント分析ポータルでのオンボード](#bkmk_uea_onboard)」セクションに進んでください。

#### <a name="enable-endpoint-analytics-data-collection-in-configuration-manager"></a><a name="bkmk_uea_cm_enable"></a> Configuration Manager でエンドポイント分析データ コレクションを有効にする

1. Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]**  >  **[既定のクライアント設定]** にアクセスします。
1. 右クリックして **[プロパティ]** を選択し、 **[コンピューター エージェント]** 設定を選択します。
1. **[Enable Endpoint analytics data collection]\(エンドポイント分析データ コレクションを有効にする\)** を **[はい]** に設定します。
   > [!Important] 
   > 既にデバイスに展開されている既存のカスタムのクライアント エージェント設定がある場合は、そのカスタム設定の **[Enable Endpoint analytics data collection]\(エンドポイント分析データ コレクションを有効にする\)** オプションを更新してから、使用するコンピューターに再展開してそれを有効にする必要があります。

#### <a name="enable-data-upload-in-configuration-manager"></a><a name="bkmk_uea_cm_upload"></a> Configuration Manager でデータのアップロードを有効にする

1. Configuration Manager コンソールで、 **[管理]**  >  **[クラウド サービス]**  >  **[共同管理]** にアクセスします。
1. **[CoMgmtSettingsProd]** を選択してから **[プロパティ]** をクリックします。
1. **[アップロードを構成する]** タブで、 **[Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager]\(Microsoft Endpoint Manager にアップロードされたデバイスのエンドポイント分析を有効にする\)** オプションをオンにします

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Microsoft Endpoint Manager にアップロードされたデバイスのエンドポイント分析を有効にする" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="onboard-in-the-endpoint-analytics-portal"></a><a name="bkmk_uea_onboard"></a> エンドポイント分析ポータルでのオンボード
エンドポイント分析ポータルからのオンボードは、Configuration Manager で管理されたデバイスにも Intune で管理されたデバイスにも必要です。

1. `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu` に移動します。
1. **[開始]** をクリックします。 これにより、すべての対象デバイスからブート パフォーマンス データを収集するための構成プロファイルが自動的に割り当てられます。 後から、[割り当てられているデバイスを変更する](#bkmk_uea_profile)ことができます。 再起動後、Intune に登録されたデバイスからのスタートアップ パフォーマンス データが設定されるまでには、最大で 24 時間かかることがあります。
   - 一般的な問題の詳細については、「[スタートアップ パフォーマンスのデバイス登録のトラブルシューティング](#bkmk_uea_enrollment_tshooter)」を参照してください。

## <a name="overview-page"></a>概要ページ

使用するデータの準備が整うと、 **[概要]** ページにいくつかの情報が表示されます。その詳細を以下で説明します。

- **[ユーザー エクスペリエンス スコア]** は、**推奨されるソフトウェア**および**スタートアップ パフォーマンス スコア**の等分の加重平均です。 サブスコアのセットは、順次拡張されます。

- ベースラインを設定することにより、現在のスコアを他のスコアと比較できます。
  - [ベースライン](#bkmk_uea_baselines)に関するセクションで説明されているように、一般的な企業との比較方法を確認するための、"*商用中央値*" の組み込みベースラインがあります。 時間の経過に伴う向上の追跡または回帰の確認を行えるようにするために、現在のメトリックに基づいて新しいベースラインを作成することができます。
   - 全体のスコアとサブスコアに対して、ベースライン マーカーが表示されます。 スコアのいずれかが、選択したベースラインから構成可能なしきい値を超えて回帰した場合、そのスコアは赤で表示され、最上位レベルのスコアは要注意としてフラグが付けられます。
  - **データ不足**の状態は、意味のあるスコアを提供するために十分な数のデバイスの報告が得られていないことを意味します。 現在では、少なくとも 5 台のデバイスが必要です。

- **[フィルター]** を使用すると、デバイスまたはユーザーのサブセットに対するスコアを表示できます。 ただし、このプレビューではフィルター機能が有効になっていません。

- **[分析情報と推奨事項]** は、スコアを向上させるための優先順位が付けられたリストです。 **[ベスト プラクティス]** または **[推奨されるソフトウェア]** に移動すると、この一覧はサブノードのコンテキストにフィルター処理されます。

[![エンドポイント分析の [概要] ページ](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a> 推奨されるソフトウェア

> [!Important]  
> エンドポイント分析では、すべての Intune マネージド デバイスの**ソフトウェア採用**スコアが計算されます。それらがエンドポイント分析に登録されているかどうかは関係ありません。

特定のソフトウェアは、低レベルの正常性メトリックに関係なく、エンドユーザー エクスペリエンスを向上させることがわかっています。 たとえば、Windows 10 のネット プロモーター スコアは、Windows 7 よりもはるかに高くなります。 **ソフトウェア導入**スコアは、推奨されるさまざまなソフトウェアを展開しているデバイスの割合の加重平均を表す、0 から 100 までの数値です。 現在の重み付けは、他のメトリックよりも Windows に対してより高くなっています。ユーザーはこれらをより頻繁に操作するためです。 各メトリックについて以下で説明します。 

[![エンドポイント分析の [推奨されるソフトウェア] ページ](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a> Windows 10

Windows 10 では、以前のバージョンの Windows よりも優れたユーザー エクスペリエンスが提供されます。 詳細については、[TEI のホワイトペーパー](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf) を参照してください。

このメトリックでは、以前のバージョンの Windows のデバイスに対する Windows 10 のデバイスの割合が測定されます。

以前のバージョンの Windows からデバイスを移行するための修復アクションとしては、[Desktop Analytics](../../desktop-analytics/overview.md) を使用して展開プランを作成することをお勧めします。

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a> Autopilot

工場からまたはリセット時に従業員のデバイスの正しいプロビジョニングを確実に行えるように、Microsoft Autopilot では、Out Of Box Experience (OOBE) の画面数を減らし、既定値を提供することで、ネイティブ エクスペリエンスよりもシンプルな Windows 10 PC 用の初期プロビジョニング エクスペリエンスを提供しています。

このメトリックでは、Autopilot に登録されている Windows 10 デバイスの割合が測定されます。

推奨される修復アクションは、[Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot) を使用して Autopilot に既存のデバイスを登録することです。

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) では、アプリおよびサービスへのデバイス全体にわたるシングル サインオン、Windows Hello サインイン、セルフサービスの BitLocker 回復、企業データ ローミングなど、生産性に関する多くの利点がユーザーに提供されます。

このメトリックでは、Azure AD に登録されているデバイスの割合が測定されます。

Microsoft Intune で管理されているデバイスは、既に Azure AD に登録されています。 Configuration Manager で管理されているデバイスに向けた修復アクションとしては、それらを [Azure AD に登録する](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)か、[共同管理する](../../comanage/overview.md)ことをお勧めします。 デバイスを共同管理すると、クラウド管理スコアも向上します。

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a> クラウド管理

Microsoft Intune では、企業ネットワークから離れた場所でも企業リソースへのアクセスが可能になるなど、生産性に関するいくつかの利点がユーザーに提供されます。さらに、グループ ポリシーのパフォーマンス オーバーヘッドが不要になるため、エンドユーザーのエクスペリエンスが向上します。 このメトリックでは、Microsoft Intune に登録されているデバイスの割合が測定されます。 [Microsoft が従業員に対してこれを有効にする](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune)方法をご覧ください。

Configuration Manager で管理され、まだ Intune に登録されていないデバイスに向けた修復アクションとしては、[それらを共同管理する](../../comanage/overview.md)ことをお勧めします。

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a> 商用中央値なし

現在、**商用中央値**の組み込みベースラインには、前のセクションに記載されているサブスコア用のメトリックがありません。

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a> スタートアップ パフォーマンス

> [!NOTE]
> すべてのデバイスのスタートアップ パフォーマンス データが表示されない場合は、[スタートアップ パフォーマンスのデバイス登録に関するトラブルシューティング](#bkmk_uea_enrollment_tshooter)の記事を参照してください。

スタートアップ パフォーマンス スコアは、ユーザーが、長いブート時間やサインインの遅延なしで、電源オンから作業開始まですばやく移行できるようにするために、IT 部門の役に立ちます。 **スタートアップ スコア**は 0 から 100 までの数値です。 このスコアは、**ブート スコア**と**サインイン** スコアの加重平均であり、次のように計算されます。

- **ブート スコア**:電源オンからサインインまでの時間に基づきます。 各デバイスの前回のブート時間 (更新フェーズを除く) を確認し、0 (悪い) から 100 (非常に良い) でスコア付けします。 これらのスコアを平均して、テナント全体のブート スコアが示されます。
- **サインイン スコア**:資格情報が入力されてから、ユーザーが応答性の高いデスクトップにアクセスできるようになるまでの時間に基づいています (デスクトップがレンダリングされ、少なくとも 2 秒間 CPU 使用率が 50% を下回っていることになります)。 各デバイスの前回のサインイン時間 (初回サインインまたは機能更新直後のサインインを除く) を確認し、0 (悪い) から 100 (非常に良い) でスコア付けします。 これらのスコアを平均して、テナント全体のブート スコアが示されます。

[![エンドポイント分析の [スタートアップ パフォーマンス] ページ](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>インサイト

**[スタートアップ パフォーマンス]** ページには、以下のセクションで説明する、 **[分析情報と推奨事項]** の優先順位が付けられたリストも表示されます。

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a> ハード ディスク ドライブ

スタートアップ パフォーマンスでは、ブート ドライブがハード ディスクであるデバイスの数についての分析情報が提供されます。 通常、ハード ディスク ドライブでは、ソリッドステート ドライブよりも 3 から 4 倍長いブート時間がかかります。 また、ソリッドステート ドライブに移行することによって得られるスタートアップ パフォーマンスの改善の予測ついてもレポートされます。

ハード ディスク ドライブを搭載しているデバイスの一覧を、それぞれクリックして確認します。 推奨されるアクションは、これらのデバイスをソリッドステート ドライブにアップグレードすることです。

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a> グループ ポリシー

スタートアップ パフォーマンスでは、グループ ポリシーが原因でブート時間とサインイン時間に遅延が発生しているデバイスの数についての分析情報が提供されます。 クリックすると、各デバイスのビューを表示できます。 このビューはグループ ポリシー時間順に並べ替えられているため、さらなるトラブルシューティングを行うために影響を受けているデバイスを確認できます。

特定のデバイスをクリックすると、そのブートとサインインの履歴を確認できます。 この履歴は、問題が回帰であるかどうか、およびいつそれが発生した可能性があるかを判断するのに役立ちます。

グループ ポリシーのパフォーマンスを最適化する方法については多くの記事がありますが、代わりにクラウド管理への移行を選択することもできます。 クラウド管理に移行することで、[Intune セキュリティ ベースライン](https://docs.microsoft.com/intune/protect/security-baselines)と、間もなくリリースされるポリシー分析ツールを使用できるようになります。

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a> 低速なブートおよびサインイン時間

スタートアップ パフォーマンスでは、ブートまたはサインイン時間が低速なデバイスの数についての分析情報が提供されます。 ブート スコアまたはサインイン スコアが "0" であるということは、低速であるということです。 クリックすると、各デバイスのビューを表示できます。 デバイスは、それぞれコア ブート時間またはコア サインイン時間順に並べ替えられているため、さらなるトラブルシューティングを行うために影響を受けているデバイスを確認できます。

特定のデバイスをクリックすると、そのブートとサインインの履歴を確認できます。 この履歴は、問題が悪化したか、またいつそれが起こったかを判断するのに役立ちます。

### <a name="reporting-tabs"></a>レポート タブ

**[Startup performance]\(スタートアップ パフォーマンス\)** ページには、次のような分析情報をサポートするレポート タブがあります。
1. **[Model performance]\(モデル パフォーマンス\)** 。 このタブには、デバイス モデル別のブートとサインインのパフォーマンスが表示されます。これは、パフォーマンスの問題が特定のモデルに分離されているかどうかを特定するのに役立ちます。
1. **[Device performance]\(デバイス パフォーマンス\)** 。 このタブには、すべてのデバイスのブートとサインインのメトリックが表示されます。 特定のメトリック (たとえば、GP サインイン時間) で並べ替えて、そのメトリックで最も悪いスコアを持つデバイスを確認できるため、トラブルシューティングに役立ちます。 デバイスを名前で検索することもできます。 デバイスをクリックするとブートとサインインの履歴が表示されるので、最近の回帰があるかどうかを特定することができます
1. **[Startup processes]\(スタートアップ プロセス\)** 。 このタブ (この機能を開発中のお客様のみに表示されます) は、サインインの "デスクトップが応答するまでの時間" フェーズにどのプロセスが影響しているかを示します。そのようなプロセスは、デスクトップがレンダリングされた後、CPU が常に 50% を超えていることになります。

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a> プロアクティブな修復

プロアクティブな修復は、ユーザーのデバイスに関する一般的なサポートの問題を、ユーザーが問題の存在に気付く前に検出して修正することができるスクリプト パッケージです。 これらの修復は、サポートへの問い合わせを減らすのに役立ちます。 独自のスクリプト パッケージを作成したり、サポート チケットを減らすために私たちが作成し社内で使用しているスクリプト パッケージを展開したりすることができます。

各スクリプト パッケージは、検出スクリプト、修復スクリプト、およびメタデータで構成されています。 Intune を使用すると、これらのスクリプト パッケージを展開して、その有効性に関するレポートを確認することができます。 Microsoft では新しいスクリプト パッケージが積極的に開発されており、お客様によるそれらの使用感を知りたいと考えています。 スクリプト パッケージに関するフィードバックをお持ちの場合は、エンドポイント分析のプレビューの連絡先までお問い合わせください。

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a> 検出スクリプトと修復スクリプトを入手する

1. この記事の下部にある「[PowerShell スクリプト](#bkmk_uea_ps_scripts)」セクションからスクリプトをコピーします。
    - 名前が `det` で始まるスクリプト ファイルは、検出スクリプトです。 修復スクリプトは `rem` から始まります。
    - スクリプトの説明については、「[スクリプトの説明](#bkmk_uea_scripts)」を参照してください。
1. 指定された名前を使用して各スクリプトを保存します。 この名前は、各スクリプトの先頭にあるコメントにも記載されています。
    - 別のスクリプト名を使用することもできますが、「[スクリプトの説明](#bkmk_uea_scripts)」セクションに記載されている名前とは一致しなくなります。


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a> スクリプトの展開と監視
**Microsoft Intune 管理拡張機能** サービスによって、Intune からスクリプトが取得され、実行されます。 スクリプトは 24 時間ごとに再実行されます。 スクリプトを展開して監視するには、次の手順に従います。

1. コンソールの **[プロアクティブな修復]** ノードに移動します。
1. **[Create script package]\(スクリプト パッケージの作成\)** ボタンをクリックして、スクリプト パッケージを作成します。
     [![エンドポイント分析の [プロアクティブな修復] ページ。[作成] リンクを選択します。](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. **[基本]** ステップで、スクリプト パッケージの **[名前]** と、必要に応じて **[説明]** を指定します。 **[発行元]** フィールドは編集できますが、規定値はお使いのテナント名です。 **[バージョン]** を編集することはできません。 
1. **[設定]** ステップで、ダウンロードしたスクリプトのテキストを、 **[検出スクリプト]** および **[修復スクリプト]** フィールドにコピーします。 
   - 対応する検出スクリプトと修復スクリプトが同じパッケージに含まれている必要があります。 たとえば、検出スクリプト `Detect_stale_Group_Policies.ps1` は修復スクリプト `Remediate_stale_GroupPolicies.ps1` に対応しています。
       [![エンドポイント分析の [プロアクティブな修復] のスクリプト設定ページ。](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. 次の推奨構成を使用して、 **[設定]** ページのオプションを完了します。
   - **[このスクリプトをログオンした資格情報を使用して実行する]** :これはスクリプトによって異なります。 詳細については、「[スクリプトの説明](#bkmk_uea_scripts)」を参照してください。
   - **[スクリプト署名チェックを強制]** : いいえ
   - **[64 ビットの PowerShell でスクリプトを実行する]** :いいえ
1. **[次へ]** をクリックした後、必要な **[スコープ タグ]** を割り当てます。
1. **[割り当て]** ステップでは、スクリプト パッケージを展開するデバイス グループを選択します。
1. 展開の **[確認および作成]** ステップを完了します。
1. **[レポートの作成]**  >  **[Endpoint analytics - Proactive remediations]\(エンドポイント分析 - プロアクティブな修復\)** で、検出と修復の状態の概要を確認できます。
       [![エンドポイント分析の [プロアクティブな修復] レポート、概要ページ。](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. **[デバイスの状態]** をクリックして、展開に含まれる各デバイスの状態に関する詳細を取得します。
       [![エンドポイント分析の [プロアクティブな修復] のデバイスの状態。](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a> エンドポイント分析の設定

設定ページから、 **[全般]** または **[ベースライン]** を選択できます。 これらの各設定について以下で説明します。

### <a name="general"></a><a name="bkmk_uea_gen"></a> 全般

**[設定]** の **[全般]** ページでは、Intune のスタートアップ パフォーマンス データ収集が有効になっているかどうかを確認できます。 これは、 **[開始]** をクリックしてユーザー エクスペリエンス分析を有効にすると、既定ですべてのデバイスに対して自動的に有効になります。 必要に応じて、[Intune データ収集ポリシー] ノードに移動し、ブートとサインインに関するレコードを収集するデバイスのセットを変更することができます。


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a> Intune データ収集ポリシー

この設定を一部のデバイスに割り当てるには、次の情報を使用して[プロファイルを作成します](/intune/configuration/device-profile-create#create-the-profile)。 

  - **名前**:プロファイルのわかりやすい名前を入力します (**Intune データ収集ポリシー**など)
   
  - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
    
  - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
   
  - **[プロファイルの種類]** : **[Windows の正常性の監視]** を選択します
   
  - 次のように**設定**を構成します。
   
       - **[正常性の監視]** : Windows 10 デバイスからイベント情報を収集するには、 **[有効化]** を選択します
    
    - **スコープ**: **[ブート パフォーマンス]** を選択します 

  - [[スコープ タグ]](/intune/configuration/device-profile-create#scope-tags) と [[適用性ルール]](/intune/configuration/device-profile-create#applicability-rules) を使用して、特定の条件を満たすグループ内の特定の IT グループまたはデバイスにプロファイルをフィルター処理します。

> [!NOTE]
> Configuration Manager データ コネクタを構成する手順のためのプレースホルダーがあります。 ただし、この最初のプライベート プレビューでは、この機能は実装されていません。

  [![エンドポイント分析の全般設定ページ](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a> ベースライン管理

ベースラインを設定することにより、現在のスコアとサブスコアを他のスコアと比較できます。

1. **商用中央値**用の組み込みベースラインが用意されています。これにより、スコアを一般的な企業と比較することができます。
1. 現在のメトリックに基づいて新しいベースラインを作成し、時間の経過に伴う向上の追跡または回帰の確認を行うことができます。 **[新規作成]** ボタンをクリックし、新しいベースラインに名前を付けます。 レポート ページのドロップダウンから簡単に選択できるようにするために、日付を含む名前を指定することをお勧めします。
1. ベースラインは、テナントあたり 100 個に制限されています。 不要になった古いベースラインは削除できます。
1. 現在のメトリックが現在のベースラインを下回ると、レポート内で赤のフラグが設定され、回帰として表示されます。 メトリックが毎日変動するのはまったく正常なことであるため、回帰のしきい値を設定することができます。既定値は 10% です。 このしきい値を使用すると、メトリックは、10% を超える回帰が発生した場合にのみ回帰としてフラグが設定されます。

   [![エンドポイント分析のベースライン設定ページ](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a> トラブルシューティング

以下のセクションを使用すると、発生する可能性のある問題のトラブルシューティングに役立てることができます。

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a> スタートアップ パフォーマンスのデバイス登録のトラブルシューティング

概要ページに、スタートアップ パフォーマンス スコアがゼロと表示され、かつデータを待機していることを示すバナーが表示されている場合、またはスタートアップ パフォーマンスの [デバイスのパフォーマンス] タブに予想よりも少ないデバイスが表示されている場合は、問題のトラブルシューティングのために実行できる手順がいくつかあります。

まず、スタートアップ パフォーマンス データ収集の制限事項の概要を次に示します。
1. デバイスは Windows 10 バージョン 1903 以降である必要があります。
2. デバイスが Azure AD に参加している必要があります。 現在、ワークプレースに参加しているデバイスはサポートされていませんが、この機能を Windows に追加できないかを積極的に調査しています。
3. デバイスは Windows 10 Enterprise エディションである必要があります。 現在、Windows 10 Home および Professional はサポートされていませんが、この機能を Windows に追加できないかを積極的に調査しています。

これらのイシューは、今後の Configuration Manager コネクタからのデータには適用されないことに注意してください。バージョン、エディション、ディレクトリ構成に関係なく、任意の Configuration Manager クライアント PC からデータを収集することができます。

次に、トラブルシューティングのために確認する簡単なチェックリストを示します。
1. パフォーマンス データが必要なすべてのデバイスを対象とした Windows 正常性監視プロファイルがあることを確認します。 このプロファイルへのリンクは、エンドポイント分析の設定ページ内から見つけられます。または、他の Intune プロファイルと同じようにアクセスします。 割り当てタブを見て、予想されるデバイスのセットにそれが割り当てられていることを確認します。 
1. データ収集について正常に構成されているデバイスを確認します。 この情報は、プロファイルの概要ページでも確認できます。  
   - プロファイル割り当てエラーがお客様に表示される可能性がある既知の問題があります。その影響を受けたデバイスには、`-2016281112 (Remediation failed)` のエラーコードが表示されます。 Microsoft ではこの問題を積極的に調査しています。
1. データ収集について正常に構成されたデバイスは、データ収集を有効にした後で再起動する必要があります。その後、デバイスが [デバイスのパフォーマンス] タブに表示されるまで、最大 24 時間待機する必要があります。
1. デバイスがデータ収集について正常に構成され、その後再起動されたが、24 時間経過してもまだ表示されない場合は、デバイスが Microsoft の収集エンドポイントに到達できていない可能性があります。 この問題は、お客様の会社がプロキシ サーバーを使用していて、エンドポイントがプロキシで有効になっていない場合に発生することがあります。 詳細については、「[エンドポイントのトラブルシューティング](#bkmk_uea_endpoints)」をご覧ください。


### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a> エンドポイント

エンドポイント分析にデバイスを登録する場合、デバイスから Microsoft に必要な機能データが送信される必要があります。 お使いの環境でプロキシ サーバーが使用されている場合は、この情報を使用してプロキシを構成します。

機能データの共有を有効にするには、以下のエンドポイントを許可するようにプロキシ サーバーを構成します。

> [!Important]  
> プライバシーとデータの整合性を確保するため、必要な機能データを共有するエンドポイントとの通信時に、Windows によって Microsoft SSL 証明書がチェックされます (証明書のピン留め)。 SSL を傍受および検査することはできません。 エンドポイント分析を使用するには、以下のエンドポイントを SSL の検査から除外します。<!-- BUG 4647542 -->

| エンドポイント  | 関数  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | [必要な機能データ](#bkmk_uea_datacollection) を Intune データ収集エンドポイントに送信するために使用されます。 |
| `https://graph.windows.net` | 階層をエンドポイント分析に (Configuration Manager サーバー ロールで) アタッチするときに、設定を自動的に取得するために使用されます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。 |
| `https://*.manage.microsoft.com` | デバイス コレクションおよびデバイスをエンドポイント分析に (Configuration Manager サーバー ロールのみで) 同期するために使用されます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。 |


### <a name="proxy-server-authentication"></a>プロキシ サーバー認証

組織でインターネット アクセスにプロキシ サーバー認証を使用している場合は、認証のためにデータがブロックされないことを確認します。 デバイスによるこのデータの送信がプロキシで許可されていない場合、それらのデバイスはデスクトップ分析に表示されません。

#### <a name="bypass-recommended"></a>バイパス (推奨)

プロキシ サーバーを構成して、データ共有エンドポイントへのトラフィックにプロキシ認証が要求されないようにします。 このオプションは、最も包括的な解決策です。 Windows 10 のすべてのバージョンで動作します。  

#### <a name="user-proxy-authentication"></a>ユーザー プロキシ認証

サインインしたユーザーのコンテキストをプロキシ認証に使用するようにデバイスを構成します。 この方法では、次の構成が必要です。

- デバイスに、サポートされているバージョンの Windows の最新の品質更新プログラムがインストールされている

- Windows の設定の [ネットワークとインターネット] グループの **[プロキシ設定]** で、ユーザー レベル プロキシ (WinINET プロキシ) を構成します。 従来の [インターネット オプション] コントロール パネルを使用することもできます。

- ユーザーに、データ共有エンドポイントにアクセスするためのプロキシ アクセス許可があることを確認します。 このオプションでは、デバイスにプロキシ アクセス許可を持つコンソール ユーザーが存在する必要があるため、この方法をヘッドレス デバイスで使用することはできません。

> [!IMPORTANT]
> ユーザー プロキシ認証の方法は、Microsoft Defender Advanced Threat Protection の使用と互換性がありません。 このような動作が発生するのは、この認証では **DisableEnterpriseAuthProxy** レジストリ キーが `0` に設定されている必要があるのに対し、Microsoft Defender ATP では `1` に設定されている必要があるためです。 詳しくは、[Microsoft Defender ATP でのコンピューターのプロキシとインターネット接続設定の構成](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)に関する記事をご覧ください。

#### <a name="device-proxy-authentication"></a>デバイス プロキシ認証

この方法では次のシナリオがサポートされます。

- ユーザーがサインインしない、またはデバイスのユーザーがインターネット アクセスを使用しないヘッドレス デバイス

- Windows 統合認証を使用しない認証プロキシ

- Microsoft Defender Advanced Threat Protection も使用する場合

この方法は、次の構成が必要であるため、最も複雑です。

- デバイスがローカル システム コンテキストで WinHTTP を使用してプロキシ サーバーに接続できることを確認します。 この動作を構成するには、次のいずれかのオプションを使用します。

  - コマンド ライン `netsh winhttp set proxy`

  - Web プロキシ自動検出 (WPAD) プロトコル

  - 透過的プロキシ

  - 次のグループ ポリシー設定を使用して、デバイス全体の WinINET プロキシを構成します。 **(ユーザー別ではなく) コンピューター別にプロキシを設定する** (ProxySettingsPerUser = `1`)

  - ルーティングされた接続、またはネットワーク アドレス変換 (NAT) を使用する接続

- Active Directory のコンピューター アカウントがデータ エンドポイントにアクセスできるように、プロキシ サーバーを構成します。 この構成では、プロキシ サーバーで Windows 統合認証をサポートする必要があります。  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a> よく寄せられる質問

### <a name="will-my-endpoint-analytics-data-migrate-if-i-move-my-intune-tenant-to-a-different-tenant-location"></a>Intune テナントを別のテナントの場所に移動した場合、エンドポイント分析データは移行されますか?

Intune テナントを別の場所に移行すると、移行時のエンドポイント分析ソリューション内のすべてのデータが失われます。 エンドポイントはエンドポイント分析に継続的に報告されるため、デバイスが適切に登録されているとすれば、移行後に発生するすべてのイベントが新しいテナントの場所に自動的にアップロードされ、レポートが再作成されます。 

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>スクリプトがコード 1 で終了するのはなぜですか。

スクリプトがコード 1 で終了するのは、修復が行われる必要があることを Intune に通知するためです。 この場合、検出スクリプトを 1 で終了することは、修復が必要であることを意味します。 CM でのみ実行されるスクリプト パッケージの多くは、準拠していると表示されることがありますが、コード 1 で終了します。 これらのスクリプトでは、コード 1 で終了することは何らかの警告ではありませんが、デバイスの修復を適切に検証することをお勧めします。

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>古いグループ ポリシーの更新スクリプトがエラー 0x87D00321 で終了したのはなぜですか。

0x87D00321 は、スクリプトの実行タイムアウト エラーです。 通常、このエラーはリモート接続されているコンピューターで発生します。 可能な軽減策としては、内部ネットワーク接続を持つコンピューターの動的なコレクションにのみ展開することが考えられます。

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a> スクリプトの説明

次の表は、スクリプトの名前、説明、検出、修復、および構成可能な項目を示しています。 名前が `Detect` で始まるスクリプト ファイルは、検出スクリプトです。 修復スクリプトは `Remediate` から始まります。 これらのスクリプトは、この記事の次のセクションからコピーできます。

|スクリプト名|[説明]|
|---|---|
|**古いグループポリシーの更新** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| 前回のグループ ポリシーの更新が `7 days` 前よりも大きいかどうかを検出します。  </br>検出スクリプトの `$numDays` の値を変更すると、7 日間のしきい値をカスタマイズできます。 </br></br>`gpupdate /target:computer /force` と `gpupdate /target:user /force` の実行による修復  </br> </br>証明書と構成がグループ ポリシー経由で配信される場合に、ネットワーク接続関連のサポートへの問い合わせを減らすのに役立ちます。 </br> </br> **ログオンした資格情報を使用してスクリプトを実行する**:はい|
|**Office クイック実行サービスを再開する** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| クイック実行サービスが自動的に開始するように設定されているかどうか、およびサービスが停止しているかどうかを検出します。 </br> </br> サービスを自動的に開始するように設定すること、およびサービスが停止している場合は開始することで修復します。 </br></br> クイック実行サービスが停止しているために Win32 Microsoft 365 Apps for enterprise が起動しない問題を解決するのに役立ちます。 </br> </br> **ログオンした資格情報を使用してスクリプトを実行する**:いいえ|
|**ネットワーク証明書をチェックする** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|有効期限が切れているか有効期限が近づいている、コンピューター、ユーザーいずれかの個人用ストアの CA によって発行された証明書を検出します。 </br> CA を指定するには、検出スクリプトの `$strMatch` の値を変更します。 有効期限が切れた証明書を検索するには `$expiringDays` に 0 を指定し、有効期限が近づいた証明書を検索するには別の日数を指定します。  </br></br>ユーザーにトースト通知を表示することで修復します。 </br> ユーザーに表示したいメッセージ タイトルとテキストを使用して `$Title` と `$msgText` の値を指定します。 </br> </br> 更新が必要な可能性がある期限切れの証明書について、ユーザーに通知します。 </br> </br> **ログオンした資格情報を使用してスクリプトを実行する**:いいえ|
|**古い証明書をクリアする** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| 現在のユーザーの個人用ストア内の CA によって発行された、有効期限が切れた証明書を検出します。 </br> CA を指定するには、検出スクリプトの `$certCN` の値を変更します。 </br> </br> 現在のユーザーの個人用ストアの CA によって発行された、有効期限が切れた証明書を削除することで修復します。 </br> CA を指定するには、修復スクリプトの `$certCN` の値を変更します。 </br> </br> 現在のユーザーの個人用ストアの CA によって発行された、有効期限が切れた証明書を検索して削除します。 </br> </br> **ログオンした資格情報を使用してスクリプトを実行する**:はい|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a> PowerShell スクリプト

### <a name="detect_stale_group_policiesps1"></a>古い_グループ_ポリシー_検出.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>古い_グループ ポリシー_修復.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>クイック_実行_サービス_状態_検出.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>クイック_実行_サービス_状態_修復.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>期限切れ_発行者_証明書_検出.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>期限切れ_発行者_証明書_修復.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>期限切れ_ユーザー_証明書_検出.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>期限切れ_ユーザー_証明書_修復.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a> エンドポイント分析のデータのプライバシー

### <a name="data-flow"></a>データ フロー

次の図は、必要な機能データが、個々のデバイスから、使用するデータ サービス、一時的なストレージを経由して、ご自身のテナントへとどのようにフローしていくかを示しています。 データは、Windows 診断データに依存せずに、既存のエンタープライズ パイプラインを通じてフローします。

[![ユーザー エクスペリエンスのデータ フロー図](media/dataflow.png)](media/dataflow.png#lightbox)

1. 登録されたデバイスの **Intune データ収集**ポリシーを構成します。 既定では、エンドポイント分析を**開始**するときに、このポリシーが "すべてのデバイス" に割り当てられます。 ただし、[割り当てはいつでも変更でき](#bkmk_uea_set)、デバイスのサブセットに割り当てたり、デバイスに一切割り当てないこともできます。

2. デバイスから必要な機能データが送信されます。

    - ポリシーが割り当てられている Intune デバイスの場合は、Intune 管理拡張機能からデータが送信されます。 詳細については、「[要件](#bkmk_uea_prereq)」を参照してください。
    - Configuration Manager で管理されたデバイスの場合は、ConfigMgr コネクタを使用してデータを Microsoft エンドポイント管理に送ることもできます。 ConfigMgr コネクタはクラウドにアタッチされています。 Intune テナントへの接続のみが必要で、共同管理を有効にする必要はありません。

> [!Note]  
> デバイスのスタートアップ スコアの計算に必要なデータは、ブート時に生成されます。 電源設定とユーザーの行動によっては、デバイスにポリシーが正しく割り当てられてから管理コンソールにスタートアップ スコアが表示されるまで、数週間かかることがあります。  

3. Microsoft エンドポイント管理サービスでは、各デバイスのデータが処理され、MS Graph API を使用して、個々のデバイスと組織の集計の両方の結果が管理コンソールに発行されます。

エンドツーエンドの平均待機時間は約 12 時間で、毎日の処理にかかる時間によって制御されます。 データ フローのその他の部分はすべて、ほぼリアルタイムです。

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a> データ収集

現時点では、エンドポイント分析の基本機能によって、[識別済み](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data)と[匿名化済み](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data)のカテゴリに該当するブート パフォーマンス レコードに関連する情報が収集されます。 時間の経過と共に機能は追加されるため、収集されるデータは必要に応じて異なります。 現在収集されている主なデータポイントは、次のとおりです。

#### <a name="identified-data"></a>識別済みデータ

- ハードウェア インベントリ情報
  - **make:** デバイスの製造元
  - **model:** デバイス モデル
  - **deviceClass:** デバイス分類。 デスクトップ、サーバー、モバイルなど。
  - **Country:** デバイスのリージョン設定
- 次のようなアプリケーション インベントリ
  - **name:** Windows
  - **ver:** 現在の OS のバージョン。
  
#### <a name="pseudonymized-data"></a>匿名化済みデータ

- ユーザーまたはデバイスに関連付けられた診断、パフォーマンス、使用状況データ
  - **logOnId**
  - **bootId:** システム ブート ID
  - **coreBootTimeInMilliseconds:** コア ブートの時間
  - **totalBootTimeInMilliseconds:** 合計ブート時間
  - **updateTimeInMilliseconds:** OS の更新が完了するまでの時間
  - **gpLogonDurationInMilliseconds**:グループ ポリシーの処理時間
  - **desktopShownDurationInMilliseconds:** デスクトップ (explorer.exe) の読み込み時間
  - **desktopUsableDurationInMilliseconds:** デスクトップ (explorer.exe) が使用可能になるまでの時間
  - **topProcesses:** ブート時に読み込まれたプロセスの一覧。名前、CPU 使用率統計、アプリの詳細 (名前、発行元、バージョン) を含む。 例: *{\"ProcessName\":\"svchost\",\"CpuUsage\":43,\"ProcessFullPath\":\"C:\\\\Windows\\\\System32\\\\svchost.exe\",\"ProductName\":\"Microsoft&reg; Windows&reg; Operating System\",\"Publisher\":\"Microsoft Corporation\",\"ProductVersion\":\"10.0.18362.1\"}*
- デバイスまたはユーザーに関連付けられていないデバイス データ (このデータがデバイスまたはユーザーに関連付けられている場合、Intune では識別済みデータとして扱われます)
  - **ID:** Windows Update によって使用される一意のデバイス ID
  - **localId:** デバイスに対してローカルに定義された一意の ID。 これは、人間が判読できるデバイス名ではありません。 ほとんどの場合、HKLM\Software\Microsoft\SQMClient\MachineId に格納されている値と等しくなります。
  - **aaddeviceid:** Azure Active Directory デバイス ID
  - **orgId:** Microsoft O365 テナントを表す一意の GUID
  
> [!Important]  
> Microsoft のデータ処理ポリシーについては、「[Microsoft Intune のプライバシーに関する声明](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)」を参照してください。 お客様のデータは、お客様がサインアップしたサービスを提供するためにのみ使用されます。 オンボード プロセス中に説明したように、基準を最新の状態に保つため、すべての登録済み組織のスコアを匿名化して集計します。


### <a name="resources"></a>リソース

関連するプライバシー面の詳細については、次の記事を参照してください。

- [Microsoft Intune のプライバシーに関する声明](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 とプライバシーのコンプライアンス](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [ライセンス条項とドキュメント](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Microsoft Azure データセンターのセキュリティとプライバシー](https://azure.microsoft.com/global-infrastructure/)  
- [信頼できるクラウドであるという自信](https://azure.microsoft.com/overview/trusted-cloud/)  
- [セキュリティ センター](https://www.microsoft.com/trustcenter)  
