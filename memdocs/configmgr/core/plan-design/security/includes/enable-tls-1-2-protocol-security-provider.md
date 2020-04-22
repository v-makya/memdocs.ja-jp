---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704080"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 は既定で有効です。 したがって、有効にするためにこれらのキーを変更する必要はありません。 これらの記事の残りのガイダンスに従い、TLS 1.2 のみを有効にして環境が機能することを確認した後、[`Protocols`] で TLS 1.0 と TLS 1.1 を無効にするように変更することができます。

`\SecurityProviders\SCHANNEL\Protocols`.NET Framework でのトランスポート層セキュリティ (TLS) のベスト プラクティス[に関するページの説明に従って、](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry) レジストリ サブキー設定を確認します。

