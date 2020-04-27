---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1709 で使用できる機能について説明します。
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bedb515c8446e13189fb84644bc0ce7563cc1574
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078772"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Configuration Manager の Technical Preview 1709 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1709 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**この Technical Preview の既知の問題:**
- **サイト サーバーがパッシブ モードの場合、プレビュー バージョン 1709 への更新に失敗します**。 プレビュー バージョン 1706、1707、または 1708 を実行し、[プライマリ サイト サーバーがパッシブ モード](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)の場合、プレビュー サイトをバージョン 1709 に正常に更新するには、パッシブ モードのサイト サーバーをアンインストールする必要があります。 パッシブ モードのサイト サーバーは、サイトでバージョン 1709 が実行された後に再インストールできます。

  パッシブ モードのサイト サーバーをアンインストールするには、次の手順を実行します。
  1. コンソールで **[管理]**  >  **[概要]**  >  **[サイトの構成]**  >  **[サーバーとサイト システムの役割]** の順に移動し、パッシブ モードのサイト サーバーを選択します。
  2. **[サイト システムの役割]** ウィンドウで、 **[サイト サーバー]** の役割を右クリックし、 **[役割の削除]** を選択します。
  3. パッシブ モードのサイト サーバーを右クリックし、 **[削除]** を選択します。
  4. サイト サーバーのアンインストール後に、アクティブなプライマリ サイト サーバーで **CONFIGURATION_MANAGER_UPDATE** のサービスを再起動します。


**このバージョンでお試しいただける新機能を次に示します。**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Configuration Manager コンソールの VPN プロファイル エクスペリエンスの向上
<!-- 1313282 -->
このリリースでは、選択したプラットフォームに適した設定が表示されるように、VPN プロファイル ウィザードとプロパティ ページが更新されました。 具体的には次のとおりです。

- 各プラットフォームには独自のワークフローがあります。つまり、新しい VPN プロファイルには、プラットフォームによってサポートされる設定のみが含まれます。
- **[全般]** ページの後に、 **[サポートされているプラットフォーム]** ページが表示されるようになりました。  プロパティの値を設定する前に、プラットフォームを選ぶことができます。
- プラットフォームが **[Android]** 、 **[Android for Work]** 、または **[Windows Phone 8.1]** に設定されている場合は、 **[サポートされているプラットフォーム]** ページは必要なく、表示されません。
- Configuration Manager のクライアント ベースのワークフローが、ハイブリッド モバイル デバイス (MDM) のクライアント ベースの Windows 10 ワークフローと統合されました。これらは同じ設定をサポートします。
- 各プラットフォームのワークフローには、そのワークフローに対して適切な設定のみが含まれます。  たとえば、Android のワークフローには Android に適した設定が含まれ、iOS または Windows 10 Mobile に適した設定は表示されなくなりました。
- Windows 8.1 デバイスの場合は、Configuration Manager によって管理される設定が明確にマークされます。
- [自動 VPN] ページは廃止され、削除されました。

これらの変更は、新しい VPN プロファイルに適用されます。  

互換性のリスクを最小限に抑えるため、既存の VPN プロファイルは変更されません。  既存のプロファイルを編集すると、プロファイル作成時のままの設定が表示されます。  

### <a name="try-it-out"></a>試してみましょう。

通常のプロセスを使って、新しい VPN プロファイルを作成します。 VPN プロファイル ウィザードのオプションの最初のページが変更されたことに注意してください。

1. **[資産とコンプライアンス]**  >  **[概要]**  >  **[コンプライアンス設定]**  >  **[会社のリソースへのアクセス]**  >  **[VPN プロファイル]** の順に移動し、 **[VPN プロファイルの作成]** を選びます。
2. **[全般]** ページで名前を入力し、 **[作成する VPN プロファイルの種類を指定します]** で次のオプションのいずれかを選びます。

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS と macOS  
    - Android  
    - Android for Work  

3. **[Windows 8.1]** を選んだ場合は、**新しいプロファイルを作成する**か、または**ファイルからインポートする**こともできます。
4. ウィザードを完了して、プロファイルの作成を終了します。

異なるプラットフォームを選ぶと、選んだプラットフォームに関連する設定のみが表示されることに注意してください。

## <a name="co-management-for-windows-10-devices"></a>Windows 10 デバイスの共同管理    
<!-- 1350871 -->
多くのユーザーは、モバイル デバイスを管理する場合と同じ低コストで簡単なクラウド ベースのソリューションを使って、Windows 10 デバイスを管理することを望んでいます。 ただし、従来の管理から最新の管理への移行は困難な場合があります。 Windows 10 バージョン 1607 (Anniversary Update とも呼ばれます) より、Windows 10 デバイスをオンプレミスの Active Directory (AD) とクラウドベースの Azure AD (ハイブリッド Azure AD) に同時に結合できるようになりました。 共同管理ではこの機能強化を活用し、Configuration Manager と Intune の両方を使用して複数の Windows 10 デバイスを同時に管理できます。 これは、従来の管理から最新の管理への橋渡しとなるソリューションであり、段階的なアプローチを使って移行する方向を提示します。 

### <a name="prerequisites"></a>[前提条件]
共同管理を有効にする前に、次の前提条件が満たされている必要があります。 一般的な前提条件のほか、既存の Configuration Manager クライアントとクライアント以外のデバイスで異なる前提条件があります。

### <a name="known-issues"></a>既知の問題
共同管理ポリシーを作成した後は、ポリシーを編集できません。 ポリシーを変更するには、いったん削除してから、必要な設定で作成し直します。 

#### <a name="general-prerequisites"></a>一般的な前提条件
共同管理を有効にするための一般的な前提条件は次のとおりです。  

- Configuration Manager の Technical Preview バージョン 1709
- Azure AD 
- すべてのユーザーの EMS または Intune のライセンス
- Intune のサブスクリプション &#40;MDM 機関が **Intune** に設定されたもの&#41;

   > [!Note]  
   > ハイブリッド MDM 環境 (Intune と Configuration Manager が統合された環境) では、共同管理を有効にできません。

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>既存の Configuration Manager クライアントに関する追加の前提条件
- Windows 10 バージョン 1709 (Fall Creators Update) 以降
- ハイブリッド Azure AD への参加 (AD と Azure AD に参加)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>新しい Windows 10 デバイスに関する追加の前提条件
- Windows 10 バージョン 1709 (Fall Creators Update) 以降
- Configuration Manager の[クラウド管理ゲートウェイ](../clients/manage/manage-clients-internet.md#cloud-management-gateway)

### <a name="workloads-you-can-switch-to-intune"></a>Intune に切り替えることができるワークロード
共同管理を有効にした後も、Configuration Manager が引き続きすべてのワークロードを管理します。 準備ができたら、Intune で使用可能なワークロードの管理を始めることができます。 このリリースでは、次のワークロードを Intune で管理できます。   

#### <a name="compliance-policies"></a>コンプライアンス ポリシー
コンプライアンス ポリシーは、デバイスが条件付きアクセス ポリシーによって "準拠している" と見なされるために遵守する必要がある規則および設定を定義します。 コンプライアンス ポリシーを使用して、条件付きアクセスとは別に、デバイスのコンプライアンスに関する問題を監視および修復することもできます。

#### <a name="windows-update-for-business-policies"></a>Windows Update for Business ポリシー
Windows Update for Business ポリシーでは、Windows Update for Business によって直接管理されている Windows 10 デバイスの Windows 10 機能更新プログラムまたは品質更新プログラムに対し、遅延ポリシーを構成できます。 遅延については、「[Windows Update for Business 遅延ポリシーの構成](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)」をご覧ください。  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>共同管理対象デバイスに対して Azure の Intune で利用できるリモート操作
Windows 10 デバイスの共同管理を有効にすると、Azure の Intune から次のリモート操作を実行できます。  
- [出荷時の設定に戻す](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [選択的ワイプ](https://docs.microsoft.com/intune/apps-selective-wipe)
- [デバイスの削除](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [デバイスの再起動](https://docs.microsoft.com/intune/device-restart)
- [新たに開始](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>共同管理用に Intune を準備する
ワークロードを Configuration Manager から Intune に切り替える前に、デバイスが引き続き確実に保護されるように、Intune で必要なプロファイルとポリシーを作成します。
Configuration Manager のオブジェクトに基づいて、Intune のオブジェクトを作成できます。 または、現在の戦略がレガシ管理または従来の管理に基づいている場合は、最新の管理に必要なポリシーとプロファイルの再考が必要な場合があります。 次のリソースを使って、ポリシーとプロファイルを作成します。    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Windows Update for Business ポリシー](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [デバイス構成プロファイル](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>共同管理のアーキテクチャの概要
次の図では、共同管理のアーキテクチャの概要と、既存の構成および Intune インフラストラクチャに共同管理がどのように組み込まれるのかを示します。

![共同管理のアーキテクチャの図](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>共同管理を有効にするシナリオ  
Microsoft Intune に登録された Windows 10 デバイスと既存の Windows 10 Configuration Manager クライアントのどちらについても、共同管理を有効にすることができます。 どちらのシナリオでも、Windows 10 デバイスは Configuration Manager と Intune によって共同管理されるだけでなく、AD と Azure AD に参加します。  

#### <a name="devices-enrolled-in-intune"></a>Intune に登録されたデバイス  
Windows 10 デバイスを Intune に登録したら、Configuration Manager クライアントを (特定のコマンドライン引数を使って) デバイスにインストールし、共同管理用にクライアントを準備できます。 その後、Configuration Manager コンソールから共同管理を有効にして、特定の Windows 10 デバイスの特定のワークロードを Intune に移動する作業を始めます。  

Windows 10 デバイスがまだ Intune に登録されていない場合は、Azure の自動登録を使って登録できます。 新しい Windows 10 デバイスの場合は、Windows AutoPilot を使って、Intune にデバイスを登録する自動登録を含む Out of Box Experience (OOBE) を構成できます。  

#### <a name="configuration-manager-clients"></a>Configuration Manager クライアント
Configuration Manager クライアントである Windows 10 デバイスの場合は、デバイスを登録して、Configuration Manager コンソールから共同管理を有効にできます。 Configuration Manager は、Azure AD テナントの情報に基づいて、Intune への自動登録をトリガーします。  

### <a name="prepare-windows-10-devices-for-co-management"></a>共同管理用に Windows 10 デバイスを準備する
AD と Azure AD に参加し Intune に登録されている Windows 10 デバイスと、Configuration Manager のクライアントで、共同管理を有効にできます。 新しい Windows 10 デバイスおよび Intune に既に登録されているデバイスでは、共同管理を有効にする前に Configuration Manager クライアントをインストールします。 既に Configuration Manager クライアントになっている Windows 10 デバイスの場合は、デバイスを Intune に登録して、Configuration Manager コンソールで共同管理を有効にできます。

#### <a name="command-line-to-install-configuration-manager-client"></a>Configuration Manager クライアントをインストールするためのコマンド ライン
まだ Configuration Manager クライアントではない Windows 10 デバイスの Intune でアプリを作成します。 次のセクションでアプリを作成するときは、次のコマンド ラインを使います。

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*クラウド管理ゲートウェイ相互認証エンドポイントの URL*&#62;/ CCMHOSTNAME=&#60;*クラウド管理ゲートウェイ相互認証エンドポイントの URL*&#62; SMSSiteCode=&#60;*サイト コード*&#62; SMSMP=https:&#47;/&#60;*MP の FQDN*&#62; AADTENANTID=&#60;*AAD テナント ID*&#62; AADTENANTNAME=&#60;*テナント名*&#62; AADCLIENTAPPID=&#60;*AAD 統合用のサーバー アプリ ID*&#62; AADRESOURCEURI=https:&#47;/&#60;*リソース ID*&#62;"

たとえば、次のような値を使うものとします。

- **クラウド管理ゲートウェイ相互認証エンドポイントの URL**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >**クラウド管理ゲートウェイ相互認証エンドポイントの URL** の値には、**vProxy_Roles** SQL ビューの **MutualAuthPath** の値を使います。

- **管理ポイント (MP) の FQDN**: sccmmp.corp.contoso.com    
- **サイトコード**:PS1    
- **Azure AD テナント ID**:72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Azure AD テナント名**: contoso    
- **Azure AD クライアント アプリ ID**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **AAD リソース ID URI**:ConfigMgrServer    

  > [!Note]    
  > **AAD リソース ID URI** の値には、**vSMS_AAD_Application_Ex** SQL ビューの **IdentifierUri** の値を使います。

この場合は、次のようなコマンド ラインを使います。

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer"

> [!Tip]
>サイトのコマンド ライン パラメーターは、次の手順を使って探すことができます。     
> 1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[Co-management]\(共同管理\)** の順に移動します。  
> 2. [ホーム] タブの [管理] グループで、 **[Configure co-management]\(共同管理の構成\)** を選んで共同管理オンボード ウィザードを開きます。    
> 3. [サブスクリプション] ページで **[サインイン]** をクリックして Intune テナントにサインインし、 **[次へ]** をクリックします。    
> 4. [Enablement]\(有効化\) ページで、 **[Devices enrolled in Intune]\(Intune に登録されているデバイス\)** セクションの **[コピー]** をクリックしてコマンド ラインをクリップボードにコピーして保存し、アプリ作成手順で使います。  
> 5. **[キャンセル]** をクリックしてウィザードを終了します。

#### <a name="new-windows-10-devices"></a>新しい Windows 10 デバイス
新しい Windows 10 デバイスの場合は、AutoPilot サービスを使って Out of Box Experience を構成できます。これには、AD および Azure AD へのデバイスの参加と、Intune へのデバイスの登録が含まれます。 その後、Intune にアプリを作成して Configuration Manager クライアントを展開します。  
1. 新しい Windows 10 デバイス用に AutoPilot を有効にします。 詳しくは、「[Windows AutoPilot の概要](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot)」をご覧ください。  
2. Azure AD で自動登録を構成し、デバイスが Intune に自動的に登録されるようにします。 詳しくは、「 [Windows デバイスの登録](https://docs.microsoft.com/intune/windows-enroll)」をご覧ください。
3. Configuration Manager クライアント パッケージで Intune にアプリを作成し、共同管理する Windows 10 デバイスにアプリを展開します。 [Azure AD を使ってインターネットからクライアントをインストールする](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure)手順の間に、[コマンド ラインを使って Configuration Manager クライアントをインストール](#command-line-to-install-configuration-manager-client)します。   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Intune に登録されていないか、Configuration Manager クライアントがインストールされている Windows 10 デバイス
Intune に登録されていないか、Configuration Manager クライアントがインストールされている Windows 10 デバイスの場合は、自動登録を使って Intune にデバイスを登録できます。 その後、Intune にアプリを作成して Configuration Manager クライアントを展開します。
1. Azure AD で自動登録を構成し、デバイスが Intune に自動的に登録されるようにします。 詳しくは、「 [Windows デバイスの登録](https://docs.microsoft.com/intune/windows-enroll)」をご覧ください。  
2. Configuration Manager クライアント パッケージで Intune にアプリを作成し、共同管理する Windows 10 デバイスにアプリを展開します。 [Azure AD を使ってインターネットからクライアントをインストールする](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure)手順の間に、[コマンド ラインを使って Configuration Manager クライアントをインストール](#command-line-to-install-configuration-manager-client)します。

#### <a name="windows-10-devices-enrolled-in-intune"></a>Intune に登録されている Windows 10 デバイス
Intune に既に登録されている Windows 10 デバイスの場合は、Intune でアプリを作成して Configuration Manager クライアントを展開します。 [Azure AD を使ってインターネットからクライアントをインストールする](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure)手順の間に、[コマンド ラインを使って Configuration Manager クライアントをインストール](#command-line-to-install-configuration-manager-client)します。  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Configuration Manager のワークロードを Intune に切り替える
前のセクションでは、共同管理のために Windows 10 デバイスを準備しました。 これらのデバイスは AD と Azure AD に結合されると同時に Intune に登録され、Configuration Manager クライアントがインストールされています。 Windows 10 デバイスが AD に参加し、Configuration Manager クライアントがインストールされていても、まだ Azure AD に参加していないか、Intune に登録されていない場合があります。 次の手順では、共同管理を有効にし、残りの Windows 10 デバイス (Intune に登録されていない Configuration Manager クライアント) を共同管理用に準備して、特定の Configuration Manager ワークロードの Intune への切り替えを開始できるようにします。

1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[Co-management]\(共同管理\)** の順に移動します。    
2. [ホーム] タブの [管理] グループで、 **[Configure co-management]\(共同管理の構成\)** を選んで共同管理オンボード ウィザードを開きます。    
3. [サブスクリプション] ページで **[サインイン]** をクリックして Intune テナントにサインインし、 **[次へ]** をクリックします。   
4. [ステージング] ページで、次の設定を構成した後、 **[次へ]** をクリックします。
    - **パイロット グループ**:パイロット グループには、選択した 1 つまたは複数のコレクションが含まれます。 共同管理の段階的なロールアウトの一部としてこのグループを使います。 小規模なテスト コレクションで開始し、共同管理をロールアウトするユーザーとデバイスを増やしながら、パイロット グループにコレクションを追加します。 パイロット グループのコレクションは共同管理のプロパティからいつでも変更できます。
    - **Production**:この設定を選ぶと、サポートされているすべての Windows 10 デバイスで共同管理が有効になります。 1 つまたは複数のコレクションで **[Exclusion group]\(除外グループ\)** を構成します。 このグループのいずれかのコレクションのメンバーであるデバイスは、共同管理から除外されます。 
5. [Enablement]\(有効化\) ページで、 **[パイロット]** または **[すべて]** ([ステージング] ページで構成した設定に応じて) を選んで Intune での自動登録を有効にし、 **[次へ]** をクリックします。 **[パイロット]** を選ぶと、パイロット グループのメンバーである Configuration manager クライアントのみが Intune に自動的に登録されます。 これにより、クライアントのサブセットで共同管理を有効にして初期テストを行ってから、段階的アプローチでロールアウトできます。 
6. [Workloads]\(ワークロード\) ページで、Configuration Manager のワークロードを Intune による管理に切り替えるかどうかを選び、 **[次へ]** をクリックします。 スライダーを使って、ワークロードを ([ステージング] ページで構成した設定に応じて) パイロット グループまたはすべての Windows 10 クライアントに切り替えるかどうかを選びます。 
7. 共同管理を有効にするには、ウィザードを終了します。  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>関連項目
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。 
