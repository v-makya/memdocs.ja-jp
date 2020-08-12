---
title: Microsoft Endpoint Manager テナントのアタッチ
titleSuffix: Configuration Manager
description: Configuration Manager デバイスをクラウドサービスにアップロードし、管理センターからアクションを実行します。
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 784a287176066ce34c3499ecdc91a450e2d6160c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127547"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Microsoft Endpoint Manager テナントの接続: デバイスの同期とデバイスの操作
<!--3555758 live 3/4/2020-->
*適用対象:Configuration Manager (Current Branch)*

Microsoft Endpoint Manager は、すべてのデバイスを管理するための統合ソリューションです。 Microsoft は、Configuration Manager と Intune を、**Microsoft Endpoint Manager 管理センター**と呼ばれる 1 つのコンソールに統合します。

Configuration Manager バージョン2002以降では、Configuration Manager デバイスをクラウドサービスにアップロードし、管理センターの [**デバイス**] ブレードから操作を実行できます。

## <a name="prerequisites"></a>前提条件

- この変更を適用するときにサインインするための*グローバル管理者*であるアカウント。 詳細については、「 [Azure Active Directory (Azure AD) 管理者ロール](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles)」を参照してください。
   - オンボードすると、Azure AD テナントにサードパーティのアプリとファーストパーティのサービスプリンシパルが作成されます。
- Azure パブリッククラウド環境。
- デバイスアクションをトリガーするユーザーアカウントには、次の前提条件があります。
   - では、 [Azure Active Directory ユーザー探索](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)と[Active Directory ユーザー探索](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)の両方が検出されました。
      - つまり、ユーザーアカウントは、Azure AD 内の同期されたユーザーオブジェクトである必要があります。
   - Microsoft Endpoint Manager 管理センターの [**リモートタスク**] の下にある**Configuration Manager アクションの開始**] アクセス許可。


## <a name="internet-endpoints"></a>インターネットエンドポイント

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a>共同管理が既に有効になっている場合にデバイスのアップロードを有効にする

共同管理を現在有効にしている場合は、共同管理プロパティを使用してデバイスのアップロードを有効にします。 共同管理がまだ有効になっていない場合[は、**共同管理の構成**ウィザードを使用](#bkmk_config)して、代わりにデバイスのアップロードを有効にします。

共同管理が既に有効になっている場合は、次の手順を使用して共同管理のプロパティを編集し、デバイスのアップロードを有効にします。

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。
1. リボンで、共同管理運用ポリシーの [**プロパティ**] を選択します。
1. **[アップロードを構成する]** タブで、 **[Upload to Microsoft Endpoint Manager admin center]\(Microsoft Endpoint Manager 管理センターにアップロードする\)** を選択します。 **[適用]** を選択します。
   - デバイスのアップロード用の既定の設定は、 **[Microsoft Endpoint Configuration Manager によって管理されているすべてのデバイス]** となります。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。
1. エンドポイント[分析](../../analytics/overview.md)でエンドユーザーエクスペリエンスを最適化するための洞察も得たい場合は、 **Microsoft endpoint Manager にアップロードされたデバイスのエンドポイント分析を有効**にするオプションをオンにします。

   [![Microsoft Endpoint Manager 管理センターにデバイスをアップロードする](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. メッセージが表示されたら、ご利用の "*全体管理者*" アカウントを使用してサインインします。
1. [**はい]** を選択して、 **AAD アプリケーションの作成**通知を受け入れます。 このアクションでは、サービス プリンシパルがプロビジョニングされ、同期を容易にするための Azure AD アプリケーション登録が作成されます。
1. 変更が完了したら、 **[OK]** を選択して共同管理のプロパティを終了します。


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a>共同管理が有効になっていないときにデバイスのアップロードを有効にする

共同管理が有効になっていない場合は、**共同管理の構成**ウィザードを使用してデバイスのアップロードを有効にします。 共同管理の自動登録を有効にしたり、ワークロードを Intune に切り替えたりすることなく、デバイスをアップロードできます。 [**クライアント**] 列に **[はい]** が設定されている Configuration Manager によって管理されているすべてのデバイスがアップロードされます。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。 共同管理が環境で既に有効になっている場合は、[共同管理プロパティを編集](#bkmk_edit)して、代わりにデバイスのアップロードを有効にします。

共同管理が有効になっていない場合は、次の手順に従ってデバイスのアップロードを有効にします。

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。
1. リボンで [**共同管理の構成**] を選択して、ウィザードを開きます。
1. **[テナントのオンボード]** ページで、ご利用の環境に対して **[AzurePublicCloud]** を選択します。 Azure Government クラウドと Azure 中国の21Vianet はサポートされていません。
1. **[サインイン]** を選択します。 ご利用の "*全体管理者*" アカウントを使用してサインインします。
1. [**テナントのオンボード**] ページで [ **Microsoft Endpoint Manager 管理センターにアップロードする**] オプションが選択されていることを確認します。
   - 今すぐ共同管理を有効にしない場合は、[**共同管理の自動クライアント登録を有効**にする] チェックボックスがオンになっていないことを確認してください。 共同管理を有効にする場合は、オプションを選択します。
   - デバイスのアップロードと共に共同管理を有効にすると、ウィザードに追加のページが表示されます。 詳しくは、[共同管理の有効化](../comanage/how-to-enable.md)に関する記事をご覧ください。

   [![共同管理構成ウィザード](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. [**次へ**] をクリックし、[**はい]** をクリックして、 **AAD アプリケーションの作成**通知を受け入れます。 このアクションでは、サービス プリンシパルがプロビジョニングされ、同期を容易にするための Azure AD アプリケーション登録が作成されます。
     - 必要に応じて、テナントの接続のオンボード中に以前に作成した Azure AD アプリケーションをインポートできます (バージョン2006以降)。 詳細については、「以前に作成した[Azure AD アプリケーションをインポートする](#bkmk_aad_app)」を参照してください。
1. [**アップロードの構成**] ページで、 **Microsoft エンドポイント Configuration Manager によって管理**されるすべてのデバイスについて、推奨されるデバイスのアップロード設定を選択します。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。
1. エンドポイント[分析](../../analytics/overview.md)でエンドユーザーエクスペリエンスを最適化するための洞察も得たい場合は、 **Microsoft endpoint Manager にアップロードされたデバイスのエンドポイント分析を有効**にするオプションをオンにします。
1. [**概要**] を選択して選択内容を確認し、[**次へ**] を選択します。
1. ウィザードが完了したら、[**閉じる**] を選択します。  

## <a name="perform-device-actions"></a>デバイスの操作を実行する

1. ブラウザーで、に移動します。`endpoint.microsoft.com`
1. [**デバイス**]、[**すべてのデバイス**] の順に選択して、アップロードしたデバイスを表示します。 アップロードされたデバイスの [**管理者の管理**列に**ConfigMgr**が表示されます。
   [![Microsoft Endpoint Manager 管理センター内のすべてのデバイス](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. [**概要**] ページを読み込むデバイスを選択します。
1. 次のいずれかの操作を選択します。
   - **コンピューター ポリシーの同期**
   - **ユーザー ポリシーの同期**
   - **アプリの評価サイクル**

   [![Microsoft Endpoint Manager 管理センターのデバイスの概要](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a>以前に作成した Azure AD アプリケーションをインポートする (省略可能)
<!--6479246-->
*(バージョン2006で導入)*

[新しいオンボード](#bkmk_config)中に、管理者はテナントの接続のオンボード時に以前に作成したアプリケーションを指定できます。 複数の階層で Azure AD アプリケーションを共有したり再利用したりしないでください。 複数の階層がある場合は、それぞれに対して個別の Azure AD アプリケーションを作成します。

**[Co-management Configuration Wizard]\(共同管理の構成ウィザード\)** の **[テナントのオンボード]** ページから、 **[Optionally import a separate web app to synchronize Configuration Manager client data to Microsoft Endpoint Manager admin center]\(オプションで別の Web アプリをインポートして、Configuration Manager クライアント データを Microsoft エンドポイント マネージャー管理センターに同期します\)** を選択します。 このオプションを選択すると、Azure AD アプリに関する次の情報を指定するように求められます。

- Azure AD テナント名
- Azure AD テナント ID
- アプリケーション名
- クライアント ID
- 秘密鍵
- 秘密鍵の有効期限
- アプリ ID URI

### <a name="azure-ad-application-permissions-and-configuration"></a>アプリケーションのアクセス許可と構成の Azure AD

テナントの接続のオンボード時に以前に作成したアプリケーションを使用するには、次のアクセス許可が必要です。

- Configuration Manager のマイクロサービスのアクセス許可:
   - CmCollectionData。読み取り
   - CmCollectionData. 書き込み

- Microsoft Graph のアクセス許可:
   - Directory. Read. すべての[アプリケーションのアクセス許可](https://docs.microsoft.com/graph/permissions-reference#application-permissions)
   - Directory. Read. すべての委任された[ディレクトリのアクセス許可](https://docs.microsoft.com/graph/permissions-reference#directory-permissions)

- Azure AD アプリケーションに対して [**テナントの管理者の同意を付与する**。 詳細については、「[アプリの登録で管理者の同意を付与](https://docs.microsoft.com/azure/active-directory/manage-apps/grant-admin-consent)する」を参照してください。

- インポートされたアプリケーションは、次のように構成する必要があります。
   - **この組織ディレクトリのアカウントにのみ**登録されています。 詳細については、「[アプリケーションにアクセスできるユーザーを変更する](https://docs.microsoft.com/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application)」を参照してください。
   -  有効なアプリケーション ID URI とシークレットがある



## <a name="next-steps"></a>次のステップ

- [Configuration Manager デバイスをエンドポイント分析に登録する](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- テナントアタッチログファイルの詳細については、「[テナント接続のトラブルシューティング](troubleshoot.md)」を参照してください。
