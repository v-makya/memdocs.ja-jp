---
title: CMG についてよくあるご質問
titleSuffix: Configuration Manager
description: この記事を使用して、クラウド管理ゲートウェイについてよくあるご質問に回答します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: ecc91168cc90af58c40903ea3d288eeaa82be7a0
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502240"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>クラウド管理ゲートウェイについてよくあるご質問

*適用対象:Configuration Manager (Current Branch)*

この記事では、クラウド管理ゲートウェイについてよくあるご質問に回答します。 詳細については、「[クラウド管理ゲートウェイの計画](plan-cloud-management-gateway.md)」を参照してください。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="what-certificates-do-i-need"></a>どの証明書が必要ですか?

詳細については、「[クラウド管理ゲートウェイの証明書](certificates-for-cloud-management-gateway.md)」を参照してください。

### <a name="do-i-need-azure-expressroute"></a>Azure ExpressRoute は必要ですか?

いいえ。 [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) では、Microsoft クラウドにオンプレミス ネットワークを拡張することができます。 Configuration Manager クラウド管理ゲートウェイでは、ExpressRoute などの仮想ネットワーク接続は必要ありません。 クラウド管理ゲートウェイの設計では、インターネット ベースのクライアントは、Azure サービス経由でオンプレミス サイト システムと通信を行うことができます。追加のネットワーク構成は必要ありません。 詳細については、「[クラウド管理ゲートウェイの計画](plan-cloud-management-gateway.md)」を参照してください。

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Azure 仮想マシンを維持する必要がありますか?

維持する必要はありません。 クラウド管理ゲートウェイの設計では、PaaS (サービスとしてのプラットフォーム) として Azure が使用されます。 指定されたサブスクリプションを使用して、Configuration Manager では必要な仮想マシン (VM)、ストレージ、ネットワークを作成します。 Azure は仮想マシンをセキュリティで保護し、更新します。 IaaS (サービスとしてのインフラストラクチャ) と同様に、これらの VM はオンプレミス環境には含まれません。 クラウド管理ゲートウェイは、クラウドに Configuration Manager 環境を拡張する PaaS です。 詳しくは、「[PaaS デプロイをセキュリティで保護する](/azure/security/security-paas-deployments)」をご覧ください。

### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>サービス更新中にサービスの継続性を確保する方法を教えてください

CMG をスケーリングして 2 つ以上のインスタンスを含めることにより、Azure の更新ドメインのベネフィットを自動的に得られます。 「[クラウド サービスの更新方法](/azure/cloud-services/cloud-services-update-azure-service)」をご覧ください。

### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>既に IBCM を使用しています。 CMG を追加した場合、クライアントはどのように動作しますか?

[インターネット ベースのクライアント管理](../plan-internet-based-client-management.md) (IBCM) を既に展開している場合は、クラウド管理ゲートウェイを展開することもできます。 クライアントは両方のサービスのポリシーを受け取ります。 インターネットへのローミング時に、これらのインターネット ベースのサービスのいずれかをランダムに選択して使用します。

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a> ユーザー アカウントは、CMG クラウド サービスをホストするサブスクリプションに関連付けられているテナントと同じ Azure AD テナント内にある必要がありますか?
<!--SCCMDocs-pr issue #2873-->
いいえ。CMG は、Azure クラウド サービスをホストできる任意のサブスクリプションにデプロイできます。

用語を明確にします。

- "_テナント_" は、ユーザー アカウントとアプリの登録のディレクトリです。 1 つのテナントは、複数のサブスクリプションを持つことができます。
- "_サブスクリプション_" によって、請求先、リソース、およびサービスが分けられます。 これは 1 つのテナントに関連付けられます。

この質問は、次のシナリオで共通です。  

- テストと実稼働用に個別の Active Directory および Azure AD 環境があるが、一元化された 1 つの Azure ホスティング サブスクリプションを使用している。

- Azure の使用がさまざまなチームにわたって有機的に増加している

Resource Manager デプロイを使用している場合、サブスクリプションに関連付けられている Azure AD テナントをオンボードします。 この接続により、Configuration Manager が Azure への認証を行い、CMG の作成、デプロイ、管理ができるようになります。  

CMG 経由で管理されているユーザーとデバイスに対して Azure AD Authentication を使用している場合は、その Azure AD テナントをオンボードします。 クラウド管理用の Azure サービスの詳細については、[Azure サービスの構成](../../../servers/deploy/configure/azure-services-wizard.md)に関するページを参照してください。 各 Azure AD テナントをオンボードすると、ホスティング場所に関係なく、1 つの CMG で Azure AD Authentication を複数のテナントに提供することができます。

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>例 1:複数のサブスクリプションを持つ 1 つのテナント

ユーザー ID、デバイスの登録、アプリの登録が、すべて同じテナント内にあります。 お客様は、CMG で使用するサブスクリプションを選択できます。 複数の CMG サービスを、1 つのサイトから別々のサブスクリプションにデプロイできます。 サイトとテナントは、一対一の関係にあります。 お客様は、請求先や論理的な分離など、さまざまな理由によってどのサブスクリプションを使用するかを決定します。

#### <a name="example-2-multiple-tenants"></a>例 2:複数のテナント

言い換えると、お客様の環境に複数の Azure AD がある場合です。 両方のテナントでユーザーとデバイスの ID をサポートする必要がある場合は、サイトを各テナントに接続する必要があります。 このプロセスには、テナントにアプリの登録を作成するために、各テナントの管理者アカウントが必要です。 その後、1 つのサイトで、複数のテナントで CMG サービスをホストできます。 いずれかのテナントで使用可能な任意のサブスクリプションに CMG を作成できます。 いずれかの Azure AD に参加しているデバイス、または Hybrid Azure AD Join を使用したデバイスで、CMG を使用できます。

ユーザーとデバイスの ID が 1 つのテナント内にあっても、CMG のサブスクリプションが別のテナント内にある場合は、サイトを両方のテナントに接続する必要があります。 技術的には、CMG サービスのみが含まれている 2 番目のテナントにはクライアント アプリは必要ありません。 クライアント アプリでは、CMG サービスを使用するクライアントに対してのみ、ユーザーとデバイスの認証が提供されます。<!-- SCCMDocs#1902 -->

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>CMG には VPN 経由で接続されているクライアントに対してどのような影響がありますか?

VPN を使用してお客様の環境に接続しているローミング クライアントは、一般に、イントラネット接続として検出されます。 それらは、管理ポイントや配布ポイントなど、オンプレミスのインフラストラクチャへの接続を試みます。 一部のお客様は、VPN 経由で接続する場合でも、これらのローミング クライアントがクラウド サービスによって管理されるのを好みます。 バージョン 1902 以降では、CMG を境界グループに関連付けます。 この操作により、これらのクライアントでは強制的にオンプレミスのサイト システムが使われなくなります。 詳細については、[境界グループの構成](setup-cloud-management-gateway.md#configure-boundary-groups)に関するページを参照してください。

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>CMG を有効にした場合、クライアントがイントラネットに接続されるとき、クライアントは CMG が有効な管理ポイントだけに接続されるのでしょうか?

CMG 経由で送信される機密情報のトラフィックをセキュリティで保護するには、HTTPS 管理ポイントを構成するか、拡張 HTTP を使います。

CMG を展開し、CMG が有効な管理ポイントでの HTTPS 通信に PKI 証明書を使う場合は、管理ポイントのプロパティで**インターネット専用クライアントを許可する**オプションを選択します。 この設定により、内部クライアントで引き続き環境内の HTTP 管理ポイントが使われることが保証されます。

拡張 HTTP を使う場合は、この設定を構成する必要はありません。 クライアントでは、CMG が有効な管理ポイントに直接通信するときに、引き続き HTTP が使われます。 詳細については、「[Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md)」(拡張 HTTP) をご覧ください。

### <a name="what-are-the-differences-with-client-authentication-between-azure-ad-and-certificates"></a>Azure AD と証明書のクライアント認証にはどのような違いがありますか?
<!-- MEMDocs#277 -->
デバイスの CMG サービスに対する認証には、Azure AD または[クライアント認証証明書](certificates-for-cloud-management-gateway.md#bkmk_clientauth)を使用できます。

Active Directory ドメインに参加している ID を使用して従来の Windows クライアントを管理する場合は、通信チャネルをセキュリティで保護するために PKI 証明書が必要です。 これらのクライアントには、Windows 8.1 と Windows 10 を含めることができます。 CMG でサポートされているすべての機能を使用できますが、ソフトウェアの配布はデバイスのみに制限されます。 デバイスがインターネットにローミングする前に Configuration Manager クライアントをインストールするか、バージョン 2002 以降では、トークン認証を使用します。

また、Azure AD との混種または単種のクラウド ドメイン参加のいずれかで、最新の ID を使用して Windows 10 クライアントを管理することもできます。 クライアントでは、PKI 証明書ではなく、Azure AD が認証に利用されます。 Azure AD を利用する場合、複雑な PKI システムより設定、構成、保守管理が簡単です。 同じ管理アクティビティとユーザーへのソフトウェアの配布をすべて実行できます。 また、リモート デバイスにクライアントをインストールするための追加の方法も有効になります。

デバイスを Azure AD に参加させることをお勧めします。 インターネットベースのデバイスでは、Azure AD を使用して、Configuration Manager での認証を行うことができます。 また、デバイスがインターネット上にあるか、内部ネットワークに接続されているかにかかわらず、デバイスとユーザーの両方のシナリオに対応できます。 詳細については、「[Azure AD の ID を使用してクライアントをインストールして登録する](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)」を参照してください。

## <a name="next-steps"></a>次のステップ

- [クラウド管理ゲートウェイの計画](plan-cloud-management-gateway.md)
- [Set up cloud management gateway](setup-cloud-management-gateway.md) (クラウド管理ゲートウェイの設定)
- [クラウド管理ゲートウェイの証明書](certificates-for-cloud-management-gateway.md)
- [クラウド管理ゲートウェイのセキュリティとプライバシー](security-and-privacy-for-cloud-management-gateway.md)
- [クラウド管理ゲートウェイのサイズとスケールの数値](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
