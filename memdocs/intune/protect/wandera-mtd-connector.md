---
title: Intune で Wandera モバイル セキュリティを設定する
titleSuffix: Intune on Azure
description: Microsoft Intune で Wandera モバイル セキュリティを設定し、会社のリソースに対するモバイル デバイスのアクセスを制御する方法。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/2/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1655c7b18262d0515308a00c617f06d917d976de
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972186"
---
# <a name="wandera-mobile-threat-defense-connector-with-intune"></a>Wandera Mobile Threat Defense コネクタと Intune  

Wandera によって実施されるリスク評価に基づく条件付きアクセスを使って、会社のリソースに対するモバイル デバイスのアクセスを制御します。 Wandera は、Microsoft Intune と統合されている Mobile Threat Defense (MTD) ソリューションです。  リスクは、Wandera サービスによりデバイスから収集される次のようなテレメトリに基づいて評価されます。
- オペレーティング システムの脆弱性
- インストールされた悪意のあるアプリ
- 悪意のあるネットワーク プロファイル
- クリプトジャッキング

Intune のデバイス コンプライアンス ポリシーを通じて有効にすることで、Wandera のリスク評価に基づく "*条件付きアクセス*" ポリシーを構成できます。 リスク評価ポリシーは、検出された脅威に基づき、非準拠デバイスの企業リソースへのアクセスを許可またはブロックすることができます。  

## <a name="how-do-intune-and-wandera-mobile-threat-defense-help-protect-your-company-resources"></a>Intune および Wandera Mobile Threat Defense が会社のリソースの保護に役立つしくみ  

Wandera のモバイル アプリは、Microsoft Intune を使用してシームレスにインストールされます。 このアプリにより、ファイル システム、ネットワーク スタック、デバイスとアプリケーションのテレメトリ (入手できる場合) がキャプチャされます。 この情報は Wandera のクラウド サービスと同期され、モバイルの脅威に対するデバイスのリスクが評価されます。 これらのリスク レベルの分類は、Wandera のコンソールである RADAR で、ご自身のニーズに合わせて構成できます。

Intune のコンプライアンス ポリシーには、Wandera のリスク評価に基づく MTD のルールが含まれています。 このルールを有効にすると、Intune は、有効にされたポリシーに基づいてデバイスの準拠状態を評価します。

非準拠のデバイスについては、Office 365 などのリソースへのアクセスをブロックできます。 ブロックされたデバイスを使っているユーザーには、問題を解決してアクセスを回復するためのガイダンスが Wandera アプリから届きます。

各デバイスの最新の脅威レベル (安全、低、中、高) が変更されるたびに、Wandera によって Intune がそのレベルで更新されます。 この脅威レベルは Wandera Security Cloud によって継続的に再計算されます。レベルは、デバイスの状態、ネットワークの活動、さまざまな脅威カテゴリにわたるさまざまなモバイル脅威インテリジェンス フィードに基づきます。

これらのカテゴリとそれに関連付けられている脅威レベルは Wandera の RADAR コンソールで構成できるため、デバイスごとに総計算される脅威レベルは、組織のセキュリティ要件に合わせてカスタマイズすることができます。 脅威レベルを把握しているとき、次の 2 種類の Intune ポリシーでこの情報を活用することで企業データへのアクセスが管理されます。

* 管理者は条件付きアクセスで**デバイス コンプライアンス ポリシー**を使用し、Wandera から報告された脅威レベルに基づいてマネージド デバイスに "コンプライアンス違反" のマークを自動的に付けるポリシーを設定します。 その後、このコンプライアンス フラグによって条件付きアクセス ポリシーが制御され、最新式の認証を利用するアプリケーションへのアクセスが許可されたり、拒否されたりします。  構成の詳細については、「[Intune で Mobile Threat Defense (MTD) デバイス コンプライアンス ポリシーを作成する](../protect/mtd-device-compliance-policy-create.md)」を参照してください。

* 管理者は条件付き起動で**アプリ保護ポリシー**を使用し、Wandera から報告された脅威レベルに基づき、ネイティブ アプリ レベル (たとえば、Outlook や OneDrive などの、Android や iOS または iPad OS のアプリ) で適用されるポリシーを設定できます。  これらのポリシーは、あらゆるデバイス プラットフォームと所有権モードでポリシーを統一する目的で、アンマネージド デバイス (MAM-WE) で使用されることもあります。 構成の詳細については、「[Intune で Mobile Threat Defense アプリ保護ポリシーを作成する](../protect/mtd-app-protection-policy.md)」を参照してください。

## <a name="supported-platforms"></a>サポートされているプラットフォーム  

Intune に登録したとき、Wandera では次のプラットフォームがサポートされます。

- Android 5.0 以降  
- iOS 10.2 以降 

プラットフォームとデバイスについて詳しくは、[Wandera の Web サイト](https://www.wandera.com/mobile-threat-defense/)をご覧ください。

## <a name="prerequisites"></a>[前提条件]  

- Microsoft Intune サブスクリプション  
- Azure Active Directory  
- Wandera Mobile Threat Defense (旧称 Wandera Secure)  

詳細については、[Wandera モバイル セキュリティ](https://www.wandera.com/mobile-security/)に関するページをご覧ください。
 
## <a name="sample-scenarios"></a>サンプル事例

Intune で Wandera MTD を使用する場合の一般的なシナリオを次に示します。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいてアクセスを制御する  

マルウェアなどの悪意のあるアプリがデバイス上で検出された場合、脅威を解決できるまで、デバイスでの一般的なツールの使用をブロックすることができます。 一般的なブロック対象には次が含まれます。  
- 会社の電子メールに接続する  
- OneDrive for Work アプリを使用して会社のファイルを同期する  
- 会社のアプリにアクセスする  

*悪意のあるアプリが検出されたときにブロックする*:

![検出された悪意のあるアプリの概念図](./media/wandera-mtd-connector/wandera-malicious-apps-blocked.png)  

*修復するとアクセス権が付与される*: 

![修復後に付与されたアクセス権の概念図](./media/wandera-mtd-connector/wandera-malicious-apps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいてアクセスを制御する  

中間者攻撃などのネットワークに対する脅威を検出し、デバイスのリスクに基づいて Wi-Fi ネットワークへのアクセスを保護します。  

*Wi-Fi 経由のネットワーク アクセスをブロックする*:  

![Wi-Fi 経由のネットワーク アクセスをブロックする](./media/wandera-mtd-connector/wandera-network-wifi-blocked.png)

*修復するとアクセス権が付与される*:  

![修復後に許可されるアクセス](./media/wandera-mtd-connector/wandera-network-wifi-unblocked.png)  

## <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークへの脅威に基づいて SharePoint Online へのアクセスを制御する

Man-in-the-middle 攻撃のようなネットワークの脅威を検出し、デバイス リスクに基づき、企業ファイルの同期を制限します。

*ネットワークの脅威が検出されたときに SharePoint Online をブロック*:  

![ネットワークの脅威が検出されたときに SharePoint Online をブロック](./media/wandera-mtd-connector/wandera-network-spo-blocked.png)  

*修復するとアクセス権が付与される*:  

![SharePoint で修復時にアクセス権が付与される例](./media/wandera-mtd-connector/wandera-network-spo-unblocked.png)  

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいて登録されていないデバイスでアクセスを制御する

Wandera Mobile Threat Defense ソリューションでデバイスが感染していると見なされる場合:

![検出されたマルウェアによるアプリ保護ポリシーのブロック](./media/wandera-mtd-connector/wandera-mobile-app-policy-block.png)

修復するとアクセス権が付与されます。

![アプリ保護ポリシーの修復時にアクセス権が付与される](./media/wandera-mtd-connector/wandera-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>次のステップ

- [Wandera を Intune と統合する](wandera-mtd-connector-integration.md)
- [Wandera アプリの設定](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Wandera デバイス コンプライアンス ポリシーの作成](mtd-device-compliance-policy-create.md)
- [Wandera MTD コネクタを有効にする](mtd-connector-enable.md)
