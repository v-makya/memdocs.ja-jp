---
title: Ready for Windows
titleSuffix: Configuration Manager
description: Ready for Windows Web サイトの提供終了
ms.date: 10/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: da56dbe1a363606e50569db8be10d65d10d1b422
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695570"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Ready for Modern Desktop の提供終了に関する FAQ

<!-- placeholder -->

## <a name="general"></a>全般

### <a name="what-happened-to-the-ready-for-windows-website"></a>Ready for Windows Web サイトはどうなりましたか?

多くのお客様は、Windows 10 と Office 365 ProPlus を最新の状態に保つことについて課題を抱えています。 通常、このプロセスは手動で行われるため、主な課題はアプリケーションのテストです。 IT 管理者とアプリケーション所有者が既存のアプリケーションを継続的に分析し、発生した問題を修正することは時間がかかります。

*Ready for Modern Desktop* ディレクトリには、Windows 10 および Office 365 ProPlus を実行している商用デバイスでサポートされ、使用されているソフトウェア ソリューションが掲載されていました。 このディレクトリは、Windows 10 および Office 365 の最新バージョンの展開を検討している IT 管理者を支援するものです。

IT 管理者からは、これらの分析情報を既に使用しているツールと統合して展開計画を立てたいというフィードバックをいただいています。 Windows 10 と Office 365 ProPlus のアップグレード プロジェクトを計画および管理するには、Configuration Manager で [Desktop Analytics](https://aka.ms/dadocs) と [Office 365 ProPlus の準備機能](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch)を使用します。 

### <a name="what-is-desktop-analytics"></a>Desktop Analytics とは

[Desktop Analytics](https://aka.ms/dadocs) は、Configuration Manager に統合されているクラウドベースのサービスです。 このサービスでは、Windows エンドポイントの更新準備に関して豊富な情報に基づく意思決定をするために役立つ分析情報やインテリジェンスが提供されます。 お客様の組織固有のデータと、Microsoft のクラウド サービスに接続された数百万台の Windows デバイスから集計された分析情報を組み合わせて利用できます。

-    組織の管理下にあるエンドポイント、アプリケーション、およびドライバーを包括的に把握できます。

-    アプリケーションおよびドライバーと、最新の Windows 機能更新プログラムとの互換性を評価できます。 既知の問題に対する軽減策に関する推奨事項と、基幹業務アプリの高度な分析情報を受け取ることができます。

-    Microsoft クラウドの人工知能 (AI) を使用して、環境全体を適切に表す一連のパイロット デバイスを最適化できます。

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Windows の展開計画に Desktop Analytics の使用が推奨されるのはなぜですか?

Desktop Analytics を使うと、次のようなメリットがあります。

-    **デバイスとソフトウェアのインベントリ**: アプリや Windows のバージョンなどの主要要因のインベントリ。

-    **パイロットの識別**: 要因が最も広範にカバーされる最小のデバイス セットの識別。 Windows のアップグレードと更新プログラムのパイロットにとって最も重要な要素が重視されます。 パイロットを確実に成功させることで、迅速かつ自信を持って、運用環境での広範な展開を続けることができます。

-    **問題の識別**: サービスでは、集計された市場データと、ユーザーの環境からのデータを使用して、Windows を最新の状態に維持することに関する潜在的な問題が予測されます。 その後、可能性のある軽減策が提案されます。

-    **Configuration Manager の統合**: 既存のオンプレミス インフラストラクチャがクラウド対応になります。 このデータと分析を使用して、デバイスに Windows を展開し、管理します。

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>Desktop Analytics の *Ready for Windows* の状態にはどのような意味がありますか?

"**導入の状態**" は、Microsoft とデータを共有する商用デバイスの情報に基づいています。 この状態は、ソフトウェア ベンダーからのサポートに関する声明と統合されています。

Desktop Analytics を使うと、商用デバイスで見つかった資産の各バージョンについて導入の状態が提供されます。 この状態には、コンシューマー デバイスまたはデータを共有していないデバイスからのデータは含まれません。 この状態は、すべての Windows 10 デバイスにおける導入率を表しているわけではありません。

詳細については、「[互換性の評価](compat-assessment.md)」を参照してください。

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Desktop Analytics で *Ready for Windows* の状態を取得するのはどの資産ですか? 

次の場合、Desktop Analytics の資産は *Ready for Windows* 状態になります。

-    ソフトウェア プロバイダーはこのソリューションのサポートを宣言しています。
-    お客様は、Microsoft と情報を共有している多数の商用 Windows 10 デバイスに展開しています。
-    この資産は商用ユーザーに関連しています。

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Desktop Analytics では、他にどのような分析情報を得られますか?

Desktop Analytics を使うと、[デバイスとそれにインストールされているアプリ](about-assets.md)のインベントリと、基幹業務アプリの[高度な分析情報](compat-assessment.md#advanced-insights)が提供されます。 

## <a name="software-providers"></a>ソフトウェア プロバイダー

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>まだ Desktop Analytics に自社のソフトウェア ソリューションを掲載できますか?

御社の製品が 32 ビットまたは 64 ビットの Windows 10 または Office 365 ProPlus で動作するというサポートに関する声明を公開してください。 御社のソリューションを Desktop Analytics で紹介するには、Microsoft の担当者にお問い合わせください。

### <a name="how-can-listing-my-solutions-benefit-me"></a>自社のソリューションを掲載すると、どのようなメリットがありますか?

数千人の IT 管理者が、Configuration Manager と Desktop Analytics を使用して数百万台のデバイスを管理しています。 これらのツールを使用すると、自信を持って組織の計画を立て、Windows 10 および Office 365 ProPlus の最新バージョンにアップグレードすることができます。 また、ソフトウェア ソリューションの購入に関する判断にも使用されます。

Microsoft では、ソフトウェア ベンダーからのサポートに関する声明を、商用デバイスから受け取った導入情報と統合しています。 世界中の組織が、Desktop Analytics や Office readiness ツールでこのデータを使用しています。 

御社のサポートに関する声明が資産に適切に関連付けられていない場合は、Microsoft の担当者にお問い合わせください。

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>自社の資産に関する詳細なパフォーマンス メトリックを確認できますか?

開発者センターを介して、正常性およびメトリック レポートで御社のソリューションのパフォーマンスを評価してください。 

- [Windows ストア](https://docs.microsoft.com/windows/uwp/publish/health-report)
- [デスクトップ](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
- [Office アドイン](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>Windows 10 と Office 365 ProPlus 用の互換性のある資産を開発するにはどうすればよいですか?

現時点で御社のデスクトップ アプリケーションに互換性があることを確認し、Windows 10 との互換性を今後も維持してください。 詳細については、「[アプリケーションの互換性](https://developer.microsoft.com/windows/desktop/app-compatibility)」を参照してください。

Office 365 ProPlus 用のソリューションを開発している場合は、「[Office での COM、VSTO、および VBA アドインの開発に関するベストプラクティス](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office)」を参照してください。
