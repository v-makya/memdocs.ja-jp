---
title: Microsoft Intune での Windows 10 デバイス向けの電子メール設定 - Azure | Microsoft Docs
description: Exchange サーバーを使用するデバイス構成電子メール プロファイルを作成し、Azure Active Directory から属性を取得します。 SSL を有効にして、Microsoft Intune を使用して Windows 10 で電子メールとスケジュールを同期することもできます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa861a266f89b82fdd2d6e73d30fdc2e58da33b4
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086904"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>Microsoft Intune での Windows 10 を実行するデバイス向けの電子メール プロファイル設定

電子メールのプロファイル設定を使用して、Windows 10 以降を実行するデバイスで "メール" アプリを構成します。

## <a name="before-you-begin"></a>始める前に

[プロファイルを作成します](email-settings-configure.md)。

## <a name="email-settings"></a>電子メールの設定

- **[電子メール サーバー]** :Exchange サーバーのホスト名を入力します。 たとえば、「`outlook.office365.com`」と入力します。
- **[アカウント名]** :電子メール アカウントの表示名を入力します。 この名前は、ユーザーのデバイス上に表示されます。
- **[AAD からのユーザー名の属性]** :これは、Intune が Azure Active Directory (AAD) から取得する名前です。 Intune はこのプロファイルで使用されるユーザー名を動的に生成します。 次のようなオプションがあります。
  - **[ユーザー プリンシパル名]** :`user1` や `user1@contoso.com` などの名前を取得します。
  - **[プライマリ SMTP アドレス]** :`user1@contoso.com` のような形式で電子メール アドレスを取得します。
  - **[sAM アカウント名]** :`domain\user1` などのドメインを要求します。 次の項目も入力します。  
    - **[ユーザー ドメイン名のソース]** : **[AAD]** (Azure Active Directory) または **[カスタム]** を選択します。

      **[AAD]** から属性を取得する場合、次を入力します。
      - **[AAD からのユーザー ドメイン名属性]** :ユーザーの **[完全なドメイン名]** または **[NetBIOS 名]** のどちらの属性を取得するかを選択します。

      **[カスタム]** 属性を使用する選択を行っている場合、次を入力します。
      - **[使用するカスタム ドメイン名]** :`contoso.com` や `contoso` など、Intune でドメイン名として使用する値を入力します。

- **[AAD からのメール アドレス属性]** :Intune では、Azure Active Directory (AAD) からこの属性が取得されます。 ユーザーの電子メール アドレスを生成する方法を選択します。 次のようなオプションがあります。
  - **[ユーザー プリンシパル名]** :`user1@contoso.com` や `user1` など、完全なプリンシパル名を電子メール アドレスとして使用します。
  - **[プライマリ SMTP アドレス]** :`user1@contoso.com` など、プライマリ SMTP アドレスを使用して Exchange にサインインします。

### <a name="security"></a>セキュリティ

- **[SSL]** : **[有効]** を選択すると、電子メールの送受信および Exchange サーバーとの通信に、SSL (Secure Sockets Layer) 通信が使用されます。 **[無効]** を選択すると、SSL は必要ありません。

### <a name="synchronization"></a>同期

- **[同期する電子メールの日数]** :同期する電子メールの日数を選択します。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 利用可能なすべての電子メールを同期するには、 **[無制限]** を選択します。
- **[同期スケジュール]** :デバイスが Exchange サーバーからデータを同期するスケジュールを選択します。 メッセージが到着したらすぐにデータを同期する **[メッセージの着信時]** を選択することもできます。 または、デバイス ユーザーが同期を開始する場合は **[手動]** を選択します。

### <a name="content-sync"></a>コンテンツの同期

- **[同期するコンテンツの種類]** :デバイスに同期するコンテンツの種類を選択します。
  - **[連絡先]** : **[オン]** にすると、連絡先が同期されます。 **[オフ]** にすると、連絡先は自動的に同期されません。 ユーザーが手動で同期します。
  - **[カレンダー]** : **[オン]** にすると、カレンダーが同期されます。 **[オフ]** にすると、連絡先は自動的に同期されません。 ユーザーが手動で同期します。
  - **[タスク]** : **[オン]** にすると、タスクが同期されます。 **[オフ]** にすると、タスクは自動的に同期されません。 ユーザーが手動で同期します。

## <a name="next-steps"></a>次のステップ

[Android](email-settings-android.md)、[Android Enterprise](email-settings-android-enterprise.md)、[iOS/iPadOS](email-settings-ios.md) でもメールの設定を構成できます。 

[Intune で電子メールの設定を構成します](email-settings-configure.md)。
