---
title: Intune を使用した Zimperium MTD コネクタ
titleSuffix: Intune on Azure
description: モバイル デバイスから会社のリソースへのアクセスを制御するための Intune と Zimperium Mobile Threat Defense の統合について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b443f922b31523ec6f27971648ba1ea9c5123867
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989405"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Zimperium Mobile Threat Defense コネクタと Intune

Microsoft Intune に統合された Mobile Threat Defense (MTD) ソリューションである Zimperium によって実行されるリスク評価に基づき、条件付きアクセスを利用し、モバイル デバイスから会社のリソースへのアクセスを制御できます。 リスクは、Zimperium アプリを実行するデバイスから収集される製品利用統計情報に基づいて評価されます。

Intune デバイス コンプライアンス ポリシーで有効にした Zimperium リスク評価に基づき、条件付きアクセスのポリシーを構成できます。登録済みデバイスの Intune デバイス コンプライアンス ポリシーは、検出された脅威に基づき、非準拠デバイスから企業リソースへのアクセスを許可したり、拒否したりするために利用できます。 登録されていないデバイスの場合、アプリ保護ポリシーを使用して、検出された脅威に基づいてブロックまたは選択的ワイプを強制することができます。

## <a name="supported-platforms"></a>[サポートされているプラットフォーム]

- **Android 4.1 以降**

- **iOS 8 以降**

## <a name="prerequisites"></a>[前提条件]

- Azure Active Directory Premium

- Microsoft Intune サブスクリプション

- Zimperium Mobile Threat Defense サブスクリプション

  - 詳細については、[Zimperium の Web サイト](https://www.zimperium.com/zips-mobile-ips)を参照してください。

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Intune と Zimperium を利用し、会社のリソースをどのように保護しますか?

Android および iOS/iPadOS 向けの Zimperium アプリでは、ファイル システム、ネットワーク スタック、デバイス、アプリケーションのテレメトリが可能な限り記録され、Zimperium クラウド サービスにテレメトリ データが送信されて、モバイル デバイスの脅威に対するリスクが評価されます。

- **登録済みデバイスのサポート** - Intune デバイス コンプライアンス ポリシーには Mobile Threat Defense (MTD) 用のルールが含まれ、そこでは Zimperium からのリスク評価情報を使用できます。 MTD ルールを有効にすると、Intune では、有効にされたポリシーに基づいてデバイスの準拠状態が評価されます。 デバイスが準拠していないことが判明した場合、ユーザーは Exchange Online や SharePoint Online などの会社リソースへのアクセスをブロックされます。 また、ユーザーは、デバイスにインストールされている Zimperium アプリから、問題を解決して会社リソースへのアクセスを回復するための案内を受け取ります。 登録されたデバイスで Zimperium の使用をサポートするには:
  - [デバイスに MTD アプリを追加する](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [MTD をサポートするデバイス コンプライアンス ポリシーを作成する](../protect/mtd-device-compliance-policy-create.md)
  - [Intune で MTD コネクタを有効にする](../protect/mtd-connector-enable.md)

- **登録されていないデバイスのサポート** - Intune では、Intune アプリ保護ポリシーを使用すると、登録されていないデバイスで Zimperium アプリからのリスク評価データを使用できます。 管理者は、この組み合わせを使用して、[Microsoft Intune の保護されたアプリ](../apps/apps-supported-intune-apps.md)内の企業データを保護することができ、それらの登録されていないデバイス上の企業データに対してブロックまたは選択的ワイプを発行することもできます。 登録されていないデバイスで Zimperium の使用をサポートするには:
  - [登録されていないデバイスに MTD アプリを追加する](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Mobile Threat Defense アプリ保護ポリシーを作成する](../protect/mtd-app-protection-policy.md)
  - [登録されていないデバイスに対して Intune で MTD コネクタを有効にする](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>サンプル事例

Intune と Zimperium を統合する場合のシナリオのいくつかを、下記で参照してください。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいてアクセスを制御する

マルウェアなどの悪意のあるアプリがデバイスで検出されると、脅威が解決されるまで、デバイスで次の行為が禁止されます。

- 会社の電子メールに接続する

- OneDrive for Work アプリを使用して会社のファイルを同期する

- 会社のアプリにアクセスする

*悪意のあるアプリが検出されたときにブロックする:*

> [!div class="mx-imgBorder"]
> ![検出された悪意のあるアプリの概念図](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*修復時に付与されるアクセス権:*

> [!div class="mx-imgBorder"]
> ![修復後に付与されたアクセス権の概念図](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいてアクセスを制御する

ネットワークで **Man-in-the-middle** のような脅威を検出し、デバイスのリスクに基づいて Wi-Fi ネットワークへのアクセスを保護します。

*Wi-Fi 経由のネットワーク アクセスをブロックする:*

> [!div class="mx-imgBorder"]
> ![Wi-Fi 経由のネットワーク アクセスをブロックする](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*修復時に付与されるアクセス権:*

> [!div class="mx-imgBorder"]
> ![修復するとアクセス権が付与される](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいて SharePoint Online へのアクセスを制御する

ネットワークで **Man-in-the-middle** のような脅威を検出し、デバイスのリスクに基づいて会社内のファイルの同期を阻止します。

*ネットワークの脅威が検出されたときに SharePoint Online をブロック:*

> [!div class="mx-imgBorder"]
> ![ネットワークの脅威が検出されたときに SharePoint Online をブロック](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*修復時に付与されるアクセス権:*

> [!div class="mx-imgBorder"]
> ![SharePoint で修復時にアクセス権を付与する例](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいて登録されていないデバイスでアクセスを制御する

Zimperium Mobile Threat Defens ソリューションでデバイスが感染していると見なされる場合:

> [!div class="mx-imgBorder"]
> ![検出されたマルウェアによるアプリ保護ポリシーのブロック](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

修復するとアクセス権が付与されます。

> [!div class="mx-imgBorder"]
> ![アプリ保護ポリシーの修復時にアクセス権が付与される](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>次のステップ

- [Zimperium を Intune と統合する](zimperium-mtd-connector-integration.md)

- [Zimperium アプリを設定する](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Zimperium デバイス コンプライアンス ポリシーを作成する](mtd-device-compliance-policy-create.md)

- [Zimperium MTD コネクタを有効にする](mtd-connector-enable.md)

- [MTD アプリ保護ポリシーの作成](../protect/mtd-app-protection-policy.md)
