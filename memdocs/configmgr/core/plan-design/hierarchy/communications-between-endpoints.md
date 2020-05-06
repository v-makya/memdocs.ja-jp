---
title: エンドポイント間の通信
titleSuffix: Configuration Manager
description: ネットワーク経由で Configuration Manager サイト システムとコンポーネントがどのように通信するかを説明します。
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f60d268e1f9bfad9c062041e810be2092da5508
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587237"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Configuration Manager でのエンドポイント間の通信

*適用対象:Configuration Manager (Current Branch)*

この記事では、ネットワーク経由で Configuration Manager サイト システムとクライアントがどのように通信するかを説明します。 次のセクションが含まれています。  

- [サイト内のサイト システム間の通信](#Planning_Intra-site_Com)  
  - [サイト サーバーから配布ポイントへ](#bkmk_site2dp)  

- [クライアントからサイト システムとサービスへの通信](#Planning_Client_to_Site_System)  
  - [クライアントから管理ポイントへの通信](#bkmk_client2mp)  
  - [クライアントから配布ポイントへの通信](#bkmk_client2dp)  
  - [インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](#BKMK_clientspan)  

- [複数の Active Directory フォレスト間での通信](#Plan_Com_X-Forest)  
  - [ご使用のサイト サーバーのフォレストによって信頼されていないフォレスト内のドメイン コンピューターのサポート](#bkmk_noforesttrust)  
  - [ワークグループ内のコンピューターのサポート](#bkmk_workgroup)  
  - [複数のドメインとフォレストにまたがるサイトまたは階層をサポートするシナリオ](#bkmk_span)  

## <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a> サイト内のサイト システム間の通信  

Configuration Manager サイト システムまたはコンポーネントがサイト内の他のサイト システムまたはコンポーネントとネットワークを介して通信する場合、サイトの構成方法に応じて次のいずれかのプロトコルが使用されます。  

- サーバー メッセージ ブロック (SMB)  

- HTTP  

- HTTPS  

サイト サーバーから配布ポイントへの通信を除き、サイト内のサーバー同士がいつ通信するかは決まっていません。 これらの通信では、ネットワーク帯域幅を制御するためのメカニズムを使用しません。 サイト システム間の通信は制御できないので、高速で接続良好なネットワークがある場所にサイト システム サーバーを設置してください。  

### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a> サイト サーバーから配布ポイントへ

サイト サーバーから配布ポイントへのコンテンツの転送を管理するには、次の方法を使用します。  

- 配布ポイントで使用するネットワーク帯域幅とスケジュールを構成します。 この構成は、サイト間通信のアドレスの構成とよく似ています。 リモート ネットワークへのコンテンツの転送が、使用可能な帯域幅に大きく影響する場合に、別の Configuration Manager サイトをインストールする代わりに、この構成を使用します。  

- 配布ポイントを、事前設定済み配布ポイントにすることができます。 配布ポイント サーバーに手動で配置したコンテンツを使用できるので、ネットワークを介してコンテンツ ファイルを転送する必要がなくなります。  

詳細については、「[コンテンツ管理でのネットワーク帯域幅の管理](manage-network-bandwidth.md)」を参照してください。

## <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a> クライアントからサイト システムとサービスへの通信

クライアントはサイト システムの役割、Active Directory Domain Services、およびオンライン サービスへの通信を開始します。 これらの通信を有効にするには、ファイアウォールがクライアントと通信のエンドポイント間のネットワーク トラフィックを許可する必要があります。 これらのエンドポイントへの通信時に、クライアントで使用されるポートとプロトコルの詳細については、「[Configuration Manager で使用されるポート](ports.md)」を参照してください。  

クライアントは、サイト システムの役割と通信する前に、サービスの場所を使用して、クライアントのプロトコル (HTTP または HTTPS) をサポートする役割を検索します。 既定では、クライアントは次のように使用可能な最も安全な方法を使用します。 詳細については、[クライアントがサイト リソースやサービスを検索する方法](understand-how-clients-find-site-resources-and-services.md)に関するページを参照してください。  

HTTPS を使用するには、次のいずれかのオプションを構成します。  

- 公開キー基盤 (PKI) を使用し、クライアントとサーバーに PKI 証明書をインストールします。 証明書の使用方法については、[PKI 証明書の要件](../network/pki-certificate-requirements.md)に関するページをご覧ください。  

- バージョン 1806 以降では、**HTTP サイト システム用に Configuration Manager で生成された証明書を使用する**ようにサイトを構成します。 詳細については、「[Enhanced HTTP](enhanced-http.md)」(拡張 HTTP) をご覧ください。  

インターネット インフォメーション サービス (IIS) を使用し、クライアントからの通信をサポートするサイト システムの役割を展開する場合は、そのサイト システムにクライアントが接続するときに HTTP と HTTPS のどちらを使用するかを指定する必要があります HTTP を使用する場合は、署名と暗号化のオプションについても検討してください。 詳細については、「[署名と暗号化の計画](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption)」をご覧ください。  

### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a> クライアントから管理ポイントへの通信

クライアントが管理ポイントと通信するときには、認証 (トランスポート) と承認 (メッセージ) の 2 つの段階があります。 このプロセスは、次の要因によって異なります。

- サイトの構成:HTTPS のみ、HTTP または HTTPS を許可、HTTP または HTTPS を許可し拡張 HTTP が有効
- 管理ポイントの構成:HTTPS または HTTP
- デバイス中心のシナリオのデバイス ID
- ユーザー中心のシナリオのユーザー ID

次の表を使用して、このプロセスのしくみを理解してください。  

| MP の種類  | クライアント認証  | クライアント認証<br>デバイス ID  | クライアント認証<br>ユーザー ID  |
|----------|---------|---------|---------|
| HTTP     | 匿名<br>拡張 HTTP を使用すると、サイトで Azure AD の*ユーザー*または*デバイス*のトークンが検証されます。 | 場所の要求:匿名<br>クライアント パッケージ:匿名<br>登録、次のいずれかの方法を使用して、デバイス ID を証明します。<br> - 匿名 (手動で承認)<br> - Windows 統合認証<br> - Azure AD *デバイス* トークン (拡張 HTTP)<br>登録後、クライアントはメッセージの署名を使用してデバイス ID を証明します。 | ユーザー中心のシナリオの場合、次のいずれかの方法を使用してユーザー ID を証明します。<br> - Windows 統合認証<br> - Azure AD *ユーザー* トークン (拡張 HTTP) |
| HTTPS    | 次のいずれかの方法を使用します。<br> - PKI 証明書<br> - Windows 統合認証<br> -Azure AD *ユーザー* トークンまたは*デバイス* トークン | 場所の要求:匿名<br>クライアント パッケージ:匿名<br>登録、次のいずれかの方法を使用して、デバイス ID を証明します。<br> - 匿名 (手動で承認)<br> - Windows 統合認証<br> - PKI 証明書<br> -Azure AD *ユーザー* トークンまたは*デバイス* トークン<br>登録後、クライアントはメッセージの署名を使用してデバイス ID を証明します。 | ユーザー中心のシナリオの場合、次のいずれかの方法を使用してユーザー ID を証明します。<br> - Windows 統合認証<br> - Azure AD *ユーザー* トークン |

> [!Tip]  
> さまざまなデバイス ID の種類の管理ポイントの構成の詳細、およびクラウド管理ゲートウェイの使用の詳細については、「[HTTPS 用の管理ポイントを有効にする](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)」を参照してください。  

### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a> クライアントから配布ポイントへの通信

クライアントが配布ポイントと通信するときに、コンテンツをダウンロードする前に認証するだけで済みます。 次の表を使用して、このプロセスのしくみを理解してください。

| DP の種類  | クライアント認証  |
|----------|---------|
| HTTP     | - 匿名 (許可されている場合)<br>- コンピューター アカウントまたはネットワーク アクセス アカウントを使用した Windows 統合認証<br> - コンテンツ アクセス トークン (拡張 HTTP) |
| HTTPS    | - PKI 証明書<br> - コンピューター アカウントまたはネットワーク アクセス アカウントを使用した Windows 統合認証<br> - コンテンツ アクセス トークン |

### <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a> インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項

詳細については、以下の記事を参照してください。

- [クラウド管理ゲートウェイの計画](../..//clients/manage/cmg/plan-cloud-management-gateway.md)

- [インターネット ベースのクライアント管理の計画](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a> 複数の Active Directory フォレスト間での通信  

Configuration Manager では、複数の Active Directory フォレストにまたがるサイトや階層がサポートされます。 また、サイト サーバーと同じ Active Directory フォレストにはないドメイン コンピューターや、ワークグループのコンピューターもサポートされます。  

### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a> ご使用のサイト サーバーのフォレストによって信頼されていないフォレスト内のドメイン コンピューターのサポート

- サイト情報をその Active Directory フォレストに発行するオプションを使用して、信頼されていないフォレストにサイト システムの役割をインストールします。  

- これらのコンピューターを、ワークグループ コンピューターであるかのように管理します。  

信頼されていない Active Directory フォレストにサイト システム サーバーをインストールすると、そのフォレストのクライアントからのクライアントとサーバー間の通信はフォレスト内で保たれ、Configuration Manager が Kerberos 方式でコンピューターを認証できるようになります。 クライアントのフォレストにサイト情報を発行した場合は、クライアントは、利用可能な管理ポイントのリストなどのサイト情報を、割り当て済み管理ポイントからダウンロードする代わりに、Active Directory フォレストから取得できるという利点があります。  

> [!NOTE]  
> インターネット上のデバイスを管理したい場合は、サイト システム サーバーが Active Directory フォレストにあるときは、インターネット ベースのサイト システムの役割を境界ネットワークにインストールできます。 この場合は、境界ネットワークとサイト サーバーのフォレスト間に双方向の信頼関係は必要ありません。  

### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a> ワークグループ内のコンピューターのサポート  

- サイト システムの役割への HTTP クライアント接続を使用するときに、ワークグループのコンピューターを手動で承認します。 Configuration Manager では Kerberos を使用してこれらのコンピューターを認証することはできません。  

- これらのコンピューターが配布ポイントからコンテンツを取得できるように、ネットワーク アクセス アカウントを使用するようにワークグループ クライアントを構成します。  

- ワークグループ クライアントが管理ポイントを検索するための代替手段を提供します。 DNS または WINS にサイト データを発行する方法と、管理ポイントを直接割り当てる方法があります。 これらのクライアントは Active Directory Domain Services から情報を取得できません。  

詳細については、以下の記事を参照してください。  

- [競合しているレコードを管理する](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

- [ネットワーク アクセス アカウント](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [ワークグループ コンピューターへの Configuration Manager クライアントのインストール方法](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> 複数のドメインとフォレストにまたがるサイトまたは階層をサポートするシナリオ  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>シナリオ 1 :複数のフォレストにまたがっている階層のサイト間の通信

このシナリオでは、Kerberos 認証をサポートするように、フォレスト間に双方向の信頼関係が成立している必要があります。  Kerberos 認証をサポートする双方向のフォレスト信頼関係がない場合、Configuration Manager ではリモート フォレスト内の子サイトがサポートされません。  

Configuration Manager では、親サイトのフォレストとの必要な双方向の信頼関係があるリモート フォレストへの子サイトのインストールがサポートされます。 たとえば、必要な信頼関係が成立している限り、プライマリ親サイトとは異なるフォレストにセカンダリ サイトを配置できます。  

> [!NOTE]  
> 子サイトは、プライマリ サイト (中央管理サイトが親サイトになります) とセカンダリ サイトのどちらでもかまいません。  

Configuration Manager のサイト間通信には、データベースのレプリケーションとファイルベースの転送を使用します。 サイトをインストールするときに、目的のサーバーにサイトをインストールするアカウントを指定する必要があります。 このアカウントは、サイト間の通信を確立して管理するときにも使います。 サイトのインストールが完了し、ファイルベースの転送とデータベースのレプリケーションが開始されたら、サイト間の通信で他に必要な構成はありません。  

フォレストに双方向の信頼関係がある場合は、Configuration Manager で他に何も構成する必要はありません。  

既定では、新しい子サイトをインストールすると、Configuration Manager によって次の構成が行われます。  

- サイト サーバーのコンピューター アカウントを使用する各サイトのファイルベースのサイト間レプリケーション ルート。 Configuration Manager は、各コンピューターのコンピューター アカウントを、対象コンピューターの **SMS_SiteToSiteConnection_&lt;サイト コード\>** グループに追加します。  

- 各サイトの SQL Server 間のデータベースのレプリケーション。  

次の構成も設定します。  

- 介在するファイアウォールとネットワーク デバイスが、Configuration Manager で必要なネットワーク パケットを許可するように設定します。  

- フォレスト間で名前が正しく解決されるようにします。  

- サイトまたはサイト システムの役割をインストールするには、目的のコンピューターのローカル管理者権限のあるアカウントを指定する必要があります。  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>シナリオ 2 :複数のフォレストにまたがっているサイト内での通信

このシナリオでは、フォレスト間の双方向の信頼関係は必要ありません。  

プライマリ サイトでは、リモート フォレスト内のコンピューターへのサイト システムの役割のインストールがサポートされます。  

- アプリケーション カタログ Web サービス ポイントは、唯一の例外です。  この場合、サイト サーバーと同じフォレストでのみサポートされます。  

- サイト システムの役割がインターネットからの接続を受け入れる場合は、セキュリティのベスト プラクティスとして、このサイト システムの役割を、フォレストの境界によってサイト サーバーが保護される場所 (境界ネットワークなど) にインストールすることをお勧めします。  

信頼されていないフォレスト内のコンピューターにサイト システムの役割をインストールするには:  

- サイトがサイト システムの役割のインストールに使用する、**サイト システムのインストール アカウント**を指定します  (このアカウントには、接続するためのローカルの管理資格情報が必要です)。指定したコンピューターにサイト システムの役割をインストールします。  

- サイト システムのオプションの **[サイト サーバーがこのサイト システムへの接続を開始する必要がある]** を選択します。 この設定では、サイト サーバーがサイト システム サーバーへの接続を確立してデータを転送する必要があります。 この構成により、信頼されていない場所にあるコンピューターが、信頼されたネットワーク内にあるサイト サーバーへの接続を開始するのを防げます。 これらの接続では **サイト システムのインストール アカウント**を使用します。  

信頼されていないフォレストにインストールされたサイト システムの役割を使用するには、サイト サーバーがデータの転送を開始する場合でも、ファイアウォールがネットワーク トラフィックを許可する必要があります。  

さらに、次のサイト システムの役割ではサイト データベースに直接アクセスする必要があります。 そのため、ファイアウォールは、信頼されていないフォレストからサイトの SQL Server への適用可能なトラフィックを許可する必要があります。  

- 資産インテリジェンス同期ポイント  

- Endpoint Protection ポイント  

- 登録ポイント  

- 管理ポイント  

- レポート サービス ポイント  

- 状態移行ポイント  

詳細については、「[Configuration Manager で使用されるポート](ports.md)」を参照してください。  

管理ポイントと登録ポイントがサイト データベースにアクセスするように構成する必要がある場合があります。

- 既定では、これらの役割をインストールするときに、Configuration Manager によって新しいサイト システム サーバーのコンピューター アカウントがサイト システムの役割の接続アカウントとして構成されます。 次に、適切な SQL Server データベースの役割にアカウントが追加されます。  

- これらのサイト システムの役割を信頼されていないドメインにインストールする場合は、サイト システムの役割の接続アカウントを構成し、サイト システムの役割がデータベースから情報を取得できるようにします。  

これらのサイト システムの役割の接続アカウントにドメイン ユーザー アカウントを構成する場合は、そのドメイン ユーザー アカウントに、対象サイトの SQL Server データベースへの適切なアクセス権があることをご確認ください。  

- 管理ポイント: **管理ポイント データベース接続アカウント**  

- 登録ポイント: **登録ポイントの接続アカウント**  

サイト サーバーとは別のフォレストにサイト システムの役割を配置する場合は、次のことも検討してください。  

- Windows ファイアウォールを実行する場合は、ファイアウォールの適切なプロファイルで、リモートのサイト システムの役割をインストールするコンピューターとサイト データベース サーバー間の通信を許可するように構成します。

- インターネット ベースの管理ポイントが、ユーザー アカウントを含むフォレストを信頼している場合は、ユーザー ポリシーを使用することができます。 信頼していない場合は、コンピューター ポリシーだけを使用できます。  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>シナリオ 3: クライアントがそのサイト サーバーと同じ Active Directory フォレストにない場合のクライアントとサイト システムの役割間の通信

Configuration Manager では、サイト サーバーと同じフォレストにないクライアントに対する次のシナリオがサポートされます。  

- クライアントのフォレストとサイト サーバーのフォレストとの間に双方向の信頼関係がある。  

- サイト システムの役割サーバーがクライアントと同じフォレストにある。  

- サイト サーバーのフォレストと双方向の信頼関係がないドメイン コンピューターにクライアントがあり、サイト システムの役割はクライアントのフォレストにインストールされていない。  

- クライアントがワークグループのコンピューターにある。  

ドメインに参加しているコンピューターのクライアントは、そのサイト情報が Active Directory フォレストに発行されていると、Active Directory Domain Services をサービスの場所として使用することができます。  

サイト情報を別の Active Directory フォレストに発行できるようにするには、次の操作を実行します。  

- フォレストを指定してから、 **[管理]** ワークスペースの **[Active Directory フォレスト]** ノードでそのフォレストへの発行を有効にする必要があります。  

- 各サイトを、Active Directory ドメイン サービスにデータを発行するように構成します。 このように構成すると、発行先フォレストにあるクライアントが、サイト情報を取得して管理ポイントを見つけられるようになります。 Active Directory Domain Services をサービスの場所として使用できないクライアントでは、DNS、WINS、またはクライアントの割り当て済み管理ポイントを使用できます。  

#### <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a> シナリオ 4:リモート フォレストへの Exchange Server コネクタの配置  

このシナリオをサポートするには、フォレスト間で名前解決が動作することを確認します。 たとえば、DNS 転送を構成します。 Exchange Server コネクタを構成するときに、Exchange Server のイントラネット FQDN を指定します。 詳しくは、「[Configuration Manager と Exchange によるモバイル デバイスの管理](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」をご覧ください。  

## <a name="see-also"></a>関連項目

- [セキュリティの計画](../security/plan-for-security.md)  

- [構成マネージャー クライアントのセキュリティとプライバシー](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
