---
title: Android Enterprise セキュリティの構成ポリシー
titleSuffix: Microsoft Intune
description: Android Enterprise デバイスの基本セキュリティと高セキュリティのために推奨される制限事項と設定について説明します。
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
ms.openlocfilehash: 3735a37d4572454968638d29ab2646d6fda943ad
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546588"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>Android Enterprise セキュリティ構成フレームワークのアプリ構成ポリシー

[Android Enterprise セキュリティ構成フレームワーク](android-configuration-framework.md)の一部として、Android Enterprise デバイス用のアプリ構成ポリシーを適切に設定する必要があります。

Android Enterprise 仕事用プロファイル デバイスは、仕事用と個人用のデータを相互に分離するように設計されています。 Android Enterprise フル マネージド デバイスは、職場または学校のデータのみを対象とするように設計されています。 したがって、これらのデバイス上に展開される Microsoft アプリを、個人アカウントを許可しないように構成する必要があります。

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>Android Enterprise デバイスで Microsoft アプリの個人アカウントを許可しない

1. アプリをマネージド Google Play に追加します。 詳細は、「[Intune で managed Google Play アプリを Android エンタープライズ デバイスに追加する](../apps/apps-add-android-for-work.md)」を参照してください。
2. 「[マネージド Android Enterprise デバイス用にアプリ構成ポリシーを追加する]()」の説明に従って、各マネージド Google Play アプリ用のポリシーを作成します。
3. 各ポリシーに次の単一のキーを作成します。

    | キー | 値 |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | 1 つまたは複数の区切られた UPN。<br>このキーで定義された管理対象のユーザー アカウントのみが許可されます。<br>Intune に登録されているデバイスでは、{{userprincipalname}} トークンを使用して登録済みのユーザー アカウントを表すことができます。 |


## <a name="next-steps"></a>次のステップ
[Android enterprise 仕事用プロファイル セキュリティ設定](android-work-profile-security-settings.md)または [Android Enterprise フル マネージド セキュリティ設定](android-fully-managed-security-settings.md)を適用します。