---
title: セキュリティの基礎
titleSuffix: Configuration Manager
description: Configuration Manager のセキュリティ層について説明します。
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c702916f73d1fbc842966161a6958a61d24044a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126071"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Configuration Manager のセキュリティの基礎

*適用対象:Configuration Manager (Current Branch)*

この記事は、任意の Configuration Manager 環境の次の基本的なセキュリティ コンポーネントをまとめたものです。
- [セキュリティ レイヤー](#bkmk_layers)
- [役割に基づいた管理](#bkmk_rba)
- [クライアント エンドポイントの保護](#bkmk_endpoints)
- [Configuration Manager のアカウントとグループ](#bkmk_accounts)
- [プライバシー](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a> セキュリティ レイヤー

Configuration Manager のセキュリティは、次の階層で構成されています。 
- [Windows OS とネットワーク セキュリティ](#bkmk_layer-windows)
- [ネットワーク インフラストラクチャ: ファイアウォール、侵入検出、公開キー基盤 (PKI)](#bkmk_layer-network)
- [Configuration Manager のセキュリティ制御](#bkmk_layer-cm)
- [SMS プロバイダー](#bkmk_layer-provider)
- [サイト データベースのアクセス許可](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a> Windows OS とネットワーク セキュリティ
OS とネットワークの両方に、Windows セキュリティ機能によって最初の層が提供されます。 この層には、次のコンポーネントが含まれます。  

-   Configuration Manager コンポーネント間でファイルを転送するためのファイル共有  

-   ファイルとレジストリ キーを保護するためのアクセス制御リスト (ACL)  

-   通信の保護に役立つインターネット プロトコル セキュリティ (IPsec)  

-   セキュリティ ポリシーを設定するためのグループ ポリシー  

-   Configuration Manager コンソールなど、配布されたアプリケーションの分散コンポーネント オブジェクト モデル (DCOM) アクセス許可  

-   セキュリティ プリンシパルを保存するための Active Directory ドメイン サービス  

-   Configuration Manager がセットアップ中に作成する一部のグループを含む、Windows アカウント セキュリティ  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a> ネットワーク インフラストラクチャ

さらにファイアウォールや侵入検出などのセキュリティ コンポーネントを使用することで、環境全体を防御することができます。 業界標準の公開キー基盤 (PKI) 実装で発行される証明書により、認証、署名および暗号化が可能になります。  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a> Configuration Manager のセキュリティ制御

Windows Server とネットワーク インフラストラクチャによって提供されるセキュリティだけでなく、Configuration Manager ではいくつかの方法でそのコンソールとリソースへのアクセスが制御されます。 既定では、Configuration Manager コンソールがインストールされているコンピューター上で必要なファイルおよびレジストリ キーへのアクセス権は、ローカル管理者のみにあります。  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a> SMS プロバイダー

次のセキュリティ階層は、Windows Management Instrumentation (WMI) によるアクセスに基づいています。これは SMS プロバイダーに特有のものです。 SMS プロバイダーは、サイト データベースの情報を照会するためのユーザー アクセスを付与する Configuration Manager コンポーネントです。 既定では、プロバイダーへのアクセスは、ローカルの SMS 管理グループのメンバーに限定されています。 このグループには最初のうち、Configuration Manager をインストールしたユーザーのみが含まれています。 他のアカウントに Common Information Model (CIM) リポジトリおよび SMS プロバイダーへのアクセス許可を与えるには、SMS 管理グループに他のアカウントを追加します。  

バージョン 1810 以降では、Configuration Manager サイトにアクセスする管理者の最低限の認証レベルを指定することができます。 この機能では、Windows にサインインする管理者には必要なレベルを持つことが強制されます。 <!--1357013-->  

詳細については、「[SMS プロバイダーの計画](../plan-design/hierarchy/plan-for-the-sms-provider.md)」を参照してください。

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a> サイト データベースのアクセス許可

最後のセキュリティ階層は、サイト データベース内のオブジェクトに対するアクセス許可に基づいています。 既定では、Configuration Manager をインストールする際に使用したローカル システム アカウントおよびユーザー アカウントは、サイト データベース内のすべてのオブジェクトを管理できます。 Configuration Manager コンソールで、ロール ベース管理を使用すると、追加の管理ユーザーに対してアクセス許可を付与したり、制限したりすることができます。  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a> 役割に基づいた管理  

 Configuration Manager では、ロール ベース管理を使用して、オブジェクト (コレクション、展開、サイトなど) を保護できます。 この管理モデルは、階層内のすべてのサイトのセキュリティのアクセス権の設定およびサイトの設定を一元的に定義および管理します。 

 管理者が*セキュリティ ロール*を管理ユーザーとグループのアクセス許可に割り当てます。 アクセス許可は、たとえばクライアント設定の作成や変更を行うために、さまざまな Configuration Manager オブジェクトの種類に接続されます。 

 *セキュリティ スコープ*は、管理ユーザーが管理を担当する特定のオブジェクトのインスタンス (Microsoft 365 Apps をインストールするアプリケーションなど) をグループ化します。 

 セキュリティ ロール、セキュリティ スコープ、およびコレクションの組み合わせによって、管理ユーザーが表示および管理できるオブジェクトが定義されます。 Configuration Manager は、一般的な管理タスクのためにいくつかの既定のセキュリティ ロールをインストールします。 独自のセキュリティ ロールを作成して、特定のビジネス要件をサポートできます。  

 詳細については、「[役割に基づいた管理の構成](../servers/deploy/configure/configure-role-based-administration.md)」を参照してください。  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a> クライアント エンドポイントの保護  

 Configuration Manager は、自己署名証明書または PKI 証明書、または Azure Active Directory (Azure AD) トークンのいずれかを使用して、サイト システムの役割へのクライアント通信をセキュリティで保護します。 一部のシナリオでは、PKI 証明書の使用が必要です。 たとえば、[インターネット ベースのクライアント管理](../clients/manage/plan-internet-based-client-management.md)や、[モバイル デバイス クライアント](../../mdm/plan-design/plan-on-premises-mdm.md)です。  

 クライアントが接続するサイト システムの役割は、HTTPS または HTTP を使用してクライアント通信を行うように構成できます。 クライアント コンピューターは、使用可能な最も安全な方法を使用して常に通信を行います。 クライアント コンピューターは、HTTP 通信を許可するサイト システムの役割がある場合にのみ、安全性が劣る通信方法を代替で使用します。  

 詳細については、[セキュリティの計画](../plan-design/security/plan-for-security.md)に関するページをご覧ください。



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a> Configuration Manager のアカウントとグループ  

 Configuration Manager では、ほとんどのサイト操作にローカル システム アカウントを使用します。 いくつかの管理タスクでは、追加のアカウントを作成して管理する必要がある場合があります。 Configuration Manager により、いくつかの既定のグループと SQL Server の役割がセットアップ時に作成されます。 既定のグループと SQL Server の役割には、コンピューターまたはユーザー アカウントを手動で追加する必要がある場合があります。  

 詳細については、「[System Center Configuration Manager で使用されるアカウント](../plan-design/hierarchy/accounts.md)」を参照してください。  



## <a name="privacy"></a><a name="bkmk_privacy"></a> プライバシー  

 Configuration Manager を実装する前に、プライバシー要件について検討してください。 多くのクライアントを効果的に管理できるため、エンタープライズ管理製品には多くの利点がありますが、このソフトウェアは組織のユーザーのプライバシーに影響を与える可能性があります。 Configuration Manager にはデータを収集してデバイスを監視するための多くのツールが備わっています。 一部のツールでは組織内でプライバシーの問題が生じる可能性があります。  

 たとえば、Configuration Manager クライアントをインストールすると、既定で多数の管理設定が有効になります。 この構成により、クライアント ソフトウェアから情報が Configuration Manager サイトに送信されます。 サイトは、クライアント情報をサイト データベースに格納します。 クライアント情報が Microsoft に直接送信されることはありません。 詳細については、「[診断結果と使用状況データ](../plan-design/diagnostics/diagnostics-and-usage-data.md)」を参照してください。



## <a name="see-also"></a>関連項目

- [セキュリティの計画](../plan-design/security/plan-for-security.md)  

- [構成マネージャー クライアントのセキュリティとプライバシー](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [セキュリティの構成](../plan-design/security/configure-security.md)   

- [エンドポイント間の通信](../plan-design/hierarchy/communications-between-endpoints.md)  

- [暗号化コントロールのテクニカル リファレンス](../plan-design/security/cryptographic-controls-technical-reference.md)  
