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
ms.openlocfilehash: 90039e9bb75bcf7c266ac033408f87d37e27ef8d
ms.sourcegitcommit: 7a5196d4d9736c5cd52a23155c479523e52a097d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84436756"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>iOS または iPadOS および macOS のポータル サイトの [デバイス] ページの改善<!-- 6055001  -->
iOS または iPadOS および Mac 用のポータル サイト アプリの **[デバイス]** ページにおけるユーザー エクスペリエンスがいくつか改善されました。 **[デバイス]** ページが改良され、より新しい印象になり、デバイス情報の編成が改善されました。 組織の iOS または iPadOS および macOS ユーザーは、定義されたセクション ヘッダーで 1 つの列を使用することで、自分のデバイスの状態を簡単に確認し、セキュリティで保護された状態と組織のリソースへのアクセスを維持できます。 さらに、デバイスがコンプライアンスに準拠していないユーザーのために、より明確なメッセージングとその他のトラブルシューティング手順が追加されました。 ポータル サイトの詳細については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」をご覧ください。

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>macOS 用ポータル サイトの登録エクスペリエンスの改善<!-- 6444452  -->
macOS 用ポータル サイトの登録エクスペリエンスにおいて登録プロセスが簡略化され、iOS 用ポータル サイトの登録エクスペリエンスとより厳密な一致がとれます。 デバイス ユーザーには次が表示されます。  
- より洗練されたユーザー インターフェイス。  
- 強化された登録チェックリスト。  
- デバイスの登録方法に関するより明確な説明。  
- 強化されたトラブルシューティング オプション。  

ポータル サイトの詳細については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」をご覧ください。

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>[自律的シングル App モード] 設定を使用して iOS ポータル サイトをサインインまたはサインアウト アプリとして構成する<!-- 7055619  -->
自律的シングル App モード (ASAM) を使用するように iOS ポータル サイトを構成できるようになります。 Microsoft Endpoint Manager コンソールの ASAM 設定を使用して、サインアウトとサインイン時にシングル App モードのオンとオフを切り替えるように iOS ポータル サイトを構成できます。 ポータル サイトが ASAM である場合、ユーザーは、ポータル サイトにサインインするまで、デバイスの他のアプリやホーム ボタンを使用できません。 サインアウト時に、ポータル サイトはシングル App モードに戻ります。 

Microsoft Endpoint Manager でポータル サイトを ASAM になるように設定するには、 **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。 プラットフォームとして **[iOS/iPadOS]** を選択し、プロファイルとして **[デバイスの制限]** を選択します。 **[構成設定]** タブで、 **[自律的シングル App モード]** を選択します。 **[アプリ名]** を `Company Portal` に設定し、 **[アプリ バンドル ID]** を `com.app.CompanyPortal` に設定します。 詳細については、「[自律的シングル App モード (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam)」と[シングル App モード](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1)に関するページをご覧ください。

<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>サード パーティの MDM パートナーからデバイス コンプライアンスの状態を設定する<!-- 6361689   -->
間もなく、サード パーティのモバイル デバイス管理 (MDM) パートナーによって管理されている iOS または Android デバイスのコンプライアンスの状態を Azure Active Directory (Azure AD) で設定できるようになります。

Intune がパートナーのコンプライアンス向けに構成されている場合、サード パーティの MDM パートナーによって管理されているデバイスのコンプライアンス データが、コンプライアンスの評価のために Intune に送信されます。 その結果は次に Azure AD に渡され、そこでコンプライアンス データを使用してこれらのデバイスの条件付きアクセス ポリシーが適用されます。

次のパートナーは間もなくサポートされます。
- VMware WorkspaceONE (旧称 AirWatch)

デバイス コンプライアンス パートナーを有効にするには、Microsoft Endpoint Manager admin center で新しいノードを使用します。 **[テナント管理]**  >  **[コネクタとトークン]**  >  **[パートナー コンプライアンス管理]** で **[コンプライアンス パートナーの追加]** を選択します。

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>コンプライアンス違反の電子メールにポータル サイト サポート Web サイトへのリンクを追加する<!-- 7225498    -->
非準拠デバイスがあるユーザーに送信される電子メール通知にポータル サイト Web サイトへのリンクを追加する新しい設定を、電子メール通知テンプレートに追加しています。 ( **[エンドポイント セキュリティ]**  >  **[デバイスのポリシー準拠]**  >  **[通知]**  >  **[通知の作成]** )。  非準拠デバイスがあるために電子メールを受信したユーザーは、リンクを使用して Web サイトを開き、自分のデバイスが準拠していない理由の詳細を知ることができます。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection デバイス構成ポリシーの新しい FileVault 設定<!-- 5459801   -->
[macOS Endpoint Protection](../protect/endpoint-protection-macos.md) テンプレート内の FileVault カテゴリに、次の新しい設定を追加しています: 回復キーを非表示にする ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[macOS]** を選択してから、"*プロファイルの種類*" として **[Endpoint Protection]** を選ぶ)。 この設定により、FileVault 2 の暗号化中は、エンド ユーザーに対して個人用キーが非表示になります。 デバイス ユーザーは、iOS ポータル サイト アプリから、または暗号化された macOS デバイス用のポータル Web サイトから、いつでも自分の個人用回復キーを表示することができます。 個人用回復キーを表示するには、[デバイスの詳細] に移動し、 *[回復キーの取得]* をクリックします。

この設定は、以前に作成されたポリシーでは使用できません。 この設定を利用するように構成するには、FileVault ポリシーを再作成する必要があります。 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>macOS デバイスでコンテンツ キャッシングを構成する<!-- 7106872 -->
macOS デバイスで、コンテンツ キャッシングを構成する構成プロファイルを作成できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[macOS]** を選択 > プロファイルに **[デバイス機能]** を選択)。 これらの設定を使用して、キャッシュの削除、共有キャッシュの許可、ディスク上のキャッシュ制限などを行います。

コンテンツ キャッシングの詳細については、「[ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching)」をご覧ください (Apple の Web サイトが開きます)。

現在構成できる設定を確認するには、「[Intune での macOS デバイスの機能設定](../configuration/macos-device-features-settings.md)」をご覧ください。

適用対象:
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Windows 10 以降のデバイス向けの新しい VPN 設定<!-- 6602122  -->
IKEv2 の接続の種類を使用して VPN プロファイルを作成する場合、構成可能な新しい設定があります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[Windows 10 以降]** を選択 > プロファイルに **[VPN]** を選択 > **[基本 VPN]** )。

- **デバイス トンネル**:ユーザーのログオンなど、ユーザー操作を必要とせずに、デバイスが VPN に自動的に接続できるようにします。 この機能を使用するには、 **[Always On]** を有効にし、認証方法として **[コンピューターの証明書]** を使用する必要があります。
- 暗号化スイートの設定:IKE と子セキュリティ アソシエーションをセキュリティで保護するために使用するアルゴリズムを構成します。これにより、クライアントとサーバーの設定を一致させることができます。

構成できる設定を確認するには、[Intune を使用して VPN 接続を追加するための Windows デバイス設定](../configuration/vpn-settings-windows-10.md)に関する記事をご覧ください。

適用対象:
- Windows 10 以降

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>共有 iPad デバイスで共有 iPad の一時セッションをブロックする<!-- 6613794 -->
Intune に、共有 iPad デバイスでの一時的なセッションをブロックする新しい **[Block Shared iPad temporary sessions]\(共有 iPad の一時セッションをブロックする\)** 設定があります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[iOS/iPadOS]** を選択 > プロファイルの種類に **[デバイスの制限]** を選択 > **[共有 iPad]** )。 有効にすると、エンド ユーザーが Guest アカウントを使用できなくなります。 ユーザーは、各自の管理対象の Apple ID とパスワードを使用してデバイスにサインインする必要があります。 

構成できる設定の詳細については、[機能を許可または制限するための iOS および iPadOS デバイスの設定](../configuration/device-restrictions-ios.md)に関する記事をご覧ください。

適用対象:
- iOS または iPadOS 13.4 以降を実行している共有 iPad デバイス

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>フル マネージドの Android エンタープライズ デバイスの起動ツールとして Microsoft Launcher を使用する<!-- 4927976  -->
Android エンタープライズ デバイス所有者デバイスでは、Microsoft Launcher をフル マネージド デバイスの既定の起動ツールとして設定できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[Android エンタープライズ]** を選択 > **[デバイスの所有者]**  >  プロファイルに **[デバイスの制限]** を選択 > **[デバイス エクスペリエンス]** )。 その他のすべての Microsoft Launcher 設定を構成するには、アプリ構成ポリシーを使用します。 

また、他にもいくつかの UI 更新があります。たとえば、 **[専用デバイス]** が **[デバイス エクスペリエンス]** に名前変更されます。

制限できるすべての設定を確認するには、「[Intune を使用して機能を許可または制限するように Android エンタープライズ デバイスを設定する](../configuration/device-restrictions-android-for-work.md)」をご覧ください。 

適用対象:
- Android エンタープライズ デバイス所有者フル マネージド デバイス (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>Android エンタープライズで OEMConfig を使用し、新しいスキーマ設定の追加と既存のスキーマ設定の検索を行う<!-- 6394386  -->
Intune で、OEMConfig を使用して Android エンタープライズ デバイスの設定を管理できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[Android エンタープライズ]** を選択 > プロファイルに **[OEMConfig]** を選択)。 **構成デザイナー**を使用すると、アプリ スキーマのプロパティが表示されます。 現在、**構成デザイナー**では次のことができます。
- アプリ スキーマに新しい設定を追加する。
- アプリ スキーマで新しい設定および既存の設定を検索する。

Intune での OEMConfig プロファイルの詳細については、「[Microsoft Intune で、OEMConfig を使って Android Enterprise デバイスを使用および管理する](../configuration/android-oem-configuration-overview.md)」をご覧ください。

適用対象:
- Android エンタープライズ

<!-- ***********************************************-->
## <a name="device-enrollment"></a>デバイスの登録

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>デバイスの自動登録の同期エラー<!-- 6988214 -->
iOS または iPadOS および macOS デバイスに対して、次のような新しいエラーが報告されます
- 電話番号に無効な文字が含まれているか、そのフィールドが空である。 
- プロファイルの構成名が無効または空である。 
- カーソルの値が無効または期限切れであるか、カーソルが見つからない。
- トークンが拒否されたか、期限切れである。 
- 部署フィールドが空であるか、長すぎる。 
- Apple でプロファイルが見つからず、新しいプロファイルを作成する必要がある。 
- 削除された Apple Business Manager デバイスの数が [概要] ページに追加され、デバイスの状態が表示される。

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>個人所有デバイスでは、VPN を使用して展開できる<!--5015344 -->
新しいオートパイロット プロファイル **[ドメインの接続チェックをスキップする]** 切り替えを使用すると、社内のネットワークにアクセスせずに、独自のサードパーティ製の Win32 VPN クライアントを使用して、Hybrid Azure AD Join デバイスを展開できます。 新しい切り替えを表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**   >  **[Windows]**  >  **[Windows 登録]**  >  **[展開プロファイル]**  >  **[プロファイルの作成]**  >  **[Out-of-box experience (OOBE)]** の順に移動します。

### <a name="shared-ipads-for-business--6367326---"></a>法人向け共有 iPad<!--6367326 -->
Intune と Apple Business Manager を使用して、複数の従業員がデバイスを共有できるように共有 iPad を簡単かつ安全に設定できるようになります。 Apple の [共有 iPad](https://developer.apple.com/education/shared-ipad/) では、ユーザー データを保持しながら、複数のユーザーに対してパーソナライズされたエクスペリエンスが提供されます。 ユーザーは、管理対象 Apple ID を使用して、組織内の共有 iPad にサインインした後、アプリ、データ、設定にアクセスできます。 共有 iPad はフェデレーション ID と連動します。

この機能を表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** の順に移動し、トークンを選択して、 **[プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS]** の順に移動します。 **[管理の設定]** ページで、 **[ユーザー アフィニティを使用しないで登録する]** を選択すると、 **[共有 iPad]** オプションが表示されます。

**適用対象:** iPadOS 13.4 以降。 このリリースでは、ユーザーが管理対象 Apple ID を使用せずにデバイスにアクセスできるように、共有 iPad での一時的なセッションのサポートが追加されました。 ログアウト時に、デバイスではすべてのユーザー データが消去されるため、デバイスをすぐに使用できる状態になり、デバイスのワイプは不要になります。 

<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>共同管理デバイスのプライマリ ユーザーを変更する<!--7319183 -->
共同管理されている Windows デバイスについて、デバイスのプライマリ ユーザーを変更できるようになります。 その確認および変更方法の詳細については、「[Intune デバイスのプライマリ ユーザーを確認する](../remote-actions/find-primary-user.md)」をご覧ください。

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics には、デバイスの詳細ログが含まれる<!--6014987  -->
Intune デバイスの詳細ログは、 **[レポート]**  >  **[ログ分析]** で入手できます。 デバイスの詳細を相互に関連付けて、カスタム クエリと Azure ブックを作成することができます。

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Intune プライマリ ユーザーを設定すると Azure AD の所有者プロパティも設定される<!--7319227 -->
この今後の機能では、新しく登録された Hybrid Azure AD Join を使用したデバイスの所有者プロパティが、Intune プライマリ ユーザーが設定されるのと同時に自動的に設定されます。 プライマリ ユーザーの詳細については、「[Intune デバイスのプライマリ ユーザーを確認する](../remote-actions/find-primary-user.md)」をご覧ください。

これは登録プロセスに加えられる変更であり、新しく登録されたデバイスにのみ適用されます。 既存の Hybrid Azure AD Join を使用したデバイスの場合、Azure AD の所有者プロパティを手動で更新する必要があります。 これを行うには、[プライマリ ユーザーの変更機能](../remote-actions/find-primary-user.md#change-a-devices-primary-user)または[スクリプト](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)を使用できます。

Windows 10 デバイスに対して Hybrid Azure Azure Directory Join が使用されるようになると、デバイスの最初のユーザーがエンドポイント マネージャーのプライマリ ユーザーになります。  現時点では、このユーザーは、対応する Azure AD デバイス オブジェクトでは設定されません。 これにより、Azure AD ポータルの "*所有者*" プロパティと Microsoft Endpoint Manager admin center の "*プライマリ ユーザー*" プロパティを比較したときに不整合が生じます。 Azure AD の所有者プロパティは、BitLocker 回復キーへのアクセスをセキュリティで保護するために使用されます。 このプロパティは、Hybrid Azure AD Join を使用したデバイスでは設定されません。 この制限により、Azure AD からの BitLocker 回復のセルフサービスの設定が妨げられます。 この今後の機能では、この制限が解決されます。

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

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>macOS デバイスのリモート ロック PIN の可用性<!--7281557-->
macOS デバイスのリモート ロック PIN の可用性は、7 日から 30 日に延長されます。

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
