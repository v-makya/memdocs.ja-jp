---
title: Desktop Analytics の新機能
titleSuffix: Configuration Manager
description: Desktop Analytics クラウド サービスの最新のマンスリー リリースの新機能の概要です。
ms.date: 08/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: c41c6333cfee1b6a24bb84c0f020c14c303fd904
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614742"
---
# <a name="whats-new-in-desktop-analytics"></a>Desktop Analytics の新機能

Desktop Analytics の各月の新機能について説明します。

> [!TIP]
> 各マンスリー更新プログラムのロールアウトには最大 3 日間かかることがあります。 一部の機能は数週間にわたってロールアウトされ、一部のお客様は最初の週にご利用になれない可能性があります。

このページが更新されたときに通知を受け取るには、次の URL をコピーして RSS フィード リーダーに貼り付けます。`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="august-2020"></a>2020 年 8 月

### <a name="apps-deployed-from-configuration-manager-are-important-by-default"></a>Configuration Manager から展開されるアプリは、既定で重要である

<!-- 4859763 -->

アプリの**重要度**の構成は、Desktop Analytics でパイロット展開に含めるデバイスを決定する際に不可欠です。 管理者は、Desktop Analytics ですべてのアプリの重要度を手動で構成する必要がありました。 パイロットを検証した後でのみ、運用環境の展開を続行できます。

現在は、Configuration Manager で展開するすべてのアプリが、Desktop Analytics によって既定で重要として自動的に構成されます。 この動作により、環境内のアプリをより迅速に構成し、運用環境に迅速に展開することができます。

詳細については、[資産のアプリ](about-assets.md#apps)に関する記事をご覧ください。

## <a name="july-2020"></a>2020 年 7 月

### <a name="windows-10-version-2004-now-available-in-desktop-analytics"></a>Desktop Analytics で Windows 10 バージョン 2004 が利用可能に

<!-- 7370207 -->

Desktop Analytics ポータルで、セキュリティと機能更新プログラムを監視するとき、Windows 10 バージョン 2004 が表示されるようになります。 展開プランを作成するときに、ターゲット バージョンとして Windows 10 バージョン 2004 を選択できます。

### <a name="improved-support-for-viewing-the-portal-from-any-device"></a>ポータルを任意のデバイスから表示するためのサポートを強化

<!-- 6270240 -->

さまざまな種類のデバイスから、Microsoft Endpoint Manager 管理センターの Desktop Analytics ポータルを表示できるようになりました。 320 x 256 ピクセルという低いディスプレイ解像度に対して、Web コンテンツ アクセシビリティ ガイドライン (WCAG) 2.1 に適合しています。 たとえば、次の画像は Apple iPhone 8 のポータルです。

:::image type="content" source="media/dashboard-iphone8.png" alt-text="iPhone 8 の Desktop Analytics ポータル":::

### <a name="notifications-for-service-impacting-events"></a>サービスに影響するイベントの通知

<!-- 4982509 -->

Desktop Analytics ポータルで、通知バナーを表示できるようになりました。 これらの通知を使って、Microsoft は重要なイベントや問題についてユーザーに連絡することができます。 たとえば、サービスに関する既知の問題、データ待機時間、または新しい前提条件があります。 詳細については、「[サービスの通知](troubleshooting.md#service-notifications)」を参照してください。

## <a name="june-2020"></a>2020 年 6 月

### <a name="improvement-to-prerequisites"></a>前提条件の改善

Desktop Analytics では、Azure Active Directory (Azure AD) テナントに Office 365 サービスをデプロイする必要がなくなりました。 Azure AD の **Office 365 クライアント管理**アプリは **Desktop Analytics** アプリになり、このサービスから Configuration Manager が情報と状態を取得できるようになりました。

## <a name="may-2020"></a>2020 年 5 月

### <a name="reduce-the-number-of-apps-for-review"></a>確認用のアプリの数を減らす

<!-- 5542186 -->

ポータルの資産ページに表示されるアプリを統合してその数を減らすために、同じ名前と発行元を持つすべてのバージョンのアプリが結合されるようになりました。 **[注目すべきアプリ]** タイル内のアプリの数には、この設定が反映されます。 たとえば、Microsoft Edge の何百ものインスタンスを一覧表示する代わりに、すべてのバージョンに対する 1 つのインスタンスが表示されます。 すべてのバージョンに対して 1 回で決定を行うことができます。 アプリの特定のバージョンに関する決定を行う必要がある場合は、この動作を構成できます。

詳細については、[資産の概要 - アプリ](about-assets.md#apps)に関する記事をご覧ください。

## <a name="march-2020"></a>2020 年 3 月

### <a name="support-for-multiple-hierarchies"></a>複数階層のサポート

<!-- 4814075, 6079184 -->

Desktop Analytics 用に、複数の Configuration Manager 階層を 1 つの商用 ID を使用する 1 つの Azure Active Directory テナントに接続できるようになりました。 ポータルでは、さまざまな階層のデバイスが分類されるため、グローバル パイロットおよび展開プランの操作性が向上します。

- グローバル パイロットを構成するときに、登録された合計デバイス数の 20% を超えるコレクションを含めると、ポータルに警告が表示されます。
- 展開プランを作成するときに、複数の階層のコレクションを選択すると、ポータルに警告が表示されます。

> [!NOTE]
> 複数の階層をサポートするには、Configuration Manager バージョン 1910 以降が必要です。

詳細については、以下の記事を参照してください。

- [グローバル パイロット](deploy-pilot.md#bkmk_GlobalPilot)
- [展開プランを作成する方法](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>互換性のセーフガードを識別する

<!-- 5746559 -->

Windows 互換性データは、一部のアプリとドライバーを*セーフガード*の有無で分類します。これにより、Windows 10 への更新が失敗したり、ロールバックしたりする可能性があります。 Desktop Analytics では、これらのセーフガードを事前に識別できるようになりました。これにより、更新プログラムを展開する前に資産を修復できます。 詳細については、[互換性評価のセーフガード](compat-assessment.md#safeguards)に関するセクションを参照してください。

## <a name="january-2020"></a>2020 年 1 月

### <a name="additional-app-usage-detail"></a>その他のアプリの使用状況の詳細

<!-- 5533890 -->

詳細情報を表示するアプリを選択すると、詳細ウィンドウに使用状況に関する追加情報が表示されるようになりました。 このデータを使用すると、アプリのインストールの幅や、そのアプリをユーザーが定期的に使用するデバイスについて容易に理解することができます。 詳細については、[資産に関するページの、アプリの使用状況](about-assets.md#usage)に関するセクションを参照してください。

### <a name="provide-feedback-on-desktop-analytics"></a>Desktop Analytics に関するフィードバックを提供する

<!-- 5451636 -->

Desktop Analytics に関するフィードバックを共有するには、ポータル上部の右側にある **[気に入った機能の報告]** アイコンを選択します。 詳細については、[製品に関するフィードバックの共有](get-support.md#bkmk_feedback)に関するページを参照してください。

## <a name="october-2019"></a>2019 年 10 月

### <a name="improvements-to-compatibility-recommendations"></a>互換性に関する推奨事項の改善

<!-- 3594545 -->

Desktop Analytics では、Windows アップグレードによってアプリケーションまたはドライバーが完全にまたは部分的に削除されることが検出される場合に、さらに詳細な情報が提供されるようになりました。 詳細については、「[互換性の評価](compat-assessment.md#asset-is-removed-during-upgrade)」を参照してください。

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Windows Analytics から既存のテナントに移行する

<!-- 5202803 -->

Desktop Analytics にオンボードした後、既存の Windows Analytics ワークスペースから入力を移行できるようになりました。

## <a name="september-2019"></a>2019 年 9 月

### <a name="migrate-inputs-from-windows-analytics"></a>Windows Analytics から入力を移行する

<!-- 4252663 -->

オンボード中に、既存の Windows Analytics ワークスペースから入力を移行できるようになりました。

### <a name="offboard-from-desktop-analytics"></a>Desktop Analytics からオフボードする

<!-- 4972396 -->

お使いの環境に Desktop Analytics を設定した後、サービスの使用を停止する場合は、アカウントを閉じることができるようになりました。 90 日以内に気が変わった場合は、アカウントを再アクティブ化することができます。 詳細については、「[アカウントを閉じる方法](account-close.md)」を参照してください。

## <a name="august-2019"></a>2019 年 8 月

### <a name="reset-your-account"></a>アカウントをリセットする

<!-- 3733897 -->

お使いの環境に Desktop Analytics を設定した後、オンボードと登録をやり直す場合は、リセットできるようになりました。 このプロセスの詳細については、[アカウントのリセット](account-reset.md)に関する記事を参照してください。

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>システム アプリとストア アプリの自動アップグレード判定

<!-- 3587232 -->

注目アプリに注釈を付ける手間を減らすために、特定の種類のアプリには、自動的に "*重要でない*" とマークされます。 こうしたアプリの展開計画のアップグレード判定にも "*準備完了*" とマークされます。 次のアプリは互換性があり、Windows のアップグレード後も引き続き機能します。

- Microsoft から発行されるシステム アプリとコンポーネント

- Microsoft Store から管理および更新されるアプリ

詳細については、「[システム アプリとストア アプリの自動アップグレード判定](about-assets.md#bkmk_plan-autoapp)」を参照してください。

## <a name="whats-new-in-configuration-manager"></a>Configuration Manager の新機能

Desktop Analytics ドキュメントでは、常に最新バージョンの Configuration Manager Current Branch の機能が参照されています。 Configuration Manager の最新の変更点の詳細については、次の記事を参照してください。

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [バージョン 1906 の新機能](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>非推奨の機能

Microsoft が Desktop Analytics サービスの重要な機能を削除する予定がある場合、その変更は Configuration Manager の非推奨の機能として事前に発表されます。 詳しくは、「[非推奨の機能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)」をご覧ください。
