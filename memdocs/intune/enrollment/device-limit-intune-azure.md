---
title: Intune と Azure のデバイスの上限数の制限の違いを理解する
titleSuffix: ''
description: Intune のデバイスの上限数の制限と Azure AD のデバイスの上限数の制限の違いを理解します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8610b619a4ac05f37b893060b3b3a2bcb1dae528
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864856"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Intune と Azure AD のデバイスの上限数の制限を理解する

デバイスの上限数の制限は、次の 2 つの方法で構成できます。
- Intune の登録
- Azure Active Directory (AD) に参加させるか、Azure AD に登録する

この記事では、ご自分の構成に基づいてこれらの制限が適用されるタイミングを明確にします。

## <a name="intune-device-limit-restrictions"></a>Intune のデバイスの上限数の制限

Intune のデバイスの上限数の制限では、1 人のユーザーが制御できるデバイスの最大数を設定します (最大設定値は 15)。 この **[デバイスの上限数]** を設定するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[登録制限]** の順に移動します。 詳細については、「[デバイスの上限数の制限を作成する](enrollment-restrictions-set.md#create-a-device-limit-restriction)」を参照してください

## <a name="azure-device-limit-restriction"></a>Azure のデバイスの上限数の制限

Azure のデバイスの上限数の制限では、Azure AD に参加させるか Azure AD に登録するデバイスの最大数を設定します。 **[ユーザーごとのデバイスの最大数]** を設定するには、Azure portal > **[Azure Active Directory]**  >  **[デバイス]** に移動します。 詳しくは、[デバイス設定の構成](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal)に関するページを参照してください

## <a name="settings-applied-based-on-user-affinity"></a>ユーザー アフィニティに基づいて適用される設定

Intune と Azure の両方のデバイスの上限数の制限を設定している場合にユーザー アフィニティ設定に基づいて適用される内容を次の表に示します。

| デバイスのプラットフォーム | ユーザー アフィニティ | Azure の適用 | Intune の適用 |
| ----- | ----- | ----- | ----- | ----- |
| Android Enterprise 仕事用プロファイル | はい | はい | はい|
| Android Enterprise 専用デバイス | いいえ | いいえ | いいえ |
| Android Enterprise のフル マネージド | はい | はい | はい |
| Android デバイス管理者 | はい | はい | はい |
| Android デバイス管理者の DEM | いいえ | | いいえ | 
| iOS/macOS の BYOD | はい | はい | はい |
| iOS/macOS の自動デバイス登録 (ADE) | はい | はい | はい |
| iOS/macOS の ADE | いいえ | はい | いいえ |
| Windows の BYOD | はい | はい | はい |
| Windows の MD のみ | | はい | はい |
| Azure AD 参加済みの Windows| はい | はい | いいえ |
| Windows Autopilot | はい | はい | いいえ |
| Hybrid Azure AD Join を使用した Windows | いいえ | いいえ | はい |
| Windows の共同管理 | いいえ | はい | いいえ |
| Windows の DEM | いいえ | はい | いいえ |
| Windows の一括登録 | いいえ | はい | いいえ |


## <a name="android-and-ios-devices"></a>Android および iOS のデバイス

### <a name="ios-or-android-devices-example-1"></a>iOS または Android デバイスの例 1

- Azure の **[ユーザーごとのデバイスの最大数]** 設定は 3 に設定されています。
- Intune の **[デバイスの上限数]** 設定は 5 に設定されています。
 
**結果:** 最大数はユーザー単位です。 たとえば、3 台の Intune デバイスを登録した場合、デバイスの登録数を制限する設定が原因で、4 台目のデバイスの Azure 登録が失敗します。

### <a name="ios-or-android-devices-example-2"></a>iOS または Android デバイスの例 2

- Azure の **[ユーザーごとのデバイスの最大数]** 設定は 20 に設定されています。
- Intune の **[デバイスの上限数]** 設定は 2 に設定されています。

**結果:** 2 台のデバイスを正常に AD と Intune に登録できます。 追加のデバイスに対する Intune の登録はブロックされます。 ユーザー アフィニティなしの ADE は、Azure のデバイス登録の上限がユーザーに関連付けられていない場合でもその上限によって制限されます。

## <a name="windows-devices"></a>Windows デバイス

Intune のデバイスの上限数の制限は、次の Windows の登録の種類に適用されません。
- 共同管理登録
- グループ ポリシー オブジェクト (GPO) の登録
- Azure AD 参加済み登録
- Azure AD 参加済み一括登録
- Autopilot 登録
- デバイス登録マネージャー登録

これらの登録の種類は共有デバイス シナリオと見なされるため、これらにデバイスの上限数の制限を適用できません。 これらの登録の種類に対するハード制限を Azure Active Directory に設定できます。

Azure のデバイスの上限数の制限については、 **[ユーザーごとのデバイスの最大数]** の設定が、Azure AD 参加済みまたは Azure AD に登録済みのデバイスに適用されます。 この設定は、Hybrid Azure AD Join を使用したデバイスには適用されません。

### <a name="windows-10-example-1"></a>Windows 10 の例 1

- Azure の **[ユーザーごとのデバイスの最大数]** 設定は 5 に設定されています。
- Intune の **[デバイスの上限数]** 設定は 3 に設定されています。
- デバイスは自動的に Hybrid Azure AD Join が使用され、登録されています (GPO 構成済み)。

**結果:** 登録は GPO を介してプッシュされるため、Azure のデバイス登録の上限は適用されません。  Intune のデバイスの上限数の制限も適用されません。

### <a name="windows-10-example-2"></a>Windows 10 の例 2

- Azure の **[ユーザーごとのデバイスの最大数]** 設定は 5 に設定されています。
- Intune の **[デバイスの上限数]** 設定は 2 に設定されています。
- デバイスは、 **[設定]**  >  **[職場または学校へのアクセス]**  >  **[接続]** を使用して、ローカル ドメイン参加済みであり、登録されています。

**結果:** ブロックされる前に Intune に登録できるのは、2 台のデバイスのみです。 最大 5 台のデバイスを AD に登録できます。


## <a name="next-steps"></a>次のステップ

- [Azure でデバイスの上限数の制限を作成する。](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Azure でデバイス設定を構成する。](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [登録とドメイン参加済みの詳細について確認する。](https://docs.microsoft.com/azure/active-directory/devices/overview#getting-devices-in-azure-ad)
