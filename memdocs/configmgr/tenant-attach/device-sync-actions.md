---
title: Microsoft Endpoint Manager テナントの接続
titleSuffix: Configuration Manager
description: Configuration Manager デバイスをクラウドサービスにアップロードし、管理センターからアクションを実行します。
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: e2b8c07a64265d33ade0b1c2c08c2d9c4096b741
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693464"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Microsoft Endpoint Manager テナントの接続: デバイスの同期とデバイスの操作
<!--3555758 live 3/4/2020-->
*適用対象:Configuration Manager (Current Branch)*

Microsoft Endpoint Manager は、すべてのデバイスを管理するための統合ソリューションです。 Microsoft は、Configuration Manager と Intune を**Microsoft Endpoint Manager 管理センター**と呼ばれる1つのコンソールにまとめます。

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
- `https://gateway.configmgr.manage.microsoft.com`
- `https://us.gateway.configmgr.manage.microsoft.com`
- `https://eu.gateway.configmgr.manage.microsoft.com`


## <a name="enable-device-upload"></a>デバイスのアップロードを有効にする

- 共同管理を現在有効にしている場合は、[共同管理プロパティを編集](#bkmk_edit)して、デバイスのアップロードを有効にします。
- 共同管理が有効になっていない場合は、 [**共同管理の構成**ウィザードを使用](#bkmk_config)してデバイスのアップロードを有効にします。
   - 共同管理の自動登録を有効にしたり、ワークロードを Intune に切り替えたりすることなく、デバイスをアップロードできます。
- [**クライアント**] 列に **[はい]** が設定されている Configuration Manager によって管理されているすべてのデバイスがアップロードされます。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>共同管理プロパティを編集してデバイスのアップロードを有効にする

共同管理を現在有効にしている場合は、次の手順を使用して共同管理のプロパティを編集し、デバイスのアップロードを有効にします。

1. Configuration Manager 管理コンソールで、[**管理** > ] [**概要** > ] [**共同管理**]**Cloud Services** > にアクセスします。
1. 共同管理設定を右クリックし、[**プロパティ**] を選択します。
1. [**アップロードの構成**] タブで、[ **Microsoft Endpoint Manager 管理センターにアップロードする**] を選択します。 **[Apply]** をクリックします。
   - デバイスのアップロードの既定の設定は、 **Microsoft エンドポイント Configuration Manager によって管理**されるすべてのデバイスです。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。

   [![共同管理構成ウィザード](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. プロンプトが表示されたら、*グローバル管理者*アカウントでサインインします。
1. [**はい**] をクリックして、 **AAD アプリケーションの作成**通知を受け入れます。 このアクションでは、サービスプリンシパルをプロビジョニングし、同期を容易にするために Azure AD アプリケーション登録を作成します。
1. 変更が完了したら、[ **OK** ] をクリックして共同管理のプロパティを終了します。


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>共同管理の構成ウィザードを使用してデバイスのアップロードを有効にする
共同管理が有効になっていない場合は、**共同管理の構成**ウィザードを使用してデバイスのアップロードを有効にします。 共同管理の自動登録を有効にしたり、ワークロードを Intune に切り替えたりすることなく、デバイスをアップロードできます。 次の手順に従って、デバイスのアップロードを有効にします。

1. Configuration Manager 管理コンソールで、[**管理** > ] [**概要** > ] [**共同管理**]**Cloud Services** > にアクセスします。
1. リボンの [**共同管理の構成**] をクリックして、ウィザードを開きます。
1. [**テナントのオンボード**] ページで、使用している環境の [ **azurepubliccloud** ] を選択します。 Azure Government cloud はサポートされていません。
1. [サインイン****] をクリックします。 *グローバル管理者*アカウントを使用してサインインします。
1. [**テナントのオンボード**] ページで [ **Microsoft Endpoint Manager 管理センターにアップロードする**] オプションが選択されていることを確認します。
   - 今すぐ共同管理を有効にしない場合は、[**共同管理の自動クライアント登録を有効**にする] チェックボックスがオンになっていないことを確認してください。 共同管理を有効にする場合は、オプションを選択します。
   - デバイスのアップロードと共に共同管理を有効にすると、ウィザードに追加のページが表示されます。 詳しくは、[共同管理の有効化](../comanage/how-to-enable.md)に関する記事をご覧ください。

   [![共同管理構成ウィザード](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. [**次へ**] をクリックし、[**はい]** をクリックして、 **AAD アプリケーションの作成**通知を受け入れます。 このアクションでは、サービスプリンシパルをプロビジョニングし、同期を容易にするために Azure AD アプリケーション登録を作成します。
1. [**アップロードの構成**] ページで、 **Microsoft エンドポイント Configuration Manager によって管理**されるすべてのデバイスについて、推奨されるデバイスのアップロード設定を選択します。 必要に応じて、アップロードを1つのデバイスコレクションに制限することができます。
1. [**概要**] をクリックして選択内容を確認し、[**次へ**] をクリックします。
1. ウィザードが完了したら、[**閉じる**] をクリックします。  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>アップロードを確認する

1. ConfigMgr インストールディレクトリ> から**Cmgatewaysyncuのログ**を&lt;開きます。
1. 次の同期時刻は、のようなログエントリ`Next run time will be at approximately: 02/28/2020 16:35:31`によって示されます。
1. デバイスをアップロードする場合は、のような`Batching N records`ログエントリを探します。 **N**は、クラウドにアップロードされたデバイスの数です。 
1. アップロードは、変更のために15分ごとに実行されます。 変更がアップロードされると、 **Microsoft Endpoint Manager 管理センター**にクライアントの変更が表示されるまでに、さらに 5 ~ 10 分かかることがあります。

## <a name="perform-device-actions"></a>デバイスの操作を実行する

1. ブラウザーで、に移動します。`endpoint.microsoft.com`
1. [**デバイス**]、[**すべてのデバイス**] の順に選択して、アップロードしたデバイスを表示します。 アップロードされたデバイスの [**管理者の管理**列に**ConfigMgr**が表示されます。
   [![Microsoft Endpoint Manager 管理センター内のすべてのデバイス](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. デバイスをクリックすると、その**概要**ページが読み込まれます。
1. 次のいずれかのアクションをクリックします。
   - **コンピューターポリシーの同期**
   - **ユーザーポリシーの同期**
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

## <a name="next-steps"></a>次のステップ

テナントアタッチログファイルの詳細については、「[テナント接続のトラブルシューティング](technical-reference.md)」を参照してください。
