---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Configuration Manager に統合された Desktop Analytics サービスの概要。
ms.date: 06/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 09f829bd1695426211ff94381a63b8f23d1b4fe8
ms.sourcegitcommit: 86c2c438fd2d87f775f23a7302794565f6800cdb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411016"
---
# <a name="what-is-desktop-analytics"></a>Desktop Analytics とは

Desktop Analytics は、Configuration Manager に統合されているクラウドベースのサービスです。 そのサービスでは、Windows クライアントの更新準備に関して豊富な情報に基づく意思決定をするために役立つ分析情報やインテリジェンスが提供されます。 組織からのデータと、Microsoft クラウド サービスに接続された何百万ものデバイスから収集されたデータが結合されます。

Configuration Manager で Desktop Analytics を使用すると、次のことができます。  

- 組織で実行されているアプリのインベントリを作成します  

- Windows 10 の最新の機能更新プログラムとのアプリの互換性を評価します  

- 互換性の問題を明らかにし、クラウド対応のデータ分析情報に基づく軽減策の提案を受け取ります  

- 最小のデバイス セットでアプリケーションとドライバー資産全体を表すパイロット グループを作成します  

- パイロット デバイスおよび運用管理デバイスに Windows 10 を展開します  

![Azure portal での Desktop Analytics ホーム ページのスクリーンショット](media/portal-home.png)

次のビデオは、Desktop Analytics に関する詳細情報を含む Ignite 2019 のセッションです。

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Desktop Analytics と Configuration Manager を使用して、管理、サービス、サポートのためのデータ主導の洞察により Windows の TCO を削減する](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

詳細なデモについては、10:00 に進んでください。

> [!Note]  
> Desktop Analytics は、2020 年 1 月 31 日に廃止された Windows Analytics の後継です。
>
> Desktop Analytics には、Windows Analytics の機能が組み込まれています。 また、Desktop Analytics は、Configuration Manager といっそう密接に統合されています。 詳細については、[Windows Analytics のお客様向けの FAQ](faq.md#existing-windows-analytics-customers) に関するページを参照してください。

## <a name="benefits"></a>利点

多くのお客様は、Windows 10 の最新情報の取得と維持に関する課題を抱えています。 主な課題は、アプリケーションをテストすることです。 通常、このプロセスは手動で行われます。 IT 管理者とアプリケーション所有者にとって、既存アプリケーションを継続的に分析するのは時間のかかる作業です。 その後、発生した問題を修復します。

Desktop Analytics を使うと、次のようなメリットがあります。

- **デバイスとソフトウェアのインベントリ**: アプリや Windows のバージョンなどの主要要因のインベントリ。  

- **パイロットの識別**: 要因が最も広範にカバーされる最小のデバイス セットの識別。 それは、Windows のアップグレードと更新プログラムのパイロットにとって最も重要なファクターに注目しています。 パイロットを確実に成功させることで、迅速かつ自信を持って、運用環境での広範な展開に進むことができます。  

- **問題の識別**: サービスでは、集計された市場データと、ユーザーの環境からのデータを使用して、Windows を最新の状態に維持することに関する潜在的な問題が予測されます。 その後、可能性のある軽減策が提案されます。  

- **Configuration Manager の統合**: サービスにより、既存のオンプレミス インフラストラクチャがクラウド対応になります。 このデータと分析を使用して、デバイスに Windows を展開し、管理します。  

## <a name="prerequisites"></a>[前提条件]

Desktop Analytics を使用するには、環境が次の前提条件を満たしていることを確認してください。

### <a name="technical"></a>技術面

- [グローバル管理者](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)のアクセス許可を持つアクティブなグローバル Azure サブスクリプション。 [Microsoft アカウント](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts)はサポートされていません。  

    > [!IMPORTANT]
    > Desktop Analytics は、Windows 診断データを利用する Azure グローバルにホストされる Windows サービスです。 Desktop Analytics は米国政府機関のお客様が利用できる Azure グローバル サービスですが、[US Government Community コンプライアンス (GCC)](https://docs.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc#us-government-community-compliance) の属性を満たしていません。 Microsoft の製品およびサービスのコンプライアンス認証の一覧については、[Microsoft セキュリティ センター](https://docs.microsoft.com/microsoft-365/compliance/offering-home?view=o365-worldwide)に関するページをご覧ください。 Desktop Analytics は、GCC High または米国国防総省 (DOD) のお客様はご利用いただけません。 Desktop Analytics ワークスペースをホストするための Azure Government サブスクリプションの使用はサポートされていません。

    - **[ワークスペースの設定]** を実行するための**ワークスペースの所有者**アクセス許可、および以下のロール:  

      - [**Desktop Analytics 管理者**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions)ロール。

      - 既存のワークスペースを使用したり、既存のリソース グループに新しいワークスペースを作成したりするための、リソース グループに対する [**Log Analytics 共同作成者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor)および[**ユーザーアクセス管理者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)。

      - 新しいリソース グループにワークスペースを作成するための、サブスクリプションに対する[**所有者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)、または[**共同作成者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)と[**ユーザー アクセス管理者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)のアクセス許可。  

    - オンボード後にポータルにアクセスするには、以下が必要です。

      - [**Desktop Analytics 管理者**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions)ロールと、作成された Log Analytics ワークスペースに対する[**所有者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)または[**共同作成者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)アクセス許可。

- Configuration Manager バージョン 1902 および更新プログラムのロールアップ (4500571) 以降。 詳しくは、[Configuration Manager の更新](connect-configmgr.md#bkmk_hotfix)に関する記事をご覧ください。  

    - Configuration Manager での[**完全な権限を持つ管理者**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles)ロール  

    > [!NOTE]
    > Desktop Analytics では、1 つの Azure AD テナントに報告する複数の Configuration Manager 階層がサポートされています。<!-- 4814075 --> 環境内に複数の階層がある場合は、次のオプションがあります。
    >
    > - 異なる商用 ID と Azure AD テナントを使用する。
    > - 同じ商用 ID を使用して Azure AD テナントと Desktop Analytics インスタンスを共有するように、両方の階層を構成する。 各階層を接続するには、[異なるアプリ](connect-configmgr.md#bkmk_connect)を使用します。 ポータルに変更が反映されるには、階層を切断してから最大で 30 日かかることがあります。 

- Windows 7、Windows 8.1、または Windows 10 が実行されているデバイス  

    - 最新の更新プログラムをインストールします。 詳しくは、「[デバイスの更新](enroll-devices.md#update-devices)」をご覧ください。  

    - デバイスには、Configuration Manager クライアント バージョン 1902 および更新プログラムのロールアップ (4500571) 以降も必要です。 詳しくは、[Configuration Manager の更新](connect-configmgr.md#bkmk_hotfix)に関する記事をご覧ください。  

    > [!Note]  
    > Desktop Analytics では、Windows 10 の長期サービス チャネル (LTSC) への、またはそこからのアップグレードはサポートされていません。 詳しくは、[サービスとしての Windows の概要](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)に関する記事をご覧ください。
    >
    > Desktop Analytics は、インプレース アップグレードのシナリオを最適にサポートするように設計されています。 32 ビットから 64 ビット アーキテクチャなど、大幅な変更を行う必要がある場合は、イメージング シナリオを使用します。 これらの従来の OS 展開シナリオでは、Desktop Analytics の分析情報が依然として有益ですが、インプレース アップグレード固有のガイダンスは無視してかまいません。 詳しくは、「[Configuration Manager を使用して、エンタープライズ オペレーティング システムを展開するシナリオ](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)」をご覧ください。

- Windows 診断データ。 詳細については、以下の記事を参照してください。  

    - [診断データのレベル](enable-data-sharing.md#diagnostic-data-levels)  

    - [Desktop Analytics のプライバシー](privacy.md)  

- デバイスから Microsoft パブリック クラウドへのネットワーク接続。 詳しくは、[データ共有を有効にする方法](enable-data-sharing.md)に関する記事をご覧ください  

> [!Important]
> Microsoft は、お客様のプライバシーを管理するためのツールとリソースを提供するために強力なコミットメントを行っています。 その結果、Microsoft は、ヨーロッパの国 (EEA およびスイス) にあるデバイスから次のデータを収集しません。
>
> - Windows 8.1 デバイスからの Windows 診断データ
> - Windows 7 のアプリ使用状況データ

### <a name="licensing-and-costs"></a>ライセンスとコスト

- アクティブなグローバル Azure サブスクリプション。

    > [!NOTE]
    > Configuration Manager の同等のサブスクリプションのほとんどには、Azure AD も含まれています。 例については、[Microsoft 365 のプラン](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans)と [Enterprise Mobility + Security のライセンス](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security)に関する記事を参照してください。

- Desktop Analytics に登録されているデバイスには、有効な Configuration Manager ライセンスが必要です。 詳細については、[Configuration Manager のライセンス](../core/understand/product-and-licensing-faq.md)に関するページを参照してください。

- このデバイスのユーザーには、次のライセンスのいずれかが必要です。

  - Windows 10 Enterprise E3 または E5 (Microsoft 365 F3、E3、または E5 に含まれます)

  - Windows 10 Education A3 または A5 (Microsoft 365 A3 または A5 に含まれます)

  - Windows Virtual Desktop Access E3 または E5  

> [!NOTE]
> これらのライセンス サブスクリプションのコスト以外に、Azure Log Analytics で Desktop Analytics を使用するための追加料金は発生しません。 Desktop Analytics によって取り込まれるデータ型は、Log Analytics データ インジェストおよびリテンション期間の料金がいずれも無料となります。 このデータはまた、課金対象外のデータ型であるため、Log Analytics の日次データ インジェスト上限の影響下にありません。 詳細については、[Log Analytics の使用状況とコスト](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

次のチュートリアルでは、Desktop Analytics と Configuration Manager の使用を開始する詳細な手順が説明されています。
  
> [!div class="nextstepaction"]
> [Windows 10 のパイロット展開](tutorial-windows10.md)
