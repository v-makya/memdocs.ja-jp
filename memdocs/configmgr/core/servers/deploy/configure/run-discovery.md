---
title: デバイスとユーザー リソースの探索
titleSuffix: Configuration Manager
description: 探索プロセスおよび探索データ レコードの概要を読んでください。
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700990"
---
# <a name="run-discovery-for-configuration-manager"></a>Configuration Manager 用の探索の実行

*適用対象:Configuration Manager (Current Branch)*

管理可能なデバイスとユーザーのリソースを見つけるには、Configuration Manager で 1 つまたは複数の探索方法を使用します。 また、環境のネットワーク インフラストラクチャを識別するために探索を使用することもできます。 さまざまなものを探すために使用できるさまざまな方法があり、各方法に独自の構成と制限があります。  

## <a name="overview-of-discovery"></a>探索の概要  
 探索は、Configuration Manager が管理可能なリソースについての情報を得るプロセスです。 利用可能な探索方法は次のとおりです。  

-   Active Directory フォレストの探索  

-   Active Directory グループの探索  

-   Active Directory システムの探索  

-   Active Directory ユーザー検出  

-   定期探索  

-   ネットワーク探索  

-   サーバー探索  

> [!TIP]  
>  「[Configuration Manager の探索方法について](../../../../core/servers/deploy/configure/about-discovery-methods.md)」で個々の探索方法について学習できます。  
>   
>  階層内のどのサイトにどの方法を使用するかについては、「[Configuration Manager に使用する探索方法の選択](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)」をご覧ください。  

 ほとんどの探索方法を使用するには、方法をサイトで有効にして、特定のネットワークまたは Active Directory の場所を検索するように設定する必要があります。 探索方法が実行されると、Configuration Manager が管理できるデバイスまたはユーザー情報について指定場所へのクエリが実行されます。 探索方法でリソースについての情報が見つかると、その情報は探索データ レコード (DDR) と呼ばれるファイルに保存されます。 そのファイルがプライマリ サイトまたは中央管理サイトで処理されます。 DDR の処理では、新たに探索されたリソースのために新しいレコードがサイト データベースに作成されるか、または既存のレコードが新しい情報で更新されます。  

 探索方法によっては、大量のネットワーク トラフィックが発生して、生成された DDR の処理に大量の CPU リソースが消費されることがあります。 したがって、目的のために必要な探索方法のみを使用することを計画してください。 始めは 1 つまたは 2 つの探索方法だけを使用するようにして、後で追加的な方法を慎重に有効にして、環境での探索レベルを拡張してください。  

 サイト データベースに追加された探索情報は、探索または処理された場所に関係なく、階層内の各サイトにレプリケートされます。 そのため、複数のサイトでさまざまなスケジュールや探索方法の設定を設定することができますが、特定の探索方法を 1 つのサイトだけで実行したほうがよいでしょう。 これによって、重複する探索処理によるネットワーク帯域幅の使用を減らすと同時に、複数サイトでの冗長な探索データの処理を減らすことができます。  

 探索データを使用すると、次のような管理タスクのために、リソースを論理的にグループ化するカスタム コレクションやクエリを作成できます。 次に例を示します。  

-   クライアントのインストールまたはアップグレードをプッシュする。  

-   ユーザーまたはデバイスにコンテンツを展開する。  

-   クライアント設定および関連する構成を展開する。

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a> 探索データ レコードについて  
 DDR は、各探索方法によって作成されるファイルです。 Configuration Manager で管理できるリソース (コンピューターやユーザー、場合によってはネットワーク インフラストラクチャなど) についての情報が保存されています。 DDR は、プライマリ サイトか中央管理サイトで処理されます。 DDR にあるリソースの情報がデータベースに挿入されると、その DDR は削除され、階層内のすべてのサイトに情報がグローバル データとしてレプリケートされます。  

 DDR を処理するサイトは、DDR に含まれている情報によって異なります。  

-   今までデータベースには存在しておらず、新しく検出されたリソースの DDR は、階層の最上位サイトで処理されます。 最上位サイトのデータベースに新しいリソース レコードが作成され、固有な識別子が割り当てられます。 DDR は、最上位サイトに到達するまで、ファイルベースのレプリケーションによって転送されます。  

-   既に検出されているオブジェクトの DDR は、プライマリ サイトで処理されます。 データベースに存在するリソースに関する情報が DDR に含まれている場合は、子プライマリ サイトは DDR を中央管理サイトに転送しません。  

-   セカンダリ サイトは、DDR を処理することはなく、常にファイルベースのレプリケーションでそれらを親プライマリ サイトに転送します。  

DDR ファイルには、.ddr という拡張子が付き、サイズは通常 1 KB ほどです。  

## <a name="get-started-with-discovery"></a>探索の概要:  
 Configuration Manager コンソールを使用して探索を設定する前に、探索方法の違い、探索方法で実行できること、および一部の探索方法にある制限について理解する必要があります。  

次のトピックに従って、探索方法を適切に使用するのに役立つ基盤を構築できます。  

-   [Configuration Manager の探索方法について](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Configuration Manager に使用する探索方法の選択](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

その後、使用しようとしている方法が理解できたら、「[Configuration Manager の探索方法を構成する](../../../../core/servers/deploy/configure/configure-discovery-methods.md)」でそれぞれの方法の構成の手引きを探します。  
