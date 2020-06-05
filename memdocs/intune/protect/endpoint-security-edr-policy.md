---
title: Microsoft Intune でエンドポイント セキュリティ ポリシーを使用してエンドポイントの検出と応答の設定を管理する | Microsoft Docs
description: Microsoft Endpoint Manager でエンドポイント セキュリティのエンドポイントの検出と応答ポリシーを使用して、管理するデバイスのポリシーを構成および展開します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: ac8f82396571a7ae39df43662000f9f3f17d0430
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990881"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのエンドポイントの検出と応答ポリシー

Microsoft Defender Advanced Threat Protection (Defender ATP) と Intune を統合すると、エンドポイントの検出と応答 (EDR) のエンドポイント セキュリティ ポリシーを使用して、EDR の設定を管理したり、デバイスを Defender ATP にオンボードしたりできます。

Defender ATP のエンドポイントの検出と応答機能により、ほぼリアルタイムの実用的で高度な攻撃検出が可能になります。 セキュリティ アナリストは、アラートの優先度を効果的に設定し、侵害の範囲全体を把握し、脅威を修復するための応答アクションを実行できます。

EDR ポリシーには、EDR の設定を管理するための、プラットフォーム固有のプロファイルが含まれています。 プロファイルには、Defender ATP の "*オンボード パッケージ*" が自動的に含まれます。 オンボード パッケージには、Defender ATP と連携するためのデバイスの構成方法が定義されています。 デバイスをオンボードすると、そのデバイスからの脅威データの使用を開始できます。

EDR ポリシーは、Intune で管理する Azure Active Directory (Azure AD) のデバイス グループと、Configuration Manager で管理するオンプレミス デバイスのコレクション (Windows サーバーを含む) に展開されます。 異なる管理パスの EDR ポリシーには、異なるオンボード パッケージが必要です。 そのため、管理するデバイスの種類ごとに個別の EDR ポリシーを作成します。

> [!TIP]
> Configuration Manager で管理しているデバイスのサポートは、"*パブリック プレビュー*" 中です。

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) の **[エンドポイント セキュリティ]** ノードにある *[管理]* で、EDR のためのエンドポイント セキュリティ ポリシーを見つけます。

[エンドポイントの検出と応答プロファイルの設定](../protect/endpoint-security-edr-profile-settings.md)を確認してください。

## <a name="prerequisites-for-edr-policies"></a>EDR ポリシーの前提条件

**全般**:

- **Microsoft Defender Advanced Threat Protection のテナント** – EDR ポリシーを作成する前に、Defender ATP テナントを Microsoft Endpoint Manager テナント (Intune サブスクリプション) と統合する必要があります。 Intune ドキュメントの [Microsoft Defender ATP の使用](../protect/advanced-threat-protection.md)に関するページを参照してください。

**Configuration Manager のデバイスをサポートするには**:

Configuration Manager デバイスに対する EDR ポリシーの使用をサポートするには、Configuration Manager 環境で次の追加構成が必要です。 この記事では、[構成のガイダンス](#set-up-configuration-manager-to-support-edr-policy)を示しています。

- **バージョン 2002 以降の Configuration Manager** - サイトで Configuration Manager 2002 以降を実行する必要があります。

- **Configuration Manager の更新プログラムのインストール** - Microsoft Endpoint Manager admin center で作成した EDR ポリシーの使用のサポートを Configuration Manager 2002 で有効にするには、Configuration Manager コンソール内から次の更新プログラムをインストールします。
  - **Configuration Manager 2002 修正プログラム (KB4563473)**

- **テナントのアタッチの構成** - テナントのアタッチを使用すると、Configuration Manager のデバイスのコレクションを Microsoft Endpoint Manager admin center に同期できます。 そうすると、admin center を使用して、EDR ポリシーをそれらのコレクションに展開することができます。

  テナントのアタッチは、多くの場合、共同管理と共に構成しますが、テナントのアタッチを単独で構成することもできます。

- **Configuration Manager コレクションの同期** – テナントのアタッチを構成するときに、Microsoft Endpoint Manager admin center と同期する Configuration Manager デバイス コレクションを選択できます。 後で戻って、同期するデバイス コレクションを変更することもできます。Configuration Manager デバイスの EDR ポリシーは、同期しているコレクションにのみ割り当てることができます。

  同期するコレクションを選択した後、Microsoft Defender ATP で使用できるようにコレクションを有効にする必要があります。

- **Azure AD に対するアクセス許可** - テナントのアタッチの設定を完了し、Microsoft Endpoint Manager admin center と同期する Configuration Manager コレクションを構成するには、Azure サブスクリプションに対するグローバル管理者のアクセス許可を持つアカウントが必要です。

## <a name="edr-profiles"></a>EDR プロファイル

次のプラットフォームとプロファイルで構成できる[設定を確認](../protect/endpoint-security-edr-profile-settings.md)してください。

**Intune** – Intune で管理するデバイスについては、以下がサポートされます。

- プラットフォーム:**Windows 10 以降** - Intune は Azure AD グループ内のデバイスにポリシーを展開します。
- プロファイル:**エンドポイントの検出と応答 (MDM)**

**Configuration Manager** " *(プレビュー中)* " - Configuration Manager で管理するデバイスについては、以下がサポートされます。

- プラットフォーム:**Windows 10 および Windows Server** - Configuration Manager は Configuration Manager コレクション内のデバイスにポリシーを展開します。
- プロファイル:**エンドポイントの検出と応答 (ConfigMgr) (プレビュー)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>EDR ポリシーをサポートするよう Configuration Manager を設定する

Configuration Manager デバイスに EDR ポリシーを展開する前に、以降のセクションで説明する構成を完了する必要があります。

これらの構成は Configuration Manager コンソール内で Configuration Manager の展開に対して行います。 Configuration Manager について詳しくない場合は、Configuration Manager 管理者と協力して、これらのタスクを完了するよう計画してください。  

以降のセクションでは、必要なタスクについて説明します。

1. [Configuration Manager の更新プログラムをインストールする](#task-1-install-the-update-for-configuration-manager)
2. [テナントのアタッチを有効にする](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [同期するコレクションを選択する](#task-3-select-collections-to-synchronize)
4. [Microsoft Defender ATP に対してコレクションを有効にする](#task-4-enable-collections-for-microsoft-defender-atp)

> [!TIP]
> Microsoft Defender ATP と Configuration Manager の併用方法の詳細については、Configuration Manager コンテンツの以下の記事を参照してください。
>
> - [Microsoft Endpoint Manager admin center を使用し構成マネージャー クライアントを Microsoft Defender ATP にオンボードする](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Endpoint Manager テナントのアタッチ: デバイスの同期とデバイスのアクション](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>タスク 1: Configuration Manager の更新プログラムをインストールする

Configuration Manager バージョン 2002 には、Microsoft Endpoint Manager admin center から展開するエンドポイントの検出と応答ポリシーの使用をサポートする更新プログラムが必要です。

**更新プログラムの詳細**:

- **Configuration Manager 2002 修正プログラム (KB4563473)**

この更新プログラムは、Configuration Manager 2002 の "*コンソール内の更新プログラム*" として見つかります。

この更新プログラムをインストールするには、Configuration Manager ドキュメントの[コンソール内の更新プログラムのインストール](../../configmgr/core/servers/manage/install-in-console-updates.md)に関するページのガイダンスに従ってください。

更新プログラムをインストールしたら、ここに戻って、Microsoft Endpoint Manager admin center の EDR ポリシーをサポートするための環境の構成を続行します。

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>タスク 2: テナントのアタッチを構成し、コレクションを同期する

共同管理を以前に有効にしている場合、テナントのアタッチは既に設定されているため、[タスク 3](#task-3-select-collections-to-synchronize) に進んでください。

テナントのアタッチでは、Microsoft Endpoint Manager admin center と同期する、Configuration Manager の展開のデバイスのコレクションを指定します。 コレクションが同期されたら、admin center を使用して、これらのデバイスに関する情報を確認し、Intune からこれらのデバイスに EDR ポリシーを展開します。  

テナントのアタッチ シナリオの詳細については、Configuration Manager コンテンツの[テナントのアタッチの有効化](../../configmgr/tenant-attach/device-sync-actions.md)に関するページを参照してください。

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>共同管理が有効になっていない場合にテナントのアタッチを有効にする

> [!TIP]
> Configuration Manager コンソールの**共同管理構成ウィザード**を使用して、テナントのアタッチを有効にしますが、共同管理を有効にする必要はありません。

共同管理を有効にすることを計画している場合は、続行する前に、共同管理、その前提条件、およびワークロードの管理方法について理解しておく必要があります。 Configuration Manager ドキュメントの「[共同管理とは](../../configmgr/comanage/overview.md)」を参照してください。

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。
2. リボンで **[共同管理の構成]** をクリックして、ウィザードを開きます。
3. **[テナントのオンボード]** ページで、ご利用の環境に対して **[AzurePublicCloud]** を選択します。 Azure Government クラウドはサポートされていません。
   1. **[サインイン]** をクリックします。 ご利用の "*全体管理者*" アカウントを使用してサインインします。

   2. **[テナントのオンボード]** ページで **[Upload to Microsoft Endpoint Manager admin center]\(Microsoft Endpoint Manager admin center にアップロードする\)** オプションを確実に選択します。

   3. **[共同管理のための自動クライアント登録を有効にする]** チェック ボックスをオフにします。

      このオプションを選択すると、ウィザードによって、共同管理の設定を完了するための追加のページが表示されます。 詳細については、Configuration Manager コンテンツの[共同管理の有効化](../../configmgr/comanage/how-to-enable.md)に関するページを参照してください。

     ![テナントのアタッチを構成する](./media/endpoint-security-edr-policy/tenant-onboarding.png)

4. **[次へ]** 、 **[はい]** の順にクリックして、 **[AAD アプリケーションの作成]** 通知を受け入れます。 このアクションにより、サービス プリンシパルがプロビジョニングされ、Microsoft Endpoint Manager admin center へのコレクションの同期を容易にするために Azure AD アプリケーション登録が作成されます。

5. **[Configure upload]\(アップロードを構成する\)** ページで、同期するコレクションを構成します。構成を 1 つまたはいくつかのデバイス コレクションに制限したり、 **[All my devices managed by Microsoft Endpoint Configuration Manager]\(Microsoft Endpoint Configuration Manager によって管理されているすべてのデバイス\)** に対して推奨されるデバイス アップロード設定を使用したりすることができます。

6. **[概要]** をクリックしてご自分の選択内容を確認して、 **[次へ]** をクリックします。

7. ウィザードが完了したら、 **[閉じる]** をクリックします。

   テナントのアタッチが構成され、選択したコレクションが Microsoft Endpoint Manager admin center に同期されるようになりました。

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>共同管理を使用する場合にテナントのアタッチを有効にする

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。

2. ご自分の共同管理設定を右クリックし、 **[プロパティ]** を選択します。

3. **[アップロードを構成する]** タブで、 **[Upload to Microsoft Endpoint Manager admin center]\(Microsoft Endpoint Manager 管理センターにアップロードする\)** を選択します。 **[適用]** をクリックします。
   - デバイスのアップロード用の既定の設定は、 **[Microsoft Endpoint Configuration Manager によって管理されているすべてのデバイス]** となります。 また、構成を 1 つまたはいくつかのデバイス コレクションに制限することもできます。

     ![共同管理の [プロパティ] タブを表示する](./media/endpoint-security-edr-policy/configure-upload.png)

4. メッセージが表示されたら、ご利用の "*全体管理者*" アカウントを使用してサインインします。

5. **[はい]** をクリックして、 **[AAD アプリケーションの作成]** 通知を受け入れます。 このアクションでは、サービス プリンシパルがプロビジョニングされ、同期を容易にするための Azure AD アプリケーション登録が作成されます。

6. 変更を行ったら、 **[OK]** をクリックして、共同管理プロパティを終了します。

   テナントのアタッチが構成され、選択したコレクションが Microsoft Endpoint Manager admin center に同期されるようになりました。

### <a name="task-3-select-collections-to-synchronize"></a>タスク 3: 同期するコレクションを選択する

テナントのアタッチが構成されている場合は、同期するコレクションを選択できます。コレクションをまだ同期していない場合や、同期するコレクションを再構成する必要がある場合は、Configuration Manager コンソールで共同管理のプロパティを編集して、その操作を行うことができます。

#### <a name="select-collections"></a>コレクションを選択する

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。

2. ご自分の共同管理設定を右クリックし、 **[プロパティ]** を選択します。

3. **[アップロードを構成する]** タブで、 **[Upload to Microsoft Endpoint Manager admin center]\(Microsoft Endpoint Manager 管理センターにアップロードする\)** を選択します。 **[適用]** をクリックします。

   デバイスのアップロード用の既定の設定は、 **[Microsoft Endpoint Configuration Manager によって管理されているすべてのデバイス]** となります。 また、構成を 1 つまたはいくつかのデバイス コレクションに制限することもできます。

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>タスク 4: Microsoft Defender ATP に対してコレクションを有効にする

Microsoft Endpoint Manager admin center に同期するようにコレクションを構成した後も、それらのコレクションをオンボードおよび Microsoft Defender ATP ポリシーの対象として有効にする必要があります。  そのためには、Configuration Manager コンソールで各コレクションのプロパティを編集します。

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Advanced Threat Protection で使用できるようにコレクションを有効にする

1. 最上位サイトに接続されている Configuration Manager コンソールで、Microsoft Endpoint Manager admin center に同期するデバイス コレクションを右クリックし、 **[プロパティ]** を選択します。

2. **[Cloud Sync]\(クラウド同期\)** タブで、**このコレクションを使用可能にして Intune で Microsoft Defender ATP ポリシーを割り当てる**オプションを有効にします。

   - Configuration Manager 階層がテナントにアタッチされていない場合は、このオプションを選択することはできません。
  
   ![クラウドの同期を構成する](./media/endpoint-security-edr-policy/cloud-sync.png)

3. **[OK]** を選択して構成を保存します。

   これで、このコレクション内のデバイスが Microsoft Defender ATP ポリシーを受け取ることができるようになりました。

## <a name="create-and-deploy-edr-policies"></a>EDR ポリシーを作成して展開する

Microsoft Defender ATP サブスクリプションが Intune と統合されている場合は、EDR ポリシーを作成して展開できます。 作成できる EDR ポリシーには、2 つの異なる種類があります。 1 つ目のポリシーの種類は、MDM を通じて Intune で管理するデバイス向けです。 2 つ目の種類は、Configuration Manager で管理するデバイス向けです。

新しい EDR ポリシーの作成時に、ポリシーのプラットフォームを選択する際、作成するポリシーの種類を選択します。

Configuration Manager によって管理されるデバイスにポリシーを展開する前に、Microsoft Endpoint Manager admin center の [EDR ポリシーをサポートするように Configuration Manager を設定](#set-up-configuration-manager-to-support-edr-policy)する必要があります。

### <a name="create-edr-policies"></a>EDR ポリシーを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[エンドポイントの検出と応答]**  >  **[ポリシーの作成]** の順に選択します。

3. ポリシーのプラットフォームとプロファイルを選択します。 次の情報はオプションを示しています。

   - Intune - Intune は Azure AD グループ内のデバイスにポリシーを展開します。 ポリシーを作成するときに、次を選択します。
     - プラットフォーム:**Windows 10 以降**
     - プロファイル:**エンドポイントの検出と応答 (MDM)**

   - Configuration Manager - Configuration Manager は Configuration Manager コレクション内のデバイスにポリシーを展開します。 ポリシーを作成するときに、次を選択します。
     - プラットフォーム:**Windows 10 および Windows Server**
     - プロファイル:**エンドポイントの検出と応答 (ConfigMgr) (プレビュー)**

4. **[作成]** を選択します。

5. **[基本]** ページで、プロファイルに名前と説明を入力して、 **[次へ]** を選択します。

6. **[構成設定]** ページで、このプロファイルで管理する設定を構成します。 オンボード パッケージは自動的に含まれ、構成することはできません。

   設定の構成が完了したら、 **[次へ]** を選択します。

7. "*この手順は、**エンドポイントの検出と応答 (MDM)** プロファイルにのみ適用されます*"。  

   **[スコープ タグ]** ページで **[スコープ タグを選択]** を選択し、 *[タグを選択する]* ペインを開いて、プロファイルにスコープ タグを割り当てます。
  
   **[次へ]** を選択して続行します。

8. **[割り当て]** ページで、このプロファイルを受け取るグループまたはコレクションを選択します。 選択肢は、選択したプラットフォームとプロファイルによって異なります。

   - Intune の場合は、Azure AD のグループを選択します。
   - Configuration Manager の場合は、Microsoft Endpoint Manager admin center に同期し、Microsoft Defender ATP ポリシーが有効になっている Configuration Manager のコレクションを選択します。

   この時点ではグループまたはコレクションを割り当てないことを選択し、後でポリシーを編集して割り当てを追加することもできます。

   続行する準備ができたら、 **[次へ]** を選択します。

9. **[確認および作成]** ページで、完了したら、 **[作成]** を選択します。

   作成したプロファイルのポリシーの種類を選択すると、新しいプロファイルが一覧に表示されます。

## <a name="edr-policy-reports"></a>EDR ポリシー レポート

Microsoft Endpoint Manager admin center では、展開する EDR ポリシーの詳細を表示できます。 詳細を表示するには、 **[エンドポイント セキュリティ]**  >  **[Endpoint deployment and response]\(エンドポイントの展開と応答\)** の順に移動し、コンプライアンスの詳細を表示するポリシーを選択します。

- **Windows 10 以降**のプラットフォーム (Intune) を対象とするポリシーの場合、ポリシーへのコンプライアンスの概要が表示されます。 また、グラフを選択して、ポリシーを受け取ったデバイスの一覧を表示し、個々のデバイスにドリルインして詳細を確認することもできます。

- **Windows 10 および Windows Server** プラットフォーム (Configuration Manager) を対象とするポリシーの場合、ポリシーへのコンプライアンスの概要は表示されますが、ドリルインして詳細を表示することはできません。 表示が制限されているのは、Configuration Manager デバイスへのポリシーの展開を管理しているのは Configuration Manager であり、admin center が Configuration Manager から受け取る状態の詳細が限られているからです。

両方のプラットフォームとプロファイルで構成できる[設定を確認](../protect/endpoint-security-edr-profile-settings.md)してください。

## <a name="next-steps"></a>次のステップ

- [エンドポイント セキュリティ ポリシーを構成する](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
- Microsoft Defender ATP ドキュメントの[エンドポイントの検出と応答](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response)に関するページで詳細を確認する。
