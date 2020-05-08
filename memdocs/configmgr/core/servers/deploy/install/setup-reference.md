---
title: セットアップのリファレンス
titleSuffix: Configuration Manager
description: Configuration Manager サイトまたは階層をインストールするための準備をするには、このリファレンスを参照してください。
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff2d5c6df0da6b25395858a55ef1ee8a3c0da00b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906521"
---
# <a name="reference-for-configuration-manager-setup"></a>Configuration Manager のセットアップのリファレンス

*適用対象:Configuration Manager (Current Branch)*

「Configuration Manager のセットアップ」には、他のトピックへのリンクが掲載されています。詳細については、以下のセクションを参照してください。 ここに記載されている情報は、Configuration Manager サイトまたは階層のインストールの準備、およびインストール中に決定する必要があるいくつかの事項についての準備に役立ちます。  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a> 始める前に  
新しい Configuration Manager サイトをインストールする前に、展開を正常に設計するためのステージの設定に役立つ次の情報を必ずご確認ください。  

-   [Configuration Manager の基本情報](../../../../core/understand/fundamentals.md)  
-   [Configuration Manager のインフラストラクチャの計画](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Configuration Manager サイトのインストールを準備する](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a> サーバーの準備状態の評価  
新しいサイトのインストールを開始する前に、サイトに使用しようとしているサイト サーバーとリモート サイト システム サーバー (サイト データベースをホストするサーバーなど) がすべての前提条件の構成を満たしていることを確認します。 ドキュメント ライブラリの以下のトピックが参考になります。  

-   [Configuration Manager のサポートされている構成](../../../../core/plan-design/configs/supported-configurations.md)  
-   [前提条件チェッカー](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> 追加のオペレーティング システム用のクライアント  
Microsoft ダウンロード センターから、次のオペレーティング システム向けの Configuration Manager のクライアント ソフトウェアをダウンロードできます。  

- macOS (Apple)
- UNIX
- Linux

次のリンクを使用して、使用する Configuration Manager のバージョンのクライアントをダウンロードします。  

- [Microsoft Endpoint Configuration Manager - macOS クライアント (64 ビット)](https://www.microsoft.com/download/details.aspx?id=100850)

- [追加のオペレーティング システム用 Microsoft 構成マネージャー クライアント](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> 使用状況データのレベルと設定  
最初の Configuration Manager サイトをインストールすると、Configuration Manager によってサイト サーバーに新しいサイト システムの役割 (**サービス接続ポイント**) が自動的にインストールされて構成されます。 既定では、サービス接続ポイントが次のように設定されています。  

-   **オンライン** モード (オフライン モードも利用可能)  
-   **拡張**のデータ収集レベル (その他 "基本" と "完全" の 2 つのデータ収集レベルが利用可能)  

サービス接続ポイントがサイト システムの役割としてオンラインになると、Microsoft が自動的に診断情報と使用状況情報をインターネット経由で収集できるようになります。 収集された情報は次のことに役立ちます。  

-   問題の識別とトラブルシューティング  
-   Microsoft の製品やサービスの向上  
-   使用する Configuration Manager のバージョンに適用する Configuration Manager の更新プログラムの識別  

### <a name="levels-of-data-collection"></a>データ コレクションのレベル  
データ収集には、次の 3 つのレベルがあります。

-   **基本**には、サイトの数や有効になる Configuration Manager 機能など、セットアップとアップグレードに関するデータが含まれます。 個人を特定できる情報は送信されません。  

-   **拡張**には、基本レベル設定内のデータが含まれるだけでなく、階層に関するデータ、各機能の使用方法 (頻度と期間)、システムまたはアプリのクラッシュが発生した場合のサーバーのメモリ状態などの詳細な診断情報が送信されます。 個人を特定できるデータは送信されません。  

-   **完全**には、基本レベル設定と拡張レベル設定内のデータが含まれるだけでなく、システム ファイルやメモリ スナップショットなどの高度な診断情報も送信されます。 このオプションには個人を特定できる情報が含まれる場合がありますが、その情報を使用して個人を特定して連絡したり、広告のターゲットにしたりすることはありません。  

各レベルで収集した詳細情報の開示を含む詳細については、「[Configuration Manager の診断結果と使用状況データ](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)」を参照してください。  

詳細については、「[Microsoft のプライバシーに関する声明](https://privacy.microsoft.com/privacystatement)」を参照してください。
