---
title: 共同管理の監視
titleSuffix: Configuration Manager
description: 共同管理ダッシュボードを使用して、共同管理デバイスに関する情報を確認します。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 64d34cef57a3d5f141093d2b099c0b352604be42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688700"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Configuration Manager で共同管理を監視する方法

*適用対象:Configuration Manager (Current Branch)*

共同管理を有効にした後に、次の方法を使用して共同管理デバイスを監視します。

- [共同管理ダッシュ ボード](#co-management-dashboard)  

- [展開ポリシー](#deployment-policies)

- [WMI デバイス データ](#wmi-device-data)

## <a name="co-management-dashboard"></a>共同管理ダッシュボード

バージョン 1802 から、共同管理に関する情報を示すダッシュボードが表示されるようになりました。 ダッシュボードを利用すれば、お使いの環境で共同管理しているコンピューターを確認できます。 各種グラフを見ることで、対処が必要なデバイスを特定できます。<!--1356648-->

Configuration Manager コンソールで **[監視]** ワークスペースに移動し、 **[共同管理]** ノードを選択します。

バージョン 1810 から、共同管理ダッシュボードが機能強化され、さらに詳細な情報が表示されるようになりました。 <!--1358980-->

![共同管理ダッシュボードのスクリーンショット](media/co-management-dashboard.png)

### <a name="co-managed-devices"></a>共同管理デバイス

*適用対象: バージョン 1802 および 1806*

環境全体の共同管理デバイスの割合が示されます。

![共同管理デバイス タイル](media/co-management-dashboard/Percent-Co-managed-graph.PNG)

### <a name="client-os-distribution"></a>クライアント OS ディストリビューション

*すべてのバージョンに適用* 

OS ごとのクライアント デバイスの数がバージョン別に表示されます。 ここでは以下のグループが使用されます。  

- Windows 7 と 8.x
- 1709 より前の Windows 10  
- Windows 10 1709 以降  

    > [!Tip]  
    > Windows 10 バージョン 1709 以降が共同管理の前提条件となります。  

グラフ セクションにカーソルを合わせると、OS グループ内のデバイスの割合が表示されます。

![クライアント OS ディストリビューション タイル](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status-donut"></a>共同管理の状態 (ドーナツ)

*適用対象: バージョン 1802 および 1806*

次のカテゴリのデバイスの成功または失敗の内訳が表示されます。

- 成功、ハイブリッド Azure AD 参加済み
- 成功、Azure AD 参加済み  
- 失敗:自動登録に失敗しました  

グラフ セクションにカーソルを合わせると、そのカテゴリ内のデバイスの割合が表示されます。

![共同管理の状態 (ドーナツ) タイル](media/co-management-dashboard/Co-management-status-graph.PNG)

グラフ セクションを選択すると、そのカテゴリのデバイスの一覧が表示されます。

![登録エラー デバイス リスト](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)

### <a name="co-management-status-funnel"></a>共同管理の状態 (じょうご)

*適用対象: バージョン 1810 以降*

登録プロセスから、次の状態にあるデバイスの数を示すじょうごグラフ。
  
- 対象デバイス
- スケジュール済み  
- 登録開始済み  
- 登録済み  

![共同管理の状態 (じょうご) タイル](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>共同管理の登録状態

*適用対象: バージョン 1810 以降*

次のカテゴリのデバイスの状態の内訳が表示されます。

- 成功、ハイブリッド Azure AD 参加済み  
- 成功、Azure AD 参加済み  
- 登録中、ハイブリッド Azure AD 参加済み  
- エラー、ハイブリッド Azure AD 参加済み  
- エラー、Azure AD 参加済み  
- ユーザー サインインの保留中  

    > [!Note]  
    > バージョン 1906 以降では、この保留中の状態にあるデバイス数を減らすために、新しい共同管理デバイスが、その Azure AD "*デバイス*" トークンに基づいて Microsoft Intune サービスに自動的に登録されるようになりました。 自動登録を開始するのに、ユーザーがデバイスにサインインするのを待機する必要はありません。 この動作をサポートするには、デバイスで Windows 10 バージョン 1803 以降が実行されている必要があります。
    >
    > デバイス トークンは、失敗すると、ユーザー トークンを使用して前の動作にフォールバックします。 **ComanagementHandler.log** で次のエントリを調べます。`Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

タイルで状態を選択すると、その状態のデバイスが一覧表示されます。  

![共同管理の登録状態タイル](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>ワークロードの切り替え

*すべてのバージョンに適用*

使用可能なワークロードのために、Microsoft Intune に切り替えたデバイスの数を示す棒グラフが表示されます

ワークロードの一覧は、Configuration Manager のバージョンによって変わります。 詳細については、「[Intune に切り替えられるワークロード](workloads.md)」を参照してください。

グラフ セクションにカーソルを合わせると、ワークロードのために切り替えたデバイスの数が表示されます。 

![ワークロードの切り替えを示す棒グラフ](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>登録エラー

*適用対象: バージョン 1810 以降*

この表は、デバイスからの登録エラーの一覧です。 これらのエラーは、Windows の MDM コンポーネント、コア Windows OS、または Configuration Manager クライアントから発生する可能性があります。

考えられるエラーは何百もあります。 次の表は、最も一般的なエラーの一覧です。
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| エラー | [説明] |
|---------|---------|
| 2147549183 (0x8000FFFF) | MDM 登録が Azure AD 上でまだ構成されていないか、想定されていない登録 URL です。<br><br>[Windows 10 の自動登録を有効にする](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | ユーザーのライセンスが正常ではない状態で登録できません<br><br>[ユーザーにライセンスを割り当てる](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Intune に自動的に登録しようとしましたが、Azure AD の構成が完全に適用されていません。 デバイスは短時間で再試行されるため、この問題は一時的なものです。 |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | ユーザーが操作を取り消しました。<br><br>MDM 登録に多要素認証が必要であり、サポートされている 2 つ目の要素でユーザーがサインインしていない場合、Windows ではユーザーに登録を促すトースト通知を表示します。 ユーザーがトースト通知に応答しない場合、このエラーが発生します。 Configuration Manager は再試行してユーザーにプロンプトを表示するため、これは一時的な問題のはずです。 ユーザーは Windows にサインインするときに多要素認証を使用する必要があります。 また、この行動を予想し、プロンプトが表示されたら操作するように教育してください。 | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | 通常、モバイル デバイス管理はサポートされていません | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | サーバーがユーザーの認証に失敗しました<br><br> ユーザーの Azure AD トークンがありません。 ユーザーが Azure AD に対して認証できることを確認します。 |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | MDM 自動登録は、Windows RS3 以降でのみサポートされています。<br><br>デバイスが共同管理の[最小要件](overview.md#windows-10)を満たしていることを確認します。 |
| 3400073293 | ADAL ユーザー領域アカウントの応答が不明です<br><br>Azure AD の構成を確認し、ユーザーが正常に認証できることを確認します。 | 
| 3399548929 | ユーザーのサインインが必要です<br><br>この問題はおそらく一時的です。 登録タスクが発生する前にユーザーがすぐにサインアウトしたときに発生します。 | 
| 3400073236 | ADAL セキュリティ トークン要求が失敗しました。<br><br>Azure AD の構成を確認し、ユーザーが正常に認証できることを確認します。 |
| 2149122477 | 一般的な HTTP の問題 |
| 3400073247 | ADAL 統合 Windows 認証はフェデレーション フローでのみサポートされています<br><br>[ハイブリッド Azure Active Directory 参加の実装を計画する](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | サーバーまたはプロキシが見つかりませんでした。<br><br>クライアントがクラウドと通信できない場合、この問題はおそらく一時的です。 問題が解決しない場合は、クライアントが一貫して Azure に接続できることを確認してください。 | 
| 2149056532 | 特定のプラットフォームまたはバージョンがサポートされていません<br><br>デバイスが共同管理の[最小要件](overview.md#windows-10)を満たしていることを確認します。 |
| 2147943568 | 要素が見つかりません<br><br>この問題はおそらく一時的です。 問題が解決しない場合は、Microsoft サポートに連絡してください。 |
| 2192179208 | このコマンドを処理するために必要なメモリ リソースがありません。<br><br>この問題はおそらく一時的であり、クライアントが再試行すると、おそらく自動的に解決します。 |
| 3399614467 | このアサーションに対する ADAL の承認の付与に失敗しました<br><br>Azure AD の構成を確認し、ユーザーが正常に認証できることを確認します。 |
| 2149056517 | DB アクセス エラーなど、管理サーバーからの一般的なエラー<br><br>この問題はおそらく一時的です。 問題が解決しない場合は、Microsoft サポートに連絡してください。 |
| 2149134055 | Winhttp 名が解決されていません<br><br>クライアントはサービスの名前を解決できません。 DNS 構成を確認してください。 | 
| 2149134050 | インターネット タイムアウト<br><br>クライアントがクラウドと通信できない場合、この問題はおそらく一時的です。 問題が解決しない場合は、クライアントが一貫して Azure に接続できることを確認してください。 |

詳細については、「[MDM Registration Error Values](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants)」(MDM 登録エラー値) を参照してください。

## <a name="deployment-policies"></a>展開ポリシー

**[監視]** ワークスペースの **[展開]** ノードに 2 つのポリシーが作成されます。 ポリシーの 1 つはパイロット グループ用であり、1 つは運用環境用です。 これらのポリシーは、Configuration Manager がポリシーを適用したデバイス数のみをレポートします。 Intune に登録されているデバイス数は、デバイスを共同管理するための前提要件ですが、考慮されていません。  

運用環境ポリシー (CoMgmtSettingsProd) の対象は **[すべてのシステム]** コレクションです。 OS の種類とバージョンを確認する適用性条件が含まれています。 クライアントがサーバー OS であり、Windows 10 ではない場合、ポリシーは適用されず、何のアクションも行われません。

## <a name="wmi-device-data"></a>WMI デバイス データ

**SMS_Client_ComanagementState** WMI クラスを照会します。 共同管理の展開状態を判断するカスタム コレクションを Configuration Manager に作成することができます。 カスタム コレクションの作成の詳細については、「[コレクションの作成方法](../core/clients/manage/collections/create-collections.md)」を参照してください。

WMI クラスでは次のフィールドを使用できます。  

- **MachineId**:Configuration Manager クライアントの一意のデバイス ID  

- **MDMEnrolled**:デバイスが MDM に登録されているかどうかを指定します  

- **Authority**:デバイスが登録されている機関  

- **ComgmtPolicyPresent**:Configuration Manager の共同管理ポリシーがクライアントに存在するかどうかを指定します。 **MDMEnrolled** 値が **0** の場合、クライアントに共同管理ポリシーが存在するかどうかにかかわらず、デバイスは共同管理されていません。  

**MDMEnrolled** フィールドと **ComgmtPolicyPresent** フィールドの両方の値が **1** の場合、デバイスは共同管理されています。  
