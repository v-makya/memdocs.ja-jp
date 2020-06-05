---
title: Microsoft Intune での共有デバイスまたはマルチユーザー デバイスの設定 - Azure | Microsoft Docs
description: Microsoft Intune で共有されるか複数のユーザーによって使用される Windows 10 デバイスと Windows Holographic for Business デバイスを追加および使用します。 すべての設定と、Microsoft HoloLens などのデバイスでのその動作の一覧を参照してください。 デバイス構成プロファイルで、ゲスト アカウントの制御、アカウントの管理、非アクティブなアカウントの削除、ローカル ストレージへの保存の許可または禁止、電源とスリープのオプションの設定、更新プログラムをインストールするタイミングの選択、および教育環境でのデバイスの使用を行います。
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
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f85c30c9472849d26802c8cdccd7a95006a3e4a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984015"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>Intune を使用して共有 PC またはマルチユーザー デバイスでのアクセス、アカウント、および電源機能を制御する

複数のユーザーを持つデバイスは共有デバイスと呼ばれ、モバイル デバイス管理 (MDM) ソリューションの一般的な部分です。 Microsoft Intune を使用して、次のプラットフォームを実行している共有デバイスをカスタマイズできます。

- Windows 10 Professional 以降
- Windows 10 Enterprise 以降
- Windows Holographic for Business (HoloLens など)

たとえば、学校には、通常多くの学生によって使用されるデバイスがあります。 この設定では、学校の Intune 管理者は共有 PC 機能をオンにして、一度に 1 人のユーザーを許可することができます。 学生は、デバイス上で異なるサインイン アカウント間を切り替えることはできません。 また、管理者は、学生がサインアウトしたときにすべてのユーザー固有設定を削除するよう選択できます。

エンドユーザーは、これらの共有デバイスにゲスト アカウントでサインインできます。 ユーザーがサインインした後、資格情報がキャッシュされます。 エンドユーザーは、デバイスを使用する際、管理者が許可する機能にのみアクセスできます。 管理者は、たとえば、デバイスがスリープ モードになるタイミング、ユーザーがファイルをローカルに表示および保存できるかどうか、電源管理設定の有効化または無効化などを選択します。 また、ユーザーがサインオフしたときにゲスト アカウントを削除するかどうかや、しきい値に達したときに非アクティブなアカウントを削除するかどうかも制御します。

この記事では、構成プロファイルを作成する方法について説明し、使用可能な設定へのリンクとその説明を示します。

Intune でプロファイルが作成されると、そのプロファイルを組織内のデバイス グループにデプロイするか割り当てます。 このプロファイルは、さまざまな種類のデバイスやさまざまなバージョンのオペレーティング システム (OS) から成るデバイス グループに割り当てることもできます。

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

   - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
   - **[プロファイル]** : **[共有のマルチユーザーのデバイス]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

   - **名前**:新しいプロファイルのわかりやすい名前を入力します。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** では、選択したプラットフォームによって構成できる設定が変わります。 詳細な設定については、お使いのプラットフォームを選択してください。

    - [Windows 10 以降](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るデバイス グループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

    > [!NOTE]
    > 必ず組織内のデバイス グループにプロファイルを割り当ててください。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

次に各デバイスがチェックインするときに、ポリシーが適用されます。

## <a name="next-steps"></a>次のステップ

- [Windows 10 以降](shared-user-device-settings-windows.md)および [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) のすべての設定を参照します。
- [プロファイルを割り当てた](device-profile-assign.md)後は、[その状態を監視します](device-profile-monitor.md)。
