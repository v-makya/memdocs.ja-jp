---
title: Technical Preview リリース
titleSuffix: Configuration Manager
description: Configuration Manager の新機能を体験する Technical Preview Branch について説明します。
ms.date: 03/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec49f9931240e17218c125f1fa514088c83c55fd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701840"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager の Technical Preview

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の毎月の Technical Preview Branch の詳細を説明します。 Technical Preview では、マイクロソフトが取り組んでいる新しい機能が紹介されます。 Configuration Manager の Current Branch にまだ組み込まれていない新機能が導入されています。 これらの機能は、最終的に Current Branch の更新プログラムに組み込まれる可能性があります。 機能が最終的に確定する前に実際に試してみて、フィードバックを提供してください。

このリリースはテクニカル プレビューであるため、詳細や機能は変更されることがあります。

この情報は、Configuration Manager Technical Preview Branch のすべてのバージョンに適用されます。 この記事では、各新機能とそれが最初に組み込まれる Technical Preview バージョンの一覧を示します。 たとえば、2020 年 (`20`) 1 月 (`01`) のバージョンは **2001** です。 個々の機能の詳細については、Preview バージョンごとの記事で説明します。

Configuration Manager の *Current Branch* の新機能については、「[System Center Configuration Manager の増分バージョンの新機能](../plan-design/changes/whats-new-incremental-versions.md)」をご覧ください。

> [!Tip]
> このページが更新されたときに通知を受け取るには、次の URL をコピーして RSS フィード リーダーに貼り付けます。`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a> 要件と制限事項

> [!IMPORTANT]
> Technical Preview はラボ環境での使用目的に限定してライセンスされます。 Microsoft はサポート サービスを提供しない場合があり、また、Technical Preview では特定の機能が使用できない場合があります。 さらに、Technical Preview ソフトウェアは、製品版ソフトウェアに比べて、セキュリティ、プライバシー、アクセシビリティ、可用性および信頼性の基準が低いか、または異なる場合があります。

ほとんどの製品の前提条件については、[サポートされている構成](../plan-design/configs/supported-configurations.md)に関するページの情報をご覧ください。 Technical Preview Branch には次の例外が適用されます。

- 各インストールは 90 日後に使用期限が切れるまでアクティブです。

- サポートされる言語は英語のみです。

- 次のセットアップ コマンド ライン パラメーターのみをサポートしています。

  - `/silent`
  - `/testdbupgrade`

- サービス接続ポイントはオンライン モードでインストールされます。 オフライン モードはサポートされません。

- Technical Preview の特定バージョンごとの個別の記事には、追加の制限または要件が含まれています。

- Technical Preview Branch では、次の機能はサポートされません。

  - この Preview Branch への、またはこの Preview Branch からの[移行](../migration/migrate-data-between-hierarchies.md)。

  - この Preview Branch への[アップグレード](../servers/deploy/install/upgrade-to-configuration-manager.md)。

  - cd.latest フォルダーからの[サイトの回復](../servers/manage/recover-sites.md)。<!--507106-->

- この Preview Branch から Current Branch への更新はサポートされていません。

    > [!Note]
    > Preview バージョンから更新プログラムが使用できる場合は、Configuration Manager コンソールの **[更新とサービス]** ノードから検索してからインストールできます。 コンソール内アップグレード プロセスについては、youtube.com のビデオ「[Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8)」(Configuration Manager 更新プログラム パッケージのインストール) をご覧ください。

- スタンドアロン プライマリ サイトのみをサポートします。 中央管理サイト、複数のプライマリ サイト、またはセカンダリ サイトはサポートされません。

Configuration Manager の Technical Preview Branch では、次の製品とテクノロジがサポートされています。

- 次のバージョンの **SQL Server** のみをサポートします。

  - SQL Server 2017 (累積的な更新プログラム 2 以降)
  - SQL Server 2016 (Service Pack なし、またはそれ以降)
  - SQL Server 2014 (Service Pack 1 以降)
  - SQL Server 2012 (Service Pack 3 以降)

- サイトでは最大 10 台のクライアントがサポートされ、これらでは任意の[サポートされているクライアントの OS バージョン](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)を実行できます。<!-- SCCMDocs#1656 -->

> [!Note]
> ここに製品が記載されていても、そのサポート ライフサイクルを超えてサポートが延長されることを意味するものではありません。 Configuration Manager では、サポート ライフサイクルが終了している製品はサポートされません。 詳しくは、「[Microsoft ライフサイクル ポリシー](https://go.microsoft.com/fwlink/p/?LinkId=208270)」をご覧ください。

## <a name="install-and-update"></a><a name="bkmk_install"></a> インストールと更新

ラボ用の Configuration Manager Technical Preview Branch は、運用環境用の Configuration Manager Current Branch とは異なります。

最初に、Technical Preview Branch のベースライン バージョンをインストールします。 ベースライン バージョンをインストールした後、コンソール内の更新プログラムを使用して、最新のプレビュー バージョンでインストール環境を最新の状態にします。 通常、Technical Preview の新バージョンは毎月使用可能になります。

各 Technical Preview Branch は、それより後の 3 つの連続するバージョンが利用可能になるまでサポートされます。 たとえば、バージョン 1908 がリリースされた時点で、バージョン 1904 はサポートされなくなります。 バージョン 1905、1906、1907 は引き続きサポートされています。 ベースラインがサポートされなくなったときも、すぐにサポートされるバージョンに更新するのであれば、新しい Technical Preview サイトのインストール用にサポートされます。 古いベースラインは、新しいベースライン バージョンが使用できるようになるまでサポートされます。 ベースラインから使用可能な最新のバージョンに更新した後、最新の Technical Preview バージョンをインストールするまで更新プロセスを繰り返します。

> [!TIP]
> Technical Preview の更新プログラムをインストールするときに、プレビュー インストール環境を対象の新しい Technical Preview バージョンに更新します。 Technical Preview のインストールでは、Current Branch のインストールにはアップグレードできません。 また、Current Branch リリースから更新プログラムを受け取ることもありません。
>
> 1 年の間に何回か、Technical Preview Branch と Current Branch のバージョン番号が同じになることがあります。 たとえば、Technical Preview バージョン 1910 と Current Branch バージョン 1910 が存在します。

### <a name="active-baseline-versions"></a>アクティブなベースライン バージョン

リリース後、最長 1 年間、ベースライン バージョンをインストールできます。 新しい Technical Preview サイトをインストールする場合は、最新のベースライン バージョンを使用してください。

- **Technical Preview バージョン 2002**:Configuration Manager Technical Preview Branch バージョン 2002 は、コンソール内更新と、新しいベースライン バージョンの両方として使用できます。

ベースライン バージョンは [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) からダウンロードします。

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> フィードバックについて

Technical Preview の新機能に関するフィードバックをお寄せください。 詳細については、「[製品に関するフィードバック](../understand/find-help.md#product-feedback)」を参照してください。

希望する新しい機能のアイデアがありましたら、ご意見をお寄せください。 新しいアイデアを送信し、他のユーザーのアイデアに投票してください: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com)。

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> 最新バージョンの機能

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2003.md#bkmk_anchor) <!--ID-->

最新の Configuration Manager Technical Preview バージョンでは、以下の機能を使用できます。

### <a name="technical-preview-version-2003"></a>Technical Preview バージョン 2003

- [Microsoft エンドポイント マネージャー コンソールを使用して構成マネージャー クライアントを Microsoft Defender ATP にオンボードする](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [構成アイテムの修復の追跡](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [デバイスの境界グループを表示する](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [新しいフィードバック ウィザード](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Microsoft Edge 管理ダッシュボードの機能強化](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [CMPivot の改善](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [Microsoft に送信されたフィードバックのクエリ](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [タスク シーケンスの進行状況用の新しい SDK メソッド](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [OS 展開の機能強化](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

> [!NOTE]
> Technical Preview の以前のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、Configuration Manager の Current Branch に追加された機能は、Technical Preview Branch でも引き続き利用できます。

<!-- temp remove for 2002 CB ## Features in recent technical previews -->

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

<!--temp remove for 2002 CB  The following features were released with previous versions of the Configuration Manager technical preview branch since current branch version 1910: -->

> [!TIP]
> 新しい Current Branch バージョンが利用できるようになると、そのバージョンで利用できる機能が最新の "*新機能*" 記事に記載されます。 詳しくは、[増分バージョンの新機能](../plan-design/changes/whats-new-incremental-versions.md#supported-versions)に関する記事をご覧ください。

<!-- ### Technical preview version 2003 -->

## <a name="features-in-previous-technical-previews"></a>以前の Technical Preview の機能

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

以下の機能は、Configuration Manager Technical Preview Branch の以前のバージョンでリリースされました。 これらの機能は、以降のバージョンでも使用できますが、Current Branch ではまだ使用できません。

| 機能        | Technical Preview のバージョン |
|----------------|---------------------------|
| フィードバックにファイルを添付する <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| マルチキャスト対応の配布ポイントの機能強化 <!--3785535--> | [Tech Preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| 段階的展開テンプレート <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| クラウド管理ゲートウェイを使用し、場所を問わずリモート制御する <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| コミュニティ ハブの機能強化 <!--3555935--> | [Tech Preview 1906](2019/technical-preview-1906.md#bkmk_hub) |
| コミュニティ ハブの機能強化 <!--4224401--> | [Tech Preview 1905](2019/technical-preview-1905.md#bkmk_hub) |
| コミュニティ ハブと GitHub <!--3555935--> | [Tech Preview 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| クラウド サービスのコスト見積もりツール <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| コミュニティ ハブからレポートのダウンロード <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| コミュニティ ハブ <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| クライアント ベースの PXE レスポンダー サービス <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE ネットワーク ブートでの IPv6 のサポート <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Azure Active Directory の使用 <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| 資産インテリジェンスの改善 <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>関連項目

詳細については、以下の記事を参照してください。

- [ラボでの Configuration Manager の評価](evaluate-with-lab-environment.md)
- [Configuration Manager の増分バージョンの新機能](../plan-design/changes/whats-new-incremental-versions.md)
- [Configuration Manager の概要](../understand/introduction.md)

> [!Tip]
> 有効化に同意が必要な最新のブランチ機能の詳細については、[プレリリース機能](../servers/manage/pre-release-features.md)に関するページを参照してください。
>
> 最初に有効にする必要があるプレリリース版以外の最新のブランチ機能の詳細については、「[更新プログラムのオプション機能の有効化](../servers/manage/install-in-console-updates.md#bkmk_options)」を参照してください。
