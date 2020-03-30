---
title: クイック スタート - iOS/iPadOS デバイス用の電子メール デバイス プロファイルを作成する
titleSuffix: Microsoft Intune
description: iOS/iPadOS デバイスが会社の電子メールに安全に接続できるように、Microsoft Intune を使用して電子メール デバイス プロファイルを作成する方法について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bc170c5260dc099d0a2b4109ed119572e0dbaff
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086846"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>クイック スタート:iOS/iPadOS 用の電子メール デバイス プロファイルを作成する

このクイック スタートでは、iOS/iPadOS デバイス用の電子メール デバイス プロファイルを作成する方法を確認します。 このプロファイルでは、iOS/iPadOS デバイス上の組み込みの電子メール アプリが会社の電子メールに接続するために必要な設定を指定します。 電子メール デバイス プロファイルは、デバイス間で設定を標準化するのに役立ちます。これにより、エンドユーザーは自分自身では何も設定する必要なく、個人のデバイスで会社の電子メールにアクセスできます。 電子メールの保護をさらに強化するには、電子メール プロファイルを使用してデバイスが準拠しているかどうかを判断し、準拠しているデバイスのみが電子メールにアクセスできるように、条件付きアクセスを設定します。 電子メール プロファイルの詳細については、「[Microsoft Intune で電子メールの設定を構成する方法](email-settings-configure.md)」を参照してください。

Intune サブスクリプションがない場合は、[無料試用版アカウントにサインアップ](../fundamentals/free-trial-sign-up.md)します。

## <a name="sign-in-to-intune"></a>Intune にサインインする

全体管理者または Intune サービス管理者として、[Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。 Intune の試用版サブスクリプションを作成した場合、サブスクリプションを作成したアカウントがグローバル管理者になります。

## <a name="create-an-iosipados-email-profile"></a>iOS/iPadOS 電子メール プロファイルを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]** 、 **[構成プロファイル]** 、 **[プロファイルの作成]** の順に移動します。
   ![Intune で iOS/iPadOS 用の電子メール プロファイルを作成する](./media/quickstart-email-profile/ios-create-profile.png)

3. 次のプロパティを入力します。
   - **[プラットフォーム]** : **[iOS/iPadOS]** を選択します
   - **[プロファイル]** : **[電子メール]** を選択します
  
4. **[作成]** を選択します。

5. **[Basics]\(基本\)** で次のプロパティを入力します。
   - **名前**:新しいプロファイルのわかりやすい名前を入力します。 この例では、「**iOS で職場の電子メールが必要**」と入力します。
   - **説明**:「**職場の電子メールを使用する iOS/iPadOS デバイスが必要**」と入力とします


        ![Intune で、iOS/iPadOS デバイスで使用するための電子メール プロファイルを作成する](./media/quickstart-email-profile/ios-email-profile-name.png)

6. **[次へ]** を選択します。

7. **[構成設定]** で、次の設定を入力します (その他の設定は既定値のままにします)。
   - **[電子メール サーバー]** :このクイック スタートでは、「**outlook.office365.com**」と入力します。 この設定では、iOS/iPadOS のメール アプリが電子メールへの接続に使用する電子メール サーバーの Exchange の場所 (URL) を指定します。
   - **[アカウント名]** :**会社の電子メール**を入力します。
   - **[AAD からのユーザー名の属性]** :Intune が Azure Active Directory (Azure AD) から取得する名前。 Intune では、この名前を使用してこのプロファイルのユーザー名を動的に生成します。 このクイック スタートでは、プロファイルのユーザー名として **[ユーザー プリンシパル名]** (たとえば、user1@contoso.com) を使用すると仮定します。
   - **[AAD からのメール アドレス属性]** :この設定は、Exchange へのサインインに使用する Azure AD からの電子メール アドレスです。 このクイック スタートでは、 **[ユーザー プリンシパル名]** を選択します。
   - **[認証方法]** :このクイック スタートでは、 **[ユーザー名とパスワード]** を選択します (Intune に証明書を既に設定している場合は、 **[証明書]** を選択することもできます)。

8. **[次へ]** を選択します。

9. **[スコープのタグ]** (省略可能) で、 **[次へ]** を選択します。 このプロファイルにはスコープのタグを使用しません。

10. **[割り当て]** で、 **[割り当て先]** ドロップダウンを使用して **[すべてのユーザーおよびすべてのデバイス]** を選択します。  **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 

## <a name="clean-up-resources"></a>リソースをクリーンアップする

追加のチュートリアルまたはテスト用に作成したプロファイルを使用しない場合は、ここで削除できます。

1. Intune で、 **[デバイス]**  >  **[デバイス構成]** を選択します。
2. 作成したテスト プロファイル "**iOS/iPadOS で職場の電子メールが必要**" を選択し、 **[削除]** を選択します。 

## <a name="next-steps"></a>次のステップ

このクイック スタートでは、iOS/iPadOS デバイス用の電子メール プロファイルを作成しました。 ここで、このプロファイルを使用して、プロファイルと一致しないすべての iOS/iPadOS デバイスを非準拠としてマークするコンプライアンス ポリシーを作成することで、iOS/iPadOS デバイスが準拠しているかどうかを判断することができます。 保護をさらに強化するには、非準拠の iOS/iPadOS デバイスが電子メールにアクセスできないようブロックする条件付きアクセス ポリシーを作成します。 デバイス コンプライアンス ポリシーの詳細については、[Intune でのデバイス コンプライアンス ポリシーの概要](../protect/device-compliance-get-started.md)に関するページを参照してください。

> [!div class="nextstepaction"]
> [チュートリアル:マネージド デバイス上で Exchange Online の電子メールを保護する](../protect/tutorial-protect-email-on-enrolled-devices.md)
