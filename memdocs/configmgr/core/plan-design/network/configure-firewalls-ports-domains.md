---
title: ネットワーク インフラストラクチャ
titleSuffix: Configuration Manager
description: Configuration Manager 通信の準備としてファイアウォール、ポート、ドメインを設定します。
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703090"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Configuration Manager のネットワーク インフラストラクチャの考慮事項

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager をサポートするようにネットワークを準備するには、いくつかのインフラストラクチャ コンポーネントを構成する必要があります。 たとえば、Configuration Manager が使用する通信が通過するようにファイアウォールのポートを開きます。  

## <a name="ports-and-protocols"></a>ポートとプロトコル

Configuration Manager 機能によって、使用されるネットワーク ポートは異なります。 必須のポートもあれば、カスタマイズできるものもあります。

ほとんどの Configuration Manager 通信では、HTTP にはポート 80、HTTPS にはポート 443 など、共通のポートを使用します。 一部のサイト システムの役割では、カスタム Web サイトとカスタム ポートの使用をサポートしています。 詳細については、[サイト システム サーバーの Web サイト](websites-for-site-system-servers.md)のページを参照してください。

Configuration Manager を展開する前に、使用する予定のポートを特定し、必要に応じてファイアウォールを設定します。

Configuration Manager をインストールした後、ポートを変更する必要がある場合は、デバイスとネットワークのファイアウォールを必ず更新します。 また、Configuration Manager でポートの構成も変更します。

詳細については、以下の記事を参照してください。

- [クライアント通信ポートを構成する方法](../../clients/deploy/configure-client-communication-ports.md)
- [Configuration Manager で使用されるポート](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>インターネット アクセス要件

一部の Configuration Manager 機能をすべて利用するには、インターネット接続が必要です。 組織がファイアウォールまたはプロキシ デバイスを使用してインターネットとのネットワーク通信を制限している場合は、必要なエンドポイントを許可する必要があります。

詳細については、「[Internet access requirements (インターネット アクセスの要件)](internet-endpoints.md)」を参照してください


## <a name="proxy-servers"></a>プロキシ サーバー

異なるサイト システム サーバーとクライアントに対して別のプロキシ サーバーを指定することができます。 サイト システムの役割またはクライアントをインストールするときにこれらの構成を行うか、後で必要に応じて変更します。

詳細については、「[プロキシ サーバーのサポート](proxy-server-support.md)」を参照してください。
