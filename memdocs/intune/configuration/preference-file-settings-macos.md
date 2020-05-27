---
title: Microsoft Intune で macOS デバイスに設定ファイルの設定を追加する - Azure | Microsoft Docs
titleSuffix: ''
description: アプリに関するキー情報が含まれる xml ファイルまたは plist ファイルを追加します。 設定ファイル デバイス構成プロファイルを使用してプロパティ リスト ファイル内のキー情報を変更し、それを macOS デバイスに割り当てます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebf65ecc6dbe5059adbd6fec70833bf2fcab9de7
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988674"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Microsoft Intune を使用してプロパティ リスト ファイルを macOS デバイスに追加する

Microsoft Intune を使用すると、macOS デバイス用のプロパティ リスト ファイル (.plist) または macOS デバイス上のアプリを追加できます。

この機能は、以下に適用されます。

- macOS 10.7 以降

プロパティ リスト ファイルには、macOS アプリケーションに関する情報が含まれています。 詳細については、「[情報プロパティ リスト ファイルについて](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)」 (Apple の Web サイト) および「[カスタム ペイロードの設定](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1)」を参照してください。

この記事では、macOS デバイスに追加できるプロパティ リスト ファイルのさまざまな設定の一覧を示して説明します。 モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使用してアプリ バンドル ID (`com.company.application`) を追加し、そのアプリの .plist ファイルを追加します。

これらの設定は、Intune でデバイスの構成プロファイルに追加した後、ご使用の macOS デバイスに割り当てたり展開したりします。

## <a name="what-you-need-to-know"></a>知っておく必要がある情報

- これらの設定は検証されません。 プロファイルをデバイスに割り当てる前に、変更をテストしてください。
- アプリ キーを入力する方法がわからない場合は、アプリ内で設定を変更します。 その後、[Xcode](https://developer.apple.com/xcode/) を使用してアプリの設定ファイルを調べて、設定がどのように構成されているかを確認します。 Apple では、ファイルをインポートする前に、Xcode を使用して管理できない設定を削除することが推奨されています。
- 管理された設定で動作するのは一部のアプリのみであり、すべての設定を管理できるとは限りません。
- ユーザー チャネルの設定ではなく、デバイス チャネルの設定を対象とするプロパティ リスト ファイルを必ずアップロードしてください。 プロパティ リスト ファイルの対象はデバイス全体です。

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[macOS]** を選択します
    - **[プロファイル]** : **[設定ファイル]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 たとえば、適切なポリシー名は **macOS: デバイスで Microsoft Defender ATP を構成する設定ファイルの追加**になります。
    - **説明**:ポリシーの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** で、次の設定を構成します。

    - **[優先ドメイン名]** : バンドル ID を入力します (`com.company.application` など)。 たとえば、「`com.Contoso.applicationName`」、「`com.Microsoft.Edge`」、または「`com.microsoft.wdav`」と入力します。

      通常、プロパティ リスト ファイルは、Web ブラウザー (Microsoft Edge)、[Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)、およびカスタム アプリに使用されます。 優先ドメインを作成すると、バンドル ID も作成されます。

    - **[プロパティ リスト ファイル]** : アプリに関連付けられているプロパティ リスト ファイルを選択します。 `.plist` ファイルまたは `.xml` ファイルであることを確認してください。 たとえば、`YourApp-Manifest.plist` ファイルまたは `YourApp-Manifest.xml` ファイルをアップロードします。

      プロパティ リスト ファイル内のキー情報が表示されます。 キー情報を変更する必要がある場合は、別のエディターでリスト ファイルを開いてから、Intune でファイルを再度アップロードします。

    ファイルの形式が正しく設定されていることを確認してください。 このファイルではキーと値のペアのみを指定し、`<dict>`、`<plist>`、または `<xml>` タグでラップしないでください。 たとえば、プロパティ リスト ファイルは次のファイルのようになります。

    ```xml
    <key>SomeKey</key>
    <string>someString</string>
    <key>AnotherKey</key>
    <false/>
    ...
    ```

8. **[次へ]** を選択します。
9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

Microsoft Edge 用の設定ファイルの詳細については、[macOS での Microsoft Edge ポリシー設定の構成](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac)に関するページを参照してください。
