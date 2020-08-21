---
title: 非推奨の機能
titleSuffix: Configuration Manager
description: Configuration Manager でサポートされなくなった機能について説明します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 29b5dd8fdceb803de77aff9adbd0614d1e201b18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694257"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Configuration Manager から削除された機能と非推奨の機能

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager のサポートから非推奨になった、または削除された機能を示します。 非推奨の機能は、今後の更新で削除されます。 これらの将来的な変更は、Configuration Manager の使用に影響する可能性があります。  

この情報は今後のリリースで変更されます。 Configuration Manager の非推奨の機能は個別に含まれないことがあります。

## <a name="deprecated-features"></a>非推奨の機能

次の機能は非推奨とされます。 今でも使用できますが、Microsoft は将来のサポート終了を計画しています。

|機能|最初に非推奨と発表|削除されたサポート&nbsp;|
|-----------|---|--------------|
|Azure からコンテンツを共有するための実装が変更されました。 コンテンツが有効なクラウド管理ゲートウェイを使用します。 今後は、従来のクラウド配布ポイントを作成できなくなります。|2019 年 2 月|未定<sup>[注 1](#bkmk_note1)</sup>|
|クラウド管理ゲートウェイとクラウドの配布ポイントのための Azure への従来のサービス展開。 詳細については、[CMG の計画](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)に関するページを参照してください。|2018 年 11 月|未定<sup>[注 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> 注 1:サポートの削除 TBD

特定の時間枠は TBD (未定) です。 Microsoft では、新しいプロセスまたは機能に変更することをおすすめしていますが、しばらくの間は、非推奨であるプロセスや機能を引き続き使用できます。

## <a name="unsupported-and-removed-features"></a>サポートされていない機能と削除された機能

次の機能はサポート対象外となりました。 製品に含まれていない場合もあります。

|機能|最初に非推奨と発表|削除されたサポート&nbsp;|  
|-----------|---|--------------|  
| デバイス登録とセキュリティ更新プログラムの **[最近のデータを表示]** の Desktop Analytics のオプション。<!-- 7080949 --> 詳細については、「[データ待機時間](../../../../desktop-analytics/troubleshooting.md#data-latency)」をご覧ください。|2020 年 5 月|2020 年 7 月|
| Windows Analytics と Upgrade Readiness の統合。 詳細については、[KB 4521815:Windows Analytics の廃止 (2020 年 1 月 31 日)](https://support.microsoft.com/help/4521815/windows-analytics-retirement) に関するページをご確認ください。 | 2019 年 10 月 14 日 | 2020 年 1 月 31 日 |
| 条件付きアクセス コンプライアンス ポリシーに対するデバイス正常性構成証明の評価 <!--1235616 aka 3608202--> 詳細については、「[ハイブリッド MDM はどうなりましたか?](../../../../mdm/understand/what-happened-to-hybrid.md)」を参照してください。| 2019 年 7 月 3 日 | バージョン 1910 |
| Configuration Manager ポータル サイト アプリ | 2019 年 5 月 21 日 | バージョン 1910 |
| アプリケーション カタログ Web サイト ポイントとアプリケーション カタログ Web サービス ポイントというサイト システムの役割を両方含む、アプリケーション カタログ: 詳細については、「[アプリケーション カタログの削除](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)」を参照してください。 | 2019 年 5 月 21 日 | バージョン 1910 |
|Configuration Manager で Windows Hello for Business 設定を使用した証明書ベースの認証<br>詳細については、[Windows Hello for Business の設定](../../../../protect/deploy-use/windows-hello-for-business-settings.md) に関するページを参照してください。|2017 年 12 月|バージョン 1910|
|Mac および Linux 用 System Center Endpoint Protection<br>詳しくは、[サポートの終了ブログ投稿](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257)をご覧ください。|2018 年 10 月|2018 年 12 月 31 日|
|オンプレミスの条件付きアクセス<br>詳細については、「[ハイブリッド MDM はどうなりましたか?](../../../../mdm/understand/what-happened-to-hybrid.md)」を参照してください。|2019 年 1 月 30 日|2019 年 9 月 1 日|
|ハイブリッド モバイル デバイス管理 (MDM)<br>詳細については、「[ハイブリッド MDM はどうなりましたか?](../../../../mdm/understand/what-happened-to-hybrid.md)」を参照してください。<br><br>2019 年 2 月末に予定されている 1902 Intune サービス リリース以降、新規のお客様は新しいハイブリッド接続を作成できなくなります。<!--Intune feature 2683117-->|2018 年 8 月 14 日|2019 年 9 月 1 日|
|Security Content Automation Protocol (SCAP) 拡張機能。 <!--3607889--><br>以前の認定バージョンは、引き続き [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=48741)でご利用いただけます。|2018 年 9 月|バージョン 1810|
|アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 新しいソフトウェア センターを使う必要があります。 詳しくは、「[ソフトウェア センターの構成](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)」をご覧ください。<!--1358309-->|2017 年 8 月 11 日| バージョン 1806|
|以前のバージョンのソフトウェア センター。<br><br>ソフトウェア センターの詳細については、「[アプリケーション管理の計画と構成](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex)」をご覧ください。|2016 年 12 月 13 日|バージョン 1802|
|Configuration Manager によるバーチャル ハード ディスク (VHD) の管理。 <br><br>この非推奨機能には、新しい VHD の作成オプション、またはタスク シーケンスを使用した VHD の管理オプションの削除と、Configuration Manager コンソールからのバーチャル ハード ディスクのノードの削除が含まれます。 <br><br>既存の VHD は削除されませんが、Configuration Manager コンソール内からはアクセスできなくなります。  |2017 年 1 月 6 日 |バージョン 1710|
|タスク シーケンス: <br /> - ディスクをダイナミックに変換 <br /> - 展開ツールのインストール |2016 年 11 月 18 日|バージョン 1710|
|Upgrade Assessment Tool<br><br>Upgrade Assessment Tool は、Configuration Manager と Application Compatibility Toolkit (ACT) 6.x の両方に依存します。 ACT の最終バージョンは、Windows 10 v1511 ADK に同梱されていました。 今後、ACT が更新されることはないため、Upgrade Assessment Tool のサポートは廃止されます。 非推奨に関する注記は、2016 年 9 月 12 日に [UAT のダウンロード ページ](https://www.microsoft.com/software-download/windows10)に追加されました。 | 2016 年 9 月 12 日  | 2017 年 7 月 11 日 |
|ネットワーク負荷分散 (NLB) クラスターを備えたソフトウェアの更新ポイント | 2016 年 2 月 27 日 | バージョン 1702 |
|タスク シーケンス: <br /> - OSDPreserveDriveLetter  <br /><br /> 既定で、オペレーティング システムの展開中に、Windows セットアップが使用する最適なドライブ文字を決定するようになりました (通常は C:)。 別のドライブを使用するように指定する場合は、オペレーティング システムの適用タスク シーケンスのステップで場所を変更できます。 **[このオペレーティング システムの適用先を選択してください。]** の設定に進みます。 **[特定の論理ドライブ文字]** を選び、使うドライブを選びます。 |2016 年 6 月 20 日 |バージョン 1606 |
|ネットワーク アクセス保護 (NAP) - System Center 2012 Configuration Manager の機能|2015 年 7 月 10 日|バージョン 1511|  
|帯域外管理 - System Center 2012 Configuration Manager の機能|2015 年 10 月 16 日|バージョン 1511|

### <a name="features-removed-in-version-1511"></a>バージョン 1511 で削除された機能

次のセクションでは、バージョン 1511 で削除された機能の詳細を示します。

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> 帯域外管理  

Configuration Manager では、Configuration Manager コンソール内からの AMT ベースのコンピューターに対するネイティブ サポートは削除されました。  

- [Configuration Manager 用 Intel SCS アドオン](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)を使用すれば、AMT ベースのコンピューターは引き続き完全に管理されます。 アドオンを使用することで、最新の機能にアクセスして AMT を管理できます。Configuration Manager にこれらの変更が組み込まれるまでに適用されていた制限は解除されます。  

- System Center 2012 Configuration Manager での帯域外管理は、この変更の影響を受けません。  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> ネットワーク アクセス保護

Configuration Manager では、ネットワーク アクセス保護のサポートが削除されました。 この機能は Windows Server 2012 R2 で非推奨となり、Windows 10 からは削除されています。  

ネットワーク アクセス保護の代替方法については、「 *ネットワーク ポリシーとアクセス サービスの概要* 」で [非推奨の機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11))に関する説明を参照してください。

## <a name="see-also"></a>関連項目

- [削除と非推奨](removed-and-deprecated.md)
- [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)
- [Configuration Manager の Current Branch バージョンのサポート](../../../servers/manage/current-branch-versions-supported.md)