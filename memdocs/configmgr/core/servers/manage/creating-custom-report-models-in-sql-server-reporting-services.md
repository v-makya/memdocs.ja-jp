---
title: カスタム レポートの作成
titleSuffix: Configuration Manager
description: ビジネス要件に適したレポート モデルを定義し、レポート モデルを Configuration Manager に展開します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: fe570eeedc2c050bdaf27903d30ddffff63109d9
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879160"
---
# <a name="creating-custom-report-models-for-configuration-manager-in-sql-server-reporting-services"></a>SQL Server Reporting Services での Configuration Manager のカスタム レポート モデルの作成

*適用対象:Configuration Manager (Current Branch)*

サンプルのレポート モデルは Configuration Manager に含まれていますが、それぞれの業務要件に適したレポート モデルを定義し、そのレポート モデルを Configuration Manager に展開して、新しいモデルベースのレポートの作成時に使用できます。 次の表に、基本レポート モデルを作成して展開するための手順を示します。  

> [!NOTE]  
>  詳細なレポート モデルを作成する手順については、このトピックの「 [SQL Server Reporting Services で詳細レポート モデルを作成する手順](#AdvancedReportModel) 」セクションを参照してください。  

|手順|[説明]|説明|  
|----------|-----------------|----------------------|  
|SQL Server Business Intelligence Development Studio がインストールされていることを確認する|レポート モデルの設計と作成には、SQL Server Business Intelligence Development Studio を使用します。 カスタム レポート モデルを作成するコンピューターに、SQL Server Business Intelligence Development Studio がインストールされていることを確認します。|SQL Server Business Intelligence Development Studio の詳細については、SQL Server 2008 のドキュメントを参照してください。|  
|レポート モデル プロジェクトを作成する|レポート モデル プロジェクトには、データ ソースの定義 (.ds ファイル)、データ ソース ビューの定義 (.dsv ファイル)、およびレポート モデル (.smdl ファイル) が含まれます。|詳細については、このトピックの「 [レポート モデル プロジェクトを作成するには](#BKMK_CreateReportModelProject) 」セクションを参照してください。|  
|レポート モデルのデータ ソースを定義する|レポート モデル プロジェクトを作成したら、ビジネス データの抽出元のデータ ソースを定義する必要があります。 通常、これは Configuration Manager サイト データベースです。|詳細については、このトピックの「 [レポート モデル用のデータ ソースを定義するには](#BKMK_DefineReportModelDataSource) 」セクションを参照してください。|  
|レポート モデルのデータ ソース ビューを定義する|レポート モデル プロジェクトで使用するデータ ソースを定義したら、次の手順で、プロジェクトのデータ ソース ビューを定義します。 データ ソース ビューは、1 つまたは複数のデータ ソースを基にした論理データ モデルです。 データ ソース ビューは、テーブルやビューなど、基盤となるデータ ソースに含まれる物理オブジェクトへのアクセスをカプセル化します。 SQL Server Reporting Services は、レポート モデルをデータ ソース ビューから生成します。<br /><br /> データ ソース ビューにより、指定したデータが分かりやすく表示されるため、モデルの設計プロセスが容易になります。 データ ソース ビュー内では、基盤となるデータ ソースを変更することなく、テーブルおよびフィールドの名前を変更したり、集計フィールドや派生テーブルを追加したりできます。 効率的なモデルを作成するには、使用するテーブルのみをデータ ソース ビューに追加します。|詳細については、このトピックの「 [レポート モデル用のデータ ソース ビューを定義するには](#BKMK_DefineReportModelDataSourceView) 」セクションを参照してください。|  
|レポート モデルを作成する|レポート モデルはデータベースの最上部に位置するレイヤーであり、ビジネスのエンティティ、フィールドおよび役割を定義します。 モデルが公開されると、レポート ビルダーを使用してレポートを作成できるようになります。その際、データベース構造やクエリに関する知識は不要で、クエリを作成する必要もありません。 モデルは、フレンドリ名でグループ化されている一連の関連レポート項目で構成されており、これらのビジネス項目間の関係や計算が定義されています。 モデルは、セマンティック モデル定義言語 (SMDL) と呼ばれる XML 言語を使用して定義されます。 レポート モデルのファイル名拡張子は .smdl です。|詳細については、このトピックの「 [レポート モデルを作成するには](#BKMK_CreateReportModel) 」セクションを参照してください。|  
|レポート モデルを発行する|作成したモデルを使用してレポートを構築するには、このモデルをレポート サーバーにパブリッシュする必要があります。 公開時には、データ ソースおよびデータ ソース ビューがモデルに含まれます。|詳細については、このトピックの「 [SQL Reporting Services 用にレポート モデルを公開するには](#BKMK_PublishReportModel) 」セクションを参照してください。|  
|レポート モデルを Configuration Manager に展開する|**レポートの作成ウィザード** で、カスタム レポート モデルを使用してモデル ベースのレポートを作成するには、先に Configuration Manager にレポート モデルを展開しておく必要があります。|詳細については、このトピックの「 [カスタム レポート モデルを Configuration Manager に展開するには](#BKMK_DeployReportModel) 」セクションを参照してください。|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>SQL Server Reporting Services で基本レポート モデルを作成する手順  
 以下の手順に従って、サイト内のユーザーが Configuration Manager データベースの単一のビューのデータに基づいて、特定のモデルベースのレポートを作成する際に使用できる基本レポート モデルを作成できます。 サイト内のクライアント コンピューターに関する情報をレポートの作成者に示す、レポート モデルを作成します。 この情報は、Configuration Manager データベースの **[v_R_System]** ビューから取得します。  

 これらの手順を実行するコンピューターに SQL Server Business Intelligence Development がインストールされていること、また、このコンピューターからネットワーク接続を介してレポート サービス ポイント サーバーにアクセスできることを確認します。 SQL Server Business Intelligence Development Studio の詳細については、SQL Server 2008 のドキュメントを参照してください。  

###  <a name="to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a> レポート モデルを作成するには  

1.  デスクトップで、 **[スタート]** 、 **[Microsoft SQL Server 2008]** 、 **[SQL Server Business Intelligence Development Studio]** の順にクリックします。  

2.  **[SQL Server Business Intelligence Development Studio]** を Microsoft Visual Studio で開いてから、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。  

3.  **[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** リストで **[レポート モデル プロジェクト]** を選択します。  

4.  **[名前]** ボックスに、このレポート モデルの名前を指定します。 この例では、「 **Simple_Model**」と入力します。  

5.  レポート モデル プロジェクトを作成するには、 **[OK]** をクリックします。  

6.  **Simple_Model** ソリューションが **[ソリューション エクスプローラー]** に表示されます。  

    > [!NOTE]  
    >  **[ソリューション エクスプローラー]** ウィンドウが表示されない場合は、 **[表示]** 、 **[ソリューション エクスプローラー]** の順にクリックします。  

###  <a name="to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a> レポート モデル用のデータ ソースを定義するには  

1.  **SQL Server Business Intelligence Development Studio** の **[ソリューション エクスプローラー]** ウィンドウで **[データ ソース]** を右クリックし、 **[新しいデータ ソースの追加]** を選択します。  

2.  **[データ ソース ウィザードへようこそ]** ページで **[次へ]** をクリックします。  

3.  **[接続の定義方法を選択します]** ページで **[既存の接続または新しい接続に基づいてデータ ソースを作成する]** が選択されていることを確認し、 **[新規作成]** をクリックします。  

4.  **[接続マネージャー]** ダイアログ ボックスで、データ ソースの次の接続プロパティを指定します。  

    -   **サーバー名**:Configuration Manager サイト データベース サーバーの名前を入力するか、一覧から選択します。 既定のインスタンスではなく、名前が付けられたインスタンスを使用している場合、&lt;*データベース サーバー*>\\&lt;*インスタンス名*> の形式で入力します。  

    -   **[Windows 認証を使用する]** を選択します。  

    -   **[データベース名の選択または入力]** リストで、Configuration Manager サイト データベースの名前を選択します。  

5.  データベース接続が正常に確立されたことを確認するには、 **[接続テスト]** をクリックします。  

6.  接続が正常に確立されたら、 **[OK]** をクリックして **[接続マネージャー]** ダイアログ ボックスを閉じます。 接続が正常に確立されない場合は、入力した情報が正しいことを確認して、 **[接続テスト]** を再度クリックします。  

7.  **[接続の定義方法を選択します]** ページで、 **[既存の接続または新しい接続に基づいてデータ ソースを作成する]** が選択されていて、直前に指定したデータ ソースが **[データ接続]** ボックスで選択された状態になっていることを確認し、 **[次へ]** をクリックします。  

8.  **[データ ソース名]** にデータ ソースの名前を指定し、 **[完了]** をクリックします。 この例では、「 **Simple_Model**」と入力します。  

9. これで、 **[ソリューション エクスプローラー]** の **[データ ソース]** ノードの下に、データ ソース **Simple_Model.ds** が表示されます。  

    > [!NOTE]  
    >  既存のデータ ソースのプロパティを編集するには、 **[ソリューション エクスプローラー]** ウィンドウの **[データ ソース]** フォルダーでデータ ソースをダブルクリックし、データ ソースのプロパティをデータ ソース デザイナーに表示します。  

###  <a name="to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a> レポート モデル用のデータ ソース ビューを定義するには  

1.  **[ソリューション エクスプローラー]** で **[データ ソース ビュー]** を右クリックし、 **[新しいデータ ソース ビューの追加]** を選択します。  

2.  **[データ ソース ビュー ウィザードへようこそ]** ページで **[次へ]** をクリックします。 **[データ ソースの選択]** ページが表示されます。  

3.  **[リレーショナル データ ソース]** ウィンドウで、 **[Simple_Model]** データ ソースが選択されていることを確認し、 **[次へ]** をクリックします。  

4.  **[テーブルとビューの選択]** ページの **[使用可能なオブジェクト]** リストで、レポート モデルで使用するビュー **[v_R_System (dbo)]** を選択します。  

    > [!TIP]  
    >  **[使用可能なオブジェクト]** リストでビューを見つけやすいように、リスト上部の見出しで **[名前]** をクリックして、オブジェクトをアルファベット順に並べ替えます。  

5.  ビューを選択した後、 **>** をクリックして、オブジェクトを **[含まれるオブジェクト]** を選択します。  

6.  **[名前の一致]** ページが表示された場合、既定値をそのまま使用し、 **[次へ]** をクリックします。  

7.  必要なオブジェクトを選択したら、 **[次へ]** をクリックして、データ ソース ビューの名前を指定します。 この例では、「 **Simple_Model**」と入力します。  

8.  **[Finish]** をクリックします。 **Simple_Model.dsv** データ ソース ビューが、 **[ソリューション エクスプローラー]** の **[データ ソース ビュー]** フォルダーに表示されます。  

###  <a name="to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a> To create the report model  

1.  **[ソリューション エクスプローラー]** で **[レポート モデル]** を右クリックし、 **[新しいレポート モデルの追加]** を選択します。  

2.  **[レポート モデル ウィザードへようこそ]** ページで **[次へ]** をクリックします。  

3.  **[データ ソース ビューの選択]** ページの **[使用可能なデータ ソース ビュー]** リストでデータ ソース ビューを選択し、 **[次へ]** をクリックします。 この例では、 **[Simple_Model.dsv]** を選択します。  

4.  **[レポート モデル生成ルールの選択]** ページで既定値をそのまま使用し、 **[次へ]** をクリックします。  

5.  **[モデルの統計の収集]** ページで **[生成の前にモデルの統計を更新する]** が選択されていることを確認し、 **[次へ]** をクリックします。  

6.  **[ウィザードの完了]** ページで、レポート モデルの名前を指定します。 この例では、 **「Simple_Model」**  と表示されていることを確認します。  

7.  ウィザードを完了してレポート モデルを作成するには、 **[実行]** をクリックします。  

8.  ウィザードを終了するには、 **[完了]** をクリックします。 レポート モデルがデザイン ウィンドウに表示されます。  

###  <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> SQL Reporting Services 用にレポート モデルを公開するには  

1.  **[ソリューション エクスプローラー]** で、レポート モデルを右クリックして、 **[展開]** を選択します。 この例では、「 **Simple_Model** 」というレポート モデルを使用します。  

2.  **[SQL Server Business Intelligence Development Studio]** ウィンドウの左下隅で展開ステータスを確認します。 展開が完了したら、 **[配置正常終了]** と表示されます。 展開に失敗すると、 **[出力]** ウィンドウに失敗の原因が表示されます。 これで新しいレポート モデルが SQL Server Reporting Services の Web サイトから使用可能になります。  

3.  **[ファイル]** 、 **[すべて保存]** の順にクリックして、 **SQL Server Business Intelligence Development Studio**を閉じます。  

###  <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1. レポート モデル プロジェクトを作成したフォルダーを検索します。 例: *USERPROFILE*%\Documents\Visual Studio 2008\Projects\\ *&lt;プロジェクト名\>*  

2. レポート モデル プロジェクト ファルダから次のファイルを、コンピューター上の一時ファルダにコピーします。  

   -   *&lt;モデル名\>* **.dsv**  

   -   *&lt;モデル名\>* **.smdl**  

3. メモ帳などのテキスト エディターを使用して前のファイルを開きます。  

4. _&lt;モデル名\>_ **.dsv** というファイルで、次のように記述された最初の行を見つけます。  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    この行を次のように編集します。  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`  

5. ファイルの内容をすべてを Windows クリップボードにコピーします。  

6. ファイル _&lt;モデル名\>_ **.dsv** を閉じます。  

7. _&lt;モデル名\>_ **.smdl** というファイルで、次のように記述された最後の 3 行を見つけます。  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. ファイル _&lt;モデル名\>_ **.dsv** の内容を、ファイルの最後の行 ( **&lt;SemanticModel\>** ) の直前に貼り付けます。  

9. ファイル _&lt;モデル名\>_ **.smdl** を保存して閉じます。  

10. ファイル _&lt;モデル名\>_ **.smdl** を、Configuration Manager サイト サーバー上の フォルダー *%programfiles%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other にコピーします。  

    > [!IMPORTANT]  
    >  レポート モデル ファイルを Configuration Manager サイト サーバーにコピーした後は、まず Configuration Manager コンソールを終了し再起動しないと、**レポートの作成ウィザード**でレポート モデルを使用できません。  

##  <a name="steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> SQL Server Reporting Services で詳細レポート モデルを作成する手順  
 以下の手順に従って、サイト内のユーザーが Configuration Manager データベースの複数のビューのデータに基づいて、特定のモデルベースのレポートを作成する際に使用できる詳細レポート モデルを作成できます。 クライアント コンピューターとそれらのコンピューターにインストールされているオペレーティング システムに関する情報をレポート作成者に示す、レポート モデルを作成します。 この情報は、Configuration Manager データベースの次のビューから取得します。  

- **V_R_System**:検出されたコンピューターと構成マネージャー クライアントに関する情報が含まれています。  

- **V_GS_OPERATING_SYSTEM**:クライアント コンピューターにインストールされているオペレーティング システムに関する情報が含まれています。  

  前述のビューから選択した項目は 1 つのリストにまとめられ、フレンドリ名が与えられ、その後、特定のレポートに含めることができるようにレポート ビルダーでレポートの作成者に表示されます。  

  これらの手順を実行するコンピューターに SQL Server Business Intelligence Development がインストールされていること、また、このコンピューターからネットワーク接続を介してレポート サービス ポイント サーバーにアクセスできることを確認します。 SQL Server Business Intelligence Development Studio の詳細については、SQL Server のドキュメントを参照してください。  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  デスクトップで、 **[スタート]** 、 **[Microsoft SQL Server 2008]** 、 **[SQL Server Business Intelligence Development Studio]** の順にクリックします。  

2.  **[SQL Server Business Intelligence Development Studio]** を Microsoft Visual Studio で開いてから、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。  

3.  **[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** リストで **[レポート モデル プロジェクト]** を選択します。  

4.  **[名前]** ボックスに、このレポート モデルの名前を指定します。 この例では、「 **Advanced_Model**」と入力します。  

5.  レポート モデル プロジェクトを作成するには、 **[OK]** をクリックします。  

6.  **Advanced_Model** ソリューションが **[ソリューション エクスプローラー]** に表示されます。  

    > [!NOTE]  
    >  **[ソリューション エクスプローラー]** ウィンドウが表示されない場合は、 **[表示]** 、 **[ソリューション エクスプローラー]** の順にクリックします。  

#### <a name="to-define-the-data-source-for-the-report-model"></a>レポート モデル用のデータ ソースを定義するには  

1.  **SQL Server Business Intelligence Development Studio** の **[ソリューション エクスプローラー]** ウィンドウで **[データ ソース]** を右クリックし、 **[新しいデータ ソースの追加]** を選択します。  

2.  **[データ ソース ウィザードへようこそ]** ページで **[次へ]** をクリックします。  

3.  **[接続の定義方法を選択します]** ページで **[既存の接続または新しい接続に基づいてデータ ソースを作成する]** が選択されていることを確認し、 **[新規作成]** をクリックします。  

4.  **[接続マネージャー]** ダイアログ ボックスで、データ ソースの次の接続プロパティを指定します。  

    -   **サーバー名**:Configuration Manager サイト データベース サーバーの名前を入力するか、一覧から選択します。 既定のインスタンスではなく、名前が付けられたインスタンスを使用している場合、&lt;*データベース サーバー*>\\&lt;*インスタンス名*> の形式で入力します。  

    -   **[Windows 認証を使用する]** を選択します。  

    -   **[データベース名の選択または入力]** リストで、Configuration Manager サイト データベースの名前を選択します。  

5.  データベース接続が正常に確立されたことを確認するには、 **[接続テスト]** をクリックします。  

6.  接続が正常に確立されたら、 **[OK]** をクリックして **[接続マネージャー]** ダイアログ ボックスを閉じます。 接続が正常に確立されない場合は、入力した情報が正しいことを確認して、 **[接続テスト]** を再度クリックします。  

7.  **[接続の定義方法を選択します]** ページで、 **[既存の接続または新しい接続に基づいてデータ ソースを作成する]** が選択されていて、直前に指定したデータ ソースが **[データ接続]** リスト ボックスで選択された状態になっていることを確認し、 **[次へ]** をクリックします。  

8.  **[データ ソース名]** にデータ ソースの名前を指定し、 **[完了]** をクリックします。 この例では、「 **Advanced_Model**」と入力します。  

9. これで、 **[ソリューション エクスプローラー]** の **[データ ソース]** ノードの下に、データ ソース **Advanced_Model.ds** が表示されます。  

    > [!NOTE]  
    >  既存のデータ ソースのプロパティを編集するには、 **[ソリューション エクスプローラー]** ウィンドウの **[データ ソース]** フォルダーでデータ ソースをダブルクリックし、データ ソースのプロパティをデータ ソース デザイナーに表示します。  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>レポート モデル用のデータ ソース ビューを定義するには  

1. **[ソリューション エクスプローラー]** で **[データ ソース ビュー]** を右クリックし、 **[新しいデータ ソース ビューの追加]** を選択します。  

2. **[データ ソース ビュー ウィザードへようこそ]** ページで **[次へ]** をクリックします。 **[データ ソースの選択]** ページが表示されます。  

3. **[リレーショナル データ ソース]** ウィンドウで、 **[Advanced_Model]** データ ソースが選択されていることを確認し、 **[次へ]** をクリックします。  

4. **[テーブルとビューの選択]** ページの **[使用可能なオブジェクト]** リストで、レポート モデルで使用する以下のビューを選択します。  

   - **[[v_R_System (dbo)]]**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     各ビューを選択した後、 **>** をクリックして、オブジェクトを **[含まれるオブジェクト]** を選択します。  

   > [!TIP]  
   >  **[使用可能なオブジェクト]** リストでビューを見つけやすいように、リスト上部の見出しで **[名前]** をクリックして、オブジェクトをアルファベット順に並べ替えます。  

5. **[名前の一致]** ダイアログ ボックスが表示された場合、既定値をそのまま使用し、 **[次へ]** をクリックします。  

6. 必要なオブジェクトを選択したら、 **[次へ]** をクリックして、データ ソース ビューの名前を指定します。 この例では、「 **Advanced_Model**」と入力します。  

7. **[完了]** をクリックします。 **Advanced_Model.dsv** データ ソース ビューが、 **[ソリューション エクスプローラー]** の **[データ ソース ビュー]** フォルダーに表示されます。  

#### <a name="to-define-relationships-in-the-data-source-view"></a>データ ソース ビュー内の各関係を定義するには  

1.  **[ソリューション エクスプローラー]** で **Advanced_Model.dsv** をダブルクリックして、デザイン ウィンドウを開きます。  

2.  **[v_R_System]** ウィンドウのタイトル バーを右クリックし、 **[テーブルの置き換え]** を選択してから、 **[新しい名前付きクエリの使用]** をクリックします。  

3.  **[名前付きクエリの作成]** ダイアログ ボックスで、 **[テーブルの追加]** アイコンをクリックします (通常は、リボンの最後のアイコン)。  

4.  **[テーブルの追加]** ダイアログ ボックスで **[ビュー]** タブをクリックして、一覧から **[V_GS_OPERATING_SYSTEM]** を選択し、 **[追加]** をクリックします。  

5.  **[閉じる]** をクリックして **[テーブルの追加]** ダイアログ ボックスを閉じます。  

6.  **[名前付きクエリの作成]** ダイアログ ボックスで、次の項目を指定します。  

    -   **名前**:クエリの名前を指定します。 この例では、「 **Advanced_Model**」と入力します。  

    -   **説明:** クエリの説明を入力します。 この例では、「 **Reporting Services レポート モデルの例**」という説明を入力します。  

7.  **[v_R_System]** ウィンドウで、オブジェクトの一覧からレポート モデルに表示する以下の項目を選択します。  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  **[v_GS_OPERATING_SYSTEM]** ボックスで、オブジェクトの一覧からレポート モデルに表示する以下の項目を選択します。  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. これらのビューのオブジェクトを 1 つのリストとしてレポート作成者に表示するには、結合を使用して、2 つのリストまたはビューの関係を指定する必要があります。 両方のビューに表示されるオブジェクトの **ResourceID**を使って、2 つのビューを結合することができます。  

10. **[v_R_System]** ウィンドウで、 **ResourceID** オブジェクトをクリックしたまま **[v_GS_OPERATING_SYSTEM]** ウィンドウの **ResourceID** オブジェクトにドラッグします。  

11. **[OK]** をクリックします。  

12. **[v_R_System]** ウィンドウから **[Advanced_Model]** ウィンドウに切り替わり、このウィンドウに **v_R_System** および **v_GS_OPERATING_SYSTEM** ビューのレポート モデルに必要なオブジェクトがすべて含まれます。 これでデータ ソース ビュー デザイナーから **[v_GS_OPERATING_SYSTEM]** ウィンドウを削除することができます。 **[v_GS_OPERATING_SYSTEM]** ウィンドウのタイトル バーを右クリックして、 **[DSV からテーブルを削除]** を選択します。 **[オブジェクトの削除]** ダイアログ ボックスで、 **[OK]** をクリックして削除を確定します。  

13. **[ファイル]** をクリックして、 **[すべて保存]** をクリックします。  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  **[ソリューション エクスプローラー]** で **[レポート モデル]** を右クリックし、 **[新しいレポート モデルの追加]** を選択します。  

2.  **[レポート モデル ウィザードへようこそ]** ページで **[次へ]** をクリックします。  

3.  **[データ ソース ビューの選択]** ページの **[使用可能なデータ ソース ビュー]** リストでデータ ソース ビューを選択し、 **[次へ]** をクリックします。 この例では、 **[Simple_Model.dsv]** を選択します。  

4.  **[レポート モデル生成ルールの選択]** ページで既定値をそのまま使用し、 **[次へ]** をクリックします。  

5.  **[モデルの統計の収集]** ページで **[生成の前にモデルの統計を更新する]** が選択されていることを確認し、 **[次へ]** をクリックします。  

6.  **[ウィザードの完了]** ページで、レポート モデルの名前を指定します。 この例では、「 **Advanced_Model** 」と表示されていることを確認します。  

7.  ウィザードを完了してレポート モデルを作成するには、 **[実行]** をクリックします。  

8.  ウィザードを終了するには、 **[完了]** をクリックします。  

9. レポート モデルがデザイン ウィンドウに表示されます。  

#### <a name="to-modify-object-names-in-the-report-model"></a>レポート モデルのオブジェクト名を変更するには  

1.  **[ソリューション エクスプローラー]** で、レポート モデルを右クリックして、 **[ビュー デザイナー]** を選択します。 この例では、 **[Advanced_Model.smdl]** を選択します。  

2.  レポート モデル デザイン ビューで、オブジェクト名を右クリックして、 **[名前の変更]** をクリックします。  

3.  選択したオブジェクトの新しい名前を入力して、Enter キーを押します。 たとえば、オブジェクトを **Windows Service Pack のバージョン** が分かるように、オブジェクトを " **CSD_Version_0**" という名前に変更することができます。  

4.  オブジェクトの名前の変更が完了したら、 **[ファイル]** をクリックして **[すべて保存]** をクリックします。  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>SQL Reporting Services 用にレポート モデルを公開するには  

1.  **[ソリューション エクスプローラー]** で、 **Advanced_Model.smdl** を右クリックして、 **[展開]** を選択します。  

2.  **[SQL Server Business Intelligence Development Studio]** ウィンドウの左下隅で展開ステータスを確認します。 展開が完了したら、 **[配置正常終了]** と表示されます。 展開に失敗すると、 **[出力]** ウィンドウに失敗の原因が表示されます。 これで新しいレポート モデルが SQL Server Reporting Services の Web サイトから使用可能になります。  

3.  **[ファイル]** 、 **[すべて保存]** の順にクリックして、 **SQL Server Business Intelligence Development Studio**を閉じます。  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1. レポート モデル プロジェクトを作成したフォルダーを検索します。 例: *USERPROFILE*%\Documents\Visual Studio 2008\Projects\\ *&lt;プロジェクト名\>*  

2. レポート モデル プロジェクト ファルダから次のファイルを、コンピューター上の一時ファルダにコピーします。  

   -   *&lt;モデル名\>* **.dsv**  

   -   *&lt;モデル名\>* **.smdl**  

3. メモ帳などのテキスト エディターを使用して前のファイルを開きます。  

4. _&lt;モデル名\>_ **.dsv** というファイルで、次のように記述された最初の行を見つけます。  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    この行を次のように編集します。  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`

5. ファイルの内容をすべてを Windows クリップボードにコピーします。  

6. ファイル _&lt;モデル名\>_ **.dsv** を閉じます。  

7. _&lt;モデル名\>_ **.smdl** というファイルで、次のように記述された最後の 3 行を見つけます。  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. ファイル _&lt;モデル名\>_ **.dsv** の内容を、ファイルの最後の行 ( **&lt;SemanticModel\>** ) の直前に貼り付けます。  

9. ファイル _&lt;モデル名\>_ **.smdl** を保存して閉じます。  

10. ファイル _&lt;Model Name\>_ **.smdl** を、Configuration Manager サイト サーバー上のフォルダー *%programfiles%* \Microsoft Endpoint Manager\AdminConsole\XmlStorage\Other にコピーします。  

    > [!IMPORTANT]  
    >  レポート モデル ファイルを Configuration Manager サイト サーバーにコピーした後は、まず Configuration Manager コンソールを終了し再起動しないと、**レポートの作成ウィザード**でレポート モデルを使用できません。  
