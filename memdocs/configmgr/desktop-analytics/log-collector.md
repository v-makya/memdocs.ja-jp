---
title: ログ コレクター
titleSuffix: Configuration Manager
description: Desktop Analytics のトラブルシューティングにログ コレクター ツールを使用する
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8782913e40bffdcbe5a151fac8821f05b7e7fece
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268574"
---
# <a name="desktop-analytics-log-collector"></a>Desktop Analytics のログ コレクター

Configuration Manager バージョン 1906 以降で、Desktop Analytics デバイスの登録の問題をトラブルシューティングするには、Configuration Manager のインストール ディレクトリの **DesktopAnalyticsLogsCollector.ps1** ツールを使います。 いくつかの基本的なトラブルシューティング手順が実行され、関連するログが 1 つの作業ディレクトリに収集されます。 このコンテンツは、Microsoft サポートと共有できます。


## <a name="prerequisites"></a>[前提条件]

- Windows 10、Windows 8.1、または Windows 7 Service Pack 1 を実行している Desktop Analytics クライアント

- 管理ユーザーとしてデバイス上でスクリプトを実行し、 **[管理者として実行]** を選択します。

    > [!Tip]
    > このツールと共に Configuration Manager の **[スクリプト]** 機能を使用できます。 詳細については、「[例 5: Configuration Manager の **[スクリプト]** を使用してスクリプトを展開する](#bkmk_ex5)」を参照してください。

- Windows 7 Service Pack 1、PowerShell バージョン 4.0 以降の場合
    - [.NET Framework バージョン 4.6 以降](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [バージョン 4.0](https://support.microsoft.com/help/2819745) (aka.ms/wmf4download) または [バージョン 5.1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.ms/wmf5download)

## <a name="usage"></a>使用方法

Configuration Manager のインストール コンテンツから次のスクリプトを取得します。`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>パラメーター

### `-LogPath`

ログおよびその他の出力ファイルを格納するローカル パスまたは UNC パスを指定します。

**値**:

- ローカル パス (最大長は 130)。例: `c:\myfolder`

- UNC パス (最大長は 130)。例: `\\myserver\myfolder`

**種類**:文字列型

**位置**: 1

**既定値**: `$Env:SystemDrive\M365AnalyticsLogs` (このパラメーターが null、空、または空白の場合、スクリプトを実行すると、システム ドライブに M365AnalyticsLogs フォルダーが作成されます)。

### `-LogMode`

ログの詳細レベルを指定します。

**値**:

- `0`: スクリプト メッセージを PowerShell コマンド ウィンドウにのみ記録します。

- `1`: 出力フォルダーと PowerShell コマンド ウィンドウの両方のログ ファイルにスクリプト メッセージを記録します。

- `2`: 出力フォルダーのログ ファイルにのみスクリプト メッセージを記録します。

**種類**:Int16

**位置**: 2

**既定値**: `1` (ログ ファイルと PowerShell コマンド ウィンドウの両方にスクリプト メッセージを記録します)。

### `-CollectNetTrace`

スクリプトでネットワーク トレースを収集するかどうかを指定します。

**値**:

- `0`: ネットワーク トレースを有効にしません。

- `1` (0 以外の整数値):ネットワーク トレースを有効にし、結果を収集します。

**種類**:Int16

**位置**: 3

**既定値**: `0` (ネットワーク トレースを有効にしません)

### `-CollectUTCTrace`

スクリプトで Windows UTC トレースを収集し、接続診断を実行するかどうかを指定します。

**値**:

- `0`: UTC トレースを有効にせず、接続診断も実行しません。

- `1` (0 以外の整数値):UTC トレースを有効にし、接続診断を実行し、結果を収集します。

**種類**:Int16

**位置**: 4

**既定値**: `0` (UTC トレースを有効にせず、接続診断も実行しません)


## <a name="output"></a>出力

このスクリプトにより、指定したパスに "*作業フォルダー*" が作成されます。 たとえば、**M365AnalyticsLogs_yy_MM_dd_HH_mm_ss** です。 すべての出力ファイルがこの作業フォルダーに格納されます。

スクリプトから "*ログ ファイル*" への書き込みを有効にすると、作業フォルダーに生成されます。 たとえば、**M365AnalyticsLogs_yy_MM_dd_HH_mm_ss.txt** です。

このスクリプトによって、作業フォルダー内に他の "*診断ファイル*" も生成されます。 次に例を示します。

- `installedKBs.txt`: デバイスにインストールされている Windows 更新プログラムの一覧
- `appcompat`: アプリケーションの互換性データ
- `Reg*.txt`: Windows レジストリからエクスポートされたデータを含む一連のファイル


## <a name="examples"></a>例

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a> 例 1: PowerShell コマンド ウィンドウで既定値を使用してスクリプトを実行する

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a> 例 2: PowerShell コマンド ウィンドウでパラメーターを指定してスクリプトを実行する

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a> 例 3: PowerShell コマンド ウィンドウで所定の順序でパラメーターを指定してスクリプトを実行する

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a> 例 4: PowerShell コマンド ウィンドウでパラメーターと詳細メッセージを指定してスクリプトを実行する

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a> 例 5: Configuration Manager の **[スクリプト]** を使用してスクリプトを展開する

詳細については、「[Configuration Manager コンソールから PowerShell スクリプトを作成して実行する](../apps/deploy-use/create-deploy-scripts.md)」を参照してください。

DesktopAnalyticsLogsCollector.ps1 は、Microsoft によってデジタル署名されています。 必要に応じて、Microsoft コード署名証明書を信頼できる発行元としてターゲット デバイスに追加します。

1. エクスプローラーでスクリプトのプロパティを開きます。 **[デジタル署名]** タブに切り替え、 **[詳細]** を選択します。

2. **[全般]** タブで **[証明書の表示]** を選択します。

    > [!Note]
    > 他のメカニズムを使用して証明書を配布するには、まず証明書をファイルにエクスポートします。 **[詳細]** タブにアクセスし、 **[ファイルにコピー]** を選択します。

3. **[証明書のインストール]** を選択します。 証明書をインポートし、 **[信頼された発行元]** ストアに配置します。


## <a name="see-also"></a>関連項目

- [Desktop Analytics のトラブルシューティング](troubleshooting.md)

- [Configuration Manager コンソールから PowerShell スクリプトを作成して実行する](../apps/deploy-use/create-deploy-scripts.md)
