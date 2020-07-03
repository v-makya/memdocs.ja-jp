---
title: インターネット アクセス要件
titleSuffix: Configuration Manager
description: Configuration Manager の機能をすべて利用するためのインターネット エンドポイントについて説明します。
ms.date: 07/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 986b8d83c705be84b04a89c99d9559471c6345c4
ms.sourcegitcommit: 2c5fd7c8603b88b753765f3cc298d0a0bacaf521
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85819952"
---
# <a name="internet-access-requirements"></a>インターネット アクセス要件

一部の Configuration Manager 機能をすべて利用するには、インターネット接続が必要です。 組織がファイアウォールまたはプロキシ デバイスを使用してインターネットとのネットワーク通信を制限している場合は、これらのエンドポイントを許可する必要があります。

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a> サービス接続ポイント

これらの構成は、サービス接続ポイントをホストするコンピューターと、そのコンピューターとインターネットの間のファイアウォールに適用されます。 どちらも、以下のインターネットの場所に対して HTTPS 用の送信ポート **TCP 443** と HTTP 用の送信ポート **TCP 80** を介した通信を許可する必要があります。

サービス接続ポイントからこれらの場所を利用する際は、Web プロキシ (認証あり、または認証なし) を使用することができます。 詳細については、「[プロキシ サーバーのサポート](proxy-server-support.md)」を参照してください。

サービス接続ポイントの詳細については、[サービスの接続ポイントの概要](../../servers/deploy/configure/about-the-service-connection-point.md)に関するページを参照してください。

その他の Configuration Manager 機能では、サービス接続ポイントから追加のエンドポイントが必要になる場合があります。 詳細については、この記事の他のセクションを参照してください。

> [!TIP]  
> サービス接続ポイントは、`go.microsoft.com` または `manage.microsoft.com` に接続するときに Microsoft Intune サービスを使います。 Baltimore CyberTrust ルート証明書がインストールされていない場合、有効期限切れの場合、またはサービス接続ポイントで破損している場合に、Intune コネクタで接続の問題が発生する既知の問題があります。 詳細については、[KB 3187516 のサービス接続ポイントが更新プログラムをダウンロードしない](https://support.microsoft.com/help/3187516)のページを参照してください。  

バージョン 2002 以降、Configuration Manager サイトがクラウド サービスに必要なエンドポイントへの接続に失敗すると、クリティカルなステータス メッセージ ID 11488 が生成されます。 サービスに接続できない場合、SMS_SERVICE_CONNECTOR コンポーネントのステータスがクリティカルに変わります。 Configuration Manager コンソールの[コンポーネントのステータス](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) ノードに、詳細なステータスが表示されます。<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a> 更新プログラムとサービス

この機能の詳細については、「[Configuration Manager の更新とサービス](../../servers/manage/updates.md)」を参照してください。

> [!Tip]  
> [管理分析情報](../../servers/manage/management-insights.md)ルールに対してこれらのエンドポイントを有効にし、**Configuration Manager を更新するためにサイトを Microsoft クラウドに接続します**。

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Windows 10 サービス

この機能の詳細については、「[サービスとしての Windows の管理](../../../osd/deploy-use/manage-windows-as-a-service.md)」を参照してください。

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Azure サービス

この機能の詳細については、「[Configuration Manager と共に使用するように Azure サービスを構成する](../../servers/deploy/configure/azure-services-wizard.md)」を参照してください。

- `management.azure.com` (Azure パブリック クラウド)
- `management.usgovcloudapi.net` (Azure US Government クラウド)

## <a name="co-management"></a>共同管理

共同管理対象の Windows 10 デバイスを Microsoft Intune に登録する場合は、それらのデバイスが Intune に必要なエンドポイントにアクセスできることを確認します。 詳細については、「[Microsoft Intune のネットワーク エンドポイント](https://docs.microsoft.com/intune/intune-endpoints)」を参照してください。

## <a name="microsoft-store-for-business"></a>ビジネス向け Microsoft Store

Configuration Manager を[ビジネス向け Microsoft Store](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) と統合する場合は、サービス接続ポイントと対象デバイスがクラウド サービスにアクセスできることを確認してください。 詳細については、[ビジネス向け Microsoft Store のプロキシ構成](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration)に関するページをご覧ください。

## <a name="delivery-optimization"></a>配信の最適化

配信の最適化を使用する場合、クライアントがそのクラウド サービス `*.do.dsp.mp.microsoft.com` と通信する必要があります。

Microsoft 接続キャッシュをサポートする配布ポイントにも、これらのエンドポイントが必要です。

詳細については、以下の記事を参照してください。

- [配信の最適化に関する FAQ](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Configuration Manager でのコンテンツ管理の基本的な概念](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Configuration Manager における Microsoft 接続済みキャッシュ](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> クラウド サービス

<!-- SCCMDocs-pr #3402 -->

このセクションでは、次の機能を取り上げます。

- クラウド管理ゲートウェイ (CMG)
- クラウド配布ポイント (CDP)
- Azure Active Directory (Azure AD) 統合
- Azure AD ベースの検出

CMG の詳細については、[CMG の計画](../../clients/manage/cmg/plan-cloud-management-gateway.md)に関するページを参照してください。

以下のセクションでは、各エンドポイントをロール別に示します。 一部のエンドポイントでは、`<name>` によってサービスが参照されます。これは、CMG または CDP のクラウド サービス名です。 たとえば、お使いの CMG が `GraniteFalls.CloudApp.Net` である場合、実際のストレージ エンドポイントは `GraniteFalls.blob.core.windows.net` です。<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>[サービス接続ポイント]

CMG または CDP サービスをデプロイする場合、サービス接続ポイントでは次にアクセスできる必要があります。

- 特定の Azure エンドポイントは、構成によって、環境ごとに異なります。 Configuration Manager はサイト データベースにこれらのエンドポイントを格納します。 Azure エンドポイントの一覧については、SQL Server の **AzureEnvironments** テーブルにクエリを実行してください。

- [Azure サービス](#azure-services)

- Azure AD ユーザー検出については:

  - バージョン 1902 以降:Microsoft Graph エンドポイント `https://graph.microsoft.com/`

  - バージョン 1810 以前:Azure AD Graph エンドポイント `https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>CMG 接続ポイント

CMG 接続ポイントでは、次のサービス エンドポイントにアクセスできる必要があります。

- クラウド サービス名 (CMG または CDP 用):
  - `<name>.cloudapp.net` (Azure パブリック クラウド)
  - `<name>.usgovcloudapp.net` (Azure US Government クラウド)

- サービス管理エンドポイント: `https://management.core.windows.net/`  

- ストレージ エンドポイント (コンテンツが有効な CMG または CDP 用):
  - `<name>.blob.core.windows.net` (Azure パブリック クラウド)
  - `<name>.blob.core.usgovcloudapi.net` (Azure US Government クラウド)
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

CMG 接続ポイント サイト システムでは、Web プロキシを使用できます。 プロキシにこのロールを構成する方法については、[プロキシ サーバーのサポート](proxy-server-support.md#configure-the-proxy-for-a-site-system-server)に関するページを参照してください。 CMG 接続ポイントは、CMG サービス エンドポイントにのみ接続する必要があります。 他の Azure エンドポイントにアクセスする必要はありません。

### <a name="configuration-manager-client"></a>Configuration Manager クライアント

- クラウド サービス名 (CMG または CDP 用):
  - `<name>.cloudapp.net` (Azure パブリック クラウド)
  - `<name>.usgovcloudapp.net` (Azure US Government クラウド)

- ストレージ エンドポイント (コンテンツが有効な CMG または CDP 用):
  - `<name>.blob.core.windows.net` (Azure パブリック クラウド)
  - `<name>.blob.core.usgovcloudapi.net` (Azure US Government クラウド)

- Azure AD トークンを取得するための Azure AD エンドポイント:
  - `login.microsoftonline.com` (Azure パブリック クラウド)
  - `login.microsoftonline.us` (Azure US Government クラウド)

### <a name="configuration-manager-console"></a>Configuration Manager コンソール

- Azure AD トークンを取得するための Azure AD エンドポイント:

  - Azure パブリック クラウド
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Azure US Government クラウド
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a> ソフトウェア更新プログラム

WSUS および自動更新が Microsoft Update クラウド サービスと通信できるように、アクティブなソフトウェア更新ポイントが次のエンドポイントにアクセスすることを許可します。  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

ソフトウェア更新プログラムの詳細については、[ソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md)に関するページを参照してください。

### <a name="intranet-firewall"></a>イントラネット ファイアウォール

次のような場合は、必要に応じて 2 つのサイト システム間にあるファイアウォールにエンドポイントを追加します。

- 子サイトにソフトウェアの更新ポイントがある場合
- サイトにリモートのアクティブなインターネット ベースのソフトウェアの更新ポイントがある場合

#### <a name="software-update-point-on-the-child-site"></a>子サイトのソフトウェアの更新ポイント

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>Office 365 の管理

> [!NOTE]
> 2020 年 4 月 21 日以降、Office 365 ProPlus は、**Microsoft 365 Apps for enterprise** に名前が変更されます。 詳細については、「[Office 365 ProPlus の名前の変更](https://docs.microsoft.com/deployoffice/name-change)」を参照してください。 コンソールの更新中は、Configuration Manager コンソールやサポート ドキュメントに古い名前へのリファレンスが表示される場合があります。

Configuration Manager を使用して Microsoft 365 Apps for enterprise を展開および更新する場合は、次のエンドポイントを許可します。

<!-- SCCMDocs#929 -->

- Microsoft 365 Apps for enterprise クライアント更新プログラムのソフトウェア更新ポイントを同期するための `officecdn.microsoft.com`

- Microsoft 365 Apps for enterprise の展開用にカスタム構成を作成するための `config.office.com`

- Office アドインの準備の評価をサポートするための `contentstorage.osi.office.net`<!-- MEMDocs#410 -->

## <a name="configuration-manager-console"></a>Configuration Manager コンソール

Configuration Manager コンソールを使用するコンピューターでは、特定の機能を利用するために次のインターネット エンドポイントにアクセスする必要があります。

### <a name="in-console-feedback"></a>コンソール内のフィードバック

- `http://petrol.office.microsoft.com`

この機能の詳細については、[製品のフィードバック](../../understand/find-help.md#product-feedback)に関するページを参照してください。

### <a name="community-workspace"></a>コミュニティ ワークスペース

#### <a name="documentation-node"></a>ドキュメント ノード

このコンソール ノードの詳細については、「[Configuration Manager コンソールの使用](../../servers/manage/admin-console.md)」を参照してください。

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>コミュニティ ハブ

この機能の詳細については、[コミュニティ ハブ](../../servers/manage/community-hub.md)に関する記事をご覧ください。

- `https://github.com`

- `https://communityhub.microsoft.com`

### <a name="monitoring-workspace-site-hierarchy-node"></a>[監視] ワークスペース、[サイト階層] ノード

**[地図]** を使用している場合は、次のエンドポイントへのアクセスを許可します。

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics クラウド サービスに必要なエンドポイントの詳細については、「[データ共有を有効にする](../../../desktop-analytics/enable-data-sharing.md#endpoints)」を参照してください。

## <a name="tenant-attach"></a>テナントのアタッチ

テナントのアタッチ機能に必要なエンドポイントの詳細については、[テナントのアタッチの有効化](../../../tenant-attach/device-sync-actions.md#internet-endpoints)に関するページをご覧ください。

## <a name="endpoint-analytics"></a>エンドポイント分析

エンドポイント分析に必要なエンドポイントの詳細については、[エンドポイント分析のプロキシ構成](../../../../analytics/troubleshoot.md#bkmk_endpoints)に関する記事をご覧ください。

## <a name="microsoft-public-ip-addresses"></a>Microsoft のパブリック IP アドレス

Microsoft IP アドレス範囲の詳細については、「[Microsoft Public IP Space (Microsoft のパブリック IP スペース)](https://www.microsoft.com/download/details.aspx?id=53602)」を参照してください。 これらのアドレスは定期的に更新されます。 サービス別に細かく分かれておらず、これらの範囲内の任意の IP アドレスを使用できます。

## <a name="see-also"></a>関連項目

- [Configuration Manager で使用されるポート](../hierarchy/ports.md)

- [Configuration Manager でのプロキシ サーバーのサポート](proxy-server-support.md)
