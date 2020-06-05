---
title: Microsoft Intune で HoloLens 2 デバイスに Windows Defender アプリケーション制御を使用する - Azure | Microsoft Docs
description: HoloLens 2 デバイスでアプリを開くことを許可またはブロックするために Microsoft Intune で Windows Defender アプリケーション制御 (WDAC) CSP を構成します。 PowerShell とカスタム構成プロファイルを使用します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d2d19b03253725bde7b0ee27f3c94b42adb5917
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990131"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>WDAC と Windows PowerShell を使用して、Microsoft Intune で HoloLens 2 デバイスのアプリを許可またはブロックする

Microsoft HoloLens 2 デバイスでは、[Windows Defender アプリケーション制御 (WDAC) CSP](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp) をサポートしています。これは、[AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp) に代わるものです。

Windows PowerShell と Microsoft Intune を使用している場合は、WDAC CSP を使用して、Microsoft HoloLens 2 デバイスで特定のアプリを開くことを許可またはブロックできます。 たとえば、組織内の HoloLens 2 デバイスで Cortana アプリを開くことを許可または禁止することができます。

この機能は、以下に適用されます。

- Windows Holographic for Business が実行されている HoloLens 2 デバイス

WDAC CSP は、[Windows Defender アプリケーション制御 (WDAC) 機能](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)に基づいています。 [複数の WDAC ポリシーを使用する](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies)こともできます。

この記事では、以下の方法を示します。

1. Windows PowerShell を使用して WDAC ポリシーを作成します。
2. Windows PowerShell を使用して WDAC ポリシーの規則を XML に変換し、その XML を更新した後、その XML をバイナリ ファイルに変換します。
3. Microsoft Intune で、[カスタム デバイス構成プロファイル](custom-settings-windows-holographic.md)を作成し、この WDAC ポリシー バイナリ ファイルを追加して、ポリシーを HoloLens 2 デバイスに適用します。

Intune では、Windows Defender アプリケーション制御 (WDAC) CSP を使用するためにカスタム構成プロファイルを作成する必要があります。 

この記事の手順をテンプレートとして使用すると、HoloLens 2 デバイスで特定のアプリを開くことを許可または拒否できます。

## <a name="prerequisites"></a>[前提条件]

- Windows PowerShell に精通している。
- 次のメンバーとして Intune にサインインする。

  - **ポリシーおよびプロファイルマネージャー**または **Intune ロール管理者**の Intune ロール

    または

  - **全体管理者**または **Intune サービス管理者**の Azure AD ロール

  詳細については、[Intune でのロールベースのアクセス制御 (RBAC)](../fundamentals/role-based-access-control.md)に関する記事を参照してください。

- お使いの HoloLens 2 デバイスでユーザー グループまたはデバイス グループを作成する。 詳細については、「[ユーザー グループとデバイス グループ](device-profile-assign.md#user-groups-vs-device-groups)」を参照してください。

## <a name="example"></a>例

この例では、Windows PowerShell を使用して、Windows Defender アプリケーション制御 (WDAC) ポリシーを作成します。 このポリシーにより、特定のアプリを開くことができなくなります。 その後、Intune を使用してこのポリシーを HoloLens 2 デバイスに展開します。

1. デスクトップ コンピューターで、**Windows PowerShell** アプリを開きます。
2. デスクトップ コンピューターにインストールされているアプリケーション パッケージに関する情報を取得します。

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    たとえば、次のように入力します。

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    次に、パッケージにアプリケーション属性があることを確認します。

    ```powershell
    $package1
    ```

    次のアプリの詳細のように属性が表示されます。

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. WDAC ポリシーを作成し、このアプリ パッケージを拒否規則に追加します。

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. 拒否したいアプリケーションが他にもある場合は、手順 2 と 3 を繰り返します。

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    たとえば、次のように入力します。

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. WDAC ポリシーを **newPolicy.xml** に変換します。

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    アプリのすべてのバージョンを対象にするには、newPolicy.xml で、`PackageVersion="65535.65535.65535.65535"` が Deny ノードに含まれていることを確認します。

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    `PackageFamilyNameRules` では、次のバージョンを使用できます。

    - **[許可]** :「`PackageVersion, 0.0.0.0`」と入力します。これは、"このバージョン以上を許可すること" を意味します。
    - **Deny**: 「`PackageVersion, 65535.65535.65535.65535`」と入力します。これは、"このバージョン以下を拒否すること" を意味します。

6. **newPolicy.xml** を、デスクトップ コンピューター上にある既定のポリシーとマージします。 この手順によって **mergedPolicy.xml** が作成されます。 たとえば、Windows、WHQL 署名されたドライバー、ストアで署名されたアプリの実行を許可します。

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. **mergedPolicy.xml** で**監査モード**規則を無効にします。 マージすると、監査モードが自動的に有効になります。

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. **mergedPolicy.xml** で**再起動時に EA を無効化**規則を有効にします。

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    これらの規則の詳細については、「[WDAC ポリシー規則とファイル規則について](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create)」を参照してください。

9. **mergedPolicy.xml** をバイナリ形式に変換します。 この手順によって **compiledPolicy.bin** が作成されます。 この **compiledPolicy.bin** バイナリ ファイルを Intune に追加します。

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Intune でカスタム デバイス構成プロファイルを作成します。

    1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、Windows 10 のカスタム デバイス構成プロファイルを作成します。

        具体的な手順については、[Intune での OMA-URI を使用したカスタム プロファイルの作成](custom-settings-configure.md)に関する記事を参照してください。

    2. プロファイルを作成する際は、次の設定を入力します。

      - **OMA-URI**:「`./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`」と入力します。 `<PolicyGUID>` は、手順 6 で作成した **mergedPolicy.xml** ファイルの PolicyTypeID ノードに置き換えます。

        この例を使用する場合は、「`./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076`」と入力します。

        このポリシー GUID は、(手順 6 で作成された) **mergedPolicy.xml** ファイルの PolicyTypeID ノードと**一致する必要があります**。

      - **[データ型]** : **[Base64 (ファイル)]** に設定します。 これで、ファイルは自動的にバイナリから Base64 に変換されます。
      - **証明書ファイル**: (手順 9 で作成された) **compiledPolicy.bin** バイナリ ファイルをアップロードします。

      設定は次のようになります。

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Microsoft Intune でカスタム OMA-URI を追加してアプリケーション制御 CSP を構成します。":::

11. プロファイルが HoloLens 2 グループに[割り当てられている](device-profile-assign.md)場合は、プロファイルの状態を確認します。 プロファイルが正常に適用されたら、HoloLens 2 デバイスを再起動します。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視する](device-profile-monitor.md)。

[Intune のカスタム プロファイルの詳細を確認する](custom-settings-configure.md)。
