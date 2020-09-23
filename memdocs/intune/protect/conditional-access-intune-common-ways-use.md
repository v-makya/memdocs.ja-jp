---
title: 条件付きアクセスのシナリオ
titleSuffix: Microsoft Intune
description: デバイスベースおよびアプリベースの条件付きアクセスで、Intune の条件付きアクセスが一般的にどのように使用されるかについて説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0b8e55e-c3d8-4599-be25-dc10c1027b62
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d062af4859dcca6c762bf401e1007a9fc9af126
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002666"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>Intune での条件付きアクセスの一般的な使用方法

Intune での条件付きアクセスには、デバイス ベースの条件付きアクセスとアプリ ベースの条件付きアクセスの 2 種類があります。 組織の条件付きアクセス コンプライアンスを進めるために関連するコンプライアンス ポリシーを構成する必要があります。 条件付きアクセスは、一般的に Exchange へのアクセスの許可またはブロック、ネットワークへのアクセスの制御、Mobile Threat Defense ソリューションとの統合などを行うために使用されます。
 
この記事は、Intune のモバイル "*デバイス*" のコンプライアンス機能と Intune のモバイル "*アプリケーション*" 管理 (MAM) 機能の使用方法を理解するのに役立ちます。 

> [!NOTE]
> 条件付きアクセスは、Azure Active Directory Premium ライセンスに含まれる Azure Active Directory の機能です。 Intune は、モバイル デバイス コンプライアンスとモバイル アプリ管理をソリューションに加えて、この機能を強化します。 *Intune* からアクセスされる条件付きアクセス ノードは、*Azure AD* からアクセスされるノードと同じです。  

## <a name="device-based-conditional-access"></a>デバイスベースの条件付きアクセス

Intune と Azure Active Directory が連携すると、マネージド デバイスと準拠しているデバイスのみが電子メール、Microsoft 365 サービス、サービスとしてのソフトウェア (SaaS) アプリ、および[オンプレミス アプリ](/azure/active-directory/active-directory-application-proxy-get-started)にアクセスできるようになります。 また、ドメインに参加しているコンピューターまたは Intune に登録されているモバイル デバイスのみが Microsoft 365 サービスにアクセスできるように、Azure Active Directory 内にポリシーを設定できます。

Intune には、デバイスのコンプライアンス対応状態を評価する、デバイス コンプライアンス ポリシーの機能があります。 コンプライアンス対応状態は Azure Active Directory に報告され、ユーザーが会社のリソースにアクセスしようとしたときに、Azure Active Directory で作成された条件付きアクセスのポリシーを適用するために使用されます。

Exchange Online や他の Microsoft 365 製品のデバイスベースの条件付きアクセス ポリシーは、[Azure portal](../fundamentals/what-is-intune.md) で構成します。

- Azure Active Directory で条件付きアクセスを使用するサポートされるブラウザーについては、[こちら](/azure/active-directory/conditional-access/require-managed-devices)を参照してください。

- Intune のデバイス コンプライアンスの詳細については、[こちら](device-compliance-get-started.md)を参照してください。

- Azure Active Directory の条件付きアクセスでサポートされるブラウザーについては、[こちら](/azure/active-directory/conditional-access/technical-reference#supported-browsers)を参照してください。

> [!NOTE]
> Android デバイスでは、SharePoint Online に対するデバイスベースのアクセスまたは Exchange Online に対するブラウザーベースのアクセスが有効な場合、ユーザーは登録されたデバイスで次のように **[ブラウザー アクセスを有効にする]** オプションを有効にする必要があります。
> 1. **ポータル サイト アプリ**を起動します。
> 2. トリプル ドット (...) またはハードウェアのメニュー ボタンから、 **[設定]** ページに移動します。
> 3. **[ブラウザー アクセスを有効にする]** ボタンを押します。 
> 4. Chrome ブラウザーでは、Microsoft 365 からサインアウトし、Chrome を再起動します。

### <a name="conditional-access-based-on-network-access-control"></a>ネットワーク アクセス制御に基づいた条件付きアクセス

Intune は Cisco ISE、Aruba Clear Pass、Citrix NetScaler などのパートナーと統合され、Intune 登録とデバイスのコンプライアンス対応状態に基づいたアクセス制御が提供されます。

ユーザーは、使用しているデバイスが管理され、Intune デバイス コンプライアンス ポリシーに準拠しているかどうかに基づいて、会社の Wi-Fi や VPN リソースへのアクセスを許可または拒否されます。

- NAC と Intune の統合について詳しくは、[こちら](network-access-control-integrate.md)をご覧ください。

### <a name="conditional-access-based-on-device-risk"></a>デバイスのリスクに基づいた条件付きアクセス

Intune は、モバイル デバイス上のマルウェア、トロイの木馬、およびその他の脅威を検出するためのセキュリティ ソリューションを提供する Mobile Threat Defense ベンダーと提携しました。

#### <a name="how-the-intune-and-mobile-threat-defense-integration-works"></a>Intune と Mobile Threat Defense の統合のしくみ

モバイル デバイスに Mobile Threat Defense エージェントがインストールされている場合、モバイル デバイスで脅威が検出されると、コンプライアンス対応状態のメッセージがエージェントから Intune に返されます。

Intune と Mobile Threat Defense の統合は、デバイスのリスクに基づいた条件付きアクセスの決定において重要な役割を果たします。

- Intune Mobile Threat Defense について詳しくは、[こちら](mobile-threat-defense.md)をご覧ください。

### <a name="conditional-access-for-windows-pcs"></a>Windows PC の条件付きアクセス

PC の条件付きアクセスでは、モバイル デバイスで利用できる機能と同様の機能が提供されます。 Intune で PC を管理する場合に条件付きアクセスを使用する方法について説明します。

#### <a name="corporate-owned"></a>企業所有

- **ハイブリッド Azure AD 参加済み:** この方法は、AD のグループ ポリシーや Configuration Manager を使用して PC を管理している現在のやり方におおむね満足している組織でよく使用されます。

- **Azure AD ドメインへの参加と Intune の管理:** このシナリオは、クラウドファーストにすることを望んでいる (つまり、主にクラウド サービスを使用し、オンプレミスのインフラストラクチャの使用を減らすことを目標としている) 組織や、クラウドのみを使用する (オンプレミスのインフラストラクチャがない) 組織向けです。 Azure AD への参加はハイブリッド環境で適切に機能し、クラウドとオンプレミスのアプリとリソースの両方にアクセスできるようにします。 Azure AD に参加したデバイスは Intune に登録されます。会社のリソースにアクセスするときに、これを条件付きアクセスの基準として使用できます。

#### <a name="bring-your-own-device-byod"></a>Bring Your Own Device (BYOD)

- **Workplace Join と Intune 管理:** この場合、ユーザーは個人のデバイスを参加させて、会社のリソースやサービスにアクセスできます。 Workplace Join を使用してデバイスを Intune MDM に登録し、デバイスレベルのポリシーを受け取ることができます。これは、条件付きアクセスの基準を評価する別のオプションです。

Azure Active Directory のデバイス管理の詳細については、[こちら](/azure/active-directory/devices/overview)を参照してください。

## <a name="app-based-conditional-access"></a>アプリベースの条件付きアクセス

Intune と Azure Active Directory が連携すると、管理対象アプリのみが会社の電子メールやその他の Microsoft 365 サービスにアクセスできるようになります。

- Intune を使用したアプリ ベースの条件付きアクセスについて詳しくは、[こちら](app-based-conditional-access-intune.md)をご覧ください。

### <a name="intune-conditional-access-for-exchange-on-premises"></a>Exchange On-Premises での Intune 条件付きアクセス

条件付きアクセスを使用すると、デバイス コンプライアンス ポリシーと登録状態に基づいて、**Exchange On-Premises** へのアクセスを許可またはブロックすることができます。 条件付きアクセスをデバイス コンプライアンス ポリシーと組み合わせて使用した場合は、準拠デバイスのみが Exchange On-Premises へのアクセスを許可されます。

条件付きアクセスの詳細設定を構成して、次のような細かい制御を行うことができます。

- 特定のプラットフォームを許可またはブロックする。

- Intune で管理されていないデバイスを即時ブロックする。

デバイス コンプライアンスと条件付きアクセス ポリシーが適用されると、Exchange On-Premises へのアクセスで使用されるデバイスがチェックされます。

デバイスが条件を満たしていない場合、エンド ユーザーは、デバイス非準拠の原因である問題を修正するためのデバイス登録プロセスを提示されます。

> [!NOTE]
> 2020 年 7 月以降、Exchange Connector のサポートは非推奨とされ、Exchange の[ハイブリッド先進認証](/office365/enterprise/hybrid-modern-auth-overview) (HMA) に置き換えられます。 HMA を使用する場合、Intune をセットアップして Exchange Connector を使用する必要はありません。 サブスクリプションで Exchange Connector を既に使用していない限り、Intune の Exchange Connector を構成および管理するための UI は、この変更により Microsoft エンドポイント マネージャー管理センターから削除されています。
>
> ご使用の環境に Exchange Connector が設定されている場合、Intune テナントの使用は引き続きサポートされ、その構成をサポートする UI に引き続きアクセスできます。 詳細については、[Exchange On-Premises Connector のインストール](../protect/exchange-connector-install.md)に関する記事を参照してください。 引き続きコネクタを使用するか、HMA を構成してから、コネクタをアンインストールすることができます。
>
> ハイブリッド先進認証は、以前に Intune の Exchange Connector によって提供されていた機能であるデバイス ID の Exchange レコードへのマッピングを備えています。  このマッピングは、Intune で行った構成、または Intune と Exchange をブリッジする Intune コネクタの要件の外部で行われるようになりました。 HMA では、"Intune" 固有の構成 (コネクタ) を使用するための要件が削除されています。


<!-- Deprecated with change from the connector to Exchange hybrid modern authentication)

#### How conditional access for Exchange on-premises works

Conditional access for Exchange on-premises works differently than Azure Conditional Access based policies. You install the Intune Exchange on-premises connector to directly interact with Exchange server. The Intune Exchange connector pulls in all the Exchange Active Sync (EAS) records that exist at the Exchange server so Intune can take these EAS records and map them to Intune device records. These records are devices enrolled and recognized by Intune. This process allows or blocks e-mail access.

If the EAS record is new and Intune isn't aware of it, Intune issues a cmdlet (pronounced "command-let") that directs the Exchange server to block access to e-mail. Following are more details on how this process works:

![Exchange on-premises with CA flow-chart](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. User tries to access corporate email, which is hosted on Exchange on-premises 2010 SP1 or later.

2. If the device is not managed by Intune, access to email will be blocked. Intune sends a block notification to the EAS client.

3. EAS receives the block notification, moves the device to quarantine, and sends the quarantine email with remediation steps that contain links so the users can enroll their devices.

4. The Workplace join process happens, which is the first step to have the device managed by Intune.

5. The device gets enrolled into Intune.

6. Intune maps the EAS record to a device record, and saves the device compliance state.

7. The EAS client ID gets registered by the Azure AD Device Registration process, which creates a relationship between the Intune device record, and the EAS client ID.

8. The Azure AD Device Registration saves the device state information.

9. If the user meets the conditional access policies, Intune issues a cmdlet through the Intune Exchange connector that allows the mailbox to sync.

10. Exchange server sends the notification to EAS client so the user can access e-mail.
-->

#### <a name="whats-the-intune-role"></a>Intune ロールとは

Intune はデバイスの状態を評価し、管理します。

#### <a name="whats-the-exchange-server-role"></a>Exchange サーバー ロールとは

Exchange サーバーでは、デバイスを検疫に移動するための API とインフラストラクチャを提供しています。

> [!IMPORTANT]
> デバイスのコンプライアンスを評価できるようにするために、デバイスを使用するユーザーにコンプライアンス プロファイルと Intune ライセンスを割り当てる必要がある点に注意してください。 コンプライアンス ポリシーがユーザーに展開されていない場合、デバイスは準拠したものと見なされ、アクセス制限は適用されません。

## <a name="next-steps"></a>次のステップ

[Azure Active Directory で条件付きアクセスを構成する方法](/azure/active-directory/active-directory-conditional-access-azure-portal)

[アプリベースの条件付きアクセス ポリシーを設定する](app-based-conditional-access-intune-create.md)

[Exchange On-Premises の条件付きアクセス ポリシーを作成する方法](conditional-access-exchange-create.md)
