---
title: Microsoft Endpoint Manager テナントのアタッチ
titleSuffix: Configuration Manager
description: Configuration Manager デバイスをクラウドサービスにアップロードし、管理センターからアクションを実行します。
ms.date: 07/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a9e97c74e4825dc49ce628b3ae176c55f4288966
ms.sourcegitcommit: 3806a1850813b7a179d703e002bcc5c7eb1cb621
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86210291"
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

- `https://aka.ms/configmgrgateway`
- `https://*.manage.microsoft.com` <!--7424742-->

## <a name="enable-device-upload"></a>デバイスのアップロードを有効にする

- 共同管理を現在有効にしている場合は、[共同管理プロパティを編集](#bkmk_edit)して、デバイスのアップロードを有効にします。
- 共同管理が有効になっていない場合は、 [**共同管理の構成**ウィザードを使用](#bkmk_config)してデバイスのアップロードを有効にします。
   - 共同管理の自動登録を有効にしたり、ワークロードを Intune に切り替えたりすることなく、デバイスをアップロードできます。
- [**クライアント**] 列に **[はい]** が設定されている Configuration Manager によって管理されているすべてのデバイスがアップロードされます。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>共同管理プロパティを編集してデバイスのアップロードを有効にする

共同管理を現在有効にしている場合は、次の手順を使用して共同管理のプロパティを編集し、デバイスのアップロードを有効にします。

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。
1. ご自分の共同管理設定を右クリックし、 **[プロパティ]** を選択します。
1. **[アップロードを構成する]** タブで、 **[Upload to Microsoft Endpoint Manager admin center]\(Microsoft Endpoint Manager 管理センターにアップロードする\)** を選択します。 **[適用]** をクリックします。
   - デバイスのアップロード用の既定の設定は、 **[Microsoft Endpoint Configuration Manager によって管理されているすべてのデバイス]** となります。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。
1. エンドポイント[分析](../../analytics/overview.md)でエンドユーザーエクスペリエンスを最適化するための洞察も得たい場合は、 **Microsoft endpoint Manager にアップロードされたデバイスのエンドポイント分析を有効**にするオプションをオンにします。

   [![Microsoft Endpoint Manager 管理センターにデバイスをアップロードする](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. メッセージが表示されたら、ご利用の "*全体管理者*" アカウントを使用してサインインします。
1. **[はい]** をクリックして、 **[AAD アプリケーションの作成]** 通知を受け入れます。 このアクションでは、サービス プリンシパルがプロビジョニングされ、同期を容易にするための Azure AD アプリケーション登録が作成されます。
1. 変更を行ったら、 **[OK]** をクリックして、共同管理プロパティを終了します。


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>共同管理の構成ウィザードを使用してデバイスのアップロードを有効にする
共同管理が有効になっていない場合は、**共同管理の構成**ウィザードを使用してデバイスのアップロードを有効にします。 共同管理の自動登録を有効にしたり、ワークロードを Intune に切り替えたりすることなく、デバイスをアップロードできます。 次の手順に従って、デバイスのアップロードを有効にします。

1. Configuration Manager 管理者コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[共同管理]** の順に移動します。
1. リボンで **[共同管理の構成]** をクリックして、ウィザードを開きます。
1. **[テナントのオンボード]** ページで、ご利用の環境に対して **[AzurePublicCloud]** を選択します。 Azure Government クラウドはサポートされていません。
1. **[サインイン]** をクリックします。 ご利用の "*全体管理者*" アカウントを使用してサインインします。
1. [**テナントのオンボード**] ページで [ **Microsoft Endpoint Manager 管理センターにアップロードする**] オプションが選択されていることを確認します。
   - 今すぐ共同管理を有効にしない場合は、[**共同管理の自動クライアント登録を有効**にする] チェックボックスがオンになっていないことを確認してください。 共同管理を有効にする場合は、オプションを選択します。
   - デバイスのアップロードと共に共同管理を有効にすると、ウィザードに追加のページが表示されます。 詳しくは、[共同管理の有効化](../comanage/how-to-enable.md)に関する記事をご覧ください。

   [![共同管理構成ウィザード](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. **[次へ]** 、 **[はい]** の順にクリックして、 **[AAD アプリケーションの作成]** 通知を受け入れます。 このアクションでは、サービス プリンシパルがプロビジョニングされ、同期を容易にするための Azure AD アプリケーション登録が作成されます。
1. [**アップロードの構成**] ページで、 **Microsoft エンドポイント Configuration Manager によって管理**されるすべてのデバイスについて、推奨されるデバイスのアップロード設定を選択します。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。
1. エンドポイント[分析](../../analytics/overview.md)でエンドユーザーエクスペリエンスを最適化するための洞察も得たい場合は、 **Microsoft endpoint Manager にアップロードされたデバイスのエンドポイント分析を有効**にするオプションをオンにします。
1. **[概要]** をクリックしてご自分の選択内容を確認して、 **[次へ]** をクリックします。
1. ウィザードが完了したら、 **[閉じる]** をクリックします。  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>アップロードを確認する

1. ConfigMgr インストールディレクトリ> から**Cmgatewaysyncuのログを開きます。** &lt;
1. 次の同期時刻は、のようなログエントリによって示され `Next run time will be at approximately: 02/28/2020 16:35:31` ます。
1. デバイスをアップロードする場合は、のようなログエントリを探し `Batching N records` ます。 **N**は、クラウドにアップロードされたデバイスの数です。 
1. アップロードは、変更のために15分ごとに実行されます。 変更がアップロードされると、 **Microsoft Endpoint Manager 管理センター**にクライアントの変更が表示されるまでに、さらに 5 ~ 10 分かかることがあります。

## <a name="perform-device-actions"></a>デバイスの操作を実行する

1. ブラウザーで、に移動します。`endpoint.microsoft.com`
1. [**デバイス**]、[**すべてのデバイス**] の順に選択して、アップロードしたデバイスを表示します。 アップロードされたデバイスの [**管理者の管理**列に**ConfigMgr**が表示されます。
   [![Microsoft Endpoint Manager 管理センター内のすべてのデバイス](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. デバイスをクリックすると、その**概要**ページが読み込まれます。
1. 次のいずれかのアクションをクリックします。
   - **コンピューター ポリシーの同期**
   - **ユーザー ポリシーの同期**
   - **アプリの評価サイクル**

   [![Microsoft Endpoint Manager 管理センターのデバイスの概要](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>既知の問題

### <a name="specific-devices-dont-synchronize"></a>特定のデバイスが同期されない

<!--7099564-->
Configuration Manager クライアントである特定のデバイスがサービスにアップロードされない可能性があります。

**影響を受けるデバイス:** デバイスが、配布ポイントの機能とクライアントエージェントの両方で同じ PKI 証明書を使用する配布ポイントである場合、そのデバイスはテナント接続デバイスの同期に含まれません。

**動作:** オンボード段階でテナント接続を実行すると、完全同期が初めて実行されます。 後続の同期サイクルは差分同期です。 影響を受けたデバイスを更新すると、デバイスが同期から削除されます。

## <a name="log-files"></a>ログ ファイル
サービス接続ポイントにある次のログを使用します。

- **Cmgatewaysyncuのログ**
- **CMGatewayNotificationWorker .log**

## <a name="next-steps"></a>次の手順

テナントアタッチログファイルの詳細については、「[テナント接続のトラブルシューティング](troubleshoot.md)」を参照してください。
