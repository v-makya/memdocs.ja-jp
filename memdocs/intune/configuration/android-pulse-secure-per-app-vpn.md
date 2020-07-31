---
title: Microsoft Intune における Android デバイス管理者用のアプリごとのカスタム VPN プロファイル - Azure | Microsoft Docs
description: Microsoft Intune で Pulse Secure または Citrix VPN の接続の種類を使用して、Android デバイス管理者でアプリごとの VPN プロファイルに対してカスタム プロファイルを使用します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c8e09b6010f7fc846fd81281053eaaa722e5ef4
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262797"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Microsoft Intune のカスタム プロファイルを使って、Android デバイス用にアプリごとの VPN プロファイルを作成する

Intune で管理する、アプリごとの VPN プロファイルを Android 5.0 以降のデバイスに作成できます。 まず、Pulse Secure または Citrix 接続の種類を使用する VPN プロファイルを作成します。 次に、特定のアプリと VPN プロファイルを関連付けるカスタム構成ポリシーを作成します。

この機能は、以下に適用されます。

- Android デバイス管理者

Android Enterprise デバイスでアプリごとの VPN を使用するには、[アプリ構成ポリシー](../apps/app-configuration-vpn-ae.md)を使います。 アプリ構成ポリシーでは、より多くの VPN クライアント アプリがサポートされています。 Android Enterprise デバイスでは、この記事の手順を使用できます。 ただしこれは推奨されません。また、Pulse Secure と Citrix VPN 接続のみに制限されます。

Android デバイスまたはユーザー グループにポリシーが割り当てられた後、ユーザーは Pulse Secure または Citrix VPN クライアントを開始する必要があります。 その後、VPN クライアントは、指定されたアプリからのトラフィックにのみ、開いている VPN 接続の使用を許可します。

> [!NOTE]
>
> Android デバイス管理者に対しては、Pulse Secure と Citrix の接続の種類のみがサポートされます。 Android Enterprise デバイスでは、[アプリ構成ポリシー](../apps/app-configuration-vpn-ae.md)を使います。

## <a name="step-1-create-a-vpn-profile"></a>手順 1:VPN プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[Android デバイス管理者]** を選択します。
    - **[プロファイル]** : **[VPN]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「**会社全体の Android デバイス管理者のアプリごとの VPN プロファイル**」は適切なプロファイル名です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** で、プロファイルに必要な設定を構成します。

    - [Android デバイス管理者デバイスの VPN 設定](vpn-settings-android.md)。

    VPN プロファイルの作成時に入力した**接続名**の値を書き留めてください。 この名前は、次の手順で必要になります。 この例では、接続名は **MyAppVpnProfile** です。

8. **[次へ]** を選択し、プロファイルの作成を続行します。 詳細については、「[VPN プロファイルの作成](vpn-settings-configure.md#create-the-profile)」を参照してください。

## <a name="step-2-create-a-custom-configuration-policy"></a>手順 2:カスタム構成ポリシーを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **名前**:カスタム プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「**会社全体のカスタム OMA-URI Android VPN プロファイル**」は適切なプロファイル名です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
    - **[プラットフォーム]** : **[Android デバイス管理者]** を選択します。
    - **[プロファイルの種類]** : **[カスタム]** を選択します。

4. **[設定]**  >  **[構成]** の順に選択します。
5. **[OMA-URI のカスタム設定]** ウィンドウで、 **[追加]** を選択します。
    - **名前**:設定の名前を入力します。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
    - **OMA-URI**:「`./Vendor/MSFT/VPN/Profile/*Name*/PackageList`」と入力します。ここで *[名前]* は手順 1 でメモした接続名です。 この例では、文字列は `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList` です。
    - **[データ型]** :「**String**」と入力します。
    - **値**:プロファイルと関連付けるセミコロンで区切られたパッケージの一覧を入力します。 たとえば、Excel と Google Chrome ブラウザーで VPN 接続を使用するには、「`com.microsoft.office.excel;com.android.chrome`」と入力します。

    :::image type="content" source="./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png" alt-text="Microsoft Intune における Android デバイス管理者のアプリごとの VPN カスタム ポリシー":::

### <a name="set-your-blocked-and-allowed-app-list-optional"></a>ブロックされたアプリと許可されたアプリの一覧を設定する (省略可能)

VPN 接続を使用*できない*アプリの一覧を入力するには、**BLACKLIST** 値を使用します。 その他のすべてのアプリは、VPN 経由で接続します。 あるいは、**WHITELIST** 値を使用し、VPN 接続を使用*できる*アプリの一覧を入力します。 一覧に含まれないアプリは、VPN 経由で接続しません。

1. **[OMA-URI のカスタム設定]** ウィンドウで、 **[追加]** を選択します。
2. 設定の名前を入力します。
3. **OMA-URI** に「`./Vendor/MSFT/VPN/Profile/*Name*/Mode`」と入力します。 *[名前]* は手順 1 でメモした VPN プロファイル名です。 今回の例では、文字列は `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode` です。
4. **[データ型]** に「**String**」と入力します。
5. **[値]** に **[BLACKLIST]** または **[WHITELIST]** と入力します。

## <a name="step-3-assign-both-policies"></a>手順 3:両方のポリシーを割り当てる

必要なユーザーまたはデバイスに[両方のデバイス プロファイルを割り当てます](device-profile-assign.md)。

## <a name="next-steps"></a>次のステップ

- すべての Android デバイス管理者の VPN 設定の一覧については、[VPN を構成するための Android デバイスの設定](vpn-settings-android.md)に関するページを参照してください。
- VPN の設定と Intune の詳細については、[Microsoft Intune での VPN の設定の構成](vpn-settings-configure.md)に関するページを参照してください。
