---
title: 共同管理を使用したクラウドの接続
titleSuffix: Configuration Manager
description: 共同管理は、有効にするとすぐに役立ちます。
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5ca960ddd6a4057da10341063f0b14a7f1d104d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075814"
---
# <a name="cloud-connecting-with-co-management"></a>共同管理を使用したクラウドの接続

![Blastoff シリーズのバナー](media/blastoff-banner.png)

共同管理によって、既存の Configuration Manager の展開に新しい機能が追加されます。これまでの作業方法は変更されません。 共同管理を有効にすると、すぐにクラウドを利用できます。 その価値は、既存の管理インフラストラクチャおよびプロセスに適用できます。

この共同管理のクイック スタート シリーズでは、新しい管理の価値をすぐに活用する方法について説明します。 共同管理は、すぐに利用できる機能やツールを作成するために構築されています。

次のビデオでは、Microsoft 社の副社長である Brad Anderson がこの共同管理シリーズを紹介します。

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]

| イミディエイト モード | はじめに |
|-----------------|-----------------|
| - [条件付きアクセス](#bkmk_ca)<br> - [Intune からのリモート操作](#bkmk_remote)<br> - [クライアントの正常性](#bkmk_client-health)<br> - [ハイブリッド Azure AD](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [共同管理へのパス](#bkmk_paths)<br> - [ハイブリッド Azure AD の設定](#bkmk_setup-hybrid-aad)<br> - [Windows 10 へのアップグレード](#bkmk_upgrade-win10)<br> - [FastTrack のサポートを受ける](#bkmk_fasttrack) |

## <a name="immediate-value"></a>イミディエイト モード

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**条件付きアクセスとデバイス コンプライアンス** | Intune のコンプライアンス規則に基づいて企業リソースへのユーザー アクセスを制御します | [![条件付きアクセスのビデオのサムネイル](media/thumbnail-conditional-access.png)](quickstart-conditional-access.md) |
| <a name="bkmk_remote"></a>**Intune からのリモート操作** | 共同管理対象デバイスに対して Intune からリモート操作を実行します。 たとえば、デバイスをワイプしてリセットし、登録とアカウントを維持します | [![リモート操作のビデオのサムネイル](media/thumbnail-remote-action.png)](quickstart-remote-actions.md) |
| <a name="bkmk_client-health"></a>**Configuration Manager クライアントの正常性** | Azure portal 上の Intune から Configuration Manager クライアントの正常性を把握します | [![クライアントの正常性のビデオのサムネイル](media/thumbnail-client-health.png)](quickstart-client-health.md) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Azure AD を利用すれば、クラウド環境とオンプレミス環境の両方で、ユーザーの生産性とリソースのセキュリティを改善できます | [![ハイブリッド Azure AD のビデオのサムネイル](media/thumbnail-azure-ad.png)](quickstart-hybrid-aad.md) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | デバイスの展開、管理、廃止、またはリサイクルに関連する時間、リソース、および複雑さを軽減します。 また、Autopilot によって、エンド ユーザーのエクスペリエンスも向上します。 | [![Windows Autopilot のビデオのサムネイル](media/thumbnail-autopilot.png)](quickstart-autopilot.md) |

## <a name="getting-started"></a>はじめに

共同管理を有効にするには、ここから始めて、技術的な懸念を解消してください。

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**共同管理へのパス** | 共同管理を設定するには、主に 2 つの方法があります。また、各パスの前提条件を理解することが重要です。  各パスは、Azure AD、ConfigMgr、Intune、Windows クライアントをいくつか組み合わせる必要があります。 | [![共同管理パス スライドのサムネイル](media/thumbnail-paths.png)](quickstart-paths.md) |
| <a name="bkmk_setup-hybrid-aad"></a>**ハイブリッド Azure AD の設定** | ご利用の環境に現在、ドメイン参加済みの Windows 10 デバイスがある場合は、共同管理を有効にする前にハイブリッド Azure AD を設定します。 | [![ハイブリッド Azure AD の設定のビデオのサムネイル](media/thumbnail-setup-azure-ad.png)](quickstart-setup-hybrid-aad.md) |
| <a name="bkmk_upgrade-win10"></a>**Windows 10 へのアップグレード** | 共同管理には Windows 10 バージョン 1709 以降が必要です。 | [![Windows 10 へのアップグレードのビデオのサムネイル](media/thumbnail-upgrade-win10.png)](quickstart-upgrade-win10.md) |
| <a name="bkmk_fasttrack"></a>**FastTrack のサポートを受ける** | FastTrack 組織は、共同管理の設定を含む、すべての種類の組織での Microsoft 365 アプリの展開のサポートを専門とする、Microsoft エンジニアの大規模なグループです。 | [![FastTrack のビデオのサムネイル](media/thumbnail-fasttrack.png)](quickstart-fasttrack.md) |
