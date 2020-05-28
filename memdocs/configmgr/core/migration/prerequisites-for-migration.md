---
title: 移行の前提条件
titleSuffix: Configuration Manager
description: Configuration Manager のサポートされているバージョン、サポートされているソース サイトの言語、および移行に必要な構成を理解します。
ms.date: 05/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36e62ea5198824a6b3466853cdbcfc3057d1829e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428733"
---
# <a name="prerequisites-for-migration-in-configuration-manager"></a>Configuration Manager での移行の前提条件

*適用対象:Configuration Manager (Current Branch)*

サポートされているソース階層から移行するには、該当する各 Configuration Manager ソース サイトのアクセス権と、Configuration Manager 移行先サイト内で移行操作を構成および実行するためのアクセス許可が必要です。  

 移行がサポートされている Configuration Manager のバージョンと必要な構成を把握する際には、以下のセクションの情報を参考にしてください。  

-   [移行がサポートされている Configuration Manager のバージョン](#BKMK_SupportedMigrationVersions)  

-   [移行がサポートされているソース サイトの言語](#BKMK_SorceSiteLanguage)  

-   [移行に必要な構成](#BKMK_Required_Configurations)  

##  <a name="versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a> 移行がサポートされている Configuration Manager のバージョン  
 次のいずれかのバージョンの Configuration Manager を実行しているソース階層からデータを移行できます。  

- Configuration Manager 2007 SP2 (移行の目的では、ソース サイト上の Configuration Manager 2007 R2 や R3 は考慮されません。 ソース サイトで SP2 を実行していれば、R2 と R3 のどちらかのアドオンがインストールされているサイトが Configuration Manager Current Branch への移行についてサポートされます)。  

- System Center 2012 Configuration Manager SP2 または System Center 2012 R2 Configuration Manager SP1。  

  > [!TIP]  
  >  移行だけでなく、System Center 2012 Configuration Manager を実行しているサイトの Configuration Manager Current Branch へのインプレース アップグレードを使用できます。  

- 同じまたは低いバージョンの Configuration Manager の Configuration Manager 階層。  

  たとえば、移行先階層で Configuration Manager Current Branch 1606 を実行している場合は、移行を使用してバージョン 1606 または 1602 を実行するソース階層からデータをコピーすることができます。 ただし、1610 を実行しているソース階層からデータを移行することはできません。  


##  <a name="source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a> 移行がサポートされているソース サイトの言語  
 Configuration Manager 階層間でデータを移行すると、データは Configuration Manager の言語に依存しない形式で移行先階層に保存されます。 Configuration Manager 2007 では、データは言語に依存しない形式では保存されないため、Configuration Manager 2007 からの移行中に、移行プロセスでオブジェクトをこの形式に変換する必要があります。 このため、以下の言語でインストールされている Configuration Manager 2007 ソース サイトのみ、移行がサポートされています。  

-   英語  

-   フランス語  

-   ドイツ語  

-   日本語  

-   韓国語  

-   ロシア語  

-   簡体中国語  

-   繁体字中国語  

System Center 2012 Configuration Manager または Configuration Manager Current Branch 階層からデータを移行するときは、ソース サイトの言語の制限はありません。 ソース サイトのデータベースのオブジェクトは、常に言語に依存しない形式になります。  

##  <a name="required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a> 移行に必要な構成  
移行と移行操作を使用するために必要な構成は以下のとおりです。  

- **Configuration Manager コンソールでの移行の構成、実行、および監視を行うには:**  

   移行先サイトでは、ロールベースの管理のセキュリティ ロール **[インフラストラクチャ管理者]** が割り当てられたアカウントを使用する必要があります。 このセキュリティ ロールにより、移行ジョブの作成、クリーンアップ、監視、および配布ポイントの共有とアップグレード操作など、すべての移行操作を管理するアクセス許可が付与されます。  

- **データ収集:**  

   移行先サイトでデータ収集を有効にするためには、各ソース サイトで使用する次の 2 つのソース サイト アクセス アカウントを構成する必要があります。  

  -   **ソース サイトのアカウント:** このアカウントを使用して、ソース サイトの SMS プロバイダーにアクセスします。  

      -   Configuration Manager 2007 SP2 ソース サイトの場合は、このアカウントにはすべてのソース サイト オブジェクトへの**読み取り**アクセス許可が必要です。  

      -   System Center 2012 Configuration Manager または Configuration Manager Current Branch ソース サイトの場合は、このアカウントには、すべてのソース サイト オブジェクトへの**読み取り**アクセス許可が必要です。ロールベースの管理を使用して、このアクセス許可をアカウントに付与します。 ロール ベース管理の使用方法については、「[Configuration Manager のロール ベース管理の基礎](../../core/understand/fundamentals-of-role-based-administration.md)」を参照してください。  

  -   **ソース サイトのデータベース アカウント**このアカウントは、ソース サイトの SQL Server データベースへのアクセスに使用され、ソース サイト データベースの **Connect**、**Execute**、**Select** のアクセス許可を必要とします。  

  新しいソース階層で追加のソース サイトのデータ収集を構成する際、またはソース サイトの資格情報を再構成する際に、これらのアカウントを構成できます。 これらのアカウントにドメイン ユーザー アカウントを使用できます。または、移行先階層の最上位サイトのコンピューター アカウントを指定することもできます。  

  > [!IMPORTANT]  
  >  いずれかのアクセス アカウントに Configuration Manager コンピューター アカウントを使用する場合、このアカウントが、ソース サイトが存在するドメインの **Distributed COM Users** セキュリティ グループのメンバーであることを確認してください。  

  データの収集時には、次のネットワーク プロトコルとポートが使用されます。  

  - NetBIOS/SMB - 445 (TCP)  

  - RPC (WMI) - 135 (TCP および UDP)  

  - 動的 RPC。 動的ポートでは、OS バージョンで定義されているポート番号の範囲を使用します。 これらのポートは、エフェメラル ポートとも呼ばれます。 既定のポート範囲の詳細については、「 [Windows のサービス概要およびネットワーク ポート要件](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)」を参照してください。<!-- SCCMDocs#1053 -->

  - SQL Server - ソースおよび移行先サイト データベースの両方で使用される TCP ポート。  

- **ソフトウェア更新プログラムの移行:**  

   ソフトウェア更新プログラムを移行する前に、移行先階層のソフトウェアの更新ポイントを構成する必要があります。 詳細については、「 [ソフトウェア更新プログラムの移行の計画](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates)」をご覧ください。  

- **配布ポイントの共有:**  

   ソース サイトの配布ポイントを共有するためには、移行先階層の少なくとも 1 つのプライマリ サイトまたは中央管理サイトで、クライアントからの要求用にソース サイトと同じポート番号を使用している必要があります。 クライアント要求ポートの詳細については、「[クライアント通信ポートの構成方法](../../core/clients/deploy/configure-client-communication-ports.md)」を参照してください。  

   各ソース サイトでは、FQDN で構成されているサイト システム サーバーにインストールされた配布ポイントのみ共有されます。  

   また、System Center 2012 Configuration Manager または Configuration Manager Current Branch ソース サイトの配布ポイントを共有するには、 **[ソース サイト アカウント]** (ソース サイト サーバーの SMS プロバイダーにアクセスするアカウント) に、ソース サイトの **[サイト]** オブジェクトへの **[変更]** アクセス許可が必要です。 アカウントにこのアクセス許可を付与するには、ロールベースの管理を使用します。 ロール ベース管理の使用方法については、「[Configuration Manager のロール ベース管理の基礎](../../core/understand/fundamentals-of-role-based-administration.md)」を参照してください。  


- **配布ポイントのアップグレードまたは再割り当て:**  

   ソース サイトの SMS プロバイダーからデータを収集するように構成された **[ソース サイトのアクセス アカウント]** には、次のアクセス許可が必要です。  

  - Configuration Manager 2007 配布ポイントをアップグレードするためには、Configuration Manager 2007 ソース サイトから配布ポイントを正常に削除するため、アカウントに Configuration Manager 2007 サイト サーバーの **[サイト]** クラスの **[読み取り]** 、 **[実行]** 、 **[削除]** アクセス許可が必要です。  

  - System Center 2012 Configuration Manager または Configuration Manager Current Branch の配布ポイントを再割り当てするには、アカウントにソース サイトの **[サイト]** オブジェクトへの **[変更]** アクセス許可が必要です。 アカウントにこのアクセス許可を付与するには、ロールベースの管理を使用します。 ロール ベース管理の使用方法については、「[Configuration Manager のロール ベース管理の基礎](../../core/understand/fundamentals-of-role-based-administration.md)」を参照してください。  

    配布ポイントを新しい階層に正常にアップグレードまたは再割り当てするには、ソース階層の配布ポイントを管理するサイトのクライアント要求用に構成されたポートが、配布ポイントを管理する移行先サイトのクライアント要求用に構成されたポートと一致している必要があります。 クライアント要求ポートの詳細については、「[クライアント通信ポートの構成方法](../../core/clients/deploy/configure-client-communication-ports.md)」を参照してください。  
