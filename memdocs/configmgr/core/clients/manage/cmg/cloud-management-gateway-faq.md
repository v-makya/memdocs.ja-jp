---
title: CMG についてよくあるご質問
titleSuffix: Configuration Manager
description: この記事を使用して、クラウド管理ゲートウェイについてよくあるご質問に回答します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 2bd3824df18ecdf426720a99db8720ef4b678733
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694930"
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


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a>ユーザー アカウントは、CMG クラウド サービスをホストするサブスクリプションに関連するテナントと同じ Azure AD テナントにある必要がありますか。
<!--SCCMDocs-pr issue #2873-->
環境内に複数のサブスクリプションがある場合は、Azure クラウド サービスをホストできる任意のサブスクリプションに CMG をデプロイできます。 

この質問は、次のシナリオで共通です。  

- 個別のテストおよび実稼働の Active Directory と Azure AD 環境はあるが、集中管理の Azure ホスティング サブスクリプションが 1 つしかない  

- Azure の使用がさまざまなチームにわたって有機的に増加している  

Resource Manager デプロイを使用している場合、サブスクリプションに関連付けられている Azure AD テナントをオンボードします。 この接続により、Configuration Manager が Azure への認証を行い、CMG の作成、デプロイ、管理ができるようになります。  

CMG 経由で管理されているユーザーとデバイスに対して Azure AD Authentication を使用している場合は、その Azure AD テナントをオンボードします。 クラウド管理用の Azure サービスの詳細については、[Azure サービスの構成](../../../servers/deploy/configure/azure-services-wizard.md)に関するページを参照してください。 各 Azure AD テナントをオンボードすると、ホスティング場所に関係なく、1 つの CMG で Azure AD Authentication を複数のテナントに提供することができます。

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>CMG には VPN 経由で接続されているクライアントに対してどのような影響がありますか?

VPN を使用してお客様の環境に接続しているローミング クライアントは、一般に、イントラネット接続として検出されます。 それらは、管理ポイントや配布ポイントなど、オンプレミスのインフラストラクチャへの接続を試みます。 一部のお客様は、VPN 経由で接続する場合でも、これらのローミング クライアントがクラウド サービスによって管理されるのを好みます。 バージョン 1902 以降では、CMG を境界グループに関連付けます。 この操作により、これらのクライアントでは強制的にオンプレミスのサイト システムが使われなくなります。 詳細については、[境界グループの構成](setup-cloud-management-gateway.md#configure-boundary-groups)に関するページを参照してください。

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>CMG を有効にした場合、クライアントがイントラネットに接続されるとき、クライアントは CMG が有効な管理ポイントだけに接続されるのでしょうか?

CMG 経由で送信される機密情報のトラフィックをセキュリティで保護するには、HTTPS 管理ポイントを構成するか、拡張 HTTP を使います。

CMG を展開し、CMG が有効な管理ポイントでの HTTPS 通信に PKI 証明書を使う場合は、管理ポイントのプロパティで**インターネット専用クライアントを許可する**オプションを選択します。 この設定により、内部クライアントで引き続き環境内の HTTP 管理ポイントが使われることが保証されます。

拡張 HTTP を使う場合は、この設定を構成する必要はありません。 クライアントでは、CMG が有効な管理ポイントに直接通信するときに、引き続き HTTP が使われます。 詳細については、「[Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md)」(拡張 HTTP) をご覧ください。

## <a name="next-steps"></a>次のステップ

- [クラウド管理ゲートウェイの計画](plan-cloud-management-gateway.md)
- [Set up cloud management gateway](setup-cloud-management-gateway.md) (クラウド管理ゲートウェイの設定)
- [クラウド管理ゲートウェイの証明書](certificates-for-cloud-management-gateway.md)
- [クラウド管理ゲートウェイのセキュリティとプライバシー](security-and-privacy-for-cloud-management-gateway.md)
- [クラウド管理ゲートウェイのサイズとスケールの数値](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
