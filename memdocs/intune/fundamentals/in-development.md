---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220134"
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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>横向きモードをサポートするための iOS 用ポータル サイト<!--6048329  -->
ユーザーは自分のデバイスを登録し、アプリを検索し、選択した画面の向きを使用して IT サポートを受けることができます。 ユーザーが縦向きモードで画面をロックしない限り、アプリでは画面を縦向きまたは横向きモードに合わせて自動的に検出して調整します。

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Android 用ポータル サイトでのサインイン エクスペリエンスの向上<!-- 6103997  -->
エクスペリエンスをユーザーにとってより新しく、シンプルでクリーンなものにするために、Android 用ポータル サイト アプリのいくつかのサインイン画面のレイアウトを更新しています。

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

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Android Enterprise デバイスで OEMConfig 構成プロファイルを作成するときのユーザー インターフェイス エクスペリエンスの向上<!-- 5568645   -->
Android Enterprise デバイスで OEMConfig プロファイルを作成または編集すると、Endpoint Management 管理センターのエクスペリエンスが更新されます。 更新されたエクスペリエンスによって、構成した設定の概要が表示されます。 この変更は、OEMConfig デバイス構成プロファイルに影響します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[Android Enterprise]** > プロファイルの種類の **[OEMConfig]** )。

この機能は、以下に適用されます。
- Android エンタープライズ 

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

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>macOS 用に Microsoft Defender ATP アプリを構成する  <!-- 5520115  -->
まもなく、Endpoint Protection デバイス構成プロファイルの一部として macOS を実行するデバイス用に、Microsoft Defender ATP アプリの[設定](../protect/endpoint-protection-macos.md)を構成できるようになります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[macOS]** を選択してから "*プロファイルの種類*" として **[Endpoint Protection]** を選ぶ)。 macOS デバイス構成の設定は 8 つになります。 

Defender ATP は macOS 10.13 (High Sierra) 以降でサポートされており、[Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) アプリは、これらの設定が適用された "*後*" にデバイスに展開する必要があります。 設定は、アプリがデプロイされる前にデバイスに送信される必要があります。 macOS のベータ版はサポートされません。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection デバイス構成ポリシーの新しい FileVault 設定<!-- 5459801   -->
[macOS Endpoint Protection](../protect/endpoint-protection-macos.md) テンプレート内の FileVault カテゴリに、次の新しい設定を追加しています: 回復キーを非表示にする ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[macOS]** を選択してから、"*プロファイルの種類*" として **[Endpoint Protection]** を選ぶ)。 この設定により、FileVault 2 の暗号化中は、エンド ユーザーに対して個人用キーが非表示になります。 デバイス ユーザーは、iOS ポータル サイト アプリから、または暗号化された macOS デバイス用のポータル Web サイトから、いつでも自分の個人用回復キーを表示することができます。 個人用回復キーを表示するには、[デバイスの詳細] に移動し、 *[回復キーの取得]* をクリックします。

この設定は、以前に作成されたポリシーでは使用できません。 この設定を利用するように構成するには、FileVault ポリシーを再作成する必要があります。 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Win32 アプリ コンテンツをダウンロードするときに配信の最適化エージェントを構成する<!-- 5410945  -->
配信の最適化エージェントを、割り当てに基づいてバックグラウンドまたはフォアグラウンド モードで Win32 アプリ コンテンツをダウンロードするように構成できるようになります。 既存の Win32 アプリでは、コンテンツは引き続きバックグラウンド モードでダウンロードされます。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[すべてのアプリ]**  > "*Win32 アプリを選択*" >  **[プロパティ]** の順に選択します。 **[割り当て]** の横にある **[編集]** を選択します。  **[必須]** セクションの **[モード]** の下で **[含める]** を選択して、割り当てを編集します。  新しい設定が使用可能になると、 **[アプリの設定]** セクションに表示されます。 配信の最適化の詳細については、[「Win32 アプリ管理」の「配信の最適化」](../apps/apps-win32-app-management.md#delivery-optimization)を参照してください。

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Windows デバイスのプライマリ ユーザーを変更する <!-- 3794742 -->
Windows ハイブリッド デバイスと Azure AD 参加済みデバイスのプライマリ ユーザーを変更できるようになります。 これを行うには、 **[Intune]**  >  **[デバイス]**  >  **[すべてのデバイス]** > デバイスを選択 > **[プロパティ]**  >  **[プライマリ ユーザー]** を選択します。

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="new-information-in-device-details---5604099---"></a>デバイスの詳細の新しい情報<!-- 5604099 -->
次の情報は、デバイスの **[概要]** ページに表示されます。

- 記憶域容量 (デバイス上の物理記憶領域の容量)
- メモリ容量 (デバイス上の物理メモリの容量)

### <a name="script-support-for-macos-devices---4280361----"></a>macOS デバイスのスクリプト サポート<!-- 4280361  -->
macOS デバイスにスクリプトを追加してデプロイできるようになります。 このサポートにより、macOS デバイスを構成する機能が拡張され、macOS デバイスでネイティブの MDM 機能を使用してできること以上のことが可能になります。

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
