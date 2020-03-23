---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e5c7ce18cc00934438e945933188d9634b36653
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79362317"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>Microsoft Intune 用に開発中 - 2020 年 3 月

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

### <a name="retarget-web-clips-to-microsoft-edge-on-iosipados-devices---5455276---"></a>iOS/iPadOS デバイス上の Microsoft Edge に Web クリップを再ターゲットする<!-- 5455276 -->
iOS/iPadOS デバイス上でピン留めされた Web アプリとして機能する Web クリップを更新する必要があります。 新しく展開された Web クリップを保護されたブラウザーで開く必要がある場合は、Intune Managed Browser ではなく Microsoft Edge で開きます。 既存の Web クリップを再ターゲットして、Managed Browser ではなく Microsoft Edge で開くようにする必要があります。

### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>macOS および iOS ポータル サイトの更新<!-- 5779439, 5780234  -->
macOS および iOS ポータル サイトの [プロファイル] ペインが更新され、サインアウト ボタンが含まれるようになります。 さらに、この更新には、macOS ポータル サイトの [プロファイル] ペインに対する UI の機能強化が含まれます。 ポータル サイトの詳細については、「[Microsoft Intune ポータル サイト アプリを構成する方法](../apps/company-portal-app.md)」をご覧ください。

### <a name="updates-to-branding-and-customization-pane---5236032---"></a>[ブランド化とカスタマイズ] ペインの更新<!-- 5236032 -->
現在は "ブランド化とカスタマイズ" という名前の Intune ペインを更新しています。これには、次のような機能強化が含まれます。

- ペインの名前を**カスタマイズ**に変更。
- 設定の編成と設計の改善。
- 設定のテキストとヒントの改善。

Intune でこれらの設定を見つけるには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に移動し、 **[テナント管理]**  >  **[カスタマイズ]** の順に選択します。 既存のカスタマイズについては、「[Microsoft Intune ポータル サイト アプリを構成する方法](../apps/company-portal-app.md)」を参照してください。

### <a name="configure-the-ios-microsoft-azure-ad-sso-app-extension---567534----"></a>iOS の Microsoft Azure AD SSO アプリ拡張機能を構成する<!-- 567534  -->
Microsoft Azure AD チームでは、iOS および iPadOS 13.0 以降のユーザーが、1 回のサインオンで Microsoft アプリと Web サイトにシームレスにアクセスできるようにするために、リダイレクト シングル サインオン (SSO) アプリ拡張機能を開発しています。 AAD SSO アプリ拡張機能がリリースされると、管理コンソールで最小限のクリックで **[デバイス機能]**  >  **[シングル サインオン アプリ拡張機能]** プロファイルを使用して、SSO 拡張機能を構成できるようになります。

iOS SSO アプリ拡張機能やデバイス機能の構成方法について詳しくは、「[シングル サインオン アプリ拡張機能](../configuration/device-features-configure.md#single-sign-on-app-extension)」をご覧ください。

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>横向きモードをサポートするための iOS 用ポータル サイト<!--6048329  -->
ユーザーは自分のデバイスを登録し、アプリを検索し、選択した画面の向きを使用して IT サポートを受けることができます。 ユーザーが縦向きモードで画面をロックしない限り、アプリでは画面を縦向きまたは横向きモードに合わせて自動的に検出して調整します。

### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128-idready-idstaged---"></a>Android と iOS 用のポータル サイトで登録を使用できるようにするかどうかを構成する<!-- 4260128 idready idstaged -->
新しい設定を使用できるようになります。これにより、Android および iOS デバイス上のポータル サイトでのデバイス登録を、プロンプトを表示して、またはプロンプトを表示せずに使用できるようにするか、あるいはユーザーが使用できないようにするかを構成できます。 Intune でこれらの設定を見つけるには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に移動し、 **[テナント管理]**  >  **[カスタマイズ]**  >  **[編集]**  >  **[デバイスの登録]** の順に選択します。 既存のポータル サイトのカスタマイズについては、「[Microsoft Intune ポータル サイト アプリを構成する方法](../apps/company-portal-app.md)」を参照してください。

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Android 用ポータル サイトでのサインイン エクスペリエンスの向上<!-- 6103997  -->
エクスペリエンスをユーザーにとってより新しく、シンプルでクリーンなものにするために、Android 用ポータル サイト アプリのいくつかのサインイン画面のレイアウトを更新しています。

<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>macOS デバイス用の有線ネットワーク デバイス構成プロファイル<!-- 3508686  -->
有線ネットワークを構成する ( **[デバイス構成]**  >  **[プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[macOS]** > プロファイル タイプの **[ワイヤード (有線) ネットワーク]** ) 新しい macOS デバイス構成プロファイルが使用できるようになります。 この機能を使用して、有線ネットワークを管理する 802.1x プロファイルを作成し、この有線ネットワークを macOS デバイスに展開します。

適用対象:
- macOS

### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices----1947932----"></a>IKEv2 VPN 接続を使用する VPN プロファイルでは iOS/iPadOS デバイスで常時接続を使用できる <!-- 1947932  -->
iOS/iPadOS デバイスでは、IKEv2 接続を使用する VPN プロファイルを作成することができます ( **[デバイス構成]**  >  **[プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[iOS/iPadOS]** > プロファイル タイプの **[VPN]** )。 今後の更新では、IKEv2 を使用して常時接続を構成することができます。 構成すると、IKEv2 VPN プロファイルは自動的に接続され、VPN に接続されたままになります (またはすぐに再接続されます)。 ネットワーク間を移動したり、デバイスを再起動したりしても、接続されたままになります。

iOS/iPadOS では、常時接続 VPN は IKEv2 プロファイルに限定されます。

現在構成できる IKEv2 設定については、「[Microsoft Intune で iOS/iPadOS デバイス向けの VPN 設定を追加する](../configuration/vpn-settings-ios.md#ikev2-settings)」を参照してください。

適用対象:
- iOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>iOS/iPadOS および macOS デバイスで構成プロファイルを作成するときのユーザー インターフェイス エクスペリエンスの向上<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
iOS/iPadOS または macOS デバイス用のプロファイルを作成すると、Endpoint Management 管理センターのエクスペリエンスが更新されます。 この変更は、次のデバイス構成プロファイルに影響します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[iOS]** または **[macOS]** ):

- カスタム: iOS/iPadOS、macOS
- デバイスの機能: iOS/iPadOS、macOS
- デバイスの制限: iOS/iPadOS、macOS
- エンドポイント保護: macOS
- 拡張機能: macOS
- 設定ファイル: macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Android Enterprise デバイスで OEMConfig 構成プロファイルを作成するときのユーザー インターフェイス エクスペリエンスの向上<!-- 5568645   -->
Android Enterprise デバイスで OEMConfig プロファイルを作成または編集すると、Endpoint Management 管理センターのエクスペリエンスが更新されます。 更新されたエクスペリエンスによって、構成した設定の概要が表示されます。 この変更は、OEMConfig デバイス構成プロファイルに影響します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[Android Enterprise]** > プロファイルの種類の **[OEMConfig]** )。

この機能は、以下に適用されます。
- Android エンタープライズ 

### <a name="enterprise-app-trust-settings-modification-setting-will-be-removed-from-iosipados-device-restriction-profiles---6225131----"></a>[エンタープライズ アプリの信頼設定の変更] 設定が iOS/iPadOS デバイスの制限プロファイルから削除される<!-- 6225131  -->
iOS/iPadOS デバイス上に、デバイスの制限プロファイルを作成します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > プラットフォームとして **[iOS/iPadOS]** > プロファイルの種類として **[デバイスの制限]** )。 **[エンタープライズ アプリの信頼設定の変更]** 設定は、Apple によって削除され、Intune から削除されます。 プロファイルでこの設定を現在使用している場合、影響はありません。新しいプロファイルを作成するまでプロファイルに保持されます。 この設定は、Intune のレポートからも削除されます。

適用対象:
- iOS/iPadOS

制限できる設定を確認するには、[機能を許可または制限するための iOS および iPadOS デバイスの設定](../configuration/device-restrictions-ios.md)に関するページに移動します。

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Windows プラットフォーム用のデバイス構成プロファイルの設定と値が更新される<!-- 4091122 -->
Windows プラットフォーム用のデバイス構成プロファイルを作成する場合 ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** > プラットフォームの任意の **Windows** オプション)、一部の設定とその値は CSP とは異なるため、混乱を招く可能性があります。 設定の名前とその値はわかりやすくするために更新されます。

適用対象:

- Windows 10 以降のデバイス構成プロファイル
- Windows Holographic for Business のデバイス構成プロファイル
- Windows 8.1 のデバイス構成プロファイル
- Windows Phone 8.1 のデバイス構成プロファイル

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Android および Android Enterprise デバイスでデバイス制限プロファイルを作成するときのユーザー インターフェイス エクスペリエンスの向上<!-- 5841361 -->
Android または Android Enterprise デバイス用のプロファイルを作成するときの、Endpoint Management 管理センターのエクスペリエンスが更新されます。 この変更は、次のデバイス構成プロファイルに影響します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > **プラットフォームの [Android デバイス管理者]** または **[Android Enterprise]** )。

- デバイスの制限:Android デバイス管理者
- デバイスの制限:Android Enterprise デバイス所有者
- デバイスの制限:Android Enterprise 仕事用プロファイル

構成できるデバイスの制限の詳細については、[Android デバイス管理者](../configuration/device-restrictions-android.md)と [Android Enterprise](../configuration/device-restrictions-android-for-work.md) に関するページを参照してください。

### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355----"></a>Android Enterprise デバイスで OEMConfig デバイス構成プロファイルのバンドルとバンドル配列を削除する<!-- 5550355  -->
Android Enterprise デバイスで、OEMConfig プロファイルを作成して更新します。 ユーザーは、Intune の**構成デザイナー**を使用して、バンドルとバンドル配列を削除できるようになります。

OEMConfig プロファイルの詳細については、「[Microsoft Intune で、OEMConfig を使って Android Enterprise デバイスを使用および管理する](../configuration/android-oem-configuration-overview.md)」を参照してください。

この機能は、以下に適用されます。
- Android エンタープライズ

### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>iOS エンタープライズ Wi-Fi プロファイルでの WPA と WPA2 のサポート<!--6215273   -->
*[セキュリティの種類]* フィールドを [iOS 用エンタープライズ Wi-Fi プロファイル](../configuration/wi-fi-settings-ios.md)に追加しています ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[iOS/iPadOS]** を選択してから、"*プロファイル*" として **[Wi-Fi]** を選ぶ)。 これは、iOS 用の基本的な Wi-Fi プロファイルで使用できるオプションに似ています。 この変更により、**WPA-エンタープライズ**または **WPA/WPA2-エンタープライズ**のセキュリティの種類を指定する新しいプロファイルを作成し、"*EAP の種類*" の選択を指定できるようになります。

### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-profiles---5615208-----"></a>証明書、電子メール、VPN、および Wi-Fi プロファイルの新しいユーザー エクスペリエンス<!-- 5615208   -->
Endpoint Management 管理センターで次のプロファイルの種類の作成および変更を行うための[ユーザー エクスペリエンス](../configuration/device-profile-create.md)を更新しています ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** )。 新しいエクスペリエンスでは、以前と同じ設定が表示されますが、あまり水平スクロールを必要としないウィザードのようなエクスペリエンスが使用されます。 新しいエクスペリエンスで既存の構成を変更する必要はありません。
- 派生資格情報
- 電子メール
- PKCS 証明書
- PKCS のインポートされた証明書
- SCEP 証明書
- 信頼された証明書
- VPN
- Wi-Fi

( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、 *[プロファイルの種類]* で、上記のいずれかのプロファイルを選択する。)

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>macOS 用に Microsoft Defender ATP アプリを構成する  <!-- 5520115  -->
まもなく、Endpoint Protection デバイス構成プロファイルの一部として macOS を実行するデバイス用に、Microsoft Defender ATP アプリの[設定](../protect/endpoint-protection-macos.md)を構成できるようになります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[macOS]** を選択してから "*プロファイルの種類*" として **[Endpoint Protection]** を選ぶ)。 macOS デバイス構成の設定は 8 つになります。 

Defender ATP は macOS 10.13 (High Sierra) 以降でサポートされており、[Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) アプリは、これらの設定が適用された "*後*" に、デバイスにデプロイされる必要があります。 設定は、アプリがデプロイされる前にデバイスに送信される必要があります。 macOS のベータ版はサポートされません。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection デバイス構成ポリシーの新しい FileVault 設定<!-- 5459801   -->
[macOS Endpoint Protection](../protect/endpoint-protection-macos.md) テンプレート内の FileVault カテゴリに、次の新しい設定を追加しています: 回復キーを非表示にする ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[macOS]** を選択してから、"*プロファイルの種類*" として **[Endpoint Protection]** を選ぶ)。 この設定により、FileVault 2 の暗号化中は、エンド ユーザーに対して個人用キーが非表示になります。 デバイス ユーザーは、iOS ポータル サイト アプリから、または暗号化された macOS デバイス用のポータル Web サイトから、いつでも自分の個人用回復キーを表示することができます。 個人用回復キーを表示するには、[デバイスの詳細] に移動し、 *[回復キーの取得]* をクリックします。

この設定は、以前に作成されたポリシーでは使用できません。 この設定を利用するように構成するには、FileVault ポリシーを再作成する必要があります。 

###  <a name="ui-update-when-configuring-compliance-policy----3961639----"></a>コンプライアンス ポリシーを構成するときの UI の更新 <!-- 3961639  -->
Microsoft Endpoint Manager でコンプライアンス ポリシーを構成するための UI を更新しています ( **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシー]**  >  **[ポリシーの作成]** )。 以前に使用したのと同じ設定と詳細を提供する新しいユーザー エクスペリエンスが表示されます。 新しいエクスペリエンスでは、ウィザードのようなプロセスに従ってコンプライアンス ポリシーを作成し、ポリシーの "*割り当て*" を追加できるページと、ポリシーを作成する前に構成を確認できる *[概要]* ページが含まれます。 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Win32 アプリ コンテンツをダウンロードするときに配信の最適化エージェントを構成する<!-- 5410945  -->
配信の最適化エージェントを、割り当てに基づいてバックグラウンドまたはフォアグラウンド モードで Win32 アプリ コンテンツをダウンロードするように構成できるようになります。 既存の Win32 アプリでは、コンテンツは引き続きバックグラウンド モードでダウンロードされます。 [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[アプリ]**  >  **[すべてのアプリ]**  > *Win32 アプリを選択* >  **[プロパティ]** の順に選択します。 **[割り当て]** の横にある **[編集]** を選択します。  **[必須]** セクションの **[モード]** の下で **[含める]** を選択して、割り当てを編集します。  新しい設定が使用可能になると、 **[アプリの設定]** セクションに表示されます。 配信の最適化の詳細については、[「Win32 アプリ管理」の「配信の最適化」](../apps/apps-win32-app-management.md#delivery-optimization)を参照してください。

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Windows デバイスのプライマリ ユーザーを変更する <!-- 3794742 -->
Windows ハイブリッド デバイスと Azure AD 参加済みデバイスのプライマリ ユーザーを変更できるようになります。 これを行うには、 **[Intune]**  >  **[デバイス]**  >  **[すべてのデバイス]** > デバイスを選択 > **[プロパティ]**  >  **[プライマリ ユーザー]** を選択します。

### <a name="new-android-report-on-android-devices-overview-page---5435435---"></a>Android デバイスの概要ページの新しい Android レポート<!-- 5435435 -->
Microsoft Endpoint Manager 管理コンソールの、各デバイス管理ソリューションに登録されている Android デバイスの数を表示する Android デバイスの概要ページにレポートを追加する予定です。 このグラフ (Azure コンソールに既にあるのと同じような) には、仕事用プロファイル、フル マネージド、専用、およびデバイス管理者が登録したデバイスの数が表示されます。 レポートを表示するには、 **[デバイス]**  >  **[Android]**  >  **[概要]** の順に選択します。

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>追加のデータ ウェアハウス デバイス インベントリ プロパティ<!-- 6125732  -->
Intune データ ウェアハウスを使って、追加のデバイス インベントリ プロパティを使用できるようになります。 次のプロパティは、[デバイス](../developer/intune-data-warehouse-collections.md#devices) コレクションを介して公開されます。

- 記憶域容量
- メモリ容量
- Office 365 バージョン
- デバイス モデル

データ ウェアハウスの詳細については、「[Microsoft Intune データ ウェアハウス API](../developer/reports-nav-intune-data-warehouse.md)」を参照してください。

### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738--"></a>Android デバイス管理者の管理から仕事用プロファイルの管理にユーザーをガイドする<!--5857738-->
Android デバイス管理者プラットフォーム用の新しいコンプライアンス設定をリリースしています。 この設定を使用すると、デバイス管理者によって管理される場合にデバイスを非準拠にすることができます。

これらの非準拠デバイスでは、 **[デバイス設定の更新]** ページに、ユーザーに対して **[新しいデバイス管理セットアップに移動する]** メッセージが表示されます。 **[解決]** ボタンをタップすると、次のようにガイドされます。

1. デバイス管理者の管理からの登録解除
2. 仕事用プロファイルの管理への登録
3. コンプライアンスに関する問題の解決

Google では、Android Enterprise を使用した最新のより豊富で安全なデバイス管理に移行するための取り組みの一環として、新しい Android リリースでのデバイス管理者サポートを縮小しています。  Intune では、Android 10 以降を実行している、デバイス管理者が管理する Android デバイスのフル サポートを 2020 年第 2 四半期までのみ提供できます。 これを過ぎると、Android 10 以降を実行している、デバイス管理者が管理するデバイス (Samsung を除く) は、完全には管理できなくなります。 具体的には、影響を受けるデバイスが新しいパスワード要件を受け取ることはありません。 詳細については、この[通知](#decreasing-support-for-android-device-administrator)を参照してください。

### <a name="retire-noncompliant-devices---1827291---"></a>非準拠デバイスをインベントリから削除する<!-- 1827291 -->
非準拠デバイスをインベントリから削除するための新しいオプションのコンプライアンス アクションを追加しています ( **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシー]**  >  **[ポリシーの作成]** の順に移動し、 *[コンプライアンス非対応に対するアクション]* ページで使用可能な "*アクション*" を表示する)。  非準拠デバイスをインベントリから削除すると、そこから会社のデータがすべて削除されます。また、デバイスが Intune によって管理されなくなります。 このアクションは、構成された日単位の値に達したときに実行されます。 最小値は 30 日間です。  デバイスをインベントリから削除するには、IT 管理者の明示的な承認が必要になります。その場合、 *[準拠していないデバイスを削除します]* セクションを使用し、そこで管理者は対象となるすべてのデバイスをインベントリから削除できます。

### <a name="new-information-in-device-details---5604099---"></a>デバイスの詳細の新しい情報<!-- 5604099 -->
次の情報は、デバイスの **[概要]** ページに表示されます。

- 記憶域容量 (デバイス上の物理記憶領域の容量)
- メモリ容量 (デバイス上の物理メモリの容量)

### <a name="script-support-for-macos-devices---4280361----"></a>macOS デバイスのスクリプト サポート<!-- 4280361  -->
macOS デバイスにスクリプトを追加してデプロイできるようになります。 このサポートにより、macOS デバイスを構成する機能が拡張され、macOS デバイスでネイティブの MDM 機能を使用してできること以上のことが可能になります。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

### <a name="help-and-support-workflow-update-to-support-additional-services---5654170---"></a>追加サービスをサポートするためのヘルプとサポート ワークフローの更新<!-- 5654170 -->
Microsoft Endpoint Manager admin center の [ヘルプとサポート] ページを更新しています。これにより、使用する管理の種類を選択して、特定のサポートを強化できるようになります ( **[トラブルシューティング + サポート]**  >   **[ヘルプとサポート]** )。 この変更により、次の管理の種類から選択できるようになります。
- Configuration Manager (Desktop Analytics を含む)
- Intune
- 共同管理

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>セキュリティ

### <a name="derived-credentials-support-on-android-cobo-devices--4839592--"></a>Android COBO デバイスでの派生資格情報のサポート<!--4839592-->
Android Enterprise の完全に管理されたデバイスで、派生資格情報を使用できるようになります。 Entrust Datacard、Intercede、および DISA Purebred の派生資格情報を取得するためのサポートが追加されます。 アプリ認証、Wi-Fi、VPN、または S/MIME 署名や、それをサポートするアプリでの暗号化に、派生資格情報を使用できるようになります。

### <a name="use-antivirus-policy-to-manage-settings-for-microsoft-defender-antivirus-and-the-windows-security-experience--6131401---"></a>ウイルス対策ポリシーを使用して Microsoft Defender ウイルス対策および Windows セキュリティ エクスペリエンスの設定を管理する<!--6131401 -->
"*エンドポイント セキュリティ*" ノードで、**ウイルス対策**の設定を構成できます。 ウイルス対策のポリシーを構成する場合は、次の 2 種類のプロファイルを使用して Windows 10 デバイスの設定を定義します。

- Microsoft Defender ウイルス対策: クラウドの保護、ウイルス対策の除外、修復、スキャン オプションなどの設定を管理します。
- Windows セキュリティ エクスペリエンス: ユーザーが自分のデバイスで Windows セキュリティ設定を体験する方法を管理します。 Microsoft Defender セキュリティ センターでエンド ユーザーが表示できる内容と、エンド ユーザーが受信する通知を構成できるようになります。

### <a name="users-personal-encrypted-recovery-key---6273943---"></a>ユーザーの個人用の暗号化された回復キー<!-- 6273943 -->
ユーザーが Android ポータル サイトア プリケーションまたは Android Intune アプリケーションを介して、Mac デバイスの個人用の暗号化された **FileVault** 回復キーを取得できるようにする、新しい Intune 機能を使用できるようになります。 ポータル サイト アプリケーションと Intune アプリケーションの両方にリンクが示されるようになります。これを使用すると、Chrome ブラウザーで Web ポータル サイトが開き、そこでユーザーは Mac デバイスにアクセスするために必要な **FileVault** 回復キーを確認できます。 暗号化の詳細については、「[Intune でデバイスの暗号化を使用する](../protect/encrypt-devices.md)」を参照してください。

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
