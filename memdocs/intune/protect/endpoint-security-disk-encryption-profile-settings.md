---
title: Intune エンドポイント セキュリティのディスク暗号化ポリシー設定 | Microsoft Docs
description: Microsoft Intune における BitLocker および FileVault 用のエンドポイント セキュリティのディスク暗号化ポリシー設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 37e9f68951c3576393e6ed3eb3346847029736c4
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663210"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのディスク暗号化ポリシー設定

[エンドポイント セキュリティ ポリシー](../protect/endpoint-security-policy.md)の一部として、Intune のエンドポイント セキュリティ ノードにある "*ディスク暗号化*" ポリシーのプロファイルで構成できる設定を確認します。

サポートされているプラットフォームとプロファイル

- **macOS**:
  - プロファイル: **FileVault**
- **Windows 10 以降**:
  - プロファイル: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>暗号化

**[FileVault を有効にする]**  
- **[未構成]** ("*既定値*")
- **[はい]** - macOS 10.13 以降が実行されるデバイスで、XTS-AES 128 と FileVault を使用したディスク全体の暗号化を有効にします。 FileVault は、ユーザーがデバイスからサインオフすると有効になります。

  *[はい]* に設定した場合は、FileVault の追加設定を構成できます。

  - **[回復キーの種類]** 
    "*個人用キー*" の回復キーがデバイスに対して作成されます。 個人用キーの次の設定を構成します。

    - **[個人用回復キーの交換]**  
      デバイスの個人用回復キーを交換する頻度を指定します。 既定値の **[未構成]** または **1** から **12** か月の値を選択できます。
    - **[個人用回復キーのエスクローの場所に関する説明]**  
      個人用回復キーを取得できる方法をユーザーに対して説明する短いメッセージを指定します。 このメッセージは、ユーザーがパスワードを忘れた場合に個人用回復キーの入力を求められる際にサインイン画面に表示されます。

  - **バイパスを許可する回数**  
    ユーザーのサインインに FileVault が必要となる前に、FileVault を有効にするプロンプトをユーザーが無視できる回数を設定します。
    - **[未構成]** ("*既定値*") - 次のサインインが許可される前に、デバイスの暗号化が必要です。
    - **1** から **10** - ユーザーは、デバイスの暗号化を要求する前に、1 から 10 回までプロンプトを無視できます。
    - **[制限なし、常に通知]** - ユーザーは FileVault を有効にするよう求められますが、暗号化は必要ありません。

  - **[サインアウトするまで延期を許可する]**  
    - **[未構成]** ("*既定値*")
    - **[はい]** - ユーザーがサインアウトするまで、FileVault を有効にするためのプロンプトを延期します。  

  - **サインアウト時のプロンプトを無効にする**  
    ユーザーがサインアウトするときに FileVault を有効にするように要求するプロンプトを表示しないようにします。無効に設定すると、サインアウト時のプロンプトは無効になり、代わりにユーザーがサインインするときにメッセージが表示されます。
    - **[未構成]** ("*既定値*")
    - **[はい]** - サインアウト時に表示される、FileVault を有効にするためのプロンプトを無効にします。

  - **[Hide recovery key]\(回復キーを非表示にする\)**  
     暗号化中は、macOS デバイスのユーザーに個人用回復キーが表示されなくなります。 ディスクが暗号化されると、ユーザーは任意のデバイスを使用して、Intune ポータル サイトの Web サイト経由、またはサポートされているプラットフォーム上のポータル サイト経由で、個人用回復キーを表示することができます。
    - **[未構成]** ("*既定値*")
    - **[はい]** - デバイスの暗号化中に個人用回復キーを非表示にします。

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker - 基本設定

- **OS および固定データ ドライブのディスク全体の暗号化を有効にする**  
  CSP:[RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  このポリシーが適用される前にドライブが暗号化されている場合、特別にアクションは行われません。 暗号化の方法とオプションがこのポリシーのものと一致する場合、構成からは成功が返されます。 インプレース BitLocker 構成オプションがこのポリシーと一致しない場合、構成からエラーが返される可能性があります。
  
  既に暗号化されているディスクにこのポリシーを適用するには、ドライブの暗号化を解除し、MDM ポリシーを再度適用します。 Windows の既定の設定では、BitLocker ドライブ暗号化が必要ありません。 ただし、Azure AD Join および Microsoft アカウント (MSA) では、登録またはログイン自動暗号化が適用され、BitLocker が XTS-AES 128 ビット暗号化で有効になる可能性があります。

  - **[未構成]** ("*既定値*") - BitLocker は強制されません。
  - **[はい]** - BitLocker の使用を強制します。

- **ストレージ カードの暗号化が必須 (モバイルのみ)**  
  CSP:[RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  この設定は、Windows Mobile および Mobile Enterprise SKU デバイスにのみ適用されます。
  - **[未構成]** ("*既定値*") - この設定は OS の既定値に戻されます。この場合、メモリ カードの暗号化は要求されません。
  - **[はい]** - モバイル デバイスでは、メモリ カードでの暗号化が必要です。

  > [!NOTE]
  > [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) と [Windows Phone 8.1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) のサポートは、2020 年 8 月に終了しました。

- **[Hide prompt about third-party encryption]\(サードパーティの暗号化に関するプロンプトを非表示にする\)**  
  CSP:[AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  サードパーティの暗号化製品によって既に暗号化されているシステムで BitLocker が有効になっている場合、デバイスが使用できなくなる可能性があります。 データが失われる可能性があることに加え、Windows の再インストールが必要になる可能性があります。 サードパーティの暗号化がインストールされているか有効になっているデバイスでは、BitLocker を有効にしないことを強くお勧めします。

  既定では、BitLocker セットアップ ウィザードにより、ユーザーはサードパーティの暗号化が適用されていないことを確認するよう求められます。

  - **[未構成]** ("*既定値*") – BitLocker セットアップ ウィザードでは警告が表示され、ユーザーはサードパーティの暗号化が存在しないことを確認するよう求められます。
  - **[はい]** - BitLocker セットアップ ウィザードのプロンプトがユーザーに表示されなくなります。

  必要なプロンプトでサイレント有効化ワークフローが中断されてしまうため、BitLocker のサイレント有効化機能が必要な場合は、サードパーティの暗号化に関する警告を非表示にする必要があります。

  *[はい]* に設定すると、次の設定を構成できます。

  - **[Autopilot 中の暗号化の有効化を標準ユーザーに許可する]**  
    CSP:[AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **[未構成]** ("*既定値*") – Azure Active Directory Join (AADJ) のサイレント有効化シナリオでは、ユーザーは BitLocker を有効にするためにローカル管理者である必要はありません。
    - **[はい]** - この設定はクライアントの既定値にままになり、BitLocker を有効にするにはローカル管理者アクセス権が必要になります。

    サイレント有効化やオートパイロット以外のシナリオでは、ユーザーは、BitLocker セットアップ ウィザードを完了するためにローカル管理者である必要があります。

- **[Enable client-driven recovery password for]\(クライアント主導の回復パスワードを有効にする\)**  
  CSP:[ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  職場アカウントの追加 (AWA、正式にはワークプレース参加済み) のデバイスは、キーの交換についてサポートされていません。
  - **[未構成]** ("*既定値*") – クライアントは BitLocker 回復キーを交換しません。
  - **[無効]**
  - **[Azure AD-joined devices]\(Azure AD 参加済みデバイス)\**
  - **[Azure AD およびハイブリッド参加済みデバイス]**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker - 固定ドライブの設定

- **BitLocker 固定ドライブ ポリシー**  
  [BitLocker グループ ポリシー設定](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **[固定ドライブの回復]**  
    CSP:[FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    必要なスタートアップ キー情報がない場合に BitLocker で保護されている固定データ ドライブを回復する方法を制御できます。

    - **[未構成]** ("*既定値*") - データ回復エージェント (DRA) を含む、既定の回復オプションがサポートされます。 エンド ユーザーが回復オプションを指定できるほか、回復情報は Azure Active Directory にバックアップされません。
    - **[構成]** – アクセスを有効にして、各種ドライブ回復方法を構成します。

    *[構成]* に設定した場合は、次の設定を使用できます。

    - **[ユーザーによる回復キーの作成]**  
      - **[ブロック]** ("*既定値*")
      - **必須**
      - **許可されます。**

    - **[Configure BitLocker recovery package]\(BitLocker 回復パッケージの構成\)**
      - **[パスワードとキー]** ("*既定値*") - 管理者とユーザーが保護されたドライブのロックを解除する際に使用する BitLocker 回復パスワードと、管理者が Active Directory で (データ回復の目的で) 使用する回復キー パッケージの両方を指定します。
      - **[パスワードのみ]** - 回復キー パッケージは、必要なときにアクセスできない場合があります。

    - **[Require device to back up recovery information to Azure Ad]\(デバイスが回復情報を Azure AD にバックアップすることを必須とする\)**
      - **[未構成]** ("*既定値*") - Azure AD への回復キーのバックアップが失敗した場合でも BitLocker の有効化が完了します。 これにより、回復情報が外部に保存されなくなる可能性があります。
      - **[はい]** - 回復キーが Azure Active Directory に正常に保存されるまで、BitLocker は有効化を完了しません。

    - **[ユーザーによる回復パスワードの作成]**  
      - **[ブロック]** ("*既定値*")
      - **必須**
      - **許可されます。**

    - **[Hide recovery options during BitLocker setup]\(BitLocker のセットアップ時に回復オプションを非表示にする\)**
      - **[未構成]** ("*既定値*") - ユーザーがその他の回復オプションにアクセスできるようにします。
      - **[はい]** - BitLocker セットアップ ウィザードで、エンド ユーザーがその他の回復オプション (回復キーの印刷など) を選択できないようにします。

    - **[回復情報を保存した後、BitLocker を有効にします]**
      - **[未構成]** ("*既定値*")  
      - **あり**

    - **[Block the use of certificate-based data recovery agent (DRA)]\(証明書ベースのデータ回復エージェント (DRA)の使用をブロックする\)**
      - **[未構成]** ("*既定値*") - DRA の使用を設定できます。 DRA を設定するには、エンタープライズ PKI とグループ ポリシー オブジェクトで DRA のエージェントと証明書を展開する必要があります。
      - **[はい]** - BitLocker が有効なドライブをデータ回復エージェント (DRA) を使用して回復する機能をブロックします。

  - **[Block write access to fixed data-drives not protected by BitLocker]\(BitLocker で保護されていない固定データドライブへの書き込みアクセスをブロックする\)**  
    CSP:[FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    この設定は、 *[BitLocker 固定ドライブ ポリシー]* が *[構成]* に設定されている場合に使用できます。

    - **未構成** (*既定値*) - 暗号化されていない固定ドライブにデータを書き込むことができます。
    - **[はい]** - Windows では、BitLocker で保護されていない固定ドライブにデータを書き込むことができません。 固定ドライブが暗号化されていない場合、ユーザーは、書き込みアクセス権が付与される前に、ドライブの BitLocker セットアップ ウィザードを完了する必要があります。

  - **固定データドライブの暗号化方法の構成**  
    CSP:[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    固定データドライブ ディスクの暗号化の方法と暗号強度を構成します。 *XTS - AES 128 ビット* は Windows の既定の暗号化方法であり、推奨される値です。

    - **[未構成]** ("*既定値*")
    - **AES 128 ビット CBC**
    - **AES 256 ビット CBC**
    - **AES 128 ビット XTS**
    - **AES 256 ビット XTS**

### <a name="bitlocker---os-drive-settings"></a>BitLocker - OS ドライブ設定

- **BitLocker システム ドライブ ポリシー**  
  CSP:[BitLocker グループ ポリシー設定](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **構成** (*既定値*)  
  - **未構成**

  *[構成]* に設定すると、次の設定を構成できます。

  - **[スタートアップ認証が必要]**  
    CSP:[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **[未構成]** ("*既定値*")
    - **[はい]** - システム スタートアップ時の追加の認証要件を構成します。たとえば、トラステッド プラットフォーム モジュール (TPM) やスタートアップ PIN の要件を使用できます。

    *[はい]* に設定すると、次の設定を構成できます。

    - **[互換性のある TPM スタートアップ]**  
      CSP:[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      BitLocker では TPM を必須にすることをお勧めします。 この設定は、初めて BitLocker を有効にする場合にのみ適用されます。BitLocker が既に有効になっている場合は無効になります。

      - **[ブロック]** ("*既定値*") - BitLocker では TPM が使用されません。
      - **[必須]** - TPM が存在し、利用可能な場合にのみ BitLocker が有効になります。
      - **[許可]** - TPM が存在する場合は BitLocker で使用されます。

    - **[互換性のある TPM スタートアップ PIN]**  
      CSP:[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **[ブロック]** ("*既定値*") - PIN の使用をブロックします。
      - **[必須]** - BitLocker を有効にするには、PIN と TPM が必要です。
      - **[許可]** - BitLocker は、TPM を使用して (存在する場合)、ユーザーによるスタートアップ PIN の構成を許可します。

      サイレント有効化シナリオでは、これを *[ブロック]* に設定する必要があります。 ユーザーによる操作が必要な場合、サイレント有効化シナリオ (オートパイロットを含む) は成功しません。

    - **[互換性のある TPM スタートアップ キー]**  
      CSP:[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **[ブロック]** ("*既定値*") - スタートアップ キーの使用をブロックします。
      - **[必須]** - BitLocker を有効にするには、スタートアップ キーと TPM が必要です。
      - **[許可]** - BitLocker は、TPM を使用して (存在する場合)、ドライブのロックを解除するためのスタートアップ キー (USB ドライブなど) を許可します。

      サイレント有効化シナリオでは、これを *[ブロック]* に設定する必要があります。 ユーザーによる操作が必要な場合、サイレント有効化シナリオ (オートパイロットを含む) は成功しません。

    - **[互換性のある TPM スタートアップ キーと PIN]**  
      CSP:[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **[ブロック]** ("*既定値*") - スタートアップ キーと PIN の組み合わせの使用をブロックします。
      - **[必須]** - BitLocker が有効になるには、スタートアップ キーと PIN が必要です。
      - **[許可]** - BitLocker は、TPM を使用して (存在する場合)、スタートアップ キーと PIN の組み合わせを許可します。

      サイレント有効化シナリオでは、これを *[ブロック]* に設定する必要があります。 ユーザーによる操作が必要な場合、サイレント有効化シナリオ (オートパイロットを含む) は成功しません。

    - **[TPM に互換性がないデバイスで BitLocker を無効にする]**  
    CSP:[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      TPM が存在しない場合、BitLocker では、スタートアップ用にパスワードまたは USB ドライブが必要になります。

      この設定は、初めて BitLocker を有効にする場合にのみ適用されます。BitLocker が既に有効になっている場合は無効になります。

      - **[未構成]** ("*既定値*")
      - **[はい]** - 互換性のある TPM チップなしで BitLocker を構成することができなくなります。

    - **[Enable preboot recovery message and url]\(プリブート回復メッセージと URL を有効にする\)**  
      CSP:[SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configure

      - **[未構成]** ("*既定値*") – 既定の BitLocker プリブート回復情報を使用します。
      - **[はい]** – ユーザーが回復パスワードの検索方法を理解できるように、カスタムのプリブート回復メッセージと URL の構成を有効にします。 プリブート メッセージと URL は、ユーザーが回復モードで PC からロックアウトされたときに表示されます。

      *[はい]* に設定すると、次の設定を構成できます。

      - **[プリブート回復メッセージ]**  
        カスタムのプリブート回復メッセージを指定します。

      - **[プリブート回復 URL]**  
        カスタムのプリブート回復 URL を指定します。

    - **[System drive recovery]\(システム ドライブの回復\)**  
      CSP:[SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **[未構成]** ("*既定値*")  
      - **[構成]** - 追加設定の構成を有効にします。

      *[構成]* に設定した場合は、次の設定を使用できます。

      - **[ユーザーによる回復キーの作成]**  
        - **[ブロック]** ("*既定値*")
        - **必須**
        - **許可されます。**

      - **[Configure BitLocker recovery package]\(BitLocker 回復パッケージの構成\)**
        - **[パスワードとキー]** ("*既定値*") - 管理者とユーザーが保護されたドライブのロックを解除する際に使用する BitLocker 回復パスワードと、管理者が Active Directory で (データ回復の目的で) 使用する回復キー パッケージの両方を指定します。
        - **[パスワードのみ]** - 回復キー パッケージは、必要なときにアクセスできない場合があります。

      - **[Require device to back up recovery information to Azure Ad]\(デバイスが回復情報を Azure AD にバックアップすることを必須とする\)**
        - **[未構成]** ("*既定値*") - Azure AD への回復キーのバックアップが失敗した場合でも BitLocker の有効化が完了します。 これにより、回復情報が外部に保存されなくなる可能性があります。
        - **[はい]** - 回復キーが Azure Active Directory に正常に保存されるまで、BitLocker は有効化を完了しません。

      - **[ユーザーによる回復パスワードの作成]**  
        - **[ブロック]** ("*既定値*")
        - **必須**
        - **許可されます。**

      - **[Hide recovery options during BitLocker setup]\(BitLocker のセットアップ時に回復オプションを非表示にする\)**
        - **[未構成]** ("*既定値*") - ユーザーがその他の回復オプションにアクセスできるようにします。
        - **[はい]** - BitLocker セットアップ ウィザードで、エンド ユーザーがその他の回復オプション (回復キーの印刷など) を選択できないようにします。

      - **[回復情報を保存した後、BitLocker を有効にします]**
        - **[未構成]** ("*既定値*")  
        - **あり**

      - **[Block the use of certificate-based data recovery agent (DRA)]\(証明書ベースのデータ回復エージェント (DRA)の使用をブロックする\)**
        - **[未構成]** ("*既定値*") - DRA の使用を設定できます。 DRA を設定するには、エンタープライズ PKI とグループ ポリシー オブジェクトで DRA のエージェントと証明書を展開する必要があります。
        - **[はい]** - BitLocker が有効なドライブをデータ回復エージェント (DRA) を使用して回復する機能をブロックします。

    - **PIN の長さの最小値**  
      CSP:[SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      BitLocker の有効化の際に TPM と PIN が必要になるときの、スタートアップ PIN の最小長を指定します。 この PIN の長さは 4 から 20 桁にする必要があります。

      この設定を構成しない場合、ユーザーは任意の長さ (4 桁から 20 桁) のスタートアップ PIN を構成できます。

      この設定は、初めて BitLocker を有効にする場合にのみ適用されます。BitLocker が既に有効になっている場合は無効になります。

  - **[Configure encryption method for Operating System drives]\(オペレーティング システム ドライブの暗号化方法の構成\)**  
   CSP:[EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    OS ドライブの暗号化方法と暗号強度を構成します。 *XTS - AES 128 ビット* は Windows の既定の暗号化方法であり、推奨される値です。

    - **[未構成]** ("*既定値*")
    - **AES 128 ビット CBC**
    - **AES 256 ビット CBC**
    - **AES 128 ビット XTS**
    - **AES 256 ビット XTS**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker - リムーバブル ドライブの設定

- **[Configure encryption method for Operating System drives]\(オペレーティング システム ドライブの暗号化方法の構成\)**  
  CSP:[BitLocker グループ ポリシー設定](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **[未構成]** ("*既定値*")  
  - **ステータス メッセージを**

  *[構成]* に設定すると、次の設定を構成できます。

  - **[Configure encryption method for removable data-drives]\(リムーバブル データドライブの暗号化方法の構成\)**  
    CSP:[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    リムーバブル データドライブのディスクに必要な暗号化方法を選択します。

    - **[未構成]** ("*既定値*")
    - **AES 128 ビット CBC**
    - **AES 256 ビット CBC**
    - **AES 128 ビット XTS**
    - **AES 256 ビット XTS**

  - **[Block write access to removable data-drives not protected by BitLocker]\(BitLocker で保護されていないリムーバブル データドライブへの書き込みアクセスをブロックする\)**  
    CSP:[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **未構成** (*既定値*) - 暗号化されていないリムーバブル ドライブにデータを書き込むことができます。
    - **[はい]** - Windows では、BitLocker で保護されていないリムーバブル ドライブにデータを書き込むことはできません。 挿入されたリムーバブル ドライブが暗号化されていない場合、ユーザーは、ドライブへの書き込みアクセスが許可される前に、BitLocker セットアップ ウィザードを完了する必要があります。

    - **[Block write access to removable data-drives not protected by BitLocker]\(BitLocker で保護されていないリムーバブル データドライブへの書き込みアクセスをブロックする\)**  
      CSP:[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **[未構成]** ("*既定値*") - BitLocker で暗号化されたどのドライブも使用できます。
      - **[はい]** - 組織が所有するコンピューターで暗号化されていない限り、リムーバブル ドライブへのアクセスをブロックします。

## <a name="next-steps"></a>次のステップ

[ディスク暗号化のエンドポイント セキュリティ ポリシー](../protect/endpoint-security-disk-encryption-policy.md)
