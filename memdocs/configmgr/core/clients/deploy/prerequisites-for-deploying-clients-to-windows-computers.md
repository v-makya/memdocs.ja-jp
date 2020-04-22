---
title: Windows クライアント展開の前提条件
titleSuffix: Configuration Manager
description: Windows コンピューターに Configuration Manager クライアントを展開するための前提条件について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d4cd7ffe38f7191a5361ad2e89817ea80f9f093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694790"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Configuration Manager で Windows コンピューターにクライアントを展開するための前提条件

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager クライアントを環境で展開するには、次の外部の依存関係、および製品内の依存関係が必要となります。 それぞれのクライアント展開方法に固有の依存関係もあり、それを満たさないとクライアント インストールを正常に実行できません。  

Configuration Manager クライアントのハードウェアおよび OS の最小要件について詳しくは、「[サポートされている構成](../../plan-design/configs/supported-configurations.md)」をご覧ください。  

> [!NOTE]  
> この記事に示されているソフトウェア バージョンの番号は、必要な最小のバージョン番号のみを示します。  


## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a> Windows クライアントの前提条件  

Windows デバイスに Configuration Manager クライアントをいつインストールするかの前提条件を判断するには次の情報を使用します。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

|コンポーネント|[説明]|  
|---|---|  
|Windows インストーラー バージョン 3.1.4000.2435|Windows インストーラーの更新 (.msp) ファイルを、パッケージおよびソフトウェアの更新に使用できるようにするために必要となります。|  
|Microsoft バックグラウンド インテリジェント転送サービス (BITS) バージョン 2.5|クライアント コンピューターと Configuration Manager サイト システムの間でデータが転送されるときのネットワーク負荷を軽減するために必要となります。 BITS は、クライアント インストール中に自動的にはダウンロードされません。 BITS がコンピューターにインストールされると通常、インストールを完了するために再起動が必要となります。<br /><br /> ほとんどのオペレーティング システムに BITS が含まれています。 そうでない場合は、Configuration Manager クライアントをインストールする前に BITS をインストールします。|  
|Microsoft タスク スケジューラ|クライアントのインストールを完了するために、クライアントでこのサービスを有効にします。|  
|SHA-2 コード署名のサポート|バージョン 1906 以降では、クライアントには、SHA-2 コード署名アルゴリズム アルゴリズムのサポートが必要です。 詳細については、[SHA-2 コード署名のサポート](#bkmk_sha2)に関するページをご覧ください。|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a>SHA-2 コード署名のサポート

<!--SCCMDocs-pr#3404-->
SHA-1 アルゴリズムの弱点と業界標準への整合性のため、Microsoft は、より安全な SHA-2 アルゴリズムを使用した Configuration Manager のバイナリにのみ署名するようになりました。 従来の Windows OS バージョンでは、SHA-2 コード署名をサポートするための更新が必要です。 詳細については、「[Windows および WSUS の 2019 SHA-2 コード署名サポートの要件](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus)」を参照してください。

これらの OS バージョンを更新しない場合、Configuration Manager クライアントのバージョン 1906 をインストールできません。 この動作は、新しいクライアントのインストールまたは以前のバージョンからの更新のいずれにも適用されます。

更新されていないバージョン、または上記のバージョンよりも古いバージョンの Windows でクライアントを管理する必要がある場合は、Configuration Manager 拡張相互運用性クライアント (EIC) バージョン 1902 を使用します。 詳細については、[拡張相互運用性クライアント](../../understand/interoperability-client.md)に関するページをご覧ください。

> [!Tip]  
> [自動クライアント更新](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)を使用しないで、別のメカニズムを使用してクライアントを更新する場合は、必ず ccmsetup のバージョンを更新してください。 古いバージョンの ccmsetup では、バージョン 1906 クライアント バイナリで新しい SHA-2 コード署名証明書が正しく検証されない場合があります。 たとえば、ccmsetup.exe をファイル共有にコピーする場合やグループ ポリシーで ccmsetup.msi を使用する場合などです。<!-- 4963362 -->
>
> 次のクライアント更新メカニズムは影響を受けません。
>
> - クライアント プッシュ インストール: サイトのクライアント パッケージを使用
> - ソフトウェアの更新に基づいたインストール: サイトの更新を WSUS に再発行
> - Intune MDM で管理された Windows デバイス: このメカニズムのサポートされているバージョンでは既に SHA-2 コード署名がサポートされていますが、その場合でも最新の ccmsetup.msi を使用することが重要です。

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a> Configuration Manager の外部の依存関係、およびインストール中の自動ダウンロードされる外部の依存関係  

Configuration Manager クライアントには外部の依存関係があります。 これらの依存関係は、クライアント コンピューターの OS バージョンやインストールされたソフトウェアによります。  

インストールを完了するためにクライアントにこれらの依存関係が必要な場合は、それらが自動的にインストールされます。  

|コンポーネント|[説明]|  
|---|---|  
|Windows Update エージェント バージョン 7.0.6000.363|更新プログラムの検出および展開のサポートに Windows で必要となります。|  
|Microsoft Core XML Services (MSXML) バージョン 6.20.5002 以降|Windows で XML ドキュメントを処理できるようにするために必要となります。|  
|Microsoft Remote Differential Compression (RDC)|ネットワークのデータ転送を最適化するために必要となります。|  
|Microsoft Visual C++ 2013 再頒布可能パッケージ バージョン 12.0.21005.1|クライアントのオペレーションをサポートするために必要となります。 クライアント コンピューターにこの更新プログラムをインストールする場合、インストールを完了するために再起動が必要になる可能性があります。|  
|Microsoft Visual C++ 2005 再頒布可能バージョン 8.0.50727.42|1606 以前のバージョンの場合、Microsoft SQL Server Compact オペレーションをサポートするために必要です。|  
|Windows Imaging APIs 6.0.6001.18000|Configuration Manager が Windows イメージ (.wim) ファイルを管理するのを許可するために必要となります。|  
|Microsoft Policy Platform 1.2.3514.0|クライアントがコンプライアンス設定を評価するのを許可するために必要となります。|  
|Microsoft .NET Framework バージョン 4.5.2|クライアントのオペレーションをサポートするために必要となります。 Microsoft .NET Framework バージョン 4.5 以降がインストールされていない場合は、クライアント コンピューターに自動的にインストールされます。 詳細については、「[Microsoft .NET Framework バージョン 4.5.2 に関する追加情報](#dotNet)」を参照してください。|  
|Microsoft SQL Server Compact 4.0 SP1 コンポーネント|クライアント オペレーションに関連した情報を保存するために必要となります。|  

> [!Important]
> アプリケーション カタログの Silverlight ユーザー エクスペリエンスは、Current Branch バージョン 1806 以降では、サポートされません。 バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  
>
> 詳細については、以下の記事を参照してください。
>
> - [ソフトウェア センターの構成](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [削除された機能と非推奨の機能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> アプリケーション カタログ Web サイトのユーザー エクスペリエンスをまだ使用していない場合、クライアントには Microsoft Silverlight 5.1.41212.0 が必要です。 クライアントは Silverlight を自動的にインストールしません。 アプリケーション カタログの主な機能はソフトウェア センターに含まれるようになりました。<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a> Microsoft .NET Framework バージョン 4.5.2 に関する追加情報  

> [!NOTE]  
> .NET 4.0、4.5、4.5.1 はサポートされなくなりました。 詳細については、[Microsoft .NET Framework のサポート ライフサイクル ポリシーに関する FAQ](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework) を参照してください。  

インストールを完了するには、Microsoft .NET Framework バージョン 4.5.2 の再起動が必要な場合があります。 システム トレイに **[再起動が必要]** 通知が表示されます。 次の一般的なシナリオではクライアント コンピューターの再起動が必要です。  

- .NET アプリケーションまたはサービスがコンピューター上で実行されている。  

- .NET インストールに必要な 1 つ以上 のソフトウェア更新プログラムが不足している。  

- コンピューターで、.NET Framework のソフトウェア更新プログラムの以前のインストールからの再起動が保留されている。  

.NET Framework 4.5.2 をインストールした後、追加の更新プログラムが必要な場合があります。 これらの追加の更新プログラムでは、コンピューターの再起動が追加で必要になることがあります。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

詳細については、[クライアントのサイト システムの役割の決定](plan/determine-the-site-system-roles-for-clients.md)に関するページを参照してください。  

|コンポーネント|[説明]|  
|---|---|  
|管理ポイント|Configuration Manager クライアントを展開するには、管理ポイントは必要ありません。 クライアントでは、サイト情報を転送するために管理ポイントが必要です。 管理ポイントがないと、クライアント コンピューターを管理できません。|  
|配布ポイント|配布ポイントはオプションですが、クライアントの展開および管理において推奨されるサイト システムの役割です。 すべての配布ポイントは、クライアント ソース ファイルをホストします。 クライアントは、クライアントの展開または更新中にソース ファイルをダウンロードする最寄りの配布ポイントを検索します。 サイトに配布ポイントがない場合、コンピューターは管理ポイントからクライアント ソース ファイルをダウンロードします。|  
|フォールバック ステータス ポイント|フォールバック ステータス ポイントはオプションですが、クライアント展開において推奨されるサイト システムの役割です。 フォールバック ステータス ポイントにより、クライアントの展開が追跡され、Configuration Manager サイトのコンピューターは、管理ポイントとやり取りできないときに状態メッセージを送信できるようになります。|  
|レポート サービス ポイント|レポート サービス ポイントはオプションですが、推奨されるサイト システムの役割です。 クライアントの展開と管理に関連するレポートが表示されます。 詳細については、「[レポートの概要](../../servers/manage/introduction-to-reporting.md)」をご覧ください。|  

### <a name="installation-method-dependencies"></a>インストール方法の依存関係  

次の前提条件は、クライアント インストールのさまざまな方法に固有です。  

#### <a name="client-push-installation"></a>クライアント プッシュ インストール  

- サイトでは、クライアント プッシュ インストール アカウントを使用してコンピューターに接続し、クライアントをインストールします。 これらのアカウントを [クライアント プッシュ インストールのプロパティ] の **[アカウント]** タブで指定します。 アカウントは、展開先のコンピューターでローカルの管理者グループのメンバーである必要があります。  

    クライアント プッシュ インストール アカウントを指定しない場合、サイト サーバーではそのコンピューター アカウントが使用されます。  

- クライアントをインストールしているコンピューターがサイトによって検出される必要があります。 少なくとも 1 つの Configuration Manager 探索方法が必要です。  

- コンピューターに ADMIN$ 共有が必要です。  

- 検出されたリソースに Configuration Manager クライアントを自動的にプッシュするには、[クライアント プッシュ インストールのプロパティ] で **[割り当てられたリソースへのクライアント プッシュ インストールを有効にする]** オプションを選択します。  

- クライアント コンピューターは、配布ポイントまたは管理ポイントと通信してソース ファイルをダウンロードする必要があります。  

- Kerberos の相互認証が必要な場合、クライアントは信頼された Active Directory フォレスト内にある必要があります。 Windows の Kerberos は、相互認証を Active Directory に依存しています。<!--1358204-->  

クライアント プッシュを使用するには、次のセキュリティ アクセス許可が必要です。  

- クライアント プッシュ インストール アカウントを構成する: **[サイト]** オブジェクトの **[変更]** および **[読み取り]** アクセス許可。  

- クライアント プッシュを使用してクライアントをコレクション、デバイス、クエリにインストールする: **[コレクション]** オブジェクトの **[リソースの変更]** および **[読み取り]** アクセス許可。  

**[インフラストラクチャの管理者]** の既定のセキュリティ ロールには、クライアント プッシュ インストールを管理するのに必要な許可が含まれています。  

#### <a name="software-update-point-based-installation"></a>ソフトウェアの更新ポイント経由のインストール  

- Active Directory スキーマを拡張していない場合、または別のフォレストからクライアントをインストールする場合は、グループ ポリシーを使用して CCMSetup.exe のインストール パラメーターをプロビジョニングします。 詳細については、[クライアント インストールのプロパティの準備方法](deploy-clients-to-windows-computers.md#BKMK_Provision)に関するページを参照してください。  

- Configuration Manager クライアントをソフトウェアの更新ポイントに発行します。  

- ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。  

Configuration Manager ソフトウェア更新プログラムの管理に必要なセキュリティのアクセス許可については、[ソフトウェア更新プログラムの前提条件](../../../sum/plan-design/prerequisites-for-software-updates.md)に関するページを参照してください。  

#### <a name="group-policy-based-installation"></a>グループ ポリシーを使用したインストール  

- Active Directory スキーマを拡張していない場合、または別のフォレストからクライアントをインストールする場合は、グループ ポリシーを使用して CCMSetup.exe のインストール パラメーターをプロビジョニングします。 詳細については、[クライアント インストールのプロパティの準備方法](deploy-clients-to-windows-computers.md#BKMK_Provision)に関するページを参照してください。  

- ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。  

#### <a name="logon-script-based-installation"></a>ログオン スクリプトを使用したインストール  

ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。 ただし、CCMSetup.exe を次のコマンド ライン パラメーターで指定した場合を除きます: `ccmsetup /source`  

#### <a name="manual-installation"></a>手動インストール  

ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。 ただし、CCMSetup.exe を次のコマンド ライン パラメーターで指定した場合を除きます: `ccmsetup /source`  

#### <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM のインストール

- Microsoft Intune サブスクリプションと適切なライセンスが必要です。  

- デバイスは、インターネット ベースでない場合でもインターネットにアクセスできる必要があります。  

- ユース ケースに応じて、次のテクノロジのいずれか、または両方が必要になる場合もあります。  

    - Azure Active Directory  

    - クラウド管理ゲートウェイ  

#### <a name="workgroup-computer-installation"></a>ワークグループ コンピューターのインストール  

Configuration Manager サイト サーバーのドメイン内のリソースにアクセスするには、このサイト用にネットワーク アクセス アカウントを構成します。  

ネットワーク アクセス アカウントの構成方法の詳細については、[コンテンツ管理の基本的な概念](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)に関するページを参照してください。  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>ソフトウェアの配布を使用したインストール (アップグレードのみ)  

- Active Directory スキーマを拡張していない場合、または別のフォレストからクライアントをインストールする場合は、グループ ポリシーを使用して CCMSetup.exe のインストール パラメーターをプロビジョニングします。 詳細については、[クライアント インストールのプロパティの準備方法](deploy-clients-to-windows-computers.md#BKMK_Provision)に関するページを参照してください。

- ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。  

アプリケーション管理を使用して Configuration Manager クライアントをアップグレードするのに必要なセキュリティのアクセス許可については、「[アプリケーション管理に関するセキュリティとプライバシー](../../../apps/plan-design/security-and-privacy-for-application-management.md)」を参照してください。  

#### <a name="automatic-client-upgrades"></a>自動のクライアント アップグレード  

自動のクライアント アップグレードを構成するには、セキュリティの役割である **[完全な権限を持つ管理者]** のメンバーである必要があります。  

### <a name="firewall-requirements"></a>ファイアウォールの要件  

サイト システム サーバーと Configuration Manager クライアントをインストールするコンピューターとの間にファイアウォールがある場合は、[クライアントの Windows ファイアウォールとポートの設定](windows-firewall-and-port-settings-for-clients.md)に関するページを参照してください。  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a> モバイル デバイス クライアントの前提条件  

Configuration Manager クライアントをモバイル デバイスにインストールして登録する場合は、以下の情報を使用して前提条件を判断します。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係

- モバイル デバイスに必要な証明書の展開と管理を行う Microsoft 企業証明機関 (CA) と証明書テンプレート。  

    発行する証明機関は、登録プロセス中モバイル デバイスのユーザーからの証明書要求を自動的に承認する必要があります。  

    証明書の要件の詳細については、[証明書プロファイルのセキュリティとプライバシー](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md)に関するページを参照してください。  

- モバイル デバイスを登録できるユーザーを含んだセキュリティ グループ。  

    このセキュリティ グループは、モバイル デバイスの登録中に使用される証明書テンプレートを構成するのに使用されます。  

- 省略可能ですがお勧めします: **ConfigMgrEnroll** という名前の DNS エイリアス (CNAME レコード)。 登録プロキシ ポイントのサーバー名用にこのエイリアスを構成します。  

    この DNS エイリアスは登録サービスの自動検出をサポートするために必要になります。 この DNS レコードを構成しない場合は、ユーザーが登録プロセスの一環として登録プロキシ ポイントの名前を手動で指定する必要があります。  

- 登録ポイントと登録プロキシ ポイント サイト システムの役割を実行するコンピューター用サイト システムの役割の依存関係。  

    詳細については、[サイト システム サーバーでサポートされるオペレーティング システム](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)に関するページを参照してください。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係

詳細については、[クライアントのサイト システムの役割の決定](plan/determine-the-site-system-roles-for-clients.md)に関するページを参照してください。  

- HTTPS クライアント接続用に構成され、モバイル デバイスが有効な管理ポイント  

    管理ポイントは、Configuration Manager クライアントをモバイル デバイスをインストールするのに常に必要となります。 HTTPS の構成要求とモバイル デバイス用の有効化に加えて、管理ポイントはインターネット FQDN で構成され、インターネットからのクライアント接続を許可する必要があります。  

- 登録ポイントおよび登録プロキシ ポイント  

    登録プロキシ ポイントはモバイル デバイスからの登録要求を管理し、登録ポイントは登録プロセスを完了します。 登録ポイントはサイト サーバーと同じ Active Directory フォレストにある必要がありますが、登録プロキシ ポイントは別のフォレストに設けることができます。  

- モバイル デバイス登録用のクライアント設定  

    ユーザーがモバイル デバイスを登録し、少なくとも 1 つの登録プロファイルを構成できるようにクライアント設定を構成します。  

- レポート サービス ポイント  

    レポート サービス ポイントはオプションですが、モバイル デバイスの登録やクライアント管理に関するレポートを表示できる、推奨されるサイト システムの役割です。  

    詳細については、「[レポートの概要](../../servers/manage/introduction-to-reporting.md)」をご覧ください。  

- モバイル デバイス用に登録を構成するには、次のセキュリティのアクセス許可が必要です。  

    - 登録サイト システムの役割を追加、変更、削除するには: **サイト** オブジェクトのアクセス許可の**変更**  

    - 登録用にクライアント設定を構成するには: 既定のクライアント設定には**サイト** オブジェクトの**変更**のアクセス許可、カスタムのクライアント設定には**クライアント エージェント**のアクセス許可が必要です。  

    **[完全な権限を持つ管理者]** の既定のセキュリティ ロールには、登録サイト システムの役割を構成するのに必要なアクセス許可が含まれています。  

- 登録されたモバイル デバイスを管理するには、次のセキュリティのアクセス許可が必要です。  

    - モバイル デバイスをワイプする、またはインベントリから削除するには: **コレクション** オブジェクトの**リソースの削除**。  

    - ワイプまたはインベントリからの削除のコマンドを取り消すには: **コレクション** オブジェクトの**リソースの削除**。  

    - モバイル デバイスを許可またはブロックするには: **コレクション** オブジェクトの**リソースの変更**。  

    - モバイル デバイスでリモート ロック、またはパスコードのリセットを実行するには: **コレクション** オブジェクトの**リソースの変更**。  

    **[オペレーションの管理者]** の既定のセキュリティ ロールには、モバイル デバイスを管理するのに必要なアクセス許可が含まれています。  

    セキュリティのアクセス許可を構成する方法の詳細については、[ロール ベース管理の基礎](../../understand/fundamentals-of-role-based-administration.md)と、[ロール ベース管理の構成](../../servers/deploy/configure/configure-role-based-administration.md)に関するページを参照してください。  

### <a name="firewall-requirements"></a>ファイアウォールの要件

ルーターやファイアウォール、および該当する場合は Windows ファイアウォールなど、介在するネットワーク デバイスは、モバイル デバイスの登録に関連付けられたトラフィックを許可する必要があります。  

- モバイル デバイスと登録プロキシ ポイントの間: HTTPS (既定では TCP 443)  

- 登録プロキシ ポイントと登録ポイントの間: HTTPS (既定では TCP 443)  

プロキシ Web サーバーを使用する場合は、SSL トンネリング用に構成する必要があります。 モバイル デバイスでは SSL ブリッジングはサポートされません。  
