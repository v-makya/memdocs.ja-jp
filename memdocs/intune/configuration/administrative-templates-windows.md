---
title: Microsoft Intune で Windows 10 デバイス用のテンプレートを使用する - Azure | Microsoft Docs
description: Microsoft Intune とエンドポイント マネージャーで管理用テンプレートを使用して、Windows 10 デバイスの設定のグループを作成します。 デバイス構成プロファイルでこれらの設定を使用して、Office プログラムや Microsoft Edge の制御、Internet Explorer の機能のセキュリティ保護、OneDrive へのアクセスの制御、リモート デスクトップ機能の使用、自動再生の有効化、電源管理の設定、HTTP 印刷の使用、さまざまなユーザー サインイン オプションの使用、イベント ログ サイズの制御を行います。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f609ec62259deffb220c8ee935d0f10a98ae77b5
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254896"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Windows 10 テンプレートを使用し、Microsoft Intune でグループ ポリシー設定を構成する

組織でデバイスを管理するとき、さまざまなデバイス グループに適用される設定のグループを作成することが推奨されます。 たとえば、いくつかのデバイス グループがあるとします。 グループ A には、特定の設定のセットを割り当てます。 グループ B には、別の設定のセットを割り当てます。 また、構成できる設定の単純なビューも必要です。

このタスクを完了するには、Microsoft Intune で**管理用テンプレート**を使用します。 管理用テンプレートには、Microsoft Edge バージョン 77 以降、Internet Explorer、Microsoft Office プログラム、リモート デスクトップ、OneDrive、パスワードと PIN などの機能を制御するための、数百の設定が含まれています。 グループ管理者は、これらの設定により、クラウドを使ってグループ ポリシーを管理できます。

この機能は、以下に適用されます。

- Windows 10 以降

Windows の設定は、Active Directory (AD) のグループ ポリシー (GPO) 設定に似ています。 これらの設定は、Windows に組み込みの、XML を使用する [ADMX ベースの設定](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) です。 Office と Microsoft Edge の設定には ADMX が取り込まれていて、[Office の管理用テンプレート ファイル](https://www.microsoft.com/download/details.aspx?id=49030)と [Microsoft Edge 管理用テンプレート ファイル](https://www.microsoftedgeinsider.com/enterprise)で ADMX 設定が使われています。 そして、Intune のテンプレートは 100% クラウドベースです。 これらによって、設定を構成し、必要な設定を見つけるための、簡単で明快な方法が提供されます。

**管理用テンプレート**は Intune 内に構築されており、OMA-URI の使用を含め、カスタマイズを必要としません。 モバイル デバイス管理 (MDM) ソリューションの一部として、これらのテンプレート設定を総合ポータルとして使用し、Windows 10 デバイスを管理します。

この記事では、Windows 10 デバイス用のテンプレートを作成する手順を示し、Intune で使用可能なすべての設定をフィルター処理する方法について説明します。 テンプレートを作成すると、デバイス構成プロファイルが作成されます。 その後、組織内でこのプロファイルを Windows 10 デバイスに割り当てるかデプロイできます。

## <a name="before-you-begin"></a>始める前に

- これらの設定の一部は、Windows 10 バージョン 1709 (RS2/ビルド 15063) 以降で使用可能です。 すべての Windows エディションに含まれているわけではない設定もあります。 最適なエクスペリエンスを得るには、Windows 10 Enterprise バージョン 1903 (19H1/ビルド 18362) 以降を使用することをお勧めします。

- Windows の設定では、[Windows ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies) が使用されます。 CSP は、Home、Professional、Enterprise など、さまざまなエディションの Windows で動作します。 CSP が特定のエディションで動作するかどうかを確認するには、[Windows ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies) に移動してください。

## <a name="create-the-template"></a>テンプレートを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイル]** : **[管理用テンプレート]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、次は適切なプロファイル名です: 「**管理テンプレート:Microsoft Edge の xyz 設定を構成する Windows 10 管理テンプレート**」。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** で、デバイスに適用される設定 ( **[コンピューターの構成]** ) と、ユーザーに適用される設定 ( **[ユーザーの構成]** ) を構成します。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune エンドポイント マネージャーでユーザーとデバイスに ADMX テンプレート設定を適用する](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. **[コンピューターの構成]** を選択すると、設定のカテゴリが表示されます。 任意のカテゴリを選択して、使用可能な設定を確認できます。

    たとえば、Internet explorer に適用されるすべてのデバイス設定を表示するには、 **[コンピューターの構成]**  >  **[Windows コンポーネント]**  >  **[Internet Explorer]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune エンドポイント マネージャーで Internet Explorer に適用されるすべてのデバイス設定を表示する](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

9. また、 **[すべての設定]** を選択して、すべてのデバイス設定を表示することもできます。 さらに設定を表示するには、下へスクロールして戻る矢印と次へ矢印を使用します。

    > [!div class="mx-imgBorder"]
    > ![設定のサンプル一覧を表示し、戻るボタンと次へボタンを使用する](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. 任意の設定を選択します。 たとえば、 **[Office]** でフィルター処理して、 **[参照の制限を有効にする]** を選択します。 設定の詳細説明が表示されます。 **[有効]** 、 **[無効]** を選択するか、または設定を **[未構成]** (既定値) のままにします。 詳細な説明では、 **[有効]** 、 **[無効]** 、または **[未構成]** を選択したときの動作についても説明されています。

    > [!TIP]
    > Intune の Windows の設定は、ローカル グループ ポリシー エディター (`gpedit`) に表示されるオンプレミスのグループ ポリシー パスに関連付けられます

11. **[OK]** を選択して変更を保存します。

    設定の一覧を移動し、環境内で必要な設定の構成に進みます。 次に例をいくつか示します。

    - **[VBA マクロ通知設定]** を使用して、Word や Excel などのさまざまな Microsoft Office プログラムで VBA マクロを処理します。
    - **[ファイルのダウンロードの許可]** 設定を使用して、Internet Explorer からのダウンロードを許可または禁止します。
    - **[コンピューターのスリープ状態の解除時にパスワードを要求する (電源接続時)]** を使用し、デバイスがスリープ モードから回復したときにユーザーにパスワードを求めるように設定します。
    - **[未署名の ActiveX コントロールのダウンロード]** 設定を使用して、Internet Explorer からユーザーが未署名の ActiveX コントロールをダウンロードできないようブロックします。
    - **[システムの復元をオフにする]** 設定を使用して、デバイスでユーザーがシステムの復元を実行するのを許可または禁止します。
    - **[Allow importing of favorites]\(お気に入りのインポートを許可する\)** 設定を使用し、別のブラウザーから Microsoft Edge にお気に入りをインポートする行為をユーザーに許可または禁止します。
    - ほかにも多数の設定があります。

12. **[次へ]** を選択します。
13. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](..//fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

14. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    プロファイルがユーザー グループに割り当てられている場合、ユーザーが登録し、サインインしたすべてのデバイスに、構成済みの ADMX 設定が適用されます。 プロファイルがデバイス グループに割り当てられている場合は、そのデバイスにサインインするすべてのユーザーに、構成済みの ADMX 設定が適用されます。 この割り当ては、ADMX 設定がコンピューター構成 (`HKEY_LOCAL_MACHINE`)、またはユーザー構成 (`HKEY_CURRENT_USER`) の場合に行われます。 一部の設定では、ユーザーに割り当てられたコンピューター設定が、そのデバイスの他のユーザーのエクスペリエンスに影響することもあります。
    
    詳細については、「[ユーザー グループとデバイス グループ](device-profile-assign.md#user-groups-vs-device-groups)」を参照してください。

    **[次へ]** を選択します。

15. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

デバイスによって次に構成の更新が確認されるときに、構成した設定が適用されます。

## <a name="find-some-settings"></a>一部の設定を見つける

これらのテンプレートで使用できる設定は数百に及びます。 特定の設定を見つけやすくするには、組み込みの機能を使用します。

- 使用するテンプレートで **[設定]** 、 **[状態]** 、 **[設定の種類]** 、または **[パス]** 列を選択し、一覧を並べ替えます。 たとえば、 **[パス]** 列を選択し、隣の矢印を使用して、`Microsoft Excel` パス内の設定を表示します。

- テンプレートで**検索**ボックスを使用して、特定の設定を見つけます。 設定またはパスで検索できます。 たとえば、「 `copy`」というメッセージを探してみてください。 「`copy`」を含むすべての設定が表示されます。

  > [!div class="mx-imgBorder"]
  > ![Intune の管理用テンプレートで「copy」と検索して、すべてのデバイス設定を表示する](./media/administrative-templates-windows/search-copy-settings.png) 

  もう 1 つの例として、「`microsoft word`」を検索します。 Microsoft Word プログラムに対して設定できる各設定が表示されます。 「`explorer`」を検索して、テンプレートに追加できる Internet Explorer の設定を確認します。

## <a name="next-steps"></a>次のステップ

テンプレートは作成されましたが、まだ何も実行できません。 次に、[テンプレート (プロファイルとも呼ばれる) を割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[管理用テンプレートを使用して Office 365](administrative-templates-update-office.md) を更新します。

[チュートリアル:クラウドを使用して、ADMX テンプレートと Microsoft Intune で Windows 10 デバイスにグループ ポリシーを構成する](tutorial-walkthrough-administrative-templates.md)
