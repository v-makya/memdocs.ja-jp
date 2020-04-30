---
title: BitLocker イベント ログ
titleSuffix: Configuration Manager
description: Windows イベント ログで BitLocker 情報を操作して問題のトラブルシューティングを行う方法について説明します
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4875e7875321294d815bfcd8a25a805d3e085aab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706030"
---
# <a name="bitlocker-event-logs"></a>BitLocker イベント ログ

*適用対象:Configuration Manager (Current Branch)*

BitLocker 管理エージェントと Web サービスは、Windows イベント ログを使用してメッセージを記録します。 イベント ビューアーで、 **[アプリケーションとサービス ログ]** 、 **[Microsoft]** 、 **[Windows]** に移動します。 ログ チャネル (ノード) は、コンピューターとコンポーネントによって異なります。

- **MBAM**:クライアント コンピューター上の BitLocker 管理エージェント
- **MBAM-Web**:
  - 管理ポイントでの回復サービス
  - セルフサービス ポータル
  - 管理と Web サイトの監視

これらのログの特定のメッセージの詳細については、次の記事を参照してください。

- [クライアント イベント ログ](client-event-logs.md)
- [サーバー イベント ログ](server-event-logs.md)

各ノードには、既定で 2 つのログ チャネルが表示されます。 **[Admin]** と **[Operational]** です。 詳細なトラブルシューティング情報については、[分析およびデバッグ ログ](#bkmk_debug)を表示することもできます。

## <a name="log-properties"></a>ログのプロパティ

Windows イベント ビューアーで、特定のログを選択します。 たとえば、 **[Admin]** です。 **[操作]** メニューに移動して、 **[プロパティ]** を選択します。 次の設定を構成します。

- **最大ログサイズ (KB)** : 既定では、この設定はすべてのログに対して `1028` (1 MB) です。
- **イベント ログ サイズが最大値に達したとき**: 既定では、 **[Admin]** および **[Operational]** ログは、 **[必要に応じてイベントを上書きする (最も古いイベントから)]** に設定されています。

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a> 分析とデバッグ ログ

トラブルシューティングのために、より詳細なログを有効にすることができます。 イベント ビューアーで、 **[表示]** メニューに移動し、 **[分析およびデバッグ ログの表示]** を選択します。 ログ チャネルを参照すると、2 つの追加のログが表示されます: **[Analytic]** と **[Debug]** です。

> [!TIP]
> 既定では、これらのログには次のプロパティがあります。
>
> - **最大ログ サイズ (KB)** :`1028` (1 MB)
> - **イベントを上書きしない (手動でログを消去)**

## <a name="export-logs-to-text"></a>ログをテキストにエクスポート

特に[分析とデバッグ ログ](#bkmk_debug)を使用すると、単一のテキスト ファイル内のログ エントリを簡単に確認できます。 次の PowerShell コマンドを使用して、イベント ログ エントリをテキスト ファイルにエクスポートします。

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
