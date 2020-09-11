---
title: レポートの概要
titleSuffix: Configuration Manager
description: Configuration Manager でレポートを管理する際に使用できるツールとリソースについて説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bfed31b820ac1f09b240122207b5bf27e432b10a
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607539"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Configuration Manager のレポートの概要

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のレポート機能には、SQL Server Reporting Services (SSRS) や Power BI Report Server の高度なレポート機能を利用する助けとなる一連のツールとリソースが用意されています。 どちらのレポート プラットフォームにも、カスタム レポートの充実したオーサリング エクスペリエンスが用意されています。 レポートは、組織内の豊富な Configuration Manager データに関する情報を収集して整理し、表示するのに役立ちます。 Configuration Manager には、変更せずに使用できる Reporting Services の定義済みレポートが、多数用意されています。 要件に合わせて既定のレポートを複製して変更することも、カスタム レポートを作成することもできます。

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services には、組織のためのレポートを作成、展開、管理するのに役立つ、すぐに使用できる幅広いツールとサービスが用意されています。 レポート機能の拡張とカスタマイズが可能になるプログラミング機能も用意されています。 Reporting Services は、さまざまな種類のデータ ソースに対して包括的なレポート機能を提供するサーバー ベースのレポート プラットフォームです。

Configuration Manager では、SQL Server Reporting Services をプライマリ レポート ソリューションとして使用します。 この Reporting Services との統合の利点は、次のとおりです。  

- Configuration Manager データベースのクエリに業界標準のレポート システムを使用できます。  

- Configuration Manager レポート ビューアー、または Web ベースでレポートに接続するレポート マネージャーを使用してレポートを表示できます。  

- 優れたパフォーマンス、可用性、およびスケーラビリティを実現します。  

- ユーザーが購読できるレポートに対するサブスクリプションを提供します。 たとえば管理者は、ソフトウェア更新プログラムのロールアウト状況の詳細が記載された、毎日メールで送信されるレポートを購読します。

- さまざまな種類のよく使われる形式でレポートをエクスポートします。  

詳細については、「[SQL Server Reporting Services (SSRS) について](/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports)」を参照してください。

## <a name="power-bi-report-server"></a>Power BI Report Server

<!-- 3721603 -->

バージョン 2002 以降では、Power BI Report Server を Configuration Manager レポートと統合します。 この統合により、最新の視覚化とパフォーマンスの向上が実現します。 SQL Server Reporting Services に既に存在するものと同様の Power BI レポートのコンソールのサポートが追加されます。 詳細については、「[Power BI Report Server との統合](powerbi-report-server.md)」を参照してください。

Power BI Report Server は、レポートを表示および管理する Web ポータルを備えたオンプレミスのレポート サーバーです。 これには、Power BI のレポート、ページ分割されたレポート、モバイル レポート、および KPI を作成するツールが含まれています。 詳細については、「[Power BI Report Server について](/power-bi/report-server/get-started)」を参照してください。

## <a name="reporting-services-point"></a>レポート サービス ポイント

レポート サービス ポイントは、Microsoft SQL Server Reporting Services を実行しているサーバーに追加するサイト システムの役割です。 レポート サービス ポイントでは、以下の機能が実行されます。

- Configuration Manager のレポート定義を Reporting Services にコピーします
- レポートのカテゴリに基づいてレポート フォルダーを作成します
- レポートのフォルダーおよびレポートに対してセキュリティ ポリシーを設定します。 これらのポリシーは、Configuration Manager 管理ユーザーのロール ベースのアクセス許可に基づいています。 10 分間隔で、レポート サービス ポイントが Reporting Services に接続し、変更した場合にはセキュリティ ポリシーを再度適用します。

レポート サービス ポイントの計画とインストールの詳細については、以下の記事を参照してください。

- [レポートの計画](planning-for-reporting.md)

- [レポートの構成](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Configuration Manager レポート

Configuration Manager では、50 を超えるレポート フォルダーに、400 を超えるレポート定義が用意されています。 それらは、レポート サービス ポイントのインストール プロセス中に、SQL Server Reporting Services のルート レポート フォルダーにコピーされます。 Configuration Manager コンソールでは、レポートが表示され、それらはレポートのカテゴリに基づくサブフォルダーに整理されます。

レポートは、Configuration Manager 階層の上下に伝達されません。 これらは、その中に作成したサイトのデータベースに対してのみ実行されます。 Configuration Manager では、グローバル データは階層全体にレプリケートされるため、レポート内で階層全体の情報にアクセスできます。 レポートがサイト データベースからデータを取得する際に、現在のサイトと子サイトのサイト データ、および階層内の全サイトのグローバル データにアクセスできます。

他の Configuration Manager オブジェクトと同様に、管理ユーザーがレポートの実行や変更を行うには適切なアクセス許可が必要となります。 レポートを実行するには、オブジェクトの **"レポートの実行"** アクセス許可が必要です。 レポートを作成するには、オブジェクトの **"レポートの変更"** アクセス許可が必要です。

### <a name="create-and-modify-reports"></a>レポートの作成と変更

Reporting Service ベースのレポートの場合、Configuration Manager では、モデル ベースと SQL ベースのレポートを対象に、専用のオーサリングおよび編集ツールとして Microsoft SQL Server レポート ビルダーが使用されます。 Configuration Manager コンソールでレポートの作成または編集を行うと、レポート ビルダーが開きます。 詳しくは、「[レポートの操作とメンテナンス](operations-and-maintenance-for-reporting.md)」を参照してください。

バージョン 2002 以降では、Power BI レポートの作成や編集のために、コンソールが Power BI Desktop と統合されます。 詳細については、「[Power BI レポートを作成する](powerbi-report-server.md#create-power-bi-reports)」を参照してください。

### <a name="run-reports"></a>レポートの実行

Configuration Manager コンソールで Reporting Services ベースのレポートを実行すると、レポート ビルダーが開き、Reporting Services に接続します。 レポートの必須パラメーターの指定後、Reporting Services がデータを取得してビューアーに結果を表示します。 また、SQL Services Reporting Services に接続し、サイトのデータ ソースにアクセスしてレポートを実行することもできます。

バージョン 2002 以降では、Power BI ベースのレポートを実行すると、Web ブラウザーで開かれます。

### <a name="report-prompts"></a>レポートのプロンプト

レポートを作成または変更するときに、レポートのプロンプトやパラメーターを構成できます。 レポートで取得するデータを制限したり指定したりするレポート プロンプトを作成します。 1 つのレポートに複数のプロンプトを含めることができます。 プロンプト名が一意で、識別子に関する SQL Server の規則に準拠する英数字のみが含まれるようにします。

レポートを実行すると、必要なパラメーターの値を要求するプロンプトが表示されます。 このパラメーター値に基づいて、レポート データが取得されます。 たとえば、**特定のコンピューターのコンピューター情報**というレポートでは、コンピューター名の入力が求められます。 Reporting Services は、指定された値を、レポートの SQL ステートメントで定義されている変数に渡します。

### <a name="report-links"></a>レポート リンク

Configuration Manager のレポート リンクは、追加データに簡単にアクセスできるように、ソース レポート内で使用されます。 たとえば、ソース レポート内の各項目に関する、より詳細な情報にリンクできます。 ターゲット レポートでプロンプトを実行する必要がある場合は、各プロンプトの適切な値の入った列をソース レポートに含める必要があります。

リンクでは、プロンプトのための値によって列番号を指定する必要があります。 次に例を示します。

- サイトで最近検出されたコンピューターを一覧表示する 1 つのレポートがあります。
- そこから、特定のコンピューターについてサイトが受信した最後のメッセージを一覧表示する別のレポートにリンクします。
- リンクを作成し、ソース レポートの列 `2` にコンピューター名が含まれることを指定します。 この値が、ターゲット レポートのために必要とされるプロンプトです。
- ソース レポートを実行すると、データの各行の左側にリンク アイコンが表示されます。
- 任意の行のアイコンを選択すると、その行の指定された列にある値が、ターゲット レポートのためのプロンプト値としてレポート ビューアーによって渡されます。

1 つのレポートに構成できるリンクは 1 つだけで、そのリンクからは、1 つのターゲット レポートにのみ接続できます。

> [!WARNING]  
> ターゲット レポートを別のレポート フォルダーに移動すると、ターゲット レポートの場所が変更されます。 Configuration Manager で、ソース レポート内のレポート リンクは、新しい場所によって自動的に更新されず、リンクはソース レポート内で機能しなくなります。

## <a name="report-folders"></a>レポート フォルダー

レポート フォルダーは、Configuration Manager が Reporting Services に格納しているレポートの並べ替えとフィルターの手段となります。 レポート フォルダーは、管理するレポートが多数ある場合に便利です。 レポート サービス ポイントをインストールすると、レポートは Reporting Services にコピーされて、50 以上のレポート フォルダーに整理されます。 レポート フォルダーは読み取り専用です。 それらは Configuration Manager コンソールで変更できません。

## <a name="report-subscriptions"></a>レポートのサブスクリプション

Reporting Services でのレポートのサブスクリプションは、特定の時点で、またはイベントへの応答としてレポートを配信することを求める定期的な要求です。 サブスクリプションでは、アプリケーション ファイル形式を指定します。 サブスクリプションは、オンデマンド レポート実行の代替手段となります。 オンデマンド レポートでは、レポートを表示するたびに手動でレポートを選択しなければなりません。 これと対照的に、サブスクリプションはスケジュールを設定して自動的にレポートを配信できます。

レポートのサブスクリプションは、Configuration Manager コンソールで管理できます。 レポート サーバーでは、サブスクリプションを処理します。 サーバーに展開されている配信拡張機能を使用して、それらの配布が行われます。 既定では、共有フォルダーまたは電子メール アドレスにレポートを送信するサブスクリプションを作成できます。

詳細については、「[レポートのサブスクリプションの管理](operations-and-maintenance-for-reporting.md#bkmk_subscription)」を参照してください。

## <a name="report-builder"></a>レポート ビルダー

Reporting Service ベースのレポートの場合、Configuration Manager では、モデル ベースのレポートと SQL ベースのレポートの両方を対象に、専用のオーサリングおよび編集ツールとして Microsoft SQL Server レポート ビルダーが使用されます。 Configuration Manager コンソールでレポートの作成または編集を行う場合、レポート ビルダーが開きます。 レポートの初回作成時または変更時に、自動的にレポート ビルダーがインストールされます。 レポートを実行または編集すると、インストールされているバージョンの SQL Server と関連付けられたバージョンの Report Builder が開きます。  

 レポート ビルダーのインストールにより、20 言語のサポートが追加されます。 レポート ビルダーを実行すると、ローカル コンピューターの OS の言語でデータが表示されます。 レポート ビルダーがその言語をサポートしていない場合、データは英語で表示されます。 レポート ビルダーは SQL Server Reporting Services の全機能をサポートしており、以下の機能が含まれています。

- Microsoft 365 Apps のような外観の直観的なレポート作成環境の提供  

- SQL Server レポート定義言語 (RDL) の柔軟なレポート レイアウト  

- チャートやゲージなど多様なデータ表示形式  

- リッチ形式のテキスト ボックス  

- Microsoft Word 形式のエクスポート  

レポート ビルダーは、SQL Server Reporting Services から直接開くこともできます。

## <a name="report-models-in-sql-server-reporting-services"></a>SQL Server Reporting Services のレポート モデル

SQL Reporting Services では、モデル ベースのレポートに含める項目を Configuration Manager データベースから選択する助けになるように、レポート モデルが使用されます。 レポートを作成するときには、選択対象となる指定したビューと項目のみが、レポート モデルに表示されます。 モデルベースのレポートを作成するには、少なくとも 1 つのレポート モデルが必要です。

レポート モデルには、次の特長があります。

- データベースのフィールドやビューに論理ビジネス名を付与します。 レポートを作成するために、Configuration Manager のデータベース構造に関する知識は必要ありません。

- 項目を論理的にグループ化します。  

- 項目間のリレーションシップを定義します。  

- 管理ユーザーに、表示するアクセス許可を持っているデータのみを表示できるように、モデルの要素をセキュリティで保護します。

Configuration Manager にはレポート モデルのサンプルが用意されていますが、それぞれの業務要件に適したレポート モデルを定義することもできます。 レポート モデルの作成方法の詳細については、[カスタム レポート モデルの作成](creating-custom-report-models-in-sql-server-reporting-services.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

[レポートの計画](planning-for-reporting.md)