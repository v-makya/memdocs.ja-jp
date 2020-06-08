---
title: Microsoft Intune でエンドポイント セキュリティ ポリシーを使用してウイルス対策設定を管理する | Microsoft Docs
description: Microsoft Endpoint Manager でエンドポイント セキュリティのウイルス対策ポリシーを使用して、管理するデバイスのポリシーを構成および展開し、レポートを使用します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 2f3a378cdb3b5e24371edb2fd6dc240962f80342
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431905"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのウイルス対策ポリシー

Intune エンドポイント セキュリティのウイルス対策ポリシーは、セキュリティ管理者がマネージド デバイスのウイルス対策設定の個別のグループを管理することに注力するのに役立ちます。 ウイルス対策ポリシーを使用するには、Intune と Microsoft Defender Advanced Threat Protection (Defender ATP) を Mobile Threat Defense ソリューションとして統合します。

ウイルス対策ポリシーには、複数のプロファイルが含まれます。 それぞれのプロファイルには、macOS および Windows 10 用の Defender ATP ウイルス対策に適した設定、または Windows 10 デバイス上の Windows セキュリティ アプリのユーザー エクスペリエンス用の設定のみが含まれます。

ウイルス対策ポリシーは、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) のエンドポイント セキュリティ ノードの **[管理]** にあります。

ウイルス対策ポリシーには、[デバイスの構成](../configuration/device-profile-create.md)ポリシーの*エンドポイント保護*プロファイルまたは*デバイスの制限*プロファイルにあり、[デバイス コンプライアンス](../protect/device-compliance-get-started.md) ポリシーの設定に類似した設定と同じものが含まれています。 ただし、これらのポリシーの種類には、ウイルス対策に関連しない設定の追加カテゴリが含まれます。 追加設定のために、ウイルス対策を構成するタスクが複雑になることがあります。 また、macOS のウイルス対策ポリシーにある設定は、他のポリシーの種類では使用できません。 macOS ウイルス対策プロファイルを使用すると、`.plist` ファイルを使用して設定を構成する必要がなくなります。

## <a name="prerequisites-for-antivirus-policy"></a>ウイルス対策ポリシーの前提条件

- **macOS**
  - サポートされているバージョンの macOS
  - Intune でデバイスのウイルス対策設定を管理するには、そのデバイスに Defender ATP がインストールされている必要があります。 See. (Defender ATP のドキュメントの) [macOS 用の Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) に関するページをご覧ください

- **Windows 10 以降**
  - Intune でデバイスのウイルス対策設定を管理するには、そのデバイスに Defender ATP がインストールされている必要があります。 Intune ドキュメントの [Windows 用の Microsoft Defender ATP](../protect/advanced-threat-protection.md) に関するページをご覧ください。
  - Windows セキュリティ アプリは、Windows 10 を実行しているすべてのデバイスにインストールされており、追加の前提条件は必要ありません。

## <a name="antivirus-profiles"></a>ウイルス対策プロファイル

**macOS プロファイル**:

- **ウイルス対策** - macOS 用の[ウイルス対策ポリシー設定](../protect/antivirus-microsoft-defender-settings-macos.md)を管理します。

  [Microsoft Defender ATP for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) を使用する場合は、`.plist` ファイルを使用してこれらの設定を構成する代わりに、Intune からウイルス対策設定を構成し、管理対象の macOS デバイスに展開することができます。

**Windows 10 プロファイル**:

- **Microsoft Defender ウイルス対策** - Windows 10 用の[ウイルス対策ポリシーの設定](../protect/antivirus-microsoft-defender-settings-windows.md)を管理します。

  Defender ウイルス対策は、Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) の次世代保護コンポーネントです。 次世代保護では、機械学習、ビッグデータ分析、脅威への耐性に関する詳細な研究、クラウド インフラストラクチャを組み合わせることにより、企業組織内のデバイスを保護します。

  *Microsoft Defender ウイルス対策*プロファイルは、デバイス構成ポリシーの*デバイス制限プロファイル*にあるウイルス対策設定の別のインスタンスです。
  
  *デバイス制限プロファイル*のウイルス対策設定とは異なり、これらの設定は、共同管理されているデバイスで使用できます。 これらの設定を使用するには、Endpoint Protection の[共同管理ワークロードのスライダー](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)が Intune に設定されている必要があります。

- **Windows セキュリティ エクスペリエンス** - エンド ユーザーが Microsoft Defender セキュリティ センターで表示できる [Windows セキュリティ アプリ設定](../protect/antivirus-security-experience-windows-settings.md)と、エンド ユーザーが受信する通知を管理します。 Windows セキュリティ アプリは、コンピューターの正常性とセキュリティに関する通知を提供するために、多くの Windows セキュリティ機能で使用されます。 セキュリティ アプリの通知には、ファイアウォール、ウイルス対策製品、Windows Defender SmartScreen などが含まれます。

## <a name="antivirus-policy-reports"></a>ウイルス対策ポリシー レポート

ウイルス対策ポリシーレポートには、エンドポイント セキュリティのウイルス対策ポリシーとデバイスの状態に関する状態の詳細が表示されます。 これらのレポートは、Microsoft Endpoint Manager admin center のエンドポイント セキュリティ ノードで使用できます。

レポートを表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) でエンドポイント セキュリティに移動して **[ウイルス対策]** を選択します。 [ウイルス対策] を選択すると、[概要] ページが開きます。 追加のレポート ビューと状態ビューは、追加のページとして使用できます。

### <a name="summary"></a>[概要]

**[概要]** ページでは、[新しいポリシーを作成](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)し、以前に作成したポリシーの一覧を表示できます。 この一覧には、ポリシーに含まれるプロファイルに関する高度な詳細概要 (ポリシーの種類) と、ポリシーが割り当てられているかどうかが表示されます。

![ウイルス対策ポリシーの [概要] ページ](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

一覧からポリシーを選択すると、そのポリシー インスタンスの *[概要]* ページが開き、詳細情報が表示されます。 このビューからタイルを選択すると、そのプロファイルのその他の詳細が使用可能な場合は、Intune にその詳細が表示されます。

![ウイルス対策ポリシーの [概要] ページ](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Windows 10 の異常なエンドポイント

**[Windows 10 の異常なエンドポイント]** ページでは、MDM で管理されている Windows 10 デバイスのウイルス対策の状態に関する情報を表示できます。 この情報は、デバイスで実行されている Windows Defender ウイルス対策から、*脅威エージェントの状態*として返されます。

問題が検出されたデバイスのみが、このビューに表示されます。 このビューには、クリーンと識別されたデバイスの詳細は表示されません。

![ウイルス対策ポリシーの [概要] ページ](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>次のステップ

[エンドポイント セキュリティ ポリシーを構成する](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
