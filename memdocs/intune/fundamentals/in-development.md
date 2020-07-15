---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5afca831e2f3cbcda69150adcbbcff996bf99554
ms.sourcegitcommit: 01c1ca337e82c5e8e92153079ed89f79e20bde9e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86157809"
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

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>登録なしで管理されている iOS および Android Enterprise デバイス上での Outlook の S/MIME<!-- 6517155  -->
登録なしで管理されているデバイス用のアプリ構成ポリシーを使用して、iOS および Android Enterprise デバイス上で Outlook の S/MIME を有効にすることが可能になります。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド アプリ]** の順に選択します。 さらに、Outlook 上でユーザーによるこの設定の変更を許可するかどうかの選択ができます。 Outlook 構成設定に関する詳細については、「[Microsoft Outlook の構成設定](../apps/app-configuration-policies-outlook.md)」を参照してください。

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS ポータル サイトでは、ユーザー アフィニティなしでの Apple の自動デバイス登録がサポートされます<!-- 7282707  --> 
割り当てられたユーザーを必要とせずに Apple の自動デバイス登録を使用して登録されたデバイス上で、iOS ポータル サイトがサポートされます。 エンド ユーザーは、iOS ポータル サイトにサインインして、デバイス アフィニティなしで登録された iOS/iPadOS デバイス上で、自身をプライマリ ユーザーとして確立できます。 自動デバイス登録に関する詳細については、「[Apple の自動デバイス登録を使用して iOS または iPadOS デバイスを自動登録する](../enrollment/device-enrollment-program-enroll-ios.md)」を参照してください。

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Win32 アプリのインストール通知とポータル サイト<!-- 7485945  -->
エンド ユーザーは、[Microsoft Intune Web ポータル サイト](https://portal.manage.microsoft.com/)に表示されるアプリケーションが、ポータル サイト アプリまたは Web ポータル サイトのどちらで開かれるようにするかを決めることができます。 このオプションは、エンド ユーザーがポータル サイト アプリをインストールしており、ブラウザーの外部で Web ポータル サイト アプリケーションを起動する場合にのみ使用できます。

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>ポータル サイトに Configuration Manager アプリケーションのサポートが追加される<!-- 4297660 -->
ポータル サイトでは、Configuration Manager アプリケーションがサポートされるようになりました。 エンド ユーザーはこの機能によって、共同管理されている顧客に対して、ポータル サイト上で Configuration Manager および Intune の両方にデプロイされているアプリケーションを表示できるようになります。 このサポートによって、管理者は異なるエンド ユーザー ポータルのエクスペリエンスを統合できます。 詳細については、「[共同管理デバイスでポータル サイト アプリを使用する](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal)」を参照してください。

<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>サード パーティの MDM パートナーからデバイス コンプライアンスの状態を設定する<!-- 6361689   -->
サード パーティの MDM ソリューションを所有している Microsoft 365 のお客様は、Microsoft Intune デバイス コンプライアンス サービスとの統合により、iOS および Android 上の Microsoft 365 アプリに条件付きアクセス ポリシーを適用できます。 サード パーティの MDM ベンダーは、Intune デバイス コンプライアンス サービスを利用して、デバイス コンプライアンス データを Intune に送信します。 その後、Intune によって、デバイスが信頼されているかどうか、Azure AD で条件付きアクセス属性が設定されているかどうかを判断するために評価されます。  お客様は、Microsoft エンドポイント マネージャー管理センターまたは Azure AD ポータル内から Azure AD 条件付きアクセス ポリシーを設定する必要があります。  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Windows 10 以降のデバイス向けの新しい VPN 設定<!-- 6602122  -->
IKEv2 の接続の種類を使用して VPN プロファイルを作成する場合、構成可能な新しい設定があります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[Windows 10 以降]** を選択 > プロファイルに **[VPN]** を選択 > **[基本 VPN]** )。

- **デバイス トンネル**:ユーザー ログオンなど、ユーザー操作を必要とせずに、デバイスから VPN に自動的に接続できるようにします。 この機能を使用するには、 **[Always On]** を有効にし、認証方法として **[コンピューターの証明書]** を使用する必要があります。
- 暗号化スイートの設定:IKE と子セキュリティ アソシエーションをセキュリティで保護するために使用するアルゴリズムを構成します。これにより、クライアントとサーバーの設定を一致させることができます。

構成できる設定を確認するには、[Intune を使用して VPN 接続を追加するための Windows デバイス設定](../configuration/vpn-settings-windows-10.md)に関する記事をご覧ください。

適用対象:
- Windows 10 以降

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Android エンタープライズ デバイス所有者の専用デバイス (COSU) 上での Managed Home Screen の新機能<!-- 7414175 7133328 7133720 7134873 7135184  -->
Android Enterprise デバイス上で、管理者はデバイス構成プロファイルを使用し、マルチアプリ キオスク モードを使って専用デバイス上の Managed Home Screen をカスタマイズできます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > プラットフォーム用の **[Android Enterprise]** > **[デバイスの所有者のみ]**  > プロファイルの **[デバイスの制限]** > **[デバイス エクスペリエンス]** )。

具体的には次のことができます。

- アイコンをカスタマイズする、画面の向きを変更する、バッジ アイコンでアプリ通知を表示する <!--7414175-->
- マネージド設定のエントリ ポイントを非表示にする <!--7133328-->
- より簡単にデバッグ メニューにアクセスする <!--7133720-->
- 許可されている Wi-Fi ネットワークの一覧を作成する <!-- 7134873-->
- より簡単にデバイス情報にアクセスする <!-- 7135184-->

詳細については、[機能を許可または制限する Android エンタープライズ デバイスの設定](../configuration/device-restrictions-android-for-work.md)に関する記事をご覧ください。

適用対象:

- Android エンタープライズ デバイス所有者、専用デバイス (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>デバイスの登録

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>企業所有の個人対応デバイス (プレビュー)<!--4442275 -->
Intune では、OS バージョンが Android 8 以降の仕事用プロファイルを使用する Android Enterprise 企業所有デバイスがサポートされます。 仕事用プロファイルを使用する企業所有デバイスは、Android Enterprise ソリューション セットの企業管理シナリオの 1 つです。 このシナリオは、企業および個人使用が想定されている単一ユーザーのデバイスに対応しています。 この企業所有の個人対応 (COPE) シナリオでは、次のことが実現されます。

- 仕事用プロファイルと個人プロファイルのコンテナー化
- 管理者向けのデバイス レベルの制御
- エンド ユーザーの個人データとアプリケーションがプライベートのままであることの保証

最初のパブリック プレビュー リリースには、一般提供のリリースに組み入れられる予定の機能のサブセットが含まれます。 追加機能は、ローリング方式で追加されます。 最初のプレビューで使用できる機能は、次のとおりです。

- 登録:管理者は、有効期限のない一意のトークンを含む複数の登録プロファイルを作成できます。 デバイスの登録は、NFC、トークン エントリ、QR コード、Zero Touch、または Knox Mobile Enrollment 経由で行うことができます。
- デバイスの構成:既存のフル マネージドおよび専用デバイス設定のサブセット。
- デバイス コンプライアンス:フル マネージド デバイスに現在利用できるコンプライアンス ポリシー。
- デバイス アクション:デバイスの削除 (出荷時の設定に戻す)、デバイスの再起動、デバイスのロック。  
- アプリ管理:アプリの割り当て、アプリの構成、および関連付けられているレポート機能 
- 条件付きアクセス



<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="device-compliance-logs-now-in-english--6014904---"></a>デバイス コンプライアンス ログが英語で利用可能になっている<!--6014904 -->
IntuneDeviceComplianceOrg のログには、ComplianceState、OwnerType、および DeviceHealthThreatLevel の列挙のみがあります。 これらのログには、今後の更新で、列内に英語の情報が含まれるようになります。

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

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>macOS デバイスのリモート ロック操作に対する更新<!--7032805 -->
macOS デバイスのリモート ロック操作に対する更新には、以下が含まれます。
- 回復用 PIN は、(7 日ではなく) 削除される 30 日前に表示されます。
- 管理者が 2 つ目のブラウザーを開いていて、別のタブまたはブラウザーからコマンドのトリガーを再試行した場合、Intune によってコマンドの実行が許可されます。 ただし、新しい PIN は生成されず、レポートの状態は "失敗" に設定されます。
- 前のコマンドが引き続き保留中の場合、またはデバイスが再チェックインされていない場合、管理者は別のリモート ロック コマンドを発行することはできなくなります。
これらの変更は、複数のリモート ロック コマンドの後に正しい PIN が上書きされないように設計されています。

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>ソフトウェア更新プログラムを macOS デバイスに展開する <!-- 3194876 -->
macOS デバイスのグループにソフトウェア更新プログラムを展開できます。 この機能には、クリティカル、ファームウェア、構成ファイル、およびその他の更新プログラムが含まれます。 次のデバイス チェックイン時に更新プログラムを送信したり、週単位でのスケジュールを選択して設定した期間内または期間外に更新プログラムを展開したりできます。 これは、標準の勤務時間外にデバイスを更新する場合や、ヘルプ デスクのスタッフが常時配置されている場合に役立ちます。 また、更新プログラムが展開されるすべての macOS デバイスの詳細なレポートも取得します。 デバイスごとにレポートの詳細を表示して、特定の更新プログラムの状態を確認することができます。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>追加の Data Warehouse v1.0 プロパティ<!-- 6125732   -->
Intune Data Warehouse v1.0 を使用して、追加のプロパティを使用できます。 次のプロパティが、[device](../developer/reports-ref-devices.md#devices) エンティティを介して公開されるようになりました。
- `ethernetMacAddress` - このデバイスの一意のネットワーク識別子。
- `office365Version` - デバイスにインストールされている Office 365 のバージョン。

次のプロパティが、[devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) エンティティを介して公開されるようになりました。
- `physicalMemoryInBytes` - 物理メモリ (バイト単位)。
- `totalStorageSpaceInBytes` - 記憶域の合計容量 (バイト単位)。

詳細については、「[Microsoft Intune データ ウェアハウス API](../developer/reports-nav-intune-data-warehouse.md)」を参照してください。

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI コンプライアンス レポート テンプレート V2.0<!-- 636958  -->
管理者は、Power BI コンプライアンス レポート テンプレートのバージョンを V1.0 から V2.0 に更新できるようになります。 V2.0 では、設計の改善が組み込まれ、テンプレートの一部として計算とデータが表示される改訂も行われます。 関連情報については、「[Power BI でデータ ウェアハウスに接続する](../developer/reports-proc-get-a-link-powerbi.md)」を参照してください。

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>ロール ベースのアクセス制御

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>カスタマイズ ポリシーのスコープ タグのサポート<!--6182440 -->
スコープ タグをカスタマイズ ポリシーに割り当てられるようになります。 これを行うには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[テナント管理]** >  **[カスタマイズ]** へ移動します。ここに、 **[スコープ タグ]** 構成オプションが表示されます。

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>[プロファイルの割り当て] と [プロファイルの更新] アクセス許可の変更<!--7177586 -->
[プロファイルの割り当て] と [プロファイルの更新] に対して、ロールベースのアクセス制御のアクセス許可が変更されます。
- プロファイルの割り当て:このアクセス許可を持つ管理者は、複数のトークンへのプロファイルの割り当てと、1 つのトークンへの既定のプロファイルの割り当ても可能になります。
- プロファイルの更新:このアクセス許可を持つ管理者は、既存のプロファイルの更新のみが可能です。

<!-- ***********************************************-->
## <a name="security"></a>セキュリティ

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Symantec Endpoint Security および Check Point Sandblast のアプリ保護ポリシーのサポート<!--  4452423, 4731168 -->

2019 年 10 月に、Intune アプリ保護ポリシーに、一部の Microsoft Threat Defense パートナー (MTD パートナー) のデータを利用する機能が追加されました。 Microsoft では以下のパートナーに対して、アプリ保護ポリシーを使用して、デバイスの正常性に基づいてユーザーの企業データをブロックしたり選択的にワイプしたりするためのサポートを追加しています。

- Android、iOS、および iPadOS 上での **Check Point Sandblast**
- Android、iOS、および iPadOS 上での **Symantec Endpoint Security**

MTD パートナーによるアプリ保護ポリシーの利用については、「[Intune で Mobile Threat Defense アプリ保護ポリシーを作成する](../protect/mtd-app-protection-policy.md)」を参照してください。

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>Intune に登録する前に FileVault によって暗号化された macOS デバイス用の回復キーを保存する<!--5239424   -->
まもなく、Intune から FileVault ポリシーによって暗号化されなかった、または Intune に登録される前に暗号化された macOS デバイスのエンド ユーザーは、Intune による再暗号化が可能であることから、デバイスの暗号化を解除する必要がなくなります。 代わりに、現在の暗号化はそのまま維持され、ユーザーはポータル サイト Web サイトにアクセスし、そこで *[Store recovery key]\(回復キーの保存\)* を選択して、暗号化された macOS デバイスの個人用回復キーを送信できます。 有効なキーが送信されると、Intune によって個人キーがローテーションされて新しいキーが生成され、ポータル サイト Web サイト、iOS/ポータル サイト、Android ポータル サイト、または Intune アプリ経由で、引き続きユーザーによる利用が可能な状態になります。 macOS デバイスからロックアウトされた場合、ユーザーは、任意のデバイスからそれらの場所にアクセスして、キーを表示することができます。

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>macOS FileVault のディスク暗号化中にデバイス ユーザーの個人用回復キーを非表示にする<!--  5475632  -->
Microsoft では、FileVault のエンドポイント セキュリティ ディスク暗号化ポリシーに *[Hide recovery key]\(回復キーを非表示にする\)* という新しい設定を追加しています ( **[エンドポイント セキュリティ]**  >  **[ディスクの暗号化]**  >  **[プロファイルの作成]**  >  **[macOS]**  >  **[FileVault]** )。 新しい設定を有効にすると、暗号化中、Intune 上では macOS デバイスのユーザーに個人用回復キーが表示されなくなります。 このときにキーを非表示にすることで、デバイスの暗号化を待機している間にユーザーが書き留めることはできなくなるため、セキュリティを確保することができます。 代わりに、回復が必要な場合は、ユーザーはいつでも任意のデバイスを使用して、Intune ポータル サイトの Web サイト経由で個人用回復キーを表示することができます。

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>デバイスのセキュリティ ベースラインの詳細のビューが改善されている<!-- 5536846   -->
Microsoft では、デバイス ( **[エンドポイント セキュリティ]**  >  **[デバイス]** ) の詳細を確認する際の、セキュリティ ベースライン設定の詳細の表示を改善する取り組みを行っています。  割り当てられた各セキュリティ ベースラインについて、設定ごとの詳細のフラット リストを表示できます。これには、そのデバイスでの設定のカテゴリ、設定の名前、および各設定の状態が含まれます。

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>Windows 10 デバイスのエンドポイント セキュリティ ウイルス対策ポリシーを使用して、定義の更新用のソースの場所を管理する<!-- 6347801  -->  
Microsoft では、Windows 10 デバイス用のエンドポイント セキュリティ ウィルス対策ポリシーの *[更新]* カテゴリに、2 つの新しい設定を追加しています。これらを利用して、デバイス上で更新の定義が取得される方法を管理することができます ( **[エンドポイント セキュリティ]** > **[ウィルス対策]** > **[ポリシーの作成]**  >  **[Windows 10 以降]**  >  **[Microsoft Defender ウイルス対策]** )。

新しい設定を利用すると、定義の更新用のダウンロード元の場所として UNC ファイル共有を追加したり、異なるソースの場所に接続する際の順序を定義したりすることが可能になります。 新しい設定によって、次の Defender CSP が管理されます。

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>テナントに接続されたデバイスを MDATP にオンボードするためのエンドポイントの検出と応答ポリシーにおいて、プレビューが終了される<!-- 7303816   -->
Intune のエンドポイント セキュリティの一部として、Configuration Manager によって管理されているデバイスで使用されるエンドポイントの検出と応答 (EDR) ポリシーのサポートは、まもなくプレビューを終了して一般公開されます ( **[エンドポイント セキュリティ]**  >  **[エンドポイントでの検出と対応]**  >  **[ポリシーの作成]**  >  **[Windows 10 and windows Server]\(Windows 10 および Windows Server\)** )。 [Configuration Manager へのテナント接続](../../configmgr/tenant-attach/device-sync-actions.md)を構成するときに、EDR ポリシーを使用して、Configuration Manager によって管理されているデバイスを Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) にオンボードできます。 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>セキュリティ ベースライン ノードの機能強化<!-- 7433136   -->
Microsoft Endpoint Manager admin center でのセキュリティ ベースライン ノードの使いやすさを向上させるために、Microsoft では各ベースラインの *[概要]* タブを削除し、代わりにベースラインの **[プロファイル]** タブを開く予定です ( **[エンドポイント セキュリティ]**  >  **[セキュリティ ベースライン]**  >  *[ベースライン]* )。

各ベースラインの *[概要]* ページには、展開した最新のベースライン バージョンから結果を集計したグラフとタイルが表示されています。 その情報は、バージョンの詳細を展開した場合に表示される内容から複写されています。 *[概要]* ページが削除された後は、バージョンの詳細を直接確認すると、それらのグラフと集計の詳細を引き続き利用できます。  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>ファイアウォール規則の移行ツールのプレビュー<!-- 6423187  -->
パブリック プレビューとして、Microsoft では Windows Defender ファイアウォール規則を移行する PowerShell ベースのツールに取り組んでいます。 ツールをインストールして実行すると、Windows 10 クライアントの現在の構成に基づいた Intune 用のエンドポイント セキュリティ ファイアウォール規則ポリシーが自動的に作成されます。

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>エンドポイント セキュリティの攻撃の回避ポリシーにおけるデバイス制御プロファイルの新しい設定<!--7032084 -->
Microsoft では、エンドポイント セキュリティの攻撃の回避ポリシーのデバイス制御プロファイルに、Windowis 10 デバイス用のいくつかの設定を追加しています ( **[エンドポイント セキュリティ]**  >  **[攻撃の回避]**  >  **[ポリシーの作成]**  >  **[Windows 10 以降]**  >  **[デバイス制御]** )。 

新しい設定は、"*デバイス構成*" の [[デバイス制限プロファイル]](../configuration/device-restrictions-windows-10.md) で今日利用可能な設定と同じです。 "*デバイス制御*" のプロファイルに追加される設定には、さまざまな Bluetooth 設定が含まれます。  


<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。
