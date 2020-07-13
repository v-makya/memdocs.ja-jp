---
title: Android Enterprise セキュリティ構成フレームワークのデバイス登録制限
titleSuffix: Microsoft Intune
description: Android Enterprise セキュリティ構成フレームワークのデバイス登録制限。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/02/2020
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
ms.openlocfilehash: 6629f416dbbc9555514dfc305db8f224f6b76526
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088447"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Android Enterprise デバイスの登録制限

[Android Enterprise セキュリティ構成フレームワーク](android-configuration-framework.md)にデバイスを登録する前に、組織では適切な制限を構成する必要があります。 これらの制限によって、ユーザーが以下のみを登録できることが保証されます。

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
「[フル マネージド デバイスを登録する](android-fully-managed-enroll.md#enroll-the-fully-managed-devices)」を読み、組織で Android Enterprise フル マネージド デバイス登録が確実にサポートされるようにします。 

## <a name="conditional-access-policies"></a>条件付きアクセス ポリシー
組織は Azure AD 条件付きアクセス ポリシーを使用して、ユーザーが確実に登録済み Android デバイスを使用して職場または学校のコンテンツにのみアクセスできるようにすることができます。 これを行うには、可能性のあるすべてのユーザーを対象とする条件付きアクセス ポリシーが必要です。 このポリシーの作成の詳細については、[条件付きアクセスを使用してクラウド アプリへのアクセスにマネージド デバイスを要求する方法](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)に関するページを参照してください。 

次のステップに従います。「[シナリオ:iOS および Android デバイスでデバイス登録を必須にする](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices)」。これにより、準拠している登録済みモバイル デバイスのみで Office 365 エンドポイントに接続できるようになります。

## <a name="next-steps"></a>次のステップ

[アプリ構成ポリシーを設定する](android-app-configuration-policies.md)
