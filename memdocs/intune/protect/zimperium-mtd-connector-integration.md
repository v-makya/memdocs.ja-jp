---
title: Zimperium MTD を Microsoft Intune と統合する
titleSuffix: Microsoft Intune
description: Microsoft Intune で Zimperium Mobile Threat Defense (MTD) ソリューションをセットアップし、モバイル デバイスから会社のリソースへのアクセスを制御する方法。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5bb106e482beb7894c84f11d0994b43ba43eb302
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79338384"
---
# <a name="integrate-zimperium-with-intune"></a>Zimperium を Intune と統合する

Zimperium Mobile Threat Defense ソリューションを Intune と統合するには、次の手順をすべて実行します。

## <a name="before-you-begin"></a>始める前に

[Zimperium MTD コンソール](https://www.zimperium.com/platform)内で、以下の手順を実行します。これにより、Intune に登録されているデバイス (デバイス コンプライアンスを使用) および登録されていないデバイス (アプリ保護ポリシーを使用) の両方で Zimperium のサービスに接続できるようになります。

Zimperium と Intune の統合を始める前に、次のサブスクリプションと資格情報があることを確認します。

- Microsoft Intune サブスクリプション

- 次のアクセス許可を付与する、Azure Active Directory グローバル管理者の管理者資格情報:

  - サインインしてユーザー プロファイルを読み取る

  - サインインしたユーザーとしてディレクトリにアクセスする

  - ディレクトリ データの読み込み

  - Intune にデバイス情報を送信する

- Zimperium MTD コンソールにアクセスするための管理者資格情報。

### <a name="zimperium-app-authorization"></a>Zimperium アプリの承認

Zimperium アプリ承認プロセスは以下で構成されます。

- Zimperium サービスがデバイスの正常性状態に関する情報を Intune に通知できるようにします。 これらのアクセス許可を付与するには、グローバル管理者の資格情報を使用する必要があります。 アクセス許可の付与は 1 回限りの操作です。 アクセス許可が付与されたら、日常業務でグローバル管理者の資格情報が必要になることはありません。

- Zimperium は、Azure Active Directory (AD) 登録グループ メンバーシップと同期してデバイスのデータベースを設定します。

- Zimperium 管理者コンソールが Azure AD シングル サインオン (SSO) を使用できるようにします。

- Zimperium アプリが Azure AD SSO を使用してサインインできるようにします。

同意と Azure Active Directory アプリケーションの詳細については、Azure Active Directory の記事「*Azure Active Directory v2.0 エンドポイントでのアクセス許可と同意*」の「[ディレクトリ管理者にアクセス許可を要求する](https://docs.microsoft.com/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin)」をご覧ください。


## <a name="to-set-up-zimperium-integration"></a>Zimperium の統合を設定するには

1. [Zimperium MTD コンソール](https://www.zimperium.com/platform)に移動し、資格情報を使用してサインインします。 Zimperium 統合のセットアップ プロセスを実行するには、グローバル管理者のロールを持つ Azure Active Directory ユーザーとしてサインインする必要があります。 この 1 回限りのセットアップ操作では、グローバル管理者権限を使用して、組織内で Zimperium アプリが Intune と通信する権限を付与します。 

2. 左のメニューから **[Management]\(管理\)** を選択します。

3. **[MDM settings]\(MDM の設定\)** タブを選択します。

4. **[Add MDM]\(MDM の追加\)** を選択し、 **[MDM provider]\(MDM プロバイダー\)** 一覧から **[Microsoft Intune]** を選択します。

5. Microsoft Intune を MDM サービスとして設定すると、 **[Microsoft Intune Configuration]\(Microsoft Intune 構成\)** ウィンドウが開くので、 **[Zimperium zConsole]** と **[zIPS iOS and Android apps]\(zIPS iOS および Android アプリ\)** オプションのそれぞれに **[Azure Active Directory を追加する]** を選択します。これらのオプションは Zimperium が Azure AD シングル サインオンを使用して Intune および Azure AD と通信することを承認するものです。

    > [!IMPORTANT]  
    > Intune との統合プロセスを完了するには、[Zimperium zConsole] と [zIPS iOS and Android apps]\(zIPS iOS および Android アプリ\) を追加する必要があります。

6. **[Accept\(承認\)]** を選択して、Zimperium アプリが Intune および Azure Active Directory と通信することを承認します。

7. **[Zimperium zConsole]** と **[zIPS iOS and Android apps]\(zIPS iOS および Android アプリ\)** を Azure AD に追加したら、Azure AD セキュリティ グループを追加します。 これで、Zimperium が Azure AD セキュリティ グループとそのサービスを同期できるようになります。

8. **[Finish]\(完了\)** を選択して構成を保存し、最初の Azure AD セキュリティ グループの同期を開始します。

9. Zimperium MTD コンソールからサインアウトします。

## <a name="next-steps"></a>次のステップ

- [登録されたデバイスに Zimperium アプリを設定する](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [登録されていないデバイスに Zimperium アプリを設定する](mtd-add-apps-unenrolled-devices.md)
