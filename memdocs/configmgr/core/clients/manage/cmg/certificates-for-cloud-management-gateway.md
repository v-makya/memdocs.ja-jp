---
title: CMG 証明書
titleSuffix: Configuration Manager
description: クラウド管理ゲートウェイと共に使用するさまざまなデジタル証明書について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: b5a9a4a7f23942ac06dc16a0b54b657c7fd617a9
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715613"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>クラウド管理ゲートウェイの証明書

*適用対象:Configuration Manager (Current Branch)*

クラウド管理ゲートウェイ (CMG) でインターネット上のクライアントを管理するためのシナリオによっては、1 つまたは複数の次のデジタル証明書が必要になります。  

- [CMG サーバー認証証明書](#bkmk_serverauth)  
  - [クライアントが信頼する CMG のルート証明書](#bkmk_cmgroot)  
  - [パブリック プロバイダーが発行したサーバー認証証明書](#bkmk_serverauthpublic)  
  - [エンタープライズ PKI から発行されたサーバー認証証明書](#bkmk_serverauthpki)  

- [クライアント認証証明書](#bkmk_clientauth)
  - [CMG 接続ポイント](#bkmk_cmgcp)
  - [CMG が信頼するクライアントのルート証明書](#bkmk_clientroot)  

- [HTTPS 用の管理ポイントを有効にする](#bkmk_mphttps)  

- [Azure 管理証明書](#bkmk_azuremgmt)  

さまざまなシナリオに関する詳細については、「[クラウド管理ゲートウェイの計画](plan-cloud-management-gateway.md)」を参照してください。

## <a name="general-information"></a>一般情報

<!--SCCMDocs issue #779-->
クラウド管理ゲートウェイの証明書では、次の構成がサポートされています。  

- 2048 ビットまたは 4096 ビットのキーの長さ

- 証明書の秘密キーのキー記憶域プロバイダー。 詳細については、「[CNG certificates overview](../../../plan-design/network/cng-certificates-overview.md)」(CNG 証明書の概要) を参照してください。  

- ポリシー: **[システム暗号化: 暗号化、ハッシュ、署名のための FIPS 準拠アルゴリズムを使う]** を使用して Windows を構成した場合。  

- **TLS 1.2**。 詳細については、「[TLS 1.2 を有効にする方法](../../../plan-design/security/enable-tls-1-2.md)」を参照してください。  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a> CMG サーバー認証証明書

*この証明書はすべてのシナリオで必要です。*

Configuration Manager コンソールで CMG を作成するとき、この証明書を提供します。

CMG によって、インターネットベースのクライアントが接続する HTTPS が作成されます。 サーバーには、安全なチャネルを構築するためにサーバー認証証明書が必要になります。 パブリック プロバイダーからこの目的で証明書を取得するか、公開キー基盤 (PKI) から証明書を発行します。 詳細については、[クライアントが信頼する CMG のルート証明書](#bkmk_cmgroot)に関するページを参照してください。

> [!NOTE]
> CMG サーバー認証証明書でワイルドカードがサポートされます。 一部の証明書機関は、ホスト名にワイルドカード文字を使用して証明書を発行します。 たとえば、`*.contoso.com` となります。 ワイルドカード証明書を利用して PKI を簡素化し、保守管理コストを下げる組織もあります。<!--491233-->  
>
> CMG でワイルドカード証明書を使用する方法の詳細については、「[CMG を設定する](setup-cloud-management-gateway.md#set-up-a-cmg)」を参照してください。<!--SCCMDocs issue #565-->  

この証明書には、Azure のサービスを識別するために、一意の名前が必要になります。 証明書を要求する前に、希望する Azure ドメイン名が一意であることを確認します。 たとえば、*GraniteFalls.CloudApp.Net* にします。

1. [Azure portal](https://portal.azure.com) にサインインします。
1. **[すべてのリソース]** を選択してから、 **[追加]** を選択します。
1. **[クラウド サービス]** を検索します。 **[作成]** を選択します。
1. **[DNS 名]** フィールドに希望するプレフィックス (たとえば、*GraniteFalls*) を入力します。 ドメイン名が使用できるか、既に別のサービスで使用されているかがインターフェイスに表示されます。

    > [!Important]  
    > ポータルではサービスを作成しないでください。名前を利用できるかどうかはこのプロセスを利用して確認してください。

コンテンツに対して CMG も有効にする場合は、CMG サービス名が一意の Azure ストレージ アカウント名であることも確認します。 CMG クラウド サービス名が一意で、ストレージ アカウント名は一意でない場合、Configuration Manager は Azure でサービスをプロビジョニングできません。 Azure portal で、以下の変更を加えて上記のプロセスを繰り返します。

- **[ストレージ アカウント]** を検索します
- **[ストレージ アカウント名]** フィールドで名前をテストします

たとえば、DNS 名のプレフィックス (たとえば、*GraniteFalls*) は 3 から 24 文字の長さにする必要があり、使用できるのは英数字のみです。 ダッシュ (`-`) などの特殊文字を使用することはできません。<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a> クライアントが信頼する CMG のルート証明書

クライアントは、CMG サーバー認証証明書を信頼する必要があります。 この信頼は、次の 2 つの方法で実現できます。

- グローバルで信頼されているパブリック証明書プロバイダーの証明書を利用します。 たとえば、DigiCert、Thawte、VeriSign です。この 3 つに限らず他にも存在します。 Windows クライアントには、このようなプロバイダーからの信頼されたルート CA (証明書機関) が含まれています。 このようなプロバイダーのいずれかが発行したサーバー認証証明書を利用することで、クライアントは自動的にそれを信頼します。  

- 公開キー基盤 (PKI) からのエンタープライズ CA によって発行された証明書を利用します。 ほとんどのエンタープライズ PKI 実装によって、Windows クライアントに信頼されたルート CA が追加されます。 たとえば、Active Directory 証明書サービスとグループ ポリシーを使用します。 クライアントによって自動的に信頼されない CA から CMG サーバー認証証明書を発行する場合は、CA の信頼されたルート証明書をインターネットベースのクライアントに追加します。  

  - Configuration Manager 証明書プロファイルを使用し、クライアントで証明書をプロビジョニングすることもできます。 詳細については、「[証明書プロファイルの概要](../../../../protect/deploy-use/introduction-to-certificate-profiles.md)」をご覧ください。

  - [Intune から Configuration Manager クライアントをインストール](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)する予定がある場合は、Intune の証明書プロファイルを使用してクライアントに証明書をプロビジョニングすることもできます。 詳細については、[証明書プロファイルの構成](../../../../../intune/protect/certificates-configure.md)に関するページを参照してください。

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a> パブリック プロバイダーが発行したサーバー認証証明書

サード パーティの証明書プロバイダーは、CloudApp.net の証明書を作成できません。これは、そのドメインが Microsoft によって所有されているためです。 自分が所有するドメインに対して発行された証明書のみを取得できます。 サード パーティ プロバイダーから証明書を取得する主な理由は、クライアントがそのプロバイダーのルート証明書を既に信頼していることにあります。

次のプロセスで DNS エイリアスを作成します。

1. 組織のパブリック DNS で正規名レコード (CNAME) を作成します。 このレコードによって、パブリック証明書で使用するフレンドリ名に CMG のエイリアスが作成されます。

    たとえば、Contoso は CMG に **GraniteFalls** と名前を付けています。 この名前は Azure では **GraniteFalls.CloudApp.Net** になります。 Contoso 社のパブリック DNS である contoso.com 名前空間内に DNS 管理者が、実際のホスト名 **GraniteFalls.CloudApp.net** に対する **GraniteFalls.Contoso.com** 用の新しい CNAME レコードを作成します。  

2. CNAME エイリアスの共通名 (CN) を使用してパブリック プロバイダーからのサーバー認証証明書を要求します。
たとえば、Contoso 社では、証明書の CN 用に **GraniteFalls.Contoso.com** を使用しています。  

3. この証明書を利用し、Configuration Manager コンソールで CMG を作成します。 クラウド管理ゲートウェイの作成ウィザードの **[設定]** ページで:  

    - このクラウド サービスのサーバー証明書を (**証明書ファイル**から) 追加すると、ウィザードによって、サービス名として証明書 CN からホスト名が抽出されます。  

    - その後、**cloudapp.net** または Azure 米国政府クラウドの **usgovcloudapp.net** にサービス FQDN としてそのホスト名が追加され、Azure でサービスが作成されます。  

    - たとえば、Contoso が CMG を作成すると、Configuration Manager によって証明書 CN からホスト名 **GraniteFalls** が抽出されます。 Azure によって、**GraniteFalls.CloudApp.net** として実際のサービスが作成されます。  

Configuration Manager で CMG インスタンスを作成する場合、証明書には GraniteFalls.Contoso.com が含まれますが、Configuration Manager によって抽出されるものはホスト名 (GraniteFalls など) のみです。 このホスト名は CloudApp.net に追加されます。Azure でクラウド サービスを作成する際には、このドメインが必要となります。 Contoso.com ドメインの DNS 名前空間内の CNAME エイリアスにより、これらの 2 つの FQDN がまとめてマップされます。 Configuration Manager により、この CMG にアクセスするためのポリシーがクライアントに提供されます。DNS マッピングによってこれが結び付けられ、Azure のサービスに安全にアクセスできるようになります。<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a> エンタープライズ PKI から発行されたサーバー認証証明書

クラウド配布ポイントの場合と同じように、CMG のカスタム SSL 証明書を作成します。 次の操作以外は、「[クラウドベースの配布ポイント用のサービス証明書の展開](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)」の指示に従います。

- カスタム Web サーバー証明書を要求するとき、証明書の共通名の FQDN を提供します。 この名前は、自分が所有するパブリック ドメイン名でも、cloudapp.net ドメインでもかまいません。 独自のパブリック ドメインを使用する場合は、組織のパブリック DNS に DNS エイリアスを作成するための上記のプロセスを参照してください。  

- CMG Web サーバー証明書用の cloudapp.net パブリック ドメインを使用する場合:  

  - Azure パブリック クラウドでは、**cloudapp.net** で終わる名前を使用します。  

  - Azure 米国政府クラウドの **usgovcloudapp.net** で終わる名前を使用します。  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a> クライアント認証証明書

クライアント認証証明書の要件:

- この証明書は、Windows 8.1 を稼働しているインターネットベースのクライアント、および Azure Active Directory (Azure AD) に参加していない Windows 10 デバイスに必要です。
- これは、CMG 接続ポイントで必要な場合があります。 詳細については、「[CMG 接続ポイント](#bkmk_cmgcp)」を参照してください。
- Azure AD に参加している Windows 10 クライアントには必要ありません。
- サイトがバージョン 2002 以降の場合、デバイスではサイトから発行されたトークンを使用できます。 詳細については、[CMG のトークンベースの認証](../../deploy/deploy-clients-cmg-token.md)に関する記事をご覧ください。

クライアントはこの証明書を利用し、CMG で認証します。 ハイブリッドであるか、クラウド ドメインに参加している Windows 10 デバイスは、Azure AD を利用して認証するため、この証明書を必要としません。

この証明書は Configuration Manager と前後関係のないところでプロビジョニングします。 たとえば、Active Directory 証明書サービスとグループ ポリシーを使用し、クライアント認証証明書を発行します。 詳細については、「[Windows コンピューター用のクライアント証明書の展開](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)」を参照してください。

> [!NOTE]
> デバイスを Azure AD に参加させることをお勧めします。 インターネットベースのデバイスでは、Azure AD を使用して、Configuration Manager での認証を行うことができます。 また、デバイスがインターネット上にあるか、内部ネットワークに接続されているかにかかわらず、デバイスとユーザーの両方のシナリオに対応できます。 詳細については、「[Azure AD の ID を使用してクライアントをインストールして登録する](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)」を参照してください。
>
> バージョン 2002 以降、<!--5686290--> Configuration Manager では、内部ネットワークに接続することがあまりなく、Azure AD に参加できず、PKI によって発行された証明書をインストールする方法を持たない、インターネット ベースのデバイスに対するサポートが拡張されています。 詳細については、[CMG のトークンベースの認証](../../deploy/deploy-clients-cmg-token.md)に関する記事をご覧ください。

### <a name="cmg-connection-point"></a><a name="bkmk_cmgcp"></a> CMG 接続ポイント

クライアント要求を安全に転送するには、CMG 接続ポイントに管理ポイントとのセキュリティで保護された接続が必要です。 デバイスと管理ポイントの構成方法に応じて、CMG 接続ポイントの構成が決まります。

- 管理ポイントが HTTPS である

  - クライアントには、クライアント認証証明書があります。CMG 接続ポイントでは、HTTPS 管理ポイント上のサーバー認証証明書に対応するクライアント認証証明書が必要です。

  - クライアントには、Azure AD 認証または Configuration Manager トークンが使用されます。この証明書は必須ではありません。

- 拡張 HTTP 用に管理ポイントを構成する場合:この証明書は必須ではありません。

詳細については、「[HTTPS 用の管理ポイントを有効にする](#bkmk_mphttps)」を参照してください。

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a> CMG が信頼するクライアントのルート証明書

*この証明書は、クライアント認証証明書を利用するときに必要です。すべてのクライアントで認証に Azure AD を使用するとき、この証明書は必要ありません。*

Configuration Manager コンソールで CMG を作成するとき、この証明書を提供します。

CMG はクライアント認証証明書を信頼する必要があります。 この信頼を実現するには、信頼されたルート証明書チェーンを提供します。 証明書チェーンには必ずすべての証明書を追加します。 たとえば、クライアント認証証明書が中間 CA によって発行されている場合は、中間 CA 証明書とルート CA 証明書の両方を追加します。

> [!NOTE]  
> CMG を作成するときに、[設定] ページで信頼されたルート証明書を指定する必要はなくなりました。 クライアント認証で Azure AD を使用するときにこの証明書は必要ありませんが、ウィザードで必要な場合は使用されます。 PKI クライアント認証証明書を使用する場合は、引き続き信頼されたルート証明書を CMG に追加する必要があります。<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> バージョン 1902 以前で追加できるのは、2 つの信頼されたルート CA と 4 つの中間 (下位) CA のみです。

#### <a name="export-the-client-certificates-trusted-root"></a>クライアント証明書の信頼されたルートをエクスポートする

クライアント認証証明書をコンピューターに発行したら、そのコンピューターでこのプロセスを使用し、信頼されたルートをエクスポートします。

1. [スタート] メニューを開きます。 [ファイル名を指定して実行] ウィンドウに "run" と入力します。 `mmc` を開きます。  

2. [ファイル] メニューで **[スナップインの追加と削除]** を選択します。  

3. [スナップインの追加と削除] ダイアログ ボックスで、 **[証明書]** を選択し、 **[追加]** を選択します。  

    1. [証明書スナップイン] ダイアログ ボックスで、 **[コンピューター アカウント]** を選択してから **[次へ]** を選択します。  

    1. [コンピューターの選択] ダイアログ ボックスで **[ローカル コンピューター]** を選択し、 **[完了]** を選択します。  

    1. [スナップインの追加と削除] ダイアログ ボックスで、 **[OK]** を選択します。  

4. **[証明書]** を展開し、 **[個人用]** を展開し、 **[証明書]** を選択します。  

5. その使用目的が **[クライアント認証]** の証明書を選択します。  

    1. [操作] メニューから **[開く]** を選択します。  

    1. **[証明のパス]** タブに移動します。  

    1. チェーンの 1 つ上の証明書を選択し、 **[証明書の表示]** を選択します。  

6. この新しい証明書ダイアログ ボックスで、 **[詳細]** タブに移動します。 **[ファイルにコピー]** を選択します。  

7. 既定の証明書形式である **DER encoded binary X.509 (.CER)** を使用して証明書のエクスポート ウィザードを完了します。 エクスポートした証明書の名前と場所をメモします。  

8. 元のクライアント認証証明書の証明パスですべての証明書をエクスポートします。 エクスポートされた証明書のうち、中間 CA である証明書と信頼されたルート CA である証明書をメモします。  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a> HTTPS 用の管理ポイントを有効にする

この証明書は Configuration Manager と前後関係のないところでプロビジョニングします。 たとえば、Active Directory 証明書サービスとグループ ポリシーを使用し、Web サーバー証明書を発行します。 詳細については、「[PKI 証明書の要件](../../../plan-design/network/pki-certificate-requirements.md)」と「[IIS を実行するサイト システム用の Web サーバー証明書の展開](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)」を参照してください。

**[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** サイト オプションを使用するときは、管理ポイントは HTTP でもかまいません。 詳細については、「[Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md)」(拡張 HTTP) をご覧ください。

> [!TIP]
> 拡張 HTTP を使用しておらず、環境内に複数の管理ポイントがある場合、CMG 用にそれらをすべて HTTPS 対応にする必要はありません。 CMG 対応管理ポイントを **[インターネットのみ]** として構成します。 オンプレミスのクライアントはこれらを使用しなくなります。<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>管理ポイント用の拡張 HTTP 証明書

拡張 HTTP を有効にすると、サイト サーバーは、ルート SMS 発行証明書によって発行される **SMS ロール SSL 証明書**という名前の自己署名証明書を生成します。 管理ポイントによって、この証明書は、ポート 443 にバインドされている IIS の既定の Web サイトに追加されます。

### <a name="management-point-client-connection-mode-summary"></a>管理ポイントのクライアント接続モードの概要

これらの表は、クライアントの種類とサイトのバージョンに応じて、管理ポイントで HTTP または HTTPS が必要かどうかをまとめたものです。

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>クラウド管理ゲートウェイと通信するインターネットベースのクライアントの場合

次のクライアント接続モードを使用して、CMG からの接続を許可するように、オンプレミスの管理ポイントを構成します。

| クライアントの種類   | 管理ポイント |
|------------------|------------------|
| ワークグループ        | E-HTTP<sup>[注 1](#bkmk_note1)</sup>、HTTPS |
| AD ドメイン参加済み | E-HTTP<sup>[注 1](#bkmk_note1)</sup>、HTTPS |
| Azure AD 参加済み  | E-HTTP、HTTPS |
| ハイブリッド参加済み    | E-HTTP、HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **注 1**:この構成では、クライアントに[クライアント認証証明書](#bkmk_clientauth)が必要で、デバイス中心のシナリオのみがサポートされます。  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>オンプレミスの管理ポイントと通信するオンプレミスのクライアントの場合

次のクライアント接続モードを使用して、オンプレミスの管理ポイントを構成します。

| クライアントの種類   | 管理ポイント |
|------------------|------------------|
| ワークグループ        | HTTP、HTTPS |
| AD ドメイン参加済み | HTTP、HTTPS |
| Azure AD 参加済み  | HTTPS       |
| ハイブリッド参加済み    | HTTP、HTTPS |

> [!NOTE]  
> AD ドメイン参加済みのクライアントは、HTTP または HTTPS の管理ポイントと通信するデバイス中心のシナリオとユーザー中心のシナリオの両方をサポートします。  
>
> Azure AD 参加済みのクライアントとハイブリッド参加済みのクライアントは、デバイス中心のシナリオでは HTTP 経由で通信できますが、ユーザー中心のシナリオを有効にするには、E-HTTP または HTTPS が必要です。 そうでない場合、これらのクライアントはワークグループ クライアントと同じように動作します。  

#### <a name="legend-of-terms"></a>用語の凡例

- *ワークグループ*:デバイスはドメインまたは Azure AD に参加していませんが、[クライアント認証証明書](#bkmk_clientauth)を持っています。
- *AD ドメイン参加済み*:デバイスをオンプレミスの Active Directory ドメインに参加させます。
- *Azure AD 参加済み*:クラウド ドメイン参加済みとも呼ばれ、デバイスを Azure AD テナントに参加させます。 詳細については、「[Azure AD 参加済みデバイス](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join)」を参照してください。
- *ハイブリッド参加済み*:デバイスをオンプレミスの Active Directory に参加させ、Azure AD に登録します。 詳細については、「[ハイブリッド Azure AD 参加済みデバイス](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid)」を参照してください。
- *HTTP*:管理ポイント プロパティで、クライアント接続を **[HTTP]** に設定します。
- *HTTPS*:管理ポイント プロパティで、クライアント接続を **[HTTPS]** に設定します。
- *E-HTTP*:サイトのプロパティの **[Communication Security]\(通信のセキュリティ\)** タブで、サイト システムの設定を **[HTTPS または HTTP]** に設定し、 **[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** のオプションを有効にします。 HTTP 用の管理ポイントはご自身で構成します。HTTP と HTTPS の両方の通信用の HTTP 管理ポイントは用意されています (トークン認証のシナリオ)。

    > [!Note]
    > 1902 以前のバージョンでは、このタブは **[クライアント コンピューターの通信方法]** という名前です。<!-- SCCMDocs#1645 -->

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a> Azure 管理証明書

*この証明書は従来のサービス展開に必要です。Azure Resource Manager の展開には必要ありません。*

> [!Important]  
> バージョン 1810 以降では、Configuration Manager での Azure の従来のサービス展開は推奨されていません。 クラウド管理ゲートウェイ用の Azure Resource Manager の展開の使用を開始します。 詳細については、[CMG の計画](plan-cloud-management-gateway.md#azure-resource-manager)に関するページを参照してください。
>
> Configuration Manager バージョン 1902 以降、クラウド管理ゲートウェイの新しいインスタンスに対しては、Azure Resource Manager が唯一の展開メカニズムです。 この証明書は、Configuration Manager バージョン 1902 以降では必須ではありません。<!-- 3605704 -->

この証明書は Azure Portal で、また、Configuration Manager コンソールで CMG を作成するときに提供します。

Azure で CMG を作成するには、Configuration Manager サービス接続ポイントは最初に Azure サブスクリプションに認証する必要があります。 従来のサービス展開を使用すると、この認証に Azure 管理証明書が使用されます。 Azure 管理者はこの証明書をサブスクリプションにアップロードします。 Configuration Manager コンソールで CMG を作成するとき、この証明書を提供します。

管理証明書をアップロードする方法の詳細と手順については、Azure のドキュメントの次の記事を参照してください。

- [クラウド サービスと管理証明書](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Azure サービス管理証明書をアップロードする](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> 管理証明書に関連付けられているサブスクリプション ID を必ずコピーしてください。 Configuration Manager コンソールで CMG を作成するために使用します。

## <a name="next-steps"></a>次のステップ

- [Set up cloud management gateway](setup-cloud-management-gateway.md) (クラウド管理ゲートウェイの設定)  

- [クラウド管理ゲートウェイについてよくあるご質問](cloud-management-gateway-faq.md)  

- [クラウド管理ゲートウェイのセキュリティとプライバシー](security-and-privacy-for-cloud-management-gateway.md)  
