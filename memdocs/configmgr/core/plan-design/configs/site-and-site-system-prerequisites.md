---
title: サイトの前提条件
titleSuffix: Configuration Manager
description: Windows コンピューターを Configuration Manager サイト システム サーバーとして構成する方法について説明します。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d4fb94d0ab64cb7c3dc3128c982b0c2b162b22b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702160"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Configuration Manager のサイトとサイト システムの前提条件

*適用対象:Configuration Manager (Current Branch)*

Windows ベースのコンピューターを Configuration Manager サイト システム サーバーとして使用するには、特定の構成が必要です。

ソフトウェア更新ポイント用の Windows Server Update Services (WSUS) など、一部の製品では、その製品のドキュメントで、使用に関する追加の前提条件と制限を確認する必要があります。 ここでは、Configuration Manager で使用するために行う必要のある構成についてのみ説明します。

.NET Framework の詳細については、「[ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)」を参照してください。


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> 一般的な要件と制限事項

すべてのサイト システム サーバーに以下の要件が適用されます。

- 各サイト システム サーバーでは、64 ビットの OS を使用する必要があります。 唯一の例外は、配布ポイント サイト システムの役割です。これは、一部の 32 ビット版のオペレーティング システムにインストール可能です。  

- サイト システムは、オペレーティング システムの Server Core インストールではサポートされません。 例外は、配布ポイント サイト システムの役割に対して、Server Core インストールがサポートされていることです。 詳細については、「[Configuration Manager サイト システム サーバーでサポートされるオペレーティング システム](supported-operating-systems-for-site-system-servers.md)」を参照してください。  

- サイト システム サーバーは、インストール後、次を変更できません。  

    - サイト システム コンピューターが配置されているドメインのドメイン名 (**ドメイン名の変更**とも呼ばれます)。  

    - コンピューターのドメイン メンバーシップ。  

    - コンピューターの名前です。  

    これらの項目のいずれかを変更する必要がある場合は、まず、コンピューターからサイト システムの役割を削除します。 変更が完了した後、役割を再インストールします。 サイト サーバーに影響する変更の場合は、まず、サイトをアンインストールします。 変更が完了した後、サイトを再インストールします。  

- サイト システムの役割は、Windows Server クラスターのインスタンスではサポートされません。 唯一の例外は、サイト データベース サーバーです。 詳細については、[Configuration Manager サイト データベースでの SQL Server クラスターの使用](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)に関するページを参照してください。  

    バージョン 1810 以降では、Configuration Manager セットアップ プロセスで、フェールオーバー クラスタリング用の Windows の役割でコンピューターにサイト サーバーの役割がインストールされるのがブロックされなくなりました。 SQL Always On では、このロールが必要なため、以前はサイト サーバーにサイト データベースを同時に配置できませんでした。 この変更により、SQL Always On とパッシブ モードのサイト サーバーを使用して、少ないサーバー数で高可用性サイトを作成できます。 詳細については、[高可用性オプション](../../servers/deploy/configure/high-availability-options.md)に関するページを参照してください。 <!--3607761, fka 1359132-->  

- Configuration Manager サービスについては、スタートアップの種類やログオン方法の設定の変更はサポートされていません。 そのようにすると、主要なサービスが正しく実行できなくなる可能性があります。  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Windows Server 2012 以降のオペレーティング システムの前提条件  

Windows Server 2012 以降のサイト システム サーバーと役割に関する特定の前提条件については、この記事の主要なセクションを参照してください。

- [中央管理サイトおよびプライマリ サイト サーバー](#bkmk_2012sspreq)
- [セカンダリ サイト サーバー](#bkmk_2012secpreq)
- [データベース サーバー](#bkmk_2012dbpreq)
- [SMS プロバイダー サーバー](#bkmk_2012smsprovpreq)
- [アプリケーション カタログ Web サイト ポイント](#bkmk_2012acwspreq)
- [アプリケーション カタログ Web サービス ポイント](#bkmk_2012ACwsitepreq)
- [資産インテリジェンス同期ポイント](#bkmk_2012AIpreq)
- [証明書登録ポイント](#bkmk_2012crppreq)
- [配布ポイント](#bkmk_2012dppreq)
- [Endpoint Protection ポイント](#bkmk_2012EPPpreq)
- [登録ポイント](#bkmk_2012Enrollpreq)
- [登録プロキシ ポイント](#bkmk_2012EnrollProxpreq)
- [フォールバック ステータス ポイント](#bkmk_2012FSPpreq)
- [管理ポイント](#bkmk_2012MPpreq)
- [レポート サービス ポイント](#bkmk_2012RSpoint)
- [サービス接続ポイント](#bkmk_SCPpreq)
- [ソフトウェアの更新ポイント](#bkmk_2012SUPpreq)
- [状態移行ポイント](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a> 中央管理サイトおよびプライマリ サイト サーバー

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework 3.5

- RDC (Remote Differential Compression)  

- サイト サーバー以外のサーバー上でソフトウェアの更新ポイントを使用する場合は、サイト サーバーに WSUS 管理コンソールをインストールしてください。

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- 中央管理サイトまたはプライマリ サイトをインストールまたはアップグレードする前に、インストールまたはアップグレードする Configuration Manager のバージョンで必要な Windows アセスメント & デプロイメント キット (ADK) のバージョンをインストールします。 詳細については、「[Windows 10 ADK](support-for-windows-10.md#windows-10-adk)」を参照してください。  

- この要件の詳細については、[OS の展開に対するインフラストラクチャ要件](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)に関するページを参照してください。  

### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル  

- Configuration Manager はサイト サーバーをインストールするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

- 中央管理サイトとプライマリ サイトには、該当する再頒布可能ファイルの x86 および x64 バージョンの両方が必要です。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a> セカンダリ サイト サーバー

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework 3.5

- RDC (Remote Differential Compression)  

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル

- Configuration Manager はサイト サーバーをインストールするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

- セカンダリ サイトには x64 バージョンのみが必要です。  

### <a name="default-site-system-roles"></a>既定のサイト システムの役割  

- 既定では、セカンダリ サイトに**管理ポイント**と**配布ポイント**がインストールされます。  

- セカンダリ サイト サーバーが、それらのサイト システムの役割に対する前提条件を満たしていることを確認します。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a> データベース サーバー  

### <a name="remote-registry-service"></a>リモート レジストリ サービス  

- Configuration Manager サイトのインストール時には、サイト データベースをホストするコンピューターで、**リモート レジストリ** サービスを有効にします。  

### <a name="sql-server"></a>SQL Server  

- 中央管理サイトまたはプライマリ サイトをインストールする前に、サイト データベースをホストする SQL Server のサポートされているバージョンをインストールします。 詳細については、[サポートされている SQL Server のバージョン](support-for-sql-server-versions.md)に関するページを参照してください。  

- セカンダリ サイトをインストールする前に、サポートされているバージョンの SQL Server をインストールすることができます。  

- セカンダリ サイトのインストールの一環として Configuration Manager によって SQL Server Express をインストールする場合は、コンピューターが SQL Server Express を実行する要件を満たしていることを確認します。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> SMS プロバイダー サーバー  

### <a name="windows-adk"></a>Windows ADK

- SMS プロバイダーのインスタンスをインストールするコンピューターには、インストールまたはアップグレードする Configuration Manager のバージョンで必要な Windows ADK のバージョンが必要です。 詳細については、「[Windows 10 ADK](support-for-windows-10.md#windows-10-adk)」を参照してください。  

- 要件の詳細については、「[オペレーティング システムの展開のインフラストラクチャ要件](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)」を参照してください。  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- [管理サービス](../../../develop/adminservice/overview.md)を使っている場合、SMS プロバイダーの役割をホストするサーバーには .NET 4.5 以降が必要です  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager バージョン 1810 には、.NET 4.5.2 以降が必要です。

- Web Server (IIS): すべてのプロバイダーが[管理サービス](../../../develop/adminservice/overview.md)のインストールしようとします。 証明書を HTTPS ポート 443 にバインドするため、このサービスは IIS に依存します。 Configuration Manager は IIS API を使用して、この証明書の構成を確認します。 サイトが[拡張 HTTP](../hierarchy/enhanced-http.md) 用に構成されている場合、Configuration Manager は IIS API を使用して、サイトで生成された証明書をバインドします。 バージョン 2002 以降、サイトでは自動的に、サイトの自己署名証明書が使用されます。

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a>アプリケーション カタログ Web サイト ポイント  

> [!Important]  
> アプリケーション カタログの Silverlight ユーザー エクスペリエンスは、Current Branch バージョン 1806 以降では、サポートされません。 バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  
>
> 詳細については、以下の記事を参照してください。
>
> - [ソフトウェア センターの構成](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [削除された機能と非推奨の機能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS の構成  

- 一般的な HTTP 機能:  

    - 既定のドキュメント  

    - 静的コンテンツ  

- アプリケーションの開発:  

    - ASP.NET 3.5 (および、自動的に選択されるオプション)  

    - ASP.NET 4.5 (および、自動的に選択されるオプション)  

    - .NET 拡張機能 3.5  

    - .NET 拡張機能 4.5  

- セキュリティ:  

    - Windows 認証  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a>アプリケーション カタログ Web サービス ポイント  

> [!Important]  
> アプリケーション カタログの Silverlight ユーザー エクスペリエンスは、Current Branch バージョン 1806 以降では、サポートされません。 バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  
>
> 詳細については、以下の記事を参照してください。
>
> - [ソフトウェア センターの構成](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [削除された機能と非推奨の機能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework 3.5

- ASP.NET 4.5:  

    - HTTP アクティブ化 (および、自動的に選択されるオプション)  

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS の構成

- 一般的な HTTP 機能:  

    - 既定のドキュメント  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  

- アプリケーション開発:  

    - ASP.NET 3.5 (および、自動的に選択されるオプション)  

    - .NET 拡張機能 3.5  

    - ASP.NET 4.5 (および、自動的に選択されるオプション)  

    - .NET 拡張機能 4.5  

### <a name="computer-memory"></a>コンピューターのメモリ  

- このサイト システムの役割をホストするコンピューターには、サイト システムの役割が要求を処理するために、コンピューターの使用可能メモリの最低 5% を空けておく必要があります。  

- このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> 資産インテリジェンス同期ポイント  

### <a name="net-framework"></a>.NET Framework

.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> 証明書登録ポイント  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework

    - HTTP アクティブ化  

### <a name="net-framework"></a>.NET Framework

.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS の構成

- アプリケーション開発:  

    - ASP.NET 3.5 (および、自動的に選択されるオプション)  

    - ASP.NET 4.5 (および、自動的に選択されるオプション)  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  

    - IIS 6 WMI 互換  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a> 配布ポイント  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- RDC (Remote Differential Compression)  

#### <a name="iis-configuration"></a>IIS の構成

- アプリケーション開発:  

    - ISAPI 拡張機能  

- セキュリティ:  

    - Windows 認証  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  

    - IIS 6 WMI 互換  

### <a name="powershell"></a>PowerShell  

- Windows Server 2012 以降では、配布ポイントをインストールする前に、PowerShell 3.0 または 4.0 が必要になります。  

### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル

- Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

- インストールされるバージョンは、コンピューターのプラットフォーム (x86 または x64) によって異なります。  

### <a name="microsoft-azure"></a>Microsoft Azure  

- Microsoft Azure のクラウド サービスを使用して、配布ポイントをホストできます。  

### <a name="to-support-pxe-or-multicast"></a>PXE またはマルチキャストをサポートするには  

- Windows 展開サービスなしで、配布ポイントで PXE レスポンダーを有効にします。  

- Windows 展開サービス (WDS) の Windows サーバー ロールをインストールして構成します。  

    > [!NOTE]  
    > WDS は、PXE またはマルチキャストをサポートするように配布ポイントを構成するときに、Windows Server 2012 以降を実行するサーバーに自動的にインストールされ構成されます。  

- マルチキャスト対応の配布ポイントの場合、SQL Server Native Client がインストールされており、最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。

詳細については、[配布ポイントのインストールと構成](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)に関するページを参照してください。

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> 配布ポイントではコンテンツを転送するときに、Windows に組み込まれた**バックグラウンド インテリジェント転送サービス** (BITS) が使用されます。 配布ポイントの役割では、オプションの BITS IIS サーバー拡張機能をインストールする必要はありません。これは、クライアントではそこに情報がアップロードされないためです。  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection ポイント  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

- .NET Framework 3.5

- Windows Defender の機能 (Windows Server 2016 以降)  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> 登録ポイント  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework 3.5

    - HTTP アクティブ化 (および、自動的に選択されるオプション)  

    - ASP.NET 4.5  

    - Windows Communication Foundation (WCF) サービス<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

> [!Note]
> このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework の再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS の構成

- 一般的な HTTP 機能:  

    - 既定のドキュメント  

- アプリケーション開発:  

    - ASP.NET 3.5 (および、自動的に選択されるオプション)  

    - .NET 拡張機能 3.5  

    - ASP.NET 4.5 (および、自動的に選択されるオプション)  

    - .NET 拡張機能 4.5  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  

### <a name="computer-memory"></a>コンピューターのメモリ

- このサイト システムの役割をホストするコンピューターには、サイト システムの役割が要求を処理するために、コンピューターの使用可能メモリの最低 5% を空けておく必要があります。  

- このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> 登録プロキシ ポイント  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

> [!Note]
> このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework の再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS の構成

- 一般的な HTTP 機能:  

    - 既定のドキュメント  

    - 静的コンテンツ  

- アプリケーションの開発:  

    - ASP.NET 3.5 (および、自動的に選択されるオプション)  

    - ASP.NET 4.5 (および、自動的に選択されるオプション)  

    - .NET 拡張機能 3.5  

    - .NET 拡張機能 4.5  

- セキュリティ:  

    - Windows 認証  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  

### <a name="computer-memory"></a>コンピューターのメモリ

- このサイト システムの役割をホストするコンピューターには、サイト システムの役割が要求を処理するために、コンピューターの使用可能メモリの最低 5% を空けておく必要があります。  

- このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> フォールバック ステータス ポイント

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- BITS サーバー拡張 (および自動的に選択されるオプション)、またはバックグラウンド インテリジェント転送サービス (BITS) (および自動的に選択されるオプション)

#### <a name="iis-configuration"></a>IIS の構成

既定の IIS 構成に加え、次が必要です。  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a> 管理ポイント  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- BITS サーバー拡張 (および自動的に選択されるオプション)、またはバックグラウンド インテリジェント転送サービス (BITS) (および自動的に選択されるオプション)  

### <a name="net-framework"></a>.NET Framework

.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS の構成

- アプリケーション開発:  

    - ISAPI 拡張機能  

- セキュリティ:  

    - Windows 認証  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  

    - IIS 6 WMI 互換  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> レポート サービス ポイント  

### <a name="net-framework"></a>.NET Framework

.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- レポート ポイントをインストールする前に、SQL Server Reporting Services をサポートするために、SQL Server の 1 つ以上のインスタンスをインストールして構成します。  

- SQL Server Reporting Services に使用するインスタンスは、サイト データベースに使用するインスタンスと同じものにすることができます。  

- さらに、そのインスタンスを別の System Center 製品と共有して使用することもできます。ただし、他の System Center 製品に SQL Server のインスタンスの共有に対する制限がない場合に限ります。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a> サービス接続ポイント  

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

> [!Note]
> このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework の再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル

- Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

- サイト システムの役割には、x64 バージョンが必要です。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a> ソフトウェアの更新ポイント  

### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework 3.5

既定の IIS 構成が必要です。

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- ソフトウェアの更新ポイントをインストールする前に、コンピューターに Windows サーバーの役割の Windows Server Update Services をインストールします。  

- 詳細については、[ソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md)に関するページを参照してください。  

> [!NOTE]  
> サイト サーバー以外のサーバーでソフトウェアの更新ポイントを使用する場合は、サイト サーバーに WSUS 管理コンソールをインストールする必要があります。

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> 状態移行ポイント

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能

- .NET Framework 3.5

    - HTTP アクティブ化 (および、自動的に選択されるオプション)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

.NET Framework 3.5 の Windows 機能を有効にします。

また、.NET Framework のサポートされているバージョン (バージョン 4.5 以降) をインストールします。 バージョン 1906 以降では、Configuration Manager は .NET Framework 4.8 をサポートします。

> [!Note]
> このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework の再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

.NET Framework のバージョンの詳細については、次の記事を参照してください。

- [.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [ライフサイクルに関する FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS の構成

- 一般的な HTTP 機能:  

    - 既定のドキュメント  

- アプリケーション開発:  

    - ASP.NET 3.5 (および、自動的に選択されるオプション)  

    - .NET 拡張機能 3.5  

    - ASP.NET 4.5 (および、自動的に選択されるオプション)  

    - .NET 拡張機能 4.5  

- IIS 6 管理互換性:  

    - IIS 6 メタベース互換  

### <a name="sql-server-native-client"></a>SQL Server Native Client

新しいサイトをインストールするときに、Configuration Manager によって SQL Server Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 サイトをインストールした後は、Configuration Manager は SQL Server Native Client をアップグレードしません。 このコンポーネントが最新であることを確認してください。 詳細については、[SQL Server Native Client の前提条件の確認](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) に関するページを参照してください。

