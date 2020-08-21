---
title: Technical Preview リリース
titleSuffix: Configuration Manager
description: Configuration Manager の新機能を体験する Technical Preview Branch について説明します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76d1edf8598e1abd71b6fd1db7faffa1750110d4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129122"
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

- 特に明記されていない限り、Technical Preview Branch では、Current Branch と同じバージョンの SQL Server がサポートされます。 詳細については、[サポートされている SQL Server のバージョン](../plan-design/configs/support-for-sql-server-versions.md)に関するページを参照してください。

- サイトでは最大 10 台のクライアントがサポートされ、これらでは任意の[サポートされているクライアントの OS バージョン](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)を実行できます。<!-- SCCMDocs#1656 -->

> [!Note]
> ここに製品が記載されていても、そのサポート ライフサイクルを超えてサポートが延長されることを意味するものではありません。 Configuration Manager では、サポート ライフサイクルが終了している製品はサポートされません。 詳しくは、「[Microsoft ライフサイクル ポリシー](https://support.microsoft.com/lifecycle)」をご覧ください。

## <a name="install-and-update"></a><a name="bkmk_install"></a> インストールと更新

ラボ用の Configuration Manager Technical Preview Branch は、運用環境用の Configuration Manager Current Branch とは異なります。

最初に、Technical Preview Branch のベースライン バージョンをインストールします。 ベースライン バージョンをインストールした後、コンソール内の更新プログラムを使用して、最新のプレビュー バージョンでインストール環境を最新の状態にします。 通常、Technical Preview の新バージョンは毎月使用可能になります。

各 Technical Preview Branch は、それより後の 3 つの連続するバージョンが利用可能になるまでサポートされます。 たとえば、バージョン 1908 がリリースされた時点で、バージョン 1904 はサポートされなくなります。 バージョン 1905、1906、1907 は引き続きサポートされています。 ベースラインがサポートされなくなったときも、すぐにサポートされるバージョンに更新するのであれば、新しい Technical Preview サイトのインストール用にサポートされます。 古いベースラインは、新しいベースライン バージョンが使用できるようになるまでサポートされます。 ベースラインから使用可能な最新のバージョンに更新した後、最新の Technical Preview バージョンをインストールするまで更新プロセスを繰り返します。

> [!TIP]
> Technical Preview の更新プログラムをインストールするときに、プレビュー インストール環境を対象の新しい Technical Preview バージョンに更新します。 Technical Preview のインストールでは、Current Branch のインストールにはアップグレードできません。 また、Current Branch リリースから更新プログラムを受け取ることもありません。
>
> 1 年の間に何回か、Technical Preview Branch と Current Branch のバージョン番号が同じになることがあります。 たとえば、Technical Preview バージョン 1910 と Current Branch バージョン 1910 が存在します。

### <a name="active-baseline-versions"></a>アクティブなベースライン バージョン

リリース後、最長 1 年間、ベースライン バージョンをインストールできます。 新しい Technical Preview サイトをインストールする場合は、最新のベースライン バージョンを使用してください。 次の Configuration Manager Technical Preview Branch バージョンは、コンソール内更新と、新しいベースライン バージョンの両方として使用できます。

- **Technical Preview バージョン 2007**

ベースライン バージョンは [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) からダウンロードしてください。

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
<!-- - [title](2020/technical-preview-2007.md) <!--ID-->

最新の Configuration Manager Technical Preview バージョンでは、以下の機能を使用できます。

### <a name="technical-preview-version-2008"></a>Technical Preview バージョン 2008

- [コレクション クエリのプレビュー](2020/technical-preview-2008.md#collection-query-preview) <!--7380401-->
- [機能更新プログラムの SetupDiag エラーを分析する](2020/technical-preview-2008.md#bkmk_setupdiag) <!--4385028-->
- [シナリオの正常性の監視](2020/technical-preview-2008.md#bkmk_health) <!--7699463-->
- [コレクション評価ビュー](2020/technical-preview-2008.md#bkmk_colleval) <!--6251274-->
- [コンソールのタスク シーケンス サイズの確認](2020/technical-preview-2008.md#bkmk_tssize) <!--7645732-->
- [期限切れの収集診断ファイルの削除タスク](2020/technical-preview-2008.md#bkmk_logs) <!--6503308-->
- [現在のフォルダーにオブジェクトをインポートする](2020/technical-preview-2008.md#bkmk_folder) <!--6601203-->

> [!NOTE]
> Technical Preview の以前のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、Configuration Manager の Current Branch に追加された機能は、Technical Preview Branch でも引き続き利用できます。

## <a name="features-in-recent-technical-previews"></a>最近の Technical Preview での機能

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

以下の機能は、Current Branch バージョン 2006 以降の Configuration Manager Technical Preview Branch の以前のバージョンでリリースされました。

> [!TIP]
> 新しい Current Branch バージョンが利用できるようになると、そのバージョンで利用できる機能が最新の "*新機能*" 記事に記載されます。 詳しくは、[増分バージョンの新機能](../plan-design/changes/whats-new-incremental-versions.md#supported-versions)に関する記事をご覧ください。

### <a name="technical-preview-version-2007"></a>Technical Preview バージョン 2007

- [テナントのアタッチ:Microsoft Endpoint Manager 管理センターでハードウェア インベントリを表示する](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [クライアント データ ソース ダッシュボードの機能強化](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [一部のコンソール領域で固定幅フォントが使用される](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [タスク シーケンス ポリシー サイズの管理](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [管理センターのデバイス タイムラインの機能強化](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

## <a name="features-in-previous-technical-previews"></a>以前の Technical Preview の機能

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

以下の機能は、Configuration Manager Technical Preview Branch の以前のバージョンでリリースされました。 これらの機能は、以降のバージョンでも使用できますが、Current Branch ではまだ使用できません。

| 機能        | Technical Preview のバージョン |
|----------------|---------------------------|
| 共同管理デバイスでポータル サイト アプリを使用する <!--3601237--> | [Tech Preview 2006](2020/technical-preview-2006.md#bkmk_portal) |
| CMG を介した利用可能なアプリの改善 <!--7033501--> | [Tech Preview 2006](2020/technical-preview-2006.md#bkmk_availapp) |
| テナント接続:Microsoft Endpoint Manager admin center での Configuration Manager 操作の改善 <!--7518897--> | [Tech Preview 2006](2020/technical-preview-2006.md#bkmk_apps) |
| テナントのアタッチ:管理センターのデバイス タイムライン <!--7141381--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_timeline) |
| テナントのアタッチ:管理センターからアプリケーションをインストールする <!--6024389--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_apps) |
| テナントのアタッチ:管理センターからの CMPivot <!--6024392--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_cmpivot) |
| テナントのアタッチ:管理センターからスクリプトを実行する <!--6234688--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_scripts) |
| クラウド管理ゲートウェイ コマンドレットの強化 <!--6978300--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_pwshcmg) |
| セットアップとアップグレードの失敗を Microsoft に報告する <!--5622909--> | [Tech Preview 2005](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) |
| コンテンツ ライブラリ クリーンアップ ツールの改善 <!--6887878--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_content) |
| コンソールからの探索データのコピー <!--6890051--> | [Tech Preview 2004](2020/technical-preview-2004.md#bkmk_copydisco) |
| PowerShell バージョン 7 のサポート <!--6023299--> | [Tech Preview 2004](2020/technical-preview-2004.md#bkmk_pwsh7) |
| 新しいフィードバック ウィザード <!--3180826--> | [Tech Preview 2003](2020/technical-preview-2003.md#bkmk_feedback) |
| Microsoft に送信されたフィードバックのクエリ <!--6488450--> | [Tech Preview 2003](2020/technical-preview-2003.md#bkmk_smile) |
| フィードバックにファイルを添付する <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| マルチキャスト対応の配布ポイントの機能強化 <!--3785535--> | [Tech Preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| 段階的展開テンプレート <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| クラウド管理ゲートウェイを使用し、場所を問わずリモート制御する <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| クラウド サービスのコスト見積もりツール <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
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
