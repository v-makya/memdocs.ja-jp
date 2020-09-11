---
title: BitLocker 設定のリファレンス
titleSuffix: Configuration Manager
description: Configuration Manager で使用できるすべての BitLocker 管理設定
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82b122f96806b6e3f77afccf8b8d4195c294b224
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608023"
---
# <a name="bitlocker-settings-reference"></a>BitLocker 設定のリファレンス

*適用対象:Configuration Manager (Current Branch)*

<!-- 5925683 -->

Configuration Manager の BitLocker 管理ポリシーには、次のポリシー グループが含まれます。

- セットアップ
- オペレーティング システム ドライブ
- 固定ドライブ
- リムーバブル ドライブ
- クライアント管理

以下のセクションでは、各グループの設定について説明し、推奨構成を示します。

> [!NOTE]
> これらの設定は Configuration Manager バージョン2002 に基づいています。 バージョン 1910 には、これらの設定のすべてが含まれているわけではありません。

## <a name="setup"></a>セットアップ

このページの設定により、グローバルな BitLocker 暗号化オプションが構成されます。

### <a name="drive-encryption-method-and-cipher-strength"></a>Drive encryption method and cipher strength (ドライブの暗号化方法と暗号強度)

*推奨構成*:既定以上の暗号化方法を使用して**有効**にします。

> [!NOTE]
> **[セットアップ]** プロパティ ページには、Windows の異なるバージョンに対応する 2 つの設定グループが含まれます。 このセクションでは、両方について説明します。

#### <a name="windows-81-devices"></a>Windows 8.1 デバイス

Windows 8.1 デバイスの場合、 **[Drive encryption method and cipher strength]\(ドライブの暗号化方法と暗号強度\)** のオプションを有効にし、次のいずれかの暗号化方法を選択します。

- ディフューザー付き AES 128 ビット
- ディフューザーを使用した AES 256 ビット
- AES 128 ビット (既定)
- AES 256 ビット

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMBLEncryptionMethodPolicy](/powershell/module/configurationmanager/new-cmblencryptionmethodpolicy)」をご覧ください。

#### <a name="windows-10-devices"></a>Windows 10 デバイス

Windows 10 デバイスの場合、 **[Drive encryption method and cipher strength (Windows 10)]\(ドライブの暗号化方法と暗号強度 (Windows 10)\)** のオプションを有効にします。 次に、OS ドライブ、固定データ ドライブ、およびリムーバブル データ ドライブについて、次のいずれかの暗号化方法を個別に選択します。

- AES-CBC 128 ビット
- AES-CBC 256 ビット
- XTS-AES 128 ビット (既定)
- XTS-AES 256 ビット

> [!TIP]
> BitLocker には、高度暗号化標準 (AES) が暗号化アルゴリズムとして使われており、キーの長さを設定することができます (128 ビットまたは 256 ビット)。 Windows 10 デバイスでは、AES 暗号化によって暗号化ブロック チェーン (CBC) または Ciphertext Stealing (XTS) がサポートされます。
>
> Windows 10 を実行していないデバイスでリムーバブル ドライブを使用する必要がある場合は、AES-CBC を使用します。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMBLEncryptionMethodWithXts](/powershell/module/configurationmanager/new-cmblencryptionmethodwithxts)」をご覧ください。

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>ドライブの暗号化と暗号強度に関する使用上の一般的な注意事項

- これらの設定を無効にした場合、または構成しなかった場合、BitLocker では既定の暗号化方法が使用されます。

- BitLocker を有効にすると、Configuration Manager によってこれらの設定が適用されます。

- ドライブが既に暗号化されている場合、または暗号化が進行中の場合は、これらのポリシー設定を変更しても、デバイスでのドライブ暗号化は変更されません。

- 既定値を使用する場合、BitLocker コンピューターの準拠レポートに、暗号強度が **[不明]** として表示されることがあります。 この問題に対処するには、この設定を有効にして、暗号強度の明示的な値を設定します。

### <a name="prevent-memory-overwrite-on-restart"></a>再起動時にメモリを上書きしない

*推奨構成*:**未構成**

再起動の際に、メモリ上の BitLocker の機密情報を上書きせずに再起動のパフォーマンスを向上させるために、このポリシーを構成します。

このポリシーを構成しない場合、BitLocker は、コンピューターの再起動時にメモリからシークレットを削除します。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMNoOverwritePolicy](/powershell/module/configurationmanager/new-cmnooverwritepolicy)」をご覧ください。

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>スマート カード証明書の使用規則の準拠を検証する

*推奨構成*:**未構成**

スマートカード証明書ベースの BitLocker の保護を使用するために、このポリシーを構成します。 次に、証明書の**オブジェクト識別子**を指定します。

このポリシーを構成しない場合、BitLocker は、既定のオブジェクト識別子 `1.3.6.1.4.1.311.67.1.1` を使用して証明書を指定します。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMScCompliancePolicy](/powershell/module/configurationmanager/new-cmsccompliancepolicy)」をご覧ください。

### <a name="organization-unique-identifiers"></a>組織の一意識別子

*推奨構成*:**未構成**

証明書ベースのデータ回復エージェント、または BitLocker To Go リーダーを使用するために、このポリシーを構成します。

このポリシーを構成しない場合、BitLocker は **[Identification]\(識別\)** フィールドを使用しません。

組織でより高度なセキュリティ対策が必要な場合は、 **[Identification]\(識別\)** フィールドを構成してください。 対象となるすべての USB デバイスでこのフィールドを設定し、この設定に適合させます。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMUidPolicy](/powershell/module/configurationmanager/new-cmuidpolicy)」をご覧ください。

## <a name="os-drive"></a>OS ドライブ

このページの設定では、Windows がインストールされているドライブの暗号化設定を構成します。

### <a name="operating-system-drive-encryption-settings"></a>オペレーティング システム ドライブの暗号化設定

*推奨構成*:**Enabled**

この設定を有効にした場合、ユーザーは OS ドライブを保護する必要があり、ドライブは BitLocker によって暗号化されます。 無効にした場合、ユーザーはドライブを保護できません。 このポリシーを構成しない場合、OS ドライブで BitLocker 保護は必要ありません。

> [!NOTE]
> ドライブが既に暗号化されいるときにこの設定を無効にした場合は、BitLocker はドライブの暗号化を解除します。  

お使いのデバイスに[トラステッド プラットフォーム モジュール (TPM)](/windows/security/information-protection/tpm/trusted-platform-module-top-node) がない場合は、 **[互換性のある TPM が装備されていない BitLocker を許可する (パスワードが必要)]** オプションを使用します。 この設定により、デバイスに TPM がない場合でも、BitLocker で OS ドライブを暗号化できます。 このオプションを有効にした場合、Windows で、BitLocker パスワードを指定するよう求めるプロンプトがユーザーに出されます。

互換性のある TPM を装備したデバイスでは、暗号化されたデータの保護を強化するためにスタートアップ時に 2 種類の認証方法を使用できます。 コンピューターの起動時に、認証に TPM のみを使用することも、個人識別番号 (PIN) の入力を要求することもできます。 次の設定を構成します。

- **Select protector for operating system drive (オペレーティング システム ドライブのプロテクターを選択)** :TPM と PIN、または TPM のみが使用されるように構成します。

- **スタートアップに対する PIN の長さの最小値を構成する**:PIN が必要なとき、ユーザーはこの長さ以上の値を指定する必要があります。 ユーザーはこの PIN を、コンピューターが起動されドライブのロックを解除するときに入力します。 既定では、PIN の長さの最小値は `4` です。

> [!TIP]
> セキュリティを強化するために、TPM + PIN 保護でデバイスを有効にする場合、 **[システム]**  >  **[電源管理]**  >  **[スリープの設定]** で次のグループ ポリシー設定を*無効にすること*を検討してください。
>
> - スリープ時にスタンバイ状態 (S1-S3) を許可する (電源接続時)
>
> - スリープ時にスタンバイ状態 (S1-S3) を許可する (バッテリ使用時)

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMBMSOSDEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsosdencryptionpolicy)」をご覧ください。

### <a name="allow-enhanced-pins-for-startup"></a>拡張スタートアップ PIN を許可する

*推奨構成*:**未構成**

拡張スタートアップ PIN を使用するように BitLocker を構成します。 これらの PIN では、大文字、小文字、記号、数字、空白などの追加文字を使用できます。 この設定は、BitLocker を有効にすると適用されます。

> [!IMPORTANT]
> 一部のコンピューターは、プリブート環境で拡張 PIN をサポートしていません。 この使用を有効にする前に、ご使用のデバイスがこの機能と互換性があるかどうかを評価してください。

この設定を有効にすると、すべての新しい BitLocker スタートアップ PIN で、ユーザーが拡張 PIN を作成できるようになります。

- **PIN を ASCII に限定する**:拡張 PIN と、プリブート環境で入力できる文字の種類または文字数に制約があるコンピューターとの間の互換性を高めることができます。

このポリシー設定を無効にした場合、または構成しない場合、BitLocker は拡張 PIN を使用しません。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMEnhancedPIN](/powershell/module/configurationmanager/new-cmenhancedpin)」をご覧ください。

### <a name="operating-system-drive-password-policy"></a>オペレーティング システム ドライブのパスワード ポリシー

*推奨構成*:**未構成**

これらの設定を使用して、BitLocker で保護されている OS ドライブのロックを解除するためのパスワードの制約を設定します。 OS ドライブで TPM 以外の保護を許可する場合は、次の設定を構成します。

- **オペレーティング システム ドライブのパスワードの複雑さを構成する**:パスワードに複雑さの条件を適用するには、 **[パスワードの複雑さの条件を満たす必要がある]** を選択します。

- **オペレーティング システム ドライブの最小パスワード長**:既定では、長さの最小値は `8` です。

- **リムーバブル OS ドライブに対して ASCII のみのパスワードを要求する**

このポリシー設定を有効にすると、ユーザーは管理者が定義した要件を満たすパスワードを構成できます。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMOSPassphrase](/powershell/module/configurationmanager/new-cmospassphrase)」をご覧ください。

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>OS ドライブのパスワード ポリシーに関する使用上の一般的な注意事項

- これらの複雑さの条件に関する設定を有効にするには、 **[コンピューターの構成]**  >  **[Windows の設定]**  >  **[セキュリティの設定]**  >  **[アカウント ポリシー]**  >  **[パスワード ポリシー]** で、グループ ポリシー設定の **[パスワードが複雑さの条件を満たす必要がある]** も有効にします。

- これらの設定は、ボリュームのロックを解除するときではなく、BitLocker を有効にするときに適用されます。 BitLocker は、ユーザーがドライブで利用できるいずれかの保護機能を使用してドライブのロックを解除できます。

- グループ ポリシーを使用して、暗号化、ハッシュ、および署名のために FIPS 準拠のアルゴリズムを有効にする場合、BitLocker 保護機能としてパスワードを許可することはできません。

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>BitLocker 回復の実行後にプラットフォームの検証データをリセットする

*推奨構成*:**未構成**

BitLocker の回復後、Windows が起動したときにプラットフォームの検証データを更新するかどうかを制御します。

この設定を有効にした場合、または構成しなかった場合、Windows によって、この状況でプラットフォームの検証データが更新されます。

このポリシー設定を無効にした場合、Windows によって、この状況でプラットフォームの検証データは更新されません。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMTpmAutoResealPolicy](/powershell/module/configurationmanager/new-cmtpmautoresealpolicy)」をご覧ください。

### <a name="pre-boot-recovery-message-and-url"></a>[プリブート回復メッセージと URL]

*推奨構成*:**未構成**

BitLocker で OS ドライブがロックされているときに、この設定を使用して、プリブート BitLocker 回復画面にカスタムの回復メッセージまたは URL を表示します。 この設定は、Windows 10 デバイスにのみ適用されます。

この設定を有効にした場合は、プリブート回復メッセージについて次のいずれかのオプションを選択します。

- **既定の回復メッセージと URL を使用する**:プリブート BitLocker 回復画面に、既定の BitLocker 回復メッセージと URL を表示します。 カスタムの回復メッセージまたは URL を以前に構成している場合、このオプションを使用して、既定のメッセージに戻します。

- **カスタム回復メッセージを使用する**:プリブート BitLocker 回復画面にカスタム メッセージを含めます。

  - **カスタム回復メッセージ オプション**:表示するカスタム メッセージを入力します。 回復 URL も指定する場合は、このカスタム回復メッセージの一部として追加します。 文字列の最大長は 32,768 文字です。

- **カスタム回復 URL を使用する**:プリブート BitLocker 回復画面に表示される既定の URL を置き換えます。

  - **カスタム回復 URL オプション**:表示する URL を入力します。 文字列の最大長は 32,768 文字です。

> [!NOTE]
> プリブートでは、一部の文字および言語はサポートされていません。 最初に、カスタム メッセージまたは URL をテストして、それがプリブート BitLocker 回復画面に正しく表示されることを確認してください。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMPrebootRecoveryInfo](/powershell/module/configurationmanager/new-cmprebootrecoveryinfo)」をご覧ください。

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Encryption policy enforcement settings (OS drive) (暗号化ポリシーの強制設定 (OS ドライブ))

*推奨構成*:**Enabled**

ユーザーが OS ドライブの BitLocker 準拠を延期できる日数を構成します。 **非準拠の猶予期間**は、Configuration Manager がそれを非準拠として最初に検出したときに開始されます。 この猶予期間が終了すると、ユーザーは必要なアクションを延期することや、除外を要求することができなくなります。

暗号化プロセスでユーザーの入力が必要な場合には、必要な情報を入力するまでユーザーが閉じることができないダイアログ ボックスが Windows に表示されます。 エラーや状態に関する以後の通知には、この制限は適用されません。

保護を追加するためのユーザーの操作が BitLocker で必要ない場合、猶予期間が終了すると、BitLocker はバックグラウンドで暗号化を開始します。

この設定を無効にした場合、または構成しなかった場合は、Configuration Manager は、BitLocker ポリシーに準拠するようにユーザーに要求しません。

ポリシーをただちに適用するには、猶予期間として `0` を設定します。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMUseOsEnforcePolicy](/powershell/module/configurationmanager/new-cmuseosenforcepolicy)」をご覧ください。

## <a name="fixed-drive"></a>固定ドライブ

このページの設定により、デバイスの追加データ ドライブの暗号化が構成されます。

### <a name="fixed-data-drive-encryption"></a>固定データ ドライブの暗号化

*推奨構成*:**Enabled**

固定データ ドライブの暗号化の要件を管理します。 この設定を有効にすると、BitLocker は、すべての固定データ ドライブを保護の対象とするようにユーザーに要求します。 その後、それらのデータ ドライブが暗号化されます。

このポリシーを有効にする場合は、自動ロック解除を有効にするか、 **[固定データ ドライブのパスワード ポリシー]** の設定を有効にします。

- **Configure auto-unlock for fixed data drive (固定データ ドライブの自動ロック解除を構成する)** :暗号化されたデータ ドライブを BitLocker で自動的にロック解除することを許可または必須とします。 自動ロック解除を使用するには、BitLocker で [OS ドライブ](#os-drive)を暗号化する必要もあります。

この設定を構成しなかった場合、BitLocker は、固定データ ドライブを保護の対象とするようにユーザーに要求しません。

この設定を無効にした場合、ユーザーは固定データ ドライブを BitLocker で保護できなくなります。 BitLocker によって固定データ ドライブが暗号化された後にこのポリシーを無効にすると、BitLocker は固定データ ドライブの暗号化を解除します。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMBMSFDVEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsfdvencryptionpolicy)」をご覧ください。

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>BitLocker で保護されていない固定ドライブへの書き込みアクセスを拒否する

*推奨構成*:**未構成**

Windows でデバイス上の固定ドライブにデータを書き込む場合に BitLocker 保護が必要になります。 このポリシーは、BitLocker を有効にすると適用されます。

この設定を有効にする場合:

- BitLocker によって固定データ ドライブが保護されている場合、Windows はそれを読み取りおよび書き込みアクセスでマウントします。

- BitLocker で保護されていない固定データ ドライブについては、Windows はそれを読み取り専用としてマウントします。

この設定を構成しなかった場合、Windows はすべての固定データ ドライブを読み取りおよび書き込みアクセスでマウントします。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMFDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmfdvdenywriteaccesspolicy)」をご覧ください。

### <a name="fixed-data-drive-password-policy"></a>固定データ ドライブのパスワード ポリシー

*推奨構成*:**未構成**

これらの設定を使用して、BitLocker で保護されている固定データ ドライブのロックを解除するためのパスワードの制約を設定します。

この設定を有効にすると、ユーザーは管理者が定義した要件を満たすパスワードを構成できます。

セキュリティを強化するには、この設定を有効にしてから、次の設定を構成します。

- **固定データ ドライブに対してパスワードを要求する**:BitLocker で保護されている固定データ ドライブのロックを解除するには、ユーザーはパスワードを指定する必要があります。

- **固定データ ドライブのパスワードの複雑さを構成する:** :パスワードに複雑さの条件を適用するには、 **[パスワードの複雑さの条件を満たす必要がある]** を選択します。

- **固定データ ドライブの最小パスワード長**:既定では、長さの最小値は `8` です。

この設定を無効にした場合、ユーザーはパスワードを構成できません。

ポリシーが構成されていない場合、BitLocker では既定の設定でパスワードがサポートされます。 既定の設定には、パスワードの複雑さの要件は含まれず、必要とされるのは 8 文字のみです。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMFDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmfdvpassphrasepolicy)」をご覧ください。

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>固定データ ドライブのパスワード ポリシーに関する使用上の一般的な注意事項

- これらの複雑さの条件に関する設定を有効にするには、 **[コンピューターの構成]**  >  **[Windows の設定]**  >  **[セキュリティの設定]**  >  **[アカウント ポリシー]**  >  **[パスワード ポリシー]** で、グループ ポリシー設定の **[パスワードが複雑さの条件を満たす必要がある]** も有効にします。

- これらの設定は、ボリュームのロックを解除するときではなく、BitLocker を有効にするときに適用されます。 BitLocker は、ユーザーがドライブで利用できるいずれかの保護機能を使用してドライブのロックを解除できます。

- グループ ポリシーを使用して、暗号化、ハッシュ、および署名のために FIPS 準拠のアルゴリズムを有効にする場合、BitLocker 保護機能としてパスワードを許可することはできません。

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>暗号化ポリシー強制適用設定 (固定データ ドライブ)

*推奨構成*:**Enabled**

ユーザーが固定データ ドライブの BitLocker 準拠を延期できる日数を構成します。 **非準拠の猶予期間**は、Configuration Manager が固定データ ドライブを非準拠として最初に検出したときに開始されます。 OS ドライブが準拠するまで、固定データ ドライブ ポリシーは適用されません。 この猶予期間が終了すると、ユーザーは必要なアクションを延期することや、除外を要求することができなくなります。

暗号化プロセスでユーザーの入力が必要な場合には、必要な情報を入力するまでユーザーが閉じることができないダイアログ ボックスが Windows に表示されます。 エラーや状態に関する以後の通知には、この制限は適用されません。

保護を追加するためのユーザーの操作が BitLocker で必要ない場合、猶予期間が終了すると、BitLocker はバックグラウンドで暗号化を開始します。

この設定を無効にした場合、または構成しなかった場合は、Configuration Manager は、BitLocker ポリシーに準拠するようにユーザーに要求しません。

ポリシーをただちに適用するには、猶予期間として `0` を設定します。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMUseFddEnforcePolicy](/powershell/module/configurationmanager/new-cmusefddenforcepolicy)」をご覧ください。

## <a name="removable-drive"></a>リムーバブル ドライブ

このページの設定により、USB キーなどのリムーバブル ドライブの暗号化が構成されます。

### <a name="removable-data-drive-encryption"></a>リムーバブル データ ドライブの暗号化

*推奨構成*:**Enabled**

この設定では、リムーバブル ドライブでの BitLocker の使用を制御します。

- **リムーバブル データ ドライブに BitLocker 保護を適用できるようにする**:ユーザーは、リムーバブル ドライブの BitLocker 保護を有効にすることができます。

- **リムーバブル データ ドライブの BitLocker を中断および暗号化解除できるようにする**:ユーザーは、リムーバブル ドライブから BitLocker ドライブの暗号化を削除することや、一時的に中断することができます。

この設定を有効にし、ユーザーが BitLocker による保護を適用できるようにすると、Configuration Manager クライアントによって、リムーバブル ドライブに関する回復情報が管理ポイントの回復サービスに保存されます。 この動作により、ユーザーは保護機能 (パスワード) を忘れたり紛失したりしても、ドライブを回復できます。

この設定を有効にする場合:

- **[リムーバブル データ ドライブのパスワード ポリシー]** の設定を有効にします。

- ユーザーとコンピューターの両方の構成について、 **[システム]**  >  **[リムーバブル記憶域へのアクセス]** で次のグループ ポリシー設定を "*無効にします*"。

  - **すべてのリムーバブル記憶域クラス: すべてのアクセスを拒否**
  - **リムーバブル ディスク: 書き込みアクセス権の拒否**
  - **リムーバブル ディスク: 読み取りアクセス権の拒否**

この設定を無効にした場合、ユーザーはリムーバブル ドライブで BitLocker を使用できません。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMRDVConfigureBDEPolicy](/powershell/module/configurationmanager/new-cmrdvconfigurebdepolicy)」をご覧ください。

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>BitLocker で保護されていないリムーバブル ドライブへの書き込みアクセスを拒否する

*推奨構成*:**未構成**

Windows でデバイス上のリムーバブル ドライブにデータを書き込む場合に BitLocker 保護が必要になります。 このポリシーは、BitLocker を有効にすると適用されます。

この設定を有効にする場合:

- BitLocker によってリムーバブル ドライブが保護されている場合、Windows はそれを読み取りおよび書き込みアクセスでマウントします。

- BitLocker で保護されていないリムーバブル ドライブについては、Windows はそれを読み取り専用としてマウントします。

- **[別の組織で構成されたデバイスへの書き込みアクセスを拒否する]** オプションを有効にすると、BitLocker では、許可された ID フィールドと一致する ID フィールドがあるリムーバブル ドライブへの書き込みアクセス権のみ付与されます。 [[セットアップ]](#setup) ページで **[組織の一意識別子]** グローバル設定を使用して、これらのフィールドを定義します。

この設定を無効にした場合、または構成しなかった場合、Windows はすべてのリムーバブル ドライブを読み取りおよび書き込みアクセスでマウントします。

> [!NOTE]
> この設定は、 **[システム]**  >  **[リムーバブル記憶域へのアクセス]** のグループ ポリシー設定によって上書きできます。 グループ ポリシー設定の **[リムーバブル ディスク: 書き込みアクセス権の拒否]** を有効にすると、BitLocker はこの Configuration Manager 設定を無視します。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMRDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmrdvdenywriteaccesspolicy)」をご覧ください。

### <a name="removable-data-drive-password-policy"></a>リムーバブル データ ドライブのパスワード ポリシー

*推奨構成*:**Enabled**

これらの設定を使用して、BitLocker で保護されているリムーバブル ドライブのロックを解除するためのパスワードの制約を設定します。

この設定を有効にすると、ユーザーは管理者が定義した要件を満たすパスワードを構成できます。

セキュリティを強化するには、この設定を有効にしてから、次の設定を構成します。

- **リムーバブル データ ドライブに対してパスワードを要求する**:BitLocker で保護されているリムーバブル ドライブのロックを解除するには、ユーザーはパスワードを指定する必要があります。

- **リムーバブル データ ドライブのパスワードの複雑さを構成する**:パスワードに複雑さの条件を適用するには、 **[パスワードの複雑さの条件を満たす必要がある]** を選択します。

- **リムーバブル データ ドライブの最小パスワード長**:既定では、長さの最小値は `8` です。

この設定を無効にした場合、ユーザーはパスワードを構成できません。

ポリシーが構成されていない場合、BitLocker では既定の設定でパスワードがサポートされます。 既定の設定には、パスワードの複雑さの要件は含まれず、必要とされるのは 8 文字のみです。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMRDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmrdvpassphrasepolicy)」をご覧ください。

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>リムーバブル データ ドライブのパスワード ポリシーに関する使用上の一般的な注意事項

- これらの複雑さの条件に関する設定を有効にするには、 **[コンピューターの構成]**  >  **[Windows の設定]**  >  **[セキュリティの設定]**  >  **[アカウント ポリシー]**  >  **[パスワード ポリシー]** で、グループ ポリシー設定の **[パスワードが複雑さの条件を満たす必要がある]** も有効にします。

- これらの設定は、ボリュームのロックを解除するときではなく、BitLocker を有効にするときに適用されます。 BitLocker は、ユーザーがドライブで利用できるいずれかの保護機能を使用してドライブのロックを解除できます。

- グループ ポリシーを使用して、暗号化、ハッシュ、および署名のために FIPS 準拠のアルゴリズムを有効にする場合、BitLocker 保護機能としてパスワードを許可することはできません。

## <a name="client-management"></a>クライアント管理

このページの設定により、BitLocker 管理サービスとクライアントが構成されます。

### <a name="bitlocker-management-services"></a>BitLocker Management Services (BitLocker 管理サービス)

*推奨構成*:**Enabled**

この設定を有効にすると、Configuration Manager によってキーの回復情報がサイト データベースに自動的に通知なしでバックアップされます。 この設定を無効にした場合、または構成しなかった場合は、Configuration Manager によってキーの回復情報は保存されません。

- **格納する BitLocker 回復情報を選択する**:BitLocker 回復情報をバックアップするためのキー回復サービスを構成します。 これにより、BitLocker によって暗号化された回復データの管理方法が提供され、キー情報がないことによるデータの損失を防ぐことができます。

- **回復情報をプレーン テキストで保存することを許可する**:SQL Server 用の BitLocker 管理の暗号化証明書がない場合、Configuration Manager によってキーの回復情報がプレーン テキストで保存されます。 詳細については、「[回復データの暗号化](../../deploy-use/bitlocker/encrypt-recovery-data.md)」をご覧ください。

- **Client checking status frequency (minutes) (クライアントが状態を確認する頻度 (分単位))** :クライアントは、構成された頻度で、コンピューターの BitLocker 保護ポリシーと状態を確認し、クライアント回復キーのバックアップも行います。 既定では、Configuration Manager クライアントは、90 分ごとに BitLocker 回復情報を更新します。

Windows PowerShell を使用してこれらのポリシーを作成する方法の詳細については、次をご覧ください。

- [Set-CMBlmPlaintextStorage](/powershell/module/configurationmanager/set-cmblmplaintextstorage)
- [New-CMBMSClientConfigureCheckIntervalPolicy](/powershell/module/configurationmanager/new-cmbmsclientconfigurecheckintervalpolicy)

### <a name="user-exemption-policy"></a>ユーザーの除外ポリシー

*推奨構成*:**未構成**

ユーザーが BitLocker 暗号化からの除外を要求するための連絡方法を構成します。

このポリシー設定を有効にする場合、次の情報を指定します。

- **Maximum days to postpone (最大延期日数)** :適用されたポリシーをユーザーが延期できる日数。 既定では、この値は `7` 日 (1 週間) です。

- **連絡方法**:ユーザーが除外を要求できる方法を指定します:URL、電子メール アドレス、または電話番号。

- **連絡先**:URL、電子メール アドレス、または電話番号を指定します。 ユーザーが BitLocker 保護からの除外を要求すると、Windows のダイアログ ボックスが表示され、適用方法に関する手順が示されます。 Configuration Manager は、入力された情報を検証しません。

  - **[URL]** :標準の URL 形式である `https://website.domain.tld` を使用します。 Windows により、URL がハイパーリンクとして表示されます。

  - **電子メール アドレス**: 標準の電子メール アドレス形式である `user@domain.tld` を使用します。 Windows により、次のハイパーリンクとしてアドレスが表示されます: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection`。

  - **電話番号**:ユーザーが通話する電話番号を指定します。 Windows により、次の説明とともに番号が表示されます: `Please call <your number> for applying exemption`。

この設定を無効にした場合、または構成しなかった場合は、Windows により、ユーザーに対して除外要求の指示は表示されません。

> [!NOTE]
> BitLocker は、コンピューターごとではなく、ユーザーごとに除外を管理します。 複数のユーザーが同じコンピューターにサインインし、1 人でも除外されていないユーザーがいると、BitLocker によってそのコンピューターは暗号化されます。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMBMSUserExemptionPolicy](/powershell/module/configurationmanager/new-cmbmsuserexemptionpolicy)」をご覧ください。

### <a name="url-for-the-security-policy-link"></a>URL for the security policy link (セキュリティ ポリシーのリンクの URL)

*推奨構成*:**Enabled**

Windows で**会社のセキュリティ ポリシー**としてユーザーに表示する URL を指定します。 このリンクを使用して、暗号化の要件に関する情報をユーザーに提供します。 これは、BitLocker によって、ドライブを暗号化するよう求めるプロンプトがユーザーに出されたときに表示されます。

この設定を有効にした場合は、 **[security policy link URL]\(セキュリティ ポリシーのリンクの URL\)** を構成します。

この設定を無効にした場合、または構成しない場合、BitLocker でセキュリティ ポリシー リンクは表示されません。

Windows PowerShell を使用してこのポリシーを作成する方法の詳細については、「[New-CMMoreInfoUrlPolicy](/powershell/module/configurationmanager/new-cmmoreinfourlpolicy)」をご覧ください。

## <a name="next-steps"></a>次の手順

Windows PowerShell を使用してこれらのポリシー オブジェクトを作成する場合は、[New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting) コマンドレットを使用します。 このコマンドレットによって、指定したすべてのポリシーを含む BitLocker 管理ポリシー設定オブジェクトを作成できます。 ポリシー設定をコレクションに展開するには、[New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment) コマンドレットを使用します。
