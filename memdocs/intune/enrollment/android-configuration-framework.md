---
title: Android Enterprise セキュリティの構成フレームワーク
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
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502979"
---
# <a name="android-enterprise-security-configuration-framework"></a>Android Enterprise セキュリティの構成フレームワーク

Android Enterprise セキュリティ構成フレームワークは、デバイスのコンプライアンスと構成ポリシーの設定に関する一連の推奨事項です。 これらの推奨事項を使用して、特定のニーズに合わせて組織のモバイル デバイスのセキュリティ保護を調整できます。

セキュリティを意識した組織は、モバイル デバイス上の会社のデータを確実に保護する方法に注目しています。 そのデータを保護するために使用される方法の 1 つとして、デバイスの登録があります。 デバイス登録によって、組織は以下を実行できます。
- コンプライアンス ポリシーを展開する (PIN の強さ、改造/ルート検証など)。
- 構成ポリシーを展開する (WIFI、証明書、VPN など)。
- アプリのライフサイクルを管理する。

完全なセキュリティ シナリオの設定を支援するために、Microsoft では、[Windows 10 でのセキュリティ構成](https://aka.ms/secconframework)用の新しい分類を導入しています。 Intune では、Android Enterprise セキュリティ構成フレームワークと同様の分類が使用されています。 これらには、基本、強化、および高セキュリティのために推奨されるデバイス コンプライアンスとデバイス制限の設定が含まれています。 この分類については、次の記事で説明されています。

1. [Android Enterprise フレームワークの展開方法](framework-deployment-methodology.md):セキュリティ構成フレームワークを展開するために推奨される方法です。
2. [Android デバイスの登録制限](device-enrollment-restrictions.md):Android Enterprise デバイスの事前登録デバイスに関する制限です。
3. [Android Enterprise デバイス用のアプリ構成ポリシーを設定する](android-app-configuration-policies.md):デバイス上のアプリを個人アカウントを許可しないように構成します。
4. [Android Enterprise 仕事用プロファイルのセキュリティ設定](android-work-profile-security-settings.md):仕事用プロファイル デバイスの基本セキュリティと高セキュリティ向けの具体的な構成設定。
5. [Android Enterprise フル マネージド セキュリティ設定](android-fully-managed-security-settings.md):フル マネージド デバイスの基本、強化、および高セキュリティ向けの具体的な構成設定。

## <a name="android-enterprise-enrollment-modes"></a>Android Enterprise の登録モード

Google では、Android 5.0 に Android Enterprise を導入しています。これには 2 つの登録モードが含まれています。 Android Enterprise セキュリティ構成フレームワークでは、両方のモードに対する推奨事項が用意されています。
- [フル マネージド デバイス (デバイス所有者)](android-fully-managed-enroll.md):1 人のユーザーに関連付けられている会社所有のものが対象です。 このようなデバイスは仕事専用であり、個人用として使用されるものではありません。
- [仕事用プロファイル (プロファイル所有者)](android-work-profile-enroll.md):通常は、IT によって仕事用のデータと個人のデータの間の明確な境界が求められる個人所有のデバイスが対象です。 IT によって制御されるポリシーによって、個人プロファイルに仕事用データを転送できないようにします。


## <a name="next-steps"></a>次のステップ

[Android Enterprise フレームワークの展開方法](framework-deployment-methodology.md)