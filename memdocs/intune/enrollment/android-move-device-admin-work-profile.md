---
title: Android デバイスをデバイス管理者から仕事用プロファイル管理に移動する
titleSuffix: Microsoft Intune
description: Android デバイスをデバイス管理者から Intune の仕事用プロファイル管理に移動します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f16c39ff0af44918099863be5d23ec9fe564493
ms.sourcegitcommit: 954b3aae7916ad14065e6e86a577c5205103a50e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "80624911"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Android デバイスをデバイス管理者から仕事用プロファイル管理に移動する

ユーザーが Android デバイスをデバイス管理者から仕事用プロファイル管理に移動できるようにするには、コンプライアンス設定を使用して、 **[Block devices managed with device administrator]\(デバイス管理者により管理されているデバイスをブロックする\)** ようにします。 この設定を使用すると、デバイス管理者を使用して管理されているデバイスを非準拠にすることができます。 

ユーザーがこの理由でコンプライアンスに違反していることを確認した場合は **[解決]** をタップできます。 以下の手順を指示するチェックリストが表示されます。
1. デバイス管理者の管理からの登録解除
2. 仕事用プロファイルの管理への登録
3. コンプライアンスの問題の解決。 

## <a name="prerequisites"></a>[前提条件]

- ユーザーは、Android ポータル サイト バージョン 5.0.4720.0 以降の [Android デバイス管理者の登録済みデバイス](android-enroll-device-administrator.md)を持っている必要があります。
- [Intune テナント アカウントを Android Enterprise アカウント](connect-intune-android-enterprise.md)に接続して、Android 仕事用プロファイル管理を設定します。
- Android 仕事用プロファイルに移動するユーザーのグループに対して、[Android Enterprise 仕事用プロファイルの登録を設定します](android-work-profile-enroll.md)。
- ユーザー デバイスの制限を引き上げることを検討します。 デバイス管理者の管理からデバイスの登録を解除しても、デバイス レコードがすぐに削除されない場合があります。 この期間中の影響を軽減するために、必要に応じて、デバイスの制限容量を増やしてユーザーが仕事用プロファイル管理に登録できるようにします。
  - ユーザーごとのデバイスの最大数について [Azure Active Directory デバイス設定を構成します](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)。
  - デバイス制限を設定して、[Intune デバイス制限の制約](enrollment-restrictions-set.md#create-a-device-limit-restriction)を調整します。 

## <a name="create-device-compliance-policy"></a>デバイス コンプライアンス ポリシーを作成する

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシー]**  >  **[ポリシーの作成]** を選択します。

    ![ポリシーを作成する](./media/android-move-device-admin-work-profile/create-policy.png)

2. **[ポリシーの作成]** ページで、 **[プラットフォーム]** を **[Android デバイス管理者]** に設定し、 **[作成]** を選択します。
3. **[基本]** ページで、 **[名前]** と **[説明]** を入力し、 **[次へ]** を選択します。

    ![[基本] ページ](./media/android-move-device-admin-work-profile/basics.png)
    
4. **[コンプライアンス設定]** ページの **[デバイスの正常性]** セクションで、 **[Block devices managed with device administrator]\(デバイス管理者により管理されているデバイスをブロックする\)** を **[はい]** に設定し、 **[次へ]** を選択します。

    ![デバイスをブロックする](./media/android-move-device-admin-work-profile/block-devices.png)

5. **[場所]** ページでは、目的の場所を追加し、 **[次へ]** を選択することができます。
6. **[コンプライアンス非対応に対するアクション]** で、 **[メールをエンド ユーザーに送信する]** アクションを設定できます。

    ![メールを送信する](./media/android-move-device-admin-work-profile/send-email.png)


    メールでは、ユーザーへのメッセージに以下の URL を含めることができます。 この URL を選択すると、Android ポータル サイトが起動し、 **[デバイス設定の更新]** ページが表示されます。 このページから、仕事用プロファイルの管理に移動するフローを開始します。
    - `https://portal.manage.microsoft.com/UpdateSettings.aspx` にする必要があります。
    - 米国政府の場合は、代わりに次のリンクを使用することができます: `https://portal.manage.microsoft.us/UpdateSettings.aspx`。
  
    > [!NOTE]
    > - もちろん、ユーザーへの連絡には、ユーザーにわかりやすいハイパーテキストをリンクに使用できます。 ただし、URL 短縮サービスを使用しないでください。このように変更するとリンクが機能しなくなる可能性があります。
    > - Android ポータル サイトが開いていてバックグラウンドにある場合、ユーザーがリンクをタップすると、代わりに開いていた最後のページが表示される可能性があります。
    > - ユーザーは、Android デバイス上のリンクをタップする必要があります。 代わりにブラウザーに貼り付けても、Android ポータル サイトは起動しません。 

    **[次へ]** を選択します。

7. **[スコープ タグ]** ページで、含めるスコープ タグを選択します。
8. **[割り当て]** ページで、デバイス管理者の管理に登録されているデバイスを持つグループにポリシーを割り当て、 **[次へ]** をクリックします。
9. **[確認および作成]** ページで、すべての設定を確認し、 **[作成]** を選択します。

## <a name="troubleshooting"></a>トラブルシューティング

[新しいデバイス管理設定に移動するエンド ユーザー フロー](../user-help/move-to-new-device-management-setup.md)のページには、ユーザーをデバイス管理者の管理から登録を解除し、仕事用プロファイル管理を設定する手順が示されています。 ユーザーは、Android ポータル サイト バージョン 5.0.4720.0 以降の [Android デバイス管理者の登録済みデバイス](android-enroll-device-administrator.md)を持っている必要があります。

### <a name="user-sees-an-error-after-tapping-resolve"></a>ユーザーが [解決] をタップした後にエラーが表示される
**[解決]** ボタンをタップした後にエラーが表示される場合は、次のいずれかの理由が考えられます。
- 仕事用プロファイルの登録が正しく設定されていません (Android Enterprise アカウントが接続されていないか、仕事用プロファイルの登録をブロックするように登録制限に設定されています)。
- デバイスでは、仕事用プロファイルの登録をサポートしていない Android 4.4 以前が実行されています。 
- デバイスの製造元は、デバイス モデルでの仕事用プロファイルの登録をサポートしていません。

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>[解決] ボタンがユーザーのデバイスに表示されない
ユーザーが上記のデバイス コンプライアンス ポリシーの対象となった後でデバイス管理者の管理に登録した場合、 **[解決]** ボタンはユーザーのデバイスに表示されません。

**[解決]** ボタンを表示するには、ユーザーがセットアップを延期し、通知からプロセスを再開する必要があります。

この状況を回避するには、登録制限を使用して、デバイス管理者の管理への登録をブロックします。

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>[デバイス設定の更新] ページの URL をタップするとエラーが表示される
ユーザーが Android ポータル サイトの **[デバイス設定の更新]** ページの URL をタップすると、ブラウザーにエラー ページが表示される場合があります。 このエラーは、以下のいずれかが原因と考えられます。
- デバイスが Android ではありません。
- Android デバイスにポータル サイト アプリがインストールされていません。
- Android ポータル サイトが 5.0.4720.0 より前のバージョンです。
- Android デバイスで Android 6 以前が使用されています。 

## <a name="next-steps"></a>次のステップ
[エンド ユーザーのフローを確認する](../user-help/move-to-new-device-management-setup.md)
[Intune で Android 仕事用プロファイルのデバイスを管理する](android-enterprise-overview.md)
