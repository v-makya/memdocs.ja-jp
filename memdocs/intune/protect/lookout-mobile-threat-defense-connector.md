---
title: Lookout Mobile Endpoint と Microsoft Intune を統合する
titleSuffix: Microsoft Intune
description: モバイル デバイスから会社のリソースへのアクセスを制御するための Intune と Lookout Mobile Threat Defense (MTD) の統合について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bf06c5057cecd63b5717440eba8bad0542ab642
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461319"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Lookout Mobile Endpoint Security コネクタと Intune

Microsoft Intune に統合された Mobile Threat Defense ソリューションである Lookout によって実行されるリスク評価に基づいて、モバイル デバイスから会社のリソースへのアクセスを制御することができます。 リスクは、Lookout サービスによりデバイスから収集される次のような製品利用統計情報に基づいて評価されます。
- オペレーティング システムの脆弱性
- インストールされた悪意のあるアプリ
- 悪意のあるネットワーク プロファイル

登録済みデバイス向けの Intune コンプライアンス ポリシーで有効にした Lookout リスク評価に基づき、条件付きアクセスのポリシーを構成できます。このポリシーは、検出された脅威に基づき、非準拠デバイスから企業リソースへのアクセスを許可したり、拒否したりするために利用できます。 登録されていないデバイスの場合、アプリ保護ポリシーを使用して、検出された脅威に基づいてブロックまたは選択的ワイプを強制することができます。

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Intune と Lookout Mobile Endpoint Security で会社リソースを保護する方法

Lookout のモバイル アプリ **Lookout for work** は、モバイル デバイスにインストールされ、実行されます。 このアプリは、利用できる場合、ファイル システム、ネットワーク スタック、デバイスとアプリケーションの製品利用統計情報を記録し、Lookout クラウド サービスに送信し、モバイル デバイスの脅威に対するリスクを評価します。 Lookout コンソールでは、要件に合わせ、脅威に対するリスク レベルの分類を変更できます。

- **登録済みデバイスのサポート** - Intune デバイス コンプライアンス ポリシーには Mobile Threat Defense (MTD) 用のルールが含まれ、そこでは Lookout for work からのリスク評価情報を使用できます。 MTD ルールを有効にすると、Intune では、有効にされたポリシーに基づいてデバイスの準拠状態が評価されます。 デバイスが準拠していないことが判明した場合、ユーザーは Exchange Online や SharePoint Online などの会社リソースへのアクセスをブロックされます。 また、ユーザーは、デバイスにインストールされている Lookout for work アプリから、問題を解決して会社のリソースへのアクセスを回復するための案内を受け取ります。 登録されたデバイスでの Lookout for work の使用をサポートするには:
  - [デバイスに MTD アプリを追加する](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [MTD をサポートするデバイス コンプライアンス ポリシーを作成する](../protect/mtd-device-compliance-policy-create.md)
  - [Intune で MTD コネクタを有効にする](../protect/mtd-connector-enable.md)

- **登録されていないデバイスのサポート** - Intune では、Intune アプリ保護ポリシーを使用すると、登録されていないデバイスで Lookout for work アプリからのリスク評価データを使用できます。 管理者は、この組み合わせを使用して、[Microsoft Intune の保護されたアプリ](../apps/apps-supported-intune-apps.md)内の企業データを保護することができ、それらの登録されていないデバイス上の企業データに対してブロックまたは選択的ワイプを発行することもできます。 登録されていないデバイスでの Lookout for work の使用をサポートするには:
  - [登録されていないデバイスに MTD アプリを追加する](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Mobile Threat Defense アプリ保護ポリシーを作成する](../protect/mtd-app-protection-policy.md)
  - [登録されていないデバイスに対して Intune で MTD コネクタを有効にする](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>サポートされているプラットフォーム

Intune に登録するとき、Lookout では次のプラットフォームがサポートされます。

- **Android 4.1 以降**  
- **iOS 8 以降**  

プラットフォームと言語サポートの詳細については、[Lookout Web サイト](https://personal.support.lookout.com/hc/articles/114094140253)を参照してください。  

## <a name="prerequisites"></a>[前提条件]

- Lookout Mobile EndPoint Security エンタープライズ サブスクリプション  
- Microsoft Intune サブスクリプション
- Azure Active Directory Premium
- ユーザーにライセンスが割り当てられている Enterprise Mobility and Security (EMS) E3 または E5。  

詳細については、「[Lookout Mobile Endpoint Security」](https://www.lookout.com/products/mobile-endpoint-security)を参照してください。

## <a name="sample-scenarios"></a>サンプル事例

Intune で Mobile Endpoint Security を使用する場合の一般的なシナリオを次に示します。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいてアクセスを制御する

マルウェアなどの悪意のあるアプリがデバイスで検出されると、脅威が解決されるまで、デバイスで次の行為が禁止されます。

- 会社の電子メールに接続する
- OneDrive for Work アプリを使用して会社のファイルを同期する
- 会社のアプリにアクセスする

*悪意のあるアプリが検出されたときにブロックする:*

> [!div class="mx-imgBorder"]
> ![悪意のあるアプリによるアクセスをブロックするポリシーの概念図](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*修復後、アクセスが与えられる:*

> [!div class="mx-imgBorder"]
> ![修復後にデバイスに付与されるアクセスを示す概念図](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいてアクセスを制御する

Man-in-the-middle 攻撃など、ネットワークに対する脅威を検出し、デバイスのリスクに基づいて WiFi ネットワークへのアクセスを保護します。

*Wi-Fi 経由のネットワーク アクセスをブロックする:*

> [!div class="mx-imgBorder"]
> ![ネットワークの脅威に基づいた WiFi アクセスのブロックを示す画像](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*修復後、アクセスが与えられる:*

> [!div class="mx-imgBorder"]
> ![修復後にアクセスを許可する条件付きアクセスの概念図](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークへの脅威に基づいて SharePoint Online へのアクセスを制御する

Man-in-the-middle 攻撃のようなネットワークの脅威を検出し、デバイス リスクに基づき、企業ファイルの同期を制限します。

*ネットワークの脅威が検出されたときに SharePoint Online をブロック:*

> [!div class="mx-imgBorder"]
> ![SharePoint Online へのアクセスをブロックする概念図](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*修復後、アクセスが与えられる:*

> [!div class="mx-imgBorder"]
> ![ネットワークの脅威の修復後にアクセスを許可する概念図](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいて登録されていないデバイスでアクセスを制御する

Lookout Mobile Threat Defens ソリューションでデバイスが感染していると見なされる場合:
> [!div class="mx-imgBorder"]
> ![検出されたマルウェアによるアプリ保護ポリシーのブロック](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

修復するとアクセス権が付与されます。

> [!div class="mx-imgBorder"]
> ![アプリ保護ポリシーの修復時にアクセス権が付与される](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>次のステップ

このソリューションを実装するために必須となる主な手順:

- [Lookout 統合を設定する](lookout-mtd-connector-integration.md)
- [Intune で Mobile Endpoint Security を有効にする](mtd-connector-enable.md)
- [Lookout for Work アプリを追加して割り当てる](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Lookout デバイス コンプライアンス ポリシーを構成する](mtd-device-compliance-policy-create.md)
- [MTD アプリ保護ポリシーの作成](mtd-app-protection-policy.md)
