---
title: Microsoft Intune の新機能 - Azure | Microsoft Docs
titleSuffix: ''
description: Intune Azure Portal の新機能を確認する
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 46c58437fab66b0a4fd22ea8452856ca701e9eb7
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546811"
---
# <a name="whats-new-in-microsoft-intune"></a>Microsoft Intune の新機能

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で Microsoft Intune の週ごとの新機能について説明します。 また、[重要なお知らせ](#notices)、[過去のリリース](whats-new-archive.md)、および [Intune サービスの更新プログラムのリリース方法](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)に関する情報もあります。 

> [!Note]
> 個々の[マンスリー更新プログラム](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)は、展開に最大 3 日かかることがあります。順序は次のとおりです。
>
> - 1 日目:アジア太平洋 (APAC)
> - 2 日目:ヨーロッパ、中東、アフリカ (EMEA)
> - 3 日目:北米
> - 4 日目以降:政府機関向け Intune
>
> 一部の機能は数週間にわたってロールアウトされ、一部のお客様は最初の週にご利用になれない可能性があります。
>
> リリースの今後の機能の一覧については、[開発中のページ](in-development.md)を参照してください。

**RSS フィード**:ご自身のフィード リーダーに次の URL をコピーして貼り付けることで、このページの更新時に通知を受け取ることができます。`https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts

<!-- ########################## -->
## <a name="week-of-july-27-2020"></a>2020 年 7 月 27 日の週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

#### <a name="power-bi-compliance-report-template-v20---636958---"></a>Power BI コンプライアンス レポート テンプレート V2.0<!-- 636958 -->
Power BI テンプレート アプリを使用すると、Power BI パートナーはコーディングをほとんどまたはまったく行わずに Power BI アプリを構築し、それを Power BI の顧客にデプロイすることができます。 管理者は、Power BI コンプライアンス レポート テンプレートのバージョンを V1.0 から V2.0 に更新できます。 V2.0 では、設計が改善され、テンプレートの一部として表示される計算とデータが変更されます。 詳細については、「[Power BI でデータ ウェアハウスに接続する](../developer/reports-proc-get-a-link-powerbi.md)」と「[テンプレート アプリを更新する](https://docs.microsoft.com/power-bi/service-template-apps-install-distribute#update-a-template-app)」を参照してください。 また、ブログ記事「[Announcing a New Version of the PowerBI Compliance Report with Intune Data Warehouse](https://aka.ms/new_compliance_report)」 (Intune データ ウェアハウスを使用した PowerBI コンプライアンス レポートの新しいバージョンの発表) を参照してください。

<!-- ########################## -->
## <a name="week-of-july-13-2020--2007-service-release"></a>2020 年 7 月 13 日の週 (2007 サービス リリース)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Win32 アプリのインストール通知とポータル サイト<!-- 7485945  -->
エンド ユーザーは、[Microsoft Intune Web ポータル サイト](https://portal.manage.microsoft.com/)に表示されるアプリケーションが、ポータル サイト アプリまたは Web ポータル サイトのどちらで開かれるようにするかを決めることができます。 このオプションは、エンド ユーザーがポータル サイト アプリをインストールしており、ブラウザーの外部で Web ポータル サイト アプリケーションを起動する場合にのみ使用できます。 

#### <a name="exchange-on-premises-connector-support---7138486----"></a>Exchange On-Premises コネクタのサポート<!-- 7138486  -->
Intune では、2007 (7 月) リリース以降、Intune サービスから Exchange On-Premises Connector 機能のサポートが削除されます。 アクティブなコネクタを使用している既存のお客様は、現時点では現在の機能を引き続きお使いいただけます。 新規のお客様や、アクティブなコネクタをお持ちでない既存のお客様は、Intune での新しいコネクタの作成、または Exchange ActiveSync (EAS) デバイスの管理ができなくなります。 そのようなお客様の場合、Microsoft では、Exchange の[ハイブリッド先進認証 (HMA)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) を使用して Exchange On-Premises へのアクセスを保護することをお勧めします。 HMA を使用すると、Intune App Protection ポリシー (MAM とも呼ばれます) と Outlook Mobile を使用した条件付きアクセスの両方が Exchange On-Premises に対して有効になります。

#### <a name="smime-for-outlook-on-ios-and-android-devices-without-enrollment---6517155---"></a>登録なしの iOS および Android デバイス上での Outlook の S/MIME<!-- 6517155 -->
マネージド アプリのアプリ構成ポリシーを使用して、iOS および Android デバイスで Outlook の S/MIME を有効にできるようになりました。 これにより、デバイスの登録状態に関係なく、ポリシーの配信が可能になります。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド アプリ]** の順に選択します。 さらに、Outlook 上でユーザーによるこの設定の変更を許可するかどうかの選択ができます。 ただし、Outlook for iOS および Outlook for Android に S/MIME 証明書を自動的に展開するには、デバイスを登録する必要があります。 S/MIME の一般情報については、「[Intune で電子メールに署名し、暗号化する S/MIME の概要](https://docs.microsoft.com/mem/intune/protect/certificates-s-mime-encryption-sign)」を参照してください。 Outlook の構成設定の詳細については、[Microsoft Outlook の構成設定](../apps/app-configuration-policies-outlook.md)に関するページと、「[デバイス登録なしで管理対象アプリ用アプリ構成ポリシーを追加する](../apps/app-configuration-policies-managed-app.md)」を参照してください。 Outlook for iOS および Outlook for Android の S/MIME 情報については、「[S/MIME シナリオ](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios)」と、[「構成キー」の「S/MIME 設定」](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings)を参照してください。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>デバイスの構成

#### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122-----"></a>Windows 10 以降のデバイス向けの新しい VPN 設定<!-- 6602122   -->

IKEv2 の接続の種類を使用して VPN プロファイルを作成する場合、構成可能な新しい設定があります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[Windows 10 以降]** を選択 > プロファイルに **[VPN]** を選択 > **[基本 VPN]** )。

- **デバイス トンネル**:ユーザーのログオンなど、ユーザー操作を必要とせずに、デバイスが VPN に自動的に接続できるようにします。 この機能を使用するには、 **[Always On]** を有効にし、認証方法として **[コンピューターの証明書]** を使用する必要があります。
- 暗号化スイートの設定:IKE と子セキュリティ アソシエーションをセキュリティで保護するために使用するアルゴリズムを構成します。これにより、クライアントとサーバーの設定を一致させることができます。

構成できる設定を確認するには、[Intune を使用して VPN 接続を追加するための Windows デバイス設定](../configuration/vpn-settings-windows-10.md)に関する記事をご覧ください。

適用対象:

- Windows 10 以降

#### <a name="configure-more-microsoft-launcher-settings-in-a-device-restrictions-profile-on-android-enterprise-devices-cobo---6285001----"></a>Android Enterprise デバイス (COBO) のデバイス制限プロファイルで、その他の Microsoft Launcher 設定を構成する<!-- 6285001  -->

Android Enterprise フル マネージド デバイスでは、デバイスの制限プロファイルを使用して、その他の Microsoft Launcher 設定を構成できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームとして **[Android Enterprise]** > **[デバイスの所有者のみ]**  >  **[デバイスの制限]**  >  **[デバイス エクスペリエンス]**  >  **[フル マネージド]** )。 

これらの設定を確認するには、[Android Enterprise デバイスの機能を許可または制限する設定](../configuration/device-restrictions-android-for-work.md#device-experience)に関するページを参照してください。

[アプリ構成プロファイル](../apps/configure-microsoft-launcher.md)を使用して Microsoft Launcher 設定を構成することもできます。

適用対象:

- Android エンタープライズ デバイス所有者フル マネージド デバイス (COBO)

#### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184---idstaged---"></a>Android エンタープライズ デバイス所有者の専用デバイス (COSU) 上での Managed Home Screen の新機能<!-- 7414175 7133328 7133720 7134873 7135184   idstaged -->

Android Enterprise デバイス上で、管理者はデバイス構成プロファイルを使用して、マルチアプリ キオスク モードを使用している専用デバイスの Managed Home Screen をカスタマイズできます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > プラットフォームとして **[Android Enterprise]** > **[デバイスの所有者のみ]**  > プロファイルの **[デバイスの制限]** > **[デバイス エクスペリエンス]**  >  **[専用デバイス]**  >  **[複数アプリ]** )。

具体的には次のことができます。

- アイコンをカスタマイズする、画面の向きを変更する、バッジ アイコンでアプリ通知を表示する <!--7414175-->
- マネージド設定のショートカットを非表示にする <!--7133328-->
- より簡単にデバッグ メニューにアクセスする <!--7133720-->
- 許可されている Wi-Fi ネットワークの一覧を作成する <!-- 7134873-->
- より簡単にデバイス情報にアクセスする <!-- 7135184-->

詳細については、[機能を許可または制限する Android Enterprise デバイスの設定](../configuration/device-restrictions-android-for-work.md)に関するページと、[こちらのブログ](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060)を参照してください。

適用対象:

- Android エンタープライズ デバイス所有者、専用デバイス (COSU)

#### <a name="administrative-templates-updated-for-microsoft-edge-84--7722068--"></a>更新された Microsoft Edge 84 管理用テンプレート<!--7722068-->
Microsoft Edge で使用可能な ADMX 設定が更新されました。 エンド ユーザーは、Edge 84 で追加された新しい ADMX 設定を構成して展開できるようになりました。 詳細については、[Edge 84 のリリース ノート](https://docs.microsoft.com/deployedge/microsoft-edge-relnote-stable-channel#policy-updates)を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>デバイスの登録

#### <a name="corporate-owned-personally-enabled-devices-preview--4442275----"></a>企業所有の個人対応デバイス (プレビュー)<!--4442275  -->
Intune では、OS バージョンが Android 8 以降の仕事用プロファイルを使用する Android Enterprise 企業所有デバイスがサポートされるようになりました。 仕事用プロファイルを使用する企業所有デバイスは、Android Enterprise ソリューション セットの企業管理シナリオの 1 つです。 このシナリオは、企業および個人使用が想定されている単一ユーザーのデバイスに対応しています。 この企業所有の個人対応 (COPE) シナリオでは、次のことが実現されます。

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

仕事用プロファイル プレビューでの企業所有の詳細については、[サポートのブログ](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325)を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805-----"></a>macOS デバイスのリモート ロック操作に対する更新<!--7032805   -->
macOS デバイスのリモート ロック操作に対する変更には、以下が含まれます。
- 回復用 PIN は、削除される 30 日前 (7 日ではなく) に表示されます。
- 管理者が 2 つ目のブラウザーを開いていて、別のタブまたはブラウザーからコマンドのトリガーを再試行した場合、Intune によってコマンドの実行が許可されます。 ただし、新しい PIN は生成されず、レポートの状態は "失敗" に設定されます。
- 前のコマンドが引き続き保留中の場合、またはデバイスが再チェックインされていない場合、管理者は別のリモート ロック コマンドを発行することはできません。
これらの変更は、複数のリモート ロック コマンドの後に正しい PIN が上書きされないように設計されています。

#### <a name="device-actions-report-differentiates-between-wipe-and-protected-wipe--7118901---"></a>デバイス アクション レポートでワイプと保護されたワイプが区別される<!--7118901 -->
**デバイス アクション** レポートで、ワイプと保護されたワイプのアクションが区別されるようになりました。 レポートを確認するには、[Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[モニター]**  >  **[デバイス操作]** ( **[その他]** の下) の順に移動します。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>デバイス セキュリティ

#### <a name="microsoft-defender-firewall-rule-migration-tool-preview---6423187-----"></a>Microsoft Defender ファイアウォール規則の移行ツール プレビュー<!-- 6423187   -->
パブリック プレビューとして、Microsoft では Microsoft Defender ファイアウォール規則を移行する PowerShell ベースのツールに取り組んでいます。 ツールをインストールして実行すると、Windows 10 クライアントの現在の構成に基づいた Intune 用のエンドポイント セキュリティ ファイアウォール規則ポリシーが自動的に作成されます。 詳細については、「[エンドポイント セキュリティ ファイアウォール規則の移行ツールの概要](../protect/endpoint-security-firewall-rule-tool.md)」を参照してください。

#### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-generally-available---7303816-----"></a>テナントに接続されたデバイスを MDATP にオンボードするためのエンドポイントの検出と応答ポリシーの一般提供が開始<!-- 7303816   -->
Intune のエンドポイント セキュリティの一部として、[Configuration Manager によって管理されているデバイスで使用する、エンドポイントの検出と応答 (EDR) ポリシー](../protect/endpoint-security-edr-policy.md)は、"*プレビュー*" が終了し、"*一般提供*" が開始されました。

デバイスで、サポートされているバージョンの Configuration Manager から EDR ポリシーを使用するには、[Configuration Manager にテナントの接続](../../configmgr/tenant-attach/device-sync-actions.md)を構成します。 テナント接続の構成を完了した後、EDR ポリシーを展開して、Configuration Manager によって管理されているデバイスを Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) にオンボードできます。

#### <a name="bluetooth-settings-are-available-in-device-control-profiles-for-endpoint-security-attack-surface-reduction-policy---7032084-----"></a>エンドポイント セキュリティ攻撃の回避ポリシーのデバイス制御プロファイルで Bluetooth の設定が使用可能 <!--7032084   -->
"*エンドポイント セキュリティ攻撃の回避ポリシー*" の[デバイス制御プロファイル](../protect/endpoint-security-asr-profile-settings.md#device-control-profile)に、Windows 10 デバイスの Bluetooth を管理するための設定が追加されました。  これらは、"*デバイス構成*" のデバイス制限プロファイルで従来から使用できる設定と同じです。

#### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801-----"></a>Windows 10 デバイスのエンドポイント セキュリティ ウイルス対策ポリシーを使用して、定義の更新用のソースの場所を管理する<!-- 6347801   -->  
デバイスで更新定義を取得する方法の管理に役立つ、[Windows 10 デバイス向けエンドポイント セキュリティのウイルス対策ポリシー](../protect/antivirus-microsoft-defender-settings-windows.md#updates)で、"*更新*" カテゴリに 2 つの新しい設定を追加しました。

- *定義ファイルの更新をダウンロードするためのファイル共有を定義する*
- *定義ファイルの更新をダウンロードするためのソースの順序を定義する*

新しい設定を利用すると、定義の更新用のダウンロード元の場所として UNC ファイル共有を追加したり、異なるソースの場所に接続するときの順序を定義したりすることができます。

#### <a name="improved-security-baselines-node---7433136------"></a>改善されたセキュリティ ベースライン ノード<!-- 7433136    -->
Microsoft エンドポイント マネージャー管理センターの[セキュリティ ベースライン ノード](../protect/security-baselines.md)の使いやすさを向上させるためにいくつかの変更が加えられました。 **[エンドポイント セキュリティ]**  >  **[セキュリティのベースライン]** にドリルインし、MDM セキュリティ ベースラインなどのセキュリティ ベースラインの種類を選択すると、 **[プロファイル]** ペインが表示されます。 [プロファイル] ペインに、そのベースラインの種類用に作成したプロファイルが表示されます。  以前は、コンソールに [概要] ペインが表示されていました。そこに含まれていた集計データの累計は、個々のプロファイルのレポートに示されている詳細情報と必ずしも一致していませんでした。

引き続き、[プロファイル] ペインからプロファイルを選択してドリルインしたそのプロファイルのプロパティのほかに、 *[モニター]* で使用できるさまざまなレポートも表示することができます。  同様に、[プロファイル] と同じレベルでは引き続き、 **[バージョン]** を選択し、展開したそのプロファイルの種類のさまざまなバージョンを表示できます。 プロファイル レポートと同様に、バージョンにドリルインすると、レポートにもアクセスできます。 

#### <a name="derived-credentials-support-for-windows---4886090-----"></a>Windows の派生資格情報のサポート<!-- 4886090   -->
Windows デバイスで、派生した資格情報を使用できるようになりました。 iOS/iPadOS と Android に対する既存のサポートが拡張され、同じ派生資格情報プロバイダーで使用できるようになります。
- Entrust Datacard
- Intercede
- DISA Purebred

Widows のサポートには、Wi-Fi または VPN プロファイルを認証するための派生資格情報の使用が含まれます。 Windows デバイスの場合、派生資格情報は、使用する派生資格情報プロバイダーによって提供されるクライアント アプリから発行されます。

#### <a name="manage-filevault-encryption-for-devices-that-were-encrypted-by-the-device-user-and-not-by-intune--5239424----"></a>Intune ではなく、デバイスのユーザーによって暗号化されたデバイスの FileVault 暗号化を管理する<!--5239424  -->
Intune では、Intune ポリシーではなく、[macOS デバイスでデバイスのユーザーによって暗号化された FileVault ディスク暗号化の管理を想定](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices)できるようになりました。  このシナリオでは、次のことが必要です。
- デバイスで、FileVault を有効にする Intune からディスク暗号化ポリシーを受信します。
- デバイスのユーザーが、ポータル Web サイトを使用して、暗号化されたデバイスの個人用回復キーを Intune にアップロードします。 キーをアップロードするには、暗号化された macOS デバイスの *[Store recovery key]\(回復キーの保存\)* オプションを選択します。

ユーザーが回復キーをアップロードすると、Intune によってキーがローテーションされて、それが有効であることが確認されます。 Intune では、ポリシーを使用してデバイスを直接暗号化した場合と同様に、キーと暗号化を管理できるようになりました。 ユーザーは、デバイスを回復する必要がある場合、次の場所にある任意のデバイスを使用して回復キーにアクセスできます。   
- ポータル Web サイト
- iOS/iPadOS 用ポータル サイト アプリ 
- Android 用ポータル サイト アプリ
- Intune アプリ

#### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632--"></a>macOS FileVault のディスク暗号化中にデバイス ユーザーの個人用回復キーを非表示にする<!--  5475632-->
エンドポイント セキュリティ ポリシーを使用して macOS FileVault ディスク暗号化を構成するとき、[ **[Hide recovery key]\(回復キーを非表示にする\)** ](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) 設定を使用して、デバイスが暗号化されている間、デバイスのユーザーに "*個人用回復キー*" が表示されないようにします。 暗号化中にキーを非表示にすることで、デバイスの暗号化を待機している間にユーザーが書き留めることはできなくなるため、セキュリティを確保することができます。 

後から、回復が必要な場合は、ユーザーはいつでも任意のデバイスを使用して、Intune ポータル Web サイト、iOS/iPadOS ポータル サイト、Android ポータル サイト、または Intune アプリ経由で個人用回復キーを表示することができます。

#### <a name="improved-view-of-security-baseline-details-for-devices---5536846----"></a>デバイスのセキュリティ ベースラインの詳細のビューが改善されている<!-- 5536846  -->
デバイスの詳細にドリルインして、デバイスに適用されるセキュリティ ベースラインの設定の詳細を表示できるようになりました。 設定はシンプルで単純なリストに表示されます。このリストには、設定カテゴリ、設定名、状態が含まれます。 詳細については、「[デバイスごとのエンドポイントのセキュリティ構成を表示する](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)」を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

#### <a name="device-compliance-logs-now-in-english--6014904----"></a>デバイス コンプライアンス ログが英語で利用可能になっている<!--6014904  -->
Intune DeviceComplianceOrg のログには、以前は ComplianceState、OwnerType、および DeviceHealthThreatLevel の列挙のみが含まれていました。 現在、これらのログには、列内に英語の情報が含まれています。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>ロール ベースのアクセス制御

#### <a name="assign-profile-and-update-profile-permission-changes--7177586-idready-wnready-wnstaged--"></a>[プロファイルの割り当て] と [プロファイルの更新] アクセス許可の変更<!--7177586 idready wnready wnstaged-->
自動デバイス登録フローの割り当てプロファイルおよび更新プロファイルで、ロールベースのアクセス制御のアクセス許可が変更されました。

プロファイルの割り当て:このアクセス許可を持つ管理者は、自動デバイス登録の場合、複数のトークンへのプロファイルの割り当てと、1 つのトークンへの既定のプロファイルの割り当てもできます。

プロファイルの更新:このアクセス許可を持つ管理者は、自動デバイス登録の場合にのみ、既存のプロファイルを更新できます。

これらのロールを表示するには、[Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[テナント管理]**  >  **[ロール]**  >  **[All roles]\(すべてのロール\)**  >  **[作成]**  >  **[アクセス許可]**  >  **[ロール]** に移動します。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>スクリプト

#### <a name="additional-data-warehouse-v10-properties---6125732-wnready---"></a>追加の Data Warehouse v1.0 プロパティ<!-- 6125732 wnready -->
Intune Data Warehouse v1.0 を使用して、追加のプロパティを使用できます。 次のプロパティが、[device](../developer/reports-ref-devices.md#devices) エンティティを介して公開されるようになりました。
- `ethernetMacAddress` - このデバイスの一意のネットワーク識別子。
- `office365Version` - デバイスにインストールされている Office 365 のバージョン。

次のプロパティが、[devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) エンティティを介して公開されるようになりました。
- `physicalMemoryInBytes` - 物理メモリ (バイト単位)。
- `totalStorageSpaceInBytes` - 記憶域の合計容量 (バイト単位)。

詳細については、「[Microsoft Intune データ ウェアハウス API](../developer/reports-nav-intune-data-warehouse.md)」を参照してください。

<!-- ########################## -->
## <a name="week-of-july-06-2020"></a>2020 年 7 月 6 日の週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023---"></a>Android 上のポータル サイトおよび Intune アプリのデバイス アイコンを更新する<!-- 6057023 -->
Microsoft では、より新しい外観を作成し、Microsoft Fluent Design System に準拠するように、Android デバイス上のポータル サイトと Intune アプリのデバイス アイコンを更新しました。 関連する情報については、「[iOS または iPadOS および macOS 用のポータル サイト アプリのアイコンの更新](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-)」を参照してください。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>デバイスの登録

#### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707---"></a>iOS ポータル サイトでは、ユーザー アフィニティなしでの Apple の自動デバイス登録がサポートされます<!-- 7282707 --> 
割り当てられたユーザーを必要とせずに Apple の自動デバイス登録を使用して登録されたデバイス上で、iOS ポータル サイトがサポートされるようになりました。 エンド ユーザーは、iOS ポータル サイトにサインインして、デバイス アフィニティなしで登録された iOS/iPadOS デバイス上で、自身をプライマリ ユーザーとして確立できます。 自動デバイス登録に関する詳細については、「[Apple の自動デバイス登録を使用して iOS または iPadOS デバイスを自動登録する](../enrollment/device-enrollment-program-enroll-ios.md)」を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview---7552762---"></a>テナントのアタッチ:管理センターでの ConfigMgr クライアントの詳細 (プレビュー)<!-- 7552762 -->

Microsoft Endpoint Manager admin center で、特定のデバイスのコレクション、境界グループのメンバーシップ、およびリアルタイムのクライアント情報を含む ConfigMgr クライアントの詳細を確認できるようになりました。 詳細については、「[テナントのアタッチ:管理センターでの ConfigMgr クライアントの詳細 (プレビュー)](../../configmgr/tenant-attach/client-details.md)」をご覧ください。

## <a name="week-of-june-22-2020"></a>2020 年 6 月 22 日の週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Intune 用に新しく利用可能になった保護されたアプリ<!-- 7248952 -->
次の保護されたアプリを使用できるようになりました。
- BlueJeans Video Conferencing
- Cisco Jabber for Intune
- Tableau Mobile for Intune
- ZERO for Intune

保護されたアプリの詳細については、「[保護されている Microsoft Intune アプリ](../apps/apps-supported-intune-apps.md)」を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>エンドポイント分析を使用してユーザーの生産性を向上させ、IT サポート コストを削減する<!-- 5653063 --> 
次の週の間、この機能はロール アウトされます。エンドポイント分析は、ユーザー エクスペリエンスに関する分析情報を提供することで、ユーザーの生産性を向上させ、IT サポートのコストを削減することを目的としています。 IT 部門は、この分析情報を使用して、プロアクティブなサポートによりエンド ユーザー エクスペリエンスを最適化したり、構成変更がもたらすユーザーへの影響を評価して、ユーザー エクスペリエンスの低下を検知したりすることができます。 詳細については、[エンドポイント分析のプレビュー](https://aka.ms/uea)に関する記事を参照してください。

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>スクリプト パッケージを使用してエンド ユーザー デバイスの問題を事前に修復する<!-- 5933328 -->
エンド ユーザー デバイスでスクリプト パッケージを作成して実行し、組織内の上位のサポート問題を事前に見つけて修復することができます。 スクリプト パッケージを展開することは、サポートへの問い合わせを減らすのに役立ちます。 独自のスクリプト パッケージを作成するか、当社が作成して社内で使用しているスクリプト パッケージのいずれかを展開するかを選択してサポート チケットを減らします。 Intune では、展開されたスクリプト パッケージの状態を確認したり、検出と修復の結果を監視したりすることができます。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[レポート]**  >  **[エンドポイント分析]**  >  **[プロアクティブな修復]** の順に選択します。 詳細については、「[プロアクティブな修復](https://aka.ms/uea_prs)」を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>デバイス セキュリティ

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Android 用のコンプライアンス ポリシーで Microsoft Defender ATP を使用する<!-- 4425686  -->

Intune を使用して、[Android デバイスを Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) にオンボード](../protect/advanced-threat-protection-configure.md#onboard-devices)できるようになりました。 登録済みデバイスがオンボードされた後、Android 用のコンプライアンス ポリシーでは、Microsoft Defender ATP からの "*脅威レベル*" シグナルを使用することができます。 これらは、Windows 10 デバイスで以前に使用できたものと同じシグナルです。

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563----"></a>Android デバイス用に Defender ATP Web 保護を構成する<!-- 6185563  -->

Android デバイスで Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を使用する場合は、[Microsoft Defender ATP Web 保護を構成](../protect/advanced-threat-protection-manage-android.md)し、フィッシング スキャン機能を無効にしたり、スキャンで VPN が使用されないようにすることができます。

Android デバイスがどのように Intune に登録されるかに応じて、次のオプションを使用できます。

- Android デバイス管理者 - カスタム OMA-URI 設定を使用して、Web 保護機能を無効にするか、スキャン中の VPN の使用のみを無効にします。
- Android Enterprise 仕事用プロファイル - アプリ構成プロファイルと構成デザイナーを使用して、すべての Web 保護機能を無効にします。

<!-- ########################## -->
## <a name="week-of-june-15-2020--2006-service-release"></a>2020 年 6 月 15 日の週 (2006 サービス リリース)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>マネージド アプリの通信データ転送保護<!-- 6884491  -->
保護されたアプリでハイパーリンクされた電話番号が検出されると、その番号をダイヤラー アプリに転送できるようにするための保護ポリシーが適用されているかどうかが Intune によって確認されます。 ポリシー マネージド アプリから開始された場合に、この種のコンテンツ転送をどのように扱うかを選択することができます。 Microsoft Endpoint Manager でアプリ保護ポリシーを作成する場合は、 **[他のアプリに組織データを送信]** からマネージド アプリ オプションを選び、 **[Transfer telecommunications data to]\(通信データの転送先\)** からオプションを選択します。 このデータ保護設定の詳細については、「[Microsoft Intune の Android アプリ保護ポリシー設定](../apps/app-protection-policy-settings-android.md)」と「[iOS アプリ保護ポリシー設定](../apps/app-protection-policy-settings-ios.md)」を参照してください。 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>ポータル サイトでの Azure AD Enterprise と Office Online アプリケーションの統合配信<!-- 7414033  -->
Intune の **[カスタマイズ]** ウィンドウで、**Azure AD Enterprise アプリケーション**と **Office Online アプリケーション**の両方を、ポータル サイトで **[非表示]** または **[表示]** することを選択できます。 各エンド ユーザーには、選択された Microsoft サービスによるアプリケーション カタログ全体が表示されます。 既定では、追加のアプリ ソースがそれぞれ **[非表示]** に設定されるようになります。 この機能は、まず、ポータル サイト Web サイトで有効になり、Windows ポータル サイトでサポートされる予定です。 この構成設定を見つけるには、[Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[テナント管理]**  >  **[カスタマイズ]** の順に選択します。 関連情報については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」を参照してください。

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>macOS 用ポータル サイトの登録エクスペリエンスの改善<!-- 6444452  -->
macOS の登録エクスペリエンス用のポータル サイトには、よりシンプルな登録プロセスが備わっています。これにより、iOS の登録エクスペリエンス用のポータル サイトと、より厳密な一致がとれます。 デバイス ユーザーには以下のものが表示されます。  
- より洗練されたユーザー インターフェイス。  
- 強化された登録チェックリスト。  
- デバイスの登録方法に関するより明確な説明。  
- 強化されたトラブルシューティング オプション。  

ポータル サイトの詳細については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」をご覧ください。

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>iOS または iPadOS および macOS のポータル サイトの [デバイス] ページの改善<!-- 6055001 -->
iOS/iPadOS および Mac ユーザーのアプリ エクスペリエンスを向上させるために、ポータル サイトの **[デバイス]** ページに変更を加えました。 最新のルック アンド フィールを作成するだけでなく、ユーザーがデバイスの状態をより簡単に確認できるように、セクション ヘッダーが定義された 1 つの列でデバイスの詳細を再構成しました。 また、デバイスがコンプライアンスに準拠していないユーザーのために、より明確なメッセージングとトラブルシューティングの手順を追加しました。 ポータル サイトの詳細については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」を参照してください。 デバイスを手動で同期する場合は、「[iOS デバイスを手動で同期する](../user-help/sync-your-device-manually-ios.md)」を参照してください。  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>iOS/iPadOS ポータル サイト アプリ用のクラウド設定<!-- 7071303  -->
iOS/iPadOS ポータル サイト用の新しい**クラウド**設定を使用すると、ユーザーは組織に適したクラウドに認証をリダイレクトできます。 既定では、この設定は **[自動]** に構成されています。この場合、ユーザーのデバイスによって自動的に検出されたクラウドに認証が送信されます。 自動的に検出されるクラウド以外の (パブリックや政府などの) クラウドに組織の認証をリダイレクトする必要がある場合、ユーザーは **[設定]** アプリ > **[ポータル サイト]**  >  **[クラウド]** の順に選択して、適切なクラウドを手動で選ぶことができます。 ユーザーは、別のデバイスからサインインしていて、適切なクラウドがデバイスによって自動的に検出されない場合にのみ、 **[クラウド]** 設定を **[自動]** から変更する必要があります。 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>重複する Apple VPP トークン<!-- 7101606  -->
**トークンの場所**が同じである Apple VPP トークンは、**重複**としてマークされるようになり、重複するトークンが削除されたときに再度同期することができます。 重複としてマークされたトークンのライセンスは、引き続き割り当ておよび取り消すことができます。 しかし、トークンが重複としてマークされると、購入した新しいアプリやブックのライセンスが反映されない場合があります。 テナントの Apple VPP トークンを見つけるには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) から、 **[テナント管理]**  >  **[コネクタとトークン]**  >  **[Apple VPP トークン]** の順に選択します。 VPP トークンの詳細については、「[Apple Volume Purchase Program で購入した iOS アプリと macOS アプリを Microsoft Intune で管理する方法](../apps/vpp-apps-ios.md)」をご覧ください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>デバイスの構成

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>macOS デバイスの Wi-Fi プロファイルに EAP-TLS 認証用の複数のルート証明書を追加する<!-- 2077871  -->

macOS デバイスでは、Wi-Fi プロファイルを作成し、認証の種類として拡張認証プロトコル (EAP) を選択できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[macOS]** (プラットフォーム) > **[Wi-Fi]** (プロファイル) の順に選択し、 **[Wi-Fi の種類]** として Enterprise を設定)。

**[EAP の種類]** を **[EAP-TLS]** 、 **[EAP-TTLS]** 、または **[PEAP]** 認証に設定した場合は、複数のルート証明書を追加できます。 以前は、追加できるルート証明書は 1 つのみでした。

構成できる設定の詳細については、「[Microsoft Intune で macOS デバイス向けの Wi-Fi 設定を追加する](../configuration/wi-fi-settings-macos.md)」を参照してください。

適用対象:
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>Windows 10 以降のデバイスの Wi-Fi プロファイルで PKCS 証明書を使用する<!-- 3246388   -->
SCEP 証明書で Windows Wi-Fi プロファイルを認証することができます ( **[デバイス構成]**  >  **[プロファイル]**  >  **[プロファイルの作成]**  >  **[Windows 10 以降]** (プラットフォーム) > **[Wi-Fi]** (プロファイルの種類) > **[Enterprise]**  >  **[EAP の種類]** )。 これで、Windows Wi-Fi プロファイルで PKCS 証明書を使用することができます。 この機能により、ユーザーはテナント内の新規または既存の PKCS 証明書プロファイルを使用して、Wi-Fi プロファイルを認証できます。 

構成できる Wi-Fi 設定の詳細については、「[Intune での Windows 10 以降のデバイス向けの Wi-Fi 設定の追加](../configuration/wi-fi-settings-windows.md)」を参照してください。

適用対象:
- Windows 10 以降

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>macOS デバイス用の有線ネットワーク デバイス構成プロファイル<!-- 3508686  -->
有線ネットワークを構成する新しい macOS デバイス構成プロファイルを使用することができます ( **[デバイス]** > **構成プロファイル > **[プロファイルの作成]**  >  **[macOS]** (プラットフォーム) > **[ワイヤード (有線) ネットワーク]** (プロファイル))。 この機能を使用して、有線ネットワークを管理する 802.1x プロファイルを作成し、この有線ネットワークを macOS デバイスに展開します。

この機能の詳細については、[macOS の有線ネットワーク](../configuration/wired-networks-configure.md)に関するページを参照してください。

適用対象:
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>フル マネージドの Android エンタープライズ デバイスの起動ツールとして Microsoft Launcher を使用する<!-- 4927976   -->
Android エンタープライズ デバイス所有者デバイスでは、Microsoft Launcher をフル マネージド デバイスの既定の起動ツールとして設定できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[Android エンタープライズ]** を選択 > **[デバイスの所有者]**  >  プロファイルに **[デバイスの制限]** を選択 > **[デバイス エクスペリエンス]** )。 その他のすべての Microsoft Launcher 設定を構成するには、[アプリ構成ポリシー](../apps/configure-microsoft-launcher.md)を使用します。 

また、他にもいくつかの UI 更新があります。たとえば、 **[専用デバイス]** が **[デバイス エクスペリエンス]** に名前変更されます。

制限できるすべての設定を確認するには、「[Intune を使用して機能を許可または制限するように Android エンタープライズ デバイスを設定する](../configuration/device-restrictions-android-for-work.md)」をご覧ください。 

適用対象:
- Android エンタープライズ デバイス所有者フル マネージド デバイス (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>自律的シングル App モード設定を使用して、iOS ポータル サイト アプリをサインイン/サインアウト アプリとして構成する<!-- 7055619   -->
iOS/iPadOS デバイスでは、自律的シングル App モード (ASAM) で実行するようにアプリを構成できます。 現在、ポータル サイト アプリでは ASAM がサポートされており、"サインイン/サインアウト" アプリとして構成することができます。 このモードでは、ユーザーは、デバイスの他のアプリとホーム画面のボタンを使用するために、ポータル サイト アプリにサインインする必要があります。 ポータル サイト アプリからサインアウトすると、デバイスはシングル App モードに戻り、ポータル サイト アプリ上でロックされます。

ASAM になるようにポータル サイトを構成するには、 **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS/iPadOS]** (プラットフォーム) > **[デバイスの制限]** (プロファイル) > **[自律的シングル App モード]** の順に移動します。

詳細については、「[自律的シングル App モード (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam)」と、[シングル App モード](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1)に関するページ (Apple の Web サイトが開きます) をご覧ください。

適用対象:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>macOS デバイスでコンテンツ キャッシングを構成する<!-- 7106872   -->
macOS デバイスで、コンテンツ キャッシングを構成する構成プロファイルを作成できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[macOS]** を選択 > プロファイルに **[デバイス機能]** を選択)。 これらの設定を使用して、キャッシュの削除、共有キャッシュの許可、ディスク上のキャッシュ制限などを行います。

コンテンツ キャッシングの詳細については、「[ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching)」をご覧ください (Apple の Web サイトが開きます)。

構成できる設定を確認する場合は、「[Intune での macOS デバイスの機能設定](../configuration/macos-device-features-settings.md)」に移動してください。

適用対象:
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Android エンタープライズで OEMConfig を使用し、新しいスキーマ設定の追加と既存のスキーマ設定の検索を行う<!-- 6394386   -->
Intune で、OEMConfig を使用して Android エンタープライズ デバイスの設定を管理できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[Android エンタープライズ]** を選択 > プロファイルに **[OEMConfig]** を選択)。 **構成デザイナー**を使用すると、アプリ スキーマのプロパティが表示されます。 現在、**構成デザイナー**では次のことができます。

- アプリ スキーマに新しい設定を追加する。
- アプリ スキーマで新しい設定および既存の設定を検索する。

Intune での OEMConfig プロファイルの詳細については、「[Microsoft Intune で、OEMConfig を使って Android Enterprise デバイスを使用および管理する](../configuration/android-oem-configuration-overview.md)」をご覧ください。

適用対象:
- Android エンタープライズ

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>共有 iPad デバイスで共有 iPad の一時セッションをブロックする<!-- 6613794  -->
Intune に、共有 iPad デバイスでの一時的なセッションをブロックする新しい **[Block Shared iPad temporary sessions]\(共有 iPad の一時セッションをブロックする\)** 設定があります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[iOS/iPadOS]** を選択 > プロファイルの種類に **[デバイスの制限]** を選択 > **[共有 iPad]** )。 有効にすると、エンド ユーザーが Guest アカウントを使用できなくなります。 ユーザーは、各自の管理対象の Apple ID とパスワードを使用してデバイスにサインインする必要があります。 

詳細については、[機能を許可または制限するための iOS および iPadOS デバイスの設定](../configuration/device-restrictions-ios.md)に関するページをご覧ください。

適用対象:
- iOS または iPadOS 13.4 以降を実行している共有 iPad デバイス

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>デバイスの登録

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>個人所有デバイスでは、VPN を使用して展開できる<!--5015344  -->
新しいオートパイロット プロファイル **[ドメインの接続チェックをスキップする]** 切り替えを使用すると、社内のネットワークにアクセスせずに、独自のサードパーティ製の Win32 VPN クライアントを使用して、Hybrid Azure AD Join デバイスを展開できます。 新しい切り替えを表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**   >  **[Windows]**  >  **[Windows 登録]**  >  **[展開プロファイル]**  >  **[プロファイルの作成]**  >  **[Out-of-box experience (OOBE)]** の順に移動します。

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>登録ステータス ページのプロファイルをデバイス グループに設定できる<!--3952138 -->
以前は、登録ステータス ページ (ESP) のプロファイルはユーザー グループのみを対象にすることができました。 現在は、ターゲット デバイス グループに設定することもできます。 詳細については、「[登録ステータス ページを設定する](../enrollment/windows-enrollment-status.md)」を参照してください。

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>デバイスの自動登録の同期エラー<!-- 6988214 -->
iOS または iPadOS および macOS デバイスに対して、次のような新しいエラーが報告されます
- 電話番号に無効な文字が含まれているか、そのフィールドが空である。 
- プロファイルの構成名が無効または空である。 
- カーソルの値が無効または期限切れであるか、カーソルが見つからない。
- トークンが拒否されたか、期限切れである。 
- 部署フィールドが空であるか、長すぎる。 
- Apple でプロファイルが見つからず、新しいプロファイルを作成する必要がある。 
- 削除された Apple Business Manager デバイスの数が [概要] ページに追加され、デバイスの状態が表示される。

#### <a name="shared-ipads-for-business--6367326-----"></a>法人向け共有 iPad<!--6367326   -->
Intune と Apple Business Manager を使用して、複数の従業員がデバイスを共有できるように共有 iPad を簡単かつ安全に設定することができます。 Apple の [共有 iPad](https://developer.apple.com/education/shared-ipad/) では、ユーザー データを保持しながら、複数のユーザーに対してパーソナライズされたエクスペリエンスが提供されます。 ユーザーは、管理対象 Apple ID を使用して、組織内の共有 iPad にサインインした後、アプリ、データ、設定にアクセスできます。 共有 iPad はフェデレーション ID と連動します。

この機能を表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** の順に移動し、トークンを選択して**、 **[プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS]** の順に移動します。 **[管理の設定]** ページで、 **[ユーザー アフィニティを使用しないで登録する]** を選択すると、 **[共有 iPad]** オプションが表示されます。

必須: iPadOS 13.4 以降。 このリリースでは、ユーザーが管理対象 Apple ID を使用せずにデバイスにアクセスできるように、共有 iPad での一時的なセッションのサポートが追加されました。 ログアウト時に、デバイスではすべてのユーザー データが消去されるため、デバイスをすぐに使用できる状態になり、デバイスのワイプは不要になります。 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Apple のデバイスの自動登録用に更新されたユーザー インターフェイス<!--7430322 -->
Apple の Device Enrollment Program をデバイスの自動登録に置き換えて、Apple の用語を反映するようにユーザー インターフェイスが更新されました。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>macOS で使用できるデバイスのリモート ロック PIN<!--7281557   -->
macOS デバイスのリモート ロック PIN の可用性が、7 日から 30 日に延長されました。

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>共同管理デバイスのプライマリ ユーザーを変更する<!--7319183  -->
共同管理されている Windows デバイスについて、デバイスのプライマリ ユーザーを変更することができます。 その確認および変更方法の詳細については、「[Intune デバイスのプライマリ ユーザーを確認する](../remote-actions/find-primary-user.md)」をご覧ください。 この機能は、今後数週間で徐々にロールアウトされます。

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Intune プライマリ ユーザーを設定すると Azure AD の所有者プロパティも設定される<!--7319227 -->
この新機能では、新しく登録された Hybrid Azure AD Join を使用したデバイスの所有者プロパティが、Intune プライマリ ユーザーが設定されるのと同時に自動的に設定されます。 プライマリ ユーザーの詳細については、「[Intune デバイスのプライマリ ユーザーを確認する](../remote-actions/find-primary-user.md)」をご覧ください。

これは登録プロセスに加えられる変更であり、新しく登録されたデバイスにのみ適用されます。 既存の Hybrid Azure AD Join を使用したデバイスの場合、Azure AD の所有者プロパティを手動で更新する必要があります。 これを行うには、[プライマリ ユーザーの変更機能](../remote-actions/find-primary-user.md#change-a-devices-primary-user)または[スクリプト](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)を使用できます。

Windows 10 デバイスに対して Hybrid Azure Azure Directory Join が使用されるようになると、デバイスの最初のユーザーがエンドポイント マネージャーのプライマリ ユーザーになります。  現時点では、このユーザーは、対応する Azure AD デバイス オブジェクトでは設定されません。 これにより、Azure AD ポータルの "*所有者*" プロパティと Microsoft Endpoint Manager admin center の "*プライマリ ユーザー*" プロパティを比較したときに不整合が生じます。 Azure AD の所有者プロパティは、BitLocker 回復キーへのアクセスをセキュリティで保護するために使用されます。 このプロパティは、Hybrid Azure AD Join を使用したデバイスでは設定されません。 この制限により、Azure AD からの BitLocker 回復のセルフサービスの設定が妨げられます。 この今後の機能では、この制限が解決されます。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>デバイス セキュリティ

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>macOS デバイスの FileVault 2 の暗号化中はユーザーに対して回復キーを非表示にする<!-- 5459801  -->
[macOS Endpoint Protection](../protect/endpoint-protection-macos.md#filevault) テンプレート内の *FileVault* カテゴリに、次の新しい設定を追加しました: **回復キーを非表示にする**。 この設定により、FileVault 2 の暗号化中は、エンド ユーザーに対して個人用キーが非表示になります。 

暗号化された macOS デバイスの個人用回復キーを表示する場合、デバイス ユーザーは次のいずれかの場所に移動し、macOS デバイスの *[回復キーの取得]* をクリックすることができます。 

- iOS/iPadOS ポータル サイト アプリ
- Intune アプリ
- ポータル サイト Web サイト
- Android 用ポータル サイト アプリ

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Android フル マネージドの Outlook での S/MIME 署名と暗号化証明書のサポート<!--5896415   -->
Android Enterprise フル マネージドを実行するデバイス上の Outlook で、S/MIME 署名と暗号化に証明書を使用できるようになりました。

これにより、他の Android バージョンで先月追加されたサポート (Android 上の Outlook での S/MIME 署名と暗号化証明書のサポート) が拡張されます。 SCEP および PKCS がインポートされた証明書プロファイルを使用して、これらの証明書をプロビジョニングすることができます。

このサポートの詳細については、Exchange のドキュメントで「[iOS および Android 向け Outlook での秘密度ラベルと保護](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android)」を参照してください。

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>コンプライアンス違反の電子メールにポータル サイト サポート Web サイトへのリンクを追加する<!-- 7225498    -->
コンプライアンス違反の電子メール通知を送信するために[通知メッセージ テンプレートを構成する](../protect/actions-for-noncompliance.md#create-a-notification-message-template)場合は、新しい設定の**ポータル サイト Web サイト リンク**を使用して、ポータル サイト Web サイトへのリンクが自動的に含まれるようにします。 このオプションを *[有効にする]* に設定すると、このテンプレートに基づいて電子メールを受信する非準拠デバイスを持つユーザーは、リンクを使用して Web サイトを開き、自分のデバイスが準拠していない理由の詳細を知ることができます。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>ライセンス

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>管理者は Microsoft Endpoint Manager 管理コンソールにアクセスするための Intune ライセンスが不要になった<!--1335430 -->
管理者が MEM 管理コンソールとクエリ グラフ API にアクセスするための Intune ライセンス要件を削除する、テナント全体の切り替えを設定できるようになりました。 ライセンス要件を削除してから復帰させることはできません。 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>スクリプト 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>macOS デバイスでのシェル スクリプトの可用性<!-- 7134839  -->
macOS デバイス用のシェル スクリプトが、米国政府機関向けおよび中国のお客様にご利用いただけるようになりました。 シェル スクリプトの詳細については、「[Intune で macOS デバイスに対してシェル スクリプトを使用する](../apps/macos-shell-scripts.md)」を参照してください。



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>2020 年 6 月 8 日の週   

### <a name="app-management"></a>アプリ管理  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>iOS/iPadOS 用ポータル サイトの情報画面の更新 <!--7032452 -->
iOS/iPadOS 用ポータル サイトの情報画面が更新され、管理者がデバイスで表示および実行できる内容についての説明が改善されました。 これらの説明は企業所有のデバイスのみに関するものです。 更新されたのはテキストのみです。管理者がユーザー デバイスで表示または実行できる内容は実際には変更されていません。 更新された画面を確認するには、「[Intune エンド ユーザー アプリの UI 更新](./whats-new-app-ui.md)」を参照してください。

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Android アプリの条件付き起動のエンド ユーザー エクスペリエンスの更新<!-- 5736084 -->
Android ポータル サイトの 2006 リリースは、2005 リリースからの更新に基づいて変更されています。 2005 では、アプリ保護ポリシーによって警告、ブロック、またはワイプが発行された Android デバイスのエンド ユーザーに、その警告、ブロック、またはワイプの理由、および問題を修復するための手順を説明するメッセージをページ全体に表示する更新をロールアウトしました。 2006 では、アプリ保護ポリシーが割り当てられた Android アプリの最初のユーザーは、ガイド付きフローを通じて、アプリのアクセスがブロックされる原因となった問題を修復します。 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>2020 年 5 月 25 日の週

### <a name="app-management"></a>アプリ管理

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>ARM64 デバイス上での Windows 32 ビット (x86) アプリ<!-- 5477661 -->
ARM64 デバイスで利用可能なものとして展開されている Windows 32 ビット (x86) アプリが、ポータル サイトに表示されるようになりました。 Windows 32 ビット アプリについて詳しくは、[Win32 アプリの管理](../apps/apps-win32-app-management.md)に関するページをご覧ください。

#### <a name="windows-company-portal-app-icon---7114635---"></a>Windows ポータル サイト アプリのアイコン<!-- 7114635 -->
Windows ポータル サイト アプリのアイコンが更新されました。 ポータル サイトの詳細については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」をご覧ください。


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>2020 年 5 月 18 日の週

### <a name="app-management"></a>アプリ管理  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>iOS または iPadOS および macOS 用のポータル サイト アプリのアイコンの更新<!--6057697 -->
より新しい外観を作成するために、ポータル サイトのアイコンが更新されました。これはデュアル スクリーン デバイスでサポートされ、Microsoft Fluent Design System と適合します。 更新されたアイコンを確認するには、「[Intune エンド ユーザー アプリの UI 更新](./whats-new-app-ui.md)」をご覧ください。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>デバイス セキュリティ

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>エンドポイント検出と応答のポリシーを使用してデバイスを Defender ATP にオンボードする<!-- 7130165  -->

[エンドポイント検出と応答](../protect/endpoint-security-edr-policy.md) (EDR) のエンドポイント セキュリティ ポリシーを使用して、Microsoft Defender Advanced Threat Protection (Defender ATP) の展開のためにデバイスをオンボードして構成します。 EDR では、Intune (MDM) で管理されている Windows デバイスのポリシーと、Configuration Manager によって管理される Windows デバイス用の個別のポリシーがサポートされます。 

Configuration Manager デバイスのポリシーを使用するには、[EDR ポリシーをサポートするように Configuration Manager を設定](../protect/endpoint-security-edr-policy.md#set-up-configuration-manager-to-support-edr-policy)する必要があります。 設定には次が含まれます。

- "*テナントのアタッチ*" 用に Configuration Manager 構成する。
- Configuration Manager のコンソール内の更新プログラムをインストールして、EDR ポリシーのサポートを有効にする。 この更新プログラムは、"*テナントのアタッチ*" を有効にした階層にのみ適用されます。
- 階層のデバイス コレクションを Microsoft Endpoint Manager admin center に同期する。


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>2020 年 5 月 11 日の週 (2005 サービス リリース)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>ポータル サイトでセルフサービス デバイス アクションをカスタマイズする<!--4393379 -->
ポータル サイト アプリと Web サイトでエンド ユーザーに表示される利用可能なセルフサービス デバイス アクションをカスタマイズすることができます。 意図しないデバイス アクションの防止に役立てるために、ポータル サイト アプリに対して設定を構成できます。そのためには、 **[テナント管理]**  >  **[カスタマイズ]** の順に選択します。 次の操作を実行できます。
- 会社の Windows デバイスで **[削除]** ボタンを非表示にする。
- 会社の Windows デバイスで **[リセット]** ボタンを非表示にする。
- 会社の iOS デバイスで **[リセット]** ボタンを非表示にする。
- 会社の iOS デバイスで **[削除]** ボタンを非表示にする。
詳細については、「[ポータル サイトからのユーザーによるセルフサービス デバイス アクション](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal)」を参照してください。

#### <a name="auto-update-vpp-available-apps---3640511----"></a>VPP の利用可能なアプリの自動更新<!-- 3640511  -->
Volume Purchase Program (VPP) の利用可能なアプリとして公開されるアプリは、VPP トークンに対して**アプリの自動更新**が有効になっている場合、自動的に更新されるようになります。 以前は、VPP の利用可能なアプリは自動的に更新されませんでした。 代わりに、エンドユーザーはポータル サイトに移動し、新しいバージョンが利用可能な場合はアプリを再インストールする必要がありました。 必須アプリでは引き続き自動更新がサポートされています。




#### <a name="android-company-portal-user-experience---5736084----"></a>Android ポータル サイトのユーザー エクスペリエンス<!-- 5736084  -->
2005 リリースの Android ポータル サイトでは、アプリ保護ポリシーによって警告、ブロック、またはワイプが発行された Android デバイスのエンドユーザーに、新しいユーザー エクスペリエンスが表示されるようになります。 現在のダイアログ エクスペリエンスの代わりに、エンドユーザーには、警告、ブロック、またはワイプの理由、および問題を修正するための手順を説明するメッセージがページ全体に表示されます。 詳細については、「[Android デバイスでのアプリ保護のエクスペリエンス](../apps/app-protection-policy.md#app-protection-experience-for-android-devices)」と「[Microsoft Intune の Android アプリ保護ポリシー設定](../apps/app-protection-policy-settings-android.md)」を参照してください。

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>macOS 用ポータル サイトでの複数アカウントのサポート<!-- 5779449  -->
macOS デバイスのポータル サイトでユーザー アカウントがキャッシュされるようになり、サインインがより簡単になりました。 ユーザーは、アプリケーションを起動するたびにポータル サイトにサインインする必要がなくなりました。 また、複数のユーザー アカウントがキャッシュされている場合、ポータル サイトにアカウント ピッカーが表示されるため、ユーザーは自分のユーザー名を入力する必要がありません。 

#### <a name="newly-available-protected-apps---7060934-----"></a>新しく利用可能な保護されたアプリ<!-- 7060934   -->
次の保護されたアプリを使用できるようになりました。
- Board Papers
- Breezy for Intune
- Hearsay Relate for Intune
- ISEC7 Mobile Exchange Delegate for Intune
- Lexmark for Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- ServiceNow® Onboarding - Intune
- Smartcrypt for Intune
- Tact for Intune
- Zero - email for attorneys

保護されたアプリの詳細については、「[保護されている Microsoft Intune アプリ](../apps/apps-supported-intune-apps.md)」を参照してください。

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>ポータル サイトから Intune ドキュメントを検索する<!-- 1736480   -->
macOS アプリ用のポータル サイトから、Intune のドキュメントを直接検索できるようになりました。 メニュー バーで、 **[ヘルプ]**  >  **[検索]** の順に選択し、検索キー ワードを入力すれば、質問に対する回答がすばやく見つかります。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>デバイスの構成

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Zebra Technologies デバイスの OEMConfig サポートの機能強化<!-- 4184154 -->
Intune は、Zebra OEMConfig によって提供されるすべての機能を完全にサポートしています。 Android Enterprise と OEMConfig を使用して Zebra Technologies デバイスを管理しているお客様は、複数の OEMConfig プロファイルを 1 つのデバイスにデプロイできます。 また、Zebra OEMConfig プロファイルの状態に関する豊富なレポートを表示することもできます。

詳細については、「[Microsoft Intuneで複数の OEMConfig プロファイルを Zebra デバイスにデプロイする](../configuration/oemconfig-zebra-android-devices.md)」を参照してください。

他の OEM の OEMConfig の動作は変更されていません。

適用対象:
- Android エンタープライズ
- OEMConfig をサポートする Zebra Technologies デバイス。 サポートの詳細については、Zebra にお問い合わせください。

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>macOS デバイスでシステム拡張機能を構成する<!-- 6255624 -->
macOS デバイスでは、カーネル レベルで設定を構成するためのカーネル拡張機能プロファイルを作成することができます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[macOS]** (プラットフォーム) > **[カーネル拡張機能]** (プロファイル))。 Apple では、最終的にカーネル拡張機能を非推奨とし、今後のリリースでシステム拡張機能に置き換える予定です。

システム拡張機能はユーザー領域で実行され、カーネルへのアクセス権がありません。 目標は、カーネル レベルでの攻撃を制限しながら、セキュリティを強化し、さらにエンド ユーザー制御を提供することです。 カーネル拡張機能とシステム拡張機能の両方で、ユーザーは、オペレーティング システムのネイティブ機能を拡張するアプリ拡張機能をインストールできます。

Intune では、カーネル拡張機能とシステム拡張機能の両方を構成できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[macOS]** (プラットフォーム) > **[システム拡張機能]** (プロファイル))。 カーネル拡張機能は 10.13.2 以降に適用されます。 システム拡張機能は 10.15 以降に適用されます。 macOS 10.15 から macOS 10.15.4 では、カーネル拡張機能とシステム拡張機能を並行して実行できます。 

macOS デバイスのこれらの拡張機能の詳細については、[macOS 拡張機能の追加](../configuration/kernel-extensions-overview-macos.md)に関するページを参照してください。

適用対象:
- macOS 10.15 以降

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>macOS デバイスでアプリとプロセスのプライバシー設定を構成する<!-- 2934232   --> 
macOS Catalina 10.15 のリリースでは、Apple によって新しいセキュリティとプライバシーの強化が加えられました。 既定では、アプリケーションとプロセスで、ユーザーの同意なしで特定のデータにアクセスすることはできません。 ユーザーが同意しない場合、アプリケーションとプロセスが機能しなくなる可能性があります。 Intune では、macOS 10.14 以降を実行しているデバイスでエンドユーザーに代わって、IT 管理者がデータ アクセスの同意を許可または許可しないようにできる設定のサポートを追加しています。 これらの設定により、アプリケーションとプロセスは引き続き正常に機能し、プロンプトの数が削減されます。 

管理できる設定の詳細については、[macOS のプライバシー設定](../configuration/device-restrictions-macos.md#privacy-preferences)に関するセクションを参照してください。

適用対象:
- macOS 10.14 以降

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>デバイスの登録

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>登録制限でスコープ タグがサポートされます<!--4209550  -->
登録制限にスコープ タグを割り当てられるようになりました。 そのためには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[登録制限]**  >  **[制限の作成]** の順に移動します。 いずれかの種類の制限を作成すると、 **[スコープ タグ]** ページが表示されます。 詳細は、「[登録制限を設定する](../enrollment/enrollment-restrictions-set.md)」を参照してください。

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Hololens 2 デバイスの Autopilot サポート<!--6305220  -->
Windows Autopilot で、Hololens 2 デバイスがサポートされるようになりました。 Hololens での Autopilot の使用の詳細については、[Windows Autopilot for HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot)に関する記事を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>iOS での同期リモート アクションの一括使用<!--6440956  idmiss-->
一度に最大 100 台の iOS デバイスに対して、同期リモート アクションを使用できるようになりました。 この機能を確認するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[すべてのデバイス]**  >  **[デバイスの一括操作]** の順に移動します。 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>自動デバイス同期間隔を 12 時間に短縮<!--3077535  -->
Apple の自動デバイス登録では、Intune と Apple Business Manager の自動デバイス同期間隔が 24 時間から 12 時間に短縮されました。 同期の詳細については、「[マネージド デバイスを同期する](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices)」を参照してください。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>デバイス セキュリティ

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Android デバイスでの DISA Purebred の派生資格情報のサポート<!-- 6939073     -->
*DISA Purebred* を、Android Enterprise のフル マネージド デバイスで[派生資格情報](../protect/derived-credentials.md)として使用できるようになりました。 サポートには、DISA Purebred の派生資格情報の取得が含まれます。 アプリ認証、Wi-Fi、VPN、または S/MIME 署名や、それをサポートするアプリでの暗号化に、派生資格情報を使用できます。 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>非準拠に対するアクションとしてプッシュ通知を送信する <!-- 1733150   -->
デバイスがコンプライアンス ポリシーの条件を満たせない場合にユーザーにプッシュ通知を送信する[非準拠のアクション](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)を構成できるようになりました。 新しいアクションは、 **[エンド ユーザーにプッシュ通知を送信する]** で、Android および iOS デバイスでサポートされています。

ユーザーがデバイスでプッシュ通知を選択すると、ポータル サイトまたは Intune アプリが開き、準拠していない理由の詳細が表示されます。

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>エンドポイント セキュリティのコンテンツと新機能<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

Intune の[エンドポイント セキュリティ](../protect/endpoint-security.md)に関するドキュメントを利用できるようになりました。 Microsoft Endpoint Manager admin center のエンドポイント セキュリティ ノードでは、次のことができます。

- マネージド デバイスに重点を置いたセキュリティ ポリシーを作成して展開する
- Microsoft Defender Advanced Threat Protection との統合を構成し、ATP チームによって特定された危険な状態のデバイスのリスクを修復するのに役立つセキュリティ タスクを管理する
- セキュリティ ベースラインを構成する
- デバイスのコンプライアンスと条件付きアクセス ポリシーを管理する
- Configuration Manager がクライアント接続用に構成されている場合に、Intune と Configuration Manager の両方でデバイスのコンプライアンス対応状態を表示する

コンテンツが利用できることに加えて、今月のエンドポイント セキュリティの新機能は次のとおりです。

- [**エンドポイント セキュリティ ポリシー**](../protect/endpoint-security-policy.md)は **"***プレビュー***" でなくなり**、"*一般公開*" として運用環境で使用できるようになりました。ただし、次の 2 つの例外があります。

  - 新しい "*パブリック プレビュー*" では、Windows 10 ファイアウォール ポリシーで [**Microsoft Defender ファイアウォール規則**プロファイル](../protect/endpoint-security-firewall-policy.md#firewall-profiles)を使用できます。 このプロファイルの各インスタンスでは、Microsoft Defender ファイアウォール プロファイルを補完するために、最大 150 のファイアウォール規則を構成できます。 
  - アカウント保護セキュリティポリシーはプレビューのままです。 

- [**エンドポイント セキュリティ ポリシーの複製を作成**](../protect/endpoint-security-policy.md#duplicate-a-policy)できるようになりました。 複製には、元のポリシーの設定構成が保持されますが、新しい名前が付けられます。 新しいポリシー インスタンスには、新しいポリシー インスタンスを編集して追加するまで、グループへの割り当ては含まれません。 次のポリシーを複製することができます。
  - ウイルス対策
  - ディスクの暗号化
  - ファイアウォール
  - エンドポイントの検出と応答
  - 攻撃の回避
  - アカウント保護

- [**セキュリティ ベースラインの複製を作成**](../protect/security-baselines.md#duplicate-a-security-baseline)できるようになりました。 複製には、元のベースラインの設定構成が保持されますが、新しい名前が付けられます。 新しいベースライン インスタンスでは、新しいベースライン インスタンスを編集して追加するまで、グループへの割り当ては含まれません。

- エンドポイント セキュリティのウイルス対策ポリシーの新しいレポートを使用できます。[**Windows 10 の異常なエンドポイント**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints)。 このレポートは、エンドポイント セキュリティのウイルス対策ポリシーを表示するときに選択できる新しいページです。 このレポートには、MDM で管理されている Windows 10 デバイスのウイルス対策の状態が表示されます。  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Android 上の Outlook での S/MIME 署名と暗号化証明書のサポート<!-- 7207474  -->
Android 上の Outlook で S/MIME 署名と暗号化に証明書を使用できるようになりました。 このサポートにより、SCEP、PKCS、および PKCS がインポートされた証明書プロファイルを使用して、これらの証明書をプロビジョニングすることができます。 次の Android プラットフォームがサポートされます。

- Android Enterprise 仕事用プロファイル
- Android デバイス管理者

Android Enterprise フル マネージド デバイスのサポートは近日中に導入されます。

このサポートの詳細については、Exchange のドキュメントで「[iOS および Android 向け Outlook での秘密度ラベルと保護](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android)」を参照してください。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

#### <a name="device-reports-ui-update---6269408---"></a>デバイス レポートの UI の更新<!-- 6269408 -->
[レポートの概要] ウィンドウに、 **[概要]** と **[レポート]** タブが表示されるようになりました。[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[レポート]** を選択し、 **[レポート]** タブを選択して、使用可能なレポートの種類を表示します。 関連情報については、「[Intune のレポート](../fundamentals/reports.md)」を参照してください。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>スクリプト

#### <a name="macos-script-support---6376978----"></a>macOS のスクリプト サポート<!-- 6376978  -->
macOS のスクリプト サポートが一般公開されるようになりました。 さらに、Apple の自動デバイス登録 (旧称: Device Enrollment Program) に登録されているユーザー割り当てスクリプトと macOS デバイスの両方のサポートが追加されました。 詳細については、「[Intune で macOS デバイスに対してシェル スクリプトを使用する](../apps/macos-shell-scripts.md)」を参照してください。


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>2020 年 5 月 4 日の週  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Android 用ポータル サイトで仕事用プロファイルの登録後にアプリを取得する方法がユーザーに示される <!-- 6103999 -->
ユーザーがアプリをより簡単に見つけてインストールできるように、ポータル サイトのアプリ内ガイダンスが改善されました。 仕事用プロファイルの管理に登録した後、バッジ付きバージョンの Google Play でおすすめのアプリを見つける方法を説明するメッセージがユーザーに表示されます。 [Android のプロファイルでデバイスを登録する方法](../user-help/enroll-device-android-work-profile.md)に関する記事の最後の手順は、新しいメッセージを示すように更新されています。 また、ユーザーには、左側のポータル サイト ドロアーで新しい **[アプリの取得]** リンクが表示されます。 これらの新規および改善されたエクスペリエンスの場所を空けるために、 **[アプリ]** タブは削除されました。 更新された画面を確認するには、「[Intune エンド ユーザー アプリの UI 更新](./whats-new-app-ui.md)」を参照してください。 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>2020 年 4 月 20 日の週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Microsoft Endpoint Manager テナントのアタッチ:デバイスの同期とデバイスのアクション<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager によって、Configuration Manager と Intune が 1 つのコンソールに統合されます。 Configuration Manager バージョン 2002 以降、ご利用の Configuration Manager デバイスをクラウド サービスにアップロードし、管理センターからそれらに対するアクションを実行できます。 詳細については、「[Microsoft Endpoint Manager テナントのアタッチ: デバイスの同期とデバイスのアクション](../../configmgr/tenant-attach/device-sync-actions.md)」を参照してください。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Microsoft Office 365 ProPlus 名前変更<!-- 6368143 -->
Microsoft Office 365 ProPlus は **Microsoft 365 Apps for enterprise** に名前変更されています。 詳細については、「[Office 365 ProPlus の名前の変更](https://docs.microsoft.com/deployoffice/name-change)」を参照してください。 このドキュメントでは、これを通例 Microsoft 365 アプリと呼びます。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]** 、 **[Windows]** 、 **[追加]** の順に選択して、このアプリを見つけることができます。 アプリを追加する方法の詳細については、「[Microsoft Intune にアプリを追加する](../apps/apps-add.md)」を参照してください。

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>2020 年 4 月 13 日の週 (2004 サービス リリース)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Android Enterprise デバイスで Outlook の S/MIME 設定を管理する<!-- 6517085   -->
アプリ構成ポリシーを使用して、Android Enterprise を実行するデバイス上で Outlook の S/MIME 設定を管理できます。 また、デバイスのユーザーが Outlook の設定で S/MIME を有効または無効にすることを許可するかどうかも選択できます。 Android 用のアプリ構成ポリシーを使用するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド デバイス]** の順に移動します。 Outlook の設定を構成する方法の詳細については、「[Microsoft Outlook の構成設定](../apps/app-configuration-policies-outlook.md)」を参照してください。

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>マネージド Google Play アプリのプレリリース テスト<!-- 2681933  -->
[アプリのプレリリース テストに Google Play のクローズド テスト トラック](https://support.google.com/googleplay/android-developer/answer/3131213)を使用している組織は、Intune でこれらのトラックを管理できます。 テストを実行するために、Google Play の実稼働前のトラックに発行されたアプリをパイロット グループに選択的に割り当てることができます。 Intune では、アプリに実稼働前のビルド テスト トラックが発行されているかどうかや、そのトラックを AAD ユーザーまたはデバイス グループに割り当てることができるかどうかを確認できます。 この機能は、現在サポートされているすべての Android Enterprise シナリオ (仕事用プロファイル、フル マネージド、および専用) で利用できます。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[Android]**  >  **[追加]** を選択して、マネージド Google Play アプリを追加できます。 詳細については、「[マネージド Google Play のクローズド テスト トラックの操作](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks)」を参照してください。

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams が Office 365 Suite for macOS に含まれるようになりました<!-- 5903936  -->
Microsoft エンドポイント マネージャーで Microsoft Office for macOS が割り当てられているユーザーは、既存の Microsoft Office アプリ (Word、Excel、PowerPoint、Outlook、OneNote) に加えて、Microsoft Teams を受け取るようになります。 Intune は、他の Office for macOS アプリがインストールされている既存の Mac デバイスを認識し、次回デバイスが Intune にチェックインするときに Microsoft Teams のインストールを試行します。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[macOS]**  >  **[追加]** の順に選択して、**Office 365 Suite** for macOS を見つけることができます。 詳しくは、「[Microsoft Intune を使用して macOS デバイスに Office 365 を割り当てる](../apps/apps-add-office365-macos.md)」をご覧ください。

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Android アプリ構成ポリシーの更新<!-- 6113334  -->
Android アプリ構成ポリシーは、アプリ構成プロファイルを作成する前に、管理者がデバイス登録の種類を選択できるように更新されています。 この機能は、登録の種類 (仕事用プロファイルまたはデバイス所有者) に基づく証明書プロファイルのために追加されます。  この更新の内容は次のとおりです。

1. 新しいプロファイルが作成され、デバイス登録の種類として [仕事用プロファイルとデバイス所有者プロファイル] が選択されている場合は、証明書プロファイルをアプリ構成ポリシーに関連付けることはできません。
2. 新しいプロファイルが作成され、[仕事用プロファイルのみ] が選択されている場合は、[デバイスの構成] で作成された仕事用プロファイルの証明書ポリシーを利用できます。
3. 新しいプロファイルが作成され、[デバイスの所有者のみ] が選択されている場合は、[デバイスの構成] で作成されたデバイスの所有者の証明書ポリシーを利用できます。 

> [!IMPORTANT]
> この機能がリリースされる前 (2020 年 4 月リリース- 2004 年) に作成され、ポリシーに関連付けられている証明書プロファイルがない既存のポリシーは、デバイス登録の種類の既定値が [仕事用プロファイルとデバイス所有者プロファイル] になります。 また、この機能がリリースされる前に作成され、関連付けられている証明書プロファイルがある既存のポリシーは、既定値が [仕事用プロファイルのみ] になります。

さらに、仕事用プロファイルとデバイス所有者の両方の登録タイプに対して機能する、Gmail および Nine の電子メール構成プロファイルを追加しています。これには、両方の電子メール構成の種類での証明書プロファイルの使用が含まれます。  仕事用プロファイル用に [デバイスの構成] で作成した Gmail または Nine のポリシーはすべて、デバイスに引き続き適用されるため、アプリ構成ポリシーに移動する必要はありません。

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[アプリ構成ポリシー]** を選択して、アプリ構成ポリシーを検索できます。 アプリ構成ポリシーの詳細については、「[Microsoft Intune 用アプリ構成ポリシー](../apps/app-configuration-policies-overview.md)」を参照してください。

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>デバイスの所有権の種類が変更されたときのプッシュ通知<!-- 5575875 -->
Android と iOS の両方のポータル サイト ユーザーに、自身のデバイスの所有権の種類が個人用から企業に変更されている場合に、プライバシーを尊重するため、プッシュ通知を送信するように構成できます。 既定では、このプッシュ通知はオフに設定されています。 この設定は、Microsoft エンドポイント マネージャーで **[テナント管理]**  >  **[カスタマイズ]** を選択すると見つかります。 デバイスの所有権がエンドユーザーに与える影響の詳細については、「[デバイス所有権を変更する](../enrollment/corporate-identifiers-add.md#change-device-ownership)」を参照してください。

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>[カスタマイズ] ペインのグループのターゲット サポート<!-- 4722837  -->
**[カスタマイズ]** ペインの設定をユーザー グループをターゲットにすることができます。 Intune でこれらの設定を見つけるには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に移動し、 **[テナント管理]**  >  **[カスタマイズ]** の順に選択します。 カスタマイズに関する詳細については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」を参照してください。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>デバイスの構成

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>iOS、iPadOS、macOS でサポートされている、複数の "接続が試みられるたびに評価する" オンデマンド VPN 規則<!-- 6424615  -->
Intune ユーザー エクスペリエンスでは、**接続が試みられるたびに評価する**アクションによって、同じ VPN プロファイル内で複数のオンデマンド VPN 規則を使用できます。( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームが **[iOS/iPadOS]** または **[macOS]** > プロファイルが **[VPN]** > **[自動 VPN]**  >  **[オンデマンド]** )。

リスト内の最初の規則のみが受け入れられます。 この動作は固定で、Intune によってリスト内のすべての規則が評価されます。 各規則は、オンデマンド規則リストに表示されている順序で評価されます。

> [!NOTE]
> これらのオンデマンド VPN 規則を使用する既存の VPN プロファイルがある場合、次回 VPN プロファイルを変更したときに修正が適用されます。 たとえば、接続の名前を変更してから、プロファイルを保存するなど、小さな変更を行います。
>
> 認証に SCEP 証明書を使用している場合、この変更により、この VPN プロファイルの証明書が再発行されます。

適用対象:
- iOS/iPadOS
- macOS

VPN プロファイルの詳細については、「[VPN プロファイルの作成](../configuration/vpn-settings-configure.md)」を参照してください。

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>iOS/iPadOS デバイスでの SSO および SSO アプリ拡張機能プロファイルの追加オプション<!-- 6504155   -->

iOS/iPadOS デバイスでは、次のことができます。
- SSO プロファイル ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > プラットフォームに **[iOS/iPadOS]** > プロファイルに **[デバイスの機能]** > **[シングル サインオン]** ) で、Kerberos プリンシパル名が SSO プロファイルのセキュリティ アカウント マネージャー (SAM) アカウント名になるように設定します。 
- SSO アプリ拡張機能プロファイル ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > プラットフォームに **[iOS/iPadOS]** > プロファイルに **[デバイスの機能]** > **[シングル サインオン アプリの拡張機能]** ) で、新しい SSO アプリ拡張機能の種類を使用して、より少ないクリック回数で iOS/iPadOS Microsoft Azure AD 拡張機能を構成します。 共有デバイス モードでデバイスの Azure AD 拡張機能を有効にし、拡張機能固有データを拡張機能に送信できます。

適用対象:
- iOS/iPadOS 13.0 以降

iOS/iPadOS デバイスでのシングル サインオンの使用に関する詳細については、[シングル サインオン アプリの拡張機能の概要](../configuration/device-features-configure.md#single-sign-on-app-extension)と[シングル サインオンの設定リスト](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>デバイスの登録

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>既定のプロファイルが存在する場合に、Apple 自動デバイス登録トークンを削除する<!--6393220 -->
以前は、既定のプロファイルを削除できませんでした。これは、関連付けられている自動デバイス登録トークンを削除できなかったことを意味します。 次の場合にトークンを削除できるようになりました。
- トークンに割り当てられているデバイスがない
- 既定のプロファイルが存在する。それを行うには、既定のプロファイルを削除してから、関連付けられているトークンを削除します。
詳細については、「[Intune から ADE トークンを削除する](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-automated-device-enrollment-token-from-intune)」を参照してください。

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Apple 自動デバイス登録と Apple Configurator 2 デバイス、プロファイル、トークンの拡張されたサポート<!--3542402 -->
分散した IT 部門と組織を支援するために、Intune では、トークンあたり最大 1000 の登録プロファイル、Intune アカウントあたり 2000 の自動デバイス登録 (旧称 DEP) トークン、およびトークンあたり 75000 のデバイスがサポートされるようになりました。 登録プロファイルあたりのデバイス数に特定の制限はなく、トークンあたりのデバイスの最大数未満です。

Intune では、最大 1000 の Apple Configurator 2 プロファイルがサポートされるようになりました。

詳細については、「[サポートされるボリューム](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume)」を参照してください。

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>[すべてのデバイス] ページの列エントリの変更<!--6967616 -->
**すべてのデバイス** ページで、**管理者** 列のエントリが変更されました。
- *MDM* ではなく、*Intune* が 表示されるようになりました
- *MDM/ConfigMgr エージェント*ではなく、* 共同管理*が表示されるようになりました

エクスポート値は変更されていません。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>トラステッド プラットフォーム マネージャー (TPM) のバージョン情報がデバイス ハードウェア ページに表示される<!--6224914 idmiss -->
デバイスのハードウェア ページに TPM バージョン番号が表示されるようになりました ([Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]** > デバイスの選択 > **[ハードウェア]** > **[システム格納装置]** の下を参照)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>ログを収集して macOS デバイスに割り当てられているスクリプトのトラブルシューティングを改善する<!-- 6359853  -->
macOS デバイスに割り当てられているスクリプトのトラブルシューティングを改善するために、ログを収集できるようになりました。 ログは、60 MB (圧縮) または 25 個のファイルのどちらか先に発生するまで収集できます。 詳細については、「[ログ収集を使用した macOS シェル スクリプト ポリシーのトラブルシューティング](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection)」を参照してください。
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>セキュリティ

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>証明書によって Android Enterprise のフル マネージド デバイスをプロビジョニングするための派生資格情報<!--4839592    -->
Intune では、Android デバイスの認証方法として、[派生資格情報](../protect/derived-credentials.md)の使用がサポートされるようになりました。 派生資格情報は、証明書をデバイスに展開するためのアメリカ国立標準技術研究所 (NIST) 800-157 標準を実装したものです。 Android のサポートは、iOS/iPadOS を実行するデバイスのサポートを拡張したものです。

派生資格情報は、スマート カードのように、Personal Identity Verification (PIV) または Common Access Card (CAC) カードの使用に依存します。 モバイル デバイスのために派生資格情報を得るには、ユーザーは Microsoft Intune アプリから開始し、使用しているプロバイダーに固有の登録ワークフローに従います。 すべてのプロバイダーに共通することは、コンピューターのスマート カードを使用し、派生資格情報プロバイダーに対して認証するという要件です。 そのプロバイダーはその後、ユーザーのスマート カードから誘導されたデバイスに証明書を発行します。

VPN および Wi-Fi のデバイス構成プロファイル用の認証方法として派生資格情報を使用できます。 それらは、アプリ認証や、それをサポートするアプリケーションの S/MIME 署名と暗号化にも使用できます。

Intune では、Android で次の派生資格情報プロバイダーをサポートするようになりました。
- Entrust Datacard
- Intercede

サードパーティ プロバイダーの DISA Purebred は、今後のリリースで Android で使用できるようになります。

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Microsoft Edge のセキュリティ ベースラインの一般提供が開始<!--6586139 -->

[Microsoft Edge のセキュリティ ベースライン](../protect/security-baselines.md#available-security-baselines)の新しいバージョンの提供が開始され、一般公開 (GA) としてリリースされました。 以前の Edge のベースラインはプレビュー段階でした。  新しいベースライン バージョンは 2020 年 4 月 (Edge バージョン 80 以降) に含まれます。 

この新しいベースラインのリリースによって、以前のベースライン バージョンに基づいてプロファイルを作成できなくなりますが、それらのバージョンで作成したプロファイルは引き続き使用できます。 また、[最新のベースライン バージョンを使用するように、既存のプロファイルを更新する](../protect/security-baselines.md#change-the-baseline-version-for-a-profile)こともできます。 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>2020 年 4 月 6 日の週

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>macOS デバイス向けの新しいシェル スクリプト設定<!-- 6884363 -->
macOS デバイス向けのシェル スクリプトを構成するときに、次の新しい設定を構成できるようになりました。 
- デバイスでスクリプトの通知を非表示にする
- スクリプトの頻度
- スクリプトが失敗した場合の再試行回数の最大値

詳細については、「[Intune で macOS デバイスに対してシェル スクリプトを使用する](../apps/macos-shell-scripts.md)」を参照してください。

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>2020 年 3 月 30 日の週

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Microsoft Endpoint Manager admin center の新しい URL<!-- 3704810 -->
昨年の Ignite での Microsoft エンドポイント マネージャーの発表に合わせて、Microsoft Endpoint Manager admin center (旧称 Microsoft 365 デバイス管理) の URL を [https://endpoint.microsoft.com](https://endpoint.microsoft.com) に変更しました。 古い管理センターの URL ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) は引き続き機能しますが、新しい URL を使用して Microsoft Endpoint Manager admin center へのアクセスを開始することをお勧めします。

詳細については、「[Microsoft Endpoint Manager admin center を使用して IT タスクを簡略化する](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center)」を参照してください。  


### <a name="app-management"></a>アプリ管理  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>iOS 用ポータル サイトでの横向きモードのサポート<!--6048329  -->   
ユーザーは、好みの画面の向きを使用して、デバイスを登録したり、アプリを検索したり、IT サポートを受けたりできるようになりました。 ユーザーが縦向きモードで画面をロックしない限り、アプリでは画面を縦向きまたは横向きモードに合わせて自動的に検出して調整します。  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>macOS デバイスのスクリプト サポート (パブリック プレビュー)<!-- 4280361  -->
macOS デバイスにスクリプトを追加して展開できます。 このサポートにより、macOS デバイスを構成する機能が拡張され、macOS デバイスでネイティブの MDM 機能を使用してできること以上のことが可能になります。 詳細については、「[Intune で macOS デバイスに対してシェル スクリプトを使用する](../apps/macos-shell-scripts.md)」を参照してください。

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>2020 年 3 月 24 日の週

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Android および Android Enterprise デバイスでデバイス制限プロファイルを作成するときのユーザー インターフェイス エクスペリエンスの向上<!-- 5841361 -->
Android または Android Enterprise デバイス用のプロファイルを作成するときの、Endpoint Management 管理センターのエクスペリエンスが更新されます。 この変更は、次のデバイス構成プロファイルに影響します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > **プラットフォームの [Android デバイス管理者]** または **[Android Enterprise]** )。

- デバイスの制限:Android デバイス管理者
- デバイスの制限:Android Enterprise デバイス所有者
- デバイスの制限:Android Enterprise 仕事用プロファイル

構成できるデバイスの制限の詳細については、[Android デバイス管理者](../configuration/device-restrictions-android.md)と [Android Enterprise](../configuration/device-restrictions-android-for-work.md) に関するページを参照してください。

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>iOS/iPadOS および macOS デバイスで構成プロファイルを作成するときのユーザー インターフェイス エクスペリエンスの向上<!-- 5569002 5568997 -->
iOS または macOS デバイス用のプロファイルを作成するときの、エンドポイント管理センターのエクスペリエンスが更新されます。 この変更は、次のデバイス構成プロファイルに影響します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[iOS/iPadOS]** または **[macOS]** ):

- カスタム: iOS/iPadOS、macOS
- デバイスの機能: iOS/iPadOS、macOS
- デバイスの制限: iOS/iPadOS、macOS
- エンドポイント保護: macOS
- 拡張機能: macOS
- 設定ファイル: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>macOS デバイスのデバイス機能でユーザー構成設定を非表示にする<!-- 6524869 -->

macOS デバイスでデバイス機能の構成プロファイルを作成するときに、新しい設定 **[ユーザーの構成を非表示にします]** があります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームに **[macOS]** > プロファイルに **[デバイスの機能]** > **[ログイン項目]** )。

この機能では、macOS デバイスの **[ユーザーとグループ]** ログイン項目アプリのリストに、アプリの非表示のチェックマークが設定されます。 既存のプロファイルでは、この設定が未構成としてリスト内に表示されます。 この設定を構成するために、管理者は既存のプロファイルを更新できます。

**[非表示]** に設定すると、アプリの [非表示] チェックボックスがオンになり、ユーザーは変更することはできません。 また、ユーザーが自分のデバイスにサインインした後に、ユーザーに対してアプリを非表示にします。

> [!div class="mx-imgBorder"]
> ![Microsoft Intune とエンドポイント マネージャーでユーザーがデバイスにサインインした後に macOS デバイスでアプリを非表示にする](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

構成できる設定の詳細については、[macOS デバイスの機能設定](../configuration/macos-device-features-settings.md)に関する記事を参照してください。

この機能は、以下に適用されます。

- macOS

<!-- ########################## -->
## <a name="week-of-march-16-2020-2003-service-release"></a>2020 年 3 月 16 日の週 (2003 サービス リリース)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>macOS および iOS ポータル サイトの更新<!-- 5779439, 5780234  -->
macOS および iOS ポータル サイトの [プロファイル] ウィンドウが更新され、サインアウト ボタンが追加されました。 さらに、macOS ポータル サイトの [プロファイル] ウィンドウは UI が改善されました。 ポータル サイトの詳細については、「[Microsoft Intune ポータル サイト アプリを構成する方法](../apps/company-portal-app.md)」をご覧ください。

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>iOS デバイス上の Microsoft Edge に Web クリップを再ターゲットする<!-- 5455276   -->
保護されたブラウザーで開く必要がある、iOS デバイス上の新たに展開された Web クリップ (ピン留めされた Web アプリ) は、Intune Managed Browser ではなく Microsoft Edge で開かれます。 既存の Web クリップを再ターゲットして、Managed Browser ではなく Microsoft Edge で開くようにする必要があります。 詳細については、「[Microsoft Edge と Microsoft Intune を使用して Web アクセスを管理する](../apps/manage-microsoft-edge.md)」および「[Web アプリを Microsoft Intune に追加する](../apps/web-app.md)」をご覧ください。

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Android 用 Microsoft Edge で Intune 診断ツールを使用する<!-- 4735244  -->
Android 用 Microsoft Edge が Intune 診断ツールと統合されました。 iOS 用 Microsoft Edge のエクスペリエンスと同様に、デバイス上の Microsoft Edge の URL バー (アドレス ボックス) に「about:intunehelp」と入力すると、Intune 診断ツールが開始されます。 このツールでは、詳細なログが提供されます。 ユーザーは、ガイドを利用しながら、これらのログを収集して IT 部門に送信したり、特定のアプリの MAM ログを表示したりできます。

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Intune のブランド化とカスタマイズの更新<!-- 5236032  -->
"ブランド化とカスタマイズ" という名前だった Intune ウィンドウが更新され、次のような改善が加えられました。

- ペインの名前を**カスタマイズ**に変更。
- 設定の編成と設計の改善。
- 設定のテキストとヒントの改善。

Intune でこれらの設定を見つけるには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に移動し、 **[テナント管理]**  >  **[カスタマイズ]** の順に選択します。 既存のカスタマイズについては、「[Microsoft Intune ポータル サイト アプリを構成する方法](../apps/company-portal-app.md)」を参照してください。

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>ユーザーの個人用の暗号化された回復キー<!-- 6273943  -->
ユーザーが Android ポータル サイト アプリケーションまたは Android Intune アプリケーションを介して、Mac デバイスの個人用の暗号化された **FileVault** 回復キーを取得できるようにする、新しい Intune 機能を使用できます。 ポータル サイト アプリケーションと Intune アプリケーションの両方にリンクが表示されます。これを使用すると、Chrome ブラウザーで Web ポータル サイトが開き、そこでユーザーは Mac デバイスにアクセスするために必要な **FileVault** 回復キーを確認できます。 暗号化の詳細については、「[Intune でデバイスの暗号化を使用する](../protect/encrypt-devices.md)」を参照してください。

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>専用デバイスの登録の最適化 <!-- 6114580  -->
Android エンタープライズ専用デバイスの登録を最適化し、Wi-Fi に関連付けられた SCEP 証明書を 2019 年 11 月 22 日より前に登録した専用デバイスに適用しやすくしています。 新しい登録の場合、Intune アプリは引き続きインストールされますが、エンド ユーザーは登録中に **Intune エージェントを有効にする**手順を実行する必要がなくなります。 インストールはバックグラウンドで自動的に行われ、Wi-Fi に関連付けられた SCEP 証明書はエンド ユーザーの介入なしで展開および設定できます。  

これらの変更は、Intune サービス バックエンドの展開として 3 月中に段階的にロールアウトされます。 3 月の終わりまでに、すべてのテナントでこの新しい動作が実現されます。 関連情報については、「[Android エンタープライズ専用デバイスでの SCEP 証明書のサポート](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147)」をご覧ください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>デバイスの構成

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Windows デバイスに対する管理用テンプレートを作成するときの新しいユーザー エクスペリエンス<!--5096036 -->
お客様からのフィードバックに基づき、新しい Azure の全画面表示エクスペリエンスへの移行に伴って、管理用テンプレート プロファイルのエクスペリエンスをフォルダー ビューを使用して再構築しました。 設定や既存のプロファイルに対する変更は加えられていません。 そのため、お使いの既存のプロファイルは変更されず、そのまま新しいビューで使用できます。 **[すべての設定]** を選択し、検索を使用することで、引き続きすべての設定オプションを参照できます。 ツリー ビューは、コンピューターの構成とユーザーの構成によって分割されます。 Windows、Office、および Edge の設定は、その関連するフォルダーに配置されます。  

適用対象:
- Windows 10 以降

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>IKEv2 VPN 接続を使用する VPN プロファイルでは iOS/iPadOS デバイスで常時接続を使用できる<!-- 1947932   -->
iOS/iPadOS デバイスでは、IKEv2 接続を使用する VPN プロファイルを作成することができます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[iOS/iPadOS]** > プロファイル タイプの **[VPN]** )。 現在、IKEv2 を使用して常時接続を構成できます。 構成すると、IKEv2 VPN プロファイルは自動的に接続され、VPN に接続されたままになります (またはすぐに再接続されます)。 ネットワーク間を移動したり、デバイスを再起動したりしても、接続されたままになります。

iOS/iPadOS では、常時接続 VPN は IKEv2 プロファイルに限定されます。

構成できる IKEv2 設定については、[Microsoft Intune で iOS デバイス向けの VPN 設定を追加する方法](../configuration/vpn-settings-ios.md#ikev2-settings)に関する記事をご覧ください。

適用対象:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Android Enterprise デバイスで OEMConfig デバイス構成プロファイルのバンドルとバンドル配列を削除する<!-- 5550355   -->
Android エンタープライズ デバイスでは、OEMConfig プロファイルを作成して構成します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[Android Enterprise]** > プロファイルの種類の **[OEMConfig]** )。 現在、ユーザーは、Intune の**構成デザイナー**を使用して、バンドルとバンドル配列を削除できます。

OEMConfig プロファイルの詳細については、「[Microsoft Intune で、OEMConfig を使って Android Enterprise デバイスを使用および管理する](../configuration/android-oem-configuration-overview.md)」を参照してください。

適用対象:
- Android エンタープライズ

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>iOS/iPadOS の Microsoft Azure AD SSO アプリ拡張機能を構成する<!-- 5672534   -->
Microsoft Azure AD チームは、iOS/iPadOS 13.0 以降のユーザーが、1 回のサインオンで Microsoft アプリと Web サイトにアクセスできるようにするために、リダイレクト シングル サインオン (SSO) アプリ拡張機能を開発しました。 以前に Microsoft Authenticator アプリで仲介型認証を使用していたすべてのアプリは、新しい SSO 拡張機能で引き続き SSO を取得します。 Azure AD SSO アプリ拡張機能のリリースに伴い、リダイレクト SSO アプリ拡張機能の種類を使用して SSO 拡張機能を構成できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  プラットフォームの **[iOS/iPadOS]** > プロファイルの種類の **[デバイスの機能]** > **[シングル サインオン アプリ拡張機能]** )。

適用対象:
- iOS 13.0 以降
- iPadOS 13.0 以降

iOS SSO アプリ拡張機能について詳しくは、「[シングル サインオン アプリ拡張機能](../configuration/device-features-configure.md#single-sign-on-app-extension)」をご覧ください。

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>[エンタープライズ アプリの信頼設定の変更] 設定が iOS/iPadOS デバイスの制限プロファイルから削除される<!-- 6225131   -->
iOS/iPadOS デバイス上に、デバイスの制限プロファイルを作成します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > プラットフォームとして **[iOS/iPadOS]** > プロファイルの種類として **[デバイスの制限]** )。 **[エンタープライズ アプリの信頼設定の変更]** 設定は、Apple によって削除され、Intune から削除されます。 プロファイルで現在この設定を使用している場合、それは影響を及ぼさず、既存のプロファイルから削除されます。 この設定は、Intune のレポートからも削除されます。

適用対象:
- iOS/iPadOS

制限できる設定を確認するには、[機能を許可または制限するための iOS および iPadOS デバイスの設定](../configuration/device-restrictions-ios.md)に関するページに移動します。

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>トラブルシューティング:保留中の MAM ポリシーの通知が情報アイコンに変更されました<!--6348954 -->
トラブルシューティング ブレードでの保留中の MAM ポリシーの通知アイコンが、情報アイコンに変更されました。

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>コンプライアンス ポリシーを構成するときの UI の更新<!-- 3961639    -->

Microsoft Endpoint Manager で[コンプライアンス ポリシーを作成する](../protect/create-compliance-policy.md#create-the-policy)ための UI が更新されました ( **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシー]**  >  **[ポリシーの作成]** )。 以前に使用していたのと同じ設定と詳細情報を含む新しいユーザー エクスペリエンスが提供されます。 新しいエクスペリエンスでは、ウィザードのようなプロセスに従ってコンプライアンス ポリシーを作成することができ、ポリシーの *[割り当て]* を追加できるページと、ポリシーを作成する前に構成を確認できる *[確認および作成]* ページが含まれます。

#### <a name="retire-noncompliant-devices---1827291---------"></a>非準拠デバイスをインベントリから削除する<!-- 1827291       -->
任意のポリシーに追加できる、準拠していないデバイスに対する新しいアクション、[準拠していないデバイスをインベントリから削除](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance)が追加されました。  この新しいアクション **[準拠していないデバイスを削除します]** を使用すると、そのデバイスから会社のデータがすべて削除され、また、そのデバイスが Intune による管理対象から削除されます。  このアクションは、構成した日数の値に達し、その時点でデバイスがインベントリから削除可能になったときに実行されます。 最小値は 30 日間です。  デバイスをインベントリから削除するには、IT 管理者の明示的な承認が必要になります。その場合、 *[準拠していないデバイスを削除します]* セクションを使用し、そこで管理者は対象となるすべてのデバイスをインベントリから削除できます。

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>iOS エンタープライズ Wi-Fi プロファイルでの WPA と WPA2 のサポート<!--6215273   -->
[iOS 用エンタープライズ Wi-Fi プロファイル](../configuration/wi-fi-settings-ios.md#enterprise-profiles)で、 *[セキュリティの種類]* フィールドがサポートされるようになりました。 *[セキュリティの種類]* には、**WPA エンタープライズ**または **WPA/WPA2 エンタープライズ**のいずれかを選択した後、 *[EAP の種類]* の選択を指定できます。  ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** で、 *[プラットフォーム]* に **[iOS/iPadOS]** を選択し、 *[プロファイル]* に **[Wi-Fi]** を選択します)。 

新しいエンタープライズ オプションは、iOS 用の基本的な Wi-Fi プロファイルに対して使用できたオプションと似ています。

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>証明書、電子メール、VPN、および Wi-Fi、VPN プロファイルの新しいユーザー エクスペリエンス<!-- 5615208   -->
Endpoint Management 管理センターで次のプロファイルの種類の作成および変更を行うための[ユーザー エクスペリエンス](../configuration/device-profile-create.md)が更新されました ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** )。 新しいエクスペリエンスでは、以前と同じ設定が表示されますが、あまり水平スクロールを必要としないウィザードのようなエクスペリエンスが使用されます。 新しいエクスペリエンスで既存の構成を変更する必要はありません。

- 派生資格情報
- 電子メール
- PKCS 証明書
- PKCS のインポートされた証明書
- SCEP 証明書
- 信頼された証明書
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>デバイスの登録

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Android と iOS 用のポータル サイトで登録を使用できるようにするかどうかを構成する<!-- 4260128  -->
Android および iOS デバイス上のポータル サイトでのデバイス登録を、プロンプトを表示して使用できるようにするか、プロンプトを表示せずに使用できるようにするか、またはユーザーが使用できないようにするかを構成できます。 Intune でこれらの設定を見つけるには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に移動し、 **[テナント管理]**  >  **[カスタマイズ]**  >  **[編集]**  >  **[デバイスの登録]** の順に選択します。  

デバイス登録設定をサポートするには、エンド ユーザーに次のバージョンのポータル サイトが必要です。
-    iOS 上のポータル サイト: バージョン 4.4 以降
-    Android 上のポータル サイト: バージョン 5.0.4715.0 以降

既存のポータル サイトのカスタマイズについては、「[Microsoft Intune ポータル サイト アプリを構成する方法](../apps/company-portal-app.md)」を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Android デバイスの概要ページの新しい Android レポート<!-- 5435435   -->
Microsoft Endpoint Manager 管理コンソールの Android デバイスの概要ページに、各デバイス管理ソリューションに登録されている Android デバイスの数を表示するレポートが追加されました。 このグラフ (Azure コンソールに既にあるのと同じような) には、仕事用プロファイル、フル マネージド、専用、およびデバイス管理者が登録したデバイスの数が表示されます。 レポートを表示するには、 **[デバイス]**  >  **[Android]**  >  **[概要]** の順に選択します。

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Android デバイス管理者の管理から仕事用プロファイルの管理にユーザーをガイドする<!--5857738   -->
Android デバイス管理者プラットフォーム用の新しいコンプライアンス設定をリリースしています。 この設定を使用すると、デバイス管理者によって管理される場合にデバイスを非準拠にすることができます。

これらの非準拠デバイスでは、 **[デバイス設定の更新]** ページに、ユーザーに対して **[新しいデバイス管理セットアップに移動する]** メッセージが表示されます。 **[解決]** ボタンをタップすると、次のようにガイドされます。

1. デバイス管理者の管理からの登録解除
2. 仕事用プロファイルの管理への登録
3. コンプライアンスに関する問題の解決 
 
Google では、Android Enterprise を使用した最新のより豊富で安全なデバイス管理に移行するための取り組みの一環として、新しい Android リリースでのデバイス管理者サポートを縮小しています。  Intune では、Android 10 以降を実行している、デバイス管理者が管理する Android デバイスのフル サポートを 2020 年第 2 四半期までのみ提供できます。 これを過ぎると、Android 10 以降を実行している、デバイス管理者が管理するデバイス (Samsung を除く) は、完全には管理できなくなります。 具体的には、影響を受けるデバイスが新しいパスワード要件を受け取ることはありません。

この設定の詳細については、「[Android デバイスをデバイス管理者から仕事用プロファイル管理に移動する](../enrollment/android-move-device-admin-work-profile.md)」をご覧ください。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>データ ウェアハウスでの MAC アドレスの提供開始<!-- 6123680  -->
Intune データ ウェアハウスでは、`device` エンティティ内の新しいプロパティ (`EthernetMacAddress`) として MAC アドレスが提供され、管理者がユーザーとホスト間の MAC アドレスを関連付けることができるようになります。 このプロパティは、特定のユーザーに接続し、そのネットワーク上で発生しているインシデントをトラブルシューティングするのに役立ちます。 また、管理者は、[Power BI レポート](../developer/reports-proc-get-a-link-powerbi.md)内でこのプロパティを使用し、より豊富な機能を備えたレポートを作成することもできます。 詳細については、Intune データ ウェアハウスの [device](../developer/intune-data-warehouse-collections.md#devices) エンティティを参照してください。

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>追加のデータ ウェアハウス デバイス インベントリ プロパティ<!-- 6125732  -->
Intune データ ウェアハウスを使用して、追加のデバイス インベントリ プロパティを使用できます。 次のプロパティが、[device](../developer/reports-ref-devices.md#devices) ベータ版コレクションを介して公開されるようになりました。
- `ethernetMacAddress` - このデバイスの一意のネットワーク識別子。
- `model` - デバイスのモデル。
- `office365Version` - デバイスにインストールされている Office 365 のバージョン。
- `windowsOsEdition` - オペレーティング システムのバージョン。

次のプロパティが、[devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) ベータ版コレクションを介して公開されるようになりました。
- `physicalMemoryInBytes` - 物理メモリ (バイト単位)。
- `totalStorageSpaceInBytes` - 記憶域の合計容量 (バイト単位)。

詳細については、「[Microsoft Intune データ ウェアハウス API](../developer/reports-nav-intune-data-warehouse.md)」を参照してください。

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>追加サービスをサポートするためのヘルプとサポート ワークフローの更新<!-- 5654170   -->
Microsoft Endpoint Manager admin center の [ヘルプとサポート] ページが更新され、[使用する管理の種類を選択](../fundamentals/get-support.md#options-to-access-help-and-support)できるようになりました。 この変更により、次の管理の種類から選択できるようになります。

- Configuration Manager (Desktop Analytics を含む)
- Intune
- 共同管理

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>セキュリティ

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>エンドポイント セキュリティの一部としてセキュリティ管理者に焦点を当てたポリシーのプレビューを使用する<!--6131401  -->
パブリック プレビューとして、Microsoft Endpoint Management 管理センターのエンドポイント セキュリティ ノードに、いくつかの新しいポリシー グループが追加されました。 セキュリティ管理者は、これらの新しいポリシーを使用してデバイス セキュリティに関する特定の側面に焦点を当て、より大きなデバイス構成ポリシー本文によるオーバーヘッドを発生させることなく、関連する設定の個別のグループを管理できます。

"*Microsoft Defender ウイルス対策のウイルス対策ポリシー*" を除き (下記参照)、これらの新しいプレビューの各ポリシーおよびプロファイルの設定は、現在既に[デバイス構成プロファイル](../configuration/device-profile-create.md)を使用して構成している可能性がある設定と同じものです。

すべてプレビューである新しいポリシーの種類と、その使用可能なプロファイルの種類を次に示します。

- **[ウイルス対策 (プレビュー)]** :
  - macOS:
    - **[ウイルス対策]** - macOS 用の[ウイルス対策ポリシーの設定](../protect/antivirus-microsoft-defender-settings-macos.md)を管理して、[Microsoft Defender ATP for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) を管理します。

  - Windows 10 以降:
    - **[Microsoft Defender ウイルス対策]** - クラウド保護、ウイルス対策の除外、修復、スキャン オプションなどのための[ウイルス対策ポリシーの設定](../protect/antivirus-microsoft-defender-settings-windows.md)を管理します。

      *[Microsoft Defender ウイルス対策]* のウイルス対策プロファイルは、デバイス制限プロファイルの一部として検出される、設定の新しいインスタンスを導入する例外です。 これらの新しいウイルス対策の設定は:

        - デバイス制限で使用されるのと同じ設定ですが、デバイス制限として構成する場合は使用できない、構成の 3 番目のオプションがサポートされています。
        - Endpoint Protection の[共同管理ワークロードのスライダー](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)が Intune に設定されている場合に、Configuration Manager で共同管理されているデバイスに適用されます。

     デバイス制限プロファイルを使用して構成する代わりに、新しい *[ウイルス対策]*  >  *[Microsoft Defender ウイルス対策]* プロファイルを使用することを計画してください。

  - **[Windows セキュリティ エクスペリエンス]** - エンド ユーザーが Microsoft Defender セキュリティ センターで表示できる Windows セキュリティ設定と、エンド ユーザーが受信する通知を管理します。 これらの設定は、デバイス構成 Endpoint Protection プロファイルとして使用できる設定から変更されていません。

- **[ディスク暗号化 (プレビュー)]** :
  - macOS:
    - **FileVault**
  - Windows 10 以降:
    - **BitLocker**
- **[ファイアウォール (プレビュー)]** :
  - macOS:
    - **[macOS ファイアウォール]**
  - Windows 10 以降:
    - **Microsoft Defender ファイアウォール**
- **[エンドポイントの検出と応答 (プレビュー)]** :
  - Windows 10 以降:-**Windows 10 Intune**
- **[攻撃面の減少 (プレビュー)]** :
  - Windows 10 以降:
    - **[アプリとブラウザーの分離]**
    - **[Web 保護]**
    - **[アプリケーションの制御]**
    - **[攻撃の回避規則]**
    - **[デバイス制御]**
    - **[悪用に対する保護]**
- **[アカウント保護 (プレビュー)]** :
  - Windows 10 以降:
    - **[アカウント保護]**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>2020 年 3 月 9 日の週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Win32 アプリ コンテンツをダウンロードするときに配信の最適化エージェントを構成する<!-- 5410945 -->

配信の最適化エージェントを、割り当てに基づいてバックグラウンドまたはフォアグラウンド モードで Win32 アプリ コンテンツをダウンロードするように構成できます。 既存の Win32 アプリでは、コンテンツは引き続きバックグラウンド モードでダウンロードされます。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[すべてのアプリ]**  > "*Win32 アプリを選択*" >  **[プロパティ]** の順に選択します。 **[割り当て]** の横にある **[編集]** を選択します。  **[必須]** セクションの **[モード]** の下で **[含める]** を選択して、割り当てを編集します。  **[アプリの設定]** セクションに新しい設定が表示されます。 配信の最適化の詳細については、[「Win32 アプリ管理」の「配信の最適化」](../apps/apps-win32-app-management.md#delivery-optimization)を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Windows デバイスのプライマリ ユーザーを変更する<!-- 3794742   -->
Windows ハイブリッド デバイスと Azure AD 参加済みデバイスのプライマリ ユーザーを変更できます。 これを行うには、 **[Intune]**  >  **[デバイス]**  >  **[すべてのデバイス]** > デバイスを選択 > **[プロパティ]**  >  **[プライマリ ユーザー]** を選択します。 詳細については、「[デバイスのプライマリ ユーザーを変更する](../remote-actions/find-primary-user.md#change-a-devices-primary-user)」をご覧ください。

このタスクに対して、新しい RBAC アクセス許可 (マネージド デバイス/プライマリ ユーザーの設定) も作成されています。 このアクセス許可は、ヘルプデスク オペレーター、学校管理者、エンドポイント セキュリティ マネージャーなどの組み込みロールに追加されています。

この機能は、プレビューとしてグローバルにお客様にロールアウトされています。 この機能は、今後数週間以内に表示されるはずです。


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>2020 年 3 月 2 日の週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Microsoft Endpoint Manager テナントのアタッチ:デバイスの同期とデバイスのアクション<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager によって、Configuration Manager と Intune が 1 つのコンソールに統合されます。 Configuration Manager Technical Preview バージョン 2002.2 以降、ご利用の Configuration Manager デバイスをクラウド サービスにアップロードし、管理センターからそれらに対するアクションを実行できます。 詳細については、[Configuration Manager Technical Preview バージョン 2002.2 の機能](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach)に関する記事をご覧ください。

この更新プログラムをインストールする前に、[Configuration Manager Technical Preview に関する記事](https://docs.microsoft.com/configmgr/core/get-started/technical-preview)をご確認ください。 この記事により、Technical Preview の使用に関する一般的な要件と制限事項、バージョン間の更新方法、フィードバックを提供する方法についての理解を深めることができます。

#### <a name="bulk-remote-actions--4576882--"></a>一括リモート操作<!--4576882-->
次のリモート操作に対して、一括コマンドを発行できるようになりました: 再起動、名前変更、Autopilot リセット、ワイプ、削除。 新しい一括操作を表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[すべてのデバイス]**  >  **[Bulk actions]\(一括操作\)** の順に移動します。

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>すべてのデバイス リストで検索、並べ替え、フィルターが改善<!--6179023-->
[すべてのデバイス] リストが改善され、パフォーマンスが上がり、検索、並べ替え、フィルター処理の各種機能が強化されました。 詳細については、[こちらのサポート ヒント](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946)に関する記事をご覧ください。  

### <a name="app-management"></a>アプリ管理  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Android 用ポータル サイトでのサインイン エクスペリエンスの向上    
エクスペリエンスをユーザーにとってより新しく、シンプルでクリーンなものにするために、Android 用ポータル サイト アプリのいくつかのサインイン画面のレイアウトを更新しました。 機能強化の詳細については、「[アプリの UI の新機能](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui)」を参照してください。

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>2020 年 2 月 24 日の週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>macOS ポータル サイトのユーザー エクスペリエンスの向上<!-- 5568987 -->
macOS デバイスを登録しやすくし、Mac 用ポータル サイト アプリを改善しました。 次の点が改善されています。
- 登録時の Microsoft **AutoUpdate** エクスペリエンスが向上し、ユーザーが最新バージョンのポータル サイトを確実に使用できるようになります。
- 登録時のコンプライアンス チェック手順が強化されます。
- インシデント ID のコピーがサポートされるため、ユーザーは自分のデバイスから会社のサポート チームにエラーを迅速に送信することができます。

Mac の登録とポータルサイトアプリの詳細については、「[ポータル サイト アプリを使用して macOS デバイスを登録する](../user-help/enroll-your-device-in-intune-macos-cp.md)」を参照してください。

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Better Mobile のアプリ保護ポリシーで iOS と iPadOS がサポートされるようになりました<!-- 6224512  -->

2019 年 10 月に、Intune アプリ保護ポリシーに、Microsoft の脅威防御パートナーのデータを使用する機能が追加されました。 この更新により、アプリ保護ポリシーを使用して、iOS と iPadOS で Better Mobile を使用するデバイスの正常性に基づいてユーザーの企業データをブロックしたり選択的にワイプしたりできるようになりました。  詳細については、「[Intune で Mobile Threat Defense アプリ保護ポリシーを作成する](../protect/mtd-app-protection-policy.md)」をご覧ください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>すべてのデバイスのリストのエクスポートが CSV 形式で圧縮されるようになりました<!--6343117-->
**[デバイス]**  >  **[すべてのデバイス]** ページからのエクスポートが CSV 形式で圧縮されるようになりました。


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>2020 年 2 月 17 日の週 (2002 サービス リリース)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>macOS 用 Microsoft Defender Advanced Threat Protection (ATP) アプリ<!-- 5424618 -->
Intune を使用すると、macOS 用 Microsoft Defender Advanced Threat Protection (ATP) アプリを管理対象 Mac デバイスに簡単に展開できます。 詳細については、「[Microsoft Intune を使用して Microsoft Defender ATP を macOS に追加する](../apps/apps-advanced-threat-protection-macos.md)」と「[Microsoft Defender Advanced Threat Protection for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)」を参照してください。  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>デバイスの構成

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>iOS デバイスで Cisco AnyConnect VPN を利用し、ネットワーク アクセス制御 (NAC) を有効にする<!-- 4860111  -->
iOS デバイスで、VPN プロファイルを作成し、Cisco AnyConnect など ( **[デバイス構成]**  >  **[プロファイル]**  >  **[プロファイルの作成]** の順に選択し > プラットフォームに **[iOS]** を選択し、プロファイルの種類に **[VPN]** を選択し、接続の種類に **[Cisco AnyConnect]** を選択する)、さまざまな種類の接続を使用できます。

Cisco AnyConnect を利用し、ネットワーク アクセス制御 (NAC) を有効にできます。 この機能を使用するには、以下を行います。

1. 「[Cisco Identity Services Engine 管理者ガイド](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)」の「**Configuring Microsoft Intune as an MDM Server**」(Microsoft Intune の MDM サーバーとしての構成) に記載されている手順を利用し、Azure で Cisco Identity Services Engine (ISE) を構成します。
2. Intune デバイス構成プロファイルで、 **[ネットワーク アクセス制御 (NAC) を有効にする]** 設定を選択します。

利用できる VPN 設定については、[iOS デバイスへの VPN 設定の構成](../configuration/vpn-settings-ios.md)に関する記事を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>デバイスの登録

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>[Apple MDM プッシュ通知証明書] ページのシリアル番号<!--5947765  -->
[Apple MDM プッシュ通知証明書] ページにシリアル番号が表示されるようになりました。 証明書を作成した Apple ID へのアクセスが失われた場合に、Apple MDM プッシュ通知証明書へのアクセスを回復するには、シリアル番号が必要です。 シリアル番号を表示するには、 **[デバイス]**  >  **[iOS]**  >  **[iOS enrollment]\(iOS の登録\)**  >  **[Apple MDM プッシュ通知証明書]** に移動します。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>デバイス管理

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>登録された iOS デバイスまたは iPadOS デバイスに OS 更新プログラムをプッシュするための新しい更新スケジュール オプション<!--5879689  -->
iOS/iPadOS デバイスのオペレーティング システムの更新をスケジュールするとき、次のオプションから選択できます。 これらのオプションは、Apple Business Manager または Apple School Manager の登録タイプを使用したデバイスに適用されます。
- 次回のチェックイン時に更新する
- スケジュールされた時刻に更新する
- スケジュールされた時刻以外に更新する

後者の 2 つのオプションでは、複数の時間帯を作成できます。

新しいオプションを確認するには、MEM > **[デバイス]**  >  **[iOS]**  >  **[Update policies for iOS/iPadOS]\(iOS または iPadOS のポリシーを更新する\)**  >  **[プロファイルの作成]** に移動します。

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>登録されたデバイスにプッシュする iOS または iPadOS の更新プログラムを選択する<!--5879689  -->
Apple Business Manager または Apple School Manager を使用すると、登録されたデバイスにプッシュする特定の iOS/iPadOS の更新プログラムを選択できます (最新の更新プログラムを除く)。 これらのデバイスでは、ソフトウェア更新プログラムの可視性を一定の日数だけ遅らせるようにデバイス構成ポリシーを設定する必要があります。 この機能を確認するには、MEM > **[デバイス]**  >  **[iOS]**  >  **[Update policies for iOS/iPadOS]\(iOS または iPadOS のポリシーを更新する\)**  >  **[プロファイルの作成]** に移動します。



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>デバイス セキュリティ

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Intune レポート エクスペリエンスの向上<!-- 3791418   -->
Intune では、新しいレポートの種類、より優れたレポート編成、より対象を絞ったビュー、より優れたレポート機能、より一貫性のあるタイムリーなデータを含め、レポート エクスペリエンスが向上しています。 レポート エクスペリエンスは、パブリック プレビューから GA (一般公開) に移行します。 また、GA リリースでは、[Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)のタイルで、ローカライズ サポート、バグ修正、設計の改善、デバイス コンプライアンス データの集計を行うことができます。

新しいレポートの種類では、次の情報に重点が置かれています。

- **運用** - 正常性への悪影響に焦点を置いた最新のレコードが表示されます。 
- **組織** - 全体的な状態の概要が表示されます。
- **履歴** - 一定期間におけるパターンと傾向が表示されます。
- **スペシャリスト** - 生データを使用して独自のカスタム レポートを作成できます。

新しいレポートの最初のセットでは、デバイスのコンプライアンスに重点が置かれています。 詳細については、[ブログ - Microsoft Intune レポート フレームワーク](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553)および[Intune レポート](reports.md)に関するページを参照してください。

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>UI でセキュリティ ベースラインの場所を統合<!-- 6177074   -->
いくつかの UI の場所から*セキュリティ ベースライン*を削除し、パスを統合して、Microsoft Endpoint Manager admin center で[セキュリティ ベースライン](../protect/security-baselines.md)を見つけられるようにしました。 セキュリティ ベースラインを見つける場合、今後は次のパスを使用します。**エンドポイント セキュリティ** > **セキュリティ ベースライン**。

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>インポートした PKCS 証明書のサポート拡張<!-- 6044197  -->
[インポートされた PKCS 証明書](../protect/certificates-imported-pfx-configure.md#supported-platforms)を使用するためのサポートが拡張され、"*Android Enterprise フル マネージド デバイス*" がサポートされるようになりました。 一般的に、PFX 証明書のインポートは S/MIME 暗号化シナリオで利用されます。ここでは、電子メールを復号化できるよう、ユーザーのすべてのデバイスでユーザーの暗号化証明書が必須となります。

次のプラットフォームでは、PFX 証明書のインポートがサポートされています。

- Android - デバイス管理者
- Android Enterprise - フル マネージド
- Android Enterprise - 仕事用プロファイル
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>デバイスのエンドポイント セキュリティ構成を表示する<!-- 6206460  -->
[特定のデバイスに適用されるエンドポイント セキュリティ構成](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)を表示する目的で、Microsoft Endpoint Manager admin center のオプションの名前を更新しました。 このオプションの名前は**エンドポイント セキュリティ構成**に変更されました。該当するセキュリティ ベースラインと、セキュリティ ベースラインの外部で作成された追加ポリシーを示すためです。 このオプションの以前の名前は "*セキュリティ ベースライン*" でした。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>ロール ベースのアクセス制御

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Intune ロールのユーザー インターフェイスが変更予定<!--5801612   -->
[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[テナント管理]**  >  **[ロール]** のユーザー インターフェイスが改善され、ユーザーにとって使いやすく、直観的なデザインになりました。 このエクスペリエンスでは、現在使用しているのと同じ設定と詳細が提供されます。ただし、新しいエクスペリエンスでは、ウィザードに似たプロセスが採用されています。

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>2020 年 2 月 17 日の週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="microsofts-new-office-app---5859926---"></a>Microsoft の新しい Office アプリ<!-- 5859926 -->
Microsoft の新しい Office アプリが一般公開され、ダウンロードして使用できるようになりました。 Office アプリは統合環境であり、ユーザーは 1 つのアプリ内で Word、Excel、PowerPoint をまたいで作業できます。 アクセスするデータが保護されるよう、アプリをアプリ保護ポリシーの対象にできます。

詳細については、「[Office モバイル プレビュー アプリで Intune アプリ保護ポリシーを有効にする方法](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493)」を参照してください。

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>2020 年 2 月 10 日の週

### <a name="windows-7-ends-extended-support--3042987---"></a>Windows 7 の延長サポートの終了<!--3042987 -->
Windows 7 の延長サポートは、2020 年 1 月 14 日に終了しました。 同時に、Intune では Windows 7 を稼働しているデバイスのサポートが非推奨になりました。 PC の保護に役立つ技術的なサポートや自動更新が利用できなくなりました。 Windows 10 にアップグレードする必要があります。 詳細については、[変更の計画に関するブログ記事](https://aka.ms/Windows7_Intune)を参照してください。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>アプリ管理

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Windows 10 デバイスの Microsoft Edge バージョン 77 以降<!-- 5843584 -->
Intune で、Windows 10 デバイスでの Microsoft Edge バージョン 77 以降のアンインストールがサポートされるようになりました。 詳細については、「[Microsoft Edge for Windows 10 を Microsoft Intune に追加する](../apps/apps-windows-edge.md)」を参照してください。

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>ポータル サイトの Android 仕事用プロファイルの登録から削除される画面<!--6103987 -->
ユーザー エクスペリエンスを効率化するために、ポータル サイトの Android 仕事用プロファイルの登録フローから **[次の手順]** 画面が削除されました。 更新後の Android 仕事用プロファイルの登録フローを確認するには、[Android 仕事用プロファイルへの登録](../user-help/enroll-device-android-work-profile.md)に関する記事を参照してください。  

#### <a name="company-portal-app-improved-performance---6178652---"></a>ポータル サイト アプリのパフォーマンスの向上<!-- 6178652 -->
ポータル サイト アプリが更新され、Surface Pro X などの ARM64 プロセッサを使用したデバイス向けのパフォーマンスの向上がサポートされました。これまでは、ポータル サイトはエミュレートされた ARM32 モードで動作していました。 現在、バージョン 10.4.7080.0 以降では、ポータル サイト アプリは ARM64 用にネイティブ コンパイルされています。 ポータル サイト アプリの詳細については、「[Microsoft Intune ポータル サイト アプリを構成する方法](../apps/company-portal-app.md)」をご覧ください。

## <a name="whats-new-archive"></a>新機能の公開履歴
以前の月については、[新機能の公開履歴](whats-new-archive.md)を参照してください。

## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


