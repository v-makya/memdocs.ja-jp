---
title: CMG のセキュリティとプライバシー
titleSuffix: Configuration Manager
description: クラウド管理ゲートウェイを使用する場合のセキュリティとプライバシーに関するガイダンスおよび推奨事項について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: 1dd64404905df1452e45beda8610932db237410d
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715290"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>クラウド管理ゲートウェイのセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

この記事には、Configuration Manager クラウド管理ゲートウェイ (CMG) のセキュリティとプライバシーの情報が含まれています。 詳細については、「[クラウド管理ゲートウェイの計画](plan-cloud-management-gateway.md)」を参照してください。

## <a name="cmg-security-details"></a>CMG のセキュリティの詳細

CMG では、CMG 接続ポイントからの接続を受け入れ、管理します。 証明書と接続 ID を利用する相互認証を使用します。

CMG では次の方法を使用して、クライアント要求を受け入れて転送します。

- PKI ベースのクライアント認証証明書または Azure AD で相互 HTTPS を使用する接続を事前に認証します。

  - CMG VM インスタンスの IIS では、CMG にアップロードした信頼されたルート証明書に基づいて、証明書のパスを検証します。

  - 証明書の失効を有効にすると、VM インスタンス上の IIS でもクライアント証明書の失効が確認されます。 詳細については、「[証明書失効リストを発行する](#bkmk_crl)」を参照してください。

- 証明書信頼リスト (CTL) では、クライアント認証証明書のルートを確認します。 また、クライアントに対して、管理ポイントと同じ検証を実行します。 詳細については、「[サイトの証明書信頼リストのエントリを確認する](#bkmk_ctl)」を参照してください。

- クライアント要求 (URL) を検証し、フィルタリングして、CMG 接続ポイントで要求を処理できるかどうかを確認します。  

- 発行エンドポイントごとにコンテンツの長さを確認します。

- ラウンドロビン動作を使用して、同じサイトの CMG 接続ポイントの負荷を分散します。

CMG 接続ポイントでは次の方法を使用します。

- CMG のすべての VM インスタンスに対して、一貫性のある HTTPS/TCP 接続を構築します。 1 分ごとにこれらの接続を確認し、維持します。

- 証明書を利用する CMG による相互認証を使用します。

- URL マッピングに基づいて、クライアント要求を転送します。

- コンソールで接続の状態をレポートして、サービスの正常性状態を表示します。

- エンドポイント別のトラフィックを 5 分ごとにレポートします。

### <a name="configuration-manager-client-facing-roles"></a>Configuration Manager クライアントと直接接続する役割

管理ポイントおよびソフトウェアの更新ポイントは、クライアント要求を処理するために IIS のエンドポイントをホストします。 CMG ではすべての内部エンドポイントが公開されません。 CMG に発行されたすべてのエンドポイントに、URL マッピングがあります。

- 外部 URL は、CMG との通信にクライアントが使用する URL です。

- 内部 URL は、内部サーバーに要求を転送するときに使用する CMG 接続ポイントです。

#### <a name="url-mapping-example"></a>URL マッピングの例

管理ポイントの CMG トラフィックを有効にすると、各管理ポイント サーバーの URL マッピングの内部セットが Configuration Manager で作成されます。 たとえば、ccm_system、ccm_incoming、sms_mp が作成されます。 管理ポイント ccm_system のエンドポイントの外部 URL は、次のようになります。  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
この URL は、管理ポイントごとに一意となっています。 その後、Configuration Manager クライアントによって、CMG が有効な管理ポイント名がインターネット管理ポイントのリストに追加されます。 この名前は次のようになります。  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
サイトでは、発行されたすべての外部 URL が自動的に CMG にアップロードされます。 これで、CMG は URL をフィルタリングできます。 すべての URL マッピングは、CMG 接続ポイントにレプリケートされます。 その後、クライアント要求からの外部 URL に従って、内部サーバーに通信が転送されます。

## <a name="security-guidance-for-cmg"></a>CMG のセキュリティ ガイダンス

<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>証明書失効リストを発行する

インターネット ベースのクライアントがアクセスする PKI の証明書失効リスト (CRL) を発行します。 PKI を使用して CMG を展開する場合は、[設定] タブで**クライアント証明書の失効を検証する**ようにサービスを構成します。この設定で、発行された証明書失効リスト (CRL) を使用するようにサービスが構成されます。 詳細については、「[PKI 証明書失効の計画](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)」を参照してください。

この CMG オプションでは、クライアント認証証明書を検証します。

- クライアントが Azure AD 認証を使用している場合、CRL は関係ありません。

- PKI を使用し、CRL を外部に公開している場合は、このオプションを有効にします (推奨)。

- PKI を使用し、CRL を公開していない場合は、このオプションを無効にします。

- このオプションを誤って構成すると、クライアントから CMG への追加のトラフィックが発生する場合があり、 その追加のトラフィックにより、Azure の出力データが増加して、Azure のコストが増加する可能性があります。<!-- SCCMDocs#1434 -->

<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>サイトの証明書信頼リストのエントリを確認する

<!--503739-->
各 Configuration Manager サイトには、信頼されたルート証明機関のリスト、つまり、証明書信頼リスト (CTL) が含まれています。 リストを表示して変更するには、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** を選択します。 サイトを選択し、リボンの **[プロパティ]** を選択します。 **[Communication Security]\(通信のセキュリティ\)** タブに切り替えて、[信頼されたルート証明機関] の下にある **[設定]** を選択します。

> [!Note]
> 1902 以前のバージョンでは、このタブは **[クライアント コンピューターの通信方法]** という名前です。<!-- SCCMDocs#1645 -->

PKI クライアント認証を利用する CMG を持つサイトに対してより制限の厳しい CTL を使用します。 それ以外の場合、管理ポイントに既に存在する信頼されたルートで発行されたクライアント認証証明書を持つクライアントは、クライアント登録のために自動的に受け入れられます。

このサブセットでは、管理者はセキュリティをより詳細に制御できます。 CTL は、CTL の認証機関から発行されるクライアント証明書のみを受け入れるようにサーバーを制限します。 たとえば、Windows には、VeriSign や Thawte など、有名なサードパーティ証明機関 (CA) が数多く付属しています。 既定では、IIS を実行するコンピューターは、これらの有名な CA へチェーンされている証明書を信頼します。 IIS を CTL を使用して構成していない場合、これらの CA から発行されたクライアント証明書を持つコンピューターはどれも、有効な Configuration Manager クライアントとして受け入れられます。 IIS をこれらの CA を含んでいない CTL を使用して構成すると、証明書がこれらの CA へチェーンされている場合にクライアント接続が拒否されます。

### <a name="enforce-tls-12"></a><a name="bkmk_tls"></a>TLS 1.2 の強制

<!-- SCCMDocs-pr#4021 -->

バージョン 1906 以降では、CMG 設定を使用して **TLS 1.2 を強制**します。 これは、Azure クラウド サービス VM にのみ適用され、 オンプレミス Configuration Manager サイト サーバーまたはクライアントには適用されません。 TLS 1.2 の詳細については、「[TLS 1.2 を有効にする方法](../../../plan-design/security/enable-tls-1-2.md)」を参照してください。

### <a name="use-token-based-authentication"></a>トークンベースの認証を使用する

バージョン 2002 以降、<!--5686290--> Configuration Manager では、内部ネットワークに接続することがあまりなく、Azure AD に参加できず、PKI によって発行された証明書をインストールする方法を持たない、インターネット ベースのデバイスに対するサポートが拡張されています。 サイトからは、内部ネットワークに登録されているデバイスのトークンが自動的に発行されます。 インターネットベースのデバイス用の一括登録トークンを作成することができます。 詳細については、[CMG のトークンベースの認証](../../deploy/deploy-clients-cmg-token.md)に関する記事をご覧ください。<!-- SCCMDocs#2331 -->

## <a name="next-steps"></a>次のステップ

- [クラウド管理ゲートウェイの計画](plan-cloud-management-gateway.md)
- [Set up cloud management gateway](setup-cloud-management-gateway.md) (クラウド管理ゲートウェイの設定)
- [クラウド管理ゲートウェイについてよくあるご質問](cloud-management-gateway-faq.md)
- [クラウド管理ゲートウェイの証明書](certificates-for-cloud-management-gateway.md)
