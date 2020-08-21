---
title: Desktop Analytics の FAQ
titleSuffix: Configuration Manager
description: Desktop Analytics に関してよく寄せられる質問。
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b24369f2c2f21208f188cf5c0c2ef3a28db83c04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700822"
---
# <a name="desktop-analytics-faq"></a>Desktop Analytics の FAQ

## <a name="prerequisites"></a>[前提条件]

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a> Intune マネージド デバイスでクラウド対応の分析を使用できますか。

現在、そうではありませんが、Microsoft Ignite 2019 で[分析情報に基づくデバイス管理](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions)に関するお知らせを参照してください。 この計画されたソリューションは、デバイスの正常性と Upgrade Readiness の後継です。

Desktop Analytics ワークフローを活用しているお客様の大部分は、Configuration Manager を使用して Windows を展開しています。 Intune のお客様も分析データから得られる追加の分析情報を好まれていることを理解しており、そのようなお客様とも分析情報を共有する方法の開発に取り組んでいます。

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>72 時間経過したのに、ポータルではまだデータが処理されています。どうすればよいですか?

初めて Desktop Analytics をセットアップするときは、Configuration Manager と Desktop Analytics ポータルのレポートで、完全なデータがすぐに表示されない場合があります。 サービスでデータが処理されるまで、2-3 日かかることがあります。 72 時間以上経ってもまだ、ポータルでデータが処理されている場合は、以下のようにしてください。

- アクティブなデバイスが正しく構成されていることを確認するには、[接続の正常性ダッシュボード](monitor-connection-health.md)を使用します。 このダッシュボードはリアルタイムに更新されません。
- デバイスで診断データが Desktop Analytics サービスに送信されていることを確認します。 詳しくは、[データ共有の有効化](enable-data-sharing.md)に関する記事をご覧ください。
- Azure AD で [Azure AD アプリケーション](troubleshooting.md#bkmk_AzureADApps)をプロビジョニングします。
- 過去 7 日間に組織に関連付けたデバイスを確認します。 [Desktop Analytics ポータル](https://aka.ms/desktopanalytics)で、 **[接続済みサービス]** ペインにアクセスします。 **[デバイスの登録]** を選択し、 **[最近のデータを表示]** を選択します

  > [!IMPORTANT]
  > **[最近のデータを表示]** の Desktop Analytics のオプションは非推奨です。 このアクションは、Desktop Analytics サービスの今後のリリースで削除される予定です。 詳しくは、「[非推奨の機能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)」をご覧ください。<!--7080949-->  

デバイスが正しく構成されていても、ワークスペースにデータが表示されない場合は、[Microsoft サポートにお問い合わせください](https://support.microsoft.com/hub/4343728/support-for-business)。

## <a name="connect-configuration-manager"></a>Configuration Manager を接続する

### <a name="can-i-change-the-target-or-additional-collections"></a>ターゲットまたは追加のコレクションを変更できますか?

はい。次のプロセスを使用してください。

- Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。 Desktop Analytics サービスに関連付けられているエントリのプロパティを開きます。

- **[Desktop Analytics 接続]** タブで、 **[ターゲット コレクション]** を変更するか、追加のコレクションを管理します。

<!-- 7130169 -->
> [!Note]
> 追加のコレクションの一覧には、20 個を超えるコレクションを含めないでください。 各コレクション内のデバイスの合計数に注意してください。 [グローバル パイロットの含めるコレクションと除外するコレクション](deploy-pilot.md#bkmk_GlobalPilot)を常に含めてください。  

> [!IMPORTANT]  
> Configuration Manager により、設定ポリシーを使用して、ターゲット コレクションのデバイスが構成されます。 このポリシーには、デバイスが Microsoft にデータを送信できるようにする診断データの設定が含まれています。 ターゲット コレクションを変更しても、ターゲット コレクションに存在しなくなったデバイスの設定ポリシーは元に戻されません。 デバイスによる診断データの送信を続行しない場合は、[デバイスを構成しなおします](account-close.md#reconfigure-clients)。

## <a name="windows-upgrade"></a>Windows のアップグレード

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Windows をアップグレードして、アーキテクチャを変更できますか?

Desktop Analytics は、インプレース アップグレードを最適にサポートするように設計されています。 インプレース アップグレードでは、32 ビット アーキテクチャから 64 ビット アーキテクチャへの移行はサポートされていません。 このシナリオでコンピューターを移行する必要がある場合は、更新のシナリオを使用します。 このシナリオでは、Desktop Analytics の分析情報が依然として有益ですが、アップグレード固有のガイダンスは無視してかまいません。

詳細については、[新しいバージョンの Windows での既存のコンピューターの更新](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)に関するページを参照してください。

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Windows をアップグレードするときに、BIOS から UEFI に変更できますか?

はい。 詳しくは、「[インプレース アップグレード時に BIOS から UEFI に変換する](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)」をご覧ください。

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Windows 10 LTSC で Desktop Analytics を使用できますか?

Desktop Analytics では、Windows 10 長期サービス チャネル (LTSC) デバイスはサポートされていません。 詳しくは、[サービスとしての Windows の概要](/windows/deployment/update/waas-overview#long-term-servicing-channel)に関する記事をご覧ください。

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Desktop Analytics ポータルでデータが更新されるまでにかかる時間を短縮できますか?

Desktop Analytics ポータルには次の 2 種類のデータがあります: 管理者データと診断データ。 必要に応じて管理者データを更新するには、データ更新状態ポップアップを開き、 **[変更の適用]** を選択します。 この操作により、ワークスペースで保留中の管理者変更が 1 回だけ更新されます。 変更は反映され、一般に 15 から 60 分以内に利用可能になります。 タイミングは、ワークスペースのサイズと、保留中の変更の範囲によって異なります。 オンデマンドのデータ更新は、24 時間以内に最大 6 回まで要求できます。

オンデマンドのデータ更新を要求しない場合でも、すべてのデータが毎日 1 回自動的に更新されます。 診断データのオンデマンド更新をトリガーする方法はありません。 Desktop Analytics におけるさまざまな種類のデータについて詳しくは、「[データ待機時間](troubleshooting.md#data-latency)」をご覧ください。

## <a name="privacy"></a>プライバシー

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Microsoft Data Management Service への直接クライアント接続がなくても、Desktop Analytics を使用できますか?

いいえ。サービス全体で Windows 診断データを使用しているので、デバイスにこの直接接続がある必要があります。

### <a name="can-i-choose-the-data-center-location"></a>データ センターの場所を選択できますか?

Azure Log Analytics の場合: はい。Desktop Analytics を設定し、Log Analytics ワークスペースを作成するとき。

Microsoft Data Management Service および Analytics Azure Storage の場合: いいえ、これらの 2 つのサービスは米国でホストされています。

### <a name="where-is-my-organizations-data-stored"></a>組織のデータはどこに格納されますか?

コンピューターからの Windows 診断データは暗号化され、米国にある Microsoft が管理するセキュリティで保護されたデータ センターに送信されて、処理されます。 Desktop Analytics 関連のデータの分析は、Azure portal の Desktop Analytics ソリューションを通じて提供されます。 Desktop Analytics は、[Log Analytics を使用できる](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all)ほとんどのリージョンでサポートされています。 国際 Azure リージョンを選択した場合でも、診断データは米国内の Microsoft のセキュリティで保護されたデータ センターに送信され、処理されます。

## <a name="existing-windows-analytics-customers"></a>既存の Windows Analytics のお客様

> [!Important]  
> Windows Analytics サービスは、2020 年 1 月 31 日をもって廃止されています。
>
> 詳細については、[KB 4521815:Windows Analytics の廃止 (2020 年 1 月 31 日)](https://support.microsoft.com/help/4521815/windows-analytics-retirement) に関するページをご確認ください。

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>Desktop Analytics と共に Update Compliance を使用できますか?

はい。 現在 Azure portal で [Update Compliance](/windows/deployment/update/update-compliance-get-started) を使用している場合は、現在も 2020 年 1 月以降も引き続きそうすることができます。

詳細については、[KB 4521815:Windows Analytics の廃止 (2020 年 1 月 31 日)](https://support.microsoft.com/help/4521815/windows-analytics-retirement) に関するページをご確認ください。

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Desktop Analytics で使用できない Windows Analytics の機能はありますか?

<!-- 3616924 -->
はい。Windows Analytics の次の機能は、廃止されたか、Desktop Analytics でまだ利用できません。

#### <a name="general"></a>全般

- Configuration Manager を必要としないシナリオのサポート。 たとえば、[Intune のサポート](#bkmk_intune)などです。
- 有効な Windows ライセンスと E3、E5 のライセンス前提条件
- Azure AD テナントごとの複数のワークスペースのサポート
- カスタム クエリを実行し、未加工のソリューション データをエクスポートする機能
- カスタム レポートのデータ モデル ドキュメント

#### <a name="upgrade-readiness"></a>Upgrade Readiness

- Internet Explorer のサイト検出データ
- Microsoft 365 Apps アドイン分析情報 (現在は、[Configuration Manager で使用可能](#bkmk_office))
- フィードバック ハブの分析情報

#### <a name="update-compliance"></a>Update Compliance

- Windows Update for Business のサポート
- 配信の最適化の分析情報
- Windows 10 長期サービス チャネル (LTSC) のサポート
- Windows Insider レポート
- Windows Defender の状態

> [!Note]
> Desktop Analytics では利用できない機能を含め、既存のすべての Update Compliance の機能は、Azure portal の [Update Compliance](/windows/deployment/update/update-compliance-get-started) ソリューションで引き続き使用できます。

#### <a name="device-health"></a>デバイスの正常性

- ドライバーの正常性
- アプリの正常性 (展開計画の範囲外)
- 頻繁にクラッシュするデバイスまたはドライバーに起因するクラッシュ
- Windows サインインの正常性
- Windows Information Protection
- Windows Server のサポート

## <a name="other"></a>その他

### <a name="can-i-use-desktop-analytics-for-my-microsoft-365-apps-upgrades"></a><a name="bkmk_office"></a> Microsoft 365 Apps のアップグレードに Desktop Analytics を使用できますか?

いいえ。Desktop Analytics は Windows が対象です。 Microsoft は、多くのお客様と密接に協力して Desktop Analytics を開発しました。 お客様からのフィードバックは、Desktop Analytics によって Windows の展開を確実に管理する方法に関するものです。 また、[Microsoft 365 Apps の準備](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness)を Configuration Manager および Intune の Microsoft 365 Apps 管理ツールともっと緊密に統合してほしいという要望もありました。 Microsoft では、Desktop Analytics での Windows のシナリオに重点を置いて、これらの領域に関する取り組みを続けています。

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Desktop Analytics に関するフィードバックを提供するにはどうすればよいですか?

Desktop Analytics に関するフィードバックを共有するには、ポータルの上部にある **[気に入った機能の報告]** アイコンを選択します。 フィードバックの理解に役立つスクリーンショットを送信に含めてください。 また、[UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805) では、製品の提案を送信したり、他のアイデアに投票したりすることもできます。

> [!Note]
> [気に入った機能の報告] や UserVoice で、個人情報を共有しないでください。 そのような個人情報としては、テナント ID や商用 ID などがあります。[気に入った機能の報告] や UserVoice のチャネルを通じて、Microsoft からサポートが提供されることはありません。 Desktop Analytics ワークスペースに関するサポートを得るには、ナビゲーション メニューの **[ヘルプとサポート]** リンクを選択し、サポート チケットを開いてください。