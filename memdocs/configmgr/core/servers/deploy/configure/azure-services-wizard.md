---
title: Azure サービスの構成
titleSuffix: Configuration Manager
description: Configuration Manager 環境を、クラウド管理、ビジネス向け Microsoft Store、Log Analytics 用の Azure サービスと接続します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7cb0a2c71a3ea326348b87d6b34e3109a8ef9f20
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700131"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configuration Manager と共に使用するように Azure サービスを構成する

*適用対象:Configuration Manager (Current Branch)*

**Azure サービス ウィザード**を使用して、Configuration Manager で使用する Azure Cloud Services の構成プロセスを簡略化します。 このウィザードでは、Azure Active Directory (Azure AD) Web アプリ登録を使用して、一般的な構成エクスペリエンスが提供されます。 これらのアプリではサブスクリプションと構成の詳細が提供され、Azure AD との通信が認証されます。 アプリを利用することで、Azure で新しい Configuration Manager コンポーネントやサービスをセットアップするたびに同じ情報を入力する必要がなくなります。

## <a name="available-services"></a>利用可能なサービス

このウィザードを使用して、次の Azure サービスを構成します。  

- **クラウド管理**:このサービスでは、Azure AD を使用して、サイトとクライアントの認証を有効にします。 この認証により、次のような他のシナリオが有効になります。  

  - [認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](../../../clients/deploy/deploy-clients-cmg-azure.md)  

  - [Azure AD ユーザー探索を構成する](configure-discovery-methods.md#azureaadisc)  

  - [Azure AD ユーザー グループ探索を構成する](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - 特定の[クラウド管理ゲートウェイ シナリオ](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)をサポートする  

  - [アプリ承認のメール通知](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Log Analytics コネクタ**:[Azure Log Analytics に接続します](/azure/azure-monitor/platform/collect-sccm)。 コレクションのデータを Log Analytics に同期します。  

    > [!Note]  
    > この記事で "*Log Analytics コネクタ*" と呼んでいるものは、以前は "*OMS コネクタ*" という名前でした。 機能に違いはありません。 詳しくは、[Azure 管理の監視](/azure/azure-monitor/terminology#log-analytics)に関するページをご覧ください。  

- **ビジネス向け Microsoft Store**:[ビジネス向け Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) に接続します。 Configuration Manager で展開できる、組織のストア アプリを取得します。  

### <a name="service-details"></a>サービスの詳細

次の表に、各サービスの詳細を一覧表示します。  

- **テナント**:構成できるサービス インスタンスの数。 各インスタンスは個別の Azure AD テナントである必要があります。  

- **クラウド**:すべてのサービスでグローバル Azure クラウドがサポートされます。ただし、Azure 米国政府クラウドなどのプライベート クラウドは、すべてのサービスでサポートされるわけではありません。  

- **Web アプリ**:サービスで "*Web アプリ/API*" (Configuration Manager ではサーバー アプリともいう) の種類の Azure AD アプリを使用するかどうか。  

- **ネイティブ アプリ**:サービスで "*ネイティブ*" (Configuration Manager ではクライアント アプリともいう) の種類の Azure AD アプリを使用するかどうか。  

- **操作**:Configuration Manager Azure サービス ウィザードでこれらのアプリをインポートするか、作成するか。  

|サービス  |テナント  |クラウド  |Web アプリ  |ネイティブ アプリ  |操作  |
|---------|---------|---------|---------|---------|---------|
|クラウド管理<br>Azure AD 探索 | 複数 | パブリック、プライベート | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | インポート、作成 |
|Log Analytics コネクタ | 1 つ | パブリック、プライベート | ![サポート](media/green_check.png) | ![サポートされていません](media/Red_X.png) | インポート |
|Microsoft Store<br>Business | 1 つ | パブリック | ![サポート](media/green_check.png) | ![サポートされていません](media/Red_X.png) | インポート、作成 |

### <a name="about-azure-ad-apps"></a>Azure AD アプリについて

Azure サービスごとに異なる構成が必要になります。この構成は Azure Portal で行います。 さらに、各サービスのアプリには Azure リソースに対する別のアクセス許可が必要になる場合があります。  

複数のサービスに対して 1 つのアプリを使用することができます。 Configuration Manager と Azure AD で管理するオブジェクトは 1 つだけです。 アプリのセキュリティ キーの期限が切れた場合、更新する必要があるキーは 1 つだけです。

Configuration Manager は、ウィザードで追加の Azure サービスを作成する際に、サービス間で共通の情報を再利用するように設計されています。 この動作により、同じ情報を複数回入力する必要がなくなります。

サービスごとの必要なアプリのアクセス許可と構成の詳細については、「[利用可能なサービス](#available-services)」の関連する Configuration Manager の記事を参照してください。

Azure アプリの詳細については、まず、以下の記事を参照してください。

- [Azure App Service での認証および承認](/azure/app-service/app-service-authentication-overview)
- [Web Apps の概要](/azure/app-service-web/app-service-web-overview)
- [Azure AD でのアプリケーションの登録の基本](/azure/active-directory/develop/authentication-scenarios)  
- [Azure Active Directory テナントにアプリケーションを登録する](/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>始める前に

接続するサービスを決定したら、「[サービスの詳細](#service-details)」の表を参照してください。 この表には、Azure サービス ウィザードを完了するために必要な情報が示されています。 事前に Azure AD 管理者と話し合ってください。 次の操作のどれを実行するかを決めます。

- Azure ポータルで事前にアプリを手動で作成します。 次に、アプリの詳細を Configuration Manager にインポートします。  

- Configuration Manager を使用して、Azure AD でアプリを直接作成します。 Azure AD から必要なデータを収集する場合は、この記事の他のセクションの情報を確認してください。  

一部のサービスでは、Azure AD アプリに特定のアクセス許可を割り当てる必要があります。 各サービスの情報を確認して、必要なアクセス許可を判別してください。 たとえば、Web アプリをインポートする前に、Azure 管理者はまず、[Azure Portal](https://portal.azure.com) でそれを作成する必要があります。

Log Analytics コネクタを構成する場合は、関連するワークスペースを含むリソース グループに対して、新たに登録した Web アプリの "*共同作成者*" アクセス許可を付与します。 これにより、Configuration Manager からそのワークスペースへのアクセスが許可されます。 アクセス許可を割り当てるときは、Azure portal の **[ユーザーの追加]** 領域でアプリの登録名を検索します。 このプロセスは、[Log Analytics へのアクセス許可を Configuration Manager に提供する](/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics)場合と同じです。 Azure 管理者は、アプリを Configuration Manager にインポートする前に、これらのアクセス許可を割り当てる必要があります。

## <a name="start-the-azure-services-wizard"></a>Azure サービス ウィザードの起動

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。  

2. リボンの **[ホーム]** タブの **[Azure サービス]** グループで、 **[Azure サービスの構成]** を選択します。  

3. Azure サービス ウィザードの **[Azure サービス]** ページで、以下の操作を行います。  

    1. Configuration Manager でオブジェクトの**名前**を指定します。  

    2. 省略可能な**説明**を指定すれば、サービスを特定するのに役立ちます。  

    3. Configuration Manager に接続する Azure サービスを選択します。  

4. **[次へ]** を選択して、Azure サービス ウィザードの [Azure アプリのプロパティ](#azure-app-properties)のページに進みます。  

## <a name="azure-app-properties"></a>Azure アプリのプロパティ

Azure サービス ウィザードの**アプリ** ページで、まず、一覧から **[Azure 環境]** を選択します。 サービスで現在使用できる環境については、「[サービスの詳細](#service-details)」の表を参照してください。

アプリ ページの残りの部分は、サービスによって異なります。 サービスで使用されるアプリの種類や、使用できる操作については、「[サービスの詳細](#service-details)」の表を参照してください。

- アプリでインポートと作成の両方の操作がサポートされている場合は、 **[参照]** を選択します。 この操作で、[サーバー アプリのダイアログ](#server-app-dialog)または[クライアント アプリのダイアログ](#client-app-dialog)が開きます。  

- アプリでインポート操作のみがサポートされている場合は、 **[インポート]** を選択します。 この操作で、[アプリのインポート ダイアログ (サーバー)](#import-apps-dialog-server) または[アプリのインポート ダイアログ (クライアント)](#import-apps-dialog-client) が開きます。

このページでアプリを指定した後、 **[次へ]** を選択して、Azure サービス ウィザードの [[構成] または [探索]](#configuration-or-discovery) ページに進みます。

### <a name="web-app"></a>Web アプリ

このアプリは、Azure AD の種類の *Web アプリ/API* (Configuration Manager ではサーバー アプリともいう) です。

#### <a name="server-app-dialog"></a>サーバー アプリのダイアログ

Azure サービス ウィザードのアプリ ページで **[Web アプリ]** の **[参照]** を選択すると、サーバー アプリのダイアログが開きます。 ここには、既存の Web アプリの以下のプロパティを示す一覧が表示されます。

- テナントのフレンドリ名
- アプリのフレンドリ名
- サービスの種類

サーバー アプリのダイアログから実行できる以下の 3 つの操作があります。

- 既存の Web アプリを再利用するには、一覧から選択します。
- **[インポート]** を選択して、[アプリのインポート ダイアログ](#import-apps-dialog-server)を開きます。
- **[作成]** を選択して、[サーバー アプリケーションの作成ダイアログ](#create-server-application-dialog)を開きます。

選択した後、Web アプリをインポートまたは作成し、 **[OK]** を選択してサーバー アプリのダイアログを閉じます。 この操作で、Azure サービス ウィザードの[アプリ ページ](#azure-app-properties)に戻ります。

#### <a name="import-apps-dialog-server"></a>アプリのインポート ダイアログ (サーバー)

Azure サービス ウィザードのサーバー アプリのダイアログまたはアプリ ページで **[インポート]** を選択すると、アプリのインポート ダイアログが開きます。 このページでは、Azure Portal で既に作成されている Azure AD Web アプリに関する情報を入力できます。 Configuration Manager にその Web アプリに関するメタデータがインポートされます。 次の情報を指定します。

- **[Azure AD テナント名]** : Azure AD テナントの名前。
- **[Azure AD テナント ID]** : Azure AD テナントの GUID。
- **アプリケーション名**:アプリのフレンドリ名。アプリ登録の表示名。
- **クライアント ID**: アプリ登録の**アプリケーション (クライアント) ID** 値。 形式は標準の GUID です。
- **[秘密キー]** : Azure AD にアプリを登録するときに、秘密鍵をコピーする必要があります。
- **秘密鍵の有効期限**:カレンダーから未来の日付を選択します。
- **アプリ ID URI**:この値は、Azure AD テナント内で一意である必要があります。 これは、サービスへのアクセスを要求するために Configuration Manager クライアントで使用されるアクセス トークンに含まれます。 値は、Azure AD ポータルのアプリ登録エントリの**アプリケーション ID URI** です。 形式は `https://ConfigMgrService` に似ています。

情報を入力した後、 **[確認]** を選択します。 次に **[OK]** を選択して、アプリのインポート ダイアログを閉じます。 この操作で、Azure サービス ウィザードの[アプリ ページ](#azure-app-properties)、または[サーバー アプリのダイアログ](#server-app-dialog)に戻ります。

> [!TIP]
> アプリを Azure AD に登録するときに、必要に応じて **[リダイレクト URI]** に `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>` を手動で指定します。 アプリのクライアント ID GUID を指定します (例: `ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49`)。<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>サーバー アプリケーションの作成ダイアログ

サーバー アプリのダイアログで **[作成]** を選択すると、サーバー アプリケーションの作成ダイアログが開きます。 このページでは、Azure AD での Web アプリの作成が自動化されます。 次の情報を指定します。

- **アプリケーション名**:アプリのフレンドリ名。
- **ホームページ URL**:この値は Configuration Manager では使用されませんが、Azure AD で必要になります。 既定値は `https://ConfigMgrService` です。  
- **アプリ ID URI**:この値は、Azure AD テナント内で一意である必要があります。 これは、サービスへのアクセスを要求するために Configuration Manager クライアントで使用されるアクセス トークンに含まれます。 既定値は `https://ConfigMgrService` です。  
- **秘密鍵の有効期間**: ドロップダウン リストから、 **[1 年]** または **[2 年]** を選択します。 1 年が既定値です。

**[サインイン]** を選択して、管理ユーザーとして Azure への認証を行います。 これらの資格情報は Configuration Manager では保存されません。 この管理者には Configuration Manager のアクセス許可は必要ありません。また、Azure サービス ウィザードを実行するアカウントと同じものである必要もありません。 Azure への認証が正常に行われると、ページに参照用の **Azure AD テナント名**が表示されます。

**[OK]** を選択して Azure AD で Web アプリを作成し、サーバー アプリケーションの作成ダイアログを閉じます。 この操作で、[サーバー アプリのダイアログ](#server-app-dialog)に戻ります。

> [!NOTE]
> Azure AD の条件付きアクセス ポリシーを定義してあり、**すべてのクラウド アプリ**に適用する場合は、このポリシーから、作成したサーバー アプリケーションを除外する必要があります。 特定のアプリを除外する方法の詳細については、「[Azure AD 条件付きアクセスのドキュメント](/azure/active-directory/conditional-access/)」を参照してください。

### <a name="native-client-app"></a>ネイティブ クライアント アプリ

このアプリは、Azure AD の種類の*ネイティブ* (Configuration Manager ではクライアント アプリともいう) です。

#### <a name="client-app-dialog"></a>クライアント アプリのダイアログ

Azure サービス ウィザードのアプリ ページで **[ネイティブ クライアント アプリ]** の **[参照]** を選択すると、クライアント アプリのダイアログが開きます。 ここには、既存のネイティブ アプリの以下のプロパティを示す一覧が表示されます。

- テナントのフレンドリ名
- アプリのフレンドリ名
- サービスの種類

クライアント アプリのダイアログから実行できる以下の 3 つの操作があります。

- 既存のネイティブ アプリを再利用するには、一覧から選択します。 
- **[インポート]** を選択して、[アプリのインポート ダイアログ](#import-apps-dialog-client)を開きます。
- **[作成]** を選択して、[クライアント アプリケーションの作成ダイアログ](#create-client-application-dialog)を開きます。

選択した後、ネイティブ アプリをインポートまたは作成し、 **[OK]** を選択してクライアント アプリのダイアログを閉じます。 この操作で、Azure サービス ウィザードの[アプリ ページ](#azure-app-properties)に戻ります。

#### <a name="import-apps-dialog-client"></a>アプリのインポート ダイアログ (クライアント)

クライアント アプリのダイアログで **[インポート]** を選択すると、アプリのインポート ダイアログが開きます。 このページでは、Azure Portal で既に作成されている Azure AD ネイティブ アプリに関する情報を入力できます。 Configuration Manager にそのネイティブ アプリに関するメタデータがインポートされます。 次の情報を指定します。

- **アプリケーション名**:アプリのフレンドリ名。
- **クライアント ID**: アプリ登録の**アプリケーション (クライアント) ID** 値。 形式は標準の GUID です。

情報を入力した後、 **[確認]** を選択します。 次に **[OK]** を選択して、アプリのインポート ダイアログを閉じます。 この操作で、[クライアント アプリのダイアログ](#client-app-dialog)に戻ります。

#### <a name="create-client-application-dialog"></a>クライアント アプリケーションの作成ダイアログ

クライアント アプリのダイアログで **[作成]** を選択すると、クライアント アプリケーションの作成ダイアログが開きます。 このページでは、Azure AD のネイティブの作成が自動化されます。 次の情報を指定します。

- **アプリケーション名**:アプリのフレンドリ名。
- **応答 URL**:この値は Configuration Manager では使用されませんが、Azure AD で必要になります。 既定値は `https://ConfigMgrService` です。

**[サインイン]** を選択して、管理ユーザーとして Azure への認証を行います。 これらの資格情報は Configuration Manager では保存されません。 この管理者には Configuration Manager のアクセス許可は必要ありません。また、Azure サービス ウィザードを実行するアカウントと同じものである必要もありません。 Azure への認証が正常に行われると、ページに参照用の **Azure AD テナント名**が表示されます。

**[OK]** を選択して Azure AD でネイティブ アプリを作成し、クライアント アプリケーションの作成ダイアログを閉じます。 この操作で、[クライアント アプリのダイアログ](#client-app-dialog)に戻ります。

## <a name="configuration-or-discovery"></a>[構成] または [探索]

アプリ ページで Web アプリとネイティブ アプリを指定した後、Azure サービス ウィザードは、接続しているサービスに応じて、 **[構成]** ページまたは **[探索]** ページに進みます。 このページの詳細はサービスによって異なります。 詳細については、以下の記事のいずれかを参照してください。  

- **クラウド管理**サービス、 **[探索]** ページ:[Azure AD ユーザー探索を構成する](configure-discovery-methods.md#azureaadisc)  

- **Log Analytics コネクタ** サービス、 **[構成]** ページ:[Log Analytics への接続を構成する](/azure/azure-monitor/platform/collect-sccm)  

- **ビジネス向け Microsoft Store** サービス、 **[構成]** ページ:[ビジネス向け Microsoft Store の同期を構成する](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

最後に、[概要]、[進行状況]、および [完了] の各ページを使用して Azure サービス ウィザードを完了します。 Configuration Manager での Azure サービスの構成が完了しました。 他の Azure サービスを構成する場合にも、この手順を繰り返します。

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a>秘密鍵を更新する

有効期限が切れる前に、Azure AD アプリの秘密鍵を更新する必要があります。 鍵の有効期限が切れると、Configuration Manager で Azure AD での認証が行えず、これにより、接続された Azure サービスの動作が停止します。

バージョン 2006 以降では、Configuration Manager コンソールにより、次のような場合に通知が表示されます。<!--6386392-->

- 1 つ以上の Azure AD アプリの秘密鍵の有効期限が間もなく切れる
- 1 つ以上の Azure AD アプリの秘密鍵が期限切れになっている

両方の場合を軽減するには、秘密鍵を更新します。

これらの通知を操作する方法の詳細については、「[Configuration Manager コンソールの通知](../../manage/admin-console-notifications.md)」を参照してください。

### <a name="renew-key-for-created-app"></a>作成済みのアプリのキーを更新する

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[クラウド サービス]** を展開して **[Azure Active Directory テナント]** ノードを選択します。

1. 詳細ウィンドウで、アプリの Azure AD テナントを選択します。

1. リボンで、 **[秘密鍵を更新する]** を選択します。 アプリ所有者または Azure AD 管理者の資格情報を入力します。

### <a name="renew-key-for-imported-app"></a>インポート済みアプリのキーを更新する

Configuration Manager で Azure アプリをインポートした場合は、Azure portal を使用して更新します。 新しい秘密鍵と有効期限日をメモします。 **[秘密鍵を更新する]** ウィザード上にこの情報を追加します。  

> [!NOTE]
> Azure アプリケーション プロパティの **[キー]** ページを閉じる前に、秘密鍵を保存します。 この情報は、ページを閉じると削除されます。

## <a name="view-the-configuration-of-an-azure-service"></a>Azure サービスの構成を表示する

構成した Azure サービスのプロパティを表示します。 Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[Azure サービス]** を選択します。 表示または編集するサービスを選択し、 **[プロパティ]** を選びます。

サービスを選択し、リボンの **[削除]** を選んだ場合、この操作で Configuration Manager の接続が削除されます。 Azure AD のアプリは削除されません。 不要になったときにアプリを削除する場合は、Azure 管理者に依頼してください。 または、Azure サービス ウィザードを実行してアプリをインポートします。<!--483440-->

## <a name="cloud-management-data-flow"></a>クラウド管理データ フロー

次の図は、Configuration Manager、Azure AD、および接続されているクラウド サービス間の相互作用の概念を表すデータ フローです。 この特定の例では、Windows 10 クライアント、およびサーバー アプリとクライアント アプリの両方を含む、**クラウド管理**サービスを使用します。 他のサービスのフローもこれと似ています。

![Azure AD とクラウド管理を含む Configuration Manager のデータ フロー図](media/aad-auth.png)

1. Configuration Manager 管理者は、Azure AD でクライアント アプリとサーバー アプリをインポートまたは作成します。  

2. Configuration Manager の Azure AD ユーザー探索が実行されます。 サイトでは Azure AD サーバー アプリ トークンを使用して、Microsoft グラフでユーザー オブジェクトを照会します。  

3. サイトにはユーザー オブジェクトに関するデータが格納されます。 詳細については、「[Azure AD ユーザー探索](about-discovery-methods.md#azureaddisc)」を参照してください。  

4. Configuration Manager クライアントは Azure AD ユーザー トークンを要求します。 クライアントは Azure AD クライアント アプリのアプリケーション ID、および対象となるサーバー アプリを使用して要求を行います。 詳細については、「[Azure AD のセキュリティ トークンの要求](/azure/active-directory/develop/authentication-scenarios#security-tokens)」を参照してください。  

5. クライアントは、Azure AD トークンをクラウド管理ゲートウェイおよびオンプレミスの HTTPS が有効な管理ポイントに提示して、サイトで認証を行います。  

詳細については、「[Azure AD の認証ワークフロー](../../../clients/manage/azure-ccmsetup.md)」を参照してください。