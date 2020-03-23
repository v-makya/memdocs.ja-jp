---
title: Intune で Mobile Threat Defense (MTD) アプリ保護ポリシーを作成する
titleSuffix: Microsoft Intune
description: Microsoft Intune で Mobile Threat Defense (MTD) アプリ保護ポリシーを作成する
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0fc25aa915762e0e1df9446c9fb14513bdf20352
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351566"
---
# <a name="create-mobile-threat-defense-app-protection-policy-with-intune"></a>Intune で Mobile Threat Defense アプリ保護ポリシーを作成する

Intune で Mobile Threat Defense (MTD) を使用すると、モバイル デバイス上で脅威を検出し、リスクを評価できます。 リスクを評価して、そのデバイスに企業データへのアクセスを許可するかどうかを判断する Intune アプリ保護ポリシーを作成できます。

> [!NOTE]
> この記事は、アプリ保護ポリシーをサポートするすべての Mobile Threat Defense パートナーに適用されます。
>
> - Better Mobile (Android、iOS/iPadOS)
> - Zimperium (Android、iOS/iPadOS)
> - Lookout for Work (Android、iOS/iPadOS)。

## <a name="before-you-begin"></a>始める前に

MTD の設定の一部として、MTD パートナー コンソールで、さまざまな脅威を高、中、低として分類するポリシーを作成しておきます。 これにより、Intune アプリ保護ポリシーに Mobile Threat Defense レベルを設定する必要があります。

MTD のアプリ保護ポリシーの前提条件:

- MTD と Intune の統合をセットアップします。 この統合がなければ、MTD アプリ保護ポリシーには効力がありません。

## <a name="to-create-an-mtd-app-protection-policy"></a>MTD アプリ保護ポリシーを作成するには

[iOS/iPadOS または Android 用のアプリケーション保護ポリシーを作成する](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps)ための手順に従い、 *[アプリ]* 、 *[条件付き起動]* 、 *[割り当て]* ページで次の情報を使用します。

- **[アプリ]** :アプリ保護ポリシーの対象とするアプリを選択します。 この機能セットでは、選択した Mobile Threat Defense ベンダーによるデバイスのリスク評価に基づいて、これらのアプリがブロックまたは選択的にワイプされます。
- **[条件付き起動]** : *[デバイスの条件]* の下で、ドロップダウン ボックスを使用して **[許容される最大デバイス脅威レベル]** を選択します。

  脅威レベルの **[値]** のオプション:

  - **[セキュリティ保護]** :このレベルはセキュリティ上最も安全です。 デバイスにいかなる脅威も存在できず、デバイスからは引き続き会社のリソースにアクセスできます。 いずれかの脅威が見つかった場合、デバイスは非準拠と評価されます。
  - **低**:存在する脅威が低レベルの場合のみ、デバイスは準拠しています。 低レベルより高い脅威が存在する場合、デバイスは非準拠状態になります。
  - **中**: デバイスに存在する脅威が低レベルまたは中レベルの場合、デバイスは準拠しています。 高レベルの脅威が検出された場合は、デバイスは非準拠と判定されます。
  - **高**: このレベルは最も安全性が低く、すべての脅威レベルが許可され、Mobile Threat Defense はレポート目的にのみ使用されます。 デバイスには、この設定でアクティブ化された MTD アプリが含まれている必要があります。

  **[アクション]** のオプション:

  - **[アクセスのブロック]**
  - **[データのワイプ]**

- **割り当て**:このポリシーをユーザーのグループに割り当てます。  Intune アプリ保護の対象アプリで企業データにアクセスすることについて、このグループのメンバーが使用するデバイスが評価されます。

## <a name="next-steps"></a>次のステップ

- Microsoft Intune の [Mobile Threat Defense](mobile-threat-defense.md) について学習します。
