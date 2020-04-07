---
title: Microsoft Intune - Azure でエンドポイント保護設定を構成する | Microsoft Docs
description: Microsoft Intune で macOS または Windows 10 デバイス プロファイルを作成するとき、エンドポイント保護設定を作成します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 4071614c7cb93194eef00f49aa2e1759ba1028f6
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359256"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Intune でエンドポイント保護設定を追加する

Intune でデバイスの構成プロファイルを使用し、次などのデバイスで、共通のエンドポイント保護セキュリティ機能を管理できます。

- ファイアウォール
- BitLocker
- アプリの許可とブロック
- Microsoft Defender と暗号化

たとえば、macOS ユーザーに Mac App Store からのみアプリのインストールを許可するエンドポイント保護プロファイルを作成できます。 あるいは、Windows 10 デバイスでアプリを実行しているとき、Windows SmartScreen を有効にします。

プロファイルを作成する前に、サポート対象のそれぞれのプラットフォームで Intune が管理できる、エンドポイント保護設定の詳細が記述されている次の記事を確認してください。

- [macOS の設定](endpoint-protection-macos.md)
- [Windows 10 の設定](endpoint-protection-windows-10.md)

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>エンドポイント保護設定を含むデバイス プロファイルを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. 次のプロパティを入力します。

    - **[プラットフォーム]** :デバイスのプラットフォームを選択します。 次のようなオプションがあります。

        - **macOS**
        - **Windows 10 以降**

    - **[プロファイル]** : **[Endpoint Protection]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 たとえば、適切なポリシー名は **macOS: すべての macOS デバイス用のファイアウォールを構成する Endpoint Protection プロファイル**になります。
    - **説明**:ポリシーの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** では、選択したプラットフォームによって構成できる設定が変わります。 詳細な設定については、お使いのプラットフォームを選択してください。

   - [macOS の設定](endpoint-protection-macos.md)
   - [Windows 10 の設定](endpoint-protection-windows-10.md)

8. **[次へ]** を選択します。
9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Windows 10 デバイスのカスタム ファイアウォール規則を追加する

Windows 10 のエンドポイント保護規則を含むプロファイルの一部として Microsoft Defender ファイアウォールを構成する場合は、ファイアウォールのカスタム規則を構成できます。 カスタム規則を使用すると、Windows 10 でサポートされているファイアウォール規則の定義済みセットを拡張できます。

カスタム ファイアウォール規則を含むプロファイルを計画する場合は、次の情報を考慮してください。これは、プロファイルでファイアウォール規則をグループ化する際に選択する方法に影響する可能性があります。

- 各プロファイルでは、最大 150 個のファイアウォール規則がサポートされます。 150 個を超える規則を使用する場合は、それぞれ 150 個の規則に限定された、追加のプロファイルを作成します。

- プロファイルごとに、単一の規則を適用できなかった場合、そのプロファイルのすべての規則が失敗し、デバイスにはどの規則も適用されません。

- 規則を適用できなかったときは、プロファイル内のすべての規則が失敗として報告されます。 Intune では、失敗した個々の規則を識別することはできません。  

Intune で管理できるファイアウォール規則については、Windows の[ファイアウォール構成サービス プロバイダー](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP) に関するページで詳しく説明されています。 Intune でサポートされる Windows 10 デバイスのカスタム ファイアウォール設定のリストを確認する場合は、[カスタム ファイアウォール規則](endpoint-protection-windows-10.md#firewall-rules)に関するセクションを参照してください。

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Endpoint Protection プロファイルにカスタム ファイアウォール規則を追加するには

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. *[プラットフォーム]* には **[Windows 10 以降]** を選択し、 *[プロファイル]* には **[Endpoint Protection]** を選択します。

    **[作成]** を選択します。

4. プロファイルの **[名前]** を入力して、 **[次へ]** を選択します。
5. **[構成設定]** で、 **[Microsoft Defender ファイアウォール]** を選択します。 *[ファイアウォール規則]* では、 **[追加]** を選択して **[ルールの作成]** ページを開きます。

6. ファイアウォール規則の設定を指定し、 **[OK]** を選択して保存します。 ドキュメントで利用可能なカスタム ファイアウォール規則のオプションを確認する場合は、[カスタム ファイアウォール規則](endpoint-protection-windows-10.md#firewall-rules)に関するセクションを参照してください。

    1. 規則は、 *[Microsoft Defender ファイアウォール]* ページの規則の一覧に表示されます。
    2. 規則を変更するには、リストから規則を選択して **[規則の編集]** ページを開きます。
    3. プロファイルから規則を削除するには、その規則の省略記号 **(...)** を選択し、 **[削除]** を選びます。
    4. 規則の表示順序を変更するには、規則リストの上部にある*上矢印、下矢印* アイコンを選択します。

7. **[確認および作成]** になるまで **[次へ]** を選択します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="next-steps"></a>次のステップ

プロファイルは作成されましたが、まだ何も実行できない可能性があります。 次に、[プロファイルを割り当て](../configuration/device-profile-assign.md)、[その状態を監視](../configuration/device-profile-monitor.md)します。
