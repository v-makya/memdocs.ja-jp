---
title: Intune アプリ保護ポリシーの展開のトラブルシューティング方法
description: Intune アプリ保護ポリシーを展開するときに発生する可能性がある問題のトラブルシューティング方法について説明します。
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: troubleshooting
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 8443ca01a0ca1647e8069fdccf1d71aef74c23d8
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989473"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Intune におけるアプリ保護ポリシーの展開のトラブルシューティング

## <a name="introduction"></a>概要

この記事は、Microsoft Intune でアプリ保護ポリシーを適用する際の問題の理解とトラブルシューティングに役立ちます。 状況に当てはまるセクションに従います。

## <a name="basic-steps"></a>基本的な手順

### <a name="collect-initial-data"></a>初期データを収集する

トラブルシューティングを始める前に、いくつかの基本的な情報を収集して問題をよく理解し、解決策を見つけるための時間を短縮します。

次の情報を収集します。

- 適用されていないポリシー設定はどれですか? ポリシーは適用されていますか?
- ユーザー エクスペリエンスはいかがですか? ユーザーは対象となるアプリをインストールして起動しましたか?
- 問題が発生し始めたのはいつですか? アプリ保護は機能していますか?
- どのプラットフォーム (Android または iOS) に問題がありますか?
- 影響を受けているユーザーの数はどれくらいですか? 影響を受けているのはすべてのデバイスですか、一部のデバイスのみですか?
- 影響を受けているデバイスの数はどれくらいですか? 影響を受けているのはすべてのデバイスですか、一部のデバイスのみですか?
- Intune アプリ保護ポリシーにはモバイル デバイス管理 (MDM) サービスは必要ありませんが、Intune またはサード パーティの EMM を使用しているユーザーに影響がありますか?
- 影響を受けているのはすべてのマネージド アプリですか、特定のアプリのみですか? たとえば、[Intune App SDK](../developer/app-sdk-get-started.md) を使用する LOB アプリは影響を受けていて、ストア アプリには影響がありませんか?

これで、これらの質問に対する回答に基づいてトラブルシューティングを開始できます。

### <a name="verify-prerequisites"></a>前提条件を確認する

トラブルシューティングの次の手順では、すべての前提条件が満たされているかどうかを確認します。

MDM ソリューションに依存しない Intune アプリ保護ポリシーを使用することもできますが、次の前提条件を満たす必要があります。

- ユーザーには Intune のライセンスが割り当てられている必要があります。
- ユーザーは、アプリ保護ポリシーの対象となるセキュリティ グループに属している必要があります。 同一のアプリ保護ポリシーでは、使用中の特定のアプリを対象とする必要があります。
- Android デバイスでは、ポータル サイト アプリがアプリ保護ポリシーを受け取る必要があります。
- [Word、Excel、または PowerPoint](https://products.office.com/business/office) アプリを使用する場合は、次の追加要件が満たされている必要があります。
    - ユーザーに、自分の Azure Active Directory (Azure AD) アカウントにリンクされた [Microsoft 365 Apps for business または Microsoft 365 Apps for enterprise](https://products.office.com/business/compare-more-office-365-for-business-plans) のライセンスが必要です。 サブスクリプションには、モバイル デバイスの Office アプリが含まれている必要があります。また、[OneDrive for Business](https://onedrive.live.com/about/business/) のクラウド ストレージ アカウントを含めることも可能です。 Office 365 ライセンスは、[Microsoft 365 管理センター](https://admin.microsoft.com)で割り当てることができます。[こちらの手順](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc)に従ってください。
    - ユーザーは、詳細な **[名前を付けて保存]** 機能を使用して構成された管理対象の場所を持っている必要があります。 このコマンドは、 **[組織データのコピーを保存]** アプリケーション保護ポリシー設定の下にあります。 たとえば、管理対象の場所が OneDrive の場合、[OneDrive](https://onedrive.live.com/about/) アプリは、ユーザーの Word アプリ、Excel アプリ、または PowerPoint アプリ内で構成される必要があります。
    - 管理対象の場所が OneDrive の場合、アプリは、ユーザーに展開されているアプリの保護ポリシーの対象となる必要があります。

  > [!NOTE]
  > 現段階では、Office モバイル アプリは SharePoint Online のみをサポートし、オンプレミスの SharePoint はサポートされていません。

- Intune アプリ保護ポリシーをオンプレミスのリソース (Microsoft Skype for Business と Microsoft Exchange Server) と共に使用する場合は、[Skype for Business と Exchange に対してハイブリッド先進認証 (HMA)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) を有効にする必要があります。

Intune アプリ保護ポリシーでは、アプリケーションと [Intune App SDK](../developer/app-sdk-get-started.md) の間でユーザーの ID の一貫性が保たれていることが必要です。 この一貫性を保証する唯一の方法は、最新の認証を使用することです。 最新の認証を使用せずに、オンプレミスの構成でアプリが動作する可能性のあるシナリオがあります。 ただし、結果は一貫性がないか、保証されていません。

Skype for Business のハイブリッド構成とオンプレミス構成で HMA を有効にする方法の詳細については、次の記事を参照してください。

- **ハイブリッド**<br>
[SfB と Exchange のハイブリッドな最新認証が一般公開](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **オンプレミス**<br>
[AAD による SfB オンプレミスの最新認証](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>アプリ保護ポリシーの状態を確認する

アプリの保護状態を確認するには、次の手順に従います。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[モニター]**  >  **[アプリの保護状態]** を選択した後、 **[割り当てられたユーザー]** タイルを選択します。
3. **[アプリ レポート]** ページ上で、 **[ユーザーの選択]** を選択してユーザーとグループの一覧を表示させます。
4. 一覧から影響を受けているユーザーのいずれかを検索して選択し、 **[ユーザーの選択]** を選択します。 [アプリ レポート] ページの上部で、ユーザーがアプリ保護のライセンスを取得しているかどうか、O365 のライセンスを取得しているかどうかを確認できます。 また、すべてのユーザーのデバイスのアプリの状態を確認することもできます。
5. 対象となるアプリ、デバイスの種類、ポリシー、デバイスのチェックイン状態、最終同期時刻などの重要な情報をメモしておきます。

> [!NOTE]
> アプリ保護ポリシーは、アプリが作業コンテキストで使用されている場合にのみ適用されます。 たとえば、ユーザーが職場アカウントを使用してアプリにアクセスする場合です。

詳細については、「[Microsoft Intune でアプリ保護ポリシーの設定を検証する方法](../apps/app-protection-policies-validate.md)」を参照してください。

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>アプリと Intune App SDK の間でユーザー ID の一貫性があることを確認する

ほとんどのシナリオでは、ユーザーはユーザー プリンシパル名 (UPN) を使用してアカウントにログインします。 ただし、一部の環境 (オンプレミスのシナリオなど) では、ユーザーは他の形式のサインイン資格情報を使用する場合があります。 このような場合は、アプリで使用されている UPN が Azure AD の UPN オブジェクトと一致していないことがあります。 この問題が発生した場合、アプリ保護ポリシーは想定どおりに適用されません。

Microsoft の推奨するベスト プラクティスは、UPN をプライマリ SMTP アドレスと一致させることです。 これにより、ユーザーは一貫性のある ID を使用して、マネージド アプリ、Intune アプリ保護、およびその他の Azure AD リソースにログインできるようになります。 詳細については、[Azure AD UserPrincipalName の設定](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname)に関するページを参照してください。

環境に代替サインイン方法が必要な場合は、「[代替ログイン ID を構成する](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)」で、特に[代替 ID を使用したハイブリッド先進認証](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id)に関する説明を参照してください。

### <a name="verify-that-the-user-is-targeted"></a>ユーザーが対象になっていることを確認する

Intune アプリ保護ポリシーは、ユーザーを対象にする必要があります。 アプリ保護ポリシーをユーザーまたはユーザー グループに割り当てない場合、ポリシーは適用されません。

対象ユーザーにポリシーが適用されていることを確認するには、次の手順に従います。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[モニター]**  >  **[アプリの保護状態]** を選択し、(デバイス OS プラットフォームに基づいて) **[ユーザーの状態]** タイルを選択します。
表示される **[アプリ レポート]** ウィンドウで、 **[ユーザーの選択]** を選択してユーザーを検索します。
3. リストからユーザーを選択します。 そのユーザーの詳細を確認できます。

ポリシーをユーザー グループに割り当てるときは、そのユーザーがユーザー グループに含まれていることを確認します。 この操作を行うには、次の手順に従います。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[グループ] > [すべてのグループ]** を選択し、アプリ保護ポリシーの割り当てに使用するグループを検索して選択します。
3. **[管理]** セクションの **[メンバー]** を選択します。
4. 影響を受けるユーザーが一覧に表示されない場合は、[Azure Active Directory グループを使用してアプリとリソースのアクセスを管理する](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups)方法に関するページを参照し、グループ メンバーシップ規則を確認します。 影響を受けるユーザーがグループに含まれていることを確認します。
5. 影響を受けるユーザーが、ポリシーの除外対象グループのいずれにも含まれていないことを確認します。

> [!IMPORTANT]
> - Intune アプリ保護ポリシーは、デバイス グループではなく、ユーザー グループに割り当てる必要があります。
> - 影響を受けるデバイスが Apple Device Enrollment Program (DEP) を使用している場合は**ユーザー アフィニティ**が有効になっていることを確認します。 DEP でのユーザー認証を必要とするすべてのアプリにはユーザー アフィニティが必要です。
> - 影響を受けるデバイスが Android Enterprise を使用している場合は、仕事用プロファイルのみがアプリ保護ポリシーをサポートします。


### <a name="verify-that-the-managed-app-is-targeted"></a>マネージド アプリが対象になっていることを確認する

Intune アプリ保護ポリシーを構成する場合は、対象のアプリで [Intune App SDK](../developer/app-sdk-get-started.md) を使用する必要があります。 そうしないと、アプリ保護ポリシーが正しく機能しないことがあります。

対象のアプリが「[保護されている Microsoft Intune アプリ](../apps/apps-supported-intune-apps.md)」に一覧表示されていることを確認します。 LOB またはカスタム アプリの場合は、アプリで [Intune App SDK](../developer/app-sdk-get-started.md) の最新バージョンが使用されていることを確認します。 次の点に注意してください。

iOS では、各バージョンにこれらのポリシーの適用方法と機能に影響する修正プログラムが含まれているため、この方法が重要になります。 詳細については、[Intune App SDK iOS リリース](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases)に関するページを参照してください。
Android の場合、この方法はあまり重要ではありません。 ただし、ポータル サイト アプリはポリシー ブローカー エージェントとして機能するため、ユーザーにはポータル サイト アプリの最新バージョンがインストールされている必要があります。

> [!NOTE]
> 2019 年 9 月以降、Intune では Intune App SDK 8.1.1 以降のバージョンを使用する iOS アプリがサポートされるようになります。 8\.1.1 よりも前のバージョンの SDK を使用してビルドされたアプリはサポートされなくなります。 

## <a name="more-information"></a>説明

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Intune MDM のマネージド デバイスの特別な要件

アプリ保護ポリシーを作成するときは、すべてのアプリの種類または次のアプリの種類を対象にすることができます。

- アンマネージド デバイス上のアプリ
- Intune マネージド デバイス上のアプリ
- Android 作業プロファイルでのアプリ

> [!NOTE] 
> アプリの種類を指定するには、 **[すべてのアプリの種類を対象にする]** を **[いいえ]** に設定し、 **[アプリの種類]** 一覧から選択します。

iOS の場合、アプリ保護ポリシー (APP) 設定のターゲットを Intune に登録されているデバイス上のアプリにするには、さらに[アプリの構成設定](../apps/app-configuration-policies-use-ios.md)が必要になります。

- **IntuneMAMUPN** を、すべての MDM (Intune またはサード パーティの EMM) マネージド アプリケーションに構成する必要があります。 詳細については、「Microsoft Intune またはサード パーティ EMM のユーザー UPN 設定を構成する」を参照してください。
- すべてのサード パーティ製アプリケーションと LOB MDM マネージド アプリケーションに **IntuneMAMDeviceID** を構成する必要があります。
- **IntuneMAMDeviceID** を、デバイスの ID トークンとして構成する必要があります。 たとえば、key=IntuneMAMDeviceID, value={{deviceID}} のようにします。 詳細については、「[管理対象の iOS デバイス用アプリ構成ポリシーを追加する](../apps/app-configuration-policies-use-ios.md)」を参照してください。
- **IntuneMAMDeviceID** 値のみが構成されている場合、Intune APP はデバイスが管理対象であると見なしません。

### <a name="scenario-policy-changes-are-not-working"></a>シナリオ:ポリシーの変更が行われない
[Intune App SDK](../developer/app-sdk-get-started.md) はポリシーの変更を定期的に確認します。 ただし、次のいずれかの理由により、このプロセスが遅れている可能性があります。

- アプリがサービスでチェックインされていません。
- デバイスから Intune ポータル サイト アプリが削除されています。

Intune アプリ保護ポリシーは、ユーザー ID に依存します。 そのため、職場または学校アカウントを使用したアプリへの有効なログインと、サービスへの一貫性のある接続が必要です。 ユーザーがアプリにサインインしていない場合、または Intune ポータル サイト アプリがデバイスから削除されている場合、ポリシーの更新は適用されません。

また、アプリ保護ポリシーの変更および更新が適用されるまで、最大 8 時間かかります。 該当する場合は、すべてのアプリを終了し、デバイスを再起動すると、通常はすぐにポリシーの更新が強制的に適用されます。

アプリの保護状態を確認するには、次の手順に従います。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[モニター]**  >  **[アプリの保護状態]** を選択した後、 **[割り当てられたユーザー]** タイルを選択します。
3. [アプリ レポート] ページ上で、 **[ユーザーの選択]** を選択してユーザーとグループの一覧を開きます。
4. 一覧から影響を受けているユーザーのいずれかを検索して選択し、 **[ユーザーの選択]** を選択します。
5. 現在適用されているポリシー (状態と最終同期時刻を含む) を確認します。
6. 状態が **[チェックインされていません]** である場合、または最近の同期が行われていないことが示されている場合は、ユーザーに一貫性のあるネットワーク接続があるかどうかを確認します。 Android ユーザーの場合は、ポータル サイト アプリの最新バージョンがインストールされていることを確認します。

> [!IMPORTANT]
> [Intune App SDK](../developer/app-sdk-get-started.md) は、選択的ワイプを 30 分ごとにチェックします。 ただし、既にサインインしているユーザーの既存ポリシーに対する変更は、最大 8 時間表示されない場合があります。 このプロセスを高速化するには、ユーザーにアプリからログアウトして再度ログオンしてもらうか、デバイスを再起動してもらいます。

Intune アプリ保護ポリシーには、複数 ID のサポートが含まれています。 Intune でアプリ保護ポリシーを適用できるのは、アプリにサインインしている職場または学校アカウントのみです。 ただし、デバイスごとに 1 つの職場または学校アカウントのみがサポートされています。

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>シナリオ:ポリシーは適用されるが、iOS ユーザーは引き続き作業ファイルをアンマネージド アプリに転送できる
iOS デバイスの **Open In Management** (![Open In ボタン](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg)) 機能を使用すると、MDM チャネルを使用して展開されているアプリ間でのみファイル転送が行われるよう制限できます。 ユーザーは、構成に応じて、OneDrive や Exchange などの管理対象の場所からアンマネージドのアプリや場所に作業ファイルを転送できる場合があります。 iOS の **Open In Management** 機能は、他のデータ転送方法の外部で動作します。 そのため、 **[名前を付けて保存]** 設定や**コピー/貼り付け**設定の影響は受けません。

Intune アプリ保護ポリシーを iOS の **Open In Management** 機能と共に使用して、以下のように会社データを保護できます。

- **MDM ソリューションで管理されていない従業員所有のデバイス**:アプリ保護ポリシー設定を **[Allow app to transfer data to only Policy Managed apps]\(アプリでポリシー管理型アプリへのデータ転送のみ許可する\)** に設定できます。 この方法で構成すると、ポリシー マネージド アプリで **Open-In** 動作を行うと、その他のポリシー マネージド アプリのみが共有対象のオプションとして表示されます。 たとえば、ネイティブ メール アプリで、ユーザーが OneDrive から保護ファイルを添付ファイルとして送信すると、そのファイルは読み取り不能になります。

- **MDM ソリューションによって管理されるデバイス**:Intune またはサード パーティの MDM ソリューションに登録されているデバイスでは、アプリと、アプリ保護ポリシーおよび MDM を通して展開される他のマネージド iOS アプリの間でのデータ共有は、Intune アプリおよび iOS の **Open in management** 機能によって制御されます。<br/><br/>
MDM ソリューションを使用して展開するアプリを、Intune アプリ保護ポリシーとも関連付けるには、[ユーザー UPN 設定の構成](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm)に関する説明に従って、ユーザー UPN 設定を構成します。<br/><br/>他のアプリへのデータ転送を許可する方法を指定するには、 **[他のアプリに組織データを送信]** を有効にして、希望する共有レベルを選択します。<br/><br/>アプリで他のアプリからのデータの受信を許可する方法を指定するには、 **[他のアプリからデータを受信]** を有効にして、希望するデータ受信レベルを選択します。

アプリ データの受信と共有の詳細については、[データ再配置の設定](../apps/app-protection-policy-settings-ios.md#data-protection)に関するページを参照してください。

詳細については、「[Microsoft Intune で iOS アプリ間のデータ転送を管理する方法](../apps/data-transfer-between-apps-manage-ios.md)」を参照してください。

## <a name="references"></a>参考資料

それでも関連する問題の解決策を探している場合、または Intune の詳細については、[Microsoft Intune フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)に質問を投稿してください。 多くのサポート エンジニア、MVP、開発チーム メンバーがフォーラムにアクセスします。 そのため、必要な情報を持っている人が見つかる可能性が高くなります。

Microsoft Intune 製品サポート チームのサポートを依頼するには、「[Microsoft Intune のサポートを受ける方法](../fundamentals/get-support.md)」を参照してください。

Intune アプリ保護ポリシーの詳細については、次の記事を参照してください。

- [モバイル アプリケーション管理に関するトラブルシューティング](../apps/troubleshoot-mam.md)
- [MAM とアプリの保護に関してよく寄せられる質問](../apps/mam-faq.md)
- [サポートのヒント:ローカル デバイスのログ ファイルを使用した Intune アプリ保護ポリシーのトラブルシューティング](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

最新のニュース、情報、技術のヒントのすべてについては、次の公式ブログを参照してください。

- [Microsoft Intune サポート チームのブログ](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Microsoft Enterprise Mobility and Security のブログ](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>次のステップ

- Intune のトラブルシューティングに関する追加情報については、「[トラブルシューティング ポータルを使用して社内のユーザーをサポートする](../fundamentals/help-desk-operators.md)」をご覧ください。 
- Microsoft Intune の既知の問題について学習します。 詳細については、[Intune のお客様の成功事例](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)に関するページを参照してください。
- さらに支援が必要ですか? 「[Microsoft Intune のサポートを受ける方法](../fundamentals/get-support.md)」を参照してください。
