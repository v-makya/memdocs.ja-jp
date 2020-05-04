---
title: チュートリアル - Microsoft Intune で管理用テンプレートを作成する - Azure | Microsoft Docs
description: このチュートリアルまたはウォークスルーでは、Microsoft Intune を使用して、Windows 10 以降のデバイスで Office、Windows、および Microsoft Edge の ADMX テンプレートを構成します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/31/2020
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41a2dce895761053e482fe029e4599819a099ac6
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254862"
---
# <a name="tutorial-use-the-cloud-to-configure-group-policy-on-windows-10-devices-with-admx-templates-and-microsoft-intune"></a>チュートリアル:クラウドを使用して、ADMX テンプレートと Microsoft Intune で Windows 10 デバイスにグループ ポリシーを構成する

> [!NOTE]
> このチュートリアルは、Microsoft Ignite のテクニカル ワークショップとして作成されました。 Intune とオンプレミスでの ADMX ポリシーの使用と構成を比較するため、一般的なチュートリアルよりも多くの前提条件があります。

グループ ポリシー管理用テンプレート (ADMX テンプレートとも呼ばれます) には、PC を含む Windows 10 デバイス上に構成できる設定が含まれています。 ADMX テンプレート設定は、さまざまなサービスで使用できます。 これらの設定は、Microsoft Intune などのモバイル デバイス管理 (MDM) プロバイダーによって使用されます。 たとえば、PowerPoint でデザイン アイデアをオンにしたり、Microsoft Edge でホーム ページを設定したり、Internet Explorer で ActiveX コントロールをブロックしたりといったことができます。

ADMX テンプレートは次のサービスで使用できます。

- **Microsoft Edge**:[Microsoft Edge ポリシー ファイル](https://www.microsoftedgeinsider.com/en-us/enterprise)でダウンロードします。
- **Office**: [Microsoft 365 アプリ、Office 2019、Office 2016](https://www.microsoft.com/download/details.aspx?id=49030)でダウンロードします。
- **Windows**: Windows 10 OS に組み込まれています。

ADMX ポリシーの詳細については、「[ADMX ベースのポリシーについて](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies)」を参照してください。

これらのテンプレートは Microsoft Intune に組み込まれており、**管理用テンプレート** プロファイルとして使用できます。 このプロファイル内に、含めたい設定を構成します。その後、このプロファイルをデバイスに "割り当て" ます。

このチュートリアルでは次のことを行います。

> [!div class="checklist"]
> * [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) の概要を学習します。
> * ユーザー グループを作成し、デバイス グループを作成します。
> * Intune での設定をオンプレミスの ADMX 設定と比較します。
> * さまざまな管理用テンプレートを作成し、異なるグループを対象とする設定を構成します。

このラボを終了すると、Intune と Microsoft 365 を使用してユーザーの管理を開始し、管理用テンプレートを展開するスキルが得られます。

この機能は、以下に適用されます。

- Windows 10 バージョン 1709 以降

## <a name="prerequisites"></a>[前提条件]

- Microsoft 365 E3 または E5 サブスクリプション (これらには Intune と Azure Active Directory (AD) Premium が含まれます)。 E3 または E5 サブスクリプションをお持ちでない場合は、[無料で試用](https://docs.microsoft.com/office365/admin/try-or-buy-microsoft-365?view=o365-worldwide)できます。

  さまざまな Microsoft 365 ライセンスの内容について詳しくは、「[エンタープライズを Microsoft 365 で変革](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans)」を参照してください。

- Microsoft Intune は **Intune MDM 機関**として構成されています。 詳細については、「[モバイル デバイス管理機関の設定](../fundamentals/mdm-authority-set.md)」を参照してください。

  > [!div class="mx-imgBorder"]
  > ![テナントの状態で MDM 機関を Microsoft Intune に設定する](./media/tutorial-walkthrough-administrative-templates/tenant-status.png)

- オンプレミスの Active Directory ドメイン コントローラー (DC) 上で次のことを行います。

  1. 次の Office テンプレートと Microsoft Edge テンプレートを[セントラル ストア (SYSVOL フォルダー)](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra) にコピーします。

      - [Office 管理用テンプレート](https://www.microsoft.com/download/details.aspx?id=49030)
      - [Microsoft Edge 管理用テンプレート > ポリシー ファイル](https://www.microsoftedgeinsider.com/en-us/enterprise)

  2. これらのテンプレートを DC と同じドメインにある Windows 10 Enterprise 管理者コンピューターにプッシュするグループ ポリシーを作成します。 このチュートリアルの内容:

      - これらのテンプレートを使用して作成したグループ ポリシーは **OfficeandEdge** と呼ばれます。 この名前が画像に表示されます。
      - 使用する Windows 10 Enterprise 管理者コンピューターは、**管理者コンピューター**と呼ばれます。

      一部の組織では、ドメイン管理者に次の 2 つのアカウントがあります。  
        - 一般的なドメイン職場アカウント
        - グループ ポリシーなど、ドメイン管理者のタスクにのみ使用される別のドメイン管理者アカウント

      この**管理者コンピューター**の目的は、管理者がドメイン管理者アカウントでサインインすることと、グループ ポリシーを管理するために設計されたツールにアクセスすることです。

- この**管理者コンピューター**上で次のことを行います。

  - ドメイン管理者アカウントを使用してサインインします。

  - **RSAT: グループ ポリシーの管理ツール**をインストールします。

    1. **[設定]** アプリ > **[アプリ]**  >  **[オプション機能]**  >  **[機能の追加]** を開きます。
    2. **[RSAT: グループ ポリシーの管理ツール]**  >  **[インストール]** を選択します。

        Windows によって機能がインストールされる間待ちます。 完了すると、最終的に **Windows 管理ツール** アプリに表示されます。

        > [!div class="mx-imgBorder"]
        > ![Windows 管理ツール アプリ (グループ ポリシーの管理アプリを含む)](./media/tutorial-walkthrough-administrative-templates/windows-administrative-tools-app.png)

  - インターネットにアクセスできること、Microsoft 365 サブスクリプション (Endpoint Manager admin center を含む) に対する管理者権限があることを確認してください。

## <a name="open-the-endpoint-manager-admin-center"></a>Endpoint Manager admin center を開く

1. Microsoft Edge バージョン 77 以降などの Chromium Web ブラウザーを開きます。
2. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に移動します。 次のアカウントでサインインします。

    **ユーザー**: Microsoft 365 テナント サブスクリプションの管理者アカウントを入力します。  
    **パスワード**: パスワードを入力します。

この admin center はデバイス管理に重点を置いており、Azure AD や Intune などの Azure サービスが含まれています。 **Azure Active Directory** と **Intune** のブランドが表示されない場合がありますが、それらは使用されています。

[Microsoft 365 管理センター](https://admin.microsoft.com)から Endpoint Manager admin center を開くこともできます。

1. [https://admin.microsoft.com](https://admin.microsoft.com)に移動します。
2. Microsoft 365 テナント サブスクリプションの管理者アカウントでサインインします。
3. **[管理センター]** で、 **[すべての管理センター]**  >  **[Endpoint management]\(エンドポイント管理\)** を選択します。 Endpoint Manager admin center が開きます。

    > [!div class="mx-imgBorder"]
    > ![Microsoft 365 管理センターですべての管理センターを表示する](./media/tutorial-walkthrough-administrative-templates/microsoft365-admin-centers.png)

## <a name="create-groups-and-add-users"></a>グループを作成し、ユーザーを追加する

オンプレミスのポリシーは LSDOU、つまりローカル、サイト、ドメイン、組織単位 (OU) という順序で適用されます。 この階層では、OU ポリシーによってローカル ポリシーが上書きされ、ドメイン ポリシーによってサイト ポリシーが上書きされる、というように上書きされていきます。

Intune では、作成したユーザーとグループにポリシーが適用されます。 階層はありません。 2 つのポリシーによって同じ設定が更新された場合、設定は競合として表示されます。 2 つのコンプライアンス ポリシーが競合している場合は、最も制限の厳しいポリシーが適用されます。 2 つの構成プロファイルが競合している場合、設定は適用されません。 詳細については、[デバイス ポリシーとプロファイルの一般的な質問、問題と解決策](device-profile-troubleshoot.md#if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied)のページを参照してください。

次に示す手順では、セキュリティ グループを作成し、ユーザーをこれらのグループに追加します。 1 人のユーザーを複数のグループに追加できます。 たとえば、1 人のユーザーが複数のデバイス (職場用の Surface Pro、個人用の Android モバイル デバイスなど) を持っていることは普通のことです。 そして、ユーザーはそれら複数のデバイスから電子メールやその他の組織リソースにアクセスします。

1. Endpoint Manager admin center で、 **[グループ]**  >  **[新しいグループ]** を選択します。

2. 次の設定を入力します。

    - **[グループの種類]** : **[セキュリティ]** を選択します。
    - **[グループ名]** :「**All Windows 10 student devices**」と入力します。
    - **[メンバーシップの種類]** : **[割り当て済み]** を選択します。

3. **[メンバー]** を選択し、いくつかのデバイスを追加します。

    デバイスの追加はオプションです。 目標は、グループの作成を練習すること、およびデバイスの追加方法を理解することです。 このチュートリアルを運用環境で使用している場合は、実行している内容に注意してください。

4. **[選択]**  >  **[作成]** で変更を保存します。

    該当のグループが見つからない場合は、 **[更新]** を選択します。

5. **[新しいグループ]** を選択し、次の設定を入力します。

    - **[グループの種類]** : **[セキュリティ]** を選択します。
    - **[グループ名]** :「**All Windows devices**」と入力します。
    - **[メンバーシップの種類]** : **[動的デバイス]** を選択します。
    - **[動的なデバイス メンバー]** : **[動的クエリの追加]** を選択し、クエリを構成します。

        - **プロパティ**: **[deviceOSType]** を選択します。
        - **演算子**: **[次の値と等しい]** を選択します。
        - **値**:「**Windows**」と入力します。

        1. **[式の追加]** を選択します。 式は、 **[規則の構文]** に表示されます。

            > [!div class="mx-imgBorder"]
            > ![動的クエリを作成し、Microsoft Intune 管理用テンプレートに式を追加する](./media/tutorial-walkthrough-administrative-templates/dynamic-group-query.png)

            ユーザーまたはデバイスが入力した条件を満たしている場合、それらは自動的に動的グループに追加されます。 この例では、デバイスのオペレーティング システムが Windows の場合、デバイスは自動的にこのグループに追加されます。 このチュートリアルを運用環境で使用している場合は、注意してください。 目標は、動的グループの作成を練習することです。

        2. **[保存]**  >  **[作成]** を選択して変更を保存します。

6. 次の設定を使用して、**All Teachers** グループを作成します。

    - **[グループの種類]** : **[セキュリティ]** を選択します。
    - **[グループ名]** :「**All Teachers**」と入力します。
    - **[メンバーシップの種類]** : **[動的ユーザー]** を選択します。
    - **[動的なユーザー メンバー]** : **[動的クエリの追加]** を選択し、クエリを構成します。

      - **プロパティ**: **[department]** を選択します。
      - **演算子**: **[次の値と等しい]** を選択します。
      - **値**:「**Teachers**」と入力します。

        1. **[式の追加]** を選択します。 式は、 **[規則の構文]** に表示されます。

            ユーザーまたはデバイスが入力した条件を満たしている場合、それらは自動的に動的グループに追加されます。 この例では、ユーザーの department が Teachers の場合、ユーザーは自動的にこのグループに追加されます。 組織にユーザーを追加するときに、department やその他のプロパティを入力できます。 このチュートリアルを運用環境で使用している場合は、注意してください。 目標は、動的グループの作成を練習することです。

        2. **[保存]**  >  **[作成]** を選択して変更を保存します。

### <a name="talking-points"></a>要点

- 動的グループは、Azure AD Premium の機能です。 Azure AD Premium をお持ちでない場合は、割り当てられたグループを作成するライセンスのみが付与されます。 動的なグループの詳細については、以下を参照してください。

  - [Azure Active Directory での動的グループ メンバーシップ (パート 1)](https://blogs.technet.microsoft.com/pauljones/2017/08/28/dynamic-group-membership-in-azure-active-directory-part-1/)
  - [Azure Active Directory での動的グループ メンバーシップ (パート 2)](https://blogs.technet.microsoft.com/pauljones/2017/08/29/dynamic-group-membership-in-azure-active-directory-part-2/)

- Azure AD Premium には、[多要素認証 (MFA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) や[条件付きアクセス](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)など、アプリとデバイスを管理するときに一般的に使用されるその他のサービスが含まれています。

- 多くの管理者の疑問は、どのような場合にユーザー グループを使用し、どのような場合にデバイス グループを使用するのかということです。 いくつかのガイダンスについては、「[ユーザー グループとデバイス グループ](device-profile-assign.md#user-groups-vs-device-groups)」を参照してください。

- 注意点として、ユーザーは複数のグループに属することができます。 作成できる他の動的ユーザー グループおよび動的デバイス グループとして、次のようなグループが考えられます。

  - すべての学生
  - すべての Android デバイス
  - すべての iOS または iPadOS デバイス
  - Marketing
  - 人事
  - シャーロットの全従業員
  - レドモンドの全従業員
  - 西海岸の IT 管理者
  - 東海岸の IT 管理者

作成したユーザーとグループは、[Microsoft 365 管理センター](https://admin.microsoft.com)、Azure portal 上の Azure AD、[Azure portal 上の Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2090973) にも表示されます。 ご自身のテナント サブスクリプションにおいて、これらのすべての領域でグループを作成および管理できます。 **デバイス管理を目標としている場合は、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) を使用することをお勧めします**。

### <a name="review-group-membership"></a>グループ メンバーシップの確認

1. Endpoint Manager admin center で、 **[ユーザー]** を選択し、任意の既存ユーザーの名前を選択します。

    > [!div class="mx-imgBorder"]
    > ![Endpoint Manager admin center で [ユーザー] を選択する](./media/tutorial-walkthrough-administrative-templates/select-users-endpoint-manager-admin-center.png)

2. 追加または変更できる情報の一部を確認します。 たとえば、役職、部署、市区町村、オフィスの所在地など、構成できるプロパティを確認します。 動的なグループを作成するときに、これらのプロパティを動的クエリで使用できます。
3. **[グループ]** を選択して、このユーザーのメンバーシップを表示します。 グループからユーザーを削除することもできます。
4. その他のオプションをいくつか選択して、詳細情報と実行できる操作を表示します。 たとえば、割り当てられているライセンス、ユーザーのデバイスなどを確認します。

### <a name="what-did-i-just-do"></a>行ったことの確認

Endpoint Manager admin center で、新しいセキュリティ グループを作成し、既存のユーザーとデバイスをこれらのグループに追加しました。 これらのグループは、このチュートリアルの後の手順で使用します。

## <a name="create-a-template-in-intune"></a>Intune でテンプレートを作成する

このセクションでは、Intune で管理用テンプレートを作成し、 **[グループ ポリシーの管理]** でいくつかの設定を確認して、Intune で同じ設定を比較します。 目標は、グループ ポリシーで設定を表示し、Intune で同じ設定を表示することです。

1. Endpoint Manager admin center で、 **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
2. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイル]** : **[管理用テンプレート]** を選択します。

3. **[作成]** を選択します。
4. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「**Admin template - Windows 10 student devices**」と入力します。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

5. **[次へ]** を選択します。
6. **[構成設定]** で、設定がデバイス ( **[コンピューターの構成]** ) に適用され、設定がユーザー ( **[ユーザーの構成]** ) に適用されます。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune エンドポイント マネージャーでユーザーとデバイスに ADMX テンプレート設定を適用する](./media/tutorial-walkthrough-administrative-templates/administrative-templates-choose-computer-user-configuration.png)

7. **[コンピューターの構成]**  >  **[Microsoft Edge]** を展開し、 **[SmartScreen の設定]** を選択します。 ポリシーへのパスと使用可能なすべての設定を確認します。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune の ADMX テンプレートで Microsoft Edge SmartScreen ポリシー設定を参照する](./media/tutorial-walkthrough-administrative-templates/computer-configuration-microsoft-edge-smartscreen-path.png)

8. [検索] に「**ダウンロード**」と入力します。 ポリシー設定がフィルター処理されています。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune ADMX テンプレートで Microsoft Edge SmartScreen ポリシー設定をフィルター処理する](./media/tutorial-walkthrough-administrative-templates/computer-configuration-microsoft-edge-smartscreen-search-download.png)

### <a name="open-group-policy-management"></a>グループ ポリシーの管理を開く

このセクションでは、Intune でポリシーを表示し、それに対応するポリシーをグループ ポリシー管理エディターで表示します。

#### <a name="compare-a-device-policy"></a>デバイス ポリシーの比較

1. **管理者コンピューター**で、**グループ ポリシーの管理**アプリを開きます。

    このアプリは **RSAT: グループ ポリシーの管理ツール** (Windows にインストールするオプションの機能) と共にインストールされます。 この記事の「[前提条件](#prerequisites)」にインストール手順が記載されています。

2. **[ドメイン]** を展開し、目的のドメインを選択します。 たとえば、**contoso.net** を選択します。
3. **OfficeandEdge** ポリシーを右クリックし、 **[編集]** を選択します。 グループ ポリシー管理エディター アプリが開きます。

    > [!div class="mx-imgBorder"]
    > ![Office と Microsoft Edge の ADMX グループ ポリシーを右クリックし、[編集] を選択する](./media/tutorial-walkthrough-administrative-templates/open-group-policy-management.png)

    **OfficeandEdge** は、Office および Microsoft Edge の ADMX テンプレートを含むグループ ポリシーです。 このポリシーについては、この記事の「[前提条件](#prerequisites)」で説明しています。

4. **[コンピューターの構成]**  >  **[ポリシー]**  >  **[管理用テンプレート]**  >  **[コントロール パネル]**  >  **[個人用設定]** の順に展開します。 利用可能な設定は次のとおりです。

    > [!div class="mx-imgBorder"]
    > ![グループ ポリシー管理エディターで [コンピューターの構成] を展開し、[個人用設定] に移動する](./media/tutorial-walkthrough-administrative-templates/open-group-policy-management-editor-admx-policy.png)

    **[ロック画面カメラを有効にできないようにする]** をダブルクリックし、使用可能なオプションを確認します。

    > [!div class="mx-imgBorder"]
    > ![グループ ポリシーの [コンピューターの構成] の設定オプションを確認する](./media/tutorial-walkthrough-administrative-templates/prevent-enabling-lock-screen-camera-admx-policy.png)

5. Endpoint Manager admin center で、**Admin template - Windows 10 student devices** テンプレートに移動します。
6. **[コンピューターの構成]**  >  **[コントロール パネル]**  >  **[個人用設定]** を選択します。 利用可能な設定は次のとおりです。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune での個人用設定のポリシー設定のパス](./media/tutorial-walkthrough-administrative-templates/computer-configuration-control-panel-personalization-path.png)

    設定の種類は **[デバイス]** で、パスは " **/コントロール パス/個人用設定**" です。 このパスはグループ ポリシー管理エディターで見たものと似ています。 **[ロック画面でカメラを有効にできないようにする]** 設定を開くと、グループ ポリシー管理エディターで見たのと同じ **[未構成]** 、 **[有効]** 、 **[無効]** のオプションが表示されます。

#### <a name="compare-a-user-policy"></a>ユーザー ポリシーの比較

1. 管理者テンプレートで、 **[コンピューターの構成]**  >  **[すべての設定]** を選択して、**InPrivate ブラウズ**を検索します。 パスに注意してください。

    **[ユーザーの構成]** に対しても同じ操作を行います。 **[すべての設定]** を選択し、**InPrivate ブラウズ**を検索します。

2. **グループ ポリシー管理エディター**で、対応するユーザーとデバイスの設定を見つけます。

    - デバイス: **[コンピューターの構成]**  >  **[ポリシー]**  >  **[管理用テンプレート]**  >  **[Windows コンポーネント]**  >  **[Internet Explorer]**  >  **[プライバシー]**  >  **[InPrivate ブラウズを無効にする]** の順に展開します。
    - ユーザー: **[ユーザーの構成]**  >  **[ポリシー]**  >  **[管理用テンプレート]**  >  **[Windows コンポーネント]**  >  **[Internet Explorer]**  >  **[プライバシー]**  >  **[InPrivate ブラウズを無効にする]** の順に展開します。

    > [!div class="mx-imgBorder"]
    > ![ADMX テンプレートを使用して Internet Explorer での InPrivate ブラウズを無効にする](./media/tutorial-walkthrough-administrative-templates/group-policy-turn-off-inprivate-browsing.png)

> [!TIP]
> 組み込みの Windows ポリシーを表示するには、GPEdit (**グループ ポリシーの編集**アプリ) を使用することもできます。

#### <a name="compare-an-edge-policy"></a>Microsoft Edge ポリシーの比較

1. Endpoint Manager admin center で、**Admin template - Windows 10 student devices** テンプレートに移動します。
2. **[コンピューターの構成]**  >  **[Microsoft Edge]**  >  **[Startup, homepage and new tab page]\(スタートアップ、ホームページ、新しいタブ ページ\)** の順に展開します。 利用可能な設定は次のとおりです。

    **[ユーザーの構成]** に対しても同じ操作を行います。

3. グループ ポリシー管理エディターで、次の設定を見つけます。

    - デバイス: **[コンピューターの構成]**  >  **[ポリシー]**  >  **[管理用テンプレート]**  >  **[Microsoft Edge]**  >  **[Startup, homepage and new tab page]\(スタートアップ、ホームページ、新しいタブ ページ\)** の順に展開します。
    - ユーザー: **[ユーザーの構成]**  >  **[ポリシー]**  >  **[管理用テンプレート]**  >  **[Microsoft Edge]**  >  **[Startup, homepage and new tab page]\(スタートアップ、ホームページ、新しいタブ ページ\)** の順に展開します。

### <a name="what-did-i-just-do"></a>行ったことの確認

Intune で管理用テンプレートを作成しました。 このテンプレートでは、いくつかの ADMX 設定を確認し、同じ ADMX 設定をグループ ポリシーの管理で確認しました。

## <a name="add-settings-to-the-students-admin-template"></a>Students 管理用テンプレートに設定を追加する

このテンプレートでは、いくつかの Internet Explorer 設定を構成して、複数の学生が共有するデバイスをロックダウンします。

1. **Admin template - Windows 10 student devices** で、 **[コンピューターの構成]** を展開して **[すべての設定]** を選択し、"**InPrivate ブラウズを無効にする**" を検索します。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune の管理用テンプレートで InPrivate ブラウズを無効にするデバイス ポリシー](./media/tutorial-walkthrough-administrative-templates/turn-off-inprivate-browsing-administrative-template.png)

2. **[InPrivate ブラウズを無効にする]** 設定を選択します。 このウィンドウで、説明と設定できる値を確認します。 これらのオプションは、グループ ポリシーに表示されるものと似ています。
3. **[有効]**  >  **[OK]** を選択して変更を保存します。
4. また、次の Internet Explorer の設定も構成します。 必ず **[OK]** を選択して変更を保存してください。

    - **ファイルのドラッグ/ドロップ、またはコピー/貼り付けの許可**
      - **種類**:デバイス
      - **パス**: \Windows コンポーネント\Internet Explorer\インターネット コントロール パネル\セキュリティ ページ\インターネット ゾーン
      - **値**:無効

    - **証明書エラーを無視できないようにする**
      - **種類**:デバイス
      - **パス**: \Windows コンポーネント\Internet Explorer\インターネット コントロール パネル
      - **値**:Enabled

    - **ホーム ページの設定の変更を許可しない**
      - **種類**:ユーザー
      - **パス**: \Windows コンポーネント\Internet Explorer
      - **値**:Enabled
      - **ホーム ページ**: `contoso.com` などの URL を入力します。

5. 検索フィルターをクリアします。 構成した設定が上部に表示されていることに注意してください。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune で構成した設定が上部に表示される](./media/tutorial-walkthrough-administrative-templates/configured-settings-administrative-template.png)

### <a name="assign-your-template"></a>テンプレートの割り当て

1. テンプレートで、 **[割り当て]** に移動するまで **[次へ]** を選択します。 **[含めるグループを選択]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune のデバイス構成プロファイルの一覧から管理用テンプレート プロファイルを選択する](./media/tutorial-walkthrough-administrative-templates/filter-administrative-template-device-configuration-profiles-list.png)

2. 既存のユーザーとグループの一覧が表示されます。 前の手順で作成した **All Windows 10 student devices** グループ > **[選択]** を選択します。

    このチュートリアルを運用環境で使用している場合は、空のグループを追加することを検討してください。 目標は、テンプレートの割り当てを練習することです。

3. **[次へ]** を選択します。 **[確認および作成]** で **[作成]** を選択し、変更内容を保存します。

プロファイルを保存するとすぐに、デバイスの Intune へのチェックイン時にプロファイルがデバイスに適用されるようになります。 デバイスがインターネットに接続されている場合、これはすぐに実行されます。 ポリシー更新時間の詳細については、「[デバイスへのポリシー、プロファイル、アプリの割り当て後にそれらが取得されるまでどれくらいの時間がかかりますか?](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)」を参照してください。

厳密または制限の厳しいポリシーとプロファイルを割り当てる場合、自分自身をロックアウトしないようにしてください。ポリシーとプロファイルから除外されたグループを作成することを検討してください。 これは、トラブルシューティングへのアクセスを確保するための考え方です。 このグループを監視して、意図したとおりに使用されていることを確認します。

### <a name="what-did-i-just-do"></a>行ったことの確認

Endpoint Manager admin center で、管理用テンプレートのデバイス構成プロファイルを作成し、このプロファイルを作成したグループに割り当てました。

## <a name="create-a-onedrive-template"></a>OneDrive テンプレートを作成する

このセクションでは、いくつかの設定を制御するための OneDrive 管理用テンプレートを Intune で作成します。 これらの特定の設定が選ばれたのは、組織でよく使用される設定であるためです。

1. 別のプロファイルを作成します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** )。

2. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイル]** : **[管理用テンプレート]** を選択します。

3. **[作成]** を選択します。
4. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:「**Admin template - OneDrive policies that apply to all Windows 10 users**」と入力します。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

5. **[次へ]** を選択します。
6. **[構成設定]** で、次の設定を構成します。 必ず **[OK]** を選択して変更を保存してください。

    - **[コンピューターの構成]**  >  **[すべての設定]** : 
      - **Windows 資格情報を使用して OneDrive 同期クライアントにユーザーをサイレント モードでサインインする**
        - **種類**:デバイス
        - **値**:Enabled
      - **OneDrive ファイル オンデマンドを使用する**
        - **種類**:デバイス
        - **値**:Enabled

    - **[ユーザーの構成]**  >  **[すべての設定]** : 
      - **ユーザーが個人用の OneDrive アカウントを同期できないようにする**
        - **種類**:ユーザー
        - **値**:Enabled

設定は次のようになります。

> [!div class="mx-imgBorder"]
> ![Microsoft Intune で OneDrive 管理用テンプレートを作成する](./media/tutorial-walkthrough-administrative-templates/one-drive-administrative-template.png)

OneDrive クライアント設定の詳細については、「[グループ ポリシーを使用し、OneDrive 同期設定を制御する](https://docs.microsoft.com/onedrive/use-group-policy)」を参照してください。

### <a name="assign-your-template"></a>テンプレートの割り当て

1. テンプレートで、 **[割り当て]** に移動するまで **[次へ]** を選択します。 **[含めるグループを選択]** を選択します。
2. 既存のユーザーとグループの一覧が表示されます。 前の手順で作成した **All Windows devices** グループ > **[選択]** を選択します。

    このチュートリアルを運用環境で使用している場合は、空のグループを追加することを検討してください。 目標は、テンプレートの割り当てを練習することです。

3. **[次へ]** を選択します。 **[確認および作成]** で **[作成]** を選択し、変更内容を保存します。

この時点で、管理用テンプレートをいくつか作成し、作成したグループにそれらのテンプレートを割り当てました。 次の手順では、Windows PowerShell と Microsoft Graph API for Intune を使用して、管理用テンプレートを作成します。

## <a name="optional-create-a-policy-using-powershell-and-graph-api"></a>オプション:PowerShell と Graph API を使用してポリシーを作成する

このセクションでは以下のリソースを使用します。 このセクションでこれらのリソースをインストールします。

- [Intune PowerShell SDK](https://github.com/microsoft/Intune-PowerShell-SDK)
- [Microsoft Graph API for Intune](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0)

1. **管理者コンピューター**で、管理者として **Windows PowerShell** を開きます。

    1. 検索バーに「**powershell**」と入力します。
    2. **[Windows PowerShell] を右クリック** >  **[管理者として実行]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![管理者として Windows PowerShell を実行する](./media/tutorial-walkthrough-administrative-templates/run-windows-powershell-administrator.png)

2. 実行ポリシーを取得して設定します。

    1. 次のように入力します: `get-ExecutionPolicy`

        何に設定されているか (**Restricted** など) を書き留めておきます。 チュートリアルを完了したら、元の値に戻します。

    2. 次のように入力します: `Set-ExecutionPolicy -ExecutionPolicy Unrestricted`

    3. 変更するには「`Y`」を入力します。

    PowerShell の実行ポリシーを使用すると、悪意のあるスクリプトの実行を防ぐことができます。 詳細については、「[実行ポリシーについて](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies)」を参照してください。

3. 次のように入力します: `Install-Module -Name Microsoft.Graph.Intune`

    次の場合は、「`Y`」を入力します。

    - NuGet プロバイダーをインストールするように求められる
    - 信頼されていないリポジトリからモジュールをインストールするように求められる

    完了するまで数分かかる場合があります。 完了すると、次のようなプロンプトが表示されます。

    > [!div class="mx-imgBorder"]
    > ![モジュールをインストールした後の Windows PowerShell プロンプト](./media/tutorial-walkthrough-administrative-templates/powershell-prompt.png)

4. 使用している Web ブラウザーで [https://github.com/Microsoft/Intune-PowerShell-SDK/releases](https://github.com/Microsoft/Intune-PowerShell-SDK/releases) にアクセスし、**Intune-PowerShell-SDK_v6.1907.00921.0001.zip** ファイルを選択します。

    1. **[名前を付けて保存]** を選択し、フォルダーを選択します。そのフォルダーを覚えておいてください。 `c:\psscripts` を選択することをお勧めします。
    2. そのフォルダーを開き、.zip ファイルを右クリック > **[すべて展開]**  >  **[展開]** を選択します。 フォルダー構造は次のフォルダーのようになります。

        > [!div class="mx-imgBorder"]
        > ![展開後の Intune PowerShell SDK のフォルダー構造](./media/tutorial-walkthrough-administrative-templates/psscripts-directory.png)

5. **[表示]** タブで、 **[ファイル名拡張子]** をオンにします。

    > [!div class="mx-imgBorder"]
    > ![エクスプローラーの [表示] タブで [ファイル名拡張子] をオンにする](./media/tutorial-walkthrough-administrative-templates/file-names-extension.png)

6. そのフォルダーで、`c:\psscripts\Intune-PowerShell-SDK_v6.1907.00921.0001\drop\outputs\build\Release\net471` に移動します。 すべての .dll を右クリック > **[プロパティ]**  >  **[ブロックの解除]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![DLL のブロックを解除する](./media/tutorial-walkthrough-administrative-templates/unblock-dll.png)

7. **Windows PowerShell** アプリで、次のように入力します。

    ```powershell
    Import-Module c:\psscripts\Intune-PowerShell-SDK_v6.1907.00921.0001\drop\outputs\build\Release\net471\Microsoft.Graph.Intune.psd1
    ```

    信頼されていない発行元からの実行を確認するメッセージが表示されたら、「`R`」を入力します。

8. Intune 管理用テンプレートでは、ベータ版の Graph が使用されます。

    1. 次のように入力します: `Update-MSGraphEnvironment -SchemaVersion 'beta'`

    2. 次のように入力します: `Connect-MSGraph -AdminConsent`

    3. プロンプトが表示されたら、同じ Microsoft 365 管理者アカウントでサインインします。 これらのコマンドレットにより、テナント組織にポリシーを作成します。

        **ユーザー**: Microsoft 365 テナント サブスクリプションの管理者アカウントを入力します。  
        **パスワード**: パスワードを入力します。

    4. **[承諾する]** を選択します。

9. **Test Configuration** という構成プロファイルを作成します。 次を入力します。

    ```powershell
    $configuration = Invoke-MSGraphRequest -Url https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations -Content '{"displayName":"Test Configuration","description":"A test configuration created through PS"}' -HttpMethod POST
    ```

    これらのコマンドレットが正常に実行されると、プロファイルが作成されます。 確認するには、Endpoint Manager admin center > **[構成プロファイル]** に移動します。 **Test Configuration** プロファイルが表示されるはずです。

10. すべての SettingDefinitions を取得します。 次を入力します。

    ```powershell
    $settingDefinitions = Invoke-MSGraphRequest -Url https://graph.microsoft.com/beta/deviceManagement/groupPolicyDefinitions -HttpMethod GET
    ```

11. 設定の表示名を使用して定義 ID を検索します。 次を入力します。

    ```powershell
    $desiredSettingDefinition = $settingDefinitions.value | ? {$_.DisplayName -Match "Silently sign in users to the OneDrive sync client with their Windows credentials"}
    ```

12. 設定を構成します。 次を入力します。

    ```powershell
    $configuredSetting = Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues" -Content ("{""enabled"":""true"",""configurationType"":""policy"",""definition@odata.bind"":""https://graph.microsoft.com/beta/deviceManagement/groupPolicyDefinitions('$($desiredSettingDefinition.id)')""}") -HttpMethod POST
    ```

    ```powershell
    Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues('$($configuredSetting.id)')" -Content ("{""enabled"":""false""}") -HttpMethod PATCH
    ```

    ```powershell
    $configuredSetting = Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues('$($configuredSetting.id)')" -HttpMethod GET
    ```

### <a name="see-your-policy"></a>ポリシーの確認

1. Endpoint Manager admin center > **[構成プロファイル]**  >  **[更新]** を選択します。
2. **Test Configuration** プロファイル > **[設定]** を選択します。
3. ドロップダウン リストで **[すべての製品]** を選択します。

**[Windows 資格情報を使用して OneDrive 同期クライアントにユーザーをサイレント モードでサインインする]** 設定が構成されていることがわかります。

## <a name="policy-best-practices"></a>ポリシーのベスト プラクティス

Intune でポリシーとプロファイルを作成する場合、考慮する必要がある推奨事項とベスト プラクティスがいくつかあります。 詳細については、[ポリシーとプロファイルのベスト プラクティス](device-profile-create.md#recommendations)に関するページを参照してください。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

不要になったら、次のことができます。

- 作成したグループを削除します。

  - **All Windows 10 student devices**
  - **All Windows devices**
  - **All Teachers**

- 作成した管理用テンプレートを削除します。

  - **Admin template - Windows 10 student devices**
  - **Admin template - OneDrive policies that apply to all Windows 10 users**
  - **Test Configuration**

- Windows PowerShell 実行ポリシーを元の値に戻します。 次の例では、実行ポリシーを Restricted に設定しています。

  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy Restricted
  ```

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) について理解し、クエリ ビルダーを使用して動的グループを作成しました。そして、Intune で管理用テンプレートを作成して [ADMX 設定](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies)を構成しました。 また、オンプレミスでの ADMX テンプレートの使用を Intune によるクラウドでの使用と比較しました。 さらに、PowerShell コマンドレットを使用して管理用テンプレートを作成しました。

Intune での管理用テンプレートの詳細については、次を参照してください: 

> [!div class="nextstepaction"]
> [Windows 10 テンプレートを使用し、Microsoft Intune でグループ ポリシー設定を構成する](administrative-templates-windows.md)
