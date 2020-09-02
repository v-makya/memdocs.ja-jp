---
title: テナントがアタッチされた Configuration Manager デバイスで Intune ポリシーを使用する | Microsoft Docs
description: サポートされているポリシーを Microsoft Intune からそれらのデバイスに展開できるように、Configuration Manager デバイスの Microsoft Endpoint Manager admin center へのテナントのアタッチを構成します。
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
ms.openlocfilehash: 5c3d5bd14efddc74e1898f374bbaac2aa962ebf7
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193667"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>Intune のエンドポイント セキュリティ ポリシーをサポートするようにテナントのアタッチを構成する

Configuration Manager のテナントのアタッチ シナリオを使用する場合、Intune から Configuration Manager で管理するデバイスにエンドポイント セキュリティ ポリシーを展開できます。 このシナリオを使用するには、まず Configuration Manager のテナントのアタッチを構成し、Configuration Manager からのデバイスのコレクションを Intune で使用できるようにする必要があります。 コレクションの使用を有効にしたら、Microsoft Endpoint Manager admin center を使用してポリシーを作成および展開します。

テナントにアタッチされている Configuration Manager デバイスでは、次のポリシーの種類がサポートされています。

- エンドポイント セキュリティのウイルス対策ポリシー
- エンドポイント セキュリティのエンドポイント検出と応答ポリシー

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>テナントのアタッチに Intune ポリシーを使用するための要件

Configuration Manager デバイスに対する Intune エンドポイントのセキュリティ ポリシーの使用をサポートするには、Configuration Manager 環境で次の構成が必要です。 この記事では、[構成のガイダンス](#set-up-configuration-manager-to-support-intune-policies)を示しています。

### <a name="general-requirements-for-tenant-attach"></a>テナントのアタッチに関する一般的な要件

- **テナントのアタッチの構成** - "*テナントのアタッチ*" のシナリオを使用すると、Configuration Manager のデバイスのコレクションを Microsoft Endpoint Manager admin center に同期できます。 そうすると、admin center を使用して、サポートされるポリシーをそれらのコレクションに展開することができます。

  テナントのアタッチは、多くの場合、共同管理と共に構成しますが、テナントのアタッチを単独で構成することもできます。

- **Configuration Manager コレクションの同期** – テナントのアタッチを構成するときに、Microsoft Endpoint Manager admin center と同期する Configuration Manager デバイス コレクションを選択できます。 後で戻って、同期するデバイス コレクションを変更することもできます。Configuration Manager デバイスのサポートされるポリシーは、同期しているコレクションにのみ割り当てることができます。

  同期するコレクションを選択した後は、それらを Intune のエンドポイント セキュリティ ポリシーで使用できるようにする必要があります。

- **Azure AD へのアクセス許可** - テナントのアタッチの設定を完了するには、Azure サブスクリプションに対して全体管理者アクセス許可を持つアカウントが必要です。

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Intune エンドポイント セキュリティ ポリシーの具体的な要件

- **ウイルス対策ポリシー** (*プレビュー*):

  - **Configuration Manager** - 次の環境がサポートされています。

    - **Configuration Manager Current Branch バージョン 2006 以降** - Intune ウイルス対策ポリシーのサポートはこの Current Branch バージョンで追加されました。
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - **Microsoft Defender Advanced Threat Protection のテナント** - Microsoft Defender ATP テナントを Microsoft Endpoint Manager テナント (Intune サブスクリプション) と統合する必要があります。  Intune ドキュメントの [Microsoft Defender ATP の使用](advanced-threat-protection.md)に関するページを参照してください。

- **エンドポイントの検出と応答ポリシー**:

  - **Configuration Manager** - 次の環境がサポートされています。

    - **Configuration Manager Technical Preview 2003 以降** - Intune エンドポイントの検出と応答ポリシーのサポートは、Technical Preview バージョン 2003 で追加されました。

    - **Configuration Manager Current Branch バージョン 2002 以降** - バージョン 2002 の Configuration Manager を使用する場合は、コンソール内更新プログラム **Configuration Manager 2002 Hotfix (KB4563473)** をインストールする必要があります。 この更新プログラムをインストールすると、Configuration Manager 2002 でエンドポイント セキュリティ ポリシーを使用できるようになります。

  - **Microsoft Defender Advanced Threat Protection のテナント** - Microsoft Defender ATP テナントを Microsoft Endpoint Manager テナント (Intune サブスクリプション) と統合する必要があります。  Intune ドキュメントの [Microsoft Defender ATP の使用](advanced-threat-protection.md)に関するページを参照してください。

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>Intune ポリシーをサポートするように Configuration Manager を設定する

Configuration Manager デバイスに Intune ポリシーを展開する前に、以降のセクションで説明する構成を完了する必要があります。 これらの構成を使用すると、Configuration Manager デバイスに Microsoft Defender ATP をオンボードし、Intune ポリシーと連携できるようになります。

次のタスクは、Configuration Manager コンソールで完了します。 Configuration Manager について詳しくない場合は、Configuration Manager 管理者と協力して、これらのタスクを完了してください。

1. [Configuration Manager の更新プログラムをインストールする](#task-1-install-the-update-for-configuration-manager)
2. [テナントのアタッチを有効にする](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [同期するコレクションを選択する](#task-3-select-collections-to-synchronize)
4. [Intune ポリシーをサポートするコレクションを有効にする](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> Microsoft Defender ATP と Configuration Manager の併用方法の詳細については、Configuration Manager コンテンツの以下の記事を参照してください。
>
> - [Microsoft Endpoint Manager admin center を使用し構成マネージャー クライアントを Microsoft Defender ATP にオンボードする](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Endpoint Manager テナントのアタッチ: デバイスの同期とデバイスのアクション](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>タスク 1: Configuration Manager の更新プログラムをインストールする

Configuration Manager Current Branch バージョン 2002 を使用する場合は、Microsoft Endpoint Manager admin center から、展開するエンドポイント セキュリティ ポリシーのサポートを追加する次のコンソール内更新プログラムをインストールします。

**更新プログラムの詳細**:

- **Configuration Manager 2002 修正プログラム (KB4563473)**

この更新プログラムをインストールするには、Configuration Manager ドキュメントの[コンソール内の更新プログラムのインストール](../../configmgr/core/servers/manage/install-in-console-updates.md)に関するページのガイダンスに従ってください。

更新プログラムをインストールしたら、ここに戻って、Microsoft Endpoint Manager admin center のエンドポイント セキュリティ ポリシーをサポートするための環境の構成を続行します。

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>タスク 2: テナントのアタッチを構成し、コレクションを同期する

テナントのアタッチでは、Microsoft Endpoint Manager admin center と同期する、Configuration Manager の展開のデバイスのコレクションを指定します。 コレクションが同期されたら、admin center を使用して、これらのデバイスに関する情報を確認し、Intune からこれらのデバイスにエンドポイント セキュリティ ポリシーを展開します。

テナントのアタッチ シナリオの詳細については、Configuration Manager コンテンツの[テナントのアタッチの有効化](../../configmgr/tenant-attach/device-sync-actions.md)に関するページを参照してください。

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>共同管理が有効になっていない場合にテナントのアタッチを有効にする

> [!TIP]
> Configuration Manager コンソールの**共同管理構成ウィザード**を使用して、テナントのアタッチを有効にしますが、共同管理を有効にする必要はありません。
>
> 共同管理を有効にすることを計画している場合は、続行する前に、共同管理、その前提条件、およびワークロードの管理方法について理解しておく必要があります。 Configuration Manager ドキュメントの「[共同管理とは](../../configmgr/comanage/overview.md)」を参照してください。

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。
2. リボンで **[共同管理の構成]** をクリックして、ウィザードを開きます。
3. **[テナントのオンボード]** ページで、ご利用の環境に対して **[AzurePublicCloud]** を選択します。 Azure Government クラウドはサポートされていません。
   1. **[サインイン]** をクリックします。 ご利用の "*全体管理者*" アカウントを使用してサインインします。

   2. **[テナントのオンボード]** ページで **[Upload to Microsoft Endpoint Manager admin center]\(Microsoft Endpoint Manager admin center にアップロードする\)** オプションを確実に選択します。

   3. **[共同管理のための自動クライアント登録を有効にする]** チェック ボックスをオフにします。

      このオプションを選択すると、ウィザードによって、共同管理の設定を完了するための追加のページが表示されます。 詳細については、Configuration Manager コンテンツの[共同管理の有効化](../../configmgr/comanage/how-to-enable.md)に関するページを参照してください。

     ![テナントのアタッチを構成する](./media/tenant-attach-intune/tenant-onboarding.png)

4. **[次へ]** 、 **[はい]** の順にクリックして、 **[AAD アプリケーションの作成]** 通知を受け入れます。 このアクションにより、サービス プリンシパルがプロビジョニングされ、Microsoft Endpoint Manager admin center へのコレクションの同期を容易にするために Azure AD アプリケーション登録が作成されます。

5. **[Configure upload]\(アップロードを構成する\)** ページで、同期するコレクションを構成します。構成を 1 つまたはいくつかのデバイス コレクションに制限したり、 **[All my devices managed by Microsoft Endpoint Configuration Manager]\(Microsoft Endpoint Configuration Manager によって管理されているすべてのデバイス\)** に対して推奨されるデバイス アップロード設定を使用したりすることができます。

   > [!TIP]
   > ここでコレクションの選択をスキップし、後で次のタスクであるタスク 3 の情報を使用して、Microsoft Endpoint Manager admin center と同期するコレクションを構成することができます。

6. **[概要]** をクリックしてご自分の選択内容を確認して、 **[次へ]** をクリックします。

7. ウィザードが完了したら、 **[閉じる]** をクリックします。

   テナントのアタッチが構成され、選択したコレクションが Microsoft Endpoint Manager admin center に同期されるようになりました。

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>共同管理を既に使用している場合にテナントのアタッチを有効にする

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。

2. ご自分の共同管理設定を右クリックし、 **[プロパティ]** を選択します。

3. **[アップロードを構成する]** タブで、 **[Upload to Microsoft Endpoint Manager admin center]\(Microsoft Endpoint Manager 管理センターにアップロードする\)** を選択します。 **[適用]** をクリックします。

   デバイスのアップロード用の既定の設定は、 **[Microsoft Endpoint Configuration Manager によって管理されているすべてのデバイス]** となります。 また、構成を 1 つまたはいくつかのデバイス コレクションに制限することもできます。

   ![共同管理の [プロパティ] タブを表示する](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > ここでコレクションの選択をスキップし、後で次のタスクであるタスク 3 の情報を使用して、Microsoft Endpoint Manager admin center と同期するコレクションを構成することができます。

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

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>タスク 4: エンドポイント セキュリティ ポリシーのコレクションを有効にする

Microsoft Endpoint Manager admin center と同期するようにコレクションを構成したら、それらのコレクションをエンドポイントのセキュリティ ポリシーで使用できるようにします。 デバイスのコレクションを Intune のエンドポイント セキュリティ ポリシーと連携できるようにすると、それらのコレクション内のデバイスに Microsoft Defender ATP がオンボードされるように構成されます。

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>エンドポイント セキュリティ ポリシーで使用するコレクションを有効にする

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>次のステップ

- "*ウイルス対策*" と "*エンドポイントの検出と応答*" のために[エンドポイント セキュリティ ポリシー](endpoint-security-policy.md#create-an-endpoint-security-policy)を構成します。

- Microsoft Defender ATP ドキュメントの[エンドポイントの検出と応答](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response)に関するページで詳細を確認する。