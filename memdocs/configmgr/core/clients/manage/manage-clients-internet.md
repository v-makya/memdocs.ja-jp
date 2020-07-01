---
title: インターネット上のクライアントを管理する
titleSuffix: Configuration Manager
description: Configuration Manager でクラウド管理ゲートウェイとインターネット ベースのクライアント管理を使用するクライアント管理について説明します。
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715596"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>インターネット上のクライアントを Configuration Manager で管理する

*適用対象:Configuration Manager (Current Branch)*

通常、Configuration Manager では、ほとんどのマネージド コンピューターとサーバーは、管理機能を実行するサイト システム サーバーと物理的に同じ内部ネットワーク上にあります。 ただし、インターネットに接続している場合は、内部ネットワークの外部にあるクライアントを管理できます。 この機能では、クライアントがサイト システム サーバーに到達するために VPN 経由で接続する必要はありません。

Configuration Manager では、インターネットに接続されているクライアントを 2 つの方法で管理できます。

- クラウド管理ゲートウェイ

- インターネット ベースのクライアント管理

> [!NOTE]
> 1 つのサイトに対して両方のサービスを組み合わせることができます。 デバイスで、IBCM と CMG の両方についてポリシーがサイトから取得される場合、それらの間で通信のためにランダム化されます。 通信の制御に使用できるメカニズムは、クライアント認証のみです。 たとえば、Azure AD に参加しているクライアントで、インターネットベースの管理ポイントのサーバー認証証明書が信頼されていない場合、使用できるのは CMG のみです。 ドメインに参加しているクライアントで CMG のサーバー認証証明書が信頼されていない場合、使用できるのはインターネットベースの管理ポイントのみです。<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>クラウド管理ゲートウェイ

クラウド管理ゲートウェイには、インターネットベースのクライアントの管理機能があります。 Microsoft Azure クラウド サービスと、そのサービスと通信するオンプレミスのサイト システム ロールの組み合わせが使用されます。 インターネットベースのクライアントは、クラウド サービスを使用してオンプレミスの Configuration Manager と通信します。

### <a name="cmg-advantages"></a>CMG の利点

- オンプレミス インフラストラクチャの追加投資は必要ありません。  

- オンプレミス インフラストラクチャをインターネットに公開しません。  

- このサービスを実行するクラウド仮想マシンは Azure により完全管理され、保守管理を必要としません。  

- Configuration Manager コンソールで簡単にセットアップし、構成できます。  

### <a name="cmg-disadvantages"></a>CMG の欠点  

- クラウド サブスクリプションにコストがかかります。  

- 管理データがクラウド サービス経由で送信されます。  

詳細については、「[クラウド管理ゲートウェイの計画](cmg/plan-cloud-management-gateway.md)」を参照してください。  

## <a name="internet-based-client-management"></a>インターネット ベースのクライアント管理

この方法は、管理目的でクライアントが直接通信する、インターネットに接続されたサイト システム サーバーに依存します。 クライアントとサイト システム サーバーにインターネットベースのクライアント管理 (IBCM) を構成する必要があります。

### <a name="ibcm-advantages"></a>IBCM の利点

- クラウド サービスの依存関係はありません。  

- クラウド サブスクリプションに関連する追加コストはありません。  

- サービスを提供するサーバーとロールを完全制御できます。  

### <a name="ibcm-disadvantages"></a>IBCM の欠点

- インフラストラクチャの追加投資が必要です。  

- 追加のインフラストラクチャに運用費と間接費がかかります。  

- インフラストラクチャをインターネットに公開する必要があります。  

詳細については、[インターネット ベースのクライアント管理の計画](plan-internet-based-client-management.md)に関するページを参照してください。  
