---
title: デバイス登録のない管理対象アプリ用構成ポリシー
titleSuffix: Microsoft Intune
description: デバイス登録のない管理対象アプリ用構成ポリシーについて説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20b5b3de16023ac475cc41a633e5d3ab915a1bd0
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910725"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>デバイス登録なしで管理対象アプリ用アプリ構成ポリシーを追加する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

登録されていないデバイスでも、Intune App SDK をサポートする管理対象アプリにアプリ構成ポリシーを使用できます。 

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド アプリ]** を選択します。
3. **[基本]** ページで、次の詳細を設定します。
    - **名前**:Azure Portal に表示されるプロファイルの名前。
    - **説明**:Azure Portal に表示されるプロファイルの説明。
    - **[デバイス登録の種類]** :マネージド アプリが選択されています。
4. 構成するアプリを選択するために、 **[パブリック アプリの選択]** または **[カスタム アプリの選択]** のいずれかを選択します。 承認して Intune に同期したアプリの一覧からアプリを選択します。
5. **[次へ]** をクリックして、 **[設定]** ページを表示します。
6. **[設定] ページ**には、構成しているアプリに基づいて表示されるオプションが提供されます。

    - **[一般的な構成設定]** - アプリでサポートする一般的な構成設定ごとに、 **[名前]** と **[値]** を入力します。 
 
        Intune App SDK 対応のアプリでは、キー/値のペアの構成がサポートされます。 サポートされるキーと値の構成の詳細については、各アプリのドキュメントを参照してください。 さらに、アプリケーションから生成されるデータが動的に設定されるトークンを使用できます。 一般的な構成設定を削除するには、省略記号 ( **[...]** ) を選択し、 **[削除]** を選択します。 詳細については、「[トークンを使用する場合の構成値](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens)」を参照してください。 

    - **[Outlook の構成設定]** - iOS および Android 用の Outlook では、管理者は、いくつかのアプリ内設定について既定の構成をカスタマイズできます。 詳細については、[iOS および Android 用 Outlook の一般的アプリ構成シナリオ](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#general-app-configuration-scenarios)に関するページを参照してください。
   
    - **[S/MIME]** - Secure/Multipurpose Internet Mail Extensions (S/MIME) は、デジタル署名および暗号化された電子メールの送受信を可能にするための仕様です。
        - **[S/MIME を有効にする]** - 電子メールを作成するときに、S/MIME コントロールを有効にするかどうかを指定してください。 既定値: **[Not configured]** (未構成)。
        - **[ユーザーに設定の変更を許可する]** - ユーザーに設定の変更を許可するかどうかを指定します。 S/MIME を有効にする必要があります。 既定値: **[はい]** 。
        
    Outlook アプリ構成ポリシー設定の詳細については、[iOS と Android 用 Outlook のアプリ構成設定の展開](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)に関する記事をご覧ください。

7. **[次へ]** をクリックして、 **[割り当て]** ページを表示します。
8. **[含めるグループを選択]** をクリックします。
9. **[含めるグループを選択]** ペインでグループを選択し、 **[選択]** をクリックします。
10. **[含めないグループを選択]** をクリックして、関連するウィンドウを表示します。
11. 除外するグループを選んで、 **[選択]** をクリックします。

    >[!NOTE]
    >グループを追加するときに、他のグループが特定の割り当て種類に既に含まれる場合は、あらかじめ選択されており、他の含める割り当て種類には変更できません。 そのため、使われているそのグループは、含まれないグループとして使えません。

12. **[次へ]** をクリックして、 **[確認と作成]** ページを表示します。
13. **[作成]** をクリックして、アプリ構成ポリシーを Intune に追加します。

## <a name="configuration-values-for-using-tokens"></a>トークンを使用する場合の構成値

Intune では特定のトークンを生成して、マネージド アプリケーションに送信することができます。 たとえば、アプリ構成で電子メール設定を使用できる場合、トークンを使用して動的電子メールを追加することができます。 アプリに予期されている名前を **[名前]** フィールドに入力し、`{{mail}}` を **[値]** フィールドに入力します。

Intune は、構成設定で次のトークンの種類をサポートしています。 その他のカスタム キーと値の組み合わせはサポートされていません。

- \{\{userprincipalname\}\} — たとえば、John@contoso.com
- \{\{mail\}\} — たとえば、John@contoso.com
- \{\{partialupn\}\} — たとえば、John
- \{\{accountid\}\} — たとえば、fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{userid\}\} — たとえば、3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\} — たとえば、John Doe
- \{\{PrimarySMTPAddress\}\} — たとえば、testuser@ad.domain.com

> [!Note]  
> \{\{ 文字と \}\} 文字を使用できるのはトークンの種類のみであり、他の目的には使用しないでください。

## <a name="next-steps"></a>次のステップ

通常どおり、アプリの[割り当て](apps-deploy.md)と[監視](apps-monitor.md)に進みます。