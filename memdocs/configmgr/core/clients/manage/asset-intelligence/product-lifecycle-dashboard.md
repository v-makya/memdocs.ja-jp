---
title: 製品ライフサイクル ダッシュボード
titleSuffix: Configuration Manager
description: Configuration Manager の製品ライフサイクル ダッシュボードを使って Microsoft のライフサイクル ポリシーを表示します。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695170"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Configuration Manager を使って Microsoft のライフサイクル ポリシーを管理する

*適用対象:Configuration Manager (Current Branch)*

バージョン 1806 以降では、Configuration Manager の製品ライフサイクル ダッシュボードを使って Microsoft のライフサイクル ポリシーを表示できます。 このダッシュボードには、Configuration Manager で管理されているデバイスにインストールされている Microsoft 製品の Microsoft ライフサイクル ポリシーの状態が表示されます。 環境内にある Microsoft 製品についての情報、サポート可能性の状態、およびサポート終了日も提供されます。 このダッシュボードを使って、各製品のサポートを利用できるかどうかを理解することができます。 この情報は、お使いの Microsoft 製品の現在のサポート期限になる前に更新を計画するのに役立ちます。  

詳細については、「[Microsoft ライフサイクル ポリシー](https://support.microsoft.com/lifecycle)」を参照してください。

バージョン 1810 以降、ダッシュボードに System Center 2012 Configuration Manager 以降の情報が含まれるようになりました。<!--1358702-->  



## <a name="prerequisites"></a>[前提条件] 

 製品ライフサイクル ダッシュボードでデータを見るには、次のコンポーネントが必要です。  

- Configuration Manager コンソールを実行するコンピューター上に、Internet Explorer 9 以降をインストールする必要があります。  

- サービス コネクション ポイントの役割のインストールと構成が必要です。 このダッシュボードでデータの更新プログラムを取得するには、サービス コネクション ポイントがオンラインか、オフラインの場合は定期的に同期される必要があります。 詳細については、「[About the service connection point](../../../servers/deploy/configure/about-the-service-connection-point.md)」 (サービスの接続ポイントについて) を参照してください。

- レポート サービス ポイントは、ダッシュボードのハイパーリンク機能に必要です。 ダッシュ ボードは、SQL Server Reporting Services (SSRS) レポートにリンクします。 詳細については、「[レポートの概要](../../../servers/manage/introduction-to-reporting.md)」をご覧ください。  

- 資産インテリジェンス同期ポイントを構成して同期する必要があります。 ダッシュボードは、製品タイトルのメタデータとして、資産インテリジェンス カタログを使います。 メタデータは、階層内のインベントリ データと比較されます。 詳細については、[Configuration Manager の資産インテリジェンスの構成](configuring-asset-intelligence.md)に関するページを参照してください。  
  - 資産インテリジェンス サービス ポイントを初めて構成する場合は、忘れずに[資産インテリジェンス ハードウェア インベントリ クラスを有効](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)にしてください。 ライフサイクル ダッシュボードは、これらの資産インテリジェンス ハードウェア インベントリ クラスに依存します。 クライアントがスキャンを行ってハードウェア インベントリを返すまで、ダッシュボードにデータは表示されません。  
  - このダッシュボードの拡張セキュリティ更新プログラム (ESU) に関する情報を表示するには、ハードウェア インベントリ クラスの **[ソフトウェア ライセンス製品 - 資産インテリジェンス (SoftwareLicensingProduct)]** を有効にします。 詳細については、「[資産インテリジェンスのハードウェア インベントリ クラスの有効化](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)」をご覧ください。 <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>製品ライフサイクル ダッシュボードの使用

サイトがマネージド デバイスから収集したインベントリ データを基にして、ダッシュボードは現在のすべての製品についての情報を表示します。 ただし、オペレーティング システムと SQL Server に関して表示される情報は、次のバージョンに制限されます。

- Windows Server 2008 以降
- Windows XP 以降
- SQL Server 2008 以降

Configuration Manager コンソールのライフサイクル ダッシュボードにアクセスするには、 **[資産とコンプライアンス]** ワークスペースに移動して **[資産インテリジェンス]** を展開し、 **[製品のライフサイクル]** ノードを選択します。

> [!NOTE]  
> ダッシュボードのデータは、Configuration Manager コンソールの接続先のサイトに基づきます。 コンソールが最上位層サイトに接続している場合は、階層全体のデータが表示されます。 子プライマリ サイトに接続しているときは、そのサイトのデータだけが表示されます。

### <a name="product-lifecycle-dashboard"></a>製品ライフサイクル ダッシュボード

![コンソールの製品ライフサイクル ダッシュボードのスクリーンショット](media/product-lifecycle-dashboard.png)

**[製品カテゴリ]** リストから次のいずれかのオプションを選択して、ビューを変更します。  
- **すべて**:すべての製品を表示  
- **Windows クライアント**:Windows クライアントの OS バージョンを表示  
- **Windows サーバー**:Windows サーバーの OS バージョンを表示  
- **データベース**: SQL Server のバージョンを表示  
- **Configuration Manager**:バージョン 1810 以降では、Configuration Manager のバージョンを表示 
- **Microsoft Office**: バージョン 1902 以降では、Office 2003 から Office 2016 のインストールされたバージョンの情報を表示 <!--3556026-->

ダッシュボードには、次のタイルがあります。  

- **[Top five products past end-of-life]\(ライフサイクルが終了した上位 5 製品\)** :このタイルは、環境内で見つかった、ライフサイクルが終了した製品の統合データ ビューです。 グラフには、インストールされているソフトウェアのうち、オペレーティング システムおよび SQL サーバー製品のサポート ライフサイクルと比較して有効期限が切れているものが示されます。  

- **[Top five products nearing end-of-life]\(ライフサイクル終了が近づいている上位 5 製品\)** :このタイルは、環境内で見つかった、有効期間の終了が 18 か月以内に近づいている製品の統合データ ビューです。 グラフには、インストールされているソフトウェアのうち、オペレーティング システムおよび SQL サーバー製品のサポート ライフサイクルと比較して有効期限が 18 か月以内のものが示されます。  

- **[インストールされている製品のライフサイクル データ]** :このタイルには、製品がサポート対象から期限切れ状態に移行する時期の概要が示されます。 グラフには、製品がインストールされているクライアントの数の内訳、サポート可用性の状態、および次に行う手順の詳細へのリンクが表示されます。 このグラフには次の情報が含まれています。     
    - 残りサポート時間
    - 環境内での数 
    - メインストリーム サポート終了日
    - 延長サポート終了日
    - 次のステップ  

> [!IMPORTANT]  
> このダッシュボードに表示される情報は、お客様の利便性のため、お客様の社内においてのみ使うことを想定して提供されています。 コンプライアンス対応を確認する場合、この情報のみに依存しないでください。 「[Microsoft ライフサイクル ポリシー](https://support.microsoft.com/lifecycle)」にアクセスして、表示された情報の正しさと、サポート情報を利用できるかどうかを確認してください。  



## <a name="reporting"></a>レポート

その他のレポートも使用できます。 Configuration Manager コンソールの **[監視]** ワークスペースに移動し、 **[レポート]** 、 **[レポート]** の順に展開します。 **[資産インテリジェンス]** カテゴリに次の新しいレポートが追加されます。  

- **ライフサイクル 01A - 特定のソフトウェア製品を搭載したコンピューター**:指定された製品が検出されたコンピューターの一覧を表示します。  

- **ライフサイクル 02A - 組織内で有効切れの製品を使用しているマシンの一覧**:期限切れになった製品が存在するコンピューターを表示します。 このレポートは、製品名でフィルター処理できます。

- **ライフサイクル 03A - 組織内の期限切れの製品一覧**:環境内にあるライフサイクルの有効期限が切れた製品の詳細を表示します。  

- **ライフサイクル 04A - 製品のライフサイクルの概要**:製品のライフサイクルの一覧を表示します。 製品名と有効期限までの日数で一覧をフィルター処理します。  

- **ライフサイクル 05A - 製品ライフサイクル ダッシュボード**:バージョン 1810 以降では、このレポートに、コンソール内のダッシュボードと同様の情報が含まれます。 カテゴリを選択して、環境内の製品の数と、サポートの残りの日数を表示します。  

詳細については、[レポートの一覧](../../../servers/manage/list-of-reports.md#asset-intelligence)に関するページを参照してください。<!--SCCMDocs issue 997-->  
