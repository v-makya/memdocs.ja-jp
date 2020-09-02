---
title: デバイス登録マネージャー アカウントを使用してデバイスを登録する
titleSuffix: Microsoft Intune
description: デバイス登録マネージャー アカウントを使用してデバイスを Intune に登録します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f674cc7b0c7d7314c7152d530cff210319c568df
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913139"
---
# <a name="enroll-devices-in-intune-by-using-a-device-enrollment-manager-account"></a>デバイス登録マネージャー アカウントを使用してデバイスを Intune に登録する

デバイス登録マネージャー (DEM) アカウントを使用することで、1 つの Azure Active Directory アカウントで最大 1,000 台のモバイル デバイスを登録できます。 DEM は AAD ユーザー アカウントに適用できる Intune アクセス許可であり、ユーザーは最大 1,000 台のデバイスを登録できます。 DEM アカウントは、デバイスのユーザーに渡される前にデバイスの登録と準備を行うシナリオで役立ちます。 設計上、Microsoft Intune では、デバイス登録マネージャー (DEM) アカウントは 150 個までに制限されています。

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>DEM アカウントで登録されるデバイスの制限事項

DEM ユーザー アカウントと DEM ユーザー アカウントを使用して登録されているデバイスには、次の制限があります。

- DEM アカウントのユーザーには、Intune ライセンスを割り当てる必要があります。
- ポータル サイトからはワイプできません。 DEM ユーザー アカウントで登録されたデバイスは、Azure portal で Intune からワイプできます。
- ポータル サイト アプリまたは Web サイトには、ローカルのデバイスのみが表示されます。
- アプリ管理のための Apple ID 要件がユーザー単位になるため、DEM ユーザー アカウントでは Apple ID ユーザー ライセンスで Apple Volume Purchase Program (VPP) アプリを利用することはできません。
- Apple の自動デバイス登録 (ADE) を使用してデバイスを登録するときに、DEM アカウントを使用することはできません。
- デバイスでは、Apple ID デバイス ライセンスがある場合に VPP アプリをインストールすることができます。
- Windows 10 1803+ 以降の例外と共にデバイスが条件付きアクセスをブロックされます
- DEM アカウントに登録されているすべてのデバイスを Intune で管理するには、適切にライセンスする必要があります。 ライセンスは、Intune ユーザー ライセンスまたは Intune デバイス ライセンスにすることができます。
- DEM アカウントを使用して [Android Enterprise 仕事用プロファイル デバイスを登録](android-work-profile-enroll.md)する場合、アカウントあたりの登録可能なデバイスは 10 台に制限されます。
- DEM アカウントを使用した [Android Enterprise フル マネージド デバイスの登録](android-fully-managed-enroll.md)はサポートされていません。
- Azure AD デバイスの制限を DEM アカウントに適用すると、DEM アカウントが登録できるデバイス数の上限である 1,000 に到達しなくなります。

## <a name="enrollment-methods-supported-by-dem-accounts"></a>DEM アカウントでサポートされている登録方法

DEM アカウントを使用してデバイスを登録する場合、次の方法を使用できます。

- [Windows Autopilot](../../autopilot/enrollment-autopilot.md)
- [Windows デバイスの一括登録](windows-bulk-enroll.md)
- ポータル サイトから DEM が開始

## <a name="add-a-device-enrollment-manager"></a>デバイス登録マネージャーの追加

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインし、 **[デバイス]**  >  **[デバイスの登録]**  >  **[デバイス登録マネージャー]** を選択します。

2. **[追加]** を選択します。

3. **[ユーザーの追加]** ブレードで、DEM ユーザーのユーザー プリンシパル名を入力し、 **[追加]** を選択します。 DEM ユーザーが DEM ユーザーの一覧に追加されます。

## <a name="permissions-required-to-create-dem-accounts"></a>DEM アカウントを作成するために必要なアクセス許可

次のために、グローバル管理者または Intune サービス管理者の Azure AD ロールが必要です。
- Azure AD ユーザー アカウントに DEM アクセス許可を割り当てる
- すべての DEM ユーザーを表示する

ユーザーにグローバル管理者または Intune サービス管理者のロールが割り当てられていないが、デバイス登録マネージャー ロールが割り当てられていてその読み取りアクセス許可を持っているという場合は、そのユーザー自身が作成した DEM ユーザーのみを表示できます。

## <a name="remove-device-enrollment-manager-permissions"></a>デバイス登録マネージャーのアクセス許可の削除

デバイス登録マネージャーを削除しても、登録済みのデバイスに影響はありません。

**デバイス登録マネージャーを削除するには**

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインし、 **[デバイス]**  >  **[デバイスの登録]**  >  **[デバイス登録マネージャー]** を選択します。
2. **[デバイス登録マネージャー]** ブレードで、DEM ユーザーを選択し、 **[削除]** を選択します。