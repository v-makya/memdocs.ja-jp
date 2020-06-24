---
title: Microsoft Intune の Windows および Holographic デバイスのキオスク設定 - Azure | Microsoft Docs
description: Microsoft Intune でシングル アプリおよびマルチ アプリ キオスクとして Windows 10 (以降) および Windows Holographic for Business デバイスを構成し、スタート メニューのカスタマイズ、アプリの追加、タスク バーの表示、および Web ブラウザーの構成を行います。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f58e457a5868053a94e1f2c1185bbae0e4b69327
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093069"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Intune を使用して専用キオスクとして実行するための Windows 10 および Windows Holographic for Business デバイスの設定

Windows 10 デバイスで Intune を使用して、専用デバイスとも呼ばれるキオスクとしてデバイスを実行します。 キオスク モードのデバイスでは、1 つのアプリも、複数のアプリも実行できます。 スタート メニューの表示とカスタマイズ、Win32 アプリを含むさまざまなアプリの追加、特定のホーム ページの Web ブラウザーへの追加などを行うことができます。 

この機能は、以下に適用されます。

- Windows 10 以降
- Windows Holographic for Business

他のプラットフォーム用のキオスク プロファイルを作成するには、[Android デバイス管理者](device-restrictions-android.md#kiosk)、[Android エンタープライズ](device-restrictions-android-for-work.md#device-experience)、[iOS または iPadOS](device-restrictions-ios.md#kiosk) を参照してください。

Intune では、デバイスごとに 1 つのキオスク プロファイルをサポートします。 1 台のデバイスに複数のキオスク プロファイルが必要な場合は、[カスタム OMA-URI](custom-settings-windows-10.md) を使用することができます。

Intune では、"構成プロファイル" を使用して、お客様の組織のニーズに合わせてこのような設定を作成およびカスタマイズします。 このような機能をプロファイルに追加したら、その設定を組織内のグループにプッシュまたは展開します。

この記事では、デバイス構成プロファイルを作成する方法について説明します。 すべての設定の一覧とその実行内容については、[Windows 10 のキオスク設定](kiosk-settings-windows.md)と [Windows Holographic for Business のキオスク設定](kiosk-settings-holographic.md)に関するページを参照してください。

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

   - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
   - **[プロファイル]** : **[キオスク]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

   - **名前**:新しいプロファイルのわかりやすい名前を入力します。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** ** > [キオスク モードを選択]** を選択し、ポリシーでサポートされているキオスク モードの種類を選択します。 次のオプションがあります。

    - **[未構成]** (既定):Intune では、この設定は変更または更新されません。 このポリシーでは、キオスク モードが有効になりません。
    - **[シングル アプリ、全画面表示キオスク]** :デバイスは単一ユーザー アカウントとして実行され、1 つのストア アプリに制限されます。 したがって、ユーザーがサインインすると、特定のアプリが起動します。 また、このモードでは、ユーザーによる新しいアプリを開く操作や、実行中のアプリを変更する操作が制限されます。
    - **[マルチ アプリ キオスク]** :デバイスはアプリケーション ユーザー モデル ID (AUMID) を使用して複数のストア アプリ、Win32 アプリ、または受信トレイの Windows アプリを実行します。 デバイスでは追加されているアプリだけを利用できます。

        マルチ アプリ キオスク (または固定目的デバイス) の利点は、ユーザーがアクセスできるのは必要なアプリだけなので、わかりやすいエクスペリエンスがユーザーに提供されることです。 また、必要のないアプリはビューから削除されます。

    すべての設定の一覧とその実行内容については、以下を参照してください。

      - [Windows 10 のキオスク設定](kiosk-settings-windows.md)
      - [Windows Holographic for Business のキオスク設定](kiosk-settings-holographic.md)

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはユーザー グループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

ポリシーは、次に各デバイスがチェックインするときに適用されます。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当てた](device-profile-assign.md)後は、[その状態を監視](device-profile-monitor.md)します。

次のプラットフォームを実行するデバイス用のキオスク プロファイルを作成できます。

- [Android デバイス管理者](device-restrictions-android.md#kiosk)
- [Android エンタープライズ](device-restrictions-android-for-work.md#device-experience)
- [Windows 10 以降](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
