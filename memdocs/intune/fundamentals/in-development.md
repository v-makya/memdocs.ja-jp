---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1f261d8d61fc2c4273ae8f137a43bb6c607430d
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002700"
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


<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Android Enterprise フル マネージド デバイス (COBO) 用の PKCS 証明書プロファイルを作成する<!-- 4839686 -->
PKCS 証明書プロファイルを作成して、Android Enterprise デバイス所有者および仕事用プロファイルのデバイスに証明書を展開できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Android Enterprise] > [デバイスの所有者のみ]** 、または **[Android Enterprise] > [仕事用プロファイルのみ]** (プラットフォーム) > **[PKCS]** (プロファイル))。

間もなく、Android Enterprise フル マネージド デバイス用の PKCS 証明書プロファイルを作成できるようになります。 Intune の PFX 証明書コネクタが必要です。 SCEP を使用せず、PKCS のみを使用する場合は、新しい PFX コネクタをインストールした後で NDES コネクタを削除できます。 新しい PFX コネクタによって PFX ファイルがインポートされ、すべてのプラットフォームに PKCS 証明書が展開されます。

PKCS 証明書の詳細については、「[Intune で PKCS 証明書を構成して使用する](../protect/certficates-pfx-configure.md)」をご覧ください。

適用対象:
- Android Enterprise フル マネージド (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>仕事用プロファイルを使用する Android Enterprise デバイスに VPN 接続の種類として NetMotion を使用する<!-- 7764263 -->
VPN プロファイルを作成するときに、VPN 接続の種類として NetMotion を使用できます ( **[デバイス]**  >  **[デバイス構成]**  >  **[プロファイルの作成]**  >  **[Android Enterprise 仕事用プロファイル]** (プラットフォーム) **[VPN]** (プロファイル) > **[NetMotion]** (接続の種類))。

Intune での VPN プロファイルの詳細については、[VPN サーバーに接続するための VPN プロファイルの作成](../configuration/vpn-settings-configure.md)に関する記事をご覧ください。

適用対象:
- Android Enterprise 仕事用プロファイル

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>デバイスの制限プロファイルでのパスワード設定の変更 (Android デバイス管理者向け)<!-- 7662279  --> 
"*Android デバイス管理者*" 向けに、"*デバイスの制限*" および "*コンプライアンス*" ポリシーのパスワード設定にいくつかの変更を導入しています ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[デバイスの制限]** および **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシーの作成]** )。これらの変更は、Intune で、Android バージョン 10 以降の変更に対応して、パスワードの設定が引き続き想定どおりにデバイスに適用されることを確実にするのに役立ちます。
 
変更内容:
- **パスワード**の上位オプションの削除。  
- 設定は、適用されるデバイスに基づいてセクションに再編成されます。
- **[パスワードの種類]** が、パスワードの長さが適用される値に構成されない限り、 **[パスワードの最小文字数]** は使用できません。
- ラベルとサンプル テキストに対する追加の更新。

これらの変更は、設定の UI に適用され、既存のプロファイルには影響しません。 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>デバイスの登録

### <a name="ending-support-for-ios-11--7327321---"></a>iOS 11 のサポートの終了<!--7327321 -->
iOS 14 のリリース後、Intune の登録とポータル サイト アプリでは、iOS バージョン 12 以降がサポートされます。 以前のバージョンはサポートされませんが、ポリシーは引き続き受け取られます。

### <a name="ending-support-for-macos-1012--7327326---"></a>macOS 10.12 のサポートの終了<!--7327326 -->
macOS 11 のリリース後、Intune の登録とポータル サイト アプリでは、macOS バージョン 10.13 以降がサポートされます。 以前のバージョンはサポートされません。


<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics には、デバイスの詳細ログが含まれる<!--6014987  -->
Intune デバイスの詳細ログは、 **[レポート]**  >  **[ログ分析]** で入手できます。 デバイスの詳細を相互に関連付けて、カスタム クエリと Azure ブックを作成することができます。

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>テナントのアタッチ:管理センターからスクリプトを実行する<!--7220536, CM6234688 -->
Configuration Manager のオンプレミスの[スクリプト実行](../../configmgr/apps/deploy-use/create-deploy-scripts.md)機能を、Microsoft Endpoint Manager admin center に導入できるようになります。 Helpdesk などの追加のペルソナが、Configuration Manager マネージド デバイスそれぞれに対してクラウドから PowerShell スクリプトを実行できるようになります。 これにより、Configuration Manager 管理者によって既に定義され、承認されている PowerShell スクリプトの従来の利点すべてを、この新しい環境でも利用できるようになります。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts) に関する記事をご覧ください。 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>ソフトウェア更新プログラムを macOS デバイスに展開する <!-- 3194876 -->
macOS デバイスのグループにソフトウェア更新プログラムを展開できます。 この機能には、クリティカル、ファームウェア、構成ファイル、およびその他の更新プログラムが含まれます。 次のデバイス チェックイン時に更新プログラムを送信したり、週単位でのスケジュールを選択して設定した期間内または期間外に更新プログラムを展開したりできます。 これは、標準の勤務時間外にデバイスを更新する場合や、ヘルプ デスクのスタッフが常時配置されている場合に役立ちます。 また、更新プログラムが展開されるすべての macOS デバイスの詳細なレポートも取得します。 デバイスごとにレポートの詳細を表示して、特定の更新プログラムの状態を確認することができます。

<!-- ***********************************************-->
## <a name="intune-apps"></a>Intune アプリ

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Windows ポータル サイトでの Azure AD Enterprise と Office Online アプリケーションの統合配信<!-- 1817861  -->
2006 リリースでは、[ポータル サイトでの Azure AD Enterprise と Office Online アプリケーションの統合配信](../fundamentals/whats-new.md)を発表しました。 この機能は、Windows ポータル サイトでサポートされています。 Intune の **[カスタマイズ]** ウィンドウで、**Azure AD Enterprise アプリケーション**と **Office Online アプリケーション**の両方を、Windows ポータル サイトで **[非表示]** または **[表示]** することを選択できます。 各エンド ユーザーには、選択された Microsoft サービスによるアプリケーション カタログ全体が表示されます。 既定では、追加のアプリ ソースがそれぞれ **[非表示]** に設定されるようになります。 この構成設定を見つけるには、[Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[テナント管理]**  >  **[カスタマイズ]** の順に選択します。 関連情報については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」を参照してください。
 

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



<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。
