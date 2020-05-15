---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7827c85585d630f64ba9c6d342b6275fca506b1d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906970"
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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Mac 用ポータル サイトでの複数アカウントのサポート<!-- 5779449  -->
macOS デバイスのポータル サイトでユーザー アカウントがキャッシュされるようになり、サインインがより簡単になりました。 ユーザーは、アプリケーションを起動するたびにポータル サイトにサインインする必要がなくなりました。 また、複数のユーザー アカウントがキャッシュされている場合、ポータル サイトにアカウント ピッカーが表示されるため、ユーザーは自分のユーザー名を入力する必要がありません。 

### <a name="auto-update-vpp-available-apps---3640511----"></a>VPP の利用可能なアプリの自動更新<!-- 3640511  -->
Volume Purchase Program (VPP) の利用可能なアプリとして公開されるアプリは、VPP トークンに対して**アプリの自動更新**が有効になっている場合、自動的に更新されるようになります。 現在、VPP の利用可能なアプリは自動的に更新されません。 代わりに、エンドユーザーはポータル サイトに移動し、新しいバージョンが利用可能な場合はアプリを再インストールする必要があります。 しかし、現在、必須アプリでは自動更新がサポートされています。

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>ポータル サイトでセルフサービス デバイス アクションをカスタマイズする<!--4393379  -->
エンドユーザーに表示される利用可能なセルフサービス デバイス アクションを、ポータル サイト アプリと Web サイトでカスタマイズできるようになります。 意図しないデバイス アクションを防ぐのに役立つように、ポータル サイト アプリに対してこれらの設定を構成できるようになります。そのためには、 **[テナント管理]**  >  **[カスタマイズ]**  >  **[作成]**  >  **[機能を非表示にする]** の順に選択します。 次の操作を実行できます。
- 会社の Windows デバイスで **[削除]** ボタンを非表示にする。
- 会社の Windows デバイスで **[リセット]** ボタンを非表示にする。
- 会社の iOS デバイスで **[リセット]** ボタンを非表示にする。
- 会社の iOS デバイスで **[削除]** ボタンを非表示にする。

詳細については、「[ポータル サイトからのユーザーによるセルフサービス デバイス アクション](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal)」を参照してください。

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>ポータル サイトでの Azure AD Enterprise または Office Online アプリケーションの統合配信<!--4404429 -->
ポータル サイトでの Azure AD Enterprise または Office Online アプリケーションの表示 ( **[非表示]** または **[表示]** ) の切り替えが可能になります。 各ユーザーには、選択された Microsoft サービスからのアプリケーション カタログ全体が表示されます。 既定では、追加のアプリ ソースがそれぞれ **[非表示]** に設定されるようになります。 この機能は、まず、2005 リリースのポータル Web サイトで有効になり、Windows、iOS と iPadOS、および macOS ポータル サイトでサポートされる予定です。 この今後の設定を見つけるには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[テナント管理]**  >  **[カスタマイズ]** の順に選択します。 関連情報については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」を参照してください。

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>ポータル サイトから Intune ドキュメントを検索する<!-- 1736480 -->
macOS アプリ用のポータル サイトから、Intune のドキュメントを直接検索できるようになりました。 メニュー バーで、 **[ヘルプ]**  >  **[検索]** の順に選択し、検索キー ワードを入力すれば、質問に対する回答がすばやく見つかります。

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Android 用ポータル サイトで仕事用プロファイルの登録後にアプリを取得する方法がユーザーに示されるようになる <!-- 6103999  -->
ユーザーがアプリをより簡単に見つけてインストールできるように、ポータル サイトのアプリ内ガイダンスを改善しています。  仕事用プロファイルの管理に登録した後、バッジ付きバージョンの Google Play で推奨されるアプリを見つけられることを示すメッセージがユーザーに表示されます。 また、ユーザーには、左側のポータル サイト ドロアーで新しい **[アプリの取得]** リンクが表示されます。 これらの新規および改善されたエクスペリエンスの場所を空けるために、 **[アプリ]** タブが削除されます。 

### <a name="android-company-portal-user-experience---5736084---"></a>Android ポータル サイトのユーザー エクスペリエンス<!-- 5736084 -->
2005 リリースの Android ポータル サイトでは、アプリ保護ポリシーによって警告、ブロック、またはワイプが発行された Android デバイスのエンドユーザーに、新しいユーザー エクスペリエンスが表示されるようになります。 現在のダイアログ エクスペリエンスの代わりに、エンドユーザーには、警告、ブロック、またはワイプの理由、および問題を修正するための手順を説明するメッセージがページ全体に表示されます。 詳細については、「[Android デバイスでのアプリ保護のエクスペリエンス](../apps/app-protection-policy.md#app-protection-experience-for-android-devices)」と「[Microsoft Intune の Android アプリ保護ポリシー設定](../apps/app-protection-policy-settings-android.md)」を参照してください。


<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

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

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>macOS デバイスでシステム拡張機能を構成する<!-- 6255624  -->
macOS デバイスでは、カーネル レベルで設定を構成するためのカーネル拡張機能プロファイルを作成することができます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[macOS]** (プラットフォーム) > **[カーネル拡張機能]** (プロファイル))。 Apple では、最終的にカーネル拡張機能を非推奨とし、今後のリリースでシステム拡張機能に置き換える予定です。 システム拡張機能はユーザー領域で実行され、カーネルへのアクセス権は付与されません。 目標は、カーネル レベルでの攻撃を制限しながら、セキュリティを強化し、さらにエンド ユーザー制御を提供することです。 カーネル拡張機能とシステム拡張機能の両方で、ユーザーは、オペレーティング システムのネイティブ機能を拡張するアプリ拡張機能をインストールできます。

Intune では、カーネル拡張機能とシステム拡張機能の両方を構成できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[macOS]** (プラットフォーム) > **[システム拡張機能]** (プロファイル))。 カーネル拡張機能は 10.13.2 以降に適用されます。 システム拡張機能は 10.15 以降に適用されます。 macOS 10.15 から macOS 10.15.4 では、カーネル拡張機能とシステム拡張機能を並行して実行できます。 

macOS デバイスのカーネル拡張機能の詳細については、[macOS カーネル拡張機能の追加](../configuration/kernel-extensions-overview-macos.md)に関するページを参照してください。

適用対象:
- macOS 10.15 以降

<!-- ***********************************************-->
## <a name="device-enrollment"></a>デバイスの登録

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>個人所有デバイスでは、VPN を使用して展開できる<!--5015344 -->
この機能は延期される可能性があります。

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>自動デバイス同期間隔を 12 時間に短縮<!--3077535 -->
Apple の自動デバイス登録では、Intune と Apple Business Manager の自動デバイス同期間隔が 24 時間から 12 時間に短縮されます。 同期の詳細については、「[マネージド デバイスを同期する](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices)」を参照してください。

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Hololens 2 デバイスの Autopilot サポート<!--6305220-->
Windows Autopilot では、Hololens 2 デバイスがサポートされるようになります。 Intune での Autopilot の使用について詳しくは、「[Windows Autopilot を使用して Intune に Windows デバイスを登録する](../enrollment/enrollment-autopilot.md)」を参照してください。

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>登録制限でスコープ タグがサポートされるようになる<!--4209550 -->
登録制限にスコープ タグを割り当てられるようになります。 そのためには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[登録制限]**  >  **[制限の作成]** の順に移動します。 いずれかの種類の制限を作成すると、 **[スコープ タグ]** ページが表示されます。

### <a name="shared-ipads-for-business--6367326---"></a>法人向け共有 iPad<!--6367326 -->
Intune と Apple Business Manager を使用して、複数の従業員がデバイスを共有できるように共有 iPad を簡単かつ安全に設定できるようになります。 Apple の [共有 iPad](https://developer.apple.com/education/shared-ipad/) では、ユーザー データを保持しながら、複数のユーザーに対してパーソナライズされたエクスペリエンスが提供されます。 ユーザーは、管理対象 Apple ID を使用して、組織内の共有 iPad にサインインした後、アプリ、データ、設定にアクセスできます。 共有 iPad はフェデレーション ID と連動します。

この機能を表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** の順に移動し、トークンを選択して**、 **[プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS]** の順に移動します。 **[管理の設定]** ページで、 **[ユーザー アフィニティを使用しないで登録する]** を選択すると、 **[共有 iPad]** オプションが表示されます。

**適用対象:** iPadOS 13.4 以降。 このリリースでは、ユーザーが管理対象 Apple ID を使用せずにデバイスにアクセスできるように、共有 iPad での一時的なセッションのサポートが追加されました。 ログアウト時に、デバイスではすべてのユーザー データが消去されるため、デバイスをすぐに使用できる状態になり、デバイスのワイプは不要になります。 

<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics には、デバイスの詳細ログが含まれる<!--6014987  -->
Intune デバイスの詳細ログは、 **[レポート]**  >  **[ログ分析]** で入手できます。 デバイスの詳細を相互に関連付けて、カスタム クエリと Azure ブックを作成することができます。


### <a name="macos-script-support---6376978----"></a>macOS のスクリプト サポート<!-- 6376978  -->
macOS のスクリプト サポートが一般公開されるようになりました。 さらに、Apple の自動デバイス登録 (旧称: Device Enrollment Program) に登録されているユーザー割り当てスクリプトと macOS デバイスの両方のサポートを追加する予定です。 詳細については、「[Intune で macOS デバイスに対してシェル スクリプトを使用する](../apps/macos-shell-scripts.md)」を参照してください。

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
## <a name="security"></a>セキュリティ

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Android デバイスでの DISA Purebred の派生資格情報のサポート<!--4839592 -->
Android Enterprise フル マネージド デバイスで、*DISA Purebred* を[派生資格情報](../protect/derived-credentials.md)プロバイダーとして使用できます ( **[テナント管理]**  >  **[コネクタとトークン]**  >  **[派生資格情報]** )。 DISA Purebred の派生資格情報を取得するためのサポートが追加されます。 アプリ認証、Wi-Fi、VPN、または S/MIME 署名や、それをサポートするアプリでの暗号化に、派生資格情報を使用できるようになります。 

4 月に、Intune では、派生資格情報のプロバイダーとして *Entrust Datacard* および *Intercede* のサポートが追加されました。 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>macOS デバイス用のプライバシーの基本設定<!-- 2934232 --> 
macOS Catalina 10.15 のリリースでは、Apple によって新しいセキュリティとプライバシーの強化が加えられました。 既定では、アプリケーションとプロセスで、ユーザーの同意なしで特定のデータにアクセスすることはできません。 ユーザーが同意しない場合、アプリケーションとプロセスが機能しなくなる可能性があります。 Intune では、macOS 10.14 以降を実行しているデバイスでエンドユーザーに代わって、IT 管理者がデータ アクセスの同意を許可または許可しないようにできる設定のサポートを追加しています。 これらの設定により、アプリケーションとプロセスは引き続き正常に機能し、エンドユーザーに示されるプロンプトの数が減ります。


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>エンドポイント セキュリティでポリシーを複製する<!-- 5892558   -->
Microsoft Endpoint Manager admin center のエンドポイント セキュリティ ノードで作成したポリシーを選択し、複製してコピーを作成できるようになります。  複製できるようになるポリシーには、以下について作成するものが含まれます。 

- ウイルス対策
- ディスクの暗号化
- ファイアウォール
- エンドポイントの検出と応答
- 攻撃の回避
- アカウント保護

複製によって元のポリシーのコピーが作成されます。その後、名前を変更して編集することができます。 コピーには元の割り当ては含まれません。

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>コンプライアンス違反に対するアクションとしてプッシュ通知を送信する <!-- 1733150   -->
iOS および Android プラットフォームについては、ポータル サイト アプリを通じてアプリのプッシュ通知を送信する、コンプライアンス違反に対する新しいアクションを追加しています。 ユーザーが通知をクリックすると、ポータル サイト アプリが起動し、それがコンプライアンス違反である理由が表示されます。 管理者は、Microsoft Endpoint Manager admin center で、コンプライアンス違反に対してこの新しいアクションを構成できます。これには、 **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシーの作成]** の順に移動して、 *[アクション]* を選択してアプリのプッシュ通知を送信します。 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>エンドポイント セキュリティ ファイアウォール ポリシーの新しいプロファイル<!-- 5653324   -->
プレビューとして、Intune のエンドポイント セキュリティのファイアウォール ポリシーに、Windows 10 以降用のプロファイルをさらに追加しています ( **[エンドポイント セキュリティ]**  >  **[ファイアウォール]**  >  **[ポリシーの作成]** > **[Windows 10 以降]** を選択)。 

この新しいプロファイルの各インスタンスでは、最大 150 のカスタム "*Microsoft Defender ファイアウォール規則*" がサポートされます。 Microsoft Defender ファイアウォール規則プロファイルを使用すると、Windows 10 のポートとアプリケーションを許可またはブロックするための詳細な Windows ファイアウォール規則を定義できます。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。



