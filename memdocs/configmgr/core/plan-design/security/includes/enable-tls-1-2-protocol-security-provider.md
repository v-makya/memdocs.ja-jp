---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: f14713431c71c1f3625d13ea4be1d919b072e273
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703822"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 は既定で有効です。 したがって、有効にするためにこれらのキーを変更する必要はありません。 これらの記事の残りのガイダンスに従い、TLS 1.2 のみを有効にして環境が機能することを確認した後、[`Protocols`] で TLS 1.0 と TLS 1.1 を無効にするように変更することができます。

[.NET Framework でのトランスポート層セキュリティ (TLS) のベスト プラクティス](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)に関するページの説明に従って、`\SecurityProviders\SCHANNEL\Protocols` レジストリ サブキー設定を確認します。