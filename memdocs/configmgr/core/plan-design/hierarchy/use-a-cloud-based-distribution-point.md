---
title: クラウド配布ポイント
titleSuffix: Configuration Manager
description: Configuration Manager でクラウド配布ポイントを使用して、Microsoft Azure を通じてソフトウェア コンテンツを配布するための計画と設計を行います。
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7a14b79a9e7fd91b6470836b4271a669725065bd
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771169"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Configuration Manager でクラウド配布ポイントを使用する

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> Azure からコンテンツを共有するための実装が変更されました。 コンテンツが有効なクラウド管理ゲートウェイを使用します。その場合、 **[CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする]** オプションを有効にします。 詳細については、[CMG の変更](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg)に関するページを参照してください。
>
> 今後は、従来のクラウド配布ポイントを作成できなくなります。 詳細については、[削除された機能と非推奨の機能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。

クラウド配布ポイントとは、Microsoft Azure でプラットフォームとしてのサービス (PaaS) としてホストされている Configuration Manager 配布ポイントです。 このサービスは次のシナリオをサポートします。  

- オンプレミス インフラストラクチャを増やすことなく、インターネットベースのクライアントにソフトウェアのコンテンツを提供する  

- コンテンツ配布システムをクラウド対応にする  

- 従来の配布ポイントの必要性を減らす  

この記事は、クラウド配布ポイントについて説明し、その使用の計画および実装の設計について説明します。 次のセクションが含まれています。

- [機能と利点](#bkmk_features)
- [トポロジ設計](#bkmk_topology)
- [Requirements](#bkmk_requirements)
- [仕様](#bkmk_spec)
- [コスト](#bkmk_cost)
- [パフォーマンスと拡張性](#bkmk_perf)
- [ポートとデータ フロー](#bkmk_dataflow)
- [証明書](#bkmk_certs)
- [よく寄せられる質問 (FAQ)](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a> 機能と利点

### <a name="features"></a>機能

クラウド配布ポイントは、オンプレミスの配布ポイントでも提供される次のような機能をサポートします。  

- クラウド配布ポイントを個別に、または配布ポイント グループのメンバーとして管理する  

- クラウド配布ポイントを代替のコンテンツの場所として使用する  

- イントラネットおよびインターネットベースの両方のクライアントをサポートする  

### <a name="benefits"></a>利点

クラウド配布ポイントのその他の利点は、次のとおりです。  

- コンテンツは、サイトで暗号化されてから、Azure のクラウド配布ポイントに送信されます。  

- クライアントによるコンテンツ要求の需要の変化に対応するため、Azure でクラウド サービスの規模を手動で調節します。 このアクションでは、Configuration Manager に追加の配布ポイントをインストールしてプロビジョニングする必要はありません。  

- Windows BranchCache や代替のコンテンツ プロバイダーなど、他のコンテンツ テクノロジ用に構成されたクライアントからのコンテンツのダウンロードをサポートしています。  

- バージョン 1806 以降では、プル配布ポイントのソースの場所としてクラウド配布ポイントを使用します。  


## <a name="topology-design"></a><a name="bkmk_topology"></a> トポロジ設計

クラウド配布ポイントの展開と操作には、次のコンポーネントが含まれます。  

- Azure の**クラウド サービス**。 サイトによりコンテンツがこのサービスに配布され、サービスによって Azure クラウド ストレージに格納されます。 管理ポイントでは、必要に応じて使用可能なソースの一覧でこのコンテンツの場所をクライアントに提供します。  

- **管理ポイント** サイト システム ロールは通常のようにクライアント要求にサービスを提供します。  

    - オンプレミスのクライアントは、通常、オンプレミスの管理ポイントを使用します。  

    - インターネットベースのクライアントは、[クラウド管理ゲートウェイ](../../clients/manage/cmg/plan-cloud-management-gateway.md)、または[インターネットベースの管理ポイント](../../clients/manage/plan-internet-based-client-management.md)のいずれかを使用します。  

- クラウド配付ポイントでは、**証明書ベースの HTTPS** Web サービスを使用し、クライアントとのネットワーク通信をセキュリティで保護します。 クライアントは、この証明書を信頼する必要があります。  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
バージョン 1806 以降では、**Azure Resource Manager** の展開を使用して、クラウド配布ポイントを作成します。 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) は、[リソース グループ](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)と呼ばれる単一のエンティティとしてすべてのソリューション リソースを管理するための最新のプラットフォームです。 Azure Resource Manager でクラウド配布ポイントを展開するとき、サイトは Azure Active Directory (Azure AD) を使って必要なクラウド リソースの認証と作成を行います。 この最新の展開では、従来の Azure 管理証明書は必要ありません。  

> [!Note]  
> この機能では、Azure クラウド サービス プロバイダー (CSP) のサポートは有効になりません。 Azure Resource Manager でのクラウド配布ポイントの展開では引き続き従来のクラウド サービスが使われ、CSP はこれをサポートしません。 詳細については、「[Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)」(Azure CSP で使用可能な Azure サービス) を参照してください。  

Configuration Manager バージョン 1902 以降、クラウド配布ポイントの新しいインスタンスに対しては、Azure Resource Manager が唯一の展開メカニズムです。 既存の展開は引き続き機能します。<!-- 3605704 -->

Configuration Manager バージョン 1810 以前のクラウド配布ポイント ウィザードでは、Azure 管理証明書を使う**従来のサービス展開**のためのオプションがまだ提供されています。 リソースの展開と管理を簡単にするため、すべての新しいクラウド配布ポイントに Azure Resource Manager デプロイ モデルを使用してください。 可能であれば、Resource Manager で既存のクラウド配布ポイントを再展開してください。

> [!Important]  
> バージョン 1810 以降では、Configuration Manager での Azure の従来のサービス展開の使用は推奨されていません。 このバージョンが、これらの Azure の展開の作成がサポートされる最後のものとなります。 この機能は、将来の Configuration Manager バージョンで削除されます。<!--SCCMDocs-pr issue #2993-->  

Configuration Manager では、既存の従来のクラウド配布ポイントが Azure Resource Manager デプロイ モデルに移行されることはありません。 Azure Resource Manager の展開を使用して新しいクラウド配布ポイントを作成してから、従来のクラウド配布ポイントを削除してください。

### <a name="hierarchy-design"></a>階層の設計

クラウド配布ポイントを作成する場所は、クライアントがアクセスする必要があるコンテンツに依存します。 バージョン 1806 以降では、3 種類のクラウド配布ポイントがあります。  

- Azure Resource Manager の展開: この種類はプライマリ サイトまたは中央管理サイトで作成します。  

- 従来のサービス展開: この型はプライマリ サイトでのみ作成します。  

- クラウド管理ゲートウェイも、クライアントにコンテンツを提供することができます。 この機能により、Azure VM の必要な証明書とコストが削減されます。 詳細については、「[クラウド管理ゲートウェイの計画](../../clients/manage/cmg/plan-cloud-management-gateway.md)」を参照してください。<!--1358651-->  

クラウド配布ポイントを境界グループに含めるかどうかを決定するには、次の動作を考慮してください。  

- インターネットベースのクライアントは、境界グループに依存しません。 インターネットに接続する配布ポイントまたはクラウド配布ポイントのみを使用します。 これらの種類のクライアントにクラウド配布ポイントのみを使用してサービスを提供している場合、これらの配布ポイントを境界グループに含める必要はありません。  

- 内部ネットワーク上のクライアントにクラウド配布ポイントを使用させる場合は、その配布ポイントがクライアントと同じ境界グループ内にある必要があります。 Azure からのコンテンツのダウンロードに関連するコストがあるため、クライアントはコンテンツ ソースのリストの最後にクラウド配布ポイントを優先付けします。 そのため、クラウド配布ポイントは、通常、イントラネットベースのクライアントのフォールバック ソースとして使用されます。 クラウド優先の設計にする場合は、このビジネス要件を満たすように境界グループを設計します。 詳細については、[境界グループの構成](../../servers/deploy/configure/boundary-groups.md)に関するページを参照してください。  

Azure の特定のリージョンにクラウド配布ポイントをインストールしても、クライアントはその Azure リージョンに対応しません。 クラウド配布ポイントをランダムに選択します。 クラウド配布ポイントを複数のリージョンにインストールし、クライアントがコンテンツの場所のリストで複数のポイントを受け取った場合は、クライアントが同じ Azure リージョンからクラウド配布ポイントを使用しない場合があります。  

### <a name="backup-and-recovery"></a>バックアップと回復  

階層内のクラウド配布ポイントを使用する場合、バックアップおよび回復を計画するときに、以下の情報を参照してください。  

- **[サイト サーバーのバックアップ]** メンテナンス タスクを使用すると、Configuration Manager によって自動的にクラウド配布ポイントの構成が組み込まれます。  

- バックアップしてサーバー認証証明書のコピーを保存します。 Azure で従来のサービス展開を使用する場合も、バックアップして Azure 管理証明書のコピーを保存します。 Configuration Manager プライマリ サイトを別のサーバーに復元する場合は、証明書を再インポートする必要があります。  


## <a name="requirements"></a><a name="bkmk_requirements"></a> 要件

- サービスをホストするには、**Azure サブスクリプション**が必要です。  

    - **Azure 管理者**は、設計によっては、特定のコンポーネントの初回作成に参加する必要があります。 この管理者には Configuration Manager のアクセス許可は必要ありません。  

- サイト サーバーでクラウド サービスを展開して管理するには、**インターネットへのアクセス**が必要です。  

- **Azure Resource Manager** デプロイ方法を使用している場合は、Configuration Manager と**クラウド管理**の [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) を統合します。 Azure AD の*ユーザー探索*は必要ありません。  

- **サーバー認証証明書**。 詳細については、この後の「[証明書](#bkmk_certs)」セクションを参照してください。  

    - 複雑さを軽減するため、サーバー認証証明書にパブリック証明書プロバイダーを使用してください。 これを行う場合は、クライアントがクラウド サービスの名前を解決するために、**DNS CNAME エイリアス**も必要になります。  

- Configuration Manager バージョン 1810 以前で、Azure クラシック デプロイ方法を利用している場合は、**Azure 管理証明書**が必要です。 詳細については、この後の「[証明書](#bkmk_certs)」セクションを参照してください。  

    > [!TIP]  
    > Configuration Manager バージョン 1806 以降では、**Azure Resource Manager** デプロイ モデルを使用します。 この管理証明書は必要ありません。  
    >
    > バージョン 1810 以降では、従来の展開方法は推奨されません。  

- **Cloud Services** グループのクライアント設定で、 **[クラウド配布ポイントへのアクセスを許可する]** を **[はい]** に設定します。 既定では、この値は **[いいえ]** に設定されています。  

- クライアント デバイスには**インターネット接続**が必要で、**IPv4** を使用する必要があります。  


## <a name="specifications"></a><a name="bkmk_spec"></a> 仕様

- クラウド配付ポイントは、[クライアントとデバイスのサポートされるオペレーティング](../configs/supported-operating-systems-for-clients-and-devices.md)に関するページに記載されているすべての Windows バージョンをサポートします。  

- 管理者は、次の種類のサポートされているソフトウェアのコンテンツを配布します。  
  - アプリケーション
  - パッケージ
  - OS アップグレード パッケージ
  - サード パーティ製ソフトウェアの更新プログラム  

    > [!Important]  
    > - Configuration Manager コンソールでは Microsoft ソフトウェア更新プログラムのクラウド配付ポイントへの配布はブロックされませんが、クライアントが使用していないコンテンツを格納するために Azure のコストを支払っていることになります。 インターネットベースのクライアントは常に、Microsoft Update クラウド サービスから Microsoft ソフトウェア更新プログラムのコンテンツを受け取ります。 Microsoft ソフトウェア更新プログラムをクラウド配布ポイントに配布しないでください。
    > - コンテンツの保存に CMG を使用する場合、[クライアント設定](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)の **[Download delta content when available]\(デルタ コンテンツが使用可能な場合はダウンロードする\)** が有効になっていると、サードパーティの更新プログラムのコンテンツはクライアントにダウンロードされません。 <!--6598587--> 

- バージョン 1806 以降では、クラウド配布ポイントをソースとして使用するように、プル配布ポイントを構成します。 詳細については、「[ソース配布ポイントについて](use-a-pull-distribution-point.md#about-source-distribution-points)」を参照してください。<!--1321554-->  

### <a name="deployment-settings"></a>展開の設定

- **[実行中のタスク シーケンスで必要になったときに、ローカルでコンテンツをダウンロードする]** オプションを使用してタスク シーケンスを展開すると、管理ポイントにクラウド配布ポイントがコンテンツの場所として含まれません。 クライアントがクラウド配布ポイントを使用するには、 **[タスク シーケンスを開始する前にすべてのコンテンツをローカルにダウンロードする]** オプションを使用してタスク シーケンスを展開します。  

- クラウド配布ポイントは、 **[配布ポイントからプログラムを実行する]** オプションを使用したパッケージのデプロイをサポートしていません。 デプロイ オプション **[配布ポイントからコンテンツをダウンロードしてローカルで実行する]** を使用します。  

### <a name="limitations"></a>制限事項  

- クラウド配布ポイントを、PXE やマルチキャストを有効にした展開に使用することはできません。  

- クラウド配布ポイントでは、App-V ストリーミング アプリケーションをサポートしていません。  

- クラウド配布ポイントで[コンテンツの事前設定](manage-network-bandwidth.md#BKMK_PrestagingContent)はできません。 クラウド配布ポイントを管理するプライマリ サイトの配布マネージャーが、すべてのコンテンツを転送します。  

- クラウド配布ポイントをプル配布ポイントとして構成することはできません。  


## <a name="cost"></a><a name="bkmk_cost"></a> コスト

<!--501018-->
> [!IMPORTANT]  
> 以下のコスト情報は、見積もり目的のみで提供されます。 ご利用の環境によっては、クラウド配布ポイントの総コストに影響を与える変動要素が他にも存在する場合があります。  

Configuration Manager には、コストの管理とデータ アクセスの監視を支援するための次のオプションがあります。  

- クラウド サービスに格納されるコンテンツの量を制御および監視します。 詳細については、[クラウド配布ポイントの監視](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor)に関するセクションを参照してください。  

- クライアント ダウンロードのしきい値に達するか、月ごとの制限を超えたときに、アラートを送信するように Configuration Manager を構成します。 詳細については、[データ転送のしきい値アラート](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts)に関するセクションを参照してください。

- クライアントによるクラウド配布ポイントからのデータ転送の数を減らすには、次のピア キャッシュ テクノロジのいずれかを使用します。  
  - Configuration Manager のピア キャッシュ
  - Windows BranchCache
  - Windows 10 配信の最適化  

    詳しくは、「[コンテンツ管理の基本的な概念](fundamental-concepts-for-content-management.md)」を参照してください。  

### <a name="components"></a>コンポーネント

クラウド配布ポイントでは次の Azure コンポーネントが使用され、Azure サブスクリプション アカウントへの課金が発生します。  

> [!Tip]  
> バージョン 1806 以降では、クラウド管理ゲートウェイも、クライアントにコンテンツを提供することができます。 この機能は、Azure VM を統合することで、コストを削減します。 詳細については、[クラウド管理ゲートウェイのコスト](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost)に関するセクションを参照してください。  

#### <a name="virtual-machine"></a>仮想マシン

- クラウド配布ポイントでは、PaaS (サービスとしてのプラットフォーム) として Azure Cloud Services が使用されます。 このサービスでは、計算処理コストを発生させる仮想マシン (VM) が使用されます。  

- 各クラウド配布ポイントのサービスでは、2 つの Standard A0 VM が使用されます。  

- 予想されるコストについては、「[Azure の料金計算ツール](https://azure.microsoft.com/pricing/calculator/)」を参照してください。

    > [!NOTE]  
    > 仮想マシンのコストは地域によって異なります。

#### <a name="outbound-data-transfer"></a>送信データの転送

- Azure に入ってくるデータは無料です (イングレスまたはアップロード)。 サイトからクラウド配布ポイントへのコンテンツの配布は、Azure へのアップロードです。  

- 課金は Azure から外に出るデータに基づきます (エグレスまたはダウンロード)。 Azure からのクラウド配布ポイントのデータフローは、クライアントがダウンロードするソフトウェアのコンテンツで構成されます。  

- 詳細については、[クラウド配布ポイントの監視](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor)に関するセクションを参照してください。  

- 予想されるコストについては、「[Azure 帯域幅の料金詳細](https://azure.microsoft.com/pricing/details/bandwidth/)」を参照してください。 データ転送の価格設定は階層になっています。 使えば使うほど、ギガバイトあたりで支払う料金が安くなります。  

#### <a name="content-storage"></a>コンテンツ ストレージ

- インターネットベースのクライアントは、Microsoft Update クラウド サービスから無料で Microsoft ソフトウェア更新プログラムのコンテンツを受け取ります。 Microsoft ソフトウェアの更新プログラムを含むソフトウェア更新プログラムの展開パッケージは、クラウド配布ポイントに配布しないでください。 配布した場合は、クライアントが使用しないコンテンツに対してデータ ストレージ コストが発生します。  

- クラウド配布ポイントは、デプロイ モデルに応じて、次の標準的な BLOB ストレージを使用します。  

    - Azure Resource Manager の展開では、Azure ローカル冗長ストレージ (LRS) を使用します。 この変更により、ストレージ アカウントのコストが削減されます。 クラシック デプロイでは、GRS の追加機能を使用していませんでした。 詳細については、[ローカル冗長ストレージ](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs)に関するページを参照してください。  

    - Configuration Manager バージョン 1810 以前を使用した従来の展開では、Azure geo 冗長ストレージ (GRS) を使用します。 詳細については、[geo 冗長ストレージ](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs)に関するページを参照してください。  

#### <a name="other-costs"></a>その他のコスト

- クラウド サービスにはそれぞれ、動的 IP アドレスが与えられます。 各クラウド配布ポイントでは、新しい動的 IP アドレスが使用されます。 クラウド サービスごとに VM を追加しても、これらのアドレスは増えません。  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a> ポートとデータ フロー

クラウド配布ポイントには、次の 2 つのプライマリ データ フローがあります。  

- クラウド配布ポイントのサービスを設定するため、サイト サーバーが Azure に接続する  

- コンテンツをダウンロードするため、クライアントがクラウド配布ポイントに接続する  

### <a name="site-server-to-azure"></a>サイト サーバーから Azure へ

オンプレミス ネットワークに受信ポートを開く必要はありません。 クラウド サービスを展開、更新、管理するため、サイト サーバーにより Azure とクラウドの配布ポイントとのすべての通信が開始されます。 サイト サーバーは、Microsoft クラウドへの送信接続を作成する必要があります。 これは、配布ポイント サイト システムの役割を特定のサイトにインストールする場合と同じです。  

### <a name="client-to-cloud-distribution-point"></a>クライアントからクラウド配布ポイントへ

オンプレミス ネットワークに受信ポートを開く必要はありません。 インターネットベースのクライアントは、Azure サービスと直接通信します。 クラウド配布ポイントを使用する内部ネットワーク上のクライアントは、Microsoft クラウドに接続する必要があります。

コンテンツの場所の優先順位と、イントラネットベースのクライアントがクラウド配布ポイントを使用するタイミングの詳細については、「[Content source priority](fundamental-concepts-for-content-management.md#content-source-priority)」 (コンテンツ ソースの優先順位) を参照してください。

クライアントがクラウド配布ポイントをコンテンツの場所として使用する場合:  

1. 管理ポイントは、コンテンツ ソースの一覧と共に、アクセス トークンをクライアントに提供します。 このトークンは 24 時間有効で、クラウド配布ポイントへのアクセスをクライアントに提供します。  

2. 管理ポイントは、クライアントの場所の要求に対して、クラウド配布ポイントの**サービスの FQDN** で応答します。 このプロパティは、サーバー認証証明書の共通名と同じです。  

    自分のドメイン名 (WallaceFalls.contoso.com など) を使用している場合、クライアントはこの FQDN の解決をまず試みます。 クライアントで Azure サービス名を解決するには、ご利用のドメインのインターネット向け DNS に CNAME エイリアスを含める必要があります (例: WallaceFalls.cloudapp.net)。  

3. クライアントは次に Azure サービス名 (WallaceFalls.cloudapp.net など) を有効な IP アドレスに解決します。 この応答は、Azure の DNS で処理される必要があります。  

4. クライアントがクラウド配布ポイントに接続します。 Azure はいずれか 1 つの VM インスタンスへの接続を負荷分散します。 クライアントは、アクセス トークンを使用して自身を認証します。  

5. クラウド配布ポイントは、クライアントのアクセス トークンを認証してから、Azure Storage 内の正確なコンテンツの場所をクライアントに提供します。  

6. クライアントがクラウド配布ポイントのサーバー認証証明書を信頼すると、Azure Storage に接続してコンテンツをダウンロードします。


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a> パフォーマンスと拡張性

<!--494872-->

どの配布ポイントの設計でも、次の要因を検討します。  

- 同時クライアント接続の最大数
- クライアントがダウンロードするコンテンツのサイズ
- ビジネス要件を満たすために許容される時間の長さ

[トポロジ設計](#bkmk_topology)によっては、クライアントに複数のクラウド配布ポイントのオプションがある場合、それらのクラウド サービス間で自然にランダム化されます。 コンテンツの特定の部分を 1 つのクラウド配布ポイントにのみ配布し、多数のクライアントが同時にこのコンテンツをダウンロードしようとした場合、このアクティビティによってその 1 つのクラウド配布ポイントへの負荷が高まります。 クラウド配布ポイントの追加には、個別の Azure ストレージ サービスも含まれます。 クライアントでのクラウド配布ポイントのコンポーネントとの通信方法と、コンテンツのダウンロード方法の詳細については、「[ポートとデータ フロー](#bkmk_dataflow)」を参照してください。  

クラウド配布ポイントは、Azure Storage へのフロント エンドとして 2 つの Azure VM を使用します。 この既定の展開は、ほとんどの顧客のニーズを満たしています。 多数の同時クライアント接続 (150,000 クライアントなど) があるような極端な状況では、Azure VM の処理能力がクライアントの要求に追いつかない場合があります。 クラウド配布ポイントで使用する Azure VM のサイズを変更することはできません。 Configuration Manager でクラウド配布ポイントの VM インスタンスの数を構成することはできませんが、必要な場合は、Azure portal でクラウド サービスを再構成します。 手動で VM インスタンスを追加するか、自動的に拡張するようにサービスを構成します。

> [!Important]  
> Configuration Manager を更新すると、サイトによってクラウド サービスが再展開されます。 Azure portal でクラウド サービスを手動で再構成すると、インスタンスの数が既定値の 2 にリセットされます。  

Azure ストレージ サービスは、1 つのファイルに対して 1 秒あたり 500 件の要求をサポートします。 1 つのクラウド配布ポイントのパフォーマンス テストでは、100 MB のファイル 1 つを 24 時間で 50,000 クライアントに配布することができました。<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a> 証明書  

クラウド配布ポイントの設計によっては、1 つ以上のデジタル証明書が必要です。  

### <a name="general-information"></a>一般情報

<!--SCCMDocs issue #779-->
クラウド配布ポイント用の証明書は、次の構成をサポートします。  

- 4096 ビットのキーの長さ

- バージョン 3 証明書。 詳細については、「[CNG certificates overview](../network/cng-certificates-overview.md)」(CNG 証明書の概要) を参照してください。  

- バージョン 1802 以降で、ポリシー: **[システム暗号化: 暗号化、ハッシュ、署名のための FIPS 準拠アルゴリズムを使う]** を使用して Windows を構成した場合。  

- バージョン 1802 以降、TLS 1.2 のサポート。 詳細については、「[暗号化コントロールのテクニカル リファレンス](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities)」を参照してください。  

### <a name="server-authentication-certificate"></a>サーバー認証証明書

*この証明書は、すべてのクラウド配布ポイントの展開に必要です。*

詳細については、「[CMG サーバー認証証明書](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth)」と、必要に応じて、次のサブセクションを参照してください。  

- クライアントが信頼する CMG のルート証明書
- パブリック プロバイダーが発行したサーバー認証証明書
- エンタープライズ PKI から発行されたサーバー認証証明書

クラウド配布ポイントは、クラウド管理ゲートウェイと同じ方法でこの種類の証明書を使用します。 また、クライアントがこの証明書を信頼する必要があります。 複雑さを軽減するため、パブリック プロバイダーによって発行された証明書を使用することをお勧めします。

ワイルドカード証明書を使用する場合を除き、同じ証明書を再利用しないでください。 クラウド配布ポイントとクラウド管理ゲートウェイの各インスタンスには、一意のサーバー認証証明書が必要です。

PKI からこの証明書を作成する方法の詳細については、「[Deploy the service certificate for cloud distribution points](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)」 (クラウド配布ポイント用のサービス証明書の展開) を参照してください。  

### <a name="azure-management-certificate"></a>Azure 管理証明書

*この証明書は従来のサービス展開に必要です。Azure Resource Manager の展開には必要ありません。*

> [!Important]  
> Configuration Manager バージョン 1806 以降では、**Azure Resource Manager** デプロイ モデルを使用します。 この管理証明書は必要ありません。  
>
> バージョン 1810 以降では、従来の展開方法は推奨されません。  
>
> Configuration Manager バージョン 1902 以降、クラウド配布ポイントの新しいインスタンスに対しては、Azure Resource Manager が唯一の展開メカニズムです。 この証明書は、Configuration Manager バージョン 1902 以降では必須ではありません。<!-- 3605704 -->

Configuration Manager バージョン 1810 以前で、Azure の従来の展開方法を利用している場合は、**Azure 管理証明書**が必要です。 詳細については、クラウド管理ゲートウェイの証明書の記事の「[Azure 管理証明書](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt)」セクションを参照してください。 Configuration Manager サイト サーバーは、Azure での認証にこの証明書を使用して、クラシック デプロイの作成と管理を行います。  

複雑さを軽減するには、すべての Azure サブスクリプションとすべての Configuration Manager サイトで、クラウド配布ポイントとクラウド管理ゲートウェイのすべてのクラシック デプロイに同じ Azure 管理証明書を使用します。


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> よく寄せられる質問 (FAQ)

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>クラウド配布ポイントからコンテンツをダウンロードするには、クライアントに証明書が必要ですか?

クライアント認証証明書は必要ありません。 クライアントは、クラウド配布ポイントで使用されるサーバー認証証明書を信頼する必要があります。 この証明書がパブリック証明書プロバイダーから発行されている場合は、ほとんどの Windows デバイスにこれらのプロバイダーの信頼されたルート証明書が既に含まれています。 自分の組織の PKI からサーバー認証証明書を発行した場合は、クライアントがチェーン全体で発行側の証明書を信頼する必要があります。 このチェーンには、ルート証明機関とすべての中間証明機関が含まれます。 PKI の設計によっては、この証明書によりクラウド配布ポイントの展開がより複雑になる場合があります。 このような複雑さを回避するために、クライアントが既に信頼しているパブリック証明書プロバイダーの使用をお勧めします。  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>オンプレミスのクライアントはクラウド配布ポイントを使用できますか?

はい。 内部ネットワーク上のクライアントにクラウド配布ポイントを使用させる場合は、その配布ポイントがクライアントと同じ境界グループ内にある必要があります。 Azure からのコンテンツのダウンロードに関連するコストがあるため、クライアントはコンテンツ ソースのリストの最後にクラウド配布ポイントを優先付けします。 そのため、クラウド配布ポイントは、通常、イントラネットベースのクライアントのフォールバック ソースとして使用されます。 クラウド優先の設計にする場合は、それに応じて境界グループを設計します。 詳細については、[境界グループの構成](../../servers/deploy/configure/boundary-groups.md)に関するページを参照してください。  

### <a name="do-i-need-azure-expressroute"></a>Azure ExpressRoute は必要ですか?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) では、Microsoft クラウドにオンプレミス ネットワークを拡張することができます。 Configuration Manager クラウド配布ポイントでは、ExpressRoute などの仮想ネットワーク接続は必要ありません。  

組織で ExpressRoute を使用している場合は、クラウド配布ポイントの Azure サブスクリプションを ExpressRoute を使用するサブスクリプションから分離します。 この構成により、クラウド配布ポイントがこの方法で誤って接続されることがなくなります。  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Azure 仮想マシンを維持する必要がありますか?

維持する必要はありません。 クラウド配布ポイントの設計では、PaaS (サービスとしてのプラットフォーム) として Azure が使用されます。 Configuration Manager は、指定されたサブスクリプションを使用して、必要な VM、ストレージ、ネットワークを作成します。 Azure は仮想マシンをセキュリティで保護し、更新します。 IaaS (サービスとしてのインフラストラクチャ) と同様に、これらの VM はオンプレミス環境には含まれません。 クラウド配布ポイントは、クラウドに Configuration Manager 環境を拡張する PaaS です。 詳細については、「[PaaS クラウド サービス モデルのセキュリティ上の利点](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model)」を参照してください。  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>クラウド配布ポイントでは、Azure CDN が使用されますか?

Azure Content Delivery Network (CDN) は、世界各地に戦略的に配置された物理ノードにコンテンツをキャッシュすることで、高帯域幅コンテンツを迅速に配信するためのグローバル ソリューションです。 詳細については、[Azure CDN の概要](https://docs.microsoft.com/azure/cdn/cdn-overview)ページを参照してください。

Configuration Manager のクラウド配布ポイントでは現在、Azure CDN をサポートしていません。


## <a name="next-steps"></a>次のステップ

[クラウド配布ポイントのインストール](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
