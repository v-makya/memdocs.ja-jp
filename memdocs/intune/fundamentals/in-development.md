---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 107ac1e2aef18bcb72a6fe1f94eade23c3f85319
ms.sourcegitcommit: 79ffc8afed164c408db6994806d71f64d1fc0b8f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85216520"
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
<!--## App management-->


<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>サード パーティの MDM パートナーからデバイス コンプライアンスの状態を設定する<!-- 6361689   -->
サード パーティの MDM ソリューションを所有している Microsoft 365 のお客様は、Microsoft Intune デバイス コンプライアンス サービスとの統合により、iOS および Android 上の Microsoft 365 アプリに条件付きアクセス ポリシーを適用できます。 サード パーティの MDM ベンダーは、Intune デバイス コンプライアンス サービスを利用して、デバイス コンプライアンス データを Intune に送信します。 その後、Intune によって、デバイスが信頼されているかどうか、Azure AD で条件付きアクセス属性が設定されているかどうかを判断するために評価されます。  お客様は、Microsoft エンドポイント マネージャー管理センターまたは Azure AD ポータル内から Azure AD 条件付きアクセス ポリシーを設定する必要があります。  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Windows 10 以降のデバイス向けの新しい VPN 設定<!-- 6602122  -->
IKEv2 の接続の種類を使用して VPN プロファイルを作成する場合、構成可能な新しい設定があります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[Windows 10 以降]** を選択 > プロファイルに **[VPN]** を選択 > **[基本 VPN]** )。

- **デバイス トンネル**:ユーザーのログオンなど、ユーザー操作を必要とせずに、デバイスが VPN に自動的に接続できるようにします。 この機能を使用するには、 **[Always On]** を有効にし、認証方法として **[コンピューターの証明書]** を使用する必要があります。
- 暗号化スイートの設定:IKE と子セキュリティ アソシエーションをセキュリティで保護するために使用するアルゴリズムを構成します。これにより、クライアントとサーバーの設定を一致させることができます。

構成できる設定を確認するには、[Intune を使用して VPN 接続を追加するための Windows デバイス設定](../configuration/vpn-settings-windows-10.md)に関する記事をご覧ください。

適用対象:
- Windows 10 以降


<!-- ***********************************************-->
<!--## Device enrollment-->



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

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI コンプライアンス レポート テンプレート V2.0<!-- 636958  -->
管理者は、Power BI コンプライアンス レポート テンプレートのバージョンを V1.0 から V2.0 に更新できるようになります。 V2.0 では、設計が改善され、テンプレートの一部として表示される計算とデータが変更されます。 関連情報については、「[Power BI でデータ ウェアハウスに接続する](../developer/reports-proc-get-a-link-powerbi.md)」を参照してください。

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。
