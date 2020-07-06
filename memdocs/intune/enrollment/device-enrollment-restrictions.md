---
title: Android Enterprise セキュリティ構成フレームワークのデバイス登録制限
titleSuffix: Microsoft Intune
description: Android Enterprise セキュリティ構成フレームワークのデバイス登録制限。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d26040c5a009a9c3877abbc25512e317f584f114
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502974"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Android Enterprise デバイスの登録制限

[Android Enterprise セキュリティ構成フレームワーク]()にデバイスを登録する前に、組織では適切な制限を構成する必要があります。 これらの制限によって、ユーザーが以下のみを登録できることが保証されます。
- 承認されたデバイス。
- 指定された数のデバイス。
- 指定されたプラットフォームのデバイス。
- 指定されたオペレーティング システムのデバイス。
- 指定されたメーカーのデバイス。

デバイスの登録制限について詳しくは、「[登録制限を設定する](enrollment-restrictions-set.md)」をご覧ください。

## <a name="work-profile-basic-level-1-security-restrictions"></a>仕事用プロファイルの基本 (レベル 1) セキュリティ制限

Android Enterprise 仕事用プロファイルの基本セキュリティ (レベル 1) では、次のデバイス制限を実装する必要があります。

| Type | プラットフォーム | バージョン | 個人デバイスを許可 |
|--------|--------|--------|--------|
| Android エンタープライズ | Allow | Android 5.0 以降。<p>Microsoft では、Microsoft アプリに対してサポートされている Android のバージョンと一致するように、Android の最小のメジャー バージョンを構成することを推奨しています。 OEM と Android Enterprise Recommended の要件に準拠しているデバイスでは、現在出荷されているリリースと 1 つ後のアップグレードをサポートしている必要があります。   現在、Android では、ナレッジ ワーカーに対して Android 8.0 とその後が推奨されています。 詳細については、「[Android Enterprise Recommended の要件](https://www.android.com/enterprise/recommended/requirements/)」を参照してください。 | はい |
| Android デバイス管理者| ブロックする | すべてのバージョン | はい |

## <a name="work-profile-high-level-3-security-restrictions"></a>仕事用プロファイルの高 (レベル 3) セキュリティ制限
Android Enterprise 仕事用プロファイルの高セキュリティ (レベル 3) では、次のデバイス制限を実装する必要があります。

| Type | プラットフォーム | バージョン | 個人デバイスを許可 |
|--------|--------|--------|--------|
| Android エンタープライズ | Allow | Android 8.0 以降 | はい |
| Android デバイス管理者| ブロックする | すべてのバージョン | はい |

## <a name="fully-managed-security-restrictions"></a>フル マネージド セキュリティ制限
Android Enterprise フル マネージド登録を見直して、組織で Android Enterprise フル マネージド デバイス登録がサポートされていることを確認します。 

## <a name="next-steps"></a>次のステップ

[アプリ構成ポリシーを設定する](android-app-configuration-policies.md)
