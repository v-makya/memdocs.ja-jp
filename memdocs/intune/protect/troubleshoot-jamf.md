---
title: Jamf Pro と Microsoft Intune の統合のトラブルシューティング
titleSuffix: Microsoft Intune
description: Mac デバイス用の Jamf Pro と Microsoft Intune を統合するときに最も多く発生する問題のうち、一部の問題の解決方法を提案します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/01/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 78f69edbc38bc41863783010a0e795290b7762c5
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270924"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>Jamf Pro と Microsoft Intune の統合のトラブルシューティング

この記事は、Intune 管理者が macOS 用 Jamf Pro と Intune の統合に関する問題を理解し、解決するのに役立ちます。

> [!TIP]  
> この記事に記載されている情報の多くは、もともとは support.microsoft.com の [Jamf と Microsoft Intune を統合するときの問題のトラブルシューティング](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune)に関する記事に記載されていたものです。

## <a name="prerequisites"></a>[前提条件]

トラブルシューティングを始める前に、いくつかの基本的な情報を収集して問題を明確にし、解決策を見つけるための時間を短縮します。 たとえば、Jamf と Intune の統合に関連する問題が発生した場合は、前提条件がすべて満たされていることを必ず確認します。 トラブルシューティングを始める前に、次の考慮事項を確認してください。

- Jamf Pro と Intune の統合を構成する方法に応じて、次の記事の前提条件を確認してください。
  - [Jamf Cloud コネクタを使用して Jamf Pro を Intune と統合する](conditional-access-jamf-cloud-connector.md)
  - [Jamf Pro と Intune を統合する](conditional-access-integrate-jamf.md#prerequisites)
- すべてのユーザーが、 Microsoft Intune と Microsoft AAD Premium P1 のライセンスを持っている必要があります
- Jamf Pro コンソールで Microsoft Intune 統合アクセス許可を持つユーザー アカウントが必要です。
- Azure でグローバル管理者のアクセス許可を持つユーザー アカウントが必要です。

Jamf Pro と Intune の統合を調べるときは、次の情報を考慮してください。

- 正確なエラー メッセージは何ですか?
- エラーメッセージはどこにありますか?
- 問題が発生し始めたのはいつですか?  Jamf Pro と Intune の統合は動作していましたか?
- 影響を受けているユーザーの数はどれくらいですか? すべてのユーザーに影響がありますか、それとも一部だけですか?
- 影響を受けているデバイスの数はどれくらいですか? すべてのデバイスですか、一部だけですか?
 
## <a name="common-problems"></a>一般的な問題

次の情報は、Intune と Jamf Pro の統合を設定した後で、デバイスの一般的な問題を特定して解決するのに役立ちます。  

| 問題   | 説明                  |
|-----------------|--------------------------|
| **デバイスが Jamf Pro で応答不能とマークされる**  | [デバイスが、Jamf Pro または Azure AD にチェックインできません](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Mac デバイスでアプリを開くとキーチェーンのサインインを求められる**  | [アプリを Azure AD に登録できるよう、ユーザーがパスワードの入力を求められます](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app)。 |
| **デバイスを登録できない**  | 次の原因が該当する可能性があります。 <br> **-** [***原因 1*** - Azure の Jamf Pro アプリのアクセス許可が正しくありません](#cause-1) <br> **-** [***原因 2*** - Azure AD の *Jamf Native macOS Connector* に問題があります](#cause-2) <br> **-** [***原因 3*** - ユーザーに Intune または Jamf の有効なライセンスがありません](#cause-3) <br> **-** [***原因 4*** - ユーザーが Jamf Self Service を使用して Intune ポータル サイト アプリを起動しませんでした](#cause-4) <br> **-** [***原因 5*** - Intune の統合がオフになっています](#cause-5) <br> **-** [***原因 6*** - デバイスが既に Intune に登録されているか、ユーザーがデバイスを複数回登録しようとしました](#cause-6) <br> **-** [***原因 7*** - JamfAAD がユーザーのキーチェーンから "Microsoft Workplace Join キー" へのアクセスを要求しています](#cause-7) |
|  **Mac デバイスが Intune では準拠と表示されるが、Azure では非準拠と表示される** | [デバイス登録に関する問題](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **Jamf を使用して登録された Mac デバイスに対して Intune コンソールで重複するエントリが表示される** | [同じデバイスに対する複数の登録](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **コンプライアンス ポリシーでデバイスの評価が失敗する** | [ポリシーでデバイス グループが対象になっています](#compliance-policy-fails-to-evaluate-the-device) |
| **Microsoft Graph API のアクセス トークンを取得できない** | 次の原因が該当する可能性があります。 <br> [Azure の Jamf Pro アプリに対する - のアクセス許可](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> [Jamf または Intune の -  期限切れライセンス](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [ポートが開かれていません](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>デバイスが Jamf Pro で応答不能とマークされる  

**原因**:Jamf Pro によってデバイスが "*応答不能*" とマークされる一般的な原因を次に示します。

- デバイスが Jamf Pro にチェックインできません。  
  Jamf Pro では、デバイスが 15 分ごとにチェックインすることが想定されています。 24 時間にわたってチェックインできなかった場合、デバイスは Jamf によって応答不能とマークされます。  

- デバイスが Azure AD にチェックインできません。  
  Azure AD への登録に成功すると、macOS デバイスは Azure トークンを受け取ります。
  - このトークンは 12 時間ごとに更新されます。   
  - 24 時間以上トークンが更新されないと、Jamf Pro はデバイスを応答不能とマークします。  
  - Azure トークンの有効期限が切れると、ユーザーは Azure にサインインして新しいトークンを取得するように求められます。 Azure アクセス用の更新トークンは 7 日ごとに生成されます。

**解決方法**  
デバイスが Jamf Pro によって "*応答なし*" としてマークされた後、デバイスの登録ユーザーはサインインして応答不能状態を修正する必要があります。 ログイン キーチェーンに Intune からの ID があるため、それはアカウントにワークプレースで参加しているユーザーである必要があります。



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Mac デバイスでアプリを開くとキーチェーンのサインインを求められる  

Intune と Jamf Pro の統合を構成し、条件付きアクセス ポリシーを展開した後、Jamf Pro で管理されているデバイスのユーザーは、Teams、Outlook、および Azure AD 認証を必要とするその他のアプリなどの Microsoft Office 365 アプリケーションを開くと、パスワードの入力を求められます。 

たとえば、Microsoft Teams を開くと、次の例のテキストのようなプロンプトが表示されます。

``` 
  Microsoft Teams wants to sign using key "Microsoft Workplace Join Key" in your keychain.  
  To allow this, enter the "login" keychain password 
```

**原因**:これらのプロンプトは、Azure AD の登録を必要とする該当する各アプリに対して Jamf Pro によって生成されます。 

**解決方法**   
プロンプトで、ユーザーはデバイスのパスワードを入力して Azure AD にサインインする必要があります。 次のオプションがあります。
- **[Deny]\(拒否\)** - サインインせず、アプリを使用しません。
- **[Allow]\(許可\)** - ワンタイム サインイン。 次にアプリを開いたときも、再びサインインするように求められます。
- **[Always Allow]\(常に許可\)** - アプリケーションに対してサインイン資格情報がキャッシュされます。 次にアプリを開いたときは、サインインするように求められません。  

1 つのアプリに対して *[Always Allow]\(常に許可\)* を選択すると、将来のサインインではそのアプリだけが承認されます。 他のアプリは、やはり *[Always Allow]\(常に許可\)* として設定されるまで、認証を要求されます。 1 つのアプリに対してキャッシュされた資格情報は、別のアプリでは使用できません。  

### <a name="devices-fail-to-register"></a>デバイスを登録できない  

Mac デバイスの登録が失敗する場合、一般的な原因がいくつかあります。  

#### <a name="cause-1"></a>原因 1  

**Azure の Jamf Pro エンタープライズ アプリケーションに、間違ったアクセス許可があるか、複数のアクセス許可があります**

  Azure でアプリを作成するときに、すべての既定の API アクセス許可を削除してから、Intune に 1 つのアクセス許可 *update_device_attributes* を割り当てる必要があります。 

  **解決方法**  
  Jamf アプリのアクセス許可を確認し、必要に応じて修正します。 Jamf Pro Cloud Connector を使用している場合は、このアプリが自動的に作成されています。 統合を手動で構成した場合は、Azure AD でアプリを作成しています。 アプリのアクセス許可については、[Azure AD で Jamf 用のアプリケーションを作成する](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory)手順を参照してください。

#### <a name="cause-2"></a>原因 2  

**Jamf Native macOS Connector **アプリが Azure AD テナントに作成されていないか、コネクタに対する同意がグローバル管理者権限のないアカウントによって署名されました****  

  **解決方法**  
  docs.jamf.com の「[Microsoft Intune との統合](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html)」の「*macOS Intune 統合の構成*」セクションを参照してください。

#### <a name="cause-3"></a>原因 3

**ユーザーに Intune または Jamf の有効なライセンスがありません**

  有効なライセンスがないと、Jamf ライセンスの有効期限が切れていることを示す次のエラーが発生する可能性があります。  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **解決方法**
  - Jamf のライセンス: Jamf の新しいライセンスを取得する方法については、Jamf にお問い合わせください。  
  - Intune のライセンス: ユーザーに有効なライセンスを割り当てるか、最新のライセンスを取得する方法について Microsoft またはパートナーにお問い合わせください。

#### <a name="cause-4"></a>原因 4  

**ユーザーが *Jamf Self Service* を使用して Intune ポータル サイト アプリを起動しませんでした**

デバイスが Jamf を通じて Intune に正常に登録するには、ユーザーは Jamf Self Service を使用して、Intune ポータル サイトを開く必要があります。 ユーザーが Intune ポータル サイトを手動で開くと、デバイスは Jamf への接続なしで登録されます。  

デバイスで登録に使用されたサービスを特定するには、デバイスで Intune ポータル サイト アプリを調べます。 Jamf を使用して登録した場合は、Self-Service アプリを開いて変更するように通知されます。

Intune ポータル サイト アプリでユーザーに **`Not registered`** と表示され、次の例のようなエントリが Intune ポータル サイト ログに記録されることがあります。  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**解決方法**  
登録ソースを Intune から Jamf に変更するには:
1. [Intune から macOS デバイスの登録を解除します](https://docs.microsoft.com/mem/intune/user-help/unenroll-your-device-from-intune-macos)。 Intune から完全に削除されていないデバイスでさらに問題が発生するのを防ぐため、この原因一覧の「[*原因 6*](#cause-6)」を参照してください。  

2. デバイスで、Jamf Self Service を使用して Intune ポータル サイト アプリを開き、Intune にデバイスを登録します。 このタスクを行うには、[Jamf を使用して macOS 用の Intune ポータル サイト アプリを展開](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro)し、[ユーザー デバイスを Azure AD に登録するポリシーを Jamf Pro で作成](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory)しておく必要があります。  

3. ポータルを開くと最初に表示される画面で、サインインを求められます。 職場または学校アカウントを使用する  

4. ポータル サイトではアカウント情報が確認され、デバイス登録の状況とデバイス コンプライアンスの状況が表示されます。 学校や職場の macOS デバイスをセキュリティで保護するために行う必要があるアクションが黄色の三角形で強調表示されます。 [開始] をクリックして登録を開始します。  

5. 求められたら、コンピューターのサインイン情報を入力します。  
     
デバイスを管理対象に登録するまで数分かかる場合があります。 この間、デバイスで他の作業を行ってもかまいません。 会社アクセス設定が完了した後、完了を知らせるメッセージが表示されます。

#### <a name="cause-5"></a>原因 5  

**Intune の統合がオフになっています**

Intune の統合が無効になっていると、ユーザーがデバイスを登録しようとすると、Intune ポータル サイトでポップアップ ウィンドウに次のメッセージが表示されます。  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

統合を無効にすると、統合が無効になっていることを Intune に通知するパルスが、Jamf Pro サーバーから Intune サーバーに送信されます。 

**解決方法**  
Jamf Pro で Intune の統合を再度有効にします。 統合の構成方法に応じて、次を参照してください。

- [Jamf Cloud コネクタを使用して Jamf Pro を Intune と統合する](conditional-access-jamf-cloud-connector.md)
- [Jamf Pro で Microsoft Intune 統合を手動で構成する](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro)。

#### <a name="cause-6"></a><a name="cause-6"></a>原因 6  

**デバイスが既に Intune に登録されているか、ユーザーがデバイスを複数回登録しようとしました**

デバイスが Jamf から登録解除されたときに Intune から正しく削除されていない場合、または複数の登録の試行が行われた場合は、同じデバイスの複数のインスタンスがポータルに表示されることがあります。 これにより、Jamf の登録が失敗します。

**解決方法**  
1. Mac で**ターミナル**を起動します。
2. **sudo JAMF removemdmprofile** を実行します。
3. **sudo JAMF removeFramework** を実行します。
4. JAMF Pro サーバーで、コンピューターのインベントリ レコードを削除します。
5. Azure AD からデバイスを削除します。
6. デバイス上に次のファイルが存在する場合は、削除します。
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/\<*username*>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/\<*username*>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Microsoft セッションのトランスポート キー (公開キーと秘密キー)
   - Microsoft Workplace Join キー (公開キーと秘密キー)
7. *Microsoft*、*Intune*、または *Intune ポータル サイト*を参照するデバイス上のキーチェーンからすべてを削除します (DeviceLogin.microsoft.com 証明書を含む)。 JAMF の公開キーと秘密キーを除く、*JAMF* の参照を削除します。 
   > [!IMPORTANT]  
   > 公開キーと秘密キーを削除すると、デバイスの登録が壊れます。

8. 次のいずれかのエントリが見つかったら削除します。  
   - 種類: アプリケーション パスワード ; アカウント: com.microsoft.workplacejoin.thumbprint
   - 種類: アプリケーション パスワード ; アカウント: com.microsoft.workplacejoin.registeredUserPrincipalName
   - 種類: 証明書 ; 発行元: MS-Organization-Access
   - 種類: ID 基本設定 ; 名前 (存在する場合は ADFS STS URL): https://adfs\<DNSName>.com/adfs/ls
   - 種類: ID 基本設定 ; 名前: `https://enterpriseregistration.windows.net`
   - 種類: ID 基本設定 ; 名前: `https://enterpriseregistration.windows.net/`
9. Mac を再起動します。
10. デバイスから Intune ポータル サイトをアンインストールします。
11. portal.manage.microsoft.com にアクセスし、Mac デバイスのすべてのインスタンスを削除します。 少なくとも 30 分待ってから、次の手順に進みます。
12. JAMF Pro にデバイスを再度登録します。
13. Self Service を再度開き、登録ポリシーを開始します。


#### <a name="cause-7"></a>原因 7  

**JamfAAD がユーザーのキーチェーンから "Microsoft Workplace Join キー" へのアクセスを要求しています**

登録の間に、macOS デバイスのユーザーは、キーチェーンからキーへの JamfAAD のアクセスの許可を求める次のようなプロンプトを受け取ります。 

```
   JamfAAD wants to access key "Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the "login" keychain password
```

**解決方法**  
デバイスを Azure AD に正常に登録するには、ユーザーがアカウント パスワードを入力して、 **[Allow]\(許可\)** を選択する必要があります。

この要求は、この記事で前に説明した[アプリを開いたときにキーチェーン サインインを求める Mac デバイス](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app)の要求と似ています。  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Mac デバイスが Intune では準拠と表示されるが、Azure では非準拠と表示される  

**原因**:次の状況により、デバイスが Intune では準拠と表示され、Azure では非準拠と表示されることがあります。  
- デバイスが正しく登録されていません。  
- デバイスが、必要なクリーンアップを行わずに複数回登録されました。

**解決方法**  
この問題を解決するには、前に説明した「*デバイスを登録できない*」の「[*原因 6*](#cause-6)」の解決策に従います。 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>Jamf を使用して登録された Mac デバイスに対して Intune コンソールで重複するエントリが表示される  
 
**原因**:デバイスが Intune に複数回登録されています。通常は、Intune から削除された後で再登録されています。  

デバイスが Intune と Jamf Pro の統合から削除されると、一部のデータが残っている場合があり、これにより、連続した登録によってエントリが重複して作成される可能性があります。  

**解決方法**  
この問題を解決するには、前に説明した「*デバイスを登録できない*」の「[*原因 6*](#cause-6)」の解決策に従います。

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>コンプライアンス ポリシーでデバイスの評価が失敗する  

**原因**:Jamf と Intune の統合では、デバイス グループを対象とするコンプライアンス ポリシーがサポートされません。

**解決方法**  
ユーザー グループに割り当てられるように、macOS デバイスのコンプライアンス ポリシーを変更します。

### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>Microsoft Graph API のアクセス トークンを取得できない

次のエラーが表示されます。

`Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.`

このエラーの原因としては、次のいずれかが考えられます。

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Azure で Jamf Pro アプリケーションにアクセス許可の問題が発生しています

Azure で Jamf Pro アプリを登録するときに、次のいずれかの状態が発生しました。

- アプリが複数のアクセス許可を受け取りました。
- **[ *\<your company>* に管理者の同意を与えます]** オプションが選択されていません。  

**解決方法**  
前に説明した「[デバイスを登録できない](#devices-fail-to-register)」の原因 1 の解決策を参照してください。

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Jamf と Intune の統合に必要なライセンスが期限切れになりました

**解決方法**:「[デバイスを登録できない](#devices-fail-to-register)」の原因 3 の解決策を参照してください。

#### <a name="the-required-ports-arent-open-on-your-network"></a>必要なポートがネットワーク上で開かれていません

**解決方法**:  
Jamf Pro と Intune を統合するための「[前提条件](conditional-access-jamf-cloud-connector.md#prerequisites)」で、ネットワークのポートに関する情報を確認してください。

## <a name="next-steps"></a>次のステップ

[Jamf Pro と Intune の統合](conditional-access-integrate-jamf.md)についてさらに学習します。