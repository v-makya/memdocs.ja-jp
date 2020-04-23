---
title: Technical Preview 1606 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1606 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05e7bbe6373ed91de5a2bb8e99a8425e733274f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705570"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Configuration Manager の Technical Preview 1606 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1606 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。      このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    

**この Technical Preview の既知の問題:**  
*  Technical Preview 1604 から 1605 に更新してからバージョン 1606 に更新すると、更新が失敗し、次のようなエラーが **cmupdate.log** に記録されることがあります。

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    これが発生した場合には、 **[更新とサービス]** ノードで **[更新プログラムの確認]** をクリックしてから更新プログラムのインストールを**再試行**します。
    ***

**このバージョンでお試しいただける新機能を次に示します。**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a> デバイスを自動的にコレクションごとに分類
Microsoft Intune と Configuration Manager を使用している場合に、デバイス コレクションにデバイスを自動的に配置するために使用できるデバイス カテゴリを作成することができます。 ユーザーは Intune にデバイスを登録するときに、デバイス カテゴリの選択を求められます。 Configuration Manager コンソールから、デバイスのカテゴリをさらに変更できます。

**重要:** この機能は、Microsoft Intune の **2016 年 6 月**のリリースで機能します。 これらの手順を実行する前に、今回のリリースに更新していることを確認してください。

### <a name="try-it-out"></a>試してみましょう。

### <a name="create-a-set-of-device-categories"></a>デバイス カテゴリのセットの作成
1.  Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースで、 **[概要]** を展開してから **[デバイス コレクション]** をクリックします。
2.  **[ホーム]** タブの **[カテゴリ]** グループで、 **[デバイス カテゴリの管理]** をクリックします。
3.  **[デバイス カテゴリの管理]** ダイアログ ボックスでは、カテゴリの作成、編集、または削除ができます。 新しいカテゴリを作成してみましょう。

### <a name="associate-a-collection-with-a-device-category"></a>コレクションをデバイス カテゴリに関連付ける
コレクションをデバイス カテゴリと関連付けると、指定したカテゴリのすべてのデバイスがそのコレクションに追加されます。
1.  デバイス コレクションの **[プロパティ]** ダイアログをクリックして、 **[規則の追加]**  >  **[デバイス カテゴリの規則]** の順にクリックします。
2.  **[デバイス カテゴリのメンバーシップ規則の作成]** ダイアログ ボックスで、コレクション内のすべてのデバイスに適用されるカテゴリを選択します。
3.  **デバイス カテゴリのメンバーシップ規則の作成** ダイアログ ボックスと コレクションのプロパティ ダイアログ ボックスを閉じます。

### <a name="change-the-category-of-a-device"></a>デバイスのカテゴリを変更する
1.  Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースで、 **[概要]** を展開してから **[デバイス]** をクリックします。
2.  **[デバイス]** の一覧からデバイスを選択して、 **[ホーム]** タブの **[デバイス]** グループで **[カテゴリの変更]** をクリックします。
3.  **[デバイス カテゴリの編集]** ダイアログ ボックスで、このデバイスに適用するカテゴリを選択し、 **[OK]** をクリックします。

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a> 必要なアプリケーションとソフトウェア更新プログラムを展開するための適用猶予期間

場合によっては、必要なアプリケーション展開またはソフトウェア更新プログラムのインストールに、設定した期限よりも多くの時間をユーザーに与えることができます。 これは通常、コンピューターが長期間オフになっていて、多数のアプリケーションや更新プログラムの展開をインストールする必要がある場合に必要になります。
たとえば、エンド ユーザーが休暇から戻って来たばかりの場合、期限切れのアプリケーションの展開がインストールされるまで、長時間待たなければならない場合があります。
この問題を解決するため、Configuration Manager クライアント設定をコレクションに展開することで、適用猶予期間を定義できるようになりました。

### <a name="try-it-out"></a>試してみましょう。

猶予期間を設定するには、次の操作を実行します。

1.  クライアント設定の **[コンピューター エージェント]** ページで、新しいプロパティ **[展開期限後の実施の猶予期間 (時間)]** の値を **1** ～ **120** 時間で設定します。
2.  新しい必須アプリケーションの展開、または既存の展開のプロパティで、 **[スケジュール]** ページで **[ユーザー設定に従い、クライアント設定で定義された猶予期間が終了するまでこの展開の実施を延期する]** チェック ボックスをオンにします。
このチェック ボックスがオンになっていて、クライアント設定も展開するデバイスを対象としているすべての展開が、適用猶予期間を使用します。

適用猶予期間を構成し、チェック ボックスをオンにすると、アプリケーションのインストール期限になると、ユーザーがその猶予期間までに設定した最初の非ビジネス ウィンドウで、アプリケーションがインストールされます。 ただし、ユーザーはソフトウェア センターを開いて、いつでもアプリケーションをインストールすることもできます。 猶予期間が切れると、適用は期限切れの展開に対する通常の動作に戻ります。
ソフトウェア更新プログラムの展開ウィザード、自動展開規則の作成ウィザード、およびプロパティ ページに、同様のオプションが追加されています。

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a> デバイス ガードにより Configuration Manager を管理インストーラーとして使用

Device Guard は、ハードウェアとソフトウェアの機能を使用して、デバイスでの実行を許可する条件を厳密に制御する Windows 10 の機能です。

Device Guard の詳細な概要とそのしくみについては、[この Technet の記事](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview)をご覧ください。

このリリースでは、Configuration Manager は Device Guard および [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) と相互運用して、Configuration Manager で展開される実行可能ファイルや DLL ファイルが、管理されたインストーラーから提供されているものとして自動的に信頼されるようにすることができます。つまり、これらのファイルが対象のデバイス上で実行されることが許可され、その他のソフトウェアは他の AppLocker の規則によって明示的に実行が許可されない限り、実行することはできません。  

現時点では、この機能は Configuration Manager コンソールから構成することはできません。 ポリシーを構成するには、クライアントごとにレジストリ キーを構成し、クライアントで Windows サービスを構成する必要があります。
これが完了したら、AppLocker ポリシー ファイルを構成します。 ポリシー ファイルを構成したら、それを互換性のある任意のクライアント デバイスに展開できます。


すべての AppLocker ポリシーと同様に、管理インストーラー規則を含むポリシーは、次の 2 つのモードで実行できます。

- 監査モード: アプリケーションの実行は妨げられませんが、ブロックされたすべてのアプリケーションがログ ファイルに報告されます (これは今後の Configuration Manager のリリースでサポートされる予定です)。
- 適用を有効にする: アプリケーションが実行できなくなります。

Configuration Manager での Device Guard の詳しい使用方法は、[Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10)をご覧ください。

参考資料:

- [Device Guard の概要](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Device Guard certification and compliance](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance) (Device Guard の証明書とコンプライアンス)
- [Device Guard 展開ガイド](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a> オンプレミス モバイル デバイス管理のための複数のデバイス管理ポイント  
  Technical Preview 1606 では、オンプレミスのモバイル デバイス管理 (MDM) で、複数のデバイス管理ポイントが使用できるように登録済みのデバイスを自動的に構成する Windows 10 Anniversary Update の新機能をサポートしています。 この機能により、通常使用しているデバイスの管理ポイントが使用できない場合に、デバイスが別のデバイス管理ポイントにフォールバックすることができます。 この機能は、Windows 10 Anniversary Update がインストールされている PC でのみ機能します。  

### <a name="try-it-out"></a>試してみましょう。  

1.  階層内に複数のデバイス管理ポイントをインストールします。  

2.  Windows 10 Anniversary Update  デバイスをオンプレミスのモバイル デバイス管理に登録します。  

サイトを準備して、デバイスをオンプレミスのモバイル デバイス管理に登録する方法の詳細については、「[オンプレミス インフラストラクチャを使用してモバイル デバイスを管理する](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」をご覧ください。  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>インターネット上でクライアントを管理するためのクラウド プロキシ サービス

クラウド プロキシ サービスは、インターネット上で Configuration Manager クライアントを管理する簡単な方法を提供します。 Microsoft Azure にデプロイされ、Azure サブスクリプションを必要とするサービスは、クラウド プロキシ コネクタ ポイントと呼ばれる新しい役割を使用して、オンプレミスの Configuration Manager インフラストラクチャに接続します。 完全にデプロイされ、構成されると、クライアントは内部のプライベート ネットワークに接続しているかどうか、またはインターネット上にあるかどうかに関係なく、オンプレミスの Configuration Manager サイト システムの役割にアクセスできるようになります。

Configuration Manager コンソールを使用して、Azure にサービスをデプロイし、クラウド プロキシ コネクタ ポイントの役割を追加し、クラウド プロキシ トラフィックを許可するサイト システムの役割を構成します。 クラウド プロキシ サービスは現在、管理ポイント、配布ポイント、およびソフトウェアの更新ポイントの役割のみをサポートしています。

コンピューターを認証し、異なる層のサービス間の通信を暗号化するには、クライアント証明書および Secure Socket Layer (SSL) 証明書が必要です。 クライアント コンピューターは通常、グループ ポリシーの適用を介してクライアント証明書を受け取ります。 クライアントと役割をホストしているサイト システム サーバー間のトラフィックを暗号化するには、CA からカスタム SSL 証明書を作成する必要があります。 これらの 2 種類の証明書に加え、クラウド プロキシ サービスのデプロイを Configuration Manager に許可する管理証明書を Azure で設定する必要もあります。  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>TP 1606 でのクラウド プロキシ サービスの要件
- クライアント コンピューターとクラウド プロキシ コネクタ ポイントを実行するサイト システム サーバー
- クライアント コンピューターからの通信を暗号化し、クラウド プロキシ サービスの ID を認証するために使用される内部 CA からのカスタムの SSL 証明書
- クラウド サービスの Azure サブスクリプション
- Azure での Configuration Manager の認証に使用される Azure 管理証明書

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>TP 1606 でのクラウド プロキシ サービスの制限事項

- 管理ポイント、配布ポイント、およびソフトウェアの更新ポイントの役割のみをサポートします。
- ユーザー ポリシーはサポートされていません。
- Configuration Manager で[オンプレミス モバイル デバイス管理 (MDM)](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) とともに使用することはできません。
- Azure のパブリック クラウド プラットフォームでのみサポートされます。


### <a name="try-it-out"></a>試してみましょう。

クラウド プロキシ サービスをデプロイするためのプロセスには、次の手順が含まれます。

1. クラウド プロキシ サービス用のカスタム SSL 証明書を作成して発行します。
1. クライアント証明書のルートをエクスポートします。
2. 管理証明書を Azure にアップロードします。
3. Configuration Manager コンソールで、クラウド プロキシ サービスを設定します。
4. クライアント証明書の認証を使用するプライマリ サイトを構成します。
5. クラウド プロキシ コネクタ ポイントをサイトに追加します。
6. クラウド プロキシ トラフィックを受け入れるサイト システムの役割を構成します。

次のセクションでは、これらの手順を完了するための詳細を提供します。

#### <a name="create-a-custom-ssl-certificate"></a>カスタム SSL 証明書を作成する

クラウド ベースの配布ポイントで行うのと同じ方法で、クラウド プロキシ サービスのカスタム SSL 証明書を作成できます。 次の操作以外は、「[クラウドベースの配布ポイント用のサービス証明書の展開](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)」の指示に従います。

* 新しい証明書テンプレートを設定する際に、Configuration Manager サーバー用に設定したセキュリティ グループに **読み取り**と**登録**のアクセス許可を与えます。

#### <a name="export-the-client-certificates-root"></a>クライアント証明書のルートをエクスポートする

ネットワークで使用されているクライアント証明書のルートをエクスポートする最も簡単な方法は、クライアント証明書を含むドメインに参加しているいずれかのコンピューター上でクライアント証明書を開いてコピーすることです。

>[!NOTE]
>クライアント証明書は、クラウド プロキシ サービスで管理するコンピューター上およびクラウド プロキシ コネクタ ポイントをホストしているサイト システム サーバー上で必要です。 これらの任意のコンピューターにクライアント証明書を追加する必要がある場合は、「[Windows コンピューター用のクライアント証明書の展開](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)」をご覧ください。

1. [実行] ウィンドウで、「**mmc**」を入力して Return キーを押します。
2. 管理コンソールの ファイル メニューで **スナップインの追加と削除** をクリックします。
3. スナップインの追加と削除 ダイアログ ボックスで **証明書** をクリックして、**追加**、**コンピューター アカウント**、**次へ**、**ローカル コンピューター** の順にクリックし、**完了** をクリックします。 **[OK]** をクリックしてダイアログ ボックスを閉じます。
4. **[証明書] > [個人用] > [証明書]** に移動します。
5. コンピューターでクライアント認証用の証明書をダブルクリックして、[証明パス] タブをクリックし、ルート証明機関 (パスの先頭) をダブルクリックします。
6.  詳細 タブをクリックし、**ファイルにコピー** をクリックします。
7. 既定の証明書形式を使用して証明書のエクスポート ウィザードを完了します。 作成したルート証明書の名前と場所をメモします。 これは後の手順でクラウド プロキシ サービスを構成する際に必要になります。

#### <a name="upload-the-management-certificate-to-azure"></a>管理証明書を Azure にアップロードする

Azure 管理証明書は、Configuration Manager が Azure API にアクセスして、クラウド プロキシ サービスを構成するために必要です。 管理証明書をアップロードする方法の詳細と手順については、Azure のドキュメントの次の記事を参照してください。
- [Azure Cloud Services の証明書の概要](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Azure Management API 管理証明書のアップロード](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

管理証明書に関連付けられているサブスクリプション ID を必ずコピーしてください。 これは Configuration Manager コンソールで、クラウド プロキシ サービスを設定する際に必要になります。

#### <a name="set-up-cloud-proxy-service"></a>クラウド プロキシ サービスの設定

1. Configuration Manager コンソールで、 **[管理] > [Cloud Services] > [クラウド プロキシ サービス]** に移動します。
2. **[クラウド プロキシ サービスの作成]** をクリックします。
3. クラウド プロキシ サービスの作成ウィザードで、(Azure 管理ポータルからコピーした) Azure サブスクリプション ID を入力し、[参照] をクリックして Azure の管理証明書としてアップロードするために使用する証明書ファイルを選択します。 **[次へ]** をクリックします。 コンソールを Azure に接続するためにしばらく待機します。
4. ウィザードで追加の詳細を入力します。
    - カスタム SSL 証明書からエクスポートした秘密キー (.pfx ファイル) を指定します。
    - クライアント証明書からエクスポートしたルート証明書を指定します。
    - 新しい証明書テンプレートを作成するときに使用したのと同じサービス名の FQDN を指定します。
    - **[クライアント証明書の失効状態を検証する]** の横のボックスをオフにします (CRL 情報をパブリックに発行している場合を除く)。
    - 完了したら、 **[次へ]** をクリックします。
5. 設定を確認して、 **[次へ]** をクリックします。 Configuration Manager がサービスの設定を開始します。 ウィザードが完了したら、 **[閉じる]** をクリックします。ただし、Azure で完全にサービスをプロビジョニングするまで 5 ～ 15 分間かかります。 新しく設定されたクラウド プロキシ サービスの **[状態]** 列を確認して、サービスの準備が完了するタイミングを判断します。

#### <a name="configure-primary-site-for-client-certification-authentication"></a>クライアント証明書の認証用にプライマリ サイトを構成する

1. Configuration Manager コンソールで、 **[管理]、[サイトの構成]、[サイト]** の順に移動します。
2. クラウド プロキシ サービスを使用して管理するクライアントのプライマリ サイトを選択して **[プロパティ]** をクリックします。
3. プライマリ サイトのプロパティ シートの クライアント コンピューターの通信方法 タブで、**使用可能な場合は PKI クライアント証明書 (クライアント認証機能) を使用する** の横のチェック ボックスをオンにします。
4. **[サイト システムの証明書失効リスト (CRL) をチェックする]** の横のチェック ボックスがオフになっていることを確認します。 このオプションは、CRL をパブリックに公開した場合にのみ必要になります。
5. **[OK]** をクリックします。

#### <a name="add-the-cloud-proxy-connector-point"></a>クラウド プロキシ コネクタ ポイントを追加する

クラウド プロキシ コネクタ ポイントは、クラウド プロキシ サービスと通信するための新しいサイト システムの役割です。 クラウド プロキシ コネクタ ポイントを追加するには、「[Configuration Manager のサイト システム役割の追加](../../core/servers/deploy/configure/add-site-system-roles.md)」の手順に従います。

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>クラウドプロキシ トラフィックの役割を構成する

クラウド プロキシ サービスを設定する最後のステップは、クラウド プロキシ トラフィックを受け入れるためのサイト システムの役割を構成することです。 Tech Preview 1606 の場合、管理ポイント、配布ポイント、およびソフトウェアの更新ポイントの役割のみがクラウド プロキシ サービスでサポートされています。 各役割を個別に構成する必要があります。

1. Configuration Manager コンソールで、 **[管理] > [サイトの構成] > [サーバーとサイト システムの役割]** の順に移動します。
2. クラウド プロキシ トラフィックに構成したい役割のサイト システム サーバーをクリックします。
3. 役割をクリックして、 **[プロパティ]** をクリックします。
4. 役割のプロパティ シートの クライアント接続 の下で、**HTTPS** を選択し、**Configuration Manager のクラウド プロキシ トラフィックを許可する** の横のチェック ボックスをオンにして **OK** をクリックします。 残りの役割にこれらの手順を繰り返します。

#### <a name="check-status-on-a-client-on-the-internet"></a>インターネットでクライアントの状態を確認する

サービスと役割をすべて構成すると、内部クライアントは次回の場所の要求でクラウド プロキシ サービスの場所を取得します。 更新された場所の情報を取得したクライアントは、インターネット上で Configuration Manager と通信できるようになります。 場所の要求のポーリング サイクルは 24 時間ごとです。 通常にスケジュール設定された場所の要求を待機したくない場合は、コンピューターで SMS Agent Host サービス (ccmexec.exe) を再起動することによって、要求を強制できます。

クライアントがクラウド プロキシ サービスの新しい場所の情報を取得したら、不要になった内部のプライベート ネットワーク上にあってインターネットにアクセスを持つクライアントの状態を確認してください。 **[管理] > [Cloud Services] > [クラウド プロキシ サービス]** の順に移動して、リスト ウィンドウでサービスを選択し、詳細ペインでトラフィックの情報を表示することで、クラウド プロキシ サービスのトラフィックを監視することもできます。   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>Configuration Manager で Office 365 のクライアント エージェントを管理  

Technical Preview 1606 を起動すると、グループ ポリシーの代わりに Configuration Manager クライアント エージェント設定を使用して、Office 365 クライアントが Configuration Manager から更新プログラムを受信できるようにすることができます。 この設定を構成し、Office 365 の更新プログラムを展開すると、Configuration Manager クライアント エージェントは、Office 365 のクライアント エージェントと通信して、配布ポイントから Office 365 の更新プログラムをダウンロードしてインストールします。 Configuration Manager は、クライアント エージェント設定のインベントリも取得します。

詳細については、「[System Center Configuration Manager での Office 365 ProPlus の更新プログラムの管理](https://technet.microsoft.com/library/mt741983.aspx)」をご覧ください。

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Configuration Manager クライアント設定で Office 365 クライアント エージェントを管理するように設定する
1.  Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クライアント設定]** の順にクリックします。
2. クライアント エージェントを有効にする適切なデバイスの設定を開きます。 既定とカスタムのクライアント設定の詳細については、[クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)に関するページをご覧ください。
3. **[ソフトウェアの更新]** を選択し、 **[Office 365 クライアント エージェントの管理を有効にする]** の設定に **[はい]** を設定します。  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter タスク シーケンス変数は使用されなくなった
OSDPreserveDriveLetter タスク シーケンス変数は、タスク シーケンスが対象コンピューターにそのイメージを適用するときに、オペレーティング システム イメージ WIM ファイルにキャプチャされたドライブ文字を使用するかどうかを判断します。
- Technical Preview 1606 では、このタスク シーケンス変数は非推奨とされます。

既定で、オペレーティング システムの展開中に、Windows セットアップが使用する最適なドライブ文字を決定するようになりました (通常は C:)。 別のドライブを使用するように指定する場合は、オペレーティング システムの適用タスク シーケンスのステップで場所を変更できます。 **[このオペレーティング システムの適用先を選択してください。]** 設定に移動し、 **[特定の論理ドライブ文字]** を選択し、使用するドライブを選択します。 設定先のコンピューター上に、選択した文字が割り当てられたドライブが作成されているはずです。 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>更新プログラムとサービス ノードの変更
Technical Preview 1606 では、Configuration Manager コンソールの [更新とサービス] に適用されるいくつかの変更が導入されています。
- **ノード名の変更:**

    **[監視]** ワークスペースで、 **[サイト サービスの状態]** ノードの名前が **[更新とサービスの状態]** に変更されました。
- **追加のインストール状態:**

    サイトの更新プログラムのインストールの状態を表示すると、次の操作の詳細がコンソールで個別に表示されるようになりました。
    - **ダウンロード** (これは、サービス接続ポイントのサイト システムの役割がインストールされている最上位層のサイトにのみ適用されます)
    - **Replication**
    - **前提条件の確認**
    - **インストール**

  さらに、各手順のより詳細な情報 (詳細な情報を表示できるログ ファイルなど) が追加されています。  
-   **前提条件のエラーを再試行する新しいオプション:**

    **[管理]** ワークスペースと **[監視]** ワークスペースの両方で、 **[更新とサービス]** ノードのリボンに **[前提条件チェックの警告を無視する]** という名前の新しいボタンが含まれています。

    [前提条件チェックの警告を無視する] オプションを使用せずに更新プログラムを (更新ウィザードから) インストールし、その更新プログラムのインストールが**前提条件の警告**状態になって停止した場合は、後でリボンから **[前提条件チェックの警告を無視する]** を選択すれば、その更新プログラムのインストールが自動的に継続され、前提条件チェックの警告が無視されます。  



- **より見やすくなった更新プログラムのビュー:**

    **[更新とサービス]** ノードを表示すると、最近インストールされた更新プログラムと、インストール可能な新しい更新プログラムのみが表示されるようになりました。 以前にインストールされた更新プログラムを表示するには、リボンに表示される新しい **[履歴]** ボタンをクリックします。  

-   **実稼働前の名前変更されたオプション:**

    更新とサービス ノードで、**クライアント オプション** という名前だったボタンが **実稼働前クライアントの昇格** に変更されました。
