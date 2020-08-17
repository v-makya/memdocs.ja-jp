---
title: Intune を使用して iOS および Android 用の Edge を管理する
titleSuffix: ''
description: iOS および Android 用の Edge で Intune アプリ保護および構成ポリシーを使用して、企業の Web サイトが確実に保護機能付きで常にアクセスされるようにすることができます。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/05/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49d731ef6e9508367ded8ed5d711b744be7d2db1
ms.sourcegitcommit: 4f10625e8d12aec294067a1d9138cbce19707560
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87912543"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>iOS および Android 用の Edge と Microsoft Intune を使用して Web アクセスを管理する

iOS および Android 用の Edge は、ユーザーが Web を閲覧できるように設計されており、複数の ID をサポートしています。 ユーザーは、閲覧用に、職場アカウントだけでなく個人アカウントも追加できます。 これら 2 つの ID は完全に分離されています。これは、他の Microsoft モバイル アプリで提供されている機能と同様です。

iOS 用の Edge は、iOS 12.0 以降でサポートされています。 Android 用の Edge は、Android 5 以降でサポートされています。

> [!NOTE]
> iOS および Android 用の Edge では、ユーザーが自分のデバイス上でネイティブ ブラウザーに対して行った設定は使用されません。これは、iOS および Android 用の Edge でこれらの設定にアクセスできないためです。

Office 365 データの豊富で広範な保護機能は、Enterprise Mobility + Security スイートにサブスクライブすると利用できます。これには、条件付きアクセスなどの Microsoft Intune と Azure Active Directory Premium の機能が含まれます。 少なくとも、モバイル デバイスから iOS および Android 用の Edge への接続のみを許可する条件付きアクセス ポリシーと、閲覧エクスペリエンスが保護される Intune アプリ保護ポリシーを展開することをお勧めします。

> [!NOTE]
> 保護されたブラウザーで開く必要がある場合、iOS デバイス上の新しい Web クリップ (ピン留めされた Web アプリ) は、Intune Managed Browser ではなく iOS および Android 用の Edge で開かれます。 以前の iOS Web クリップの場合は、これらの Web クリップのターゲットを再設定して、Managed Browser ではなく iOS および Android 用の Edge で開くようにする必要があります。

## <a name="apply-conditional-access"></a>条件付きアクセスを適用する
組織は Azure AD 条件付きアクセス ポリシーを使用して、ユーザーが iOS および Android 用の Edge を使用して職場または学校のコンテンツにのみアクセスできるようにすることができます。 これを行うには、可能性のあるすべてのユーザーを対象とする条件付きアクセス ポリシーが必要です。 このポリシーの作成の詳細については、[条件付きアクセスを使用してクラウド アプリへのアクセスにアプリ保護ポリシーを要求する方法](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access)に関するページを参照してください。

1. [シナリオ 2:ブラウザー アプリとしてアプリ保護ポリシーが適用された承認済みアプリを要求する方法](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies)の説明に従い、iOS および Android 用の Edge が Office 365 エンドポイントに接続することを許可し、他のモバイル デバイス Web ブラウザーはブロックします。

   >[!NOTE]
   > このポリシーにより、モバイル ユーザーは、iOS および Android 用の Edge 内からすべての Office 365 エンドポイントにアクセスできるようになります。 また、このポリシーは、ユーザーが InPrivate を使用して Office 365 エンドポイントにアクセスできないようにします。

条件付きアクセスを使用すると、[Azure AD アプリケーション プロキシ](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)経由で外部ユーザーに公開したオンプレミス サイトを対象にすることもできます。

## <a name="create-intune-app-protection-policies"></a>Intune のアプリ保護ポリシーを作成する

アプリ保護ポリシー (APP) では、組織データの使用を許可されるアプリとそのデータに対して実行できる操作を定義します。 APP で利用できる選択肢を使用することで、組織は固有のニーズに合わせて保護を調整できます。 場合によっては、完全なシナリオを実装するためにどのポリシー設定が必要であるかが明確ではないことがあります。 組織がモバイル クライアント エンドポイントのセキュリティ強化を優先できるよう、Microsoft では、iOS および Android モバイル アプリ管理のための APP データ保護フレームワークの分類を導入しました。

APP データ保護フレームワークは 3 つの異なる構成レベルに編成されており、各レベルは前のレベルを基に構築されています。

- **エンタープライズ基本データ保護** (レベル 1) では、アプリが PIN で保護され、暗号化されており、選択的ワイプ操作を実行できるようにします。 Android デバイスの場合、このレベルでは Android デバイスの構成証明を検証します。 これは、Exchange Online メールボックス ポリシーに類似したデータ保護制御を提供し、IT 部門およびユーザー集団に APP を経験させる、エントリ レベルの構成です。
- **エンタープライズ拡張データ保護** (レベル 2) では、APP データ漏えい防止メカニズムと OS の最小要件が導入されています。 この構成は、職場または学校のデータにアクセスするほとんどのモバイル ユーザーに適用されます。
- **エンタープライズ高度データ保護** (レベル 3) では、高度なデータ保護メカニズム、強化された PIN の構成、および APP Mobile Threat Defense が導入されています。 この構成は、危険度の高いデータにアクセスするユーザーに適しています。

各構成レベルおよび、最低限保護する必要のあるアプリに関する具体的な推奨事項については、「[アプリ保護ポリシーを使用するデータ保護フレームワーク](app-protection-framework.md)」を参照してください。

デバイスが統合エンドポイント管理 (UEM) ソリューションに登録されているかどうかに関係なく、「[アプリ保護ポリシーを作成して割り当てる方法](app-protection-policies.md)」の手順を使用して、iOS アプリと Android アプリの両方に対して Intune アプリ保護ポリシーを作成する必要があります。 これらのポリシーは、少なくとも次の条件を満たしている必要があります。

1. Microsoft Edge、Outlook、OneDrive、Office、Teams など、すべての Microsoft 365 モバイル アプリケーションを含める。これにより、ユーザーは Microsoft アプリ内の職場または学校のデータに対し、セキュリティで保護された方法でアクセスして操作できることが保証されます。

2. すべてのユーザーに割り当てられている。 これにより、iOS および Android 用の Edge のどちらを使用しているかに関係なく、すべてのユーザーが確実に保護されます。

3. 要件を満たすフレームワーク レベルを決定する。 ほとんどの組織では、データ保護とアクセス要件の制御を可能にするために、**エンタープライズ拡張データ保護** (レベル 2) に定義されている設定を実装する必要があります。

利用可能な設定について詳しくは、「[Android アプリ保護ポリシー設定](app-protection-policy-settings-android.md)」と「[iOS アプリ保護ポリシー設定](app-protection-policy-settings-ios.md)」をご覧ください。

> [!IMPORTANT]
> Intune に登録されていない Android デバイス上のアプリに対して Intune アプリ保護ポリシーを適用するには、ユーザーが Intune ポータル サイトもインストールする必要があります。 詳しくは、「[アプリ保護ポリシーを使用して Android アプリを管理するときの注意点](../fundamentals/end-user-mam-apps-android.md)」を参照してください。

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>ポリシーで保護されたブラウザーでの Azure AD に接続されている Web アプリへのシングル サインオン

iOS および Android 用の Edge では、Azure AD に接続されているすべての Web アプリ (SaaS およびオンプレミス) へのシングル サインオン (SSO) を利用できます。 SSO では、ユーザーは資格情報を再入力しなくても、iOS および Android 用の Edge を介して Azure AD に接続されている Web アプリにアクセスできます。

SSO では、iOS デバイス用の Microsoft Authenticator アプリ、または Android 上の Intune ポータル サイトで、ご利用のデバイスを登録する必要があります。 これらのいずれかを利用している場合、ポリシーで保護されているブラウザーで Azure AD に接続された Web アプリにアクセスすると、デバイスの登録を求められます (これは、デバイスがまだ登録されていない場合のみ該当します)。 Intune で管理されているユーザーのアカウントでデバイスが登録されると、そのアカウントでは Azure AD に接続されている Web アプリに対する SSO が有効になります。

> [!NOTE]
> デバイスの登録は、Azure AD サービスによる単純なチェックインです。 デバイスを完全に登録する必要はなく、デバイスに対する追加の権限が IT に与えられることもありません。

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>アプリ構成を利用して閲覧エクスペリエンスを管理する

iOS および Android 用の Edge は、Microsoft Endpoint Manager などの統合エンドポイント管理の管理者によってアプリの動作をカスタマイズできるようにするアプリ設定をサポートしています。

アプリ構成を配信するには、登録済みデバイスのモバイル デバイス管理 (MDM) OS チャネル (iOS 用の[マネージド アプリ構成](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html)チャネルまたは Android 用の [Android in the Enterprise](https://developer.android.com/work/managed-configurations) チャネル) を使用するか、または Intune アプリ保護ポリシー (APP) チャネルを使用します。 iOS および Android 用の Edge では、次の構成シナリオがサポートされています。

- 職場または学校アカウントのみ許可
- 一般的なアプリ構成設定
- データ保護設定

> [!IMPORTANT]
> Android でデバイスを登録する必要がある構成シナリオでは、デバイスを Android Enterprise に登録し、Android 用の Edge をマネージド Google Play ストアを使用して展開する必要があります。 詳しくは、「[Android Enterprise 仕事用プロファイル デバイスの登録を設定する](../enrollment/android-work-profile-enroll.md)」および「[マネージド Android Enterprise デバイス用にアプリ構成ポリシーを追加する](app-configuration-policies-use-android.md)」を参照してください。

各構成シナリオでは、固有の要件に焦点を当てています。 たとえば、構成シナリオにデバイスの登録が必要であるために UEM プロバイダーで動作するか、Intune アプリ保護ポリシーが必要かどうかを示します。

> [!NOTE]
> Microsoft Endpoint Manager を使用すると、MDM OS チャネルを介して配信されるアプリ構成は、**マネージド デバイス** アプリ構成ポリシー (ACP) と呼ばれます。アプリ保護ポリシー チャネルを介して配信されるアプリ構成は、**マネージド アプリ**のアプリ構成ポリシーと呼ばれます。

## <a name="only-allow-work-or-school-accounts"></a>職場または学校アカウントのみ許可

最大規模で規制の厳しいお客様のデータのセキュリティとコンプライアンス ポリシーを尊重することは、Microsoft 365 の価値の重要な柱です。 企業によっては、企業環境内のすべての通信情報をキャプチャし、デバイスが企業の通信にのみ使用されるようにする必要があります。 これらの要件をサポートするために、アプリ内で 1 つの企業アカウントのみをプロビジョニングできるように登録済みデバイスの iOS および Android 用の Edge を構成することができます。

組織の許可されたアカウント モード設定の構成については、以下を参照してください。

- [Android の設定](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS の設定](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

この構成シナリオは、登録済みデバイスでのみ機能します。 ただし、UEM プロバイダーはすべてサポートされています。 Microsoft Endpoint Manager を使用していない場合は、これらの構成キーの展開方法について UEM のドキュメントを参照する必要があります。

## <a name="general-app-configuration-scenarios"></a>一般的なアプリ構成シナリオ

iOS および Android 用の Edge では、管理者は、いくつかのアプリ内設定について既定の構成をカスタマイズできます。 この機能は、現在、iOS および Android の Edge で、アプリにサインインしている職場または学校のアカウントに Intune App Protection ポリシーが適用されていて、ポリシー設定がマネージド アプリのアプリ構成ポリシーを介して配信されている場合にのみ提供されます。

> [!IMPORTANT]
> Android 用の Edge では、マネージド Google Play で使用できる Chromium 設定がサポートされていません。

Edge では、次の構成設定がサポートされています。

- 新しいタブ ページのエクスペリエンス
- ブックマークのエクスペリエンス
- アプリの動作のエクスペリエンス
- キオスク モードのエクスペリエンス

これらの設定は、デバイスの登録ステータスに関係なくアプリに展開できます。

### <a name="new-tab-page-experiences"></a>新しいタブ ページのエクスペリエンス

iOS および Android 用の Edge には、新しいタブ ページのエクスペリエンスを調整する複数のオプションが用意されています。

#### <a name="organization-logo-and-brand-color"></a>組織のロゴとブランドの色

これらの設定を使用すると、iOS および Android 用の Edge の新しいタブ ページをカスタマイズして、組織のロゴとブランドの色をページの背景として表示することができます。

組織のロゴと色をアップロードするには、まず、次の手順を実行します。
1. [Microsoft Endpoint Manager](https://endpoint.microsoft.com) 内で、 **[テナント管理]**  ->  **[カスタマイズ]**  ->  **[Company Identity Branding]\(会社 ID のブランド化\)** に移動します。
2. ブランドのロゴを設定するには、 **[ヘッダーに表示]** の横にある [組織のロゴのみ] を選択します。 背景が透明なロゴをお勧めします。
3. ブランドの背景色を設定するには、 **[テーマの色]** を選択します。 iOS および Android 用の Edge では、新しいタブ ページ上に明るい色の網掛けが適用され、ページの読みやすさが向上しています。

次に、以下のキーと値のペアを使用して、組織のブランドを iOS および Android 用の Edge にプルします。

|    キー    |    値    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    **true** を設定すると、組織のブランド ロゴを表示します<br>**false** (既定値) を設定すると、ロゴが表示されません    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    **true** を設定すると、組織のブランドの色を表示します<br>**false** (既定値) を設定すると、色が表示されません    |

#### <a name="homepage-shortcut"></a>ホームページ ショートカット

この設定では、iOS および Android 用の Edge のホーム ページ ショートカットを構成することができます。 構成したホーム ページ ショートカットは、ユーザーが iOS および Android 用の Edge で新しいタブを開くと、検索バーの下に最初のアイコンとして表示されます。 ユーザーは、自分で管理しているコンテキストで、このショートカットを編集したり削除したりすることはできません。 ホーム ページ ショートカットには、区別のために組織の名前が表示されます。 

|    キー    |    値    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    有効な URL を指定します。 セキュリティ対策のため、誤った URL はブロックされます。<br>例: `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>複数のトップ サイト ショートカット

ホームページのショートカットを構成するのと同様に、iOS および Android 用の Edge の新しいタブ ページで、複数のトップ サイト ショートカットを構成できます。 ユーザーは、管理しているコンテキストで、これらのショートカットを編集したり削除したりすることはできません。 注: ホームページのショートカットを含めて、全部で 8 個のショートカットを構成できます。 ホームページのショートカットを構成した場合、構成されている最初の最上位サイトがそれによってオーバーライドされます。 

|    キー    |    値    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    値の URL のセットを指定します。 各トップ サイト ショートカットは、タイトルと URL で構成されます。 タイトルと URL は、`|` 文字で区切ります。<br>例: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>業界ニュース

iOS および Android 用の Edge 内の新しいタブ ページ エクスペリエンスを構成して、組織に関連する業界のニュースを表示できます。 この機能を有効にすると、iOS および Android 用の Edge では、組織のドメイン名を使用して、組織、組織の業界、および競合他社に関するニュースが Web から集約されるので、ユーザーは iOS および Android 用の Edge の新しいタブ ページだけですべての関連する外部ニュースを検索できます。 業界ニュースは、既定では無効になっています。 

|    キー    |    値    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **true** を設定すると、新しいタブ ページに業界ニュースを表示します<br>**false** (既定値) を設定すると、新しいタブ ページに業界ニュースが表示されません    |

### <a name="bookmark-experiences"></a>ブックマークのエクスペリエンス

iOS および Android 用の Edge には、ブックマークを管理する複数のオプションが用意されています。

#### <a name="managed-bookmarks"></a>マネージド ブックマーク

アクセスしやすくするため、ユーザーが iOS および Android 用の Edge を使用するときに利用できるようにしたいブックマークを構成できます。

- ブックマークは職場または学校アカウントにのみ表示され、個人のアカウントには公開されません。
- ブックマークを、ユーザーが削除したり、変更したりすることはできません。
- ブックマークは、リストの上部に表示されます。 ユーザーが作成したブックマークは、これらのブックマークの下に表示されます。
- アプリケーション プロキシのリダイレクトを有効にしてある場合は、内部 URL または外部 URL を使ってアプリケーション プロキシ Web アプリを追加できます。
- リストに入力するときは、すべての URL の先頭に必ず **http://** または **https://** を付けてください。
- ブックマークは、Azure Active Directory で定義されている組織から名前を付けたフォルダー内に作成されます。

|    キー    |    値    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    この構成の値はブックマークのリストです。 各ブックマークは、ブックマークのタイトルとブックマークの URL で構成されます。 タイトルと URL は、`|` 文字で区切ります。<br> 例: `Microsoft Bing|https://www.bing.com`<p>複数のブックマークを構成するには、二重の `||` 文字で各ペアを区切ります。<br>次に例を示します。<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>[マイ アプリ] ブックマーク

既定で、iOS および Android 用の Edge には、組織フォルダー内で [マイ アプリ] ブックマークが設定されています。

|    キー    |    値    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **true** (既定値) を設定すると、iOS および Android 用の Edge のブックマーク内に [マイ アプリ] を表示します<br>**false** を設定すると、iOS および Android 用の Edge 内に [マイ アプリ] が表示されません    |

### <a name="app-behavior-experiences"></a>アプリの動作のエクスペリエンス

iOS および Android 用の Edge には、アプリの動作を管理する複数のオプションが用意されています。

#### <a name="default-protocol-handler"></a>既定のプロトコル ハンドラー

既定では、iOS および Android 用の Edge では、ユーザーが URL でプロトコルを指定しない場合に、HTTPS プロトコル ハンドラーが使用されます。 一般に、これはベスト プラクティスと考えられますが、無効にすることができます。

|    キー    |    値    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     **true** (既定値) を設定すると、既定のプロトコル ハンドラーは HTTPS になります<br>**false** を設定すると、既定のプロトコル ハンドラーは HTTP になります     |

#### <a name="disable-data-sharing-for-personalization"></a>個人用設定のデータ共有を無効にする

iOS および Android 用の Edge の既定では、閲覧エクスペリエンスをカスタマイズするために、使用状況データの収集と閲覧履歴の共有についてユーザーに確認します。 組織は、この確認がエンド ユーザーに表示されないようにすることで、このデータの共有を無効にすることができます。

|    キー    |    値    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     **true** を設定すると、この確認はエンド ユーザーに表示されなくなります<br>**false** (既定値) を設定すると、ユーザーは使用状況データを共有するように求められます    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     **true** を設定すると、この確認はエンド ユーザーに表示されなくなります<br>**false** (既定値) を設定すると、ユーザーは閲覧履歴を共有するように求められます     |

#### <a name="disable-specific-features"></a>特定の機能を無効にする

iOS および Android 用の Edge を使用すると、組織は既定で有効になっている特定の機能を無効にすることができます。 これらの機能を無効にするには、次の設定を構成します。

|    キー    |    値    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    **password** にすると、エンド ユーザーのパスワードを保存するための確認が無効になります<br>**inprivate** にすると、InPrivate ブラウズが無効になります<p>複数の機能を無効にするには、`|` で値を区切ります。 たとえば、`inprivate|password` は InPrivate とパスワード保存を無効にします。     |

> [!NOTE]
> Android 用の Edge では、Password Manager の無効化はサポートされていません。

#### <a name="disable-extensions"></a>拡張機能を無効にする

Android 用の Edge 内の拡張機能フレームワークを無効にして、ユーザーがアプリ拡張機能をインストールできないようにすることができます。 これを行うには、次の設定を構成します。

|    キー    |    値    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    **true** を設定すると、拡張機能フレームワークが無効になります<br>**false** (既定値) を設定すると、拡張機能フレームワークが有効になります    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Android デバイスでのキオスク モード エクスペリエンス

Android 用の Edge は、次の設定を使用して、キオスク アプリとして有効にすることができます。

|    キー    |    値    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    **true** を設定すると、Android 用の Edge でキオスク モードが有効になります<br>**false** (既定値) を設定すると、キオスク モードが無効になります    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    **true** を設定すると、キオスク モードでアドレス バーが表示されます<br> **false** (既定値) を設定すると、キオスク モードが有効な場合にアドレス バーが非表示になります    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    **true** を設定すると、キオスク モードで下部のアクション バーが表示されます<br> **false** (既定値) を設定すると、キオスク モードが有効な場合に下部のバーが非表示になります    |

## <a name="data-protection-app-configuration-scenarios"></a>データ保護アプリ構成シナリオ

アプリが Microsoft Endpoint Manager によって管理され、アプリにサインインしている職場または学校のアカウントに Intune アプリ保護ポリシーが適用されており、ポリシー設定がマネージド アプリのアプリ構成ポリシーを介して配信されている場合、iOS および Android 用の Edge によって、次のデータ保護設定のためのアプリ構成ポリシーがサポートされます。

- アカウントの同期を管理する
- 制限付き Web サイトを管理する
- プロキシの構成を管理する
- NTLM シングル サインオン サイトを管理する

これらの設定は、デバイスの登録ステータスに関係なくアプリに展開できます。

### <a name="manage-account-synchronization"></a>アカウントの同期を管理する

既定では、Microsoft Edge 同期を使用すると、ユーザーはサインインしているすべてのデバイスで閲覧データにアクセスできます。 同期によってサポートされるデータには次のものが含まれます。

- お気に入り
- パスワード
- アドレスなど (オートフィル フォーム入力)

同期機能はユーザーの同意によって有効になり、ユーザーは上記の各種データに対して同期をオンまたはオフにすることができます。 詳細については、[Microsoft Edge の同期](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync)に関するページを参照してください。

組織は、iOS および Android で Edge 同期を無効にする機能を備えています。 

|キー  |値  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |**true** (既定値) を設定すると、Edge 同期を許可します<br>**false** を設定すると、Edge 同期を無効にします          |

### <a name="manage-restricted-web-sites"></a>制限付き Web サイトを管理する

組織は、iOS および Android 用の Edge で、職場または学校アカウントのコンテキスト内でユーザーがアクセスできるサイトを定義できます。 許可リストを使用した場合、ユーザーは明示的にリストされているサイトにのみアクセスできます。 ブロック リストを使用した場合、ユーザーは明示的にブロックされているサイトを除く、すべてのサイトにアクセスできます。 両方ではなく、許可リストまたはブロック リストのみを適用する必要があります。 両方を適用した場合は、許可リストのみが受け付けられます。

また、ユーザーが制限付き Web サイトに移動しようとしたときの動作も定義します。 既定では、移行が許可されます。 組織で許可されている場合、制限付き Web サイトは、個人アカウントのコンテキストまたは Azure AD アカウントの InPrivate コンテキストとして、サイトが完全にブロックされている状況でも開くことができます。 サポートされるさまざまなシナリオの詳細については、「[Microsoft Edge モバイルで制限付き Web サイトの移行](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333)」を参照してください。 移行エクスペリエンスを許可することにより、組織のユーザーは保護された状態を維持しながら、会社のリソースを安全に保ちます。

> [!NOTE]
> iOS および Android 用の Edge では、直接アクセスされたときにのみ、サイトへのアクセスをブロックできます。 ユーザーがサイトへのアクセスに中間サービス (翻訳サービスなど) を使っている場合、アクセスはブロックされません。

iOS および Android 用の Edge に対して許可またはブロックするサイトのリストを構成するには、次のキー/値ペアを使います。 

|キー  |値  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |キーに対応する値は URL のリストです。 許可するすべての URL をパイプ `|` 文字で区切り、単一の値として入力します。<p>**例:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |キーに対応する値は URL のリストです。 ブロックするすべての URL をパイプ `|` 文字で区切り、単一の値として入力します。<br>**例:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |**true** (既定値) を設定すると、iOS および Android 用の Edge で制限付きサイトを移行できます。 個人アカウントが無効になっていない場合、ユーザーは、個人用コンテキストに切り替えて制限付きサイトを開くか、個人アカウントを追加するように求められます。 com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked が true に設定されている場合、ユーザーは InPrivate コンテキスト内で制限付きサイトを開くことができます。<p>**false** を設定すると、iOS および Android 用の Edge でユーザーを移行できなくなります。 ユーザーには、アクセスしようとしているサイトがブロックされていることを示すメッセージが単に表示されます。         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |**true** を設定すると、Azure AD アカウントの InPrivate コンテキストで制限付きサイトを開くことができます。 Azure AD アカウントが、iOS および Android 用の Edge で構成されている唯一のアカウントである場合、制限付きサイトは InPrivate コンテキストで自動的に開かれます。 ユーザーが個人アカウントを構成している場合、InPrivate を開くか、個人アカウントに切り替えるかを選択するようにユーザーに求められます。<p> **false** (既定値) を設定すると、ユーザーの個人アカウントで制限付きサイトを開く必要があります。 個人アカウントが無効になっている場合、サイトはブロックされます。<p>この設定を有効にするには、com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock を true に設定する必要があります。          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | スナック バー通知 "Link opened with InPrivate mode. Your organization requires the use of InPrivate mode for this content." (リンクを InPrivate モードで開きました。組織では、このコンテンツに対し、InPrivate モードの使用を要求しています。) をユーザーに表示する秒数を入力します。 既定では、スナック バー通知は 7 秒間表示されます。

次のサイトは、定義された許可リストまたはブロック リストの設定に関係なく、常に許可されます。
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>許可およびブロック サイト リストの URL 形式 

さまざまな URL 形式を使用して、許可/ブロック サイト リストを作成することができます。 次の表で、これらの許可されているパターンについて詳しく説明します。

- リストに入力するときは、すべての URL の先頭に必ず **http://** または **https://** を付けてください。
- ワイルドカード記号 (\*) は、以下の許可されているパターン リストの規則に従って使用できます。
- ワイルドカードは、ホスト名のコンポーネント全体 (ピリオドで区切られた部分) またはパスの全体部分 (スラッシュで区切られた部分) にのみ一致します。 たとえば、`http://*contoso.com` はサポートされて**いません**。
- アドレスにはポート番号を指定できます。 ポート番号を指定しない場合は、次の値が使用されます。
  - http の場合はポート 80
  - https の場合はポート 443
- ポート番号でのワイルドカードの使用はサポートされて**いません**。 たとえば、 `http://www.contoso.com:*` と `http://www.contoso.com:*/` はサポートされていません。 

    |    [URL]    |    説明    |    ［一致する］    |    ［次の値に一致しない］    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    単一のページと一致する    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    単一のページと一致する    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*`   |    `www.contoso.com` で始まるすべての URL と一致する    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    `contoso.com` の下のすべてのサブドメインと一致する    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    `contoso.com/` で終わるすべてのサブドメインと一致する    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    単一のフォルダーと一致する    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    ポート番号を使用し、単一のページと一致する    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    セキュリティで保護された単一のページと一致する    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    1 つのフォルダーおよびすべてのサブフォルダーと一致する    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- 指定することができない入力例を次に示します。
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP アドレス
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>プロキシの構成を管理する

iOS および Android 用の Edge と [Azure AD アプリケーション プロキシ](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)を一緒に使用して、ユーザーが自分のモバイル デバイスでイントラネット サイトにアクセスできるようにすることができます。 次に例を示します。 

- ユーザーは、Intune で保護されている、Outlook モバイル アプリを使用しています。 その後、メールでイントラネット サイトへのリンクをクリックすると、iOS および Android 用の Edge によって、このイントラネット サイトがアプリケーション プロキシを介してユーザーに公開されていることが認識されます。 ユーザーは、イントラネット サイトに到達する前に、適用される多要素認証と条件付きアクセスによる認証を行うため、アプリケーション プロキシを経由するよう自動的にルーティングされます。 これにより、ユーザーはモバイル デバイス上でも内部サイトにアクセスできるようになり、Outlook のリンクが意図したとおりに機能するようになります。
- ユーザーは、iOS または Android デバイスで、ユーザーが iOS および Android 用の Edge を開きます。 iOS および Android 用の Edge が Intune で保護されており、アプリケーション プロキシが有効になっている場合、ユーザーは、内部 URL を使用してイントラネット サイトに移動できます。 iOS および Android 用の Edge では、このイントラネット サイトがアプリケーション プロキシを使ってユーザーに公開されていることが認識されます。 ユーザーは、イントラネット サイトに到達する前に認証を行うため、アプリケーション プロキシを経由するよう自動的にルーティングされます。 

始める前に

- Azure AD アプリケーション プロキシを経由するように内部アプリケーションを設定します。
  - アプリケーション プロキシを構成し、アプリケーションを公開するには、[セットアップに関するドキュメント](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)を参照してください。
- iOS および Android 用の Edge アプリのユーザーは、[Intune アプリの保護ポリシー](app-protection-policy.md)を割り当てておく必要があります。
- Microsoft アプリには、 **[その他のアプリでの Web コンテンツの転送を制限する]** データ転送設定が **[Microsoft Edge]** に設定されているアプリ保護ポリシーが必要です。

> [!NOTE]
> 更新されたアプリケーション プロキシのリダイレクト データが iOS および Android 用の Edge で有効になるまでには、最大で 24 時間かかる場合があります。

次のキー/値ペアで iOS 用の Edge を対象とし、アプリケーション プロキシを有効にします。

|    キー    |    値    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **true** を設定すると、Azure AD アプリ プロキシ リダイレクト シナリオを有効にします<br>**false** (既定値) を設定すると、Azure AD アプリ プロキシ シナリオを禁止します    |

> [!NOTE]
> Android 用の Edge は、このキーを使用しません。 代わりに、Android 用の Edge では、サインインしている Azure AD アカウントにアプリ保護ポリシーが適用されている限り、Azure AD アプリケーション プロキシ構成を自動的に使用します。

オンプレミスの Web アプリへのシームレスな (保護された) アクセスのために、iOS および Android 用の Edge と Azure AD アプリケーション プロキシを並行使用する方法について詳しくは、「[Better together: Intune and Azure Active Directory team up to improve user access (最適な組み合わせ: ユーザーのアクセスを向上するための Intune と Azure Active Directory の連携)](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254)」を参照してください。 このブログ記事では Intune Managed Browser を参照しますが、そのコンテンツは iOS および Android 用の Edge にも適用されます。

### <a name="manage-ntlm-single-sign-on-sites"></a>NTLM シングル サインオン サイトを管理する

組織は、イントラネット Web サイトにアクセスするために、NTLM を使用した認証をユーザーに要求する場合があります。 既定では、NTLM 資格情報のキャッシュが無効になっているため、NTLM 認証を必要とする Web サイトにアクセスするたびに資格情報を入力するように求められます。 

組織は、特定の Web サイトに対する NTLM 資格情報のキャッシュを有効にすることができます。 これらのサイトでは、ユーザーが資格情報を入力し、正常に認証されると、資格情報が既定で 30 日間キャッシュされます。


|キー  |値  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |キーに対応する値は URL のリストです。 許可するすべての URL をパイプ `|` 文字で区切り、単一の値として入力します。<p>**例:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>サポートされている URL 形式の種類の詳細については、「[許可およびブロック サイト リストの URL 形式](#url-formats-for-allowed-and-blocked-site-list)」を参照してください。         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |資格情報をキャッシュする時間数。既定値は 720 時間         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Microsoft Endpoint Manager を使用してアプリ構成シナリオを展開する

Microsoft Endpoint Manager をモバイル アプリ管理プロバイダーとして使用している場合は、次の手順に従って、マネージド アプリのアプリ構成ポリシーを作成できます。 構成が作成されたら、その設定をユーザーのグループに割り当てることができます。

1. [Microsoft Endpoint Manager](https://endpoint.microsoft.com) にサインインします。

2. **[アプリ]** を選択し、 **[アプリ構成ポリシー]** を選択します。

3. **[アプリ構成ポリシー]** ブレードで **[追加]** を選択し、 **[マネージド アプリ]** を選択します。

4. **[基本]** セクションで **[名前]** に入力し、必要に応じてアプリ構成設定の **[説明]** に入力します。

5. **[パブリック アプリ]** で **[パブリック アプリの選択]** を選択し、 **[対象アプリ]** ブレードで、iOS と Android の両方のプラットフォーム アプリを選択して **iOS および Android 用の Edge** を選択します。 **[選択]** をクリックして、選択したパブリック アプリを保存します。

6. **[次へ]** をクリックして、アプリ構成ポリシーの基本設定を完了します。

7. **[設定]** セクションで、 **[Microsoft Edge の構成設定]** を展開します。

8. データ保護設定を管理する場合は、必要に応じて設定を構成します。

    - **[アプリケーション プロキシのリダイレクト]** で使用可能なオプションである **[有効]** 、 **[無効]** (既定値) から選択します。

    - **[ホームページのショートカットの URL]** で、*http://* または *https://* のプレフィックスを含む有効な URL を指定します。 セキュリティ対策のため、誤った URL はブロックされます。

    - **[マネージド ブックマーク]** で、タイトルと、*http://* または *https://* のプレフィックスを含む有効な URL を指定します。

    - **[許可された URL]** で、有効な URL を指定します (これらの URL のみが許可され、その他のサイトにはアクセスできません)。 サポートされている URL 形式の種類の詳細については、「[許可およびブロック サイト リストの URL 形式](#url-formats-for-allowed-and-blocked-site-list)」を参照してください。

    - **[ブロックする URL]** で、有効な URL を指定します (これらの URL のみがブロックされます)。 サポートされている URL 形式の種類の詳細については、「[許可およびブロック サイト リストの URL 形式](#url-formats-for-allowed-and-blocked-site-list)」を参照してください。

    - **[制限付きサイトを個人用コンテキストにリダイレクトする]** で、使用可能なオプションである **[有効]** (既定値)、 **[無効]** から選択します。

    > [!NOTE]
    > [許可された URL] と [ブロックする URL] の両方がポリシーで定義されている場合は、許可リストのみが受け付けられます。

9. 上記のポリシーで公開されていない追加のアプリ構成設定を使用する場合は、 **[一般的な構成設定]** ノードを展開し、キーと値のペアを入力します。

10. 構成設定が完了したら、 **[次へ]** をクリックします。

11. **[割り当て]** セクションで、 **[含めるグループを選択]** を選択します。 アプリ構成ポリシーを割り当てる Azure AD グループを選択し、 **[選択]** を選択します。

12. 割り当てが完了したら、 **[次へ]** を選択します。

13. **[アプリ構成ポリシーの作成] の [確認および作成]** ブレードで、構成される設定を確認し、 **[作成]** を選択します。

新しく作成された構成が **[アプリの構成]** ブレードに表示されます。

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>iOS および Android 用の Edge を使用して、マネージド アプリのログにアクセスする

iOS または Android デバイスに iOS および Android 用の Edge をインストールしているユーザーは、Microsoft で公開されたすべてのアプリの管理状態を表示できます。 次の手順を使用して、iOS または Android のマネージド アプリのトラブルシューティング用のログを送信できます。

1. デバイスで iOS および Android 用の Edge を開きます。
2. アドレス バーに「`about:intunehelp`」と入力します。
3. iOS および Android 用の Edge でトラブルシューティング モードが起動します。

アプリ ログに格納されている設定の一覧については、「[クライアント アプリの保護ログのレビュー](app-protection-policy-settings-log.md)」を参照してください。

Android デバイスでログを表示する方法については、[メールによる IT 管理者へのログの送信](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

- [アプリ保護ポリシーとは?](app-protection-policy.md) 
- [Microsoft Intune 用アプリ構成ポリシー](app-configuration-policies-overview.md)
