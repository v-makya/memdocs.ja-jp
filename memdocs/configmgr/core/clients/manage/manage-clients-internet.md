---
title: インターネット上のクライアントを管理する
titleSuffix: Configuration Manager
description: Configuration Manager でクラウド管理ゲートウェイとインターネット ベースのクライアント管理を使用するクライアント管理について説明します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c00d480b993498c5fa27e2a4d91a5f2a3bc130ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690030"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>インターネット上のクライアントを Configuration Manager で管理する

*適用対象:Configuration Manager (Current Branch)*

通常、Configuration Manager では、ほとんどのマネージド コンピューターとサーバーは、管理機能を実行するサイト システム サーバーと物理的に同じ内部ネットワーク上にあります。 ただし、インターネットに接続している場合は、内部ネットワークの外部にあるクライアントを管理できます。 この機能では、クライアントがサイト システム サーバーに到達するために VPN 経由で接続する必要はありません。

Configuration Manager では、インターネットに接続されているクライアントを 2 つの方法で管理できます。

-   クラウド管理ゲートウェイ

-   インターネット ベースのクライアント管理


## <a name="cloud-management-gateway"></a>クラウド管理ゲートウェイ

クラウド管理ゲートウェイには、インターネットベースのクライアントの管理機能があります。 Microsoft Azure クラウド サービスと、そのサービスと通信する新しいサイト システム ロールの組み合わせが使用されます。 インターネットベースのクライアントは、クラウド サービスを使用してオンプレミスの Configuration Manager と通信します。

#### <a name="advantages"></a>長所  

-   オンプレミス インフラストラクチャの追加投資は必要ありません。  

-   オンプレミス インフラストラクチャをインターネットに公開しません。  

-   このサービスを実行するクラウド仮想マシンは Azure により完全管理され、保守管理を必要としません。  

-   Configuration Manager コンソールで簡単にセットアップし、構成できます。  

#### <a name="disadvantages"></a>短所  

-   クラウド サブスクリプションにコストがかかります。  

-   管理データがクラウド サービス経由で送信されます。  

詳細については、「[クラウド管理ゲートウェイの計画](cmg/plan-cloud-management-gateway.md)」を参照してください。  



## <a name="internet-based-client-management"></a>インターネット ベースのクライアント管理

この方法は、管理目的でクライアントが通信する、インターネットに接続されたサイト システム サーバーに依存します。 クライアントとサイト システム サーバーにインターネット ベースの管理を構成する必要があります。

#### <a name="advantages"></a>長所  

-   クラウド サービスの依存関係はありません。  

-   クラウド サブスクリプションに関連する追加コストはありません。  

-   サービスを提供するサーバーとロールを完全制御できます。  

#### <a name="disadvantages"></a>短所  

-   インフラストラクチャの追加投資が必要です。  

-   追加のインフラストラクチャに運用費と間接費がかかります。  

-   インフラストラクチャをインターネットに公開する必要があります。  

詳細については、[インターネット ベースのクライアント管理の計画](plan-internet-based-client-management.md)に関するページを参照してください。  
