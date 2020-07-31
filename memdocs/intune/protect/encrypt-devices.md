---
title: Intune で Windows 10 デバイスを BitLocker で暗号化する
titleSuffix: Microsoft Intune
description: BitLocker に組み込まれている暗号化方式を使用してデバイスを暗号化し、Intune ポータル内からそれらの暗号化されたデバイスの回復キーを管理します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: a9fad599342cf358409c7be09ebb8b4eb1c0c4a5
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334625"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Intune で Windows 10 の BitLocker ポリシーを管理する

Intune を使用して、Windows 10 を実行するデバイスで BitLocker ドライブ暗号化を構成します。

BitLocker は、Windows 10 以降を実行しているデバイスで使用できます。 BitLocker の一部の設定では、デバイスにサポートされている TPM が必要です。

次の種類のポリシーのいずれかを使用して、マネージド デバイスで BitLocker を構成します。

- **[Windows 10 BitLocker のエンドポイント セキュリティ ディスク暗号化ポリシー](#create-an-endpoint-security-policy-for-bitlocker)** 。 *エンドポイント セキュリティ*の BitLocker プロファイルは、BitLocker の構成専用の一連の設定です。

  [ディスク暗号化ポリシーの BitLocker プロファイル](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)で、利用可能な BitLocker 設定を表示します。

- **[Windows 10 BitLocker のエンドポイント保護のデバイス構成プロファイル](#create-an-endpoint-security-policy-for-bitlocker)** 。 BitLocker 設定は、Windows 10 エンドポイント保護で使用可能な設定カテゴリの 1 つです。

  [デバイス構成ポリシーのエンドポイント保護プロファイルの BitLocker で使用できる BitLocker 設定](../protect/endpoint-protection-windows-10.md#windows-settings)を表示します。

> [!TIP]
> Intune では、すべてのマネージド デバイスのデバイスの暗号化ステータスに関する詳細を表示する、組み込みの[暗号化レポート](encryption-monitor.md)を用意されています。 Intune で BitLocker を使用して Windows 10 デバイスを暗号化すると、暗号化レポートを表示したときに、BitLocker 回復キーを表示して取得できます。
>
> Azure Active Directory (Azure AD) で見られるように、お使いのデバイスから BitLocker の重要な情報にアクセスすることもできます。
すべてのマネージド デバイスのデバイスの暗号化ステータスに関する詳細を表示する、組み込みの[暗号化レポート](encryption-monitor.md)。

## <a name="permissions-to-manage-bitlocker"></a>BitLocker を管理するためのアクセス許可

Intune で BitLocker を管理するには、アカウントに適切な Intune [ロールベースのアクセス制御](../fundamentals/role-based-access-control.md) (RBAC) アクセス許可を与える必要があります。

リモート タスク カテゴリとアクセス許可を付与する組み込み RBAC ロールに含まれる、BitLocker アクセス許可を以下に示します。

- **BitLocker キーの交換**
  - ヘルプ デスク オペレーター

## <a name="create-and-deploy-policy"></a>ポリシーの作成と展開

次のいずれかの手順に従って、目的のポリシーの種類を作成します。

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>BitLocker のエンドポイント セキュリティ ポリシーを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[ディスク 暗号化]**  >  **[ポリシーの作成]** を選択します。

3. 次のオプションを設定します。
   1. **[プラットフォーム]** :Windows 10 以降
   2. **[プロファイル]** :BitLocker

   ![BitLocker プロファイルの選択](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. **[構成設定]** ページで、ビジネス ニーズに合わせて BitLocker の設定を構成します。  

   BitLocker をサイレント モードで有効にする場合は、この記事の「[デバイスで BitLocker をサイレント モードで有効にする](#silently-enable-bitlocker-on-devices)」を参照してください。他の前提条件と使用する必要のある設定構成について説明します。

   **[次へ]** を選択します。

5. **[スコープ (タグ)]** タブで **[スコープ タグを選択]** を選択し、[タグを選択する] ウィンドウを開いて、プロファイルにスコープ タグを割り当てます。

   **[次へ]** を選択して続行します。

6. **[割り当て]** ページで、このプロファイルを受け取るグループを選択します。 プロファイルの割り当ての詳細については、ユーザーおよびデバイス プロファイルの割り当てに関するページを参照してください。

   **[次へ]** を選択します。

7. **[確認および作成]** ページで、完了したら、 **[作成]** を選択します。 作成したプロファイルのポリシーの種類を選択すると、新しいプロファイルが一覧に表示されます。

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>BitLocker 用のデバイス構成プロファイルを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. 次のオプションを設定します。
   1. **[プラットフォーム]** :Windows 10 以降
   2. **[プロファイルの種類]** :エンドポイント保護

   ![BitLocker プロファイルの選択](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. **[設定]**  >  **[Windows 暗号化]** の順に選択します。

   ![BitLocker 設定](./media/encrypt-devices/bitlocker-settings.png)

5. ビジネス ニーズに合わせて BitLocker の設定を構成します。

   BitLocker をサイレント モードで有効にする場合は、この記事の「[デバイスで BitLocker をサイレント モードで有効にする](#silently-enable-bitlocker-on-devices)」を参照してください。他の前提条件と使用する必要のある設定構成について説明します。

6. **[OK]** を選択します。

7. 追加設定の構成を完了したら、プロファイルを保存します。

## <a name="manage-bitlocker"></a>BitLocker の管理

BitLocker ポリシーを受信するデバイスに関する情報を表示するには、[ディスク暗号化の監視](../protect/encryption-monitor.md)に関する記事を参照してください。 暗号化レポートを表示するときに、BitLocker 回復キーを表示および取得することもできます。

### <a name="silently-enable-bitlocker-on-devices"></a>デバイスで BitLocker をサイレント モードで有効にする

デバイスで BitLocker を自動的にサイレント モードで有効にする BitLocker ポリシーを構成できます。 つまり、ユーザーがデバイスのローカル管理者でない場合でも、エンド ユーザーに UI を表示せずに BitLocker が正常に有効化されます。

**デバイスの前提条件**:

BitLocker をサイレント モードで有効にするには、デバイスが次の条件を満たしている必要があります。

- デバイスで Windows 10 バージョン 1809 以降を実行している必要があります
- デバイスが Azure AD に参加している必要があります  

**BitLocker ポリシーの構成**:

BitLocker ポリシーでは、*BitLocker の基本設定*の次の 2 つの設定を構成する必要があります。

- **他のディスク暗号化に対する警告** =  "*ブロック*"。
- **Azure AD 参加中の暗号化の有効化を標準ユーザーに許可する** =  "*許可*"

BitLocker ポリシーでは、スタートアップ PIN またはスタートアップ キーの使用は**必要ありません**。 TPM スタートアップ PIN またはスタートアップ キーが "*必須*" である場合、BitLocker をサイレント モードで有効にできず、エンド ユーザーとの対話が必要です。  この要件を満たすには、同じポリシーの次の 3 つの *BitLocker OS ドライブ設定*を行います。

- **[互換性のある TPM スタートアップ PIN]** を "*TPM でスタートアップ PIN を要求する*" に設定しないでください
- **[互換性のある TPM スタートアップ キー]** を "*TPM でスタートアップ キーを要求する*" に設定しないでください
- **[互換性のある TPM スタートアップ キーと PIN]** を "*TPM でスタートアップ キーと PIN を要求する*" に設定しないでください

### <a name="view-details-for-recovery-keys"></a>回復キーの詳細を表示する

Intune では BitLocker 用の Azure AD ブレードにアクセスできます。これにより、Intune ポータル内から、ご利用の Windows 10 デバイス用の BitLocker キー ID および回復キーを確認できます。 アクセスできるようになるには、デバイスのキーが Azure AD にエスクローされている必要があります。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[すべてのデバイス]** の順に選択します。

3. 一覧からデバイスを選択して、 *[監視]* 下にある **[回復キー]** を選択します。
  
   キーが Azure AD で利用できる場合は、次の情報を入手できます。
   - BitLocker キー ID
   - BitLocker 回復キー
   - ドライブの種類

   キーが Azure AD 内に存在していない場合、Intune によって "*このデバイスの BitLocker キーが見つかりません*" が表示されます。

BitLocker の情報については、[BitLocker 構成サービス プロバイダー](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) (CSP) に関するページを参照してください。 BitLocker CSP は、Windows 10 の場合、バージョン 1703 以降で、Windows 10 Pro の場合、バージョン 1809 以降でサポートされています。

### <a name="rotate-bitlocker-recovery-keys"></a>BitLocker 回復キーを交換する

Intune デバイス アクションを使用することで、Windows 10 バージョン 1909 以降を実行するデバイスの BitLocker 回復キーをリモートで交換できます。

#### <a name="prerequisites"></a>[前提条件]

BitLocker 回復キーの交換をサポートするには、デバイスで次の前提条件を満たしている必要があります。

- デバイスで Windows 10 バージョン 1909 以降を実行している必要があります。

- Azure AD 参加デバイスと Hybrid 参加デバイスでは、BitLocker ポリシーの構成を使用してキーの交換のサポートを有効にしておく必要があります。

  - **[クライアント主導の回復パスワードのローテーション]** を *[Azure AD 参加済みデバイスでローテーションを有効にする]* または *[Azure AD およびハイブリッド参加済みデバイスでローテーションを有効にする]* に
  - **[BitLocker 回復情報を Azure Active Directory に保存]** を *[有効]* に
  - **[BitLocker を有効にする前に Azure Active Directory で回復情報を保存]** を *[必須]* に

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>BitLocker 回復キーを交換するには

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[すべてのデバイス]** の順に選択します。

3. 管理するデバイスの一覧で、デバイスを選択して、 **[詳細]** を選択し、 **[BitLocker キーの交換]** デバイス リモート アクションを選択します。

4. デバイスの **[概要]** ページで、 **[BitLocker キーの交換]** を選択します。 このオプションが表示されない場合は、省略記号 ( **...** ) を選択して他のオプションを表示し、 **[BitLocker キーの交換]** デバイス リモート アクションを選択します。

   ![省略記号を選択してその他のオプションを表示](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>次のステップ

[FileVault ポリシーの管理](../protect/encrypt-devices-filevault.md)

[ディスク暗号化の監視](../protect/encryption-monitor.md)
