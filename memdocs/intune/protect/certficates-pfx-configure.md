---
title: Microsoft Intune で秘密キーと公開キーの証明書を使用する - Azure | Microsoft Docs
description: Microsoft Intune で公開キー暗号化標準 (PKCS) 証明書を使用し、ルート証明書と証明書テンプレートを処理し、Microsoft Intune コネクタ (NDES) をインストールし、PKCS 証明書のデバイス構成プロファイルを使用します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28ca32bc65ee0c4647c22b10b6b5d47a25efa202
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643616"
---
# <a name="configure-and-use-pkcs-certificates-with-intune"></a>Intune で PKCS 証明書を構成して使用する

Intune では、秘密キーと公開キーのペア (PKCS) の証明書の使用がサポートされています。 この記事は、オンプレミスの証明書コネクタなどの必要なインフラストラクチャを構成し、PKCS 証明書をエクスポートして、Intune デバイス構成プロファイルに証明書を追加するのに役立ちます。

Microsoft Intune には、組織のリソースへのアクセスと認証に PKCS 証明書を使用するための組み込みの設定が含まれています。 証明書により、VPN や WiFi ネットワークなど、企業リソースへのアクセスが認証され、セキュリティで保護されます。 Intune でデバイス構成プロファイルを使用してこれらの設定をデバイスに展開します。

インポートした PKCS 証明書の使用については、[インポートした PFX 証明書](certificates-imported-pfx-configure.md)に関する記事をご覧ください。


## <a name="requirements"></a>要件

Intune で PKCS 証明書を使用するには、次のインフラストラクチャが必要です。

- **Active Directory ドメイン**:  
  このセクションで示されているすべてのサーバーは、Active Directory ドメインに参加する必要があります。

  Active Directory Domain Services (AD DS) をインストールして構成する詳細については、「[Active Directory の設計と計画について](/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning)」を参照してください。

- **証明機関**:  
   エンタープライズ証明機関 (CA)。

  Active Directory 証明書サービス (AD CS) のインストールおよび構成の詳細については、「[Active Directory 証明書サービス ステップ バイ ステップ ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772393(v=ws.10))」を参照してください。

  > [!WARNING]  
  > Intune ではスタンドアロン CA ではなく、エンタープライズ証明機関 (CA) の AD CS を実行する必要があります。

- **クライアント**:  
  エンタープライズ CA に接続する。

- **ルート証明書**:  
  エンタープライズ CA のルート証明書のエクスポートされたコピーです。

- **PFX Certificate Connector for Microsoft Intune**:

  前提条件やリリース バージョンなど、PFX 証明書コネクタの詳細については、[証明書コネクタ](certificate-connectors.md)に関する記事を参照してください。

  > [!IMPORTANT]
  > PFX 証明書コネクタのバージョン 6.2008.60.607 のリリース以降、PKCS 証明書プロファイルでは Microsoft Intune コネクタが不要になりました。 
  
## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>エンタープライズ CA からルート証明書をエクスポートする

VPN、WiFi、またはその他のリソースを使用してデバイスを認証するには、デバイスにルートまたは中間の CA 証明書が必要です。 次の手順では、エンタープライズ CA から必要な証明書を取得する方法について説明します。

**コマンド ラインの使用**:  

1. 管理者アカウントでルート証明機関サーバーにログインします。

2. **[スタート]**  >  **[実行]** の順に移動し、「**Cmd**」を入力してコマンド プロンプトを開きます。

3. **certutil -ca.cert ca_name.cer** を指定して、ルート証明書を *ca_name.cer* という名前のファイルとしてエクスポートします。

## <a name="configure-certificate-templates-on-the-ca"></a>CA 上で証明書テンプレートを構成する

1. 管理特権があるアカウントでエンタープライズ CA にサインインします。
2. **[証明機関]** コンソールで **[証明書テンプレート]** を右クリックして **[管理]** を選択します。
3. **User** 証明書テンプレートを探して右クリックし、 **[テンプレートの複製]** を選択して **[新しいテンプレートのプロパティ]** を開きます。

    > [!NOTE]
    > S/MIME メールの署名と暗号化のシナリオの場合、管理者の多くは、署名と暗号化に対して別々の証明書を使用します。 Microsoft Active Directory Certificate Services を使用している場合、S/MIME メールの署名証明書には **[Exchange 署名のみ]** テンプレートを使用し、S/MIME 暗号化証明書には **[Exchange ユーザー]** テンプレートを使用することができます。  サード パーティ証明機関を使用している場合は、該当するガイダンスを確認して署名および暗号化のテンプレートを設定することをお勧めします。

4. **[互換性]** タブで:

    - **[証明機関]** に **[Windows Server 2008 R2]** を設定します。
    - **[証明書の受信者]** に **[Windows 7 / Server 2008 R2]** を設定します。

5. **[全般]** タブで、 **[テンプレート表示名]** にわかりやすい名前を設定します。

    > [!WARNING]
    > 既定では、 **[テンプレート名]** は **[テンプレート表示名]** (*スペースなし*) と同じです。 テンプレートの名前をメモします。後で必要になります。

6. **[要求処理]** で、 **[プライベート キーのエクスポートを許可する]** を選択します。

    > [!NOTE]
    > SCEP とは対照的に、PKCS では、証明書の秘密キーはデバイス上ではなく、コネクタがインストールされているサーバー上で生成されます。 証明書テンプレートで秘密キーのエクスポートを許可する必要があります。それにより、証明書コネクタでは、PFX 証明書をエクスポートし、それをデバイスに送信できます。 
    >
    > ただし、証明書はデバイス自体にインストールされますが、秘密キーはエクスポート不可としてマークされることにご注意ください。

7. **[暗号化]** で、 **[最小キー サイズ]** が 2048 に設定されていることを確認します。
8. **[サブジェクト名]** で **[要求に含まれる]** を選択します。
9. **[拡張子]** で、 **[アプリケーション ポリシー]** に暗号化ファイル システム、セキュリティで保護された電子メール、クライアント認証が表示されていることを確認します。

    > [!IMPORTANT]
    > iOS/iPadOS の証明書テンプレートの場合、 **[拡張]** タブで、 **[キー使用法]** を更新し、 **[署名は発行元の証明である]** が選択されていないことを確認します。

10. **[セキュリティ]** で、Microsoft Intune コネクタがインストールされているサーバーのコンピューター アカウントを追加します。 このアカウントに、**読み取り**と**登録**のアクセス許可を割り当てます。
11. **[適用]**  >  **[OK]** をクリックして証明書テンプレートを保存します。 **証明書テンプレート コンソール**を閉じます。
12. **[証明機関]** コンソールで **[証明書テンプレート]** を右クリックして、 **[新規作成]**  >  **[発行する証明書テンプレート]** をクリックします。 上記の手順で作成したテンプレートを選択します。 **[OK]** を選択します。
13. 登録されたデバイスとユーザーの証明書をサーバーで管理する場合は、次の手順を使用します。

    1. 証明機関を右クリックして、 **[プロパティ]** を選択します。
    2. [セキュリティ] タブで、コネクタ (**Microsoft Intune コネクタ**、または **PFX Certificate Connector for Microsoft Intune**) が実行されているサーバーのコンピューター アカウントを追加します。 
    3. このコンピューター アカウントに、**証明書の発行と管理**と**証明書の要求**のアクセス許可を付与します。

14. エンタープライズ CA からサインアウトします。

## <a name="download-install-and-configure-the-pfx-certificate-connector"></a>PFX 証明書コネクタのダウンロード、インストール、構成を行う

開始する前に、[コネクタの要件を確認](certificate-connectors.md)し、ご利用の環境と Windows Server でコネクタをサポートする準備ができていることを確認します。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[テナント管理]** 、 **[コネクタとトークン]** 、 **[証明書のコネクタ]** 、 **[+ 追加]** の順に選択します。

3. PKCS #12 のコネクタの *[Certificate Connector ソフトウェアをネットワーク上のセキュリティで保護された場所にダウンロード]* をクリックし、コネクタのインストール先となるサーバーからアクセスできる場所にファイルを保存します。

   ![Microsoft Intune コネクタのダウンロード](./media/certficates-pfx-configure/download-connector.png)

4. ダウンロードが完了したら、サーバーにサインインし、インストーラー (PfxCertificateConnectorBootstrapper) を実行します。  
   - 既定のインストール場所を受け入れると、コネクタは `Program Files\Microsoft Intune\PFXCertificateConnector` にインストールされます。
   - コネクタ サービスはローカル システム アカウントの下で実行されます。 インターネットにアクセスするためにプロキシが必要な場合は、ローカル サービス アカウントがサーバー上のプロキシ設定にアクセスできることを確認します。

5. インストール後、PFX Certificate Connector for Microsoft Intune によって **[登録]** タブが開かれます。 Intune への接続を有効にするには、 **[サインイン]** を選択し、Azure 全体管理者のアクセス許可または Intune 管理者のアクセス許可を持つアカウントを入力します。

   > [!WARNING]
   > 既定では、Windows Server の **[IE セキュリティ強化の構成]** が **[オン]** に設定されています。これにより、Office 365 へのサインインに関する問題が発生する可能性があります。

6. **[CA アカウント]** タブを選択し、発行側の証明機関で証明書の発行と管理アクセス許可を持つアカウントの資格情報を入力します。 これらの資格情報は、証明機関で証明書の失効を実行するために使用されます。 

    変更を**適用**します。

7. ウィンドウを閉じます。

8. Microsoft Endpoint Manager admin center で、 **[テナント管理]**  >  **[コネクタとトークン]**  >  **[証明書のコネクタ]** に戻ります。 しばらくすると、緑のチェック マークが表示され、接続状態が更新されます。 これでコネクタ サーバーは Intune と通信できます。

## <a name="create-a-trusted-certificate-profile"></a>信頼済み証明書プロファイルを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動します。

3. 次のプロパティを入力します。
   - **[プラットフォーム]** :このプロファイルを受信するデバイスのプラットフォームを選択します。
   - **[プロファイル]** : **[信頼された証明書]** を選択します。
  
4. **[作成]** を選択します。

5. **[Basics]\(基本\)** で次のプロパティを入力します。
   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「*会社全体の信頼済み証明書プロファイル*」は適切なプロファイル名です。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** で、以前にエクスポートした .cer ファイルのルート CA 証明書を指定します。

   > [!NOTE]
   > **手順 3** で選択したプラットフォームに応じて、証明書の**保存先ストア**を選択するオプションが使用できる場合と使用できない場合があります。

   ![プロファイルを作成し、信頼済み証明書をアップロードする](./media/certficates-pfx-configure/certificates-pfx-configure-profile-fill.png)

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

   **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 この証明書プロファイルを、PKCS 証明書プロファイルを受信する同じグループに展開するようにします。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. (*Windows 10 のみに適用*) **[適用性ルール]** で、適用性ルールを指定してこのプロファイルの割り当てを調整します。 デバイスの OS エディションまたはバージョンに基づいて、プロファイルを割り当てるかどうかを選択できます。

  詳細については、「*Microsoft Intune でのデバイス プロファイルの作成*」の「[適用性ルール](../configuration/device-profile-create.md#applicability-rules)」を参照してください。

12. **[確認と作成]** で、設定を確認します。 [作成] を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="create-a-pkcs-certificate-profile"></a>PKCS 証明書プロファイルを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動します。

3. 次のプロパティを入力します。
   - **[プラットフォーム]** :デバイスのプラットフォームを選択します。 次のようなオプションがあります。
     - Android デバイス管理者
     - [Android Enterprise] > [フル マネージド、専用、会社所有の仕事用プロファイル]
     - [Android エンタープライズ] > [仕事用プロファイルのみ]
     - iOS/iPadOS
     - macOS
     - Windows 10 以降
   - **[プロファイル]** : **[PKCS 証明書]** を選択します

   > [!NOTE]
   > Android エンタープライズ プロファイルを使用しているデバイスでは、PKCS 証明書プロファイルを使用してインストールされた証明書は、デバイス上に表示されません。 証明書の展開に成功したことを確認するには、Intune コンソール上でプロファイルの状態を確認します。
4. **[作成]** を選択します。

5. **[Basics]\(基本\)** で次のプロパティを入力します。
   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「*会社全体の PKCS プロファイル*」は適切なプロファイル名です。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** では、選択したプラットフォームによって構成できる設定が変わります。 詳細設定のプラットフォームを選択します。- Android デバイス管理者 - Android Enterprise - iOS/iPadOS - Windows 10
   
   |設定     | プラットフォーム     | 詳細   |
   |------------|------------|------------|
   |**[更新しきい値 (%)]**        |<ul><li>すべて         |推奨値は 20% です  | 
   |**[証明書の有効期間]**  |<ul><li>すべて         |証明書テンプレートを変更していない場合、このオプションはおそらく 1 年に設定されています。 |
   |**キー記憶域プロバイダー (KSP)**   |<ul><li>Windows 10  |Windows では、デバイス上のキーを格納する場所を選択します。 |
   |**証明機関**      |<ul><li>すべて         |エンタープライズ CA の内部完全修飾ドメイン名 (FQDN) が表示されます。  |
   |**証明機関名** |<ul><li>すべて         |"Contoso Certification Authority" など、エンタープライズ CA の名前が一覧表示されます。 |
   |**証明書テンプレート名**:    |<ul><li>すべて         |証明書テンプレートの名前を一覧表示します。 |
   |**証明書の種類**             |<ul><li>Android Enterprise (*仕事用プロファイル*)</li><li>iOS</li><li>macOS</li><li>Windows 10 以降|種類の選択: <ul><li> "**ユーザー**" 証明書では、証明書のサブジェクトと SAN 内にユーザー属性とデバイス属性の両方を含めることができます。 </il><li>**[デバイス]** 証明書では、証明書のサブジェクトと SAN にデバイスの属性を含めることができます。 キオスクやその他の共有デバイスなど、ユーザーのいないデバイスなどのシナリオには、[デバイス] を使用します。  <br><br> この選択は、サブジェクト名の形式に影響します。 |
   |**[サブジェクト名の形式]**          |<ul><li>すべて         |サブジェクト名の形式を設定する方法については、この記事で後述する「[サブジェクト名の形式](#subject-name-format)」を参照してください。  <br><br> ほとんどのプラットフォームでは、特に指定がない限り、 **[共通名]** オプションを使用します。 <br><br>次のプラットフォームの場合、サブジェクト名の形式は証明書の種類によって決まります。 <ul><li>Android Enterprise (*仕事用プロファイル*)</li><li>iOS</li><li>macOS</li><li>Windows 10 以降</li></ul>  <p>  |
   |**[サブジェクトの別名]**     |<ul><li>すべて         |*[属性]* については、特に指定がない場合は **[ユーザー プリンシパル名 (UPN)]** を選択し、それに対応する *[値]* を選択し、 **[追加]** をクリックします。 <br><br>詳細については、後述する「[サブジェクト名の形式](#subject-name-format)」を参照してください。|
   |**[拡張キー使用法]**           |<ul><li> Android デバイス管理者 </li><li>Android Enterprise (*デバイス所有者*、*仕事用プロファイル*) </li><li>Windows 10 |ユーザーまたはデバイスがサーバーに対して認証できるように、証明書には通常、 *[クライアント認証]* が必要です。 |
   |**[すべてのアプリが秘密キーにアクセスできるようにする]** |<ul><li>macOS  |**[有効にする]** に設定すると、PKCS 証明書の秘密キーへのアクセスが関連 mac デバイスに構成されているアプリに与えられます。 <br><br> この設定の詳細については、Apple 開発者ドキュメントにある「[Configuration Profile Reference](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf)」の「Certificate Payload」セクションに記載されている *AllowAllAppsAccess* を参照してください。 |
   |**ルート証明書**             |<ul><li>Android デバイス管理者 </li><li>Android Enterprise (*デバイス所有者*、*仕事用プロファイル*) |前に割り当てられたルート CA 証明書プロファイルを選択します。 |

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

   **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 この証明書プロファイルを、信頼された証明書プロファイルを受信するのと同じグループに展開することを計画してください。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 [作成] を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。


### <a name="subject-name-format"></a>サブジェクト名の形式

次のプラットフォーム用の PKCS 証明書プロファイルを作成するとき、サブジェクト名の形式のオプションは、選択した証明書の種類 ( **[ユーザー]** または **[デバイス]** ) によって異なります。  

プラットフォーム:

- Android Enterprise (*仕事用プロファイル*)
- iOS
- macOS
- Windows 10 以降

> [!NOTE]
> PKCS を使用した証明書の取得について、生成される証明書署名要求 (CSR) 内のサブジェクト名に次の文字のいずれかがエスケープ文字 (前にバックスラッシュ \\ が付く) として含まれていた場合に関する既知の問題があります。[SCEP でも同じ問題が確認されています](certificates-profile-scep.md#avoid-certificate-signing-requests-with-escaped-special-characters)。
> - \+
> - ;
> - ,
> - =

- **ユーザー証明書の種類**  
  *[サブジェクト名の形式]* の形式オプションが 2 つあります。**共通名 (CN)** と**電子メール (E)** ) をサポートしています。 **共通名 (CN)** は、次のいずれかの変数に設定できます。

  - **CN={{UserName}}** : janedoe@contoso.com など、ユーザーのユーザー プリンシパル名。
  - **CN={{AAD_Device_ID}}** : Azure Active Directory (AD) にデバイスを登録するときに割り当てられた ID。 通常、この ID は Azure AD での認証に使われます。
  - **CN={{SERIALNUMBER}}** : 一意のシリアル番号 (SN)。通常はデバイスを識別するために製造元によって使われます。
  - **CN={{IMEINumber}}** : 携帯電話の識別に使用される IMEI (International Mobile Equipment Identity) の一意の番号です。
  - **CN={{OnPrem_Distinguished_Name}}** : コンマで区切られた相対識別名のシーケンスです (*CN=Jane Doe,OU=UserAccounts,DC=corp,DC=contoso,DC=com* など)。

    *{{OnPrem_Distinguished_Name}}* 変数を使用するには、[Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) を使用して、*onpremisesdistinguishedname* ユーザー属性をご自分の Azure AD に同期してください。

  - **CN={{onPremisesSamAccountName}}** : 管理者は、Azure AD Connect を使用して、Active Directory の samAccountName 属性を、Azure AD の *onPremisesSamAccountName* という属性に同期できます。 Intune では、証明書のサブジェクト内の証明書発行要求の一部として、その変数を置き換えることができます。 samAccountName 属性は、以前のバージョンの Windows (windows 2000 より前) のクライアントとサーバーをサポートするために使われるユーザー サインイン名です。 ユーザー サインイン名の形式は次のとおりです。*DomainName\testUser*、または *testUser* のみ。

    *{{onPremisesSamAccountName}}* 変数を使用するには、[Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) を使用して、*onPremisesSamAccountName* ユーザー属性をご自分の Azure AD に同期してください。

  これらの変数と静的文字列の 1 つまたは複数を組み合わせて使用することで、次のようなサブジェクト名のカスタム形式を作成できます。  
  - **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**
  
  その例には、CN 変数と E 変数に加えて、組織単位、組織、場所、州、国の各値を表す文字列を使用するサブジェクト名形式が含まれています。 [CertStrToName 関数](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea)の記事では、この関数とそのサポートされる文字列について説明されています。

- **デバイス証明書の種類**  
  サブジェクト名の形式のフォーマットオプションには、次の変数が含まれます。 
  - **{{AAD_Device_ID}}**
  - **{{Device_Serial}}**
  - **{{Device_IMEI}}**
  - **{{SerialNumber}}**
  - **{{IMEINumber}}**
  - **{{AzureADDeviceId}}**
  - **{{WiFiMacAddress}}**
  - **{{IMEI}}**
  - **{{DeviceName}}**
  - **{{FullyQualifiedDomainName}}** *(Windows およびドメインに参加しているデバイスにのみ適用)*
  - **{{MEID}}**

  これらの変数は、テキスト ボックスで指定し、その後に変数のテキストを続けることができます。 たとえば、*Device1* という名前のデバイスの共通名は、**CN={{DeviceName}}Device1** として追加できます。

  > [!IMPORTANT]  
  > - 変数を指定する場合は、エラーが発生しないように、例に示すように、変数名を中かっこ { } で囲みます。  
  > - デバイス証明書の "*サブジェクト*" または *SAN* で使用されるデバイス プロパティ (**IMEI**、**SerialNumber**、**FullyQualifiedDomainName** など) は、デバイスへのアクセス権を持つユーザーによってスプーフィングされる可能性のあるプロパティです。
  > - 証明書プロファイルをデバイスにインストールする場合は、そのプロファイルで指定されたすべての変数が該当するデバイスでサポートされている必要があります。  たとえば、 **{{IMEI}}** が SCEP プロファイルのサブジェクト名に使用されていて、IMEI 番号を持たないデバイスに割り当てられている場合、プロファイルのインストールは失敗します。

## <a name="next-steps"></a>次のステップ

[証明書に SCEP を使用](certificates-scep-configure.md)するか、[Symantec PKI マネージャー Web サービスから PKCS 証明書を発行](certificates-digicert-configure.md)します。

[PKCS 証明書プロファイルのトラブルシューティング](../protect/troubleshoot-pkcs-certificate-profiles.md)
