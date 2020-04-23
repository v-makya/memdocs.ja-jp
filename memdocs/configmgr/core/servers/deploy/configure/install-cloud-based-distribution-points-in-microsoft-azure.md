---
title: クラウド配布ポイントのインストール
titleSuffix: Configuration Manager
description: 以下の手順を使用し、Configuration Manager でクラウド配布ポイントを設定します。
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30cd61240b09f821d8b18c37e6accc7450f35817
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701670"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Configuration Manager 用にクラウド配布ポイントをインストールする

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> Azure からコンテンツを共有するための実装が変更されました。 コンテンツが有効なクラウド管理ゲートウェイを使用します。その場合、 **[CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする]** オプションを有効にします。 詳細については、[CMG の変更](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg)に関するページを参照してください。
>
> 今後は、従来のクラウド配布ポイントを作成できなくなります。 詳細については、[削除された機能と非推奨の機能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。

この記事では、Microsoft Azure で Configuration Manager クラウド配布ポイントをインストールする手順を説明します。 次のセクションが含まれています。

- [始める前に](#bkmk_before)
- [設定](#bkmk_setup)
- [DNS の構成](#bkmk_dns)
- [サイト サーバーのプロキシの設定](#bkmk_proxy)
- [コンテンツの配布とクライアントの構成](#bkmk_client)
- [管理と監視](#bkmk_monitor)
- [変更](#bkmk_modify)
- [高度なトラブルシューティング](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a> 始める前に

最初に[クラウド配布ポイントの使用](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)に関する記事をお読みください。 この記事は、クラウド配布ポイントの計画と設計に役立ちます。

以下のチェックリストを使用し、クラウド配布ポイントの作成に必要な情報と前提条件が揃っていることを確認します。  

- サイト サーバーで Azure に接続できます。 お使いのネットワークでプロキシが使用されている場合、[サイト システムの役割を構成](#bkmk_proxy)します。  

- 使用する **Azure 環境**。 たとえば、Azure パブリック クラウドや Azure 米国政府クラウドです。  

- バージョン 1806 以降、および*推奨*。**Azure Resource Manager の展開**を使用します。 これには以下の要件があります。<!--1322209-->  

    - **クラウド管理**のための [Azure Active Directory](azure-services-wizard.md) との統合。 Azure AD のユーザー探索は必要ありません。  

    - Azure **サブスクリプション ID**。  

    - Azure **リソース グループ**。  

    - **サブスクリプション管理アカウント**では、ウィザードの途中でサインインする必要があります。  

- **サーバー認証証明書**。 .PFX ファイルとしてエクスポートされます。  

- クラウド配布ポイントでグローバルに一意な**サービス名**。  

    > [!TIP]  
    > このサービス名を使用するサーバー認証証明書を要求する前に、希望する Azure ドメイン名が一意であることを確認します。 たとえば、*WallaceFalls.CloudApp.Net* のようになります。
    >
    > 1. [Azure portal](https://portal.azure.com) にサインインします。
    > 1. **[すべてのリソース]** を選択してから、 **[追加]** を選択します。
    > 1. **[クラウド サービス]** を検索します。 **[作成]** を選択します。
    > 1. **[DNS 名]** フィールドに希望するプレフィックス (たとえば、*WallaceFalls*) を入力します。 ドメイン名が使用できるか、既に別のサービスで使用されているかがインターフェイスに表示されます。
    >
    > ポータルではサービスを作成しないでください。名前を利用できるかどうかはこのプロセスを利用して確認してください。

- この展開の Azure **リージョン**。  

- まだ Configuration Manager バージョン 1810 以前で Azure **クラシック サービス展開**を使用する必要がある場合は、次の要件が必要です。  

    > [!Important]  
    > バージョン 1810 以降では、Configuration Manager での Azure の従来のサービス展開は推奨されていません。 クラウド配布ポイント用の Azure Resource Manager の展開の使用を開始します。 詳細については、[Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager) に関するページを参照してください。  
    >
    > Configuration Manager バージョン 1902 以降、クラウド配布ポイントの新しいインスタンスに対しては、Azure Resource Manager が唯一の展開メカニズムです。<!-- 3605704 -->

    - Azure **サブスクリプション ID**。  

    - Azure **管理証明書**。 .CER ファイルと .PFX ファイルの両方としてエクスポートされます。 Azure サブスクリプション管理者が [Azure Portal](https://portal.azure.com) で .CER 管理証明書をサブスクリプションに追加する必要があります。  

### <a name="branchcache"></a>BranchCache

クラウド配布ポイントを有効にして Windows BranchCache を使用するには、サイト サーバーに BranchCache 機能をインストールします。<!-- SCCMDocs-pr#4054 -->

- サイト サーバーにオンプレミス配布ポイント サイト システム ロールが与えられている場合、そのロールのプロパティのオプションを構成し、**BranchCache を有効にして構成**します。 詳細については、[配布ポイントの構成](install-and-configure-distribution-points.md#bkmk_config-general)に関するページを参照してください。

- サイト サーバーに配布ポイント ロールがない場合、Windows に BranchCache 機能をインストールします。 詳細については、[BranchCache 機能のインストール](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature)に関するページを参照してください。

既にクラウド配布ポイントにコンテンツを配布し、BranchCache を有効にすることにしている場合、最初にこの機能をインストールします。 その後もう一度、クラウド配布ポイントにコンテンツを配布します。

> [!NOTE]  
> Configuration Manager バージョン 1810 以前では、クラウド配布ポイントが複数ある場合、BranchCache キー パスフレーズを手動で設定する必要があります。 詳細は、[Microsoft サポート KB 4458143](https://support.microsoft.com/help/4458143) を参照してください。

## <a name="set-up"></a><a name="bkmk_setup"></a> 設定  

サイトでこの手順を行い、自分の[デザイン](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology)によって決定されるこのクラウド配布ポイントをホストします。  

1. Configuration Manager コンソールで **[管理]** ワークスペースに進み、 **[クラウド サービス]** を展開して **[クラウド配布ポイント]** を選択します。 リボンの **[クラウド配布ポイントの作成]** を選択します。  

2. クラウドの配布ポイントの作成ウィザードの **[全般]** ページで、次の設定を構成します。  

    1. 最初に **Azure 環境**を指定します。  

    2. バージョン 1806 以降および*推奨*。展開方法として **[Azure Resource Manager の展開]** を選択します。 **[サインイン]** を選択し、Azure サブスクリプション管理者アカウントで認証を行います。 ウィザードは、Azure AD 統合の前提条件の間に格納された情報から、残りのフィールドを自動的に設定します。 複数のサブスクリプションを所有している場合は、使用する適切なサブスクリプションの**サブスクリプション ID** を選びます。  

    > [!Note]  
    > バージョン 1810 以降では、Configuration Manager での Azure の従来のサービス展開は推奨されていません。
    >
    > 従来のサービス展開を使用する必要がある場合は、このページでそのオプションを選択します。 まず、Azure **サブスクリプション ID** を入力します。 次に **[参照]** を選択し、Azure 管理証明書の .PFX ファイルを選びます。  

3. **[次へ]** を選択します。 サイトで Azure への接続テストが完了するまで待ちます。  

4. **[設定]** ページで、次の設定を指定して **[次へ]** を選択します。  

    - **地域**:クラウド配布ポイントを作成する Azure リージョンを選択します。  

    - **リソース グループ**: (Azure Resource Manager の展開方法のみ)  

        - **既存のものを使用**:ドロップダウン リストから既存のリソース グループを選択します。  

        - **新規作成**:お使いの Azure サブスクリプションで作成する新しいリソース グループ名を入力します。  

    - **プライマリ サイト**:この配布ポイントにコンテンツを配布するプライマリ サイトを選択します。

    - **証明書ファイル**: **[参照]** を選択し、このクラウド配布ポイントのサーバー認証証明書の .PFX ファイルを選びます。 この証明書からの共通名が必須の **[サービス FQDN]** フィールドと **[サービス名]** フィールドに入力されます。  

        > [!NOTE]  
        > クラウド配布ポイントのサーバー認証証明書ではワイルドカードがサポートされます。 ワイルドカード証明書を使用する場合、 **[サービス FQDN]** フィールドのアスタリスク (`*`) をサービスの適切なホスト名に置き換えます。  

5. **[アラート]** ページで、記憶域クォータ、転送クォータを設定し、Configuration Manage にアラートを生成させるそれぞれのクォータの使用率を指定します。 その後、 **[次へ]** を選択します。  

6. ウィザードを完了します。  

### <a name="monitor-installation"></a>インストールの監視  

サイトにより、クラウド配布ポイントの新しいホステッド サービスの作成が開始されます。 ウィザードを閉じると、Configuration Manager コンソールでクラウド配布ポイントのインストール進行状況を監視します。 プライマリ サイト サーバーで **CloudMgr.log** ファイルも監視します。 必要に応じて、Azure Portal でクラウド サービスのプロビジョニングを監視します。  

> [!NOTE]  
> Azure に新しい配布ポイントをプロビジョニングするのに最大 30 分かかる可能性があります。 **CloudMgr.log** ファイルにより、ストレージ アカウントがプロビジョニングされるまで、次のメッセージが繰り返されます。  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> ストレージ アカウントのプロビジョニング後、サービスが作成され、構成されます。  

### <a name="verify-installation"></a>インストールの検証

次の方法を使用し、クラウド配布ポイントのインストールが完了したことを確認します。  

- Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[クラウド サービス]** を展開し、 **[クラウド配布ポイント]** ノードを選択します。 一覧から新しいクラウド配布ポイントを見つけます。 [状態] 列が **[準備完了]** になっている必要があります。  

- Configuration Manager コンソールで、 **[監視]** ワークスペースに移動します。 **[システムのステータス]** を展開し、 **[コンポーネントのステータス]** ノードを選択します。 **SMS_CLOUD_SERVICES_MANAGER** コンポーネントからすべてのメッセージを表示し、ステータス メッセージ ID **9409** を探します。  

- 必要に応じて、Azure Portal に進みます。 クラウド配布ポイントの **[展開]** にステータス **[準備完了]** と表示されます。  


## <a name="configure-dns"></a><a name="bkmk_dns"></a> DNS の構成  

クライアントでクラウド配布ポイントを使用するには、Azure で管理される IP アドレスにクラウド配布ポイントの名前をクライアントで解決できる必要があります。 管理ポイントによりクライアントにクラウド配布ポイントの**サービス FQDN** が与えられます。 クラウド配布ポイントは Azure に**サービス名**として存在します。 クラウド配布ポイントのプロパティの **[設定]** タブでこれらの値を確認します。

> [!Note]  
> コンソールの **[クラウド配布ポイント]** ノードには、**サービス名**という名前の列が含まれますが、実際には**サービス FQDN** 値が表示されます。 両方の値を表示するには、クラウド配布ポイントの **[プロパティ]** を開き、 **[設定]** タブに切り替えます。  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

サーバー認証証明書の共通名には、お使いのドメイン名が含まれているはずです。 パブリック プロバイダーから証明書を購入するとき、この名前が必要になります。 PKI からこの証明書を発行するときに推奨されます。 たとえば、`WallaceFalls.contoso.com` となります。 クラウドの配布ポイントの作成ウィザードでこの証明書を指定すると、共通名が **[サービス FQDN]** プロパティに入力されます (`WallaceFalls.contoso.com`)。 **[サービス名]** には同じホスト名 (`WallaceFalls`) が入り、Azure ドメイン名に追加されます (`cloudapp.net`)。 このシナリオでは、クライアントでお使いのドメインの**サービス FQDN** (`WallaceFalls.contoso.com`) を Azure **サービス名**に解決する必要があります (`WallaceFalls.cloudapp.net`)。 これらの名前にマッピングする CNAME エイリアスを作成します。

### <a name="create-cname-alias"></a>CNAME エイリアスを作成する

組織で使用している、インターネットに接続するパブリック DNS で正規名レコード (CNAME) を作成します。 このレコードにより、Azure **サービス名**に、クライアントが受け取る、クラウド配布ポイントの**サービス FQDN** のエイリアスが作成されます。 たとえば、`WallaceFalls.contoso.com` の新しい CNAME レコードを `WallaceFalls.cloudapp.net` に作成します。  

### <a name="client-name-resolution-process"></a>クライアント名前解決プロセス

次のプロセスでは、クラウド配布ポイントの名前がクライアントで解決されるしくみを説明します。  

1. クライアントによって、コンテンツ ソース リストにあるクラウド配布ポイントの**サービス FQDN** が取得されます。 たとえば、`WallaceFalls.contoso.com` となります。  

2. DNS にクエリが実行されます。DNS により、CNAME エイリアスを利用してサービス FQDN が Azure **サービス名**に解決されます。 たとえば、`WallaceFalls.cloudapp.net` となります。  

3. DNS に再度クエリが実行されます。DNS により、Azure サービス名が Azure パブリック IP アドレスに解決されます。  

4. クライアントではこの IP アドレスを使用し、クラウド配布ポイントとの通信が開始されます。  

5. クラウド配布ポイントによりクライアントにサーバー認証証明書が提示されます。 クライアントでは、証明書の信頼チェーンが検証に使用されます。  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a> サイト サーバー プロキシの設定  

クラウド配布ポイントを管理するプライマリ サイト サーバーでは、Azure と通信する必要があります。 組織でプロキシ サーバーを使用してインターネット アクセスを制御している場合、このプロキシを使用するようにプライマリ サイト サーバーを構成します。  

詳細については、「[プロキシ サーバーのサポート](../../../plan-design/network/proxy-server-support.md)」を参照してください。  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a> コンテンツの配布とクライアントの構成

他のあらゆるオンプレミス配布ポイントと同じようにクラウド配布ポイントにコンテンツを配布します。 クライアントにより要求されたコンテンツが含まれていない限り、管理ポイントのコンテンツの場所リストにはクラウド配布ポイントが含まれません。 詳細については、[コンテンツの配布と管理](deploy-and-manage-content.md)に関するページをご覧ください。

他のあらゆるオンプレミス配布ポイントと同じようにクラウド配布ポイントを管理します。 これらのアクションには、配布ポイント グループへの割り当てとコンテンツ パッケージの管理が含まれます。 詳細については、[配布ポイントのインストールと構成](install-and-configure-distribution-points.md)に関するページを参照してください。

既定のクライアント設定により、自動的にクラウド配布ポイントをクライアントで使用できるようになります。 階層のすべてのクラウド配布ポイントへのアクセスは次のクライアント設定で制御します。  

- **[クラウド設定]** グループで、 **[クラウド配布ポイントへのアクセスを許可する]** という設定を変更します。  

    - 既定では、この設定は **[はい]** に設定されています。  

    - ユーザーとデバイスの両方でこの設定を変更し、展開します。  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a> 管理と監視  

他のあらゆるオンプレミス配布ポイントと同じようにクラウド配布ポイントに配布するコンテンツを監視します。 詳細については、[コンテンツの監視](monitor-content-you-have-distributed.md)に関するページを参照してください。

### <a name="alerts"></a><a name="bkmk_alerts"></a> アラート  

Configuration Manager では、Azure サービスを定期的にチェックします。 サービスがアクティブになっていない場合、あるいはサブスクリプションか証明書に問題がある場合、Configuration Manager によってアラートが生成されます。

クラウド配布ポイントに格納するデータの量と配布ポイントからクライアントによってダウンロードされるデータの量にしきい値を構成します。 クラウド サービスを停止または削除するタイミングを決定するとき、クラウド配布ポイントに保存するコンテンツを調整するとき、サービスを使用できるクライアントを変更するとき、これらのしきい値のアラートが役に立ちます。

- **記憶域のアラートしきい値**:記憶域のアラートしきい値では、クラウド配布ポイントに格納するデータ量またはコンテンツ量の上限を GB で設定します。 既定では、このしきい値は 2,000 GB です。 Configuration Manager によって、残りの空き領域が指定のレベルに達したときに警告アラートと重要なアラートが生成されます。 既定では、これらのアラートはしきい値の 50% と 90% で発生します。  

- **月単位の転送のアラートしきい値**:月単位の転送のアラートしきい値を使用すると、30 日間に配布ポイントからクライアントに転送されたコンテンツの量を監視できます。 既定では、このしきい値は 10,000 GB です。 このサイトでは、定義した値に転送が到達すると、警告アラートと重要なアラートが生成されます。 既定では、これらのアラートはしきい値の 50% と 90% で発生します。  

    > [!IMPORTANT]  
    > Configuration Manager は、データ転送を監視しますが、指定の転送のアラートしきい値を超えるデータ転送は停止しません。  

インストール中、クラウド配布ポイント別のしきい値を指定するか、クラウド配布ポイントのプロパティの **[アラート]** タブを使用します。  

> [!NOTE]  
> クラウド配布ポイントのアラートは、Azure からの使用量の統計情報によって異なります。また、アラートが利用できるようになるまでに、最大 24 時間かかる場合があります。 Azure の Storage Analytics に関する詳細については、「[Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/storage-analytics)」を参照してください。  

クラウド配布ポイントを監視するプライマリ サイトにより 1 時間ごとに Azure からトランザクション データがダウンロードされます。 このトランザクション データがサイト サーバーの `CloudDP-<ServiceName>.log` ファイルに保存されます。 Configuration Manager によって、この情報がストレージと比較評価され、各クラウド配布ポイントにクォータが転送されます。 警告アラートまたは重大なアラートに指定されている量にデータ転送が達した場合または超えた場合、Configuration Manager が該当するアラートを生成します。  

> [!WARNING]  
> サイトではデータ転送の情報は Azure から 1 時間ごとにダウンロードされるため、Configuration Manager でデータにアクセスしてアラートを生成する前に、使用量が警告または重大のしきい値を超える場合があります。  


## <a name="modify"></a><a name="bkmk_modify"></a> 変更

配布ポイントの概要は、Configuration Manager コンソールの **[管理]** ワークスペースにある **[クラウド サービス]** の **[クラウド配布ポイント]** ノードに表示されます。 配布ポイントを選択し、 **[プロパティ]** を選んで詳細を表示します。  

クラウド配布ポイントのプロパティを編集するときに、次のタブに編集する設定が含まれます。  

#### <a name="settings"></a>Settings

- **説明**  

- **証明書ファイル**: サーバー認証証明書が失効する前に、同じ共通名で新しい証明書を発行します。 次に、ここで新しい証明書を追加し、サービスで使用を開始します。 証明書が失効した場合、クライアントではサービスが信頼されず、使用されません。  

#### <a name="alerts"></a>アラート

ストレージと月単位の転送のアラートのデータしきい値を調整します。  

#### <a name="content"></a>Content

オンプレミス配布ポイントの場合と同様にコンテンツを管理します。  

### <a name="redeploy-the-service"></a>サービスの再展開

次の構成など、より重要な変更には、サービスの再展開が必要です。

- 従来の展開方法から Azure Resource Manager へ
- Subscription
- サービス名
- プライベートからパブリック PKI へ
- Azure リージョン

バージョン 1806 より、従来の展開方法で既存のクラウド配布ポイントを展開している場合、Azure Resource Manager の展開方法を使用するには、新しいクラウド配布ポイントを展開する必要があります。 次の 2 つのオプションがあります。

- 同じサービス名を再利用する場合:  

    1. 最初に、従来のクラウド配布ポイントを削除します。 クラウド配布ポイントが他にない場合、クライアントではコンテンツを取得できないことがあります。  

    2. Resource Manager デプロイを利用して新しいクラウド配布ポイントを作成します。 同じサーバー認証証明書を再利用します。  

    3. 新しいクラウド配布ポイントに必要なソフトウェア パッケージ コンテンツを配布します。  

- 新しいサービス名を使用する場合:  

    1. Resource Manager デプロイを利用して新しいクラウド配布ポイントを作成します。 新しいサーバー認証証明書を使用します。  

    2. 新しいクラウド配布ポイントに必要なソフトウェア パッケージ コンテンツを配布します。  

    3. 従来のクラウド配布ポイントを削除します。

> [!Tip]  
> クラウド配布ポイントの現在のデプロイ モデルを決定するには、次の手順を実行します。<!--SCCMDocs issue #611-->  
>
> 1. Configuration Manager コンソールで **[管理]** ワークスペースに進み、 **[クラウド サービス]** を展開して **[クラウド配布ポイント]** ノードを選択します。  
> 2. **デプロイ モデル**属性をリスト ビューに列として追加します。 Resource Manager のデプロイでは、この属性は **Azure Resource Manager** です。  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>クラウド サービスのオンデマンドの停止と開始

クラウド配布ポイントは Configuration Manager コンソールでいつでも停止できます。 このアクションを行った直後から、クライアントでは、サービスから追加のコンテンツをダウンロードできなくなります。 クライアントのためにアクセスを回復するには、Configuration Manager コンソールからクラウド サービスを再起動します。 たとえば、データのしきい値に達したとき、クラウド サービスを停止します。  

クラウド配布ポイントを停止したとき、クラウド サービスでコンテンツがストレージ アカウントから削除されることはありません。 サイト サーバーでクラウド配布ポイントへの追加コンテンツの転送が禁止されることもありません。 管理ポイントからは引き続き、有効なコンテンツ ソースとしてクライアントにクラウド配布ポイントが返されます。

次の手順を使用し、クラウド配布ポイントを停止します。  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[クラウド サービス]** を展開し、 **[クラウド配布ポイント]** ノードを選択します。  

2. クラウド配布ポイントを選択します。 Azure で実行されているクラウド サービスを停止するには、リボンの **[サービスの停止]** を選択します。  

3. クラウド配布ポイントを再開するには、 **[サービスの開始]** を選択します。  

### <a name="delete-a-cloud-distribution-point"></a>クラウド配布ポイントの削除

クラウド配布ポイントをアンインストールするには、Configuration Manager コンソールで配布ポイントを選択し、 **[削除]** を選択します。  

階層からクラウド配布ポイントを削除すると、Configuration Manager によって Azure のクラウド サービスからコンテンツが削除されます。

Azure でコンポーネントを手動で削除すると、システムが一貫性のない状態になります。 その場合、情報が孤立した状態のままになり、予期しない動作が発生する可能性があります。


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a> 高度なトラブルシューティング

クラウド配布ポイントに関する問題の解決に役立てる目的で Azure VM から診断ログを収集する必要がある場合、次の PowerShell サンプルを利用し、サブスクリプションのサービス診断拡張を有効にします。<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

次のサンプルは **diagnostics.wadcfgx** ファイルのレイです。上記の PowerShell スクリプトの **public_config** 変数で参照されています。 詳細については、[Azure Diagnostics 拡張機能の構成スキーマ](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema)に関するページを参照してください。  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
