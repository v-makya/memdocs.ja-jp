---
title: 拡張 HTTP
titleSuffix: Configuration Manager
description: 先進認証を使用して、PKI サーバー認証証明書を必要とせずにクライアント通信をセキュリティ保護します。
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79b4119a12826596fcc91fa1b4ead4e151e2ddd8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262100"
---
# <a name="enhanced-http"></a>拡張 HTTP

*適用対象:Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> この機能はバージョン 1806 で[プレリリース機能](../../servers/manage/pre-release-features.md)として初めて導入されました。 バージョン 1810 からは、この機能はプレリリース機能ではなくなりました。  

すべての Configuration Manager 通信パスで HTTPS 通信を使用することが推奨されていますが、PKI 証明書の管理のオーバーヘッドが原因で、一部の顧客にとっては、この使用が困難な課題になります。

Configuration Manager バージョン 1806 では、クライアントがシステム クライアントと通信する方法を強化しました。 これらの強化の主な目的は、以下の 2 つです。  

- PKI サーバー認証証明書を必要とせずに機密性のクライアント通信を保護できる。  

- クライアントは、ネットワーク アクセス アカウント、クライアント PKI 証明書、Windows 認証を必要とせずに、配布ポイントからコンテンツに安全にアクセスできる。  

他のすべてのクライアント通信は HTTP 経由で行われます。 拡張 HTTP は、クライアント通信またはサイト システムで HTTPS を有効にすることと同じではありません。<!-- SCCMDocs issue #1212 -->

> [!Note]  
> PKI 証明書は、以下の要件がある顧客にとっては引き続き有効なオプションです。  
>
> - すべてのクライアント通信が HTTPS 経由で行われる  
> - 署名インフラストラクチャの高度な制御
>
> また、既に PKI を使用している場合は、拡張 HTTP が有効になっている場合でも、IIS にバインドされている PKI 証明書が使用されます。



## <a name="scenarios"></a><a name="bkmk_scenario"></a> シナリオ

これらの強化によって、次のシナリオでの動作が向上しました。  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a> シナリオ 1:管理ポイントに対するクライアント

<!--1356889-->
サイトに対して拡張 HTTP を有効にすると、[Azure Active Directory (Azure AD) に参加しているデバイス](/azure/active-directory/devices/concept-azure-ad-join)と、[Configuration Manager によって発行されたトークン](../../clients/deploy/deploy-clients-cmg-token.md)を持つデバイスが、HTTP 用に構成された管理ポイントと通信できるようになります。 拡張 HTTP が有効になっていると、サイト サーバーによって管理ポイントに対する証明書が生成され、安全なチャネル経由での通信が可能になります。

> [!Note]  
> HTTPS 対応の管理ポイントは、このシナリオで使用する必要はありませんが、拡張 HTTP の使用に代わる手段としてサポートされています。 HTTPS 対応の管理ポイントの使い方の詳細については、「[HTTPS 用の管理ポイントを有効にする](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)」を参照してください。  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a> シナリオ 2:配布ポイントに対するクライアント

<!--1358228-->
ワークグループまたは Azure AD 参加済みクライアントは、HTTP 用に構成されている配布ポイントから安全なチャネル経由で、認証やコンテンツのダウンロードを行うことができます。 これらの種類のデバイスは、クライアント上の PKI 証明書を必要とせずに、HTTPS 用に構成された配布ポイントを使用して、認証やコンテンツのダウンロードを行うこともできます。 ワークグループまたは Azure AD 参加済みクライアントにクライアント認証証明書を追加するのは簡単ではありません。

この動作には、タスク シーケンスがブート メディア、PXE、またはソフトウェア センターから実行されている OS 展開シナリオが含まれます。 詳細については、「[ネットワーク アクセス アカウント](accounts.md#network-access-account)」を参照してください。<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a> シナリオ 3:Azure AD デバイス ID

<!--1358460-->
Azure AD 参加済みデバイスまたは[ハイブリッド Azure AD デバイス](/azure/active-directory/devices/concept-azure-ad-join-hybrid)は、サインインしている Azure AD ユーザーがいない場合、割り当てられているサイトと安全に通信できます。 現在は、デバイス中心のシナリオで CMG および管理ポイントを使用して認証を行うには、クラウドベースのデバイス ID で十分になりました。 (ユーザー中心のシナリオでは、ユーザー トークンがまだ必要です。)  


## <a name="features"></a>機能

次の Configuration Manager 機能は、拡張 HTTP をサポートしているか、必要としています。

- [クラウド管理ゲートウェイ](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [ネットワーク アクセス アカウントなしの OS の展開](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [新しいインターネットベースの Windows 10 デバイスの共同管理を有効にする](../../../comanage/tutorial-co-manage-new-devices.md)
- [メールによるアプリの承認](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [管理サービス](../../../develop/adminservice/overview.md)
- [最近接続されたコンソールを表示する](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> ソフトウェアの更新ポイントとそれに関連するシナリオでは、クライアントだけでなくクラウド管理ゲートウェイとのセキュリティで保護された HTTP トラフィックを常にサポートしてきました。 これには、証明書またはトークンベースの認証とは異なる管理ポイントによるメカニズムが使用されます。<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>[前提条件]  

- HTTP クライアント接続用に構成された管理ポイント。 管理ポイントのロール プロパティの **[全般]** タブで、このオプションを設定します。  

- HTTP クライアント接続用に構成された配布ポイント。 配布ポイントのロール プロパティの **[通信]** タブで、このオプションを設定します。 **[クライアントに匿名接続を許可する]** オプションを有効にしないでください。  

- クラウド管理のために、サイトを Azure AD にオンボードします。  

- " *[シナリオ 3](#bkmk_scenario3) のみ*":Windows 10 バージョン 1803 以降を実行していて、Azure AD に参加しているクライアント。 このクライアントでは Azure AD デバイス認証にこの構成が必要です。<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>サイトを構成する

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。 サイトを選択して、リボンの **[プロパティ]** を選択します。  

2. **[クライアント コンピューターの通信方法]** タブに切り替えます。

    > [!Note]
    > バージョン 1906 以降では、このタブは **[通信のセキュリティ]** と呼ばれています。<!-- SCCMDocs#1645 -->  

    **[HTTPS] または [HTTP]** のオプションを選択します。 **[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** オプションを有効にします。

> [!Tip]
> 管理ポイントがサイトから新しい証明書を受信して構成するまで、最大 30 分待機します。

<!--3798957-->
バージョン 1902 以降では、中央管理サイトに対して拡張 HTTP を有効にすることもできます。 これと同じプロセスを使用して、中央管理サイトのプロパティを開きます。 このアクションでは、中央管理サイトの SMS プロバイダーの役割に対してのみ拡張 HTTP が有効になります。 階層内のすべてのサイトに適用されるグローバルな設定ではありません。

Configuration Manager コンソールでこれらの証明書を確認できます。 **[管理]** ワークスペースに移動して、 **[セキュリティ]** を展開し、 **[証明書]** ノードを選択します。 SMS 発行ルートによって発行されたサイト サーバー ロール証明書と共に、**SMS 発行**ルート証明書を検索します。

この構成でクライアントが管理ポイントおよび配布ポイントと通信する方法の詳細については、「[クライアントからサイト システムとサービスへの通信](communications-between-endpoints.md#Planning_Client_to_Site_System)」をご覧ください。


## <a name="see-also"></a>関連項目

- [セキュリティの計画](../security/plan-for-security.md)  

- [構成マネージャー クライアントのセキュリティとプライバシー](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [セキュリティの構成](../security/configure-security.md)  

- [エンドポイント間の通信](communications-between-endpoints.md)  
