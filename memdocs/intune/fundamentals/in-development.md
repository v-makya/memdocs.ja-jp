---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b55c8cced4e559655018b36843e1599cc6e2d1bf
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262739"
---
# <a name="in-development-for-microsoft-intune"></a>Microsoft Intune 用に開発中

お客様の準備と計画をサポートするため、このページでは、開発中でまだリリースされていない Intune UI の更新と機能が一覧表示されます。 このページの情報に加えて: 

- 変更前にお客様による対処が必要であると予測される場合は、Office メッセージ センターに補足の投稿が公開されます。
- 機能の運用が始まると、機能の説明はプレビュー版も一般公開版も、このページから[新機能](whats-new.md)に関するページに移行します。
- このページと[新機能](whats-new.md)に関するページは、定期的に更新されます。 適宜確認してください。
- 戦略的な成果物とタイムラインについては、「[Microsoft 365 のロードマップ](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS)」を参照してください。

> [!NOTE]
> このページには、今後のリリースでの Intune の機能に関する現在の予測が反映されています。 日付と個々の機能は変更される可能性があります。 このページは、開発中のすべての機能を説明しているわけではありません。

**RSS フィード**:ご自身のフィード リーダーに次の URL をコピーして貼り付けることで、このページが更新されたときにわかるようになります。`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**この記事は、上記のタイトルの下に示されている日付に最後に更新されました。**

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

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Android 上のポータル サイトおよび Intune アプリのデバイス アイコンを更新する<!-- 6057023  -->
Microsoft では、より新しい外観を作成し、Microsoft Fluent Design System に準拠するように、Android デバイス上のポータル サイトと Intune アプリのデバイス アイコンを更新しています。 関連する情報については、「[iOS または iPadOS および macOS 用のポータル サイト アプリのアイコンの更新](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-)」を参照してください。 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS ポータル サイトでは、ユーザー アフィニティなしでの Apple の自動デバイス登録がサポートされます<!-- 7282707  --> 
割り当てられたユーザーを必要とせずに Apple の自動デバイス登録を使用して登録されたデバイス上で、iOS ポータル サイトがサポートされます。 エンド ユーザーは、iOS ポータル サイトにサインインして、デバイス アフィニティなしで登録された iOS/iPadOS デバイス上で、自身をプライマリ ユーザーとして確立できます。 自動デバイス登録に関する詳細については、「[Apple の自動デバイス登録を使用して iOS または iPadOS デバイスを自動登録する](../enrollment/device-enrollment-program-enroll-ios.md)」を参照してください。

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>ポータル サイトに Configuration Manager アプリケーションのサポートが追加される<!-- 4297660 -->
ポータル サイトでは、Configuration Manager アプリケーションがサポートされるようになりました。 エンド ユーザーはこの機能によって、共同管理されている顧客に対して、ポータル サイト上で Configuration Manager および Intune の両方にデプロイされているアプリケーションを表示できるようになります。 このサポートによって、管理者は異なるエンド ユーザー ポータルのエクスペリエンスを統合できます。 詳細については、「[共同管理デバイスでポータル サイト アプリを使用する](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal)」を参照してください。

<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>サード パーティの MDM パートナーからデバイス コンプライアンスの状態を設定する<!-- 6361689   -->
サード パーティの MDM ソリューションを所有している Microsoft 365 のお客様は、Microsoft Intune デバイス コンプライアンス サービスとの統合により、iOS および Android 上の Microsoft 365 アプリに条件付きアクセス ポリシーを適用できます。 サード パーティの MDM ベンダーは、Intune デバイス コンプライアンス サービスを利用して、デバイス コンプライアンス データを Intune に送信します。 その後、Intune によって、デバイスが信頼されているかどうか、Azure AD で条件付きアクセス属性が設定されているかどうかを判断するために評価されます。  お客様は、Microsoft エンドポイント マネージャー管理センターまたは Azure AD ポータル内から Azure AD 条件付きアクセス ポリシーを設定する必要があります。

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Android Enterprise フル マネージド デバイス (COBO) 用の PKCS 証明書プロファイルを作成する<!-- 4839686 -->
PKCS 証明書プロファイルを作成して、Android Enterprise デバイス所有者および仕事用プロファイルのデバイスに証明書を展開できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Android Enterprise] > [デバイスの所有者のみ]** 、または **[Android Enterprise] > [仕事用プロファイルのみ]** (プラットフォーム) > **[PKCS]** (プロファイル))。

間もなく、Android Enterprise フル マネージド デバイス用の PKCS 証明書プロファイルを作成できるようになります。 Intune の PFX 証明書コネクタが必要です。 SCEP を使用せず、PKCS のみを使用する場合は、新しい PFX コネクタをインストールした後で NDES コネクタを削除できます。 新しい PFX コネクタによって PFX ファイルがインポートされ、すべてのプラットフォームに PKCS 証明書が展開されます。

PKCS 証明書の詳細については、「[Intune で PKCS 証明書を構成して使用する](../protect/certficates-pfx-configure.md)」をご覧ください。

適用対象:
- Android Enterprise フル マネージド (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631---"></a>iOS および iPadOS、macOS デバイスの VPN 接続の種類として NetMotion を使用する<!-- 1333631 -->
VPN プロファイルを作成するときに、VPN 接続の種類として NetMotion を使用できます ( **[デバイス]**  >  **[デバイス構成]**  >  **[プロファイルの作成]**  >  **[iOS/iPadOS]** または **[macOS]** (プラットフォーム) > **[VPN]** (プロファイル) > **[NetMotion]** (接続の種類))。

Intune での VPN プロファイルの詳細については、[VPN サーバーに接続するための VPN プロファイルの作成](../configuration/vpn-settings-configure.md)に関する記事をご覧ください。

適用対象:
- iOS/iPadOS
- macOS

### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024---"></a>Windows 10 Wi-Fi プロファイル用の保護された拡張認証プロトコル (PEAP) オプションの追加<!-- 3805024 -->
Windows 10 デバイスで、Wi-Fi 接続を認証するために拡張認証プロトコル (EAP) を使用する Wi-Fi プロファイルを作成できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Windows 10 以降]** (プラットフォーム) > **[Wi-Fi]** (プロファイル) > **[Enterprise]** )。 保護された EAP (PEAP) を選択する場合、次のような新しい設定を使用できます。

- **PEAP フェーズ 1 でサーバー検証を実行する**:PEAP ネゴシエーション フェーズ 1 では、デバイスによって証明書が検証され、サーバーが確認されます。
  - **PEAP フェーズ 1 でのサーバー検証に関するユーザー プロンプトを無効にする**:PEAP ネゴシエーション フェーズ 1 では、信頼された証明機関に対して新しい PEAP サーバーの承認を求めるユーザー プロンプトは表示されません。
- **暗号化バインドを要求する**:PEAP ネゴシエーション中に、暗号化バインドを使用しない PEAP サーバーへの接続を禁止します。

現在構成できる設定を確認するには、[Windows 10 以降のデバイス向けの Wi-Fi 設定の追加](../configuration/wi-fi-settings-windows.md)に関する記事をご覧ください。

適用対象: 
- Windows 10 以降

### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576---"></a>macOS Microsoft Enterprise SSO プラグインを構成する<!-- 5627576 -->
Microsoft Azure AD チームでは、リダイレクト シングル サインオン (SSO) アプリ拡張機能を開発しました。これにより、macOS 10.15 以降のユーザーが、Apple の SSO 機能をサポートし、認証に Azure AD を使用する Microsoft アプリ、組織アプリ、Web サイトに対して、1 回のサインオンでアクセスできるようになります。 Microsoft Enterprise SSO プラグインのリリースに伴い、新しい Microsoft Azure AD アプリ拡張機能の種類を使用して SSO 拡張機能を構成できるようになります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[macOS]** (プラットフォーム) > **[デバイスの機能]** (プロファイル) > **[シングル サインオン アプリの拡張機能]** > [SSO アプリ拡張機能の種類] > **[Microsoft Azure AD]** )。

Microsoft Azure AD SSO アプリ拡張機能の種類を使用した SSO を実現するには、ユーザーが各自の macOS デバイスにポータル サイト アプリをインストールしてサインインする必要があります。 

macOS SSO アプリ拡張機能について詳しくは、「[シングル サインオン アプリ拡張機能](../configuration/device-features-configure.md#single-sign-on-app-extension)」をご覧ください。

適用対象:
- macOS 10.15 以降

### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991---"></a>Microsoft Enterprise SSO プラグインを使用して、さらに多くの iOS および iPadOS アプリで SSO アプリ拡張機能を使用する<!-- 7369991 -->
[Apple デバイス用の Microsoft Enterprise SSO プラグイン](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin)は、SSO アプリ拡張機能がサポートされているすべてのアプリで使用できます。 Intune の場合、この機能は、Apple デバイス用の Microsoft Authentication Library (MSAL) を使用しない iOS および iPadOS のモバイル アプリで、プラグインが動作するということを意味します。 アプリで MSAL を使用する必要はありませんが、Azure AD エンドポイントを使用して認証する必要があります。

プラグインで SSO を使用するように iOS または iPadOS アプリを構成するには、iOS または iPadOS の構成プロファイルにアプリ バンドル ID を追加します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS/iPadOS]** (プラットフォーム) > **[デバイスの機能]** (プロファイル) > **[シングル サインオン アプリの拡張機能]**  >  **[Microsoft Azure AD]** (SSO アプリ拡張機能の種類) > **[アプリ バンドル ID]** )。

構成できる現在の SSO アプリ拡張機能設定を確認するには、「[シングル サインオン アプリの拡張機能](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)」にアクセスしてください。

適用対象:
- iOS/iPadOS

### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-show-descriptions---7414768---"></a>Android 用ポータル サイト アプリの [デバイス設定の更新] ページを説明が表示されるように改善<!-- 7414768 -->
Android デバイス上のポータル サイト アプリの **[デバイス設定の更新]** ページには、準拠するためにユーザーが更新する必要がある設定の一覧が表示されます。 そのユーザー エクスペリエンスが改善され、一覧表示される設定が既定で展開されて、説明と **[解決]** ボタン (適用できる場合) が表示されるようになりました。 以前は、折りたたまれた状態が既定でした。 この新しい既定の動作によってクリック回数が減るため、ユーザーがより迅速に問題を解決できるようになります。

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics には、デバイスの詳細ログが含まれる<!--6014987  -->
Intune デバイスの詳細ログは、 **[レポート]**  >  **[ログ分析]** で入手できます。 デバイスの詳細を相互に関連付けて、カスタム クエリと Azure ブックを作成することができます。

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>テナントのアタッチ:管理センターのデバイス タイムライン<!--7220536, CM7141381 -->
Configuration Manager で、テナントのアタッチを使用してデバイスを Microsoft Endpoint Manager と同期すると、イベントのタイムラインを確認できるようになります。 このタイムラインにはそのデバイス上での過去の活動が表示され、問題のトラブルシューティングに役立ちます。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline) に関する記事をご覧ください。  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>テナントのアタッチ:管理センターからアプリケーションをインストールする<!-- 7220536, CM6024389 -->
Microsoft エンドポイント管理の管理センターからテナントに接続されたデバイスへのアプリケーションのインストールを、リアルタイムで開始できるようになります。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps) に関する記事をご覧ください。

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>テナントのアタッチ:管理センターからの CMPivot<!--7220536, CM6024392 -->
[CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) の機能を、Microsoft Endpoint Manager admin center に導入できるようになります。 Helpdesk などの追加のペルソナが、ConfigMgr マネージド デバイスそれぞれに対してクラウドからリアルタイムのクエリを開始して、結果を管理センターに返すことができるようになりました。 これにより、CMPivot の従来の利点すべてを利用して、IT 管理者やその他の指定されたペルソナが環境内のデバイスの状態をすばやく評価し、アクションを実行することが可能になります。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot) に関する記事をご覧ください。 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>テナントのアタッチ:管理センターからスクリプトを実行する<!--7220536, CM6234688 -->
Configuration Manager のオンプレミスの[スクリプト実行](../../configmgr/apps/deploy-use/create-deploy-scripts.md)機能を、Microsoft Endpoint Manager admin center に導入できるようになります。 Helpdesk などの追加のペルソナが、Configuration Manager マネージド デバイスそれぞれに対してクラウドから PowerShell スクリプトを実行できるようになります。 これにより、Configuration Manager 管理者によって既に定義され、承認されている PowerShell スクリプトの従来の利点すべてを、この新しい環境でも利用できるようになります。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts) に関する記事をご覧ください。 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Windows 10 デバイス用の新しいマージ ロジック<!--179048-->
現時点では、お客様がデバイスを再イメージ化してから再登録すると、そのデバイスの複数のレコードが Microsoft Endpoint Manager 管理コンソールに表示されます。 Windows 10 デバイスのそのような重複するレコードをマージするために、新しいマージ ロジックを開発中です。

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>ソフトウェア更新プログラムを macOS デバイスに展開する <!-- 3194876 -->
macOS デバイスのグループにソフトウェア更新プログラムを展開できます。 この機能には、クリティカル、ファームウェア、構成ファイル、およびその他の更新プログラムが含まれます。 次のデバイス チェックイン時に更新プログラムを送信したり、週単位でのスケジュールを選択して設定した期間内または期間外に更新プログラムを展開したりできます。 これは、標準の勤務時間外にデバイスを更新する場合や、ヘルプ デスクのスタッフが常時配置されている場合に役立ちます。 また、更新プログラムが展開されるすべての macOS デバイスの詳細なレポートも取得します。 デバイスごとにレポートの詳細を表示して、特定の更新プログラムの状態を確認することができます。

### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322---"></a>Apple VPP トークンの削除前に関連ライセンスが失効する<!--6195322 -->
今後の更新では、Microsoft Endpoint Manager で Apple VPP トークンを削除すると、そのトークンに関連付けられているすべての Intune 割り当てライセンスが、削除前に自動的に失効します。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI コンプライアンス レポート テンプレート V2.0<!-- 636958  -->
管理者は、Power BI コンプライアンス レポート テンプレートのバージョンを V1.0 から V2.0 に更新できるようになります。 V2.0 では、設計の改善が組み込まれ、テンプレートの一部として計算とデータが表示される改訂も行われます。 関連情報については、「[Power BI でデータ ウェアハウスに接続する](../developer/reports-proc-get-a-link-powerbi.md)」を参照してください。

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>セキュリティ

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Symantec Endpoint Security および Check Point Sandblast のアプリ保護ポリシーのサポート<!--  4452423, 4731168 -->

2019 年 10 月に、Intune アプリ保護ポリシーに、一部の Microsoft Threat Defense パートナー (MTD パートナー) のデータを利用する機能が追加されました。 Microsoft では以下のパートナーに対して、アプリ保護ポリシーを使用して、デバイスの正常性に基づいてユーザーの企業データをブロックしたり選択的にワイプしたりするためのサポートを追加しています。

- Android、iOS、および iPadOS 上での **Check Point Sandblast**
- Android、iOS、および iPadOS 上での **Symantec Endpoint Security**

MTD パートナーによるアプリ保護ポリシーの利用については、「[Intune で Mobile Threat Defense アプリ保護ポリシーを作成する](../protect/mtd-app-protection-policy.md)」を参照してください。

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP による脆弱性の詳細を含んだエンドポイント マネージャー セキュリティ タスクの作成<!-- 5568193  -->
Microsoft Defender ATP の脅威と脆弱性の管理 (TVM) によって、デバイスの正しく構成されていないセキュリティ設定を検出できます。 管理者は、この情報を使用して、脆弱性のあるデバイスを更新できます。

近日中に、Microsoft Defender ATP によって脆弱性の詳細を含むエンドポイント マネージャー セキュリティ タスク ( **[エンドポイント マネージャー]**  >  **[エンドポイント セキュリティ]**  >  **[セキュリティ タスク]** ) を生成し、影響を受けたデバイスを表示できるようになります。 IT 管理者は、セキュリティ タスクを受け入れ、必要な構成を展開できます。 

セキュリティ タスク詳細については、「[Intune を使用して Microsoft Defender ATP によって検出された脆弱性を修復する](../protect/atp-manage-vulnerabilities.md)」をご覧ください。

### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119----"></a>エンドポイント セキュリティ ウイルス対策ポリシーの除外に関する変更<!--5583940, 6018119  -->
エンドポイント セキュリティ ウイルス対策ポリシーの一部として構成する Microsoft Defender ウイルス対策の除外リストの管理について、2 点の変更が導入されます。 ( **[エンドポイント セキュリティ]**  >  **[ウイルス対策]**  >  **[ポリシーの作成]**  >  **[Windows 10 以降]** (プラットフォーム))。 これら 2 つの変更はポリシー間の競合を防ぐのに役立ちます。また、競合していた既存のポリシーが除外リストと競合しなくなります。

- まず、Windows 10 以降向けに新しいプロファイルの種類が追加されます。 **[Microsoft Defender ウイルス対策の除外]** です。  この新しいプロファイルの種類には、Defender "*プロセス*、"*ファイル拡張子*"、および "*ファイル*" と、Microsoft Defender を使用してスキャンしたくない "*フォルダー*" の一覧を指定するための設定のみが含まれます。 これは、除外リストを他のポリシー構成から分離し、除外リストの管理を簡素化するのに役立ちます。
- 2 番目の変更点は、異なるプロファイルで定義した除外リストが、特定のユーザーまたはデバイスに適用される個々のポリシーに基づいて、デバイスまたはユーザーごとに単一の除外リストにマージされされることです。 たとえば、3 つの独立したポリシーで 1 人のユーザーを対象とする場合、その 3 つのポリシーからの除外リストが Microsoft Defender ウイルス対策の除外の単一スーパーセットにマージされ、その後ユーザーに適用されます。 このマージには、新しいプロファイルの種類から追加された除外リストと、"*Microsoft Defender ウイルス対策*" プロファイルで構成された既存のポリシーからの除外リストが含まれます。



<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。
