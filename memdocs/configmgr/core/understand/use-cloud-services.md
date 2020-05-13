---
title: クラウド サービスの使用
titleSuffix: Configuration Manager
description: オンプレミスのインフラストラクチャを補足するための Configuration Manager 用クラウド リソースをプロビジョニングします。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84cb878de3eea56dc68180a83fd4b6a32b2d1073
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906419"
---
# <a name="use-cloud-services-with-configuration-manager"></a>Configuration Manager でのクラウド サービスの使用

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager は、いくつかのクラウド ベースのオプションをサポートしています。 これらは、オンプレミス インフラストラクチャを補完し、次のようなビジネス上の問題を解決することができます。  

-   BYOD を管理する方法 (Intune をモバイル デバイス管理に使用する)  

-   企業ファイアウォール外部のイントラネット上の隔離されたクライアントやリソースに対し、コンテンツ リソースを提供する方法 (クラウドベースの配布ポイントを使用する)  

-   物理ハードウェアを利用できない事情があるときや、個別のニーズに対応するために論理的にハードウェアを導入できないとき、インフラストラクチャをスケールアウトする方法 (Microsoft Azure Virtual Machines を使用する)  

クラウド リソースのプロビジョニングは、Configuration Manager を展開する前に必ず実行しなければならないものではありませんが、階層の設計プランの基礎段階でこれらのオプションを理解しておくと役に立つ場合があります。 クラウド リソースを使用することによって、オンプレミスのインフラストラクチャでは解決できないビジネスの課題に対応すると共に、コストを削減し、時間を短縮することができます。  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Configuration Manager で使用できるクラウド ベースのリソース  
 選択肢によって要件は異なりますが、それぞれの要件を詳しく調査し、前提条件や制限、使用に応じて発生する追加コストなどを把握してください。  

-   クラウドベースの配布ポイントの詳細については、「[クラウドベースの配布ポイントのインストール](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)」を参照してください。

-   Azure の詳細については、「[Azure とは](https://azure.microsoft.com/overview/what-is-azure/)」を参照してください

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Azure 仮想マシン (クラウドベースのインフラストラクチャ用)  
 Configuration Manager は、物理的な企業ネットワーク内でオンプレミスで実行されるコンピューターと同じように、Azure の仮想マシン内で動作するコンピューターの使用をサポートします。 次のシナリオで Azure 仮想マシンを使用することができます。  

-   **シナリオ 1 :** ある仮想マシンで Configuration Manager を実行し、それを使用して、別の仮想マシンにインストールされたクライアントを管理することができます。  

-   **シナリオ 2 :** 仮想マシンで Configuration Manager を実行し、それを使用して Azure で実行されていないクライアントを管理することができます。  

-   **シナリオ 3:** 仮想マシンで複数の Configuration Manager サイト システムの役割を実行しながら、(通信のための適切なネットワーク接続がある) 物理的な企業ネットワークで他の役割を実行することができます。  

物理的な企業ネットワークに Configuration Manager をインストールするときと同じネットワーク、オペレーティング システム、ハードウェアの要件が、Azure での Configuration Manager のインストールにも適用されます。  

Azure の仮想マシンを使用するには、Azure サブスクリプションが必要です。 仮想マシンの使用台数や構成、クラウドベースのリソースの使用に応じた料金が発生します。  

加えて、Azure Virtual Machines で実行している Configuration Manager サイトおよびクライアントには、オンプレミス インストールと同じライセンス要件が課されます。  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Azure サービス (クラウドベースの配布ポイント用)  
 Azure サービスを Configuration Manager 配布ポイントのホストとして使用することができます。これをクラウドベースの配布ポイントと呼びます。 オンプレミスの配布ポイントや、Azure 仮想マシンに展開されている配布ポイントと一緒に、[Configuration Manager でクラウド ベースの配布ポイントを使用](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)できます。  

 これは、サイト システムの役割の展開先の Azure の仮想マシンを使うこととは異なります。 クラウドベースの配布ポイント:  

-   仮想マシン上ではなく Azure でサービスとして実行される。  

-   クライアントからのコンテンツ要求の増加に対応するように自動的に拡張する。  

-   インターネットとイントラネット上のクライアントをサポートする。  

Azure で配布ポイントをホストするには、Azure サブスクリプションが必要です。 サービス間で転送されたデータ量に基づいて料金が発生します。  

### <a name="additional-configuration-manager-capabilities"></a>その他の Configuration Manager の機能  
 Configuration Manager の一部の機能は、次のようなクラウドベースのサービスに接続することができます。  

-   Windows Server Update Services (WSUS)  

-   Configuration Manager の更新プログラムをダウンロードする Configuration Manager サービスのクラウド  

これらの追加機能では、Azure サブスクリプションを所有する必要がありません。 クラウド内の特定の接続、証明書、またはサービスを設定する必要はありません。 これらは Configuration Manager によって自動的に管理されます。 必要なのは、対象となるサイト システムとデバイスからインターネット ベースの URL にアクセスできることを確認するだけです。  

##  <a name="security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a> クラウドベースのサービスのセキュリティ  
 Configuration Manager は証明書を使用して、Azure 内のコンテンツのプロビジョニングとアクセスを行い、使用するサービスを管理します。 Configuration Manager は Azure に保存されるデータを暗号化しますが、Azure が提供する機能以外のセキュリティ機能やデータ制御機能を提供しません。  

 詳細については、クラウドベースのリソースの各種シナリオを参照してください。 「[Azure のセキュリティの概要](https://docs.microsoft.com/azure/security/fundamentals/overview)」も参照してください。
