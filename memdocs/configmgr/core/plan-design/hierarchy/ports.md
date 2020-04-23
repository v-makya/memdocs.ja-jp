---
title: 接続に使用するポート
titleSuffix: Configuration Manager
description: Configuration Manager が接続に使用する必要なポートとカスタマイズ可能なネットワーク ポートについて説明します。
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0bb4f3f3dfcddaa12a8c6f3fffbe59954b10964a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704490"
---
# <a name="ports-used-in-configuration-manager"></a>Configuration Manager で使用されるポート

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager が使用するネットワーク ポートを一覧表示します。 接続によっては、構成不可能なポートを使用する場合も、ユーザーが指定するカスタム ポートをサポートする場合もあります。 任意のポート フィルター処理テクノロジを使用する場合は、必要なポートが使用できることを確認してください。 これらのポート フィルター処理テクノロジには、ファイアウォール、ルーター、プロキシ サーバー、IPsec などが含まれます。   

> [!NOTE]  
> SSL ブリッジを使用してインターネットベースのクライアントをサポートする場合は、特定の HTTP 動詞とヘッダーでファイアウォールの通過を許可することが必要になることもあります。   



##  <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> 構成できるポート  
Configuration Manager では、次の種類の通信でポートを構成できます。  

- アプリケーション カタログ Web サイト ポイントからアプリケーション カタログ Web サービス ポイントへの通信  

- 登録プロキシ ポイントから登録ポイントへの通信  

- クライアントから IIS を実行するサイト システムへの通信  

- クライアントからインターネットへの通信 (プロキシ サーバー設定として)  

- ソフトウェアの更新ポイントからインターネットへの通信 (プロキシ サーバー設定として)  

- ソフトウェアの更新ポイントから WSUS サーバーへの通信  

- サイト サーバーからサイト データベース サーバーへの通信  

- サイト サーバーから WSUS データベース サーバーへ

- レポート サービス ポイント  

  > [!NOTE]  
  > レポート サービス ポイントのサイト システムの役割に使用されるポートは、SQL Server Reporting Services で構成されます。 レポート サービス ポイントとの通信中に、Configuration Manager によりこれらのポートが使用されます。 IPsec ポリシーまたはファイアウォールの構成用に IP フィルターの情報を定義する各ポートを確認しておいてください。  

既定では、クライアントからサイト システムへの通信に使用する HTTP ポートは 80、既定の HTTPS ポートは 443 です。 クライアントとサイト システム間の HTTP または HTTPS 通信に使用するポートは、セットアップ中に変更することも、Configuration Manager サイトのサイト プロパティで変更することもできます。  

レポート サービス ポイントのサイト システムの役割に使用されるポートは、SQL Server Reporting Services で構成されます。 レポート サービス ポイントとの通信中に、Configuration Manager によりこれらのポートが使用されます。 IPsec ポリシーまたはファイアウォールの構成用に IP フィルターの情報を定義する場合に、各ポートを確認しておいてください。  



##  <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> 構成不可能なポート  

Configuration Manager では、次の種類の通信用にポートを構成することはできません。  

- サイト間の通信  

- サイト サーバーからサイト システムへの通信  

- Configuration Manager コンソールから SMS プロバイダーへの通信  

- Configuration Manager コンソールからインターネットへの通信  

- クラウド サービスへの接続 (Microsoft Intune やクラウド配布ポイントなど)  



##  <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Configuration Manager クライアントとサイト システムで使用されるポート  

次のセクションでは、Configuration Manager で通信に使用されるポートについて詳しく説明します。 セクションのタイトルの矢印は、通信の方向を示します。  

- -- > は、一方のコンピューターが通信を開始し、他方のコンピューターが常に応答する状態を示します  

- &lt; -- > は、どちらのコンピューターからも通信を開始できる状態を示します  


###  <a name="asset-intelligence-synchronization-point-----microsoft"></a><a name="BKMK_PortsAI"></a> 資産インテリジェンス同期ポイント -- > Microsoft  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="asset-intelligence-synchronization-point-----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> 資産インテリジェンス同期ポイント -- > SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="application-catalog-web-service-point-----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> アプリケーション カタログ Web サービス ポイント -- > SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="application-catalog-website-point-----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> アプリケーション カタログ Web サイト ポイント -- > アプリケーション カタログ Web サービス ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="client-----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> クライアント -- > アプリケーション カタログ Web サイト ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="client-----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> クライアント -- &gt; クライアント  

この表に一覧表示されているポートの他に、ウェイク アップ プロキシも、クライアント間の ICMP エコー要求メッセージを使用します。 クライアントはこの通信を使用して、他のクライアントがネットワークで起動しているかどうかを確認します。 ICMP は Ping コマンドとも呼ばれます。 ICMP には UDP または TCP プロトコル番号がないため、次の表には記載されていません。 ただし、サブネット内のこのようなクライアント コンピューターまたは介在するネットワーク デバイスに、ホストベースのファイアウォールがある場合、ウェイクアップ プロキシ通信が正常に実行されるように、そのファイアウォールで ICMP トラフィックを許可する必要があります。  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|--|  
|ウェイクアップ プロキシ|25536 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|--|  
|Windows PE ピア キャッシュのブロードキャスト|8004|--|  
|Windows PE ピア キャッシュのダウンロード|--|8003|  

詳細については、「[Windows PE ピア キャッシュ](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements)」をご覧ください。


###  <a name="client-----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> クライアント -- > Configuration Manager ネットワーク デバイス登録サービス (NDES) ポリシー モジュール   

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  


###  <a name="client-----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> クライアント -- > クラウド配布ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

詳細については、「[ポートとデータ フロー](use-a-cloud-based-distribution-point.md#bkmk_dataflow)」を参照してください。


###  <a name="client-----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> クライアント -- > クラウド管理ゲートウェイ (CMG)  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

詳細については、CMG の「[ポートとデータ フロー](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)」を参照してください。


###  <a name="client-----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> クライアント -- > 配布ポイント (標準とプルの両方)  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="client-----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> クライアント -- > マルチキャスト向けに構成された配布ポイント (標準とプルの両方)  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|マルチキャスト プロトコル|63000-64000|--|  

###  <a name="client-----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> クライアント -- > PXE 向けに構成された配布ポイント (標準とプルの両方)  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 および 68|--|  
|TFTP|69 <sup>[注 4](#bkmk_note4)</sup> |--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

> [!Important]  
> ホストベースのファイアウォールを有効にした場合は、規則でこれらのポートでのサーバーの送受信が許可されることを確認します。 PXE 用の配布ポイントを有効にすると、Configuration Manager で Windows ファイアウォールの受信規則を有効にすることができます。 送信規則は構成されません。<!--SCCMDocs issue #744-->  


###  <a name="client-----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> クライアント -- > フォールバック ステータス ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="client-----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> クライアント -- > グローバル カタログ ドメイン コントローラー  
Configuration Manager クライアントは、ワークグループ コンピューターである場合やインターネットのみの通信用に構成されている場合、グローバル カタログ サーバーに接続しません。  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|グローバル カタログ LDAP|--|3268|  


###  <a name="client-----management-point"></a><a name="BKMK_PortsClient-MP"></a> クライアント -- > 管理ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|クライアント通知 (代替で HTTP または HTTPS が使用される前の既定の通信)|--|10123 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|HTTP|--|80 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="client-----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> クライアント -- > ソフトウェアの更新ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 または 8530 <sup>[注 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 または 8531 <sup>[注 3](#bkmk_note3)</sup>|  


###  <a name="client-----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> クライアント -- > 状態移行ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|サーバー メッセージ ブロック (SMB)|--|445|  


###  <a name="cmg-connection-point-----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> CMG 接続ポイント -- > CMG クラウド サービス  

Configuration Manager では、これらの接続を使用して CMG チャネルを構築します。 詳細については、CMG の「[ポートとデータ フロー](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)」を参照してください。

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (推奨)|--|10140-10155|  
|HTTPS (1 つの VM でフォールバック)|--|443|  
|HTTPS (複数の VM でフォールバック)|--|10124-10139|  


###  <a name="cmg-connection-point-----management-point"></a><a name="bkmk_cmgcp-mp"></a> CMG 接続ポイント -- > 管理ポイント  

#### <a name="version-1706-or-1710"></a>バージョン 1706 または 1710
特定のポートは管理ポイント構成に依存します。 

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

#### <a name="version-1802"></a>バージョン 1802

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

詳細については、CMG の「[ポートとデータ フロー](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)」を参照してください。


###  <a name="cmg-connection-point-----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> CMG 接続ポイント -- > ソフトウェアの更新ポイント  

特定のポートはソフトウェアの更新ポイント構成に依存します。 

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

詳細については、CMG の「[ポートとデータ フロー](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)」を参照してください。


###  <a name="configuration-manager-console-----client"></a><a name="BKMK_PortsConsole-Client"></a> Configuration Manager コンソール -- > クライアント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|リモート コントロール (コントロール)|--|2701|  
|リモート アシスタンス (RDP および RTC)|--|3389|  


###  <a name="configuration-manager-console-----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Configuration Manager コンソール -- > インターネット  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

Configuration Manager コンソールは、次のアクションにインターネット アクセスを使います。 
- Microsoft Update からの展開パッケージ用ソフトウェア更新プログラムのダウンロード。
- リボンのフィードバック項目。
- コンソール内のドキュメントへのリンク。
<!--506823-->


###  <a name="configuration-manager-console-----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Configuration Manager コンソール -- > レポート サービス ポイント  


|[説明]|UDP|TCP|
|-----------------|---------|---------|   
|HTTP|--|80 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="configuration-manager-console-----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Configuration Manager コンソール -- > サイト サーバー  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (プロバイダー システムを特定するための WMI への初期接続)|--|135|  


###  <a name="configuration-manager-console-----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Configuration Manager コンソール -- > SMS プロバイダー  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module-----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager ネットワーク デバイス登録サービス (NDES) ポリシー モジュール -- > 証明書登録ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="data-warehouse-service-point-----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> データ ウェアハウス サービス ポイント -- > SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="distribution-point-both-standard-and-pull-----management-point"></a><a name="BKMK_PortsDist_MP"></a> 配布ポイント (標準とプルの両方) -- > の管理ポイント  
配布ポイントは次のシナリオで管理ポイントと通信します。  

- 事前設定されたコンテンツのステータスをレポートする  

- 使用状況の概要データをレポートする  

- コンテンツの検証をレポートする  

- パッケージのダウンロード (プル配布ポイントのみ) のステータスをレポートする

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="endpoint-protection-point-----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection ポイント -- > インターネット  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  


###  <a name="endpoint-protection-point-----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection ポイント -- > SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="enrollment-proxy-point-----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> 登録プロキシ ポイント -- > 登録ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="enrollment-point-----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> 登録ポイント -- > SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="exchange-server-connector-----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server コネクタ -- &gt; Exchange Online  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS 経由の Windows リモート管理|--|5986|  


###  <a name="exchange-server-connector-----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server コネクタ -- > 社内の Exchange Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP 経由の Windows リモート管理|--|5985|  


###  <a name="mac-computer-----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac コンピューター -- > 登録プロキシ ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="management-point-----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> 管理ポイント -- > ドメイン コントローラー  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|ライトウェイト ディレクトリ アクセス プロトコル (LDAP)|389|389|  
|グローバル カタログ LDAP|--|3268|  
|RPC エンドポイント マッパー|--|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="management-point-lt-----site-server"></a><a name="BKMK_PortsMP-Site"></a> 管理ポイント &lt; -- > サイト サーバー  
<sup>[注 5](#bkmk_note5)</sup>   

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|RPC エンドポイント マッパー|--|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  
|サーバー メッセージ ブロック (SMB)|--|445|  


###  <a name="management-point-----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> 管理ポイント -- > SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="mobile-device-----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> モバイル デバイス -- > 登録プロキシ ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="mobile-device-----microsoft-intune"></a><a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> モバイル デバイス -- > Microsoft Intune  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="reporting-services-point-----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> レポート サービス ポイント -- > SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="service-connection-point-----microsoft-intune"></a><a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> サービス接続ポイント -- > Microsoft Intune  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

詳しくは、サービス接続ポイントの「[インターネット アクセス要件](../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls)」をご覧ください。


###  <a name="service-connection-point-----azure-cmg"></a><a name="bkmk_scp-cmg"></a> サービス接続ポイント -- > Azure (CMG)  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|CMG サービス展開用の HTTPS|--|443|

詳細については、CMG の「[ポートとデータ フロー](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)」を参照してください。


###  <a name="site-server-lt-----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> サイト サーバー &lt; -- > アプリケーション カタログ Web サービス ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> サイト サーバー &lt; -- > アプリケーション カタログ Web サイト ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> サイト サーバー &lt; -- > 資産インテリジェンス同期ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-----client"></a><a name="BKMK_PortsSite-Client"></a> サイト サーバー -- > クライアント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|--|  


###  <a name="site-server-----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> サイト サーバー -- > クラウド配布ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

詳細については、「[ポートとデータ フロー](use-a-cloud-based-distribution-point.md#bkmk_dataflow)」を参照してください。


###  <a name="site-server-----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> サイト サーバー -- > 配布ポイント (標準とプルの両方)  
 <sup>[注 5](#bkmk_note5)</sup>  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> サイト サーバー -- > ドメイン コントローラー  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|ライトウェイト ディレクトリ アクセス プロトコル (LDAP)|389|389|  
|グローバル カタログ LDAP|--|3268|  
|RPC エンドポイント マッパー|--|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> サイト サーバー &lt; -- > 証明書登録ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> サイト サーバー &lt; -- > Endpoint Protection ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> サイト サーバー &lt; -- > 登録ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> サイト サーバー &lt; -- > 登録プロキシ ポイント  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> サイト サーバー &lt; -- > フォールバック ステータス ポイント  
 <sup>[注 5](#bkmk_note5)</sup>  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-----internet"></a><a name="BKMK_PortSite-Internet"></a> サイト サーバー -- > インターネット  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[注 1](#bkmk_note1)</sup>|  


###  <a name="site-server-lt-----issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> サイト サーバー &lt; -- > 発行元の証明機関 (CA)  
 この通信は、証明書登録ポイントを使用して、証明書プロファイルを展開するときに使用します。 通信は階層内のすべてのサイト サーバーで使用されるわけではありません。 代わりに、階層の最上位のサイト サーバーでのみ使用されます。  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|RPC エンドポイント マッパー|135|135|  
|RPC (DCOM)|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> サイト サーバー --> リモート コンテンツ ライブラリ共有をホストするサーバー  
バージョン 1806 以降、 コンテンツ ライブラリを別のストレージの場所に再配置して、中央管理サーバーまたはプライマリ サイト サーバー上のハード ドライブ スペースを解放できるようになりました。 詳細については、「[サイト サーバーのリモート コンテンツ ライブラリを構成する](the-content-library.md#bkmk_remote)」を参照してください。  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  


###  <a name="site-server-lt-----reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> サイト サーバー &lt; -- > レポート サービス ポイント  
 <sup>[注 5](#bkmk_note5)</sup>  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----site-server"></a><a name="BKMK_PortsSite-Site"></a> サイト サーバー &lt; -- > サイト サーバー  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  


###  <a name="site-server-----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> サイト サーバー -- > SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  

 サイト データベースをリモート SQL Server でホストするサイトをインストールするときに、サイト サーバーと SQL Server 間の次のポートを開きます。  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  

###  <a name="site-server-----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> サイト サーバー -- > WSUS 用 SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 3](#bkmk_note3) 代替ポートを利用可能</sup>|  

###  <a name="site-server-----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> サイト サーバー -- > SMS プロバイダー  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC <sup>[注 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> サイト サーバー &lt; -- > ソフトウェアの更新ポイント  
 <sup>[注 5](#bkmk_note5)</sup>  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|HTTP|--|80 または 8530 <sup>[注 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 または 8531 <sup>[注 3](#bkmk_note3)</sup>|  


###  <a name="site-server-lt-----state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> サイト サーバー &lt; -- > 状態移行ポイント  
 <sup>[注 5](#bkmk_note5)</sup>  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  


###  <a name="sms-provider-----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> SMS プロバイダー -- &gt; SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="software-update-point-----internet"></a><a name="BKMK_PortsSUP-Internet"></a> ソフトウェアの更新ポイント -- > インターネット  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[注 1](#bkmk_note1)</sup>|  


###  <a name="software-update-point-----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> ソフトウェアの更新ポイント -- > 上流の WSUS サーバー  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 または 8530 <sup>[注 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 または 8531 <sup>[注 3](#bkmk_note3)</sup>|  


###  <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 サイト間のデータベース レプリケーションでは、1 つのサイトの SQL Server がその親または子のサイトの SQL Server と直接通信する必要があります。  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server サービス|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  
|SQL Server Service Broker|--|4022 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  

> [!TIP]  
>  Configuration Manager では、SQL Server Browser は必要ありません。SQL Server Browser は、UDP ポート 1434 を使用します。  


###  <a name="state-migration-point-----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> 状態移行ポイント --> SQL Server  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[注 2](#bkmk_note2) 代替ポートを利用可能</sup>|  


###  <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Configuration Manager クライアントとサイト システムで使用されるポートのメモ  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> 注 1:プロキシ サーバーのポート
このポートは構成できませんが、構成されたプロキシ サーバーを経由してルーティングすることができます。  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> 注 2:代替ポートを利用可能
この値に対して代替ポートを Configuration Manager 内で定義できます。 カスタム ポートを定義済みの場合、IPsec ポリシーまたはファイアウォールの構成用の IP フィルター情報を定義するときは、そのカスタム ポートを代わりに使用してください。  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> 注 3:Windows Server Update Services (WSUS)
WSUS をインストールする際、クライアント接続用にポート 80/443 を使用するかポート 8530/8531 を使用するかを選択できます。 Windows Server 2012 または Windows Server 2016 で WSUS を実行する場合、WSUS は既定で HTTP にはポート 8530 を、HTTPS にはポート 8531 を使うように構成されています。  

ポートはインストールした後に変更できます。 サイト階層全体で同じポート番号を使用する必要はありません。  

- HTTP ポートが 80 の場合、HTTPS ポートは 443 の必要があります。  

- HTTP ポートがその他の場合、HTTPS ポートは 1 大きくする必要があります (8530 と 8531 など)。   

    > [!NOTE]  
    >  HTTPS を使用するようソフトウェアの更新ポイントを構成するときには、HTTP ポートも開いている必要があります。 特定の更新プログラムの使用許諾契約書などの暗号化されていないデータは、HTTP ポートを使用します。 

- WSUS クリーンアップ用に次のオプションを有効にすると、サイト サーバーから SUSDB をホストしている SQL サーバーへの接続が行われます。
  - WSUS データベースに非クラスター化インデックスを追加して、WSUS のクリーンアップのパフォーマンスを向上させる
  - WSUS データベースから古い更新プログラムを削除する
  
  SQL Server 構成マネージャーを使って既定の SQL Server ポートを代替ポートに変更した場合は、サイト サーバーが定義済みのポートを使って接続可能であることを確認してください。 Configuration Manager は、動的ポートをサポートしていません。 既定では、SQL Server の名前付きインスタンスによるデータベース エンジンへの接続には、動的ポートが使用されます。 名前付きインスタンスを使用する場合は、静的ポートを手動で構成してください。

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> 注 4:簡易 FTP (TFTP) デーモン
簡易 FTP (TFTP) デーモン システム サービスは、Windows 展開サービス (WDS) で不可欠な要素で、ユーザー名やパスワードを必要としません。 簡易 FTP デーモン サービスでは、次の RFC で定義されている TFTP プロトコルのサポートを実装しています。  

- RFC 1350: TFTP  

- RFC 2347:オプションの拡張  

- RFC 2348:ブロック サイズのオプション  

- RFC 2349:タイムアウト間隔、および転送サイズのオプション  

TFTP は、ディスクレス ブート環境をサポートするように設計されています。 TFTP デーモンは、UDP ポート 69 でリッスンしますが、動的に割り当てられた高次のポートから応答します。 そのため、このポートを有効にすると、TFTP サービスは着信 TFTP 要求を受信できるようになりますが、選択したサーバーがそれらの要求に応答することはできません。 TFTP サーバーがポート 69 から応答するように構成しなければ、選択したサーバーが着信 TFTP 要求に応答するようにできません。  

PXE 対応配布ポイントと、Windows PE のクライアントでは、TFTP 転送に動的に割り当てられた非特権ポートが選択されます。 これらのポートは、Microsoft によって 49152 から 65535 の間で定義されます。 詳細については、「[Windows のサービス概要およびネットワーク ポート要件](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)」を参照してください

しかし、実際の PXE ブート時には、デバイス上のネットワーク カードでは、TFTP 転送中に使用される、動的に割り当てられた非特権ポートが選択されます。 デバイス上のネットワーク カードは、Microsoft によって定義された、動的に割り当てられた非特権ポートにバインドされません。 RFC 1350 で定義されているポートにのみバインドされます。 このポートは、0 から 65535 のいずれかにすることができます。 ネットワーク カードで使用される動的に割り当てられた非特権ポートの詳細については、デバイスのハードウェア製造元にお問い合わせください。


#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> 注 5:サイト サーバーとサイト システムの間の通信
既定では、サイト サーバーとサイト システムの間の通信は双方向です。 サイト サーバーが通信を開始してサイト システムを構成し、次にほとんどのサイト システムはサイト サーバーに接続してステータス情報を送り返します。 レポート サービス ポイントおよび配布ポイントは、ステータス情報を送信しません。 サイト システムのプロパティで **[サイト サーバーがこのサイト システムへの接続を開始する必要がある]** を選択した場合、サイト システムのインストール後、サイト システムがサイト サーバーとの通信を開始しません。 代わりに、サイト サーバーが通信を開始し、サイト システム サーバーに対する認証用にサイト システムのインストール アカウントを使用します。  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> 注 6:動的ポート
動的ポートでは、OS のバージョンで定義されているポート番号の範囲が使用されます。 これらのポートは、エフェメラル ポートとも呼ばれます。 既定のポート範囲の詳細については、「 [Windows のサービス概要およびネットワーク ポート要件](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)」を参照してください。  



##  <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> その他のポートの一覧  

 次のセクションには、Configuration Manager により使用されるポートに関する追加情報が記載されています。  

###  <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> クライアントからサーバーへの共有  

 クライアントは、UNC 共有に接続するたびにサーバー メッセージ ブロック (SMB) を使用します。 次に例を示します。  

- CCMSetup.exe **/source:** コマンド ライン プロパティを指定する手動クライアント インストール  

- UNC パスから定義ファイルをダウンロードする Endpoint Protection クライアント

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  


###  <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Microsoft SQL Server への接続  

 SQL Server データベース エンジンとの通信、およびサイト間のレプリケーションには、SQL Server の既定ポートを使用することも、カスタム ポートを指定することもできます。  

- サイト間通信では、次のポートが使用されます。  

  - SQL Server Service Broker では、既定のポート TCP 4022 が使用されます。  

  - SQL Server サービスでは、既定のポート TCP 1433 が使用されます。  

- SQL Server データベース エンジンとさまざまな Configuration Manager サイト システムの役割の間のサイト内通信では、既定でポート TCP 1433 が使用されます。  

- Configuration Manager は、サイト データベースをホストする各 SQL 可用性グループ レプリカがスタンドアロン SQL Server インスタンスであるかのように、同じポートとプロトコルを利用して各レプリカと通信します。

Azure を使用していて、サイト データベースが内部または外部のロード バランサーの背後にある場合、次のコンポーネントを構成します。
- 各レプリカでのファイアウォールの例外
- 負荷分散規則 

次のポートを構成します。
- SQL over TCP:TCP 1433
- SQL Server Service Broker:TCP 4022
- サーバー メッセージ ブロック (SMB):TCP 445
- RPC エンドポイント マッパー:TCP 135

> [!WARNING]  
> Configuration Manager は、動的ポートをサポートしていません。 既定では、SQL Server の名前付きインスタンスは、データベース エンジンへの接続に動的ポートを使用します。 名前付きインスタンスを使用する場合は、サイト間の通信用に静的ポートを手動で構成します。  

次のサイト システムの役割は、SQL Server データベースと直接通信します。  

- アプリケーション カタログ Web サービス ポイント  

- 証明書登録ポイントの役割  

- 登録ポイントの役割  

- 管理ポイント  

- サイト サーバー  

- レポート サービス ポイント  

- SMS プロバイダー  

- SQL Server --> SQL Server  

SQL Server が複数のサイトからデータベースをホストする場合、各データベースは個別の SQL Server インスタンスを使用する必要があります。 各インスタンスを一意のポート セットで構成します。  

SQL Server 上でホスト ベースのファイアウォールを有効にする場合は、正しいポートを許可するようにそのファイアウォールを構成します。 SQL Server と通信するコンピューター間のネットワーク ファイアウォールも構成します。  

特定のポートを使用する SQL Server を構成する方法の例については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)」をご覧ください。  


### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> 検出と公開

Configuration Manager では、サイト情報の検出と公開に次のポートが使用されます。
- ライトウェイト ディレクトリ アクセス プロトコル (LDAP):389
- グローバル カタログ LDAP:3268
- RPC エンドポイント マッパー:135
- RPC:動的に割り当てられた高 TCP ポート
- TCP:1024:5000
- TCP:49152:65535


###  <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Configuration Manager により確立される外部接続  

オンプレミスの Configuration Manager クライアントまたはサイト システムは、次の外部接続を実行できます。  

- [資産インテリジェンス同期ポイント -- &gt; Microsoft](#BKMK_PortsAI)  

- [Endpoint Protection ポイント -- &gt; インターネット](#BKMK_PortsEndpointProtection_Internet)  

- [クライアント -- &gt; グローバル カタログ ドメイン コントローラー](#BKMK_PortsClient-GCDC)  

- [Configuration Manager コンソール -- &gt; インターネット](#BKMK_PortsConsole-Internet)  

- [管理ポイント -- &gt; ドメイン コントローラー](#BKMK_PortsMP-DC)  

- [サイト サーバー -- &gt; ドメイン コントローラー](#BKMK_PortsSite-DC)  

- [サイト サーバー &lt; -- &gt; 発行元の証明機関 (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [ソフトウェアの更新ポイント -- &gt; インターネット](#BKMK_PortsSUP-Internet)  

- [ソフトウェアの更新ポイント -- &gt; 上流の WSUS サーバー](#BKMK_PortsSUP-WSUS)  

- [サービス接続ポイント -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

- [ サービス接続ポイント -- > Azure](#bkmk_scp-cmg)  

- [CMG 接続ポイント -- > CMG クラウド サービス](#bkmk_cmgcp-cmg)  


###  <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> インターネット ベースのクライアントをサポートするサイト システムのインストール要件  

> [!Note]  
> このセクションは、インターネット ベースのクライアント管理 (IBCM) にのみ適用されます。 クラウド管理ゲートウェイには適用されません。 詳細については、[インターネット上でのクライアントの管理](../../clients/manage/manage-clients-internet.md)に関するページを参照してください。  

インターネットベースのクライアントをサポートするインターネットベースの管理ポイントと配布ポイント、ソフトウェアの更新ポイント、およびフォールバック ステータス ポイントは、インストールと修復に次のポートを使用します。  

- サイト サーバー --> サイト システム:UDP および TCP ポート 135 を使用する RPC エンドポイント マッパー。  

- サイト サーバー --> サイト システム:RPC 動的 TCP ポート  

- サイト サーバー &lt; --> サイト システム:TCP ポート 445 を使用するサーバー メッセージ ブロック (SMB)

配布ポイントでのアプリケーションとパッケージのインストールには、次の RPC ポートが必要です。  

- サイト サーバー --> 配布ポイント:UDP および TCP ポート 135 を使用する RPC エンドポイント マッパー

- サイト サーバー --> 配布ポイント:RPC 動的 TCP ポート  

サイト サーバーとサイト システム間のトラフィックをセキュリティで保護するために IPsec を使用します。 RPC で使用される動的ポートを制限する必要がある場合、Microsoft RPC 構成ツール (rpccfg.exe) を使用し、これらの RPC パケットに対しポートの限定範囲を構成することができます。 RPC 構成ツールの詳細については、「 [RPC で特定のポートが使用されるように構成する方法、および IPSec を使用してそれらのポートをセキュリティで保護する方法](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those)」を参照してください。  

> [!IMPORTANT]  
>  これらのサイト システムをインストールする前に、リモート レジストリ サービスがサイト システム サーバーで実行されていること、サイト システムが信頼関係のない別の Active Directory フォレストにある場合は、サイト システムのインストール アカウントを指定していることを確認します。 たとえば、リモート レジストリ サービスは、配布ポイント (プルと標準の両方) などのサイト システムを実行しているサーバー、リモート SQL サーバー、およびアプリケーション カタログで使用されます。


###  <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Configuration Manager クライアント インストールで使用されるポート  

Configuration Manager がクライアントのインストール中に使用するポートは、展開方法に依存します。 

- クライアントの展開方法別のポートの一覧については、「[Configuration Manager クライアントの展開で使用されるポート](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment)」を参照してください。  

- クライアントのインストールとインストール後の通信用にクライアントの Windows ファイアウォールを構成する方法の詳細については、[クライアントの Windows ファイアウォールとポートの設定](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md)に関するページを参照してください。  


###  <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> 移行で使用されるポート  

移行を実行するサイト サーバーでは、複数のポートを使用してソース階層内の該当するサイトに接続します。 詳細については、「[移行に必要な構成](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations)」を参照してください。  


###  <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Windows サーバーで使用されるポート  

次の表に、Windows サーバーで使用される主なポートを示します。 

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 および 68|--|  
|NetBIOS 名前解決|137|--|  
|NeTBIOS データグラム サービス|138|--|  
|NeTBIOS セッション サービス|--|139|  
|Kerberos 認証|--|88|

詳細については、以下の記事を参照してください。
- [Windows サーバー システムのサービス概要およびネットワーク ポート要件](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)  

- [ドメインと信頼関係のためのファイアウォールを構成する方法](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)
