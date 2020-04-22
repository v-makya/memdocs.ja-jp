---
title: コンテンツ ライブラリのクリーンアップ ツール
titleSuffix: Configuration Manager
description: Configuration Manager の展開と関連付けられなくなった孤立コンテンツを削除するには、コンテンツ ライブラリ クリーンアップ ツールを使います。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703630"
---
# <a name="content-library-cleanup-tool"></a>コンテンツ ライブラリのクリーンアップ ツール

*適用対象:Configuration Manager (Current Branch)*

配布ポイントのパッケージまたはアプリケーションと関連付けられなくなったコンテンツを削除するには、コンテンツ ライブラリ クリーンアップ コマンドライン ツールを使います。 この種類のコンテンツのことを "*孤立コンテンツ*" と呼びます。 このツールは、過去の Configuration Manager 製品用にリリースされた同様のツールの古いバージョンに代わるものです。  

このツールでは、ツールを実行するときに指定する配布ポイントのコンテンツのみが処理されます。 このツールで、サイト サーバー上のコンテンツ ライブラリからコンテンツを削除することはできません。

サイト サーバーの  **で `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup`ContentLibraryCleanup.exe** を探します。



## <a name="requirements"></a>要件  

- 一度に 1 つの配布ポイントに対してのみツールを実行します。  

- クリーンアップする配布ポイントをホストしているコンピューター上で直接、または別のサーバーからリモートで、ツールを実行します。  

- ツールを実行するユーザー アカウントには、Configuration Manager の**完全な権限を持つ管理者**セキュリティ ロールと同じアクセス許可が必要です。  



## <a name="modes-of-operation"></a>操作モード

このツールは、次の 2 つのモードで実行します。[What-if](#what-if-mode) と[削除](#delete-mode)。

> [!Tip]  
> 最初に *What-if* モードを使います。 結果に満足した後、"*削除*" モードでツールを実行します。  


### <a name="what-if-mode"></a>What-if モード   

`/delete` パラメーターを指定しないと、ツールは What-if モードで実行します。 このモードでは、配布ポイントから削除されるコンテンツが識別されます。

- このモードでツールを実行した場合、データは削除されません。  

- 削除されるコンテンツに関する情報がログ ファイルに書き込まれます。 各削除候補についての確認は求められません。  


### <a name="delete-mode"></a>削除モード   

`/delete` パラメーターを使ってツールを実行すると、ツールは削除モードで実行されます。

- このモードでツールを実行すると、指定した配布ポイントで検出された孤立コンテンツを、配布ポイントのコンテンツ ライブラリから削除することができます。  

- 各ファイルを削除する前に、ツールがそれを削除する必要があることを確認します。 削除する場合は **[Y]** 、削除しない場合は **[N]** 、以降のメッセージを省略してすべての孤立コンテンツを削除する場合は **[すべてはい]** を選択します。  


### <a name="log-file"></a>ログ ファイル

いずれかのモードでツールを実行すると、ログが自動的に作成されます。 ログ ファイルの名前は次の情報を基にして付けられます。 
- ツールが実行されたモード  
- 配布ポイントの名前  
- 操作日時  

ツールが終了すると、Windows でログ ファイルが自動的に開かれます。 

既定では、ログ ファイルはツールが実行されているユーザー アカウントの一時フォルダーに書き込まれます。 この場所は、常にツールを実行したコンピューター上であり、ツールのターゲットではありません。 ネットワーク共有などの別の場所にログ ファイルをリダイレクトするには、`/log` パラメーターを使います。



## <a name="run-the-tool"></a>ツールを実行します。

ツールを実行するには: 

1. コマンド プロンプトを管理者として開きます。 **ContentLibraryCleanup.exe** を含むフォルダーにディレクトリを変更します。  

2. 必須の[コマンド ライン パラメーター](#bkmk_params)と、使用する省略可能なパラメーターを含むコマンド ラインを入力します。



## <a name="command-line-parameters"></a><a name="bkmk_params"></a> コマンド ライン パラメーター  

以下のコマンド ライン パラメーターを任意の順で使います。   

### <a name="required-parameters"></a>必須のパラメーター

|パラメーター|詳細|
|---------|-------|
| `/dp <distribution point FQDN>`  | クリーンアップする配布ポイントの完全修飾ドメイン名 (FQDN) を指定します。 |
| `/ps <primary site FQDN>` | セカンダリ サイトで配布ポイントからコンテンツをクリーンアップする場合にのみ "*必須*" です。 このツールは、親プライマリ サイトに接続して、SMS プロバイダーに対するクエリを実行します。 これらのクエリにより、ツールは配布ポイントに必要なコンテンツを決定します。 その後、削除する孤立コンテンツを特定できます。 必要な情報がセカンダリ サイトからは直接入手できないため、親プライマリ サイトへのこの接続はセカンダリ サイトの配布ポイントに対して行う必要があります。|
| `/sc <primary site code>`  | セカンダリ サイトで配布ポイントからコンテンツをクリーンアップする場合にのみ "*必須*" です。 親プライマリ サイトのサイト コードを指定します。 |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>例:削除するコンテンツをスキャンしてログに記録する (What-if)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>例:セカンダリ サイトの配布ポイントをスキャンしてコンテンツをログに記録する
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>省略可能なパラメーター

|パラメーター|詳細|
|---------|-------|
|`/delete`| 配布ポイントからコンテンツを削除する準備ができたらこのパラメーターを使います。 コンテンツを削除する前にユーザーの確認を求めます。 </br></br> このパラメーターを使用しないと、ツールは削除されるコンテンツに関する結果を記録します。 このパラメーターを指定しないと、配布ポイントからコンテンツが実際に削除されることはありません。 |
| `/q` | このパラメーターは、すべてのプロンプトを表示しない Quiet モードでツールを実行します。 コンテンツを削除するときのプロンプトが含まれます。 また、自動的にログ ファイルを開きません。 |
| `/ps <primary site FQDN>` | プライマリ サイトで配布ポイントからコンテンツをクリーニングする場合にのみ省略可能です。 配布ポイントが属するプライマリ サイトの FQDN を指定します。 |
| `/sc <primary site code>` | プライマリ サイトで配布ポイントからコンテンツをクリーニングする場合にのみ省略可能です。 配布ポイントが属するプライマリ サイトのサイト コードを指定します。 |
| `/log <log file directory>` | ツールがログ ファイルを書き込む場所を指定します。 ローカル ドライブやネットワーク共有上の場所を指定できます。</br></br> このパラメーターを使用しないと、ログ ファイルはツールを実行ているコンピューター上のユーザーの一時ディレクトリに格納されます。|

#### <a name="example-delete-content"></a>例:コンテンツを削除する 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>例:プロンプトを表示せずにコンテンツを削除する
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>例:ローカル ドライブにログを格納する
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>例:ネットワーク共有にログを格納する
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>既知の問題

いずれかのパッケージまたは展開が失敗した場合、または実行中の場合、ツールは次のエラーを返す可能性があります。`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

この問題の回避策はありません。 コンテンツの展開が進行中または失敗した場合、このツールは孤立ファイルを確実に識別することはできません。 その問題を解決するまで、ツールではコンテンツのクリーンアップが許可されません。
