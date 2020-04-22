---
title: サービス接続ツール
titleSuffix: Configuration Manager
description: このツールによって、Configuration Manager クラウド サービスに接続し、使用状況の情報を手動でアップロードできます。
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e535653e0f31e186a6bdbde8da77750f2afdfdb0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690300"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Configuration Manager のサービス接続ツールの使用

*適用対象:Configuration Manager (Current Branch)*

サービス接続ポイントがオフライン モードになっている場合、または Configuration Manager のサイト システム サーバーがインターネットに接続されていない場合は、**サービス接続ツール**を使用してください。 このツールは、Configuration Manager に最新の更新プログラムを適用することで、サイトを最新の状態に保つことができます。  

実行時に、ツールを手動で Configuration Manager クラウド サービスに接続し、階層の使用状況の情報をアップロードしたり、更新プログラムをダウンロードしたりすることができます。 ご使用の展開に適切な更新プログラムをクラウド サービスが提供できるようにするには、使用状況データのアップロードが必要です。  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>サービス接続ツールを使用するための前提条件
次の前提条件と既知の問題があります。

**必要条件:**

- サービス接続ポイントがインストールされ、 **[オフライン (オンデマンド接続)]** に設定されている必要があります。  

- このツールがコマンド プロンプトから実行される必要があります。  

- ツールを実行する各コンピューター (サービス接続ポイントのコンピューター、およびインターネットに接続されているコンピューター) は、x64 ビット システムである必要があります。また、以下がインストールされている必要もあります。  

  - **Visual C++ 再頒布可能パッケージ** x86 と x64 の両方のファイル。   Configuration Manager の既定では、これらのファイルを、サービス接続ポイントをホストする x64 バージョンのコンピューターにインストールします。  

    Visual C++ ファイルのコピーをダウンロードするには、Microsoft ダウンロード センターの「 [Visual Studio 2013 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=40784) 」にアクセスしてください。  

  - .NET Framework 4.5.2 以降。  

- ツールの実行に使用するアカウントには次が必要です。
  - サービス接続ポイントをホストするコンピューター (ツールが実行される) の**ローカル管理者** のアクセス許可。
  - サイト データベースに対する**読み取り** アクセス許可。  



- ファイルと更新プログラムを格納するための十分な空き領域を持つ USB ドライブ、またはサービス接続ポイントのコンピューターとインターネットに接続しているコンピューターの間でファイルを転送する別の方法が必要になります。 (このシナリオでは、サイトとマネージド コンピューターはインターネットに直接接続されていないことを想定しています)。  



## <a name="use-the-service-connection-tool"></a>サービス接続ツールの使用  

 サービス接続ツール (**serviceconnectiontool.exe**) は、Configuration Manager インストール メディアの **%path%\smssetup\tools\ServiceConnectionTool** フォルダーにあります。 必ず、使用している Configuration Manager のバージョンに合ったサービス接続ツールを使用してください。


 この手順では、コマンド ラインの例で、次のファイル名とフォルダーの場所を使用します (これらのパスとファイル名を使用する必要はありません。ご使用の環境や設定に一致する代替のパスとファイル名を使用できます)。  

- USB スティック (サーバー間で転送するためデータが格納される場所) へのパス: **D:\USB\\**  

- サイトからエクスポートしたデータが格納される .cab ファイルの名前: **UsageData.cab**  

- サーバー間で転送するため Configuration Manager のダウンロードされた更新プログラムが格納される空のフォルダーの名前: **UpdatePacks**  

サービス接続ポイントをホストするコンピューターで、以下を実行します。  

- 管理者特権でコマンド プロンプトを開き、 **serviceconnectiontool.exe**を格納する場所にディレクトリを変更します。  

  既定では、このツールは Configuration Manager インストール メディアの **%path%\smssetup/tools\ServiceConnectionTool** フォルダーにあります。 サービス接続ツールを動作させるために、このフォルダーにあるすべてのファイルを同一のフォルダー内に配置する必要があります。  

次のコマンドを実行すると、ツールにより、使用状況の情報を含む .cab ファイルが準備されて、指定した場所にコピーされます。 .cab ファイル内のデータは、収集のためにサイトが構成された診断の使用状況データのレベルに基づいています。 (「[Configuration Manager の診断結果と使用状況データ](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)」を参照してください)。  .cab ファイルを作成するには、次のコマンドを実行します。  

- **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

USB ドライブに ServiceConnectionTool フォルダーとその中身をすべてコピーする必要もあります。または、手順 3 と 4 で使用するコンピューターで使用可能にする必要があります。  

### <a name="overview"></a>概要
#### <a name="there-are-three-primary-steps-to-using-the-service-connection-tool"></a>サービス接続ツールを使用するための 3 つの主要なステップがあります  

1.  **準備**: このステップは、サービス接続ポイントをホストするコンピューターで実行されます。 ツールが実行されると、使用状況データが .cab ファイルに格納され、そのファイルが USB ドライブ (または指定した代替の転送場所) に保存されます。  

2.  **接続**: このステップでは、インターネットに接続されたリモート コンピューターでツールを実行し、使用状況データのアップロードおよび更新プログラムのダウンロードを行います。  

3.  **インポート**: このステップは、サービス接続ポイントをホストするコンピューターで実行されます。 実行すると、ダウンロードした更新プログラムがツールによってインポートされ、サイトに追加されるため、Configuration Manager コンソールから更新プログラムを表示したり、インストールしたりできるようになります。  

バージョン 1606 以降では、Microsoft に接続すると複数の .cab ファイルを (別の階層からそれぞれ) 一度にアップロードして、プロキシ サーバーとプロキシ サーバーのユーザーを指定できます。   

#### <a name="to-upload-multiple-cab-files"></a>複数の .cab ファイルをアップロードするには
- 個別の階層からエクスポートした各 .cab ファイルを同じフォルダーに配置します。 各ファイルの名前は一意である必要があります。名前は、必要に応じて手動で変更することができます。
- 次に、データを Microsoft にアップロードするコマンドを実行する際に、.cab ファイルを含むフォルダーを指定します。 (更新プログラム 1606 より前では、一度にアップロードできるデータは 1 つの階層からだけであり、ツールでフォルダーの .cab ファイルに名前を指定する必要がありました。)
- その後、階層のサービス接続ポイントでインポート タスクを実行すると、ツールで自動的にその階層のデータのみがインポートされます。  

#### <a name="to-specify-a-proxy-server"></a>プロキシ サーバーを指定するには
次のオプション パラメーターを使用して、プロキシ サーバーを指定できます (これらのパラメーターの使用に関する詳細は、このトピックのコマンド ライン パラメーターのセクションで確認できます)。
- **-proxyserveruri [FQDN_of_proxy_sever]**  パラメーターを使用して、この接続に使用するプロキシ サーバーを指定します。
- **-proxyusername [username]**  プロキシ サーバーのユーザーを指定する必要がある場合に、このパラメーターを使用します。

#### <a name="specify-the-type-of-updates-to-download"></a>ダウンロードする更新プログラムの種類を指定する
バージョン 1706 より、ツールの既定のダウンロード動作が変更され、ダウンロードするファイルの種類を制御するオプションがツールでサポートされるようになりました。
- 既定では、サイトのバージョンに適用される最新の更新プログラムのみがダウンロードされます。 修正プログラムはダウンロードされません。

この動作を変更するには、次のパラメーターのいずれか 1 つを使用してダウンロードするファイルの種類を変更します。 

> [!NOTE]
> サイトのバージョンは、ツールの実行時にアップロードされる .cab ファイル内のデータから決定されます。
>
> バージョンを確認するには、.cab ファイル内の *SiteVersion*.txt ファイルを探してください。

- **-downloadall**  このオプションではサイトのバージョンに関係なく、更新プログラムと修正プログラムを含めたすべてがダウンロードされます。
- **-downloadhotfix**  このオプションではサイトのバージョンに関係なくすべての修正プログラムがダウンロードされます。
- **-downloadsiteversion**  このオプションでは、サイトのバージョン以降のバージョンの更新プログラムと修正プログラムがダウンロードされます。

*-downloadsiteversion* を使用するコマンド ラインの例:
- **serviceconnectiontool.exe -connect  *-downloadsiteversion* -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**




### <a name="to-use-the-service-connection-tool"></a>サービス接続ツールを使用するには  

1. サービス接続ポイントをホストするコンピューターで、以下を実行します。  

   - 管理者特権でコマンド プロンプトを開き、 **serviceconnectiontool.exe**を格納する場所にディレクトリを変更します。   

2. 次のコマンドを実行して、ツールで使用状況の情報を含む .cab ファイルを準備し、指定した場所にコピーします。  

   - **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

   1 つ以上の階層から同時に複数の .cab ファイルをアップロードする場合は、フォルダー内の各 .cab ファイルの名前は一意である必要があります。 フォルダーに追加するファイルの名前は手動で変更できます。

   Configuration Manager のクラウド サービスにアップロードするために収集される使用状況情報を表示する場合は、次のコマンドを実行し、.csv ファイルとして同じデータをエクスポートすると、Excel のようなアプリケーションを使用して表示できます。  

   - **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3. 準備ステップが完了したら、インターネットに接続しているコンピューターに USB ドライブを移動します (または別の方法でエクスポートされたデータを転送します)。  

4. インターネットにアクセスできるコンピューターで、管理者特権を使用してコマンド プロンプトを開き、ツール (  **serviceconnectiontool.exe** ) とそのフォルダーのその他のファイルのコピーを格納している場所にディレクトリを変更します。  

5. 次のコマンドを実行し、使用状況情報のアップロードと Configuration Manager の更新プログラムのダウンロードを開始します。  

   - **serviceconnectiontool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**

   このコマンドラインのより多くの例については、このトピックで後述する「[コマンド ライン オプション](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd)」を参照してください。

   > [!NOTE]  
   >  Configuration Manager のクラウド サービスに接続するためのコマンド ラインを実行すると、次のようなエラーが発生する可能性があります。  
   >   
   > - ハンドルされない例外: System.UnauthorizedAccessException:  
   >   
   >      パス C:\  
   >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' へのアクセスが拒否されました。  
   >   
   > このエラーは無視しても問題ありません。エラー ウィンドウを閉じて、続行することができます。  

6. Configuration Manager の更新プログラムのダウンロードが完了したら、サービス接続ポイントをホストしているコンピューターに USB ドライブを移動します (または別の方法でエクスポートされたデータを転送します)。  

7. サービス接続ポイントをホストするコンピューターで、管理者特権でコマンド プロンプトを開き、 **serviceconnectiontool.exe**が格納されている場所にディレクトリを変更して、次のコマンドを実行します。  

   - **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8. インポートが完了したら、コマンド プロンプトを閉じることができます。 (該当する階層の更新プログラムのみがインポートされます)。  

9. Configuration Manager コンソールを開き、 **[管理]**  >  **[更新とサービス]** の順に移動します。 インポートされた更新プログラムは、インストールできるようになりました (1702 より前のバージョンでは、[更新とサービス] は、 **[管理]**  >  **[クラウド サービス]** にありました)。

   更新プログラムのインストールの詳細については、「[Configuration Manager のコンソール内更新プログラムのインストール](../../../core/servers/manage/install-in-console-updates.md)」を参照してください。  

## <a name="log-files"></a><a name="bkmk_cmd"></a> ログ ファイル

**ServiceConnectionTool.log**

サービス接続ツールを実行するたびに、ツールと同じ場所に **ServiceConnectionTool.log** という名前のログ ファイルが生成されます。  このログ ファイルでは、使用コマンドに基づく、ツールの実行に関する簡単な詳細が示されます。  ツールを実行するたびに、既存のログ ファイルが置き換えられます。

**ConfigMgrSetup.log**

ツールを使用して接続し更新プログラムをダウンロードする場合、システム ドライブのルート上に、**ConfigMgrSetup.log** という名前のログ ファイルが生成されます。  このログ ファイルでは、ダウンロードされたファイル、抽出されたファイル、ハッシュのチェックの成否など、より詳しい情報が示されます。

## <a name="command-line-options"></a><a name="bkmk_cmd"></a> コマンド ライン オプション  
サービス接続ポイント ツールのヘルプ情報を表示するには、コマンド プロンプトを開き、ツールを格納するフォルダーに移動して、コマンド  **serviceconnectiontool.exe**を実行します。  


|コマンド ライン オプション|詳細|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [drive:][path][filename.cab]**|このコマンドは、現在の使用状況データを .cab ファイルに格納します。<br /><br /> サービス接続ポイントをホストするサーバーで、 **ローカル管理者** としてこのコマンドを実行します。<br /><br /> 例:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [drive:][path] -updatepackdest [drive:][path] -proxyserveruri [FQDN of proxy server] -proxyusername [username]** <br /> <br /> 1606 より前のバージョンの Configuration Manager を使用する場合は、.cab ファイルの名前を指定する必要があり、プロキシ サーバーのオプションを使用することはできません。  サポートされているコマンド パラメーターは次のとおりです。 <br /> **-connect -usagedatasrc [drive:][path][filename] -updatepackdest [drive:][path]** |このコマンドは、Configuration Manager のクラウド サービスに接続し、指定した場所から使用状況データの .cab ファイルをアップロードしたり、利用可能な更新パックとコンソールのコンテンツをダウンロードしたりします。 プロキシ サーバーのオプションは省略できます。<br /><br /> インターネットに接続できるコンピューターで、 **ローカル管理者** としてこのコマンドを実行します。<br /><br /> プロキシ サーバーを使用せずに接続する例: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> プロキシ サーバーを使用して接続する例: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> 1606 より前のバージョンを使用する場合は、.cab ファイルのファイル名を指定する必要があります。また、プロキシ サーバーを指定することはできません。 次のコマンド ラインの例を使用します: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [drive:][path]**|このコマンドは、先ほど Configuration Manager コンソールにダウンロードした更新パックとコンソールのコンテンツをインポートします。<br /><br /> サービス接続ポイントをホストするサーバーで、 **ローカル管理者** としてこのコマンドを実行します。<br /><br /> 例:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [drive:][path][filename.csv]**|このコマンドは使用状況データを .csv ファイルにエクスポートします。このファイルでデータを確認できます。<br /><br /> サービス接続ポイントをホストするサーバーで、 **ローカル管理者** としてこのコマンドを実行します。<br /><br /> 例: **-export -dest D:\USB\usagedata.csv**|  
