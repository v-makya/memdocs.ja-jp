---
title: Technical Preview 1511 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1511 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 475cb4e9a4c6c3b90582210b0ebf4a7f69e9f643
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694290"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Configuration Manager の Technical Preview 1511 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1511 で利用できる機能について説明します。 このバージョンは、新しい Technical Preview サイトをインストールまたは以前のバージョンの Technical Preview からアップグレードするために使用できる Technical Preview の基準インストールです。   このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。  

このバージョンでお試しいただける新機能を次に示します。  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a> Windows 10 における Windows Update for Business との統合  
 Configuration Manager では、Windows Update for Business (WUfB) を介して直接接続されている Windows 10 コンピューターと、Windows 10 の更新プログラムとアップグレードを取得するために WSUS に接続されているコンピューターとを区別できるようになりました。  WUfB を介して接続されているコンピューターの場合、更新プログラムとアップグレードは、管理ユーザーによってグループ ポリシーまたは MDM ポリシーを使用して設定された間隔で管理でき、これらの更新プログラムやアップグレードを WUfB から直接インストールできます。    
WUfB を介して接続されているコンピューターの場合、Configuration Manager で、対応ステータス (Windows Update や定義の更新プログラムを含む) についてレポートすることはできません。 また、Configuration Manager では、これらのコンピューターに Microsoft Update やサード パーティの更新プログラムを展開することもできません。  

 **このシナリオの前提条件:**  

-   Windows 10 Desktop Pro または Windows 10 Enterprise Edition バージョン 1511 以降  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx)を介して管理されているコンピューター  

### <a name="try-it-out"></a>試してみましょう。  
 次のタスクを実行してから、このトピックの先頭付近にあるフィードバック情報を使用してその動作を報告してください。  

1.  Windows Update エージェントが以前有効になっていた場合は、WSUS がスキャンされないように、無効にします。   
    レジストリ キー **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** を設定し、コンピューターによって WSUS または Windows Update がスキャンされるかどうかを指定できます。  この値が 2 の場合、WSUS についてはスキャンされません。  

2.  Configuration Manager リソース エクスプローラーで、 **Windows Update**ノードの下にある新しい属性 **UseWUServer** を確認します。  

3.  更新プログラムとアップグレードのために WUfB を介して接続されているすべてのコンピューターを対象とした **UseWUServer** 属性に基づいて、コレクションを作成します。  

4.  ソフトウェア更新プログラム ワークフローを無効にするクライアント エージェント設定を作成し、WUfB に直接接続されているコンピューターのコレクションに、この設定を展開します。  

5.  WUfB を介して管理されているコンピューターの対応ステータスには **[不明]** と表示され、全体のコンプライアンス対応率をカウントする際に、これらのコンピューターは除外されます。  

##  <a name="managing-office-365-proplus-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a> Configuration Manager を使用した Office 365 ProPlus クライアント更新プログラムの管理  
 Configuration Manager では、Configuration Manager ソフトウェア更新管理のワークフローを使用して、Office 365 デスクトップ クライアントの更新プログラムを管理できます。    
Microsoft から、Windows Server Updates Services (WSUS) に新しい Office 365 デスクトップ クライアントの更新プログラムが公開されると、Office 365 の更新プログラムがカタログの同期の一部として構成されている場合、Configuration Manager で、この更新プログラムをそのカタログと同期することができます。  Configuration Manager サイト サーバーでは、Office 365 クライアントの更新プログラムをダウンロードして、そのパッケージを Configuration Manager 配布ポイントに配布します。  次に、Configuration Manager クライアントにより、更新プログラムの取得場所とそのインストール プロセスの開始時期が、Office 365 デスクトップ クライアントに通知されます。  

**このシナリオの前提条件:**  

### <a name="try-it-out"></a>試してみましょう。  
 次のタスクを実行してから、このトピックの先頭付近にあるフィードバック情報を使用してその動作を報告してください。  

1. Office 365 の更新プログラムを Configuration Manager サイト サーバーと同期して、Configuration Manager コンソールから表示できます。  

2. Office 365 の更新プログラムを承認して、正常に展開できます。  

3. クライアントに Office 365 の更新プログラムを正常にダウンロードできます。  

4. コンソール内の監視機能またはレポートを使用して、Office 365 の更新プログラムのコンプライアンス対応を確認できます。  

   詳しい手順については、「[Configuration Manager Technical Preview による Office 365 クライアント更新プログラムの管理](https://technet.microsoft.com/library/mt628083.aspx)」をご覧ください。  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a> 高可用性データベース用の SQL Server AlwaysOn のサポート  
 Configuration Manager は、SQL Server AlwaysOn 可用性グループを使用したサイト データベースのホスティングをサポートします。  新しいサイトをインストールするときに、SQL Server の通常のインスタンスではなく、可用性グループを使用するようにセットアップに指示できます。  

> [!NOTE]  
>  可用性グループを正しく構成および使用するには、SQL Server 可用性グループの構成に習熟している必要があり、SQL Server ドキュメント ライブラリで提供されるドキュメントと手順に従う必要があります。  

可用性グループを構成して使用するプロセスには、大まかに、次のことが含まれます。  

1.  SQL Server で可用性グループを構成します。  

2.  新しい Configuration Manager サイトをインストールして、セットアップ中に、グループのエンドポイントを指定することによって、可用性グループを使用するようにサイトに指示します。  

**このシナリオの前提条件:**  

-   Configuration Manager Technical Preview でサポートされる SQL Server のバージョンが必要です。  

-   Configuration Manager をインストールする前に、SQL Server 可用性グループを作成して構成する必要があります。  

-   可用性グループには、1 つのプライマリ レプリカを含める必要があり、最大 2 つの同期セカンダリ レプリカを含めることができます。  

-   可用性グループには、少なくとも 1 つのエンドポイントを含める必要があります。  

-   可用性グループ内の SQL Server からアクセス可能なネットワークの場所を用意する必要があります。 この場所は、可用性グループの構成時にセットアップで使用され、セットアップの完了後に削除することができます。  

**このリリースの既知の問題:**  

-   既にサイト データベースとして使用されている可用性グループに新しいレプリカ メンバーを追加することはできません。 新しいレプリカ メンバーを追加するには、サイトをインストールし直す必要があります。  

-   このシナリオでは、管理ポイント サーバーに **SQL Server 2012 ネイティブ クライアント** を ([SQL Server 2012 機能パックから](https://www.microsoft.com/download/details.aspx?id=29065)) インストールしなければならない場合があります。 これにより、SQL 接続エラー (管理ポイント サーバー上の **mp_getauth.log** に記録される) が回避されます。  

### <a name="try-it-out"></a>試してみましょう。  
次のタスクを実行してから、このトピックの先頭付近にあるフィードバック情報を使用してその動作を報告してください。  

-   SQL AlwaysOn 可用性グループ用に構成されたデータベース サーバーを使用するプライマリ サイトをインストールすることができます。  

-   自分の SQL AlwaysOn 可用性グループをグループ内の新しいレプリカにフェールオーバーできました。プライマリ サイトはまだ稼働しています。  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configuration Manager 用の SQL Server AlwaysOn の構成  
 次の手順を使用して、可用性グループを作成して構成してから、その可用性グループを使用する新しい Configuration Manager サイトをインストールします。  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn 可用性グループを作成するには  
[SQL Server 可用性グループを作成する](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx) プロセスは、SQL Server ドキュメント ライブラリに記載されています。  可用性グループを作成するときに、Configuration Manager で使用するための次の要件が満たされていることを確認します。  

-   最大 3 つのメンバー:  

    -   1 つのプライマリ レプリカと最大 2 つのセカンダリ レプリカ  

    -   セカンダリ レプリカは同期している必要があります。  

        > [!TIP]  
        >  セカンダリ レプリカは読み取り専用に構成することをお勧めします。 これにより、サイト操作のためのプライマリ レプリカのパフォーマンスを維持しながら、レポートなどの機能にセカンダリ レプリカを使用することができます。  

-   少なくとも 1 つのエンドポイント。 Configuration Manager サイトをインストールするときに、このエンドポイントの仮想名が使用されます。  

    > [!TIP]  
    >  グループには複数のエンドポイントを含めることができますが、Configuration Manager はそのうちの 1 つしか利用できません。  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>可用性グループを使用する Configuration Manager サイトをインストールするには  
SQL Server 可用性グループを使用するサイトをインストールするには、次のようにします。  

1.  Configuration Manager セットアップから要求されたら、以下を代入します。  

    -   **SQL Server 名**:可用性グループを作成するときに構成したエンドポイントの仮想名を入力します。 仮想名は、 **&lt;endpointServer\>.fabrikam.com** のように完全な DNS 名にする必要があります。  

    -   **インスタンス**: この値は空白のままにする必要があります。 この構成内にはインスタンスが存在しません。  

    -   **データベース**: 可用性グループのプライマリ レプリカ上に作成したデータベースの名前を入力します。  

2.  次に、グループ内の SQL Server からアクセス可能なネットワークの場所を用意する必要があります。  

    -   各 SQL Server からのコンピューター アカウントとサービス アカウントには、この場所へのフル コントロール アクセス権が必要です。  

    -   この場所は、セットアップ中にのみ使用され、セットアップが完了してサイトがインストールされたら、共有解除または削除することができます。  

3.  この情報を提供した後、通常のプロセスと構成を使ってセットアップを完了します。  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a> サーバー クラスターの提供  
クラスター内のサーバーを含むコレクションを作成してから、更新プログラムをクラスターに展開するときに使用するようにクラスター設定を構成できるようになりました。 任意の時点でオンラインになっているサーバーの割合を制御できるだけでなく、カスタム アクションを実行するように展開前および展開後の PowerShell スクリプトを構成できます。  

**このリリースの既知の問題:**  

-   クラスター サーバーのソフトウェア更新プログラム展開のステータスのチェックに使用できるレポートはありません。  

-   このリリースでは、 **[クラスター設定]** ページのメンテナンス シーケンス オプションが無効になっており、使用できません。  

### <a name="try-it-out"></a>試してみましょう。  
次のタスクを実行してから、このトピックの先頭付近にあるフィードバック情報を使用してその動作を報告してください。  

-   サーバーのクラスターを表すコレクションを作成できます。 このテストでは、このコレクションに 2 台のコンピューターを含めるようにメンバーシップ収集規則を構成できます。  

-   クラスター内の 50% のサーバーしかクラスター サービス中の任意の時点でオフラインにできないことを指定できます。 手順内のサンプル スクリプトを使用して、展開前スクリプトと展開後スクリプトを指定します。  

-   更新プログラムをこのコレクションに展開します。 C:\temp で start.txt ファイルと end.txt ファイルを調査して、クラスター内のサーバー上の展開の開始時刻と終了時刻を確認します。 詳細については、UpdatesDeployment.log ファイルを参照してください。  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>サーバー クラスターのコレクションを作成するには  

1.  クラスター内のサーバーを含む[デバイス コレクションを作成します](https://technet.microsoft.com/library/gg712295.aspx)。  

2.  **[資産とコンプライアンス]** ワークスペースで **[デバイス コレクション]** をクリックし、クラスター内のサーバーを含むコレクションを右クリックして、 **[プロパティ]** をクリックします。  

3.  **[全般]** タブで **[すべてのデバイスが同じサーバー クラスターに含まれる]** を選択し、 **[設定]** をクリックします。  

4.  **[クラスター設定]** ページで、ソフトウェア更新プログラムをインストールするために、同時にオフラインにできるサーバーの割合を選択します。 指定した割合に関係なく、クラスター サーバーは一度に 1 台ずつオフラインになります。 Configuration Manager では、一度にサービスを提供できるサーバー数の端数は切り捨てられます。 たとえば、51% を選択し、クラスターに 4 台のサーバーがある場合、2 台のサーバーが同時にオフラインになります。  

5.  展開前 (ノードのドレイン) スクリプトまたは展開後 (ノードの再開) スクリプトを使用するかどうかを指定します。  

    > [!TIP]  
    >  次の例は、現在の時刻をテキスト ファイルに書き込む、展開前スクリプトと展開後スクリプトをテストするときに使用できます。  
    >   
    >  **展開前**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **展開後**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>ソフトウェア更新プログラムをサーバー クラスターに展開するには  

1.  サーバー クラスター コレクションにソフトウェア[更新プログラムを展開します](https://technet.microsoft.com/library/gg712304.aspx)。  

2.  [ソフトウェア更新プログラムの展開を監視します](https://technet.microsoft.com/library/gg712304.aspx)。  
