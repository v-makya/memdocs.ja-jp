---
title: サポート センター
titleSuffix: Configuration Manager
description: サポート センターで Configuration Manager クライアントのトラブルシューティングを行います。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21279eb2f7d7962d1286d60a599411912d38313a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701320"
---
# <a name="support-center-for-configuration-manager"></a>Configuration Manager のサポート センター

*適用対象:Configuration Manager (Current Branch)*

<!--1357489-->
バージョン 1810 以降では、サポート センターを使用して、クライアントをトラブルシューティングしたり、リアルタイムでログを表示したり、後で分析するために Configuration Manager クライアント コンピューターの状態をキャプチャしたりします。 サポート センターは、多くの管理者用トラブルシューティング ツールを統合する 1 つのツールです。


## <a name="about"></a>の概要

サポート センターは、Configuration Manager クライアント コンピューターをトラブルシューティングする際の課題とフラストレーションを軽減することを目的としています。 これまで、Configuration Manager クライアントの問題解決をサポートと行う際には、問題のトラブルシューティングに使用するログ ファイルやその他の情報を手動で収集する必要がありました。 しかし、この段階で誤って重要なログ ファイルを忘れてしまうこともあり、お客様ご自身やお客様のサポート担当者がさらに困難に直面する原因になっていました。

サポート センターを使用して、サポート エクスペリエンスを合理化してください。 これにより、次のことが可能になります。

- Configuration Manager クライアントのログ ファイルが含まれているトラブルシューティング バンドル (.zip ファイル) を作成できます。 すると、サポート担当者に送信する 1 つのファイルが生成されます。  

- Configuration Manager クライアントのログ ファイル、証明書、レジストリ設定、デバッグ ダンプ、クライアント ポリシーを参照できます。  

- インベントリのリアルタイム診断 (ContentSpy を置き換える)、ポリシー (PolicySpy を置き換える)、およびクライアント キャッシュ。  

### <a name="support-center-viewer"></a>サポート センター ビューアー

サポート センターには、担当者がサポート センターを使用して作成するファイルのバンドルを開くためのツールである、サポート センター ビューアーが含まれます。 サポート センターのデータ コレクターは、ローカルまたはリモートの Configuration Manager クライアントからの診断ログを収集し、パッケージ化します。 データ コレクターのバンドルを表示するには、ビューアー アプリケーションを使用します。

### <a name="support-center-log-file-viewer"></a>サポート センター ログ ファイル ビューアー

サポート センターには、最新のログ ビューアーが含まれます。 このツールによって、CMTrace が置き換えられ、タブおよびドッキング可能なウィンドウのサポートと共に、カスタマイズ可能なインターフェイスが提供されます。 高速のプレゼンテーション層を備えており、大きなログ ファイルを秒単位で読み込むことができます。

### <a name="support-center-onetrace-preview"></a>サポート センターの OneTrace (プレビュー)

<!--3555962-->
バージョン 1906 以降、**OneTrace** は、サポート センターの新しいログ ビューアーです。 CMTrace と同様に機能しますが、いくつかの点が改善されています。 詳しくは、「[サポート センターの OneTrace](support-center-onetrace.md)」をご覧ください。

### <a name="powershell-cmdlets"></a>PowerShell コマンドレット

サポート センターには [Windows PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=397830)も含まれます。 これらのコマンドレットを使用して、別の Configuration Manager クライアントへのリモート接続を作成したり、データ収集オプションを構成したり、データの収集を開始したりします。


## <a name="prerequisites"></a>[前提条件]

サーバーまたはクライアント コンピューターのサポート センターをインストールするには、次のコンポーネントをインストールします。

- Configuration Manager でサポートされている OS バージョン。 詳細については、[クライアントでサポートされている OS バージョン](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)に関するページを参照してください。 サポート センターは、モバイル デバイスをサポートしていません。  

- サポート センターおよびそのコンポーネントを実行するコンピューターでは、.NET framework 4.5.2 が必要です。  


## <a name="install"></a>[インストール]

次のパスで、サイト サーバー上のサポート センター インストーラーを見つけます: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`。

インストール後、[スタート] メニューの **[Microsoft System Center]** グループで、次の項目を見つけます。  

- サポート センター (ConfigMgrSupportCenter.exe)  
- サポート センター ログ ファイル ビューアー (CMLogViewer.exe)  
- サポート センター ビューアー (ConfigMgrSupportCenterViewer.exe)  


## <a name="known-issues"></a>既知の問題

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>以前のバージョンが既にインストールされている場合、最新バージョンをインストールすることができません。

<!--SCCMDocs-pr issue #3090-->
*適用対象: バージョン 1810 および 1902*

古いバージョンのサポート センターが既にインストールされている場合、新しいバージョンのインストーラは失敗します。 この問題の原因は、元のバージョンと最新バージョンのファイルのバージョン管理方法の違いです。 この問題を回避するには、まず以前のバージョンのサポート センターをアンインストールします。 最新バージョンをインストールします。

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>リモート接続には、ユーザー名の一部としてコンピューター名またはドメイン名を含める必要があります。

サポート センターからリモート クライアントに接続する場合、接続の確立時に、ユーザー アカウント用のコンピューター名またはドメイン名を提供する必要があります。 コンピューター名またはドメイン名を簡略化した場合 (`.\administrator` など)、接続は成功しますが、サポート センターではクライアントからデータを収集しません。

この問題を回避するには、次のユーザー名の形式を使用してリモート クライアントに接続します。

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>リモート クライアントへのスクリプト化されたサーバー メッセージ ブロック接続を削除する必要がある場合があります。

[New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) PowerShell コマンドレットを使用してリモート クライアントに接続すると、サポート センターは、各リモート クライアントへのサーバー メッセージ ブロック (SMB) 接続を作成します。 データ収集の完了後、それらの接続が保持されます。 Windows のリモート接続の最大数を超えることを防止するには、`net use` コマンドを使用して、現在アクティブなリモート接続のセットを確認します。 その後、次のコマンドを使用して、不要な接続を無効にします: `net use <connection_name> /d`。
ここで、`<connection_name>` はリモート接続の名前です。

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>アプリケーション展開の評価サイクルの要求がリモート コンピューターに正しく送信されない

<!--2849356-->
*適用対象: バージョン 1810*

サポート センター内で、 **[コンテンツ]** タブの **Invoke trigger (トリガーの起動)** アクションから **[アプリケーション展開の評価]** を選択した場合、展開されたアプリケーションを評価するタスクがこのアクションによって起動されます。 ローカル クライアントに接続している場合は、コンピューターとユーザー アプリケーションの展開の両方が評価されます。 ただし、リモート クライアントに接続している場合は、マシンのアプリケーションの展開のみが評価されます。


## <a name="next-steps"></a>次のステップ

[サポート センターのクイックスタート](support-center-quickstart.md)
