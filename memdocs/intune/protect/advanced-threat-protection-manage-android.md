---
title: Microsoft Intune で Microsoft Defender ATP の Android デバイス用 Web 保護を管理する - Azure | Microsoft Docs
description: Intune で Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) の Android 用 Web 保護を構成します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49423d1d1b887aaf3ed3323ff36678bb7319b1ad
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909467"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>Intune で管理する Android デバイスに対して Microsoft Defender ATP を構成する

Microsoft Intune と Microsoft Defender Advanced Threat Protection (ATP) を統合する場合、デバイス構成プロファイルを使用して、Android デバイスに対する Microsoft Defender ATP の設定の一部を変更することができます。

先に進む前に、適切に [Intune で Microsoft Defender ATP を構成](../protect/advanced-threat-protection-configure.md)し、Microsoft Defender ATP に Android デバイスをオンボードする必要があります。

## <a name="configure-web-protection-on-devices-that-run-android"></a>Android を実行するデバイスで Web 保護を構成する

既定では、Android 用 Microsoft Defender ATP には Web 保護機能が含まれており、有効になります。 [Web 保護](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview)は、Web の脅威からデバイスを保護し、フィッシング攻撃からユーザーを保護するのに役立ちます。

既定では有効になっていますが、一部の Android デバイスでこの保護を無効にする正当な理由があります。 たとえば、Microsoft Defender ATP アプリ スキャン機能のみを使用するか、Web 保護で有害な URL をスキャンするときに VPN を使用しないようにするかを選択できます。

Intune では、Web 保護機能のすべてまたは一部をオフにすることがサポートされます。 使用する方法と無効にできる機能は、Android デバイスが Intune に登録されている方法によって異なります。

- **Android デバイス管理者**: 構成プロファイルを使用して、Web 保護機能全体を無効にするか、VPN の使用のみを無効にするためにデバイスで OMA-URI のカスタム設定を指定します。 Android デバイスのカスタム設定に関する一般的な情報については、[カスタム設定](../configuration/custom-settings-android.md)に関するページを参照してください。

- **Android Enterprise 仕事用プロファイル**: アプリ構成プロファイルと "*構成デザイナー*" を使用して、Web 保護を無効にします。 この方法と登録の種類では、すべての Web 保護機能の無効化がサポートされますが、VPN の使用のみの無効化はサポートされません。 アプリ構成ポリシーに関する一般的な情報については、「[構成デザイナーを使用する](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer)」を参照してください。

デバイスで Web 保護を構成するには、次の手順を使用し、該当する構成を作成して展開します。

### <a name="disable-web-protection-for-android-device-administrator"></a>Android デバイス管理者の Web 保護を無効にする

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. 次の設定を入力します。

   - **[プラットフォーム]** : **[Android デバイス管理者]** を選択します
   - **[プロファイル]** : **[カスタム]** を選択します

   **[作成]** を選択します。

4. **[基本]** で、次の詳細を入力します。

   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、"*Microsoft Defender ATP Web 保護用の Android カスタム プロファイル*" などとします
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

5. **[構成設定]** で、 **[追加]** を選択します。

   展開する構成の設定を指定します。

   - **Web 保護を無効にする**:
     - **名前**:簡単に見つけられるように、この OMA-URI 設定の一意の名前を入力します。 たとえば、"*Microsoft Defender ATP Web 保護を無効にする*" などとします
     - **説明**:(省略可能) 設定の概要および他の重要な詳細を示す説明を入力します。
     - **OMA-URI**:「 **./Vendor/MSFT/DefenderATP/AntiPhishing**」と入力します
     - **[データ型]** :ドロップダウンを使用して、 **[整数]** を選択します
     - **値**:VPN ベースのスキャンを含め、Web 保護を無効にするには「**0**」と入力します。
       > [!NOTE]
       > Web 保護を有効にするには、「**1**」と入力します。これは、Web 保護の既定値です。

   - **Web 保護での VPN の使用のみを無効にする**:
     - **名前**:簡単に見つけられるように、この OMA-URI 設定の一意の名前を入力します。 たとえば、"*Microsoft Defender ATP Web 保護の VPN を無効にする*" などとします
     - **説明**:(省略可能) 設定の概要および他の重要な詳細を示す説明を入力します。
     - **OMA-URI**:「 **./Vendor/MSFT/DefenderATP/Vpn**」と入力します
     - **[データ型]** :ドロップダウンを使用して、 **[整数]** を選択します
     - **値**:VPN ベースのスキャンを無効にするには、「**0**」と入力します。
       > [!NOTE]
       > Web 保護を有効にするには、「**1**」と入力します。これは、Web 保護の既定値です。

   **[追加]** を選択して OMA-URI 設定の構成を保存し、 **[次へ]** を選んで続行します。

6. **[割り当て]** で、このプロファイルを受け取るグループを指定します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

7. **[確認および作成]** で、完了したら、 **[作成]** を選択します。 作成したプロファイルのポリシーの種類を選択すると、新しいプロファイルが一覧に表示されます。

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Android Enterprise 仕事用プロファイルの Web 保護を無効にする

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]** の順に選択してから、マネージド デバイスを選びます。

3. **[基本]** で、次の詳細を入力します。

   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、"*Microsoft Defender ATP Web 保護用の Android アプリ構成*" などとします。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
   - **[プラットフォーム]** : **[Android Enterprise]** を選択します
   - **[プロファイルの種類]** : **[仕事用プロファイルのみ]** を選択します
   - **対象アプリ**: **[アプリの選択]** をクリックします。

4. **[関連アプリ]** で、 **[Defender ATP]** を見つけて選択し、 **[OK]**  >  **[次へ]** の順に選びます。

5. **[設定]** で、 **[構成設定の形式]** のドロップダウンを使用し、 **[構成デザイナーを使用する]** を選択してから **[追加]** をクリックします。 JSON エディターが開きます。

6. **[Web 保護]** を見つけて選択し、 **[OK]** を選んで **[設定]** ページに戻ります。

7. **[構成値]** では、「**0**」と入力して Web 保護を無効にします。

   > [!NOTE]
   > Web 保護を有効にするには、「**1**」と入力します。これは、Web 保護の既定値です。

   **[次へ]** を選択して続行します。

8. **[割り当て]** で、このプロファイルを受け取るグループを指定します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

9. **[確認および作成]** で、完了したら、 **[作成]** を選択します。 作成したプロファイルのポリシーの種類を選択すると、新しいプロファイルが一覧に表示されます。

## <a name="next-steps"></a>次のステップ

- [リスク レベルのコンプライアンスを監視する](../protect/advanced-threat-protection-monitor.md)
- [ATP の脆弱性の管理を使用したセキュリティ タスクを使ってデバイスの問題を修復する](../protect/atp-manage-vulnerabilities.md)

Microsoft Defender ATP のドキュメントで詳細を確認します。

- [Microsoft Defender ATP の条件付きアクセス](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP のリスク ダッシュボード](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)