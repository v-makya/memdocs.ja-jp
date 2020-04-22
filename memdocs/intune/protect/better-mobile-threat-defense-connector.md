---
title: Better Mobile Threat Defense コネクタと Intune
titleSuffix: Intune on Azure
description: Better Mobile Threat Defense コネクタを Intune で設定します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79353984"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Better Mobile Threat Defense コネクタと Intune

Microsoft Intune に統合された Mobile Threat Defense (MTD) ソリューションである Better Mobile によって実行されるリスク評価に基づき、条件付きアクセスを利用し、モバイル デバイスから会社のリソースへのアクセスを制御できます。 リスクは、Better Mobile アプリを実行するデバイスから収集される製品利用統計情報に基づいて評価されます。

Intune デバイス コンプライアンス ポリシーで有効にした Better Mobile リスク評価に基づき、条件付きアクセスのポリシーを構成できます。登録済みデバイスの Intune デバイス コンプライアンス ポリシーは、検出された脅威に基づき、非準拠デバイスから企業リソースへのアクセスを許可したり、拒否したりするために利用できます。 登録されていないデバイスの場合、アプリ保護ポリシーを使用して、検出された脅威に基づいてブロックまたは選択的ワイプを強制することができます。

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Intune と Better Mobile が会社のリソースを保護する方法

Better Mobile のアプリは、モバイル デバイスにインストールされ、実行されます。 このアプリは、利用できる場合、ファイル システム、ネットワーク スタック、デバイスとアプリケーションの製品利用統計情報を記録し、Better Mobile クラウド サービスにデータを送信し、モバイル デバイスの脅威に対するリスクを評価します。

- **登録済みデバイスのサポート** - Intune デバイス コンプライアンス ポリシーには Mobile Threat Defense (MTD) 用のルールが含まれ、そこでは Better Mobile からのリスク評価情報を使用できます。 MTD ルールを有効にすると、Intune では、有効にされたポリシーに基づいてデバイスの準拠状態が評価されます。 デバイスが準拠していないことが判明した場合、ユーザーは Exchange Online や SharePoint Online などの会社リソースへのアクセスをブロックされます。 また、ユーザーは、デバイスにインストールされている Better Mobile アプリから、問題を解決して会社リソースへのアクセスを回復するための案内を受け取ります。 登録されたデバイスで Better Mobile の使用をサポートするには:
  - [デバイスに MTD アプリを追加する](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [MTD をサポートするデバイス コンプライアンス ポリシーを作成する](../protect/mtd-device-compliance-policy-create.md)
  - [Intune で MTD コネクタを有効にする](../protect/mtd-connector-enable.md)

- **登録されていないデバイスのサポート** - Intune では、Intune アプリ保護ポリシーを使用すると、登録されていないデバイスで Better Mobile アプリからのリスク評価データを使用できます。 管理者は、この組み合わせを使用して、[Microsoft Intune の保護されたアプリ](../apps/apps-supported-intune-apps.md)内の企業データを保護することができ、それらの登録されていないデバイス上の企業データに対してブロックまたは選択的ワイプを発行することもできます。 登録されていないデバイスで Better Mobile の使用をサポートするには:
  - [登録されていないデバイスに MTD アプリを追加する](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Mobile Threat Defense アプリ保護ポリシーを作成する](../protect/mtd-app-protection-policy.md)
  - [登録されていないデバイスに対して Intune で MTD コネクタを有効にする](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>サポートされているプラットフォーム

- **Android 4.1 以降**

- **iOS 8.0 以降**

## <a name="prerequisites"></a>[前提条件]

- Azure Active Directory Premium

- Microsoft Intune サブスクリプション

- Better Mobile Threat Defense サブスクリプション

  - 詳細については、[Better Mobile の Web サイト](https://www.better.mobi/)を参照してください。

## <a name="sample-scenarios"></a>サンプル事例

一般的なシナリオを次に示します。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいてアクセスを制御する

マルウェアなどの悪意のあるアプリがデバイスで検出されると、脅威が解決されるまで、デバイスで次の行為が禁止されます。

- 会社の電子メールに接続する

- OneDrive for Work アプリを使用して会社のファイルを同期する

- 会社のアプリにアクセスする

悪意のあるアプリが検出されたときにブロックする:

![検出された悪意のあるアプリを示す画像](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

修復するとアクセス権が付与されます。

![悪意のあるアプリの検出、アクセス権](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいてアクセスを制御する

**Man-in-the-middle** 攻撃など、ネットワークに対する脅威を検出し、デバイスのリスクに基づいて Wi-Fi ネットワークへのアクセスを保護します。

Wi-Fi 経由のネットワーク アクセスをブロックする:

![Wi-Fi 経由のネットワーク アクセスをブロックする](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

修復するとアクセス権が付与されます。

![修復時にアクセス権が付与されたことを示す画像](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークへの脅威に基づいて SharePoint Online へのアクセスを制御する

**Man-in-the-middle** 攻撃など、ネットワークに対する脅威を検出し、デバイスのリスクに基づいて会社内のファイルの同期を阻止します。

ネットワークの脅威が検出されたときに SharePoint Online をブロック:

![ネットワークの脅威が検出されたときに SharePoint Online をブロック](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

修復時に付与されるアクセス権:

![SharePoint で修復時にアクセス権を付与する例](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいて登録されていないデバイスでアクセスを制御する

BETTER Mobile Threat Defens ソリューションでデバイスが感染していると見なされる場合:![検出されたマルウェアによるアプリ保護ポリシーのブロック](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

修復するとアクセス権が付与されます。

![アプリ保護ポリシーの修復時にアクセス権が付与される](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>次のステップ

- [Better Mobile と Intune を統合する](better-mobile-mtd-connector-integration.md)

- [Better Mobile アプリを設定する](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Better Mobile デバイスのコンプライアンス ポリシーを作成する](mtd-device-compliance-policy-create.md)

- [Better Mobile MTD コネクタを有効にする](mtd-connector-enable.md)

- [MTD アプリ保護ポリシーの作成](mtd-app-protection-policy.md) 
