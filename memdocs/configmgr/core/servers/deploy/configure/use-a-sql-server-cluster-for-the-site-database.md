---
title: SQL Server クラスター
titleSuffix: Configuration Manager
description: SQL Server クラスターを使用して Configuration Manager サイト データベースをホストします
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 988a9c31fca8d06104ce317f4709ee990089d723
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699145"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>サイト データベースに対して SQL Server クラスターを使用する

*適用対象:Configuration Manager (Current Branch)*

SQL Server フェールオーバー クラスターを使用して Configuration Manager サイト データベースをホストできます。 クラスターを使用すると、フェールオーバーがサポートされ、サイト データベースの信頼性が高まります。 ただし、処理や負荷分散に関するベネフィットが増えることはありません。 さらに、SQL Server フェールオーバー クラスターでは、共有ストレージが使用され、単一障害点が発生します。 サイト サーバーは、サイト データベースに接続する前に SQL Server クラスターのアクティブ ノードを検索する必要があるため、パフォーマンスの低下が発生する可能性があります。  

> [!IMPORTANT]  
> SQL Server クラスターの正常なセットアップは、SQL Server ドキュメント ライブラリで提供されるドキュメントと手順に依存します。  


Configuration Manager をインストールする前に、Configuration Manager をサポートする SQL Server クラスターを準備します。 詳細については、[クラスター化された SQL Server インスタンスの準備](#bkmk_prepare)に関する記事を参照してください。

Configuration Manager のセットアップ中に、Microsoft Windows Server クラスターの各物理コンピューター ノードに Windows ボリューム シャドウ コピー サービス ライターがインストールされます。 このサービスでは、**バックアップ サイト サーバー** メンテナンス タスクがサポートされます。  

サイトのインストール後に Configuration Manager は、1 時間ごとにクラスター ノードが変更されたかどうかを確認します。 Configuration Manager では、検出された変更の中で、そのコンポーネントのインストールに影響を与えるものが自動的に管理されます。 たとえば、ノードのフェールオーバーや、SQL Server クラスターへの新しいノードの追加です。  



## <a name="supported-options"></a>サポートされるオプション

サイト データベースとして使用される SQL Server フェールオーバー クラスターでは、次のオプションがサポートされます。

- 単一インスタンス クラスター  

- 複数インスタンス構成  

- 複数のアクティブ ノード  

- 名前付きインスタンスと既定のインスタンスの両方  



## <a name="prerequisites"></a>[前提条件]

次の前提条件に注意してください。  

- サイト データベースは、サイト サーバーからリモートである必要があります クラスターにサイト システム サーバーを含めることはできません。  

    > [!Note]  
    > バージョン 1810 以降では、Configuration Manager セットアップ プロセスで、フェールオーバー クラスタリング用の Windows の役割でコンピューターにサイト サーバーの役割がインストールされるのがブロックされなくなりました。 以前は、サイト サーバー上にサイト データベースを併置できませんでした。 この変更により、SQL クラスターとサイト サーバーをパッシブ モードで使用して、より少ないサーバー数で高可用性サイトを作成できます。 詳細については、[高可用性オプション](high-availability-options.md)に関するページを参照してください。 <!--3607761, fka 1359132-->  

- サイト サーバーのコンピューター アカウントを、クラスター内の各サーバーのローカル **Administrators** グループに追加します。  

- Kerberos 認証をサポートするには、各 SQL Server クラスター ノードのネットワーク接続に対して **TCP/IP** ネットワーク通信プロトコルを有効にします。 **名前付きパイプ** プロトコルは不要ですが、Kerberos 認証の問題をトラブルシューティングするために使用できます。 ネットワーク プロトコルの設定は、 **[SQL Server ネットワークの構成]** にある **[SQL Server 構成マネージャー]** で構成します。  

- サイト データベースに対して SQL Server クラスターを使用する場合の特定の証明書要件があります。 詳細については、以下の記事を参照してください。
  - [SQL フェールオーバー クラスター構成に証明書をインストールする](/sql/database-engine/configure-windows/manage-certificates?view=sql-server-ver15#provision-failover-cluster-cert)
  - [Configuration Manager での PKI 証明書の要件](../../../plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers)

  > [!NOTE]
  > SQL で証明書を事前にプロビジョニングしていない場合、Configuration Manager は SQL の自己署名証明書を作成してプロビジョニングします。<!-- 7099499 -->

## <a name="limitations"></a>制限事項

次の制限が適用されます。  


### <a name="installation-and-configuration"></a>インストールおよび構成

- セカンダリ サイトでは、SQL Server クラスターは使用できません。  

- SQL Server クラスターを指定する場合、サイト データベースに対して既定以外のファイルの場所を指定するオプションは使用できません。  


### <a name="sms-provider"></a>SMS プロバイダー

SQL Server クラスター上に SMS プロバイダーのインスタンスをインストールすることはできません。 また、これはクラスター化された SQL Server ノードとして実行されているコンピューター上でもサポートされません。  


### <a name="data-replication-options"></a>データ レプリケーションのオプション

**分散ビュー**を使用する場合は、SQL Server クラスターを使用してサイト データベースをホストすることはできません。  


### <a name="backup-and-recovery"></a>バックアップと回復

Configuration Manager では、名前付きインスタンスを使用する SQL Server クラスターの Data Protection Manager (DPM) のバックアップはサポートされません。 SQL Server の既定のインスタンスを使用する SQL Server クラスター上の DPM バックアップはサポートします。  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a>クラスター化された SQL Server インスタンスを準備する  

サイト データベースを準備するために完了する主なタスクを次に示します。

- サイト データベースをホストする仮想 SQL Server クラスターを既存の Windows Server クラスター環境で作成します。 SQL Server クラスターをインストールおよび設定するための特定の手順については、使用している SQL Server のバージョンのドキュメントをご覧ください。 詳細については、「[新しい SQL Server フェールオーバー クラスターの作成](/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017)」を参照してください。  

- SQL Server クラスター内の各コンピューターで、Configuration Manager によるサイト コンポーネントのインストールを望まない各ドライブのルート フォルダーにファイルを配置します。 そのファイルに `NO_SMS_ON_DRIVE.SMS` という名前を付けます。 既定では、Configuration Manager は各物理ノードにいくつかのコンポーネントをインストールして、バックアップなどの操作をサポートします。  

- サイト サーバーのコンピューター アカウントを、各 Windows Server クラスター ノード コンピューターのローカル **Administrators** グループに追加します。  

- 仮想 SQL Server インスタンスで、Configuration Manager の設定を実行するユーザー アカウントに、**sysadmin** という SQL Server ロールを割り当てます。  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>クラスター化された SQL Server を使用して新しいサイトをインストールするには  

クラスター化されたサイト データベースを使用するサイトをインストールするには、次の部分を変更したうえで通常のサイトのインストール プロセスに従って、Configuration Manager のセットアップを実行します。  

- **[データベース情報]** ページで、サイト データベースをホストする仮想 SQL Server クラスター インスタンスの名前を指定します。 仮想インスタンスは、SQL Server を実行するコンピューターの名前を置き換えます。  

    > [!IMPORTANT]  
    > 仮想 SQL Server クラスター インスタンスの名前を入力するとき、Windows Server クラスターによって作成される仮想 Windows Server 名を入力しないでください。 仮想 Windows Server 名を使用すると、サイト データベースが、アクティブな Windows Server クラスター ノードのローカル ハード ディスクにインストールされます。 これにより、そのノードに障害が発生しても、正常にフェールオーバーできません。