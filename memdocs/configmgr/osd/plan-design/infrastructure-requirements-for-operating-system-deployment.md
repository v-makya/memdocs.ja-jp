---
title: OSD インフラストラクチャの要件
titleSuffix: Configuration Manager
description: Configuration Manager での OS の展開に対する外部および製品の依存関係と要件について説明します
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34c803cb2b43a2c69cee4c16f5029474e318eb2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709340"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Configuration Manager での OS の展開に対するインフラストラクチャ要件

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager での OS の展開には、外部依存関係と製品内部の依存関係があります。 この記事の内容は、OS の展開のためにインフラストラクチャを準備するのに役立ちます。  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a> Configuration Manager 外部の依存関係  

このセクションでは、Configuration Manager でオペレーティング システムを展開するのに必要な外部ツール、インストール キット、および OS バージョンに関する情報を提供します。  

### <a name="windows-adk-for-windows-10"></a>Windows 10 用 Windows ADK  

Windows アセスメント & デプロイメント キット (ADK) は、Windows の構成と展開をサポートするツールとドキュメントのセットです。 Configuration Manager は Windows ADK を使用して、Windows のインストール、イメージのキャプチャ、ユーザー プロファイルおよびデータの移行などの操作を自動化します。  

詳細については、以下の記事を参照してください。  

- [IT 担当者向け Windows ADK for Windows 10 シナリオ](https://docs.microsoft.com/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Windows ADK for Windows 10 をダウンロードする](https://docs.microsoft.com/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > **Windows ADK for Windows 10** と、**ADK 用の Windows PE アドオン**の両方をダウンロードしてください。

- [Windows 10 のサポート](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>サイト システム
Windows ADK は、次のサイト システム サーバーの前提条件です。

- 階層の最上位サイトのサイト サーバー  

- 階層の各プライマリ サイトのサイト サーバー  

- SMS プロバイダーの各インスタンス  


> [!NOTE]  
> Configuration Manager サイトをインストールする前に、各サイト サーバーに Windows ADK を手動でインストールします。  

#### <a name="windows-adk-features"></a>Windows ADK の機能
Windows ADK の次の機能をインストールします。  

-   ユーザー状態移行ツール (USMT)  

    > [!Note]  
    > USMT は、SMS プロバイダーでは必要ありません。

-   Windows 展開ツール  

-   Windows プレインストール環境 (Windows PE)  

    > [!Important]  
    > Windows 10 バージョン 1809 以降、Windows PE は個別のインストーラーとなっています。 それ以外に機能の違いはありません。<!--SCCMDocs-pr issue 2908-->  

さまざまなバージョンの Configuration Manager で使用できる Windows 10 ADK のバージョン一覧については、[Windows 10 のサポート](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)に関するページを参照してください。


### <a name="user-state-migration-tool-usmt"></a>ユーザー状態移行ツール (USMT)  

Configuration Manager では、USMT 10 ソース ファイルを含む USMT パッケージを使用して、OS の展開の一部として、ユーザーの状態をキャプチャして復元します。 最上位サイトに Configuration Manager をセットアップすると、USMT パッケージが自動的に作成されます。 USMT 10 では、Windows 7、Windows 8、Windows 8.1 および Windows 10 からユーザー状態をキャプチャします。  

詳細については、以下の記事を参照してください。  

- [USMT 10 の一般的な移行シナリオ](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [ユーザー状態の管理](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Windows PE は、コンピューターを起動するブート イメージに使用されます。 それは、Windows のバージョンのプレインストールや展開の最中に使用される、サービスが制限された Windows です。 次に一覧したのは、サポートされているバージョンの Windows ADK for Configuration Manager (カレント ブランチ) です。  

#### <a name="windows-adk-version"></a>Windows ADK バージョン  
Windows 10 用 Windows ADK。 詳細については、[Windows 10 のサポート](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)に関するページをご覧ください。

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Configuration Manager コンソールでカスタマイズできる Windows PE ブート イメージのバージョン  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Configuration Manager コンソールでカスタマイズできない Windows PE ブート イメージのバージョン  
Windows PE 3.1<sup>1</sup> および Windows PE 5  

<sup>1</sup> Windows PE 3.1 のブートイメージしか Configuration Manager に追加することができません。 Windows AIK for Windows 7 (Windows PE 3 の構築用) を Windows AIK Supplement for Windows 7 SP1 (Windows PE 3.1 の構築用) にアップグレードしてください。 Windows AIK Supplement for Windows 7 SP1 は、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=5188)からダウンロードできます。  

たとえば、Configuration Manager を使っている場合は、Windows 10 用 Windows ADK (Windows PE 10 に基づく) で構築したブート イメージを Configuration Manager コンソールでカスタマイズできます。 一方、Windows PE 5 のブート イメージはサポートされていますが、このブート イメージをカスタマイズするには、別のコンピューターにある Windows 8 用 Windows ADK に付属している DISM を使わなければなりません。 その後、ブート イメージを Configuration Manager コンソールに追加します。 ブート イメージのカスタマイズ (オプションのコンポーネントとドライバーの追加)、ブート イメージのコマンド サポートの有効化、Configuration Manager コンソールへのブート イメージの追加、ブート イメージによる配布ポイントの更新の手順の詳細については、「[ブート イメージのカスタマイズ](../get-started/customize-boot-images.md)」を参照してください。 ブート イメージの詳細については、「[ブート イメージの管理](../get-started/manage-boot-images.md)」を参照してください。  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

OS の展開時にソフトウェア更新プログラムをインストールするために必要となるソフトウェアの更新ポイントでは、WSUS が必要です。 詳細については、「[ソフトウェアの更新ポイントのインストールと構成](../../sum/get-started/install-a-software-update-point.md)」を参照してください。


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>サイト システム サーバー上のインターネット インフォメーション サービス (IIS)  

IIS は、配布ポイント、状態移行ポイント、および管理ポイントに必要です。 詳細については、「[サイトとサイト システムの前提条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)」をご覧ください。  


### <a name="windows-deployment-services-wds"></a>Windows 展開サービス (WDS)  

バージョン 1802 以前では、PXE の展開には WDS が必要です。 バージョン 1806 以降では、WDS がなくても配布ポイントで PXE を有効にできます。 詳細については、この記事の「 [Windows 展開サービス](#BKMK_WDS) 」をご覧ください。 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>動的ホスト構成プロトコル (DHCP)  

PXE の展開には DHCP が必要です。 PXE を使用してオペレーティング システムを展開するには、アクティブなホストを持つ、機能している DHCP サーバーを用意する必要があります。 PXE 展開に関する詳細については、「[PXE を使用したネットワーク経由での Windows の展開](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>サポートされるオペレーティング システムおよびハード ディスクの構成  

オペレーティング システムを展開するときに Configuration Manager がサポートする OS のバージョンとハード ディスクの構成について詳しくは、「[サポートされるオペレーティング システム](#BKMK_SupportedOS)」および「[対応するディスク構成](#BKMK_SupportedDiskConfig)」をご覧ください。  


### <a name="windows-device-drivers"></a>Windows デバイス ドライバー  

対象のコンピューターに OS をインストールするときには、Windows デバイス ドライバーを使用できます。 Windows デバイス ドライバーは、ブート イメージで Windows PE を実行するときにも使用されます。 詳細については、「[Manage drivers](../get-started/manage-drivers.md)」(ドライバーの管理) を参照してください。  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a> Configuration Manager の依存関係  

このセクションでは、Configuration Manager の OS の展開の前提条件について説明します。  


### <a name="os-image"></a>OS イメージ  

Configuration Manager の OS イメージは、Windows Imaging (WIM) ファイル形式で格納されます。 これらのイメージは、参照ファイルおよび参照フォルダーのコレクションを圧縮したものであり、 コンピューターへの OS のインストールおよび構成を正常に行うために必要です。 詳しくは、[OS イメージの管理](../get-started/manage-operating-system-images.md)に関するページをご覧ください。  


### <a name="driver-catalog"></a>ドライバー カタログ  

デバイス ドライバーを展開するには、まずデバイス ドライバーをインポートしてこれを有効化し、Configuration Manager クライアントがアクセスできる配布ポイントで利用可能にします。 ドライバー カタログの詳細については、「[ドライバーの管理](../get-started/manage-drivers.md)」を参照してください。  


### <a name="management-point"></a>管理ポイント  

管理ポイントは、クライアントと Configuration Manager サイト間で情報を転送します。 クライアントは管理ポイントを使用して、OS を展開するためのタスク シーケンスを実行します。 タスク シーケンスの詳細については、「[タスクの自動化計画に関する考慮事項](planning-considerations-for-automating-tasks.md)」を参照してください。  


### <a name="distribution-point"></a>配布ポイント  

配布ポイントは、イメージやドライバーのパッケージなど、OS を展開するのに使用されるデータを格納するために、ほとんどの展開において使用されます。 タスク シーケンスは通常、OS を展開するために配布ポイントからデータを取得します。 配布ポイントをインストールして、コンテンツを管理する方法の詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  


### <a name="pxe-enabled-distribution-point"></a>PXE 対応配布ポイント  

PXE を使った展開を行うには、クライアントからの PXE 要求を受け入れるように配布ポイントを構成します。 詳細については、[配布ポイントの構成](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)に関するページを参照してください。


### <a name="multicast-enabled-distribution-point"></a>マルチキャスト対応の配布ポイント  

マルチキャストを使って OS の展開を最適化するには、配布ポイントがマルチキャストをサポートするように構成します。 詳細については、[配布ポイントの構成](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)に関するページを参照してください。   


### <a name="state-migration-point"></a>状態移行ポイント  

並列展開および更新展開用にユーザー状態のデータをキャプチャして復元する場合、別のコンピューターにユーザー状態データを格納するように状態移行ポイントを構成します。  

状態移行ポイントを構成する方法の詳細については、「 [状態移行ポイント](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)」をご覧ください。  

ユーザー状態をキャプチャして復元する方法の詳細については、「[ユーザー状態の管理](../get-started/manage-user-state.md)」をご覧ください。  


### <a name="reporting-services-point"></a>レポート サービス ポイント  

OS の展開に Configuration Manager レポートを使用するには、レポート ポイントをインストールして構成します。 詳細については、「[レポートの概要](../../core/servers/manage/introduction-to-reporting.md)」をご覧ください。  


### <a name="security-permissions-for-os-deployments"></a>OS 展開でのセキュリティ アクセス許可  

**[オペレーティング システム展開マネージャー]** セキュリティ ロールは、変更のできない組み込みのセキュリティ ロールです。 しかし、このセキュリティ ロールをコピーして、変更を加え、変更を新しいカスタム セキュリティ ロールとして保存することができます。 OS の展開に直接適用できるアクセス許可を次に示します。  

- **ブート イメージ パッケージ**:作成、削除、変更、フォルダーの変更、オブジェクトの移動、読み取り、セキュリティ スコープの設定  

- **デバイス ドライバー**:作成、削除、変更、フォルダーの変更、レポートの変更、オブジェクトの移動、読み取り、レポートの実行  

- **ドライバー パッケージ**:作成、削除、変更、フォルダーの変更、オブジェクトの移動、読み取り、セキュリティ スコープの設定  

- **オペレーティング システム イメージ**:作成、削除、変更、フォルダーの変更、オブジェクトの移動、読み取り、セキュリティ スコープの設定  

- **オペレーティング システム アップグレード パッケージ**:作成、削除、変更、フォルダーの変更、オブジェクトの移動、読み取り、セキュリティ スコープの設定  

- **タスク シーケンス パッケージ**:作成、タスク シーケンス メディアの作成、削除、変更、フォルダーの変更、レポートの変更、オブジェクトの移動、読み取り、レポートの実行、セキュリティ スコープの設定  

詳細については、「[カスタム セキュリティ ロールの作成](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)」をご覧ください。  


### <a name="security-scopes-for-os-deployments"></a>OS 展開のセキュリティ スコープ  

セキュリティ スコープを使用すると、管理者は、OS とブート イメージ、ドライバー パッケージ、タスク シーケンス パッケージなど、OS の展開で使用される保護可能なオブジェクトにアクセスすることができます。 詳細については、「 [セキュリティ スコープ](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)」をご覧ください。  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Windows 展開サービス  

バージョン 1802 以前では、PXE またはマルチキャストをサポートするように構成する配布ポイントと同じサーバーに、Windows 展開サービス (WDS) をインストールする必要があります。 WDS は、サーバー OS に含まれています。 PXE 展開では、PXE ブートを行うサービスは WDS です。 PXE 用に配布ポイントがインストールされ、有効化された場合、Configuration Manager は、WDS PXE ブート機能を使用する WDS にプロバイダーをインストールします。  

バージョン 1806 以降では、WDS がなくても配布ポイントで PXE を有効にできます。 詳しくは、[配布ポイントのインストールと構成](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)に関するページで **[Windows 展開サービスなしで PXE レスポンダーを有効にする]** オプションをご覧ください。


> [!NOTE]  
>  サーバーの再起動が必要な場合、WDS のインストールに失敗する場合があります。 


### <a name="wds-requirements"></a>WDS の要件  

-   WDS のサーバーへのインストールには、管理者がローカルの Administrators グループのメンバーであることが必要です。  

-   WDS サーバーが、Active Directory ドメインのメンバーか、Active Directory ドメインのドメイン コントローラーであること。 すべての Windows ドメインおよびフォレストの構成が WDS をサポートしていること。  

-   プロバイダーがリモート サーバーにインストールされている場合は、サイト サーバーとリモート プロバイダーに WDS をインストールします。  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> 同じサーバー上に、WDS と DHCP がある場合の考慮事項  

DHCP を実行するサーバーで配布ポイントを同時にホストする場合は、次の構成の問題を考慮してください。  

-   アクティブなスコープを持つ、機能している DHCP サーバーが必要です。 WDS は、DHCP サーバーを必要とする PXE を使用します。  

-   WDS を実行するには DNS サーバーが必要です。  

-   WDS サーバー上で次の UDP ポートを開く必要があります。  

    -   ポート 67 (DHCP)  

    -   ポート 69 (TFTP)  

    -   ポート 4011 (PXE)  

    > [!NOTE]  
    >  サーバーで DHCP の承認が必要な場合、サーバーで DHCP クライアント用のポート 68 を開く必要があります。  

-   DHCP と WDS は両方ともポート番号 67 を必要とします。 WDS と DHCP を同時にホストする場合、PXE 用に構成した DHCP または配布ポイントを別のサーバーに移動できます。 または、次の手順を使用して、別のポートをリッスンするように WDS サーバーを構成できます。  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>別のポートをリッスンするように WDS サーバーを構成するには  

1.  次のレジストリ キーを変更します。  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  レジストリ値 **UseDHCPPorts** を **0** に設定します。  

3.  新しい構成を適用するには、サーバーで次のコマンドを実行します。  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> バージョン 1810 以前では、DHCP サーバーも実行しているサーバーで、WDS なしで PXE レスポンダーを使用することはサポートされていません。
>
> バージョン 1902 以降では、Windows 展開サービスのない配布ポイントで PXE レスポンダーを有効にするときは、DHCP サービスと同じサーバーでもかまわなくなりました。 詳細については、「[PXE 要求を許可するために少なくとも 1 つの配布ポイントを構成する](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure)」を参照してください。


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a> サポートされるオペレーティング システム  

[クライアントとデバイスでサポートされるオペレーティング システム](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)に関するページでサポート対象クライアントとして示されているすべての Windows オペレーティング システムは OS 展開に対応しています。  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a> 対応するディスク構成  

次の表は、Configuration Manager の OS 展開での使用がサポートされている参照コンピューターおよび展開先コンピューターのハード ディスク構成の組み合わせを示します。  

|参照コンピューターのハード ディスク構成|展開先コンピューターのハード ディスク構成|  
|------------------------------------------------|--------------------------------------------------|  
|ベーシック ディスク|ベーシック ディスク|  
|ダイナミック ディスク上のシンプル ボリューム|ダイナミック ディスク上のシンプル ボリューム|  

Configuration Manager では、シンプル ボリュームで構成されたコンピューターからの OS イメージのキャプチャのみをサポートしています。 次のハード ディスク構成はサポートされません。  

-   スパン ボリューム  

-   ストライプ ボリューム (RAID 0)  

-   ミラー ボリューム (RAID 1)  

-   パリティ ボリューム (RAID 5)  

次の表は、Configuration Manager の OS 展開でサポートされていない参照および展開先コンピューターの追加のハード ディスク構成を示します。  

|参照コンピューターのハード ディスク構成|展開先コンピューターのハード ディスク構成|  
|------------------------------------------------|--------------------------------------------------|  
|ベーシック ディスク|ダイナミック ディスク|  



## <a name="next-steps"></a>次のステップ

- [オペレーティング システムの展開用のサイト システムの役割を準備する](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [オペレーティング システムの展開の準備](../get-started/prepare-for-operating-system-deployment.md)
