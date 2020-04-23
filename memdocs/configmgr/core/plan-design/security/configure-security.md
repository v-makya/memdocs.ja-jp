---
title: セキュリティの構成
titleSuffix: Configuration Manager
description: Configuration Manager のセキュリティ関連オプションを構成します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701410"
---
# <a name="configure-security-in-configuration-manager"></a>Configuration Manager でセキュリティを構成する

*適用対象:Configuration Manager (Current Branch)*

この記事に含まれる情報は、Configuration Manager のセキュリティ関連オプションの設定に役立ちます。 次のセキュリティ オプションが含まれます。
- クライアント PKI 証明書のための[クライアント コンピューター通信](#BKMK_ConfigureClientPKI)  
- [署名と暗号化](#BKMK_ConfigureSigningEncryption)  
- [役割に基づいた管理](#BKMK_ConfigureRBA)  
- [アカウントの管理](#BKMK_ManageAccounts)  
- [Azure Active Directory の構成](#bkmk_azuread)  
- [SMS プロバイダー認証の構成](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> クライアント PKI 証明書の設定の構成  

インターネット インフォメーション サービス (IIS) を使用するサイト システムへのクライアント接続に公開キー基盤 (PKI) 証明書を使用する場合、次の手順に従ってこれらの証明書の設定を構成します。  

#### <a name="to-configure-client-pki-certificate-settings"></a>クライアント PKI 証明書の設定を構成するには  

1.  Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。 構成するプライマリ サイトを選択します。  

2.  リボンで、 **[プロパティ]** を選択します。 次に、 **[クライアント コンピューターの通信方法]** タブに切り替えます。  

    > [!Note]
    > バージョン 1906 以降では、このタブは **[通信のセキュリティ]** と呼ばれています。<!-- SCCMDocs#1645 -->  

3.  IIS を使用するサイト システムの設定を選択します。  

    - **HTTPS のみ**:サイトに割り当てられているクライアントが IIS を使用するサイト システムに接続するときに、常にクライアント PKI 証明書を使用します。  

    - **HTTPS または HTTP**:PKI 証明書の使用をクライアントに要求しません。  

    - **HTTP サイト システムには Configuration Manager によって生成された証明書を使用する**:この設定に関する詳細については、「[拡張 HTTP](../hierarchy/enhanced-http.md)」を参照してください。  

4.  クライアント コンピューターの設定を選択します。  

    - **使用可能な場合はクライアント PKI 証明書 (クライアント認証機能) を使用する**:サイト サーバー設定に **[HTTPS または HTTP]** を選択した場合、このオプションを選択し、HTTP 接続にクライアント PKI 証明書を使用します。 クライアントは、サイト システムに対する認証に、自己署名入り証明書ではなく、この証明書を使用します。 **[HTTPS のみ]** を選択すると、このオプションが自動的に選択されます。  

    クライアントで有効な PKI クライアント証明書が複数使用できるときは、 **[変更]** を選択し、クライアント証明書選択方法を構成します。  

    クライアント証明書の選択方法の詳細については、「[PKI クライアント証明書の選択の計画](plan-for-security.md#BKMK_PlanningForClientCertificateSelection)」を参照してください。  

    - **サイト システムの証明書失効リスト (CRL) をチェックする**:クライアントに対してこの設定を有効にし、取り消されている証明書がないか、組織の CRL で確認します。  

    クライアントの CRL チェックの詳細については、「[PKI 証明書失効の計画](plan-for-security.md#BKMK_PlanningForCRLs)」を参照してください。  

5.  信頼されているルート証明機関の証明書をインポート、表示、削除するには、 **[設定]** を選択します。  

    詳細については、「[PKI 信頼されたルート証明書と証明書発行者リストの計画](plan-for-security.md#BKMK_PlanningForRootCAs)」を参照してください。  


階層内のすべてのプライマリ サイトで、この手順を繰り返します。  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> 署名と暗号化の構成  

サイト内のすべてのクライアントがサポートすることができるサイト システムに、最も安全な署名設定と暗号化設定を構成します。 これらの設定が特に重要になるのが、自己署名入り証明書を使用してクライアントが HTTP 経由でサイト システムと通信する場合です。  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>サイトに署名と暗号化を構成するには  

1.  Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。 構成するプライマリ サイトを選択します。  

2.  リボンで **[プロパティ]** を選択し、 **[署名および暗号化]** タブに切り替えます。  

    このタブは、プライマリ サイトでのみ使用できます。 **[署名および暗号化]** タブが表示されない場合、中央管理サイトまたはセカンダリ サイトに接続されていないことを確認してください。  

3.  サイトと通信するクライアントに対して署名と暗号化のオプションを構成します。  

    - **署名を必要とする**:管理ポイントに送信する前に、クライアントによってデータに署名されます。  

    - **SHA-256 を必要とする**:データに署名するとき、クライアントで SHA-256 アルゴリズムが使用されます。  

    > [!WARNING]  
    >  **[SHA-256 を必要とする]** を選択する場合、このハッシュ アルゴリズムがすべてのクライアントでサポートされていることを先に確認してください。 今後サイトに割り当てられる可能性があるクライアントについても確認してください。  
    >   
    >  このオプションを選択するとき、自己署名証明書が与えられたクライアントで SHA-256 をサポートできない場合、Configuration Manager によって自己署名証明書が拒否されます。 SMS_MP_CONTROL_MANAGER コンポーネントによってメッセージ ID 5443 がログに記録されます。  

    - **暗号化を使用する**:管理ポイントに送信する前に、クライアントによってクライアント インベントリ データと状態メッセージが暗号化されます。 3DES アルゴリズムが使用されます。  

階層内のすべてのプライマリ サイトで、この手順を繰り返します。  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> 役割に基づいた管理の構成  

役割に基づいた管理では、セキュリティ ロール、セキュリティ スコープ、および割り当てられたコレクションを組み合わせて、各管理ユーザーの管理スコープを定義します。 スコープには、ユーザーがコンソールで表示できるオブジェクトと、実行許可が与えられたオブジェクトに関連付けられているタスクが含まれます。 役割に基づいた管理の構成は、階層内の各サイトに適用されます。  

詳細については、「[役割に基づいた管理の構成](../../servers/deploy/configure/configure-role-based-administration.md)」を参照してください。 この記事には次のアクションの詳細があります。  

- カスタム セキュリティ ロールの作成  

- セキュリティ ロールの構成  

- オブジェクトのセキュリティ スコープの構成  

- セキュリティを管理するコレクションの構成  

- 新しい管理ユーザーの作成  

- 管理ユーザーの管理スコープの変更  

> [!IMPORTANT]  
>  独自の管理スコープでオブジェクトと設定を定義し、別の管理ユーザーの役割に基づいた権限を構成するときに、これらのオブジェクトと設定を割り当てることができます。 ロールベース管理を計画する方法については、[ロール ベース管理の基礎](../../understand/fundamentals-of-role-based-administration.md)に関するページを参照してください。  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a> Configuration Manager で使用されるアカウントの管理  

Configuration Manager は、Windows アカウントのさまざまなタスクとユーザーをサポートしています。 さまざまなタスク用に構成されているアカウントを表示し、各アカウントについて Configuration Manager が使用するパスワードを管理するには、次の手順に従います。  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Configuration Manager で使用されるアカウントを管理するには  

1.  Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[セキュリティ]** を展開して **[アカウント]** ノードを選択します。  

2.  アカウントのパスワードを変更するには、一覧からそのアカウントを選択します。 リボンで **[プロパティ]** を選択します。  

3.  **[設定]** を選択し、 **[Windows ユーザー アカウント]** ダイアログ ボックスを開きます。 このアカウントに使用する Configuration Manager に新しいパスワードを指定します。  

    > [!NOTE]  
    >  指定するパスワードは、Active Directory にあるこのアカウントのパスワードと一致する必要があります。  

詳細については、「[System Center Configuration Manager で使用されるアカウント](../hierarchy/accounts.md)」を参照してください。



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a> Azure Active Directory の構成

Configuration Manager と Azure Active Directory (Azure AD) を統合し、ご利用の環境を簡素化し、クラウド対応にします。 Azure AD を利用し、サイトとクライアントの認証を有効にします。 詳細については、[Azure サービスの構成](../../servers/deploy/configure/azure-services-wizard.md)に関するページの**クラウド管理**サービスに関するセクションを参照してください。



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a> SMS プロバイダー認証の構成

バージョン 1810 以降では、Configuration Manager サイトにアクセスする管理者の最低限の認証レベルを指定することができます。 この機能では、Windows にサインインする管理者には必要なレベルを持つことが強制されます。 詳細については、「[SMS プロバイダーの計画](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)」を参照してください。 <!--1357013-->  



## <a name="see-also"></a>関連項目

- [セキュリティの計画](plan-for-security.md)  

- [構成マネージャー クライアントのセキュリティとプライバシー](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [エンドポイント間の通信](../hierarchy/communications-between-endpoints.md)  

- [暗号化コントロールのテクニカル リファレンス](cryptographic-controls-technical-reference.md)  

- [PKI 証明書の要件](../network/pki-certificate-requirements.md)  
