---
title: Microsoft Intune で SCEP 証明書プロファイルを使用する - Azure | Microsoft Docs
description: Microsoft Intune で Simple Certificate Enrollment Protocol (SCEP) 証明書プロファイルを作成して割り当てます。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5126f2e5cc145e864fb4f56e472dba7a5179540f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915587"
---
# <a name="create-and-assign-scep-certificate-profiles-in-intune"></a>Intune で SCEP 証明書プロファイルを作成して割り当てる

Simple Certificate Enrollment Protocol (SCEP) 証明書をサポートするように[インフラストラクチャを構成](certificates-scep-configure.md)したら、Intune で SCEP 証明書プロファイルを作成し、それをユーザーとデバイスに割り当てることができます。

> [!IMPORTANT]
> SCEP 証明書プロファイルを使用するデバイスの場合、デバイスで信頼されたルート証明機関 (CA) を信頼する必要があります。 ルート CA の信頼を確立するには、SCEP 証明書プロファイルを受信するものと同じグループに[信頼された証明書プロファイル](../protect/certificates-configure.md#create-trusted-certificate-profiles)を展開することをお勧めします。 信頼された証明書プロファイルによって、信頼されたルート CA 証明書がプロビジョニングされます。

## <a name="create-a-scep-certificate-profile"></a>SCEP 証明書プロファイルを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動します。

3. 次のプロパティを入力します。
   - **[プラットフォーム]** :デバイスのプラットフォームを選択します。
   - **[プロファイル]** : **[SCEP 証明書]** を選択します

     **[Android エンタープライズ]** プラットフォームの場合、 *[プロファイルの種類]* は *[フル マネージド、専用、会社所有の仕事用プロファイル]* と *[仕事用プロファイルのみ]* の 2 つのカテゴリに分かれています。 管理するデバイスに対する正しい SCEP 証明書プロファイルを選択してください。  

     *[フル マネージド、専用、会社所有の仕事用プロファイル]* プロファイルの SCEP 証明書プロファイルには次の制限があります。

      1. [監視] では、証明書レポートはデバイス所有者の SCEP 証明書プロファイルに対しては使用できません。

      2. Intune を使用して、デバイス所有者の SCEP 証明書プロファイルによってプロビジョニングされた証明書を失効させることはできません。 失効を管理するには、外部プロセスを使用するか、証明機関で直接行います。

      3. Android Enterprise 専用デバイスの場合、SCEP 認証プロファイルは Wi-Fi ネットワーク構成、VPN、認証でサポートされます。 Android Enterprise 専用デバイスの SCEP 証明書プロファイルは、アプリの認証ではサポートされていません。

4. **[作成]** を選択します。

5. **[Basics]\(基本\)** で次のプロパティを入力します。
   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「*会社全体の SCEP プロファイル*」は適切なプロファイル名です。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** で、次の構成を行います。

   - **[証明書の種類]** :

     *(適用対象: Android、Android エンタープライズ、iOS/iPadOS、macOS、Windows 8.1 以降、Windows 10 以降。)*

     証明書プロファイルの使用方法に応じて、種類を選択します。

     - **ユーザー**: "*ユーザー*" 証明書では、証明書のサブジェクトと SAN 内にユーザー属性とデバイス属性の両方を含めることができます。  
     - **デバイス**: *[デバイス]* 証明書では、証明書のサブジェクトと SAN にデバイスの属性を含めることができます。

       キオスクのようなユーザーのいないデバイスなどのシナリオまたは Windows デバイスには、 **[デバイス]** を使用します。 Windows デバイスでは、ローカル コンピューターの証明書ストアに証明書が配置されます。

     > [!NOTE]
     > macOS では、SCEP でプロビジョニングする証明書は常に、デバイスのシステム キーチェーン (システム ストア) に配置されます。
 
   - **[サブジェクト名の形式]** :

     Intune が証明書要求のサブジェクト名をどのように自動生成するかを選択します。 サブジェクト名の形式のオプションは、選択した証明書の種類 ( **[ユーザー]** または **[デバイス]** ) によって異なります。

     > [!NOTE]
     > SCEP を使用した証明書の取得について、生成される証明書署名要求 (CSR) 内のサブジェクト名に次の文字のいずれかがエスケープ文字 (前にバックスラッシュ \\ が付く) として含まれていた場合に関する[既知の問題](#avoid-certificate-signing-requests-with-escaped-special-characters)があります。
     > - \+
     > - ;
     > - ,
     > - =

     - **ユーザー証明書の種類**

       *[サブジェクト名の形式]* の形式オプションは次のとおりです。

       - **未構成**
       - **共通名**
       - **電子メールを含む共通名**
       - **電子メールとしての共通名**
       - **IMEI (International Mobile Equipment Identity)**
       - **シリアル番号**
       - **[カスタム]** : このオプションを選択すると、 **[カスタム]** テキスト ボックスも表示されます。 このフィールドを使用して、変数など、カスタムのサブジェクト名の形式を入力します。 カスタムの形式では、2 つの変数 (**共通名 (CN)** と**電子メール (E)** ) をサポートしています。 **共通名 (CN)** は、次のいずれかの変数に設定できます。

         - **CN={{UserName}}** : janedoe など、ユーザーのユーザー名。
         - **CN={{UserPrincipalName}}** :janedoe@contoso.com など、ユーザーのユーザー プリンシパル名。\*
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
         
         \* [Android フル マネージド、専用、会社所有の仕事用プロファイル] プロファイルには、**CN={{UserPrincipalName}}** 設定は動作しません。 Android の "Android フル マネージド、専用、会社所有の仕事用プロファイル" プロファイルは、"ユーザー" なしのデバイスに使用できるため、このプロファイルではユーザーのユーザー プリンシパル名を受け取れません。 ユーザーのいるデバイスに対してこのオプションが本当に必要な場合は、**CN={{UserName}}\@contoso.com** のような回避策を使用できます。これにより、手動で追加したユーザー名とドメイン (janedoe@contoso.com など) が指定されます

      - **デバイス証明書の種類**

        サブジェクト名の形式のフォーマットオプションには、次の変数が含まれます。

        - **{{AAD_Device_ID}}** または **{{AzureADDeviceId}}** - いずれかの変数を使用して、デバイスをその Azure AD ID で識別できます。
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
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

   - **[サブジェクトの別名]** : Intune が証明書の要求内でサブジェクト代替名 (SAN) を自動的に作成する方法を選択します。 SAN のオプションは、選択した証明書の種類 ( **[ユーザー]** または **[デバイス]** ) によって異なります。

      - **ユーザー証明書の種類**

        次の使用可能な属性から選択します。

        - **電子メール アドレス**
        - **ユーザー プリンシパル名 (UPN)**

        たとえば、ユーザー証明書の種類では、サブジェクトの別名にユーザー プリンシパル名 (UPN) を含めることができます。 クライアント証明書をネットワーク ポリシー サーバーでの認証に使用する場合は、サブジェクトの別名を UPN に設定します。

      - **デバイス証明書の種類**

        **[属性]** ドロップダウンを使用して、属性を選択し、**値**を割り当てて、それを証明書プロファイルに**追加**します。 複数の値を追加するには、追加の属性を選択します。

        使用できる属性は次のとおりです。

        - **電子メール アドレス**
        - **ユーザー プリンシパル名 (UPN)**
        - **DNS**

        *[デバイス]* 証明書の種類を使用すると、値に次のデバイス証明書変数を使用できます。

        - **{{AAD_Device_ID}}** または **{{AzureADDeviceId}}** - いずれかの変数を使用して、デバイスをその Azure AD ID で識別できます。
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - **{{FullyQualifiedDomainName}}**
        - **{{MEID}}**

        属性の値を指定するには、変数名に中かっこを付け、その後にその変数のテキストを入力します。 たとえば、DNS 属性の値を追加して、 **{{AzureADDeviceId}}.domain.com** とすることができます。ここで、 *.domain.com* はテキストです。 *User1* という名前のユーザーについては、電子メール アドレスが {{FullyQualifiedDomainName}}User1@Contoso.com と表示されることがあります。

        > [!IMPORTANT]
        > - デバイス証明書変数を使用する場合は、変数名を中かっこ { } で囲みます。
        > - 変数の後に続くテキストには、中かっこ **{ }** 、パイプ記号 **|** 、セミコロン **;** を使用しないでください。
        > - デバイス証明書の "*サブジェクト*" または *SAN* で使用されるデバイス プロパティ (**IMEI**、**SerialNumber**、**FullyQualifiedDomainName** など) は、デバイスへのアクセス権を持つユーザーによってスプーフィングされる可能性のあるプロパティです。
        > - 証明書プロファイルをデバイスにインストールする場合は、そのプロファイルで指定されたすべての変数が該当するデバイスでサポートされている必要があります。  たとえば、 **{{IMEI}}** が SCEP プロファイルの SAN で使用されていて、IMEI 番号のないデバイスに割り当てられている場合、プロファイルのインストールに失敗します。

   - **[証明書の有効期間]** :

     証明書テンプレートの有効期限よりも小さい値を入力できますが、大きい値は指定できません。 [Intune コンソール内から設定できるカスタム値をサポート](certificates-scep-configure.md#modify-the-validity-period-of-the-certificate-template)するように証明書テンプレートを構成した場合、この設定を使用して、証明書の有効期限が切れるまでの残り時間を指定します。

     たとえば、証明書テンプレートで証明書の有効期限が 2 年の場合は、この値を 1 年にすることはできますが、5 年にすることはできません。 また、発行元の CA の証明書の残りの有効期限よりも小さい値を指定する必要があります。

   - **キー記憶域プロバイダー (KSP)** :

     *(適用対象: Windows 8.1 以降、Windows 10 以降)*

     証明書のキーを格納する場所を指定します。 次の値から選択します。

     - **トラステッド プラットフォーム モジュール (TPM) KSP が存在する場合は TPM KSP に登録する (それ以外はソフトウェア KSP に登録する)**
     - **トラステッド プラットフォーム モジュール (TPM) KSP に登録する (それ以外は失敗)**
     - **Passport に登録する、それ以外は失敗 (Windows 10 以降)**
     - **ソフトウェア KSP に登録する**

   - **[キー使用法]** :

     証明書のキー使用法のオプションを選択します。

     - **[デジタル署名]** : キーがデジタル署名で保護されている場合のみ、キーを交換できます。
     - **[キーの暗号化]** : キーが暗号化されている場合のみ、キーを交換できます。

   - **[キー サイズ (ビット)]** :

     キーに含めるビット数を選択します。

   - **ハッシュ アルゴリズム**:

     *(Android、Android Enterprise、Windows 8.1 以降、Windows 10 以降に適用されます)*

     この証明書で使用するハッシュ アルゴリズムの種類を 1 つ選択します。 接続しているデバイスをサポートするセキュリティの最も強力なレベルを選択します。

   - **[ルート証明書]** :

     構成済みであって、さらにこの SCEP 証明書プロファイルの適用対象のユーザーとデバイスに割り当ててある "*信頼された証明書プロファイル*" を選択します。 信頼された証明書プロファイルは、信頼されたルート CA 証明書でユーザーとデバイスをプロビジョニングするために使用されます。 信頼された証明書プロファイルの詳細については、*Intune での認証に証明書を使用*に関するページの「[信頼されたルート CA 証明書をエクスポートする](certificates-configure.md#export-the-trusted-root-ca-certificate)」と「[信頼された証明書プロファイルを作成する](certificates-configure.md#create-trusted-certificate-profiles)」を参照してください。 ルート証明機関と発行元の証明機関がある場合は、発行元の証明機関の検証に使用する信頼されたルート証明書プロファイルを選択します。
     > [!NOTE]
     > iOS/iPadOS デバイス上では、ルート証明機関と発行元の証明機関がある場合は、ルート証明機関の検証に使用する信頼されたルート証明書プロファイルを選択します。 

   - **[拡張キー使用法]** :

     証明書の使用目的に対応する値を追加します。 ほとんどの場合、ユーザーまたはデバイスがサーバーに対して認証できるように、証明書には "*クライアント認証*" が必要です。 必要に応じて、追加のキー使用法を追加できます。

   - **[更新しきい値 (%)]** :

     証明書の有効期間の残りがどの程度 (%) になったら、デバイスが更新を要求するかを入力します。 たとえば、「20」と入力した場合、証明書の更新は、証明書の有効期限が 80% 経過すると試行されます。 更新が成功するまで更新の試行は続行されます。 更新によって新しい証明書が生成され、その結果、公開キーと秘密キーのペアが新しくなります。

   - **[SCEP サーバーの URL]** :

     SCEP 経由で証明書を発行する NDES サーバーの URL を 1 つまたは複数入力します。 たとえば、`https://ndes.contoso.com/certsrv/mscep/mscep.dll` のようなものを入力します。

     必要に応じて負荷分散のために SCEP URL を追加できます。 デバイスでは、3 回に分けて NDES サーバーが呼び出されます。それぞれ、サーバー機能を取得するため、公開キーを取得するため、署名要求を送信するためです。 複数の URL を使用するとき、負荷分散によって、その後 NDES サーバーを呼び出すとき、別の URL が使用されることがあります。 同じ要求中に、後続の呼び出しのために別のサーバーが接触されると、要求が失敗します。

     NDES サーバー URL を管理するための動作は各デバイス プラットフォームに固有です。

     - **Android**: デバイスにより SCEP ポリシーで受信した URL の一覧がランダム化され、アクセス可能な NDES サーバーが見つかるまで一覧が処理されます。 その後、プロセス全体で引き続き、その同じ URL とサーバーがデバイスで使用されます。 デバイスでいずれの NDES サーバーにもアクセスできない場合、プロセスは失敗します。
     - **iOS/iPadOS**:Intune では、URL がランダム化され、デバイスに URL が 1 つ提供されます。 そのデバイスで NDES サーバーにアクセスできない場合、SCEP 要求が失敗します。
     - **Windows**: NDES URL の一覧がランダム化され、Windows デバイスに渡されて、それにより利用できるものが見つかるまで、受け取った順番に試行されます。 デバイスでいずれの NDES サーバーにもアクセスできない場合、プロセスは失敗します。

     NDES サーバーを 3 回呼び出す過程のいずれかでデバイスが同じ NDES サーバーに到達できなかった場合、SCEP 要求は失敗します。 たとえば、このような失敗は、NDES サーバーを呼び出す 2 回目か 3 回目で負荷分散ソリューションにより別の URL が指定されるとき、あるいは NDES の仮想 URL に基づき、別の実際の NDES サーバーが指定されるときに起こることがあります。 要求に失敗すると、次のポリシー サイクルでデバイスはプロセスを再試行します。そのとき、NDES URL のランダム化された一覧から始めるか、iOS/iPadOS の場合、1 つの URL から始めます。  

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

   **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. (*Windows 10 のみに適用*) **[適用性ルール]** で、適用性ルールを指定してこのプロファイルの割り当てを調整します。 デバイスの OS エディションまたはバージョンに基づいて、プロファイルを割り当てるかどうかを選択できます。

   詳細については、「*Microsoft Intune でのデバイス プロファイルの作成*」の「[適用性ルール](../configuration/device-profile-create.md#applicability-rules)」を参照してください。

12. **[確認と作成]** で、設定を確認します。 [作成] を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

### <a name="avoid-certificate-signing-requests-with-escaped-special-characters"></a>エスケープされた特殊文字を含む証明書署名要求を回避する

SCEP と PKCS 証明書要求に、以下の特殊文字をエスケープ文字として 1 文字以上含んでいる [サブジェクト名] (CN) が含まれている場合について、既知の問題があります。 サブジェクト名にエスケープ文字として特殊文字が 1 文字含まれていると、CSR のサブジェクト名が不正になります。 サブジェクト名が不正な場合、Intune SCEP チャレンジの検証に失敗し、証明書が発行されません。

その特殊文字は次のとおりです。
- \+
- ,
- ;
- =

使用するサブジェクト名に特殊文字のいずれかが含まれている場合は、次のオプションのいずれかを使用してこの制限を回避してください。

- 特殊文字を含む CN 値を引用符で囲む。  
- CN 値から特殊文字を削除する。

**たとえば**、*Test user (TestCompany, LLC)* として表示される [サブジェクト名] があるとします。  *TestCompany* と *LLC* の間にコンマがある CN を含んでいる CSR で問題が発生します。  この問題を回避するには、CN 全体を引用符で囲むか、*TestCompany* と *LLC* の間のコンマを削除します。

- **引用符を追加する**:*CN="Test User (TestCompany, LLC)",OU=UserAccounts,DC=corp,DC=contoso,DC=com*
- **コンマを削除する**:*CN=Test User (TestCompany LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

 ただし、バックスラッシュ文字を使ってコンマをエスケープしようとすると失敗し、CRP ログにエラーが記録されます。
 
- **エスケープしたコンマ**:*CN=Test User (TestCompany\\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

このエラーは次のようなエラーになります。

```
Subject Name in CSR CN="Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com" and challenge CN=Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com do not match  

  Exception: System.ArgumentException: Subject Name in CSR and challenge do not match

   at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

Exception:    at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

   at Microsoft.ConfigurationManager.CertRegPoint.Controllers.CertificateController.VerifyRequest(VerifyChallengeParams value
```

## <a name="assign-the-certificate-profile"></a>証明書プロファイルを割り当てる

他の目的で[デバイス プロファイルを展開](../configuration/device-profile-assign.md)する場合と同じ方法で、SCEP 証明書プロファイルを割り当てます。

SCEP 証明書プロファイルを使用するには、信頼されたルート CA 証明書を使用してプロビジョニングする信頼された証明書プロファイルもデバイスで受信している必要があります。 信頼されたルート証明書プロファイルと SCEP 証明書プロファイルの両方を同じグループに展開することをお勧めします。

続行する前に、次の点を考慮してください。

- SCEP 証明書プロファイルをグループに割り当てると、信頼されたルート CA 証明書プロファイル (*信頼された証明書プロファイル*に指定されている) がデバイスにインストールされます。 デバイスでは、SCEP 証明書プロファイルを使用して、その信頼されたルート CA 証明書に対する証明書要求が作成されます。

- SCEP 証明書プロファイルは、証明書プロファイルの作成時に指定されたプラットフォームを実行するデバイス上にのみインストールされます。

- ユーザー コレクションまたはデバイス コレクションに証明書プロファイルを割り当てることができます。

- デバイス登録後すぐに証明書をデバイスに公開するには、証明書プロファイルをデバイス グループではなくユーザー グループに割り当てます。 デバイス グループに割り当てた場合は、デバイスがポリシーを受け取る前に、デバイスの登録を完全に行う必要があります。

- Intune と Configuration Manager に共同管理を使用する場合は、Configuration Manager でリソース アクセス ポリシーの[ワークロード スライダー](/configmgr/comanage/how-to-switch-workloads)を **[Intune]** または **[パイロット Intune]** に設定します。 この設定により、Windows 10 クライアントは証明書を要求するプロセスを開始できます。

> [!NOTE]
> - iOS/iPadOS デバイスでは、SCEP 証明書プロファイルまたは PKCS 証明書プロファイルが Wi-Fi プロファイルや VPN プロファイルなどの追加のプロファイルに関連付けられている場合、デバイスは、該当する追加のプロファイルの各々に対する証明書を受け取ります。 これにより、SCEP 証明書または PKCS 証明書の要求によって提供される複数の証明書を持つ iOS/iPadOS デバイスが存在するようになります。 
> 
>   SCEP によって提供される証明書はそれぞれ一意です。 PKCS によって提供される証明書は同じ証明書ですが、各プロファイル インスタンスは管理プロファイルの別の行で表されるため、異なるように見えます。
> - iOS 13 および macOS 10.15 の場合は、[Apple によって文書化されている追加のセキュリティ要件](https://support.apple.com/HT210176)をいくつか考慮に入れる必要があります。  


## <a name="next-steps"></a>次のステップ

[プロファイルの割り当て](../configuration/device-profile-assign.md)

[SCEP 証明書プロファイルの展開に関するトラブルシューティング](../protect/troubleshoot-scep-certificate-profiles.md)