---
title: Technical Preview 1705
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1705 で使用できる機能について説明します。
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0ddad23dfde87fa402c01d4eaa21a1b76db27d93
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692929"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Configuration Manager の Technical Preview 1705 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1705 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    

**この Technical Preview の既知の問題:**
-   **Operations Manager Suite コネクタがアップグレードされない。** OMS コネクタが構成されている Technical Preview の以前のバージョンからアップグレードすると、そのコネクタはアップグレードされず、コンソールで使用できなくなります。 アップグレード後に、[Azure サービス ウィザードを使用して](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms)、OMS ワークスペースへの接続を再確立する必要があります。
-   **Surface ドライバーが正常に同期しない。** Technical Preview の Configuration Manager コンソールの**新機能**には Surface ドライバーのサポートが記載されていますが、この機能はまだ期待どおりに動作しません。
-   **Windows Update for Business 遅延ポリシーを作成できない。** Technical Preview の Configuration Manager コンソールの**新機能**には Windows Update for Business 遅延ポリシーを構成する機能が記載されていますが、ウィザードは起動せず、ポリシーを構成することはできません。


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**このバージョンでお試しいただける新機能を次に示します。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>更新のリセット ツール  
コンソール内の更新プログラムにダウンロードやレプリケートの問題がある場合に、Configuration Manager Update Reset Tool (**CMUpdateReset.exe**) を使用して問題を解決することができます。 このツールは、Technical Preview バージョン 1705 に付属しています。 このツールは、Technical Preview のインストール後、Technical Preview サイトのサイト サーバーの ***\cd.latest\SMSSETUP\TOOLS*** フォルダー内にあります。

このツールは、Technical Preview バージョン 1606 以降で使用できます。 この後方互換のサポートは、Technical Preview の更新シナリオの範囲でツールが使用できるようにするためと、次の Technical Preview が使用可能になるまで待たなくても済むように提供されています。

このツールは、コンソール内の更新プログラムがまだインストールされておらず、エラー状態のときに使用することができます。 エラー状態は、更新プログラムのダウンロードは進行中だが、スタックして極端に長い時間 (同様のサイズの更新パッケージのこれまでの所要時間よりも数時間も長い) かかっていることを意味している場合があります。 また、更新プログラムの子プライマリ サイトへのレプリケートの失敗を意味している場合もあります。  

ツールを実行する際には、指定した更新プログラムに対して実行します。 既定では、このツールで正常にインストールまたはダウンロードされた更新プログラムが削除されることはありません。  

### <a name="prerequisites"></a>[前提条件]
ツールの実行に使用するアカウントには、次のアクセス許可が必要です。
-   中央管理サイトと階層の各プライマリ サイトのサイト データベースへの**読み取り**と**書き込み**アクセス許可。 これらのアクセス許可を設定するため、各サイトの Configuration Manager データベースで、ユーザー アカウントを **db_datawriter** および **db_datareader** の[固定データベース ロール](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles)のメンバーとして追加できます。 このツールは、セカンダリ サイトとは対話しません。
-   階層の最上位サイトの**ローカル管理者**。
-   サービス接続ポイントをホストするコンピューターの**ローカル管理者**。

リセットする更新プログラム パッケージの GUID が必要になります。 GUID の取得には、次の手順を実行します。
-   コンソールで、 **[管理]**  >  **[更新とサービス]** の順に移動し、表示ウィンドウでいずれかの列の見出し ( **[状態]** など) を右クリックして、 **[パッケージ GUID]** を選択します。 これによりその列が表示に追加され、列には更新プログラム パッケージの GUID が示されます。

> [!TIP]  
> GUID をコピーするには、リセットする更新プログラム パッケージの行を選択し、CTRL + C キーを使用してその行をコピーします。 コピーした選択をテキスト エディターに貼り付けると、ツールを実行する際に、GUID のみをコピーしてコマンド ライン パラメーターとして使用できます。

### <a name="run-the-tool"></a>ツールを実行します。    
このツールは、階層の最上位サイトで実行する必要があります。

ツールを実行する際に、コマンド ライン パラメーターを使用して、階層の最上位サイトの SQL Server、サイト データベース名、およびリセットする更新プログラム パッケージの GUID を指定します。 ツールは、更新プログラムの状態に基づいてアクセスする必要がある追加のサーバーを識別します。   

更新プログラム パッケージが*ダウンロード後*の状態にある場合、ツールはパッケージをクリーンアップしません。 オプションとして、強制削除パラメーター (このトピックで後述するコマンド ライン パラメーターを参照) を使用して、正常にダウンロードされた更新プログラムの削除を強制できます。

ツールの実行後:
-   パッケージが削除されたら、最上位層サイトの SMS_Executive サービスを再起動してから、更新プログラムを確認してパッケージを再度ダウンロードします。
-   パッケージが削除されていない場合は、特に何もする必要はありません。更新プログラムによって再初期化され、レプリケーションまたはインストールが再開されます。

**コマンド ライン パラメーター**  


|                        パラメーター                         |                                                            [説明]                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;最上位層サイトの SQL Server の FQDN>** | *必須* <br> 階層の最上位層サイトのサイト データベースをホストする SQL Server の FQDN を指定する必要があります。 |
|                **-D &lt;データベース名>**                 |                             *必須* <br> 最上位層サイト データベースの名前を指定する必要があります。                             |
|                 **-P &lt;パッケージ GUID>**                 |                        *必須* <br> リセットする更新プログラム パッケージの GUID を指定する必要があります。                        |
|           **-I &lt;SQL Server インスタンス名>**           |                   *省略可能* <br> サイト データベースをホストする SQL Server のインスタンスを識別するには、これを使用します。                   |
|                       **-FDELETE**                       |                      *省略可能* <br> 正常にダウンロードした更新プログラム パッケージの削除を強制するには、これを使用します。                      |

 **例:**  
 一般的なシナリオで、ダウンロードに関する問題のある更新プログラムをリセットするとします。 SQL Server の FQDN が *server1.fabrikam.com* で、サイト データベースが *CM_XYZ*、パッケージ GUID が *61F16B3C-F1F6-4F9F-8647-2A524B0C802C* の場合、  次を実行します。***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 より極端なシナリオで、問題のある更新プログラム パッケージの削除を強制するとします。 SQL Server の FQDN が *server1.fabrikam.com* で、サイト データベースが *CM_XYZ*、パッケージ GUID が *61F16B3C-F1F6-4F9F-8647-2A524B0C802C* の場合、  次を実行します。***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Technical Preview でツールをテストする  
このツールは、Technical Preview バージョン 1606 以降で使用できます。 この後方互換のサポートは、Technical Preview のより多くの更新シナリオでツールが使用できるようにするためと、Technical Preview の次のバージョンが使用可能になるまで待たなくても済むように提供されています。

更新プログラムの前提条件の確認を完了する前に、Technical Preview の更新プログラム パッケージでツールを実行します。 前提条件の確認が完了した状態は、 **[管理]**  >  **[更新とサービス]** でパッケージが次のいずれかの状態で識別できます。  
-   **前提条件チェックに合格しました**
-   **前提条件チェックに合格しましたが警告が発生しました**
-   **前提条件チェックに合格しませんでした**


## <a name="high-dpi-console-support"></a>高 DPI コンソールのサポート

このリリースでは、高 DPI デバイス (Surface Book など) で表示したときに、Configuration Manager コンソールのスケーリング方法と、UI のさまざまな部分を表示する方法に修正すべき問題があります。


## <a name="peer-cache-improvements"></a>ピア キャッシュの改善
この Technical Preview から、ピア キャッシュはピアからのダウンロード要求を認証するために[ネットワーク アクセス アカウントを使用しなくなりました](../plan-design/hierarchy/client-peer-cache.md)。


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性グループの機能強化  
このリリースでは、Configuration Manager で使用する SQL Server Always On 可用性グループで非同期コミット レプリカを使用できるようになりました。  これにより、オフサイトの (リモート) バックアップとして使用する追加のレプリカを可用性グループに追加して、それらをディザスター リカバリー シナリオで使用することができます。  

- Configuration Manager は、同期レプリカを復旧するために非同期コミット レプリカの使用をサポートしています。  これを実行する方法については、バックアップと回復に関するトピックで[サイト データベースの回復オプション](../servers/manage/recover-sites.md#site-database-recovery-options)を参照してください。

- このリリースでは、非同期コミット レプリカをサイト データベースとして使用するためのフェールオーバーはサポートされていません。
  > [!CAUTION]  
  > Configuration Manager では、非同期コミット レプリカが最新のものかどうかを確認するために状態を検証せず、また、[このようなレプリカは意図的に非同期にできる](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2014#AvailabilityModes)ため、非同期コミット レプリカをサイト データベースとして使用すると、サイトとデータの整合性が危険にさらされる場合があります。  

- 可用性グループでは、使用する SQL Server のバージョンでサポートされているのと同じ数と種類のレプリカを使用できます    (以前のサポートでは、同期コミット レプリカは 2 つに制限されていました)。

### <a name="configure-an-asynchronous-commit-replica"></a>非同期コミット レプリカを構成する
非同期レプリカを[ Configuration Manager で使用する可用性グループ](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)に追加するために、同期レプリカの構成に必要な構成スクリプトを実行する必要はありません  (これは、その非同期レプリカをサイト データベースとして使用するためのサポートがないためです)。詳細については、[可用性グループへのセカンダリ レプリカの追加](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server?view=sql-server-2014)に関するページを参照してください。

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>非同期レプリカを使用してサイトを回復する
非同期レプリカを使用してサイト データベースを回復する前に、サイト データベースへの追加の書き込みを防止するために、アクティブなプライマリ サイトを停止する必要があります。 サイトの停止後、[手動で回復したデータベース](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered)の代わりに、非同期レプリカを使用することができます。

サイトを停止するには、[階層のメンテナンス ツール](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md)を使用して、サイト サーバーの主要なサービスを停止します。 次のコマンド ラインを使用します:**Preinst.exe /stopsite**   

サイトを停止することは、サイト サーバーでサイト コンポーネント マネージャー サービス (sitecomp) に続いて SMS_Executive サービスを停止することと同じです。


## <a name="improved-user-notifications-for-office-365-updates"></a>Office 365 更新プログラムのユーザーへの通知の改善
クライアントが Office 365 更新プログラムをインストールする場合に、Office クイック実行ユーザー エクスペリエンスを活用するように改善されました。 これには、ポップアップとアプリ内通知、およびカウントダウン エクスペリエンスが含まれます。 以前のリリースでは、Office 365 更新プログラムがクライアントに送信されると、開いていた Office アプリケーションが警告なしで自動的に閉じられていました。 この更新により、Office アプリケーションが予期せずに閉じられることはなくなります。

### <a name="prerequisites"></a>[前提条件]
この更新プログラムは、Office 365 ProPlus クライアントに適用されます。

### <a name="known-issues"></a>既知の問題
クライアントが初めて Office 365 の更新割り当てを評価し、その更新プログラムの期限が過去にスケジュールされている場合、今すぐにスケジュールされている場合、または 30 分以内にスケジュールされている場合、Office 365 のユーザー エクスペリエンスに一貫性がなくなる場合があります。 たとえば、クライアントが更新プログラムに対して 30 分間のカウント ダウン ダイアログを受け取った場合でも、実際の適用はカウント ダウンが終わる前に開始できます。 この動作を回避するには、次を考慮してください。
- 現在の時刻から 60 分以上先にスケジュールされた期限付きで Office 365 の更新プログラムを展開します。
- コレクションに対して勤務時間外にメンテナンス期間を設定するか、展開に対して適用猶予期間を設定します。

### <a name="try-it-out"></a>試してみましょう。
次のタスクを試した後、どのように動作したかについて、リボンの **[ホーム]** タブから **[フィードバック]** を送信してください。
- 現在の時刻から 60 分以上先の時間に設定した期限付きで Office 365 更新プログラムをクライアントに展開します。 クライアントで新しい動作を確認します。


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Windows Defender Application Guard ポリシーの構成と展開

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) は、信頼できない Web サイトをオペレーティング システムの他の部分からはアクセスできない安全な分離コンテナーで開くことでユーザーを保護する Windows の新機能です。 この Technical Preview では、設定する Configuration Manager のコンプライアンス設定を使用して、この機能を構成し、コレクションに展開するためのサポートが追加されました。
この機能は、64 ビット版の Windows 10 Creators Update のプレビューでリリースされます。 この機能を今すぐテストするには、この更新プログラムのプレビュー バージョンを使用している必要があります。


### <a name="before-you-start"></a>開始する前に

Windows Defender Application Guard ポリシーを作成して展開するには、ネットワーク分離ポリシーを使用して、ポリシーを展開する Windows 10 デバイスを構成する必要があります。 詳細については、後述のブログ記事を参照してください。
この機能は、最新の Windows 10 Insider Build でのみ動作します。 これをテストするには、クライアントが最新の Windows 10 Insider Build で実行されている必要があります。

### <a name="try-it-out"></a>試してみましょう。

ブログ記事を読み、Windows Defender Application Guard に関する基本を確実に理解してください。

ポリシーを作成し、使用可能な設定を参照するには、次の手順を実行します。

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** を選択します。
2.  **[資産とコンプライアンス]** ワークスペースで、 **[概要]**  >  **[Endpoint Protection]**  >  **[Windows Defender Application Guard]** の順に選択します。
3.  **[ホーム]** タブの **[作成]** グループで、 **[Windows Defender Application Guard ポリシーの作成]** をクリックします。
4.  ブログ記事を参照として使用して、使用可能な設定を参照および構成して、機能を試すことができます。
5.  完了したら、ウィザードを終了し、1 つ以上の Windows 10 デバイスにポリシーを展開します。

### <a name="further-reading"></a>参考資料

Windows Defender Application Guard の詳細については、[このブログ記事]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)を参照してください。
また、Windows Defender Application Guard のスタンドアロン モードの詳細については、[このブログ記事](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)を参照してください。




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Azure AD の新機能とクラウド管理

このリリースでは、次のシナリオをサポートするために、クラウド サービスで Azure AD を使用するように構成できます。

- インターネットから手動で Configuration Manager クライアントをインストールして、Configuration Manager サイトに割り当てる。
- Intune を使用して、インターネット上で Configuration Manager クライアントをデバイスに展開する。

### <a name="advantages"></a>長所

クラウド サービスと Azure AD を使用することで、クライアント認証証明書を使用する必要がなくなります。

コレクションおよびその他の Configuration Manager の操作で使用するサイト内で Azure AD ユーザーを検出できます。

### <a name="before-you-start"></a>開始する前に

- Azure AD テナントが必要です。
- デバイスで、Windows 10 が実行され、Azure AD が参加している必要があります。  参加している Azure AD に加え、クライアントもドメインに参加できます。
- 管理ポイントのサイト システムの役割に対する[既存の前提条件](../plan-design/configs/site-and-site-system-prerequisites.md)に加え、**ASP.NET 4.5** (およびこれと一緒に自動的に選択されるその他のオプション) が、このサイト システムの役割をホストするコンピューターで有効になっていることを確認する必要があります。
- Microsoft Intune を使用して、Configuration Manager クライアントを展開するには:
    - 動作中の Intune テナント (Configuration Manager と Intune を接続する必要はありません) が必要です。
    - Intune で、Configuration Manager クライアントを含むアプリを作成して展開している必要があります。 この方法について詳しくは、「Intune に登録されている MDM 管理対象 Windows デバイスへのクライアントのインストール方法」を参照してください。
- Configuration Manager を使用して、クライアントを展開するには:
    - HTTPS モード用に少なくとも 1 つの管理ポイントを構成する必要があります。
    - クラウド管理ゲートウェイを設定する必要があります。


### <a name="set-up-the-cloud-management-gateway"></a>クラウド管理ゲートウェイを設定する

クライアントが証明書を使用せずにインターネットから Configuration Manager サイトにアクセスできるように、クラウド管理ゲートウェイを設定します。

この方法についてのヘルプは、次のトピックにあります。

- [Configuration Manager でクラウド管理ゲートウェイを計画する](../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Configuration Manager のクラウド管理ゲートウェイを設定する](../clients/manage/cmg/setup-cloud-management-gateway.md)
- [Configuration Manager でクラウド管理ゲートウェイを監視する](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md)

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configuration Manager Cloud Services で Azure サービス アプリを設定する

これにより、Configuration Manager サイトを Azure AD に接続します。これは、このセクションの他のすべての操作の前提条件です。 手順は次のとおりです。

1. Configuration Manager コンソールの **[管理]** ワークスペースで、 **[クラウド サービス]** を展開して、 **[Azure サービス]** をクリックします。
2. **[ホーム]** タブの **[Azure サービス]** グループで、 **[Azure サービスの構成]** をクリックします。
3. Azure サービス ウィザードの **[Azure サービス]** ページで、 **[クラウド管理]** を選択して、クライアントが Azure AD を使用して、階層で認証できるようにします。
4. ウィザードの **[全般]** ページで、Azure サービスの名前と説明を指定します。
5. ウィザードの **[アプリ]** ページで、リストからご使用の Azure 環境を選択し、 **[参照]** をクリックして Azure サービスの構成に使用されるサーバーとクライアント アプリを選択します。
   - **[サーバー アプリ]** ウィンドウで、使用するサーバー アプリを選択し、 **[OK]** をクリックします。 サーバー アプリとは、Azure アカウントの構成 (クライアントのテナント ID、クライアント ID、シークレット キーなど) を格納する Azure Web アプリです。 利用可能なサーバー アプリがない場合は、次のいずれかを使用します。
       - **作成**: 新しいサーバー アプリを作成するには、 **[作成]** をクリックします。 アプリとテナントのフレンドリ名を指定します。 次に、Azure にサインインすると、Configuration Manager によって、Azure で Web アプリと、Web アプリで使用するクライアント ID やシークレット キーが作成されます。 その後、Azure Portal からこれらを表示できます。
       - **インポート**: ご利用の Azure サブスクリプションに既に存在する Web アプリを使用するには、 **[インポート]** をクリックします。 アプリとテナントのフレンドリ名を指定し、Configuration Manager で使用する Azure Web アプリのテナント ID、クライアント ID、シークレット キーを指定します。 情報を確認した後、 **[OK]** をクリックして続行します。 このオプションは、この Technical Preview では現在使用できません。
   - クライアント アプリに同じプロセスを繰り返します。

   アプリケーションのインポートを使用して、ポータルで適切なアクセス許可を設定する場合には、*ディレクトリ データの読み取り*アプリケーションのアクセス許可を付与する必要があります。 アプリケーションでアクセス許可が自動的に作成されるアプリケーションの作成を使用した場合でも、Azure ポータルでアプリケーションに承諾を与える必要があります。
6. ウィザードの **[検出]** ページで、オプションで **[Azure Active Directory ユーザーの探索を有効にする]** 、 **[設定]** の順にクリックします。
   **[Azure AD ユーザー探索設定]** ダイアログ ボックスで、検出を実行するスケジュールを設定します。 Azure AD の新規または変更されたアカウントのみをチェックする差分探索を有効にすることもできます。
7. ウィザードを完了します。

この時点で、Configuration Manager サイトが Azure AD に接続されています。


### <a name="install-the-cm-client-from-the-internet"></a>インターネットから CM クライアントをインストールする

開始する前に、クライアント インストール ソース ファイルが、クライアントをインストールするデバイスのローカルに保存されていることを確認します。
次に、次のインストール コマンド ラインを使用して (例の値は、独自の値に置き換えてください)、「[クライアントを Windows コンピューターに展開する方法](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)」の手順に従います。

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=\<GUID> AADRESOURCEURI=<code>https://contososerver</code>**

- **/NoCrlCheck**:管理ポイントまたはクラウド管理ゲートウェイが非公開のサーバー証明書を使用する場合、クライアントが CRL の場所に到達できない場合があります。
- **/Source**:ローカル フォルダー: クライアント インストール ファイルの場所。
- **CCMHOSTNAME**:インターネット管理ポイントの名前。 これを見つけるには、管理対象クライアントのコマンド プロンプトから **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** を実行します。
- **SMSMP**:ルックアップ管理ポイントの名前。イントラネットを指定することもできます。
- **SMSSiteCode**:Configuration Manager サイトのサイト コード。
- **AADTENANTID**、**AADTENANTNAME**:Configuration Manager にリンクした Azure AD テナントの ID と名前。 これを見つけるには、Azure AD に参加しているデバイスで、コマンド プロンプトから dsregcmd.exe/status を実行します。
- **AADCLIENTAPPID**:Azure AD クライアント アプリ ID。 これを見つけるには、「[リソースにアクセスできる Azure Active Directory アプリケーションとサービス プリンシパルをポータルで作成する](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)」を参照してください。
- **AADResourceUri**:搭載された Azure AD サーバー アプリの識別子 URI。

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Azure サービス ウィザードを使用して、OMS への接続を構成する
Technical Preview リリース 1705 からは、**Azure サービス ウィザード**を使用して、Configuration Manager から Operations Management Suite (OMS) のクラウド サービスへの接続を構成します。 ウィザードは、前のワークフローを置き換えてこの接続を構成します。

-   ウィザードは、Configuration Manager (OMS など)、ビジネス向け Windows ストア (WSfB)、および Azure Active Directory (Azure AD) 用にクラウド サービスを構成するために使用されます。  

-   Configuration Manager では、Log Analytics や Upgrade Readiness などの機能のために OMS に接続されます。

### <a name="prerequisites-for-the-oms-connector"></a>OMS コネクタの前提条件
OMS への接続を構成するための前提条件は、[Current Branch バージョン 1702 のドキュメント](/azure/azure-monitor/platform/collect-sccm)に記載されているものと変わりません。 ここではその情報を再掲します。  

-   Configuration Manager のアクセス許可を OMS に提供します。

-   OMS コネクタは、[オンライン モード](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)の[サービス接続ポイント](../servers/deploy/configure/about-the-service-connection-point.md)をホストするコンピューターにインストールする必要があります。

-   サービス接続ポイントには、OMS 用の Microsoft Monitoring Agent、および OMS コネクタをインストールする必要があります。 エージェントと OMS コネクタは、同じ **OMS ワークスペース**を使用するように構成する必要があります。 エージェントをインストールする場合は、OMS ドキュメントの「[エージェントのダウンロードとインストール](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)」を参照してください。
-   コネクタとエージェントをインストールしたら、Configuration Manager データを使用するように OMS を構成する必要があります。 そのためには、OMS ポータルで [Configuration Manager コレクションをインポート](/azure/log-analytics/log-analytics-sccm#import-collections)します。

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Azure サービス ウィザードを使用して、OMS への接続を構成する

1.  コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[Azure サービス]** の順に移動し、リボンの **[ホーム]** タブから **[Azure サービスの構成]** を選択して、**Azure サービス ウィザード**を開始します。

2.  **[Azure サービス]** ページで、Operation Management Suite クラウド サービスを選択します。 **[Azure サービス名]** にフレンドリ名を入力し、任意で説明を入力して、 **[次へ]** をクリックします。

3.  **[アプリ]** ページで、ご使用の Azure 環境を指定します (Technical Preview では、パブリック クラウドのみがサポートされます)。 次に、 **[参照]** をクリックして [サーバー アプリ] ウィンドウを開きます。

4.  Web アプリを選択します。

    -   **インポート**:ご利用の Azure サブスクリプションに既に存在する Web アプリを使用するには、 **[インポート]** をクリックします。 アプリとテナントのフレンドリ名を指定し、Configuration Manager で使用する Azure Web アプリのテナント ID、クライアント ID、シークレット キーを指定します。 情報を**確認**した後、 **[OK]** をクリックして続行します。   

    > [!NOTE]   
    > このプレビューで OMS を構成すると、OMS は Web アプリの*インポート*機能のみをサポートします。 新しい Web アプリの作成はサポートされません。 同様に、OMS に既存のアプリを再利用することはできません。

5.  その他の手順をすべて正常に完了すると、 **[OMS Connection Configuration]\(OMS 接続構成\)** 画面の情報が、自動的にこのページに表示されます。 接続設定の情報は、 **[Azure サブスクリプション]** 、 **[Azure リソース グループ]** 、および **[Operations Management Suite ワークスペース]** に表示されます。

6.  ウィザードは、入力した情報を使用して、OMS サービスに接続します。 OMS と同期するデバイス コレクションを選択し、 **[追加]** をクリックします。

7.  **[概要]** 画面で、 **[次へ]** の接続設定を確認します。 **[進行状況]** 画面に接続状態が表示され、 **[完了]** をクリックします。

8.  ウィザードが完了すると、Configuration Manager コンソールに**クラウド サービスの種類**として **Operation Management Suite** を構成したことが示されます。