---
title: コレクションを作成する
titleSuffix: Configuration Manager
description: Configuration Manager でユーザーとデバイスのグループをより簡単に管理するコレクションを作成します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eccc3bf6b7ded9db93f5af78d55f090e9704cbc
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438607"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Configuration Manager でのコレクションの作成方法

*適用対象:Configuration Manager (Current Branch)*

コレクションはユーザーまたはデバイスのグループです。 コレクションを使用して、アプリケーションの管理、コンプライアンス設定の展開、ソフトウェア更新プログラムのインストールなどのタスクを行います。 クライアント設定のグループを管理したり、役割ベースの管理を行ってリソースを管理者ユーザーのみアクセス可能に指定したりといったことに、コレクションを使用することもできます。 Configuration Manager には、組み込みコレクションが複数含まれます。 詳細については、「[コレクションの概要](introduction-to-collections.md)」をご覧ください。  

> [!NOTE]  
> コレクションにはユーザーまたはデバイスを含めることができますが、両方を含めることはできません。  


この記事に記載されている情報は、Configuration Manager でコレクションを作成するのに役立ちます。 また、現在の Configuration Manager サイトや別の場所で作成されたコレクションをインポートすることもできます。 コレクションのエクスポートとインポートの方法については、[コレクションの管理方法](manage-collections.md)に関するページを参照してください。  


## <a name="collection-rules"></a>収集規則

Configuration Manager でのコレクションのメンバーを構成するために、さまざまな種類の規則を使用できます。  


### <a name="direct-rule"></a>ダイレクト規則

ダイレクト規則を使って、コレクションに追加するユーザーまたはコンピューターを選択します。 Configuration Manager からリソースを削除しない限り、メンバーシップは変わりません。 リソースをダイレクト規則コレクションに追加するには、そのリソースが Configuration Manager で既に検出されているか、ユーザーがそのリソースをインポートしておく必要があります。 ダイレクト規則のコレクションは手動で変更する必要があるため、クエリ規則のコレクションよりも管理オーバーヘッドが増加します。


### <a name="query-rule"></a>クエリ規則

Configuration Manager がスケジュールに従って実行するクエリに基づいて、コレクションのメンバーシップを動的に更新します。 たとえば、Active Directory ドメイン サービスの人事ユニットのメンバーであるユーザーのコレクションを作成することができます。 このコレクションは、人事ユニットに対して新しいユーザーが追加または削除されたりすると、自動的に更新されます。

コレクションの構築に使用できるクエリの例については、[クエリの作成方法](../../../servers/manage/create-queries.md)に関するページを参照してください。


### <a name="device-category-rule"></a>デバイス カテゴリの規則

デバイス カテゴリをデバイス コレクションに関連付けると、デバイスの管理が簡単になります。 

詳細については、[デバイスを自動的にコレクションごとに分類する方法](automatically-categorize-devices-into-collections.md)に関するページを参照してください。<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>[コレクションを含める] 規則

Configuration Manager に他のコレクションのメンバーを含めます。 含められるコレクションのメンバーシップに変更があった場合、Configuration Manager は現在のコレクションのメンバーシップはスケジュールで更新します。

複数の [コレクションを含める] 規則をコレクションに追加できます。


### <a name="exclude-collection-rule"></a>[コレクションを除外する] 規則

[コレクションを除外する] 規則を使用すると、1 つのコレクションのメンバーを別の Configuration Manager のコレクションから除外することができます。 除外されるコレクションのメンバーシップに変更があった場合、Configuration Manager は現在のコレクションのメンバーシップはスケジュールで更新します。

複数の [コレクションを除外する] 規則をコレクションに追加できます。 コレクションが、[コレクションを含める] 規則と [コレクションを除外する] 規則の両方を含み、競合が生じた場合は、[コレクションを除外する] 規則が優先されます。

#### <a name="example"></a>例
[コレクションを含める] 規則と [コレクションを除外する] 規則が 1 つずつ含まれるコレクションを作成します。 [コレクションを含める] 規則の対象は Dell デスクトップのコレクションです。 [コレクションを除外する] の対象は、RAM が 4 GB 未満のコンピューターのコレクションです。 新しいコレクションには、RAM が 4 GB 以上の Dell デスクトップが含まれます。



## <a name="create-a-collection"></a><a name="bkmk_create"></a> コレクションを作成する  

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動します。  

    - *[デバイス コレクション]* を作成するには、 **[デバイス コレクション]** ノードを選択します。 次に、リボンの **[ホーム]** タブの **[作成]** グループで、 **[デバイス コレクションの作成]** を選択します。  

    - *[ユーザー コレクション]* を作成するには、 **[ユーザー コレクション]** ノードを選択します。 次に、リボンの **[ホーム]** タブの **[作成]** グループで、 **[ユーザー コレクションの作成]** を選択します。  

2. ウィザードの **[全般]** ページで、 **[名前]** と **[コメント]** を指定します。 **[限定コレクション]** セクションで、 **[参照]** を選択した後、限定コレクションを選択します。 作成しているコレクションには、限定コレクションのメンバーのみが含まれるようになります。  

4. **[メンバーシップの規則]** ページの **[規則の追加]** 一覧から、コレクションに使用したいメンバーシップ規則の種類を選択します。 1 つのコレクションにつき複数の規則を構成することができます。 構成は規則によって変わります。 各規則の構成の詳細については、この記事に含まれる以下のセクションを参照してください。  
    - [ダイレクト規則](#bkmk-direct)
    - [クエリ規則](#bkmk-query)
    - [デバイス カテゴリの規則](#bkmk-category)
    - [[コレクションを含める] 規則](#bkmk-include)
    - [[コレクションを除外する] 規則](#bkmk-exclude)

5. また、 **[メンバーシップの規則]** ページで、次の設定を確認してください。

    - **このコレクションで増分更新を使用する**:新しいリソースまたは前回のコレクション評価から変更されたリソースのみを定期的にスキャンおよび更新する場合は、このオプションを選択します。 このプロセスは、コレクションのフル評価とは関係がありません。 既定では、増分更新は 5 分間隔で行われます。  

        > [!IMPORTANT]  
        >  次のクラスを使用しているクエリ規則を持つコレクションは、増分更新をサポートしません。  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (ユーザーのコレクションのみ)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (ユーザーのコレクションのみ)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **このコレクションの完全な更新をスケジュールする:** コレクションのメンバーシップのフル評価を定期的にスケジュールします。  

        バージョン 1810 以降、コレクション評価動作が次のように変更されたため、サイトのパフォーマンスが向上する可能性があります。<!--3607726-->  

        - 以前は、クエリ ベースのコレクションでスケジュールを構成すると、コレクションの設定 **[このコレクションの完全な更新をスケジュールする]** が有効かどうかにかかわらず、サイトではクエリの評価が続けられました。 スケジュールを完全に無効にするには、スケジュールを **[なし]** に変更する必要がありました。

            現在は、この設定を無効にすると、サイトはスケジュールをクリアします。 コレクション評価のスケジュールを指定するには、オプション **[このコレクションの完全な更新をスケジュールする]** を有効にします。  

            サイトを更新すると、スケジュールが指定されていた既存のコレクションについて、サイトはオプション **[このコレクションの完全な更新をスケジュールする]** を有効にします。 この構成はお客様の意図に沿わないかもしれませんが、サイトを更新する前に、スケジュールは実際にこのように動作していました。 スケジュールに従ったサイトのコレクション評価を停止するには、このオプションを無効にします。  

        - **すべてのシステム**のような組み込みコレクションの評価を無効にすることはできませんが、スケジュールを構成できるようになりました。 この動作により、要件を満たしているときはこの操作をカスタマイズできます。 

            > [!TIP]  
            > 組み込みコレクションでは、カスタム スケジュールの **[時刻]** のみを変更してください。 **[パターンの設定]** は変更しないでください。 今後のイテレーションでは、特定の繰り返しパターンが適用される可能性があります。  

6. 新しいコレクションを作成するウィザードを完了します。 新しいコレクションは、 **[資産とコンプライアンス]** ワークスペースの **[デバイス コレクション]** ノードに表示されます。  

> [!NOTE]  
> コレクション メンバーを表示するには、Configuration Manager コンソールを更新または再読み込みする必要があります。 これらは、最初のスケジュールされた更新の後までコレクションに表示されません。 また、コレクションに対して **[メンバーシップの更新]** を手動で選択することもできます。 コレクションの更新が完了するまでに数分かかる場合があります。  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a> ダイレクト規則を構成する  

1. **[ダイレクト メンバーシップの規則の作成ウィザード]** の **[リソースの検索]** ページで、次の情報を指定します。  

    - **リソース クラス**:検索してコレクションに追加するリソースの種類を選択します。 次に例を示します。
        - **システム リソース**:クライアント コンピューターから返されたインベントリ データを検索します。
        - **不明なコンピューター**:不明なコンピューターから返された値から選択します。
        - **ユーザー リソース**:Configuration Manager によって収集されたユーザー情報を検索します。
        - **ユーザー グループ リソース**:Configuration Manager によって収集されたユーザー グループ情報を検索します。

    - **属性名**:検索対象として選択したリソース クラスに関連する属性を選択します。 次に例を示します。  

        - NetBIOS 名でコンピューターを選択する場合は、 **[リソース クラス]** の一覧で **[システム リソース]** を、 **[属性名]** の一覧で **[NetBIOS 名]** を選択します。  

        - 組織単位 (OU) 名でユーザーを選択する場合は、 **[リソース クラス]** の一覧で **[ユーザー リソース]** を、 **[属性名]** の一覧で **[ユーザー OU 名]** を選択します。  

    - **不使用とマークされているリソースを除外する**:クライアント コンピューターが不使用とマークされている場合は、検索結果にその値を含めません。  

    - **Configuration Manager クライアントがインストールされていないリソースを除外する**:このようなリソースは検索結果に表示されません。  

    - **値**:選択した属性名を検索するための値を入力します。 ワイルドカードとしてパーセント記号 (%) を使用します。 次に例を示します。  
        - "M" で始まる NetBIOS 名のコンピューターを検索する場合は、このフィールドに「**M%** 」と入力します。  
        - Contoso OU 内のユーザーを検索するには、このフィールドに「**Contoso**」と入力します。

2. **[リソースの選択]** ページで、コレクションに追加するリソースを **[リソース]** の一覧から選択した後、 **[次へ]** を選択します。  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a> クエリ規則を構成する  

**[クエリ規則のプロパティ]** ダイアログ ボックスで、次の情報を指定します。  

- **名前**:クエリ固有の名前を指定します。  

- **クエリ ステートメントのインポート**: **[クエリの参照]** ダイアログ ボックスを開きます。 コレクションのクエリ規則として使用する [Configuration Manager](../../../servers/manage/create-queries.md) クエリを選択します。   

- **リソース クラス**:検索してコレクションに追加するリソースの種類を選択します。 **[システム リソース]** から値を選択してクライアント コンピューターから返されたインベントリ データを検索するか、 **[不明なコンピューター]** から選択して不明なコンピューターにより返された値から選択します。  

- **クエリ ステートメントの編集**:コレクションの規則として使用するクエリを記述できる **[クエリ ステートメントのプロパティ]** ダイアログ ボックスを開きます。 クエリの詳細については、[クエリの概要](../../../servers/manage/introduction-to-queries.md)に関するページを参照してください。  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="device-category-rule"></a><a name="bkmk-category"></a> デバイス カテゴリの規則

**[デバイス カテゴリの選択]** ウィンドウでは、次のアクションを利用できます。

- **作成**: 名前を指定して新しいカテゴリを作成します。
- **名前の変更**:選択したカテゴリの名前を変更します。
- **削除**:1 つ以上のカテゴリを選択し、このアクションを使用してそれらを一覧から削除します。

詳細については、[デバイスを自動的にコレクションごとに分類する方法](automatically-categorize-devices-into-collections.md)に関するページを参照してください。<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a> [コレクションを含める] 規則を構成する  

**[コレクションの選択]** ダイアログ ボックスで、新しいコレクションに含めるコレクションを選択した後、 **[OK]** を選択します。  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a> [コレクションを除外する] 規則を構成する  

**[コレクションの選択]** ダイアログ ボックスで、新しいコレクションから除外するコレクションを選択した後、 **[OK]** を選択します。  



## <a name="import-a-collection"></a><a name="bkmk_import"></a> コレクションをインポートする  

サイトからエクスポートしたコレクションは、Configuration Manager によって管理オブジェクト フォーマット (MOF) ファイルとして保存されます。 この手順を使用してファイルをサイト データベースにインポートします。 この手順を完了するには、コレクション クラスに対する**作成**アクセス許可が必要です。

> [!IMPORTANT]  
> - ファイルにはコレクション データだけが含まれ、信頼できるソースからのものであり、改ざんされていないことを確認してください。  
> 
> - 使用しているのと同じバージョンの Configuration Manager を実行していたサイトからエクスポートされたファイルであることを確認します。  

コレクションのエクスポートの詳細については、[コレクションの管理方法](manage-collections.md)に関するページを参照してください。


1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動します。 **[ユーザー コレクション]** または **[デバイス コレクション]** ノードのいずれかを選択します。  

2. リボンの **[ホーム]** タブの **[作成]** グループで、 **[コレクションのインポート]** を選択します。  

3. **[コレクションのインポート ウィザード]** の **[全般]** ページで、 **[次へ]** を選択します。  

4. **[MOF ファイル名]** ページで、 **[参照]** を選択します。 インポートするコレクション情報を含む MOF ファイルを参照します。  

5. コレクションをインポートするウィザードを完了します。 新しいコレクションは、 **[資産とコンプライアンス]** ワークスペースの **[ユーザー コレクション]** または **[デバイス コレクション]** ノードに表示されます。 新しくインポートされたコレクションのコレクション メンバーを表示するには、Configuration Manager コンソールを更新または再読み込みします。  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a> コレクションのメンバーシップの結果の Azure Active Directory グループとの同期

<!--3607475-->
> [!Tip]  
> この機能はバージョン 1906 で[プレリリース機能](../../../servers/manage/pre-release-features.md)として初めて導入されました。 バージョン 2002 以降、プレリリース機能ではなくなりました。  

コレクション メンバーシップと Azure Active Directory (Azure AD) グループの同期を有効にすることができます。 この同期により、コレクション メンバーシップの結果に基づいて Azure AD グループのメンバーシップを作成して、クラウドで既存のオンプレミスのグループ化規則を使用することができます。 デバイス コレクションを同期できます。 Azure Active Directory レコードを持つデバイスのみが Azure AD に反映されます。 ハイブリッド Azure AD 参加済みデバイスと Azure Active Director 参加済みデバイスの両方がサポートされます。

Azure AD 同期は 5 分おきに行われます。 これは Configuration Manager から Azure AD への一方向プロセスです。 Azure AD で行われた変更は Configuration Manager コレクションで反映されませんが、Configuration Manager で上書きされることがありません。 たとえば、Configuration Manager コレクションにデバイスが 2 台あり、Azure AD グループに異なるデバイスが 3 台あるとき、同期後、Azure AD グループのデバイスは 5 台となります。

### <a name="prerequisites"></a>[前提条件]

- [クラウド管理](../../../servers/deploy/configure/azure-services-wizard.md)のための Azure AD との統合
- [Azure Active Directory ユーザー探索](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- HTTPS または [拡張 HTTP](../../../plan-design/hierarchy/enhanced-http.md) 対応の管理ポイント
- **[すべてのシステム]** コレクションへのアクセス

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Azure AD でグループを作成して所有者を設定する

1. [https://portal.azure.com](https://portal.azure.com)に移動します。
1. **[Azure Active Directory]**  >  **[グループ]**  >  **[すべてのグループ]** の順に移動します。
1. **[新しいグループ]** をクリックして、 **[グループ名]** と必要に応じて **[グループの説明]** を入力します。
1. **[メンバーシップの種類]** が **[割り当て済]** であることを確認します。
1. **[所有者]** を選択して、Configuration Manager で同期関係を作成する ID を追加します。
1. **[作成]** をクリックして、Azure AD グループの作成を完了します。

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Azure サービスのコレクションの同期を有効にする

1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[Azure サービス]** の順に移動します。
1. グループを作成した Azure AD テナントを右クリックして、 **[プロパティ]** を選択します。
1. **[コレクションの同期]** タブで、 **[Azure Active Directory グループの同期を有効にする]** のチェックボックスをオンにします。
1. **[OK]** をクリックして設定を保存します。

### <a name="enable-the-collection-to-synchronize"></a>同期するコレクションを有効にする

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[概要]**  >  **[デバイス コレクション]** の順に移動します。
1. 同期するコレクションを右クリックして、 **[プロパティ]** をクリックします。 
1. **[クラウドの同期]** タブで、 **[追加]** をクリックします。
1. ドロップダウン メニューで、Azure AD グループを作成した **[テナント]** を選択します。
1. **[名前の先頭]** フィールドに検索条件を入力し、 **[検索]** をクリックします。
  - サインインを求めるメッセージが表示されたら、Azure AD グループの所有者として指定した ID を使用します。
1. ターゲット グループを選択し、 **[OK]** をクリックしてグループを追加し、再度 **[OK]** をクリックして、コレクションのプロパティを終了します。
1. Azure portal でグループ メンバーシップを確認できるようになるまで約 5 から 7 分かかります。
   - 完全同期を開始するには、コレクションを右クリックして、 **[Synchronize Membership]\(メンバーシップを同期する\)** を選択します。


### <a name="verify-the-azure-ad-group-membership"></a>Azure AD グループのメンバーシップを確認する

1. [https://portal.azure.com](https://portal.azure.com)に移動します。
1. **[Azure Active Directory]**  >  **[グループ]**  >  **[すべてのグループ]** の順に移動します。
1. 作成したグループを見つけて、 **[メンバー]** を選択します。 
1. メンバーに Configuration Manager コレクション内のメンバーが反映されていることを確認します。
   - Azure AD ID を持つデバイスのみがグループに表示されます。


![コレクションを Azure AD に同期する](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a>PowerShell の使用

PowerShell を使用してコレクションの作成とインポートを実行できます。 詳細については、次をご覧ください。

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>次のステップ

[コレクションを管理する](manage-collections.md)
