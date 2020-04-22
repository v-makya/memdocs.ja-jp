---
title: Microsoft Intune での Android 用のアプリごとのカスタム VPN プロファイル - Azure | Microsoft Docs
description: Microsoft Intune で管理する Android デバイス管理者デバイス用にアプリごとの VPN プロファイルを作成する方法について説明します。
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
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d58ab666929e1e28cab4e19f2e2cec668f428452
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80083867"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Microsoft Intune のカスタム プロファイルを使って、Android デバイス用にアプリごとの VPN プロファイルを作成する

Intune で管理する、アプリごとの VPN プロファイルを Android 5.0 以降のデバイスに作成できます。 まず、Pulse Secure または Citrix 接続の種類を使用する VPN プロファイルを作成します。 次に、特定のアプリと VPN プロファイルを関連付けるカスタム構成ポリシーを作成します。

> [!NOTE]
> Android Enterprise デバイスでアプリごとの VPN を使用する目的でもこの手順を利用できます。 ただし、VPN クライアント アプリには[アプリ構成ポリシー](../apps/app-configuration-policies-use-android.md)を使用することをお勧めします。

Android デバイスまたはユーザー グループにポリシーが割り当てられた後、ユーザーは Pulse Secure または Citrix VPN クライアントを開始する必要があります。 その後、VPN クライアントは、指定されたアプリからのトラフィックにのみ、開いている VPN 接続の使用を許可します。

> [!NOTE]
>
> このプロファイルに対しては Pulse Secure 接続タイプと Citrix 接続タイプのみがサポートされます。

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

    > [!div class="mx-imgBorder"]
    >![Android デバイス管理者のアプリごとの VPN カスタム ポリシーの例](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>アプリの一覧をブラックリストまたはホワイトリストとして設定する (省略可能)

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
