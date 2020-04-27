---
title: Azure での Configuration Manager
titleSuffix: Configuration Manager
description: Azure 環境での Configuration Manager の使用に関する情報。
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c12372325573c6795396ff0832ca60cba68b8c29
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078500"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Azure の Configuration Manager - よく寄せられる質問

*適用対象:Configuration Manager (Current Branch)*

次の質問と回答が、Microsoft Azure での Configuration Manager の使用のタイミングと構成方法を理解するのに役立つ場合があります。

## <a name="general-questions"></a>一般的な質問
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>会社で Microsoft Azure にできるだけ多くの物理サーバーを移動しようとしているのですが、Azure に Configuration Manager サーバーを移動することはできますか?
もちろんできます。  [Configuration Manager での仮想環境のサポート](../plan-design/configs/support-for-virtualization-environments.md)に関するページを参照してください。

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>すばらしい。 現在の環境では複数のサイトが必要なのですが、 子プライマリ サイトをすべて、中央管理サイトと共に Azure に配置すべきですか? それともオンプレミスに配置すべきでしょうか? また、セカンダリ サイトはどうすればよいですか?
Azure でホストする場合、サイト間の近接通信 (ファイルベースおよびデータベース レプリケーション) が可能になります。 ただし、すべてのクライアントに関連するトラフィックはサイト サーバーとサイト システムから離れた場所で発生します。 無制限データ プランで Azure とイントラネット間の高速で信頼性の高い接続を使用する場合は、Azure ですべてのインフラストラクチャをホストすることを選択できます。

ただし、従量制課金接続プランを使用し、利用可能な帯域幅またはコストが気になる場合や、Azure とイントラネット間のネットワーク接続が高速でないか信頼できない可能性がある場合には、オンプレミスでの特定のサイト (およびサイト システム) の配置を検討し、Configuration Manager に組み込まれている帯域幅制御を使用するようにしてください。

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Azure の Configuration Manager では SaaS (サービスとしてのソフトウェア) シナリオが適用されるのですか?
いいえ。Azure Virtual Machines では Configuration Manager インフラストラクチャをホストするため、IaaS (サービスとしてのインフラストラクチャ) になります。

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>Azure への Configuration Manager インフラストラクチャの移行を検討する場合、どのような点に注意すべきですか?
いい質問です。この決定を行う際に最も重要な点はいくつかあるため、このトピックでは次のようにそれぞれ別々に説明します。
1. ネットワーク
2. 可用性
3. パフォーマンス
4. コスト
5. ユーザーの作業

## <a name="networking"></a>ネットワーク
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>ネットワーク要件はどうなっていますか? ExpressRoute または Azure VPN Gateway を使用する必要がありますか?
ネットワークは非常に重要な決定事項です。 ネットワークの速度と待機時間が、サイト サーバーとリモート サイト システムおよびサイト システムへのクライアント通信機能に影響する可能性があります。 したがって、ExpressRoute を使用することをお勧めします。 ただし、Configuration Manager で Azure VPN Gateway を使用できないわけではありません。 このインフラストラクチャの要件 (パフォーマンス、修正プログラムの適用、ソフトウェアの配布、オペレーティング システムの展開) をよく確認したうえで、決定する必要があります。 各ソリューションの考慮事項は次のとおりです。

- **ExpressRoute** (推奨)
  - データセンターへの自然な拡張 (複数のデータセンターをつなげることができる)
  - Azure データセンターとインフラストラクチャ間のプライベート接続
  - パブリック インターネットを経由しない
  - 信頼性、高速、低待機時間、高セキュリティを提供
  - 最大で 10 gbps の速度と無制限データ通信プラン オプションをオファー
- **VPN Gateway**
  - サイト間/ポイント対サイト VPN
  - トラフィックがパブリック インターネットを経由する
  - インターネット プロトコル セキュリティ (IPsec) とインターネット キー交換 (IKE) を使用

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute には、無制限と従量制課金、異なる速度オプション、Premium Add-on など、さまざまなオプションがありますが、 どれを選べばよいですか?
選択するオプションは、実装シナリオや計画しているデータの配布量によって異なります。 サイト サーバーと配布ポイント間の Configuration Manager データ転送は制御できますが、サイト サーバー間の通信を制御することはできません。   従量制課金接続プランを使用する場合、オンプレミスで特定のサイト (およびサイト システム) を配置し、[Configuration Manager の組み込み帯域幅制御](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)を使用すれば、Azure の使用コストの制御に役立ちます。

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Active Directory ドメインなどのインストール要件はどうなっていますか? サイト サーバーを Active Directory ドメインに引き続き参加させる必要はありますか?
はい。 Azure に移行しても、Configuration Manager のインストールに関する Active Directory 要件を含め、[サポートされる構成](../plan-design/configs/supported-configurations.md)は同じです。

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Active Directory ドメインにサイト サーバーを参加させる必要があることはわかりましたが、Azure Active Directory は使用できますか?
いいえ。現時点では Azure Active Directory はサポートされていません。 サイト サーバーは引き続き [Windows Active Directory ドメイン](../plan-design/configs/support-for-active-directory-domains.md)のメンバーである必要があります。



## <a name="availability"></a>可用性
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Azure にインフラストラクチャを移行する理由の 1 つは高可用性の保証です。 Configuration Manager で使用する VM の Azure VM 可用性セットのような高可用性オプションを利用できますか?
はい。 Azure VM 可用性セットは、配布ポイントや管理ポイントのような冗長的なサイト システムの役割で使用できます。

また、Configuration Manager サイト サーバーでも使用できます。 たとえば、中央管理サイトとプライマリ サイトをすべて同じ可用性セットに含めることができます。これは、同時に再起動されないようにするのに役立ちます。

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>データベースに高可用性を持たせるにはどうすればよいですか? Azure SQL Database を使用できますか? それとも VM では Microsoft SQL Server を使用する必要がありますか?
VM では Microsoft SQL Server を使用する必要があります。 現時点では、Configuration Manager では Azure SQL Server はサポートされていません。 ただし、SQL Server の AlwaysOn 可用性グループのような機能を使用することができます。 [AlwaysOn 可用性グループ](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)の使用をお勧めします。これは、Configuration Manager のバージョン 1602以降、公式にサポートされています。

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>管理ポイントやソフトウェアの更新ポイントのようなサイト システムの役割で Azure Load Balancer を使用することはできますか?
Configuration Manager は Azure Load Balancer でテストされていませんが、機能がアプリケーションに対して透過的である場合、通常の操作には悪影響はありません。


## <a name="performance"></a>パフォーマンス
### <a name="what-factors-affect-performance-in-this-scenario"></a>このシナリオではどのような要素がパフォーマンスに影響しますか?
[Azure VM のサイズと種類](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs)、Azure VM ディスク (特に SQL Server では Premium Storage が推奨されます)、ネットワーク待機時間、および速度が最も重要です。

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Azure Virtual Machines について詳しく知りたいのですが、どのようなサイズの VM を使用すべきですか?
一般に、コンピューターの性能 (CPU およびメモリ) は、[Configuration Manager の推奨ハードウェア](../plan-design/configs/recommended-hardware.md)に対応する必要があります。 ただし、通常のコンピューター ハードウェアと Azure VM には、特にこれらの VM で使用されるディスクについて、いくつか異なる点があります。  使用する VM のサイズは使用環境の規模によって異なりますが、次のようないくつかの推奨事項があります。
- 非常に大規模な運用環境の展開では、"**S**" クラスの Azure VM をお勧めします。 Premium Storage ディスクを活用できるためです。  "S" 以外のクラスの VM では BLOB ストレージが使用され、一般的に許容される運用エクスペリエンスで必要なパフォーマンス要件が満たされません。
- 規模が大きい場合は複数の Premium Storage ディスクを使用する必要があり、最大 IOPS の Windows ディスク管理コンソールでストライピングする必要があります。  
- 初期サイトの展開時にはより高性能な、または複数の Premium ディスクを使用することをお勧めします (P20 ではなく P30、あるいは 1xP30 ではなくストライプ ボリュームの 2xP30 など)。 その後、サイトで負荷の増加に伴い VM サイズを大きくする必要がある場合は、より大きなサイズの VM で提供される追加の CPU とメモリを利用できます。 より大きいサイズの VM で許可される追加の IOPS スループットを、既存のディスクで利用することもできます。



次の表に、さまざまなサイズのインストールのプライマリおよび中央管理サイトで利用できる初期の推奨ディスク数をリストします。

**併置されたサイト データベース** - サイト サーバー上のサイト データベースを持つプライマリまたは中央管理サイト:

| デスクトップ クライアント    |推奨 VM サイズ|推奨ディスク|
|--------------------|-------------------|-----------------|
|**最大 25 K**       |   DS4_V2          |2xP30 (ストライプ)  |
|**25 K から 50 K**      |   DS13_V2         |2xP30 (ストライプ)  |
|**50 K から 100 K**     |   DS14_V2         |3xP30 (ストライプ)  |


**リモート サイト データベース** - リモート サーバー上のサイト データベースを持つプライマリまたは中央管理サイト:

| デスクトップ クライアント    |推奨 VM サイズ|推奨ディスク |
|--------------------|-------------------|------------------|
|**最大 25 K**       | サイト サーバー:F4S </br>データベース サーバー:DS12_V2 | サイト サーバー:1xP30 </br>データベース サーバー:2xP30 (ストライプ)  |
|**25 K から 50 K**      | サイト サーバー:F4S </br>データベース サーバー:DS13_V2 | サイト サーバー:1xP30 </br>データベース サーバー:2xP30 (ストライプ)   |
|**50 K から 100 K**     | サイト サーバー:F8S </br>データベース サーバー:DS14_V2 | サイト サーバー:2xP30 (ストライプ)   </br>データベース サーバー:3xP30 (ストライプ)   |

以下は、DS14_V2 で 50k から 100k クライアントを構成した例です。3xP30 のディスクがストライプ ボリュームで構成されており、別の論理ボリュームが Configuration Manager インストールとデータベース ファイルのために割り当てられています。![VM)disks](media/vm_disks.png)  



## <a name="user-experience"></a>ユーザーの作業
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>ユーザー エクスペリエンスが主に重要な点の 1 つということですが、それはなぜですか?
ネットワーク、可用性、パフォーマンス、および Configuration Manager サイト サーバーの配置場所に関する決定事項が、ユーザーに直接影響する場合があります。 Azure への移行はユーザーに対して透過的であるため、Configuration Manager との日常的な対話は変わらないと考えています。

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>わかりました。 Azure Virtual Machine への単一のスタンドアロン プライマリ サイトのインストールを予定しており、コストを抑えられるかどうかを知りたいのですが、 Azure Virtual Machines にも (リモート) サイト システム (管理ポイント、配布ポイント、ソフトウェアの更新ポイントなど) を配置すべきですか? それともオンプレミスに配置すべきでしょうか?
サイト サーバーから配布ポイントへの通信を除き、サイト内のサーバー同士がいつ通信するかは決まっておらず、ネットワーク帯域幅の使用も制御できません。 サイト システム間の通信は制御できないため、これらの通信に関するコストを考慮する必要があります。

ネットワークの速度や待機時間も考慮する必要があります。 低速ネットワークや信頼できないネットワークは、サイト サーバーとリモート サイト システム間およびサイト システムへのクライアント通信機能に影響する可能性があります。 よく使用する機能だけでなく、特定のサイト システムを使用する管理対象クライアントの数も考慮する必要があります。
一般に、開始点として WAN リンクとサイト システムに関する通常のガイダンスを利用できます。 選択する Azure とイントラネット間の受信ネットワーク スループットが、高速ネットワークに適切に接続されている WAN と一致するのが理想的です。

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>コンテンツ配信とコンテンツ管理はどうなっていますか? 標準配布ポイントは Azure またはオンプレミスになければならないのでしょうか? また、BranchCache やプル配布ポイントはオンプレミスで使用すべきですか? それとも、クラウド配布ポイントのみを使用すべきでしょうか?
コンテンツ管理の方法は、サイト サーバーやサイト システムの場合とほとんど同じです。
- 無制限データ プランで Azure とイントラネット間の高速で信頼性の高いネットワーク接続を使用する場合は、Azure で標準配布ポイントをホストすることを選択できます。
- 従量制課金接続プランと帯域幅コストが気になる場合や、Azure とイントラネット間のネットワーク接続が高速でないか信頼できない可能性がある場合には、他の方法を検討してください。 これには、オンプレミスでの標準またはプル配布ポイントの配置と BranchCache の使用が含まれます。 クラウドベースの配布ポイントを使用することもできますが、サポートされるコンテンツの種類にはいくつか制限があります (ソフトウェア更新プログラム パッケージがサポートされないなど)。

> [!NOTE]
>  PXE またはマルチキャストのサポートが必要な場合は、オンプレミスの配布ポイント (標準またはプル) を使用してブート要求に応じる必要があります。


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>クラウドベース配布ポイントの制限についてはわかりましたが、インターネット ベースのクライアントをサポートするために必要でも、DMZ に管理ポイントを配置したくありません。 他の選択肢はありますか?
はい、ご利用いただけます。 Configuration Manager のバージョン 1610 では、プレリリース機能として[クラウド管理ゲートウェイ](../clients/manage/manage-clients-internet.md#cloud-management-gateway)をご紹介しました (この機能は、[クラウド プロキシ サービス](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)として、Technical Preview バージョン 1606 で初めて登場しました)。

**クラウド管理ゲートウェイ**は、インターネット上で Configuration Manager クライアントを管理する簡単な方法を提供します。 Microsoft Azure にデプロイされ、Azure サブスクリプションを必要とするサービスは、クラウド管理ゲートウェイ コネクタ ポイントと呼ばれる新しい役割を使用して、オンプレミスの Configuration Manager インフラストラクチャに接続します。 デプロイされ、構成されると、クライアントは内部のプライベート ネットワークに接続しているかどうか、またはインターネット上にあるかどうかに関係なく、オンプレミスの Configuration Manager サイト システムの役割にアクセスできます。

実際の環境でクラウド管理ゲートウェイの使用を開始できます。フィードバックをお送りいただくことで、改善することができます。 プレリリース機能の詳細については、「[更新プログラムからプレリリース機能を使用する](../servers/manage/install-in-console-updates.md#bkmk_prerelease)」を参照してください。

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>バージョン 1610 のプレリリース機能として導入されたピア キャッシュという新機能もあると聞きましたが、 BranchCache とは異なるものですか? どちらを選べばよいですか?
はい、まったく異なるものです。 [ピア キャッシュ](../plan-design/hierarchy/client-peer-cache.md)は Configuration Manager の 100% ネイティブのテクノロジですが、BranchCache は Windows の機能の 1 つです。 どちらも便利ですが、BranchCache ではブロードキャストを使用して必要なコンテンツを検索するのに対して、ピア キャッシュでは Configuration Managers の通常の配布ワークフローと境界グループの設定を使用します。

任意のクライアントをピア キャッシュのソースとして構成することができます。 そうすれば、管理ポイントがコンテンツ ソースの場所に関する情報を提供する際に、クライアントで必要なコンテンツがあるピア キャッシュ ソースと配布ポイントの両方の詳細が提供されます。


## <a name="cost"></a>コスト
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>わかりました。では、コストについて簡単に説明してください。 これは費用対効果の高い方法ですか?
使用環境はそれぞれ異なるため、何とも言えません。 Microsoft Azure の料金計算ツール (https://azure.microsoft.com/pricing/calculator/ ) を使用して、ご使用の環境でかかる費用を見積もることをお勧めします。

## <a name="additional-resources"></a>その他の資料
**基礎:** https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Azure Virtual Machine の種類:**
- Azure マシンのサイズ: https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
- VM 価格設定: https://azure.microsoft.com/pricing/details/virtual-machines/  
- ストレージ価格設定: https://azure.microsoft.com/pricing/details/storage/

**ディスク パフォーマンスに関する考慮事項:**    
- Premium ディスクの概要: https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Premium ディスクの詳細情報: https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- ストレージの最大サイズとパフォーマンス ターゲットの表を集めた便利なページ: https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- Premium Storage のしくみに関するその他の情報とかなり専門的ですが役に立つデータ:  https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**可用性:**
- Azure IaaS アップタイム SLA: https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- 可用性セットの説明: https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**接続:**
- ExpressRoute と Azure VPN: https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- Express Route の価格設定: https://azure.microsoft.com/pricing/details/expressroute/
- Express Route の詳細: https://azure.microsoft.com/documentation/articles/expressroute-introduction/
