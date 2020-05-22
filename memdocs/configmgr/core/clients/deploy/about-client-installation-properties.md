---
title: クライアント インストール パラメーターとプロパティ
titleSuffix: Configuration Manager
description: Configuration Manager クライアントをインストールするための ccmsetup コマンド ライン パラメーターとプロパティについて説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ccfb523cc1abc3a64d396f32d55a4dc4551987c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428607"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Configuration Manager のクライアント インストールのパラメーターとプロパティについて

*適用対象:Configuration Manager (Current Branch)*

CCMSetup.exe コマンドを使用して、Configuration Manager クライアントをインストールします。 コマンド ラインでクライアント インストール "*パラメーター*" を指定すると、インストール動作が変更されます。 コマンド ラインでクライアント インストール "*プロパティ*" を指定すると、インストールされたクライアント エージェントの初期構成が変更されます。

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> CCMSetup.exe について

CCMSetup.exe コマンドは、クライアントのインストールに必要なファイルを管理ポイントまたはソースの場所からダウンロードします。 次のようなファイルが含まれます。  

- クライアント ソフトウェアをインストールする Windows インストーラー パッケージ client.msi

- クライアントに関する前提条件

- Configuration Manager クライアントの更新プログラムと修正プログラム

> [!NOTE]
> client.msi を直接インストールすることはできません。  

CCMSetup.exe には、インストールをカスタマイズするためのコマンド ライン "*パラメーター*" が用意されています。 パラメーターは、先頭にスラッシュ (`/`) が付いていて、慣例により小文字で表されます。 コロン (`:`) の直後に値を置くことで、必要に応じてパラメーターの値を指定できます。 詳細については、「[CCMSetup.exe のコマンドライン パラメーター](#ccmsetupexe-command-line-parameters)」をご覧ください。

CCMSetup.exe コマンド ラインに "*プロパティ*" を指定して、client.msi の動作を変更することもできます。慣例により、プロパティは大文字で表されます。 プロパティの値を指定するには、等号 (`=`) の直後にその値を置きます。 詳細については、「[Client.msi のプロパティ](#clientMsiProps)」をご覧ください。

> [!IMPORTANT]  
> client.msi のプロパティを指定する前に、CCMSetup のパラメーターを指定します。  

CCMSetup.exe およびサポート ファイルは、サイト サーバー上の、Configuration Manager インストール フォルダーの **Client** フォルダーにあります。 Configuration Manager では、サイト共有の下で、このフォルダーがネットワークに共有されます。 たとえば、`\\SiteServer\SMS_ABC\Client` となります。

コマンド プロンプトで、CCMSetup.exe コマンドは次の形式を使用します。  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

次に例を示します。  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

この例では次のことが行われます。  

- 配布ポイントの一覧を要求し、クライアント インストール ファイルをダウンロードするために SMSMP01 という名前の管理ポイントを指定します。  

- クライアントのバージョンが既にコンピューターに存在している場合にインストールを停止するように指定します。  

- クライアントをサイト コード S01 に割り当てるように client.msi で指定します。  

- SMSFP01 というフォールバック ステータス ポイントを使用するように client.msi で指定します。  

> [!TIP]  
> パラメーターの値がスペースを含む場合は、引用符で囲みます。  

Configuration Manager 用に Active Directory スキーマを拡張した場合、サイトでは多くのクライアント インストール プロパティが Active Directory Domain Services に発行されます。 Configuration Manager クライアントはこれらのプロパティを自動的に読み取ります。 詳細については、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](about-client-installation-properties-published-to-active-directory-domain-services.md)」を参照してください。  

## <a name="ccmsetupexe-command-line-parameters"></a>CCMSetup.exe のコマンドライン パラメーター

### <a name=""></a><a name="bkmk_help"></a> /?

ccmsetup.exe の使用可能なコマンド ライン パラメーターを表示します。  

例: `ccmsetup.exe /?`

### <a name="source"></a>/source

ファイルのダウンロード場所を指定します。 ローカルまたは UNC パスを使用します。 デバイスにより、サーバー メッセージ ブロック (SMB) プロトコルを使用してファイルがダウンロードされます。 **/source** を使用するには、クライアント インストール用の Windows ユーザー アカウントに、その場所に対する**読み取り**アクセス許可が必要です。

> [!TIP]  
> コマンド ラインで **/source** パラメーターを複数回使用して、ダウンロードの代替場所を指定することができます。  

例: `ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/mp

コンピューターの接続先のソース管理ポイントを指定します。 コンピューターではこの管理ポイントを使用して、インストール ファイルの最も近い配布ポイントを見つけます。 配布ポイントがない、またはコンピューターで 4 時間経っても配布ポイントからファイルをダウンロードできない場合、指定された管理ポイントからファイルがダウンロードされます。  

> [!IMPORTANT]  
> このパラメーターを使用すると、コンピューターでダウンロード ソースを見つけるための最初の管理ポイントを指定できます。これには、任意のサイト内の任意の管理ポイントを指定できます。 指定した管理ポイントにクライアントを "*割り当てる*" わけではありません。

クライアント接続におけるサイト システムの役割の構成によって、コンピューターは HTTP または HTTPS 接続でファイルをダウンロードします。 構成すれば、このダウンロードで BITS 調整を使用することもできます。 すべての配布ポイントおよび管理ポイントを、HTTPS クライアント接続用にのみ構成した場合は、クライアント コンピューターに有効なクライアント証明書があることを確認してください。  

**/mp** コマンド ライン パラメーターを使用して、複数の管理ポイントを指定できます。 コンピューターで最初の管理ポイントへの接続に失敗した場合は、指定されたリスト内の次の管理ポイントが試行されます。 複数の管理ポイントは、値をセミコロンで区切って指定します。

クライアントが HTTPS を使用して管理ポイントに接続する場合は、コンピューター名ではなく FQDN を指定します。 その値は、管理ポイントの PKI 証明書の **[サブジェクト]** または **[サブジェクトの別名]** と一致している必要があります。 Configuration Manager では、イントラネットの接続のために証明書のコンピューター名を使用することがサポートされますが、FQDN を使用することが推奨されます。

コンピューター名を使用した例: `ccmsetup.exe /mp:SMSMP01`  

FQDN を使用した例: `ccmsetup.exe /mp:smsmp01.contoso.com`  

このパラメーターでは、クラウド管理ゲートウェイ (CMG) の URL を指定することもできます。 この URL を使用して、インターネット ベースのデバイスにクライアントをインストールします。 このパラメーターの値を取得するには、次の手順を使用します。

- CMG を作成します。 詳細については、[CMG の設定](../manage/cmg/setup-cloud-management-gateway.md)に関する記事をご覧ください。
- アクティブなクライアントで、管理者として Windows PowerShell コマンド プロンプトを開きます。
- 次のコマンドを実行します。

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- **/mp** パラメーターで使用する `https://` プレフィックスを追加します。

クラウド管理ゲートウェイの URL を使用する場合の例: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> **/mp** パラメーターにクラウド管理ゲートウェイの URL を指定する場合は、先頭が `https://` である必要があります。

### <a name="regtoken"></a>/regtoken

<!--5686290-->

バージョン 2002 以降では、このパラメーターを使用して一括登録トークンを指定します。 インターネットベースのデバイスでは、クラウド管理ゲートウェイ (CMG) を介して、登録プロセスでこのトークンが使用されます。 詳細については、[CMG のトークンベースの認証](deploy-clients-cmg-token.md)に関する記事をご覧ください。

このパラメーターを使用する場合は、次のパラメーターとプロパティも指定してください。

- [ **/mp**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

次のコマンド ラインの例には、他の必要なセットアップ パラメーターとプロパティが含まれています。

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

CCMSetup.exe によるインストール ファイルのダウンロードが失敗する場合、このパラメーターを使用して分単位で再試行間隔を指定します。 CCMSetup は、[ **/downloadtimeout**](#downloadtimeout) パラメーターで指定した制限に達するまで再試行を続けます。

例: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

このパラメーターを指定すると、CCMSetup がサービスとして実行 (既定の動作) されなくなります。 CCMSetup がサービスとして実行される場合、コンピューターのローカル システム アカウントのコンテキストで実行されます。 このアカウントには、インストールに必要なネットワーク リソースにアクセスするための十分な権限がない可能性があります。 **/noservice** を使用すると、CCMSetup.exe は、インストールを開始するために使用するユーザー アカウントの関連で実行されます。

例: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

ローカル システム アカウントを使用するサービスとして CCMSetup を実行することを指定します。  

> [!TIP]
> スクリプトを使用して **/service** パラメーターと共に CCMSetup.exe を実行した場合は、サービスが開始した後に CCMSetup.exe は終了します。 この場合、スクリプトにインストールの詳細が正しく報告されない可能性があります。

例: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

構成マネージャー クライアントをアンインストールするには、このパラメーターを使用します。 詳細については、「[クライアントをアンインストールする](../manage/manage-clients.md#BKMK_UninstalClient)」をご覧ください。

例: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

任意のバージョンのクライアントが既にインストールされている場合は、このパラメーターでクライアント インストールを停止するように指定します。  

例: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

インストールの完了に必要であれば強制的にコンピューターを再起動させる場合は、このパラメーターを使用します。 このパラメーターを指定しない場合は、再起動が必要になると CCMSetup は終了します。 次回手動で再起動した後に続行します。

例: `CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

デバイスによって HTTP 接続経由でクライアント インストール ファイルがダウンロードされる場合、このパラメーターを使用してダウンロードの優先順位を指定します。 次のいずれかの値を指定します。

- `FOREGROUND`

- `HIGH`

- `NORMAL` (既定)

- `LOW`

例: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

CCMSetup によるクライアント インストール ファイルのダウンロードが失敗する場合、このパラメーターによってタイムアウトの最大値を分単位で指定します。 このタイムアウトの後、CCMSetup はインストール ファイルのダウンロードを試行しなくなります。 既定値は **1440** 分 (1 日) です。

再試行の間隔を指定するには、[ **/retry**](#retry) パラメーターを使用します。

例: `ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

クライアントが PKI クライアント認証証明書を使用するようにするには、このパラメーターを指定します。 このパラメーターを指定しない場合、またはクライアントで有効な証明書が見つからない場合は、自己署名証明書による HTTP 接続が使用されます。

例: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> 一部のシナリオでは、このパラメーターを指定する必要はなく、引き続きクライアント証明書を使用します。 たとえば、クライアント プッシュおよびソフトウェアの更新に基づいたクライアント インストールです。 クライアントを手動でインストールし、 **/mp** パラメーターを使用して HTTPS が有効な管理ポイントを指定する場合は、このパラメーターを使用します。
>
> また、インターネットのみの通信用にクライアントをインストールする場合も、このパラメーターを指定してください。 **CCMALWAYSINF=1** プロパティを、インターネット ベースの管理ポイント (**CCMHOSTNAME**) とサイト コード (**SMSSITECODE**) のプロパティと共に使用します。 インターネット ベースのクライアント管理の詳細については、「[インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)」を参照してください。  

### <a name="nocrlcheck"></a>/NoCRLCheck

PKI 証明書を使用して HTTPS で通信するときは、クライアントが証明書失効リスト (CRL) を確認しないように指定します。 このパラメーターを指定しない場合、クライアントでは、HTTPS 接続を確立する前に CRL が確認されます。 クライアントの CRL チェックの詳細については、「[PKI 証明書失効の計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)」を参照してください。

例: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

このパラメーターでは、クライアント インストールのプロパティの一覧が記載されたテキスト ファイルを指定します。

- CCMSetup がサービスとして実行されている場合は、このファイルを CCMSetup システム フォルダー `%Windir%\Ccmsetup` に配置します。

- [ **/noservice**](#noservice) パラメーターを指定する場合は、このファイルを CCMSetup.exe と同じフォルダーに配置します。

例: `CCMSetup.exe /config:"configuration file name.txt"`

正しいファイル形式を指定するには、サイト サーバー上の Configuration Manager インストール ディレクトリの `\bin\<platform>` フォルダーにある **mobileclienttemplate.tcf** ファイルを使用します。 このファイルには、セクションとその使用方法に関するコメントが含まれています。 `[Client Install]` セクションで、次のテキストの後にクライアント インストールのプロパティを指定します: `Install=INSTALL=ALL`。

`[Client Install]` セクションのエントリの例: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/skipprereq

このパラメーターでは、指定した前提条件を CCMSetup.exe でインストールしないように指定します。 複数の値を入力できます。 それぞれの値を区切るには、セミコロン文字 (`;`) を使用します。

例:

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

クライアントの前提条件の詳細については、[Windows クライアントの前提条件](prerequisites-for-deploying-clients-to-windows-computers.md)に関する記事をご覧ください。

### <a name="forceinstall"></a>/forceinstall

CCMSetup.exe で既存のクライアントをすべてアンインストールし、新しいクライアントをインストールするように指定します。  

### <a name="excludefeatures"></a>/ExcludeFeatures

このパラメーターでは、指定した機能を CCMSetup.exe でインストールしないように指定します。

例: `CCMSetup.exe /ExcludeFeatures:ClientUI` は、クライアントにソフトウェア センターをインストールしません。  

> [!NOTE]  
> `ClientUI` は、 **/ExcludeFeatures** パラメーターでサポートされる唯一の値です。

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> CCMSetup.exe のリターン コード

CCMSetup.exe コマンドを実行すると、次のリターン コードが提供されます。 トラブルシューティングを行うには、クライアントの `%WinDir%\ccmsetup\ccmsetup.log` を確認して、リターン コードに関するコンテキストと追加情報を確認します。

|リターン コード|意味|  
|-----------|-------|  
|0|成功|  
|6|エラー|  
|7|再起動が必要です|  
|8|セットアップは既に実行されています|  
|9|前提条件の評価エラー|  
|10|セットアップのマニフェスト ハッシュ検証エラー|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a> Ccmsetup.msi プロパティ

次のプロパティを使用し、ccmsetup.msi のインストールの動作を変更できます。

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

この ccmsetup.*msi* プロパティを使用すると、ccmsetup.*exe* に対して追加のコマンド ライン パラメーターおよびプロパティを渡すことができます。 他のパラメーターとプロパティは、引用符 (`"`) で囲みます。 [Intune MDM インストール方法](plan/client-installation-methods.md#microsoft-intune-mdm-installation)を使用して構成マネージャー クライアントをブートストラップするときに、このプロパティを使用します。

例: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune では、コマンド ラインが 1024 文字に制限されます。

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a> Client.msi のプロパティ

次のプロパティを使って、client.msi のインストールの動作を変更することができます。これは ccmsetup.exe によってインストールされます。 [クライアント プッシュ インストール方法](plan/client-installation-methods.md#client-push-installation)を使用する場合は、Configuration Manager コンソールの **[クライアント プッシュ インストールのプロパティ]** の **[クライアント]** タブでこれらのプロパティを指定します。

### <a name="aadclientappid"></a>AADCLIENTAPPID

Azure Active Directory (Azure AD) クライアント アプリの ID を指定します。 クラウド管理用に [Azure サービスを構成する](../../servers/deploy/configure/azure-services-wizard.md)ときに、クライアント アプリを作成またはインポートします。 Azure 管理者は、Azure Portal からこのプロパティの値を取得することができます。 詳細については、「[アプリケーション ID の取得](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)」を参照してください。 **AADCLIENTAPPID** プロパティの場合、このアプリケーション ID は、**ネイティブ** アプリケーションの種類用です。

例: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Azure AD サーバー アプリの ID を指定します。 クラウド管理用に [Azure サービスを構成する](../../servers/deploy/configure/azure-services-wizard.md)ときに、サーバー アプリを作成またはインポートします。 サーバー アプリを作成するとき、[サーバー アプリケーションの作成] ウィンドウでは、このプロパティは **[アプリケーション ID/URI]** になります。

Azure 管理者は、Azure Portal からこのプロパティの値を取得することができます。 **[Azure Active Directory]** で、 **[アプリの登録]** の下にあるサーバー アプリを見つけます。 アプリケーションの種類 **[Web アプリ/API]** を探します。 アプリを開き、 **[設定]** を選択して、 **[プロパティ]** を選択します。 この **AADRESOURCEURI** クライアント インストール プロパティに対して **[アプリケーション ID/URI]** の値を使用します。

例: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

Azure AD テナントの ID を指定します。 クラウド管理用に [Azure サービスを構成する](../../servers/deploy/configure/azure-services-wizard.md)ときに、Configuration Manager がこのテナントにリンクします。 このプロパティの値を取得するには、次の手順を使用します。

- 同じ Azure AD テナントに参加している Windows 10 デバイスで、コマンド プロンプトを開きます。
- 次のコマンドを実行します。`dsregcmd.exe /status`
- [デバイスの状態] セクションで、**TenantId** の値を見つけます。 たとえば、 `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a` と記述します。

  > [!Note]
  > Azure 管理者は、Azure Portal でこの値を取得することもできます。 詳細については、[テナント ID の取得](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)に関する記事をご覧ください。

例: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

クライアント設定およびポリシーへのアクセスを許可する 1 つまたは複数の Windows ユーザー アカウントまたはグループを指定します。 このプロパティは、クライアント コンピューターに対するローカル管理者資格情報がない場合に役立ちます。 セミコロン (`;`) で区切られたアカウントの一覧を指定します。

例: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

必要に応じて、クライアントのインストール後にコンピューターが自動的に再起動するようにします。

> [!IMPORTANT]  
> このプロパティを使用すると、コンピューターは警告なしで再起動します。 この動作は、ユーザーが Windows にサインインしていた場合でも発生します。

例: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

クライアントが常にインターネット ベースであり、イントラネットには接続しないことを指定するには、このプロパティの値を `1` に設定します。 クライアントの接続の種類に **[常にインターネット]** と表示されます。  

このプロパティを [**CCMHOSTNAME**](#ccmhostname) と共に使用して、インターネット ベースの管理ポイントの FQDN を指定します。 また、CCMSetup パラメーター [ **/UsePKICert**](#usepkicert)、およびサイト コード ([**SMSSITECODE**](#smssitecode)) と共に使用します。

インターネット ベースのクライアント管理の詳細については、「[インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)」を参照してください。

例: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

このプロパティを使用して、証明書の発行者リストを指定します。 このリストには、Configuration Manager サイトが信頼する、信頼されたルート証明機関 (CA) の証明書情報が含まれます。  

ルート CA 証明書のサブジェクト属性では、この値の大文字と小文字が区別されます。 属性はコンマ (`,`) またはセミコロン (`;`) で区切ります。 区切りバー (`|`) を使用して、複数のルート CA 証明書を指定します。

例: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> サイトの **mobileclient.tcf** ファイルに含まれる **CertificateIssuers** 属性の値を使用します。 このファイルは、サイト サーバー上の Configuration Manager インストール ディレクトリの `\bin\<platform>` サブフォルダーにあります。

証明書発行者リストと、これをクライアントが証明書選択プロセスで使用する方法の詳細については、「[PKI クライアント証明書の選択の計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection)」を参照してください。

### <a name="ccmcertsel"></a>CCMCERTSEL

クライアントに HTTPS 通信用の証明書が複数ある場合、このプロパティによって、有効なクライアント認証証明書を選択するための条件を指定します。

証明書の [サブジェクト名] または [サブジェクトの別名] を検索するには、次のキーワードを使用します。

- **[件名]** : 完全一致を検索します
- **SubjectStr**:部分一致を検索します

例:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: [サブジェクト名] または [サブジェクトの別名] でコンピューター名 `computer1.contoso.com` と完全一致する証明書を検索します。

- `CCMCERTSEL="SubjectStr:contoso.com"`: [サブジェクト名] または [サブジェクトの別名] に `contoso.com` が含まれる証明書を検索します。

**SubjectAttr** キーワードを使用して、[サブジェクト名] または [サブジェクトの別名] で、オブジェクト識別子 (OID) または識別名の属性を検索します。

例:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: オブジェクト識別子として表され、`Computers` という名前の、組織単位属性を検索します。

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: 識別名として表され、`Computers` という名前の、組織単位属性を検索します。

> [!IMPORTANT]
> [サブジェクト名] を使用する場合、**Subject** キーワードでは大文字と小文字が区別され、**SubjectStr** キーワードでは区別されません。
>
> [サブジェクトの別名] を使用する場合、**Subject** キーワードでも **SubjectStr** キーワードでも大文字と小文字は区別されません。

証明書の選択に使用できる属性の完全な一覧については、[PKI 証明書の選択条件としてサポートされている属性値](#BKMK_attributevalues)に関する記事をご覧ください。

複数の証明書が検索条件に一致し、[**CCMFIRSTCERT**](#ccmfirstcert) を `1` に設定している場合は、クライアント インストーラーによって有効期限が最も長い証明書が選択されます。

### <a name="ccmcertstore"></a>CCMCERTSTORE

クライアント インストーラーで、コンピューターの既定の**個人用**証明書ストアから有効な証明書を見つけられない場合は、このプロパティを使用して代替の証明書ストアの名前を指定します。

例: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

このプロパティを指定すると、クライアントのインストール時にデバッグ ログが有効になります。 このプロパティの場合、クライアントではトラブルシューティングのための低レベルの情報がログ出力されます。 運用サイトではこのプロパティを使用しないでください。 過度のログ記録が実行され、ログ ファイル内で関連情報を見つけることが困難になる可能性があります。 また、[**CCMENABLELOGGING**](#ccmenablelogging) も有効にします。

サポートされる値:

- `0`: デバッグ ログを無効にします (既定値)
- `1`: デバッグ ログを有効にします

例: `CCMSetup.exe CCMDEBUGLOGGING=1`  

詳細については、[ログ ファイルの概要](../../plan-design/hierarchy/about-log-files.md)に関する記事をご覧ください。

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Configuration Manager では、既定でログ記録が有効になります。

サポートされる値:

- `TRUE`: ログ記録を有効にします (既定値)
- `FALSE`: ログ記録を無効にします

例: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

詳細については、[ログ ファイルの概要](../../plan-design/hierarchy/about-log-files.md)に関する記事をご覧ください。

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

クライアントの正常性評価ツール (ccmeval.exe) を実行する頻度 (分単位) です。 `1` から `1440` までの整数値を指定してください。 既定では、ccmeval は 1 日 (1440 分) に 1 回実行されます。

例: `CCMSetup.exe CCMEVALINTERVAL=1440`

クライアントの正常性評価の詳細については、[クライアントの監視](../manage/monitor-clients.md#bkmk_health)に関する記事をご覧ください。

### <a name="ccmevalhour"></a>CCMEVALHOUR

クライアントの正常性評価ツール (ccmeval.exe) を実行する 1 日のうちの時刻です。 `0` (深夜 0 時) から `23` (午後 11:00) までの整数値を指定します。 既定では、ccmeval は深夜 0 時に実行されます。

クライアントの正常性評価の詳細については、[クライアントの監視](../manage/monitor-clients.md#bkmk_health)に関する記事をご覧ください。

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

このプロパティを `1` に設定する場合は、クライアントにより、有効期限が最も長い PKI 証明書が選択されます。

例: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

クライアントがインターネット経由で管理される場合は、このプロパティでインターネット ベースの管理ポイントの FQDN を指定します。  

インストール プロパティ **SMSSITECODE=AUTO** と共にこのオプションを指定しないでください。 インターネット ベースのクライアントを、インターネット ベースのサイトに直接割り当てます。

例: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

このプロパティでは、クラウド管理ゲートウェイ (CMG) のアドレスを指定できます。 このプロパティの値を取得するには、次の手順を使用します。

- CMG を作成します。 詳細については、[CMG の設定](../manage/cmg/setup-cloud-management-gateway.md)に関する記事をご覧ください。
- アクティブなクライアントで、管理者として Windows PowerShell コマンド プロンプトを開きます。
- 次のコマンドを実行します。

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- **CCMHOSTNAME** プロパティで戻り値をそのまま使用します。

例: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> **CCMHOSTNAME** プロパティに CMG のアドレスを指定する場合は、`https://` などのプレフィックスを追加しないでください。 このプレフィックスは、CMG の **/mp** URL と共にのみ使用してください。

### <a name="ccmhttpport"></a>CCMHTTPPORT

クライアントが HTTP を介してサイト システム サーバーと通信するときに使用するポートを指定します。 既定では、この値は `80` です。

例: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

クライアントが HTTPS を介してサイト システム サーバーと通信するときに使用するポートを指定します。 既定では、この値は `443` です。

例: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

このプロパティを使用して、構成マネージャー クライアント ファイルをインストールするフォルダーを設定します。 既定では、`%WinDir%\CCM` が使用されます。

> [!TIP]
> クライアント ファイルをインストールする場所に関係なく、常に `%WinDir%\System32` フォルダーに **ccmcore.dll** ファイルがインストールされます。 64 ビット OS では、`%WinDir%\SysWOW64` フォルダーに ccmcore.dll のコピーがインストールされます。 このファイルでは、Configuration Manager SDK の 32 ビット バージョンのクライアント API を使用する 32 ビット アプリケーションがサポートされます。

例: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

このプロパティを使用して、Configuration Manager ログ ファイルに記録する詳細レベルを指定します。

サポートされる値:

- `0`: 詳細
- `1`: Default
- `2`: 警告とエラー
- `3`: エラーのみ

例: `CCMSetup.exe CCMLOGLEVEL=0`

詳細については、[ログ ファイルの概要](../../plan-design/hierarchy/about-log-files.md)に関する記事をご覧ください。

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Configuration Manager ログ ファイルが最大サイズに達した場合、クライアントはバックアップとしてその名前を変更し、新しいログ ファイルを作成します。 このプロパティでは、保持する以前のバージョンのログ ファイルの数を指定します。 既定値は `1` です。 この値を `0` に設定した場合、クライアントではログ ファイルの履歴が保持されません。

例: `CCMSetup.exe CCMLOGMAXHISTORY=5`

詳細については、[ログ ファイルの概要](../../plan-design/hierarchy/about-log-files.md)に関する記事をご覧ください。

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

このプロパティでは、ログ ファイルの最大サイズをバイト単位で指定します。 ログが指定されたサイズに達した場合、クライアントはその名前を履歴ファイルとして変更し、新しいファイルを作成します。 既定のサイズは 250,000 バイトで、最小サイズは 10,000 バイトです。

例:`CCMSetup.exe CCMLOGMAXSIZE=300000` (300,000 バイト)

### <a name="disablesiteopt"></a>DISABLESITEOPT

このプロパティを `TRUE` に設定すると、管理者は Configuration Manager コントロール パネルで割り当て済みサイトを変更できなくなります。

例:**CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

このプロパティを TRUE に設定すると、管理ユーザーは、**Configuration Manager** コントロール パネルでクライアント キャッシュ フォルダー設定を変更できなくなります。  

例: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

DNS に発行した管理ポイントをクライアントが検索できるように、DNS ドメインを指定します。 クライアントが管理ポイントを見つけると、その管理ポイントによって階層内のその他の管理ポイントに関する情報がクライアントに通知されます。 この動作は、クライアントが DNS から見つける管理ポイントは、階層内のどれでもかまわないということを意味します。

> [!NOTE]
> 発行された管理ポイントとクライアントが同じドメインにある場合は、このプロパティを指定する必要はありません。 この場合、DNS で管理ポイントを検索するために、クライアントのドメインが自動的に使用されます。

Configuration Manager クライアントに対するサービスの場所の検索方法として DNS 発行を使用することの詳細については、「[サービスの場所とクライアントが割り当て済み管理ポイントを特定する方法](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)」を参照してください。

> [!NOTE]  
> 既定では、Configuration Manager では DNS 発行は有効になっていません。

例: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Configuration Manager クライアントによって送信される状態メッセージを受信して処理するフォールバック ステータス ポイントを指定します。

詳細については、[フォールバック ステータス ポイントが必要かどうかを判断する方法](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)に関する記事をご覧ください。

例: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

このプロパティを `TRUE` に設定した場合、クライアント インストーラーでは、Microsoft Application Virtualization (App-V) の最低限必要なバージョンがチェックされません。

> [!IMPORTANT]  
> App-V をインストールせずに構成マネージャー クライアントをインストールする場合、[仮想アプリケーションをデプロイする](../../../apps/get-started/deploying-app-v-virtual-applications.md)ことはできません。

例: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

このプロパティを有効にすると、クライアントによって状態が報告されますが、見つかった問題は修復されません。

例: `CCMSetup.exe NOTIFYONLY=TRUE`

詳細については、「[クライアント ステータスを構成する方法](configure-client-status.md)」を参照してください。

### <a name="provisionts"></a>PROVISIONTS

<!--5526972-->

バージョン 2002 以降では、このプロパティを使用して、サイトに正常に登録された後にクライアント上でタスク シーケンスを開始します。

たとえば、Windows Autopilot を使用して新しい Windows 10 デバイスをプロビジョニングし、Microsoft Intune に自動登録した後、共同管理用の Configuration Manager クライアントをインストールします。 この新しいオプションを指定すると、新しくプロビジョニングされたクライアントでタスク シーケンスが実行されるようになります。 このプロセスにより、アプリケーションとソフトウェア更新プログラムをインストールしたり、設定を構成したりするための柔軟性が向上します。

次の手順を使用します。

1. [OS 以外の展開用タスク シーケンスを作成](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)して、アプリのインストール、ソフトウェア更新プログラムのインストール、および設定の構成を行います。

1. 新しい組み込みコレクションの**すべてのプロビジョニング デバイス**に、[このタスク シーケンスを展開](../../../osd/deploy-use/deploy-a-task-sequence.md)します。 タスク シーケンスの展開 ID (`PRI20001` など) をメモします。

1. デバイスに [Configuration Manager クライアントをインストール](deploy-clients-to-windows-computers.md#BKMK_Manual)し、`PROVISIONTS=PRI20001` というプロパティを含めます。 このプロパティの値をタスク シーケンスの展開 ID として設定します。

    - 共同管理の登録中に Intune からクライアントをインストールする場合は、「[共同管理用にインターネットベースのデバイスを準備する方法](../../../comanage/how-to-prepare-Win10.md)」を参照してください。

      > [!NOTE]
      > この方法には、追加の前提条件がある場合があります。 たとえば、Azure Active Directory へのサイトの登録や、コンテンツが有効なクラウド管理ゲートウェイの作成などです。

クライアントがインストールされ、サイトに正しく登録されると、参照されているタスク シーケンスが開始されます。 クライアントの登録に失敗すると、タスク シーケンスは開始されません。

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

クライアントに間違った Configuration Manager の信頼されたルート キーがある場合、信頼された管理ポイントに接続して新しい信頼されたルート キーを取得することがはできません。 このプロパティを使用して、古い信頼されたルート キーを削除します。 この状況は、クライアントを 1 つのサイト階層から別のサイト階層に移動したときに発生する場合があります。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。 詳細については、「[信頼されたルート キーの計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。

例: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

[SMSSITECODE=AUTO](#smssitecode) と共に使用した場合、クライアント アップグレードの自動サイト再割り当てが有効になります。

例: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

クライアント コンピューター上のクライアント キャッシュ フォルダーの場所を指定します。 既定では、キャッシュの場所は `%WinDir%\ccmcache` です。

例: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

このプロパティを [**SMSCACHEFLAGS**](#smscacheflags) プロパティと共に使用すると、クライアント キャッシュ フォルダーの場所を制御できます。 たとえば、最も空き容量の大きいクライアント ディスク ドライブにクライアント キャッシュ フォルダーをインストールする場合: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

このプロパティを使用して、クライアント キャッシュ フォルダーのインストールに関するさらなる詳細を指定します。 **SMSCACHEFLAGS** プロパティは、単独で使用することも、セミコロン (`;`) で区切った組み合わせで使用することもできます。

このプロパティを指定しない場合:

- クライアントでは、[**SMSCACHEDIR**](#smscachedir) プロパティに従ってキャッシュ フォルダーがインストールされます
- フォルダーは圧縮されません
- クライアントでは、キャッシュのサイズ制限 (MB) として [**SMSCACHESIZE**](#smscachesize) プロパティが使用されます

既存のクライアントをアップグレードする場合、クライアント インストーラーではこのプロパティは無視されます。

#### <a name="values-for-the-smscacheflags-property"></a>SMSCACHEFLAGS プロパティの値

- **PERCENTDISKSPACE**:キャッシュ サイズを "*合計*" ディスク領域に対するパーセントとして設定します。 このプロパティを指定する場合は、[**SMSCACHESIZE**](#smscachesize) もパーセント値に設定します。

- **PERCENTFREEDISKSPACE**:キャッシュ サイズを "*空き*" ディスク領域に対するパーセントとして設定します。 このプロパティを指定する場合は、[**SMSCACHESIZE**](#smscachesize) もパーセント値として設定します。 たとえば、ディスクに 10 MB の空き領域があり、`SMSCACHESIZE=50` を指定したとします。 クライアント インストーラーによって、キャッシュ サイズは 5 MB に設定されます。 このプロパティを **PERCENTDISKSPACE** プロパティと共に使用することはできません。

- **MAXDRIVE**:使用可能な最大のディスクにキャッシュをインストールします。 [**SMSCACHEDIR**](#smscachedir) プロパティを使用してパスを指定した場合、クライアント インストーラーではこの値が無視されます。

- **MAXDRIVESPACE**:空き領域が最大のディスク ドライブにキャッシュをインストールします。 [**SMSCACHEDIR**](#smscachedir) プロパティを使用してパスを指定した場合、クライアント インストーラーではこの値が無視されます。

- **NTFSONLY**:NTFS 形式のディスク ドライブにのみキャッシュをインストールします。 [**SMSCACHEDIR**](#smscachedir) プロパティを使用してパスを指定した場合、クライアント インストーラーではこの値が無視されます。

- **COMPRESS**:キャッシュを圧縮された形式で格納します。

- **FAILIFNOSPACE**:キャッシュをインストールするための十分な領域がない場合は、構成マネージャー クライアントを削除します。

例: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> クライアント設定でクライアント キャッシュ フォルダーのサイズを指定できます。 これらのクライアント設定を追加すると、SMSCACHESIZE を使用して、クライアント キャッシュのサイズを指定する client.msi プロパティとして効果的に置き換えられます。 詳細については、「[キャッシュ サイズに関するクライアント設定](about-client-settings.md#client-cache-settings)」を参照してください。  

既存のクライアントをアップグレードする場合、クライアント インストーラーではこの設定は無視されます。 クライアントでは、ソフトウェア更新プログラムをダウンロードするときにもキャッシュ サイズが無視されます。

例: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> クライアントを再インストールする場合、**SMSCACHESIZE** または **SMSCACHEFLAGS** を使用して以前よりも小さいキャッシュ サイズを設定することはできません。 以前のサイズが最小値となります。

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

このプロパティを使用して、クライアント インストーラーによって構成設定が確認される場所と順序を指定します。 これは、各文字が特定の構成ソースを定義する 1 文字以上の文字列で構成されます。

- `R`: レジストリで構成設定を確認します。

  詳細については、「[クライアント インストールのプロパティをプロビジョニングする](deploy-clients-to-windows-computers.md#BKMK_Provision)」をご覧ください。

- `P`: コマンド ラインからのインストール プロパティに含まれる構成設定を確認します。

- `M`: 古いクライアントをアップグレードする場合に既存の設定を確認します。

- `U`: インストールしたクライアントを新しいバージョンにアップグレードし、割り当てられたサイト コードを使用します。

既定では、クライアント インストーラーでは `PU` が使用されます。 最初にインストール プロパティ (`P`) が確認された後、既存の設定 (`U`) が確認されます。  

例: `CCMSetup.exe SMSCONFIGSOURCE=RP`

<!--
### SMSDIRECTORYLOOKUP

Specifies whether the client can use Windows Internet Name Service (WINS) to find a management point that accepts HTTP connections. Clients use this method when they can't find a management point in Active Directory Domain Services or in DNS.  

 This property doesn't affect whether the client uses WINS for name resolution.  

 You can configure two different modes for this property:  

-   NOWINS: This value is the most secure setting for this property and prevents clients from finding a management point in WINS. When you use this setting, clients must have an alternative method to locate a management point on the intranet, such as Active Directory Domain Services or by using DNS publishing.  

-   WINSSECURE (default): In this mode, a client that uses HTTP communication can use WINS to find a management point. However, the client must have a copy of the trusted root key before it can successfully connect to the management point. For more information, see [Planning for the trusted root key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

Example: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  
-->

### <a name="smsmp"></a>SMSMP

Configuration Manager クライアントが使用する最初の管理ポイントを指定します。  

> [!IMPORTANT]  
> 管理ポイントが HTTPS 経由のクライアント接続のみを受け入れる場合は、管理ポイント名の先頭に `https://` を付けてください。

例:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

クライアントが Active Directory Domain Services から Configuration Manager の信頼されたルート キーを取得できない場合は、このプロパティを使用してキーを指定します。 このプロパティは、HTTP および HTTPS 通信を使用するクライアントに適用されます。 詳細については、「[信頼されたルート キーの計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。

例: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> サイト サーバー上の mobileclient.tcf ファイルから、サイトの信頼されたルート キーの値を取得します。 詳細については、「[ファイルを使用して信頼されたルート キーをクライアントに事前に準備する](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file)」をご覧ください。

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

このプロパティを使用すると、Configuration Manager の信頼されたルート キーを再インストールできます。 信頼されたルート キーを含むファイルの完全なパスと名前を指定します。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。 詳細については、「[信頼されたルート キーの計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。

例: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

サイト サーバー上のエクスポートされた自己署名証明書の完全なパスと名前を指定します。 サイト サーバーでは、この証明書が **SMS** 証明書ストアに格納されます。 そのサブジェクト名は **Site Server** で、フレンドリ名は **Site Server Signing Certificate** です。

例: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

このプロパティでは、クライアントを割り当てる Configuration Manager サイトを指定します。 この値には、3 文字のサイト コード、または `AUTO` という単語を指定できます。 `AUTO` を指定する場合、またはこのプロパティを指定しない場合、クライアントは、Active Directory Domain Services または指定した管理ポイントからサイト割り当てを判断しようとします。 クライアントのアップグレードに対して `AUTO` を有効にするには、[SITEREASSIGN=TRUE](#sitereassign) も設定してください。

> [!NOTE]  
> また、[**CCMHOSTNAME**](#ccmhostname) プロパティを使用してインターネット ベースの管理ポイントも指定する場合は、**SMSSITECODE** と共に `AUTO` を使用しないでください。 サイト コードを指定することで、クライアントを直接そのサイトに割り当ててください。

例: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> 証明書の選択条件のための属性値

Configuration Manager は、PKI 証明書の選択条件として次の属性値をサポートしています。

|OID 属性|識別名属性|属性の定義|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|ドメイン要素|  
|1.2.840.113549.1.9.1|E または E-mail|電子メール アドレス|  
|2.5.4.3|CN|共通名|  
|2.5.4.4|SN|サブジェクト名|  
|2.5.4.5|SERIALNUMBER|シリアル番号|  
|2.5.4.6|C|国番号|  
|2.5.4.7|L|地域|  
|2.5.4.8|S または ST|州または都道府県|  
|2.5.4.9|STREET|住所|  
|2.5.4.10|O|組織名|  
|2.5.4.11|OU|組織単位|  
|2.5.4.12|T または Title|タイトル|  
|2.5.4.42|G または GN または GivenName|名前|  
|2.5.4.43|I または Initials|イニシャル|  
|2.5.29.17|(値なし)|サブジェクト代替名|  
