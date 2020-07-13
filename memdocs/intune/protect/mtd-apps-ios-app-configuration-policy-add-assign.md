---
title: MTD アプリを追加し、Microsoft Intune に割り当てる
titleSuffix: Microsoft Intune
description: Intune を使用し、Mobile Threat Defense (MTD) アプリ、Microsoft Authenticator アプリ、iOS 構成ポリシーを Azure Portal で追加します。
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
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4782c2a8f2c8791929ca4e585dab96031bf550fa
ms.sourcegitcommit: f999131e513d50967f88795e400d5b089ebc5878
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85914627"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Intune で Mobile Threat Defense (MTD) アプリを追加して割り当てる

脅威がモバイル デバイスで特定されたときにエンドユーザーが通知を受け取れるように、また、脅威を除去するための手引きが受けられるように、Intune を利用して Mobile Threat Defense (MTD) アプリを追加して展開することができます。

> [!NOTE]
> この記事は、すべての Mobile Threat Defense パートナーに適用されます。

## <a name="before-you-begin"></a>始める前に

Intune で次の手順を実行します。 次のプロセスをよく理解している必要があります。

- [Intune にアプリを追加する](../apps/apps-add.md)。
- [iOS アプリ構成ポリシーを Intune に追加する](../apps/app-configuration-policies-use-ios.md)。
- [Intune でアプリを割り当てる](../apps/apps-deploy.md)。

> [!TIP]
> Intune ポータル サイトは Android デバイスでブローカーとして機能するため、ユーザーに Azure AD によってチェックされた ID が与えられます。

## <a name="configure-microsoft-authenticator-for-ios"></a>iOS 向け Microsoft Authenticator を構成する

iOS デバイスでは、Azure AD によってチェックされた ID がユーザーに与えられるように、[Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) が必要です。 さらに、Intune で使用する MTD の iOS アプリを設定する iOS アプリ構成ポリシーも必要です。

iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ情報]** を構成するときに、こちらの [Microsoft Authenticator のアプリ ストア URL](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) を使用してください。

## <a name="configure-your-mtd-apps-with-an-app-configuration-policy"></a>MTD アプリにアプリ構成ポリシーを構成する

ユーザーのオンボードを簡単にするために、MDM マネージド デバイス上のモバイル脅威防御アプリでは、アプリ構成が使用されます。 未登録のデバイスに対して MDM ベースのアプリ構成を使用することはできないため、「[モバイル脅威防御アプリを未登録のデバイスに追加する](../protect/mtd-add-apps-unenrolled-devices.md)」を参照してください。

### <a name="lookout-for-work-app-configuration-policy"></a>Lookout for Work アプリ構成ポリシー

[iOS アプリ構成ポリシーの使用](../apps/app-configuration-policies-use-ios.md)に関する記事の説明に従って、iOS アプリ構成ポリシーを作成します。

### <a name="sep-mobile-app-configuration-policy"></a>SEP モバイル アプリ構成ポリシー

[Symantec Endpoint Protection Management コンソール](https://aad.skycure.com)で以前に構成したものと同じ Azure AD アカウントを使います。これは、Intune へのサインインに使用するアカウントと同じものである必要があります。

- iOS アプリ構成ポリシー ファイルを**ダウンロード**します。
  - [Symantec Endpoint Protection Management コンソール](https://aad.skycure.com)に移動し、管理者資格情報でサインインします。

  - **[Settings]\(設定\)** に移動し、 **[Integrations]\(統合\)** で **[Intune]** を選びます。 **[EMM Integration Selection]\(EMM 統合の選択\)** を選びます。 **[Microsoft]** を選び、選択内容を保存します。

  - **[Integration setup files]\(統合セットアップ ファイル\)** リンクをクリックし、生成された \*.zip ファイルを保存します。 この .zip ファイルには * **.plist** ファイルが含まれます。このファイルを利用し、Intune で iOS アプリ構成ポリシーが作成されます。

  - [iOS 用 Microsoft Intune アプリ構成ポリシーを使用する](../apps/app-configuration-policies-use-ios.md)手順に従って、SEP Mobile iOS アプリ構成ポリシーを追加します。

    - **[構成設定の形式]** に対して、 **[XML データを入力する]** を選択し、* **.plist** ファイルから内容をコピーして、その内容を構成ポリシーの本文に貼り付けます。

> [!NOTE]
> ファイルを取得できない場合は、[Symantec Endpoint Protection Mobile エンタープライズ サポート](https://support.symantec.com/en_US/contact-support.html)にお問い合わせください。

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Check Point SandBlast Mobile アプリ構成ポリシー

[iOS 用 Microsoft Intune アプリ構成ポリシーを使用する](../apps/app-configuration-policies-use-ios.md)手順に従って、Check Point SandBlast Mobile iOS アプリ構成ポリシーを追加します。

- **[構成設定の形式]** に対して、 **[XML データを入力する]** を選択し、次の内容をコピーして、構成ポリシーの本文に貼り付けます。

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### <a name="zimperium-app-configuration-policy"></a>Zimperium アプリ構成ポリシー

[iOS 用 Microsoft Intune アプリ構成ポリシーを使用する](../apps/app-configuration-policies-use-ios.md)手順に従って、Zimperium iOS アプリ構成ポリシーを追加します。

- **[構成設定の形式]** に対して、 **[XML データを入力する]** を選択し、次の内容をコピーして、構成ポリシーの本文に貼り付けます。

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### <a name="pradeo-app-configuration-policy"></a>Pradeo アプリ構成ポリシー

Pradeo では、iOS/iPadOS でのアプリケーション構成ポリシーをサポートしていません。  アプリを構成するには、代わりに、Pradeo を使用して目的の設定であらかじめ構成されたカスタム IPA または APK ファイルを実装します。

### <a name="better-mobile-app-configuration-policy"></a>Better Mobile モバイル アプリ構成ポリシー

[iOS 用 Microsoft Intune アプリ構成ポリシーを使用する](../apps/app-configuration-policies-use-ios.md)手順に従って、Better Mobile iOS アプリ構成ポリシーを追加します。

- **[構成設定の形式]** に対して、 **[XML データを入力する]** を選択し、次の内容をコピーして、構成ポリシーの本文に貼り付けます。 `https://client.bmobi.net` の URL を適切なコンソールの URL に置き換えます。

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### <a name="sophos-mobile-app-configuration-policy"></a>Sophos Mobile アプリ構成ポリシー

[iOS アプリ構成ポリシーの使用](../apps/app-configuration-policies-use-ios.md)に関する記事の説明に従って、iOS アプリ構成ポリシーを作成します。 詳細については、Sophos ナレッジ ベースの「[Sophos Intercept X for Mobile iOS - Available managed settings (Sophos Intercept X for Mobile iOS - 使用できる管理設定)](https://community.sophos.com/kb/133963)」を参照してください。

### <a name="wandera-app-configuration-policy"></a>Wandera アプリ構成ポリシー

> [!NOTE]
> 初期テストでは、構成ポリシーの [割り当て] セクションでユーザーとデバイスを割り当てるときに、テスト グループを使用します。 

- **Android**
  - [Android 用 Microsoft Intune アプリ構成ポリシーを使用する](../apps/app-configuration-policies-use-android.md)ための手順を参照します。プロンプトが表示されたら、以下の情報を使用して Wandera Android アプリ構成ポリシーを追加します。

1. **RADAR Wandera ポータル**で、 **[構成設定の形式]** の下の **[追加]** ボタンをクリックします。
2. **[構成キー]** の一覧から **[アクティブ化プロファイルの URL]** を選択します。 **[OK]** をクリックします。
3. **[アクティブ化プロファイルの URL]** で、 **[値の型]** メニューから **[文字列]** を選択し、RADAR で目的のアクティブ化プロファイルから**共有可能なリンク URL** をコピーします。
4. **Intune 管理コンソール アプリ構成 UI** で、 **[設定]** を選択し、 **[構成設定の形式]、[構成デザイナーを使用する]** の順に定義し、**共有可能なリンク URL** を貼り付けます。  

> [!NOTE] 
> iOS とは異なり、Wandera アクティブ化プロファイルごとに一意の Android Enterprise アプリ構成ポリシーを定義する必要があります。 複数の Wandera アクティブ化プロファイルを必要としない場合は、すべてのターゲット デバイスに対して単一の Android アプリ構成を使用できます。 Wandera でアクティブ化プロファイルを作成するときは、[関連付けられているユーザーの構成] で必ず [Azure Active Directory] を選択して、Wandera で UEM 接続を介して確実にデバイスと Intune を同期できるようにしてください。

- **Android**
  - [iOS 用 Microsoft Intune アプリ構成ポリシーを使用する](../apps/app-configuration-policies-use-ios.md)ための手順を参照します。プロンプトが表示されたら、以下の情報を使用して Wandera iOS アプリ構成ポリシーを追加します。

1. **RADAR Wandera ポータル**で、 **[デバイス] > [アクティブ化]** に移動し、任意のアクティブ化プロファイルを選択します。 **[Deployment Strategies]\(展開戦略\) > [マネージド デバイス] > [Microsoft Intune]** をクリックし、 **[iOS アプリ構成設定]** を見つけます。  
2. ボックスを展開して iOS アプリ構成の XML を表示し、それをシステム クリップボードにコピーします。  
3. **Intune 管理コンソール アプリ構成 UI 設定**で、 **[構成設定の形式]、[XML データを入力する]** の順に定義します。 
4. [アプリの構成] テキスト ボックスに XML を貼り付けます。

> [!NOTE]
> Wandera を使用してプロビジョニングされるすべてのデバイスで、単一の iOS 構成ポリシーを使用できます。  

## <a name="assigning-mobile-threat-defense-apps-to-end-users-via-intune"></a>Intune を使用したエンド ユーザーへのモバイル脅威防御アプリの割り当て

エンド ユーザーのデバイスにモバイル脅威防御アプリをインストールするために、Azure portal で次の手順に従うことができます。 次のプロセスをよく理解している必要があります。

- [Intune を使用したグループへのアプリの割り当て](../apps/apps-deploy.md)

MTD プロバイダーに対応するセクションを選択します。

- [Lookout for Work](#assigning-lookout-for-work)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [Check Point SandBlast Mobile](#assigning-check-point-sandblast-mobile)
- [Zimperium](#assigning-zimperium)
- [Pradeo](#assigning-pradeo)
- [Better Mobile](#assigning-better-mobile)
- [Sophos Mobile](#assigning-sophos)
- [Wandera](#assigning-wandera)

### <a name="assigning-lookout-for-work"></a>Lookout for Work の割り当て

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Lookout for work の Google アプリ ストア URL](https://play.google.com/store/apps/details?id=com.lookout.enterprise) を使用してください。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Lookout for Work の iOS アプリ ストア URL](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) を使用してください。

- **Apple ストア以外の Lookout for Work アプリ**
  - Lookout for Work iOS アプリに再署名する必要があります。 Lookout により、その Lookout for Work iOS アプリが the iOS App Store の外部で配布されます。 アプリを配布する前に、iOS Enterprise Developer Certificate でアプリに再署名する必要があります。  
  - Lookout for Work iOS アプリに再署名する詳細な手順については、Lookout の Web サイトの「[Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714)」(Lookout for Work iOS アプリの再署名プロセス) を参照してください。

  - **Lookout for Work iOS アプリ ユーザーに対して Azure AD Authentication を有効にします。**

    1. [Azure Portal](https://portal.azure.com) に移動し、資格情報でサインインして、アプリケーションのページに移動します。

    2. **Lookout for Work iOS アプリ**を**ネイティブ クライアント アプリケーション**として追加します。

    3. **com.lookout.enterprise.yourcompanyname** を、IPA に署名したときに選択したカスタマー バンドル ID に置換します。

    4. リダイレクト URI を追加します。 **&lt;companyportal://code/>** の後に、元のリダイレクト URI を URL エンコードしたバージョンを続けます。

    5. アプリに**デリゲートされたアクセス許可**を追加します。

    > [!NOTE]
    > 詳細については、「[ネイティブ クライアント アプリケーションの構成](https://azure.microsoft.com/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application)」を参照してください。

  - **Lookout for Work の ipa ファイルを追加します。**

    - [Intune での iOS LOB アプリの追加](../apps/lob-apps-ios.md)に関する記事の説明に従って、再署名した .ipa ファイルをアップロードします。 また、最小 OS バージョンを iOS 8.0 以降に設定する必要があります。

### <a name="assigning-symantec-endpoint-protection-mobile"></a>Symantec Endpoint Protection Mobile の割り当て

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [SEP Mobile の アプリ ストア URL](https://play.google.com/store/apps/details?id=com.skycure.skycure) を使用してください。  **[Minimum operating system]\(最小オペレーティング システム\)** では、**Android 4.0 (Ice Cream Sandwich)** を選びます。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [SEP Mobile の アプリ ストア URL](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) を使用してください。

### <a name="assigning-check-point-sandblast-mobile"></a>Check Point SandBlast Mobile の割り当て

- **Android**  
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Check Point SandBlast Mobile の アプリ ストア URL](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) を使用してください。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Check Point SandBlast Mobile の アプリ ストア URL](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) を使用してください。  

### <a name="assigning-zimperium"></a>Zimperium の割り当て

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Zimperium の アプリ ストア URL](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) を使用してください。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Zimperium の アプリ ストア URL](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) を使用してください。  
 
### <a name="assigning-pradeo"></a>Pradeo の割り当て

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Pradeo の アプリ ストア URL](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) を使用してください。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Pradeo の アプリ ストア URL](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) を使用してください。

### <a name="assigning-better-mobile"></a>Better Mobile の割り当て

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Active Shield の アプリ ストア URL](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) を使用してください。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [ActiveShield の アプリ ストア URL](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) を使用してください。

### <a name="assigning-sophos"></a>Sophos の割り当て

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Sophos の アプリ ストア URL](https://play.google.com/store/apps/details?id=com.sophos.smsec) を使用してください。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [ActiveShield の アプリ ストア URL](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) を使用してください。

### <a name="assigning-wandera"></a>Wandera の割り当て

- **Android**
  - Android ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-android.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Wandera Mobile の アプリ ストア URL](https://play.google.com/store/apps/details?id=com.wandera.android) を使用してください。 **[Minimum operating system]\(最小オペレーティング システム\)** では、 **[Android 5.0]** を選びます。

- **Android**
  - iOS ストア アプリを Microsoft Intune に追加する方法については、[こちら](../apps/store-apps-ios.md)をご覧ください。 **[アプリ ストアの URL]** には、こちらの [Wandera Mobile の アプリ ストア URL](https://itunes.apple.com/app/wandera/id605469330) を使用してください。

## <a name="next-steps"></a>次のステップ

- [MTD のデバイス コンプライアンス ポリシーを構成する](mtd-device-compliance-policy-create.md)
