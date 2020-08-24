---
title: Autopilot でプロビジョニングされたデバイス用に Windows 10 ポータル サイト アプリを追加して割り当てる
titleSuffix: Microsoft Intune
description: Autopilot でプロビジョニングされたデバイス用に Windows 10 ポータル サイト アプリを Intune に追加して割り当てる
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559523"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Autopilot でプロビジョニングされたデバイス用に Windows 10 ポータル サイト アプリを追加して割り当てる

デバイスの管理およびアプリのインストールのために、ユーザーはポータル サイト アプリを使用できます。 Windows 10 ポータル サイト アプリを Intune から直接割り当てることができます。 

## <a name="prerequisites"></a>[前提条件]

Windows 10 Autopilot でプロビジョニングされたデバイスの場合は、ビジネス向け Microsoft Store アカウントを Intune に関連付けることをお勧めします。 詳細については、「[ビジネス向け Microsoft Store のボリューム購入アプリを Microsoft Intune で管理する方法](windows-store-for-business.md)」を参照してください。

次の手順を使用して**ポータル サイト (オフライン)** アプリをインストールすることを選択できます。 ポータル サイト アプリは、Autopilot グループに割り当てられるとデバイスのコンテキストでインストールされ、ユーザーがログインする前にデバイスにインストールされます。

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>オフライン アプリを表示するようにストアの設定を構成する

1. 自分の管理アカウントを使って[ビジネス向け Microsoft Store](https://www.microsoft.com/business-store) にサインインします。
2. ウィンドウの上部付近にある **[管理]** タブを選択します。
3. 左側のウィンドウで、 **[設定]** を選択します。
4. **[Shopping experience]\(ショッピング体験\)** の **[Show offline apps]\(オフライン アプリの表示\)** を **[オン]** に設定します。  
   オフラインのライセンスされたアプリが表示されます。

## <a name="get-the-offline-company-portal-app-from-the-store"></a>ストアからオフライン ポータル サイト アプリを取得する

1. **ポータル サイト** アプリを検索して選択します。
2. **[ライセンスの種類]** を **[オフライン]** に設定します。
3. **[アプリの取得]** を選択し、オフラインのポータル サイト アプリを取得して、インベントリに追加します。
   アプリが Intune にリストされるようにするには、同期スケジュールが完了するまで待つか、または Microsoft Endpoint Manager 管理センターから手動同期を実行する必要があります。

## <a name="manually-sync-company-portal-app-with-intune"></a>Intune でポータル サイト アプリを手動で同期する

1. 管理者アカウントを使用して  [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431)  にサインインします。
2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[Microsoft Store for Business]** を選択します。
3. **[有効化]** をクリックします。
4. ビジネス向け Microsoft ストアにまだサインアップしていない場合は、前に詳しく説明したように、サインアップ用のリンクをクリックしてサインアップし、アカウントを関連付けます。
5. **[言語]** ドロップダウン リストで、Azure Portal で表示するビジネス向け Microsoft ストアのアプリに使用する言語を選択します。 アプリは、どの言語を使用して表示するかに関係なく、使用可能なエンド ユーザーの言語でインストールされます。
6. **[同期]** をクリックして、Microsoft ストアから購入したアプリを Intune に取り込みます。

## <a name="assign-the-company-portal-app"></a>ポータル サイト アプリを割り当てる

1. 管理者アカウントを使用して  [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431)  にサインインします。
2. **[アプリ]**  >  **[Windows]** の順に選択します。
3. Windows アプリのリストから、 **[ポータル サイト (オフライン)]** を選択します。
4. 選択した Autopilot デバイス グループに、必要なアプリとしてポータル サイト アプリを[割り当て](apps-deploy.md)ます。

## <a name="next-steps"></a>次のステップ

- アプリの割り当てに関する詳細については、[グループへのアプリの割り当て](apps-deploy.md)に関するページを参照してください。

