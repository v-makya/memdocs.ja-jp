---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a807a90cdca18d79e7b92b4efeb56d341da2596
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438725"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>Microsoft Intune 用に開発中 - 2020 年 4 月

お客様の準備と計画をサポートするため、このページでは、開発中でまだリリースされていない Intune UI の更新と機能が一覧表示されます。 このページの情報に加えて: 

- 変更前にお客様による対処が必要であると予測される場合は、Office メッセージ センターに補足の投稿が公開されます。
- 機能の運用が始まると、機能の説明はプレビュー版も一般公開版も、このページから[新機能](whats-new.md)に関するページに移行します。
- このページと[新機能](whats-new.md)に関するページは、定期的に更新されます。 適宜確認してください。
- 戦略的な成果物とタイムラインについては、「[Microsoft 365 のロードマップ](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS)」を参照してください。

> [!NOTE]
> このページには、将来のリリースでの Intune の機能に関する現在の予測が反映されています。 日付と個々の機能は変更される可能性があります。 このページは、開発中のすべての機能を説明しているわけではありません。

**RSS フィード**:ご自身のフィード リーダーに次の URL をコピーして貼り付けることで、このページが更新されたときにわかるようになります。`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>アプリ管理

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Android アプリ構成ポリシーの更新<!-- 6113334  -->
Android アプリ構成ポリシーは、アプリ構成プロファイルを作成する前に、管理者がデバイス登録の種類を選択できるように更新されます。 この機能は、登録の種類 (仕事用プロファイルまたはデバイス所有者) に基づく証明書プロファイルのために追加されます。  リリースされると、次のことが発生します。

- この機能がリリースされる前に作成され、ポリシーに関連付けられている証明書プロファイルがない既存のポリシーは、デバイス登録の種類の既定値が [仕事用プロファイルとデバイス所有者プロファイル] になります。
- この機能がリリースされる前に作成され、関連付けられている証明書プロファイルがある既存のポリシーは、既定値が [仕事用プロファイルのみ] になります。
- 新しいプロファイルが作成され、デバイス登録の種類に [仕事用プロファイルとデバイス所有者プロファイル] が選択されている場合、証明書プロファイルをアプリ構成ポリシーに関連付けることはできません。
- 新しいプロファイルが作成され、[仕事用プロファイルのみ] が選択されている場合は、[デバイスの構成] で作成された仕事用プロファイルの証明書ポリシーを利用できます。
- 新しいプロファイルが作成され、[デバイスの所有者のみ] が選択されている場合は、[デバイスの構成] で作成されたデバイスの所有者の証明書ポリシーを利用できます。

既存のポリシーで、新しい証明書が修復または発行されることはありません。

さらに、仕事用プロファイルとデバイス所有者の両方の登録タイプに対して機能する、Gmail および Nine の電子メール構成プロファイルを追加しています。これには、両方の電子メール構成の種類での証明書プロファイルの使用が含まれます。  仕事用プロファイル用に [デバイスの構成] で作成した Gmail または Nine のポリシーはすべて、デバイスに引き続き適用されるため、アプリ構成ポリシーに移動する必要はありません。

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[アプリ構成ポリシー]** を選択して、アプリ構成ポリシーを検索できます。 アプリ構成ポリシーの詳細については、「[Microsoft Intune 用アプリ構成ポリシー](../apps/app-configuration-policies-overview.md)」を参照してください。

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams が Office 365 Suite for macOS に含まれるようになりました<!-- 5903936  -->
Microsoft エンドポイント マネージャーで Microsoft Office for macOS が割り当てられているユーザーは、既存の Microsoft Office アプリ (Word、Excel、PowerPoint、Outlook、OneNote) に加えて、Microsoft Teams を受け取るようになります。 Intune は、他の Office for macOS アプリがインストールされている既存の Mac デバイスを認識し、次回デバイスが Intune にチェックインするときに Microsoft Teams のインストールを試行します。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[macOS]**  >  **[追加]** の順に選択して、**Office 365 Suite** for macOS を見つけることができます。 詳しくは、「[Microsoft Intune を使用して macOS デバイスに Office 365 を割り当てる](../apps/apps-add-office365-macos.md)」をご覧ください。

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>[カスタマイズ] ペインのグループのターゲット サポート <!-- 4722837  -->
[カスタマイズ] ペインの設定をユーザー グループをターゲットにすることができるようになります。 Intune ポータルで、 **[クライアント アプリ]**  >  **[カスタマイズ]** の順に選択します。 詳細については、「Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法」 (company-portal-app.md) を参照してください。

<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>macOS デバイス用の有線ネットワーク デバイス構成プロファイル<!-- 3508686  -->
有線ネットワークを構成する ( **[デバイス構成]**  >  **[プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[macOS]** > プロファイル タイプの **[ワイヤード (有線) ネットワーク]** ) 新しい macOS デバイス構成プロファイルが使用できるようになります。 この機能を使用して、有線ネットワークを管理する 802.1x プロファイルを作成し、この有線ネットワークを macOS デバイスに展開します。

適用対象:
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>iOS/iPadOS および macOS デバイスで構成プロファイルを作成するときのユーザー インターフェイス エクスペリエンスの向上<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
iOS/iPadOS または macOS デバイス用のプロファイルを作成すると、Endpoint Management 管理センターのエクスペリエンスが更新されます。 この変更は、次のデバイス構成プロファイルに影響します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[iOS]** または **[macOS]** ):

- カスタム: iOS/iPadOS、macOS
- デバイスの機能: iOS/iPadOS、macOS
- デバイスの制限: iOS/iPadOS、macOS
- エンドポイント保護: macOS
- 拡張機能: macOS
- 設定ファイル: macOS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Windows プラットフォーム用のデバイス構成プロファイルの設定と値が更新される<!-- 4091122 -->
Windows プラットフォーム用のデバイス構成プロファイルを作成する場合 ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** > プラットフォームの任意の **Windows** オプション)、一部の設定とその値は CSP とは異なるため、混乱を招く可能性があります。 設定の名前とその値はわかりやすくするために更新されます。

適用対象:

- Windows 10 以降のデバイス構成プロファイル
- Windows Holographic for Business のデバイス構成プロファイル
- Windows 8.1 のデバイス構成プロファイル
- Windows Phone 8.1 のデバイス構成プロファイル

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>macOS 用に Microsoft Defender ATP アプリを構成する  <!-- 5520115  -->
まもなく、Endpoint Protection デバイス構成プロファイルの一部として macOS を実行するデバイス用に、Microsoft Defender ATP アプリの[設定](../protect/endpoint-protection-macos.md)を構成できるようになります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[macOS]** を選択してから "*プロファイルの種類*" として **[Endpoint Protection]** を選ぶ)。 macOS デバイス構成の設定は 8 つになります。 

Defender ATP は macOS 10.13 (High Sierra) 以降でサポートされており、[Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) アプリは、これらの設定が適用された "*後*" にデバイスに展開する必要があります。 設定は、アプリがデプロイされる前にデバイスに送信される必要があります。 macOS のベータ版はサポートされません。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection デバイス構成ポリシーの新しい FileVault 設定<!-- 5459801   -->
[macOS Endpoint Protection](../protect/endpoint-protection-macos.md) テンプレート内の FileVault カテゴリに、次の新しい設定を追加しています: 回復キーを非表示にする ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[macOS]** を選択してから、"*プロファイルの種類*" として **[Endpoint Protection]** を選ぶ)。 この設定により、FileVault 2 の暗号化中は、エンド ユーザーに対して個人用キーが非表示になります。 デバイス ユーザーは、iOS ポータル サイト アプリから、または暗号化された macOS デバイス用のポータル Web サイトから、いつでも自分の個人用回復キーを表示することができます。 個人用回復キーを表示するには、[デバイスの詳細] に移動し、 *[回復キーの取得]* をクリックします。

この設定は、以前に作成されたポリシーでは使用できません。 この設定を利用するように構成するには、FileVault ポリシーを再作成する必要があります。 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>コンプライアンス違反に対するアクションとしてプッシュ通知を送信する <!-- 1733150   -->
iOS および Android プラットフォームに対して、ポータル サイト アプリを通じてアプリのプッシュ通知を送信する、コンプライアンス違反に対する新しいアクションを追加しています。 ユーザーが通知をクリックすると、ポータル サイト アプリが起動し、それがコンプライアンス違反である理由が表示されます。 管理者は、Microsoft Endpoint Manager admin center で、コンプライアンス違反に対してこの新しいアクションを構成できます。これには、 **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシーの作成]** の順に移動して、 *[アクション]* を選択してアプリのプッシュ通知を送信します。

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>マネージド Google Play アプリのプレリリース テスト<!-- 2681933  -->
[アプリのプレリリース テストに Google Play の終了したテスト トラック](https://support.google.com/googleplay/android-developer/answer/3131213)を使用している組織は、Intune でこれらのトラックを管理できるようになります。 テストを実行するために、Google Play の実稼働前のトラックに発行された基幹業務アプリをパイロット グループに選択的に割り当てることができるようになります。 Intune では、アプリに実稼働前のビルド テスト トラックが発行されているかどうかや、そのトラックを AAD ユーザーまたはデバイス グループに割り当てることができるかどうかを確認することもできるようになります。 この機能は、現在サポートされているすべての Android Enterprise シナリオ (仕事用プロファイル、フル マネージド、および専用) で利用できます。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[Android]**  >  **[追加]** を選択して、マネージド Google Play アプリを追加できます。 詳細は、「[Intune で managed Google Play アプリを Android エンタープライズ デバイスに追加する](../apps/apps-add-android-for-work.md)」を参照してください。

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>Android で Outlook の S/MIME 設定を管理する<!-- 6517085   -->
アプリ構成ポリシーを使用して、Android Enterprise を実行するデバイス上で Outlook の S/MIME 設定を管理できるようになります。 また、デバイスのユーザーが Outlook の設定で S/MIME を有効または無効にすることを許可するかどうかも選択できるようになります。 Android 用のアプリ構成ポリシーを使用するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド デバイス]** の順に移動します。

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>iOS/iPadOS デバイスでの SSO および SSO アプリ拡張機能プロファイルの追加オプション<!-- 6504155  -->
iOS/iPadOS デバイスでは、次のことができます。

- SSO プロファイル ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > プラットフォームに **[iOS/iPadOS]** > プロファイルに **[デバイスの機能]** > **[シングル サインオン]** ) で、Kerberos プリンシパル名が SSO プロファイルのセキュリティ アカウント マネージャー (SAM) アカウント名になるように設定します。 
- SSO アプリ拡張機能プロファイル ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > プラットフォームに **[iOS/iPadOS]** > プロファイルに **[デバイスの機能]** > **[シングル サインオン アプリの拡張機能]** ) で、新しい SSO アプリ拡張機能の種類を使用して、より少ないクリック回数で iOS/iPadOS Microsoft Azure AD 拡張機能を構成します。 共有デバイスに Azure AD 拡張機能を有効にし、拡張機能固有のデータを拡張機能に送信できます。

適用対象:
- iOS/iPadOS 13.0 以降

iOS/iPadOS デバイスでのシングル サインオンの使用に関する詳細については、[シングル サインオン アプリの拡張機能の概要](../configuration/device-features-configure.md#single-sign-on-app-extension)と[シングル サインオンの設定リスト](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)を参照してください。

<!-- ***********************************************-->
## <a name="device-enrollment"></a>デバイスの登録

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>個人所有デバイスでは、VPN を使用して展開できる<!--5015344 -->
新しいオートパイロット プロファイル **[ドメインの接続チェックをスキップする]** 切り替えを使用すると、社内のネットワークにアクセスせずに、独自のサードパーティ製の Win32 VPN クライアントを使用して、Hybrid Azure AD Join デバイスを展開できます。 新しい切り替えを表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**   >  **[Windows]**  >  **[Windows 登録]**  >  **[展開プロファイル]**  >  **[プロファイルの作成]**  >  **[Out-of-box experience (OOBE)]** の順に移動します。

<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="script-support-for-macos-devices---4280361----"></a>macOS デバイスのスクリプト サポート<!-- 4280361  -->
macOS デバイスにスクリプトを追加してデプロイできるようになります。 このサポートにより、macOS デバイスを構成する機能が拡張され、macOS デバイスでネイティブの MDM 機能を使用してできること以上のことが可能になります。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics には、デバイスの詳細ログが含まれる<!--6014987  -->
Intune デバイスの詳細ログは、 **[レポート]**  >  **[ログ分析]** で入手できます。 デバイスの詳細を相互に関連付けて、カスタム クエリと Azure ブックを作成することができます。

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>デバイスの所有権の種類が変更されたときのプッシュ通知<!-- 5575875  -->
Android と iOS の両方のポータル サイト ユーザーに、自身のデバイスの所有権の種類が個人用からから企業に変更されている場合に、プライバシーを尊重するため、プッシュ通知を送信するように構成できるようになります。 この設定は、Microsoft エンドポイント マネージャーで **[テナント管理]**  >  **[カスタマイズ]** を選択すると見つかります。 デバイスの所有権がエンドユーザーに与える影響の詳細については、「[デバイス所有権を変更する](../enrollment/corporate-identifiers-add.md#change-device-ownership)」を参照してください。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>セキュリティ

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Android フル マネージド デバイスでの派生資格情報のサポート<!--4839592-->
Android Enterprise の完全に管理されたデバイスで、派生資格情報を使用できるようになります。 Entrust Datacard、Intercede、および DISA Purebred の派生資格情報を取得するためのサポートが追加されます。 アプリ認証、Wi-Fi、VPN、または S/MIME 署名や、それをサポートするアプリでの暗号化に、派生資格情報を使用できるようになります。

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>macOS デバイス用のプライバシーの基本設定<!-- 2934232 --> 
macOS Catalina 10.15 のリリースでは、Apple によって新しいセキュリティとプライバシーの強化が加えられました。 既定では、アプリケーションとプロセスで、ユーザーの同意なしで特定のデータにアクセスすることはできません。 ユーザーが同意しない場合、アプリケーションとプロセスが機能しなくなる可能性があります。 Intune では、macOS 10.14 以降を実行しているデバイスでエンドユーザーに代わって、IT 管理者がデータ アクセスの同意を許可または許可しないようにできる設定のサポートを追加しています。 これらの設定により、アプリケーションとプロセスは引き続き正常に機能し、エンドユーザーに示されるプロンプトの数が減ります。

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Windows 10 の Endpoint Protection プロファイル設定の UI テキストとラベルの更新<!-- 5983747 -->
Windows 10 デバイス構成プロファイルとして構成するさまざまな設定のテキストを更新して、使用する設定と結果を理解しやすくしています。

更新している設定には、次の Windows 10 デバイス構成プロファイルが含まれます。

- [デバイスの制限](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Microsoft Defender ウイルス対策  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender ウイルス対策

Intune でサポートされている設定は変更されません。 これは、Microsoft Endpoint Management 管理センターの UI テキストに対する更新のみです。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。



