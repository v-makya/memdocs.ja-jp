---
title: ソフトウェア更新プログラムの同期の管理
titleSuffix: Configuration Manager
description: ソフトウェア更新プログラムの同期のスケジュール、手動によるソフトウェア更新プログラムの同期の開始、ソフトウェア更新プログラムの同期の監視を行うには、次の手順を実行します。
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1b47965fa5cc36b0c0eb6d47c2214d1dceb8ee8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692940"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a> ソフトウェア更新プログラムの同期

*適用対象:Configuration Manager (Current Branch)*

 Configuration Manager におけるソフトウェア更新プログラムの同期は、構成された基準を満たすソフトウェア更新プログラムのメタデータを取得するプロセスです。 これには、特定の製品、分類、言語が含まれます。 通常、中央管理サイトまたはスタンドアロン プライマリ サイトのソフトウェアの更新ポイントでは、Microsoft Update からメタデータを取得します。 次に、最上位サイトは他のサイトに同期要求を送信します。 サイトが親サイトから同期要求を受信すると、そのサイトのソフトウェアの更新ポイントがアップストリームの [同期ソース](../plan-design/plan-for-software-updates.md#BKMK_SyncSource)からソフトウェア更新プログラムのメタデータを取得します。 ソフトウェア更新プログラムの同期プロセスの詳細については、「[Software updates synchronization](../understand/software-updates-introduction.md#BKMK_Synchronization)」 (ソフトウェアの更新プログラムの同期) を参照してください。

最上位サイトのソフトウェアの更新ポイントのプロパティで、ソフトウェア更新プログラムの同期がスケジュールに従って実行されるように構成します。 いったん同期スケジュールを構成すると、通常の運用業務の一環として変更することは一般的にはありません。 ただし、必要な場合は、手動でソフトウェア更新プログラムの同期を開始することができます。

  > [!NOTE]  
  >  ソフトウェアの更新ポイントは、ソフトウェア更新プログラムを同期するためには、アップストリームの同期ソースに接続されている必要があります。 ソフトウェアの更新ポイントがアップストリームの同期ソースから切断されている場合は、エクスポートとインポートの方法を使ってソフトウェアの更新プログラムを同期できます。 詳細については、「[切断されているソフトウェアの更新ポイントからのソフトウェア更新プログラムの同期](synchronize-software-updates-disconnected.md)」を参照してください。  

## <a name="schedule-software-updates-synchronization"></a>ソフトウェア更新プログラムの同期のスケジュール
ソフトウェア更新プログラムの同期のスケジュールを構成する場合は、最上位のソフトウェア更新ポイントが、スケジュールされた日付と時刻に Microsoft Update との同期を開始します。 カスタム スケジュールを使用すると、Windows Server Update Services (WSUS) サーバー、サイト サーバー、およびネットワークの要求が低い日時にソフトウェア更新プログラムを同期することができます。 たとえば、ソフトウェア更新プログラムが、毎週午前 2:00 に同期されるように、スケジュールを設定できます。 スケジュールされた同期では、前回のスケジュールされた同期以降にソフトウェア更新プログラムのメタデータに加えられたすべての変更がサイト データベースに挿入されます。 これには、新しいソフトウェア更新プログラムのメタデータ、あるいは変更、削除、または期限切れになったメタデータが含まれます。

ソフトウェア更新プログラムの同期をスケジュールするには、最上位サイトで次の手順を実行します。  

#### <a name="to-schedule-software-updates-synchronization"></a>ソフトウェア更新プログラムの同期をスケジュールするには  

  1.  Configuration Manager コンソールで、 **[管理]** をクリックします。  

  2.  [管理] ワークスペースで **[サイトの構成]** を展開して、 **[サイト]** をクリックします。  

  3.  結果ウィンドウで、中央管理サイトまたはスタンドアロン プライマリ サイトをクリックします。  

  4.  **[ホーム]** タブの **[設定]** グループで、 **[サイト コンポーネントの構成]** をクリックして **[ソフトウェアの更新ポイント]** を選択します。  

  5.  [ソフトウェアの更新ポイント コンポーネントのプロパティ] ダイアログ ボックスで、 **[スケジュールによる同期を有効にする]** を選択して、同期スケジュールを指定します。  

## <a name="manually-start-software-updates-synchronization"></a>ソフトウェア更新プログラムの同期を手動で開始
Configuration Manager コンソールで **[ソフトウェア ライブラリ]** ワークスペースの **[すべてのソフトウェア更新]** ノードから、最上位サイトのソフトウェア更新プログラムの同期を手動で開始することもできます。  

ソフトウェア更新プログラムの同期を手動で開始するには、最上位サイトで次の手順を実行します。  

#### <a name="to-manually-start-software-updates-synchronization"></a>ソフトウェア更新プログラムの同期を手動で開始するには  

1. 中央管理サイトまたはスタンドアロン プライマリ サイトに接続された Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。  

2. ソフトウェア ライブラリ ワークスペースで、 **ソフトウェア更新プログラム** を展開して、**すべてのソフトウェア更新プログラム** または **ソフトウェア更新プログラム グループ** をクリックします。  

3. **[ホーム]** タブの **[作成]** グループで、 **[ソフトウェア更新プログラムの同期]** をクリックします。 ダイアログ ボックスで **[はい]** をクリックして、同期プロセスの開始を確定します。  

   ソフトウェアの更新ポイントで同期プロセスを開始した後、階層内のすべてのソフトウェアの更新ポイントについて、Configuration Manager コンソールから同期プロセスを監視することができます。 ソフトウェア更新プログラムの同期プロセスを監視するには、次の手順に従います。  


## <a name="monitor-software-updates-synchronization"></a>ソフトウェア更新プログラムの同期の監視
同期プロセスを開始した後に、Configuration Manager コンソールを使用して、階層内のすべての更新ポイントの同期プロセスを監視することができます。 ソフトウェア更新プログラムの同期プロセスを監視するには、次の手順に従います。 ソフトウェア更新プログラムの同期プロセスの監視の詳細については、「[Monitor software updates](../deploy-use/monitor-software-updates.md)」 (ソフトウェアの更新プログラムの監視) を参照してください。

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>ソフトウェア更新プログラムの同期プロセスを監視するには  

1. Configuration Manager コンソールで、 **[監視]** をクリックします。  

2. **[監視]** ワークスペースで、 **[ソフトウェアの更新ポイントの同期ステータス]** をクリックします。  

   Configuration Manager 階層内のソフトウェアの更新ポイントが結果ウィンドウに表示されます。 このビューから、すべてのソフトウェアの更新ポイントの同期ステータスを監視することができます。 同期プロセスの詳細情報が必要な場合は、各サイト サーバーの <*ConfigMgrInstallationPath*>\Logs にある wsyncmgr.log ファイルを確認できます。  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Microsoft Update カタログから更新プログラムをインポートする

最上位のソフトウェアの更新ポイントでは、WSUS を使用して、Microsoft からのソフトウェア更新プログラムに関する情報を Configuration Manager に取り込みます。 場合によっては、選択した製品および分類の WSUS に自動的に同期しない更新プログラムが必要な場合がありますが、これは [Microsoft Update カタログ](https://catalog.update.microsoft.com)から入手できます。 WSUS に自動的に同期しない更新プログラムは、通常、特殊な問題を解決することが意図されています。 通常、カタログ内で更新プログラムが使用できる場合は、それを WSUS にインポートできます。 その後、Configuration Manager に同期して、他の更新プログラムと同じように展開できます。

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Microsoft Update カタログから更新プログラムをインポートするには

1. WSUS 管理コンソールを開き、階層内の最上位の WSUS サーバーに接続します。
   - Internet Explorer がコンピューターの既定の Web ブラウザーでない場合、一時的に既定のブラウザーとして設定されます。
2. **[更新プログラム]** をクリックするか、WSUS サーバーの名前をクリックします。 
3. **[アクション]** ウィンドウで **[更新プログラムのインポート]** を選択すると、[Microsoft Update カタログ](https://catalog.update.microsoft.com) のブラウザー ウィンドウが開きます。
   ![WSUS コンソールで [更新プログラムのインポート] を選択](media/wsus-console-import-updates.png)
4. 求められたら、Microsoft Update カタログ ActiveX コントロールをインストールします。 このコントロールは、更新プログラムを WSUS にインポートするためにインストールする必要があります。 
5. ブラウザー ウィンドウで、必要な更新プログラムを検索します。 **[追加]** * ボタンをクリックして、バスケットに追加します。
6. **[バスケットの表示]** をクリックします。 オプション **[Import directly into Windows Server Update Services]\(Windows Server Update Services に直接インポートする\)** が選択されていることを確認します。 **[インポート]** をクリックします。
    ![カタログから更新プログラムを WSUS にインポート](./media/import-catalog-update-into-wsus.png)
7. インポートが完了したら、ブラウザー ウィンドウで **[閉じる]** をクリックします。
     - 必要に応じて、既定のブラウザーをリセットします。
8. Configuration Manager ソフトウェアの更新ポイントを同期します。


## <a name="next-steps"></a>次のステップ
最初にソフトウェア更新プログラムを同期した後、または使用可能な新しい分類または製品があったら、[新しい分類と製品を構成](configure-classifications-and-products.md)して、新しい条件のソフトウェア更新プログラムを同期します。

必要な条件でソフトウェア更新プログラムを同期した後、[ソフトウェア更新プログラムの設定を管理します](manage-settings-for-software-updates.md)。  
