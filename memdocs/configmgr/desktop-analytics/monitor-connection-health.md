---
title: 接続の正常性の監視
titleSuffix: Configuration Manager
description: Configuration Manager で Desktop Analytics の接続の正常性とデバイスの状態を監視する方法について、詳しく説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: fdc15860f2d093a4c9c61b787ba0b780051d3f3d
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864873"
---
# <a name="monitor-connection-health"></a>接続の正常性の監視

Configuration Manager の **[接続の正常性]** ダッシュボードを使用して、デバイスの正常性別のカテゴリにドリルダウンします。 Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースにアクセスし、 **[Desktop Analytics サービス]** ノードを展開し、 **[接続の正常性]** ダッシュボードを選択します。  

[![Configuration Manager の [接続の正常性] ダッシュボードのスクリーンショット](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

初めて Desktop Analytics を設定したとき、これらのグラフに完全なデータが表示されない場合があります。 アクティブなデバイスから Desktop Analytics サービスに診断データが送信されるまで、2-3 日かかることがあります。このサービスによってそのデータが処理され、Configuration Manager サイトと同期されます。<!-- 4098037 -->

## <a name="connection-details"></a>接続の詳細情報

このタイルには、Configuration Manager から Desktop Analytics への接続に関する、次の基本的な情報が表示されます。

- **[テナント名]** :**Azure サービス** ノードの Desktop Analytics 接続の名前

- **ターゲット コレクション**: Configuration Manager を Desktop Analytics に接続したときに指定したものと同じ "*ターゲット コレクション*" です。 このコレクションには、商用 ID と診断データの設定を使用して Configuration Manager によって構成されるすべてのデバイスが含まれます。 それは、Configuration Manager によって Desktop Analytics サービスに接続されるデバイスの完全なセットです。

- **[対象となるデバイス]** :ターゲット コレクション内のすべてのデバイスから、次の種類のデバイスを除いたものです。

  - 使用停止
  - 古い
  - 非アクティブ
  - アンマネージド
  - Windows 10 の長期サービス チャネル (LTSC) バージョンを稼働しているデバイス
  - Windows Server を稼働しているデバイス

    これらのデバイスの状態について詳しくは、「[クライアント ステータスについて](../core/clients/manage/monitor-clients.md#bkmk_about)」をご覧ください。

    > [!Note]  
    > Configuration Manager によって、ターゲット コレクション内のすべてのデバイスから使用停止のクライアントと古いクライアントを除いたものが、Desktop Analytics にアップロードされます。

- **[DA の対象デバイス]** :対象となるデバイスから Desktop Analytics に適さないデバイスを除いた数です。 たとえば、ターゲット コレクション内のデバイスのうち、Windows Server や Windows 10 の長期サービス チャネル (LTSC) を稼働しているものです。

## <a name="last-sync-details"></a>最後の同期の詳細

このタイルには、Configuration Manager が Desktop Analytics クラウド サービスと同期する日時と、同期するデバイスの数が表示されます。

- **[同期されたデバイス]** :Configuration Manager から Desktop Analytics に送信される、対象デバイスの数です。 サービスにより、これらのデバイスが現在表示されているスナップショットに追加されます。

- **[Last service sync]\(最後のサービス同期\)** :Desktop Analytics ポータルにおける **[最終更新日時]** の時間と同じです。

- **[次回のサービス同期]** :Desktop Analytics での次の毎日のスナップショットを想定する日時。

> [!Note]  
> 初めて Desktop Analytics にデバイスを登録する場合、データのアップロードと処理に数日かかることがあります。 この間、 **[Last sync details]\(最後の同期の詳細\)** タイルは空白で表示される場合があります。
> また、オンデマンドのスナップショットを要求した場合、このタイルの値はいずれも自動的に更新されません。 詳細については、「[データ待機時間](troubleshooting.md#data-latency)」をご覧ください。

一部のデバイスが Desktop Analytics に表示されないと思う場合は、そのデバイスが Desktop Analytics でサポートされていることを確認してください。 詳細については、「[前提条件](overview.md#prerequisites)」を参照してください。

## <a name="connection-health"></a>接続の正常性

**[接続の正常性]** グラフには、次の正常性状態にあるデバイスの数が表示されます。  

- [[正しく登録されています]](#properly-enrolled):デバイスは、完全なインベントリと共に Desktop Analytics に表示されます
- [[Unable to enroll]\(登録できません\)](#unable-to-enroll):障害となっている問題があり、デバイスを登録できません
- [[Configuration alert]\(構成の警告\)](#configuration-alert):デバイスが Desktop Analytics に表示されないか、不完全なインベントリで表示されます。 Configuration Manager により、デバイスの登録に問題があることも確認されました。
- [[Awaiting enrollment]\(登録を待機しています\)](#awaiting-enrollment):Configuration Manager によってデバイスが構成されましたが、Desktop Analytics にはまだ表示されません
- [[状態保留中]](#status-pending):Configuration Manager でまだこのデバイスが構成中であるか、その状態を判断するのに十分なデバイスのデータがありません
- [[データがありません]](#missing-data):Configuration Manager によってデバイスが構成されましたが、Desktop Analytics には部分的なデータしかありません

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

このグラフのデバイスの合計数は、[接続の詳細] タイルの **[DA の対象デバイス]** の値と同じです。

グラフ内のスライスを選択すると、その状態のデバイスの一覧にドリルダウンできます。 詳細については、「[デバイス一覧](#device-list)」をご覧ください。

凡例内のカテゴリ名を選択すると、それをグラフから削除したり、追加したりできます。 このアクションは、グラフをズームして、小さいセグメントの相対的なサイズを確認するのに役立ちます。

### <a name="properly-enrolled"></a>正しく登録されています

このデバイスには、次の属性があります。

- 構成マネージャー クライアント バージョン 1902 以降  
- 構成エラーがない  
- 過去 28 日以内に、このデバイスから Desktop Analytics に完全な診断データが送信されている  
- Desktop Analytics に、このデバイスの構成とインストール済みアプリに関する完全なインベントリがある  

### <a name="unable-to-enroll"></a>登録できません

Configuration Manager により、デバイスの登録を妨げる 1 つまたは複数の障害となっている問題が検出されました。 詳細については、[Configuration Manager での Desktop Analytics のデバイス プロパティ](#bkmk_config-issues)の一覧を参照してください。  

たとえば、構成マネージャー クライアントが、バージョン 1902 (5.0.8790) 以上ではありません。 クライアントを最新のバージョンに更新してください。 Configuration Manager サイトの自動クライアント アップグレードを有効にすることを検討してください。 詳細については、「[クライアントをアップグレードする](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)」をご覧ください。  

> [!TIP]
> Windows 7 の 2020 年 4 月の拡張セキュリティ更新プログラム (ESU) に関する、デバイスでこのエラーが誤って報告される既知の問題があります。 詳細については、「[リリース ノート](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack)」を参照してください。<!-- 7283186 -->

バージョン 2002 以降では、次の 2 つの領域でクライアント プロキシの構成に関する問題をより簡単に特定できます。

- **エンドポイント接続チェック**:必要なエンドポイントにクライアントが接続できない場合に、ダッシュボードに構成アラートが表示されます。 プロキシ構成の問題が原因でクライアントが接続できないエンドポイントを表示するために、登録できないクライアントにドリルダウンします。 詳細については、「[エンドポイント接続チェック](#endpoint-connectivity-checks)」をご覧ください。<!-- 4963230 -->

- **接続性の状態**:クライアントが Desktop Analytics へのアクセスにプロキシ サーバーを使用している場合、Configuration Manager によって、クライアントからのプロキシ認証の問題が表示されます。 ドリルダウンして、プロキシ認証の問題が原因で登録できないクライアントを表示します。 詳しくは、「[接続性の状態](#connectivity-status)」をご覧ください。<!-- 4963383 -->

### <a name="configuration-alert"></a>構成の警告

デバイスが Desktop Analytics に表示されないか、不完全なインベントリで表示されます。 Configuration Manager により、デバイスの登録に問題があることも確認されました。 詳細については、[Configuration Manager での Desktop Analytics のデバイス プロパティ](#bkmk_config-issues)の一覧を参照してください。

たとえば、デバイスがサービスに接続できません。 詳細については、「[Windows 診断エンドポイント接続](#windows-diagnostic-endpoint-connectivity)」をご覧ください。

### <a name="awaiting-enrollment"></a>登録を待機しています

Desktop Analytics に、このデバイスの診断データがありません。 この問題は、デバイスをターゲット コレクションに最近追加したばかりで、まだデータが送信されていないことが原因である可能性があります。 また、デバイスがサービスと正しく通信しておらず、最新の診断データが 28 日以上経過している場合も考えられます。

デバイスがサービスと通信できることを確認してください。 詳しくは、「[エンドポイント](enable-data-sharing.md#endpoints)」をご覧ください。  

### <a name="status-pending"></a>状態保留中

Configuration Manager でまだこのデバイスが構成中であるか、その状態を判断するのに十分なデバイスのデータがありません。

### <a name="missing-data"></a>データがありません

Configuration Manager によってデバイスが正しく構成されましたが、Desktop Analytics で互換性の評価を作成できません。 デバイスの構成 (センサス) またはインストール済みアプリ (インベントリ) に関する完全なデータ セットがありません。

多くの場合、この問題は、デバイスの再試行時に自動的に修正されます。 問題が解決しない場合は、デバイスがサービスと通信できることを確認してください。 詳しくは、「[エンドポイント](enable-data-sharing.md#endpoints)」をご覧ください。  

## <a name="device-list"></a>デバイス一覧

状態別に特定のデバイスの一覧を表示する場合、 **[接続の正常性]** ダッシュボードから開始します。 **[接続の正常性]** タイルのいずれかのセグメントを選択し、その状態のデバイスの一覧にドリルダウンします。 このカスタム デバイス ビューには、既定では次の Desktop Analytics 列が表示されます。

- 商用 ID の構成
- 互換性に関する最小の更新プログラム
- Windows 診断データのオプトイン
- Windows 商用データのオプトイン
- Windows 診断エンドポイント接続
- 接続性の状態 (バージョン 2002 以降)
- エンドポイント接続チェック (バージョン 2002 以降)

これらの列は、デバイスが Desktop Analytics と通信するための、主要な[前提条件](overview.md#prerequisites)に対応しています。

[![登録できないデバイス一覧のスクリーンショット](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

デバイスを選択すると、詳細ウィンドウに使用可能なプロパティの完全な一覧が表示されます。 これらのプロパティのいずれかを、デバイス一覧の列として追加することもできます。

## <a name="device-properties"></a><a name="bkmk_config-issues"></a> デバイス プロパティ

次の Desktop Analytics のデバイス プロパティは、Configuration Manager のデバイス一覧の列として使用できます。

- [エンドポイント接続チェック](#endpoint-connectivity-checks) (バージョン 2002 以降)
- [接続性の状態](#connectivity-status) (バージョン 2002 以降)
- [Appraiser の構成](#appraiser-configuration)  
- [互換性に関する最小の更新プログラム](#minimum-compatibility-update)  
- [Appraiser のバージョン](#appraiser-version)  
- [最後に成功した Appraiser の完全な実行](#last-successful-full-run-of-appraiser)  
- [Appraiser データの収集](#appraiser-data-collection)  
- [最後に成功した Census の完全な実行](#last-successful-full-run-of-census)  
- [Census データの収集](#census-data-collection)  
- [Windows 診断エンドポイント接続](#windows-diagnostic-endpoint-connectivity)  
- [エンド ユーザーの診断データをご確認ください](#check-end-user-diagnostic-data)  
- [ユーザーのプロキシを確認します](#check-user-proxy)  
- [商用 ID の構成](#commercial-id-configuration)  
- [Windows 商用データのオプトイン](#windows-commercial-data-opt-in)  
- [診断データのデバイス名をご確認ください](#check-device-name-in-diagnostic-data)  
- [DiagTrack サービスの構成](#diagtrack-service-configuration)  
- [DiagTrack のバージョン](#diagtrack-version)  
- [SQM ID の取得](#sqm-id-retrieval)  
- [デバイスの一意識別子の取得](#unique-device-identifier-retrieval)  
- [Windows 診断データのオプトイン](#windows-diagnostic-data-opt-in)  

[接続の正常性] ダッシュボードの **[最もよく発生する登録ブロックと構成アラート]** タイルに は、デバイスから最も頻繁に問題として報告されているプロパティが表示されます。

### <a name="endpoint-connectivity-checks"></a>エンドポイント接続チェック

バージョン 2002 以降では、<!-- 4963230 --> プロキシ認証の問題を検出するために、クライアントは必要なエンドポイントに対して接続チェックを実行します。 クライアントが必要なエンドポイントにアクセスできない場合、このプロパティは、プロキシの構成の問題が原因で接続できないエンドポイントの番号付きリストを表示します。 この一覧と[必須のエンドポイント](enable-data-sharing.md#endpoints)の発行済みリストを比較します。

### <a name="connectivity-status"></a>接続性の状態

バージョン 2002 以降では、<!-- 4963383 --> クライアントが Desktop Analytics へのアクセスにプロキシ サーバーを使用している場合、このプロパティでクライアントからのプロキシ認証の問題が表示されます。 プロキシ認証に関連する次の詳細情報が含まれます。

- 状態コード
- リターン コード

ログ ファイルには、次のようなエラーが表示されます。

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

ここでの `%s` は、必要なエンドポイントの URL です。

デバイスに登録の問題が発生するまで、注意する必要がない非確定的なエラー メッセージが表示される場合もあります。 次に例を示します。

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Desktop Analytics で使用するプロキシ サーバーの構成の詳細については、「[プロキシ サーバー認証](enable-data-sharing.md#proxy-server-authentication)」を参照してください。

### <a name="appraiser-configuration"></a>Appraiser の構成

<!--20,21-->
Appraiser は、[互換性に関する更新プログラム](enroll-devices.md#update-devices)に対応した Windows コンポーネントです。 デバイス上のアプリとドライバーについて、最新バージョンの Windows との互換性を評価することができます。

このチェックが成功した場合、デバイス上で Appraiser コンポーネントが正しく構成されています。

そうでない場合は、次のいずれかのエラーが表示されることがあります。

- デバイスのアプリの互換性データ コレクションを構成できません (SetRequestAllAppraiserVersions)。 ログで例外の詳細を確認してください  

- デバイスのアプリの互換性データ コレクションを構成できません (SetRequestAllAppraiserVersions)。 ログで例外の詳細を確認してください  

- RequestAllAppraiserVersions をレジストリ キー `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser` に書き込めません。 アクセス許可を確認してください  

このレジストリ キーに対するアクセス許可を確認してください。 構成マネージャー クライアントで設定できるように、ローカル システム アカウントでこのキーにアクセスできることを確認します。  

詳細については、クライアントの M365AHandler.log を確認してください。  

### <a name="minimum-compatibility-update"></a>互換性に関する最小の更新プログラム

<!--18,19,32-->
デバイス上で、互換性に関する更新プログラム (appraiser.dll) がインストールされていないか、最新ではありません。 Desktop Analytics の最小要件である 10.0.17763 よりも古くなっています。

最新の互換性に関する更新プログラムをインストールしてください。 詳細については、「[互換性に関する更新プログラム](enroll-devices.md#update-devices)」をご覧ください。

### <a name="appraiser-version"></a>Appraiser のバージョン

このプロパティでは、デバイス上の Appraiser コンポーネントの現在のバージョンが表示されます。 `%windir%\System32\appraiser.dll` のファイル バージョンが、小数点なしで表示されます。 たとえば、ファイル バージョン 10.0.17763 は、10017763 と表示されます。

### <a name="last-successful-full-run-of-appraiser"></a>最後に成功した Appraiser の完全な実行

このプロパティでは、デバイスによって最後に Appraiser が正常に実行された日時が表示されます。

### <a name="appraiser-data-collection"></a>Appraiser データの収集

<!--Appraiser run status-->
<!--22,33-->
このプロパティでは、Appraiser コンポーネントを実行している Windows からの最新の結果が表示されます。

成功しない場合は、次のいずれかのエラーが表示されることがあります。

- アプリの互換性データを収集できません (RunAppraiser)。 詳細については、ログをご確認ください  

- アプリの互換性データの収集 (CompatTelRunner.exe) がエラー コードで終了しました  

詳細については、クライアントの M365AHandler.log を確認してください。

次のファイルを確認してください: `%windir%\System32\CompatTelRunner.exe`。 存在しない場合は、必要な[互換性に関する更新プログラム](enroll-devices.md#update-devices)を再インストールしてください。 グループ ポリシーやマルウェア対策サービスなど、他のシステム コンポーネントによってこのファイルが削除されていないことを確認してください。

クライアント上の M365AHandler.log ファイルに、次のいずれかのエラーが含まれていた場合:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

これらのエラーを修復するには、影響を受けるクライアント上で、管理者特権の Windows PowerShell コンソールから次のコマンドを実行します。

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>最後に成功した Census の完全な実行

このプロパティでは、デバイスによって最後に Census が正常に実行された日時が表示されます。

### <a name="census-data-collection"></a>全数調査データの収集

<!-- Census run status -->
<!--51,52-->
Census は、デバイスをインベントリする Windows コンポーネントです。 このインベントリ データは、デバイスとその構成について把握するために使用されます。

このプロパティでは、Census コンポーネントを実行している Windows からの最新の結果が表示されます。

成功しない場合は、次のいずれかのエラーが表示されることがあります。

- デバイスとその構成に関するデータを収集できません (RunCensus)。 ログで例外の詳細を確認してください  

- デバイスと構成のデータ収集ツール (devicecensus.exe) が見つかりません  

詳細については、クライアントの M365AHandler.log を確認してください。

次のファイルを確認してください: `%windir%\System32\DeviceCensus.exe`。 存在しない場合は、必要な[互換性に関する更新プログラム](enroll-devices.md#update-devices)を再インストールしてください。 グループ ポリシーやマルウェア対策サービスなど、他のシステム コンポーネントによってこのファイルが削除されていないことを確認してください。

### <a name="windows-diagnostic-endpoint-connectivity"></a>Windows 診断エンドポイント接続

<!--12,15-->
このチェックが成功した場合、デバイスから接続ユーザー エクスペリエンスとテレメトリのエンドポイント (Vortex) に接続できます。

そうでない場合は、次のいずれかのエラーが表示されることがあります。  

- 接続ユーザー エクスペリエンスとテレメトリ エンドポイントに接続できません (Vortex)。 お使いのネットワーク/プロキシの設定をご確認ください  

- 接続ユーザー エクスペリエンスとテレメトリ エンドポイントへの接続を確認できません (CheckVortexConnectivity)。 ログで例外の詳細を確認してください  

デバイスでは、OS のバージョンに基づく次のエンドポイントへの GET 要求を使って、接続が確認されます。

| OS のバージョン | エンドポイント |
|------------|----------|
| - Windows 10 バージョン 1809 以降<br/>- Windows 10 バージョン 1803 (2018-09 以降の累積的な更新プログラムを含む) | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10 バージョン 1803 (2018-09 以降の累積的な更新プログラムを "*含まない*") | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10 バージョン 1709 以前 | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 または Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

デバイスがサービスと通信できることを確認してください。 このチェックでは、必要なエンドポイントの一部が検証されますが、すべてではありません。 詳しくは、「[エンドポイント](enable-data-sharing.md#endpoints)」をご覧ください。  

詳細については、クライアントの M365AHandler.log を確認してください。  

### <a name="check-end-user-diagnostic-data"></a>エンド ユーザーの診断データをご確認ください

<!--1004-->
このチェックが成功しなかった場合、ユーザーはデバイス上で、低レベルの Windows 診断データを選択しています。 また、グループ ポリシー オブジェクトの競合が原因である場合もあります。 詳細については、「[Windows の設定](enroll-devices.md#windows-settings)」をご覧ください。

お客様のビジネス要件によっては、グループ ポリシーを使用してユーザーの選択を無効にすることができます。 **[Configure telemetry opt-in setting user interface]\(テレメトリのオプトイン設定のユーザー インターフェイスを構成する\)** 設定を使用します。 詳しくは、「[組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)」をご覧ください。

### <a name="check-user-proxy"></a>ユーザーのプロキシを確認します

<!--30,35-->
DisableEnterpriseAuthProxy 設定は、Windows 7 では既定で有効になっています。 Windows 8.1 コンピューターの場合、Configuration Manager によって DisableEnterpriseAuthProxy 設定が 0 (無効ではありません) に設定されます。

このプロパティには、次のエラーが表示される場合があります。

- 認証プロキシが有効になっています。 `HKLM\Software\Policies\Microsoft\Windows\DataCollection` で DisableEnterpriseAuthProxy を 0 に設定してください

- 認証プロキシの状態を確認できません。 ログで例外の詳細を確認してください

詳細については、クライアントの M365AHandler.log を確認してください。  

このレジストリ キーに対するアクセス許可を確認してください。 構成マネージャー クライアントで設定できるように、ローカル システム アカウントでこのキーにアクセスできることを確認します。 また、グループ ポリシー オブジェクトの競合が原因である場合もあります。 詳細については、「[Windows の設定](enroll-devices.md#windows-settings)」をご覧ください。  

### <a name="commercial-id-configuration"></a>商用 ID の構成

<!--9, 11, 53-->
Microsoft では、デバイスから Desktop Analytics ワークスペースに情報をマップするために、一意の商用 ID が使用されています。 Configuration Manager を Desktop Analytics と統合した場合、サービスに対して自動的にこの ID が照会されます。 Desktop Analytics 設定の対象にするクライアントに対して、Configuration Manager によってこの ID が自動的に適用されます。

このチェックが成功した場合、デバイスは商用 ID を使って正しく構成されています。

そうでない場合は、次のいずれかのエラーが表示されることがあります。

- CommercialId をレジストリ キー `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` に書き込めません。 アクセス許可を確認してください  

- レジストリ キー `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` で CommercialId を更新できません。 ログで例外の詳細を確認してください  

- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` で、正しい CommercialId の値を指定してください  

詳細については、クライアントの M365AHandler.log を確認してください。  

このレジストリ キーに対するアクセス許可を確認してください。 構成マネージャー クライアントで設定できるように、ローカル システム アカウントでこのキーにアクセスできることを確認します。 また、グループ ポリシー オブジェクトの競合が原因である場合もあります。 詳細については、「[Windows の設定](enroll-devices.md#windows-settings)」をご覧ください。  

デバイスには別の ID があります。 このレジストリ キーは、グループ ポリシーによって使用されます。 これは、Configuration Manager によって提供される ID よりも優先されます。  

<a name="bkmk_ViewCommercialID"></a> Desktop Analytics ポータルで商用 ID を表示するには、次の手順に従います。

1. Desktop Analytics ポータルに移動し、[グローバル設定] グループの **[接続済みサービス]** を選択します。  

2. **[接続済みサービス]** ウィンドウでは、既定で **[デバイスの登録]** ウィンドウが選択されています。 [デバイスの登録] ウィンドウの [情報] セクションに、商用 ID キーが表示されます。  

[![Desktop Analytics ポータルでの商用 ID のスクリーンショット](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> 現在の ID キーを使用できない場合は、 **[新しい ID キーを取得]** してください。 商用 ID を再生成する場合は、[新しい ID を使ってデバイスを再登録](enroll-devices.md#device-enrollment)してください。このプロセスにより、移行中の診断データが失われる可能性があります。  

### <a name="windows-commercial-data-opt-in"></a>Windows 商用データのオプトイン

<!--64-->
このプロパティは、Windows 7 または Windows 8.1 を稼働しているデバイスに固有です。 CommercialDataOptIn の値を除いて、「[Windows 診断データのオプトイン](#windows-diagnostic-data-opt-in)」と類似したテストが実行されます。

### <a name="check-device-name-in-diagnostic-data"></a>診断データのデバイス名をご確認ください

<!--56,58-->
このチェックが成功した場合、デバイスは、デバイス名を共有するように正しく構成されています。

そうでない場合は、次のいずれかのエラーが表示されることがあります。

- Windows 診断データの一部として Microsoft に送信されるデバイス名を確認できません。 ログで例外の詳細を確認してください  

- AllowDeviceNameInTelemetry をレジストリ キー `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` に書き込めません。 アクセス許可を確認してください  

詳細については、クライアントの M365AHandler.log を確認してください。  

このレジストリ キーに対するアクセス許可を確認してください。 構成マネージャー クライアントで設定できるように、ローカル システム アカウントでこのキーにアクセスできることを確認します。 また、グループ ポリシー オブジェクトの競合が原因である場合もあります。 詳細については、「[Windows の設定](enroll-devices.md#windows-settings)」をご覧ください。  

グループ ポリシーなどの別のポリシー メカニズムによって、この設定が無効になっていないことを確認してください。

### <a name="diagtrack-service-configuration"></a>DiagTrack サービスの構成

<!--44,45,50-->
このチェックが成功した場合、デバイス上で DiagTrack コンポーネントが正しく構成されています。 Desktop Analytics に必要な最小バージョンは、10010586 (10.0.10586) です。

そうでない場合は、次のいずれかのエラーが表示されることがあります。

- 接続ユーザー エクスペリエンスとテレメトリ (diagtrack.dll) コンポーネントの期限が切れています。 要件をご確認ください  

    > [!TIP]
    > Windows 7 の 2020 年 4 月の拡張セキュリティ更新プログラム (ESU) に関する、デバイスでこのエラーが誤って報告される既知の問題があります。 詳細については、「[リリース ノート](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack)」を参照してください。<!-- 7283186 -->

- 接続ユーザー エクスペリエンスとテレメトリ (diagtrack.dll) コンポーネントが見つかりません。 要件をご確認ください  

- Microsoft にデータを送信するために接続ユーザー エクスペリエンスとテレメトリ サービスを有効にして開始する  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

最新の更新プログラムをインストールします。 詳細については、[デバイスの更新プログラム](enroll-devices.md#update-devices)に関する記事をご覧ください。

デバイス上の**接続ユーザー エクスペリエンスとテレメトリ** サービスが実行されていることを確認してください。

### <a name="diagtrack-version"></a>DiagTrack のバージョン

このプロパティでは、デバイス上の接続ユーザー エクスペリエンスとテレメトリ コンポーネントの現在のバージョンが表示されます。 `%windir%\System32\diagtrack.dll` のファイル バージョンが、小数点なしで表示されます。 たとえば、ファイル バージョン 10.0.10586 は、10010586 と表示されます。

### <a name="sqm-id-retrieval"></a>SQM ID の取得

<!--38-->
このプロパティは、主に Windows 7 デバイス用です。 以降のバージョンの OS では、デバイスのフォールバック ID として使用される場合があります。

成功しない場合は、次のエラーが表示されることがあります。

- レガシ デバイス テレメトリ ID (SQM ID) を取得できません

詳細については、クライアントの M365AHandler.log を確認してください。  

お使いの環境内に、重複する ID がないことを確認してください。 たとえば、一般化されていない OS イメージを使用してデバイスを展開した場合などです。

### <a name="unique-device-identifier-retrieval"></a>デバイスの一意識別子の取得

<!--54-->
Desktop Analytics では、より信頼性の高いデバイス ID のために、Microsoft アカウント サービスが使用されます。

**Microsoft アカウント サインイン アシスタント** サービスが無効になっていないことを確認します。 スタートアップの種類は、 **[手動 (トリガー開始)]** にする必要があります。

エンド ユーザーの Microsoft アカウント アクセスを無効にするには、このエンドポイントをブロックするのではなく、ポリシー設定を使用します。 詳しくは、「[エンタープライズでの Microsoft アカウント](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)」をご覧ください。

### <a name="windows-diagnostic-data-opt-in"></a>Windows 診断データのオプトイン

<!--8,40,55,62-->
このプロパティでは、診断データを許可するように Windows が正しく構成されていることが確認されます。 次のレジストリ キーの AllowTelemetry の値が確認されます。

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

これらのレジストリ キーに対するアクセス許可を確認してください。 構成マネージャー クライアントで設定できるように、ローカル システム アカウントでこれらのキーにアクセスできることを確認します。 また、グループ ポリシー オブジェクトの競合が原因である場合もあります。 詳細については、「[Windows の設定](enroll-devices.md#windows-settings)」をご覧ください。  

詳細については、クライアントの M365AHandler.log を確認してください。  

## <a name="see-also"></a>関連項目

[Desktop Analytics のトラブルシューティング](troubleshooting.md)
