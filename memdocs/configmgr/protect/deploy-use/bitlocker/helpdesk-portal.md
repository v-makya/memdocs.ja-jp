---
title: BitLocker administration and monitoring web サイト
titleSuffix: Configuration Manager
description: Configuration Manager で BitLocker 管理と監視の Web サイト (ヘルプデスク ポータル) を使用する方法
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84725ac494e1d9497524303b841207bd05cd3859
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699840"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>BitLocker administration and monitoring web サイト

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

BitLocker 管理と監視の Web サイトは、BitLocker ドライブ暗号化の管理インターフェイスです。 これは、ヘルプ デスク ポータルとも呼ばれます。 この Web サイトを使用して、レポートの確認、ユーザーのドライブの回復、およびデバイス TPM の管理を行います。

[![既定の BitLocker administration and monitoring web サイトの スクリーンショット](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

このコンポーネントを使用するには、Web サーバーにこのコンポーネントをインストールしておく必要があります。 詳細については、「[BitLocker のレポートとポータルのセットアップ](setup-websites.md)」を参照してください。

管理と監視の Web サイトに、次の URL からアクセスします。`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> **回復の監査レポート**は Administration and Monitoring Web サイトで確認できます。 他の BitLocker 管理レポートをレポート サービス ポイントに追加します。 詳細については、「[BitLocker レポートの表示](view-reports.md)」を参照してください。

## <a name="groups"></a>[グループ]

管理と監視の Web サイトの特定の領域にアクセスするには、ユーザー アカウントが次のいずれかのグループに含まれている必要があります。 任意の名前を使用して、Active Directory にこれらのグループを作成します。 この Web サイトをインストールするときに、これらのグループ名を指定します。 詳細については、「[BitLocker のレポートとポータルのセットアップ](setup-websites.md)」を参照してください。

|Group|[説明]|
|--- |--- |
|BitLocker ヘルプ デスク管理者|Administration and Monitoring web サイトのすべての領域にアクセスできます。 ユーザーがドライブを回復できるようにするには、ドメインとユーザー名ではなく、回復キーのみを入力します。 ユーザーがこのグループと BitLocker ヘルプ デスク ユーザー グループの両方のメンバーである場合、管理者グループのアクセス許可は、ユーザー グループのアクセス許可よりも優先されます。|
|BitLocker ヘルプ デスク ユーザー|Administration and Monitoring web サイトの **TPM 管理**領域と**ドライブ回復**領域へのアクセス権付与を行います。 これらのいずれかの領域を使用する場合、ユーザーのドメイン名とアカウント名など、すべてのフィールドに入力する必要があります。 ユーザーがこのグループと BitLocker ヘルプデスク管理者グループの両方のメンバーである場合、管理者グループのアクセス許可は、ユーザー グループのアクセス許可よりも優先されます。|
|BitLocker レポート ユーザー|Administration and Monitoring web サイトの**レポート**領域に対するアクセス権付与を行います。|

## <a name="manage-tpm"></a>TPM の管理

ユーザーが正しくない PIN を何回も入力すると、TPM がロックアウトされる可能性があります。 TPM がロックされるまでにユーザーが正しくない PIN を入力できる回数は、製造元によって異なります。 管理と監視の Web サイトの **[TPM の管理]** 領域から、集中管理されているキー回復データ システムにアクセスします。

TPM 所有権の詳細については、「[MBAM を構成して TPM をエスクローし、所有者の認証パスワードを保存する](https://docs.microsoft.com/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm)」を参照してください。

> [!NOTE]
> Windows 10 バージョン 1607 以降では、TPM のプロビジョニング時に Windows は TPM 所有者パスワードを保持しません。

1. Web ブラウザーで管理と監視の Web サイト (`https://webserver.contoso.com/HelpDesk` など) にアクセスします。

1. 左ペインで、 **[TPM の管理]** 領域を選択します。

    ![BitLocker 管理と監視の Web サイトの [TPM の管理] ページ](media/bitlocker-admin-manage-tpm.png)

1. コンピューターの完全修飾ドメイン名とコンピューター名を入力します。

1. 必要に応じて、エンド ユーザーのドメインとユーザー名を入力して、TPM 所有者パスワード ファイルを取得します。

1. **[TPM 所有者パスワード ファイルが必要な理由]** に対して、次のいずれかのオプションを選択します。

    - PIN のロックアウトをリセットするため
    - TPM をオンにするため
    - TPM をオフにするため
    - TPM パスワードを変更するため
    - TPM をクリアするため
    - その他

    フォームを **[送信]** すると、Web サイトは次のいずれかの応答を返します。

    - 一致する TPM 所有者パスワード ファイルが見つからない場合は、エラー メッセージが返されます。

    - 送信されたコンピューターの TPM 所有者パスワード

    TPM 所有者パスワード ファイルを取得すると、所有者パスワードが Web サイトに表示されます。

1. パスワードをファイルに保存するには、 **[保存]** を選択します。

1. **[TPM の管理]** 領域で、 **[TPM ロックアウトのリセット]** オプションを選択し、TPM 所有者パスワード ファイルを指定します。

    TPM ロックアウトがリセットされます。 BitLocker は、デバイスへのユーザーのアクセスを復元します。

    > [!IMPORTANT]
    > TPM ハッシュ値または TPM 所有者パスワード ファイルを共有しないでください。

## <a name="drive-recovery"></a>ドライブの回復

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a> 回復モードでドライブを回復する

ドライブは、次のシナリオで回復モードに移行します。

- ユーザーが PIN またはパスワードを紛失したり、忘れたりした場合
- トラステッド プラットフォーム モジュール (TPM) がコンピューターの BIOS またはスタートアップ ファイルの変更を検出した場合

回復パスワードを取得するには、Administration and Monitoring web サイトの **[ドライブの回復]** 領域を使用します。

> [!IMPORTANT]
> 回復パスワードは 1 回限りの使い捨てです。 OS ドライブと固定データ ドライブでは、使い捨てのルールは自動的に適用されます。 リムーバブル ドライブでは、ドライブを取り外して再挿入するときに適用されます。

1. Web ブラウザーで管理と監視の Web サイト (`https://webserver.contoso.com/HelpDesk` など) にアクセスします。

1. 左ペインで、 **[ドライブの回復]** 領域を選択します。

    ![BitLocker 管理と監視の Web サイトの [ドライバーの回復] ページ](media/bitlocker-admin-drive-recovery.png)

1. 必要に応じて、ユーザーのドメインとユーザー名を入力して、回復情報を表示します。

1. 一致する可能性のある回復キーの一覧を表示するには、回復キー ID の最初の 8 桁を入力します。 正確な回復キーを取得するには、回復キー ID 全体を入力します。

1. **[ドライブのロックを解除する理由]** に対して、次のいずれかのオプションを選択します。

    - オペレーティング システムのブート順が変わったため
    - BIOS が変わったため
    - オペレーティング システム ファイルが変わったため
    - 起動キーを紛失したため
    - PIN を忘れたため
    - TPM をリセットしたため
    - パスフレーズを忘れたため
    - スマートカードを紛失したため
    - その他

    フォームを **[送信]** すると、Web サイトは次のいずれかの応答を返します。

    - ユーザーが複数の一致する回復パスワードを持っていれば、複数の一致候補が返されます。

    - 提出したユーザーの回復パスワードと回復パッケージ。

        > [!NOTE]
        > 破損したドライブを回復する場合は、回復パッケージのオプションにより、BitLocker にドライブの回復に必要な重要情報が提供されます。

    - 一致する回復パスワードが見つからない場合は、エラー メッセージが返されます。

    回復パスワードと回復パッケージを取得すると、Web サイトに回復パスワードが表示されます。

1. パスワードをコピーするには、 **[キーのコピー]** を選択します。 回復パスワードをファイルに保存するには、 **[保存]** を選択します。

ドライブのロックを解除するには、回復パスワードを入力するか、回復パッケージを使用します。

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a> 移動したドライブを回復する

ドライブを新しいコンピューターに移動すると、TPM が異なるために BitLocker は前の PIN を受け入れません。 移動したドライブを回復するには、回復キー ID を入手して回復パスワードを取得します。

移動したドライブを回復するには、Administration and Monitoring web サイトの **[ドライブの回復]** 領域を使用します。

1. 移動したドライブがあるコンピューターで、Windows 回復環境 (WinRE) モードでコンピューターを起動します。

1. WinRE では、BitLocker は移動した OS ドライブを固定データ ドライブとして扱います。 BitLocker にドライブの回復パスワード ID が表示され、回復パスワードの入力が求められます。

    > [!NOTE]
    > 場合によっては、スタートアップ プロセス中に、オプションが使用できる場合は **[PIN を忘れた場合]** を選択します。 次に、回復モードに入って回復キー ID を表示します。

1. 回復キー ID を使用して、管理と監視の Web サイトから回復パスワードを取得します。 詳細については、「[回復モードでドライブを回復する](#bkmk_recovery)」を参照してください。

移動したドライブが元のコンピューターで TPM チップを使用するように構成されている場合は、次の手順を行います。 それ以外の場合、回復プロセスはこれで終了です。

1. ドライブのロックを解除したら、WinRE モードでコンピューターを起動します。 WinRE でコマンド プロンプトを開き、`manage-bde` コマンドを使用してドライブの暗号化を解除します。 このツールは、元の TPM チップがない状態で **TPM と PIN** 保護機能を削除する唯一の手段です。 このコマンドの詳細については、「[Manage-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde)」を参照してください。

1. 完了したら、通常どおりにコンピューターを起動します。 Configuration Manager によって、新しいコンピューターの TPM と PIN を使用してドライブを暗号化する BitLocker ポリシーが適用されます。

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a> 破損したドライブを回復する

回復キー ID を使用して、管理と監視の Web サイトから回復キー パッケージを取得します。 詳細については、「[回復モードでドライブを回復する](#bkmk_recovery)」を参照してください。

1. **回復キー パッケージ**をコンピューターに保存し、破損したドライブのあるコンピューターにコピーします。

1. 管理者としてコマンド プロンプトを開き、次のコマンドを入力します。

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    次の値を置き換えます。

    - `<corrupted drive>`: 破損したドライブのドライブ文字。たとえば、`D:`
    - `<fixed drive>`: 破損したドライブとサイズが同じかそれ以上の、使用可能なハード ディスク ドライブのドライブ文字。 BitLocker は破損したドライブ上のデータを回復し、指定されたドライブに移動します。 このドライブのすべてのデータが上書きされます。
    - `<key package>`: 回復キー パッケージの場所
    - `<recovery password>`: 関連付けられている回復パスワード

    次に例を示します。

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

このコマンドの詳細については、「[Repair-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde)」を参照してください。

## <a name="reports"></a>レポート

管理と監視の Web サイトには、**回復の監査レポート**が含まれています。 その他のレポートは、Configuration Manager レポート サービス ポイントから入手できます。 詳細については、「[BitLocker レポートの表示](view-reports.md)」を参照してください。

1. Web ブラウザーで管理と監視の Web サイト (`https://webserver.contoso.com/HelpDesk` など) にアクセスします。

1. 左ペインで、 **[レポート]** 領域を選択します。

1. 上部のメニュー バーから、[**回復の監査レポート]** を選択します。

このレポートの詳細については、「[回復の監査レポート](view-reports.md#bkmk-audit)」を参照してください。

> [!TIP]
> レポートの結果を保存するには、 **[レポート]** メニュー バーで **[エクスポート]** を選択します。
