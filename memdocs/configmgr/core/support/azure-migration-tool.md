---
title: オンプレミスのサイトを拡張して Microsoft Azure に移行する
titleSuffix: Configuration Manager
description: 移行ツールを使用して Configuration Manager 用の Azure 仮想マシンをプログラムで作成する方法について説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d5f0c9127cc5c5819368eb0454d7bc63546ccc1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699502"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>オンプレミスのサイトを拡張して Microsoft Azure に移行する

*適用対象:Configuration Manager (Current Branch)*


バージョン 1910 で導入されたこのツールは、Configuration Manager 用の Azure 仮想マシン (VM) をプログラムで作成するのに役立ちます。 <!--3556022--> パッシブ サイト サーバー、管理ポイント、配布ポイントなど、既定の設定のサイトの役割を使用してインストールできます。 新しい役割を検証したら、高可用性のための追加のサイト システムとしてそれらを使用します。 また、オンプレミスのサイト システムの役割を削除し、Azure VM の役割のみを保持することもできます。

## <a name="prerequisites"></a>[前提条件]

- Azure サブスクリプション

- ExpressRoute ゲートウェイを使用した Azure 仮想ネットワーク

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- 使用するユーザー アカウントは、Configuration Manager の **[完全な権限を持つ管理者]** であり、プライマリ サイト サーバーに対して管理者権限を持っている必要があります。

- パッシブ サーバーを追加するには、プライマリ サイトが[サイト サーバーの高可用性要件](../servers/deploy/configure/site-server-high-availability.md#prerequisites)を満たしている必要があります。 たとえば、[リモート コンテンツ ライブラリ](../plan-design/hierarchy/the-content-library.md#bkmk_remote)が必要です。

### <a name="required-azure-permissions"></a>必要な Azure アクセス許可

ツールを実行するときは、Azure で次のアクセス許可が必要になります。
<!--5789222-->
Microsoft.Resources/subscriptions/resourceGroups/read <br>
Microsoft.Resources/subscriptions/resourceGroups/write <br>
Microsoft.Resources/deployments/read <br>
Microsoft.Resources/deployments/write <br>
Microsoft.Resources/deployments/validate/action <br>
Microsoft.Compute/virtualMachines/extensions/read <br>
Microsoft.Compute/virtualMachines/extensions/write <br>
Microsoft.Compute/virtualMachines/read <br>
Microsoft.Compute/virtualMachines/write <br>
Microsoft.Network/virtualNetworks/read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft.Network/networkInterfaces/read <br>
Microsoft.Network/networkInterfaces/write <br>
Microsoft.Network/networkInterfaces/join/action <br>
Microsoft.Network/networkSecurityGroups/write <br>
Microsoft.Network/networkSecurityGroups/read <br>
Microsoft.Network/networkSecurityGroups/join/action <br>
Microsoft.Storage/storageAccounts/write <br>
Microsoft.Storage/storageAccounts/read <br>
Microsoft.Storage/storageAccounts/listkeys/action <br>
Microsoft.Storage/storageAccounts/listServiceSas/action <br>
Microsoft.Storage/storageAccounts/blobServices/containers/write <br>
Microsoft.Storage/storageAccounts/blobServices/containers/read <br>
Microsoft.KeyVault/vaults/deploy/action <br>
Microsoft.KeyVault/vaults/read <br>


アクセス許可とロールの割り当ての詳細については、[RBAC を使用した Azure リソースへのアクセスの管理](/azure/role-based-access-control/role-assignments-portal)に関するページを参照してください。

## <a name="run-the-tool"></a>ツールを実行します。

1. プライマリ サイト サーバーにサインオンし、Configuration Manager のインストール ディレクトリで次のツールを実行します: `Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. **[全般]** タブの情報を確認した後、 **[Azure Information]\(Azure 情報\)** タブに切り替えます。

1. **[Azure Information]\(Azure 情報\)** タブで、お使いの **[Azure 環境]** を選択してから、 **[サインイン]** を選択します。

    > [!TIP]
    > 正常にサインインするために、信頼された Ｗeb サイトの一覧に `https://*.microsoft.com` を追加する必要がある場合があります。

    [ ![拡張と移行ツールの [Azure Information]\(Azure 情報\) タブ](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. サインインした後、 **[サブスクリプション ID]** と **[仮想ネットワーク]** を選択します。 このツールでは、ExpressRoute ゲートウェイを備えたネットワークのみが一覧表示されます。

## <a name="site-server-high-availability"></a>サイト サーバーの高可用性

1. **[サイト サーバーの高可用性]** タブで、 **[チェック]** を選択してご自身のサイトの準備を評価します。

    いずれかのチェックが失敗した場合は、 **[詳細]** を選択して、問題の修復方法を決定します。 これらの前提条件について詳しくは、[サイト サーバーの高可用性](../servers/deploy/configure/site-server-high-availability.md#prerequisites)に関するページをご覧ください。

2. サイト サーバーを Azure に拡張または移行する場合は、 **[Create a site server in Azure]\(Azure にサイト サーバーを作成する\)** を選択します。 次に、以下のフィールドを入力します。

    |名前|[説明]|
    |---|---|
    |**サブスクリプション**|読み取り専用です。 サブスクリプションの名前と ID が表示されます。|
    |**リソース グループ**| 使用可能なリソース グループが一覧表示されます。 新しいリソース グループを作成する必要がある場合は、[Azure portal](https://portal.azure.com) を使用した後、このツールを再実行します。|
    |**場所**| 読み取り専用です。 仮想ネットワークの場所によって決まります|
    |**VM のサイズ**|ワークロードに合わせてサイズを選択します。 Microsoft では、 **[Standard_DS3_v2]** を推奨しています。|
    |**オペレーティング システム**|読み取り専用です。 このツールでは、Windows Server 2019 が使用されます。|
    |**ディスクの種類**|読み取り専用です。 このツールでは、最適なパフォーマンスを得るために Premium SSD が使用されます。|
    |**仮想ネットワーク**|読み取り専用です。|
    |**サブネット**|使用するサブネットを選択します。 新しいサブネットを作成する必要がある場合は、[Azure portal](https://portal.azure.com) を使用します。|
    |**コンピューター名**|Azure のパッシブ サイト サーバー VM の名前を入力します。 これは [Azure portal](https://portal.azure.com) に表示される名前と同じです。|
    |**ローカル管理者ユーザー名**|Azure VM によってドメイン参加前に作成されるローカル管理ユーザーの名前を入力します。|
    |**ローカル管理者パスワード**|ローカル管理ユーザーのパスワードです。 Azure デプロイ中にパスワードを保護するには、パスワードをシークレットとして [Azure Key Vault](/azure/key-vault/key-vault-overview) に保存します。 次に、ここで参照を使用します。 必要に応じて、[Azure portal](https://portal.azure.com) から新しく作成します。|
    |**ドメイン FQDN**|参加する Active Directory ドメインの完全修飾ドメイン名です。 既定では、ツールによって、現在のコンピューターからこの値が取得されます。|
    |**ドメイン ユーザー名**|ドメインへの参加が許可されているドメイン ユーザーの名前です。 既定では、ツールによって、現在サインインしているユーザーの名前が使用されます。|
    |**ドメイン パスワード**|ドメインに参加するドメイン ユーザーのパスワードです。 **[開始]** を選択すると、ツールによってそれが検証されます。 Azure デプロイ中にパスワードを保護するには、パスワードをシークレットとして [Azure Key Vault](/azure/key-vault/key-vault-overview) に保存します。 次に、ここで参照を使用します。 必要に応じて、[Azure portal](https://portal.azure.com) から新しく作成します。|
    |**ドメイン DNS IP**|ドメインに参加するために使用されます。 既定では、ツールによって、現在のコンピューターから現在の DNS が使用されます。|
    |**種類**|読み取り専用です。 種類として *[パッシブ サイト サーバー]* が表示されます。|

    > [!IMPORTANT]
    > 既定では、仮想マシンの **[既存の Windows Server ライセンスを使用]** は **[いいえ]** に設定されています。 ソフトウェア アシュアランス付きのオンプレミスの Windows Server ライセンスを使用する場合は、仮想マシンがプロビジョニングされた後に、[Azure portal](https://portal.azure.com) でこの設定を構成します。 詳細については、「[Windows Server 向け Azure ハイブリッド特典](/windows-server/get-started/azure-hybrid-benefit)」を参照してください。

1. Azure VM のプロビジョニングを開始するには、 **[開始]** を選択します。 デプロイの状態を監視するには、ツールの **[Deployments in Azure]\(Azure でのデプロイ)** に切り替えます。 最新の状態を取得するには、 **[Refresh deployment status]\(デプロイの状態を更新する\)** を選択します。

    > [!TIP]
    > [Azure portal](https://portal.azure.com) を使って状態を確認し、エラーを見つけ、修正の可能性を判断することもできます。

1. デプロイが完了したら、SQL サーバーに移動して、新しい Azure VM に対するアクセス許可を付与します。 詳細については、[サイト サーバーの高可用性 - 前提条件](../servers/deploy/configure/site-server-high-availability.md#prerequisites)に関するページをご覧ください。

1. パッシブ モードのサイト サーバーとして Azure VM を追加するには、 **[Add site server in passive mode]\(パッシブ モードでサイト サーバーを追加する\)** を選択します。

1. サイトによってパッシブ モードでサイト サーバーが追加されると、 **[サイト サーバーの高可用性]** タブにその状態が表示されます。

   [![[サイト サーバーの高可用性] タブに追加されたパッシブ サイト サーバー](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. 次に、[[Deployments in Azure]\(Azure でのデプロイ)](#bkmk_deploy-azure) タブに移動して、デプロイを完了します。

## <a name="site-database"></a>サイト データベース

現在、このツールには、オンプレミスから Azure にデータベースを移行するためのタスクは含まれていません。 オンプレミスの SQL サーバーから Azure SQL Server VM にデータベースを移動することを選択できます。 ツールによって、 **[サイト データベース]** タブに次の記事がサポートのために一覧表示されます。

- [データベースのバックアップと復元](../servers/manage/backup-and-recovery.md)
- [SQL Always On を構成し、データのレプリケートを許可する](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [SQL データベースを Azure SQL Server VM に移行する](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>サイト システムの役割

1. **[サイト システムの役割]** タブに切り替えます。既定の設定で新しいサイト システムの役割をプロビジョニングするには、 **[新規作成]** を選択します。 管理ポイント、配布ポイント、ソフトウェアの更新ポイントなどの役割をプロビジョニングできます。 現在、すべての役割がこのツールで使用できるわけではありません。

    [![拡張と移行ツールの [サイトシステムの役割] タブ](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. プロビジョニング ウィンドウで、フィールドを入力し、Azure のサイトの役割の VM をプロビジョニングします。 これらの詳細は、サイト サーバー用の上記の一覧に似ています。

1. Azure VM のプロビジョニングを開始するには、 **[開始]** を選択します。 デプロイの状態を監視するには、ツールの **[Deployments in Azure]\(Azure でのデプロイ)** に切り替えます。 最新の状態を取得するには、 **[Refresh deployment status]\(デプロイの状態を更新する\)** を選択します。

    > [!TIP]
    > [Azure portal](https://portal.azure.com) を使って状態を確認し、エラーを見つけ、修正の可能性を判断することもできます。

1. サイト システムの役割をさらに追加するには、このプロセスを繰り返します。

1. 次に、[[Deployments in Azure]\(Azure でのデプロイ)](#bkmk_deploy-azure) タブに移動して、デプロイを完了します。

1. デプロイが完了したら、Configuration Manager コンソールに移動して、サイトの役割に追加の変更を加えます。

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a> Azure でのデプロイ

1. Azure によって VM が作成されたら、ツールの **[Azure でのデプロイ]** タブに切り替えます。 **[デプロイ]** を選択して、既定の設定で役割を構成します。

1. **[実行]** を選択して、PowerShell スクリプトを開始します。

    [![生成された PowerShell スクリプトを実行してサイトの役割をデプロイする](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. さらに役割を構成するには、このプロセスを繰り返します。

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a> 既存の仮想マシンのデプロイにサイトの役割を追加する
<!--5665775, 6307931-->
Configuration Manager バージョン 2002 以降、Microsoft Azure ツールへのオンプレミス サイトの拡張と移行 では、1 つの Azure 仮想マシンに複数のサイト システムの役割をプロビジョニングできます。 最初の Azure 仮想マシンの展開が完了した後、サイト システムの役割を追加できます。 既存の仮想マシンに新しい役割を追加するには、次の手順を行います。
1. **[Deployments in Azure]\(Azure での展開\)** タブで、 **[完了]** 状態の仮想マシンの展開をクリックします。
1. **[新規作成]** ボタンをクリックして、仮想マシンに追加の役割を追加します。


## <a name="next-steps"></a>次のステップ

[Azure portal](https://portal.azure.com) で変更内容を確認する