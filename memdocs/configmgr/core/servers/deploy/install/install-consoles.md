---
title: コンソールをインストールする
titleSuffix: Configuration Manager
description: Configuration Manager コンソールをインストールし、中央管理サイトまたはプライマリ サイトに接続します。
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700800"
---
# <a name="install-the-configuration-manager-console"></a>Configuration Manager コンソールをインストールする

*適用対象:Configuration Manager (Current Branch)*

管理者は Configuration Manager コンソールを利用し、Configuration Manager 環境を管理します。 各 Configuration Manager コンソールで中央管理サイト (CAS) またはプライマリ サイトに接続できます。 Configuration Manager コンソールをセカンダリ サイトに接続することはできません。

Configuration Manager コンソールは常に、CAS またはプライマリ サイトのサイト サーバーにインストールされます。 サイト サーバーのインストールとは別にコンソールをインストールするには、スタンドアロンのインストーラーを実行します。  



## <a name="prerequisites"></a>[前提条件]

- コンソールのターゲット コンピューターの**ローカル管理者**権限が与えられていること。  

- コンソールのインストール ファイルのある場所の **読み取り** 権限が与えられていること。  



## <a name="source-paths"></a>ソース パス

使用するソース パスを決定します。  

- サイト サーバーの ConsoleSetup フォルダー: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    サイト サーバーをインストールするときには、コンソールのインストール ファイル、およびサイト用にサポートされている言語パックが **Tools\ConsoleSetup** サブフォルダーにコピーされます。 **ConsoleSetup** フォルダーを別の場所にコピーして、その場所からインストールを開始することもできます。 サイトを更新するときに、常にそのローカル バージョンが最新の状態に維持されます。  

- Configuration Manager インストール メディア: `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    インストール メディアから Configuration Manager コンソールをインストールすると、常に英語バージョンがインストールされます。 この動作は、サイト サーバーがさまざまな言語をサポートしているか、ターゲット コンピューターの OS が別の言語に設定されている場合でも発生します。  

可能であれば、ソース メディアではなく **ConsoleSetup** フォルダーからコンソールのインストーラーを起動します。

> [!Important]  
> **CD.Latest** ソース ファイルを使ってコンソールをインストールしないでください。 これはサポートされていないシナリオであり、コンソールのインストールで問題が発生する可能性があります。 詳細については、「[CD.Latest フォルダー](../../manage/the-cd.latest-folder.md#unsupported-scenarios)」を参照してください。<!-- SCCMDocs issue 1359 -->  

他のコンピューターにコンソールをインストールするためのパッケージを作成する場合は、パッケージに次のファイルが含まれていることを確認します。<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (バージョン 1902 以降)
- ConfigMgr.AC_Extension.amd64.cab (バージョン 1902 以降)



## <a name="use-the-setup-wizard"></a>セットアップ ウィザードの使用  

1. ソース パスに移動し、**ConsoleSetup.exe** を開きます。  

    > [!IMPORTANT]  
    > 常に **ConsoleSetup.exe** を使ってコンソールをインストールします。 AdminConsole.msi を実行することで Configuration Manager コンソールをインストールできますが、この方法では前提条件や依存関係のチェックが実行されません。 インストールが正しくインストールされない可能性があります。  

2. ウィザードで、 **[次へ]** を選択します。  

3. **[サイト サーバー]** ページで、Configuration Manager コンソールが接続するサイト サーバーの完全修飾ドメイン名 (FQDN) を入力します。  

4. **[インストール先フォルダー]** ページで、Configuration Manager コンソールのインストール先フォルダーを入力します。 フォルダーのパスに末尾のスペースや Unicode 文字を含めることはできません。  

5. **[カスタマー エクスペリエンス向上プログラム]** ページで、カスタマー エクスペリエンス向上プログラム (CEIP) に参加するかどうかを選択します。  

    > [!Note]  
    > Configuration Manager バージョン 1802 以降では、CEIP 機能が製品から削除されます。

6. **[インストールの準備完了]** ページで、 **[インストール]** を選択します。  



## <a name="install-from-a-command-prompt"></a>コマンド プロンプトからインストールする  

> [!TIP]  
> コマンド プロンプトから Configuration Manager コンソールをインストールすると、常に英語バージョンがインストールされます。 この動作は、ターゲット コンピューターの OS が別の言語に設定されている場合でも発生します。 英語以外の言語で Configuration Manager コンソールをインストールするには、[セットアップ ウィザードを使います](#use-the-setup-wizard)。  


### <a name="consolesetupexe-command-line-options"></a>ConsoleSetup.exe コマンド ライン オプション

#### <a name="q"></a>/q

Configuration Manager コンソールを無人インストールします。 **EnableSQM**、 **TargetDir**、 **DefaultSiteServerName** の各オプションは、このオプションを使用する場合に指定する必要があります。

#### <a name="uninstall"></a>/uninstall

Configuration Manager コンソールをアンインストールします。 **/q** オプションと共に使用する場合は、このオプションを先に指定します。

#### <a name="langpackdir"></a>LangPackDir

言語ファイルが含まれているフォルダーのパスを指定します。 **セットアップ ダウンローダー** を使用して言語ファイルをダウンロードできます。 このオプションを使わない場合、セットアップにより現在のフォルダー内で言語フォルダーが検索されます。 言語フォルダーが見つからなかった場合、セットアップが続行され英語版だけがインストールされます。 詳細については、「[セットアップ ダウンローダー](setup-downloader.md)」を参照してください。

#### <a name="targetdir"></a>TargetDir

Configuration Manager コンソールをインストールするインストール先フォルダーを指定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。

#### <a name="enablesqm"></a>EnableSQM

カスタマー エクスペリエンス向上プログラム (CEIP) に参加するかどうかを指定します。 値として **1** を指定すると、CEIP に参加します。**0** を指定すると、参加しません。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。

> [!Important]  
> Configuration Manager バージョン 1802 以降では、CEIP 機能が製品から削除されます。 パラメーターを使用すると、インストールが失敗します。

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

コンソールを開いたときに接続されるサイト サーバーの FQDN を指定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。


### <a name="examples"></a>例

> [!Important]  
> バージョン 1802 以降の場合は、**EnableSQM** パラメーターを指定しないでください

#### <a name="silent-install"></a>サイレント インストール

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>言語パックを使ったサイレント インストール

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>サイレント アンインストール

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>関連項目

管理者は、そのユーザー アカウントに割り当てられたアクセス許可に基づいて、コンソール内のオブジェクトを表示できます。 詳細については、「[ロール ベース管理の基礎](../../../understand/fundamentals-of-role-based-administration.md)」を参照してください。

Configuration Manager コンソールの操作の基礎について詳しくは、[コンソールの使用](../../manage/admin-console.md)に関するページをご覧ください。
