---
title: 仕事用プロファイルを備えた会社所有の Android Enterprise デバイスの Intune 登録の設定
titleSuffix: Microsoft Intune
description: 仕事用プロファイルを備えた会社所有の Android Enterprise デバイスを Intune で登録する方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a19a78002d0655cf63a8b757ea252fb8992603f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915264"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>仕事用プロファイルを備えた会社所有の Android Enterprise デバイスの Intune 登録の設定

仕事用プロファイルを備えた会社所有の Android Enterprise デバイスは、会社および私事での使用が想定される単一ユーザー デバイスです。

エンド ユーザーは、仕事のデータと個人のデータを分けておくことができ、個人のデータとアプリケーションのプライバシーの維持が保証されます。 管理者は、デバイス全体にわたって設定や機能の一部を管理することができます。次に例を示します。

- デバイス パスワードの要件の設定
- Bluetooth とデータ ローミングの制御
- 工場出荷時へのリセット防止の構成

Intune は、仕事用プロファイルを備えた会社所有の Android Enterprise デバイスへのアプリと設定の展開に役立ちます。 Android Enterprise に関する特定の詳細については、[Android Enterprise の要件](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)に関するページを参照してください。

## <a name="device-requirements"></a>デバイスの要件

仕事用プロファイルを備えた会社所有の Android Enterprise デバイスとしてデバイスを管理するには、以下の要件を満たす必要があります。

- Android OS バージョン 8.0 以降。
- デバイスは、Google Mobile Services (GMS) に接続できる Android ディストリビューションを実行する必要があります。 デバイスで GMS が利用できて、GMS に接続できる必要があります。

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>仕事用プロファイルを備えた会社所有の Android Enterprise デバイスの管理を設定する

仕事用プロファイルを備えた会社所有の Android Enterprise デバイスの管理を設定するには、次の手順を行います。

1. モバイル デバイス管理の準備として、[MDM (モバイル デバイス管理) 機関を **Microsoft Intune** に設定](../fundamentals/mdm-authority-set.md)し、そこに指示を求める必要があります。 この項目は、モバイル デバイス管理について初めて Intune を設定するときに一度だけ設定します。
2. [managed Google Play アカウントに Intune テナント アカウントを接続します](connect-intune-android-enterprise.md)。
3. [登録プロファイルを作成します](#create-an-enrollment-profile)。
4. [デバイス グループを作成します](#create-a-device-group)。
5. [会社所有の仕事用プロファイル デバイスを登録します](#enroll-the-corporate-owned-work-profile-devices)。

### <a name="create-an-enrollment-profile"></a>登録プロファイルの作成

> [!NOTE]
> 仕事用プロファイルを備えた会社所有のデバイスのトークンは、自動的に期限切れになることはありません。 管理者がトークンの取り消しを決定した場合、そのトークンに関連付けられているプロファイルは、 **[デバイス]**  >  **[Android]**  >  **[Android の登録]**  >  **[仕事用プロファイルを備えた会社所有のデバイス (プレビュー)]** の順に移動しても表示されることはありません。 アクティブと非アクティブの両方のトークンに関連付けられているすべてのプロファイルを表示するには、 **[フィルター]** をクリックし、[アクティブ] と [非アクティブ] の両方のポリシーの状態のチェックボックスをオンにします。 

ユーザーが会社所有の仕事用プロファイル デバイスを登録できるように、登録プロファイルを作成する必要があります。 プロファイルが作成されると、登録トークン (ランダムな文字列) と QR コードが与えられます。 デバイスの Android OS とバージョンに基づき、トークンか QR コードのいずれかを使って[専用デバイスを登録](#enroll-the-corporate-owned-work-profile-devices)できます。

1. [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインして、 **[デバイス]**  >  **[Android]**  >  **[Android の登録]**  >  **[仕事用プロファイルを備えた会社所有のデバイス (プレビュー)]** の順に選択します。
2. **[プロファイルの作成]** を選択して、必須フィールドに入力します。
    - **名前**:動的デバイス グループにプロファイルを割り当てるときに使用する名前を入力します。
    - **説明**:プロファイルの説明を追加します (省略可能)。
3. **[次へ]** を選択します。
5. **[確認および作成]** ページで、 **[作成]** を選択してポリシーを作成します。

### <a name="create-a-device-group"></a>デバイス グループを作成する

アプリとポリシーの対象を、割り当てたデバイス グループか動的デバイス グループに設定できます。 特定の登録プロファイルで登録されているデバイスに自動でデータを入力するように、次の手順で動的 Azure AD デバイス グループを構成できます。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインし、 **[グループ]**  >  **[すべてのグループ]**  >  **[新しいグループ]** を選択します。
2. **[グループ]** ブレードで、次のように必須フィールドに入力します。
    - **[グループの種類]** :セキュリティ
    - **[グループ名]** :わかりやすい名前を入力します (Factory 1 デバイスなど)
    - **[メンバーシップの種類]** :動的デバイス
3. **[動的クエリの追加]** を選択します。
4. **[動的メンバーシップ ルール]** ブレードで、次のようにフィールドに入力します。
    - **[動的メンバーシップ ルールの追加]** :簡易ルール
    - **[追加するデバイスの場所]** : enrollmentProfileName
    - 中央のボックスで **[等しい]** を選択します。
    - 最後のフィールドには、先ほど作成した登録プロファイル名を入力します。
    動的メンバーシップ ルールの詳細については、[AAD 内のグループに対する動的メンバーシップ ルール](/azure/active-directory/users-groups-roles/groups-dynamic-membership)に関する記事を参照してください。 
5. **[クエリの追加]**  >  **[作成]** を選択します。

### <a name="revoke-tokens"></a>トークンの取り消し

トークン/QR コードをただちに失効させることができます。 取り消した時点から、トークンまたは QR コードは使用できなくなります。 次の場合にこのオプションを使用できます。
  - 認められていない団体と誤ってトークン/QR コードを共有した
  - 登録がすべて完了し、トークン/QR コードが不要になった

トークン/QR コードを取り消しても、登録済みのデバイスに影響が出ることはありません。

1. [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインして、 **[デバイス]**  >  **[Android]**  >  **[Android の登録]**  >  **[仕事用プロファイルを備えた会社所有のデバイス (プレビュー)]** の順に選択します。
2. 置き換えるか取り消すプロファイルを選択します。
3. **[トークン]** を選択します。
5. トークンを取り消すには、 **[トークンの取り消し]**  >  **[はい]** を選択します。

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>会社所有の仕事用プロファイル デバイスを登録する

ユーザーは、[会社所有の仕事用プロファイル デバイスを登録](android-dedicated-devices-fully-managed-enroll.md)することができるようになりました。

> [!NOTE]
> **Microsoft Intune** アプリは、会社所有の仕事用プロファイル デバイスの登録時に自動的にインストールされます。  このアプリは登録に必要であり、アンインストールすることはできません。 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>会社所有の Android Enterprise 仕事用プロファイル デバイス上のアプリの管理

割り当ての種類が [[必須] に設定されている](../apps/apps-deploy.md#assign-an-app)アプリのみ、会社所有の Android Enterprise 仕事用プロファイル デバイスにインストールできます。 アプリは、Android Enterprise 仕事用プロファイル デバイスと同じ方法で managed Google Play ストアからインストールされます。

アプリは、アプリ開発者が更新版を Google Play に公開したとき、管理対象デバイスで自動的に更新されます。

会社所有の Android Enterprise 仕事用プロファイル デバイスからアプリを削除するには、次のいずれかの操作を行います。
- 要求されたアプリの展開を削除します。
- アプリのアンインストール展開を作成します。

## <a name="next-steps"></a>次のステップ
- [Android アプリを展開する](../apps/apps-deploy.md)
- [Android 構成ポリシーを追加する](../configuration/device-profiles.md)