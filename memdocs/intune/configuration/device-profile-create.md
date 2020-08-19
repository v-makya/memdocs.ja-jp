---
title: Microsoft Intune - Azure でのデバイス プロファイルの作成 | Microsoft Docs
description: Microsoft Intune でデバイス構成プロファイルを追加または構成します。 プラットフォームの種類を選択し、設定を構成し、スコープのタグを追加します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bd1cb0445ceb4c9434b93949973125422aa1df19
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146424"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>Microsoft Intune でのデバイス プロファイルの作成

デバイス プロファイルでは、設定を追加および構成してから、組織内のデバイスにこれらの設定をプッシュすることができます。 可能な操作を含め、詳細については、[デバイス プロファイルを使用してデバイスに機能と設定を適用する](device-profiles.md)方法に関するページを参照してください。

この記事の内容:

- プロファイルを作成する手順を示します。
- プロファイルを "フィルター処理" するためにスコープのタグを追加する方法を示します。
- Windows 10 デバイスに対する適用性ルールについて説明し、ルールを作成する方法を示します。
- デバイスでプロファイルおよびプロファイルの更新を受信した際のチェックインの更新サイクル時間を示します。

## <a name="create-the-profile"></a>プロファイルの作成

プロファイルは、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で作成されます。 この管理センターで、 **[デバイス]** を選択します。 次のオプションがあります。

- **概要**:プロファイルの状態を一覧表示し、ユーザーとデバイスに割り当てたプロファイルに関する追加の詳細を提供します。
- **監視**:プロファイルの状態が成功か失敗かを確認し、プロファイルのログも表示します。
- **プラットフォーム別**: プラットフォーム別にポリシーとプロファイルを作成して表示します。 このビューには、プラットフォームに固有の機能が表示される場合もあります。 たとえば、 **[Windows]** を選択します。 **Windows 10 更新リング**や **PowerShell スクリプト**など、Windows 固有の機能が表示されます。
- **ポリシー**: デバイス プロファイルを作成し、カスタムの [PowerShell スクリプト](../apps/intune-management-extension.md)をアップロードしてデバイス上で実行し、[eSIM](esim-device-configuration.md) を使用してデバイスにデータ プランを追加します。

プロファイルを作成する場合 ( **[構成プロファイル]**  >  **[プロファイルの作成]** )、ご利用のプラットフォームを選択します。

- **Android デバイス管理者**
- **Android エンタープライズ**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 以降**
- **Windows 8.1 以降**

次に、プロファイルの種類を選択します。 選択したプラットフォームによって構成できる設定が異なります。 次の記事では、さまざまなファイルの種類の設定について説明します。

- [管理用テンプレート (Windows)](administrative-templates-windows.md)
- [カスタム](custom-settings-configure.md)
- [配信の最適化 (Windows)](delivery-optimization-windows.md)
- [派生資格情報 (Android エンタープライズ、iOS、iPadOS)](../protect/derived-credentials.md)
- [デバイスの機能 (macOS、iOS、iPadOS)](device-features-configure.md)
- [デバイスのファームウェア (Windows)](device-firmware-configuration-interface-windows.md)
- [デバイスの制限](device-restrictions-configure.md)
- [ドメイン参加 (Windows)](domain-join-configure.md)
- [エディションのアップグレードとモードの切り替え (Windows)](edition-upgrade-configure-windows-10.md)
- [教育 (iOS、iPadOS)](../fundamentals/education-settings-configure-ios.md)
- [電子メール](email-settings-configure.md)
- [Endpoint Protection (macOS、Windows)](../protect/endpoint-protection-configure.md)
- [拡張機能 (macOS)](kernel-extensions-overview-macos.md)
- [ID 保護 (Windows)](../protect/identity-protection-configure.md)
- [キオスク](kiosk-settings.md)
- [Microsoft Defender ATP (Windows)](../protect/advanced-threat-protection.md)
- [モビリティ拡張 (MX) プロファイル (Android デバイス管理者)](android-zebra-mx-overview.md)
- [OEMConfig (Android エンタープライズ)](android-oem-configuration-overview.md)
- [PKCS 証明書](../protect/certficates-pfx-configure.md)
- [PKCS のインポートされた証明書](../protect/certificates-imported-pfx-configure.md)
- [設定ファイル (macOS)](preference-file-settings-macos.md)
- [SCEP 証明書](../protect/certificates-scep-configure.md)
- [セキュリティで保護された評価 (教育) (Windows)](education-settings-configure.md)
- [共有のマルチユーザーのデバイス (Windows)](shared-user-device-settings.md)
- [通信費 (Android デバイス管理者、iOS、iPadOS)](telecom-expenses-monitor.md)
- [信頼された証明書](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)
- [有線ネットワーク (macOS)](wired-network-settings-macos.md)

たとえば、プラットフォームとして **iOS/iPadOS** を選択した場合、プロファイルのオプションは次のプロファイルのようになります。

:::image type="content" source="./media/device-profile-create/create-device-profile.png" alt-text="Microsoft Intune で iOS/iPadOS プロファイルを作成します。":::

## <a name="scope-tags"></a>スコープのタグ

設定を追加したら、プロファイルにスコープのタグを追加することもできます。 スコープ タグを使うと、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理することができます。 また、分散 IT で使用されます。

スコープのタグと可能な操作の詳細については、[分散 IT での RBAC とスコープのタグの使用](../fundamentals/scope-tags.md)に関するページを参照してください。

## <a name="applicability-rules"></a>適用性ルール

適用対象:

- Windows 10 以降

管理者は、適用性ルールを使用して、グループの特定の条件を満たすデバイスを対象にすることができます。 たとえば、**すべての Windows 10 デバイス** グループに適用されるデバイス制限プロファイルを作成します。 また、Windows 10 Enterprise を実行しているデバイスにのみプロファイルを割り当てことができます。

これを行うには、**適用性ルール**を作成します。 これらのルールは、次のシナリオに最適です。

- Windows 10 Education (EDU) を使用しています。 Bellows College では、RS3 から RS4 までのすべての Windows 10 EDU デバイスを対象にする必要があります。
- Contoso では、人事部のすべてのユーザーを対象にし、さらに Windows 10 Professional または Enterprise デバイスのみを対象にする必要があります。

これらのシナリオに取り組むには:

- Bellows College のすべてのデバイスを含むデバイス グループを作成します。 プロファイルに、OS の最小バージョンが `16299` であり、最大バージョンが `17134` である場合に適用される適用性ルールを追加します。 このプロファイルを Bellows College デバイス グループに割り当てます。

  割り当てられると、入力した最小バージョンから最大バージョンまでのデバイスに対してプロファイルが適用されます。 入力した最小バージョンから最大バージョンまでに含まれないデバイスの場合、その状態は **[適用なし]** と表示されます。

- Contoso の人事部 (HR) のすべてのユーザーを含むユーザー グループを作成します。 プロファイルに、Windows 10 Professional または Enterprise を実行しているデバイスに適用される適用性ルールを追加します。 このプロファイルを HR ユーザー グループに割り当てます。

  割り当てられると、Windows 10 Professional または Enterprise を実行しているデバイスに対してプロファイルが適用されます。 これらのエディションを実行していないデバイスの場合、その状態は **[適用なし]** と表示されます。

- まったく同じ設定のプロファイルが 2 つある場合は、適用性ルールが含まれていないプロファイルが適用されます。 

  たとえば、ProfileA では Windows 10 デバイス グループを対象とし、BitLocker が有効ですが、適用性ルールは含まれていません。 ProfileB では同じ Windows 10 デバイス グループを対象とし、BitLocker が有効であり、Windows 10 Enterprise にのみプロファイルを適用するという適用性ルールが含まれています。

  両方のプロファイルが割り当てられた場合、適用性ルールがないため、ProfileA が適用されます。 

プロファイルをグループに割り当てると、適用性ルールはフィルターとして機能し、条件を満たすデバイスのみが対象になります。

### <a name="add-a-rule"></a>ルールを追加する

1. **[適用性ルール]** を選択します。 次のように **[ルール]** と **[プロパティ]** を選択できます。

    :::image type="content" source="./media/device-profile-create/applicability-rules.png" alt-text="Microsoft Intune で Windows 10 のデバイス構成プロファイルに適用性ルールを追加します。":::

2. **[ルール]** で、ユーザーまたはグループを含めるか除外するかを選択します。 次のようなオプションがあります。

    - **プロファイルを割り当てる条件**:入力した条件を満たすユーザーまたはグループを含めます。
    - **プロファイルを割り当てない条件**:入力した条件を満たすユーザーまたはグループを除外します。

3. **[プロパティ]** で、フィルターを選択します。 次のようなオプションがあります。 

    - **OS のエディション**:一覧で、ルールに含める (または除外する) Windows 10 のエディションをオンにします。
    - **OS のバージョン**:ルールに含める (または除外する) Windows 10 の**最小**および**最大**のバージョン番号を入力します。 両方の値が必要です。

      たとえば、最小バージョンには `10.0.16299.0` (RS3 または 1709) を、最大バージョンには `10.0.17134.0` (RS4 または 1803) を入力できます。 または、さらに細かい設定が可能であり、最小バージョンとして `10.0.16299.001` を、最大バージョンとして `10.0.17134.319` を入力できます。

4. **[追加]** を選択して変更を保存します。

## <a name="refresh-cycle-times"></a>サイクル時間の更新

Intune では、複数の更新サイクルを使用して、構成プロファイルへの更新が確認されます。 登録してすぐのデバイスでは、チェックインの実行頻度が高くなります。 「[ポリシーとプロファイルの更新サイクル](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)に、おおよその更新間隔が一覧表示されています。

ユーザーはいつでもポータル サイト アプリを起動し、デバイスを同期して、プロファイルの更新をすぐに確認できます。

## <a name="recommendations"></a>推奨事項

プロファイルを作成するとき、次の推奨設定を考慮してください。

- それが何であり、何をするものなのかわかるようにポリシーに名前を付けます。 [コンプライアンス ポリシー](../protect/create-compliance-policy.md)と[構成プロファイル](../configuration/device-profile-create.md)にはすべて、省略可能な **[説明]** プロパティがあります。 **[説明]** には、ポリシーの内容を他のユーザーが理解できるよう、具体的な情報を入力します。

  いくつかの構成プロファイルの例を次に示します。

  **プロファイル名**:管理者テンプレート - Windows 10 の全ユーザー用の OneDrive 構成プロファイル  
  **プロファイルの説明**:Windows 10 の全ユーザー用の最小設定と基本設定が含まれる OneDrive 管理者テンプレート プロファイル。 ユーザーが組織データを個人 OneDrive アカウントと共有することを禁止する目的で user@contoso.com により作成されます。

  **プロファイル名**:iOS/iPadOS の全ユーザー用の VPN プロファイル  
  **プロファイルの説明**:すべての iOS/iPadOS ユーザーが Contoso VPN に接続するための最小設定と基本設定が含まれる VPN プロファイル。 ユーザー名とパスワードをユーザーに求めず、ユーザーが VPN で自動的に認証されるよう、user@contoso.com によって作成されます。

- Microsoft Edge 設定を構成する、Microsoft Defender のウイルス対策設定を有効にする、iOS/iPadOS 脱獄デバイスをブロックするなど、そのタスク別にプロファイルを作成します。

- マーケティング、販売、IT 管理者などの特定のグループに適用されるプロファイルや、場所や学校のシステム別に適用されるプロファイルを作成します。

- ユーザー ポリシーとデバイス ポリシーを分離します。

  たとえば、[Intune の管理テンプレート](administrative-templates-windows.md)には、数千の ADMX 設定があります。 これらのテンプレートには、設定がユーザーに適用されるのか、デバイスに適用されるのかが示されます。 管理テンプレートを作成するときは、ユーザー設定をユーザー グループに割り当て、デバイス設定をデバイス グループに割り当てます。

  次の画像は、ユーザーとデバイスに適用できる設定の例です。

  :::image type="content" source="./media/device-profile-create/setting-applies-to-user-and-device.png" alt-text="ユーザーとデバイスに適用される Intune 管理テンプレート。":::

- 制限の厳しいポリシーを作成するたびに、この変更についてユーザーに伝えます。 たとえば、パスコードの要件を 4 文字から 6 文字に変更する場合、ポリシーを割り当てる前にユーザーに通知できます。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。
