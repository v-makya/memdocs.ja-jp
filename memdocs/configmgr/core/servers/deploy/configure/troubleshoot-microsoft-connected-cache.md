---
title: 接続済みキャッシュのトラブルシューティング
titleSuffix: Configuration Manager
description: 問題のトラブルシューティングに役立つ Microsoft 接続済みキャッシュの技術的な詳細。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a08b74552d5d17a737ec9e1802e10c87621f5b97
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126360"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Configuration Manager における Microsoft 接続済みキャッシュのトラブルシューティング

この記事では、Configuration Manager の Microsoft 接続済みキャッシュに関する技術的な詳細情報について説明します。 使用している環境で発生する可能性のある問題のトラブルシューティングに役立ちます。 そのしくみと使用方法については、「[Configuration Manager における Microsoft 接続済みキャッシュ](../../../plan-design/hierarchy/microsoft-connected-cache.md)」を参照してください。

> [!NOTE]
> バージョン 1910 以降、この機能は、**Microsoft 接続済みキャッシュ**という名前になりました。 以前は、"配信の最適化のネットワーク内キャッシュ" という名前でした。

## <a name="verify"></a>確認事項

配信の最適化キャッシュ サーバーを正しくインストールし、クライアントを正しく設定すると、インターネットではなく、配布ポイントにインストールされているキャッシュ サーバーからダウンロードが行われます。

[クライアント](#bkmk_verify-client)または[サーバー](#bkmk_verify-server)でこの動作を検証します。

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a> クライアントで検証する

1. Windows 10 バージョン 1809 以降を実行しているクライアントで、クラウド管理コンテンツをダウンロードします。 接続済みキャッシュでサポートされているコンテンツの種類については、[接続済みキャッシュの検証](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify)に関する記事を参照してください。

2. PowerShell を起動し、コマンド `Get-DeliveryOptimizationStatus` を実行します。

次に例を示します。

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

`BytesFromCacheServer` 属性がゼロではないことにご注目ください。

クライアントが正しく設定されていないか、キャッシュ サーバーが正しくインストールされていない場合、配信の最適化クライアントは元のクラウド ソースにフォールバックします。 その後、BytesFromCacheServer 属性がゼロになります。

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a> サーバーで検証する

まず、レジストリ プロパティ `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache` が正しく構成されていることを確認します。 たとえば、ドライブ キャッシュの場所は `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294` です。ここでは、`C,D,E` のように、`PrimaryDrivesInput` が複数のドライブになることがあります。

次に、次の方法で必須のヘッダーを指定し、サーバーへのクライアント ダウンロード要求をシミュレーションします。

1. 管理者として 64 ビット PowerShell ウィンドウを開きます。
2. 次のコマンドを実行し、`<DoincServer>` のサーバーの名前または IP アドレスを置換します。

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

出力は次の例のようになります。

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

次の属性は成功を示します。

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>ログ ファイル

- ARR セットアップ ログ: `%temp%\arr_setup.log`

- DO キャッシュ サーバー セットアップ ログ: 配布ポイントの場合は `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` で、サイト サーバーの場合は `DistMgr.log`

- IIS 操作ログ:既定では `%SystemDrive%\inetpub\logs\LogFiles`

- DO キャッシュ サーバーの操作ログ: `C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > 用途は他にもありますが、このログは Microsoft クラウドの接続問題の特定に役立ちます。

## <a name="setup-error-codes"></a>セットアップ エラー コード

Configuration Manager によって配布ポイントに接続済みキャッシュ コンポーネントがインストールされるときに発生することがあるエラー コードをまとめたものが次の表です。

| エラー コード | エラーの説明 |
|------------|-------------------|
| 0x00000000 | 成功 |
| 0x00000BC2 | 成功、再起動が必要 |
| 0x00000643 | 一般的なインストール エラー |
| 0x00D00001 | 接続済みキャッシュは、インターネット インフォメーション サービス (IIS) がインストールされている場合にのみ実行できます |
| 0x00D00002 | 接続済みキャッシュは、"既定の Web サイト" がサーバーに置かれている場合にのみ実行できます |
| 0x00D00003 | アプリケーション要求ルーティング処理 (ARR) が既にインストールされている場合、接続済みキャッシュをインストールできません |
| 0x00D00004 | アプリケーション要求ルーティング処理 (ARR) が Install.ps1 スクリプトによってインストールされた場合にのみ、接続済みキャッシュのセットアップを実行できます |
| 0x00D00005 | 接続済みキャッシュをセットアップするには、PowerShell セッションを管理者として実行する必要があります |
| 0x00D00006 | 接続済みキャッシュのセットアップは 64 ビットの PowerShell 環境からのみ実行できます |
| 0x00D00007 | 接続済みキャッシュのセットアップは Windows Server でのみ実行できます |
| 0x00D00008 | 失敗:指定されているキャッシュ ドライブの数値は、指定されているキャッシュ ドライブ サイズ パーセンテージの数値に一致する必要があります |
| 0x00D00009 | 失敗:有効なキャッシュ ノード ID を指定する必要があります |
| 0x00D0000A | 失敗:有効なキャッシュ ドライブ セットを指定する必要があります |
| 0x00D0000B | 失敗:有効なキャッシュ ドライブ サイズ パーセント セットを指定する必要があります |
| 0x00D0000C | 失敗:有効なキャッシュ ドライブ サイズ パーセント セットまたはキャッシュ ドライブ サイズ (GB) を指定する必要があります |
| 0x00D0000D | 失敗:有効なキャッシュ ドライブ サイズ パーセント セットとキャッシュ ドライブ サイズ (GB) の両方を指定することはできません |
| 0x00D0000E | 失敗:指定されているキャッシュ ドライブの数値は指定されているキャッシュ ドライブ サイズの数値 (GB) に一致する必要があります |
| 0x00D0000F | 失敗:applicationhost.config ファイルを $AppHostConfig から $AppHostConfigDestinationName にバックアップできません |
| 0x00D00010 | 失敗:既定の Web サイトの web.config ファイルを $WebsiteConfigFilePath から $WebConfigDestinationName にバックアップできません |
| 0x00D00011 | 失敗:SetupARRWebFarm.ps1 で例外が発生しました |
| 0x00D00012 | 失敗:SetupARRWebFarmRewriteRules.ps1 で例外が発生しました |
| 0x00D00013 | 失敗:SetupARRWebFarmProperties.ps1 で例外が発生しました |
| 0x00D00014 | 失敗:SetupAllowableServerVariables.ps1 で例外が発生しました |
| 0x00D00015 | 失敗:SetupFirewallRules.ps1 で例外が発生しました |
| 0x00D00016 | 失敗:SetupAppPoolProperties.ps1 で例外が発生しました |
| 0x00D00017 | 失敗:SetupARROutboundRules.ps1 で例外が発生しました |
| 0x00D00018 | 失敗:SetupARRDiskCache.ps1 で例外が発生しました |
| 0x00D00019 | 失敗:SetupARRProperties.ps1 で例外が発生しました |
| 0x00D0001A | 失敗:SetupARRHealthProbes.ps1 で例外が発生しました |
| 0x00D0001B | 失敗:VerifyIISSItesStarted.ps1 で例外が発生しました |
| 0x00D0001C | 失敗:SetDrivesToHealthy.ps1 で例外が発生しました |
| 0x00D0001D | 失敗:VerifyCacheNodeSetup.ps1 で例外が発生しました |
| 0x00D0001E | 既定の Web サイトがポート 80 にない場合、接続済みキャッシュをインストールできません |
| 0x00D0001F | 失敗:キャッシュ ドライブの割り当て (パーセンテージ) が 100 を超えることはありません |
| 0x00D00020 | 失敗:キャッシュ ドライブの割り当て (GB) がドライブの空き領域を超過することはできません |
| 0x00D00021 | 失敗:キャッシュ ドライブの割り当て (パーセンテージ) はゼロより大きくする必要があります |
| 0x00D00022 | 失敗:キャッシュ ドライブの割り当て (GB) はゼロより大きくする必要があります |
| 0x00D00023 | 失敗:RegisterScheduledTask_CacheNodeKeepAlive で例外が発生しました |
| 0x00D00024 | 失敗:RegisterScheduledTask_Maintenance で例外が発生しました |
| 0x00D00025 | 失敗:HTTPS ファーム: $FarmName の書き換えルール設定中に例外が発生しました |
| 0x00D00026 | 失敗:HTTP ファーム: $FarmName の書き換えルール設定中に例外が発生しました |
| 0x00D00027 | 依存ソフトウェア "アプリケーション要求ルーティング処理 (ARR)" をインストールできなかったため、接続済みキャッシュをインストールできません。 %temp%\arr_setup.log にあるログ ファイルをご覧ください |

## <a name="iis-configurations"></a>IIS 構成

DO キャッシュ サーバーをインストールすると、配布ポイントの IIS 構成にいくつかの変更が加えられます。

### <a name="application-request-routing"></a>アプリケーション要求ルーティング処理

DO キャッシュ サーバーによって IIS [アプリケーション要求ルーティング処理 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) がインストールされ、構成されます。 潜在的な競合を避けるために、この時点で配布ポイントにこのコンポーネントをインストールしておくことはできません。

### <a name="allowed-server-variables"></a>許可されるサーバー変数

DO キャッシュ サーバーをインストールすると、既定の Web サイトに次の*ローカル* サーバー変数が与えられます。

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### <a name="rewrite-rules"></a>書き換えルール

DO キャッシュ サーバーにより次の書き換えルールが追加されます。

#### <a name="inbound-rewrite-rules"></a>受信書き換えルール

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>送信書き換えルール

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>サーバー リソースの管理

DO キャッシュ サーバーごとに必要になるディスク容量は、組織の更新の要件によって異なることがあります。 次のコンテンツをキャッシュする場合、100 GB の容量で十分です。

- 機能更新プログラム
- 2 から 3 か月分の品質更新プログラムと Microsoft 365 Apps 更新プログラム
- Microsoft Intune アプリと Windows 受信トレイ アプリ

DO キャッシュ サーバーでは、システム メモリやプロセッサ時間をたくさん消費すべきではありません。 DO キャッシュ サーバーのインストール後、プロセスまたはメモリ リソースに大きな消費が見られた場合、IIS と ARR のログ ファイルを分析してください。

IIS と ARR のログ ファイルでサーバー上の領域がたくさん占められている場合、いくつかの方法でログ ファイルを管理できます。 詳細については、「[IIS ログ ファイル ストレージの管理](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview)」をご覧ください。

## <a name="see-also"></a>関連項目

[Configuration Manager における Microsoft 接続済みキャッシュ](../../../plan-design/hierarchy/microsoft-connected-cache.md)
