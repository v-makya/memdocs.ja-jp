---
title: Microsoft Intune でエンドポイント セキュリティ ポリシーを使用してエンドポイントの検出と応答の設定を管理する | Microsoft Docs
description: Microsoft Endpoint Manager でエンドポイント セキュリティのエンドポイントの検出と応答ポリシーを使用して、管理するデバイスのポリシーを構成および展開します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: cba7b357dfae0c9dae06e8a21ddd0583fd96bcae
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820529"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのエンドポイントの検出と応答ポリシー

Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) と Intune を統合すると、エンドポイントの検出と応答 (EDR) のエンドポイント セキュリティ ポリシーを使用して、EDR の設定を管理したり、デバイスを Microsoft Defender ATP にオンボードしたりできます。

Microsoft Defender ATP のエンドポイントの検出と応答機能により、ほぼリアルタイムの実用的で高度な攻撃検出が可能になります。 セキュリティ アナリストは、アラートの優先度を効果的に設定し、侵害の範囲全体を把握し、脅威を修復するための応答アクションを実行できます。

EDR ポリシーには、EDR の設定を管理するための、プラットフォーム固有のプロファイルが含まれています。 プロファイルには、Microsoft Defender ATP の "*オンボード パッケージ*" が自動的に含まれます。 オンボード パッケージには、Microsoft Defender ATP と連携するためのデバイスの構成方法が定義されています。 デバイスをオンボードすると、そのデバイスからの脅威データの使用を開始できます。

EDR ポリシーは、Intune で管理する Azure Active Directory (Azure AD) のデバイス グループと、Configuration Manager で管理するオンプレミス デバイスのコレクション (Windows サーバーを含む) に展開されます。 異なる管理パスの EDR ポリシーには、異なるオンボード パッケージが必要です。 そのため、管理するデバイスの種類ごとに個別の EDR ポリシーを作成します。

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) の **[エンドポイント セキュリティ]** ノードにある *[管理]* で、EDR のためのエンドポイント セキュリティ ポリシーを見つけます。

[エンドポイントの検出と応答プロファイルの設定](endpoint-security-edr-profile-settings.md)を確認してください。

## <a name="prerequisites-for-edr-policies"></a>EDR ポリシーの前提条件

**全般**:

- **Microsoft Defender Advanced Threat Protection のテナント** – EDR ポリシーを作成する前に、Microsoft Defender ATP テナントを Microsoft Endpoint Manager テナント (Intune サブスクリプション) と統合する必要があります。 Intune ドキュメントの [Microsoft Defender ATP の使用](advanced-threat-protection.md)に関するページを参照してください。

**Configuration Manager クライアントのサポート**:

- **Configuration Manager デバイスのテナントのアタッチを設定する** - Configuration Manager によって管理されるデバイスへの EDR ポリシーの展開をサポートするには、*テナントのアタッチ*を構成します。 これには、Intune からのエンドポイント セキュリティ ポリシーをサポートするための Configuration Manager デバイス コレクションの構成が含まれます。

  Configuration Manager コレクションの Microsoft Endpoint Manager admin center への同期や、エンドポイント セキュリティ ポリシーと連携できるようにするテナントのアタッチを設定するには、[エンドポイント保護ポリシーをサポートするようにテナントのアタッチを構成する](../protect/tenant-attach-intune.md)方法に関するページを参照してください。

## <a name="edr-profiles"></a>EDR プロファイル

次のプラットフォームとプロファイルで構成できる[設定を確認](endpoint-security-edr-profile-settings.md)してください。

**Intune** – Intune で管理するデバイスについては、以下がサポートされます。

- プラットフォーム:**Windows 10 以降** - Intune は Azure AD グループ内のデバイスにポリシーを展開します。
- プロファイル:**エンドポイントの検出と応答 (MDM)**

**Configuration Manager** - Configuration Manager で管理するデバイスについては、以下がサポートされます。

- プラットフォーム:**Windows 10 および Windows Server (ConfigMgr)** - Configuration Manager は Configuration Manager コレクション内のデバイスにポリシーを展開します。
- プロファイル:**エンドポイントの検出と応答 (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>EDR ポリシーをサポートするよう Configuration Manager を設定する

Configuration Manager デバイスに EDR ポリシーを展開する前に、以降のセクションで説明する構成を完了する必要があります。

これらの構成は Configuration Manager コンソール内で Configuration Manager の展開に対して行います。 Configuration Manager について詳しくない場合は、Configuration Manager 管理者と協力して、これらのタスクを完了するよう計画してください。  

以降のセクションでは、必要なタスクについて説明します。

1. [Configuration Manager の更新プログラムをインストールする](#task-1-install-the-update-for-configuration-manager)
2. [テナントのアタッチを有効にする](#task-2-configure-tenant-attach-and-synchronize-collections)  

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

Intune で管理するデバイスについては、以下がサポートされます。

- プラットフォーム:**Windows 10 以降** - Intune は Azure AD グループ内のデバイスにポリシーを展開します。
  - プロファイル:**エンドポイントの検出と応答 (MDM)**

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Configuration Manager によって管理されるデバイス " *(プレビュー段階)* "

Configuration Manager で管理するデバイスについては、"*テナントのアタッチ*" シナリオを通じて以下がサポートされます。

- プラットフォーム:**Windows 10 および Windows Server (ConfigMgr)** - Configuration Manager は Configuration Manager コレクション内のデバイスにポリシーを展開します。
  - プロファイル:**エンドポイントの検出と応答 (ConfigMgr) (プレビュー)**

## <a name="create-and-deploy-edr-policies"></a>EDR ポリシーを作成して展開する

Microsoft Defender ATP サブスクリプションを Intune と統合している場合は、EDR ポリシーを作成して展開できます。 作成できる EDR ポリシーには、2 つの異なる種類があります。 1 つ目のポリシーの種類は、MDM を通じて Intune で管理するデバイス向けです。 2 つ目の種類は、Configuration Manager で管理するデバイス向けです。

ポリシーのプラットフォームを選択することにより、新しい EDR ポリシーの構成時に作成するポリシーの種類を選択します。

Configuration Manager によって管理されるデバイスにポリシーを展開する前に、Microsoft Endpoint Manager admin center の EDR ポリシーをサポートするように Configuration Manager を設定する必要があります。 [エンドポイント保護ポリシーをサポートするようにテナントのアタッチを構成する](../protect/tenant-attach-intune.md)方法に関するページを参照してください。


### <a name="create-edr-policies"></a>EDR ポリシーを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[エンドポイントの検出と応答]**  >  **[ポリシーの作成]** の順に選択します。

3. ポリシーのプラットフォームとプロファイルを選択します。 次の情報はオプションを示しています。

   - Intune - Intune は Azure AD グループ内のデバイスにポリシーを展開します。 ポリシーを作成するときに、次を選択します。
     - プラットフォーム:**Windows 10 以降**
     - プロファイル:**エンドポイントの検出と応答 (MDM)**

   - Configuration Manager - Configuration Manager は Configuration Manager コレクション内のデバイスにポリシーを展開します。 ポリシーを作成するときに、次を選択します。
     - プラットフォーム:**Windows 10 および Windows Server (ConfigMgr)**
     - プロファイル:**エンドポイントの検出と応答 (ConfigMgr)**

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

  **[ATP センサーがあるデバイス]** のグラフには、**Windows 10 以降**のプロファイルを使用して Microsoft Defender ATP に正常にオンボードしたデバイスのみが表示されます。 このグラフにデバイスを完全に表現できるようにするには、オンボード プロファイルをすべてのデバイスに展開します。 グループ ポリシーや PowerShell のように、外部から Microsoft Defender ATP にオンボードするデバイスは、**ATP センサーのないデバイス**としてカウントされます。

- **Windows 10 および Windows Server (ConfigMgr)** プラットフォーム (Configuration Manager) を対象とするポリシーの場合、ポリシーへのコンプライアンスの概要は表示されますが、ドリルインして詳細を表示することはできません。 表示が制限されているのは、Configuration Manager デバイスへのポリシーの展開を管理しているのは Configuration Manager であり、admin center が Configuration Manager から受け取る状態の詳細が限られているからです。

両方のプラットフォームとプロファイルで構成できる[設定を確認](endpoint-security-edr-profile-settings.md)してください。

## <a name="next-steps"></a>次のステップ

- [エンドポイント セキュリティ ポリシーを構成する](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Microsoft Defender ATP ドキュメントの[エンドポイントの検出と応答](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response)に関するページで詳細を確認する。
