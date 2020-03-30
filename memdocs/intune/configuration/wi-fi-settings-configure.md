---
title: Microsoft Intune でデバイス用の Wi-Fi プロファイルを作成する - Azure | Microsoft Docs
description: Microsoft Intune で Wi-Fi デバイスの構成プロファイルを作成する手順を説明します。 Android デバイス管理者、Android エンタープライズ、Android キオスク、iOS、iPadOS、macOS、Windows 10 以降、Windows Holographic for Business 用のプロファイルを作成します。 これらのプロファイルは、証明書を使用するための Wi-Fi 接続の作成、EAP の種類の選択、認証方法の選択、プロキシの有効化、その他に使用します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 235f5517c9968ba63b04fefa03d9486e5bd6e52d
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086404"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Microsoft Intune でデバイスに Wi-Fi 設定を追加して使用する

Wi-Fi は、多数のモバイル デバイスがネットワークにアクセスするために使用しているワイヤレス ネットワークです。 Microsoft Intune には、組織内のユーザーとデバイスに展開できる組み込みの Wi-Fi 設定が含まれています。 この設定のグループは "プロファイル" と呼ばれ、さまざまなユーザーとグループに割り当てることができます。 割り当てると、ユーザーは自分で構成しなくても組織の Wi-Fi ネットワークにアクセスできるようになります。

たとえば、Contoso Wi-Fi という新しい Wi-Fi ネットワークをインストールします。 そして、すべての iOS/iPadOS デバイスをこのネットワークに接続するように設定するものとします。 その手順は次のとおりです。

1. Contoso Wi-Fi ワイヤレス ネットワークに接続するための設定が含まれる Wi-Fi プロファイルを作成します。
2. iOS/iPadOS デバイスのすべてのユーザーを含むグループにそのプロファイルを割り当てます。
3. ユーザーは、自分のデバイスでワイヤレス ネットワークの一覧にある新しい Contoso Wi-Fi ネットワークを見つます。 ユーザーは、選択されている認証方法を使用して、ネットワークに接続できます。

この記事では、Wi-Fi プロファイルの作成手順を説明します。 また、各プラットフォームのさまざまな設定について説明されたリンクも含まれています。

## <a name="supported-device-platforms"></a>サポートされているデバイス プラットフォーム

Wi-Fi プロファイルでは次のデバイス プラットフォームをサポートしています。

- Android 4 以降
- Android エンタープライズ、キオスク
- iOS 8.0 以降
- iPadOS 13.0 以降
- macOS X 10.11 以降
- Windows 10 以降、Windows 10 Mobile、Windows Holographic for Business

> [!NOTE]
> Windows 8.1 を実行しているデバイスの場合は、以前に別のデバイスからエクスポートした Wi-Fi 構成をインポートできます。

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

    - **[プロファイル]** : **[Wi-Fi]** を選択します。

      > [!TIP]
      >
      > - 専用デバイス (キオスク) として実行されている **Android エンタープライズ** デバイスの場合、 **[デバイスの所有者のみ]**  >  **[Wi-Fi]** の順に選択します。
      > - **Windows 8.1 以降**の場合は、 **[Wi-Fi インポート]** を選択できます。 このオプションを使用すると、以前に別のデバイスからエクスポートした Wi-Fi 設定を XML ファイルとしてインポートすることができます。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「**会社全体の WiFi プロファイル**」は適切なプロファイル名です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** では、選択したプラットフォームによって構成できる設定が変わります。 詳細な設定については、お使いのプラットフォームを選択してください。

    - [Android デバイス管理者](wi-fi-settings-android.md)
    - [Android エンタープライズ](wi-fi-settings-android-enterprise.md) (専用デバイスを含む)
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 以降](wi-fi-settings-windows.md)
    - [Windows 8.1 以降](wi-fi-settings-import-windows-8-1.md) (Windows Holographic for Business を含む)

8. **[次へ]** を選択します。
9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="next-steps"></a>次のステップ

プロファイルは作成されますが、何も実行されません。 次に、[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Intune での Wi-Fi プロファイルのトラブルシューティング](troubleshoot-wi-fi-profiles.md)。
