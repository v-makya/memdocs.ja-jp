---
title: リアルタイム データ用 CMPivot
titleSuffix: Configuration Manager
description: Configuration Manager でクライアントに対してクエリをリアルタイムで実行するために CMPivot を使用する方法について学習します。
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcd441c7f35748f42adc8824c68ec703291a13e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702090"
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


- CMPivot のアクセス許可:
  - **SMS スクリプト** オブジェクトの**読み取り**アクセス許可
  - **コレクション**の**スクリプトの実行**アクセス許可
    - または、バージョン 1906 以降では、**コレクション**の **CMPivot の実行**を使用できます。
  - **インベントリ レポート**の**読み取り**アクセス許可
  - 既定のスコープ

>[!NOTE]
> **スクリプトの実行**は、**CMPivot の実行**アクセス許可のスーパーセットです。
 
## <a name="limitations"></a>制限事項

- 階層で Configuration Manager コンソールを*プライマリ サイト*に接続して、CMPivot を実行します。 **[CMPivot の開始]** アクションは、中央管理サイト (CAS) に接続されているときはコンソールに表示されません。
  - Configuration Manager バージョン 1902 以降では、CAS から CMPivot を実行できます。 一部の環境では、追加のアクセス許可が必要になります。 詳細については、「[CMPivot starting in version 1902](#bkmk_cmpivot1902)」(バージョン 1902 以降の CMPivot) を参照してください。

- CMPivot は、現在のサイトに接続されているクライアントのデータのみを返します。  

- コレクションに別のサイトのデバイスが含まれる場合、CMPivot の結果は現在のサイトのデバイスのもののみです。  

- エンティティのプロパティ、結果用の列、デバイスのアクションはカスタマイズできません。  

- Configuration Manager コンソールを実行するコンピューターでは、CMPivot のインスタンスは 1 つしか同時に実行できません。  

- バージョン 1806 では、**Administrators** エンティティに対するクエリは、グループの名前が "Administrators" の場合にのみ機能します。 グループ名がローカライズされている場合は機能しません。 たとえば、日本語の "管理者" などです。<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>CMPivot の開始

1. Configuration Manager コンソールで、プライマリ サイトに接続します。 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス コレクション]** ノードを選択します。 対象となるコレクションを選択し、リボンにある **[Start CMPivot]\(CMPivot の開始\)** をクリックして、ツールを起動します。  

    > [!Tip]  
    > このオプションが表示されない場合、次の構成を確認します。  
    > 
    > - アカウントに必要なアクセス許可があるか、サイト管理者に確認します。 詳細については、「[前提条件](#prerequisites)」を参照してください。  
    > 
    > - コンソールを*プライマリ サイト*に接続します。  

2. インターフェイスでは、ツールの使用に関する詳細情報を提供しています。  

     - 最上部でクエリ文字列を手動入力したり、インライン ドキュメントのリンクをクリックしたりすることも可能です。  

     - いずれかの**エントリ**をクリックして、クエリ文字列にそのエントリを追加します。  

     - **テーブル演算子**、**集計関数**、および**スカラー関数**へのリンクでは、Web ブラウザーの言語リファレンス ドキュメントが開かれます。 CMPivot には [Kusto Query Language (KQL)](https://docs.microsoft.com/azure/kusto/query/) が使用されます。  

3. クライアントからの結果を表示するために CMPivot ウィンドウは開いたままにします。 CMPivot ウィンドウを閉じたら、このセッションは完了です。  

    > [!Note]  
    > クエリを送信すると、クライアントはサーバーに状態のメッセージ応答を送信します。  



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

    - CMPivot には [Kusto Query Language (KQL)](https://docs.microsoft.com/azure/kusto/query/) のサブセットが使用されます。  

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


## <a name="cmpivot-starting-in-version-1810"></a><a name="bkmk_cmpivot"></a> バージョン 1810 以降の CMPivot
<!--1359068, 3607759-->

Configuration Manager バージョン 1810 以降、CMPivot には次の改善が含まれています。

- [CMPivot のユーティリティとパフォーマンス](#bkmk_cmpivot-perf)
- [スカラー関数](#bkmk_cmpivot-functions)  
- [視覚エフェクトのレンダリング](#bkmk_cmpivot-charts)  
- [ハードウェア インベントリ](#bkmk_cmpivot-hinv)  
- [スカラー演算子](#bkmk_cmpivot-operators)  
- [クエリの概要](#bkmk_cmpivot-summary)  
- [監査ステータス メッセージ](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a> CMPivot のユーティリティとパフォーマンス

- CMPivot では、20,000 行ではなく、最大 100,000 個のセルが返されます。
  - エンティティにプロパティが 5 個ある場合 (5 列を意味する)、最大 20,000 行が表示されます。
  - 10 個のプロパティを持つエンティティの場合、最大 10,000 行が表示されます。
  - 表示された合計データは、セルが 100,000 個以下になります。
- [クエリ概要] タブで、エラーが発生したデバイスまたはオフラインのデバイスを選択し、**コレクションを作成する**オプションを選択します。 このオプションにより、修復展開でこれらのデバイスを簡単に対象として設定できます。
- フォルダー アイコンをクリックして、**お気に入り**のクエリを保存します。
   ![CMPivot でお気に入りのクエリを保存する例](media/cmpivot-favorite.png)

- 1810 バージョンに更新したクライアントでは、高速の通信チャネルでサイトに 80 KB 未満の出力が返されます。
  - この変更により、スクリプトまたはクエリの出力を表示するパフォーマンスが上がります。
  - スクリプトまたはクエリの出力が 80 KB を超える場合、クライアントによって状態メッセージを介してデータが送信されます。
  - クライアントが 1810 クライアント バージョンに更新されていない場合、状態メッセージが引き続き使用されます。

- CMPivot を開始すると、次のエラーが表示される場合があります。**スクリプトのバージョンに互換性がないため、現時点では CMPivot を使用できません。この問題の原因として考えられるのは、階層でサイトがアップグレード中であることです。アップグレードが完了するまで待ってから、もう一度お試しください。**

  - このメッセージが表示された場合は、次の可能性があります。
    - セキュリティ スコープが適切に設定されていない。
    - プロセスのアップグレードに関する問題がある。
    - 基になる CMPivot スクリプトに互換性がない。


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a> スカラー関数
CMPivot では、次のスカラー関数がサポートされています。
- **ago()** :指定された期間を現在の UTC 時刻から減算します  
- **datetime_diff()** :予定表の 2 つの日時値の差を計算します  
- **now()** :現在の UTC 時刻を返します  
- **bin()** :指定のビンのサイズの倍数の整数に値を切り捨てます  

> [!Note]  
> 日時データ型は、通常は日付と時刻として表現される、時間の瞬間を表します。 時刻値は 1 秒単位で測定されます。 日時値は、常に UTC タイム ゾーンで表されます。 日時リテラルは、常に ISO 8601 形式 (たとえば、`yyyy-mm-dd HH:MM:ss`) で表されます。  

#### <a name="examples"></a>例
- `datetime(2015-12-31 23:59:59.9)`: 特定の日時リテラル   
- `now()`: 現在の時刻  
- `ago(1d)`: 現在の時刻より 24 時間前  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a> 視覚エフェクトのレンダリング

CMPivot に KQL の[レンダリング演算子](https://docs.microsoft.com/azure/kusto/query/renderoperator)の基本サポートが含まれるようになりました。 このサポートには次の型が含まれます。  
- **barchart**:最初の列は x 軸で、テキスト、日時、または数値を指定できます。 2 番目の列は数値である必要があり、水平方向のストリップとして表示されます。  
- **columnchart**:barchart と同様に、水平方向のストリップの代わりに垂直方向のストリップが表示されます。  
- **piechart**:最初の列は色の軸、2 番目の列は数値です。  
- **timechart**:線グラフ。 最初の列は x 軸で、日時を指定する必要があります。 2 番目の列は y 軸です。  

#### <a name="example-bar-chart"></a>例: 横棒グラフ
次のクエリでは、最近使用されたアプリケーションを横棒グラフとしてレンダリングします。

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![CMPivot 横棒グラフの視覚エフェクトの例](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>例: 時間グラフ
時間グラフをレンダリングするには、新しい **bin()** 演算子を使用して、イベントを時間でグループ化します。 次のクエリでは、過去 7 日間にデバイスがいつ開始したかを示します。

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![CMPivot 時間グラフの視覚エフェクトの例](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>例: 円グラフ
次のクエリでは、すべての OS バージョンを円グラフで表示します。

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![CMPivot 円グラフの視覚エフェクトの例](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a> ハードウェア インベントリ
CMPivot を使用して、任意のハードウェア インベントリ クラスをクエリします。 これらのクラスには、ハードウェア インベントリに対して行ったカスタム拡張機能が含まれます。 CMPivot では、サイト データベースに格納されている最後のハードウェア インベントリ スキャンから、キャッシュされた結果をすぐに返します。 同時に、必要に応じていずれかのオンライン クライアントからのライブ データで結果を更新します。

結果テーブルまたはグラフ内のデータの色の彩度は、データがライブかキャッシュされたものかを示します。 たとえば、濃い青は、オンライン クライアントからのリアルタイム データです。 明るい青色は、キャッシュされたデータです。

#### <a name="example"></a>例

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![縦棒グラフの視覚エフェクトによる CMPivot インベントリ クエリの例](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>制限事項
- 次のハードウェア インベントリ エンティティはサポートされていません  
    - IP アドレスなどの配列プロパティ  
    - Real32/Real64 <!--example?-->  
    - 埋め込まれたオブジェクトのプロパティ <!--example?-->  
- インベントリ エンティティ名の先頭は文字である必要があります
- 同じ名前のインベントリ エンティティを作成して組み込みのエンティティを上書きすることはできません  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a> スカラー演算子
CMPivot には次のスカラー演算子が含まれます。  

> [!Note]  
> - LHS: 演算子の左側の文字列  
> - RHS: 演算子の右側の文字列  


|演算子|[説明]|例 (結果は true)|
|--------|-----------|---------------------|
|==|次の値と等しい|`"aBc" == "aBc"`|
|!=|次の値と等しくない|`"abc" != "ABC"`|
|like|LHS には RHS に対する一致が含まれています|`"FabriKam" like "%Brik%"`|
|!like|LHS には RHS に対する一致が含まれていません|`"Fabrikam" !like "%xyz%"`|
|次の値を含む|RHS は LHS のサブシーケンスとして出現します|`"FabriKam" contains "BRik"`|
|!contains|RHS は LHS の中に出現しません|`"Fabrikam" !contains "xyz"`|
|startswith|RHS は LHS の冒頭のサブシーケンスです|`"Fabrikam" startswith "fab"`|
|!startswith|RHS は LHS の冒頭のサブシーケンスではありません|`"Fabrikam" !startswith "kam"`|
|endswith|RHS は LHS の末尾のサブシーケンスです|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS は LHS の末尾のサブシーケンスではありません|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a> クエリの概要

CMPivot ウィンドウの下部にある **[クエリの概要]** タブを選択します。 ここに示される状態から、オフラインになっているクライアントを識別したり、発生する可能性のあるエラーのトラブルシューティングを行ったりできます。 [カウント] 列で値を選択して、その状態にある特定のデバイスの一覧を表示します。 

たとえば、障害状態のデバイスの数を選択します。 特定のエラー メッセージを参照し、これらのデバイスの一覧をエクスポートします。 特定のコマンドレットが認識されないエラーである場合は、エクスポートされたデバイスの一覧からコレクションを作成して、Windows PowerShell 更新プログラムをデプロイします。  

### <a name="cmpivot-audit-status-messages"></a>CMPivot 監査ステータス メッセージ

バージョン 1810 以降では、CMPivot を実行する場合、監査ステータス メッセージが **MessageID 40805** で作成されます。 **[監視]**  >  **[システム ステータス]**  >  **[ステータス メッセージ クエリ]** の順に移動することで、ステータス メッセージを表示できます。 **特定のユーザーのすべての監査ステータス メッセージ**、**特定のサイトに対するすべての監査ステータス メッセージ**を実行したり、独自のステータス メッセージ クエリを作成したりすることができます。

メッセージには、次の形式が使用されます。

MessageId 40805: ユーザー &lt;UserName> は、コレクション &lt;Collection-ID> でハッシュ &lt;Script-Hash> のスクリプト &lt;Script-Guid> を実行しました。

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 は、CMPivot のスクリプト GUID です。
- スクリプト ハッシュは、クライアントの scripts.log ファイルで確認できます。
- ハッシュがクライアントのスクリプト ストアに格納されていることも確認できます。 クライアントのファイル名は、&lt;Script-Guid>_&lt;Script-Hash> です。
    - ファイル名の例: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![CMPivot 監査ステータス メッセージのサンプル](media/cmpivot-audit-status-message.png)

## <a name="cmpivot-starting-in-version-1902"></a><a name="bkmk_cmpivot1902"></a> バージョン 1902 以降の CMPivot
<!--3610960-->
Configuration Manager バージョン 1902 以降、階層内の中央管理サイト (CAS) から CMPivot を実行できます。 まだ、プライマリ サイトでクライアントへの通信が処理されます。 中央管理サイトから CMPivot を実行するとき、高速メッセージ サブスクリプション チャネル経由でプライマリ サイトとの通信が行われます。 この通信では、サイト間の標準の SQL レプリケーションは利用されません。

SQL またはプロバイダーが同じマシン上にない場合や、SQL Always On 構成のケースではない場合、CAS で CMPivot を実行するには、追加のアクセス許可が必要になります。 これらのリモート構成では、CMPivot に "ダブル ホップ シナリオ" を使用できます。

このような "ダブル ホップ シナリオ" で CMPivot を CAS で動作するようにするには、制約付き委任を定義します。 この構成のセキュリティの影響を理解するには、[Kerberos の制約付き委任](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview)に関する記事を参照してください。 Kerberos は、マシン間のすべてのホップを処理する必要があります。<!--5746133--> CAS などと同じ位置に配置されている SQL や SMS プロバイダーなどのリモート構成が複数ある、または信頼できるフォレストが複数ある場合、アクセス許可の設定の組み合わせが必要になることがあります。 必要なステップは次のとおりです。

### <a name="cas-has-a-remote-sql-server"></a>CAS にリモート SQL Server がある

1. 各プライマリ サイトの SQL サーバーに移動します。
   1. CAS リモート SQL サーバーと CAS サイト サーバーを [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) グループに追加します。
   ![プライマリ サイトの SQL サーバー上の Configmgr_DviewAccess グループ](media/cmpivot-dviewaccess-group.png)
1. [Active Directory ユーザーとコンピューター] に移動します。
   1. プライマリ サイト サーバーごとに右クリックして **[プロパティ]** を選択します。
      1. [委任] タブで、3 つ目のオプションの **[指定されたサービスへの委任でのみこのコンピューターを信頼する]** を選択します。 
      1. **[Kerberos のみを使う]** を選びます。
      1. ポートとインスタンスと共に CAS の SQL サーバー サービスを追加します。
      1. これらの変更が会社のセキュリティ ポリシーに合致していることを確認します。
   1. CAS サイトでは、右クリックして **[プロパティ]** を選択します。
      1. [委任] タブで、3 つ目のオプションの **[指定されたサービスへの委任でのみこのコンピューターを信頼する]** を選択します。 
      1. **[Kerberos のみを使う]** を選びます。
      1. ポートとインスタンスと共に各プライマリ サイトの SQL サーバー サービスを追加します。
      1. これらの変更が会社のセキュリティ ポリシーに合致していることを確認します。

   ![ダブル ホップの CMPivot AD の委任の例](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CAS にリモート プロバイダーがある

1. 各プライマリ サイトの SQL サーバーに移動します。
   1. CAS プロバイダー マシン アカウントと CAS サイト サーバーを [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) グループに追加します。
1. [Active Directory ユーザーとコンピューター] に移動します。
   1. CAS プロバイダー マシンを選択し、右クリックして **[プロパティ]** を選択します。
      1. [委任] タブで、3 つ目のオプションの **[指定されたサービスへの委任でのみこのコンピューターを信頼する]** を選択します。 
      1. **[Kerberos のみを使う]** を選びます。
      1. ポートとインスタンスと共に各プライマリ サイトの SQL サーバー サービスを追加します。
      1. これらの変更が会社のセキュリティ ポリシーに合致していることを確認します。
   1. CAS サイト サーバーを選択し、右クリックして **[プロパティ]** を選択します。
      1. [委任] タブで、3 つ目のオプションの **[指定されたサービスへの委任でのみこのコンピューターを信頼する]** を選択します。 
      1. **[Kerberos のみを使う]** を選びます。
      1. ポートとインスタンスと共に各プライマリ サイトの SQL サーバー サービスを追加します。
      1. これらの変更が会社のセキュリティ ポリシーに合致していることを確認します。
1. CAS リモート プロバイダー マシンを再起動します。

### <a name="sql-always-on"></a>SQL Always On

1. 各プライマリ サイトの SQL サーバーに移動します。
   1. CAS サイト サーバーを [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) グループに追加します。
1. [Active Directory ユーザーとコンピューター] に移動します。
   1. プライマリ サイト サーバーごとに右クリックして **[プロパティ]** を選択します。
      1. [委任] タブで、3 つ目のオプションの **[指定されたサービスへの委任でのみこのコンピューターを信頼する]** を選択します。 
      1. **[Kerberos のみを使う]** を選びます。
      1. ポートとインスタンスと共に CAS の SQL ノードに対する SQL サーバー サービス アカウントを追加します。
      1. これらの変更が会社のセキュリティ ポリシーに合致していることを確認します。
   1. CAS サイト サーバーを選択し、右クリックして **[プロパティ]** を選択します。
      1. [委任] タブで、3 つ目のオプションの **[指定されたサービスへの委任でのみこのコンピューターを信頼する]** を選択します。 
      1. **[Kerberos のみを使う]** を選びます。
      1. ポートとインスタンスと共に各プライマリ サイトの SQL サーバー サービスを追加します。
      1. これらの変更が会社のセキュリティ ポリシーに合致していることを確認します。
1. [SPN が CAS SQL リスナー名と各プライマリ SQL リスナー名に公開されている](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs)ことを確認します。
1. プライマリ SQL サーバーを再起動します。
1. CAS サイト サーバーと CAS SQL サーバーを再起動します。

## <a name="cmpivot-starting-in-version-1906"></a><a name="bkmk_cmpivot1906"></a> バージョン 1906 以降の CMPivot

バージョン 1906 以降では、CMPivot に次の項目が追加されています。

- [結合、追加の演算子、およびアグリゲーター](#bkmk_cmpivot_joins)
- [セキュリティ管理者ロールに追加された CMPivot のアクセス許可](#bkmk_cmpivot_secadmin1906)
- [CMPivot スタンドアロン](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a> CMPivot で結合、追加の演算子、およびアグリゲーターを追加する
<!--4054074-->
追加の算術演算子とアグリゲーターを使用できるようになりました。また、レジストリとファイルの併用など、クエリを結合する機能も追加されました。 次の項目が追加されています。

#### <a name="table-operators"></a>テーブル演算子

|テーブル演算子| [説明]|
|-----|-----|
| [join](https://docs.microsoft.com/azure/kusto/query/joinoperator)| 同じデバイスの行を照合して、2 つのテーブルの行をマージして新しいテーブルを形成します|
|render|結果をグラフィカル出力としてレンダリングします|

render 演算子は、CMPivot に既に存在します。 複数の系列と **with** ステートメントのサポートが追加されました。 詳細については、「[例](#bkmk_cmpivot_examples1906)」セクションと Kusto の「[join operator](https://docs.microsoft.com/azure/kusto/query/joinoperator)」(join 演算子) を参照してください。

#### <a name="limitations-for-joins"></a>結合の制限事項

1. 結合列は**デバイス** フィールドで常に暗黙的に行われます。
1. クエリあたり最大 5 つの結合を使用できます。
1. 最大 64 の結合列を使用することができます。

#### <a name="scalar-operators"></a>スカラー演算子

|演算子| [説明]|例|
|-----|-----|-----|
| + | 追加| `2 + 1, now() + 1d`|
| - |  減算| `2 - 1, now() - 1d`|
| * | 乗算| `2 * 2`|
| / | 除算 | `2 / 1`|
| % | 剰余 | `2 % 1`

#### <a name="aggregation-functions"></a>集計関数

|関数| [説明]|
|-----|-----|
| percentile()| 式で定義された母集団の指定したランクに最も近いパーセンタイルの推定値を返します|
| sumif() | 述語が True に評価される式の合計を返します|

#### <a name="scalar-functions"></a>スカラー関数

|関数| [説明]|
|-----|-----|
| case()| 述語の一覧を評価し、その述語を満たす最初の結果式を返します |
| iff() | 最初の引数を評価し、述語が true または false に評価されるかどうかに応じて、2 番目 (true) または 3 番目 (false) の引数の値を返します|
 | indexof() | 関数は、入力文字列内で指定された文字列の最初の出現の 0 から始まるインデックスを報告します|
| strcat() | 1 から 64 の引数を連結します |
| strlen()| 入力文字列の文字の長さを返します|
| substring() | いくつかのインデックスから始まり文字列で終わるソース文字列からサブ文字列を抽出します |
| tostring() | 入力を文字列操作に変換します |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a> 例

- デバイス、製造元、モデル、および OSVersion を示します。

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- デバイスのブート時間のグラフを示します。

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![デバイスのブート時間をミリ秒単位で示す積み上げ横棒グラフ](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a>セキュリティ管理者ロールに追加された CMPivot のアクセス許可
<!--4683130-->

バージョン 1906 以降では、次のアクセス許可が、Configuration Manager の組み込みの**セキュリティ管理者**ロールに追加されています。

 - SMS スクリプトに対する**読み取り**
 - コレクションに対する **CMPivot の実行**
 - インベントリ レポートに対する**読み取り**

>[!NOTE]
> **スクリプトの実行**は、**CMPivot の実行**アクセス許可のスーパーセットです。
 

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot スタンドアロン
<!--3555890, 4619340, 4683130 -->

バージョン 1906 以降では、CMPivot をスタンドアロン アプリとして使用できます。 CMPivot スタンドアロンは、英語でのみ利用できます。 CMPivot を Configuration Manager コンソールの外で実行して、環境内にあるデバイスの状態をリアルタイムで表示することができます。 この変更により、最初にコンソールをインストールしなくてもデバイスで CMPivot を使用できます。

> [!Tip]  
> この機能はバージョン 1906 で[プレリリース機能](pre-release-features.md)として初めて導入されました。 バージョン 2002 以降、プレリリース機能ではなくなりました。  

CMPivot の機能を、ヘルプデスクやセキュリティ管理者など、コンソールをコンピューターにインストールしていない他のユーザーと共有できます。 他のユーザーは今まで使用していた他のツールと共に CMPivot を使用し、Configuration Manager にクエリを実行できます。 この充実した管理データを共有することで、職務をまたぐビジネス上の問題を同僚と共に事前解決できます。

#### <a name="install-cmpivot-standalone"></a>CMPivot スタンドアロンのインストール

1. CMPivot の実行に必要なアクセス許可を設定します。 詳細については、「[前提条件](#prerequisites)」を参照してください。 [セキュリティ管理者のロール](#bkmk_cmpivot_secadmin1906)がユーザーに適している場合、そのアクセス許可を使用することもできます。
2. CMPivot アプリのインストーラは、`<site install path>\tools\CMPivot\CMPivot.msi`にあります。 アプリはこのパスから実行するか、別の場所にコピーできます。
3. CMPivot スタンドアロン アプリを実行すると、サイトに接続するように求められます。 中央管理サイトまたはプライマリ サイトのサーバーの完全修飾ドメイン名またはコンピューター名を指定します。
   - CMPivot スタンドアロンを開くたびにサイト サーバーに接続するように求められます。
4. CMPivot を実行するコレクションを参照して、クエリを実行します。

   ![クエリを実行するコレクションを参照します。](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> アクションを右クリックします。**スクリプトの実行**、**リソース エクスプローラー**、Web 検索などは、CMPivot スタンドアロンでは使用できません。 CMPivot スタンドアロンの主な用途は、Configuration Manager インフラストラクチャとは別にクエリを実行することです。 セキュリティ管理者を支援するために、CMpivot スタンドアロンには Microsoft Defender Security Center に接続する機能が含まれています。 <!--5605358-->

## <a name="cmpivot-starting-in-version-1910"></a><a name="bkmk_cmpivot1910"></a> バージョン 1910 以降の CMPivot
<!--5410930, 3197353-->
バージョン 1910 以降では、サーバーへのネットワーク トラフィックと負荷を軽減するために、CMPivot が大幅に最適化されています。 さらに、トラブルシューティングや探索を支援するために、さまざまなエンティティとエンティティ拡張機能が追加されています。 バージョン 1910 の CMPivot では、次の変更が導入されました。

- [CMPivot エンジンに対する最適化](#bkmk_optimization)
- 追加のエンティティとエンティティ拡張機能:
  - Windows イベント ログ ([WinEvent](#bkmk_WinEvent))
  - ファイルの内容 ([FileContent](#bkmk_File))
  - プロセスによって読み込まれた dll ([ProcessModule](#bkmk_ProcessModule))
  - Azure Active Directory 情報 ([AADStatus](#bkmk_AadStatus))
  - エンドポイント保護の状態 ([EPStatus](#bkmk_EPStatus))
- [CMPivot スタンドアロンを使用したローカル デバイスのクエリ評価](#bkmk_local-eval)
- [CMPivot のその他の拡張機能](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a> CMPivot エンジンに対する最適化
<!--3197353-->
サーバーのネットワーク トラフィックと負荷を軽減するために、CMPivot は 1910 の時点で最適化されました。 多くのクエリ操作が、サーバーではなくクライアントで直接実行されるようになりました。 また、この変更により、一部の CMPivot 操作で最初のクエリから最小限のデータが返されるようになりました。 データの詳細についてドリルダウンする場合は、新しいクエリを実行して、クライアントから追加のデータをフェッチできます。 たとえば、"集計カウント" クエリを実行すると、以前は大規模なデータ セットがサーバーに返されていました。  大規模なデータ セットが返されるので即時にドリルダウンできましたが、多くの場合、必要なのは集計カウントだけでした。 1910 では、特定のクライアントにドリルダウンするよう選択すると、別のデータのコレクションが作成されて、要求した追加のデータが返されます。 この変更により、多数のクライアントに対するクエリのパフォーマンスとスケーラビリティが向上します。 <!--3197353, 5458337-->

#### <a name="examples"></a>例

CMPivot の最適化によって、CMPivot クエリの実行に必要なネットワークとサーバーの CPU 負荷が大幅に軽減されます。 これらの最適化を利用して、数ギガバイトのクライアント データをリアルタイムで処理できるようになりました。 次のクエリは、これらの最適化を示しています。

- 企業内のすべてのクライアントのすべてのイベント ログで認証エラーを検索します。

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- ハッシュを使用してファイルを検索します。

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent(\<ログ名>,[\<期間>])

このエンティティは、イベント ログおよびイベント トレーシング ログ ファイルからイベントを取得するために使用します。 このエンティティを使って、Windows イベント ログ テクノロジによって生成されたイベント ログからデータを取得できます。 また、このエンティティを使って、Windows イベント トレーシング (ETW) によって生成されたログ ファイル内のイベントも取得できます。 WinEvent では、既定で、過去 24 時間以内に発生したイベントが調べられます。 ただし、24 時間の既定値は、期間を含めることによってオーバーライドできます。

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> FileContent(\<ファイル名>)

FileContent は、テキスト ファイルの内容を取得するために使用します。

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule(\<プロセス名>)  

このエンティティは、指定したプロセスによって読み込まれたモジュール (dll) を列挙するために使用します。 ProcessModule は、正当なプロセス内に隠されたマルウェアを探索するときに便利です。  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a> AadStatus

このエンティティは、デバイスから現在の Azure Active Directory の ID 情報を取得するために使用できます。

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a> EPStatus

EPStatus は、コンピューターにインストールされているマルウェア対策ソフトウェアの状態を取得するために使用します。

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a> CMPivot スタンドアロンを使用したローカル デバイスのクエリ評価
<!--3197353-->
Configuration Manager コンソールの外部で CMPivot を使用する場合は、Configuration Manager インフラストラクチャを必要とせずに、ローカル デバイスだけにクエリを実行できます。 CMPivot Azure Log Analytics のクエリを利用して、ローカル デバイスに関する WMI 情報をすばやく表示できるようになりました。 これにより、大規模な環境内で実行する前に、CMPivot クエリの検証と改良を行うこともできます。 CMPivot スタンドアロンは、英語でのみ利用できます。 CMPivot スタンドアロンのインストールの詳細については、[CMPivot スタンドアロンのインストール](#install-cmpivot-standalone)に関するページをご覧ください。

#### <a name="known-issues-for-local-device-query-evaluation"></a>ローカル デバイスのクエリ評価に関する既知の問題

 - **この PC** で、ロックされた WMI クラスなど、アクセス権のない WMI エンティティに対してクエリを実行すると、CMPivot がクラッシュする可能性があります。 管理者特権を持つアカウントを使用して CMPivot を実行し、これらのエンティティに対してクエリを実行します。 <!--5753242-->
- **この PC**  で、非 WMI エンティティに対してクエリを実行すると、**無効な名前空間**またはあいまいな例外が発生します。
- 実行可能ファイルのパスから直接ではなく、[スタート] メニューのショートカットから CMPivot スタンドアロンを実行します。 <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> その他の機能強化

- 新しい `like` 演算子を使用して、正規表現の型のクエリを実行できます。 次に例を示します。<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- **CcmLog()** および **EventLog()** エンティティが更新され、既定で過去 24 時間以内のメッセージのみが調べられるようになりました。 この動作は、省略可能な期間を渡すことによってオーバーライドできます。 たとえば、次のクエリでは、過去 1 時間のイベントを確認します。

   ```kusto
   CcmLog('Scripts',1h)
   ```

- **File()** エンティティが更新され、隠しファイルとシステム ファイルに関する情報が収集され、MD5 ハッシュが含められるようになりました。 MD5 ハッシュは、SHA256 ハッシュほど正確ではありませんが、ほとんどのマルウェア情報で一般的に報告されるハッシュとなる傾向があります。  

- クエリにコメントを追加できます。<!-- 5431463 --> この動作は、クエリを共有する場合に便利です。 次に例を示します。

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot は最後のサイトに自動的に接続されます。<!-- 5420395 --> CMPivot を起動した後、必要に応じて新しいサイトに接続できます。

- **[エクスポート]** メニューから、 **[Query link to clipboard]\(クリップボードへのクエリ リンク\)** を行うための新しいオプションを選択できます。<!-- 5431577 --> このアクションによってリンクがクリップボードにコピーされ、他のユーザーと共有できます。 次に例を示します。

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    このリンクを使用すると、CMPivot スタンドアロンが開き、次のクエリが表示されます。

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > このリンクを動作させるには、[CMPivot スタンドアロンをインストール](#install-cmpivot-standalone)してください。

- クエリ結果で、デバイスが Microsoft Defender Advanced Threat Protection (ATP) に登録されている場合、デバイスを右クリックして **[Microsoft Defender セキュリティ センター]** のオンライン ポータルを起動することができます。

### <a name="known-issues-for-cmpivot-in-version-1910"></a>バージョン 1910 の CMPivot に関する既知の問題

- 結果の最大件数が上限に達すると、最大件数バナーが表示されない場合があります。 <!--5431427-->
  - 各クライアントは、クエリごとに 128 KB 相当のデータに制限されています。
  - クエリの結果が 128 KB を超えると、結果が切り捨てられる場合があります。
  
## <a name="cmpivot-starting-in-version-2002"></a><a name="bkmk_2002"></a> バージョン 2002 以降の CMPivot
<!--5870934-->
CMPivot エンティティの移動が容易になりました。 Configuration Manager バージョン 2002 以降では、CMPivot エンティティを検索できます。 エンティティとエンティティ オブジェクトの種類を簡単に区別できるように、新しいアイコンも追加されました。

![CMPivot エンティティの検索](./media/5870934-search-cmpivot-entities.png)

 
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
 
[CMPivot のトラブルシューティング](cmpivot-tsg.md)

[PowerShell スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)


