---
title: Microsoft Intune で macOS デバイス用の 802.1x 有線ネットワーク設定を構成する - Azure | Microsoft Docs
titleSuffix: ''
description: macOS デスクトップ コンピューター デバイス用の有線ネットワーク デバイス構成プロファイルを作成または追加します。 さまざまな設定を確認し、証明書を追加し、EAP の種類を選択し、Microsoft Intune で認証方法を選択します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095807"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>Microsoft Intune で macOS デバイスの有線ネットワーク設定を追加して使用する

有線ネットワークは、デスクトップ コンピューターにネットワーク アクセスを提供するために多くの組織で使用されています。 Microsoft Intune には、組織内の macOS ユーザーおよびデバイスに展開できる組み込み設定が含まれています。 この設定のグループは "プロファイル" と呼ばれます。 プロファイルには、ネットワーク インターフェイス、受け入れられる EAP の種類、サーバーの信頼設定などの一般的な設定を含めることができます。

プロファイルの準備が整ったら、さまざまなユーザーやグループに割り当てることができます。 割り当てると、ユーザーは自分で構成しなくても組織の有線ネットワークにアクセスできるようになります。

モバイル デバイス管理 (MDM) ソリューションの一部として、この機能を使用して 802.1x プロファイルを作成し、有線ネットワークを管理します。 次に、これらの有線ネットワークを macOS デバイスに展開します。

この機能は、以下に適用されます。

- macOS

たとえば、**Contoso 有線ネットワーク**という名前の有線ネットワークがあるとします。 このネットワークに接続するようにすべての macOS デスクトップを設定する必要があります。 その手順は次のとおりです。

1. **Contoso 有線ネットワーク**に接続する設定を含む有線ネットワーク プロファイルを作成します。
2. すべてのユーザーの macOS デスクトップ コンピューターを含むグループにプロファイルを割り当てます。 グループの種類の使用に関する推奨事項については、「[ユーザー グループとデバイス グループ](device-profile-assign.md#user-groups-vs-device-groups)」を参照してください。
3. ユーザーは、デスクトップ上で、ネットワークの一覧から **Contoso 有線ネットワーク**を見つけます。 ユーザーは、選択されている認証方法を使用して、ネットワークに接続できます。

この記事では、有線ネットワーク プロファイルを作成する手順を示します。 また、さまざまな設定を説明するリンクも示します。

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[macOS]** を選択します。
    - **[プロファイル]** : **[ワイヤード (有線) ネットワーク]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、適切なプロファイル名として、**macOS デバイス上の会社全体用の有線ネットワーク プロファイル**があります。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** で、ネットワークのネットワーク インターフェイスを選択し、拡張認証プロトコル (EAP) の種類を選択します。 すべての設定の一覧とその実行内容については、以下を参照してください。

    - [macOS](wired-network-settings-macos.md)

8. **[次へ]** を選択します。
9. **[割り当て]** で、プロファイルを受け取るユーザー グループまたはデバイス グループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

> [!TIP]
> 有線ネットワーク プロファイルに証明書ベースの認証を使用する場合は、有線ネットワーク プロファイル、証明書プロファイル、および信頼されたルート プロファイルを同じグループに展開します。 この展開により、各デバイスが証明機関の正当性を確実に認識できるようになります。 詳細については、[Microsoft Intune を使用した証明書の構成](../protect/certificates-configure.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

プロファイルは作成されましたが、何も実行できない可能性があります。 必ず[このプロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)してください。
