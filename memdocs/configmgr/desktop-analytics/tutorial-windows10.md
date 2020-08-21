---
title: チュートリアル - Windows 10 の展開
titleSuffix: Configuration Manager
description: Desktop Analytics と Configuration Manager を使用したパイロット グループへの Windows 10 の展開に関するチュートリアル。
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 5c5337433b0d64ec1f6bf1efae97bd2391031f2e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694271"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>チュートリアル:Windows 10 のパイロット展開

このチュートリアルでは、Desktop Analytics と Configuration Manager を使用して、Windows 10 をパイロット グループに展開します。 オンプレミス製品に Windows を展開するための分析情報を提供するクラウド サービスの統合に焦点を当てています。 Desktop Analytics を使用して、パイロット グループに配置する最適なデバイスを決定します。 その後、Configuration Manager を使用して、Windows を最新のものにします。

このチュートリアルでは、以下を実行する方法について説明します。  

> [!div class="checklist"]  
> * Azure portal で Desktop Analytics をセットアップする  
> * Configuration Manager に接続し、デバイス設定を構成する  
> * Windows 10 用の Desktop Analytics 展開計画を作成する  
> * Configuration Manager を使用して、Windows 10 をパイロット グループに展開する  

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウント](https://azure.microsoft.com/free)を作成してください。 適切に構成すると、Desktop Analytics を使用しても Azure のコストは発生しません。

Desktop Analytics では、Azure サブスクリプション内の *Log Analytics ワークスペース*が使用されます。 ワークスペースは、基本的には、アカウント情報と、アカウントの単純な構成情報が含まれるコンテナーです。 詳しくは、[ワークスペースの管理](/azure/log-analytics/log-analytics-manage-access?toc=%2fazure%2fazure-monitor%2ftoc.json)に関するページをご覧ください。



## <a name="prerequisites"></a>[前提条件]

このチュートリアルを開始する前に、次の前提条件が満たされていることを確認します。  

- [**グローバル管理者**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)のアクセス許可を持つアクティブな Azure サブスクリプション  

    詳細については、[Desktop Analytics の前提条件](overview.md#prerequisites)に関する記事を参照してください。

- Configuration Manager バージョン 1902 以降、更新プログラムのロールアップ (4500571) あり、**完全な権限を持つ管理者**ロールあり  

- 最新バージョンの Windows 10 のインストール メディア

- 以下の構成の少なくとも 1 台の Windows 10 デバイス:  

    - Windows 10 バージョン 1709 以降。ただし、使用する予定のインストール メディアのバージョンよりも前のバージョン

    - 最新の Windows 10 累積的品質更新プログラム  

    - Configuration Manager クライアント バージョン 1902 以降、更新プログラムのロールアップ (4500571) あり  

- パイロット デバイスの Windows 診断データ レベルを **[省略可能 (制限あり)]** に構成するための業務上の承認  

    詳細については、[Desktop Analytics のプライバシー](privacy.md)に関する記事を参照してください。

- デバイスから次のインターネット エンドポイントへのネットワーク接続:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (Configuration Manager サーバー ロールのみ)
    - `https://*.manage.microsoft.com` (Configuration Manager サーバー ロールのみ)

    詳細については、「[Desktop Analytics のデータ共有を有効にする](enable-data-sharing.md#endpoints)」方法を参照してください。  

> [!Important]  
> これらの前提条件は、このチュートリアルを実行することを目的としています。 Desktop Analytics と Configuration Manager の一般的な前提条件の詳細については、「[前提条件](overview.md#prerequisites)」を参照してください。  



## <a name="set-up-desktop-analytics"></a>Desktop Analytics の設定

次の手順に従って、Desktop Analytics にサインインし、サブスクリプション内に構成します。 この手順は、組織のために Desktop Analytics をセットアップするための 1 回限りのプロセスです。  

1. Microsoft 365 デバイス管理で、**グローバル管理者**のアクセス許可を持つユーザーとして、[Desktop Analytics](https://aka.ms/desktopanalytics) ポータルを開きます。 **[スタート]** を選択します。  

2. **[サービス契約に同意する]** ページで、サービス契約を確認し、 **[同意する]** を選択します。  

3. **[サブスクリプションを確認してください]** ページの [必要な使用条件を満たしているライセンス] の一覧は、Desktop Analytics の Windows デバイスの正常性機能を対象にしています。 **[次へ]** を選択して続行します。  

4. **[ユーザーにアクセス許可を付与する]** ページで:

    - **[Allow Desktop Analytics to manage Directory roles on your behalf]\(Desktop Analytics による自動的なディレクトリ ロールの管理を許可する\)** :Desktop Analytics によって、**ワークスペースの所有者**に **Desktop Analytics 管理者**ロールが自動的に割り当てられます。 これらのグループが既に**グローバル管理者**である場合、変更はありません。  

        このオプションを選択しない場合でも、Desktop Analytics によって、セキュリティ グループのメンバーとしてユーザーが追加されます。 **グローバル管理者**が、ユーザーに **Desktop Analytics 管理者**ロールを手動で割り当てる必要があります。  

        Azure Active Directory での管理者ロールのアクセス許可の割り当てと、**Desktop Analytics 管理者**に割り当てられるアクセス許可の詳細については、「[Azure Active Directory での管理者ロールのアクセス許可](/azure/active-directory/users-groups-roles/directory-assign-admin-roles)」を参照してください。  

    - ワークスペースと展開計画を作成して管理するために、Desktop Analytics によって、 **[ワークスペースの所有者]** セキュリティ グループが Azure Active Directory 内に事前構成されます。 

        グループにユーザーを追加するには、 **[名前または電子メールアドレスを入力してください]** セクションに名前または電子メール アドレスを入力します。 完了したら **[次へ]** を選択します。

5. **[ワークスペースの設定]** ページで:  

    > [!Note]  
    > 次の手順を完了するには、**ワークスペースの所有者**のアクセス許可と、Azure サブスクリプションとリソース グループへの追加のアクセス権が必要です。 詳細については、「[前提条件](overview.md#prerequisites)」を参照してください。  

    - Azure サブスクリプションを選択します。  

    - 既存のワークスペースを Desktop Analytics で使用するには、それを選択し、次の手順に進みます。  

    - Desktop Analytics 用のワークスペースを作成するには、 **[ワークスペースの追加]** を選択します。  

        1. **[ワークスペース名]** を入力します。  

        2. **[Select the Azure subscription name for this workspace]\(このワークスペース用の Azure サブスクリプションの名前を選択する\)** ドロップダウン リストから、このワークスペース用の Azure サブスクリプションを選択します。  

        3. リソース グループを **[新規作成]** するか、 **[既存のものを使用]** します。  

        4. 一覧から **[リージョン]** を選択し、 **[追加]** を選択します。  

6. 新規または既存のワークスペースを選択し、 **[Set as Desktop Analytics workspace]\(Desktop Analytics ワークスペースとして設定\)** を選択します。  次に、 **[確認してアクセス権を付与する]** ダイアログで **[続行]** を選択します。  

7. 新しいブラウザーのタブで、サインインに使用するアカウントを選択します。 **[組織の代理として同意する]** オプションを選択し、 **[同意する]** を選択します。  


    > [!Note]  
    > この同意は、ワークスペース用の Log Analytics 閲覧者ロールを MALogAnalyticsReader アプリケーションに割り当てるためのものです。 このアプリケーション ロールは、Desktop Analytics で必要です。 詳細については、「[MALogAnalyticsReader アプリケーション ロール](troubleshooting.md#bkmk_MALogAnalyticsReader)」を参照してください。  

8. **[ワークスペースの設定]** ページに戻り、 **[次へ]** を選択します。  

9. **[最後の手順]** ページで、 **[Desktop Analytics に移動]** を選択します。 Azure portal に、Desktop Analytics の **[ホーム]** ページが表示されます。  



## <a name="connect-configuration-manager"></a>Configuration Manager を接続する

次の手順を使用して、Configuration Manager を更新し、Desktop Analytics に接続し、デバイス設定を構成します。 この手順は、階層をクラウド サービスにアタッチするための 1 回限りのプロセスです。  

### <a name="update-configuration-manager"></a>Configuration Manager の更新

Desktop Analytics との統合をサポートするには、Configuration Manager バージョン 1902 の更新プログラムのロールアップ (4500571) をインストールします。 この更新プログラムの詳細については、「[Configuration Manager Current Branch、バージョン 1902 の更新プログラムのロールアップ](https://support.microsoft.com/help/4500571)」を参照してください。

1. バージョン 1902 の更新プログラムのロールアップを使用してサイトを更新します。 詳細については、[コンソール内の更新プログラムのインストール](../core/servers/manage/install-in-console-updates.md)に関するページを参照してください。  

2. クライアントを更新します。 このプロセスを簡単にするには、自動クライアント アップグレードの使用を検討します。 詳細については、「[クライアントをアップグレードする](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)」をご覧ください。  


### <a name="connect-to-the-service"></a>サービスに接続する

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。 リボンの **[Azure サービスの構成]** を選択します。  

2. Azure サービス ウィザードの **[Azure サービス]** ページで、次の設定を構成します。  

    - Configuration Manager のオブジェクトの **[名前]** を指定します。  

    - サービスを識別するのに役立つ **[説明]** を指定します (省略可能)。  

    - 利用可能なサービスの一覧から **[Desktop Analytics]** を選択します。  
  
   **[次へ]** を選択します。  

3. **[アプリ]** ページで、適切な **[Azure 環境]** を選択します。 次に、Web アプリの **[参照]** を選択します。

4. Desktop Analytics 接続用の Azure AD アプリを簡単に追加するために、 **[作成]** を選択します。

5. **[サーバー アプリケーションの作成]** ウィンドウで、次の設定を構成します。  

    - **アプリケーション名**:Azure AD 内のアプリのフレンドリ名。

    - **ホームページ URL**:この値は Configuration Manager では使用されませんが、Azure AD で必要になります。 既定値は `https://ConfigMgrService` です。  

    - **アプリ ID URI**:この値は、Azure AD テナント内で一意である必要があります。 これは、サービスへのアクセスを要求するために Configuration Manager クライアントで使用されるアクセス トークンに含まれます。 既定値は `https://ConfigMgrService` です。  

    - **秘密鍵の有効期間**: ドロップダウン リストから、 **[1 年]** または **[2 年]** を選択します。 1 年が既定値です。  

    **[サインイン]** を選択します。 Azure への認証が正常に行われると、ページに参照用の **Azure AD テナント名**が表示されます。

    > [!Note]  
    > この手順は、**グローバル管理者**として実行してください。これらの資格情報は Configuration Manager では保存されません。 この管理者には Configuration Manager のアクセス許可は必要ありません。また、Azure サービス ウィザードを実行するアカウントと同じものである必要もありません。  

    **[OK]** を選択して Azure AD で Web アプリを作成し、サーバー アプリケーションの作成ダイアログを閉じます。 [サーバー アプリ] ダイアログで、 **[OK]** を選択します。 次に、Azure サービス ウィザードの **[アプリ]** ページで、[次へ] を選択します。  

6. **[診断データ]** ページで、次の設定を構成します。  

    - **商用 ID**: この値には、組織の ID が自動的に入力されます。  

    - **Windows 10 診断データ レベル**: 少なくとも **[省略可能 (制限あり)]** を選択します。  

    - **[診断データでデバイス名を許可する]** : **[有効にする]** を選択します。  
  
   **[次へ]** を選択します。 **[利用可能な機能]** ページには、前のページの診断データの設定で使用できる Desktop Analytics 機能が表示されます。 **[次へ]** を選択します。  

7. **[コレクション]** ページで、次の設定を構成します。  

    - **[表示名]** :Desktop Analytics ポータルでは、この Configuration Manager 接続が、この名前を使用して表示されます。 異なる階層を区別するために使用してください。 例: "*テスト ラボ*" や "*実稼働*"。  

    - **ターゲット コレクション**:このコレクションには、商用 ID と診断データの設定を使用して Configuration Manager によって構成されるすべてのデバイスが含まれます。 それは、Configuration Manager によって Desktop Analytics サービスに接続されるデバイスの完全なセットです。  

    - **ターゲット コレクション内のデバイスでは、送信方向の通信にユーザー認証済みプロキシが使用されます**:既定では、この値は **[いいえ]** です。 環境内で必要な場合は、 **[はい]** に設定します。  

    - **Desktop Analytics と同期する特定のコレクションを選択します**:追加のコレクションを指定するには、 **[追加]** を選択します。 これらのコレクションは、Desktop Analytics ポータルで展開計画を使用してグループ化するために使用できます。 パイロット コレクションとパイロット除外コレクションが含まれていることを確認してください。  

        これらのコレクションは、メンバーシップが変更されても引き続き同期されます。 たとえば、展開計画で、Windows 7 のメンバーシップ規則付きのコレクションを使用するとします。 これらのデバイスが Windows 10 にアップグレードされ、Configuration Manager によってコレクションのメンバーシップが評価されると、これらのデバイスはコレクションと展開計画から削除されます。  

8. ウィザードを完了します。  

Configuration Manager によって、ターゲット コレクション内にデバイスを構成するための設定ポリシーが作成されます。 このポリシーには、デバイスが Microsoft にデータを送信できるようにする診断データの設定が含まれています。 既定では、クライアントでのポリシーの更新は 1 時間ごとに行われます。 新しい設定を受信した後、Desktop Analytics でデータが使用可能になるまでに数時間以上かかる可能性があります。

> [!Note]  
> これらの設定の詳細については、「[Windows の設定](enroll-devices.md#windows-settings)」を参照してください。  

Desktop Analytics 用のデバイスの構成を監視します。 Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースにアクセスし、 **[Desktop Analytics サービス]** ノードを展開し、 **[接続の正常性]** ダッシュボードを選択します。  

接続の作成後、コレクションが、Configuration Manager によって 60 分以内に同期されます。 Desktop Analytics ポータルで、 **[グローバル パイロット]** にアクセスし、Configuration Manager デバイス コレクションを確認します。 ポータルの残りの部分に完全なデータが表示されるまでには 2、3 日かかる場合があります。 詳細については、「[データ待機時間](troubleshooting.md#data-latency)」をご覧ください。

## <a name="create-a-desktop-analytics-deployment-plan"></a>Desktop Analytics 展開計画を作成する

次の手順を使用して、Desktop Analytics で展開計画を作成します。

1. [Desktop Analytics](https://aka.ms/desktopanalytics) ポータルを開きます。 少なくとも**ワークスペースの共同作成者**のアクセス許可を持つ資格情報を使用します。  

2. [管理] グループの **[展開計画]** を選択します。  

3. **[展開計画]** ウィンドウで、 **[作成]** を選択します。  

4. **[展開プランを作成]** ウィンドウで、次の設定を構成します。  

    - **名前**:展開計画の一意の名前 (例: `Windows 10 pilot`)。  

    - **[製品とバージョン]** : 展開する Windows 10 のバージョンを選択します。 最新バージョンを使用する展開計画を作成することをお勧めします。

    - **[デバイス グループ]** : [Configuration Manager] タブで 1 つまたは複数のグループを選択し、 **[ターゲット グループとして設定]** を選択します。 これらのグループは、Configuration Manager から同期されるコレクションです。  

    - **準備ルール**:これらのルールは、どのデバイスがアップグレードの対象になるかを判断するのに役立ちます。 **[Windows OS]** を選択し、次の設定を構成します。  

        - **ドライバーを自動的に Windows Update から取得する**:既定の設定は **[オフ]** です。これは、Configuration Manager を使用して展開する場合に推奨される設定です。  

        - **アプリの低インストール数しきい値を定義します**:既定の設定は [`2%`] です。 このしきい値を下回るアプリには、自動的に " *[低インストール数]* " が設定されます。 パイロット中は、Desktop Analytics によるこれらのアドインの検証は行われません。  

            このしきい値よりも高い割合のコンピューターにアプリがインストールされている場合、展開計画では、アプリは " *[注目]* " とマークされます。 その後、パイロット フェーズ中にテストするための重要度を決定できます。  

    - **完了日**:その日までに対象となるすべてのデバイスに Windows を完全に展開する日付を選択します。  

5. **[作成]** を選択します。 新しい計画は、その処理中に展開計画の一覧に表示されます。 処理を早めるには、オンデマンドのデータ更新を要求します。 詳細については、「[Desktop Analytics の FAQ](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)を参照してください。

6. 展開計画を、その名前を選択して開きます。  

7. [展開計画] メニューの **[準備]** グループで、 **[重要度を指定]** を選択します。  

    1. **[アプリ]** タブで、 **[未プレビュー]** を選択して、プレビューされていない資産のみを表示します。  

    2. 各アプリを選択し、 **[編集]** を選択します。 複数のアプリを選択して、同時に編集できます。  

    3. **[重要度]** の一覧から重要度レベルを選択します。 パイロット中に Desktop Analytics でアプリを検証する場合は、 **[クリティカル]** または **[重要]** を選択します。 **[重要ではない]** とマークされたアプリは検証されません。 重要度レベルを割り当てるときは、その[互換性](compat-assessment.md)と他の計画の分析情報を評価します。  

        重要度レベルを割り当てるときに、アップグレードの決定を選択することもできます。  

    4. 完了したら **[保存]** を選択します。  

8. [展開計画] メニューの **[準備]** グループで、 **[パイロットの識別]** を選択します。  

    1. パイロット用に推奨されているデバイスを確認します。  

    2. 各デバイスを選択し、 **[パイロットに追加]** を選択します。 推奨に同意しない場合は、 **[置換]** を選択します。  

        Desktop Analytics によってこれらの推奨がどのように行われているかの詳細については、 **[パイロットの識別]** ウィンドウの右上隅にある情報アイコンを選択してください。



## <a name="deploy-windows-10-in-configuration-manager"></a>Configuration Manager で Windows 10 を展開する

次の手順を使用して、Configuration Manager で Windows 10 をパイロット グループに展開します。

- すでに所有していない場合は、最初に [Windows 10 用の OS アップグレード パッケージ](#bkmk_create-package)を作成します。  

- すでに所有していない場合は、[Windows 10 の OS アップグレード タスク シーケンス](#bkmk_create-ts)を作成します。  

- Desktop Analytics 展開計画を使用して[タスク シーケンス を展開](#bkmk_deploy-ts)します。  

- ソフトウェア センターからターゲット デバイス上に[タスク シーケンスをインストール](#bkmk_install-ts)します。  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a> Windows 10 の OS アップグレード パッケージを作成する

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[オペレーティング システム]** を展開して、 **[オペレーティング システム アップグレード パッケージ]** ノードを選択します。  

2. リボンの **[ホーム]** タブの **[作成]** グループで、 **[オペレーティング システム アップグレード パッケージの追加]** を選択します。 このアクションにより、オペレーティング システム アップグレード パッケージの追加ウィザードが開始されます。  

3. **[データ ソース]** ページで、OS アップグレード パッケージのインストール ソース ファイルのネットワーク **パス**を指定します。 たとえば、`\\server\share\path` となります。  

    > [!NOTE]  
    > インストール ソース ファイルには、OS をインストールするための setup.exe やその他のファイルとフォルダーが含まれています。  

4. **[全般]** ページで、OS アップグレード パッケージの一意の **[名前]** を指定します。  

5. オペレーティング システム アップグレード パッケージの追加ウィザードを完了します。  

#### <a name="distribute-content"></a>コンテンツの配布

次に、配布ポイントに OS アップグレード パッケージを配布します。  

1. 一覧から OS アップグレード パッケージを選択します。 リボンの **[ホーム]** タブの **[展開]** グループで、 **[コンテンツの配布]** を選択します。 コンテンツの配布ウィザードが開きます。  

2. **[全般]** ページで、一覧に表示されているコンテンツが配布対象のコンテンツであることを確認し、 **[次へ]** をクリックします。  

3. **[コンテンツの配布先]** ページで、 **[追加]** をクリックし、 **[配布ポイント]** をクリックします。 既存の配布ポイントを選択し、 **[OK]** をクリックします。 コンテンツの配布先の追加が完了したら、 **[次へ]** を選択します。  

4. コンテンツの配布ウィザードを完了します。  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a>Windows 10 の OS アップグレード タスク シーケンスを作成する

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[オペレーティング システム]** を展開して **[タスク シーケンス]** を選択します。  

2. リボンの **[ホーム]** タブにある **[作成]** グループで、 **[タスク シーケンスの作成]** を選択します。  

3. タスク シーケンスの作成ウィザードの **[新しいタスク シーケンスの作成]** ページで、 **[オペレーティング システムをアップグレード パッケージからアップグレードする]** を選択してから、 **[次へ]** を選択します。  

4. **[タスク シーケンス情報]** ページで、タスク シーケンスを識別する **[タスク シーケンス名]** を指定します。  

5. **[Windows オペレーティング システムのアップグレード]** ページで次の設定を指定し、 **[次へ]** をクリックします。  

    - **[アップグレード パッケージ]** :OS のアップグレードのソース ファイルを含むアップグレード パッケージを指定します。  

    - **[エディション インデックス]** :複数の OS のエディション インデックスをパッケージから入手できる場合、希望のエディション インデックスを選択します。 既定では、最初のインデックスが選択されます。  

    - **プロダクト キー**:インストールする OS の Windows プロダクト キーを指定します。 エンコードされたボリューム ライセンス キーまたは標準のプロダクト キーを指定します。 標準のプロダクト キーを使う場合は、5 つの各文字グループをダッシュ (-) で区切ります。 次に例を示します。*XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*。 ボリューム ライセンス版のアップグレードの場合、プロダクト キーは必要ないことがあります。  

        > [!Note]  
        > このプロダクト キーは、マルチ ライセンス認証キー (MAK) または汎用ボリューム ライセンス キー (GVLK) でもかまいません。 GVLK は、キー管理サービス (KMS) クライアント セットアップ キーとも呼ばれます。 詳細については、「[ボリューム ライセンス認証の計画](/windows/deployment/volume-activation/plan-for-volume-activation-client)」を参照してください。 KMS クライアント セットアップ キーの一覧については、Windows Server のライセンス認証ガイドの「[付録 A](/windows-server/get-started/kmsclientkeys)」を参照してください。

6. **[更新プログラムを含める]** ページで、 **[次へ]** を選択して、ソフトウェアの更新プログラムをインストールしないようにします。  

7. **[アプリケーションのインストール]** ページで、 **[次へ]** を選択して、アプリケーションをインストールしないようにします。

8. タスク シーケンスの作成ウィザードを完了します。  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a> Desktop Analytics 展開計画を使用してタスク シーケンス を展開する

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** に移動し、 **[Desktop Analytics サービス]** ノードを展開し、 **[展開計画]** ノードを選択します。  

2. 使用する Windows 10 パイロット展開計画を選択し、リボンの **[展開計画の詳細]** を選択します。  

3. **[パイロットの状態]** タイルで、ドロップダウン リストから **[タスク シーケンス]** を選択し、 **[展開]** を選択します。  

4. ソフトウェアの展開ウィザードの **[全般]** ページで、 **[ソフトウェア]**  フィールドの横にある **[参照]** を選択します。 Windows 10 のインプレース アップグレード タスク シーケンスを選択し、 **[次へ]** を選択します。  

    > [!Note]  
    > Desktop Analytics の統合により、Configuration Manager によって、展開計画用のパイロット コレクションと実稼働コレクションが自動的に作成されます。 これらのコレクションを使用できるようになる前に、それらが同期されるまでに時間がかかることがあります。 詳細については、[トラブルシューティング (データの遅延)](troubleshooting.md#data-latency)に関する記事を参照してください。<!-- 4984639 -->
    >
    > このコレクションは、Desktop Analytics 展開計画デバイス用に予約されています。 このコレクションに対する手動での変更はサポートされていません。<!-- 3866460, SCCMDocs-pr 3544 -->  

5. **[コンテンツ]** ページで、 **[追加]** をクリックし、 **[配布ポイント]** をクリックします。 インストール コンテンツをホストするために使用できる配布ポイントを選択し、 **[OK]** を選択します。 その後、 **[次へ]** を選択します。  

6. **[展開設定]** ページで、 **[次へ]** を選択して、既定の設定をそのまま使用します (利用可能なインストール)。  

7. **[Scheduling]\(スケジュール設定\)** ページで、 **[次へ]** を選択して、既定の設定をそのまま使用します (直ちに利用可能)。  

8. **[ユーザー エクスペリエンス]** ページで、 **[次へ]** を選択して、既定値をそのまま使用します (ソフトウェア センターに、コンピューターの再起動通知のみ表示されます)。  

9. **[アラート]** ページで、 **[次へ]** を選択して、既定の設定をそのまま使用します。  

10. ウィザードを完了します。  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a> ソフトウェア センターからタスク シーケンスをインストールする

1. パイロット展開計画のメンバーであるデバイスにサインインします。  

2. **ソフトウェア センター**を開き、Windows 10 の利用可能なオペレーティング システムをインストールします。  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>次のステップ

次の記事に進んで、Desktop Analytics の展開計画の詳細を確認します。
> [!div class="nextstepaction"]  
> [展開計画](about-deployment-plans.md)