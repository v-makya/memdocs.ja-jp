---
title: セキュリティの計画
titleSuffix: Configuration Manager
description: Configuration Manager のセキュリティに関するベスト プラクティスとその他の情報を取得します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0cdb14d282cbfa93655d6678b12b5f0837a225aa
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699281"
---
# <a name="plan-for-security-in-configuration-manager"></a>Configuration Manager でのセキュリティの計画

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager 実装でのセキュリティの計画時に考慮する概念について説明します。 次のセクションが含まれています。  

- [証明書の計画 (自己署名および PKI)](#BKMK_PlanningForCertificates)  
  - [Cryptography:Next Generation (CNG) 証明書](#bkmk_plan-cng)  
  - [拡張 HTTP](#bkmk_plan-ehttp)  
  - [CMG と CDP の証明書](#bkmk_plan-cmgcdp)  
  - [サイト サーバー署名証明書 (自己署名)](#bkmk_plansitesign)  
  - [PKI 証明書の失効](#BKMK_PlanningForCRLs)  
  - [PKI 信頼されたルート証明書と証明書発行者](#BKMK_PlanningForRootCAs)  
  - [PKI クライアント証明書の選択](#BKMK_PlanningForClientCertificateSelection)  
  - [PKI 証明書とインターネットベースのクライアント管理の移行戦略](#BKMK_PlanningForPKITransition)  

- [信頼されたルート キーの計画](#BKMK_PlanningForRTK)  

- [署名と暗号化の計画](#BKMK_PlanningForSigningEncryption)  

- [ロールベース管理の計画](#BKMK_PlanningForRBA)  

- [Azure Active Directory の計画](#bkmk_planazuread)  

- [SMS プロバイダー認証の計画](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> 証明書の計画 (自己署名および PKI)  

Configuration Manager は、自己署名入り証明書と公開キー基盤 (PKI) 証明書の組み合わせを使用します。  

可能な限り、PKI 証明書を使用します。 詳細については、「[PKI 証明書の要件](../network/pki-certificate-requirements.md)」を参照してください。 モバイル デバイスの登録中に Configuration Manager で PKI 証明書が要求される場合は、Active Directory Domain Services およびエンタープライズ証明機関を使用する必要があります。 他のすべての PKI 証明書の場合、Configuration Manager とは別にそれらの証明書を展開および管理します。 

クライアント コンピューターからインターネットベースのサイト システムへの接続時に、PKI 証明書が必要になります。 クラウド管理ゲートウェイとクラウド配布ポイントを使用する一部のシナリオでも PKI 証明書が必要です。 詳細については、[インターネット上でのクライアントの管理](../../clients/manage/manage-clients-internet.md)に関するページを参照してください。

PKI を使用するときは、IPsec も使用して、サイト内および異なるサイト間でのサイト システムのサーバー間の通信や、コンピューター間の他のデータ転送を、セキュリティで保護することができます。 IPsec の実装は、Configuration Manager には依存しません。  

PKI 証明書を使用できない場合は、Configuration Manager で自己署名証明書が自動的に生成されます。 Configuration Manager の一部の証明書は常に自己署名されます。 ほとんどの場合、Configuration Manager で自己署名証明書が自動的に管理されるため、他の操作を行う必要はありません。 1 つの例として、サイト サーバー署名証明書があります。 この証明書は常に自己署名されます。 これにより、クライアントによって管理ポイントからダウンロードされるポリシーがサイト サーバーから送信されたものであり、改ざんされていないことが保証されます。  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a>Cryptography:Next Generation (CNG) 証明書  

Configuration Manager では、Cryptography:Next Generation (CNG) 証明書がサポートされます。 Configuration Manager クライアントは、PKI クライアント認証証明書と CNG キー格納プロバイダー (KSP) の秘密キーを使用できます。 Configuration Manager クライアントは KSP をサポートしているので、PKI クライアント認証証明書用の TPM KSP など、ハードウェアベースの秘密キーをサポートしています。 詳細については、「[CNG certificates overview](../network/cng-certificates-overview.md)」(CNG 証明書の概要) を参照してください。


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a> 拡張 HTTP  

HTTPS 通信の使用は、すべての Configuration Manager 通信パスで推奨されていますが、PKI 証明書の管理のオーバーヘッドが原因で、一部の顧客にとっては、この使用が困難な課題になっています。 Azure Active Directory (Azure AD) の統合を導入することで、一部は軽減されますが、証明書要件のすべてには対応できません。 バージョン 1806 以降では、サイトで**拡張 HTTP** を使用することができます。 この構成では、自己署名証明書と Azure AD の組み合わせを使用することで、サイト システムで HTTPS がサポートされます。 PKI は必要ありません。 詳細については、「[Enhanced HTTP](../hierarchy/enhanced-http.md)」(拡張 HTTP) をご覧ください。  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a> CMG と CDP の証明書

クラウド管理ゲートウェイ (CMG) とクラウド配布ポイント (CDP) 経由のインターネットでクライアントを管理するには、証明書を使用する必要があります。 証明書の数と種類は、特定のシナリオによって異なります。 詳細については、以下の記事を参照してください。
- [クラウド管理ゲートウェイの証明書](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [クラウド配布ポイントの証明書](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a> サイト サーバー署名証明書の計画 (自己署名)  

クライアントは、Active Directory Domain Services およびクライアント プッシュ インストールからサイト サーバー署名証明書のコピーを安全に取得できます。 クライアントでこれらのメカニズムのいずれかでこの証明書のコピーを取得できない場合は、クライアントをインストールするときにそれをインストールします。 このプロセスは、クライアントとサイトの最初の通信がインターネットベースの管理ポイントを使用して行われる場合に特に重要です。 このサーバーは信頼されていないネットワークに接続されるため、攻撃を受けやすくなります。 この追加の手順を行わないと、管理ポイントからクライアントにサイト サーバー署名証明書のコピーが自動的にダウンロードされます。  

次のシナリオでは、クライアントでサイト サーバー証明書のコピーを安全に取得できません。  

- クライアント プッシュを使用してクライアントをインストールしておらず、次のような状態である。  

  - Active Directory スキーマを Configuration Manager 用に拡張していない場合。  

  - クライアントのサイトを Active Directory Domain Services に発行していない。  

  - クライアントが、信頼されていないフォレストまたはワークグループに属している。  

- インターネットベースのクライアント管理を使用しており、クライアントをインターネット上にあるときにインストールしている。  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>クライアントと共にサイト サーバー署名証明書のコピーをインストールするには  

1.  プライマリ サイト サーバーで、サイト サーバー署名証明書を見つけます。 証明書は、Windows の **SMS** 証明書ストアに格納されています。 サブジェクト名は **Site Server** で、フレンドリ名は **Site Server Signing Certificate** です。  

2.  秘密キーなしで証明書をエクスポートし、ファイルを安全な場所に格納し、このファイルにはセキュリティで保護されたチャネルからのみアクセスします。  

3.  次の client.msi プロパティを使用してクライアントをインストールします。`SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> PKI 証明書失効の計画  

Configuration Manager で PKI 証明書を使用する場合は、証明書失効リスト (CRL) の使用を計画します。 デバイスでは CRL を使用して、接続するコンピューターの証明書を確認します。 CRL は、証明書機関 (CA) によって作成され、署名されるファイルです。 CA によって発行されたが、取り消された証明書のリストがあります。 証明書管理者が証明書を取り消した場合、その拇印が CRL に追加されます。 たとえば、発行した証明書が侵害された場合や、侵害が疑われる場合などです。

> [!IMPORTANT]  
> CRL の場所は、CA が証明書を発行したときに証明書に追加されるため、Configuration Manager で使用する PKI 証明書を展開する前に CRL を計画してください。  

IIS では常にクライアント証明書の CRL が確認され、Configuration Manager でこの構成を変更することはできません。 既定では、Configuration Manager クライアントは常にサイト システムの CRL をチェックします。 サイトのプロパティを指定し、CCMSetup プロパティを指定することにより、この設定を無効にします。  

証明書失効確認を使用していても、CRL を検出できないコンピューターは、証明チェーンのすべての証明書が失効しているかのように動作します。 この動作の原因は、証明書が証明書失効リストにあるかどうかをそれらが確認できないためです。 このシナリオでは、証明書が必要で、CRL チェックを含んでいるすべての接続が失敗します。 CRL にアクセスできることを、その http の場所を参照することで確認するときは、構成マネージャー クライアントがローカル システムとして実行されることに注意する必要があります。 そのため、ユーザー コンテキストで実行されている Web ブラウザーを使った CRL へのアクセスのテストは成功する場合がありますが、同じ CRL の URL に http 接続を試みたときに、内部のフィルター処理に関する Web ソリューションが原因でコンピューター アカウントがブロックされる可能性があります。 このような状況では、フィルター処理に関するすべての Web ソリューション上で CRL の URL をホワイトリスト登録することが必要となる場合があります。

証明書が使用されるたびに CRL を確認することで、失効した証明書の使用に対するセキュリティが強化されます。 しかし、これにより、接続が遅くなり、クライアントでの処理が増えます。 組織では、インターネットまたは信頼されていないネットワーク上にあるクライアントでこのような追加のセキュリティ チェックが必要になる場合があります。  

Configuration Manager クライアントで CRL を確認する必要があるかどうかを決定する前に、PKI 管理者に相談してください。 その後、次の両方の条件に当てはまる場合は、このオプションを Configuration Manager で有効にしておくことを検討してください。  

- PKI インフラストラクチャで CRL がサポートされており、すべての Configuration Manager クライアントで検出可能な場所に CRL が公開されている。 これらのクライアントには、インターネット上のデバイスや、信頼されていないフォレスト内のデバイスが含まれる場合があります。  

- PKI 証明書を使用するように構成されているサイト システムに接続するたびに CRL を確認する必要性が、以下より高い。  
  - 高速接続  
  - クライアントでの効率的な処理  
  - CRL を検出できない場合にクライアントがサーバーに接続できないリスク  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> PKI 信頼されたルート証明書と証明書発行者リストの計画  

IIS サイト システムで HTTP 経由のクライアント認証または HTTPS 経由のクライアント認証と暗号化に PKI クライアント証明書を使用する場合、ルート CA 証明書をサイト プロパティとしてインポートする必要があることがあります。 2 つのシナリオを次に示します。  

- Configuration Manager を使用してオペレーティング システムを展開し、管理ポイントで HTTPS クライアント接続のみを受け入れる。  

- 管理ポイントによって信頼されているルート証明書にチェーンされない、PKI クライアント証明書を使用する。  

  > [!NOTE]  
  > 管理ポイントに使用するサーバー証明書を発行するのと同じ CA 階層からクライアント PKI 証明書を発行する場合、このルート CA 証明書を指定する必要はありません。 しかし、複数の CA 階層を使用しており、それらの階層が相互に信頼関係にあるかどうかが不明な場合は、クライアントの CA 階層用にルート CA をインポートします。  

Configuration Manager 用にルート CA 証明書をインポートする必要がある場合は、発行元の CA またはクライアント コンピューターからルート CA 証明書をエクスポートします。 証明書をエクスポートする発行元の CA がルート CA でもある場合、秘密キーをエクスポートしていないことを確認します。 改ざんを防ぐため、エクスポートした証明書ファイルを安全な場所に保存します。 サイトを設定するときは、ファイルにアクセスする必要があります。 ネットワーク経由でファイルにアクセスする場合は、IPsec を使用して通信が改ざんから保護されていることを確認します。  

インポートしたルート CA 証明書のいずれかが更新された場合、更新された証明書をインポートする必要があります。  

これらのインポートしたルート CA 証明書および各管理ポイントのルート CA 証明書では、証明書発行者リストが作成され、Configuration Manager コンピューターで次のように使用されます。  

- クライアントが管理ポイントに接続されると、管理ポイントで、クライアント証明書がサイトの証明書発行者リストの信頼されたルート証明書にチェーンされていることが確認されます。 確認されない場合、証明書が拒否され、PKI 接続は失敗します。  

- クライアントは、PKI 証明書を選択し、証明書発行者リストがある場合、証明書発行者リストの信頼されたルート証明書にチェーンされている証明書を選択します。 一致するものがない場合は、クライアントで PKI 証明書が選択されません。 詳細については、「[PKI クライアント証明書の選択の計画](#BKMK_PlanningForClientCertificateSelection)」を参照してください。  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> PKI クライアント証明書の選択の計画  

IIS サイト システムで、HTTP 経由のクライアント認証または HTTPS 経由のクライアント認証と暗号化に PKI クライアント証明書を使用する場合、Configuration Manager に対して使用する証明書を、Windows クライアントで選択する方法を計画します。  

> [!NOTE]  
> 一部のデバイスでは、証明書の選択方法がサポートされません。 代わりに、証明書の要件を満たす最初の証明書を自動的に選択します。 たとえば、Mac コンピューター上のクライアントやモバイル デバイスでは、証明書の選択方法がサポートされません。  

ほとんどの場合、既定の構成と動作で十分です。 Windows コンピューターの Configuration Manager クライアントは、次の順序で条件を使って複数の証明書をフィルタリングします。  

1.  証明書発行者リストで、ルート CA への証明書チェーンが管理ポイントによって信頼されている。  

2.  証明書が既定の証明書ストア **[個人用]** に保存されている。  

3.  証明書が有効であり、失効しておらず、期限切れになっていない。 有効性チェックでは、秘密キーにアクセスできることも検証されます。  

4.  証明書にクライアント認証機能がある。

5.  証明書のサブジェクト名に、ローカル コンピューター名が substring として含まれている。  

6.  証明書に最長の有効期間が設定されている。  

次のメカニズムを使用して、証明書発行者リストを使用するようにクライアントを構成します。  

- Configuration Manager サイト情報を示すリストを Active Directory Domain Services に発行する。  

- クライアント プッシュを使用してクライアントをインストールする。  

- クライアントがサイトに正常に割り当てられた後、管理ポイントからリストをダウンロードする。  

- クライアントのインストール時に、CCMSetup の client.msi の CCMCERTISSUERS プロパティとしてリストを指定する。  

最初にインストールされるときにサイトに証明書の発行元リストがなく、まだサイトに割り当てられていないクライアントでは、このチェックをスキップします。 クライアントに証明書発行者リストがあり、証明書発行者リストの信頼されたルート証明書にチェーンされている PKI 証明書がない場合、証明書の選択は失敗します。 クライアントでは、他の証明書選択条件を使用して作業が続行されません。  

ほとんどの場合、Configuration Manager クライアントは、適切な一意の PKI 証明書を正しく識別します。 しかし、この動作が行われない場合、クライアント認証機能に基づいて証明書を選択する方法の代わりに、別の 2 つの選択方法を設定できます。  

- クライアント証明書のサブジェクト名との部分文字列の一致。 この方法では大文字と小文字が区別されせん。 サブジェクト フィールドでコンピューターの完全修飾ドメイン名 (FQDN) を使用していて、**contoso.com**などのドメイン サフィックスに基づいて証明書を選択する場合に便利です。 しかし、この選択方法を使用すれば、クライアントの証明書ストア内で証明書を他の証明書と区別する、証明書のサブジェクト名の任意の連続した文字を識別することができます。  

  > [!NOTE]
  > サイト設定のサブジェクトの別名 (SAN) に、部分文字列の一致を指定することはできません。 CCMSetup を使用して SAN の部分文字列の一致を指定できますが、次のシナリオでは、サイトのプロパティによって上書きされます。  
  > 
  > - クライアントで、Active Directory Domain Services に発行されているサイト情報を取得する。  
  >   - クライアント プッシュ インストールを使用してクライアントがインストールされている。  
  > 
  >   クライアントを手動でインストールしており、クライアントで Active Directory Domain Services からサイト情報を取得しない場合にのみ、SAN で部分文字列の一致を使用してください。 たとえば、これらの条件はインターネットのみのクライアントに当てはまります。  

- クライアント証明書のサブジェクト名属性値またはサブジェクトの別名 (SAN) 属性値との一致。 この方法では大文字と小文字が区別されます。 RFC 3280 に対応し、X500 識別名または同等のオブジェクト ID (OID) を使用していて、属性値に基づいて証明書を選択したい場合に便利です。 証明書ストアの他の証明書の中から特定の証明書を一意に識別する (検証して選別する) のに必要な属性と値のみを指定できます。  

次の表に、クライアント証明書の選択条件で Configuration Manager がサポートしている属性値を示します。  

|OID 属性|識別名属性|属性の定義|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|ドメイン要素|  
|1.2.840.113549.1.9.1|E または E-mail|電子メール アドレス|  
|2.5.4.3|CN|共通名|  
|2.5.4.4|SN|サブジェクト名|  
|2.5.4.5|SERIALNUMBER|シリアル番号|  
|2.5.4.6|C|国番号|  
|2.5.4.7|L|地域|  
|2.5.4.8|S または ST|州または都道府県|  
|2.5.4.9|STREET|住所|  
|2.5.4.10|O|組織名|  
|2.5.4.11|OU|組織単位|  
|2.5.4.12|T または Title|タイトル|  
|2.5.4.42|G または GN または GivenName|名前|  
|2.5.4.43|I または Initials|イニシャル|  
|2.5.29.17|(値なし)|サブジェクト代替名| 

  > [!NOTE]
  > 上記の代替証明書の選択方法のいずれかを構成する場合、証明書のサブジェクト名にローカル コンピューター名を含める必要はありません。

選択条件を適用すると該当する証明書が複数検出される場合、有効期間が最長の証明書を選択するように既定の構成をオーバーライドして、その代わりに、証明書が選択されていないことを指定できます。 このシナリオの場合、クライアントは、PKI 証明書で IIS サイト システムと通信することはできません。 クライアントは、割り当てられたフォールバック ステータス ポイントにエラー メッセージを送信し、証明書の選択に失敗したことを通知します。これにより、証明書選択条件の変更や改善が可能になります。 クライアントの動作は、失敗した接続が HTTPS 経由または HTTP 経由のいずれであるのかによって異なります。  

- 失敗した接続が HTTPS 経由の場合:クライアントは、クライアントの自己署名入り証明書を使用して HTTP 経由で接続を試みます。  

- 失敗した接続が HTTP 経由の場合:クライアントは、自己署名入り証明書を使用して HTTP 経由で接続を再度試みます。  

一意の PKI クライアント証明書を識別できるように、**コンピューター** ストア内に既定の **[個人用]** 以外のカスタム ストアを指定することもできます。 しかし、このストアは Configuration Manager とは別に作成する必要があります。 このカスタム ストアに証明書を展開して、有効期間が切れる前に証明書を更新できる必要があります。  

詳細については、「[クライアント PKI 証明書の設定の構成](configure-security.md#BKMK_ConfigureClientPKI)」を参照してください。  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> PKI 証明書とインターネットベースのクライアント管理の移行戦略の計画  

Configuration Manager の柔軟な構成オプションを使用すると、PKI 証明書を使用するようにクライアントとサイトを徐々に移行して、クライアント エンドポイントをセキュリティで保護することができます。 PKI 証明書は優れたセキュリティを提供し、インターネット クライアントを管理できるようにします。  

Configuration Manager の構成オプションと選択肢の数のため、すべてのクライアントが HTTPS 接続を使用するようにサイトを移行する方法は 1 つではありません。 ただし、ガイダンスとして、次の手順に従うことができます。  

1. Configuration Manager サイトをインストールし、サイト システムが HTTPS 経由および HTTP 経由でクライアント接続を受け入れるようにサイトを構成します。  

2. サイト プロパティの **[クライアント コンピューターの通信]** タブで、 **[サイト システム設定]** が **HTTP または HTTPS** になるように構成し、 **[使用可能な場合は PKI クライアント証明書 (クライアント認証機能) を使用する]** を選択します。  詳細については、「[クライアント PKI 証明書の設定の構成](configure-security.md#BKMK_ConfigureClientPKI)」を参照してください。  

    > [!Note]
    > バージョン 1906 以降では、このタブは **[通信のセキュリティ]** と呼ばれています。<!-- SCCMDocs#1645 -->  

3. PKI クライアント証明書の展開を試験的に行います。 展開例については、「[Windows コンピューター用のクライアント証明書の展開](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)」を参照してください。  

4. クライアント プッシュ インストール方法を使用してクライアントをインストールします。 詳細については、[クライアント プッシュを使用した Configuration Manager クライアントのインストール方法](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)に関する記述を参照してください。  

5. Configuration Manager コンソールのレポートと情報を使用して、クライアントの展開とステータスを監視します。  

6. **[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノードで **[クライアント証明書]** 列を表示して、クライアント PKI 証明書を使用しているクライアントの数を追跡します。  

    コンピューターに Configuration Manager HTTPS 準備評価ツール (**cmHttpsReadiness.exe**) を展開することもできます。 その後、レポートを使用して、Configuration Manager でクライアント PKI 証明書を使用できるコンピューターの数を表示します。  

   > [!NOTE]
   >  Configuration Manager クライアントをインストールするときに、`%windir%\CCM` フォルダーに **CMHttpsReadiness.exe** ツールがインストールされます。 このツールを実行するときに、次のコマンド ライン オプションを使用できます。  
   > 
   > - `/Store:<name>`: このオプションは、**CCMCERTSTORE** client.msi プロパティと同じです  
   > - `/Issuers:<list>`: このオプションは、**CCMCERTISSUERS** client.msi プロパティと同じです    
   > - `/Criteria:<criteria>`: このオプションは、**CCMCERTSEL** client.msi プロパティと同じです    
   > - `/SelectFirstCert`: このオプションは、**CCMFIRSTCERT** client.msi プロパティと同じです    
   > 
   >   詳しくは、[クライアント インストールのプロパティ](../../clients/deploy/about-client-installation-properties.md)に関するページをご覧ください。  

7. 十分なクライアントで HTTP 経由での認証にクライアント PKI 証明書が正しく使用されている場合は、次の手順に従います。  

   1.  PKI Web サーバー証明書を、サイトの追加の管理ポイントを実行するメンバー サーバーに展開し、その証明書を IIS に構成します。 詳細については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)」を参照してください。  

   2.  このサーバーに管理ポイントの役割をインストールし、 **[HTTPS]** の管理ポイントのプロパティで **[クライアント接続]** オプションを構成します。  

8. PKI 証明書があるクライアントが HTTPS 経由で新しい管理ポイントを使用していることを、監視および確認します。 IIS ログまたはパフォーマンス カウンターを使用して確認できます。  

9. HTTPS クライアント接続を使用するように、他のサイト システムの役割を再構成します。 インターネット上のクライアントを管理する場合は、サイト システムにインターネット FQDN があることを確認します。 インターネットからのクライアント接続を受け入れるように、個々の管理ポイントと配布ポイントを構成します。  

    > [!IMPORTANT]  
    > インターネットからの接続を受け入れるようにサイト システムの役割を設定する前に、インターネットベースのクライアント管理の計画情報と前提条件を確認してください。 詳細については、「[System Center Configuration Manager でのエンドポイント間の通信](../hierarchy/communications-between-endpoints.md)」をご覧ください。  

10. IIS を実行するサイト システムとクライアントに PKI 証明書のロールアウトを拡張します。 必要に応じて、HTTPS クライアント接続およびインターネット接続用にサイト システムの役割を設定します。  

11. セキュリティを最大限に高めるため、すべてのクライアントが認証と暗号化にクライアント PKI 証明書を使用している場合は、HTTPS のみを使用するようにサイト プロパティを変更します。  

    この計画では、まず、HTTP 経由での認証にのみ PKI 証明書が導入され、その後、HTTPS 経由での認証と暗号化に導入されます。 この計画に従って、これらの証明書を段階的に導入すると、クライアントが管理されなくなるというリスクが軽減されます。 また、セキュリティを Configuration Manager がサポートしている最大限のレベルにまで高めることができます。  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> 信頼されたルート キーの計画  

Configuration Manager の信頼されたルート キーでは、サイト システムが階層に属していることを Configuration Manager クライアントが確認するメカニズムが提供されます。 すべてのサイト サーバーが、他のサイトと通信するためにサイト交換キーを生成します。 階層内の最上位のサイトのサイト交換キーは、信頼されたルート キーと呼ばれます。  

Configuration Manager の信頼されたルート キーの機能は、公開キー基盤のルート証明書に似ています。 信頼されたルート キーの秘密キーによって署名されたものはすべて、下位の階層で信頼されます。 クライアントでは、**root\ccm\locationservices** という WMI 名前空間に、サイトの信頼されたルート キーのコピーが格納されます。 

たとえば、サイトで管理ポイントに証明書が発行され、信頼されたルート キーの秘密キーで署名が行われます。 サイトでは、信頼されたルート キーの公開キーをクライアントと共有します。 その後、クライアントで、階層内の管理ポイントと、階層内にない管理ポイントを区別することができます。   

クライアントでは、次の 2 つのメカニズムを使用して、信頼されたルート キーの公開コピーが自動的に取得されます。  

- Configuration Manager 向けに Active Directory スキーマを拡張し、Active Directory Domain Services にサイトを発行する。 その後、クライアントでグローバル カタログ サーバーからこのサイト情報を取得します。 詳細については、「[サイト発行のために Active Directory を準備する](../network/extend-the-active-directory-schema.md)」を参照してください。  

- クライアント プッシュ インストール方法を使用して、クライアントをインストールする場合。 詳しくは、「[クライアント プッシュ インストール](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)」をご覧ください。  

クライアントでは、これらのメカニズムのいずれかを使用して信頼されたルート キーを取得できない場合、通信している最初の管理ポイントで提供される信頼されたルート キーを信頼します。 この場合は、偽の管理ポイントからポリシーを受け取る攻撃者の管理ポイントにクライアントが誘導される可能性があります。 この操作には巧妙な攻撃者が必要となります。 この攻撃は、クライアントで有効な管理ポイントから信頼されたルート キーを取得する前の短時間に制限されます。 攻撃者がクライアントを偽の管理ポイントに誘導するリスクを軽減するには、クライアントに信頼されたルート キーを事前に準備します。  

Configuration Manager クライアントに信頼されたルート キーを事前に準備および検証するには、次の手順に従います。  

- [ファイルを使用して信頼されたルート キーをクライアントに事前に準備する](#bkmk_trk-provision-file)  

- [ファイルを使用せずに信頼されたルート キーをクライアントに事前に準備する](#bkmk_trk-provision-nofile)  

- [クライアントの信頼されたルート キーを検証する](#bkmk_trk-verify)  

- [信頼されたルート キーを削除または置き換える](#bkmk_trk-reset)  

  > [!NOTE]  
  > クライアントで Active Directory Domain Services から、またはクライアント プッシュを使用して信頼されたルート キーを取得できる場合は、事前に準備する必要はありません。 
  > 
  > クライアントで管理ポイントに対して HTTPS 通信を使用する場合は、信頼されたルート キーを事前に準備する必要はありません。 PKI 証明書で信頼が確立されます。  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a> ファイルを使用して信頼されたルート キーをクライアントに事前に準備する  

1.  サイト サーバーで、`<Configuration Manager install directory>\bin\mobileclient.tcf` というファイルをテキスト エディターで開きます。  

2.  **SMSPublicRootKey=** というエントリを見つけます。 その行からキーをコピーし、変更せずにファイルを閉じます。  

3.  新しいテキスト ファイルを作成し、mobileclient.tcf ファイルからコピーしたキー情報を貼り付けます。  

4.  すべてのコンピューターからアクセスできるが、改ざんされない場所にファイルを保存します。  

5.  client.msi プロパティが受け入れられるインストール方法を使用して、クライアントをインストールします。 `SMSROOTKEYPATH=<full path and file name>` というプロパティを指定します。  

    > [!IMPORTANT]  
    > クライアントのインストール中に信頼されたルート キーを指定する場合は、サイト コードも指定します。 `SMSSITECODE=<site code>` という client.msi プロパティを使用します。   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a> ファイルを使用せずに信頼されたルート キーをクライアントに事前に準備する  

1.  サイト サーバーで、`<Configuration Manager install directory>\bin\mobileclient.tcf` というファイルをテキスト エディターで開きます。  

2.  **SMSPublicRootKey=** というエントリを見つけます。 その行からキーをコピーし、変更せずにファイルを閉じます。  

3.  client.msi プロパティが受け入れられるインストール方法を使用して、クライアントをインストールします。 `SMSPublicRootKey=<key>` という client.msi プロパティを指定します。ここで、`<key>` は mobileclient.tcf からコピーした文字列です。  

    > [!IMPORTANT]  
    >  クライアントのインストール中に信頼されたルート キーを指定する場合は、サイト コードも指定します。 `SMSSITECODE=<site code>` という client.msi プロパティを使用します。   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a> クライアントの信頼されたルート キーを検証する  

1. 管理者として Windows PowerShell コンソールを開きます。  

2. 次のコマンドを実行します。  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

返される文字列は信頼されたルート キーです。 これが、サイト サーバー上の mobileclient.tcf ファイルにある **SMSPublicRootKey** の値と一致することを検証します。  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a> 信頼されたルート キーを削除または置き換える  

client.msi プロパティ **RESETKEYINFORMATION = TRUE** を使用して、クライアントから信頼されたルート キーを削除します。 

信頼されたルート キーを置き換えるには、新しい信頼されたルート キーと共にクライアントを再インストールします。 たとえば、クライアント プッシュを使用するか、client.msi プロパティ **SMSPublicRootKey** を指定します。  

これらのインストール プロパティの詳細については、[クライアント インストールのパラメーターとプロパティについて](../../clients/deploy/about-client-installation-properties.md)のページを参照してください。



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> 署名と暗号化の計画  
 
すべてのクライアント通信に PKI 証明書を使用する場合は、クライアント データの通信をセキュリティで保護するために、署名と暗号化を計画する必要はありません。 HTTP クライアント接続を許可するように IIS を実行しているサイト システムを設定する場合は、サイトのクライアント接続をどのようにセキュリティで保護するのかを決めます。  

クライアントから管理ポイントに送信されるデータを保護するために、クライアントでデータに署名することを要求できます。 署名の際に SHA-256 アルゴリズムを要求することもできます。 この構成はより安全ですが、すべてのクライアントでサポートされていない限り、SHA-256 を要求しないでください。 多くのオペレーティング システムでこのアルゴリズムはネイティブにサポートされますが、以前のオペレーティング システムには更新プログラムまたは修正プログラムが必要になる場合があります。 

署名によって改ざんからデータを保護できますが、暗号化によって情報漏えいからデータを保護できます。 サイト内の管理ポイントにクライアントが送信するインベントリ データと状態メッセージに対して、3DES 暗号化を有効にすることができます。 このオプションをサポートするために、クライアントで更新プログラムをインストールする必要はありません。 クライアントと管理ポイントでは、暗号化と復号化のためにさらに CPU を使用する必要があります。  

署名と暗号化の設定を構成する方法の詳細については、「[署名と暗号化の構成](configure-security.md#BKMK_ConfigureSigningEncryption)」を参照してください。  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> 役割に基づいた管理の計画  

詳細については、「[ロール ベース管理の基礎](../../understand/fundamentals-of-role-based-administration.md)」を参照してください。  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a> Azure Active Directory の計画

Configuration Manager と Azure Active Directory (Azure AD) を統合することにより、サイトとクライアントで先進認証を使用できるようになります。 Azure AD でのサイトのオンボードでは、次の Configuration Manager のシナリオがサポートされます。

**クライアント**  

- [クラウド管理ゲートウェイ経由のインターネットでクライアントを管理する](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [クラウド ドメイン参加デバイスを管理する](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [共同管理](../../../comanage/overview.md)  

- [ユーザーが利用できるアプリを展開する](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)

- [ビジネス向け Microsoft ストアのオンライン アプリ](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- インフラストラクチャの要件を減らす。 たとえば、アプリケーション カタログではなく、[管理ポイントを使用するソフトウェア センター](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)  

- [Microsoft 365 Apps for enterprise を管理する](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**サーバー**  

- [Desktop Analytics](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm)  

- [コミュニティ ハブ](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [クラウド配布ポイント](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [ユーザーの探索](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Azure AD へのサイトの接続の詳細については、[Azure サービスの構成](../../servers/deploy/configure/azure-services-wizard.md)に関するページを参照してください。


Azure AD の詳細については、「[Azure Active Directory のドキュメント](/azure/active-directory/)」を参照してください。



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a> SMS プロバイダー認証の計画
<!--1357013--> 

バージョン 1810 以降では、Configuration Manager サイトにアクセスする管理者の最低限の認証レベルを指定することができます。 この機能では、Windows にサインインする管理者には必要なレベルを持つことが強制されます。 SMS プロバイダーにアクセスするすべてのコンポーネントに適用されます。 たとえば、Configuration Manager コンソール、SDK メソッド、Windows PowerShell コマンドレットなどです。 

この構成は階層全体の設定です。 この設定を変更する前に、すべての Configuration Manager 管理者が必要な認証レベルで Windows にサインインできることを確認してください。 

次のレベルを使用できます。

- **Windows 認証**:Active Directory ドメイン資格情報による認証が必要です。   

- **証明書認証**:信頼された PKI 証明機関によって発行された有効な証明書による認証が必要です。  

- **Windows Hello for Business 認証**:デバイスに関連付けられた、生体認証か PIN を使用する強力な 2 要素認証による認証が必要です。  

詳細については、「[SMS プロバイダーの計画](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)」を参照してください。 



## <a name="see-also"></a>関連項目
- [構成マネージャー クライアントのセキュリティとプライバシー](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [セキュリティの構成](configure-security.md)  

- [エンドポイント間の通信](../hierarchy/communications-between-endpoints.md)  

- [暗号化コントロールのテクニカル リファレンス](cryptographic-controls-technical-reference.md)  

- [PKI 証明書の要件](../network/pki-certificate-requirements.md)