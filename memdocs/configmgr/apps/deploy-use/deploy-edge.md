---
title: Microsoft Edge バージョン 77 以降を展開および更新する
titleSuffix: Configuration Manager
description: Configuration Manager で Microsoft Edge バージョン 77 以降を展開および更新する方法
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 423864c2c954cc67da4ef54d55d7263ae346e786
ms.sourcegitcommit: 24ce7df7dadf2385afe364b817ec58feeb04c700
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86212292"
---
# <a name="microsoft-edge-management"></a>Microsoft Edge の管理

*適用対象:Configuration Manager (Current Branch)*

まったく新しい Microsoft Edge をビジネスにご利用いただけます。 Configuration Manager バージョン 1910 以降では、[Microsoft Edge バージョン 77 以降](https://docs.microsoft.com/deployedge/)をユーザーに展開できるようになりました。 PowerShell スクリプトは、選択した Edge ビルドをインストールするために使用されます。 また、このスクリプトでは、Configuration Manager を使用して管理できるように、Edge の自動更新がオフにされます。

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a>Microsoft Edge を展開する
<!--4561024-->
管理者は、展開する Microsoft Edge クライアントのバージョンと共に Beta、Dev、または安定チャンネルを選択できます。 各リリースには、お客様とコミュニティから得られた知識と機能改善が組み込まれています。

### <a name="prerequisites-for-deploying"></a>展開するための前提条件

Microsoft Edge 展開の対象となるクライアントの場合:

- PowerShell [実行ポリシー](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies)は制限ありに設定できません。
  - インストールのために PowerShell が実行されます。

- Microsoft Edge インストーラーと [CMPivot](../../core/servers/manage/cmpivot.md) は、**Microsoft コード署名**証明書で署名されています。 その証明書が**信頼された発行元**ストアに登録されていない場合は、追加する必要があります。 そうしないと、PowerShell 実行ポリシーが **AllSigned** に設定されている場合に、Microsoft Edge インストーラーと CMPivot が実行されません。 <!--7585106-->

Configuration Manager コンソールを実行しているデバイスは次のエンドポイントにアクセスする必要があります。

|場所|vmmblue_2|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Microsoft Edge のリリースに関する情報|
|`http://dl.delivery.mp.microsoft.com`|Microsoft Edge リリースのコンテンツ|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a>Microsoft Edge 更新ポリシーを検証する

#### <a name="configuration-manager-version-1910"></a>Configuration Manager バージョン 1910

バージョン 1910 では、Microsoft Edge が展開されると、インストール スクリプトによって Microsoft Edge の自動更新が無効になり、Configuration Manager で管理できるようになります。 この動作はグループ ポリシーを使用して変更できます。 詳細については、「[Microsoft Edge の展開を計画する](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies)」および「[Microsoft Edge - 更新ポリシー](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies)」を参照してください。

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager バージョン 2002 以降
<!--4561024-->
バージョン 2002 以降では、自動更新を無効にするのではなく、自動更新を受信するように設定された Microsoft Edge アプリケーションを作成できます。 この変更により、Configuration Manager を使用して Microsoft Edge の更新プログラムを管理するか、Microsoft Edge による自動更新を許可するかを選択できます。 アプリケーションを作成するときに、 **[Microsoft Edge の設定]** ページの **[Allow Microsoft Edge to automatically update the version of the client on the end user's device]\(エンド ユーザーのデバイス上で Microsoft Edge によるクライアントのバージョンの自動更新を許可する\)** を選択します。 以前にグループ ポリシーを使用してこの動作を変更した場合は、グループ ポリシーにより、Microsoft Edge のインストール中に Configuration Manager によって行われた設定が上書きされます。

[![Microsoft Edge の自動更新設定](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>配置の作成

組み込みアプリケーション エクスペリエンスを使用して、Microsoft Edge アプリケーションを作成し、Microsoft Edge をより簡単に管理できるようにします。

1. コンソールの **[ソフトウェア ライブラリ]** の下に、**Microsoft Edge の管理**という名前の新しいノードがあります。
1. リボンから、あるいは **Microsoft Edge の管理**ノードを右クリックし、 **[Microsoft Edge アプリケーションの作成]** を作成します。

   ![Microsoft Edge の管理ノードの右クリック アクション](./media/4561024-create-microsoft-edge-application.png)

1. ウィザードの **[アプリケーション設定]** ページで、アプリのコンテンツの名前、説明、場所を指定します。 指定したコンテンツの場所のフォルダーが空であることを確実にしてください。
1. **[Microsoft Edge の設定]** ページで、次の項目を選択します。
   - 展開するチャネル
   - 展開するバージョン
   - **[Microsoft Edge がエンド ユーザーのデバイス上のクライアントのバージョンを自動的に更新することを許可する]** かどうか (バージョン 2002 で追加)
1. **[展開]** ページで、アプリケーションを展開するかどうかを決定します。 **[はい]** を選択した場合、アプリケーションの展開設定を指定できます。 展開設定の詳細については、「[アプリケーションの展開](deploy-applications.md#bkmk_deploy-general)」を参照してください。
1. クライアント デバイスで **[ソフトウェアセンター]** で、ユーザーはアプリケーションを表示したり、インストールしたりできます。

   ![展開ウィザードの [Microsoft Edge の設定] ページ](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>展開のログ ファイル

|場所|ログ|vmmblue_2|
|---|---|---|
| サイト サーバー|SMSProv.log|アプリの作成または展開に失敗した場合、詳細を表示します。|
| [場合により異なる](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| コンテンツのダウンロードに失敗した場合、詳細を表示します|
| クライアント|  AppEnforce.log|インストール情報を表示します|

## <a name="update-microsoft-edge"></a>Microsoft Edge を更新する
<!--4831871-->

Configuration Manager バージョン 1910 以降、 **[Microsoft Edge 管理]** 下に **[Microsoft Edge のすべての更新プログラム]** というノードが表示されます。 このノードは、Microsoft Edge のすべてのチャネルの更新プログラムを管理するのに役立ちます。<!--initial edge updates released Jan 15,2020-->

1. Microsoft Edge の更新プログラムを入手するには、[分類] で **[更新プログラム]** を、[製品] で **[Microsoft edge]** を[ 同期用に選択](../../sum/get-started/configure-classifications-and-products.md)していることを確認します。

   [![[ソフトウェアの更新ポイント コンポーネントのプロパティ] の [製品] で [Microsoft Edge] を選択する](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. **[ソフトウェア ライブラリ]** ワークスペースで、 **[Microsoft Edge 管理]** を展開し、 **[Microsoft Edge のすべての更新プログラム]** ノードをクリックします。

1. 必要に応じて、リボンの **[ソフトウェア更新プログラムの同期]** をクリックして同期を開始します。 詳細については、「[ソフトウェア更新プログラムの同期](../../sum/get-started/synchronize-software-updates.md)」を参照してください。

   ![Microsoft Edge のすべての更新プログラム ノード](./media/4831871-all-microsoft-edge-updates.png)

1. 他の更新プログラムと同様、Microsoft Edge 更新プログラムを管理し、展開します。たとえば、Microsoft Edge 更新プログラムを[自動展開規則](../../sum/deploy-use/automatically-deploy-software-updates.md)に追加するなどの作業を行います。 **[Microsoft Edge のすべての更新プログラム]** ノードで実行できる一般的な更新タスクには、次のようなものがあります。

   - [段階的な展開の作成](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [ソフトウェア更新プログラムの手動展開](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [ソフトウェア更新プログラムのダウンロード](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a> Microsoft Edge の管理ダッシュボード
<!--3871913-->
*(バージョン 2002 で導入)*

Configuration Manager 2002 以降、Microsoft Edge の管理ダッシュボードを使用すると、Microsoft Edge やその他のブラウザーの使用状況に関する分析情報を得ることができます。 このダッシュボードでは、次のことができます。

- Microsoft Edge がインストールされているデバイスの数を確認する
- 異なるバージョンの Microsoft Edge がインストールされているクライアントの数を確認する。
   - Canary チャネルは、このグラフに含まれていません。
- デバイス全体のインストールされているブラウザーを確認する
- デバイス別の優先ブラウザーを確認する <!--5907383-->
   - 2002 リリースでは現在、このグラフは空になります。

### <a name="prerequisites-for-the-dashboard"></a>ダッシュボードの前提条件

Microsoft Edge の管理ダッシュボード用に、以下の[ハードウェア インベントリ](../../core/clients/manage/inventory/extend-hardware-inventory.md) クラスで次のプロパティを有効にしてください。

- **インストール済みのソフトウェア - 資産インテリジェンス (SMS_InstalledSoftware)**
   - ソフトウェア コード
   - 製品名
   - 製品バージョン

- **既定のブラウザー (SMS_DefaultBrowser)**
   - ブラウザー プログラム ID

- **ブラウザー使用量 (SMS_BrowserUsage)**
   - BrowserName
   - UsagePercentage

### <a name="view-the-dashboard"></a>ダッシュボードの表示

**[ソフトウェア ライブラリ]** ワークスペースで、 **[Microsoft Edge の管理]** をクリックしてダッシュボードを表示します。 グラフ データのコレクションを変更するには、 **[参照]** をクリックし、別のコレクションを選択します。 既定では、最も大きい 5 つのコレクションがドロップダウン リストに表示されます。 リストにないコレクションを選択すると、新しく選択されたコレクションがドロップダウン リストの下の方に移動します。

[![Microsoft Edge の管理ダッシュボード](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="known-issues"></a>既知の問題

### <a name="hardware-inventory-may-fail-to-process"></a>ハードウェア インベントリの処理に失敗する場合がある
<!--7535675-->
デバイスのハードウェア インベントリの処理に失敗する場合があります。 Dataldr.box ファイルに次のようなエラーが表示される場合があります。

```text
Begin transaction: Machine=<machine>
*** [23000][2627][Microsoft][SQL Server Native Client 11.0][SQL Server]Violation of PRIMARY KEY constraint 'BROWSER_USAGE_HIST_PK'. Cannot insert duplicate key in object 'dbo.BROWSER_USAGE_HIST'. The duplicate key value is (XXXX, Y). : dbo.dBROWSER_USAGE_DATA
ERROR - SQL Error in
ERROR - is NOT retyrable.
Rollback transaction: XXXX
```

**対策:** この問題を回避するには、ブラウザーの使用状況 (SMS_BrowerUsage) のハードウェア インベントリ クラスの収集を無効にします。

## <a name="next-steps"></a>次のステップ

[アプリケーションの監視](monitor-applications-from-the-console.md)

[ソフトウェア更新プログラムの監視](../../sum/deploy-use/monitor-software-updates.md)

[段階的な展開の管理と監視](../../osd/deploy-use/manage-monitor-phased-deployments.md)
