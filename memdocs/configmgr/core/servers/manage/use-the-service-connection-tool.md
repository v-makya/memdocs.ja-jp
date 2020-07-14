---
title: サービス接続ツール
titleSuffix: Configuration Manager
description: このツールによって、Configuration Manager クラウド サービスに接続し、使用状況の情報を手動でアップロードできます。
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 48aa08f3318aaa4629691bfb30b60580cd3e25f0
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946846"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Configuration Manager のサービス接続ツールを使用する

*適用対象:Configuration Manager (Current Branch)*

サービス接続ポイントがオフライン モードの場合は、**サービス接続ツール**を使用します。 これは、Configuration Manager サイト システムのサーバーがインターネットに接続されていない場合にも使用できます。 このツールは、Configuration Manager の最新の更新プログラムを使用して、サイトを最新の状態に保つのに役立ちます。

このツールを実行すると、Configuration Manager クラウド サービスへの接続、階層の使用状況に関する情報のアップロード、更新プログラムのダウンロードが行われます。 クラウド サービスからお客様の環境に適切な更新プログラムが提供されるためには、使用状況データのアップロードが必要です。

## <a name="prerequisites"></a>[前提条件]

- サイトにサービス接続ポイントがあり、 **[オフライン (オンデマンド接続)]** 用に構成していること。

- コマンド プロンプトから管理者としてツールを実行します。 ユーザー インターフェイスはありません。

- サービス接続ポイント、およびインターネットに接続できるコンピューターからツールを実行します。 これらの各コンピューターには、x64 ビットの OS と、次のコンポーネントが必要です。

  - **Visual C++ 再頒布可能パッケージ** x86 と x64 の両方のファイル。 Configuration Manager の既定では、これらのファイルを、サービス接続ポイントをホストする x64 バージョンのコンピューターにインストールします。 このコンポーネントをダウンロードするには、「[Visual Studio 2013 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=40784)」を参照してください。

  - **.NET Framework 4.5.2** 以降

- ツールの実行に使用するアカウントには、次のアクセス許可が必要です。

  - サービス接続ポイントをホストするコンピューターの**ローカル管理者**

  - サイト データベースに対する**読み取り**アクセス許可

- インターネットにアクセスできるコンピューターとサービス接続ポイント間でファイルを転送する方法が必要です。 たとえば、ファイルと更新プログラムを格納するのに十分な空き領域がある USB ドライブなどです。

## <a name="overview"></a>概要

1. **準備**: サービス接続ポイント上でツールを実行します。 使用状況データが指定した場所にある .cab ファイルに格納されます。 そのデータ ファイルを、インターネット接続しているコンピューターにコピーします。

2. **接続**: インターネットに接続しているコンピューター上でツールを実行します。 使用状況データがアップロードされた後、Configuration Manager 更新プログラムがダウンロードされます。 ダウンロードされた更新プログラムをサービス接続ポイントにコピーします。

    それぞれ異なる階層からの複数のデータ ファイルを、一度にアップロードできます。 プロキシ サーバーとプロキシ サーバーのユーザーを指定することもできます。

3. **インポート**: サービス接続ポイント上でツールを実行します。 更新プログラムがインポートされ、サイトに追加されます。 その後、Configuration Manager コンソールで表示し、[これらの更新プログラムをインストール](install-in-console-updates.md)できます。

### <a name="upload-multiple-data-files"></a>複数のデータ ファイルをアップロードする

- 別々の階層からエクスポートされたすべてのデータ ファイルを同じフォルダーに配置します。 各ファイルに一意の名前を付けます。 必要に応じて、手動で名前を変更できます。

- Microsoft にデータをアップロードするためにツールを実行する際に、データ ファイルが格納されているフォルダーを指定します。

- データをインポートするためにツールを実行すると、その階層のデータのみがインポートされます。

### <a name="specify-a-proxy-server"></a>プロキシ サーバーを指定する

インターネットに接続しているコンピューターにプロキシ サーバーが必要な場合、このツールでは基本的なプロキシ構成がサポートされています。 省略可能なパラメーター **-proxyserveruri** と **-proxyusername** を使用してください。 詳細については、「[コマンド ライン パラメーター](#bkmk_cmd)」をご覧ください。

### <a name="specify-the-type-of-updates-to-download"></a>ダウンロードする更新プログラムの種類を指定する

このツールでは、ダウンロードするファイルを制御するオプションがサポートされています。 既定では、サイトのバージョンに適用される最新の更新プログラムのみがダウンロードされます。 修正プログラムはダウンロードされません。

この動作を変更するには、次のパラメーターのいずれかを使用してダウンロードするファイルの種類を変更します。

- **-downloadall**:更新プログラムや修正プログラムなど、サイトのバージョンにかかわらず、すべての更新プログラムをダウンロードします。
- **-downloadhotfix**:サイトのバージョンにかかわらず、すべての修正プログラムをダウンロードします。
- **-downloadsiteversion**:サイトのバージョンよりも新しいバージョンの更新プログラムと修正プログラムをダウンロードします。

    > [!IMPORTANT]
    > Configuration Manager バージョン 2002 の既知の問題が原因で、既定の動作は想定どおりに動作しません。 **-downloadsiteversion** パラメーターを使用して、バージョン 2002 に必要な更新プログラムをダウンロードしてください。<!-- 7594517 -->

詳細については、「[コマンド ライン パラメーター](#bkmk_cmd)」をご覧ください。

> [!TIP]
> ツールによって、データ ファイルからサイトのバージョンが特定されます。 バージョンを確認するには、.cab ファイルで、名前にサイト バージョンが付いたテキスト ファイルを探してください。

## <a name="use-the-tool"></a>ツールを使用する  

サービス接続ツールは、Configuration Manager インストール メディアの次のパスにあります: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe`。 必ず、使用している Configuration Manager のバージョンに合ったサービス接続ツールを使用してください。 サービス接続ツールを動作させるには、これらのファイルがすべて同じフォルダー内にある必要があります。

**ServiceConnectionTool** フォルダーを、そのすべての内容と共にインターネットに接続しているコンピューターにコピーします。

以下の手順のコマンド ライン例では、次のファイル名とフォルダーの場所を使用します。 お客様は、これらのパスとファイル名を使用する必要はありません。 ご自分の環境と設定に一致する代替を使用できます。

- サービス接続ポイント上の Configuration Manager インストール メディアのソース ファイルへのパス: `C:\Source`

- コンピューター間で転送するデータを格納する USB ドライブへのパス: `D:\USB\`

- サイトからエクスポートするデータ ファイルの名前: `UsageData.cab`

- ツールによってダウンロードされた Configuration Manager の更新プログラムが格納される空のフォルダーの名前: `UpdatePacks`

### <a name="prepare"></a>準備

1. サービス接続ポイントをホストするコンピューター上で、管理者としてコマンド プロンプトを開き、ツールの場所にディレクトリを変更します。 次に例を示します。

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. 次のコマンドを実行して、データ ファイルを準備します。

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > 複数の階層からのデータ ファイルを同時にアップロードする場合は、各データ ファイルに一意の名前を付けます。 必要に応じて、後でファイルの名前を変更できます。

    ファイル内のデータは、お客様がサイトに対して構成した診断と使用状況データのレベルに基づいています。 詳細については、[診断結果と使用状況データの概要](../../plan-design/diagnostics/diagnostics-and-usage-data.md)に関する記事をご覧ください。 ツールを使用してデータを CSV ファイルにエクスポートし、内容を表示できます。 詳細については、「[-export](#-export)」をご覧ください。

1. ツールによる使用状況データのエクスポートが完了したら、インターネットにアクセスできるコンピューターにデータ ファイルをコピーします。

### <a name="connect"></a>接続

1. インターネットにアクセスできるコンピューター上で、管理者としてコマンド プロンプトを開き、ツールの場所にディレクトリを変更します。 この場所は **ServiceConnectionTool** フォルダー全体のコピーです。 次に例を示します。

    `cd D:\USB\ServiceConnectionTool\`

1. 次のコマンドを実行してデータ ファイルをアップロードし、Configuration Manager の更新プログラムをダウンロードします。

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    その他の例については、「[コマンド ライン パラメーター](#bkmk_cmd)」をご覧ください。

    > [!NOTE]  
    > このコマンド ラインを実行すると、次のエラーが表示される場合があります。
    >
    > **ハンドルされない例外: System.UnauthorizedAccessException:パス 'C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' へのアクセスが拒否されました。**
    >
    > このエラーは無視してかまいません。 エラー ウィンドウを閉じて続行してください。

1. ツールによる更新プログラムのダウンロードが完了したら、それらをサービス接続ポイントにコピーします。

### <a name="import"></a>インポート

1. サービス接続ポイントをホストするコンピューター上で、管理者としてコマンド プロンプトを開き、ツールの場所にディレクトリを変更します。 次に例を示します。

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. 次のコマンドを実行して、更新プログラムをインポートします。

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. インポートが完了したら、コマンド プロンプトを閉じます。 該当する階層の更新プログラムのみがインポートされます。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[更新とサービス]** ノードを選択します。 インポートされた更新プログラムをインストールできるようになりました。 詳細については、[コンソール内の更新プログラムのインストール](install-in-console-updates.md)に関するページを参照してください。

## <a name="log-files"></a>ログ ファイル

- **ServiceConnectionTool.log**:サービス接続ツールを実行するたびに、このログ ファイルに書き込まれます。 ログ ファイルのパスは、常にツールと同じ場所です。 このログ ファイルには、使用するパラメーターに基づいて、ツールの使用状況に関する簡単な情報が記録されます。 ツールを実行するたびに、ツールによって既存のログ ファイルが置き換えられます。

- **ConfigMgrSetup.log**:[接続](#connect)フェーズ中、ツールによって、システム ドライブのルートにあるこのログ ファイルに書き込みが行われます。 このログ ファイルには、より詳細な情報が記録されます。 たとえば、ツールによってダウンロードされるファイルや、ハッシュのチェックが成功したかどうかなどです。

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a> コマンド ライン パラメーター

このセクションでは、サービス接続ツールで使用できるすべてのパラメーターをアルファベット順に示します。

### <a name="-connect"></a>-connect

インターネットにアクセスできるコンピューター上で[接続](#connect)フェーズ中に使用します。 Configuration Manager クラウド サービスへの接続、データ ファイルのアップロード、更新プログラムのダウンロードが行われます。

次のパラメーターが必要です。

- **-usagedatasrc**:アップロードするデータ ファイルの場所
- **-updatepackdest**:ダウンロードされた更新プログラム用のパス

次の省略可能なパラメーターを使用することもできます。

- **-proxyserveruri**:プロキシ サーバーの FQDN
- **-proxyusername**:プロキシ サーバーのユーザー名
- **-downloadall**:更新プログラムや修正プログラムなど、サイトのバージョンにかかわらず、すべてのものをダウンロードします。
- **-downloadhotfix**:サイトのバージョンにかかわらず、すべての修正プログラムをダウンロードします。
- **-downloadsiteversion**:サイトのバージョンよりも新しいバージョンの更新プログラムと修正プログラムをダウンロードします。

#### <a name="example-of-connect-without-a-proxy-server"></a>プロキシ サーバーを使用しない接続の例

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>プロキシ サーバーを使用する接続の例

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>サイトのバージョンの適用可能な更新プログラムのみをダウンロードする接続の例

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-dest

エクスポートする CSV ファイルのパスとファイル名を指定するための、 **-export** パラメーターと共に必須のパラメーターです。 詳細については、「[-export](#-export)」をご覧ください。

### <a name="-downloadall"></a>-downloadall

更新プログラムや修正プログラムなど、サイトのバージョンにかかわらず、すべてのものをダウンロードするための、 **-connect** パラメーターと共に使用する省略可能なパラメーターです。 詳細については、「[-connect](#connect)」をご覧ください。

### <a name="-downloadhotfix"></a>-downloadhotfix

サイトのバージョンにかかわらず、すべての修正プログラムのみをダウンロードするための、 **-connect** パラメーターと共に使用する省略可能なパラメーターです。 詳細については、「[-connect](#-connect)」をご覧ください。

### <a name="-downloadsiteversion"></a>-downloadsiteversion

サイトのバージョンよりも新しいバージョンの更新プログラムと修正プログラムのみをダウンロードするための、 **-connect** パラメーターと共に使用する省略可能なパラメーターです。 詳細については、「[-connect](#-connect)」をご覧ください。

### <a name="-export"></a>-export

使用状況データを CSV ファイルにエクスポートするために、[準備](#prepare)フェーズ中に使用します。 サービス接続ポイント上で管理者として実行します。 この操作により、Microsoft にアップロードする前に使用状況データの内容を確認できます。 CSV ファイルの場所を指定するには、 **-dest** パラメーターが必要です。

#### <a name="example-of-export"></a>エクスポートの例

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>-import

[インポート](#import) フェーズ中にサービス接続ポイント上で使用して、サイトに更新プログラムをインポートします。 ダウンロードされた更新プログラムの場所を指定するには、 **-updatepacksrc** パラメーターが必要です。

#### <a name="example-of-import"></a>インポートの例

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>-prepare

[準備](#prepare)フェーズ中にサービス接続ポイント上で使用して、サイトから使用状況データをエクスポートします。 エクスポートされたデータ ファイルの場所を指定するには、 **-usagedatadest** パラメーターが必要です。

#### <a name="example-of-prepare"></a>準備の例

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>-proxyserveruri

プロキシ サーバーの FQDN を指定するための、 **-connect** パラメーターと共に使用する省略可能なパラメーターです。 詳細については、「[-connect](#-connect)」をご覧ください。

### <a name="-proxyusername"></a>-proxyusername

プロキシ サーバーで認証するユーザー名を指定するための、 **-connect** パラメーターと共に使用する省略可能なパラメーターです。 詳細については、「[-connect](#-connect)」をご覧ください。

### <a name="-updatepackdest"></a>-updatepackdest

ダウンロードされた更新プログラム用のパスを指定するための、 **-connect** パラメーターと共に必須のパラメーターです。 詳細については、「[-connect](#-connect)」をご覧ください。

### <a name="-updatepacksrc"></a>-updatepacksrc

ダウンロードされた更新プログラムのパスを指定するための、 **-import** パラメーターと共に必須のパラメーターです。 詳細については、「[-import](#-import)」をご覧ください。

### <a name="-usagedatadest"></a>-usagedatadest

エクスポートされたデータ ファイルのパスとファイル名を指定するための、 **-prepare** パラメーターと共に必須のパラメーターです。 詳細については、「[-prepare](#-prepare)」をご覧ください。

## <a name="next-steps"></a>次のステップ

[コンソール内の更新プログラムのインストール](install-in-console-updates.md)

[診断および使用状況データを使用する方法](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
