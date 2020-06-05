---
title: Microsoft Intune での Windows 10 用のドメイン参加プロファイルの設定 - Azure | Microsoft Docs
description: ハイブリッド Azure AD 参加済みデバイス用のドメイン参加デバイス構成プロファイルを作成します。 このプロファイルを使用して、Windows Autopilot と Microsoft Intune を使用してプロビジョニングされたデバイスにオンプレミスの Active Directory ドメイン情報を展開します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 211722a02183d3b86525468f907d4093331d9de6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988433"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Microsoft Intune でのハイブリッド Azure AD 参加済みデバイス用のドメイン参加設定の構成

多くの環境では、オンプレミスの Active Directory (AD) が使用されます。 AD ドメイン参加済みデバイスが Azure AD にも参加している場合、それらはハイブリッド Azure AD 参加済みデバイスと呼ばれます。 Windows Autopilot を使用して、Intune に[ハイブリッド Azure AD 参加済みデバイスを登録する](../enrollment/windows-autopilot-hybrid.md)ことができます。 登録するには、**ドメイン参加**構成プロファイルも必要です。

**ドメイン参加**構成プロファイルには、オンプレミスの Active Directory ドメインの情報が含まれます。 デバイスが (通常はオフラインで) プロビジョニングされている場合、デバイスがどのオンプレミスのドメインに参加するかを認識できるように、このプロファイルによって AD ドメインの詳細が展開されます。 ドメイン参加プロファイルを作成しなかった場合、これらのデバイスの展開が失敗する可能性があります。

この機能は、以下に適用されます。

- Windows 10 以降
- ハイブリッド Azure AD 参加済みデバイス
- Autopilot と Intune を使用したハイブリッド展開

この記事では、ハイブリッド Autopilot 展開のためのドメイン参加プロファイルを作成する方法について説明します。 使用可能な設定を確認することもできます。

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイル]** : **[ドメイン参加 (プレビュー)]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 適切なポリシー名の例:「**Windows 10:Windows Autopilot を使用してハイブリッド AD 参加済みデバイスを登録するためのオンプレミスのドメイン情報を含んだドメイン参加プロファイル**」。
    - **説明**:ポリシーの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** で、次のプロパティを入力します。

    - **[コンピューター名のプレフィックス]** :デバイス名のプレフィックスを入力します。 コンピューター名は 15 文字です。 プレフィックスに続く残りの 15 文字はランダムに生成されます。
    - **[ドメイン名]** :デバイスが参加する完全修飾ドメイン名 (FQDN) を入力します。 たとえば、「`americas.corp.contoso.com.`」と入力します
    - **[組織単位]** (省略可能):コンピューター アカウントが作成される組織単位 (OU) への完全なパス ([識別名](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) を入力します。 たとえば、「`"CN=Users,DC=Contoso,DC=com"`」と入力します。 値を入力しなかった場合は、既知のコンピューター オブジェクト コンテナーが使用されます。

      この設定に関する詳細とアドバイスについては、[ハイブリッド Azure AD 参加済みデバイスの展開](../enrollment/windows-autopilot-hybrid.md)に関する記事をご覧ください。

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはユーザー グループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

これで、[Intune と Windows Autopilot を使用してハイブリッド Azure AD 参加済みデバイスを展開する](../enrollment/windows-autopilot-hybrid.md)準備が整いました。

## <a name="next-steps"></a>次のステップ

プロファイルを[割り当て](device-profile-assign.md)た後、[その状態を監視します](device-profile-monitor.md)。

[Intune と Windows Autopilot を使用してハイブリッド Azure AD 参加済みデバイスを展開する](../enrollment/windows-autopilot-hybrid.md)。
