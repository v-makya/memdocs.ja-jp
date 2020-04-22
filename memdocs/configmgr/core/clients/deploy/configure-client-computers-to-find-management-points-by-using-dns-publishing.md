---
title: DNS 発行を使用するようにクライアントを構成する
titleSuffix: Configuration Manager
description: DNS 発行を使用して管理ポイントを検出するように Configuration Manager クライアント コンピューターを構成します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d28a8a35f711dcef7e3f9adb6dccbabc4082ab28
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693540"
---
# <a name="configure-client-computers-to-find-management-points-by-using-dns-publishing"></a>DNS 発行を使用して、管理ポイントを検出するようにクライアント コンピューターを構成する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のクライアントは、サイトの割り当てを完了しても、実行中のプロセスとして管理対象にとどまるために、管理ポイントを検出する必要があります。 Active Directory ドメイン サービスは、イントラネット上のクライアントが管理ポイントを見つけるのに最も安全な方法を提供します。 しかし、クライアントがこのサービスの場所検索方法を利用できない場合は (たとえば Active Directory スキーマを拡張していない、クライアントがワークグループに所属するなど)、DNS 発行を代替方法として使用します。  

> [!NOTE]  
>  Linux および UNIX 用のクライアントをインストールする場合、最初の接続ポイントとして使用する管理ポイントを使用する必要があります。 Linux と UNIX でクライアントをインストールする方法については、[UNIX および Linux サーバーにクライアントを展開する方法](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)に関するページを参照してください。  

 管理ポイント用に DNS 発行を使用する前に、イントラネット上の DNS サーバーがそのサイトの管理ポイントについて、サービスの場所のリソース レコード (SRV RR) とそれに対応するホスト (A または AAA) のリソース レコードを持っていることを確認してください。 このサービスの場所リソース レコードは、Configuration Manager で自動的に作成することもできますが、DNS でレコードを作成する DNS 管理者によって手動で作成することもできます。  

 Configuration Manager クライアントに対するサービスの場所の検索方法として DNS 発行を使用することの詳細については、[クライアントで Configuration Manager のサイト リソースとサービスを検索する方法についての理解](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)に関するページを参照してください。  

 既定では、クライアントは、クライアントの DNS ドメインで、管理ポイント用の DNS を検索します。 ただし、クライアントのドメインに発行されている管理ポイントが存在しない場合、手動でクライアントに管理ポイントの DNS サフィックスを構成する必要があります。 このクライアントの DNS サフィックスは、クライアントのインストール中、またはインストール後に構成できます。  

-   クライアントのインストール中に、クライアントに管理ポイントのサフィックスを構成するには、CCMSetup Client.msi プロパティを構成します。  

-   クライアントのインストール後に、クライアントに管理ポイントのサフィックスを構成するには、コントロールパネルで、 **[Configuration Manager のプロパティ]** を構成します。  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>クライアントのインストール中に、クライアントに管理ポイントのサフィックスを構成するには  

- 次の CCMSetup client.msi プロパティを使用してクライアントをインストールします。  

  - **DNSSUFFIX=** *&lt;管理ポイント ドメイン\>*  

     サイトに複数の管理ポイントがあり、その管理ポイントが複数のドメインに存在する場合は、一つのドメインだけを指定します。 このドメインの管理ポイントにクライアントが接続すると、クライアントは、使用可能な管理ポイントの一覧をダウンロードします。この一覧には、ほかのドメインにある管理ポイントも含まれます。  

    CCMSetup コマンド ライン プロパティの詳細については、[クライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)に関するページを参照してください。  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>クライアントのインストール後に、クライアントに管理ポイントのサフィックスを構成するには  

1.  クライアント コンピューターのコントロール パネルで、 **Configuration Manager**に移動し、 **[プロパティ]** をダブルクリックします。  

2.  **[サイト]** タブで管理ポイントの DNS サフィックスを指定してから、 **[OK]** をクリックします。  

     サイトに複数の管理ポイントがあり、その管理ポイントが複数のドメインに存在する場合は、一つのドメインだけを指定します。 このドメインの管理ポイントにクライアントが接続すると、クライアントは、使用可能な管理ポイントの一覧をダウンロードします。この一覧には、ほかのドメインにある管理ポイントも含まれます。
