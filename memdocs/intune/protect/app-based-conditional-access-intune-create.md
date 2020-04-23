---
title: Intune を使用してアプリベースの条件付きアクセス ポリシーを設定する
titleSuffix: Microsoft Intune
description: Intune でアプリベースの条件付きアクセス ポリシーを作成する方法について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fadd5817ccd4e591fe92c11cb30041296ac85d61
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696474"
---
# <a name="set-up-app-based-conditional-access-policies-with-intune"></a>Intune を使用してアプリベースの条件付きアクセス ポリシーを設定する

承認済みアプリの一覧に含まれるアプリに適用されるアプリベースの条件付きアクセス ポリシーを設定します。 承認済みのアプリの一覧は、Microsoft によってテストされたアプリで構成されます。

アプリベースの条件付きアクセス ポリシーを使用する前に、[Intune アプリ保護ポリシー](../apps/app-protection-policies.md)をアプリに適用する必要があります。

> [!IMPORTANT]
> この記事では、シンプルなアプリベースの条件付きアクセス ポリシーを追加する手順について説明します。 他のクラウド アプリに対しても同じ手順を使用できます。 詳細については、[条件付きアクセスの展開を計画する方法](https://docs.microsoft.com/azure/active-directory/conditional-access/plan-conditional-access)に関する記事をご覧ください

## <a name="create-app-based-conditional-access-policies"></a>アプリベースの条件付きアクセス ポリシーを作成する

条件付きアクセスは、Azure Active Directory (Azure AD) テクノロジです。 *Intune* からアクセスされる条件付きアクセス ノードは、*Azure AD* からアクセスされるものと同じノードです。 同じノードであるため、ポリシーを構成するために、Intune と Azure AD の間を切り替える必要はありません。

Microsoft Endpoint Manager admin center から条件付きアクセス ポリシーを作成するには、その前に Azure AD Premium ライセンスを用意する必要があります。

### <a name="to-create-an-app-based-conditional-access-policy"></a>アプリベースの条件付きアクセス ポリシーを作成するには

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインします。

2. **[エンドポイント セキュリティ]** 、 **[条件付きアクセス]** 、 **[新しいポリシー]** の順に選択します。

3. ポリシーの**名前**を入力し、 *[割り当て]* で **[ユーザーとグループ]** を選択します。 含めるオプションまたは除外するオプションを使用して、ポリシーのグループを追加し、 **[完了]** を選択します。

4. **[クラウド アプリまたは操作]** を選択し、保護するアプリを選びます。 たとえば、 **[アプリを選択]** を選択し、 **[Office 365 (プレビュー)]** を選択します。

   **[完了]** を選択して変更を保存します。

5. **[条件]**  >  **[クライアント アプリ]** の順に選択して、アプリとブラウザーにポリシーを適用します。 たとえば、 **[はい]** を選択し、 **[ブラウザー]** と **[モバイル アプリとデスクトップ クライアント]** を有効にします。

   **[完了]** を選択して変更を保存します。

6. *[アクセスの制御]* で **[許可]** を選択し、デバイスのコンプライアンスに基づいて条件付きアクセスを適用します。 たとえば、 **[アクセス権の付与]**  >  **[承認されたクライアント アプリが必要です]** および **[アプリの保護ポリシーが必要 (プレビュー)]** の順に選択した後、 **[選択したコントロールのいずれかが必要]** を選択します

   **[選択]** を選んで変更を保存します。

7. **[ポリシーを有効にする]** には、 **[オン]** を選択し、 **[作成]** を選択して変更を保存します。





## <a name="next-steps"></a>次のステップ
[最新の認証を使用していないアプリをブロックする](app-modern-authentication-block.md)

## <a name="see-also"></a>関連項目

[アプリ保護ポリシーでアプリ データを保護する](../apps/app-protection-policies.md)
[Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
