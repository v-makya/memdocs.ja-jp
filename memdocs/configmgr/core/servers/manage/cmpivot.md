---
title: リアルタイム データ用 CMPivot
titleSuffix: Configuration Manager
description: Configuration Manager でクライアントに対してクエリをリアルタイムで実行するために CMPivot を使用する方法について学習します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 11b5a58a6d9501b0368fcb0b47bf31df1bd8a6af
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700584"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>Configuration Manager でのリアルタイム データ用の CMPivot

<!--1358456-->

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、レポートを目的として顧客が使用する、デバイス データの大規模な一元化ストアを常に提供しています。 このサイトでは、通常、週次でこのデータが収集されます。 バージョン 1806 以降導入された CMPivot は、お使いの環境でリアルタイム状態のデバイスへのアクセスを提供する、新しいコンソール内ユーティリティです。 対象となるコレクション内の現在接続されているすべてのデバイス上で直ちにクエリを実行して、結果を返します。 次に、ツール内で、このデータをフィルター処理およびグループ化します。 オンライン クライアントからリアルタイム データを提供することで、業務上の質問に迅速に回答し、問題をトラブルシューティングし、セキュリティの問題に対応できます。

たとえば、[予測実行によるサイド チャネルの脆弱性を緩和する](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)場合、 システムの BIOS の更新が要件の 1 つになっています。 CMPivot を使用して、システム BIOS 情報に対して迅速にクエリを実行し、コンプライアンスにはないクライアントを検索できます。

 > [!IMPORTANT]  
 > - セキュリティ ソフトウェアの中には、c:\windows\ccm\scriptstore から実行されるスクリプトをブロックするものもあります。 これにより、CMPivot クエリの実行が成功するのを防ぐことができます。 CMPivot PowerShell の実行時に、一部のセキュリティ ソフトウェアで監査イベントまたはアラートが生成される可能性もあります。
 > - 特定のマルウェア対策ソフトウェアでは、誤って Configuration Manager 実行スクリプトまたは CMPivot 機能に対してイベントがトリガーされることがあります。 %Windir%\CCM\ScriptStore を除外することをお勧めします。これにより、マルウェア対策ソフトウェアでこれらの機能を許可し、干渉なしで実行することができます。


## <a name="prerequisites"></a>[前提条件]

次のコンポーネントでは、CMPivot を使用する必要があります。

- 対象のデバイスを、Configuration Manager クライアントの最新バージョンにアップグレードします。  

- ターゲット クライアントには、最低限の PowerShell バージョン 4 が必要です。

- 次のエンティティのデータを収集するには、ターゲット クライアントに PowerShell バージョン 5.0 が必要です。  
  - Administrators
  - 接続
  - IPConfig
  - SMBConfig

- CMPivot と [Microsoft Edge](../../../apps/deploy-use/deploy-edge.md) インストーラーは、**Microsoft コード署名**証明書で署名されています。 その証明書が**信頼された発行元**ストアに登録されていない場合は、追加する必要があります。 そうしないと、PowerShell 実行ポリシーが **AllSigned** に設定されている場合に、CMPivot と Microsoft Edge インストーラーが実行されません。 <!--7585106-->

## <a name="permissions"></a>アクセス許可

CMPivot に必要なアクセス許可は次のとおりです。

- **SMS スクリプト** オブジェクトの**読み取り**アクセス許可
- **コレクション**の**スクリプトの実行**アクセス許可
   - または、バージョン 1906 以降では、**コレクション**の **CMPivot の実行**を使用できます。
- **インベントリ レポート**の**読み取り**アクセス許可
- 既定のスコープ

> [!NOTE]
> - **スクリプトの実行**は、**CMPivot の実行**アクセス許可のスーパーセットです。
> - バージョン 1906 以降では、Configuration Manager の組み込みの**セキュリティ管理者**ロールに [CMPivot に対するアクセス許可が追加されています](cmpivot-changes.md#bkmk_cmpivot_secadmin1906)。
 
## <a name="limitations"></a>制限事項

- 階層で Configuration Manager コンソールを*プライマリ サイト*に接続して、CMPivot を実行します。 **[CMPivot の開始]** アクションは、中央管理サイト (CAS) に接続されているときはコンソールに表示されません。
  - Configuration Manager バージョン 1902 以降では、CAS から CMPivot を実行できます。 一部の環境では、追加のアクセス許可が必要になります。 詳しくは、「[バージョン 1902 の CMPivot 変更](cmpivot-changes.md#bkmk_cmpivot1902)」をご覧ください。

- CMPivot は、現在のサイトに接続されているクライアントのデータのみを返します。  

- コレクションに別のサイトのデバイスが含まれる場合、CMPivot の結果は現在のサイトのデバイスのもののみです。  

- エンティティのプロパティ、結果用の列、デバイスのアクションはカスタマイズできません。  

- Configuration Manager コンソールを実行するコンピューターでは、CMPivot のインスタンスは 1 つしか同時に実行できません。  

- バージョン 1806 では、**Administrators** エンティティに対するクエリは、グループの名前が "Administrators" の場合にのみ機能します。 グループ名がローカライズされている場合は機能しません。 たとえば、日本語の "管理者" などです。<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>CMPivot の開始

1. Configuration Manager コンソールで、プライマリ サイトに接続します。 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス コレクション]** ノードを選択します。 対象となるコレクションを選択し、リボンにある **[Start CMPivot]\(CMPivot の開始\)** をクリックして、ツールを起動します。 このオプションが表示されない場合、次の構成を確認します。  
   - アカウントに必要なアクセス許可があるか、サイト管理者に確認します。 詳細については、「[前提条件](#prerequisites)」を参照してください。  
   - コンソールを*プライマリ サイト*に接続します。  

2. インターフェイスでは、ツールの使用に関する詳細情報を提供しています。  

     - 最上部でクエリ文字列を手動入力したり、インライン ドキュメントのリンクをクリックしたりすることも可能です。  

     - いずれかの**エントリ**をクリックして、クエリ文字列にそのエントリを追加します。  

     - **テーブル演算子**、**集計関数**、および**スカラー関数**へのリンクでは、Web ブラウザーの言語リファレンス ドキュメントが開かれます。 CMPivot には [Kusto Query Language (KQL)](/azure/kusto/query/) が使用されます。  

3. クライアントからの結果を表示するために CMPivot ウィンドウは開いたままにします。 CMPivot ウィンドウを閉じたら、このセッションは完了です。
   - クエリを送信すると、クライアントはサーバーに状態のメッセージ応答を送信します。  



## <a name="how-to-use-cmpivot"></a>CMPivot の使用方法

![CMPivot ウィンドウのサンプル](media/1358456-cmpivot-sample.png)

CMPivot ウィンドウには、次の要素があります。  

1. CMPivot が現在対象としているコレクションは、上部のタイトル バーと、ウィンドウ下部の状態バーにあります。 たとえば、上のスクリーンショットの "PM_Team_Machines" です。  

2. 左のウィンドウには、クライアントにある **[エンティティ]** が列挙されます。 一部のエンティティは WMI に依存するのに対し、他はクライアントからデータを取得するのに PowerShell を使用します。   

    - 次のアクション用にエンティティを右クリックします。  

       - **挿入**:現在のカーソルの位置でクエリにエンティティを追加します。 クエリは自動的には実行されません。 このアクションは、エンティティをダブルクリックしたときの既定です。 クエリを構築するときには、このアクションを使用します。  

       - **クエリをすべて実行**:すべてのプロパティを含むこのエンティティ用のクエリを実行します。 1 つのエンティティを迅速にクエリするには、このアクションを使用します。  

       - **デバイスでクエリ実行**:このエンティティ用にクエリを実行し、結果をグループ化します。 たとえば、 `Disk | summarize dcount( Device ) by Name` と記述します。  

    - エンティティを拡張し、各エンティティで利用可能な特定のプロパティを参照します。 プロパティをダブルクリックし、現在のカーソル位置にクエリに追加します。  

3. **[ホーム]** タブには、サンプル クエリおよびサポートされているドキュメントを含む CMPivot の一般的な情報が含まれます。  

4. **[クエリ]** タブには、クエリ ウィンドウ、結果ウィンドウ、状態バーが表示されます。 上のスクリーンショット例では、[クエリ] タブが選択されています。  

5. [クエリ] ウィンドウは、コレクション内のクライアント上で実行するクエリをビルドまたは入力する場所です。  

    - CMPivot には [Kusto Query Language (KQL)](/azure/kusto/query/) のサブセットが使用されます。  

    - クエリ ウィンドウのコンテンツを切り取ったり、コピーしたり、貼り付けます。  
    <!-- markdownlint-disable MD038 -->
    - 既定で、このウィンドウは IntelliSense を使用します。 たとえば、`D` で入力を開始すると、IntelliSense ではその文字で開始するすべてのエンティティを提案します。 オプションを選択し、挿入するために Tab を押します。 パイプ文字とスペース `| ` を入力すると、IntelliSense がすべてのテーブル演算子を提案します。 `summarize` を挿入し、空白を入力すると、IntelliSense はすべての集計関数を提案します。 これらの演算子および関数の詳細については、CMPivot の **[ホーム]** タブをクリックします。  

    - クエリ ウィンドウには、次のオプションもあります。  

        - クエリを実行します。  

        - クエリの履歴一覧で、前後に移動します。  

        - ダイレクト メンバーシップのコレクションを作成します。  

        - クエリ結果を CSV またはクリップボードにエクスポートします。  

6. 結果ウィンドウには、クエリのアクティブ クライアントによって返されたデータが表示されます。  

   - 利用可能な列は、エンティティとクエリによって異なります。  

   - 列名をクリックし、プロパティで結果を並べ替えます。  

   - 任意の列名を右クリックし、その列の同じ情報で結果をグループ化するか、結果を並べ替えます。  

   - デバイス名を右クリックし、デバイスで次の追加のアクションを実行します。  

      - **ピボット先**:デバイスの別のエンティティに対してクエリを実行します。
         - バージョン 2006 以降、 **[ピボット先]** は **[Device Pivot]\(デバイス ピボット\)** に置き換えられました。 詳しくは、「[バージョン 2006 の CMPivot 変更](cmpivot-changes.md#bkmk_2006)」をご覧ください。

      - **スクリプトの実行**:スクリプトの実行ウィザードを起動し、デバイスで既存の PowerShell スクリプトを実行します。 詳細については、「[スクリプトの実行](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script)」を参照してください。  

      - **リモート コントロール**:このデバイスで、Configuration Manager リモート コントロール セッションを起動します。 詳細については、「[Windows クライアント コンピューターをリモート管理する方法](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)」を参照してください。  

      - **リソース エクスプローラー**:このデバイスの Configuration Manager リソース エクスプローラーを起動します。 詳細については、[ハードウェア インベントリの表示](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)に関するページ、または[ソフトウェア インベントリの表示](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)に関するページを参照してください。  

   - デバイスではない任意のセルを右クリックして、次の追加のアクションを実行します。  

     - **コピー**:セルのテキストをクリップボードにコピーします。  

     - **次を含むデバイスを表示**:このプロパティの値のデバイスに対し、クエリを実行します。 たとえば、`OS` クエリの結果から、[Version] 列のセルからこのオプション `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)` を選択します。  

     - **次を含まないデバイスを表示**:このプロパティにこの値がないデバイスに対し、クエリを実行します。 たとえば、`OS` クエリの結果から、[Version] 列のセルからこのオプション `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device` を選択します。  

     - **Bing で検索する**:この値をクエリ文字列として使用し、既定の Web ブラウザーで https://www.bing.com を開きます。  

   - 任意のハイパーリンクが設定されたテキストをクリックし、ビューの中心がその特定の情報になるようにします。  

   - 結果ウィンドウには 20,000 行しか表示されません。 データをさらにフィルタリングするには、クエリを調整するか、より小規模なコレクションで CMPivot を再開します。  

7. ステータス バーには、次の情報が表示されます (左から右へ)。  

   - ターゲット コレクションへの現在のクエリの状態。 状態には次が含まれます。  
     - クエリが完了したアクティブなクライアントの数 (3)  
     - クライアント数の合計 (5)  
     - オフライン クライアントの数 (2)  
     - エラーを返したすべてのクライアント (0)  

       例: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - クライアント操作の ID。 例: `id(16780221)`  

   - 現在のコレクション。 例: `PM_Team_Machines`  

   - 結果ウィンドウ内の行の合計数。 たとえば、 `1 objects` と記述します。  



## <a name="example-scenarios"></a>シナリオ例

次のセクションには、環境で CMPivot を使用する例があります。


### <a name="example-1-stop-a-running-service"></a>例 1:実行中のサービスの停止

会計部署のすべてのデバイスのコンピューター ブラウザーを停止して無効にするよう、セキュリティ管理者から求められました。 会計のすべてのデバイスのコレクションで CMPivot を起動し、 **[サービス]** エンティティで **[クエリをすべて実行]** を選択します。 

`Service`

結果が表示されたら、 **[名前]** 列を右クリックし、 **[グループ化]** を選択します。 

`Service | summarize dcount( Device ) by Name`

**ブラウザー** サービスの行で、**dcount_** 列のハイパーリンク付きの数字をクリックします。 

`Service | where (Name == 'Browser') | summarize count() by Device`

すべてのデバイスを複数選択し、選択を右クリックし、 **[スクリプトの実行]** を選択します。 このアクションは、サービスを停止または無効にするためにある既存のスクリプトを実行するスクリプトの実行ウィザードを起動します。 CMPivot を使用すると、アクティブなすべてのコンピューターのセキュリティ インシデントに迅速に対応したり、スクリプトの実行ウィザードで結果を参照することができます。 次いでフォローアップを行い、アクティブになった後、コレクション内の他のコンピューターを修復する構成基準を作成します。 

![ブラウザー サービスおよびスクリプトの実行アクション用の CMPivot の例](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>例 2:アプリケーションのエラーの先を見越した解決  

先を見越した運用保守を行うには、管理しているサーバーに対して、1 週間に一度 CMPivot を実行し、 **[AppCrash]** エンティティに対して **[クエリをすべて実行]** を実行します。 **[FileName]** 列を右クリックし、 **[昇順で並べ替え]** を選択します。 1 台のデバイスは、毎日約 03:00 のタイムスタンプで sqlsqm.exe から 7 件の結果を返します。 1 つの行でファイル名を選択し、それを右クリックして **[Bing で検索する]** を選択します。 Web ブラウザーで検索結果を参照すると、この問題の情報および解決方法がある Microsoft サポート記事が見つかります。 


### <a name="example-3-bios-version"></a>例 3:BIOS バージョン

[予測実行によるサイド チャネルの脆弱性を緩和する](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)には、システムの BIOS の更新が要件の 1 つになっています。 **BIOS** エンティティ用のクエリで開始します。 次いで、 **[バージョン]** プロパティを **[グループ化]** します。 次いで "LENOVO - 1140" などの特定の値を右クリックし、 **[次を含むデバイスを表示]** を選択します。  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>例 4:空きディスク領域

ネットワーク ファイル サーバーに一時的に大容量のファイルを保存したいが、十分な容量があるのがどれだかわからない場合があります。 ファイル サーバーのコレクションに対して CMPivot を起動し、 **[ディスク]** エンティティに対してクエリを実行します。 CMPivot のクエリを変更し、ストレージのリアルタイム データを含むアクティブなサーバーの一覧を迅速に返します。  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot スタンドアロン

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
## <a name="inside-cmpivot"></a>CMPivot の内部

CMPivot は、Configuration Manager の "高速チャネル" を使用してクライアントにクエリを送信します。 サーバーからのクライアントへのこの通知チャネルは、クライアントの通知アクション、クライアントの状態、Endpoint Protection などその他の機能でも使用されています。 クライアントは、同様に迅速な状態メッセージ システム経由で結果を返します。 状態メッセージは、一時的にデータベースに格納されます。 クライアントの通知に使用されるポートの詳細については、[ポート](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP)に関する記事を参照してください。

クエリとその結果は、単なるテキストです。 エンティティ **InstallSoftware** と **Process** は、最大の結果セットをいくつか返します。 パフォーマンス テスト時、これらのクエリに対する 1 つのクライアントからの状態メッセージの最大ファイル サイズは **1 KB** 未満でした。 50,000 のアクティブなクライアントがある大規模な環境にスケーリングすると、この 1 回限りのクエリは、ネットワーク上で 50 MB 未満のデータしか生成しません。 ウェルカム ページで下線が引かれたすべての項目で、クライアントごとに 1K 未満の情報が返されます。

![CMPivot の下線付きエンティティの例](media/cmpivot-underlined-entities.png)

Configuration Manager 1810 以降、CMPivot では、拡張されたハードウェア インベントリ クラスなどのハードウェア インベントリ データに対してクエリを実行できます。 これらの新しいエンティティ (ウェルカム ページで下線が付いていないエンティティ) は、指定したハードウェア インベントリ プロパティに定義されているデータ量によって、より大きいデータ セットが返される可能性があります。 たとえば、"InstalledExecutable" エンティティは、クエリを実行する特定のデータによって、クライアントごとに数 MB のデータが返される可能性があります。 CMPivot を使用してより大きいコレクションからより大きいハードウェア インベントリ データ セットを返している場合、ご利用のシステム上のパフォーマンスとスケーラビリティに注意してください。

1 時間後にクエリはタイム アウトします。 たとえば、コレクションには 500 のデバイスがあり、450 のクライアントが現在オンラインです。 これらのアクティブなデバイスはクエリを受け取り、ほぼ瞬時に結果を返します。 他の 50 のクライアントがオンラインになるときに、CMPivot ウィンドウを開いたままにした場合、それらもクエリを受け取り、結果を返します。 

## <a name="log-files"></a>ログ ファイル

 CMPivot のやり取りは、次のログ ファイルに記録されます。

**サーバー側:**
- SmsProv.log
- BgbServer.log
- StateSys.log

**クライアント側:**
- CCMNotificationAgent.log
- Scripts.log
- StateMessage.log

詳細については、[ログ ファイル](../../plan-design/hierarchy/log-files.md)に関するページと「[Troubleshooting CMPivot](cmpivot-tsg.md)」 (CMPivot のトラブルシューティング) を参照してください。

## <a name="next-steps"></a>次のステップ

- [CMPivot に対する変更](cmpivot-changes.md)
- [CMPivot のトラブルシューティング](cmpivot-tsg.md)
- [PowerShell スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)