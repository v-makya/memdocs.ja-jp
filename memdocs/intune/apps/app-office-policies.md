---
title: Office アプリのポリシー
titleSuffix: Microsoft Intune
description: Office アプリで使用可能なポリシーについて理解します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca558b40ad3d006aa764819a0fbccc16a03fd0e2
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89644032"
---
# <a name="policies-for-office-apps"></a>Office アプリのポリシー

Intune には、Microsoft Office アプリ専用のポリシーが用意されています。 Microsoft 365 サービスに接続する Office モバイル アプリ向けのモバイル アプリ管理ポリシーを作成するための特定のオプションを選択できます。 Microsoft Intune に追加してエンド ユーザー グループに適用できる Office アプリのポリシーが多数あります。

Office アプリ ポリシーのほんの数例を次に示します。
- Microsoft Word:*Outlook から開いた添付ファイルの保護ビューをオフにする*
- Microsoft Visio:*インターネットからの Office ファイルでのマクロの実行をブロックする*
- Microsoft Project:*ネットワーク上の信頼できる場所を許可する*
- Microsoft Publisher:*Publisher の自動セキュリティ レベル*
- Microsoft PowerPoint:*Outlook から開いた添付ファイルの保護ビューをオフにする*

> [!NOTE]
> 特定のアプリ ポリシーを構成するために選択すると、追加のポリシーの詳細が表示されます。 Office ポリシー一覧をフィルター処理して、推奨される**セキュリティ ベースライン** ポリシーをすばやく選択できます。

ハイブリッドの最新認証に対応する iOS/iPadOS および Android 用の Outlook のために Intune アプリ保護ポリシーを作成することで、Exchange オンプレミス メールボックスへのアクセスも保護できます。 この機能を使用する前に、Office クラウド ポリシー サービスを使用するための要件を満たす必要があります。 アプリ保護ポリシーは、オンプレミス Exchange サービスや SharePoint サービスに接続する他のアプリではサポートされていません。 関連情報については、「[Microsoft 365 Apps for enterprise の Office クラウド ポリシー サービスの概要](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)」を参照してください。

## <a name="prerequisites"></a>前提条件

Office アプリのポリシーを使用するための要件を満たす必要があります。 詳しくは、「[Office クラウド ポリシー サービスを使うための要件](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service)」を参照してください。

## <a name="to-add-an-office-app-policy"></a>Office アプリ ポリシーを追加するには

組織で Intune を設定した後、Office アプリ ポリシーを作成できます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[Office アプリのポリシー]**  >  **[作成]** を選択します。
3. 次の値を追加します。
    - **[名前]:** (必須) 新しいポリシーの名前を入力します。
    - **説明:** (省略可能) 説明を入力します。
    - **種類の選択:** このポリシー構成を適用する方法を選択します。
    - **グループの選択:** このポリシー構成のグループを選択します。
    - **ポリシーの構成:** 適用する Office ポリシーを選択します。 提供された一覧を、ポリシー、プラットフォーム、アプリケーション、推奨事項、および状態に基づいて並べ替えることができます。
4. **［作成］** を選択します ポリシーが作成され、 **[ポリシー構成]** ペイン上のテーブルに表示されます。

   > [!TIP]
   > **[ポリシー構成]** ペインには、各ポリシーの **[正常性状態]** が表示されます。

## <a name="additional-information"></a>追加情報

- [エンタープライズ向けの Microsoft 365 アプリの Office クラウド ポリシー サービスの概要](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)
- [ポリシー設定を使用して、エンタープライズ向けの Microsoft 365 アプリのプライバシー コントロールを管理する](https://docs.microsoft.com/deployoffice/privacy/manage-privacy-controls)
- [ユーザー設定を使用して Office for Mac のプライバシー コントロールを管理する](https://docs.microsoft.com/deployoffice/privacy/mac-privacy-preferences)
- [ユーザー設定を使用して iOS デバイス上の Office のプライバシー コントロールを管理する](https://docs.microsoft.com/deployoffice/privacy/ios-privacy-preferences)
- [ポリシー設定を使用して Android デバイス上の Office のプライバシー コントロールを管理する](https://docs.microsoft.com/deployoffice/privacy/android-privacy-controls)

## <a name="next-steps"></a>次のステップ

- [Microsoft Intune でアプリの情報と割り当てを監視する](apps-monitor.md)