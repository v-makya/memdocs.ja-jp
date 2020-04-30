---
title: チュートリアル&#58; インターネット デバイスの共同管理を有効にする
titleSuffix: Configuration Manager
description: Configuration Manager と Microsoft Intune を使用し、新しいインターネットベースの Windows 10 デバイスの共同管理を構成する方法について説明します。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/12/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 75016e8028dde29c83ae7e7f5a23a1f6dbb4417f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692990"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>チュートリアル:新しいインターネットベースのデバイスの共同管理を有効にする

共同管理では、Configuration Manager を使用して組織の PC を管理するための既に確立されているプロセスを保持できます。 同時に、セキュリティと最新のプロビジョニングのために Intune の使用を通してクラウドに投資しています。

このチュートリアルでは、Azure Active Directory (AD) とオンプレミス AD の両方を使用し、[ハイブリッド Azure Active Directory](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD) がない環境で Windows 10 デバイスの共同管理を設定します。 Configuration Manager 環境には、すべてのサイト システムの役割が同じサーバー (サイト サーバー) 上にある単一のプライマリ サイトが含まれています。 このチュートリアルは、Windows 10 デバイスが既に Intune に登録されているという前提から始まります。 

オンプレミスの AD が Azure AD に参加しているハイブリッド Azure AD の場合は、[Configuration Manager クライアントの共同管理の有効化](tutorial-co-manage-clients.md)に関する手引きのチュートリアルに従うことをお勧めします。

このチュートリアルは、以下に該当する場合に使用します。
  
- 共同管理に参加させる Windows 10 デバイスがあります。 このようなデバイスは、Windows Autopilot を介してプロビジョニングされる場合、またはハードウェア OEM から直接プロビジョニングされる場合があります。
- インターネット上に現在 Intune で管理しており、Configuration Manager クライアントを追加する Windows 10 デバイスがあります。

**このチュートリアルでは、以下を行います。**  
> [!div class="checklist"]  
> * Azure とオンプレミス環境の前提条件を確認する
> * クラウド管理ゲートウェイ (CMG) 用のパブリック SSL 証明書を要求する
> * Configuration Manager で Azure サービスを有効にする
> * クラウド管理ゲートウェイを展開して構成する  
> * CMG を使用するように管理ポイントとクライアントを構成する
> * Configuration Manager で共同管理を有効にする
> * Configuration Manager クライアントをインストールするように Intune を構成する

## <a name="prerequisites"></a>[前提条件]  

### <a name="azure-services-and-environment"></a>Azure サービスと環境

- Azure サブスクリプション ([無料試用版](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune サブスクリプション
  > [!TIP]  
  > Enterprise Mobility + Security (EMS) のサブスクリプションには、Azure Active Directory Premium と Microsoft Intune の両方が含まれています。 EMS サブスクリプション ([無料試用版](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial))。  

- [デバイスを自動登録する](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)ように Intune を構成する  

> [!TIP]
> ユーザーに対して個別の Intune または EMS ライセンスを購入して割り当てる必要はなくなりました。 詳細については、「[Configuration Manager のブランチとライセンスに関してよく寄せられる質問](../core/understand/product-and-licensing-faq.md#bkmk_mem)」を参照してください。

### <a name="on-premises-infrastructure"></a>オンプレミス インフラストラクチャ

- Configuration Manager (Current Branch) バージョン 1810 以降。
  
  バージョン 1810 では[拡張 HTTP](../core/plan-design/hierarchy/enhanced-http.md) が導入されました。このチュートリアルでは、より複雑な PKI 要件を回避するためにこれを使用します。 拡張 HTTP を使用すると、クライアントの管理に使用するプライマリ サイトは、HTTP サイト システム用に Configuration Manager が生成した証明書を使用するように構成する必要があります。  

  また、バージョン 1810 では、Configuration Manager クライアントをインターネットベースでインストールするためのより簡単なコマンド ラインも導入されています。

- MDM 機関を Intune に設定する必要があります  

### <a name="external-certificates"></a>外部の証明書

- CMG サーバー認証証明書。 この証明書は、パブリックでグローバルで信頼されている証明書プロバイダーの SSL 証明書です。 たとえば、DigiCert、Thawte、VeriSign です。この 3 つに限らず他にも存在します。 秘密キーを含む .PFX ファイルとしてこの証明書をエクスポートします。  

- このチュートリアルの後半では、この証明書に対する要求を構成する方法に関するガイダンスを示します。

### <a name="permissions"></a>アクセス許可

このチュートリアルでは、次のアクセス許可を使用してタスクを完了します。

- Azure Active Directory (Azure AD) の "*全体管理者*" であるアカウント
- オンプレミス インフラストラクチャ上で "*ドメイン管理者*" であるアカウント  
- Configuration Manager の "*すべての*" スコープで "*完全な権限を持つ管理者*" であるアカウント

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>クラウド管理ゲートウェイ用のパブリック証明書を要求する

デバイスがインターネットに接続されている場合、共同管理には Configuration Manager クラウド管理ゲートウェイ (CMG) が必要です。 CMG を使用すると、インターネットベースの Windows 10 デバイスは、オンプレミスの Configuration Manager 展開と通信できます。 デバイスと Configuration Manager 環境との間に信頼関係を確立するには、CMG に SSL 証明書が必要です。

このチュートリアルでは、グローバルに信頼されている証明書プロバイダーから承認が派生した **CMG サーバー認証証明書**というパブリック証明書を使用します。 オンプレミスの Microsoft 証明機関から承認が派生する証明書を使用して共同管理を構成することはできますが、自己署名証明書の使用については、このチュートリアルでは扱いません。

**CMG サーバー認証証明書**は、Configuration Manager クライアントと CMG 間の通信トラフィックを暗号化するために使用されます。 この証明書は信頼されたルートまでさかのぼってトレースし、クライアントに対してサーバーの ID を確認します。 パブリック証明書には、Windows クライアントが既に信頼している信頼されたルートが含まれています。

この証明書の概要: 

- Azure で CMG サービスの一意の名前を特定してから、証明書要求でその名前を指定します。  
- 特定のサーバーで証明書要求を生成してから、その要求をパブリック証明書プロバイダーに送信し、必要な SSL 証明書を取得します。  
- 要求を生成したシステムに、プロバイダーから受信した証明書をインポートします。 後で CMG を Azure にデプロイするときに使用する証明書のエクスポートにも同じコンピューターを使用します。  
- CMG をインストールすると、証明書で指定した名前を使用して Azure に CMG サービスが作成されます。  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Azure でクラウド管理ゲートウェイの一意の名前を特定する

CMG サーバー認証証明書を要求するときは、Azure で "*クラウド サービス (クラシック)* " を特定できる一意の名前を指定する必要があります。 既定では、Azure パブリック クラウドは *cloudapp.net* を使用し、CMG は *\<YourUniqueDnsName>.cloudapp.net* という cloudapp.net ドメイン内でホストされます。  

> [!TIP]  
> このチュートリアルの **CMG サーバー認証証明書**では末尾が *contoso.com* の FQDN を使用します。  CMG を作成したら、組織のパブリック DNS に正規名レコード (CNAME) を構成します。 このレコードによって、パブリック証明書で使用する名前に対応する CMG のエイリアスを作成します。  

パブリック証明書を要求する前に、使用する名前が Azure で使用できることを確認してください。 Azure 内にサービスを直接作成しません。 CMG のインストール時にクラウド サービスを作成する際に、Configuration Manager では要求したパブリック証明書に指定されている名前が代わりに使用されます。  

1. [Microsoft Azure ポータル](https://portal.azure.com/)にサインインします。  

2. **[リソースの作成]** を選択し、 **[コンピューティング]** カテゴリを選択して、 **[クラウド サービス]** を選択します。 クラウド サービス (クラシック) ページが開きます。

3. **[DNS 名]** には、使用するクラウド サービスのプレフィックス名を指定します。 このプレフィックスは、後で CMG サーバー認証証明書のパブリック証明書を要求するときに使用するものと同じにする必要があります。 *MyCSG* を使用して、*MyCSG.cloudapp.net* の名前空間を作成します。 インターフェイスで、その名前が使用できるか、既に別のサービスで使用されているかを確認できます。  
 目的の名前を使用できることを確認したら、証明書署名要求 (CSR) を送信する準備は完了です。

### <a name="request-the-certificate"></a>証明書を要求する

次の情報を使用して、CMG の証明書署名要求をパブリック証明書プロバイダーに送信します。 以下の値は実際の環境に合わせて変更してください。  

- クラウド管理ゲートウェイのサービス名を識別する *MyCMG*
- 会社名の *Contoso*
- パブリック ドメインの *Contoso.com*

プライマリ サイト サーバーを使用して証明書署名要求 (CSR) を生成することをお勧めします。 証明書を取得したら、CSR を生成したサーバーと同じサーバーに登録する必要があります。そうしないと、必須の証明書の秘密キーをエクスポートできません。  

CSR を生成するときはバージョン 2 のキー プロバイダーの種類が必要です。 サポートされているのはバージョン 2 の証明書のみです。  

> [!TIP]  
> CMG を展開するときは、クラウド配布ポイント (CDP) も同時にインストールします。 CMG を展開する場合、既定では **[CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする]** オプションがオンです。 同じサーバー上に CDP と CMG を配置すると、CDP をサポートするための個別の証明書と構成が不要になります。 共同管理を使用するために CDP は必須ではありませんが、ほとんどの環境で役立ちます。  
>
> 共同管理に追加のクラウド配布ポイントを使用する場合は、追加のサーバーごとに個別の証明書を要求する必要があります。 CDP のパブリック証明書を要求するには、クラウド管理ゲートウェイの CSR の場合と同じ詳細情報を使用します。 共通名を変更するだけで、CDP ごとに一意の名前にすることができます。  

#### <a name="details-for-the-cloud-management-gateway-csr"></a>クラウド管理ゲートウェイ CSR の詳細情報

- **共通名**:クラウドサービス名 CMG. 会社のパブリックドメイン名.com  
例:MyCSG.contoso.com  
- **サブジェクトの別名**:共通名 (CN) と同じです。  
- **組織**:組織の名前  
- **部署**:組織ごと  
- **市区町村**:組織ごと  
- **状態**:組織ごと  
- **国**:組織ごと  
- **キーのサイズ:2048**  
- **プロバイダー:Microsoft RSA SChannel Cryptographic Provider**  

### <a name="import-the-certificate"></a>証明書をインポートする

パブリック証明書を受け取ったら、CSR を作成したコンピューターのローカル証明書ストアにインポートします。 次に、その証明書を .PFX ファイルとしてエクスポートして、Azure 内の CMG に使用できるようにします。  

通常、証明書のインポートに関する指示はパブリック証明書プロバイダーから提供されます。 証明書をインポートするプロセスは、次のようなガイダンスになります。  

1. 証明書のインポート先のコンピューターで、証明書の .pfx ファイルを見つけます。  

2. ファイルを右クリックして、 **[PFX のインストール]** を選択します  

3. 証明書のインポート ウィザードが起動したら、 **[次へ]** を選択します  

4. **[インポートする証明書ファイル]** ページで **[次へ]** を選択します

5. **[パスワード]** ページで [パスワード] ボックスに秘密キーのパスワードを入力し、 **[次へ]** を選択します。  
  
   キーをエクスポートできるようにするオプションを選択します。

6. **[証明書ストア] ページ**で、 **[証明書の種類に基づいて、自動的に証明書ストアを選択する]** をオンにして **[次へ]** を選択します  

7. **[完了]** を選択します。

### <a name="export-the-certificate"></a>証明書のエクスポート

サーバーから *CMG サーバー認証証明書*をエクスポートします。 証明書を再エクスポートすると、Azure のクラウド管理ゲートウェイで使用できるようになります。  

1. パブリック SSL 証明書をインポートしたサーバー上で、**certlm.msc** を実行して証明書マネージャー コンソールを開きます。  

2. 証明書マネージャー コンソールで、 **[個人] > [証明書]** を選択します。 次に、前の手順で登録した *[CMG サーバー認証証明書]* を右クリックし、 **[すべてのタスク] > [エクスポート]** を選択します。  

3. 証明書のエクスポート ウィザードが起動したら、 **[次へ]** を選択し、 **[はい、秘密キーをエクスポートします]** を選択して **[次へ]** をクリックします。  

4. [エクスポート ファイルの形式] ページで **[Personal Information Exchange - PKCS #12 (.PFX)]** を選択し、 **[次へ]** を選択してパスワードを指定します。 ファイル名には **C:\ConfigMgrCloudMGServer** のような名前を指定します。 Azure で CMG を作成するときにこのファイルを参照します。  

5. **[次へ]** を選択し、次の設定を確認してから、 **[完了]** を選択してエクスポートを完了します。  

   - [キーのエクスポート] = はい  
   - [証明のパスにあるすべての証明書を含める] = はい  
   - [ファイル形式] = Personal Information Exchange (*.pfx)  

6. エクスポートが完了したら、.pfx ファイルを見つけて、インターネットベースのクライアントを管理する Configuration Manager プライマリ サイト サーバー上の **C:\Certs** にそのコピーを配置します。 Certs フォルダーは、サーバー間で証明書を移動するときに使用する一時フォルダーです。 クラウド管理ゲートウェイを Azure にデプロイするときに、プライマリ サイト サーバーから証明書ファイルにアクセスします。  

証明書をプライマリ サイト サーバーにコピーした後、メンバー サーバー上の個人用証明書ストアから証明書を削除できます。

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Configuration Manager で Azure クラウド サービスを有効にする

Configuration Manager コンソールから Azure サービスを構成するには、Azure サービスの構成ウィザードを使用して、2 つの Azure Active Directory (Azure AD) アプリを作成します。  

- **サーバー アプリ**: Azure AD の *Web アプリ*  
- **クライアント アプリ**: Azure AD の *ネイティブ クライアント* アプリ  

プライマリ サイト サーバーから次の手順を実行します。  

1. プライマリ サイト サーバーから Configuration Manager コンソールを開き、 **[管理] > [クラウド サービス] > [Azure サービス]** の順に移動し、 **[Azure サービスの構成]** を選択します。  

   [Azure サービスの構成] ページで、構成しているクラウド管理サービスのフレンドリ名を指定します。 次に例を示します。*自分のクラウド管理サービス*。

   次に、 **[クラウド管理]** を選択してから **[次へ]** を選択します。  

   > [!TIP]  
   > ウィザードで行う構成の詳細については、「[Azure サービス ウィザードの起動](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard)」を参照してください。

2. **[アプリのプロパティ]** ページで、 **[Web アプリ]** の場合は **[参照]** を選択して **[サーバー アプリ]** ダイアログを開き、 **[作成]** を選択します。 次のフィールドを構成します。

   - **アプリケーション名**:「*クラウド管理 Web アプリ*」など、アプリのフレンドリ名を指定します。  

   - **ホームページ URL**:この値は Configuration Manager では使用されませんが、Azure AD で必要になります。 既定では、この値は `https://ConfigMgrService` です。  

   - **アプリ ID URI**:この値は、Azure AD テナント内で一意である必要があります。 サービスへのアクセスを要求するために Configuration Manager クライアントで使用されるアクセス トークンにあります。 既定では、この値は `https://ConfigMgrService` です。  

   次に **[サインイン]** を選択し、Azure AD 全体管理者アカウントを指定します。 これらの資格情報は Configuration Manager では保存されません。 この管理者には Configuration Manager のアクセス許可は必要ありません。また、Azure サービス ウィザードを実行するアカウントと同じものである必要もありません。

   サインインすると、結果が表示されます。 **[OK]** を選択して [サーバー アプリケーションの作成] ダイアログを閉じ、[アプリのプロパティ] ページに戻ります。

3. **[ネイティブ クライアント アプリ]** の場合は、 **[参照]** を選択して **[クライアント アプリ]** ダイアログを開きます。

4. **[作成]** を選択して **[クライアント アプリケーションの作成]** ダイアログを開き、次のフィールドを構成します。  

   - **アプリケーション名**:「*クラウド管理ネイティブ クライアント アプリ*」など、アプリのフレンドリ名を指定します。

   - **応答 URL**:この値は Configuration Manager では使用されませんが、Azure AD で必要になります。 既定では、この値は `https://ConfigMgrClient` です。
   次に **[サインイン]** を選択し、Azure AD 全体管理者アカウントを指定します。 Web アプリと同様に、これらの資格情報は保存されず、Configuration Manager のアクセス許可は必要ありません。

   サインインすると、結果が表示されます。 **[OK]** を選択して [クライアント アプリケーションの作成] ダイアログを閉じ、[アプリのプロパティ] ページに戻ります。 次に、 **[次へ]** を選択して続行します。

5. **[検出の設定の構成]** ページで **[Azure Active Directory ユーザーの探索を有効にする]** チェック ボックスをオンにし、 **[次へ]** を選択して、実際の環境に合わせて [検出] ダイアログの構成を完了します。  

6. [概要]、[進行状況]、および [完了] の各ページに進み、ウィザードを終了します。  

   Azure AD ユーザー探索の Azure サービスが Configuration Manager で有効になります。  ここではコンソールを開いたままにしておきます。  

7. ブラウザーを開いて [Azure portal](https://portal.azure.com/) にサインインします。  

8. **[すべてのサービス] > [Azure Active Directory] > [アプリの登録]** の順に選択し、次の手順を実行します。

   1. 作成した Web アプリを選択します。

   2. **[設定] > [必要なアクセス許可]** の順に移動し、 **[アクセス許可の付与]** を選択してから **[はい]** を選択します。  

   3. 作成したネイティブ クライアント アプリを選択します。

   4. **[設定] > [必要なアクセス許可]** の順に移動し、 **[アクセス許可の付与]** を選択してから **[はい]** を選択します。  

9. Configuration Manager コンソールで **[管理] > [クラウド サービス] > [Azure サービス]** の順に移動し、[Azure サービスの構成] を選択します。 次に **[Azure Active Directory ユーザー探索]** を右クリックし、 **[今すぐ完全な探索を実行する]** を選択します。 **[はい]** を選択して操作を確定します。  

10. プライマリ サイト サーバーで、Configuration Manager の **SMS_AZUREAD_DISCOVERY_AGENT.log** を開き、次のエントリを探して、探索が機能していることを確認します。*Azure Active Directory ユーザーの成功した UDX の公開*  

    既定では、ログファイルは *%Program_Files%\Microsoft Configuration Manager\Logs* にあります。  

## <a name="create-the-cloud-services-in-azure"></a>Azure でクラウド サービスを作成する

**チュートリアルのこのセクションでは、次の操作を行います**。

- CMG クラウド サービスを作成する  
- 両方のサービス用に DNS CNAME レコードを作成する  

### <a name="create-the-cmg"></a>CMG を作成する

この手順を使用して、クラウド管理ゲートウェイを Azure のサービスとしてインストールします。 CMG は階層の最上位層サイトにインストールされます。 このチュートリアルでは、証明書が登録およびエクスポートされたプライマリ サイトを引き続き使用します。

1. プライマリ サイト サーバー上で Configuration Manager コンソールを開き、 **[管理] > [概要] > [クラウド サービス] > [クラウド管理ゲートウェイ]** の順に移動し、 **[クラウド管理ゲートウェイの作成]** を選択します。  

2. **[全般]** ページで次の手順を実行します。  

   1. **[Azure 環境]** には実際のクラウド環境を選択します。 このチュートリアルでは、**AzurePublicCloud** を使用します。  

   2. **[Azure Resource Manager の展開]** を選択します。  
  
   3. Azure サブスクリプションに**サインイン**します。 Configuration Manager では、Configuration Manager に対して Azure クラウド サービスを有効にしたときに構成した情報に基づいて追加情報が入力されます。  

   **[次へ]** を選択して続行します。  

3. **[設定]** ページで、**ConfigMgrCloudMGServer.pfx** というファイルを参照して選択します。これは、CMG サーバー認証証明書のインポート後にエクスポートしたファイルです。 パスワードを指定すると、.pfx 証明書ファイルの詳細に基づいて、 **[サービス名]** と **[デプロイ名]** が自動的に入力されます。

4. **[リージョン]** を設定します。

5. **[リソース グループ]** には、既存のリソース グループを使用するか、**CofigMgrCloudServices** のようにスペースを使用しないフレンドリ名のグループを作成します。 グループの作成を選択した場合、そのグループは Azure のリソース グループとして追加されます。  

6. 大規模に構成する準備ができていない場合は、**VM インスタンス**の数に 1 を使用します。 VM インスタンスの数を指定することで、単一のクラウド管理ゲートウェイ (CMG) クラウド サービスをスケールアウトし、より多くのクライアント接続をサポートすることができます。 後で Configuration Manager コンソールを使用して、使用している VM インスタンスの数を取得し、編集できます。  

7. **[クライアント証明書の失効状態の検証]** のチェックボックスをオンにします。

8. CMG と共にクラウド配布ポイントを展開する場合は、 **[CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする]** のチェックボックスをオンにします。

9. **[次へ]** を選択して続行します。

10. **[アラート]** ページの値を確認して、 **[次へ]** を選択します。

11. **[概要]** ページを確認し、 **[次へ]** をクリックしてクラウド管理ゲートウェイ クラウド サービスを作成します。 **[閉じる]** を設定してウィザードを終了します。  

12. Configuration Manager コンソールのクラウド管理ゲートウェイ ノードで、新しいサービスを表示できるようになりました。  

### <a name="create-dns-cname-records"></a>DNS の CNAME レコードを作成する

CMG の DNS エントリを作成すると、社内ネットワークの内部と外部の両方で Windows 10 デバイスが名前解決を使用して Azure の CMG クラウド サービスを見つけることができるようになります。

この CNAME レコードの例では、次の詳細を使用します。  

- 会社名は **Contoso**、パブリック DNS 名前空間は ***Contoso.com*** です。  

- CMG サービス名は **MyCMG** です。これは、Azure では ***MyCMG.CloudApp.Net*** になります。  

CNAME レコードの例:*MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>CMG を使用するように管理ポイントとクライアントを構成する

オンプレミスの管理ポイントとクライアントがクラウド管理ゲートウェイを使用できるように設定を構成します。

ここではクライアント通信に拡張 HTTP を使用しているため、HTTPS 管理ポイントを使用する必要はありません。  

### <a name="create-the-cmg-connection-point"></a>CMG 接続ポイントを作成する

拡張 HTTP をサポートするようにサイトを構成します。  

1. Configuration Manager コンソールで、 **[管理] > [概要] > [サイトの構成] > [サイト]** の順に移動し、プライマリ サイトのプロパティを開きます。  

2. **[クライアント コンピューターの通信方法]** タブで、 **[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** に *[HTTPS または HTTP]* オプションを選択し、 **[OK]** を選択して構成を保存します。

    > [!Note]
    > バージョン 1906 以降では、このタブは **[通信のセキュリティ]** と呼ばれています。<!-- SCCMDocs#1645 -->  

3. 次に **[管理] > [概要] > [サイトの構成] > [サーバーとサイト システムの役割]** の順に移動し、クラウド管理ゲートウェイ接続ポイントをインストールする管理ポイントがあるサーバーを選択します。  

4. **[サイト システムの役割の追加]** を選択してから、 **[次へ]** >  **[次へ]** の順に選択します。  

5. **[クラウド管理ゲートウェイ接続ポイント]** を選択し、 **[次へ]** を選択して続行します。  

6. **[クラウド管理ゲートウェイ接続ポイント]** ページで既定の選択を確認し、正しい CMG が選択されていることを確認します。 複数のクラウド管理ゲートウェイがある場合は、ドロップダウン リストを使用して別の CMG を指定できます。 インストール後に、使用中の CMG を変更することもできます。 **[次へ]** を選択して続行します。

7. **[次へ]** を選択してインストールを開始してから、[完了] ページに結果を表示します。  **[閉じる]** を選択して接続ポイントのインストールを完了します。

8. 次に **[管理] > [概要] > [サイトの構成] > [サーバーとサイト システムの役割]** の順に移動し、接続ポイントをインストールした管理ポイントの **[プロパティ]** を開きます。 **[全般]** タブで、 **[Configuration Manager のクラウド管理ゲートウェイ トラフィックを許可する]** チェックボックスをオンにし、 **[OK]** を選択して構成を保存します。
   > [!TIP]  
   > 共同管理を有効にするには必須ではありませんが、ソフトウェアの更新ポイントについてもこれと同じ編集を行うことをお勧めします。

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>クライアントに CMG を使用するように指示するクライアント設定を構成する

CMG と通信するように Configuration Manager クライアントを構成するクライアント設定を使用します。  

1. **Configuration Manager コンソールを開き、[管理] > [概要] > [クライアント設定]** を選択し、 **[既定のクライアント設定]** を編集します。  

2. **[クラウド サービス]** を選択します。

3. **[既定の設定]** ページで、次の設定を **[はい]** に設定します。  

   - **新しい Windows 10 ドメインに参加しているデバイスを自動的に Azure Active Directory に登録する**  

   - **クライアントでクラウド管理ゲートウェイを使用できるようにする**

   - **クラウド配布ポイントへのアクセスを許可する**

4. **[クライアント ポリシー]** ページで、 **[インターネット クライアントからのユーザー ポリシー要求を有効にする]**  =  **[はい]** を設定します。

5. **[OK]** を選択して、この構成を保存します。

## <a name="enable-co-management-in-configuration-manager"></a>Configuration Manager で共同管理を有効にする

Azure 構成、サイト システムの役割、およびクライアント設定が適切に行われていると、Configuration Manager を構成して共同管理を有効にすることができます。 ただし、共同管理を有効にした後でも、このチュートリアルが完了する前に、Intune でいくつかの構成を行う必要があります。 このようなタスクの 1 つとして、Configuration Manager クライアントを展開するように Intune を構成する場合があります。 共同管理の構成ウィザード内から使用できるクライアント展開のコマンド ラインを保存することで、このタスクは簡単になります。 そのため、ここでは Intune の構成が完了する前に共同管理を有効にしています。

> [!TIP]
> - 共同管理を有効にすると、 *[パイロット グループ]* としてコレクションが割り当てられます。 これは、共同管理構成をテストするための少数のクライアントを含むグループです。 手順を開始する前に、適切なコレクションを作成することをお勧めします。 その後、それを行う手順を終了せずにコレクションを選択できます。
> - Configuration Manager バージョン 1906 以降では、各ワークロードに対して異なる "*パイロット グループ*" を割り当てることができるため、複数のコレクションが必要となる場合があります。

### <a name="enable-co-management-starting-in-version-1906"></a>バージョン 1906 以降での共同管理の有効化

Configuration Manager バージョン 1906 以降で共同管理を有効化するには、次の手順に従います。

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>バージョン 1902 以前での共同管理の有効化

Configuration Manager バージョン 1902 以前で共同管理を有効化するには、次の手順に従います。

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Intune を使用して Configuration Manager クライアントを展開する

Intune を使用して、現在 Intune でのみ管理されている Windows 10 デバイスに Configuration Manager クライアントをインストールできます。  

以前は管理されていなかった Windows 10 デバイスが Intune に登録されると、自動的に Configuration Manager クライアントがインストールされます。

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Configuration Manager クライアントをインストールするように Intune アプリを作成する

1. プライマリ サイト サーバーから [Azure portal](https://portal.azure.com/) にサインインし、 **[Intune] > [クライアント アプリ] > [アプリ] > [追加]** に移動します。

2. **[アプリの種類]** の場合:**基幹業務アプリ**を選択します。

3. **アプリ パッケージ ファイル**を選択してから、Configuration Manager ファイル **ccmsetup.msi** の場所を参照し、 **[開く] > [OK]** の順に選択します。
たとえば、*C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi* です

4. **[アプリ情報]** を選択してから、以下の詳細情報を指定します。
   - **説明**:Configuration Manager クライアント  

   - **[発行元]** : Microsoft  

   - **コマンドライン引数**: *\< **CCMSETUPCMD** コマンド行を指定します。共同管理の構成ウィザードの* [有効化] *ページから保存したコマンド ラインを使用できます。このコマンド ラインには、クラウド サービスの名前と、デバイスが Configuration Manager クライアント ソフトウェアをインストールできるようにする追加の値が含まれています。>*  

     コマンドライン構造は、CCMSETUPCMD および SMSSiteCode パラメーターのみを使用したこの例のようになります。  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > コマンド ラインを使用できない場合は、Configuration Manager コンソールで *CoMgmtSettingsProd* のプロパティを表示してコマンド ラインのコピーを取得できます。

5. **[OK] > [追加]** の順に選択します。  アプリが作成され、Intune コンソールで使用できるようになります。 アプリを使用できるようになったら、次のセクションを使用して Intune を Windows 10 デバイスに割り当てるように構成できます。

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Configuration Manager クライアントをインストールするように Intune アプリを割り当てる

次の手順では、前の手順で作成した Configuration Manager クライアントをインストールするためのアプリを展開します。

1. [Azure portal](https://portal.azure.com/) にサインインします。  **[すべてのサービス] > [Intune] > [クライアント アプリ] > [アプリ]** の順に選択し、Configuration Manager クライアントを展開するために作成したアプリである **[ConfigMgr Client Setup Bootstrap]\(ConfigMgr クライアント セットアップ ブートストラップ\)** を選択します。  

2. **[割り当て] > [グループの追加]** の順に選択します。  **[割り当ての種類]** を **[必須]** に設定し、 **[Included Groups]\(含まれるグループ\)** と **[Excluded Groups]\(除外されるグループ\)** を使用して、共同管理に参加させるユーザーとデバイスを含む Azure Active Directory (AD) グループを設定します。  

3. **[OK]** を選択して構成を **[保存]** します。
アプリは、割り当てるユーザーとデバイスに必要になりました。 アプリが Configuration Manager クライアントをデバイスにインストールした後は、共同管理によって管理されます。

## <a name="summary"></a>[概要]

このチュートリアルの構成手順を完了すると、デバイスの共同管理を開始できます。

## <a name="next-steps"></a>次のステップ

- [共同管理ダッシュ ボード](how-to-monitor.md)で、共同管理されているデバイスの状態を確認する
- [Windows Autopilot](quickstart-autopilot.md) を使用して新しいデバイスをプロビジョニングする
- [条件付きアクセス](quickstart-conditional-access.md)と Intune のコンプライアンス規則を使用して、企業リソースへのユーザー アクセスを管理する
