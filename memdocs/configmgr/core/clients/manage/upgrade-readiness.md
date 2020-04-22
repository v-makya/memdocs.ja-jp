---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: Upgrade Readiness と Configuration Manager を統合して Windows 10 アップグレードの互換性データにアクセスし、アップグレードまたは修復対象のデバイスを指定します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 18d8b66a7b9f5ad889645cbc8e48ebcbfe6550a9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696320"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Upgrade Readiness と Configuration Manager の統合

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> Windows Analytics サービスは、2020 年 1 月 31 日をもって廃止されています。 詳細については、[KB 4521815:Windows Analytics の廃止 (2020 年 1 月 31 日)](https://support.microsoft.com/help/4521815/windows-analytics-retirement) に関するページをご確認ください。
>
> Desktop Analytics が Windows Analytics の進化版です。 詳細については、「[Desktop Analytics とは](../../../desktop-analytics/overview.md)」を参照してください。

Configuration Manager サイトが Upgrade Readiness に接続されている場合は、それを削除し、クライアントを再構成する必要があります。

## <a name="remove-upgrade-readiness-connection"></a><a name="bkmk_remove"></a> Upgrade Readiness 接続を削除する

1. **完全な権限を持つ管理者** ロールのユーザーとして Configuration Manager コンソールを開きます。

1. **[管理]** ワークスペースに移動し、 **[クラウド サービス]** を展開し、 **[Azure サービス]** ノードを選択します。

1. Windows Analytics サービスを削除します。

## <a name="reconfigure-clients"></a>クライアントを再構成する

### <a name="unenroll-devices"></a>デバイスの登録を解除する

まず、**Windows Analytics** グループのサイトの既定値またはカスタム クライアント デバイス設定を確認します。 たとえば、次の設定を無効にします: **Configuration Manager を使用して、Windows テレメトリ設定を管理します**。

> [!IMPORTANT]
> Desktop Analytics を使用する予定がある場合は、クライアントで Windows 診断データ設定が構成されます。 Azure サービス接続ウィザードを使用して、Desktop Analytics で使用するためにこれらの設定を構成します。 詳細については、[Configuration Manager を Desktop Analytics に接続する方法](../../../desktop-analytics/connect-configmgr.md)に関する記事をご覧ください。

登録済みのデバイスに関して、次の Windows レジストリキーから CommercialID 値を削除します。

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Windows の診断データの構成

デバイスによる診断データの送信を続行しない場合:

- Windows 10: 診断データ レベルを **[セキュリティ]** に設定します
- Windows 7 SP1 または 8.1: **[商用データ オプトイン キー]** を無効にします

次のいずれかの方法で、これらの値を設定します。

- グループ ポリシー: **[コンピューターの構成]**  >  **[管理用テンプレート]**  >  **[Windows コンポーネント]**  >  **[データの収集とプレビュー ビルド]**
- モバイル デバイス管理 (MDM): [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry) など

詳しくは、「[組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)」をご覧ください。

> [!NOTE]  
> これらの変更を適用すると、デバイスによる診断データの送信は、すぐに停止されます。 Microsoft がワークスペースの分析情報の処理を停止するまでに 24 時間から48 時間かかることがあります。 Microsoft では、このデータを、30 日以内にクラウド サービスから削除します。

<!--
Upgrade Readiness is a part of [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](monitor-windows-analytics.md).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](../../servers/deploy/configure/azure-services-wizard.md) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  
- [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)  
- [Create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)  
