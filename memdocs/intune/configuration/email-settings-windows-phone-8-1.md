---
title: Windows Phone 8.1 デバイス向けの Microsoft Intune 電子メール設定
titleSuffix: ''
description: Windows Phone 8.1 を実行するデバイスでの電子メール接続の構成に使用できる Intune 設定について説明します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5bd00f12ab0f015c6408e2bbc934e1320c7540e
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146145"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>Windows Phone 8.1 を実行するデバイス向けの Microsoft Intune 電子メール プロファイル設定

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

この記事では、Windows Phone 8.1 を実行しているデバイス用に構成できる電子メール プロファイル設定を示します。

>[!IMPORTANT]
>Windows Phone 8.1 の電子メール プロファイルは、Windows 10 デバイスにも適用されます。

## <a name="before-you-begin"></a>始める前に

[Windows Phone 8.1 の電子メール プロファイルを作成します](email-settings-configure.md)。

## <a name="email-settings"></a>電子メールの設定

- **[電子メール サーバー]** :Exchange サーバーのホスト名を入力します。 たとえば、「`outlook.office365.com`」と入力します。
- **[アカウント名]** :電子メール アカウントの表示名を入力します。 この名前は、ユーザーのデバイス上に表示されます。
- **[AAD からのユーザー名の属性]** :これは、Intune が Azure Active Directory (AAD) から取得する名前です。 Intune はこのプロファイルで使用されるユーザー名を動的に生成します。 次のようなオプションがあります。
  - **[ユーザー プリンシパル名]** :`user1` や `user1@contoso.com` などの名前を取得します。
  - **[プライマリ SMTP アドレス]** :`user1@contoso.com` のような形式で電子メール アドレスを取得します。
  - **[sAM アカウント名]** :`domain\user1` などのドメインを要求します。 次の項目も入力します。
    - **[ユーザー ドメイン名のソース]** :次のようなオプションがあります。
      - **[AAD]** (Azure Active Directory): **[AAD からのユーザー ドメイン名属性]** を入力します。 ユーザーの **[完全なドメイン名]** または **[NetBIOS 名]** のどちらの属性を取得するかを選択します。
      - **[カスタム]** : **[使用するカスタム ドメイン名]** を入力します。 `contoso.com` や `contoso` など、Intune でドメイン名として使用する値を入力します。

- **[AAD からのメール アドレス属性]** :Intune では、Azure Active Directory (AAD) からこの属性が取得されます。 ユーザーの電子メール アドレスを生成する方法を選択します。 次のようなオプションがあります。
  - **[ユーザー プリンシパル名]** :`user1@contoso.com` や `user1` など、完全なプリンシパル名を電子メール アドレスとして使用します。
  - **[プライマリ SMTP アドレス]** :`user1@contoso.com` など、プライマリ SMTP アドレスを使用して Exchange にサインインします。

## <a name="security-settings"></a>セキュリティ設定

- **[SSL]** : **[有効]** を選択すると、電子メールの送受信および Exchange サーバーとの通信に、SSL (Secure Sockets Layer) 通信が使用されます。 **[無効]** を選択すると、SSL は必要ありません。

## <a name="synchronization-settings"></a>同期設定

- **[同期する電子メールの日数]** :同期する電子メールの日数を選択します。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 利用可能なすべての電子メールを同期するには、 **[無制限]** を選択します。
- **[同期スケジュール]** :デバイスが Exchange サーバーからデータを同期するスケジュールを選択します。 メッセージが到着したらすぐにデータを同期する **[メッセージの着信時]** を選択することもできます。 または、デバイス ユーザーが同期を開始する場合は **[手動]** を選択します。

## <a name="content-sync-settings"></a>コンテンツ同期設定

- **[同期するコンテンツの種類]** :デバイスに同期するコンテンツの種類を選択します。
  - **[連絡先]** : **[オン]** にすると、連絡先が同期されます。 **[オフ]** にすると、連絡先は自動的に同期されません。 ユーザーが手動で同期します。
  - **[カレンダー]** : **[オン]** にすると、カレンダーが同期されます。 **[オフ]** にすると、連絡先は自動的に同期されません。 ユーザーが手動で同期します。
  - **[タスク]** : **[オン]** にすると、タスクが同期されます。 **[オフ]** にすると、タスクは自動的に同期されません。 ユーザーが手動で同期します。

## <a name="next-steps"></a>次のステップ

[Android](email-settings-android.md)、[Android Enterprise](email-settings-android-enterprise.md)、[iOS/iPadOS](email-settings-ios.md)、[Windows 10](email-settings-windows-10.md) でもメールの設定を構成できます。

[Intune で電子メールの設定を構成します](email-settings-configure.md)。
