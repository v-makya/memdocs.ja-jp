---
title: サポート センターの OneTrace (プレビュー)
titleSuffix: Configuration Manager
description: OneTrace は、サポート センターでの新しいログ ビューアーであり、CMTrace より改善されています。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707450"
---
# <a name="support-center-onetrace-preview"></a>サポート センターの OneTrace (プレビュー)

<!--3555962-->

バージョン 1906 以降、OneTrace がサポート センターの新しいログ ビューアーです。 CMTrace と同様に機能しますが、以下の点が改善されています。

- タブ付きビュー
- ドッキング可能なウィンドウ
- 改善された検索機能
- ログ ビューを終了せずにフィルターを有効にする機能
- エラーのクラスターを素早く特定できるスクロールバーのヒント
- 大きなファイルの高速ログ オープン処理

[![OneTrace ログ ビューアーのスクリーンショット](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace は、次のようなさまざまな種類のログ ファイルで動作します。

- Configuration Manager クライアントのログ
- Configuration Manager サーバーのログ
- ステータス メッセージ
- Windows 10 上の Windows Update ETW ログ ファイル
- Windows 7 および Windows 8.1 上の Windows Update ログ ファイル

## <a name="prerequisites"></a>[前提条件]

- .NET Framework バージョン 4.6 以降

## <a name="install"></a>[インストール]

OneTrace はサポート センターと共にインストールされます。 次のパスで、サイト サーバー上のサポート センター インストーラーを見つけます: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`。

既定では、OneTrace アプリケーションは `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe` にインストールされます。

> [!Note]  
> サポート センターと OneTrace には Windows Presentation Foundation (WPF) が使用されます。 このコンポーネントは Windows PE では使用できません。 タスク シーケンスの展開を含むブート イメージで CMTrace を引き続き使用します。  

## <a name="log-groups"></a>ログ ビューアー

<!--5559993-->

バージョン 2002 以降、OneTrace では、サポート センターの機能に似たカスタマイズ可能なログ グループがサポートされます。 ログ グループを使用すると、1 つのシナリオのすべてのログ ファイルを開くことができます。 OneTrace には、現在、次のシナリオ向けのグループが含まれています。

- アプリケーション管理
- コンプライアンス設定 (Desired Configuration Management とも呼ばれます)
- ソフトウェア更新プログラム

ログ グループを表示するには、 **[ビュー]** メニューにアクセスし、 **[ログ グループ]** を選択します。

![アプリケーション管理用の OneTrace ログ グループのスクリーンショット](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>ログ グループをカスタマイズする

これらのグループをカスタマイズするには、既定で次のパスにある構成 XML を変更します: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`

次の例は、既定の構成ファイルの一部分です。

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

`GroupType` プロパティでは次の値を指定することができます。

- `0`: 不明またはその他
- `1`: Configuration Manager クライアントのログ
- `2`: Configuration Manager サーバーのログ

`GroupFilePath` プロパティには、ログ ファイルの明示的なパスを含めることができます。 それが空の場合、OneTrace は、グループの種類に対するレジストリ構成に依存します。 たとえば、`GroupType=1` を設定した場合、既定ではそのグループ内のログの `C:\Windows\CCM\Logs` が OneTrace によって自動的に検索されます。 この例では、`GroupFilePath` を指定する必要はありません。

## <a name="see-also"></a>関連項目

- [サポート センターのログ ビューアー](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
