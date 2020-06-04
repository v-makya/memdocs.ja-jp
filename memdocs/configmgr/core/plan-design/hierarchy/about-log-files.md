---
title: ログ ファイルについて
titleSuffix: Configuration Manager
description: Configuration Manager クライアントとサイト システムに関する問題のトラブルシューティングを行うには、ログ ファイルを使用します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 588bccc533909f2438dc61d6f25b39c3a582c71b
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879026"
---
# <a name="about-log-files-in-configuration-manager"></a>Configuration Manager のログ ファイルについて

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、クライアント コンポーネントとサイト サーバー コンポーネントによって、処理情報が個々のログ ファイルに記録されます。 ログに記録された情報を、発生した問題を解決するときの参考にしてください。 既定では、Configuration Manager ではクライアント コンポーネントとサーバー コンポーネントのログ記録が有効になっています。

この記事では、Configuration Manager のログファイルに関する一般的な情報を提供します。 使用するツール、ログの構成方法、およびその検索場所に関する情報が含まれています。 特定のログ ファイルについて詳しくは、[ログ ファイル リファレンス](log-files.md)をご覧ください。


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a> しくみ

Configuration Manager のプロセスの多くで、そのプロセス専用のログ ファイルに処理情報が書き込まれます。 これらのログ ファイルには、 **.log** 拡張子か **.lo_** 拡張子が付いています。 Configuration Manager は、ログが最大サイズに達するまで .log ファイルに書き込みます。 このファイルがいっぱいになると、同じ名前で .lo_ 拡張子の付いたファイルに内容がコピーされ、元の .log ファイルへの書き込みが続行されます。 .log ファイルが再びいっぱいになると、.lo_ ファイルが上書きされ、元の .log ファイルに書き込まれます。この同じプロセスが繰り返されます。 一部のコンポーネントでは、ログ ファイルの名前に日付と時刻のスタンプが追加され、.log 拡張子が維持されることによって、ログ ファイルの履歴が確立されます。


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a> ログ ビューアー ツール

Configuration Manager のすべてのログ ファイルはプレーンテキストであるため、メモ帳などのテキスト リーダーで表示できます。 ログでは独自の形式が使われており、次のいずれかの専用ツールを使うと最適に表示できます。

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [サポート センターのログ ビューアー](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

ログを表示するには、Configuration Manager ログ ビューアー ツールの **CMTrace** を使います。 これは、Configuration Manager ソース メディアの `\SMSSetup\Tools` フォルダーにあります。 また、CMTrace ツールは、[ソフトウェア ライブラリ] に格納されるすべてのブート イメージに追加されます。 CMTrace ログ表示ツールは、Configuration Manager クライアントと共に自動的にインストールされます。<!--1357971--> 詳細については、「[CMTrace](../../support/cmtrace.md)」を参照してください。

### <a name="onetrace"></a>OneTrace

バージョン 1906 以降、**OneTrace** は、サポート センターの新しいログ ビューアーです。 CMTrace と同様に機能しますが、いくつかの点が改善されています。 詳しくは、「[サポート センターの OneTrace](../../support/support-center-onetrace.md)」をご覧ください。

### <a name="support-center-log-viewer"></a>サポート センターのログ ビューアー

**サポート センター**には、最新のログ ビューアーが含まれます。 このツールによって、CMTrace が置き換えられ、タブおよびドッキング可能なウィンドウのサポートと共に、カスタマイズ可能なインターフェイスが提供されます。 高速のプレゼンテーション層を備えており、大きなログ ファイルを秒単位で読み込むことができます。 詳しくは、「[サポート センター ログ ビューアー リファレンス](../../support/support-center-ui-reference.md#bkmk_log-viewer)」をご覧ください。

> [!Note]  
> サポート センターと OneTrace には Windows Presentation Foundation (WPF) が使用されます。 このコンポーネントは Windows PE では使用できません。 タスク シーケンスの展開を含むブート イメージで CMTrace を引き続き使用します。


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a> ログのオプションを構成する

詳細レベル、サイズ、履歴など、ログ ファイルの構成を変更できます。 これらの設定を変更するには、次のいくつかの方法があります。

- [クライアントのインストール時](#bkmk_logoptions-clientprop)
- [Configuration Manager Service Manager の使用](#bkmk_logoptions-sm)
- [Windows レジストリの使用](#bkmk_logoptions-registry)
- [Configuration Manager コンソールで](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a> クライアントのインストール時にログ オプションを構成する

インストールの間に、クライアント ログ ファイルの構成を設定できます。 次のプロパティを使います。

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

詳細については、「[クライアント インストールのプロパティ](../../clients/deploy/about-client-installation-properties.md#clientMsiProps)」を参照してください。

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a> Configuration Manager サービス マネージャーを使用したログのオプションの構成

Configuration Manager によって格納されるログ ファイルの場所とそのサイズを変更することができます。  

ログ ファイルのサイズを変更するには、ログ ファイルの名前と場所を変更します。また、1 つのログ ファイルに対して複数のコンポーネントを強制的に書き込むには、次の手順を実行します。  

#### <a name="modify-logging-for-a-component"></a>コンポーネントのログ記録を変更する  

1. Configuration Manager コンソールで、 **[監視]** ワークスペースに移動し、 **[システムのステータス]** を展開し、 **[サイトのステータス]** ノードまたは **[コンポーネントのステータス]** ノードを選択します。  

2. リボンで **[開始]** を選択して、 **[Configuration Manager サービス マネージャー]** を選択します。  

3. Configuration Manager サービス マネージャーが開いたら、管理するサイトに接続します。 管理するサイトが表示されない場合は、 **[サイト]** 、 **[接続]** の順にクリックして、該当するサイトのサイト サーバー名を入力します。  

4. サイトを展開して、管理したいコンポーネントのある場所に応じて、 **[コンポーネント]** または **[サーバー]** に移動します。  

5. 右側のウィンドウで、1 つまたは複数のコンポーネントを選択します。  

6. **[コンポーネント]** メニューで **[ログの記録]** を選択します。  

7. **[Configuration Manager コンポーネントのログ]** ダイアログ ボックスで、必要な構成オプションを設定します。  

8. **[OK]** を選択して構成を保存します。  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a> Windows レジストリを使用してログ オプションを構成する

<!-- SCCMDocs#992 -->
サーバーまたはクライアントの Windows レジストリを使って、次のログ オプションを変更します。

- 詳細レベル
- 最大履歴
- 最大サイズ

問題のトラブルシューティングを行うときは、Configuration Manager の詳細ログ記録を有効にして、ログ ファイルに詳細情報を書き込むことができます。

> [!Warning]
> これらの設定を誤って構成すると、Configuration Manager で大量の情報がログに記録されたり、まったく記録されなかったりする可能性があります。 このデータはトラブルシューティングに役立ちますが、運用サイトでこれらの値を変更する場合は注意が必要です。 常に、最初にラボ環境でこれらの変更をテストします。 過度のログ記録が実行され、ログ ファイル内で関連情報を見つけることが困難になる可能性があります。

これらのレジストリ設定を変更した後、コンポーネントを再起動します。

- クライアントの設定を変更する場合は、**SMS Agent Host** サービス (CcmExec) を再起動します。
- サーバーの設定を変更する場合は、**SMS Executive** サービスを再起動します。

レジストリの設定は、コンポーネントによって異なります。

- [クライアントと管理ポイント](#bkmk_reg-client)
- [サイト サーバー](#bkmk_reg-site)
- [サイト システムの役割](#bkmk_reg-role)
- [Configuration Manager コンソール](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a> クライアントと管理ポイントのログ オプション

クライアントまたは管理ポイント サイト システム上のすべてのコンポーネントのログ オプションを構成するには、次の Windows レジストリ キーの **REG_DWORD** 値を構成します。

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|名前  |値  |[説明]  |
|---------|---------|---------|
|LogLevel|`0`: 詳細<br>`1`: Default<br>`2`: 警告とエラー<br>`3`: エラーのみ|ログ ファイルに書き込む詳細さのレベル。|
|LogMaxHistory|0 以上の任意の整数。次に例を示します。<br>`0`: 履歴なし<br>`1`: Default|ログ ファイルが最大サイズに達した場合、クライアントはバックアップとしてその名前を変更し、新しいログ ファイルを作成します。 保持する以前のバージョンの数を指定します。|
|LogMaxSize|10,000 以上の任意の整数。次に例を示します。<br>250000|ログ ファイルの最大サイズ (バイト単位) です。 ログが指定されたサイズに達した場合、クライアントは履歴ファイルとしてその名前を変更し、新しいファイルを作成します。 既定値は 250,000 バイトです。|

> [!Note]  
> このレジストリ キーに存在する可能性のある他の値は変更しないでください。

高度なデバッグでは、次の Windows レジストリ キーの下にこの **REG_SZ** 値を追加することもできます。

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|名前  |値  |[説明]  |
|---------|---------|---------|
|Enabled | `True`: デバッグ ログを有効にします<br>`False`: デバッグ ログを無効にします |トラブルシューティングのためにデバッグ ログを有効にします。|

この設定では、クライアントによりトラブルシューティングのための低レベルの情報がログ出力されます。 運用サイトではこの設定を使用しないでください。 過度のログ記録が実行され、ログ ファイル内で関連情報を見つけることが困難になる可能性があります。 問題を解決したら、この設定をオフにしてください。

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a> サイト サーバーのログ オプション

設定をグローバルに構成することも、Configuration Manager サイト サーバー上の特定のコンポーネントについて構成することもできます。

次の Windows レジストリ キーでこれらの値を構成します。

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|名前  |値  |Type  |[説明]
|---------|---------|---------|---------|
|SqlEnabled| `1`: SQL トレースを有効にします<br> `0`: SQL トレースを無効にします |REG_DWORD|すべてのサイト サーバー ログに SQL トレース ログを追加します。|
|ArchiveEnabled| `1`: ログのアーカイブを有効にします<br> `0`: ログのアーカイブを無効にします | REG_DWORD |履歴を保存するためにサイト サーバーのログを別の場所にアーカイブします。|
|ArchivePath| 有効なフォルダー パス (例: `C:\Logs\Archive`) | REG_SZ |サイト サーバーのログをアーカイブするパス。|

トラブルシューティングの目的でのみ SQL トレースを有効にします。 運用サイトでは使用しないでください。 過度のログ記録が実行され、ログ ファイル内で関連情報を見つけることが困難になる可能性があります。 問題を解決したら、この設定をオフにしてください。

> [!Note]  
> このレジストリ キーに存在する可能性のある他の値は変更しないでください。

特定のサーバー コンポーネントのログ オプションを構成するには、次の Windows レジストリ キーの **REG_DWORD** 値を構成します。

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|名前  |値  |[説明]  |
|---------|---------|---------|
|LoggingLevel|`0`: 詳細<br>`1`: Default<br>`2`: 警告とエラー<br>`3`: エラーのみ|ログ ファイルに書き込む詳細さのレベル。|
|LogMaxHistory|0 以上の任意の整数。次に例を示します。<br>`0`: 履歴なし<br>`1`: Default|ログ ファイルが最大サイズに達した場合、サーバーはバックアップとしてその名前を変更し、新しいログ ファイルを作成します。 保持する以前のバージョンの数を指定します。|
|MaxFileSize|10,000 以上の任意の整数。次に例を示します。<br>250000|ログ ファイルの最大サイズ (バイト単位) です。 ログが指定されたサイズに達した場合、クライアントは履歴ファイルとしてその名前を変更し、新しいファイルを作成します。 既定値は 250,000 バイトです。|
|DebugLogging| `1`: デバッグ ログを有効にします<br>`0`: デバッグ ログを無効にします |トラブルシューティングのためにデバッグ ログを有効にします。|

DebugLogging の設定では、サーバーによりトラブルシューティングのための低レベルの情報がログ出力されます。 運用サイトではこの設定を使用しないでください。 過度のログ記録が実行され、ログ ファイル内で関連情報を見つけることが困難になる可能性があります。 問題を解決したら、この設定をオフにしてください。

> [!Note]  
> このレジストリ キーに存在する可能性のある他の値は変更しないでください。

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a> サイト システムの役割ログ オプション

設定をグローバルに構成することも、Configuration Manager サーバーの役割をホストするサイト システム上の特定のコンポーネントについて構成することもできます。

特定のサーバー コンポーネントのログ オプションを構成するには、次の Windows レジストリ キーの **REG_DWORD** 値を構成します。

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

たとえば、配布ポイントの役割の場合:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|名前  |値  |[説明]  |
|---------|---------|---------|
|LogLevel|`0`: 詳細<br>`1`: Default<br>`2`: 警告とエラー<br>`3`: エラーのみ|ログ ファイルに書き込む詳細さのレベル。|
|LogMaxHistory|0 以上の任意の整数。次に例を示します。<br>`0`: 履歴なし<br>`1`: Default|ログ ファイルが最大サイズに達した場合、サーバーはバックアップとしてその名前を変更し、新しいログ ファイルを作成します。 保持する以前のバージョンの数を指定します。|
|LogMaxSize|10,000 以上の任意の整数。次に例を示します。<br>250000|ログ ファイルの最大サイズ (バイト単位) です。 ログが指定されたサイズに達した場合、サーバーは履歴ファイルとしてその名前を変更し、新しいファイルを作成します。 既定値は 250,000 バイトです。|

> [!Note]  
> このレジストリ キーに存在する可能性のある他の値は変更しないでください。

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a> Configuration Manager コンソールのログ オプション

Configuration Manager コンソールの AdminUI.log の詳細レベルを変更するには、次の手順のようにします。

1. コンソール構成ファイル **Microsoft.ConfigurationManagement.exe.config** を、メモ帳などの XML エディターで開きます。 既定の構成ファイルは次の場所にあります: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

    > [!IMPORTANT]
    > バージョン 1910 以降、このパスは `Microsoft Endpoint Manager` フォルダーを使用するように変更されました。 別のフォルダーに存在する可能性がある古いバージョンのファイルを使用しないようにしてください。

1. **system.diagnostics** > **sources** > **source** 要素で、**switchValue** 属性を `Error` から `Verbose` に変更します。 次に例を示します。

    変更前:`<source name="SmsAdminUISnapIn" switchValue="Error">` 変更後: `<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. ファイルを保存し、コンソールを再起動します。

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a> Configuration Manager コンソールのログ オプションを構成する

<!-- 4433455 -->

バージョン 1910 以降では、詳細なクライアントのログ記録またはコンソールからのコレクションを有効または無効にします。

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス]** ノードを選択し、ターゲット デバイスを選択します。

1. リボンの **[ホーム]** タブの **[デバイス]** グループで **[クライアント診断]** を選択します。 いずれかのアクションを選択します。

詳細については、[クライアント診断](../../clients/manage/client-notification.md#client-diagnostics)に関するページを参照してください。

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a> ログ ファイルの検索

Configuration Manager と依存コンポーネントでは、さまざまな場所にログ ファイルが格納されます。 これらの場所は、ログ ファイルを作成するプロセスと、環境の構成よって異なります。

既定の場所は次のとおりです。 環境内でインストール ディレクトリをカスタマイズした場合、実際のパスは異なる可能性があります。

- クライアント: `C:\Windows\CCM\logs`
- サーバー: `C:\Program Files\Microsoft Configuration Manager\Logs`
- 管理ポイント: `C:\SMS_CCM\Logs`
- Configuration Manager コンソール: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog`
- IIS: `C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>タスク シーケンス ログの場所

タスク シーケンス ログ ファイル **smsts.log** の場所は、タスク シーケンスのフェーズによって異なります。

- Windows PE で、[ディスクのフォーマットとパーティション作成](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk)ステップの前:`X:\Windows\temp\smstslog\smsts.log` (X は Windows PE の RAM ドライブ)
- Windows PE で、**ディスクのフォーマットとパーティション作成**ステップの後: `X:\smstslog\smsts.log`、その後ドライブの準備ができたら `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` にコピーされます
- 新しい Windows OS で、クライアントがインストールされる前: `C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- Windows で、クライアントがインストールされた後: `C:\Windows\CCM\Logs\smstslog\smsts.log`
- Windows で、タスク シーケンスが完了した後: `C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> 読み取り専用のタスク シーケンス変数 [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) には、常に、現在のログ ファイルのパスが含まれます。


## <a name="see-also"></a>関連項目

- [ログ ファイルのリファレンス](log-files.md)

- [サポート センターの OneTrace](../../support/support-center-onetrace.md)

- [サポート センター ログ ファイル ビューアー](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
