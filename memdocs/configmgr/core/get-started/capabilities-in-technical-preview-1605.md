---
title: Technical Preview 1605 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1605 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: d52725e0127f7129a3962cd3ef178d2540bb785a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905750"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Configuration Manager の Technical Preview 1605 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1605 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。      このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。  

 **この Technical Preview の既知の問題:**  

- Technical Preview 1605 をインストールした後、管理ポイントのプロパティを更新すると、コンソールを強制的に閉じまるコンソール エラーが発生する場合があります。  これが発生した場合、管理ポイントをアンインストールし、目的の設定を使用して管理ポイントを再インストールできます。 または、Technical Preview 1605 をインストールする前に、管理ポイントを変更することができます。  

- ビジネス向け Windows ストア機能を Technical Preview 1604 で使用していて、Technical Preview 1605 にアップグレードすると、オンボード データを表示できなくなります。 他の機能はすべて引き続き機能します。 Technical Preview 1604 でオンボードした場合、Technical Preview 1605 をインストールした後もオンボードされたままで、追加のアクションを行う必要はありません。  

  **このバージョンでお試しいただける新機能を次に示します。**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a> Windows 10 デバイス向けのアプリごとの VPN  
 Configuration Manager と Intune を使用して管理されている Windows 10 デバイスの場合、Configuration Manager 管理コンソールで構成した VPN 接続を自動的に開くアプリの一覧を追加できます。 これらのアプリへの VPN トラフィックを制限するか、VPN 接続を介してすべてのトラフィックを許可し続けることができます。  

 **要件**:  

-   Configuration Manager と Intune  

-   少なくとも 1 つのデバイスに展開されている Windows 10 の VPN プロファイル  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a> ソフトウェア更新プログラムのインストール タスク シーケンスの向上  
 ソフトウェア更新プログラムのインストール タスク シーケンスに次の改良が加えられています。  

-   新しいタスク シーケンス変数 SMSTSSoftwareUpdateScanTimeout が使用可能になり、タスク シーケンスの「ソフトウェア更新プログラム インストール」ステップの間に、ソフトウェア更新プログラムのスキャンのタイムアウトを制御できます。 既定値は 30 分です。  

-   ログ記録が改善されています。 smsts.log ログ ファイルには、ソフトウェア更新プログラムのインストール プロセス中に問題をトラブルシューティングするのに役立つその他のログ ファイルを参照する新しいログ エントリが格納されます。  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a> ConfigMgr クライアントのキャプチャの準備タスク シーケンス ステップの向上  
 ConfigMgr クライアントの準備手順で、キー情報だけではなく、Configuration Manager クライアントが完全に削除されるようになりました。 タスク シーケンスでキャプチャしたオペレーティング システム イメージを展開すると、毎回新しい Configuration Manager クライアントがインストールされます。  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a> 必要なアプリケーション展開の猶予期間  
 場合によっては、必要なアプリケーション展開のインストールに、設定した期限よりも多くの時間をユーザーに与えることができます。 たとえば、エンド ユーザーが休暇から戻って来たばかりの場合、期限切れのアプリケーションの展開がインストールされるまで、長時間待たなければならない場合があります。 ただし、必要なときにいつでもアプリケーションをすぐにインストールできます。  

 この問題を解決するため、Configuration Manager クライアント設定をコレクションに展開することで、**猶予期間**を定義できるようになりました。  

 猶予期間を設定するには、次の操作を実行します。  

1. クライアント設定の **[コンピューター エージェント]** ページで、新しいプロパティ **[展開期限後の実施の猶予期間 (時間)]** の値を **1** ～ **120** 時間で設定します。  

2. 新しいアプリケーションの展開、または既存の展開のプロパティで、 **[スケジュール]** ページで **[ユーザー設定に従い、クライアント設定で定義された猶予期間が終了するまでこの展開の実施を延期する]** チェック ボックスをオンにします。  

    このチェック ボックスがオンになっていて、クライアント設定も展開するデバイスを対象としているすべての展開が、猶予期間を使用します。  

   このリリースでは、構成する猶予期間はクライアント デバイスでは使用されません。 猶予期間を構成し、チェック ボックスをオンにすると、期限後にユーザーが構成した最初の非ビジネス ウィンドウで、アプリケーションがインストールされます。  

   ソフトウェア更新プログラムの展開ウィザード、自動展開規則の作成ウィザード、およびプロパティ ページに、同様のオプションが追加されています。 ただし、現在、これらはこの Technical Preview には実装されていません。  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a> リモート デバイスの操作の新しいエクスペリエンス  
 Configuration Manager コンソールからリモート デバイスの操作を実行するため、エクスペリエンスが改善されました。  
**[削除/ワイプ]** 、 **[パスコードのリセット]** 、 **[リモート ロック]** 、および **[アクティブ化ロックのバイパス]** などの一般的なアクションは、 **[資産とコンプライアンス]** ワークスペースからアクセスする **[リモート デバイスの操作]** メニューに移動しました。  

 ![新しいリモート デバイスの操作のスクリーンショット](media/New-Remote-Device-Actions.png)  

 これらの各操作の状態は次の場所で確認できます。  

- **[デバイス]** ノードからデバイスを選択する場合は、詳細ウィンドウ  

- デバイスの **[プロパティ]** ページ  

- **[デバイス]** ノードのメイン ページ (既定ではすべての列が表示されない場合があります)  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a> ビジネス向け Windows ストアのアプリ  
 [ビジネス向け Windows ストア](https://www.microsoft.com/business-store)は、組織向けのアプリを検索して、個別に、または一括で購入できる場所です。 ストアを Configuration Manager に接続すると、一括購入したアプリを Configuration Manager コンソールから管理できます。例を挙げます。  

- 購入したアプリの一覧を Configuration Manager に同期させることができます。  

- 同期されたアプリは Configuration Manager コンソールに表示され、他のすべてのアプリと同様に展開できます。  

- Configuration Manager は 24 時間ごとにストアからアプリのライセンス情報をダウンロードし、Configuration Manager コンソールで、これを確認することができます。  

  Technical Preview の 1604 リリースでは、Configuration Manager コンソールでビジネス向け Windows ストアからアプリの同期と表示ができました。 このリリースでは、同期されたストア アプリから Configuration Manager アプリケーションを作成して展開する機能が追加されています。  

### <a name="set-up-windows-store-for-business-synchronization"></a>ビジネス向け Windows ストアの同期の設定  

1.  Azure Active Directory で、"Web アプリケーションや Web API" の管理ツールとして Configuration Manager を登録します。 後で必要なクライアント ID が表示されます。  

    1.  [https://manage.windowsazure.com](https://manage.windowsazure.com) の Active Directory ノードで、Azure Active Directory を選択し、 **[アプリケーション]**  >  **[追加]** をクリックします。  

    2.  **[組織で開発中のアプリケーションを追加]** をクリックします。  

    3.  アプリケーションの名前を入力し、 **[Web アプリケーション]** または **[Web API]** 、あるいはその両方を選択し、**次へ進む**矢印をクリックします。  

    4.  **[サインオン URL]** と **[アプリケーション ID/URI]** の両方に同じ URL を入力します。 URL はあらゆるものを使用でき、実際のアドレスに解決する必要はありません。 たとえば、**https://&lt;yourdomain>/sccm** を入力できます。  

    5.  ウィザードを完了します。  

2.  Azure Active Directory で、登録済み管理ツールのクライアント キーを作成します。  

    1.  作成したアプリケーションを強調表示し、 **[構成]** をクリックします。  

    2.  **[キー]** で、リストから期間を選択して、 **[保存]** をクリックします。 これにより、新しいクライアント キーが作成されます。 ビジネス向け Windows ストアを Configuration Manager に正常にオンボードするまで、このページから移動しないでください。  

3.  ビジネス向け Windows ストアで、ストア管理ツールとして Configuration Manager を構成します。  

    1.  [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) を開き、求められたらサインインします。  

    2.  要求された場合は、使用条件に同意します。  

    3.  **[管理ツール]** で、 **[Add a management tool]** (管理ツールを追加) をクリックします。  

    4.  **[Search for the tool by name]** (名前でツールを検索) で、先ほど AAD で作成したアプリケーションの名前を入力して、 **[追加]** クリックします。  

    5.  インポートしたアプリケーションの横にある **[アクティブ化]** をクリックします。  

    6.  オフラインでライセンスされるアプリケーションを購入する場合、**オフラインでライセンスされたアプリの表示**ウィザードで、 **[はい]** をクリックします。  

4.  ビジネス向け Windows ストアから少なくとも 1 つのアプリを購入します。  

5.  Configuration Manager コンソールの**管理**ワークスペースで、 **[Cloud Services]** を展開して、 **[ビジネス向け Windows ストア]** をクリックします。  

6.  **[ホーム]** タブの **[作成]** グループで、 **[ビジネス向け Windows ストア アカウントの追加]** をクリックします。  

7.  Azure Active Directory からテナント ID、クライアント ID、クライアント キーを追加し、ウィザードを完了します。  

8.  完了した時点で、Configuration Manager コンソールの **[ビジネス向け Windows ストア]** で構成されたアカウントが表示されます。  

### <a name="try-it-out"></a>試してみましょう。  
 次のタスクを完了し、Microsoft Connect サイトの「[Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)」 (Configuration Manager フィードバック プログラム) ページのフィードバック フォームを使用して、どのように動作したかをお知らせください。  

 ビジネス向け Windows ストアのオフライン ライセンス付きアプリから Configuration Manager アプリケーションを作成して展開します。  

1. Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、 **[ストア アプリのライセンス情報]** をクリックします。  

2. 展開するアプリを選び、 **[ホーム]** タブの **[作成]** グループで、 **[アプリケーションの作成]** をクリックします。  

   ビジネス向け Windows ストアのアプリを含む Configuration Manager アプリケーションが作成されます。 他の Configuration Manager のアプリケーションと同様に、このアプリケーションを展開して監視できます。  

> [!IMPORTANT]  
>  オフライン ライセンス付きアプリから単一の展開の種類で Configuration Manager アプリケーションを作成すると、これを MDM 管理されたデバイスに展開して、Configuration Manager クライアントで管理することもできます。 複数の展開の種類でアプリを展開しようとすると、インストールは失敗します。  
>   
>  現在、Configuration Manager でオフライン ライセンス付きアプリを展開することはできません。  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a> ボリューム購入アプリの全般的な向上  

-   このリリースでは、ビジネス向け Windows ストアおよび iOS App Store のボリューム購入アプリが同じビューの **[ストア アプリのライセンス情報]** に統合されています。  

-   iOS のボリューム購入アプリの場合、アプリケーションの作成ウィザードの **iOS アプリケーション パッケージ ブラウザー** ダイアログ ボックスから Apple Volume Purchase Program タブが削除されています。 iOS のボリューム購入アプリを作成するには、次の手順を使用します。  

    1.  1.  Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、 **[ストア アプリのライセンス情報]** をクリックします。  

    2.  2.  展開するアプリを選び、 **[ホーム]** タブの **[作成]** グループで、 **[アプリケーションの作成]** をクリックします。  

-   ボリューム購入アプリの Apple VPP トークンの取得とアップロードに使用する Configuration Manager コンソール内の場所が変更されました。 これは、 **[Cloud Services]**  >  **[Apple Volume Purchase Program のトークン]** ノードの下の **[管理者]** ワークスペースで行えます。  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a> エンタープライズ データ保護 (EDP)  
 エンタープライズ データ保護 (EDP) ポリシー (保護されているアプリ、EDP 保護レベル、およびネットワーク上の企業データを検索する方法を選択できるようにするなど) を展開するのに便利な構成項目を作成することができます。 EDP の詳細については、次のトピックを参照してください。  

- [Windows 情報保護 (WIP) を使用したエンタープライズ データの保護](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Configuration Manager を使用した Windows 情報保護 (WIP) ポリシーの作成と展開](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a> エンド ユーザーはポータル サイトからアプリをインストールできる  
 オンプレミスの MDM は、Configuration Manager バージョン 1511 で導入されました。 以前のバージョンでは、オンプレミスの MDM で管理されているデバイスへの**必須**インストールの展開目的で、MDM で管理された Windows 10 デバイスにアプリケーションを展開することができました。  

 このリリースでは、オンプレミスの MDM で管理された Windows 10 コンピューターのユーザーにアプリを**使用可能にする**目的で展開できるようになり、ユーザーはこれらのアプリをポータル サイトから自身でインストールできるようになりました。
この Technical Preview では、会社のポータルを 15 分以上開いたままにすると、エンド ユーザーにエラー メッセージが表示されます。 この問題に対処するには、会社のポータルを再起動します。  

### <a name="before-you-start"></a>開始する前に  

#### <a name="server-prerequisites"></a>サーバーの前提条件  

-   .NET 4.5 以降 (再起動が必要)  

-   設定スクリプト用の PowerShell 3.0 (再起動が必要)  

#### <a name="client-prerequisites"></a>クライアントに関する前提条件  

-   Windows 10 Desktop 1511 (OS ビルド番号 10586.218) 以降  

#### <a name="general-prerequisites"></a>一般的な前提条件  

-   [オンプレミス MDM の準備手順](../../mdm/plan-design/plan-on-premises-mdm.md)と[デバイスの登録](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)が完了していることを確認します。  

-   会社のポータルを使用した場合の最適なアプリケーションのインストール エクスペリエンスのため、Configuration Manager に Microsoft Intune へのアクティブな接続があることを確認します。  

-   一括登録オプションを選択した場合は、このシナリオを実行する前に登録したデバイスにユーザーとデバイスのアフィニティを構成します。  

### <a name="configuration-steps"></a>構成手順  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>アプリケーション カタログの役割をインストールし、モバイル デバイス管理のサポートを有効にします。  

1.  アプリケーション カタログ Web サービスと Web サイトのロールを追加します。  

    1.  **[HTTPS モード]** と **[モバイル デバイスでこのアプリケーション カタログ Web サービス ポイントの使用を許可する]** オプションを選びます。  

    2.  この Technical Preview の制限事項:  

        -   モバイル デバイスの接続を許可するオプションを選択する前に、既存のアプリケーション カタログの役割をアンインストールする必要があります。  

        -   アプリケーション カタログの役割が 1 セットしかないことを確認し、その役割が登録ポイントと登録プロキシ ポイントの役割と同じサイト システムに併置されていることを確認します。  

2.  次のコンポーネントが Configuration Manager コンソールの [コンポーネント ステータス] ノードから動作可能であることを確認します。  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>［境界の構成］  
 イントラネット専用の配布ポイントの必要な境界を構成します。  

> [!NOTE]  
>  現時点では、モバイル デバイス管理には IPv4 範囲の境界のみがサポートされています。  

### <a name="deploy-the-company-portal-application-and-configuration"></a>会社のポータル アプリケーションと構成を展開する  

1. Technical Preview に含まれている構成スクリプトを使用して、会社のポータルの展開と構成を準備します。  

   1. 管理者特権の PowerShell コマンド ウィンドウを開きます。  

   2. **set-executionPolicy RemoteSigned** を実行します。  

   3. フォルダー **&lt;SCCM のインストール ディレクトリ\>\cd.latest\SMSSETUP\TOOLS\MDM** から **.\ConfigurationScript.ps1** を実行します。  

      構成スクリプトは、以下を行います。  

   4. 同じフォルダー内の**CompanyPortalOnPremisesMDM.appx** を使用して、Windows アプリ パッケージの展開の種類を持つ Configuration Manager アプリケーションを作成する  

   5. 会社のポータルを構成する構成項目と構成基準を作成する  

   6. 構成基準とアプリケーションの両方を展開し、すべての配布ポイントにアプリケーションを追加する  

   > [!NOTE]
   >  アプリケーション カタログの役割が、プライマリ サイトと併置されていない場合は、次の操作を実行します。  
   > 
   > - **[資産とコンプライアンス]** ワークスペースで、構成項目 **OnPremMDM Portal Configuration CI - server urls** を検索します。  
   >   -   **[コンプライアンス規則]** の値をアプリケーション カタログの役割が配置されているサイト システムの完全修飾ドメイン名に変更します。  

2. 会社のポータル アプリケーションとその構成がどちらも展開されたら、Configuration Manager コンソールの **[展開]** セクションを使用して、アプリケーションと構成基準が特定のデバイスに対応していることを確認します。 デバイスの スタート メニューに、会社のポータルが **会社のポータル (Technical Preview)** として表示されます。  

### <a name="try-it-out"></a>試してみましょう。  
 次のタスクを完了し、Microsoft Connect サイトの「[Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)」 (Configuration Manager フィードバック プログラム) ページのフィードバック フォームを使用して、どのように動作したかをお知らせください。  

1.  サポートされている展開の種類を持つ複数のアプリケーションを、**使用可能にする**目的でユーザー コレクションに展開します。 この Technical Preview では、管理者の承認を必要とするアプリケーションはサポートされておらず、会社のポータルにも表示されません。  

2.  ユーザーはポータル サイトからアプリを参照してインストールできます。  

     会社のポータルを開くと、 **[Configuration Manager]** という認証ダイアログ ボックスが表示されます。ユーザーの Active Directory の資格情報を (user@domain またはドメイン\ユーザーのいずれかの形式で) 指定してログインします。  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a> ソフトウェア センターの更新プログラムおよびオペレーティング システムの新しいタブ  
 このリリースでは、ソフトウェア センター アプリケーションのレイアウトを改善するため、次の変更が加えられています。  

-   **[アプリケーション]** タブは、 **[更新]** 、「**オペレーティング システム**」 (どちらも以前は 「**フィルター**」 一覧にありました)、および **[アプリケーション]** の 3 つの別々のタブに分割されています。  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a> サーバー グループの提供  
 Configuration Manager の Technical Preview バージョン 1511 には、コレクション内のすべてのデバイスがサーバー グループを構成するコレクションを作成する機能が含まれていました。 そして、サーバー グループにソフトウェアの更新プログラムを展開するときに使用するサーバー グループ設定を構成する、特定の時間に更新されるコンピューターの割合を制御する、および展開前および展開後の PowerShell スクリプトを構成してカスタム アクションを実行することができました。  

 Configuration Manager の Technical Preview バージョン 1605 では、サーバー グループ内のコンピューターを定義した順番で更新できる機能と、サーバー グループ内のコンピューターの状態を表示するため強化された監視が追加されています。また、クライアントがソフトウェア更新プログラムのインストールに失敗し、他のクライアントのソフトウェア更新プログラムのインストールを妨げている場合に便利な、展開ロックを解除する機能も提供されています。  

### <a name="try-it-out"></a>試してみましょう。  
 次のタスクを完了し、Microsoft Connect サイトの「[Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)」 (Configuration Manager フィードバック プログラム) ページのフィードバック フォームを使用して、どのように動作したかをお知らせください。  

-   サーバー グループを表すコレクションを作成できます。 このテストでは、このコレクションに 2 台のコンピューターを含めるようにメンバーシップ収集規則を構成できます。   

-   サーバー グループ内のコンピューターが、コレクションのサーバー グループの設定に基づいて、特定の順序でソフトウェア更新プログラムをインストールすることを指定できます。 手順内のサンプル スクリプトを使用して、展開前スクリプトと展開後スクリプトを指定します。  

-   ソフトウェア更新プログラムをこのコレクションに展開できます。 C:\temp で (サンプル スクリプトから作成した) start.txt ファイルと end.txt ファイルを調査して、サーバー グループ内のコンピューター上の展開の開始時刻と終了時刻を確認します。 詳細については、UpdatesDeployment.log ファイルを参照してください。  

#### <a name="to-create-a-collection-for-a-server-group"></a>サーバー グループのコレクションを作成するには  

1.  サーバー グループ内のコンピューターを含む[デバイス コレクションを作成](../clients/manage/collections/create-collections.md)します。  

2.  **[資産とコンプライアンス]** ワークスペースで **[デバイス コレクション]** をクリックし、サーバー グループ内のコンピューターを含むコレクションを右クリックして、 **[プロパティ]** をクリックします。  

3.  **[全般]** タブで **[すべてのデバイスが同じサーバー グループに属す]** を選択し、 **[設定]** をクリックします。  

4.  **[サーバー グループ設定]** ページで、次のいずれかの設定を指定します。  

    -   **同時更新を許可するコンピューターの割合**: 任意の時点で特定の割合のクライアントのみを更新するように指定します。 たとえば、コレクションに 10 のクライアントがあり、クライアントの 30% を同時に更新するようにコレクションが構成されている場合は、任意の時点で 3 つのクライアントだけがソフトウェア更新プログラムをインストールします。  

    -   **同時更新を許可するコンピューターの数**: 任意の時点で特定の数のクライアントのみを更新するように指定します。  

    -   **メンテナンス シーケンスを指定する**: コレクション内のクライアントが、構成した順番で 1 つずつ更新されるように指定します。 クライアントは、一覧で前にあるクライアントがソフトウェア更新プログラムのインストールを完了しないと、ソフトウェア更新プログラムをインストールできません。  

5.  展開前 (ノードのドレイン) スクリプトまたは展開後 (ノードの再開) スクリプトを使用するかどうかを指定します。  

    > [!TIP]  
    >  次の例は、現在の時刻をテキスト ファイルに書き込む、展開前スクリプトと展開後スクリプトをテストするときに使用できます。  
    >   
    >  **展開前**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **展開後**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>ソフトウェア更新プログラムをサーバー グループに展開して状態を監視するには  

1.  サーバーグループ コレクションに[ソフトウェア更新プログラムを展開](../../sum/deploy-use/deploy-software-updates.md)します。  

2.  [ソフトウェア更新プログラムの展開を監視](../../sum/deploy-use/monitor-software-updates.md)します。 ソフトウェア更新プログラムの展開の標準の監視ビューに加え、クライアントがソフトウェア更新プログラムをインストールする順番を待機している際に、新しい状態の説明が表示されるようになりました。 **[ロックを待っています]** がこの新しい状態に表示されます。  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>サーバー グループ内のコンピューターの展開のロックを解除するには  

1.  **[資産とコンプライアンス]** ワークスペースで、 **[デバイス コレクション]** ノードをクリックしてから、コレクションをクリックして展開のロックを解除します。  

2.  **[ホーム]** タブの **[展開]** グループで、 **[サーバー グループ展開のロックを解除]** をクリックします。 クライアントがソフトウェア更新プログラムのインストールに失敗し他のクライアントのソフトウェア更新プログラムのインストールを妨げている場合は、展開のロックを手動でクリアできます。  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a> Microsoft Defender Advanced Threat Protection サービスのサポート  
 Microsoft Defender Advanced Threat Protection (ATP) は、企業が自社のネットワーク上の高度な攻撃を検出、調査、対応するのに役立つサービスです。 Microsoft Defender ATP は、以前は Windows Defender ATP と呼ばれていました。 [Microsoft Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection) の詳細についてご確認ください。 Configuration Manager は、管理対象の Windows 10 Anniversary Edition クライアント デバイスのオンボードと監視に役立ちます。  

### <a name="try-it-now"></a>今すぐ試す  
 次のタスクを完了し、Microsoft Connect サイトの「[Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)」 (Configuration Manager フィードバック プログラム) ページのフィードバック フォームを使用して、どのように動作したかをお知らせください。  

- Microsoft Defender Advanced Threat Protection (ATP) オンライン サービスにデバイスをオンボードする  

- マネージド デバイスへの Microsoft Defender ATP の展開を監視する  

  **必要条件**  

- Microsoft Defender Advanced Threat Protection オンライン サービスのサブスクリプション  

- Windows 10 Anniversary Edition (ビルド番号 14328 以降) を実行しているクライアント  

- クライアント オンボード構成ファイルの作成  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>オンボード構成ファイルの作成方法  

  1.  Microsoft Defender ATP オンライン サービスにログオンします。  

  2.  **[クライアント オンボーディング]** メニュー項目をクリックします。  

  3.  **[Configuration Manager]** を選択し、 **[パッケージのダウンロード]** をクリックします。  

  4.  圧縮済みアーカイブ (.zip) ファイルをダウンロードして内容を抽出します。  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Microsoft Defender ATP のオンボード デバイス  

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[概要]**  >  **[Endpoint Protection]**  >  **[Windows Defender ATP ポリシー]** の順に移動し、 **[Windows Defender ATP ポリシーの作成]** をクリックします。 Microsoft Defender ATP ポリシー ウィザードが開きます。  

2. Microsoft Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、 **[オンボード]** を選択します。 [次へ] をクリックします。  

3. 組織の Microsoft Defender ATP のクラウド サービス テナントによって提供される構成ファイルを**参照**します。 **[次へ]** をクリックします。  

4. マネージド デバイスから分析用に収集され共有されるファイルのサンプルを指定します。  

   - **なし**: 分析用にサンプル ファイルは収集されません。  

   - **移植可能な実行可能ファイル**: プログラム ファイル (.exe)、ダイナミック ライブラリ リンク (.dll) ファイル、およびサイバー攻撃にさらされる可能性がある同様のファイルなどが分析用に収集され共有されます。  

     **[次へ]** をクリックします。  

5. 概要を確認して、ウィザードを完了します。  

6. これで、 **[展開]** をクリックすると、Microsoft Defender ATP ポリシーを管理対象のクライアント コンピューターに展開できます。  

##### <a name="monitor-microsoft-defender-atp"></a>Microsoft Defender ATP の監視  

1.  Configuration Manager コンソールで、 **[監視]**  >  **[概要]**  >  **[セキュリティ]** の順に移動し、 **[Windows Defender ATP]** をクリックします。  

2.  Microsoft Defender Advanced Threat Protection ダッシュボードを確認します。  

    -   **Windows Defender のエージェントの展開ステータス**: アクティブな Microsoft Defender ATP ポリシーがオンボードされている管理対象のクライアント コンピューターの数と割合  

    -   **Windows Defender ATP Agent Health**: 自身の Microsoft Defender ATP エージェントの状態を報告するコンピューター クライアントの割合  

        -   **正常**: 正常に機能しています  

        -   **非アクティブ**: 期間中にサービスに送信されるデータがありません  

        -   **エージェントの状態**: Windows でエージェントのシステム サービスが実行されていません。  

        -   **非オンボード**: ポリシーは適用されましたが、エージェントがポリシー オンボードを報告していません。  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a> オンプレミスのデバイス正常性構成証明書  
 オンプレミスのインフラストラクチャを使用して通信するように、Windows 10 デバイスの正常性構成証明書を構成できるようになりました。 管理者は、報告がクラウドを使用して行われるか、オンプレミスのリソースを使用して行われるかを指定できます。 正常性構成証明書の報告にオンプレミスが選択されている場合、サービスに URL を指定することができます。 これにより、インターネット アクセスを使用しないクライアント PC が、正常性構成証明書を使用してデバイスを有効化および管理できるようになります。  

### <a name="enable-health-attestation-for-on-premises-devices"></a>オンプレミス デバイス正常性構成証明書の有効化  
 1605 では、1604 の Technical Preview で見つかったいくつかのバグが修正されています。  これを試すには、クライアント エージェント設定を使用して、オンプレミスの正常性構成証明書サービスを構成します。  

1.  Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クライアント設定]** に移動し、 **[オンプレミスの正常性構成証明書サービスを使用]** を **[はい]** に設定します。  

2.  **[オンプレミスの正常性構成証明書サービスの URL]** を指定し、 **[OK]** をクリックします。  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Windows 10 クライアントにおけるソフトウェア更新プログラムのインストール後の新しい再起動オプション  
 再起動の必要なソフトウェア更新プログラムが Configuration Manager により展開され、コンピューターにインストールされた場合、再起動が保留中としてスケジュールされ、再起動のダイアログ ボックスが表示されます。 現在、Windows 8 以降のコンピューターでは、再起動が保留中となっているときに、(再起動ダイアログから行う代わりに) Windows 電源オプションを使用してコンピューターをシャットダウンまたは再起動する場合、再起動ダイアログはコンピューターの再起動後もそのまま表示され、コンピューターも構成された期限までに再起動が必要になります。 この Technical Preview では、Configuration Manager ソフトウェアの更新のために再起動が保留中となっているときはいつでも Windows 10 コンピューターの Windows 電源オプションで **[更新と再起動]** および **[更新とシャットダウン]** のオプションを利用できるようになりました。 これらのオプションのいずれかを使用した場合、コンピューターの再起動後に再起動ダイアログは表示されません。  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a> IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言  
 会社が所有するデバイスの International station Mobile Equipment Identity (IMEI) 番号をインポートすることでデバイスを識別できるようになりました。 デバイスの IMEI 番号を含むコンマ区切り値 (.csv) ファイルをアップロードするか、デバイス情報を手動で入力することができます。  iOS デバイスのシリアル番号をインポートすることもできます。  インポートされた情報によって登録するデバイスの所有権が "企業" として設定されます。  Intune ライセンスも、サービスにアクセスする各ユーザーに必要です。  

### <a name="try-it-out"></a>試してみましょう。  
 次のタスクを完了し、Microsoft Connect サイトの「[Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)」 (Configuration Manager フィードバック プログラム) ページのフィードバック フォームを使用して、どのように動作したかをお知らせください。  

-   IMEI 番号のセットを .csv ファイルでインポートします。 各行には、IMEI 番号に続いて詳細フィールドを含めることができます。  

-   Configuration Manager コンソールから IMEI 番号を手動でインポートします。  

-   iOS 番号のセットを .csv ファイルでインポートします。 ここでも、各行には、番号に続いてデバイスの詳細を含めることができます。  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言  

1. Configuration Manager コンソールで **[資産とコンプライアンス]**  >  **[概要]**  >  **[会社が所有しているすべてのデバイス]**  >  **[事前に宣言されたデバイス]** の順に移動し、 **[事前に宣言されたデバイスを作成します]** をクリックします。 事前に宣言されたデバイス ウィザードが開きます。  

2. デバイス情報を追加する方法を指定します。  

   -   **デバイスの IMEI 番号と詳細情報を記載した CSV ファイルをアップロードする**: 番号の一覧をアップロードするには、ステップ 3 を参照してください。  

   -   **IMEI 番号と詳細情報を手作業で追加する**: 手動で情報を入力するには、IMEI 番号または iOS シリアル番号とデバイスの詳細を入力してからステップ 4 に進みます。  

3. アップロードされたファイルの場合、情報を含む .csv ファイルを参照し、会社所有のデバイスを事前に宣言します。 ファイルには、次の形式が必要です。ただし、一番上の行 (ガイダンスのためだけに提供) は除きます。  

   |**IMEI #**|**iOS シリアル**|**OS**|**詳細**|
   |---|---|---|---|
   |123456789012345||WINDOWS|会社所有の Windows デバイス|
   |123456789012|A0BCD0EFGH0J|IOS|会社所有の iOS デバイス|
   |123456789012346||ANDROID|会社所有の Android デバイス|

    **列:**  

   - 列 1: IMEI 番号: 各行に IMEI 番号または iOS シリアル番号のいずれかが必要です。  

   - 列 2: iOS シリアル番号: 事前宣言できるのは iOS シリアル番号だけです。 他のデバイス プラットフォームには IMEI 番号を使用します。  

   - 列 3: デバイスのオペレーティング システム (大文字化が必要):  

     -   IOS: すべての iOS デバイス  

     -   WINDOWS: Windows Phone、Window 10 Mobile、および Windows PC など  

     -   ANDROID: すべての Android デバイス  

   - 列 4: 詳細: Configuration Manager コンソールに表示される追加のデバイス情報  

     **[次へ]** をクリックします。  

4. ファイル インポートの結果を確認します。 以前にインポートした IMEI またはシリアル番号には、新しい詳細で更新された詳細があります。  **[次へ]** をクリックして続行するか、 **[戻る]** をクリックして最新の詳細を保持して、ウィザードを完了します。  
