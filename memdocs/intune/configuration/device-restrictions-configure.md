---
title: Microsoft Intune でポリシーを使用してデバイスの機能を制限する - Azure | Microsoft Docs
description: デバイス プロファイルを追加して、Microsoft Intune で Android デバイス管理者、Android エンタープライズ、macOS、iOS、iPadOS、Windows Phone、および Windows 10 の各デバイスの機能を制限します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 716925f077b7433eab06a6ea2f557c7653d0b03d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551414"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Microsoft Intune でデバイスの制限設定を構成する

Intune には、管理者が Android、iOS/iPadOS、macOS、および Windows の各デバイスを制御するのに役立つデバイス制限ポリシーが含まれています。 これらの制限を使用して、組織のリソースを保護するための幅広い設定と機能を制御できます。 たとえば、管理者には次の機能があります。

- デバイス カメラを許可またはブロックします。
- Google Play、アプリ ストア、ドキュメントの表示、ゲームへのアクセスを制御します。
- 組み込みアプリをブロックするか、許可または禁止するアプリの一覧を作成します。
- クラウドとストレージ アカウントへのファイルのバックアップを許可または禁止します。
- パスワードの最小文字数を設定し、単純なパスワードをブロックします。

これらの機能は Intune で使用できます。また、管理者が構成できます。 Intune では、"構成プロファイル" を使用して、お客様の組織のニーズに合わせてこのような設定を作成およびカスタマイズします。 これらの機能をプロファイルに追加した後、そのプロファイルをお客様の組織のデバイスにプッシュまたは展開できます。

この記事では、デバイス制限プロファイルの作成方法について説明します。 さまざまなプラットフォームで使用できるすべての設定を確認することもできます。

> [!NOTE]
> Intune ユーザー インターフェイス (UI) は全画面表示エクスペリエンスに向けて更新中であり、これには数週間かかる場合があります。 ご自分のテナントがこの更新プログラムを受信するまでは、この記事で説明する設定を作成または編集する際のワークフローが若干異なります。

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
        - **Windows 8.1 以降**
        - **Windows Phone 8.1**

    - **[プロファイル]** : **[デバイスの制限]** を選択します。

        Surface Hub などの Windows 10 Team デバイス用のデバイスの制限プロファイルを作成するには、 **[デバイスの制限 (Windows 10 Team)]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 たとえば、適切なポリシー名は **iOS/iPadOS:デバイスのカメラをブロックする**です。
    - **説明**:ポリシーの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** では、選択したプラットフォームによって構成できる設定が変わります。 詳細な設定については、お使いのプラットフォームを選択してください。

    - [Android デバイス管理者](device-restrictions-android.md)
    - [Android エンタープライズ](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 以降](device-restrictions-windows-10.md)
    - [Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. **[次へ]** を選択します。
9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="next-steps"></a>次のステップ

プロファイルが作成されると、割り当てることができます。 次に、[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
