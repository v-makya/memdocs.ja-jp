---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d443cb784c19956f52347a10f4123c622ab82a8
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820065"
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

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>Windows ポータル サイトに Configuration Manager アプリケーションのサポートが追加される<!-- 4297660 -->
Windows ポータル サイトでは、Configuration Manager アプリケーションがサポートされるようになりました。 エンド ユーザーはこの機能によって、共同管理されている顧客に対して、Windows ポータル サイト上で Configuration Manager および Intune の両方にデプロイされているアプリケーションを表示できるようになります。 このサポートによって、管理者は異なるエンド ユーザー ポータルのエクスペリエンスを統合できます。 詳細については、「[共同管理デバイスでポータル サイト アプリを使用する](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal)」を参照してください。

<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Android Enterprise フル マネージド デバイス (COBO) 用の PKCS 証明書プロファイルを作成する<!-- 4839686 -->
PKCS 証明書プロファイルを作成して、Android Enterprise デバイス所有者および仕事用プロファイルのデバイスに証明書を展開できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Android Enterprise] > [デバイスの所有者のみ]** 、または **[Android Enterprise] > [仕事用プロファイルのみ]** (プラットフォーム) > **[PKCS]** (プロファイル))。

間もなく、Android Enterprise フル マネージド デバイス用の PKCS 証明書プロファイルを作成できるようになります。 Intune の PFX 証明書コネクタが必要です。 SCEP を使用せず、PKCS のみを使用する場合は、新しい PFX コネクタをインストールした後で NDES コネクタを削除できます。 新しい PFX コネクタによって PFX ファイルがインポートされ、すべてのプラットフォームに PKCS 証明書が展開されます。

PKCS 証明書の詳細については、「[Intune で PKCS 証明書を構成して使用する](../protect/certficates-pfx-configure.md)」をご覧ください。

適用対象:
- Android Enterprise フル マネージド (COBO)

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

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>ソフトウェア更新プログラムを macOS デバイスに展開する <!-- 3194876 -->
macOS デバイスのグループにソフトウェア更新プログラムを展開できます。 この機能には、クリティカル、ファームウェア、構成ファイル、およびその他の更新プログラムが含まれます。 次のデバイス チェックイン時に更新プログラムを送信したり、週単位でのスケジュールを選択して設定した期間内または期間外に更新プログラムを展開したりできます。 これは、標準の勤務時間外にデバイスを更新する場合や、ヘルプ デスクのスタッフが常時配置されている場合に役立ちます。 また、更新プログラムが展開されるすべての macOS デバイスの詳細なレポートも取得します。 デバイスごとにレポートの詳細を表示して、特定の更新プログラムの状態を確認することができます。

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


<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。
