---
title: 中国の 21Vianet が運用する Intune
titleSuffix: ''
description: 中国の 21Vianet が運用している Intune。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c4e567c7812f53a7497f368ded47d72640443f6
ms.sourcegitcommit: 678104677ad36b789630befdc5e0f1efc572c14b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86137393"
---
# <a name="intune-operated-by-21vianet-in-china"></a>中国の 21Vianet が運用する Intune  

21Vianet が運用している Intune は、中国において、セキュリティで保護され、信頼性の高い、スケーラブルなクラウド サービスのニーズを満たすように設計されています。 サービスとしての Intune は Microsoft Azure に基づいて構築されています。 21Vianet が運用している Microsoft Azure は、中国に配置された、物理的に分離されたクラウド サービスのインスタンスです。 これは、21Vianet によって独立して運用され、業務が行われます。 このサービスでは、Microsoft が21Vianet にライセンスしたテクノロジが利用されています。

Microsoft がサービス自体を運用しているわけではありません。 21Vianet により、サービスの運用、提供、および配信の管理が行われます。 21Vianet は、中国にあるインターネット データセンター サービス プロバイダーです。 ホスティング、管理されたネットワーク サービス、およびクラウド コンピューティング インフラストラクチャ サービスが提供されます。 21Vianet は、Microsoft テクノロジのライセンスを取得することでローカル データセンターを運用し、ユーザーが中国内にデータを保持しながら Intune サービスを使用できるようになります。 また、21Vianet によって、サブスクリプション、課金、およびサポートのサービスも提供されます。

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>21Vianet が運用している Intune の機能の違い

中国のサービスは中国内のパートナーによって運用されているため、Intune には機能の違いがいくつかあります。 

- 21Vianet が運用している Intune では、スタンドアロン展開のみがサポートされています。 System Center Configuration Manager を使用した共同管理のサポートは、現在開発中です。
- パブリック クラウドからソブリン クラウドへの移行はサポートされていません。 21Vianet が運用している Intune への移行を希望されるお客様は、手動で移行する必要があります。
- テナントのアタッチ機能 (クラウド コンソールのシナリオをサポートするために登録なしでデバイスを Intune に同期する) は、現在サポートされていません。
- 派生資格情報は、21Vianet が運用する Intune ではサポートされていません。
- 21Vianet が運用している Intune では Intune エージェントがサポートされていないため、レガシ PC 管理もサポートされていません。
- Windows 10 の管理は、最新の MDM チャネルの使用によってサポートされます。
- 21Vianet が運用している Intune では、オンプレミス Exchange Connector がサポートされていません。
- Windows Autopilot およびビジネス ストア機能は、現在使用できません。
- 中国では Google Mobile Services を使用できないため、21Vianet が運用している Intune のお客様は Google Mobile Services を必要とする機能を使用できません。 これには次の機能があります。
  - SafetyNet デバイスの構成証明などの Google Play プロテクト機能。
  - Google Play ストアからのアプリの管理。
  - Android エンタープライズの機能。 詳細については、こちらの [Google のドキュメント](https://support.google.com/work/android/answer/6270910?hl=en)をご覧ください。
- Android 用 Intune ポータル サイト アプリでは、Microsoft Intune サービスと通信するために Google Mobile Services が使用されます。 中国では Google Play サービスを使用できないため、一部のタスクは完了までに最大 8 時間かかることがあります。 詳細については、[こちらの記事](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable)を参照してください。 
- 地域の規制に従って機能を強化するために、中国では、Intune のクライアント エクスペリエンス (ポータル サイト アプリ) が異なる場合があります。
- フェンシングは使用できません。
- モバイル アプリケーション管理 (MAM) の可用性は、中華人民共和国で使用できるアプリに制限されます。

## <a name="you-control-customer-data"></a>自分で顧客データを制御する

21Vianet が運用している Microsoft Azure、Intune、Office 365、および Power BI では、自分のデータを完全に制御できます。
- 顧客データがどこに配置されているかがわかります。
- 顧客データへのアクセスを制御できます。
- サービスを退会する場合、顧客データを制御できます。
- 顧客データのセキュリティを制御するオプションがあります。

21Vianet が運用している Microsoft Azure、Intune、Office 365、および Power BI では、ご自身が自分のデータの所有者になります。
- 21Vianet は広告のために顧客データを使用しません。
- 顧客データにアクセスできるユーザーを制御できます。
- 各顧客のデータを分離するために、論理的な分離が使用されます。
- 私たちはシンプルで透明性のあるデータ使用ポリシーを提供し、独立した監査を受けます。
- 私たちの下請け業者は、私たちのプライバシー要件を満たすように契約を結んでいます。

## <a name="data-subject-requests"></a>データ主体の要求

21Vianet が運用している Intune のテナント管理者ロールでは、次の方法でデータ主体のデータを要求できます。

- Azure Active Directory 管理センターを使用すると、テナント管理者は、Azure Active Directory および関連するサービスからデータ主体を完全に削除できます。 詳細については、[Azure データ主体の要求 - 削除](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)に関する記事をご覧ください
- 21Vianet が運用している Microsoft サービスのシステム生成ログは、テナント管理者がデータ ログのエクスポートを使用してエクスポートできます。 詳細については、[Azure データ主体の要求 - エクスポート](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export)に関する記事をご覧ください。

## <a name="next-steps"></a>次のステップ

[Intune でサポートされている構成の詳細](supported-devices-browsers.md)