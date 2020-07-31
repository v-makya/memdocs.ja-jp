---
title: Microsoft Intune で Mobile Threat Defense (MTD) デバイス コンプライアンス ポリシーを作成する
titleSuffix: Microsoft Intune
description: モバイル デバイスが会社のリソースにアクセスできるかどうかを決定するために、MTD パートナー脅威レベルを使用する Intune デバイスのコンプライアンス ポリシーを作成します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88f8a2ff04f536370f613341170e7fae0a808ff6
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365527"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Intune で Mobile Threat Defense (MTD) デバイス コンプライアンス ポリシーを作成する

Intune で MTD を使用すると、モバイル デバイス上で脅威を検出し、リスクを評価できます。 リスクを評価する Intune デバイス コンプライアンス ポリシー ルールを作成すれば、デバイスがポリシーに準拠しているかどうかを判断できます。 さらに、[条件付きアクセス ポリシー](create-conditional-access-intune.md)を使用することで、デバイスのコンプライアンスに基づいて、サービスへのアクセスを禁止できます。

> [!NOTE]
> この情報は、すべての Mobile Threat Defense パートナーに適用されます。

## <a name="before-you-begin"></a>始める前に

MTD の設定の一部として、MTD パートナー コンソールで、さまざまな脅威を高、中、低として分類するポリシーを作成しておきます。 次に、Intune デバイス コンプライアンス ポリシーで Mobile Threat Defense レベルを設定します。

MTD でのデバイス コンプライアンス ポリシーの前提条件:

- MTD と Intune の統合をセットアップする

## <a name="to-create-an-mtd-device-compliance-policy"></a>MTD デバイス コンプライアンス ポリシーを作成するには

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[デバイスのポリシー準拠]**  >  **[ポリシーの作成]** の順に選択します。

3. **[プラットフォーム]** を選択し、 **[作成]** を選択します。

4. **[基本]** で、デバイス コンプライアンス ポリシーの **[名前]** と **[説明]** (省略可能) を指定します。 **[次へ]** を選択して続行します。


5. **[コンプライアンス設定]** で、 **[デバイスの正常性]** を展開して構成します。 **[デバイスは、デバイス脅威レベル以下であることが必要]** のドロップダウン リストからモバイル脅威レベルを選択します。

   - **[セキュリティ保護]** :このレベルはセキュリティ上最も安全です。 デバイスにいかなる脅威も存在できず、デバイスからは引き続き会社のリソースにアクセスできます。 いずれかの脅威が見つかった場合、デバイスは非準拠と評価されます。

   - **低**:存在する脅威が低レベルの場合のみ、デバイスは準拠しています。 低レベルより高い脅威が存在する場合、デバイスは非準拠状態になります。

   - **中**: デバイスに存在する脅威が低レベルまたは中レベルの場合、デバイスは準拠しています。 高レベルの脅威が検出された場合は、デバイスは非準拠と判定されます。

   - **高**: この脅威レベルは最も安全性が低くなります。すべての脅威レベルが許可され、Mobile Threat Defense がレポート目的にのみ使用されるためです。 デバイスには、この設定でアクティブ化された MTD アプリが含まれている必要があります。

6. **[次へ]** を選択して、 **[割り当て]** に進みます。 このプロファイルを受け取るグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

   **[次へ]** を選択します。

7. **[確認および作成]** ページで、完了したら、 **[作成]** を選択します。 作成したプロファイルのポリシーの種類を選択すると、新しいプロファイルが一覧に表示されます。

> [!IMPORTANT]
> Office 365 またはその他のサービスに対する条件付きアクセス ポリシーを作成すると、デバイス コンプライアンス評価が適用され、非準拠デバイスはデバイスで脅威が解決されるまで会社のリソースへのアクセスは禁止されます。

## <a name="to-assign-an-mtd-device-compliance-policy"></a>MTD デバイス コンプライアンス ポリシーを割り当てるには

デバイス コンプライアンス ポリシーをユーザーに割り当てる場合、または割り当てを変更する場合は、次のようにします。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[デバイスのポリシー準拠]** の順に選択します。

3. ユーザーに割り当てるポリシーを選択し、 **[プロパティ]** を選択します。

4. [割り当て] の **[編集]** を選択した後、使用可能なオプションを使用して、このポリシーを受け取るグループを *[含める]* または *[除外]* します。  

5. **[レビューと保存]** を選択して、割り当てを完了します。 割り当てを保存すると、ポリシーが選択したユーザーに展開され、デバイスのコンプライアンスが評価されます。

## <a name="next-steps"></a>次のステップ

[Intune で MTD を有効にする](mtd-connector-enable.md)
