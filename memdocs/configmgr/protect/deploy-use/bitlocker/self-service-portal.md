---
title: BitLocker セルフサービス ポータル
titleSuffix: Configuration Manager
description: BitLocker の回復のために Configuration Manager でユーザー セルフサービス ポータルを使用する方法
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ad1f79bb439e0a426229680960092a5f0d8fb3c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129241"
---
# <a name="bitlocker-self-service-portal"></a>BitLocker セルフサービス ポータル

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

[BitLocker セルフサービス ポータルをインストール](setup-websites.md)すると、ユーザーのデバイスが BitLocker によってロックされた場合に、ユーザーは単独でコンピューターにアクセスできるようになります。 ヘルプ デスクのスタッフによる支援は不要です。

[![既定の BitLocker セルフサービスポータルの スクリーンショット](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> セルフサービス ポータルから回復キーを取得するには、ユーザーが少なくとも 1 回はコンピューターに正常にサインインしている必要があります。 このサインインは、リモート セッションではなく、デバイスに対してローカルである必要があります。 それ以外の場合は、ヘルプ デスクに連絡してキーを回復する必要があります。 ヘルプ デスクの管理者は、[administration and monitoring web サイト](helpdesk-portal.md)を使用して、回復キーを要求できます。

BitLocker は、次の状況でデバイスをロックすることがあります。

- ユーザーが BitLocker のパスワードまたは PIN を忘れた場合

- デバイスの OS ファイル、BIOS、またはトラステッド プラットフォーム モジュール (TPM) が変更されている場合

セルフサービス ポータルから BitLocker 回復キーを要求するには、次のようにします。

1. BitLocker によってデバイスがロックされると、起動時に BitLocker の回復画面が表示されます。 32 桁の BitLocker 回復キー ID を書き留めます。

1. 別のコンピューターで、web ブラウザーを使用してセルフサービス ポータル (`https://webserver.contoso.com/SelfService` など) にアクセスします。

1. 通知を読み、同意します。

1. **[回復キー ID]** フィールドに、BitLocker 回復キー ID の最初の 8 桁を入力します。 複数のキーが一致する場合は、32 桁すべてを入力します。

1. この要求の **[理由]** に対して、次のいずれかのオプションを選択します。

    - [BIOS/TPM changed] (BIOS/TPM の変更)
    - [OS filed modified] (OS ファイルの変更)
    - [Lost PIN/passphrase] (PIN/パスフレーズの紛失)

1. **[キーの取得]** を選択します。 セルフサービス ポータルに、48 桁の **BitLocker 回復キー**が表示されます。

1. この 48 桁のコードを、お使いのコンピューターの BitLocker 回復画面に入力してください。

> [!NOTE]
> BitLocker セルフサービス ポータルは、非アクティブな状態が一定期間続くとタイムアウトすることがあります。 たとえば、5 分後に、60 秒のカウンターでタイムアウト警告が表示される場合があります。
>
> ![BitLocker セルフサービス ポータルのタイムアウト警告](media/bitlocker-self-service-portal-timeout-warning.png)
>
> カウントダウンに応答しない場合、セッションは期限切れになります。
>
> ![BitLocker セルフサービス ポータルのセッション期限切れページ](media/bitlocker-self-service-portal-session-expired.png)
