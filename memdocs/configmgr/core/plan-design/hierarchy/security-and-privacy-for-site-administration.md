---
title: サイト管理のセキュリティとプライバシー
titleSuffix: Configuration Manager
description: Configuration Manager でのサイト管理のセキュリティとプライバシーを最適化する
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182261"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Configuration Manager でのサイト管理のセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

この記事には、Configuration Manager のサイトと階層のセキュリティとプライバシーの情報が含まれています。

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a> サイト管理のセキュリティ ガイダンス

Configuration Manager のサイトと階層をセキュリティで保護するのに役立つ、次のガイダンスを使用します。  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>信頼できるソースからセットアップを実行し、通信をセキュリティで保護する

誰かにソース ファイルが改ざんされることを防ぐために、信頼できるソースから Configuration Manager セットアップを実行します。 ファイルをネットワーク上に保存している場合は、ネットワークの場所をセキュリティで保護します。  

ネットワークの場所からセットアップを実行する場合、ファイルがネットワーク経由で転送されるときに攻撃者によって改ざんされるのを防ぐため、セットアップ ファイルのソースの場所とサイト サーバー間で IPsec または SMB 署名を使用します。  

セットアップ ダウンローダーを使用してセットアップに必要なファイルをダウンロードする場合は、これらのファイルが格納されている場所を必ずセキュリティで保護してください。 また、セットアップを実行するときに、この場所の通信チャネルをセキュリティで保護します。  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Active Directory スキーマを拡張して、ドメインにサイトを発行する  

スキーマ拡張は Configuration Manager の実行には必要ありませんが、より安全な環境が作成されます。 クライアントとサイト サーバーでは、信頼できるソースから情報を取得できます。  

クライアントが信頼されていないドメインに属している場合、クライアントのドメインに次のサイト システムの役割を展開します。  

- 管理ポイント  

- 配布ポイント  

> [!NOTE]  
> Configuration Manager の信頼されたドメインには、Kerberos 認証が必要です。 サイト サーバーのフォレストと双方向のフォレストの信頼関係がない別のフォレストにクライアントが存在する場合、これらのクライアントは信頼されていないドメインにあると見なされます。 この目的では外部の信頼は十分ではありません。  

### <a name="use-ipsec-to-secure-communications"></a>IPsec を使用して通信をセキュリティで保護する

Configuration Manager では、サイト サーバーと、SQL Server を実行するコンピューター間の通信がセキュリティで保護されますが、Configuration Manager でサイト システムの役割と SQL Server 間の通信はセキュリティで保護されません。 サイト内の通信用に構成できるのは、HTTPS を使用する一部のサイト システムのみです。  

追加の制御を使って、これらのサーバー間チャネルをセキュリティで保護しないと、攻撃者はサイト システムに対してさまざまなスプーフィング攻撃や中間者攻撃を使用することができます。 IPsec を使用できない場合は、SMB 署名を使用します。  

> [!Important]  
> サイト サーバーとパッケージ ソース サーバー間の通信チャネルをセキュリティで保護します。 この通信には SMB が使用されます。 この通信をセキュリティで保護するために IPsec を使用できない場合は、SMB 署名を使い、ファイルがクライアントでダウンロードされ、実行される前に改ざんされないようにしてください。  

### <a name="dont-change-the-default-security-groups"></a>既定のセキュリティ グループを変更しない

Configuration Manager によってサイト システムの通信用に作成および管理されている、次のセキュリティ グループを変更しないでください。

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager は、これらのセキュリティ グループを自動的に作成して管理します。 この動作には、サイト システムの役割が削除された場合の、コンピューター アカウントの削除も含まれます。  

サービスの継続性と最小限の特権を確保するため、これらのグループを手動で編集しないでください。  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>信頼されたルート キーのプロビジョニング プロセスを管理する

クライアントでは、グローバル カタログで Configuration Manager の情報を照会できない場合、信頼されたルート キーに依存して有効な管理ポイントを認証する必要があります。 信頼されたルート キーは、クライアント レジストリに格納されます。 グループ ポリシーまたは手動の構成を使用して設定できます。  

クライアントでは、初めて管理ポイントに接続する前に信頼されたルート キーのコピーがない場合、最初に通信した管理ポイントを信頼します。 攻撃者がクライアントを承認されていない管理ポイントに誘導するリスクを軽減するため、信頼されたルート キーをクライアントに事前に準備することができます。 詳細については、「[信頼されたルート キーの計画](../security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。  

### <a name="use-non-default-port-numbers"></a>既定以外のポート番号を使用する

既定以外のポート番号を使用することで、セキュリティを強化できます。 これにより、攻撃者が攻撃準備として環境を探索することが難しくなります。 既定以外のポートを使用することにした場合は、Configuration Manager をインストールする前に、これらのポートについて計画します。 階層内のすべてのサイトで一貫して使用します。 クライアント要求ポートと Wake On LAN は、既定以外のポート番号を使用できる場合の例です。  

### <a name="use-role-separation-on-site-systems"></a>サイト システムで役割の分離を使用する

サイト システムの役割をすべて 1 台のコンピューターにインストールすることはできますが、この方法が実稼働ネットワークで使用されることはほとんどありません。 これにより、単一障害点が生じます。  

### <a name="reduce-the-attack-profile"></a>攻撃プロファイルを減らす

各サイト サーバーの役割を複数のサーバーに分離すると、あるサイト システムの脆弱性に対する攻撃が別のサイト システムで利用される可能性が少なくなります。 多くの役割で、サイト システムに Internet Information Services (IIS) をインストールする必要があり、これにより、攻撃面が増えることになります。 ハードウェア経費を削減するためにサイト システムの役割を結合する必要がある場合は、IIS の役割を、IIS を必要とする他の役割とのみ結合します。  

> [!IMPORTANT]  
> フォールバック ステータス ポイントの役割は例外です。 このサイト システムの役割では、クライアントから認証されていないデータを受け入れるため、フォールバック ステータス ポイントの役割を他の Configuration Manager サイト システムの役割に割り当てないでください。  

### <a name="configure-static-ip-addresses-for-site-systems"></a>サイト システムに静的 IP アドレスを構成する

静的 IP アドレスの方が、名前解決攻撃から保護するのが簡単です。  

静的 IP アドレスを使用すると、IPsec の構成も簡単になります。 Configuration Manager でのサイト システム間での通信のセキュリティのベスト プラクティスは IPsec を使用することです。  

### <a name="dont-install-other-applications-on-site-system-servers"></a>サイト システム サーバーに他のアプリケーションをインストールしない

サイト システム サーバーに他のアプリケーションをインストールすると、Configuration Manager の攻撃面を増やすことになります。 非互換性の問題のリスクもあります。  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>サイト オプションとして署名を要求して暗号化を有効にする

サイトで署名オプションと暗号化オプションを有効にします。 すべてのクライアントで SHA-256 ハッシュ アルゴリズムが確実にサポートされているようにして、 **[SHA-256 を必要とする]** オプションを有効にします。  

### <a name="restrict-and-monitor-administrative-users"></a>管理ユーザーを制限して監視する

信頼できるユーザーにのみ、Configuration Manager への管理アクセス権を付与します。 その後、組み込みのセキュリティ ロールを使用するか、セキュリティ ロールをカスタマイズして、これらのユーザーに最小限のアクセス許可を付与します。 ソフトウェアと構成を作成、変更、および展開できる管理ユーザーは、Configuration Manager 階層内のデバイスを制御する可能性があります。  

管理ユーザーの割り当てと承認レベルを定期的に監査して、必要な変更を確認します。  

詳細については、「[役割に基づいた管理の構成](../../servers/deploy/configure/configure-role-based-administration.md)」を参照してください。  

### <a name="secure-configuration-manager-backups"></a>Configuration Manager バックアップをセキュリティで保護する

Configuration Manager のバックアップ時に、この情報には、攻撃者がなりすましに使用する可能性がある証明書や他の機密データが含まれています。  

このデータをネットワーク経由で転送するときに SMB 署名または IPsec を使用し、バックアップの場所をセキュリティで保護します。  

### <a name="secure-locations-for-exported-objects"></a>エクスポートされたオブジェクトの場所をセキュリティで保護する

Configuration Manager コンソールからネットワークの場所にオブジェクトをエクスポートまたはインポートする場合は常に、その場所とネットワーク チャネルをセキュリティで保護します。

ネットワーク フォルダーにアクセスできるユーザーを制限します。  

エクスポートされたデータが攻撃者によって改ざんされるのを防ぐには、ネットワークの場所とサイト サーバー間で SMB 署名または IPsec を使用します。 また、Configuration Manager コンソールを実行するコンピューターとサイト サーバー間の通信もセキュリティで保護します。 情報開示を防ぐため、IPsec を使用してネットワーク上のデータを暗号化します。  

### <a name="manually-remove-certificates-from-failed-servers"></a>障害が発生したサーバーから証明書を手動で削除する

サイト システムが適切にアンインストールされていない場合、または機能が停止され、復元できない場合は、このサーバーの Configuration Manager 証明書を他の Configuration Manager サーバーから手動で削除します。

最初にサイト システムとサイト システムの役割で確立されたピア信頼を削除するには、他のサイト システム サーバーの**信頼されたユーザー**証明書ストアで、障害が発生したサーバーの Configuration Manager 証明書を手動で削除します。 サーバーを再フォーマットせずに再利用する場合、この操作は重要です。  

詳細については、[サーバー通信の暗号化制御](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication)に関するページを参照してください。  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>境界ネットワークをブリッジするようにインターネットベースのサイト システムを構成しない

境界ネットワークとイントラネットに接続するように、サイト システム サーバーをマルチホームに構成しないでください。 この構成では、インターネットベースのサイト システムでインターネットとイントラネットからのクライアント接続を受け入れることができますが、境界ネットワークとイントラネットの間のセキュリティ境界が排除されます。  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>境界ネットワークへの接続を開始するようにサイト サーバーを構成する

境界ネットワークなどの信頼されていないネットワーク上にサイト システムがある場合は、サイト システムへの接続を開始するようにサイト サーバーを構成します。

既定では、サイト システムで、データを転送するためにサイト サーバーへの接続が開始されます。 この構成は、信頼されていないネットワークから信頼されたネットワークへの接続の開始時に、セキュリティ上のリスクになる可能性があります。 サイト システムでインターネットからの接続が受け入れられた場合、またはサイト システムが信頼されていないフォレストに存在する場合は、 **[サイト サーバーがこのサイト システムへの接続を開始する必要がある]** サイト システム オプションを構成します。 サイト システムと役割のインストール後、すべての接続は信頼されたネットワークからサイト サーバーによって開始されます。  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>SSL ブリッジングと認証による終了を使用する

インターネットベースのクライアント管理に Web プロキシ サーバーを利用する場合は、認証による終了を使い、SSL への SSL ブリッジングを使用します。

プロキシ Web サーバーで SSL ターミネーションを構成すると、インターネットからのパケットが内部ネットワークに転送される前に検査されます。 プロキシ Web サーバーはクライアントからの接続を認証してから終了します。次に、インターネット ベースのサイト システムに認証済みの新しい接続を開きます。  

Configuration Manager クライアント コンピューターでプロキシ Web サーバーを使用してインターネットベースのサイト システムに接続する場合、クライアント ID (GUID) はパケット ペイロード内に安全に格納されます。 その後、管理ポイントでは、プロキシ Web サーバーはクライアントと見なされません。

プロキシ Web サーバーで SSL ブリッジングの要件をサポートできない場合は、SSL トンネリングもサポートされます。 このオプションでは安全性が低くなります。 インターネットからの SSL パケットは、終了せずにサイト システムに転送されます。 その後、悪意のあるコンテンツを検査することはできません。  

> [!WARNING]  
> Configuration Manager によって登録されるモバイル デバイスでは、SSL ブリッジングを使用できません。 SSL トンネリングのみを使用する必要があります。  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>コンピューターをウェイク アップしてソフトウェアをインストールするようにサイトを構成する場合に使用する構成

- 従来のウェイク アップ パケットを使用する場合、サブネット向けブロードキャストではなくユニキャストを使用する  

- サブネット向けのブロードキャストを使用する必要がある場合は、サイト サーバーのみから、既定以外のポート番号のみで IP 向けのブロードキャストを許可するルートを構成する  

さまざまな Wake On LAN テクノロジの詳細については、[クライアントをウェイクアップする方法の計画](../../clients/deploy/plan/plan-wake-up-clients.md)に関するページを参照してください。

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>電子メール通知を使用する場合は、SMTP メール サーバーへの認証済みアクセスを構成します

可能な限り、認証済みアクセスをサポートするメール サーバーを使用してください。 認証でサイト サーバーのコンピューター アカウントを使用します。 認証でユーザー アカウントを指定する必要がある場合は、少なくとも特権のあるアカウントを使用します。 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>LDAP チャネル バインディングと LDAP 署名を適用する

Active Directory ドメイン コントローラーのセキュリティは、署名を要求しない簡易認証およびセキュリティ層 (SASL) の LDAP バインドを拒否するように、またはクリア テキスト接続で実行された LDAP 単純バインドを拒否するように、サーバーを構成することにより、強化することができます。 バージョン 1910 以降の Configuration Manager では、LDAP チャネル バインディングと LDAP 署名の適用がサポートされています。 詳しくは、「[Windows の 2020 年 LDAP 署名と LDAP チャネル バインディングの要件](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows)」をご覧ください。 <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> サイト サーバーのセキュリティ ガイダンス

Configuration Manager サイト サーバーをセキュリティで保護するのに役立つ、次のガイダンスを使用します。  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>ドメイン コントローラーの代わりにメンバー サーバーに Configuration Manager をインストールする

Configuration Manager のサイト サーバーとサイト システムは、ドメイン コントローラーにインストールする必要はありません。 ドメイン コントローラーには、ドメイン データベース以外のローカルのセキュリティ アカウント マネージメント (SAM) データベースはありません。 Configuration Manager をメンバー サーバーにインストールすると、ドメイン データベース内ではなくローカルの SAM データベース内で Configuration Manager アカウントを保持できます。  

これにより、ドメイン コントローラーの攻撃対象も減らすことができます。  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>ネットワーク経由でファイルをコピーせずにセカンダリ サイトをインストールする

セットアップを実行してセカンダリ サイトを作成する場合は、親サイトからセカンダリ サイトにファイルをコピーするオプションを選択しないでください。 また、ネットワーク ソースの場所を使用しないでください。 ネットワーク経由でファイルをコピーすると、高い技術を持つ攻撃者がセカンダリ サイトのインストール パッケージを乗っ取り、インストール前にファイルを改ざんする可能性があります。 この攻撃のタイミングは難しくなります。 ファイルの転送時に IPsec または SMB を使用すると、この攻撃を軽減できます。  

ネットワーク経由でファイルをコピーする代わりに、セカンダリ サイト サーバーで、メディア フォルダーからローカル フォルダーにソース ファイルをコピーします。 次に、セカンダリ サイトを作成するセットアップの実行中に、 **[インストール ソース ファイル]** ページで、 **[セカンダリ サイト コンピューターで、次の場所にあるソース ファイルを使用する (最もセキュリティが高い)]** を選択し、このフォルダーを指定します。  

詳細については、「[セカンダリ サイトをインストールする](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary)」を参照してください。

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>サイトの役割のインストールでドライブ ルートからアクセス許可が継承される

<!-- SCCMDocs#1380 -->
最初のサイト システムの役割を任意のサーバーにインストールする前に、必ず、システム ドライブのアクセス許可を適切に構成してください。 たとえば、`C:\SMS_CCM` では `C:\` からアクセス許可が継承されます。 ドライブのルートが適切にセキュリティで保護されていないと、権限の低いユーザーによる Configuration Manager フォルダー内のコンテンツに対するアクセスや変更が可能になる場合があります。


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> SQL Server のセキュリティ ガイダンス

Configuration Manager では、SQL Server がバックエンド データベースとして使用されます。 データベースが侵害された場合、攻撃者は Configuration Manager をバイパスする可能性があります。 直接 SQL Server にアクセスする場合、Configuration Manager を通じて攻撃を仕掛けることができます。 SQL Server に対する攻撃を高いリスクと見なし、適切に減らしてください。  

Configuration Manager の SQL Server をセキュリティで保護するのに役立つ、次のセキュリティ ガイダンスを使用します。  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>Configuration Manager サイト データベース サーバーを使用して、他の SQL Server アプリケーションを実行しない

Configuration Manager サイト データベース サーバーへのアクセスを増やすと、Configuration Manager データに対するリスクが増えます。 Configuration Manager サイト データベースが侵害された場合、同じ SQL Server コンピューター上の他のアプリケーションも危険にさらされます。  

### <a name="configure-sql-server-to-use-windows-authentication"></a>Windows 認証を使用するように SQL Server を構成する

Configuration Manager では Windows アカウントと Windows 認証を使用してサイト データベースにアクセスしますが、SQL Server 混在モードを使用するように SQL Server を構成することもできます。 SQL Server 混在モードでは、追加の SQL サインインでデータベースにアクセスできます。 この構成は必須ではなく、攻撃面が増えます。  

### <a name="update-sql-server-express-at-secondary-sites"></a>セカンダリ サイトの SQL Server Express を更新する

プライマリ サイトをインストールするときに、Configuration Manager では、Microsoft ダウンロード センターから SQL Server Express がダウンロードされます。 その後、ファイルがプライマリ サイト サーバーにコピーされます。 セカンダリ サイトをインストールし、SQL Server Express をインストールするオプションを選択した場合、Configuration Manager では以前にダウンロードされたバージョンがインストールされます。 新しいバージョンが使用可能かどうかは確認されません。 セカンダリ サイトに最新バージョンが適用されていることを確認するには、次のいずれかのタスクを実行します。  

- セカンダリ サイトをインストールした後、セカンダリ サイト サーバーで Windows Update を実行します。  

- セカンダリ サイトをインストールする前に、SQL Server Express をセカンダリ サイト サーバーに手動でインストールします。 必ず、最新バージョンとすべてのソフトウェア更新プログラムをインストールするようにしてください。 次に、セカンダリ サイトをインストールし、既存の SQL Server インスタンスを使用するオプションを選択します。  

インストールされているすべてのバージョンの SQL Server に対して、Windows Update を定期的に実行します。 これにより、最新のソフトウェア更新プログラムが確実に適用されます。  

### <a name="follow-general-guidance-for-sql-server"></a>SQL Server の一般的なガイダンスに従う

使用する SQL Server のバージョンに関する一般的なガイダンスを特定し、それに従います。 ただし、Configuration Manager に関する次の要件を考慮します。  

- サイト サーバーのコンピューター アカウントが、SQL Server を実行しているコンピューターの管理者グループのメンバーである必要があります。 "管理者プリンシパルを明示的にプロビジョニングする" という SQL Server の推奨事項に従う場合、サイト サーバーでセットアップを実行する際に使用するアカウントが SQL ユーザー グループのメンバーである必要があります。  

- ドメイン ユーザー アカウントを使用して SQL Server をインストールする場合は、Active Directory Domain Services に発行されるサービス プリンシパル名 (SPN) にサイト サーバーのコンピューター アカウントが構成されていることを確認します。 SPN がない場合、Kerberos 認証が失敗して Configuration Manager のセットアップが失敗します。  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> IIS を実行するサイト システムのセキュリティ ガイダンス

Configuration Manager の複数のサイト システムの役割に IIS が必要です。 IIS をセキュリティで保護するプロセスにより、Configuration Manager が正しく動作するようになるため、セキュリティ攻撃のリスクが軽減されます。 これを実際に行うと、IIS が必要なサーバーの数が最小限に抑えられます。 たとえば、インターネットベースのクライアント管理のための高可用性とネットワーク分離を考慮し、クライアント ベースをサポートするために必要な数の管理ポイントのみを実行します。  

IIS を実行するサイト システムをセキュリティで保護するのに役立つ、次のガイダンスを使用します。  

### <a name="disable-iis-functions-that-you-dont-require"></a>不要な IIS 機能を無効にする

インストールするサイト システムの役割に最小限の IIS 機能をインストールします。 詳細については、「[サイトとサイト システムの前提条件](../configs/site-and-site-system-prerequisites.md)」をご覧ください。  

### <a name="configure-the-site-system-roles-to-require-https"></a>HTTPS を要求するようにサイト システムの役割を構成する

クライアントでは、HTTPS を使用するのではなく、HTTP を使用してサイト システムに接続する場合、Windows 認証を使用します。 この動作では、Kerberos 認証ではなく、NTLM 認証を使用するように切り替えられる可能性があります。 NTLM 認証を使用すると、クライアントが偽のサーバーに接続する可能性があります。  

このガイダンスの例外として、配布ポイントが考えられます。 配布ポイントが HTTPS 用に構成されている場合、パッケージ アクセス アカウントは機能しません。 パッケージ アクセス アカウントはコンテンツに対する承認を提供します。これにより、コンテンツにアクセスできるユーザーを制限することができます。 詳細については、「[コンテンツ管理について推奨する運用方法](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)」を参照してください。  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>サイト システムの役割用に IIS で証明書信頼リスト (CTL) を構成する

サイト システムの役割 :  

- HTTPS 用に構成する配布ポイント  

- HTTPS 用に構成し、モバイル デバイスをサポートするために有効にする管理ポイント

CTL は、信頼されたルート証明機関 (CA) の定義済みリストです。 CTL をグループ ポリシーおよび公開キー基盤 (PKI) の展開と共に使用すると、CTL で、ネットワーク上に構成されている既存の信頼されたルート CA を補うことができます。 たとえば、Microsoft Windows と共に自動的にインストールされるか、Windows エンタープライズ ルート CA を通じて追加される CA です。 CTL が IIS で構成されている場合、その CTL でこれらの信頼されたルート CA のサブセットが定義されます。  

このサブセットでは、セキュリティをより詳細に制御できます。 CTL によって、受け入れられるクライアント証明書が、CTL にリストされている CA から発行された証明書のみに制限されます。 たとえば、Windows には、VeriSign や Thawte など、よく知られている多くのサードパーティ CA 証明書が付属しています。

既定では、IIS を実行するコンピューターで、これらのよく知られている CA にチェーンされている証明書が信頼されます。 リストされているサイト システムの役割に対して CTL を使用して IIS を構成しない場合、サイトでは、これらの CA から発行された証明書を持つどのデバイスも有効なクライアントとして受け入れられます。 これらの CA が含まれていない CTL を使用して IIS を構成すると、証明書がこれらの CA にチェーンされている場合、サイトではクライアント接続が拒否されます。 リストされているサイト システムの役割で Configuration Manager クライアントが受け入れられるようにするには、Configuration Manager クライアントで使用される CA を指定する CTL を使用して IIS を構成する必要があります。  

> [!NOTE]  
> IIS で CTL を構成することが必要になるのは、リストされているサイト システムの役割のみです。 Configuration Manager が管理ポイントに使用する証明書発行者リストは、クライアント コンピューターが HTTPS 管理ポイントに接続するときに同じ機能を提供します。  

IIS で信頼された CA のリストを構成する方法の詳細については、IIS のドキュメントを参照してください。  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>IIS と共にサイト サーバーをコンピューター上に配置しない

役割を分離すると、攻撃プロファイルを減らし、回復性を向上できます。 サイト サーバーのコンピューター アカウントには、通常、すべてのサイト システムの役割に対する管理特権があります。 クライアント プッシュ インストールを使用する場合は、Configuration Manager クライアントに対するこれらの特権がある場合もあります。  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Configuration Manager に専用の IIS サーバーを使用する

Configuration Manager でも使用される IIS サーバーに複数の Web ベース アプリケーションをホストできますが、これにより、攻撃対象が大幅に増える可能性があります。 アプリケーションが正しく構成されていないと、攻撃者によって Configuration Manager サイト システムの制御が奪われる可能性があります。 この侵害で、攻撃者によって階層の制御が奪われる可能性があります。  

他の Web ベース アプリケーションを Configuration Manager サイト システムで実行する必要がある場合、Configuration Manager サイト システムにカスタム Web サイトを作成します。  

### <a name="use-a-custom-website"></a>カスタム Web サイトを使用する

IIS を実行するサイト システムでは、既定の Web サイトではなく、カスタム Web サイトを使用するように Configuration Manager を構成します。 サイト システムで他の Web アプリケーションを実行する場合は、カスタム Web サイトを使用する必要があります。 この設定は、特定のサイト システムの設定ではなく、サイト全体の設定です。  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>カスタム Web サイトを使用する場合は、既定の仮想ディレクトリを削除する

既定の Web サイトの使用からカスタム Web サイトの使用に変更した場合、Configuration Manager により、以前の仮想ディレクトリが削除されることはありません。 既定の Web サイトの下に Configuration Manager によって作成された、仮想ディレクトリを削除します。  

たとえば、配布ポイントの次の仮想ディレクトリを削除します。  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>IIS サーバーのセキュリティ ガイダンスに従う

使用する IIS サーバーのバージョンに関する一般的なガイダンスを特定し、それに従います。 特定のサイト システムの役割について、Configuration Manager で適用される要件を考慮してください。 詳細については、「[サイトとサイト システムの前提条件](../configs/site-and-site-system-prerequisites.md)」をご覧ください。  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> 管理ポイントのセキュリティ ガイダンス

管理ポイントは、デバイスと Configuration Manager の間の基本インターフェイスです。 管理ポイントおよび管理ポイントが実行されているサーバーに対する攻撃を高いリスクと見なし、適切に減らしてください。 適切なセキュリティ ガイダンスをすべて適用し、異常なアクティビティを監視します。  

Configuration Manager の管理ポイントをセキュリティで保護するのに役立つ、次のガイダンスを使用します。  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>管理ポイントのクライアントを同じサイトに割り当てる

管理ポイントにある Configuration Manager クライアントを、管理ポイントのサイト以外のサイトに割り当てるシナリオは避けてください。  

以前のバージョンから Configuration Manager Current Branch に移行する場合は、管理ポイントのクライアントをできるだけ早く新しいサイトに移行します。  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> フォールバック ステータス ポイントのセキュリティ ガイダンス

Configuration Manager にフォールバック ステータス ポイントをインストールする場合は、次のセキュリティ ガイダンスを使用します。

フォールバック ステータス ポイントをインストールするときのセキュリティの注意事項については、「[フォールバック ステータス ポイントが必要かどうかを判断する](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)」を参照してください。  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>同じサイト システムで他の役割を実行しない

フォールバック ステータス ポイントは、どのコンピューターからでも認証されていない通信を受け入れるように設計されています。 このサイト システムの役割を他の役割またはドメイン コントローラーと共に実行すると、そのサーバーのリスクが大幅に増加します。  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>PKI 証明書を使用してクライアントをインストールする前に、フォールバック ステータス ポイントをインストールする

Configuration Manager サイト システムで HTTP クライアント通信が受け入れられない場合、PKI 関連の証明書の問題により、クライアントが管理されていないことがわからない可能性があります。 クライアントをフォールバック ステータス ポイントに割り当てると、これらの証明書の問題はフォールバック ステータス ポイントを通じて報告されます。  

セキュリティ上の理由から、クライアントのインストール後に、フォールバック ステータス ポイントをクライアントに割り当てることはできません。 この役割は、クライアントのインストール時にのみ割り当てることができます。  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>境界ネットワークでのフォールバック ステータス ポイントの使用を避ける

仕様により、フォールバック ステータス ポイントは任意のクライアントからデータを受け入れます。 境界ネットワークのフォールバック ステータス ポイントはインターネットベース クライアントのトラブルシューティングに役立つ場合がありますが、トラブルシューティングの利点と、パブリックにアクセス可能なネットワークで認証されていないデータがサイト システムによって受け入れられるというリスクとのバランスを取ってください。  

境界ネットワークまたは信頼されていないネットワークにフォールバック ステータス ポイントをインストールする場合は、データ転送を開始するようにサイト サーバーを構成します。 フォールバック ステータス ポイントでサイト サーバーへの接続を開始できるようにする既定の設定は使用しないでください。  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a> サイト管理に関するセキュリティの問題

Configuration Manager に関する次のセキュリティの問題を確認します。  

- Configuration Manager には、ネットワークの攻撃に Configuration Manager を使用する承認された管理ユーザーに対する防御がありません。 承認されていない管理ユーザーは、セキュリティ上の高いリスクになります。 次のような戦略を含む、多くの攻撃を仕掛ける可能性があります。  

    - ソフトウェアの展開を使用して、組織内のすべての Configuration Manager クライアント コンピューターに悪意のあるソフトウェアを自動的にインストールして実行する。  

    - クライアントのアクセス許可なしで Configuration Manager クライアントをリモートで制御する。  

    - ポーリング間隔を短縮し、インベントリの量が膨大になるように構成する。 この操作によって、クライアントとサーバーに対するサービス拒否攻撃が行われます。  

    - 階層内のいずれかのサイトを使用して、別のサイトの Active Directory データにデータを書き込む。  

    サイト階層はセキュリティの境界です。 サイトが管理境界のみになるように考えてください。  

    管理ユーザーのすべてのアクティビティを監査し、定期的に監査ログを調べます。 すべての Configuration Manager 管理ユーザーが、採用前に身元調査を受ける必要があります。 雇用の条件として、定期的な再調査が必要です。  

- 登録ポイントが侵害された場合、攻撃者は認証用の証明書を取得する可能性があります。 モバイル デバイスを登録するユーザーの資格情報を盗み出す可能性があります。  

    登録ポイントでは CA と通信を行います。 Active Directory オブジェクトの作成、変更、および削除を行うことができます。 境界ネットワークに登録ポイントをインストールしないでください。 異常なアクティビティを常に監視してください。  

- インターネットベースのクライアント管理に対してユーザー ポリシーを許可すると、攻撃プロファイルを増やすことになります。  

    クライアントとサーバー間の接続に PKI 証明書を使用するだけでなく、これらの構成には Windows 認証が必要です。 Kerberos ではなく、NTLM 認証を使用するように切り替えられる場合があります。 NTLM 認証は、なりすましや再生攻撃に対して脆弱です。 インターネット上のユーザーを正しく認証するには、インターネットベースのサイト システムからドメイン コントローラーへの接続を許可する必要があります。  

- サイト システム サーバーでは **Admin$** 共有が必要です。  

    Configuration Manager サイト サーバーでは Admin$ 共有を使用して、サイト システムに対する接続とサービス操作を行います。 この共有を無効にしたり、削除したりしないでください。  

- Configuration Manager では名前解決サービスを使用して、他のコンピューターに接続します。 これらのサービスを、次のセキュリティ攻撃から保護することは困難です。
    - スプーフィング
    - 改ざん
    - 否認
    - 情報漏えい
    - サービス拒否
    - 特権の昇格

    名前解決に使用する DNS のバージョンに関するセキュリティ ガイダンスを特定し、それに従ってください。  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> 探索のプライバシー情報

探索では、ネットワーク リソースのレコードが作成され、それらが Configuration Manager データベースに格納されます。 探索データ レコードには、IP アドレス、OS、コンピューター名などのコンピューター情報が含まれます。 組織によって Active Directory Domain Services に格納されている情報を返すように、Active Directory 探索方法を構成することもできます。  

既定で Configuration Manager で有効になる探索方法は、定期探索のみです。 この方法で探索されるのは、Configuration Manager クライアント ソフトウェアが既にインストールされているコンピューターのみです。  

探索情報が Microsoft に直接送信されることはありません。 これは、Configuration Manager データベースに格納されます。 Configuration Manager では、データが削除されるまでデータベース内の情報が保持されます。 このプロセスは、**期限切れの探索データの削除**というサイトのメンテナンス タスクにより、90 日おきに行われます。  
