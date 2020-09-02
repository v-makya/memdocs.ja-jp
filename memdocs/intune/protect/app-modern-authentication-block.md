---
title: 最新の認証を使用していないアプリを Intune でブロックする
titleSuffix: Microsoft Intune
description: Microsoft Intune を使用するアプリケーションと先進認証 (ADAL) について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/22/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4703288faac219b40fae08c6551425d6f0d5e4f3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909416"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>先進認証 (ADAL) を使用していないアプリをブロックする

> [!NOTE]
> Azure Active Directory (Azure AD) 認証ライブラリ (ADAL) と Azure AD Graph API は非推奨になります。 詳細については、[Microsoft Authentication Library (MSAL) と Microsoft Graph API を使用するようにアプリケーションを更新する](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363)方法に関するページを参照してください。

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

アプリ保護ポリシーを使用したアプリベースの条件付きアクセスは、[先進認証](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)を使用するアプリケーションに依存しています。これは OAuth2 の実装です。 最新のモバイルおよびデスクトップ用 Office アプリケーションでは、先進認証が使用されています。 しかし、基本認証やフォームベースの認証など、他の認証方式が使用されているサードパーティ製アプリや古い Office アプリがあります。

## <a name="block-access-to-apps"></a>アプリへのアクセスをブロックする

先進認証を使用していないアプリへのアクセスをブロックするには、Intune アプリ保護ポリシーを使用して、条件付きアクセスを実装します。 詳細については、「[Intune でのアプリベースの条件付きアクセス](app-based-conditional-access-intune.md)」を参照してください。

## <a name="additional-information"></a>追加情報

Azure AD 条件付きアクセスの詳細については、次のトピックを参照してください。
- [Azure Active Directory の条件付きアクセスとは](/azure/active-directory/conditional-access/overview)
- [アプリベースの条件付きアクセスのしくみ](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [SharePoint Online と Exchange Online に Azure Active Directory の条件付きアクセスを設定する](/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>次のステップ

- [Intune でのアプリ ベースの条件付きアクセス](app-based-conditional-access-intune.md)