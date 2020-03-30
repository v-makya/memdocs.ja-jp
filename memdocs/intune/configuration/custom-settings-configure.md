---
title: Microsoft Intune でカスタム デバイス設定を使用する - Azure | Microsoft Docs
description: Microsoft Intune を使用し、Windows Phone、Windows 8.1、Windows 10 以降、Android デバイス管理者、Android Enterprise、macOS、iOS/iPadOS デバイスのカスタム設定を使用するプロファイルを追加または作成します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083999"
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

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 適切なポリシー名の例:「**Windows 10:AllowVPNOverCellular カスタム OMA-URI を有効にするカスタム プロファイル**」。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
    - **[プラットフォーム]** :デバイスのプラットフォームを選択します。 次のようなオプションがあります。

      - **Android デバイス管理者**
      - **Android エンタープライズ**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 以降**
      - **Windows 8.1 以降**

    - **[プロファイルの種類]** : **[カスタム]** を選択します。

4. 設定はプラットフォームごとに異なります。 特定のプラットフォーム向けの設定を確認するには、プラットフォームを選択します。

    - [Android デバイス管理者](custom-settings-android.md)
    - [Android エンタープライズ](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. 完了したら、 **[プロファイルの作成]**  >  **[作成]** の順に選択します。

プロファイルが作成され、プロファイル一覧に表示されます ( **[デバイス構成]**  >  **[プロファイル]** )。

## <a name="next-steps"></a>次のステップ

プロファイルが作成されると、割り当てることができます。 次に、[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。
