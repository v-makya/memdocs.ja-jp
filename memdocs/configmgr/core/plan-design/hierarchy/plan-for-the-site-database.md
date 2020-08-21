---
title: サイト データベースの計画
titleSuffix: Configuration Manager
description: Configuration Manager の階層を計画するとき、サイト データベースとサイト データベース サーバーの役割を考える必要があります。
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 068511c5b3b0c15eb355c484b241a76d9dd512e2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700182"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>Configuration Manager のサイト データベースの計画

*適用対象:Configuration Manager (Current Branch)*

サイト データベース サーバーとは、Microsoft SQL Server のサポートされているバージョンを実行するコンピューターのことです。 SQL Server を使用して、Configuration Manager サイトの情報を格納します。 Configuration Manager 階層内の各サイトには、サイト データベースと、サイト データベース サーバーの役割を持つサーバーがあります。  

-   中央管理サイトとプライマリ サイトでは、SQL Server をサイト サーバーにインストールすることも、サイト サーバー以外のサーバーにインストールすることもできます。  

-   セカンダリ サイトでは、SQL Server の完全版の代わりに、SQL Server Express をインストールできます。 ただし、データベース サーバーは、セカンダリ サイト サーバーで実行する必要があります。  

-  SQL 可用性グループを使用するためには、データベース復旧モデルを FULL に設定する必要があります。  

-  SQL 可用性グループを使用しない場合は、データベース復旧モデルを SIMPLE に設定する必要があります。  

SQL の回復モードについては、「[復旧モデル (SQL Server)](/sql/relational-databases/backup-restore/recovery-models-sql-server)」をご覧ください。

次の SQL Server 構成を使用して、サイト データベースをホストできます。  

-   SQL Server の既定のインスタンス  

-   SQL Server を実行している 1 台のコンピューターの名前付きインスタンス  

-   SQL Server のクラスター化されたインスタンスの名前付きインスタンス  

-   SQL Server AlwaysOn 可用性グループ (Configuration Manager のバージョン 1602 以降)


サイト データベースをホストするには、[Configuration Manager の SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)に関する記事で説明されている要件を SQL Server が満たす必要があります。  



## <a name="remote-database-server-location-considerations"></a>リモート データベース サーバーの場所に関する考慮事項  

リモート データベース サーバーのコンピューターを使用する場合は、介在するネットワーク接続が可用性の高い広帯域のネットワーク接続であることを確認します。 サイト サーバーとサイト システムの役割のいくつかは、サイト データベースをホストしているリモート サーバーと継続的に通信する必要があります。

-   データベース サーバーとの通信に必要な帯域幅は、サイトとクライアントの構成によって異なります。 そのため、実際に必要な帯域幅を的確に予測することはできません。  

-   SMS プロバイダーを実行し、サイト データベースに接続するコンピューターが多いほど、必要なネットワーク帯域幅が大きくなります。  

-   SQL Server を実行するコンピューターは、サイト サーバー、および SMS プロバイダーを実行しているすべてのコンピューターとの双方向の信頼関係があるドメインになければなりません。  

-   サイト データベースとサイト サーバーを併置する場合は、クラスター化された SQL Server をサイト データベース サーバーにすることはできません。  


通常、サイト システム サーバーは、1 つだけの Configuration Manager サイトのサイト システムの役割をサポートしています。 ただし、SQL Server を実行するクラスター化または非クラスター化サーバーで、SQL Server のさまざまなインスタンスを使用して、さまざまな Configuration Manager サイトのデータベースをホストできます。 この場合は、SQL Server の各インスタンスが、通信用に別々のポートを使用するように構成する必要があります。