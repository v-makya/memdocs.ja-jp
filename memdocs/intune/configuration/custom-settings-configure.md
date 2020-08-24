---
title: Microsoft Intune でカスタム デバイス設定を使用する - Azure | Microsoft Docs
description: Microsoft Intune を使用して Windows 8.1、Windows 10 以降、Android デバイス管理者、Android Enterprise、macOS、iOS/iPadOS のデバイスに対してカスタム設定を使用するためのプロファイルを追加または作成します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: aaa0deaf2c6332965f40ae02a47b7541cf2f9e8e
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146407"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Intune でカスタム設定を持つプロファイルを作成する

Microsoft Intune には、デバイスのさまざまな機能を制御する多くの組み込み設定が含まれます。 カスタム プロファイルを作成することもできます。その作成方法は組み込みのプロファイルと同様です。 カスタム プロファイルは、Intune に組み込まれていないデバイスの設定と機能を使用する場合に最適です。 これらのプロファイルには、組織のデバイスを制御するための機能と設定が含まれます。 たとえば、すべての iOS/iPadOS デバイスに対して同じ機能を設定するカスタム プロファイルを作成できます。

カスタム設定は、プラットフォームごとに構成が異なります。 たとえば、Android デバイスと Windows デバイスで機能を制御するには、Open Mobile Alliance Uniform Resource Identifier (OMA-URI) 値を入力できます。 Apple デバイスでは、[Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) または [Apple Profile Manager](https://support.apple.com/profile-manager) で作成したファイルをインポートできます。

構成プロファイルの詳細については、「[Microsoft Intune のデバイス プロファイルとは](device-profiles.md)」をご覧ください。

この記事では、Android デバイス管理者、Android Enterprise、iOS/iPadOS、macOS、Windows 用のカスタム プロファイルを作成する方法について説明します。 さまざまなプラットフォームで使用できるすべての設定を確認することもできます。

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** :デバイスのプラットフォームを選択します。 次のようなオプションがあります。  

        - **Android デバイス管理者**
        - **Android エンタープライズ**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 以降**

    - **[プロファイル]** : **[カスタム]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 適切なポリシー名の例:「**Windows 10:AllowVPNOverCellular カスタム OMA-URI を有効にするカスタム プロファイル**」。
    - **説明**:ポリシーの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** では、選択したプラットフォームによって構成できる設定が変わります。 詳細な設定については、お使いのプラットフォームを選択してください。

    - [Android デバイス管理者](custom-settings-android.md)
    - [Android エンタープライズ](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)

8. **[次へ]** を選択します。
9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="example"></a>例

次の例では、**Connectivity/AllowVPNOverCellular** 設定が有効です。 この設定により、移動体通信ネットワーク上の Windows 10 デバイスで VPN 接続が利用できるようになります。

> [!div class="mx-imgBorder"]
> ![Intune とエンドポイント マネージャーの VPN 設定を含むカスタム ポリシーの例](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>次のステップ

プロファイルは作成されましたが、まだ何も実行できない可能性があります。 次に、[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。
