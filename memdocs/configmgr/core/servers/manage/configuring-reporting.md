---
title: レポートの構成
titleSuffix: Configuration Manager
description: SQL Server Reporting Services に関する情報を含む、Configuration Manager 階層でのレポートのセットアップ方法。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ba67fee260867494302e49b7c9d3a97480e236b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708380"
---
# <a name="configure-reporting-in-configuration-manager"></a>Configuration Manager でのレポートの構成

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager コンソール内でレポートを作成、変更、実行するには、事前にいくつかの構成タスクを完了する必要があります。 この記事を使用すると、Configuration Manager 階層内でレポートを構成する場合に役立ちます。  

階層内での SQL Server Reporting Services のインストールおよび構成に進む前に、以下の Configuration Manager のレポートに関する記事をご確認ください。  

- [レポートの概要](introduction-to-reporting.md)  

- [レポートの計画](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services は、サーバー ベースのレポート プラットフォームであり、各種のデータ ソースに包括的なレポート機能を提供します。 Configuration Manager 内のレポート サービス ポイントでは、SQL Server Reporting Services と通信して、以下を行います。

- 指定されたレポート フォルダーへの Configuration Manager レポートのコピー
- Reporting Services 設定の構成
- Reporting Services のセキュリティ設定の構成

レポートを実行すると、Reporting Services コンポーネントは、データを取得するために Configuration Manager サイト データベースに接続されます。  

Configuration Manager サイトにレポート サービス ポイントをインストールする前に、ターゲットのサイト システムに SQL Server Reporting Services をインストールして構成します。 詳細については、「[SQL Server Reporting Services のインストール](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services)」をご覧ください。  

### <a name="verify-sql-server-reporting-services-installation"></a>SQL Server Reporting Services のインストール状態の検証

SQL Server Reporting Services がインストールされていて、正常に実行されているかどうかを確認するには、次の手順に従います。

1. サイト システム上で **[スタート]** メニューに移動し、 **[Reporting Services Configuration Manager]** を開きます。 これは、 **[Microsoft SQL Server]** グループの **[構成ツール]** セクションにあります。

2. **[Reporting Services 構成の接続]** ウィンドウで、SQL Server Reporting Services がホストされるサーバーの名前を入力します。 SQL Reporting Services をインストールした SQL Server のインスタンスを選択します。 次に、 **[接続]** を選択して Reporting Services Configuration Manager を開きます。  

3. **[レポート サーバーの状態]** ページで、 **[レポート サービスの状態]** が **[開始]** であることを確認します。 この状態になっていない場合は、 **[開始]** を選択します。  

4. **[Web サービス URL]** ページの **[レポート サービスの Web サービスの URL]** で、URL を選択します。 このアクションにより、レポート フォルダーへの接続がテストされます。 ブラウザーから資格情報の入力を求められる場合があります。 Web ページが正常に開くことを確認します。

5. **[データベース]** ページで、 **[レポート サーバー モード]** が **[ネイティブ]** に設定されていることを確認します。  

6. **[レポート マネージャー URL]** ページの **[レポート マネージャー サイトの識別情報]** で、URL を選択します。 このアクションにより、レポート マネージャー用の仮想ディレクトリへの接続がテストされます。 ブラウザーから資格情報の入力を求められる場合があります。 Web ページが正常に開くことを確認します。

    > [!NOTE]  
    > Configuration Manager のレポートでは、Reporting Services レポート マネージャーは必要ありません。 これは、ブラウザー内でレポートを実行する場合、またはレポート マネージャーを使用してレポートを管理する場合にのみ必要です。  

7. **[終了]** を選択して Reporting Services Configuration Manager を閉じます。  

## <a name="configure-reporting-to-use-report-builder-30"></a>レポートの操作にレポート ビルダー 3.0 を使用するように構成する

1. Configuration Manager コンソールを実行しているコンピューターで、Windows レジストリ エディターを開きます。  

2. を参照します。 `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting`

3. **ReportBuilderApplicationManifestName** キーを開いて、値データを編集します。  

4. 値を `ReportBuilder_3_0_0_0.application` に変更し、**OK** を選択して保存します。

5. Windows レジストリ エディターを閉じます。  

## <a name="install-a-reporting-services-point"></a>レポート サービス ポイントのインストール

サイトでレポートを管理するには、レポート サービス ポイントをインストールします。 レポート サービス ポイントでは、以下が行われます。

- レポート フォルダーとレポートを SQL Server Reporting Services にコピーする
- レポートとフォルダーにセキュリティ ポリシーを適用する
- Reporting Services の構成設定を設定する

### <a name="requirements-and-limitations"></a>要件と制限事項

Configuration Manager コンソール内でレポートを表示または管理するには、レポート サービス ポイントが必要です。 Microsoft SQL Server Reporting Services を使用して、サーバー上でこのサイト システムの役割を構成します。 詳しくは、[レポートの前提条件](prerequisites-for-reporting.md)に関する記事をご覧ください。  

- レポート サービス ポイントをインストールするサイトを選択するときは、レポートにアクセスすることになるユーザーが、役割のインストール先サイトと同じセキュリティ スコープにいる必要があります。  

- サイト システムにレポート サービス ポイントをインストールした後に、レポート サーバーの URL を変更しないでください。

    たとえば、レポート サービス ポイントを作成します。 次に、Reporting Services Configuration Manager 内でレポート サーバーの URL を変更します。 Configuration Manager コンソールでは古い URL の使用が継続されます。 コンソールからレポートを実行、編集、または作成することはできません。

    レポート サーバーの URL を変更する必要がある場合は、まず既存のレポート サービス ポイントを削除します。 URL を変更してから、レポート サービス ポイントを再インストールします。  

- レポート サービス ポイントをインストールするときに、[レポート サービス ポイント アカウント](../../plan-design/hierarchy/accounts.md#reporting-services-point-account)を指定します。 別のドメインのユーザーがレポートを実行できるようにするには、ドメイン間に双方向の信頼を作成します。 そうしないと、レポートの実行に失敗します。

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" /> サイト システムにレポート サービス ポイントをインストールする  

サイト システムの構成について詳しくは、「[サイト システムの役割のインストール](../deploy/configure/install-site-system-roles.md)」をご覧ください。  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サーバーとサイト システムの役割]** ノードを選択します。  

1. 新規または既存のサイト システム サーバーにレポート サービス ポイントを追加します。  

    - *新しいサイト システム*:リボンの **[ホーム]** タブにある **[作成]** グループで、 **[サイト システム サーバーの作成]** を選択します。 **サイト システム サーバーの作成ウィザード** が開きます。  

    - *既存のサイト システム*:ターゲット サーバーを選択します。 リボンの **[ホーム]** タブにある **[サーバー]** グループで、 **[サイト システムの役割の追加]** を選択します。 **サイト システムの役割の追加ウィザード**が開きます。  

1. **[全般]** ページで、サイト システム サーバーの全般設定を指定します。 レポート サービス ポイントを既存のサーバーに追加する場合は、以前に構成した値を確認します。  

1. **[システムの役割の選択]** ページの利用可能な役割の一覧で **[レポート サービス ポイント]** を選択し、 **[次へ]** を選択します。  

1. **[レポート サービス ポイント]** ページで、次の設定を構成します。  

    - **サイト データベース サーバー名**:Configuration Manager サイト データベースをホストするサーバーの名前を指定します。 通常、ウィザードではサーバーの完全修飾ドメイン名 (FQDN) が取得されます。 データベース インスタンスを指定するには、&lt;"*サーバー名*">\&lt;"*インスタンス名*"> という形式を使用します。 たとえば、`sqlserver\named1` となります。

    - **データベース名**:Configuration Manager サイト データベースの名前を指定します。 **[確認]** を選択して、ウィザードからサイト データベースにアクセスできることを確認します。  

        > [!IMPORTANT]  
        > レポート サービス ポイントの作成に使用するユーザー アカウントには、サイト データベースに対する**読み取り**アクセス許可がある必要があります。 接続テストに失敗した場合、赤色の警告アイコンが表示されます。 アイコン上のコンテキスト ホバー テキストには、エラーの詳細が表示されます。 エラーを修正し、 **[テスト]** をもう一度選択します。  

    - **フォルダー名**:Reporting Services 内で Configuration Manager レポート用に作成および使用されるフォルダー名を指定します。  

    - **Reporting Services サーバー インスタンス**:Reporting Services の SQL Server のインスタンスを選択します。 このページにインスタンスが表示されない場合は、SQL Server Reporting Services がインストール、構成、開始されていることを確認します。  

        > [!IMPORTANT]  
        > Configuration Manager により、現在のユーザーのコンテキストで、選択したサイト システム上の WMI への接続が行われます。 この接続を使用して、Reporting Services の SQL Server のインスタンスが取得されます。 現在のユーザーには、サイト システム上の WMI に対する **[読み取り]** アクセス許可が必要です。それがない場合は、ウィザードで Reporting Services インスタンスを取得できません。  

    - **レポート サービス ポイントのアカウント**: **[設定]** を選択し、使用するアカウントを選択します。 レポート サービス ポイント上の SQL Server Reporting Services では、Configuration Manager サイト データベースに接続するためにこのアカウントが使用されます。 この接続は、レポートのデータを取得するためのものです。 **[既存のアカウント]** を選択して、以前に Configuration Manager アカウントとして構成した Windows ユーザー アカウントを指定します。 **[新しいアカウント]** を選択して、現在使用するように構成されていない Windows ユーザー アカウントを指定します。 Configuration Manager は指定したユーザーにサイト データベースへのアクセスを自動的に付与します。  

        Reporting Services を実行するアカウントは、ドメイン ローカル セキュリティ グループ **Windows Authorization Access Group** に属している必要があります。 また、 **[tokenGroupsGlobalAndUniversal の読み取り]** アクセス許可が **[許可]** に設定されている必要もあります。 レポート サービス ポイント アカウントとは異なるドメイン内のユーザーがレポートを正常に実行するには、ドメイン間の双方向の信頼が必要です。

        指定された Windows ユーザー アカウントとパスワードは、暗号化されて Reporting Services データベースに格納されます。 Reporting Services は、このアカウントとパスワードを使用して、サイト データベースからレポートのデータを取得します。  

        > [!IMPORTANT]  
        > 指定するアカウントには、Reporting Services データベースをホストするサーバーに対する **[ローカル ログオン]** アクセス許可が必要です。  

1. ウィザードを完了します。

ウィザードが完了すると、Configuration Manager によって Reporting Services にレポート フォルダーが作成されます。 次に、指定したレポート フォルダーにそのレポートがコピーされます。  

> [!TIP]  
> レポート サービス ポイント サイトの役割をホストするサイト システムのみを一覧表示するには、 **[サーバーとサイト システムの役割]** を右クリックして、 **[レポート サービス ポイント]** を選択します。  

### <a name="languages-for-reports"></a><a name="bkmk_languages" /> レポート用の言語

<!-- SCCMDocs#1067 -->

Configuration Manager によってレポート フォルダーが作成され、レポートがレポート サーバーにコピーされるときに、そのオブジェクトに適した言語が決定されます。

- レポート フォルダーの作成、レポートのコピー

  - サイト サーバーの OS のロケールを使用してオブジェクトを作成します

  - 特定の言語パックを使用できない場合は、既定で英語 (ENU) に設定されます

- Web ブラウザーでのレポートの表示

  - フォルダー名とレポート名: サイト サーバーと同じロケール
  
  - レポートの内容: ブラウザーのロケールに基づいて動的

- Configuration Manager コンソールでのレポートの表示

  - フォルダー名とレポート名: コンソールのロケールに基づいて動的
  
  - レポートの内容: コンソールのロケールに基づいて動的

言語パックがないサイトにレポート サービス ポイントをインストールすると、レポートは英語でインストールされます。 レポート サービス ポイントをインストールした後に言語パックをインストールする場合、レポートのレポート サービス ポイントを適切な言語パックの言語で使用できるようにするには、そのポイントをアンインストールしてから再インストールする必要があります。  

詳細については、「[言語パック](../deploy/install/language-packs.md)」を参照してください。

### <a name="file-installation-and-report-folder-security-rights"></a>ファイルのインストールおよびレポート フォルダーのセキュリティ権限

Configuration Manager では次のアクションが実行されて、レポート サービス ポイントがインストールされ、Reporting Services が構成されます。  

> [!IMPORTANT]  
> サイトでは、SMS_Executive サービス用に構成されたアカウントのコンテキストでこれらのアクションが実行されます。 通常、このアカウントは、サイト サーバーのローカル システム アカウントです。  

- レポート サービス ポイントのサイトの役割をインストールします。  

- ウィザードで指定した格納されている資格情報を使用して、Reporting Services にデータ ソースを作成します。 このアカウントは、レポートを実行したときに、Reporting Services がサイト データベースに接続するために使用する Windows ユーザー アカウントとパスワードです。  

- Reporting Services に Configuration Manager のルート フォルダーを作成します。  

- Reporting Services に **[ConfigMgr レポート ユーザー]** と **[ConfigMgr レポート管理者]** セキュリティ ロールを追加します。  

- サブフォルダーを作成し、サイト サーバー上の `%ProgramFiles%\SMS_SRSRP` から Reporting Services に Configuration Manager レポートをデプロイします。  

- **サイトの読み取り**権限を持つ Configuration Manager 内のすべてのユーザー アカウントに、ルート フォルダーに対する Reporting Services の **[ConfigMgr レポート ユーザー]** ロールを追加します。  

- **サイトの変更**権限を持つ Configuration Manager 内のすべてのユーザー アカウントに、ルート フォルダーに対する Reporting Services の **[ConfigMgr レポート管理者]** ロールを追加します。  

- レポート フォルダーと Configuration Manager のセキュリティで保護されたオブジェクトの種類との間のマッピングを取得します。 Configuration Manager では、このマップがサイト データベース内に保持されます。  

- Configuration Manager の管理ユーザーに、Reporting Services の特定のレポート フォルダーに対する次の権限を構成します。  

  - ユーザーを追加し、Configuration Manager オブジェクトの **[レポートの実行]** アクセス許可を持つ管理ユーザーに、関連付けられているレポート フォルダーに対する **[ConfigMgr レポート ユーザー]** ロールを割り当てます。  

  - ユーザーを追加し、Configuration Manager オブジェクトの **[レポートの変更]** アクセス許可を持つ管理ユーザーに、関連付けられているレポート フォルダーに対する **[ConfigMgr レポート管理者]** ロールを割り当てます。  

Configuration Manager は Reporting Services に接続し、Configuration Manager と Reporting Services のルート フォルダーおよび特定のレポート フォルダーに対するアクセス許可をユーザーに設定します。 レポート サービス ポイントが最初にインストールされてから、Configuration Manager は Reporting Services に 10 分間隔で接続し、レポート フォルダーに構成されているユーザー権限が Configuration Manager ユーザーに設定された関連付けられている権限であることを確認します。 Reporting Services のレポート マネージャーを使用して、レポート フォルダーへのユーザーの追加、またはユーザー権限の変更を行うと、Configuration Manager は、サイト データベースに格納されている役割に基づいた割り当てを使用して、それらの変更を上書きします。 また、Configuration Manager では、Configuration Manager でのレポート権限を持っていないユーザーが削除されます。  

### <a name="reporting-services-security-roles"></a>Reporting Services のセキュリティ ロール

Configuration Manager によってレポート サービス ポイントがインストールされるときに、Reporting Services に次のセキュリティ ロールが追加されます。  

- **ConfigMgr レポート ユーザー**:このセキュリティ ロールが割り当てられたユーザーは、Configuration Manager レポートのみを実行できます。  

- **ConfigMgr レポート管理者**:このセキュリティ ロールが割り当てられたユーザーは、Configuration Manager のレポートに関連するすべてのタスクを実行できます。  

## <a name="verify-installation"></a><a name="bkmk_verify"></a> インストールの検証

レポート サービス ポイントのインストールを検証するには、特定のステータス メッセージおよびログ ファイルのエントリを確認します。 レポート サービス ポイントのインストールが成功したことを確認するには、次の手順に従います。  

> [!Note]  
> レポートが Configuration Manager コンソールの **[監視]** ワークスペースにある **[レポート]** ノードの **[レポート]** サブフォルダーに表示される場合は、この手順をスキップすることができます。

### <a name="verify-installation-by-status-message"></a>ステータス メッセージによるインストールの検証

1. Configuration Manager コンソールで、 **[監視]** ワークスペースに移動し、 **[システム ステータス]** を展開し、 **[コンポーネントのステータス]** ノードを選択します。  

1. **SMS_SRS_REPORTING_POINT** コンポーネントを選択します。  

1. リボンの **[ホーム]** タブの **[コンポーネント]** グループで、 **[メッセージを表示する]** を選択し、 **[すべて]** を選択します。  

1. レポート サービス ポイントをインストールする前の期間の日付と時刻を指定して、 **[OK]** を選択します。  

1. ステータス メッセージ ID **1015** を確認します。 このステータス メッセージは、レポート サービス ポイントが正常にインストールされたことを示します。

### <a name="verify-installation-by-log-file"></a>ログ ファイルによるインストールの検証

Configuration Manager のインストール パスの **Logs** ディレクトリにある **Srsrp.log** ファイルを開きます。 文字列 `Installation was successful` を検索します。

ログ ファイルのレポート サービス ポイントが正常にインストールされた時刻からログを確認します。 レポート フォルダーが作成されたこと、レポートが展開されたこと、および各フォルダーのセキュリティ ポリシーが確認されたことを検証します。 セキュリティ ポリシーの確認の最後の行の後で、文字列 `Successfully checked that the SRS web service is healthy on server` を探します。  

## <a name="configure-a-certificate-to-author-reports"></a>レポートを作成するための証明書の構成

SQL Server Reporting Services 内でレポートを作成する場合、多くのオプションがあります。 Configuration Manager コンソールでレポートを作成または編集する場合、Configuration Manager はレポート ビルダーを開いて、作成環境として使用します。 Configuration Manager レポートをどのように作成するかにかかわらず、サイト データベース サーバーでのサーバー認証のために自己署名入り証明書が必要です。

> [!NOTE]  
> SQL Server Reporting Services を使用したレポートの作成について詳しくは、「[レポートビルダーの作成環境](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs)」をご覧ください。  

Configuration Manager によって、サイト サーバー上の証明書と SMS プロバイダーの役割が自動的にインストールされます。 これらのサーバーのいずれかから Configuration Manager コンソールを実行する場合は、そこからレポートを作成または編集できます。

別のコンピューター上の Configuration Manager コンソールからレポートを作成または変更する場合は、サイト サーバーから証明書をエクスポートします。 特定の証明書のフレンドリ名は、ローカル コンピューターの**信頼されたユーザー**証明書ストア内のサイト サーバーの FQDN です。 Configuration Manager コンソールを実行するコンピューター上で、この証明書を**信頼されたユーザー**証明書ストアに追加します。  

## <a name="modify-reporting-services-point-settings"></a>レポート サービス ポイントの設定の変更

この役割をインストールした後、サイト データベースの接続および認証の設定をレポート サービス ポイントのプロパティで変更できます。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サーバーとサイト システムの役割]** ノードを選択します。  

    > [!TIP]  
    > レポート サービス ポイントをホストするサイト システムのみを一覧表示するには、 **[サーバーとサイト システムの役割]** ノードを右クリックして、 **[レポート サービス ポイント]** を選択します。  

1. レポート サービス ポイントをホストするサイト システムを選択します。 次に、詳細ウィンドウで、**レポート サービス ポイント**のサイト システムの役割を選択します。

1. リボンの **[サイトの役割]** タブの **[プロパティ]** グループで、 **[プロパティ]** を選択します。  

1. **[レポート サービス ポイントのプロパティ]** で、次の設定を変更できます。  

    - **サイト データベース サーバー名**

    - **データベース名**

    - **ユーザー アカウント**

1. **[OK]** を選択して変更を保存し、プロパティを閉じます。  

これらの設定について詳しくは、「[サイト システムにレポート サービス ポイントをインストールする](#bkmk_install)」のセクションの説明をご覧ください。

## <a name="power-bi-report-server"></a>Power BI Report Server

バージョン 2002 以降では、Power BI Report Server をレポートと統合できるようになりました。 構成の詳細については、「[Power BI Report Server との統合](powerbi-report-server.md)」を参照してください。

## <a name="upgrade-sql-server"></a>SQL Server のアップグレード

SQL Server と SQL Server Reporting Services をアップグレードするには、まずサイトからレポート サービス ポイントを削除します。 SQL Server をアップグレードした後、Configuration Manager にレポート サービス ポイントを再インストールします。

このプロセスに従わないと、Configuration Manager コンソールからレポートを実行または編集するときにエラーが表示されます。 Web ブラウザーからは引き続き正常にレポートの実行と編集を行うことができます。  

## <a name="configure-report-options"></a>レポート オプションの構成

レポートの管理に使用する既定のレポート サービス ポイントを選択できます。 サイトには複数のレポート サービス ポイントを含めることができますが、レポートの管理には既定のサーバーのみが使用されます。 サイトのレポート オプションを構成するには、次の手順に従います。  

1. Configuration Manager コンソールで、 **[監視]** ワークスペースに移動して、 **[レポート]** を展開し、 **[レポート]** ノードを選択します。  

1. リボンの **[ホーム]** タブの **[設定]** グループで、 **[レポート オプション]** を選択します。  

1. 一覧から既定のレポート サーバーを選択して、 **[OK]** を選択します。

サーバーが表示されない場合は、サイトにレポート サービス ポイントがインストールされ、構成されていることを確認します。 詳しくは、「[インストールの検証](#bkmk_verify)」をご覧ください。

レポート サーバーで使用する SQL Server のバージョンと一致する SQL Server レポート ビルダーのバージョンがコンピューターで実行されていることを確認します。 そうでないと、エラーが表示され、既定のレポート サーバーによってレポートが保存されず、レポートの作成や編集はできません。<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>次のステップ

[レポートの操作とメンテナンス](operations-and-maintenance-for-reporting.md)
