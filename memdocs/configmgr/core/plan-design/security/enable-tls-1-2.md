---
title: トランスポート層セキュリティ (TLS) 1.2 の有効化の概要
titleSuffix: Configuration Manager
description: Configuration Manager に対して TLS 1.2 を有効にする方法の概要。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e1334603bcf60ea3eb8c3d18b73d511570cdc5d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699740"
---
# <a name="how-to-enable-tls-12"></a>TLS 1.2 を有効にする方法

*適用対象:Configuration Manager (Current Branch)*

Secure Sockets Layer (SSL) などのトランスポート層セキュリティ (TLS) は、ネットワーク経由で転送されるデータのセキュリティ保護を目的とした暗号化プロトコルです。 これらの記事では、Configuration Manager のセキュリティで保護された通信で TLS 1.2 プロトコルが確実に使用されるようにするために必要な手順について説明します。 また、これらの記事では、よく使用されるコンポーネントの更新の要件と、一般的な問題のトラブルシューティングについても説明します。

## <a name="enabling-tls-12"></a>TLS 1.2 を有効にする

Configuration Manager は、セキュリティで保護された通信のためにさまざまなコンポーネントに依存しています。 特定の接続に使用されるプロトコルでは、クライアント側とサーバー側の両方で、関連するコンポーネントの機能が利用されます。 いずれかのコンポーネントが古い場合、または適切に構成されていない場合は、古く安全性の低いプロトコルが通信に使用される可能性があります。 Configuration Manager ですべてのセキュリティ保護された通信に対して適切に TLS 1.2 をサポートできるようにするには、必要なすべてのコンポーネントで TLS 1.2 を有効にする必要があります。 必要なコンポーネントは、環境と使用する Configuration Manager の機能によって異なります。

> [!IMPORTANT]
> このプロセスはクライアントから、特に以前のバージョンの Windows から開始します。 Configuration Manager サーバーで TLS 1.2 を有効にして、古いプロトコルを無効にする前に、すべてのクライアントが TLS 1.2 に対応していることを確認します。 そうでない場合、クライアントはサーバーと通信できず、孤立する可能性があります。


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Configuration Manager クライアント、サイト サーバー、リモート サイト システムでのタスク

Configuration Manager がセキュリティ保護された通信のために依存するコンポーネントで TLS 1.2 を有効にするには、クライアントとサイト サーバーの両方で複数のタスクを実行する必要があります。

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Configuration Manager クライアントで TLS 1.2 を有効にする

- [Windows 8.0、Windows Server 2012 (R2 以外) 以前の Windows および WinHTTP を更新する](enable-tls-1-2-client.md#bkmk_winhttp)
- [オペレーティング システム レベルで SChannel のプロトコルとして TLS 1.2 を確実に有効にする](enable-tls-1-2-client.md#bkmk_protocol)
- [TLS 1.2 をサポートするように .NET Framework を更新して構成する](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Configuration Manager サイト サーバーとリモート サイト システムで TLS 1.2 を有効にする

- [オペレーティング システム レベルで SChannel のプロトコルとして TLS 1.2 を確実に有効にする](enable-tls-1-2-server.md#bkmk_protocol)
- [TLS 1.2 をサポートするように .NET Framework を更新して構成する](enable-tls-1-2-server.md#bkmk_net)
- [SQL Server と SQL Native Client を更新する](enable-tls-1-2-server.md#bkmk_sql)
- [Windows Server Update Services (WSUS) を更新する](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>機能とシナリオの依存関係

このセクションでは、Configuration Manager の特定の機能とシナリオの依存関係について説明します。 次の手順を決定するには、お客様の環境に適用される項目を見つけてください。

|機能またはシナリオ|更新タスク|
|--- |--- |
|サイト サーバー (中央、プライマリ、またはセカンダリ)| - [.NET Framework を更新する](enable-tls-1-2-server.md#bkmk_net)<br/> - 強力な暗号化設定を確認する|
|サイト データベース サーバー|[SQL Server とそのクライアント コンポーネントを更新する](enable-tls-1-2-server.md#bkmk_sql)|
|セカンダリ サイト サーバー|[SQL Server とそのクライアント コンポーネントを更新](enable-tls-1-2-server.md#bkmk_sql)して、準拠しているバージョンの SQL Express にする|
|サイト システムの役割| - [.NET Framework を更新](enable-tls-1-2-server.md#bkmk_net)し、強力な暗号化設定を確認する <br/> - それを必要とする役割で [SQL Server とそのクライアント コンポーネントを更新する](enable-tls-1-2-server.md#bkmk_sql) ([SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client) など)|
|レポート サービス ポイント|- サイト サーバー、SQL Reporting Services サーバー、およびコンソールを使う任意のサーバー上で [.NET Framework を更新する](enable-tls-1-2-server.md#bkmk_net)<br/> - 必要に応じて SMS_Executive サービスを再起動する|
|ソフトウェアの更新ポイント|[WSUS を更新する](enable-tls-1-2-server.md#bkmk_wsus)|
|クラウド管理ゲートウェイ|[TLS 1.2 を強制する](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Configuration Manager コンソール| - [.NET Framework を更新する](enable-tls-1-2-client.md#bkmk_net)<br/> - 強力な暗号化設定を確認する|
|HTTPS サイト システムの役割を持つ構成マネージャー クライアント|[WinHTTP を使用し、クライアントとサーバー間の通信で TLS 1.2 をサポートするように Windows を更新する](enable-tls-1-2-client.md#bkmk_winhttp)|
|ソフトウェア センター| - [.NET Framework を更新する](enable-tls-1-2-client.md#bkmk_net)<br/> - 強力な暗号化設定を確認する|
|Windows 7 クライアント| あらゆるサーバー コンポーネント上で TLS 1.2 を有効にする "*前に*"、[WinHTTP を使って、クライアントとサーバー間の通信で TLS 1.2 をサポートするように Windows を更新します](enable-tls-1-2-client.md#bkmk_winhttp)。 最初にサーバー コンポーネント上で TLS 1.2 を有効にすると、以前のバージョンのクライアントが孤立する可能性があります。|

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="why-use-tls-12-with-configuration-manager"></a>なぜ Configuration Manager で TLS 1.2 を使用するのですか?

TLS 1.2 は、SSL 2.0、SSL 3.0、TLS 1.0、TLS 1.1 などの以前の暗号化プロトコルより安全性が高くなっています。 基本的に、TLS 1.2 を使うと、より安全にネットワーク経由でデータを転送できます。

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Configuration Manager ではどのような場合に TLS 1.2 などの暗号化プロトコルが使われますか?

基本的に、Configuration Manager で TLS 1.2 のような暗号化プロトコルが使われる領域は次の 5 つです。

- IIS ベースのサイト サーバーの役割が HTTPS を使用するように構成されている場合の、役割へのクライアント通信。 このような役割の例としては、配布ポイント、ソフトウェアの更新ポイント、管理ポイントなどがあります。
- 管理ポイント、SMS Executive、SMS プロバイダーと SQL との通信。 Configuration Manager では、SQL 通信は常に暗号化されます。
- WSUS が HTTPS を使用するように構成されている場合の、サイト サーバーから WSUS への通信。
- SQL Reporting Services (SSRS) が HTTPS を使用するように構成されている場合の、SSRS に対する Configuration Manager コンソール。
- インターネット ベースのサービスへのすべての接続。 たとえば、クラウド管理ゲートウェイ (CMG)、サービス接続ポイントの同期、Microsoft Update からの更新メタデータの同期などです。

### <a name="what-determines-which-encryption-protocol-is-used"></a>使用される暗号化プロトコルはどのようにして決定されますか?

暗号化された会話の場合、HTTPS では、クライアントとサーバーの両方でサポートされている最も高いバージョンのプロトコルが、常にネゴシエートされます。 接続が確立されるとき、クライアントからサーバーに使用可能な最も高いプロトコルでメッセージが送信されます。 サーバーで同じバージョンがサポートされている場合は、そのバージョンを使用してメッセージが送信されます。 このネゴシエートされたバージョンが、接続に使用されます。 クライアントによって示されたバージョンがサーバーでサポートされていない場合は、サーバーのメッセージで、使用できる最も高いバージョンが指定されます。 TLS ハンドシェイク プロトコルについて詳しくは、「[TLS を使用してセキュリティで保護されたセッションを確立する](/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls)」を参照してください。

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>クライアントとサーバーが使用できるプロトコル バージョンはどのようにして決定されますか?

一般に、次の項目により、使用されるプロトコル バージョンを決定できます。

- アプリケーションでは、ネゴシエートする特定のプロトコル バージョンを指定できます。
  - ベスト プラクティスとしては、アプリケーションレ ベルで特定のプロトコル バージョンをハード コーディングすることは避け、コンポーネントとオペレーティング システムのプロトコル レベルで定義されている構成に従います。
  - Configuration Manager は、このベスト プラクティスに従います。
- .NET Framework を使用して作成されているアプリケーションの場合、既定のプロトコルのバージョンは、フレームワークがコンパイルされたバージョンによって決まります。  
  - 既定では、4.6.3 より前のバージョンの .NET では、ネゴシエーション対象のプロトコルの一覧に TLS 1.1 と 1.2 は含まれていませんでした。
- Configuration Manager クライアントのように、HTTPS 通信に WinHTTP を使用するアプリケーションでは、オペレーティング システムのバージョン、パッチ レベル、プロトコル バージョン サポートの構成によって決まります。


## <a name="additional-resources"></a>その他のリソース

- [暗号化コントロールのテクニカル リファレンス](cryptographic-controls-technical-reference.md)
- [.NET Framework でのトランスポート層セキュリティ (TLS) のベスト プラクティス](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244:Microsoft SQL Server 用の TLS 1.2 のサポート](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>次のステップ

- [クライアントで TLS 1.2 を有効にする](enable-tls-1-2-client.md)
- [サイト サーバーで TLS 1.2 を有効にする](enable-tls-1-2-server.md)