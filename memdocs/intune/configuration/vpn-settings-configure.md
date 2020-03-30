---
title: Microsoft Intune デバイスに VPN 設定を追加する - Azure | Microsoft Docs
description: Android デバイス管理者、Android Enterprise、iOS、iPadOS、macOS、および Windows デバイスでは、組み込みの設定を使用して Microsoft Intune で仮想プライベート ネットワーク (VPN) 接続を作成します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64356bf9be0c2c439c1f4fc296a9728a7937b001
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086577"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Intune で VPN サーバーに接続するための VPN プロファイルを作成する

仮想プライベート ネットワーク (VPN) を使用すると、組織のユーザーが組織のネットワークにリモート アクセスする際にセキュリティで保護することができます。 デバイスでは、VPN 接続プロファイルを使用して VPN サーバーとの接続が開始されます。 Microsoft Intune の **VPN プロファイル**によって組織内のユーザーとデバイスに VPN 設定を割り当て、組織のネットワークに簡単かつ安全に接続できるようにします。

たとえば、組織のネットワーク上のファイル共有に接続するために必要な設定をすべての iOS/iPadOS デバイスに構成したいとします。 これらの設定を含む VPN プロファイルを作成します。 その後、iOS/iPadOS デバイスを持っているすべてのユーザーにこのプロファイルを割り当てます。 使用できるネットワークの一覧に VPN 接続が表示されるので、ユーザーは最小限の労力で接続できます。

> [!NOTE]
> [Intune のカスタム構成ポリシー](custom-settings-configure.md)を使用して、次のプラットフォーム用の VPN プロファイルを作成できます。
>
> * Android 4 以降
> * Windows 8.1 以降を実行する登録済みのデバイス
> * Windows Phone 8.1 以降
> * Windows 10 デスクトップを実行する登録済みのデバイス
> * Windows 10 Mobile
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>VPN 接続の種類

次の接続の種類を使用して、VPN プロファイルを作成できます。

- 自動
  - Windows 10

- Check Point Capsule VPN
  - Android デバイス管理者
  - Android エンタープライズ仕事用プロファイル
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Cisco AnyConnect
  - Android デバイス管理者
  - Android エンタープライズ仕事用プロファイル
  - Android エンタープライズ デバイス所有者 (フル マネージド)
  - iOS/iPadOS
  - macOS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Android デバイス管理者
  - Android エンタープライズ仕事用プロファイル[アプリ構成ポリシー](../apps/app-configuration-policies-use-android.md)を使用する
  - Android エンタープライズ デバイス所有者 (フル マネージド)[アプリ構成ポリシー](../apps/app-configuration-policies-use-android.md)を使用する
  - iOS/iPadOS
  - Windows 10

- カスタム VPN
  - iOS/iPadOS
  - macOS

  [カスタム設定を持つプロファイルの作成](custom-settings-configure.md)に関するページを参照して、URI の設定を使ってカスタム VPN プロファイルを作成します。

- F5 Access
  - Android デバイス管理者
  - Android エンタープライズ仕事用プロファイル
  - Android エンタープライズ デバイス所有者 (フル マネージド)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Android エンタープライズ仕事用プロファイル[アプリ構成ポリシー](../apps/app-configuration-policies-use-android.md)を使用する
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Android デバイス管理者
  - Android エンタープライズ仕事用プロファイル
  - Android エンタープライズ デバイス所有者 (フル マネージド)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- SonicWall Mobile Connect
  - Android デバイス管理者
  - Android エンタープライズ仕事用プロファイル
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Zscaler
  - Android エンタープライズ仕事用プロファイル[アプリ構成ポリシー](../apps/app-configuration-policies-use-android.md)を使用する
  - iOS/iPadOS

> [!IMPORTANT]
> デバイスに割り当てられた VPN プロファイルを使用する前に、プロファイル用の該当する VPN アプリをインストールする必要があります。 Intune を使用してアプリを割り当てるには、「[Microsoft Intune でのアプリの管理とは](../apps/app-management.md)」を参照してください。  

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** :デバイスのプラットフォームを選択します。 次のようなオプションがあります。
      - **Android デバイス管理者**
      - **[Android エンタープライズ]**  >  **[デバイスの所有者のみ]**
      - **[Android エンタープライズ]**  >  **[仕事用プロファイルのみ]**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 以降**
      - **Windows 8.1 以降**
      - **Windows Phone 8.1**
    - **[プロファイル]** : **[VPN]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「**会社全体の VPN プロファイル**」は適切なプロファイル名です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** では、選択したプラットフォームによって構成できる設定が変わります。 詳細な設定については、お使いのプラットフォームを選択してください。

    - [Android デバイス管理者](vpn-settings-android.md)
    - [Android エンタープライズ](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10 (Windows Holographic for Business を含む)](vpn-settings-windows-10.md)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. **[次へ]** を選択します。
9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="secure-your-vpn-profiles"></a>VPN プロファイルをセキュリティで保護する

VPN プロファイルは、さまざまな製造元から提供される多くの異なる接続の種類およびプロトコルに対応しています。 これらの接続は、通常、次の方法を通じてセキュリティで保護されます。

### <a name="certificates"></a>証明書

VPN プロファイルを作成するときに、Intune で事前に作成した SCEP または PKCS の証明書プロファイルを選択します。 このプロファイルは ID 証明書と呼ばれます。 ユーザーのデバイスの接続を許可するために作成した信頼済み証明書プロファイル (または、"*ルート証明書*") に対して認証を行うために使用されます。 信頼できる証明書は、VPN 接続を認証するコンピューター (通常は VPN サーバー) に割り当てられます。

Intune で証明書プロファイルを作成および使用する方法の詳細については、[Microsoft Intune で証明書を構成する方法](../protect/certificates-configure.md)に関する記事を参照してください。

### <a name="user-name-and-password"></a>ユーザー名とパスワード

ユーザーは、ユーザー名とパスワードを提供することにより、VPN サーバーに対して認証を行います。

## <a name="next-steps"></a>次のステップ

プロファイルを作成しましたが、まだ何も行っていません。 次に、一部のデバイスに[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Android デバイス管理者または Android Enterprise](android-pulse-secure-per-app-vpn.md) デバイスと [iOS/iPadOS](vpn-setting-configure-per-app.md) デバイス上でアプリごとの VPN を作成し、使用することもできます。
