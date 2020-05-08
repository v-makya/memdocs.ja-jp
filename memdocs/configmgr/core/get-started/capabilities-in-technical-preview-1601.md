---
title: Technical Preview 1601 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1601 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ed3f53b6e2e9557def20fc459dfcf4641b0e396d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905824"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Configuration Manager の Technical Preview 1601 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1601 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。      このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、および Technical Preview の機能に関するフィードバックを提供する方法について理解してください。  

 **この Technical Preview の既知の問題:**  

-   **[Client Update Options (クライアント更新オプション)]** を管理して、実稼働前クライアントを実稼働版に昇格するときに、このチェック ボックスのテキストに、実際のクライアント ビルド番号ではなく、クライアント バージョン 0 が表示されます。 実稼働前クライアントの正しいバージョンはこのオプションの上にある画面に表示され、このオプションを選択すると、実稼働版に昇格されるクライアント バージョンです。  

-   Technical Preview 1601 に更新し、実稼働前コレクションで Configuration Manager クライアントをテストするように選択した場合、コレクションのクライアント パッケージはアップグレードされません。 この問題は Technical Preview 1601 のみが対象です。  

     この問題を回避するには、次のいずれかを行います。  

    -   プライマリ サイトのデータベースで、次の SQL スクリプトを実行します。  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   ラボ サイトに新しい配布ポイント サイト システム役割を追加します。 新しい配布ポイントでは、新しいクライアント パッケージを使用して実稼働前コレクションをアップグレードします。  

**このバージョンでお試しいただける新機能を次に示します。**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a> Microsoft Intune の統合の機能強化  
1601 Technical Preview では、次の機能のサポートが追加されました。  

### <a name="improvements-to-conditional-access"></a>条件付きアクセスの機能強化  

-   **Configuration Manager が管理する PC の条件付きアクセス サポート**  

     Configuration Manager の管理対象 PC に条件付きアクセス ポリシーを設定できるようになりました。こうすると、Exchange Online サービスと SharePoint Online サービスにアクセスするために、対象の PC がコンプライアンス ポリシーに準拠していることが必要になります。  この新しい機能を使用すると、コンプライアンス ポリシーによって PC を Azure AD に登録し、Azure AD 登録を監視してレポートすることもできます。  

    > [!NOTE]  
    >  条件付きアクセスは、Windows 10 ではまだサポートされていません。  

    この機能を使用する前提条件を次に示します。  

    -   Azure Active Directory Premium サブスクリプションと ADFS 同期。  

    -   Microsoft Intune サブスクリプション。 Microsoft Intune サブスクリプションは、Configuration Manager コンソールで構成する必要があります。  

    -   [Azure AD 自動登録の前提条件](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)。  

    このオプションを使用するには、以下に示す特定のルールが含まれるコンプライアンス ポリシーを Configuration Manager で作成し、Intune コンソールで条件付きアクセス ポリシーを設定する必要があります。  また、コンプライアンスに適合した PC のみにアクセスが許可されるようにするため、Windows コンピューターの要件で **[デバイスは準拠デバイスである必要があります]** オプションを設定しなければなりません。 Configuration Manager によって管理される PC に適用されるコンプライアンス ポリシー ルールを次に示します。  

    -   **Azure Active Directory への登録が必要**: このルールでは、ユーザーのデバイスが Azure AD に社内参加しているかどうかがチェックされ、参加していない場合、そのデバイスは Azure AD 内に自動的に登録されます。 自動登録がサポートされているのは Windows 8.1 のみです。 Windows 7 PC の場合には、MSI を展開して自動登録を実行します。 詳しくは、[こちら](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)をご覧ください。  

    -   **必要な更新が特定の日数の期限を過ぎている場合、そのすべてをインストール:** このルールでは、指定された期限および猶予期間内の必須のすべての更新プログラム (**必須の自動更新**ルールで指定) がユーザーのデバイスに含まれているかどうかが確認され、保留されている必須の更新プログラムがあれば自動的にインストールされます。  

    -   **BitLocker ドライブ暗号化が必要:** これは、デバイス上のプライマリ ドライブ (C:\\ など) が BitLocker で暗号化されたかどうかをチェックします。 Bitlocker 暗号化がプライマリ デバイスで有効でない場合、電子メール サービスおよび SharePoint サービスへのアクセスがブロックされます。  

    -   **マルウェア対策が必要:** これによって、マルウェア対策ソフトウェア (System Center Endpoint Protection または Windows Defender 限定) が有効になっていて実行されているかどうかがチェックされます。  
         無効な場合、電子メール サービスおよび SharePoint サービスへのアクセスがブロックされます。  

    非対応のためにブロックされているエンドユーザーは、ソフトウェア センターでコンプライアンス情報を表示し、コンプライアンスに関する問題が解決されると新たにポリシー評価が開始されます。  

-   **正常性構成証明書サービスによる条件付きアクセス** 電子メール サービスと 0365 サービスへのアクセスを、正常性構成証明書サービスによってレポートされるデバイスの正常性に基づいて制限できるようになりました。  さらに、Intune で管理されているデバイスが、デバイスの正常性レポートに含まれます。  

    新しいコンプライアンス ルールが Configuration Manager コンソールに追加されました。このルールを使用すると、デバイスの正常性の状態に基づいてアクセスを許可するかブロックするかを指定できます。  このルールを作成するには、 **[コンプライアンス ポリシーの作成ウィザード]** を開き、新しいルールを追加します。  条件として 「**Reported as health by Health Attestation Service**」 (正常性構成証明書サービスによって正常と報告される) を選択し、値を **True** にします。  これにより、正常と報告されるデバイスのみが、会社のリソースにアクセスできるようになります。 正常性構成証明書サービスと Intune でデバイスの正常性を報告する方法に関する詳細については、「[デバイス正常性構成証明書](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)」をご覧ください。  

-   **新しいコンプライアンス ポリシーの設定:** 新しいコンプライアンス ポリシーの設定は、会社の電子メール サービスおよび SharePoint サービスにアクセスするために使用するデバイス上でセキュリティと保護を強化するのに役立ちます。  

    -   **自動更新が必要:** Windows 8.1 以降のデバイスで、更新プログラムの自動インストールを許可し、インストールされる更新プログラムのクラスを指定できるように求めることができます。  重要というマークが付いている更新のみをインストールするか、推奨される更新すべてをインストールするかを選択できます。  

         自動更新用のルールを作成するには、 **[コンプライアンス ポリシーの作成ウィザード]** を開き、新しいルールを追加します。  条件として **[必須の更新プログラムの最小限の分類]** を選択し、次の使用可能な値のいずれかを設定します。 **[なし]** 、 **[推奨]** 、 **[重要]** 。  

        -   **なし:** 更新プログラムは自動的にインストールされません。  

        -   **推奨:** すべての推奨される更新プログラムがインストールされます。  

        -   **重要:** 重要として分類された更新プログラムのみがインストールされます。  

    -   **モバイル デバイスのロックを解除するパスワードを要求する:** この設定を **[はい]** にすると、エンドユーザーは対象デバイスにアクセスする前にパスワードを入力する必要があります。  

         モバイル デバイスのロックを解除するためのルールを作成するには、 **[コンプライアンス ポリシーの作成ウィザード]** を開き、新しいルールを追加します。 条件として **[Require a password to unlock an idle device]** \(アイドル状態のデバイスのロックを解除するパスワードを要求する) を選択し、値を **True** にします。  

    -   **デバイスの画面がロックされるまでの非アクティブな時間 (分):** ユーザーがパスワードを再入力しなければならなくなるまでのアイドル時間を指定します。  

         このルールを作成するには、 **[コンプライアンス ポリシーの作成ウィザード]** を開き、新しいルールを追加します。 条件として **[デバイスの画面がロックされるまでの非アクティブな時間 (分)]** を選択し、値を 1 分、5 分、15 分、30 分、1 時間のいずれかのオプションに設定します。  

-   **既定ルールをオーバーライド - Intune に登録された準拠デバイスがオンプレミスの Exchange にいつでもアクセスできるようにする:**  

     このオプションをオンにすると、Intune に登録され、コンプライアント ポリシーに準拠しているデバイスはオンプレミスの Exchange へのアクセスが許可されます。 このルールは既定のルールにオーバーライドします。つまり、アクセスを検疫またはブロックする既定のルールを設定した場合でも、登録された準拠デバイスは引き続きオンプレミスの Exchange にアクセスできます。  
     この設定は、登録された準拠デバイスを、オンプレミスの Exchange を介して電子メールにいつでもアクセスさせる場合に使用します。  

     これは、次のプラットフォームでサポートされています。Windows Phone 8 以降、iOS 6 以降。 Android 4.0 以降、Samsung KNOX Standard 4.0 以降  

     このオプションを使用するには、オンプレミスの Exchange の **[条件付きアクセス ポリシーの構成ウィザード]** の **[全般]** ページに移動します。  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a> クライアントのオンライン状態  
Technical Preview 1601 以降、Configuration Manager コンソールでクライアントがオンラインとオフラインのどちらであるかがすぐにわかるようになりました。 コンソール デバイス一覧の更新されたアイコンと列によって、環境内のクライアントの状態を把握し、問題の領域と、注意が必要なその他の問題を特定できます。  

クライアントが Configuration Manager 管理ポイント サイト システムの役割に接続されている場合には、オンラインです。 管理ポイントが、クライアントから ping のようなメッセージを受信している場合には、状態はオンラインになります。 管理ポイントがメッセージを 5 分間ほど何も受け取らないと、クライアントの状態はオフラインになります。  

### <a name="icons-for-client-status"></a>クライアントの状態アイコン  

|||  
|-|-|  
|![クライアントのオンライン状態アイコン](media/online-status-icon.png)|クライアントはオンラインです。|  
|![クライアントのオフライン状態アイコン](media/offline-status-icon.png)|クライアントはオフラインです。|  
|![クライアントの不明な状態アイコン](media/unknown-status-icon.png)|クライアントの状態は不明です。|  

### <a name="prerequisites"></a>[前提条件]  
 クライアントのオンライン状態には、前提条件はありません。 Configuration Manager Technical Preview 1601 がインストールされるとすぐに使用を開始できます。  

### <a name="limitations"></a>制限事項  
 クライアントのオンライン状態が利用できるのは、Configuration Manager クライアントがインストールされている Windows コンピューターのみです。 クライアントのオンライン状態は、Mac コンピューター、Linux と UNIX コンピューター、オンプレミス モバイル デバイス管理によって管理されているデバイスではサポートされていません。  

### <a name="to-view-client-online-status"></a>クライアントのオンライン状態を表示するには  

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]、[概要] > [デバイス]** に移動します。  

2. 列ヘッダーを右クリックし、デバイスのビューに追加するクライアントのオンライン状態フィールドのいずれかをクリックします。 次のフィールドがあります。  

   -   **[デバイスのオンライン状態]** は、クライアントが現在オンラインとオフラインのどちらであるかを示します。  

   -   **[Last Online Time]** \(前回のオンライン時刻) は、クライアントのオンライン状態がオフラインからオンラインにいつ変わったかを示します。  

   -   **[Last Offline Time]** \(前回のオフライン時刻) は、状態がオンラインからオフラインにいつ変わったかを示します。  

   クライアントの状態に対する最近の変更を表示するには、コンソールを更新します。  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a> アプリケーション管理の機能強化  
 1601 Technical Preview では、次の機能のサポートが追加されました。  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>iOS デバイス用のボリューム購入アプリの管理  
 一部のアプリ ストアでは、社内で実行するアプリの複数のライセンスを購入できます。 これは、購入したアプリの複数コピーを追跡する管理オーバーヘッドを削減するのに役立ちます。  

 Configuration Manager は、このようなプログラムなどを通じて購入したアプリを、アプリ ストアからライセンス情報をインポートし、使用したライセンスの数を追跡することにより、管理できるようにします。  


### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS - アプリケーションのアプリ構成<br />ハイブリッド  
 一部の iOS アプリケーションでは、アプリケーションが接続する必要があるサーバーまたはデータベースなどの事前構成設定をサポートしています。 Configuration Manager は、デバイスに対するアプリ構成ポリシーの展開をサポートするようになりました。これにより、ユーザーは情報を知る必要なくアプリをすぐに使用できます。 開発者が対象アプリでこの機能を有効にする必要があります。  

 現在、事前構成がサポートされているアプリが既にいくつかリリースされています。また、社内で開発された基幹業務アプリでこれらがサポートされている可能性もあります。  

#### <a name="prerequisites-for-this-scenario"></a>このシナリオの前提条件  

-   Microsoft Intune サブスクリプションを Configuration Manager に追加しておく必要があります。  

-   有効な Apple APN 証明書を Intune サブスクリプションに追加する必要があります。  

-   アプリケーション構成をサポートする iOS アプリケーションを展開する必要があります。  

#### <a name="try-it-out"></a>試してみましょう。  
 前述の前提条件を満たした後、iOS展開の種類を使用する Configuration Manager アプリケーションを作成しなければなりません。 使用するアプリは、アプリケーション構成をサポートしている必要があります。 構成できる具体的な項目 (名前/値ペア) については、アプリケーション ベンダーの資料を参照してください。  

 次に、アプリ展開の際に、アプリ構成ポリシーを iOS 展開の種類に関連付けます。 既存のアプリとコレクションを対象としている **[App Configuration Policies]** \(アプリ構成ポリシー) ノードからポリシーを展開することもできます。  

 次のタスクを実行してから、このトピックの先頭付近にあるフィードバック情報を使用してその動作を報告してください。  

-   アプリ構成をサポートする iOS アプリの場合は、アプリ ベンダーの資料を参照して、アプリケーションを構成するために指定する必要がある名前と値のペアを調べてください。  

-   **[Create App Configuration Policy]** \(アプリ構成ポリシーの作成) ウィザードを開始します。 ウィザードの **[iOS のポリシー]** ページで、アプリ ベンダーの資料で調べた名前と値のペアを追加するか、必要な値が入っている XML ファイルをインポートできます。  

-   **[ソフトウェアの展開]** ウィザードの **[App Configuration Policy]** \(アプリ構成ポリシー) ページで、作成したアプリ構成ポリシーを、アプリケーションの互換性がある展開の種類と関連付けます。  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a> コンプライアンス設定の機能強化  
 1601 Technical Preview では、次の機能のサポートが追加されました。  

### <a name="microsoft-edge-browser-settings"></a>Microsoft Edge ブラウザーの設定  
 Microsoft Edge ブラウザーの新しい設定が、**Windows 8.1 および Windows 10** 構成項目 (Windows 10 デバイスのみに適用される設定) に追加されました。  

 これらの新しい設定を確認するには、 **[構成項目の作成]** ウィザードの構成項目 **[デバイス設定]** ページで、 **[Microsoft Edge]** を選択します。  

 詳しくは、「[Configuration Manager クライアントを使用せずに管理されている Windows 8.1 デバイスと Windows 10 デバイスの構成項目を作成する方法](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)」をご覧ください。  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Windows 10 Team デバイスのコンプライアンス設定  
 これらの新しいコンプライアンス設定を使用すると、Surface Hub デバイスなどの Windows 10 Team を実行するデバイスを構成できます。  

 新しい設定を確認するには、 **[構成項目の作成]** ウィザードの構成項目 **[デバイス設定]** ページで、 **[Windows 10 Team]** を選択します。  

 詳しくは、「[Configuration Manager クライアントを使用せずに管理されている Windows 8.1 デバイスと Windows 10 デバイスの構成項目を作成する方法](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)」をご覧ください。  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android - Samsung KNOX Standard のキオスク モード<br />ハイブリッド  
 キオスク モードを使用すると、特定の機能のみ実行できるようにデバイスをロックできます。 たとえば、指定した 1 つの管理対象アプリの実行のみをデバイスに許可することや、デバイスのボリューム ボタンを無効にすることができます。 これらの設定は、デバイスのデモ モデルや、POS デバイスなどの 1 つの機能の実行専用のデバイス向けに使用できます。 これらの設定は、**Windows 8.1 および Windows 10** 構成項目 (Windows 10 デバイスのみに適用される設定) で Samsung KNOX Standard デバイスには使用できません。  

 新しい設定を確認するには、 **[構成項目の作成]** ウィザードの構成項目 **[デバイス設定]** ページで、 **[Kiosk Mode - Samsung KNOX]** \(キオスク モード - Samsung KNOX) を選択します。  

 詳しくは、「[Configuration Manager クライアントを使用せずに管理されている Windows 8.1 デバイスと Windows 10 デバイスの構成項目を作成する方法](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)」をご覧ください。  
