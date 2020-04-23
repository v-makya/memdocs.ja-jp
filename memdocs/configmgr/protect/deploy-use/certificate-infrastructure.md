---
title: 証明書インフラストラクチャの構成
titleSuffix: Configuration Manager
description: Configuration Manager で証明書の登録を構成する方法について説明します。
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fe34768de48f52dd4872a63ccf353fda1c691a44
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705800"
---
# <a name="configure-certificate-infrastructure"></a>証明書インフラストラクチャの構成

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の証明書インフラストラクチャについて説明します。 作業を始める前に、「[System Center Configuration Manager での証明書プロファイルの前提条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)」にある前提条件を確認してください。  

次の手順を使用し、SCEP のインフラストラクチャまたは PFX 証明書を構成します。

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>手順 1 - ネットワーク デバイス登録サービスおよび依存する要素をインストールして構成する (SCEP 証明書の場合のみ)

 Active Directory 証明書サービス (AD CS) 用のネットワーク デバイス登録サービスの役割サービスをインストールして構成し、証明書テンプレートのセキュリティ アクセスを変更し、公開キー基盤 (PKI) クライアント認証証明書を展開して、レジストリでインターネット インフォメーション サービス (IIS) の既定の URL サイズの制限を上げます。 必要に応じて、証明書の発行元証明機関 (CA) でカスタムの有効期限を使えるように構成します。  

> [!IMPORTANT]  
>  Configuration Manager でネットワーク デバイス登録サービスを構成して使用できるようにする前に、ネットワーク デバイス登録サービスがインストールおよび構成されていることを確認してください。 サービスに依存する要素が正しく動作しないと、Configuration Manager を使用して証明書登録のトラブルシューティングを実行するのが難しくなります。  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>ネットワーク デバイス登録サービスおよび依存する要素をインストールして構成するには  

1. Windows Server 2012 R2 を実行しているサーバーに、ネットワーク デバイス登録サービスの役割サービスをインストールし、Active Directory 証明書サービス サーバーの役割用に構成します。 詳細については、TechNet の Active Directory 証明書サービスの「 [Network Device Enrollment Service Guidance (ネットワーク デバイス登録サービス ガイド)](https://go.microsoft.com/fwlink/p/?LinkId=309016) 」を参照してください。  

2. 必要に応じて、ネットワーク デバイス登録サービスが使用している証明書テンプレートのセキュリティ アクセス許可を変更します。  

   -   Configuration Manager コンソールを実行するアカウントの場合: **[読み取り]** アクセス許可。  

        このアクセス許可は、証明書プロファイルの作成ウィザードを実行して、SCEP 設定プロファイルの作成に使用する証明書テンプレートを参照して選択するときに必要です。 証明書テンプレートを選択すると、ウィザードのページに設定値がいくつか自動的に挿入されます。そのため、手動で入力する手間が省けるだけでなく、ネットワーク デバイス登録サービスが使用している証明書テンプレートと適合しない設定を選択する危険性が低くなります。  

   -   ネットワーク デバイス登録サービスのアプリケーション プールで使用する SCEP サービス アカウントの場合: **[読み取り]** および **[登録]** のアクセス許可。  

        この要件は Configuration Manager に固有ではありませんが、ネットワーク デバイス登録サービスの構成に含まれます。 詳細については、TechNet の Active Directory 証明書サービスの「 [Network Device Enrollment Service Guidance (ネットワーク デバイス登録サービス ガイド)](https://go.microsoft.com/fwlink/p/?LinkId=309016) 」を参照してください。  

   > [!TIP]  
   >  どの証明書テンプレートをネットワーク デバイス登録サービスで使用しているかを調べるには、ネットワーク デバイス登録サービスを実行しているサーバーの次のレジストリ キーを表示します。HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP  

   > [!NOTE]  
   >  これらは、ほとんどの環境に適した既定のセキュリティ アクセス許可です。 ただし、別のセキュリティ構成を使用することもできます。 詳細については、[証明書プロファイルに関する証明書テンプレート アクセス許可の計画](../../protect/plan-design/planning-for-certificate-template-permissions.md)に関する記事を参照してください。  

3. このサーバーに、クライアント認証をサポートする PKI 証明書を展開します。 使用するコンピューターに、既に適切な証明書がインストールされている場合もあれば、この目的専用の証明書を展開しなければならない (または展開したい) 場合もあります。 この証明書の要件の詳細については、「[Configuration Manager での PKI 証明書の要件](../../core/plan-design/network/pki-certificate-requirements.md)」トピックの「**サーバー向け PKI 証明書**」セクションで、「ネットワーク デバイス登録サービスの役割サービスを含む Configuration Manager ポリシー モジュールを実行するサーバー」を参照してください。  

   > [!TIP]
   >  この証明書の展開について不明な点がある場合は、「[配布ポイント用のクライアント証明書の展開](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)」の手順を参照してください。次の 1 つの例外を除き、証明書の要件は同じです。  
   > 
   > - 証明書テンプレートのプロパティの **[要求処理]** タブにある **[プライベート キーのエクスポートを許可する]** チェック ボックスをオンにしないでください。  
   > 
   >   Configuration Manager ポリシー モジュールを構成するときにローカルのコンピューター ストアを参照して選択できるので、プライベート キーを使用してこの証明書をエクスポートする必要はありません。  

4. クライアント認証証明書が関連付けられているルート証明書を探します。 そのルート CA 証明書を証明書ファイル (.cer) にエクスポートします。 このファイルを、後で証明書登録ポイント サイト システム サーバーのインストールと構成を行うときに安全にアクセスできる場所に保存します。  

5. 同じサーバーでレジストリ エディターを使って IIS の既定の URL サイズの制限を上げます。このためには、HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters のレジストリ キー DWORD 値を次のように設定します。  

   - **MaxFieldLength** キーを **65534**に設定します。  

   - **MaxRequestBytes** キーを **16777216**に設定します。  

     詳細については、Microsoft サポート技術情報「[820129: Windows 用の Http.sys レジストリ設定](https://go.microsoft.com/fwlink/?LinkId=309013)」を参照してください。  

6. 同じサーバーでインターネット インフォーメーション サービス (IIS) マネージャーを開き、/certsrv/mscep アプリケーションの要求のフィルタリング設定を変更してサーバーを再起動します。 **[要求フィルター設定の編集]** ダイアログ ボックスの **[要求制限]** 設定は次のように設定されています。  

   - **許可されたコンテンツ最大長 (バイト)** : **30000000**  

   - **URL の最大長 (バイト)** : **65534**  

   - **クエリ文字列の最大長 (バイト)** : **65534**  

     これらの設定とその構成方法の詳細については、IIS リファレンス ライブラリの「 [Requests Limits (要求の制限)](https://go.microsoft.com/fwlink/?LinkId=309014) 」を参照してください。  

7. 使用している証明書テンプレートよりも有効期間が短い証明書を要求できるようにしたい場合があります。この設定は、エンタープライズ CA では既定で無効になっています。 エンタープライズ CA でこのオプションを有効にするには、次のように、Certutil コマンドライン ツールを使って設定を変更してから、証明書サービスをいったん停止して再開します。  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      詳細については、TechNet ライブラリの PKI Technologies セクションの「 [Certificate Services Tools and Settings (証明書サービスのツールと設定)](https://go.microsoft.com/fwlink/p/?LinkId=309015) 」を参照してください。  

8. **https://server.contoso.com/certsrv/mscep/mscep.dll** のようなリンクを使用して、ネットワーク デバイス登録サービスが動作していることを確認してください。 組み込まれているネットワーク デバイス登録サービスの Web ページが表示されるはずです。 この Web ページには、登録サービスの紹介と、ネットワーク デバイスが証明書要求を送信する URL の説明が記載されています。  

   ネットワーク デバイス登録サービスと依存する要素の構成が完了したら、証明書登録ポイントをインストールおよび構成することができます。


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>手順 2 - 証明書登録ポイントをインストールおよび構成する

Configuration Manager の階層に少なくとも 1 つの証明書登録ポイントをインストールして構成する必要があります。このサイト システムの役割は、中央管理サイトまたはプライマリ サイトにインストールできます。  

> [!IMPORTANT]  
>  証明書登録ポイントをインストールする前に、「[Configuration Manager のサポートされている構成](../../core/plan-design/configs/supported-configurations.md)」トピックの**サイト システム要件**に関するセクションで、証明書登録ポイントのオペレーティング システムの要件と依存関係を確認してください。  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>証明書登録ポイントをインストールおよび構成するには  

1. Configuration Manager コンソールで、 **[管理]** をクリックします。  

2. **[管理]** ワークスペースで **[サイトの構成]** を展開し、 **[サーバーとサイト システムの役割]** をクリックしてから、証明書登録ポイントに使用するサーバーを選択します。  

3. **[ホーム]** タブの **[サーバー]** グループで、 **[サイト システムの役割の追加]** をクリックします。  

4. **[全般]** ページで、サイト システムの全般設定を指定し、 **[次へ]** をクリックします。  

5. **[プロキシ]** ページで **[次へ]** をクリックします。 証明書登録ポイントでは、インターネット プロキシ設定を使用しません。  

6. **[システムの役割の選択]** ページで、利用可能な役割の一覧から **[証明書登録ポイント]** を選択してから、 **[次へ]** をクリックします。 

7. **証明書の登録モード** ページで、この証明書登録ポイントで **SCEP 証明書要求を処理する**のか、**PFX 証明書要求を処理する**のか選択します。 1 つの証明書登録ポイントで 2 種類の要求を処理することはできません。ただし、両方の種類の証明書を使用している場合、複数の証明書登録ポイントを作成できます。

   PFX 証明書を処理している場合、証明機関として Microsoft または Entrust のいずれかを選択する必要があります。

8. **[証明書登録ポイント設定]** ページは証明書の種類によって異なります。
   - **[SCEP 証明書要求を処理する]** を選択した場合、次を構成します。
     -   証明書登録ポイントの **[Web サイト名]** 、 **[HTTPS ポート番号]** 、 **[仮想アプリケーション名]** 。 これらのフィールドには既定値が自動的に入力されます。 
     -   **ネットワーク デバイス登録サービスの URL とルート CA 証明書** - **[追加]** をクリックし、 **[URL とルート証明機関証明書の追加]** ダイアログ ボックスで次を指定します。
         - **ネットワーク デバイス登録サービスの URL**: 次の形式で URL を指定します: https:// *<server_FQDN>* /certsrv/mscep/mscep.dll。 たとえば、ネットワーク デバイス登録サービスを実行しているサーバーの FQDN が server1.contoso.com の場合は、「 **https://server1.contoso.com/certsrv/mscep/mscep.dll** 」と入力します。
         - **ルート CA 証明書**: 「**手順 1: ネットワーク デバイス登録サービスおよび依存する要素をインストールして構成する**」で保存した証明書 (.cer) ファイルを参照して選択します。 このルート CA 証明書を使用すると、Configuration Manager ポリシー モジュールで使用するクライアント認証証明書が、証明書登録ポイントによって検証されます。  

   - **[PFX 証明書要求を処理する]** を選択した場合、選択した証明書機関の接続詳細と資格情報を構成します。

     - 証明書機関として Microsoft を利用するには、 **[追加]** をクリックし、 **[証明機関とアカウントを追加する]** ダイアログ ボックスで次を指定します。
         - **証明機関のサーバー名** - 証明機関サーバーの名前を入力します。
         - **証明機関アカウント** - **[設定]** をクリックし、証明機関のテンプレートで登録するアクセス許可が与えられているアカウントを選択するか、作成します。
         - **証明書登録ポイント接続アカウント** - 証明書登録ポイントを Configuration Manager データベースに接続するアカウントを選択するか、作成します。 あるいは、証明書登録ポイントをホストしているコンピューターのローカル コンピューター アカウントを利用できます。
         - **Active Directory 証明書の公開アカウント** - Active Directory のユーザー オブジェクトに証明書を公開するためのアカウントを選択するか、新規作成します。

         - **[URL for the Network Device Enrollment and root CA certificate]\(ネットワーク デバイス登録の URL とルート CA 証明書\)** ダイアログ ボックスで、次の項目を指定し、 **[OK]** をクリックします。  

     - 証明機関として Entrust を使用するには、次のように指定します。

       - **MDM Web サービス URL**
       - URL のユーザー名とパスワード資格情報

         MDM API を使用し、Entrust Web サービス URL を定義するとき、次のサンプルのように、API のバージョン 9 以降を使用してください。

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         それ以前のバージョンの API は Entrust に対応していません。

9. **[次へ]** をクリックして、ウィザードを完了します。  

10. インストールが完了するまで待ち、次のいずれかの方法を使用して、証明書登録ポイントが正常にインストールされたことを確認します。  

    -   **[監視]** ワークスペースで **[システムのステータス]** を展開し、 **[コンポーネントのステータス]** をクリックし、 **[SMS_CERTIFICATE_REGISTRATION_POINT]** コンポーネントからのステータス メッセージを参照します。  

    -   サイト システム サーバーで、 *<ConfigMgr インストール パス\>* \Logs\crpsetup.log ファイルおよび *<ConfigMgr インストール パス\>* \Logs\crpmsi.log ファイルを使用します。 インストールが成功した場合、0 の終了コードを返します。  

    -   ブラウザーを使用して、証明書登録ポイントの URL (https://server1.contoso.com/CMCertificateRegistration など) に接続できることを確認します。 アプリケーション名の **サーバー エラー** ページが開き、 HTTP 404 の説明が表示されます。  

11. 証明書登録ポイントが自動的に作成してエクスポートしたルート CA 証明書ファイルを、プライマリ サイト サーバー コンピューターの *<ConfigMgr Installation Path\>* \inboxes\certmgr.box フォルダーで見つけます。 ネットワーク デバイス登録サービスを実行しているサーバーに Configuration Manager ポリシー モジュールを後でインストールするときに安全にアクセスできる場所に、このファイルを保存します。  

    > [!TIP]  
    >  この証明書ファイルは、上に示されているフォルダー内にすぐに格納されません。 Configuration Manager がこの場所にファイルをコピーするまで、しばらく (30 分ほど) 待つ必要がある場合があります。  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>手順 3 - Configuration Manager ポリシー モジュールをインストールする (SCEP 証明書の場合のみ)

指定した各サーバーに、Configuration Manager ポリシー モジュールをインストールして構成する必要があります。これは、「**手順 2: 証明書登録ポイントをインストールおよび構成する**」で、証明書登録ポイントのプロパティに **[ネットワーク デバイス登録サービスの URL]** として指定したサーバーです。  

##### <a name="to-install-the-policy-module"></a>ポリシー モジュールをインストールするには  

1. ネットワーク デバイス登録サービスを実行するサーバーで、ドメイン管理者としてログオンし、次のファイルを Configuration Manager インストール メディアの <ConfigMgrInstallationMedia\>\SMSSETUP\POLICYMODULE\X64 フォルダーから一時フォルダーにコピーします。  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   さらに、インストール メディアのに LanguagePack フォルダーがある場合、そのフォルダーとフォルダーの内容をコピーします。  

2. 一時フォルダーから、PolicyModuleSetup.exe を実行して、Configuration Manager ポリシー モジュール セットアップ ウィザードを起動します。  

3. ウィザードの最初のページで **[次へ]** をクリックしてライセンス条項に同意し、 **[次へ]** ボタンをクリックします。  

4. **[インストール先フォルダー]** ページで、ポリシー モジュールの既定のインストール先フォルダーをそのまま使用するか、別のフォルダーを指定し、 **[次へ]** をクリックします。  

5. **[証明書登録ポイント]** ページで、サイト システム サーバーの FQDN と証明書登録ポイントのプロパティで指定した仮想アプリケーション名から成る、証明書登録ポイントの URL を指定します。 既定の仮想アプリケーション名は CMCertificateRegistration です。 たとえば、サイト システム サーバーの FQDN が server1.contoso.com で、既定の仮想アプリケーション名を使用した場合は、「 **https://server1.contoso.com/CMCertificateRegistration** 」と指定します。  

6. **[443]** という既定のポートをそのまま使用するか、証明書登録ポイントが使用する別のポート番号を指定して、 **[次へ]** をクリックします。  

7. **[ポリシー モジュールのクライアント証明書]** ページで、「**手順 1: ネットワーク デバイス登録サービスおよび依存する要素をインストールして構成する**」で展開したクライアント認証証明書を参照して指定し、 **[次へ]** をクリックします。  

8. **[証明書登録ポイント証明書]** ページで **[参照]** をクリックし、「**手順 2: 証明書登録ポイントをインストールおよび構成する**」の最後で見つけて保存した、ルート CA にエクスポートされた証明書ファイルを選択します。  

   > [!NOTE]  
   >  この証明書ファイルを以前に保存していない場合は、サイト サーバー コンピューターの <ConfigMgr インストール パス\>\inboxes\certmgr.box にあります。  

9. **[次へ]** をクリックして、ウィザードを完了します。  

   Configuration Manager ポリシー モジュールをアンインストールする場合は、コントロール パネルの **[プログラムと機能]** を使用します。 

 
これで構成手順が完了したので、証明書をユーザーやデバイスに展開できます。証明書をユーザーやデバイスに展開するには、証明書プロファイルを作成して展開します。 証明書プロファイルの作成方法の詳細については、[証明書プロファイルの作成方法](../../protect/deploy-use/create-certificate-profiles.md)に関する記事を参照してください。  
