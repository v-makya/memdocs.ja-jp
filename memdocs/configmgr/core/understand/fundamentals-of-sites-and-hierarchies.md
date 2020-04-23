---
title: サイトおよび階層の基礎
titleSuffix: Configuration Manager
description: Configuration Manager サイトと階層の基本情報を取得します。
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707030"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>Configuration Manager のサイトおよび階層の基礎

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager 展開は Active Directory ドメインにインストールする必要があります。 この展開の基礎には、サイトの階層を形成する 1 つ以上の Configuration Manager サイトが含まれます。 1 つのサイトからマルチサイト階層まで、インストールするサイトの種類と場所では、必要に応じて展開をスケールアップ (拡張) して、キー サービスを管理されているユーザーとデバイスに配信できます。

## <a name="hierarchies-of-sites"></a>サイトの階層
Configuration Manager を初めてインストールするときに最初にインストールする Configuration Manager サイトによって、階層のスコープが決まります。 最初の Configuration Manager サイトは、社内のデバイスとユーザーを管理する基礎となります。 この最初のサイトは、中央管理サイトまたはスタンドアロンのプライマリ サイトである必要があります。  

 *中央管理サイト*は大規模な展開に適しており、管理の中心点となり、グローバルなネットワーク インフラストラクチャ全体に配布されるデバイスの柔軟なサポートを可能にします。 中央管理サイトのインストール後に、子サイトとして 1 つ以上のプライマリ サイトをインストールする必要があります。 プライマリ サイトの機能である、デバイスの管理は中央管理サイトでは直接サポートされないため、この構成が必要になります。 中央管理サイトでは、複数の子プライマリ サイトがサポートされます。 マネージド デバイスがさまざまな地理的な場所にある場合に、子プライマリ サイトを使用して、デバイスを直接管理したり、ネットワーク帯域幅を制御したりします。  

 *スタンドアロン プライマリ サイト*は小規模な展開に適しています。追加サイトをインストールせずにデバイスを管理するには、スタンドアロン プライマリ サイトを使用できます。 スタンドアロン プライマリ サイトは、展開のサイズを制限できますが、後で新しい中央管理サイトをインストールすることによって階層を拡張するシナリオもサポートします。 このサイト拡張シナリオで、スタンドアロン プライマリ サイトが子プライマリ サイトになったら、新しい中央管理サイトの下に追加の子プライマリ サイトをインストールできます。 その後、初期の展開を会社の将来の成長に合わせて拡張できます。  

> [!TIP]  
>  スタンドアロン プライマリ サイトと子プライマリ サイトは実際には同じ種類のサイト、つまりプライマリ サイトです。 名前の違いは、中央管理サイトも使用する場合に作成される階層関係に基づいています。 また、この階層関係では、Configuration Manager の機能を拡張する特定のサイト システムの役割のインストールを制限することもできます。 特定のサイト システムの役割をインストールできるのは、階層の最上位層サイト、中央管理サイト、またはスタンドアロン プライマリ サイトのみであるため、このように役割を制限します。  

 最初のサイトをインストールした後に、追加サイトをインストールできます。 最初のサイトが中央管理サイトの場合は、1 つまたは複数の子プライマリ サイトをインストールできます。 プライマリ サイト (スタンドアロンまたは子プライマリ) をインストールした後に、1 つ以上のセカンダリ サイトをインストールできます。  

 *セカンダリ サイト* はプライマリ サイトの下に子サイトとしてのみインストールできます。 このサイトの種類は、プライマリ サイトへのネットワーク接続が低速な場所のデバイスを管理するために、プライマリ サイトの範囲を拡張します。 セカンダリ サイトによってプライマリ サイトが拡張されても、クライアントはすべてプライマリ サイトによって管理されます。 セカンダリ サイトは、離れた場所のデバイスをサポートします。 ネットワーク経由でクライアントに送信 (展開) される情報とクライアントからサイトに返信される情報を圧縮して、情報の転送を管理することによりサポートを行います。  

 次の図に、サイト設計のいくつかの例を示します。  

 ![階層の例](media/Hierarchy_examples.png)  

 詳細については、以下のトピックを参照してください。  

-   [Configuration Manager の概要](../../core/understand/introduction.md)  

-   [Configuration Manager のサイト階層の設計](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Configuration Manager サイトをインストールする](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>サイト システム サーバーとサイト システムの役割  
 各 Configuration Manager サイトは、管理操作をサポートする*サイト システムの役割*をインストールします。 次の役割は、サイトをインストールすると、既定でインストールされます。

-   サイト サーバーの役割は、サイトをインストールするコンピューターに割り当てられます。

-   サイト データベース サーバーの役割は、サイト データベースをホストする SQL Server に割り当てられます。

その他のサイト システムの役割はオプションであり、サイト システムの役割でアクティブである機能の使用時にのみ使用されます。 サイト システムの役割をホストするコンピューターは、サイト システム サーバーと呼ばれます。  

 Configuration Manager の小規模展開の場合、最初にすべてのサイト システムの役割をサイト サーバーのコンピューターで直接実行することがあります。 その後、管理対象環境とニーズの拡大に伴い、増加するデバイスにサービスを提供するサイトの効率を高めるために、追加のサイト システム サーバーをインストールして、追加のサイト システムの役割をホストできます。  

 さまざまなサイト システムの役割については、「[Configuration Manager のサイト システム サーバーとサイト システムの役割の計画](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)」の「[サイト システムの役割](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)」を参照してください。

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Active Directory Domain Services へのサイト情報の発行  
 Configuration Manager の管理を簡素化するために、Configuration Manager で使用される詳細情報をサポートするように Active Directory スキーマを拡張してから、サイトのキー情報が Active Directory Domain Services (AD DS) に公開されるようにすることができます。 これにより、管理対象コンピューターが AD DS の信頼されたソースからサイト関連情報を安全に取得できるようになります。 クライアントが取得できる情報は、使用可能なサイト、サイト システム サーバー、およびそれらのサイト システム サーバーが提供するサービスを識別します。  

 *Active Directory スキーマの拡張*は、フォレストごとに 1 回だけ実行され、Configuration Manager のインストールの前または後に実行できます。   スキーマを拡張したら、各ドメインで System Management という名前の新しい Active Directory コンテナーを作成する必要があります。 このコンテナーには、クライアントで検索するためのデータを発行する Configuration Manager サイトが含まれます。 詳細については、「[サイト発行のために Active Directory を準備する](../../core/plan-design/network/extend-the-active-directory-schema.md)」を参照してください。  

 *サイト データの発行*は、Configuration Manager 階層のセキュリティを強化して、管理オーバーヘッドを削減しますが、基本的な Configuration Manager 機能には必要ありません。  
