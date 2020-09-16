---
title: Hybrid Azure AD 参加済みデバイスの登録 - Windows Autopilot
titleSuffix: ''
description: Windows Autopilot を使用して Hybrid Azure AD 参加済みデバイスを Microsoft Intune に登録します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1580726640612325fd22ca1fa4ae55517036644
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568592"
---
# <a name="deploy-hybrid-azure-ad-joined-devices-by-using-intune-and-windows-autopilot"></a>Intune と Windows Autopilot を使用して Hybrid Azure AD 参加済みデバイスをデプロイする
Intune と Windows Autopilot を使用して、Hybrid Azure Active Directory (Azure AD) 参加済みデバイスを設定できます。 そのためには、この記事の手順のようにします。

## <a name="prerequisites"></a>[前提条件]

[Hybrid Azure AD 参加済みデバイス](/azure/active-directory/devices/hybrid-azuread-join-plan)を正しく構成します。 Get-MsolDevice コマンドレットを使用して、[デバイスの登録を確認](/azure/active-directory/devices/hybrid-azuread-join-managed-domains#verify-the-registration)します。

登録するデバイスは、次の要件に従う必要があります。
- Windows 10 v1809 以上を使用します。
- [Windows の自動操縦ネットワーク要件に従っ](/windows/deployment/windows-autopilot/windows-autopilot-requirements#networking-requirements)て、インターネットにアクセスできるようにします。
- Active Directory ドメインコントローラーにアクセスできる。 デバイスは、次のことができるように、組織のネットワークに接続されている必要があります。
  - AD ドメインと AD ドメインコントローラーの DNS レコードを解決します。
  - ユーザーを認証するためにドメインコントローラーと通信します。
- 参加しようとしているドメインのドメインコントローラーに対して ping が正常に実行されました。
- プロキシを使用する場合は、WPAD プロキシ設定オプションを有効にして構成する必要がある。
- OOBE (Out-of-Box Experience) を使用している。
- Azure Active Directory が OOBE でサポートしている認証の種類を使用する。

## <a name="set-up-windows-10-automatic-enrollment"></a>Windows 10 の自動登録を設定する

1. Azure にサインインし、左側のウィンドウで [ **Azure Active Directory**  >  **モビリティ (MDM および MAM)**] Microsoft Intune を選択し  >  **Microsoft Intune**ます。

2. Intune と Windows を使用して Azure AD 参加済みデバイスを展開するユーザーが、 **MDM ユーザースコープ**に含まれているグループのメンバーであることを確認します。

    ![[モビリティ (MDM および MAM)] の [構成] ウィンドウ](./media/windows-autopilot-hybrid/auto-enroll-scope.png)

3. **[MDM 利用規約 URL]** 、 **[MDM 探索 URL]** 、 **[MDM 準拠 URL]** の各ボックスには既定値を使用して、 **[保存]** を選択します。

## <a name="increase-the-computer-account-limit-in-the-organizational-unit"></a>組織単位でコンピューター アカウントの上限を増やす

Active Directory 用の Intune コネクタでは、オンプレミスの Active directory ドメインに Autopilot 登録済みコンピューターが作成されます。 Intune コネクタをホストするコンピューターには、ドメイン内にコンピューター オブジェクトを作成する権限が必要です。 

一部のドメインでは、コンピューターにコンピューターを作成する権限が付与されていません。 また、ドメインには組み込みの制限 (既定値は 10) があり、コンピューター オブジェクトの作成権限を委任されていないすべてのユーザーとコンピューターに適用されます。 この権限は、ハイブリッド Azure AD 参加済みデバイスが作成される組織単位で Intune コネクタをホストするコンピューターに委任する必要があります。

コンピューター作成権限を付与される組織単位は、次のどちらかと一致している必要があります。
- ドメイン参加プロファイルで入力された組織単位。
- プロファイルが選択されていない場合は、お使いのドメインに対するコンピューターのドメイン名。

1. **[Active Directory ユーザーとコンピューター]** (DSA.msc) を開きます。

2. ハイブリッド Azure AD 参加済みコンピューターの作成に使用する組織単位を右クリックして、 **制御を委任**> ます。

    ![[制御の委任] コマンド](./media/windows-autopilot-hybrid/delegate-control.png)

3. **制御の委任**ウィザードで、 **[次へ]**  >  **[追加]**  >  **[オブジェクトの種類]** を選択します。

4. [**オブジェクトの種類**] ウィンドウで、[**コンピューター**  >  **]** を選択します。

    ![[オブジェクトの種類] ウィンドウ](./media/windows-autopilot-hybrid/object-types-computers.png)

5. **[ユーザー、コンピューター、またはグループの選択]** ウィンドウの **[選択するオブジェクト名を入力してください]** ボックスに、コネクタをインストールするコンピューターの名前を入力します。

    ![[ユーザー、コンピューター、またはグループの選択] ウィンドウ](./media/windows-autopilot-hybrid/enter-object-names.png)

6. **名前の確認** を選択して入力を検証 > **OK** > **次へ**をクリックします。

7. **[委任するカスタム タスクを作成する]**  >  **[次へ]** を選択します。

8. [コンピューターオブジェクト]**フォルダー内の次のオブジェクトのみ**を選択し  >  **Computer objects**ます。

9. [ **このフォルダー内の選択されたオブジェクトを作成** し、 **このフォルダー内の選択したオブジェクトを削除**する] を選択します。

    ![[Active Directory オブジェクトの種類] ウィンドウ](./media/windows-autopilot-hybrid/only-following-objects.png)
 
10. **[次へ]** を選択します。

11. **[アクセス許可]** で、 **[フル コントロール]** チェック ボックスをオンにします。 この操作で、他のすべてのオプションが選択されます。

    ![[アクセス許可] ウィンドウ](./media/windows-autopilot-hybrid/full-control.png)

12. **[次へ]**  >  **[完了]** を選択します。

## <a name="install-the-intune-connector"></a>Intune コネクタをインストールする

Active Directory 用の Intune コネクタは、Windows Server 2016 以降を実行しているコンピューターにインストールする必要があります。 コンピューターは、インターネットとお使いの Active Directory にもアクセスできる必要があります。 スケーラビリティと可用性を高めるために、環境内に複数のコネクタをインストールできます。 コネクタは、他の Intune コネクタが実行されていないサーバーにインストールすることをお勧めします。 各コネクタは、サポートするドメインにコンピューターオブジェクトを作成できる必要があります。

> [!NOTE]
> 組織に複数のドメインがあり、複数の Intune コネクタをインストールする場合は、特定のドメインに対してのみハイブリッド Azure AD 参加を実装する予定がある場合でも、すべてのドメインにコンピューターオブジェクトを作成できるサービスアカウントを使用する必要があります。 これらが信頼されていないドメインの場合は、Windows 自動操縦を使用しないドメインからコネクタをアンインストールする必要があります。 複数のドメインにわたって複数のコネクタを使用する場合は、すべてのコネクタがすべてのドメインでコンピューターオブジェクトを作成できる必要があります。

Intune コネクタには、[Intune と同じエンドポイント](../intune/fundamentals/intune-endpoints.md)が必要です。

1. [IE セキュリティ強化の構成] をオフにします。 Windows Server では既定で、Internet Explorer セキュリティ強化の構成がオンになっています。 Active Directory 用に Intune コネクタにサインインできない場合は、管理者の [IE セキュリティ強化の構成] をオフにします。 [Internet Explorer セキュリティ強化の構成をオフにする方法](/archive/blogs/chenley/how-to-turn-off-internet-explorer-enhanced-security-configuration)。 
2. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[Windows]**  >  **[Windows の登録]**  >  **[Active Directory の Intune コネクタ]**  >  **[追加]** を選択します。 
3. 手順に従ってコネクタをダウンロードします。
4. ダウンロードしたコネクタのセットアップ ファイル *ODJConnectorBootstrapper.exe* を開いて、コネクタをインストールします。
5. セットアップの最後に、 **[構成]** を選択します。
6. **[サインイン]** を選択します。
7. ユーザーのグローバル管理者ロールまたは Intune 管理者ロールの資格情報を入力します。 
 ユーザー アカウントに Intune ライセンスが割り当てられている必要があります。
8. **[デバイス]**  >  **[Windows ]**  >  **[Windows の登録]**  >  **[Active Directory の Intune コネクタ]** に移動し、接続の状態が **[アクティブ]** であることを確認します。

> [!NOTE]
> コネクタにサインインした後、それが [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に表示されるまでに数分かかる場合があります。 Intune サービスと正常に通信できる場合にのみ表示されます。

### <a name="configure-web-proxy-settings"></a>Web プロキシ設定の構成

ネットワーク環境に Web プロキシがある場合は、「[既存のオンプレミス プロキシ サーバーと連携する](../intune/enrollment/autopilot-hybrid-connector-proxy.md)」を参照して、Active Directory 用の Intune コネクタが正しく動作することを確認します。


## <a name="create-a-device-group"></a>デバイス グループを作成する
1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[グループ]**  >  **[新しいグループ]** を選択します。

1. [ **グループ** ] ウィンドウで、次のオプションを選択します。

    1. **[グループの種類]** で、 **[セキュリティ]** を選択します。
    2. **[グループ名]** と **[グループの説明]** を入力します。
    3. **[メンバーシップの種類]** を選択します。

4. [メンバーシップの種類] で [ **動的デバイス** ] を選択した場合は、 **グループ** ウィンドウで [ **動的なデバイスメンバー**] を選択します。

5. **[高度なルール**] ボックスで、次のいずれかのコード行を入力します。
    - すべての Autopilot デバイスを含むグループを作成するには、「`(device.devicePhysicalIDs -any _ -contains "[ZTDId]")`」と入力します。
    - Intune のグループ タグ フィールドは、Azure AD デバイス上の OrderID 属性にマップされます。 特定のグループタグ (OrderID) を持つすべての自動操縦デバイスを含むグループを作成する場合は、次のように入力します。 `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - 特定の注文書 ID のすべての Autopilot デバイスを含むグループを作成するには、「`(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`」と入力します。
 
6. [**保存**] [作成] を選択し  >  **Create**ます。 

## <a name="register-your-autopilot-devices"></a>Autopilot デバイスを登録する

次の方法のいずれかを選択して Autopilot デバイスを登録します。

### <a name="register-autopilot-devices-that-are-already-enrolled"></a>既に登録されている Autopilot デバイスを登録する

1. **[すべての対象デバイスを Autopilot に変換する]** を **[はい]** に設定して、Autopilot Deployment プロファイルを作成します。 
2. Autopilot で自動的に登録するメンバーが含まれるグループにプロファイルを割り当てます。

詳しくは、「[Autopilot Deployment プロファイルを作成する](enrollment-autopilot.md#create-an-autopilot-deployment-profile)」をご覧ください。

### <a name="register-autopilot-devices-that-arent-enrolled"></a>登録されていない Autopilot デバイスを登録する

デバイスがまだ登録されていない場合は、自分で登録できます。 詳しくは、「[デバイスを追加する](enrollment-autopilot.md#add-devices)」をご覧ください。

### <a name="register-devices-from-an-oem"></a>OEM からデバイスを登録する

新しいデバイスを購入する場合、OEM によってはデバイスを登録できます。 詳細については、「 [OEM の登録](add-devices.md#oem-registration)」を参照してください。

*登録*されている自動操縦デバイスは、Intune に登録される前に、次の3か所に表示されます (名前はシリアル番号に設定されています)。
- Azure portal の Intune の **[Autopilot デバイス]** ウィンドウ。 **[デバイスの登録]**  >  **[Windows の登録]**  >  **[デバイス]** を選択します。
- Azure portal の Intune の **[Azure AD デバイス]** ウィンドウ。 **[デバイス]**  >  **[Azure AD デバイス]** を選択します。
- Azure portal の Azure Active Directory の **[Azure AD All Devices]\(Azure AD のすべてのデバイス\)** ウィンドウ ( **[デバイス]**  >  **[すべてのデバイス]** )。

Autopilot デバイスが "*登録*" された後は、次の 4 つの場所に表示されます。
- Azure portal の Intune の **[Autopilot デバイス]** ウィンドウ。 **[デバイスの登録]**  >  **[Windows の登録]**  >  **[デバイス]** を選択します。
- Azure portal の Intune の **[Azure AD デバイス]** ウィンドウ。 **[デバイス]**  >  **[Azure AD デバイス]** を選択します。
- Azure portal の Azure Active Directory の **[Azure AD All Devices]\(Azure AD のすべてのデバイス\)** ウィンドウ。 **[デバイス]**  >  **[すべてのデバイス]** を選択します。
- Azure portal の Intune の **[すべてのデバイス]** ウィンドウ。 **[デバイス]**  >  **[すべてのデバイス]** を選択します。

登録後の Autopilot デバイスの名前は、デバイスのホスト名になります。 既定では、ホスト名は *DESKTOP-* で始まります。


## <a name="create-and-assign-an-autopilot-deployment-profile"></a>AutoPilot Deployment プロファイルを作成して割り当てる
Autopilot Deployment プロファイルは、Autopilot デバイスを構成する場合に使用されます。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[Windows]**  >  **[Windows の登録]**  >  **[デプロイ プロファイル]**  >  **[プロファイルの作成]** を選択します。
2. **[基本]** ページ上で、 **[名前]** と省略可能な **[説明]** に入力します。
3. 割り当てられたグループ内のデバイスのすべてが自動的に Autopilot に変換されるようにする場合は、 **[すべての対象デバイスを Autopilot に変換する]** を **[はい]** に設定します。 割り当てられたグループ内にある会社所有の Autopilot 以外のデバイスは、すべて Autopilot デプロイ サービスに登録されます。 個人所有のデバイスは自動操縦に変換されません。 登録が処理されるまで 48 時間待ちます。 デバイスが登録解除されリセットされると、Autopilot によってそのデバイスが登録されます。 この方法でデバイスを登録すると、このオプションを無効にしてもプロファイルの割り当てを削除しても、Autopilot 展開サービスからデバイスは削除されません。 [デバイスを直接削除](enrollment-autopilot.md#delete-autopilot-devices)する必要があります。
4. **[次へ]** を選択します。
5. **[Out-of-box experience (OOBE)]** ページの **[配置モード]** で、 **[ユーザー ドリブン]** を選択します。
6. **[Azure AD への参加の種類]** ボックスで、 **[ハイブリッド Azure AD 参加済み]** を選択します。
7. VPN サポートを使用して組織のネットワークからデバイスを展開している場合は、[ **ドメインの接続をスキップ** する] チェックボックスを **[はい]** に設定します。 詳細については、「 [ハイブリッド Azure Active Directory のユーザー主導モードと VPN サポートの結合](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support)」を参照してください。
8. 必要に応じて、 **[Out-of-box experience (OOBE)]** ページで残りのオプションを構成します。
9. **[次へ]** を選択します。
10. [ **スコープタグ** ] ページで、[このプロファイルの [スコープタグ](../intune/fundamentals/scope-tags.md) ] を選択します。
11. **[次へ]** を選択します。
12. **[割り当て]** ページで、 **[含めるグループを選択]** を選択し、デバイス グループを検索して選択し、 **[選択]** を選択します。
13. **[次へ]**  >  **[作成]** を選択します。

デバイス プロファイルの状態が *[未割り当て]* から *[割り当て中]* を経て最後に *[割り当て済み]* に変わるまでに、約 15 分かかります。

## <a name="optional-turn-on-the-enrollment-status-page"></a>(省略可能) 登録状態ページを有効にする

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[Windows]**  >  **[Windows の登録]**  >  **[登録ステータス ページ]** を選択します。
2. **[登録ステータス ページ]** ウィンドウで、 **[既定]**  >  **[設定]** の順に選択します。
3. **[アプリとプロファイルのインストール進行状況を表示する]** ボックスで、 **[はい]** を選択します。
4. 必要に応じて、他のオプションを構成します。
5. **[保存]** を選択します。

## <a name="create-and-assign-a-domain-join-profile"></a>ドメイン参加プロファイルを作成して割り当てる

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** を選択します。
2. 次のプロパティを入力します。
    - **名前**:新しいプロファイルのわかりやすい名前を入力します。
    - **説明**:プロファイルの説明を入力します。
    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイルの種類]** : **[ドメイン参加 (プレビュー)]** を選択します。
3. **[設定]** を選択し、**コンピューター名のプレフィックス**と**ドメイン名**を指定します。
4. (省略可能) [DN 形式](/windows/desktop/ad/object-names-and-identities#distinguished-name)で**組織単位** (OU) を指定します。 次のような方法があります。
    - Intune コネクタを実行している Windows 2016 デバイスに制御を委任した OU を指定します。
    - オンプレミスの Active Directory でルート コンピューターに制御を委任した OU を指定します。
    - この値を空白のままにすると、コンピューター オブジェクトが Active Directory の既定のコンテナー ([変更しないかぎり](https://support.microsoft.com/help/324949/redirecting-the-users-and-computers-containers-in-active-directory-dom) CN=Computers) に作成されます。
 
    有効な例を示します。
      - OU=Level 1、OU=Level2、DC=contoso、DC=com
      - OU=Mine、DC=contoso、DC=com
 
    次に、無効な例をいくつか示します。
      - CN = Computers, DC = contoso, DC = com (コンテナーを指定することはできません。代わりに、ドメインの既定値を使用する場合は空白のままにします)
      - OU = 地雷 (DC = attributes でドメインを指定する必要があります)
 
    > [!NOTE]
    > **[組織単位]** の値の周りで引用符を使用しないでください。

5. **[OK]**  >  **[作成]** を選択します。 プロファイルが作成されて、一覧に表示されます。
6. 「[デバイスグループの作成](windows-autopilot-hybrid.md#create-a-device-group)」の手順で使用したものと同じグループに[デバイスプロファイルを割り当て](../intune/configuration/device-profile-assign.md#assign-a-device-profile)ます。 デバイスを別のドメインまたは Ou に参加させる必要がある場合は、さまざまなグループを使用できます。

> [!NOTE]
> Hybrid Azure AD Join 用の Windows Autopilot の名前付け機能では、%SERIAL% などの変数はサポートされません。サポートされるのは、コンピューター名のプレフィックスのみです。

## <a name="next-steps"></a>次のステップ

Windows Autopilot を構成した後は、これらのデバイスを管理する方法を学習します。 詳細については、「[Microsoft Intune デバイスの管理とは](../intune/remote-actions/device-management.md)」を参照してください。