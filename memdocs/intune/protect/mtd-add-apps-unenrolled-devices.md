---
title: Mobile Threat Defense アプリを未登録のデバイスに追加する
titleSuffix: Microsoft Intune
description: Mobile Threat Defense アプリを未登録のデバイスに追加する (デバイス ユーザー別に)
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
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
ms.openlocfilehash: f667b6ad9ba9f7c353d89b4d3fc4ff749499bfaf
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972039"
---
# <a name="add-mobile-threat-defense-apps-to-unenrolled-devices"></a>Mobile Threat Defense アプリを未登録のデバイスに追加する

既定では、Mobile Threat Defense で Intune アプリ保護ポリシーを使用するとき、Intune では、必要なすべてのアプリをインストールしてそれにサインインし、関連サービスとの接続を有効にするように、デバイスのエンド ユーザーが誘導されます。

エンド ユーザーは、そのデバイスを登録するために Microsoft Authenticator (iOS) を、モバイル デバイスで脅威が確認されたときに通知を受け取り、脅威に対処する指示を受け取るために Mobile Threat Defense (Android と iOS の両方) を必要とします。

必要に応じて、Intune を使用し、Microsoft Authenticator アプリと Mobile Threat Defense (MTD) アプリを追加して展開できます。

> [!NOTE]
> この記事は、アプリ保護ポリシーをサポートするすべての Mobile Threat Defense パートナーに適用されます。
>
> - Better Mobile (Android、iOS/iPadOS)
> - Lookout for Work (Android、iOS/iPadOS)。
> - Wandera (Android、iOS/iPadOS)
> - Zimperium (Android、iOS/iPadOS)

> 未登録のデバイスについては、Intune で使用する Mobile Threat Defense for iOS アプリを設定する **iOS アプリ構成ポリシーは必要ありません**。 Intune 登録デバイスと比較したとき、これが大きな違いです。

## <a name="configure-microsoft-authenticator-for-ios-via-intune-optional"></a>Intune から iOS 向け Microsoft Authenticator を構成する (任意)

Mobile Threat Defense で Intune アプリ保護ポリシーを使用するとき、Intune では、Microsoft Authenticator (iOS) をインストールし、それにサインインし、それにデバイスを登録するようにエンド ユーザーが指示されます。

ただし、エンド ユーザーが Intune ポータル サイト経由でアプリを入手できるようにする場合、「[iOS ストア アプリを Microsoft Intune に追加する](../apps/store-apps-ios.md)」の指示を参照してください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [Microsoft Authenticator - iOS アプリ ストア URL](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) を使用します。 最後の手順として、忘れずに [Intune でグループにアプリを割り当ててください](../apps/apps-deploy.md)。

> [!NOTE]
> iOS デバイスでは、Azure AD によってチェックされた ID がユーザーに与えられるように、[Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) が必要です。 Intune ポータル サイトは Android デバイスでブローカーとして機能するため、ユーザーに Azure AD によってチェックされた ID が与えられます。

## <a name="making-mobile-threat-defense-apps-available-via-intune-optional"></a>Mobile Threat Defense アプリを Intune から入手できるようにする (任意)

Mobile Threat Defense で Intune アプリ保護ポリシーを使用するとき、Intune では、必須の Mobile Threat Defense クライアント アプリをインストールし、それにサインインするようにエンド ユーザーが指示されます。

ただし、Intune ポータル サイトからエンド ユーザーがアプリを入手できるようにする場合、[Azure portal](https://portal.azure.com/) で以下の手順に従います。 次のプロセスをよく理解している必要があります。

- [Intune にアプリを追加する](../apps/apps-add.md)
- [Intune でアプリを割り当てる](../apps/apps-deploy.md)

### <a name="making-lookout-for-work-available-to-end-users"></a>Lookout for Work をエンド ユーザーが利用できるようにする

- **Android**  
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [Lookout for Work - Play ストア URL](https://play.google.com/store/apps/details?id=com.lookout.enterprise) を使用します。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [Lookout for Work - iOS アプリ ストア URL](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) を使用します。

<!-- ### Making Symantec Endpoint Protection Mobile available to end users
- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). When completing the **Configure app information** section, use this [SEP Mobile app store URL](https://play.google.com/store/apps/details?id=com.skycure.skycure). For **Minimum operating system**, select **Android 4.0 (Ice Cream Sandwich)**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [SEP Mobile - App Store URL](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) when completing the **Configure app information** section.

### Making Check Point SandBlast Mobile available to end users
- **Android**  
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Check Point SandBlast Mobile - Play Store URL](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) when completing the **Configure app information** section. 

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Check Point SandBlast Mobile - App Store URL](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) when completing the **Configure app information** section. -->

### <a name="making-zimperium-available-to-end-users"></a>Zimperium をエンド ユーザーが入手できるようにする

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [Zimperium - Play ストア URL](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) を使用します。
- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [Zimperium - アプリ ストア URL](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) を使用します。

<!-- ### Making Pradeo available to end users
- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Pradeo - Play Store URL](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Pradeo - App Store URL](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) when completing the **Configure app information** section. -->

### <a name="making-better-mobile-available-to-end-users"></a>Better Mobile をエンド ユーザーが入手できるようにする

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [Active Shield - Play ストア URL](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) を使用します。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [ActiveShield - App Store URL](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) を使用します。

<!-- ### Making Sophos available to end users
- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Sophos - Play Store URL](https://play.google.com/store/apps/details?id=com.sophos.smsec) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield - App Store URL](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) when completing the **Configure app information** section.  -->

### <a name="making-wandera-available-to-end-users"></a>Wandera をエンド ユーザーが入手できるようにする
- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [Wandera Mobile - Play ストア URL](https://play.google.com/store/apps/details?id=com.wandera.android) を使用します。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 「**アプリ情報を構成する**」セクションで情報を入力するときは、この [Wandera Mobile - App Store URL](https://itunes.apple.com/app/wandera/id605469330) を使用します。

## <a name="next-steps"></a>次のステップ

- [未登録デバイスに対して Intune で Mobile Threat Defense コネクタを有効にする](mtd-enable-unenrolled-devices.md)
