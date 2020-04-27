---
title: Technical Preview 1604 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1604 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1785880af8c7d0d106abfe3eea8ecd390f6ce6b1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074454"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Configuration Manager の Technical Preview 1604 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1604 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。      このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。  

 このバージョンでお試しいただける新機能を次に示します。  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a> ビジネス向け Windows ストアからの一括購入アプリの管理  
 [ビジネス向け Windows ストア](https://www.microsoft.com/business-store)は、組織向けのアプリを検索して、個別に、または一括で購入できる場所です。 ストアを Configuration Manager に接続すると、一括購入したアプリを Configuration Manager コンソールから管理できます。例を挙げます。  

-   購入したアプリの一覧を Configuration Manager に同期させることができます。  

-   同期されたアプリは Configuration Manager コンソールに表示され、他のすべてのアプリと同様に展開できます。  

-   使用可能なライセンスの数と、使用中の数を Configuration Manager コンソールで追跡できます。  

### <a name="try-it-out"></a>試してみましょう。  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>シナリオ 1 :ビジネス向け Windows ストアの同期の設定  

1.  Azure Active Directory で、"Web アプリケーションや Web API" 管理ツールとして Configuration Manager を登録します。 後で必要なクライアント ID が表示されます。  

    1.  [https://manage.windowsazure.com](https://manage.windowsazure.com) の **Active Directory** ノードで、Azure Active Directory を選択し、 **[アプリケーション]**  >  **[追加]** をクリックします。  

    2.  **[組織で開発中のアプリケーションを追加]** をクリックします。  

    3.  アプリケーションの名前を入力し、 **[Web アプリケーション]** または **[Web API]** 、あるいはその両方を選択し、次へ進む矢印をクリックします。  

    4.  **[サインオン URL]** と **[アプリケーション ID/URI]** の両方に同じ URL を入力します。  URL はあらゆるものを使用でき、実際のアドレスに解決する必要はありません。 たとえば、**https://&lt;yourdomain\>/sccm** を入力できます。  

    5.  ウィザードを完了します。  

2.  Azure Active Directory で、登録済み管理ツールのクライアント キーを作成します。  

    1.  作成したアプリケーションを強調表示し、 **[構成]** をクリックします。  

    2.  **[キー]** で、リストから期間を選択して、 **[保存]** をクリックします。  これにより、新しいクライアント キーが作成されます。  ビジネス向け Windows ストアを Configuration Manager に正常にオンボードするまで、このページから移動しないでください。  

3.  ビジネス向け Windows ストアで、ストア管理ツールとして Configuration Manager を構成します。  

    1.  [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) を開き、求められたらサインインします。  

    2.  要求された場合は、使用条件に同意します。  

    3.  **[管理ツール]** で、 **[Add a management tool]** (管理ツールを追加) をクリックします。  

    4.  **[Search for the tool by name]** (名前でツールを検索) で、先ほど AAD で作成したアプリケーションの名前を入力して、 **[追加]** クリックします。  

    5.  インポートしたアプリケーションの横にある **[アクティブ化]** をクリックします。  

    6.  オフラインでライセンスされるアプリケーションを購入する場合、**オフラインでライセンスされたアプリの表示**ウィザードで、 **[はい]** をクリックします。  

4.  ビジネス向け Windows ストアから少なくとも 1 つのアプリを購入します。  

5.  Configuration Manager コンソールの**管理**ワークスペースで、 **[Cloud Services]** を展開して、 **[ビジネス向け Windows ストア]** をクリックします。  

6.  **[ホーム]** タブの **[作成]** グループで、 **[ビジネス向け Windows ストア アカウントの追加]** をクリックします。  

7.  Azure Active Directory からテナント ID、クライアント ID、クライアント キーを追加し、ウィザードを完了します。  

8.  完了した時点で、Configuration Manager コンソールの **[ビジネス向け Windows ストア]** で構成されたアカウントが表示されます。  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>シナリオ 2 :ビジネス向け Windows ストアのオフライン ライセンス付きアプリから Configuration Manager アプリケーションを作成して展開します。  

1.  Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、 **[ストア アプリのライセンス情報]** をクリックします。  

2.  **[購入されたビジネス向け Windows ストア]** のリストにストアから同期されたアプリが一覧表示されます。 展開するアプリを選び、 **[ホーム]** タブの **[作成]** グループで、 **[アプリケーションの作成]** をクリックします。  

3.  ビジネス向け Windows ストアのアプリを含む Configuration Manager アプリケーションが作成されます。 他の Configuration Manager のアプリケーションと同様に、このアプリケーションを展開して監視できます。  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a> Microsoft Passport for Work 管理の機能強化  
 Configuration Manager クライアントで管理されたドメインに参加している Windows 10 デバイスに Passport for Work ポリシーを展開できるようになりました。  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a> クライアントが新しいソフトウェア更新ポイントに切り替えるためのオプション  
 1604 Technical Preview では、アクティブなソフトウェア更新ポイントに問題がある場合に、Configuration Manager クライアントが新しいソフトウェア更新ポイントに切り替えるためのオプションを有効にできます。 このオプションには、プライマリ サイトで利用可能な複数のソフトウェア更新ポイントが必要です。 デバイス コレクションでこのオプションを有効にします。有効にすると、コレクション内のクライアントは、次回のスキャンでアクティブなソフトウェアの更新ポイントへの接続に失敗したときに、別のソフトウェア更新ポイントを検索します。 WSUS の構成設定に応じて (更新プログラムの分類、製品など)、新しいソフトウェアの更新ポイントへの切り替えにより、追加のネットワーク トラフィックが発生します。 したがって、必要な場合に、このオプションのみを使用する必要があります。  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>ソフトウェア更新ポイントを切り替えるオプションを有効にするには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス] > [概要] > [デバイス コレクション]** に移動します。  

2.  **[ホーム]** タブの **[コレクション]** グループで、 **[クライアント通知]** をクリックして、 **[次のソフトウェアの更新ポイントに切り替える]** をクリックします。  

> [!NOTE]  
>  このオプションは、複数のソフトウェア更新ポイントを持つサイトでのみ使用できます。  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a> クライアント キャッシュ設定とクライアント ピア キャッシュを管理するためのクライアント設定  
 Technical Preview 1604 で、クライアントのキャッシュの使用に影響する 2 つの新しいデバイス クライアント設定が導入されています。 両方とも個別に使用できますが、クライアント設定の同じプロパティ シートで構成されており、リモートの場所のクライアントへのコンテンツの展開を管理するために役立つよう結合されます。  

-   1 つ目は、クライアントがローカル キャッシュから直接他のクライアントとコンテンツを共有するための組み込みの Configuration Manager ソリューションである、**クライアント ピア キャッシュ**です。 ピア キャッシュ クライアントがコンテンツを共有するには、同じ境界グループのメンバーである必要があります。 ピア キャッシュは、BracnchCache などのその他のソリューションの使用に取って代わるものではなく、並列動作し、配布ポイントなどの従来のコンテンツ展開ソリューションを拡張する他のオプションを提供します。  

     ピア キャッシュを有効にするクライアント設定をコレクションに展開すると、そのコレクションのメンバーはその境界グループ内の他のクライアントのピア コンテンツ ソースとして動作できます。  ピア コンテンツ ソースとして動作するクライアントは、管理ポイントにキャッシュされている利用可能なコンテンツの一覧を送信します。 これで、その境界グループ内の次のクライアントがそのコンテンツを要求すると、ピア キャッシュ ソースが潜在的なコンテンツのソースとして高速にするために構成されているすべての配布ポイントとともに提供されます。 クライアントは、コンテンツ ソースの結合されたこのプールから、任意のコンテンツ ソースを選択します。 クライアントは、高速な配布ポイントがないまたはピア キャッシュ ソースが境界グループ内に存在している場合に、遅くなるように構成されている配布ポイントからコンテンツのシークのみを行います。  

-   2 つ目の新しい設定により、クライアントの**キャッシュのサイズを管理**できます。 クライアントのドライブの領域に対する割合としてメガバイト単位の最大サイズを持つように、キャッシュを設定することができます。  クライアントは、先に到達した設定を適用します。  

クライアントが正常にクライアント ピア キャッシュの使用を把握しやすいように、**クライアント データ ソース** ダッシュボードを表示できます。 コンソールで、 **[監視] > [クライアント ステータス] > [Client Data Sources (クライアント データ ソース)]** に移動します。 ここで、ダッシュボードに適用する期間を選択できます。 次に、表示で、情報を表示する境界グループまたはパッケージを選択できます。 情報を表示しているときは、画面上にマウスを移動して、コンテンツまたはポリシーのソースのソースについての詳細を表示できます。  

 各境界グループのクライアント データ ソースの概要を表示する、新しいレポート 「**Client Data Sources - Summarization**」 (クライアント データ ソース - 概要) を使用することもできます。   
**ピア キャッシュを使用するための要件:**  

-   各クライアントのキャッシュ フォルダーに対する**フル コントロール**を持つ**ネットワーク アクセス アカウント**を使用してサイトを構成する必要があります。 これは、既定では、 **%windir%\ccmcache** です。  

-   クライアントは同じ境界グループのメンバーの場合にのみ、ピア キャッシュを使用して、コンテンツを転送できます。  

#### <a name="to-configure-client-peer-cache-client-settings"></a>クライアント ピア キャッシュのクライアント設定を構成するには  

1.  どちらの設定もクライアント設定の同じページで構成されます。 Configuration Manager コンソールで **[管理] > [クライアント設定]** に移動し、使用するデバイス クライアント設定オブジェクトを開きます。 既定のクライアント設定オブジェクトを変更することもできます。  

2.  使用可能な設定のリストから **[クライアント キャッシュ設定]** を選びます。  

3.  キャッシュのサイズを管理するには、 **[クライアント キャッシュ サイズを構成する]** を **[はい]** に設定します。 最大キャッシュ サイズをメガバイトとクライアント ドライブ領域の割合として構成することができます。  

4.  クライアントがクライアント ピア キャッシュに参加できるようにするには、 **[完全な OS 上の Configuration Manager クライアントにコンテンツの共有を許可する]** を **[はい]** に設定します。 これでクライアントが使用するポート (HTTP または HTTPS でも) を構成することができます。  

### <a name="try-it-out"></a>試してみましょう。  
 次のタスクを実行してから、このトピックの先頭付近にあるフィードバック情報を使用してその動作を報告してください。  

1.  クライアント設定を変更してクライアント キャッシュの新しいサイズを指定し、クライアントでこの設定を確認します。  

2.  クライアント設定を使用してピア キャッシュを使用する複数のクライアントを構成する  

3.  コンテンツをクライアントに展開して、一部またはほとんどのクライアントがピア キャッシュを使用して別のクライアントからそのコンテンツを取得できるようにします。  新しいダッシュ ボード表示することによって、使用されるコンテンツのソースを確認することができます。  

    > [!NOTE]  
    >  テクニカル プレビューと単一の配布ポイントに関するこのタスクを完了するには、すべてのクライアントのネットワークの場所で低速になるように配布ポイントを構成します。 その後、単一のクライアントにコンテンツを配布します。  そのクライアントがコンテンツを取得した後は、クライアントの場所から低速であると見なされる配布ポイントを使用する前に、コンテンツ ソースとして使用するローカルのピアを検索する別のクライアントにコンテンツを配布できます。  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a> KSP としての Passport for Work のサポート  
 Configuration Manager により、Microsoft Passport for Work を統合できます。これは Active Directory や Azure Active Directory アカウントを使った代替サインイン方法であり、パスワード、スマート カード、または仮想スマート カードに置き換わります。  
Passport を使用すると、パスワードの代わりにユーザー ジェスチャを使用してログインできます。 ユーザー ジェスチャには、単純な暗証番号 (PIN)、Windows Hello などの生体認証、または指紋リーダーなどの外部のデバイスがあります。  

-   Configuration Manager を使用して、ユーザーがログインに使用できるジェスチャと使用できないジェスチャを制御できます。また、PIN の複雑さの要件を構成できます。  

-   Passport for Work のキー格納プロバイダー (KSP) に認証証明書を格納できます。  

ユーザーが Passport の PIN を作成すると、Windows は、Configuration Manager がリッスンする通知を送信します。  これにより、Configuration Manager が、Passport の PIN を作成したユーザーをすぐに認識できるようになります。 その後、Passport が証明書プロファイルでのキー記憶域プロバイダーとして使用される場合に、Configuration Manager はそれらのユーザーに対して新しい証明書を発行することもできます。  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a> オンプレミスのデバイス正常性構成証明書  
 オンプレミスのインフラストラクチャを使用して通信するように、Windows 10 デバイスの正常性構成証明書を構成できるようになりました。  管理者は、報告がクラウドを使用して行われるか、オンプレミスのリソースを使用して行われるかを指定できます。  正常性構成証明書の報告に**オンプレミス**が選択されている場合、サービスに URI を指定することができます。 これにより、インターネット アクセスを使用しないクライアント PC が、正常性構成証明書を使用してデバイスを有効化および管理できるようになります。  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>オンプレミス デバイス正常性構成証明書の有効化  

1.  Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クライアント設定]** に移動し、 **[オンプレミスの正常性構成証明書サービスを使用]** を **[はい]** に設定します。  

2.  **[オンプレミスの正常性構成証明書サービスの URL]** を指定し、 **[OK]** をクリックします。  

これを試すには、クライアント エージェント設定を使用して、オンプレミスの正常性構成証明書サービスを構成します。  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a> Android デバイスの SmartLock 設定  
 新しい設定の **[Allow SmartLock and other trust agents]** \(SmartLock およびその他の信頼エージェントを許可) が **[Android and Samsung KNOX]** \(Android および Samsung KNOX) 構成項目に追加され、互換性のある Android デバイスで SmartLock 機能を制御することができます。 信頼エージェントとも呼ばれるこの電話機能では、デバイスが特定の Bluetooth デバイスに接続したときや、NFC タグの近くにある場合など、信頼できる場所にある場合、デバイスのロック画面のパスワードを無効化またはバイパスすることができます。 この設定を使用して、エンドユーザーが SmartLock を構成することを禁止できます。  
