---
title: Microsoft Intune でセキュリティのベースラインの成功または失敗を確認する - Azure | Microsoft Docs
description: Microsoft Intune MDM でセキュリティのベースラインをユーザーとデバイスに展開するときに、エラー、競合、成功の状態を確認します。 クライアント ログを使用してトラブルシューティングする方法と Intune のレポート機能について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ccf9801c7a5977485c6c1864a69be2e46a4af55
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914873"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Microsoft Intune でセキュリティのベースラインとプロファイルを監視する

Intune からは、セキュリティ ベースラインを監視するためのオプションがいくつか与えられます。 次の操作を行います。

- セキュリティのベースライン、および推奨値と一致する (または一致しない) デバイスを監視します。
- ユーザーとデバイスに適用されるセキュリティのベースライン プロファイルを監視します。
- 選択したプロファイルが、選択したデバイスでどのように設定されているかを表示します。

また、セキュリティのベースラインが含まれる個々のデバイスに適用される "*エンドポイントのセキュリティ構成*" を表示することもできます。

この記事では、これらの監視オプションについて手順を追って説明します。

Microsoft Intune のセキュリティのベースライン機能の詳細については、[Intune のセキュリティのベースライン](security-baselines.md)に関するページを参照してください。

## <a name="monitor-the-baseline-and-your-devices"></a>ベースラインとデバイスを監視する

ベースラインを監視すると、Microsoft の推奨事項に基づいて、デバイスのセキュリティ状態に関する分析情報が得られます。 これらの分析情報を表示するには、[Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインし、 **[エンドポイントのセキュリティ]**  >  **[セキュリティ ベースライン]** の順にアクセスして、 *[MDM セキュリティ ベースライン]* など、セキュリティのベースラインの種類を選択します。 次に、 *[プロファイル]* ウィンドウで、詳細を表示するプロファイル インスタンスを選択します。 これにより、プロファイルの *[プロパティ]* ウィンドウが開き、ここにある *[モニター]* セクションから任意のプロファイル レポートを選択することができます。 

最初にベースラインを割り当ててからデータが表示されるまで最大 24 時間かかります。 その後の変更は、表示されるまで最大 6 時間かかります。

レポートとデバイスを確認すると、さまざまな詳細情報が表示されます。

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>プロファイルを監視する

プロファイルを監視すると、デバイスの展開状態に関する分析情報を得られますが、ベースラインの推奨事項に基づくセキュリティ状態に関する分析情報は得られません。

1. Intune で **[セキュリティ ベースライン]** を選択し、ベースラインを選択して、その *[プロファイル]* ウィンドウを開きます。

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. **[管理]**  >  **[プロパティ]** に、ベースラインのすべての設定の一覧が表示されます。 これらの設定のすべてを変更することもできます。

   ![セキュリティのベースライン プロファイルの設定を確認および更新する](./media/security-baselines-monitor/manage-settings.png)

4. **[監視]** では、個々のデバイスに関するプロファイルの展開状態、各ユーザーの状態、およびベースラインの各設定の状態を確認できます。

   ![セキュリティのベースライン プロファイルのさまざまなモニター オプションを確認する](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>デバイスに適用されるプロファイルの設定を表示する

セキュリティのベースライン プロファイルを選択すると、個々のデバイスに適用されるプロファイルの設定の一覧を表示することができます。  この一覧を表示するには、 **[エンドポイントのセキュリティ]**  >  **[セキュリティ ベースライン]**  > "*セキュリティ ベースラインの種類を選択します*" > "*表示するプロファイルを選択します*" >  **[デバイスの状態]** の順に移動します。 一覧を表示するには、 **[エンドポイントのセキュリティ]**  >  **[すべてのデバイス]**  > "*デバイスを選択します*" >  **[エンドポイントのセキュリティ構成]**  > "*ベースラインのバージョンを選択します*" の順に移動します。

デバイスを選択すると、Microsoft エンドポイント マネージャー管理センターに、そのプロファイルの設定の一覧が表示されます。これには、設定の基になるカテゴリや、デバイスの構成の状態が含まれます。 構成の状態には、次の値が含まれます。

- **成功** – デバイスの設定は、プロファイルで構成されている値と一致します。 これは、ベースラインの既定値と推奨値、またはプロファイルの構成時に管理者によって指定されたカスタム値のいずれかです。
- **競合** – 設定が別のポリシーと競合しているか、エラーが発生しているか、更新が保留されています。
- **該当なし** - 設定はプロファイルによって適用されません。

> [!NOTE]
> 設定の状態の値は、今後のリリースで更新され、詳細に指定されます。

## <a name="view-endpoint-security-configurations-per-device"></a>デバイスごとのエンドポイントのセキュリティ構成を表示する

個々のデバイスに適用されるセキュリティ構成の詳細を表示します。これは、正しく構成されていない設定を特定するのに役立ちます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[すべてのデバイス]** の順に移動し、表示するデバイスを選択します。

3. *[監視]* カテゴリで、 **[Endpoint security configuration]\(エンドポイントのセキュリティ構成\)** を選択して、そのデバイスに適用されているセキュリティ構成の一覧を表示します。

4. さらに詳細に調べたい場合は、エンドポイントのセキュリティ構成を選択して、デバイスに対するそのセキュリティ構成の評価に関する追加の詳細情報を表示することができます。

## <a name="troubleshoot-using-per-setting-status"></a>設定ごとの状態を使用したトラブルシューティング

セキュリティのベースラインを展開しましたが、展開状態にエラーが表示されます。 次の手順では、エラーのトラブルシューティングに関するガイダンスをいくつか紹介します。

1. Intune で、 **[セキュリティ ベースライン]** を選択し、ベースラインを選択したら、 **[プロファイル]** を選択します。

2. プロファイルを選択し、 **[監視]**  >  **[設定ごとの状態]** を選択します。

3. この表には、すべての設定と、各設定の状態が表示されます。 **[エラー]** 列または **[競合]** 列を選択して、エラーの原因となっている設定を確認します。

### <a name="mdm-diagnostic-information"></a>MDM の診断情報

これで問題のある設定がわかりました。 次の手順は、この設定がエラーまたは競合を引き起こしている理由を見つけることです。

Windows 10 デバイスには、組み込みの MDM 診断情報レポートがあります。 このレポートには、既定値、現在の値、ポリシーの一覧、デバイスとユーザーのどちらに展開されているかなどが表示されます。 このレポートを使用すると、設定によって競合やエラーが発生している理由を特定できます。

1. デバイス上で、 **[設定]**  >  **[アカウント]**  >  **[職場または学校にアクセスする]** の順に移動します。

2. アカウントを選択し、 **[情報]**  >  **[Advanced Diagnostic Report]\(高度な診断レポート\)**  >  **[レポートの作成]** の順に選択します。

3. **[エクスポート]** を選択し、生成されたファイルを開きます。

4. レポートでは、レポートのさまざまなセクションに含まれるエラーまたは競合の設定を探します。

  たとえば、 **[Enrolled configuration sources and target resources]\(登録済みの構成ソースとターゲット リソース\)** セクションや **[Unmanaged policies]\(管理されていないポリシー\)** セクションを調べます。 エラーや競合の原因となっている理由を把握できます。

[[Diagnose MDM failures in Windows 10]\(Windows 10 の MDM エラーを診断する\)](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) を使用すると、この組み込みレポートに関する詳細情報が表示されます。

> [!TIP]
>
> - 一部の設定には GUID の一覧も表示されます。 任意の設定値について、ローカル レジストリ (regedit) でこの GUID を検索できます。
> - イベント ビューアー ログには、問題のある設定に関するエラー情報もいくつか含まれている場合があります ( **[イベント ビューアー]**  >  **[アプリケーションとサービス ログ]**  >  **[Microsoft]**  >  **[Windows]**  >  **[DeviceManagement-Enterprise-Diagnostics-Provider]**  >  **[Admin]** )。

## <a name="next-steps"></a>次のステップ

- [セキュリティ ベースラインに関する詳細](security-baselines.md)
- [競合を回避する](security-baselines.md#avoid-conflicts)
- [デバイス プロファイルを監視する](../configuration/device-profile-monitor.md) 
- [よくある問題と解決策](../configuration/device-profile-troubleshoot.md)。
- [Intune でのポリシーとプロファイルのトラブルシューティング](../configuration/troubleshoot-policies-in-microsoft-intune.md)