---
title: Jamf Pro Cloud Connector を Microsoft Intune と統合する
titleSuffix: Microsoft Intune
description: Jamf Cloud Connector と一緒に Microsoft Intune コンプライアンス ポリシーと Azure Active Directory の条件付きアクセスを使って、Jamf でマネージド デバイスを統合し、セキュリティで保護できます。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f86b418df46069b2a33dd56d06e0e82dbbbf8090
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81538450"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>Jamf Cloud Connector を Microsoft Intune で使用する

この記事では、Jamf Cloud Connector をインストールして、Jamf Pro を Microsoft Intune と統合する方法について説明します。 Cloud Connector では、「[コンプライアンスのために Jamf Pro を Intune と統合する](../protect/conditional-access-integrate-jamf.md)」の説明に従って手動で統合を構成する場合に必要となる手順の多くを自動化します。

Cloud Connector を設定すると:

- 設定を行うと、Jamf Pro アプリケーションが Azure に自動的に作成されるので、手動で構成する必要がなくなります。
- Jamf Pro の複数のインスタンスを、お客様の Intune サブスクリプションをホストする同一の Azure テナントに統合できます。

Jamf Pro の複数のインスタンスを単一の Azure テナントに接続することは、Cloud Connector を使用する場合にのみサポートされます。 手動で構成された接続を使用する場合、Jamf のインスタンスは 1 つのみ Azure テナントと統合できます。

Cloud Connector の使用には、次の選択肢があります。

- まだ Jamf と統合されていない新しいテナントの場合は、この記事の説明に従って Cloud Connector を構成するか、 「[コンプライアンスのために Jamf Pro を Intune と統合する](../protect/conditional-access-integrate-jamf.md)」の説明に従って手動で統合を構成するかをユーザーが選択できます。
- 既に手動で構成されているテナントの場合は、その統合を削除してから、Cloud Connector を設定することを選択できます。 この記事では、既存の統合の削除と Cloud Connector の設定の両方について説明します。

以前の統合を Jamf Cloud Connector に置き換えるには:

- [現在の構成を削除するための手順](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)を実行します。これには、Jamf Pro 用のエンタープライズ アプリを削除し、その手動統合を無効にすることが含まれます。 次に、[Cloud Connector を構成するための手順](#configure-the-cloud-connector-for-a-new-tenant)を実行できます。
- デバイスを再登録する必要はありません。 既に登録されているデバイスでは、追加の構成をしなくても Cloud Connector を使用できます。
- 登録済みデバイスが自身の状態を報告し続けられるようにするため、手動統合を削除してから 24 時間以内に Cloud Connector を必ず構成してください。

Jamf Cloud Connector の詳細については、docs.jamf.com の「[Cloud Connector を使用した macOS Intune 統合の構成](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html)」を参照してください。

## <a name="prerequisites"></a>[前提条件]

**製品とサービス**:  
- Jamf Pro 10.18 以降
- 条件付きアクセス特権を持つ Jamf Pro ユーザー アカウント  
- Microsoft Intune
- Microsoft Azure AD Premium
- [macOS 用ポータル サイト アプリ](https://aka.ms/macoscompanyportal)
- OS X 10.12 Yosemite 以降を使用する macOS デバイス

**ネットワーク**:  
Jamf と Intune を適切に統合するには、次のポートとエンドポイントにアクセスできる必要があります。

- **Intune**:ポート 443
- **Apple**:ポート 2195、2196、および 5223 (Intune へのプッシュ通知)
- **Jamf**:ポート 80 および 5223

- エンドポイント:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

APNS がネットワーク上で正常に機能するには、次のポートに対する発信接続、およびそれらのポートからのリダイレクトを有効にする必要があります。

- すべてのクライアント ネットワークからの TCP ポート 5223 および 443 上の Apple 17.0.0.0/8 ブロック。
- Jamf Pro サーバーからのポート 2195 および 2196。

これらのポートの詳細については、次の記事を参照してください。

- [Intune のネットワーク構成の要件と帯域幅](../fundamentals/network-bandwidth-use.md)。
- jamf.com 上で [Jamf Pro に使用されるネットワーク ポート](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro)。
- support.apple.com 上で [Apple ソフトウェア製品に使用される TCP ポートと UDP ポート](https://support.apple.com/HT202944)

**[アカウント]** :  
この記事の手順を実行するには、次のアクセス許可を持つアカウントを使用する必要があります。

- **Jamf Pro コンソール**:Jamf Pro を管理するためのアクセス許可を持つアカウント
- **Microsoft Endpoint Management 管理センター**:グローバル管理者
- **Azure portal**:グローバル管理者

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>以前に構成したテナントの Jamf Pro 統合を削除する

Cloud Connector を構成する*前に*、次の手順を実行して、Azure テナントから手動で構成した Jamf Pro の統合を削除します。

Jamf Pro と Intune との間の接続をこれまでに設定していない場合、または Cloud Connector を既に使用している接続が 1 つ以上ある場合は、この手順をスキップし、「[新しいテナント用に Cloud Connector を構成する](#configure-the-cloud-connector-for-a-new-tenant)」に進んでください。

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>手動で構成された Jamf Pro 統合を削除する

1. Jamf Pro コンソールにサインインします。

2. **[設定]** (右上隅の歯車アイコン) を選択し、 **[グローバル管理]**  >  **[条件付きアクセス]** の順に移動します。

   ![[条件付きアクセス] に移動](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. **[編集]** を選択します。

4. **[Enable Intune Integration for macOS]\(macOS の Intune 統合の有効化\)** チェックボックスをオフにします。

   この設定をオフにすると、接続は無効になりますが、構成は保存されます。

5. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインし、 **[テナント管理]**  >  **[パートナー デバイス管理]** の順に移動します。

   **[パートナー デバイス管理]** ノードで、 **[Jamf の Azure Active Directory アプリ ID を指定します]** フィールドにある**アプリケーション ID** を削除し、 **[保存]** を選択します。

   このアプリケーション ID は、Jamf Pro の場合に手動統合を設定するときに Azure で作成された Azure エンタープライズ アプリの ID です。

6. グローバル管理者のアクセス許可を持つアカウントで [Azure portal](https://portal.azure.com/) にサインインし、 **[Azure Active Directory]**  >  **[エンタープライズ アプリケーション]** の順に移動します。

   2 つの Jamf アプリを見つけて、それらを削除します。 次の手順で Jamf Cloud Connector を構成すると、新しいアプリケーションが自動的に作成されます。

   ![Jamf アプリの選択と削除](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   Jamf Pro で統合を無効にし、エンタープライズ アプリケーションを削除すると、 **[パートナー デバイス管理]** ノードに接続の状態が **[Terminated]\(終了\)** として表示されます。

   ![[Terminated]\(終了\) の接続状態](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

これで、Jamf Pro 統合の手動構成が正常に削除されたので、Cloud Connector を使用して統合を設定することができます。 これを行うには、この記事の「[新しいテナント用に Cloud Connector を構成する](#configure-the-cloud-connector-for-a-new-tenant)」を参照してください。

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>新しいテナント用に Cloud Connector を構成する

次の場合は、以下に示す手順を使用して、Jamf Cloud Connector を構成し、Jamf Pro と Microsoft Intune を統合します。

- Jamf Pro と Intune の間に Azure テナント用の統合は構成されていない。
- Azure テナントで Jamf Pro と Intune の間に Cloud Connector が既に設定されており、追加の Jamf インスタンスをサブスクリプションと統合する必要がある。

Intune と Jamf Pro の間に手動で構成された統合がある場合は、先に進む前に、この記事の「[以前に構成したテナントの Jamf Pro 統合を削除する](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)」を参照してその統合を削除してください。 Jamf Cloud Connector を正常に設定するには、その前に、手動で構成された統合を削除する必要があります。

### <a name="create-a-new-connection"></a>新しい接続を作成する

1. Jamf Pro コンソールにサインインします。

2. **[設定]** (右上隅の歯車アイコン) を選択し、 **[グローバル管理]**  >  **[条件付きアクセス]** の順に移動します。

   ![[条件付きアクセス] に移動](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. **[編集]** を選択します。

4. **[Enable Intune Integration for macOS]\(macOS の Intune 統合の有効化\)** チェックボックスをオンにします。
   - この設定を選択すると、Jamf Pro はインベントリの更新情報を Microsoft Intune に送信します。
   - この設定をオフにして接続を無効にしても、構成は保存できます。

   > [!IMPORTANT]
   > **[Enable Intune Integration for macOS]\(macOS の Intune 統合の有効化\)** が既に選択されていて、 *[接続の種類]* が **[手動]** に設定されている場合は、先に進む前にその統合を削除する必要があります。 先に進む前に、この記事の「[以前に構成したテナントの Jamf Pro 統合を削除する](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)」を参照してください。

5. *[接続の種類]* で、 **[Cloud Connector]** を選択します。

   ![Jamf Pro コンソールで Cloud Connector を選択](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. **[ソブリン クラウド]** ポップアップ メニューから、Microsoft からのソブリン クラウドの場所を選択します。

7. Microsoft Azure によって認識されないコンピューターについて、次のいずれかのランディング ページ オプションを選択します。
   - **[Default Jamf Pro Device Registration]\(既定の Jamf Pro デバイス登録\) ページ** - このオプションを使用すると、macOS デバイスの状態によって、ユーザーは Jamf Pro デバイス登録ポータル (Jamf Pro に登録する場合) か、Intune ポータル サイト アプリ (Azure AD に登録する場合) のどちらかにリダイレクトされます。
   - **[アクセスが拒否されました] ページ**
   - **カスタム URL**

8. **[接続]** を選択します。 Azure に Jamf Pro アプリケーションを登録するため、リダイレクトが実行されます。

   プロンプトが表示されたら、Microsoft Azure の資格情報を指定し、画面の指示に従って要求されたアクセス許可を付与します。 **Cloud Connector** に対してアクセス許可を付与し、**Cloud Connector ユーザー登録アプリ**に対してもアクセス許可を付与します。 両方のアプリは、エンタープライズ アプリケーションとして Azure に登録されます。

   両方のアプリに対してアクセス許可が付与されると、 **[アプリケーション ID]** ページが開きます。

9. **[アプリケーション ID]** ページで、 **[Intune をコピーして開く]** を選択します。

   ![アプリケーション ID](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   次の手順で使用するために *アプリケーション ID* がシステム クリップボードにコピーされ、*Microsoft Endpoint Manager admin center* の **[パートナー デバイス管理]** ノードが開きます。 ( **[テナント管理]**  >  **[パートナー デバイス管理]** )。

10. **[パートナー デバイス管理]** ノードで、 **[Jamf の Azure Active Directory アプリ ID を指定します]** フィールドに**アプリケーション ID** を*貼り付け*し、 **[保存]** を選択します。

    ![パートナー デバイス管理の構成](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. Jamf Pro の [アプリケーション ID] ページに戻り、 **[確認]** を選択します。

12. Jamf Pro により構成が完了され、テストが実行されます。接続の成功または失敗は、条件付きアクセス設定ページに表示されます。 成功の例を次の図に示します。

    ![Jamf Pro での成功した構成の確認](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. Microsoft Endpoint Manager 管理センターで、 **[パートナー デバイス管理]** ノードを最新の情報に更新します。 接続が **[アクティブ]** として表示されるはずです。

    ![接続状態が [アクティブ]](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

Jamf Pro と Microsoft Intune の間の接続が正常に確立されると、Jamf Pro は Azure AD に登録されている各コンピューターのインベントリ情報を Microsoft Intune に送信します (Azure AD への登録はエンドユーザーのワークフローです)。 Jamf Pro のコンピューターのインベントリ情報の [ローカル ユーザー アカウント] カテゴリで、ユーザーとコンピューターの条件付きアクセス インベントリ状態を確認できます。

Jamf Cloud Connector を使用して Jamf Pro のインスタンスを 1 つ統合できれば、この同じ手順を使用して、Azure テナント内の同じ Intune サブスクリプションで Jamf Pro の追加インスタンスを構成できます。  

## <a name="set-up-compliance-policies-and-register-devices"></a>コンプライアンス ポリシー設定してデバイスを登録する

Intune と Jamf の統合を構成したら、[Jamf で管理されたデバイスにコンプライアンス ポリシーを適用する](../protect/conditional-access-assign-jamf.md)必要があります。

## <a name="disconnect-jamf-pro-and-intune"></a>Jamf Pro と Intune を切断する

Jamf Pro と Intune の統合を削除する必要がある場合は、次の手順に従って、Jamf Pro コンソール内から接続を削除します。この情報は、Cloud Connector と手動で構成された統合の両方に適用されます。

1. Jamf Pro で、 **[グローバル管理]**  >  **[条件付きアクセス]** に移動します。 **[macOS Intune Integration]\(macOS Intune 統合\)** タブで、 **[編集]** を選択します。

2. **[Enable Intune Integration for macOS]\(macOS の Intune 統合の有効化\)** チェック ボックスをオフにします。

3. **[保存]** を選択します。 Jamf Pro によって構成が Intune に送信され、統合が終了します。

4. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

5. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[パートナー デバイスの管理]** の順に選択して、状態が **[終了]** になっていることを確認します。

   > [!NOTE]
   > 組織の Mac デバイスは、コンソールに表示されている日付 (3 か月後) に削除されます。

## <a name="get-support-for-the-cloud-connector"></a>Cloud Connector のサポートを受ける

統合に必要な Azure エンタープライズ アプリは Cloud Connector によって自動的に作成されるので、最初のサポート連絡先は **Jamf** になります。 次のオプションがあります。

- メールでのサポート: `support@jamf.com`
- Jamf Nation のサポート ポータルを使用する: https://www.jamf.com/support/ 


サポートに問い合わせる前に:

- 使用するポートや製品バージョンなどの前提条件を確認します。
- Azure で作成された次の 2 つの Jamf Pro アプリのアクセス許可が変更されていないことを確認します。 アプリのアクセス許可の変更は Intune でサポートされていないため、統合が失敗する可能性があります。

  **Cloud Connector ユーザー登録アプリ**:
  - API 名:Microsoft Graph
    - アクセス許可:サインインし、ユーザー プロファイルを読む
    - 種類:委任
    - 付与方法:管理者の同意
    - 許可元:管理者

  **Cloud Connector アプリ**:
  - API 名:Microsoft Graph (インスタンス 1)
    - アクセス許可:サインインし、ユーザー プロファイルを読む
    - 種類:委任
    - 付与方法:管理者の同意
    - 許可元:管理者

  - API 名:Microsoft Graph (インスタンス 2)
    - アクセス許可:ディレクトリ データの読み込み
    - 種類:アプリケーション
    - 付与方法:管理者の同意
    - 許可元:管理者

  - API 名:Intune API
    - アクセス許可:デバイス属性を Microsoft Intune に送信する
    - 種類:アプリケーション
    - 付与方法:管理者の同意
    - 許可元:管理者

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Jamf Cloud Connector に関してよく寄せられる質問

### <a name="what-data-is-shared-via-the-cloud-connector"></a>Cloud Connector を介して共有されるのはどのようなデータですか?

Cloud Connector は Microsoft Azure で認証を行い、デバイス インベントリ データを Jamf Pro から Azure に送信します。 また、Cloud Connector は、Azure でのサービス検出、トークン交換、通信エラー、およびディザスター リカバリーを管理します。

### <a name="where-is-device-inventory-data-stored"></a>デバイス インベントリ データはどこに保存されますか?

デバイス インベントリ データは、Jamf Pro データベースに保存されます。

### <a name="what-credentials-are-stored"></a>どのような資格情報が保存されますか?

資格情報は保存されません。 Cloud Connector を構成するときに、管理者は、Jamf マルチテナント アプリと Native macOS Connector アプリを Azure AD テナントに追加することに同意する必要があります。 マルチテナント アプリケーションが追加されると、Cloud Connector は Azure API と対話するためにアクセス トークンを要求します。 アプリケーション アクセスは、いつでも Microsoft Azure で取り消して、アクセスを制限できます。

### <a name="how-is-data-encrypted"></a>データはどのように暗号化されますか?

Cloud Connector は、Jamf Pro と Microsoft Azure の間で送信されるデータに対してトランスポート層セキュリティ (TLS) を使用します。

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>Jamf は、どのデバイスが Jamf Pro のどのインスタンスに関連付けられているかをどのように認識しますか?

Jamf Pro は、AWS のマイクロサービスを使用して、正しいインスタンスにデバイス情報を正しくルーティングします。

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>使用する接続の種類を Cloud Connector から手動に切り替えることはできますか?

はい。 接続の種類を [手動] に戻して、手動セットアップの手順を実行できます。 ご質問がある場合は、Jamf にお問い合わせください。

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>必要なアプリ (*Cloud Connector* および *Cloud Connector ユーザー登録アプリ*) の 1 つまたは両方でアクセス許可が変更されており、登録が機能していません。これはサポートされていますか?

アプリのアクセス許可の変更は、サポートされていません。

## <a name="next-steps"></a>次のステップ

- [Jamf で管理されたデバイスにコンプライアンス ポリシーを適用する](../protect/conditional-access-assign-jamf.md)
- [Jamf から Intune に送られるデータ](../protect/data-jamf-sends-to-intune.md)
