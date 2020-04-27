---
title: サポートされるクライアントとデバイス
titleSuffix: Configuration Manager
description: Configuration Manager がクライアントとデバイスをサポートする OS のバージョンについて説明します。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 57c60fcdadf3e58b59d33ecf2753789122a38ecc
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078687"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Configuration Manager でクライアントとデバイスに対してサポートされる OS のバージョン

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager は、Windows および macOS コンピューター上のクライアント ソフトウェアのインストールをサポートします。  

## <a name="general-requirements-and-limitations"></a>一般的な要件と制限事項

すべてのクライアントの次の要件と制限事項を確認します。

- Configuration Manager サービスについては、スタートアップの種類や**ログオン方法**の設定の変更はサポートされていません。 変更すると、主要なサービスが正しく実行できなくなる可能性があります。

## <a name="windows-computers"></a>Windows コンピューター  

次のバージョンの Windows OS を管理するには、Configuration Manager に含まれているクライアントを使用します。 詳しくは、「[Windows コンピューターにクライアントを展開する方法](../../clients/deploy/deploy-clients-to-windows-computers.md)」をご覧ください。  

### <a name="supported-client-os-versions"></a>サポートされているクライアントの OS のバージョン

- **Windows 10**  

    詳細については、[Windows 10 のサポート](support-for-windows-10.md)に関するページをご覧ください。  

- **Windows 8.1** (x86、x64):Professional、Enterprise

#### <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

<!--3556025-->
[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) は、Microsoft Azure 上で実行されるデスクトップおよびアプリの仮想化サービスです。 バージョン 1906 以降では、Configuration Manager を使用して、Azure で Windows が実行されているこれらの仮想デバイスを管理できます。

ターミナル サーバーと同様に、これらの仮想デバイスの中には、アクティブ ユーザーの同時実行セッションが複数許可されるものもあります。 クライアントのパフォーマンスを支援する目的で、Configuration Manager では、このような複数のユーザー セッションを許可するあらゆるデバイスでユーザー ポリシーが無効になりました。 ユーザー ポリシーを有効にした場合でも、Windows 10 Enterprise マルチセッションやターミナル サーバーを含む、これらのデバイスでは、クライアントによって既定でポリシーが無効化されます。

新しいインストール中、この種類のデバイスが検出されたときにのみ、クライアントによりユーザー ポリシーが無効化されます。 このバージョンに更新した、この種類の既存クライアントの場合、前の動作が存続します。 既存のデバイスでは、複数のユーザー セッションがデバイスで許可されることが検出された場合でも、ユーザー ポリシー設定が構成されます。

このシナリオでユーザー ポリシーが必要で、パフォーマンスに影響する可能性を受け入れる場合は、次のいずれかの方法を使用してユーザー ポリシーを有効にします。

- バージョン 1910 以降では、[クライアント設定](../../clients/deploy/configure-client-settings.md)を使用します。 **[クライアントポリシー]** グループで、次の設定を構成します。**複数のユーザー セッションのユーザー ポリシーを有効にします**。<!-- 4737447 -->

- バージョン 1906 では、Configuration Manager SDK と [SMS_PolicyAgentConfig サーバー WMI クラス](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md)を使用します。 新しい `PolicyEnableUserPolicyOnTS` プロパティを `true` に設定します。

> [!Note]  
> Windows 10 Enterprise マルチセッションを実行しているクライアントで共同管理を使用することはできません。 <!-- SCCMDocs-pr#3950 -->

### <a name="supported-server-os-versions"></a>サポートされているサーバーの OS のバージョン

- **Windows Server 2019**:Standard、Datacenter <sup>[注 1](#bkmk_note1)</sup>  
    (Configuration Manager バージョン 1806 以降。)

- **Windows Server 2016**:Standard、Datacenter <sup>[注 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**:Workgroup、Standard  

- **Windows Server 2012 R2** (x64):Standard、Datacenter <sup>[注 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64):Standard、Datacenter <sup>[注 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

次のバージョンでは具体的に OS の Server Core インストールが参照されます。 <sup>[注 3](#bkmk_note3)</sup>  

Windows Server の半期チャネル バージョンは Server Core インストールです (Windows Server バージョン 1809 など)。 Configuration Manager クライアントとして、これらは関連する Windows 10 の半期チャネル バージョンと同じようにサポートされています。 詳細については、[Windows 10 のサポート](support-for-windows-10.md)に関するページをご覧ください。

- **Windows Server 2019** (x64) <sup>[注 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[注 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[注 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[注 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a> 注 1

Configuration Manager では Windows Server Datacenter エディションがテストおよびサポートされていますが、Windows Server に対して公式に認定されていません。 Windows Server Datacenter エディションに固有の問題に対しては、Configuration Manager の修正プログラムのサポートは提供されません。 Windows Server の認定プログラムについて詳しくは、[Windows Server カタログ](https://www.windowsservercatalog.com/)をご覧ください。

#### <a name="note-2"></a><a name="bkmk_note2"></a> 注 2

[クライアント プッシュ インストール](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)をサポートするには、[ファイルおよび記憶域サービス] サーバー ロールのファイル サーバー サービスを追加します。 Server Core への Windows 機能のインストールについて詳しくは、「[Install roles, role services, and features by using Windows PowerShell cmdlets](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets)」(Windows PowerShell コマンドレットを使用して役割、役割サービス、機能をインストールする) をご覧ください。  

#### <a name="note-3"></a><a name="bkmk_note3"></a> 注 3

新しいソフトウェア センター アプリは、Windows Server Core のどのバージョンでもサポートされていません。<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Windows Embedded コンピューター  

Windows Embedded デバイスを管理するには、デバイス上に Configuration Manager クライアントをインストールします。 詳細については、「[Windows Embedded デバイスへのクライアント展開の計画](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)」を参照してください。  

### <a name="requirements-and-limitations"></a>要件と制限事項

- すべてのクライアント機能は、書き込みフィルターが有効ではない Windows Embedded システムでサポートされます。  

- 次のいずれかを使用するクライアントは、電源管理以外のすべての機能がサポートされます。  

  - Enhanced Write Filter (EWF)

  - RAM ファイル ベースの書き込みフィルター (FBWF)

  - Unified Write Filter (UWF)  

- アプリケーション カタログは、どのような Windows Embedded デバイスについてもサポートされません。  

### <a name="supported-os-versions"></a>サポートされている OS のバージョン  

- **Windows 10 Enterprise** (x86、x64)  

- **Windows 10 IoT Enterprise** (x86、x64)  
    このバージョンには、長期的なサービス チャネル (LTSC) が含まれています。 詳細については、「[Windows 10 IoT Enterprise の概要](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise)」を参照してください。<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry** (x86、x64)

- **Windows Embedded 8 Standard** (x86、x64)

- **Windows Thin PC** (x86、x64)

- **Windows Embedded POSReady 7** (x86、x64)

- **Windows Embedded Standard 7 SP1** (x86、x64)

## <a name="windows-ce-computers"></a>Windows CE コンピューター

Configuration Manager に含まれる Configuration Manager モバイル デバイス レガシ クライアントで Windows CE デバイスを管理します。  

### <a name="requirements-and-limitations"></a>要件と制限事項

- モバイル デバイス クライアントのインストールには、0.78 MB の記憶領域が必要です。 サインインするには、さらに最大で 256 KB の追加の記憶領域が必要な場合があります。

- これらのモバイル デバイスの機能は、プラットフォームとクライアントの種類によって異なります。 サポートされる管理機能の詳細については、「[デバイス管理ソリューションの選択](../choose-a-device-management-solution.md)」を参照してください。  

### <a name="supported-os-versions"></a>サポートされている OS のバージョン

- Windows CE 7.0 (ARM および x86 プロセッサ)  

    > [!Note]
    > Configuration Manager では Windows CE 7.0 のサポートは非推奨とされています。 詳細については、「[削除され、非推奨になった Configuration Manager クライアントの項目](../changes/deprecated/removed-and-deprecated-client.md)」を参照してください。

#### <a name="supported-languages-include"></a>次の言語がサポートされています

- 中国語 (簡体字、繁体字)

- 英語 (米国)

- フランス語 (フランス)

- ドイツ語

- イタリア語

- 日本語  

- 韓国語  

- ポルトガル語 (ブラジル)  

- ロシア語  

- スペイン語 (スペイン)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> 延長セキュリティ更新プログラムと Configuration Manager

[延長セキュリティ更新プログラム (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) は、特定のレガシ Microsoft 製品をサポート終了後に実行する必要があるお客様のための最後の手段となります。 たとえば、Windows 7 です。 これには、製品の延長サポート期間が終了してから最長 3 年間、重大または重要なセキュリティ更新プログラム ([Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc) によって定義されています) が含まれます。

既にサポート ライフサイクルが終了している製品は、Configuration Manager ではサポートされません。 これには、ESU プログラムの対象となるすべての製品が含まれます。 ESU プログラムでリリースされたセキュリティ更新プログラムは、Windows Server Update Services (WSUS) に発行されます。 これらの更新プログラムは、Configuration Manager コンソールに表示されます。 ESU プログラムの対象となる製品は、Configuration Manager での使用がサポートされなくなりましたが、[最新リリース バージョンの Configuration Manager の現在のブランチ](../../servers/manage/updates.md#version-details)を使用して、プログラムでリリースされた Windows セキュリティ更新プログラムを展開およびインストールできます。 Windows 7 を稼働しているデバイスに Windows 10 を展開するために、最新のリリース バージョンを使用することもできます。

Windows ソフトウェア更新プログラムの管理または OS 展開に関係のないクライアント管理機能は、ESU プログラムの対象となるオペレーティング システムではテストされなくなり、引き続き機能することが保証されません。 クライアント管理のサポートを受けるには、できるだけ早く現在のバージョンのオペレーティング システムにアップグレードまたは移行することを強くお勧めします。

## <a name="mac-computers"></a>Mac コンピューター  

macOS 向けの Configuration Manager クライアントで Apple Mac コンピューターを管理します。  

Configuration Manager メディアでは、macOS クライアント インストール パッケージは提供されません。 Microsoft ダウンロード センターからダウンロードしてください ([Microsoft Endpoint Configuration Manager - macOS クライアント (64 ビット)](https://www.microsoft.com/download/details.aspx?id=100850))。  

詳しくは、「[Mac にクライアントを展開する方法](../../clients/deploy/deploy-clients-to-macs.md)」をご覧ください。  

### <a name="requirements-and-limitations"></a>要件と制限事項

- root 以外のアカウント下のコンピューターでは、macOS 用の Configuration Manager クライアントのインストールと実行はサポートされていません。 そのようにすると、主要なサービスが正しく実行できなくなる可能性があります。  

### <a name="supported-versions"></a>サポートされるバージョン

- **macOS Catalina (10.15)** (Configuration Manager サイトのバージョン 1910 以降、および macOS 用構成マネージャー クライアントのバージョン 5.0.8742.1000 以降が必要)

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

## <a name="linux-and-unix-servers"></a>Linux および UNIX サーバー  

> [!Important]  
> Configuration Manager バージョン 1902 では、クライアントとして Linux および UNIX のサポートが削除されます。 廃止は[バージョン 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support) で発表されました。 Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。

Configuration Manager メディアでは、Linux および UNIX クライアント インストール パッケージは提供されません。 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?LinkID=525184)から、**追加のオペレーティング システム用のクライアント**をダウンロードします。 クライアント インストール パッケージに加え、クライアント ダウンロードには、各コンピューター上でクライアントのインストールを管理するスクリプトも含まれています。  

### <a name="requirements-and-limitations"></a>要件と制限事項

- Linux および UNIX 向けクライアントの OS ファイルの依存関係を確認するには、「[Linux および UNIX サーバーへのクライアントの展開の前提条件](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU)」をご覧ください。  

- Linux または UNIX を実行するコンピューターでサポートされている管理機能の概要については、「[UNIX および Linux サーバーにクライアントを展開する方法](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)」をご覧ください。  

- Linux および UNIX のサポートされるバージョンの場合、一覧に示したバージョンには後続のマイナー バージョンがすべて含まれます。 たとえば、CentOS バージョン 6 には CentOS 6.3 が含まれています。 同様に、サービス パックを使用する OS (SUSE Linux Enterprise Server 11 SP1 など) がサポートされている場合は、その OS のバージョンの後続のサービス パックもサポートに含まれます。  

- Linux と UNIX でクライアントをインストールする方法については、「[UNIX および Linux サーバーにクライアントを展開する方法](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)」をご覧ください。  

### <a name="supported-versions"></a>サポートされるバージョン

次のバージョンは、指定された .tar ファイルを使用してサポートされます。  

#### <a name="aix"></a>AIX  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 6.1 (Power)|ccm-Aix61ppc.&lt;ビルド\>.tar|  
|バージョン 7.1 (Power)|ccm-Aix71ppc.&lt;ビルド\>.tar|  

#### <a name="centos"></a>CentOS  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="debian"></a>Debian  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 8 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 8 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;ビルド\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="solaris"></a>Solaris  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 10 x86|ccm-Sol10x86.&lt;ビルド\>.tar|  
|バージョン 10 SPARC|ccm-Sol10sparc.&lt;ビルド\>.tar|  
|バージョン 11 x86|ccm-Sol11x86.&lt;ビルド\>.tar|  
|バージョン 11 SPARC|ccm-Sol11sparc.&lt;ビルド\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 10 SP1 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 10 SP1 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 11 SP1 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 11 SP1 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 12 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 10.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 10.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 12.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 12.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 14.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 14.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 16.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 16.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a> オンプレミス MDM

Configuration Manager には、クライアント ソフトウェアをインストールすることなく、オンプレミスであるモバイル デバイスを管理する組み込みの機能があります。 詳しくは、「[オンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」をご覧ください。  

### <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

- **Windows 10 Pro** (x86、x64)  

- **Windows 10 Pro Enterprise** (x86、x64)  

- **Windows 10 IoT Enterprise** (x86、x64)  
    このバージョンには、長期的なサービス チャネル (LTSC) が含まれています。 詳細については、「[Windows 10 IoT Enterprise の概要](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise)」を参照してください。<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Surface Hub の Windows 10 Team**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!Note]
    > Configuration Manager では、Windows 10 Mobile と Windows 10 Mobile Enterprise のサポートは非推奨となりました。 詳細については、「[削除され、非推奨になった Configuration Manager クライアントの項目](../changes/deprecated/removed-and-deprecated-client.md)」を参照してください。


## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Exchange Server コネクタ  

Configuration Manager は、Configuration Manager クライアントをインストールすることがない、Exchange サーバーに接続するデバイスの限定された管理をサポートしています。 詳しくは、「[Configuration Manager と Exchange によるモバイル デバイスの管理](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」をご覧ください。  

### <a name="supported-versions-of-exchange-server"></a>サポートされている Exchange Server のバージョン

- **Exchange Online (Office 365)** :このバージョンには、Business Productivity Online Standard Suite が含まれます  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** または **Exchange Server 2010 SP2**
