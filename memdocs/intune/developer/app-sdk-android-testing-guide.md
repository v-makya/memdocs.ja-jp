---
title: Android 用 Microsoft Intune App SDK テスト ガイド
description: Android 用 Microsoft Intune アプリ SDK テスト ガイドは、Intune で管理される Android アプリのテストに役立ちます。
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce008c21cefeb3920182a09547db091547681401
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343077"
---
# <a name="microsoft-intune-app-sdk-for-android-testing-guide"></a>Android 用 Microsoft Intune App SDK テスト ガイド

このガイドは、開発者が Intune で管理されている Android アプリをテストするのに役立ちます。  

## <a name="prerequisite-test-accounts"></a>前提条件のテスト アカウント
事前に生成されたデータを使用して、または使用せずに、新しいアカウントを作成できます。 新しいアカウントを作成するには:
1. [Microsoft Demos](https://demos.microsoft.com/environments/create/tenant) のサイトに移動します。 
2. モバイル デバイス管理 (MDM) が有効になるよう、[Intune をセットアップ](../fundamentals/setup-steps.md)します。
3. [ユーザーを作成します](../fundamentals/users-add.md)。
4. [グループを作成します](../fundamentals/groups-add.md)。
5. テストに適した[ライセンスを割り当てます](../fundamentals/licenses-assign.md)。


## <a name="azure-portal-policy-configuration"></a>Azure Portal ポリシー構成
[Azure portal の Intune ブレード](https://portal.azure.com/?feature.customportal=false#blade/Microsoft_Intune_Apps/MainMenu/14/selectedMenuItem/Overview)で[アプリ保護ポリシーを作成し、割り当てます](../apps/app-protection-policies.md)。 Intune ブレードで[アプリ構成ポリシー](../apps/app-configuration-policies-overview.md)を作成し、割り当てることもできます。

> [!NOTE]
> アプリが Azure portal で一覧表示されていない場合は、 **[その他のアプリ]** オプションを選択し、テキスト ボックスにパッケージ名を指定することで、ポリシーを使って対象とすることができます。

## <a name="test-cases"></a>テスト ケース

次のテスト ケースでは、構成と確認の手順がわかります。 このガイダンスを使用すると、Intune で管理される Android アプリの問題解決に役立てることができます。

### <a name="required-pin-and-corporate-credentials"></a>必要な PIN と会社の資格情報

会社のリソースへのアクセスに PIN を要求できます。 また、ユーザーが管理対象アプリを使用する前に会社による認証を強制できます。 次に手順を示します。

1. **[アクセスのために PIN を要求する]** と **[アクセスの際に会社の資格情報を要求する]** を **[はい]** に設定します。 詳細については、「[Microsoft Intune の Android アプリ保護ポリシー設定](../apps/app-protection-policy-settings-android.md#access-requirements)」を参照してください。
2. 次の条件を確認します。
    - アプリが起動するとき、PIN の入力や、ポータル サイトへの登録中に使用した実ユーザーの入力が求められます。
    - Android マニフェストが正しく構成されていない場合、特に Azure Active Directory Authentication Library (ADAL) 統合 (SkipBroker、ClientID、Authority) の値が間違っている場合、有効なサインイン プロンプトを提示できないことがあります。
    - `MAMActivity` 値が正しく統合されていないことが、プロンプトが表示されないことの原因である場合があります。 `MAMActivity` の詳細については、「[Android 用 Microsoft Intune アプリ SDK 開発者ガイド](app-sdk-android.md)」を参照してください。

> [!NOTE] 
> 前のテストが動作していない場合は、次のテストも失敗する可能性があります。 [SDK](app-sdk-android.md#sdk-integration) と [ADAL](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal) 統合を確認してください。

### <a name="restrict-transferring-and-receiving-data-with-other-apps"></a>他のアプリによるデータの転送と受信を制限する
会社で管理されるアプリケーション間のデータ転送を次のように制御できます。

1. **[アプリで他のアプリへのデータ転送を許可する]** を **[ポリシー マネージド アプリ]** に設定します。
2. **[このアプリで他のアプリからデータを受信できるようにする]** を **[すべてのアプリ]** に設定します。 意図とコンテンツ プロバイダーの使用は、これらのポリシーの影響を受けます。
3. 次の条件を確認します。
    - 非管理対象アプリから自分のアプリに開くと、正しく機能します。
    - 管理対象アプリ間でコンテンツを共有できます。
    - 管理対象アプリと非管理対象アプリ (Chrome など) の間の共有は禁止されています。

### <a name="restrict-cut-copy-and-paste"></a>切り取り、コピー、貼り付けを制限
次のように、システム クリップボードをマネージド アプリケーションに制限できます。

1. **[他のアプリとの間で切り取り、コピー、貼り付けを制限する]** を **[貼り付けを使用する、ポリシーで管理されているアプリ]** に設定します。
2. 次の条件を確認します。
    - アプリからアンマネージド アプリ (例: Messages) へのテキストのコピーはブロックされています。

### <a name="prevent-save"></a>保存を禁止する
**[名前を付けて保存]** 機能を次のように制御できます。

1. アプリで[統合された [名前を付けて保存] コントロール](app-sdk-android.md#example-determine-if-saving-to-device-or-cloud-storage-is-permitted)が必要な場合は、 **[[名前を付けて保存] を禁止する]** を **[はい]** に設定します。
2. 次の条件を確認します。
    - 保存は、適切に管理されている場所にのみ制限されます。

### <a name="file-encryption"></a>ファイルの暗号化
次のように、デバイス上のデータを暗号化できます。

1. **[[アプリ データの暗号化]]** を **[はい]** に設定します。
2. 次の条件を確認します。
    - 通常のアプリケーション動作は影響を受けません。

### <a name="prevent-android-backups"></a>[Android でのバックアップを禁止する]
次のように、アプリのバックアップを制御できます。

1. [統合バックアップ制限](app-sdk-android.md#protecting-backup-data)を設定している場合は、 **[Android でのバックアップを禁止する]** を **[はい]** に設定します。
2. 次の条件を確認します。
    - バックアップが制限されます。

### <a name="unenrollment"></a>登録解除
会社のメールやドキュメントから、マネージド アプリをリモートでワイプできます。また、個人データは、管理されなくなったときに暗号化が解除されます。 次に手順を示します。

1. Azure portal から、[ワイプを発行します](../apps/apps-selective-wipe.md)。
2. アプリにワイプ ハンドラーが登録されていない場合、次の条件を確認してください。
    - アプリの完全ワイプが行われます。
3. アプリで `WIPE_USER_DATA` または `WIPE_USER_AUXILARY_DATA` が登録されている場合、次の条件を確認してください。
    - 管理コンテンツがアプリから削除されている。 詳細については、[Android 用 Intune App SDK の開発者ガイド - 選択的ワイプ](app-sdk-android.md#selective-wipe)に関するページをご覧ください。

### <a name="multi-identity-support"></a>複数 ID のサポート
[複数 ID サポート](app-sdk-android.md#multi-identity-optional)の組み込みは、高いリスクを伴う変更であり、徹底的なテストが必要となります。 最も一般的な問題は、ID の不適切な設定 (コンテキストと脅威レベル) と追跡ファイル (`MAMFileProtectionManager`) が原因で発生します。

少なくとは、次のことを確認します。

- **[名前を付けて保存]** が複数 ID で正しく機能している。
- マネージドから個人まで、制限のコピーと貼り付けが、正しく適用されている。
- マネージド ID に属するデータのみが暗号化され、個人ファイルは変更されていない。
- 登録解除中の選択的ワイプでは、マネージド ID データのみが削除される。
- アンマネージド アカウントからマネージド アカウントに変更するとき、ユーザーに条件付き起動が求められる (初回のみ)。

### <a name="app-configuration-optional"></a>アプリの構成 (省略可能)
マネージド アプリの動作は構成できます。 アプリで何らかのアプリ構成設定が使用される場合、(管理者として) 設定できるすべての値がアプリで正しく処理されることをテストしてください。 Intune で[アプリ構成ポリシー](../apps/app-configuration-policies-overview.md)を作成し、割り当てることができます。

## <a name="next-steps"></a>次のステップ

- [Android の基幹業務アプリを Microsoft Intune に追加する](../apps/lob-apps-android.md)
