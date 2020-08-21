---
title: ラボのセットアップ
titleSuffix: Configuration Manager
description: シミュレートされた現実のアクティビティを使用して Configuration Manager を評価するためのラボを設定します。
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c8159928e5fe3e8524c3282cfd1eb543dc9537da
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696499"
---
# <a name="set-up-a-configuration-manager-lab"></a>Configuration Manager ラボの設定

*適用対象:Configuration Manager (Current Branch)*

このトピックのガイダンスに従うことで、シミュレートされた実際のアクティビティで Configuration Manager を評価するためのラボを設定できます。  

> [!NOTE]
> Microsoft では、Configuration Manager の評価版を使用したこのラボの構成済みバージョンを提供しています。 詳細については、[Windows と Office の展開および管理ラボ キット](/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab)に関するページをご覧ください。 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> コア コンポーネント  
 Configuration Manager 用に環境をセットアップするには、Configuration Manager のインストールをサポートするためにいくつかのコア コンポーネントが必要です。    

-   **ラボ環境では Windows Server 2012 R2 が使用**されています。これに対して Configuration Manager のインストールをサポートするコア コンポーネントがいくつか必要です。  

     Windows Server 2012 R2 の評価版は、[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012) からダウンロードできます。  

     これらの演習で参照されている一部のダウンロードに簡単にアクセスできるように、Internet Explorer のセキュリティ強化の構成を変更または無効化することを検討してください。 詳細については、[Internet Explorer のセキュリティ強化構成に関するページを参照してください。セキュリティ強化構成](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10))を無効にします。  

-   **ラボ環境では SQL Server 2012 SP2 が使用** されています (サイト データベース用)。  

     SQL Server 2012 の評価版は、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=43340)からダウンロードできます。  

     SQL Server には、Configuration Manager で使用するために満たしている必要がある[サポートされる SQL Server のバージョン](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions)があります。  

    -   Configuration Manager には、サイト データベースをホストするために 64 ビット版の SQL Server が必要です。  

    -   **SQL 照合順序** クラスとしての **SQL_Latin1_General_CP1_CI_AS** 。  

    -   **SQL 認証**ではなく、 [Windows 認証](/sql/relational-databases/security/choose-an-authentication-mode?view=sql-server-ver15)ではなく、 is required.  

    -   **専用の SQL Server インスタンス**が必要です。  

    -   SQL Server に対して**システム アドレス指定可能なメモリ**を制限しないでください。  

    -   権限の低いドメイン ユーザー アカウントを使用して実行するように **SQL Server サービス アカウント**を構成します。  

    -   **SQL Server Reporting Services** をインストールする必要があります。  

    -   **サイト間の通信** では、既定のポート TCP 4022 で SQL Server Service Broker が使用されます。  

    -   SQL Server データベース エンジンと Configuration Manager サイト システムの役割の間の**サイト内通信**では、既定のポート TCP 1433 が使用されます。  

-   ドメイン コントローラーは、**Active Directory Domain Services がインストールされた Windows Server 2008 R2** を使用します。 ドメイン コントローラーは、完全修飾ドメイン名で使用するための DHCP サーバーと DNS サーバーのホストとしても機能します。  

     詳細については、[Active Directory Domain Services の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831484(v=ws.11))に関するページを参照してください。  

-   演習で実行する管理手順が意図したとおりに機能していることを確認するため、**Hyper-V がいくつかの仮想マシンで使用されます**。 Windows 10 がインストールされている 3 台以上の仮想マシンを使用することをお勧めします。  

     詳細については、[Hyper-V の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11))に関するページを参照してください。  

-   **管理者のアクセス許可** が必要になります。  

    -   Configuration Manager には、Windows Server 環境内でローカルのアクセス許可を持つ管理者が必要です  

    -   Active Directory には、スキーマを変更するアクセス許可を持つ管理者が必要です  

    -   仮想マシンには、マシン自体に対するローカルのアクセス許可が必要です  

このラボでは必要ありませんが、「[Configuration Manager のサポートされている構成](../../core/plan-design/configs/supported-configurations.md)」で Configuration Manager の実装に関する要件の追加情報を確認できます。 ここで言及されていないソフトウェア バージョンについては、このドキュメントを参照してください。  

このすべてのコンポーネントをインストールしたら、追加の手順を実行し Configuration Manager 向けに Windows 環境を構成する必要があります。  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> ラボ向けの Active Directory コンテンツの準備  
 このラボでは、セキュリティ グループを作成し、そのグループにドメイン ユーザーを追加します。  

-   セキュリティ グループ:**Evaluation**  

    -   グループのスコープ:**Universal**  

    -   グループの種類:**Security**  

-   ドメイン ユーザー:**ConfigUser**  

     通常の状況では、環境内のすべてのユーザーに対してユニバーサル アクセスを付与することはありません。 この操作は、このユーザーについて、ラボをオンラインにする操作を効率化する目的で行います。  

次の手順では、Configuration Manager クライアントが Active Directory Domain Services に対してクエリを実行して、サイトのリソースを見つける方法について説明します。  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> System Management コンテナーの作成  
 Configuration Manager では、スキーマの拡張時に、必要な System Management コンテナーが Active Directory Domain Services に自動的に作成されません。 したがって、これをラボ向けに作成します。 この手順では、[ADSI エディターをインストール](/previous-versions/windows/it-pro/windows-server-2003/cc773354(v=ws.10))する必要があります。

 Active Directory ドメイン サービス内の **System** コンテナーで **すべての子オブジェクトを作成する** アクセス許可を持つアカウントとしてログオンします。  

#### <a name="to-create-the-system-management-container"></a>System Management コンテナーを作成するには:  

1.  **ADSI エディター**を実行して、サイト サーバーが常駐しているドメインに接続します。  

2.  **Domain&lt;コンピューターの完全修飾名\>** 、 **<識別名\>** の順に展開して、 **[CN=System]** を右クリックし、 **[新規]** 、 **[オブジェクト]** の順にクリックします。  

3.  **[オブジェクトの作成]** ダイアログ ボックスで、 **[コンテナー]** を選択し、 **[次へ]** をクリックします。  

4.  **[値]** ボックスに「 **System Management**」と入力し、 **[次へ]** をクリックします。  

5.  **[完了]** をクリックしてこの手順を完了します。  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> System Management コンテナーのセキュリティ アクセス許可の設定  
 サイト サーバーのコンピューター アカウントに、サイト情報をコンテナーに発行するのに必要なアクセス許可を付与します。 ADSI エディターもこのタスクに使用します。  

> [!IMPORTANT]  
>  次の手順を開始する前に、サイト サーバーのドメインに接続していることを確認します。  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>System Management コンテナーのセキュリティ アクセス許可を設定するには:  

1.  コンソール ウィンドウで、**サイト サーバーのドメイン**を展開し、 **[DC=&lt;サーバー識別名\>]** 、 **[CN=System]** の順に展開します。 **[CN=System Management]** を右クリックし、 **[プロパティ]** をクリックします。  

2.  **[CN=System Management のプロパティ]** ダイアログ ボックスで、 **[セキュリティ]** タブをクリックし、 **[追加]** をクリックして、サイト サーバーのコンピューター アカウントを追加します。 このアカウントに **フル コントロール** アクセス許可を付与します。  

3.  **[詳細設定]** をクリックして、サイト サーバーのコンピューター アカウントを選択し、 **[編集]** をクリックします。  

4.  **[適用先]** の一覧で **[このオブジェクトとすべての子オブジェクト]** を選択します。  

5.  **[OK]** をクリックして **[ADSI エディター]** コンソールを閉じ、手順を完了します。  

     詳細については、[Configuration Manager 向けの Active Directory スキーマの拡張](../../core/plan-design/network/extend-the-active-directory-schema.md)に関するページを参照してください  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> extadsch.exe を使用した Active Directory スキーマの拡張  
 このラボの Active Directory スキーマを拡張します。これにより、最小限の管理オーバーヘッドですべての Configuration Manager 機能を使用できます。 Active Directory スキーマの拡張は、フォレストごとに 1 回実行されるフォレスト全体の構成です。 スキーマを完全に拡張すると、Active Directory の基本構成の一連のクラスと属性が変更されます。 この操作は、元に戻すことはできません。 スキーマを拡張すると、Configuration Manager がラボ環境内で最も効果的に機能できるように、コンポーネントにアクセスできます。  

> [!IMPORTANT]  
>  **スキーマ管理** セキュリティ グループのメンバーであるアカウントで、スキーマ マスター ドメイン コントローラーにログオンしていることを確認します。 代わりの資格情報を使用することはできません。  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>extadsch.exe を使用して Active Directory スキーマを拡張するには:  

1.  スキーマ マスター ドメイン コントローラーのシステム状態のバックアップを作成します。 マスター ドメイン コントローラーのバックアップの詳細については、「[Windows Server バックアップ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770757(v=ws.11))」を参照してください  

2.  インストール メディアの **\SMSSETUP\BIN\X64** に移動します。  

3.  **extadsch.exe**を実行します。  

4.  システム ドライブのルート フォルダーにある **extadsch.log** を確認して、スキーマの拡張が成功したことを確かめます。  

     詳細については、[Configuration Manager 向けの Active Directory スキーマの拡張](../../core/plan-design/network/extend-the-active-directory-schema.md)に関するページを参照してください。  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> その他の必要なタスク  
 インストールする前に、次のタスクも完了する必要があります。  

 **すべてのダウンロードを格納するフォルダーを作成する**  

 この演習では、インストール メディアのコンポーネントに必要なダウンロードが複数あります。 インストール手順を開始する前に、ラボの使用を停止するまではこれらのファイルを移動せずに済む場所を決めます。 1 つのフォルダーに個別のサブフォルダーを作成して、これらのダウンロードを格納することをお勧めします。  

 **.NET をインストールし、Windows Communication Foundation をアクティブ化する**  

 2 つの .NET Framework をインストールする必要があります。最初に .NET 3.5.1 をインストールしてから、.NET 4.5.2+ をインストールします。 また、Windows Communication Foundation (WCF) をアクティブ化する必要もあります。 WCF は、分散コンピューティング、広範な相互運用性、およびサービス指向の直接サポートに対する管理しやすいアプローチを提供するように設計されており、サービス指向のプログラミング モデルで接続アプリケーションの開発を簡略化します。 詳細については、[Windows Communication Foundation の概要](/previous-versions/dotnet/netframework-3.5/ms731082(v=vs.90))に関するページを参照してください。

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>.NET をインストールし、Windows Communication Foundation をアクティブ化するには:  

1.  **Server Manager**を開き、 **[管理]** に移動します。 **[役割と機能の追加]** をクリックし、 **[役割と機能の追加] Wizard.** を開きます。  

2.  **[始める前に]** パネルの情報を確認し、 **[次へ]** をクリックします。  

3.  **[役割ベースまたは機能ベースのインストール]** をクリックし、 **[次へ]** をクリックします。  

4.  **[サーバー プール]** からサーバーを選択し、 **[次へ]** をクリックします。  

5.  **[サーバーの役割]** パネルを確認し、 **[次へ]** をクリックします。  

6.  次の **機能** を一覧から選択して追加します。  

    -   **.NET Framework 3.5 の機能**  

        -   **.NET Framework 3.5 (.NET 2.0 と 3.0 を含む)**  

    -   **.NET Framework 4.5 の機能**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **WCF サービス**  

            -   **HTTP アクティブ化**  

            -   **TCP ポート共有**  

7.  **[Web サーバーの役割 (IIS)]** と **[役割サービス]** 画面を確認して、 **[次へ]** をクリックします。  

8.  **[確認]** 画面を確認して、 **[次へ]** をクリックします。  

9. **[インストール]** をクリックし、 **サーバー マネージャー** の **[通知]** ウィンドウで、インストールが正常に完了したことを確認します。  

10. .NET の基本インストールの完了後、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=42643) に移動して、.NET Framework 4.5.2 の Web インストーラーを入手します。 **[ダウンロード]** をクリックし、インストーラーを **実行** します。 これにより、選択した言語の必要なコンポーネントが自動的に検出され、インストールされます。  

**BITS、IIS、および RDC の有効化**  

[バックグラウンド インテリジェント転送サービス (BITS)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282296(v=ws.11)) は、クライアントとサーバーの間でファイルを非同期的に転送する必要があるアプリケーションに使用します。 BITS では、フォアグラウンドとバックグラウンドの転送フローを測定することで、他のネットワーク アプリケーションの応答性を保持します。 また、転送セッションが中断した場合は、ファイル転送を自動的に再開します。  

このサイト サーバーは管理ポイントとしても使用されるため、このラボでは BITS をインストールします。  

インターネット インフォメーション サービス (IIS) は、柔軟でスケーラブルな Web サーバーです。これを使用すると、Web であらゆるものをホストできます。 IIS は、さまざまなサイト システムの役割に対して Configuration Manager によって使用されます。 IIS の詳細については、「[サイト システム サーバーの Web サイト](../../core/plan-design/network/websites-for-site-system-servers.md)」を参照してください。  

[Remote Differential Compression (RDC)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754372(v=ws.11)) は、一連のファイルに変更が行われたかどうかをアプリケーションが判断するときに使用できる一連の API です。 RDC を使用すると、ファイルの変更された部分のみをレプリケートすることで、ネットワーク トラフィックを最小限に抑えることができます。  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>BITS、IIS、および RDC サイト サーバーの役割を有効にするには:  

1.  サイト サーバーで、 **Server Manager**を開きます。 **[管理]** に移動します。 **[役割と機能の追加]** をクリックし、 **役割と機能の追加ウィザード**を開きます。  

2.  **[始める前に]** パネルの情報を確認し、 **[次へ]** をクリックします。  

3.  **[役割ベースまたは機能ベースのインストール]** をクリックし、 **[次へ]** をクリックします。  

4.  **[サーバー プール]** からサーバーを選択し、 **[次へ]** をクリックします。  

5.  次の **サーバーの役割** を一覧から選択して追加します。  

    -   **Web サーバー (IIS)**  

        -   **HTTP 共通機能**  

            -   **既定のドキュメント**  

            -   **ディレクトリの参照**  

            -   **HTTP エラー**  

            -   **静的コンテンツ**  

            -   **HTTP リダイレクト**  

        -   **状態と診断**  

            -   **HTTP ログ**  

            -   **ログ ツール**  

            -   **要求監視**  

            -   **トレース**  

    -   **パフォーマンス**  

        -   **静的コンテンツ圧縮**  

        -   **動的なコンテンツの圧縮**  

    -   **Security**  

        -   **要求のフィルタリング**  

        -   **基本認証**  

        -   **クライアント証明書マッピング認証**  

        -   **IP およびドメインの制限**  

        -   **URL 認証**  

        -   **Windows 認証**  

    -   **アプリケーションの開発**  

        -   **.NET 拡張機能 3.5**  

        -   **.NET 拡張機能 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **ISAPI 拡張機能**  

        -   **ISAPI フィルター**  

        -   **サーバー側インクルード**  

    -   **FTP サーバー**  

        -   **FTP サービス**  

    -   **管理ツール**  

        -   **IIS 管理コンソール**  

        -   **IIS 6 管理互換性**  

            -   **IIS 6 メタベース互換**  

            -   **IIS 6 管理コンソール**  

            -   **IIS 6 スクリプト ツール**  

            -   **IIS 6 WMI 互換**  

        -   **IIS 6 管理スクリプトおよびツール**  

        -   **Management Service**  

6.  次の **機能** を一覧から選択して追加します。  

    -   **バックグラウンド インテリジェント転送サービス (BITS)**  

          -   **IIS サーバー拡張機能**  

    -   **リモート サーバー管理ツール**  

          -   **機能管理ツール**  

          -   **BITS サーバー拡張ツール**  

7.  **[インストール]** をクリックし、 **サーバー マネージャー** の **[通知]** ウィンドウで、インストールが正常に完了したことを確認します。  

IIS では、複数の種類のファイル拡張子と場所が、HTTP または HTTPS 通信によってアクセスできないように既定で設定されています。 これらのファイルをクライアント システムに配布できるようにするには、配布ポイントで IIS の要求のフィルタリングを構成する必要があります。 詳しくは、「[IIS の要求フィルター (配布ポイント用)](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering)」を参照してください。  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>配布ポイントで IIS フィルタリングを構成するには:  

1.  **IIS Manager** を開き、サイドバーでサーバーの名前を選択します。 これにより **ホーム** 画面が表示されます。  

2.  **ホーム** 画面の下部で **[機能ビュー]** が選択されていることを確認します。 **IIS** に移動し、 **[要求のフィルタリング]** を開きます。  

3.  **[アクション]** ウィンドウで、 **[ファイル名拡張子の許可]** をクリックします。  

4.  ダイアログ ボックスに「 **.msi** 」と入力し、 **[OK]** をクリックします。  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Configuration Manager のインストール  
クライアントを直接管理するための[プライマリ サイトを使用する場合の判別](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary)を作成します。 これにより、ラボ環境で、使用される可能性のあるデバイスの[サイト システムのスケール](../plan-design/configs/size-and-scale-numbers.md)の管理をサポートできます。  
この処理中、Configuration Manager コンソールもインストールします。このコンソールは、今後評価版のデバイスを管理するときに使用されます。  

インストールを開始する前に、Windows Server 2012 を使用してサーバー上で [Prerequisite Checker](../servers/deploy/install/prerequisite-checker.md) を起動して、すべての設定が正常に有効になっていることを確認します。  

#### <a name="to-download-and-install-configuration-manager"></a>構成マネージャーをダウンロードしてインストールするには:  

1.  [System Center の評価](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) ページに移動して、最新の評価版 Configuration Manager をダウンロードします。  

2.  定義済みの場所でダウンロード メディアを解凍します。  

3.  「[Configuration Manager のセットアップ ウィザードを使用してサイトをインストールする](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md)」のインストール手順に従います。 この手順で、次の情報を入力します。  

    |サイトのインストール手順|選択内容|  
    |-----------------------------------------|---------------|  
    |手順 4. **[プロダクト キー]** ページ|**[評価]** を選択します。|  
    |手順 7: **必須ファイルのダウンロード**|**[必須ファイルをダウンロード]** を選択し、定義済みの場所を指定します。|  
    |手順 10: **サイトとインストールの設定**|-   **サイト コード:LAB**<br />-   **サイト名:Evaluation**<br />-   **インストール フォルダー:** 定義済みの場所を指定します。|  
    |手順 11: **プライマリ サイトのインストール**|**[プライマリ サイトをスタンドアロン サイトとしてインストール]** をクリックし、 **[次へ]** をクリックします。|  
    |手順 12:**データベースのインストール**|-   **SQL Server 名 (FQDN):** FQDN を入力します。<br />-   **インスタンス名:** 空白にして、前にインストールした SQL の既定のインスタンスを使用します。<br />-   **Service Broker ポート:** 既定のポート 4022 のままにします。|  
    |手順 13:**データベースのインストール**|これらの設定は既定値のままにします。|  
    |手順 14:**SMS プロバイダー**|これらの設定は既定値のままにします。|  
    |手順 15:**クライアント通信設定**|**[すべてのサイト システムの役割でクライアントからの HTTPS 通信のみ受け付ける]** がオンになっていないことを確認します。|  
    |手順 16:**サイト システムの役割**|FQDN を入力し、 **[すべてのサイト システムの役割でクライアントからの HTTPS 通信のみ受け付ける]** がまだオフになっていることを確認します。|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a> Configuration Manager サイトで発行を有効にする  
各 Configuration Manager サイトは、サイト特有の情報を、Active Directory スキーマ上のドメイン パーティション内のそのサイトの System Management コンテナーに発行します。 このトラフィックは、Active Directory と Configuration Manager の間の通信用に双方向チャネルを開いて処理する必要があります。 さらに、フォレストの探索も有効にして、Active Directory とネットワーク インフラストラクチャの特定のコンポーネントを決定することもできます。  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Active Directory フォレストを発行用に構成するには  

1.  Configuration Manager コンソールの左下隅で、 **[管理]** をクリックします。  

2.  **[管理]** ワークスペースで、 **[階層の構成]** を展開し、 **[探索方法]** をクリックします。  

3.  **[Active Directory フォレストの探索]** をクリックし、 **[プロパティ]** をクリックします。  

4.  **[プロパティ]** ダイアログ ボックスで、 **[Active Directory フォレストの探索を有効にする]** をオンにします。 これがアクティブになったら、 **[探索時に Active Directory サイトの境界を自動的に作成する]** をオンにします。 ダイアログ ボックスが表示され、 **[今すぐ完全な探索を実行しますか?]** **[はい]** のインストールをサポートするコア コンポーネントがいくつか必要です。  

5.  画面上部の **[探索方法]** グループで、 **[今すぐフォレスト探索を実行する]** をクリックし、サイドバーの **[Active Directory フォレスト]** に移動します。 Active Directory フォレストは、検出されたフォレストの一覧に表示されます。  

6.  画面上部の **[全般]** タブに移動します。  

7.  **[管理]** ワークスペースで、 **[階層の構成]** を展開し、 **[Active Directory フォレスト]** をクリックします。  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Configuration Manager サイトが Active Directory フォレストにサイト情報を発行できるようにするには:  

1.  Configuration Manager コンソールで、 **[管理]** をクリックします。  

2.  まだ検出されていない新しいフォレストを構成します。  

3.  **[管理]** ワークスペースで **[Active Directory フォレスト]** をクリックします。  

4.  サイトのプロパティの **[発行]** タブで、接続されているフォレストを選択し、 **[OK]** をクリックします。