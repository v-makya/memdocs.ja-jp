---
title: Windows にクライアントを展開する
titleSuffix: Configuration Manager
description: 構成マネージャー クライアントを Windows コンピューターに展開する方法を説明します。
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2eea75f39430f1cc38ff994280425ca918eaa432
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694561"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Configuration Manager でクライアントを Windows コンピューターに展開する方法

*適用対象:Configuration Manager (Current Branch)*

この記事では、構成マネージャー クライアントを Windows コンピューターに展開する方法を説明します。 クライアントの展開の計画と準備について詳しくは、次の記事をご覧ください。

- [クライアント インストール方法](plan/client-installation-methods.md)  
- [Windows コンピューターにクライアントを展開するための前提条件](prerequisites-for-deploying-clients-to-windows-computers.md)
- [構成マネージャー クライアントのセキュリティとプライバシー](plan/security-and-privacy-for-clients.md)  
- [クライアント展開のベスト プラクティス](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a> クライアント プッシュ インストール

クライアント プッシュを使う方法は主に次の 3 つです。  

- サイトに対してクライアント プッシュ インストールを構成するときに、サイトが検出したコンピューターでクライアントのインストールを自動的に実行します。 この方法の範囲は、サイトの境界が境界グループとして構成されているときの、構成済みの境界です。  

- 特定のコレクションまたはコレクション内のリソースでクライアント プッシュ インストール ウィザードを実行して、クライアント プッシュ インストールを開始します。  

- クライアント プッシュ インストール ウィザードを使って構成マネージャー クライアントをインストールします。これを使って結果に対する[クエリを実行する](../../servers/manage/introduction-to-queries.md)ことができます。 インストールが成功するには、クエリで返される項目の 1 つが、**System Resource** クラスの **ResourceID** 属性である場合のみです。

サイト サーバーは、クライアント コンピューターにアクセスできない場合やセットアップ プロセスを開始できない場合、1 時間ごとに自動的にインストールを再試行します。 サーバーは、最大 7 日間再試行を続けます。  

クライアントのインストール プロセスを追跡するには、クライアントをインストールする前に、フォールバック ステータス ポイントをインストールします。 インストールしたフォールバック ステータス ポイントは、クライアント プッシュ インストール方法でクライアントをインストールするときに、自動的にクライアントに割り当てられます。 クライアントのインストールの進行状況を追跡するには、クライアント展開レポートとクライアント割り当てレポートを確認します。

クライアント ログ ファイルは、トラブルシューティングに関する詳細な情報を提供します。 ログ ファイルには、フォールバック ステータス ポイントは不要です。 たとえば、サイト サーバー上の CCM.log ファイルには、サイト サーバーがコンピューターに接続するときに発生するすべての問題が記録されます。 クライアント上の CCMSetup.log ファイルには、インストールのプロセスが記録されます。  

> [!IMPORTANT]  
> クライアント プッシュは、すべての前提条件が満たされている場合にのみ成功します。 詳細については、「[インストール方法の依存関係](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies)」をご覧ください。

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>検出されたコンピューターに対してクライアント プッシュを自動的に使用するようにサイトを構成する

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2. サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

3. リボンの **[ホーム]** タブの **[設定]** グループで、 **[クライアント インストール設定]** を選択した後、 **[クライアント プッシュ インストール]** を選択します。  

4. [クライアント プッシュ インストールのプロパティ] ウィンドウの **[全般]** タブで、 **[サイト全体にクライアントを自動的にプッシュ インストールする]** を選択します。

5. バージョン 1806 以降では、サイトを更新すると、クライアント プッシュに対する Kerberos のチェックが有効になります。 以前の動作と同じように、 **[NTLM への接続フォールバックを許可する]** オプションは既定で有効になります。 サイトが Kerberos を使ってクライアントを認証できない場合は、NTLM を使って接続が再試行されます。 セキュリティを強化するため、この設定を無効にすることをお勧めします。そのためには、NTLM フォールバックなしの Kerberos が必要です。<!--1358204-->  

    > [!NOTE]  
    > 構成マネージャー クライアントをインストールするためにクライアント プッシュが使われた場合、サイト サーバーによってクライアントへのリモート接続が作成されます。 バージョン 1806 以降のサイトでは、接続を確立する前の NTLM へのフォールバックを許可しないことによって、Kerberos の相互認証を要求できます。 この機能強化は、サーバーとクライアント間の通信をセキュリティで保護するのに役立ちます。  
    >
    > セキュリティ ポリシーによっては、お客様の環境が既に以前の NTLM 認証よりも Kerberos を優先する、または要求するものになっている場合があります。 これらの認証プロトコルに関するセキュリティの考慮事項について詳しくは、[NTLM を制限する Windows セキュリティ ポリシーの設定](/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations)に関するページをご覧ください。  
    >
    > この機能を使用するには、信頼された Active Directory フォレスト内にクライアントがいる必要があります。 Windows の Kerberos は、相互認証について Active Directory に依存しています。  

6. Configuration Manager でクライアント ソフトウェアをプッシュするシステムの種類を選択します。 ドメイン コント ローラーにクライアントをインストールするかどうかを選択します。  

7. **[アカウント]** タブで、ターゲット コンピューターに接続する際に Configuration Manager によって使用されるアカウントを 1 つ以上指定します。 **[作成]** アイコンを選択し、 **[ユーザー名]** と **[パスワード]** (38 文字以内) を入力して、パスワードを確認入力してから、 **[OK]** を選択します。 クライアント プッシュ インストール アカウントを少なくとも 1 つ指定します。 クライアントをインストールするには、このアカウントがターゲット コンピューターに対するローカル管理者権限を持っている必要があります。 クライアント プッシュ インストール アカウントを指定しないと、Configuration Manager はサイト システムのコンピューター アカウントを使います。 サイト システムのコンピューター アカウントを使った場合、クロス ドメインのクライアント プッシュは失敗します。  

    > [!NOTE]  
    > セカンダリ サイトからのクライアント プッシュを使うには、クライアント プッシュを開始するセカンダリ サイトのアカウントを指定します。  
    >
    > クライアント プッシュ インストール アカウントについては、次の手順「[クライアント プッシュ インストール ウィザードを使用する](#use-the-client-push-installation-wizard)」をご覧ください。  

8. **［インストールのプロパティ］** タブ上で必要なインストールのプロパティを指定します。

    Configuration Manager 用に Active Directory スキーマを拡張している場合は、サイトにより、指定された[クライアント インストール プロパティ](about-client-installation-properties.md)が Active Directory Domain Services に発行されます。 CCMSetup は、実行時にインストール プロパティがないと、Active Directory からプロパティを読み取ります。  

    > [!NOTE]  
    > セカンダリ サイトでクライアント プッシュ インストールを有効にする場合は、**SMSSITECODE** プロパティをその親プライマリ サイトの Configuration Manager サイト コードに設定します。 Active Directory スキーマを Configuration Manager 用に拡張した場合、正しいサイトの割り当てを自動的に発見するには、このプロパティを **AUTO** に設定します。

### <a name="use-the-client-push-installation-wizard"></a>クライアント プッシュ インストール ウィザードを使用する

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2. サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

3. リボンの **[ホーム]** タブの **[設定]** グループで、 **[クライアント インストール設定]** を選択した後、 **[クライアント プッシュ インストール]** を選択します。  

4. **［インストールのプロパティ］** タブ上で必要なインストールのプロパティを指定します。  

    Configuration Manager 用に Active Directory スキーマを拡張している場合は、サイトにより、指定された[クライアント インストール プロパティ](about-client-installation-properties.md)が Active Directory Domain Services に発行されます。 CCMSetup は、実行時にインストール プロパティがないと、Active Directory からプロパティを読み取ります。

5. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動します。  

6. **[デバイス]** ノードで、1 つ以上のコンピューターを選択します。 または、 **[デバイス コレクション]** ノードで、コンピューターのコレクションを選択します。  

7. リボンの **[ホーム]** タブで、次のオプションのいずれかを選びます。  

    - クライアントを 1 つまたは複数のデバイスにプッシュするには、 **[デバイス]** グループで、 **[クライアントのインストール]** を選択します。  

    - クライアントをデバイスのコレクションにプッシュするには、 **[コレクション]** グループで、 **[クライアントのインストール]** を選択します。  

8. [Configuration Manager クライアントのインストール ウィザード] の **[開始する前に]** ページで情報を確認してから、 **[次へ]** を選択します。  

9. **[インストール オプション]** ページで、適切なオプションを選択します。  

10. インストールの設定を確認してから、ウィザードを完了します。  

> [!NOTE]  
> サイトがクライアント プッシュ用に構成されていない場合でも、このウィザードを使ってクライアントをインストールします。  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> ソフトウェアの更新に基づいたインストール  

ソフトウェアの更新に基づいたクライアント インストールでは、クライアントをソフトウェア更新プログラムとしてソフトウェアの更新ポイントに発行します。 初回のインストールまたはアップグレードには、この方法を使用します。  

コンピューターに構成マネージャー クライアントがインストールされている場合、そのコンピューターはサイトからクライアント ポリシーを受け取ります。 このポリシーには、ソフトウェアの更新ポイントのサーバー名と、ソフトウェア更新プログラムの取得元のポートが含まれます。

> [!IMPORTANT]  
> ソフトウェアの更新に基づいたインストールの場合は、クライアントのインストールとソフトウェア更新プログラムに同じ Windows Server Update Services (WSUS) サーバーを使います。 このサーバーは、プライマリ サイトでアクティブなソフトウェアの更新ポイントである必要があります。 詳細については、「[Install a software update point](../../../sum/get-started/install-a-software-update-point.md)」 (ソフトウェアの更新ポイントのインストール) をご覧ください。

コンピューターに構成マネージャー クライアントがインストールされていない場合は、グループ ポリシー オブジェクトを構成して割り当てます。 グループ ポリシーによって、ソフトウェアの更新ポイントのサーバー名を指定します。  

ソフトウェア更新プログラムに基づいたクライアント インストールに、コマンド ライン プロパティを追加することはできません。 Configuration Manager 用に Active Directory スキーマを拡張している場合は、クライアントをインストールすると自動的に Active Directory Domain Services でインストールのプロパティが照会されます。  

Active Directory スキーマを拡張していない場合は、グループ ポリシーを使って、クライアント インストールの設定をプロビジョニングします。 これらの設定は、ソフトウェアの更新に基づいたクライアント インストールに自動的に適用されます。 詳しくは、[クライアント インストール プロパティのプロビジョニング方法](#BKMK_Provision)に関するセクションおよび[サイトにクライアントを割り当てる方法](assign-clients-to-a-site.md)に関する記事をご覧ください。  

構成マネージャー クライアントでソフトウェアの更新ポイントを使わずにコンピューターを構成するには、次の手順を使います。 ソフトウェアの更新ポイントにクライアント ソフトウェアを発行するための手順もあります。  

> [!TIP]  
> コンピューターが前のソフトウェアのインストール後に再起動の保留状態になっている場合、ソフトウェアの更新に基づいたクライアントのインストールによってコンピューターが再起動する可能性があります。  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>グループ ポリシー オブジェクトを構成してソフトウェアの更新ポイントを指定する  

1. **グループ ポリシー管理コンソール**を使って、新規または既存のグループ ポリシー オブジェクトを開きます。  

2. **[コンピューターの構成]** 、 **[管理用テンプレート]** 、 **[Windows コンポーネント]** の順に展開し、 **[Windows Update]** を選択します。  

3. **[イントラネットの Microsoft 更新サービスの場所を指定する]** 設定のプロパティを開いてから、 **[有効]** を選択します。  

4. **[更新を検出するためのイントラネットの更新サービスを設定する]** :ソフトウェア更新ポイント サーバーの名前とポートを指定します。  

    - 完全修飾ドメイン名 (FQDN) を使うように Configuration Manager サイト システムを構成している場合は、その形式を使います。  

    - Configuration Manager サイト システムが完全修飾ドメイン名 (FQDN) を使うように構成されていない場合は、短い名前の形式を使います。

    > [!TIP]  
    > ポート番号を確認するには、[WSUS で使用するポート設定の特定方法](../../../sum/plan-design/plan-for-software-updates.md)に関するページをご覧ください。

    FQDN 形式での例: `http://server1.contoso.com:8530`  

5. **[イントラネット統計サーバーの設定]** :通常、この設定は同じサーバー名を使って構成されます。

6. クライアントのインストール先とし、ソフトウェア更新プログラムを受け取るコンピューターに、グループ ポリシー オブジェクトを割り当てます。  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>構成マネージャー クライアントをソフトウェアの更新ポイントに発行する  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2. ソフトウェアの更新に基づいたクライアントのインストールを構成するサイトを選択します。  

3. リボンの **[ホーム]** タブの **[設定]** グループで、 **[クライアント インストール設定]** を選択し、 **[ソフトウェアの更新に基づいたクライアントのインストール]** を選択します。  

4. **[ソフトウェアの更新に基づいたクライアントのインストールを有効にする]** を選択します。  

5. サイトのクライアントのバージョンが、ソフトウェアの更新ポイントでのバージョンより新しい場合は、 **[新しいバージョンのクライアント パッケージが見つかりました]** ダイアログ ボックスが開きます。 **[はい]** を選択して、最新バージョンを発行します。  

    > [!NOTE]  
    > クライアント ソフトウェアをソフトウェアの更新ポイントにまだ発行していない場合、このダイアログ ボックスは空白になります。

構成マネージャー クライアント用のソフトウェア更新プログラムは、新しいバージョンが存在する場合に自動的に更新されるわけではありません。 サイトを更新するときに、この手順を繰り返してクライアントを更新します。  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a> グループ ポリシーによるインストール

Active Directory Domain Services のグループ ポリシーを使って、構成マネージャー クライアントの発行や割り当てを行います。 クライアントは、コンピューターの起動時にインストールされます。 グループ ポリシーを使用すると、コントロール パネルの **[プログラム追加と削除]** にクライアントが表示されます。 ユーザーはそこからそれをインストールできます。  

グループ ポリシーに基づいたインストールには、Windows インストーラー パッケージ CCMSetup.msi を使います。 このファイルは、サイト サーバーの `<ConfigMgr installation directory>\bin\i386` フォルダーにあります。 このファイルにプロパティを追加してインストールの動作を変更することはできません。  

> [!IMPORTANT]  
> クライアント インストール ファイルにアクセスするには、管理者権限をお持ちである必要があります。  

- Active Directory スキーマを Configuration Manager 用に拡張していて、 **[サイトのプロパティ]** ダイアログ ボックスの **[発行]** タブでこのドメインを選択している場合、クライアント コンピューターによって自動的に Active Directory Domain Services でインストールのプロパティが検索されます。 詳細については、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](about-client-installation-properties-published-to-active-directory-domain-services.md)」をご覧ください。  

- Active Directory スキーマを拡張していない場合、コンピューターの Windows レジストリにインストールのプロパティを格納する方法については、[クライアント インストール プロパティのプロビジョニング](#BKMK_Provision)に関するセクションをご覧ください。 クライアントはインストール時にこれらのインストール プロパティを使います。  

詳細については、[グループ ポリシーを使用してソフトウェアをリモートでインストールする方法](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server)に関するページをご覧ください。  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a> 手動インストール

CCMSetup.exe を使用してクライアント ソフトウェアをコンピューターに手動でインストールします。 このプログラムとそのサポート ファイルは、サイト サーバー上の Configuration Manager インストール フォルダーの Client フォルダー内にあります。 サイトは次のようにネットワークに対してこのフォルダーを共有します。  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>` はプライマリ サイト サーバーの名前です。 `<site code>` は、クライアントが割り当てられているプライマリ サイト コードです。 クライアントでコマンド ラインから CCMSetup.exe を実行するには、このネットワークの場所に接続してから、コマンドを実行します。  

> [!IMPORTANT]  
> クライアント インストール ファイルにアクセスするには、管理者権限をお持ちである必要があります。  

CCMSetup.exe は、必要なすべての前提条件をクライアント コンピューターにコピーし、Windows インストーラー パッケージ (Client.msi) を呼び出してクライアントをインストールします。 Client.msi を直接実行することはできません。  

クライアント インストールの動作を変更するには、CCMSetup.exe と Client.msi の両方にコマンド ライン オプションを指定します。 Client.msi のプロパティを指定する前に、`/` で始まる CCMSetup のパラメーターを指定する必要があります。 次に例を示します。  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

この例では、次のオプションを使ってクライアントがインストールされます。  

|オプション|[説明]|  
|--------------|-----------------|  
|`/mp:SMSMP01`|この CCMSetup パラメーターを使って、必要なクライアント インストール ファイルをダウンロードする管理ポイント SMSMP01 を指定します。|  
|`/logon`|この CCMSetup パラメーターは、既存の構成マネージャー クライアントがコンピューターで見つかった場合はインストールを停止するように指定します。|  
|`SMSSITECODE=AUTO`|この Client.msi のプロパティを使うと、たとえば Active Directory Domain Services を使って、使用する Configuration Manager サイト コードの特定をクライアントが試みるよう指定できます。|  
|`FSP=SMSFP01`|Client.msi のこのプロパティで、SMSFP01 というフォールバック ステータス ポイントを使って、クライアント コンピューターから送信される状態メッセージを受信するように指定します。|  

詳しくは、[クライアント インストールのパラメーターとプロパティ](about-client-installation-properties.md)に関するページをご覧ください。  

> [!TIP]  
> Azure Active Directory (Azure AD) の ID を使って最新の Windows 10 デバイスに構成マネージャー クライアントをインストールする手順については、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](deploy-clients-cmg-azure.md)」をご覧ください。 その手順は、イントラネットまたはインターネット上のクライアント向けのものです。  

### <a name="manual-installation-examples"></a>手動インストールの例

以下の例は、Active Directory に参加しているイントラネット上のクライアントに関するものです。 次の値を使います。  

- **MPSERVER**: 管理ポイントをホストするサーバー
- **FSPSERVER**: フォールバック ステータス ポイントをホストするサーバー  
- **ABC**: サイト コード  
- **contoso.com**: ドメイン名  

イントラネットの FQDN を使ってすべてのサイト システム サーバーを構成し、Active Directory にサイト情報を発行していると想定してください。  

クライアント コンピューターで以下の手順を始めます。  

1. ローカル管理者としてサインインします。  
2. Z ドライブを `\\MPSERVER\SMS_ABC\Client` にマップします。  
3. コマンド プロンプトを Z ドライブに切り替えます。  

それから、次のいずれかのコマンドを実行します。  

#### <a name="manual-example-1"></a>手動の例 1  

`CCMSetup.exe`  

このコマンドを使って、追加のパラメーターまたはプロパティなしでクライアントをインストールします。 クライアントは、Active Directory Domain Services に発行されたクライアント インストール プロパティを使って自動的に構成されます。次の設定が含まれます。  

- サイト コード:この設定では、クライアントの割り当て用に構成されている境界グループに、クライアントのネットワークの場所が含まれる必要があります。  
- 管理ポイント。
- フォールバック ステータス ポイント。
- HTTPS のみを使った通信。  

詳細については、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](about-client-installation-properties-published-to-active-directory-domain-services.md)」をご覧ください。  

#### <a name="manual-example-2"></a>手動の例 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
このコマンドでは、Active Directory Domain Services に用意されている自動構成がオーバーライドされます。 クライアントの割り当て用に構成されている境界グループに、クライアントのネットワークの場所を含める必要はありません。 代わりに、インストールでは次の設定を指定します。

- サイト コード
- イントラネット管理ポイント
- インターネット ベースの管理ポイント
- インターネットからの接続を受け入れるフォールバック ステータス ポイント
- 最長の有効期間を持つクライアントの公開キー基盤 (PKI) 証明書を使用する (使用できる場合)

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a> ログオン スクリプトによるインストール

Configuration Manager では、構成マネージャー クライアント ソフトウェアをインストールするログオン スクリプトの使用がサポートされています。 ログオン スクリプトで CCMSetup.exe プログラム ファイルを使用して、クライアント インストールを開始します。  

ログオン スクリプト インストールの使用方法は、手動のクライアント インストールと同じです。 CCMSsetup.exe に対して `/logon` インストール パラメーターを指定します。 このパラメーターを指定すると、クライアントのいずれかのバージョンがコンピューターに既に存在する場合、クライアントはインストールされません。 この動作により、ログオン スクリプトが実行されるたびにクライアントの再インストールが発生することはなくなります。  

`/Source` パラメーターを使ってインストール ソースを指定せず、`/MP` パラメーターでインストール取得元の管理ポイントを指定しなかった場合、CCMSetup.exe では Active Directory Domain Services を検索することで管理ポイントが見つけられます。 この動作は、スキーマを Configuration Manager 用に拡張し、サイトを Active Directory Domain Services に発行している場合にのみ発生します。 または、クライアントが DNS または WINS を使用して管理ポイントを特定することもできます。  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a> パッケージとプログラムのインストール

選択したデバイスのクライアント ソフトウェアをアップグレードするパッケージとプログラムを作成して展開するには、Configuration Manager を使います。 Configuration Manager には、通常使用される値をパッケージ プロパティに設定するパッケージ定義ファイルが付属しています。 追加のコマンド ライン パラメーターとプロパティを指定することで、クライアント インストールの動作をカスタマイズします。  

> [!NOTE]  
> この方法では、Configuration Manager 2007 クライアントをアップグレードすることはできません。 代わりに、最新バージョンのクライアントが含まれたパッケージを自動的に作成して展開する自動クライアント アップグレードを使用します。 詳細については、「[クライアントをアップグレードする](../manage/upgrade/upgrade-clients.md)」をご覧ください。  
>
> 旧バージョンの構成マネージャー クライアントから移行する方法については、「[System Center Configuration Manager でのクライアント移行戦略の計画](../../migration/planning-a-client-migration-strategy.md)」をご覧ください。  

### <a name="create-a-package-and-program-for-the-client-software"></a>クライアント ソフトウェア用のパッケージとプログラムを作成する  

次の手順に従って、クライアント ソフトウェアをアップグレードするために構成マネージャー クライアント コンピューターに展開できる、Configuration Manager パッケージとプログラムを作成します。  

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[パッケージ]** ノードを選択します。  

2. リボンの **[ホーム]** タブの **[作成]** グループで、 **[定義に基づいたパッケージの作成]** を選択します。  

3. ウィザードの **[パッケージの定義]** ページで、 **[発行元]** の一覧から **[Microsoft]** を選択し、 **[パッケージ定義]** の一覧から **[Configuration Manager クライアントのアップグレード]** を選択します。  

4. **[ソース ファイル]** ページで、 **[常にソース フォルダーからファイルを取得する]** を選択します。  

5. **[ソース フォルダー]** ページで、 **[ネットワーク パス (UNC 名)]** を選びます。 その後、クライアント インストール ファイルが含まれているサーバーと共有のネットワーク パスを入力します。  

    > [!NOTE]  
    > Configuration Manager の展開を実行するコンピューターが、指定したネットワーク フォルダーへのアクセス権を持っている必要があります。 ない場合、クライアントのインストールは失敗します。  

    クライアント インストールのプロパティを変更するには、 **[Configuration Manager エージェントのサイレント アップグレードのプロパティ]** プログラム ダイアログ ボックスの **[全般]** タブで CCMSetup.exe のコマンド ラインを変更します。 既定のインストール プロパティは `/noservice SMSSITECODE=AUTO` です。  

6. クライアント アップグレード パッケージをホストする必要があるすべての配布ポイントにパッケージを配布します。 次に、アップグレードが必要なクライアントが含まれているデバイスのコレクションにパッケージを展開します。  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a> Intune MDM で管理された Windows デバイス

Microsoft Intune で登録されたデバイスに構成マネージャー クライアントを展開します。

この手順は、イントラネットに接続されている従来のクライアントに向けたものです。 従来のクライアント認証方法を使います。 クライアントのインストール後にデバイスが管理された状態のままになるようにするには、デバイスがイントラネット上にあり、Configuration Manager サイトの境界内にある必要があります。  

Azure AD の ID を使って最新の Windows 10 デバイスに構成マネージャー クライアントをインストールする手順については、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](deploy-clients-cmg-azure.md)」をご覧ください。

構成マネージャー クライアントをインストールした後に、デバイスが Intune から登録解除されることはありません。 それらでは、構成マネージャー クライアントと MDM 登録を同時に使用することができます。 詳しくは、[共同管理の概要](../../../comanage/overview.md)に関するページをご覧ください。  

> [!Note]
> 他のクライアント インストール方法を使って、Intune で管理されたデバイスに構成マネージャー クライアントをインストールすることができます。 たとえば、Intune で管理されたデバイスがイントラネット上にあり、Active Directory ドメインに参加している場合は、グループ ポリシーを使って構成マネージャー クライアントをインストールできます。<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>Intune を使って構成マネージャー クライアントをインストールする

1. Intune で、構成マネージャー クライアントのインストール ファイル **CCMSetup.msi** を含んだ [Windows 基幹業務アプリを追加](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows)します。 このファイルは、サイト サーバー上の Configuration Manager インストール ディレクトリの `\bin\i386` フォルダー内にあります。  

2. Intune ソフトウェア パブリッシャーで、コマンド ライン パラメーターを入力します。 たとえば、イントラネット上の従来のクライアントでは次のコマンドを使います。  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > Azure AD 認証を使用する最新の Windows 10 クライアントで使うコマンドの例については、[共同管理用にインターネット ベースのデバイスを準備する方法](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)に関するページをご覧ください。  

3. 登録済みの Windows コンピューターのグループに[アプリを割り当て](../../../../intune/apps/apps-deploy.md)ます。  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a> OS イメージのインストール

OS イメージの作成に使う参照コンピューターに、構成マネージャー クライアントをプレインストールします。

> [!IMPORTANT]  
> Configuration Manager のタスク シーケンスを使って OS イメージを展開する場合、[ConfigMgr クライアントの準備](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)ステップによって構成マネージャー クライアントが完全に削除されます。  

### <a name="prepare-the-client-computer-for-imaging"></a>イメージング用にクライアント コンピューターを準備する  

1. 参照コンピューターに構成マネージャー クライアント ソフトウェアを手動でインストールします。 詳細については、[構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションをご覧ください。  

    > [!IMPORTANT]  
    > CCMSetup.exe コマンド ライン プロパティでクライアントに Configuration Manager サイト コードを指定しないでください。  

2. コマンド プロンプトで「`net stop ccmexec`」と入力して、参照コンピューター上の SMS Agent Host サービス (CcmExec.exe) を停止します。  

3. 参照コンピューター上の Windows フォルダーから、SMSCFG.INI ファイルを削除します。  

4. 参照コンピューターのローカル コンピューター ストアに保存されている証明書を削除します。 たとえば、PKI 証明書を使用する場合、コンピューターをイメージングする前に、 **[コンピューター]** と **[ユーザー]** の **[個人用]** ストアの証明書を削除します。  

5. 参照コンピューターの Configuration Manager 階層とは別の階層にクライアントをインストールする場合は、参照コンピューターから信頼されたルート キーを削除します。  

    > [!NOTE]  
    > クライアントは、Active Directory Domain Services に管理ポイントを照会できない場合、信頼されたルート キーを使用して信頼された管理ポイントを検索します。 イメージングされたすべてのクライアントをマスター コンピューターと同じ階層に展開する場合は、信頼されたルート キーをそのまま残しておきます。
    >
    > クライアントを別の階層に展開する場合は、信頼されたルート キーを削除します。 また、信頼されたルート キーでクライアントをプロビジョニングします。 詳細については、「[信頼されたルート キーの計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。  

6. イメージング ソフトウェアを使用して、参照コンピューターのイメージをキャプチャします。  

7. イメージをターゲット コンピューターに展開します。  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> ワークグループ コンピューター

Configuration Manager は、ワークグループ内のコンピューターへのクライアント インストールをサポートします。 [構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションで指定された方法を使って、ワークグループ コンピューターにクライアントをインストールします。  

### <a name="prerequisites"></a>[前提条件]  

- 各ワークグループ コンピューターにクライアントを手動でインストールします。 インストール時に、対話ユーザーはローカル管理者権限を持っている必要があります。  

- Configuration Manager サイト サーバーのドメイン内のリソースにアクセスするには、このサイト用にネットワーク アクセス アカウントを構成します。 このアカウントをソフトウェアの配布サイト コンポーネントで指定します。 詳しくは、「[サイト コンポーネント](../../servers/deploy/configure/site-components.md)」をご覧ください。  

### <a name="limitations"></a>制限事項  

- ワークグループ クライアントは、Active Directory Domain Services から管理ポイントを特定できません。 代わりに、DNS、WINS、または別の管理ポイントが使用されます。  

- グローバル ローミングはサポートされていません。 ワークグループ クライアントは、Active Directory Domain Services でサイト情報を照会できません。  

- Active Directory 探索方法では、ワークグループ内のコンピューターを探索できません。  

- ワークグループ コンピューターのユーザーにソフトウェアを展開することはできません。  

- クライアント プッシュ インストール方法を使用して、ワークグループ コンピューターにクライアントをインストールすることはできません。  

- ワークグループ クライアントの場合は、認証に Kerberos を使用できないので、手動の承認が必要になる場合があります。  

- 配布ポイントとしてワークグループ クライアントを構成することはできません。 Configuration Manager では、配布ポイントであるコンピューターがドメインのメンバーに指定されている必要があります。  

### <a name="install-the-client-on-workgroup-computers"></a>ワークグループ コンピューターにクライアントインストールする  

前提条件を確認してから、[構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションの指示に従います。  

#### <a name="workgroup-example-1"></a>ワークグループの例 1

この例では次の処理を行います。

- イントラネット クライアント管理用のクライアントをインストールします
- サイト コードを指定します
- 管理ポイントを検索するための DNS サフィックスを指定します  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>ワークグループの例 2

この例では、境界グループ内に構成されたネットワークの場所にクライアントを配置する必要があります。 この要件が満たされていない場合、サイトの自動割り当ては機能しません。 コマンドには、サーバー FSPSERVER 上のフォールバック ステータス ポイントが含まれます。 このプロパティは、クライアントの展開を追跡し、クライアントの通信に関する問題を特定するのに役立ちます。

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> インターネット ベースのクライアント管理  

> [!NOTE]  
> このセクションの内容は、[クラウド管理ゲートウェイ](../manage/cmg/plan-cloud-management-gateway.md)を使うクライアントには適用されません。 クラウド管理ゲートウェイを使ってインターネット ベースのクライアントをインストールするには、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](deploy-clients-cmg-azure.md)」をご覧ください。  

Configuration Manager サイトで、イントラネット上にある場合とインターネット上にある場合があるクライアントに対する[インターネットベースのクライアント管理](../manage/plan-internet-based-client-management.md)がサポートされている場合は、次の 2 つの方法のいずれかを使ってイントラネット上のクライアントをインストールできます。  

- クライアントをインストールするときに、たとえば手動インストールやクライアント プッシュを使うことで、Client.msi のプロパティ `CCMHOSTNAME=<internet FQDN of the internet-based management point>` を含めます。 この方法を使うときは、サイトにクライアントを直接割り当てます。 サイトの自動割り当てを使うことはできません。 [構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションをご覧ください。この構成方法の例があります。  

- イントラネットのクライアント管理用にクライアントをインストールしてから、インターネット ベースのクライアント管理ポイントをクライアントに割り当てます。 コントロール パネルの **[Configuration Manager]** ページ上にあるクライアントのプロパティを使うか、またはスクリプトを使って、管理ポイントを変更します。 この方法を使用するときに、自動クライアント割り当てを使用できます。 詳細については、「[クライアント インストール後のインターネット ベースのクライアント管理用のクライアントを構成するには](#BKMK_ConfigureIBCM_MP)」セクションをご覧ください。  

インターネット上のクライアントをインストールするには、以下のサポートされる方法の 1 つから選択します。  

- これらのクライアントが VPN でイントラネットに一時的に接続するためのメカニズムを提供します。 その後、適切なクライアント インストール方法を使ってクライアントをインストールします。  

- Configuration Manager に依存しないインストール方法を使います。 たとえば、リムーバブル メディアにクライアント インストールのソース ファイルをパッケージ化し、そのメディアをユーザーに送ります。 クライアント インストール ソース ファイルは、Configuration Manager サイト サーバーの `<installation path>\Client` フォルダーにあります。 クライアント フォルダーを手動でコピーするスクリプトをメディア上に含めます。 このフォルダーから、CCMSetup.exe および適切なすべての CCMSetup コマンド ライン プロパティを使用してクライアントをインストールします。  

> [!NOTE]  
> Configuration Manager では、インターネット ベースの管理ポイントまたはインターネット ベースのソフトウェア更新ポイントからクライアントを直接インストールすることはサポートしていません。

インターネット経由で管理されるクライアントは、インターネット ベースのサイト システムと通信する必要があります。 クライアントをインストールする前に、これらのクライアントが公開キー基盤 (PKI) 証明書も持っていることを確認します。 これらの証明書は Configuration Manager とは別にインストールします。 詳細については、「[PKI 証明書の要件](../../plan-design/network/pki-certificate-requirements.md)」を参照してください。  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>CCMSetup コマンドライン プロパティを指定してインターネット上のクライアントをインストールする  

1. [構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションの指示に従います。 次のオプションを常に含めます。  

    - CCMSetup のコマンド ライン パラメーター `/source:<local path of the copied Client folder>`  

    - CCMSetup のコマンド ライン パラメーター `/UsePKICert`  

    - Client.msi のプロパティ `CCMHOSTNAME=<FQDN of internet-based management point>`  

    - Client.msi のプロパティ `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - Client.msi のプロパティ `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > 複数のインターネット ベースの管理ポイントがサイトにある場合は、`CCMHOSTNAME` プロパティに対してどれを指定してもかまいません。 構成マネージャー クライアントが指定したインターネット ベースの管理ポイントに接続するときに、サイト内で使用できるインターネット ベースの管理ポイントの一覧が管理ポイントからクライアントに送信されます。 クライアントは一覧から 1 つをランダムに選びます。

2. クライアントで証明書失効リスト (CRL) を確認しないようにする場合は、CCMSetup コマンド ライン パラメーター `/NoCRLCheck` を指定します。  

3. インターネット ベースのフォールバック ステータス ポイントを使用する場合、Client.msi プロパティ `FSP=<internet FQDN of the internet-based fallback status point>` を指定します。  

4. インターネットのみのクライアント管理用にクライアントをインストールする場合、Client.msi プロパティ `CCMALWAYSINF=1` を指定します。  

5. その他の CCMSetup コマンドライン パラメーターを指定する必要があるかどうかを判断します。 たとえば、クライアントに複数の有効な PKI 証明書がある場合は、場合によって証明書選択条件を指定する必要があります。 使用可能なプロパティの一覧については、[クライアント インストールのパラメーターとプロパティ](about-client-installation-properties.md)に関するページをご覧ください。  

#### <a name="internet-based-example"></a>インターネット ベースの例

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

この例では、次の動作を持つクライアントがインストールされます。

- D ドライブ上のフォルダーにあるソース ファイルを使う。
- クライアント PKI 証明書を使う。
- 有効期限の最も長い証明書を選択する。
- インターネットのみのクライアント管理。
- SERVER1 という名前のインターネット ベースの管理ポイントを使うようにクライアントを割り当てる。
- contoso.com ドメインのインターネット ベースのフォールバック ステータス ポイントを割り当てる。
- ABC サイトにクライアントを割り当てる。  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> クライアント インストール後のインターネット ベースのクライアント管理用のクライアントを構成するには  

クライアントのインストール後にインターネットベースの管理ポイントを割り当てるには、次のいずれかの手順に従います。 1 つ目の手順では手動で構成します。クライアントが少数の場合に適しています。 クライアントの数が多い場合は、2 つ目の手順が適しています。  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Configuration Manager コントロール パネルからクライアントをインストールした後、インターネットベースのクライアント管理用のクライアントを構成する  

1. クライアントで **Configuration Manager** コントロール パネルを開きます。  

2. **[インターネット]** タブで、 **[インターネット FQDN]** としてインターネットベースの管理ポイントの完全修飾ドメイン名 (FQDN) を入力します。  

    > [!NOTE]  
    > **[インターネット]** タブは、クライアントにクライアント PKI 証明書がある場合にのみ使用できます。  

3. クライアントがプロキシ サーバーを使ってインターネットにアクセスする場合は、プロキシ サーバーの設定を入力します。  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>クライアントのインストール後に、スクリプトを使用して、インターネットベースのクライアント管理用のクライアントを構成する  

##### <a name="powershell"></a>PowerShell

1. PowerShell ISE や Visual Studio Code のような、PowerShell のインライン エディターを開きます。 メモ帳などのテキスト エディターを使うこともできます。

2. 次のコード行をコピーし、エディターに挿入します。 `'mp.contoso.com'` を、使用するインターネット ベースの管理ポイントのインターネット FQDN に置き換えます。

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > 最後の行は、新しいインターネット管理ポイントの値を確認するためだけにあります。
    >
    > 指定したインターネット ベースの管理ポイントを削除するには、引用符内のサーバーの FQDN 値を削除します。 この行は `$newInternetBasedManagementPointFQDN = ''` になります。

3. 拡張子 .ps1 を使ってファイルを保存します。  

4. クライアント コンピューター上で、管理者権限を使ってスクリプトを実行します。 次のいずれかの方法を使います。  

    - パッケージとプログラムを使用して、既存の Configuration Manager クライアントにファイルを展開する  

    - エクスプローラーでスクリプト ファイルをダブルクリックし、既存の構成マネージャー クライアントでファイルをローカルに実行する。  

変更を適用するために、クライアントの再起動が必要になることがあります。  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a> クライアント インストールのプロパティをプロビジョニングする

グループ ポリシーおよびソフトウェアの更新に基づいたクライアント インストール用に、クライアント インストールのプロパティをプロビジョニングします。 構成マネージャー クライアントのインストール プロパティを使ってコンピューターをプロビジョニングするには、Windows グループ ポリシーを使います。 これらのプロパティは、コンピューターのレジストリに格納されます。 クライアントはインストールするときに読み取ります。 この手順は、通常必要ありませんが、次のような一部のクライアント インストール シナリオで必要となる場合があります。  

- グループ ポリシー設定またはソフトウェア更新ベースのクライアント インストール方法を使っていて、 Active Directory スキーマを Configuration Manager 用に拡張していない場合。  

- 特定のコンピューターのクライアント インストール プロパティをオーバーライドする場合。  

> [!NOTE]  
> CCMSetup.exe コマンド ラインで何らかのインストール プロパティを指定した場合、コンピューターにプロビジョニングされたインストール プロパティは使われません。

Configuration Manager インストール メディア上には、`ConfigMgrInstallation.adm` という名前のグループ ポリシー管理テンプレートが用意されています。 このテンプレートを使って、インストール プロパティでクライアント コンピューターをプロビジョニングします。

> [!TIP]
> 既定では、`ConfigMgrInstallation.adm` では 255 文字を超える文字列はサポートされていません。 この構成は、複数のパラメーターや、長い値を持つパラメーターを追加する場合に影響する可能性があります (CCMCERTISSUERS など)。<!-- SCCMDocs#1648 -->
>
> この問題を回避するには、次の操作を行います。
>
> 1. メモ帳で `ConfigMgrInstallation.adm` を編集します。
> 2. プロパティ `VALUENAME SetupParameters` の `MAXLEN` 値をより大きな整数に変更します。 たとえば、`MAXLEN 511` となります。

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>グループ ポリシー オブジェクトを使用してクライアント インストール プロパティの構成と割り当てを行う  

1. Windows グループ ポリシー オブジェクト エディターなどのエディターを使って、新規または既存のグループ ポリシー オブジェクト (GPO) に、管理テンプレート ConfigMgrInstallation.adm をインポートします。 このファイルは、Configuration Manager インストール メディア上の `TOOLS\ConfigMgrADMTemplates` フォルダーにあります。  

2. インポートした設定 **[クライアント展開の設定を構成する]** のプロパティを開きます。  

3. **[有効]** を選択します。  

4. **[CCMSetup]** ボックスに、必要な CCMSetup コマンドライン プロパティを入力します。 CCMSetup コマンド ライン プロパティの詳細と使用例については、[クライアント インストールのパラメーターとプロパティ](about-client-installation-properties.md)に関するページをご覧ください。  

5. 構成マネージャー クライアントのインストール プロパティをプロビジョニングするコンピューターに、GPO を割り当てます。