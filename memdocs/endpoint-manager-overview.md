---
title: Microsoft Endpoint Manager の概要 - Azure | Microsoft Docs
description: エンドポイント マネージャーには、Intune、Configuration Manager、共同管理、Desktop Analytics、Windows Autopilot の他に、オンプレミスを含むすべてのデバイスを管理するための管理センターが含まれています。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2095fdd349437e03c673fb9f7906511c5e3af388
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088379"
---
# <a name="microsoft-endpoint-manager-overview"></a>Microsoft Endpoint Manager の概要

Microsoft Endpoint Manager は、クラウドとオンプレミスでデータを安全な状態に保つための最新のワークプレースおよび最新の管理を実現するのに役立ちます。 Endpoint Manager には、モバイル デバイス、デスクトップ コンピューター、仮想マシン、組み込みデバイス、およびサーバーを管理および監視するために使用するサービスとツールが含まれています。

Endpoint Manager は、既知のサービスと既に使用しているサービス (Microsoft Intune、Configuration Manager、Desktop Analytics、共同管理、Windows Autopilot など) を組み合わせたものです。 これらのサービスは Microsoft 365 スタックの一部であり、アクセスのセキュリティ保護、データの保護、リスクへの応答と管理に役立ちます。

まずは、Microsoft 365 担当の Microsoft コーポレート バイス プレジデントである Brad Anderson による次の 2 分間のビデオをご覧ください。

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>含まれるもの

Endpoint Manager には、次のサービスが含まれています。

- **Microsoft Intune**: Microsoft Intune は、お使いのアプリとサービスに、100% のクラウドベースのモバイル デバイス管理 (MDM) とモバイル アプリケーション管理 (MAM) を提供します。 Android、Android Enterprise、iOS/iPadOS、macOS、Windows 10 のデバイスの機能と設定を制御できます。 Azure Active Directory (AD)、モバイル脅威防御、ADMX テンプレート、Win32 およびカスタムの LOB アプリなどの他のサービスと統合されています。

  Exchange や Active Directory などのオンプレミス インフラストラクチャがある場合は、次のような Intune コネクタを使用することもできます。

  - **Active Directory の Intune コネクタ**は、Windows Autopilot を使用して登録するコンピューターのオンプレミスの Active Directory ドメインにエントリを追加します。 詳細については、[ハイブリッド Azure AD 参加済みデバイスの展開](/mem/intune/enrollment/windows-autopilot-hybrid)に関する記事を参照してください。
  - **Intune Certificate Connector** は、認証と S/MIME 電子メール暗号化で証明書を使用するデバイスからの証明書要求を処理します。 詳細については、[認証での証明書の使用](/mem/intune/protect/certificates-configure)に関する記事を参照してください。

  コンプライアンスの作成と確認のために、エンドポイント マネージャーの一部として Intune を使用し、クラウドを使用してデバイスにアプリ、機能、および設定を展開します。

  詳細については、「[Microsoft Intune の概要](https://docs.microsoft.com/intune/fundamentals/what-is-intune)」を参照してください。

- **Configuration Manager**:Configuration Manager は、ネットワーク上にある、またはインターネットベースのデスクトップ、サーバー、ラップトップを管理するためのオンプレミス管理ソリューションです。 これをクラウド対応にして、Intune、Azure Active Directory (AD)、Microsoft Defender ATP、その他のクラウド サービスと統合することができます。 Configuration Manager を使用して、アプリ、ソフトウェア更新プログラム、およびオペレーティング システムを展開します。 また、コンプライアンスの監視、クエリ、クライアントの操作などをリアルタイムで行うことができます。

  エンドポイント マネージャーの一部として、常に Configuration Manager を使用してください。 いくつかのタスクをクラウドに移行する準備ができたら、[共同管理](https://docs.microsoft.com/configmgr/comanage/)を検討してください。

  詳しくは、「[Configuration Manager とは](https://docs.microsoft.com/configmgr/core/understand/introduction)」を参照してください。

- **共同管理**: 共同管理は、既存のオンプレミス Configuration Manager の投資と、Intune やその他の Microsoft 365 クラウド サービスを使用したクラウドを組み合わせたものです。 Configuration Manager または Intune が 7 つの異なるワークロード グループの管理機関であるかどうかを選択します。

  共同管理では、エンドポイント マネージャーの一部として、条件付きアクセスなどのクラウド機能を使用します。 一部のタスクはオンプレミスのままにし、他のタスクは Intune を使用してクラウドで実行します。

  詳細については、「[共同管理とは](https://docs.microsoft.com/configmgr/comanage/overview)」をご覧ください。

- **Desktop Analytics**: Desktop Analytics は、Configuration Manager に統合されているクラウドベースのサービスです。 Windows クライアントの更新準備に関して豊富な情報に基づく意思決定をするために役立つ分析情報やインテリジェンスを提供します。 このサービスでは、組織からのデータと、Microsoft クラウドに接続された何百万ものデバイスから収集されたデータが結合されます。 組織内のセキュリティ更新プログラム、アプリ、およびデバイスに関する情報を提供し、アプリとドライバーの互換性の問題を特定します。 デバイスにパイロットを作成するのは、多くの場合、組織全体の資産に最適な分析情報を提供するためです。

  エンドポイント マネージャーの一部として、Desktop Analytics のクラウドを利用した分析情報を使用して、Windows 10 デバイスを最新の状態に保ちます。

  詳細については、「[Desktop Analytics とは](https://docs.microsoft.com/configmgr/desktop-analytics/overview)」を参照してください。

- **Windows Autopilot**: Windows Autopilot によって新しいデバイスが設定され、事前に構成され、使用できるようになります。 IT とエンド ユーザーの両方について、最初の展開から有効期限まで、Windows デバイスのライフサイクルを簡略化するように設計されています。

  エンドポイント マネージャーの一部として、オートパイロットを使用してデバイスを事前に構成し、Intune にデバイスを自動的に登録します。 さらに複雑なデバイス構成では、オートパイロットと Configuration Manager、共同管理を統合することもできます (プレビュー中)。

  詳細については、「[Windows Autopilot の概要](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot)」と、[Intune での Windows デバイスの登録](/mem/intune/enrollment/enrollment-autopilot)に関する記事を参照してください。

- **Azure Active Directory (AD)** :Azure AD は、デバイス、ユーザー、グループ、および多要素認証 (MFA) の ID として Endpoint Manager によって使用されます。 **Azure AD Premium** (追加費用がかかる場合があります) には、動的グループ、自動登録、条件付きアクセスなど、デバイス、アプリ、およびデータの保護に役立つ[追加の機能](https://azure.microsoft.com/pricing/details/active-directory/)があります。

  詳細については、[ユーザーの追加](/mem/intune/fundamentals/users-add)、[自動登録の設定](/mem/intune/enrollment/windows-enroll)、[条件付きアクセス](/mem/intune/protect/conditional-access)に関する記事を参照してください。

- **Endpoint Manager admin center**: [管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)は、ポリシーを作成してデバイスを管理するためのワンストップの Web サイトです。 グループ、セキュリティ、条件付きアクセス、レポートなど、その他の主要なデバイス管理サービスをプラグインします。 この管理センターには、Configuration Manager および Intune によって管理されているデバイスも表示されます (プレビュー中)。

## <a name="choose-whats-right-for-you"></a>適切なものを選ぶ

組織に適したものを確認するには、いくつかの方法があります。 次のステップは、組織の目的によって異なります。 何を達成したいかを考慮してください。

次に例を示します。

- 継続的に新しいデバイスをプロビジョニングする場合は、Windows Autopilot から開始します。
- ユーザー、アプリ、デバイスの規則と制御設定を追加する場合は、Intune から開始します。
- 現在 Configuration Manager を使用してアプリを展開していて、セキュリティ要件に基づいた条件付きアクセスを使用する場合は、共同管理から開始します。
- 現在 Configuration Manager を使用していて、Windows 10 デバイスを最新の状態に保つ必要がある場合は、Desktop Analytics から開始します。
- MDM と MAM の使用を開始している場合、または ADMX テンプレートを使用して Office、Microsoft Edge、および Windows の設定を制御する場合は、Intune から開始します。

エンドポイント マネージャーは、クラウド、オンプレミス、クラウド + オンプレミスの 3 つの部分で考えることもできます。

- **クラウド**: すべてのデータは Azure に保存されます。 データ センターは使用しません。 このアプローチにより、クラウドのモビリティによるベネフィットと Azure のセキュリティ上のベネフィットが得られます。

- **オンプレミス**: Configuration Manager を含むオンプレミスのインフラストラクチャがある場合、またはクラウドを使用する準備ができていない場合は、既存のシステムを保持することができます。

- **クラウド + オンプレミス**: 多くの環境が混在しており、クラウド接続のアプローチを使用します。 つまり、クラウドとオンプレミスの組み合わせを使用します。 新しいデバイスの場合は、データのアクセスと保護に Intune のベネフィットを利用します。 Configuration Manager を使用する場合は、追加の機能と分析のためにクラウドに接続します。 一部のワークロードをクラウドに移動する場合は、共同管理を使用することをお勧めします。

## <a name="what-you-need-to-get-started"></a>必要事項

Microsoft Endpoint Manager は、複数のテクノロジを統合するソリューション プラットフォームです。 新しいライセンスではありません。 このサービスは、個々のライセンス条項に従ってライセンス供与されます。 詳細については、[製品のライセンス条項](https://www.microsoft.com/licensing/product-licensing/products)に関するページを参照してください。

現在 Configuration Manager を使用している場合は、Windows デバイスを共同管理するために Microsoft Intune も入手します。 iOS/iPadOS や Android などの他のプラットフォームでは、別の Intune ライセンスが必要になります。

ほとんどのシナリオでは、エンドポイント マネージャーと Office 365 が提供される Microsoft 365 が最適なオプションになります。 詳細については、「[Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise)」を参照してください。

## <a name="next-steps"></a>次のステップ

[クラウド インテリジェンスの機能を活用して、IT を簡素化し、加速させ、最新のワークプレースに移行する](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[チュートリアル:Microsoft Endpoint Manager の Intune のチュートリアル](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[Microsoft 365 とは何ですか? 学習モジュール](https://docs.microsoft.com/learn/modules/what-is-m365/index)
