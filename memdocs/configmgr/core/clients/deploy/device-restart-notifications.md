---
title: デバイスの再起動の通知
titleSuffix: Configuration Manager
description: Configuration Manager のさまざまなクライアント設定に対する再起動通知の動作。
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693960"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Configuration Manager でのデバイスの再起動通知

*適用対象:Configuration Manager (Current Branch)*

保留中のデバイス再起動に関してユーザーが受け取る通知は、[コンピューターの再起動のクライアント設定](about-client-settings.md#computer-restart)と、使われている Configuration Manager のバージョンによって異なります。 この記事は、管理者が保留中のデバイス再起動通知に対するユーザー エクスペリエンスを判断するのに役立ちます。

>[!NOTE]
> - この記事で対象になっているクライアント設定は、Configuration Manager バージョン 1902 およびバージョン 1906 のものです。


## <a name="deployment-types-for-restart-notifications"></a>再起動通知の展開の種類

[コンピューターの再起動のクライアント設定](about-client-settings.md#computer-restart)により、再起動を必要とする以下の種類のすべての必要な展開に対するユーザー エクスペリエンスが変更されます。

- [アプリケーション](../../../apps/deploy-use/deploy-applications.md)。
- [タスク シーケンス](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [ソフトウェア更新プログラム](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>再起動通知の種類

再起動が必要になると、エンド ユーザーには予定されている再起動が通知されます。 ユーザーは、次の 4 つの一般的な通知を受け取る場合があります。

再起動が必要であることを知らせる**トースト通知**。 トースト通知の情報は、実行されている Configuration Manager のバージョンによって異なる場合があります。 この種類の通知は Windows OS にネイティブであり、サードパーティ製のソフトウェアでこの種類の通知が使われていることもあります。

![保留中再起動のトースト通知](media/3555947-restart-toast.png)

再起動が強制されるまでの残り時間を示す、再通知オプションを含むソフトウェア センターの通知。 メッセージは、Configuration Manager のバージョンによって異なる場合があります。

![再通知ボタンのある保留中再起動のソフトウェア センター通知](media/3976435-snooze-restart-countdown.png)

ユーザーは閉じることができないソフトウェア センターの最終カウントダウン通知。 再通知ボタンはグレー表示になります。

![ソフトウェア センターの最終カウントダウン通知](media/3976435-final-restart-countdown.png)

期限になる前に、再起動の必要な必須ソフトウェアをユーザーが事前にインストールすると、別の通知が表示されます。 ユーザー エクスペリエンスの設定で通知が許可されていて、かつ、展開にトースト通知が使われていない場合は、次の通知が発生します。 これらの設定の構成について詳しくは、「[展開の**ユーザー エクスペリエンス**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)」および「[必要な展開のユーザー通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)」をご覧ください。

![事前にインストールされたソフトウェアに対する通知](media/3976435-proactive-user-restart-notification.png)

- トースト通知を使っていない場合、**利用可能**とマークされたソフトウェアに対するダイアログは、事前にインストールされたソフトウェアのものと似ています。

  - **利用可能**なソフトウェアの場合、通知に再起動の期限はなく、ユーザーは独自に再通知間隔を選択できます。 詳しくは、「[承認設定](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)」をご覧ください。

    !["使用可能" とマークされているソフトウェアでは、通知に再起動の期限はありません。](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>バージョン 1902 でのデバイス再起動通知

<!--3555947-->
再起動や必須の展開に関する Windows のトースト通知が表示されないことがあります。 また、リマインダーを再通知するエクスペリエンスが表示されません。 クライアントが期限に達すると、この動作が原因でユーザー エクスペリエンスが低下する可能性があります。

バージョン 1902 以降では、ソフトウェアの変更が必要な場合、または展開で再起動が必要な場合に、より頻繁に表示されるダイアログ ウィンドウを使用できるようになりました。

クライアント設定の [[コンピューターの再起動]](about-client-settings.md#computer-restart) グループで、次のオプションを有効にします。 **[When a deployment requires a restart, show a dialog window to the user instead of a toast notification]\(展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する\)** 。  

このクライアント設定を構成すると、トースト通知からの再起動が必要な、すべての必要な展開のユーザー エクスペリエンスが変更されます。

!["再起動が必要" というトースト通知](media/3555947-restart-toast-initial.png)  

さらに詳細なソフトウェア センターのダイアログ ウィンドウになります。

![コンピューターを再起動するためのダイアログ ウィンドウ](media/3976435-proactive-user-restart-notification.png)

インストール後にユーザーがデバイスを再起動しなかった場合、リマインダーとして通知が送られます。 この一時的なリマインダーは、次のクライアント設定に基づいてユーザーに表示されます: **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)]** 。 この設定は、再起動が強制される前に、ユーザーがコンピューターを再起動する必要がある全体的な時間です。

- トースト通知を使用したときの一時的な通知:

  ![保留中再起動のトースト通知](media/3555947-restart-toast.png)

- トーストではなく、ソフトウェア センターのダイアログ ウィンドウを使用したときの一時的な通知:

  ![再通知ボタンのある保留中再起動のソフトウェア センター通知](media/3555947-1902-hide-notification.png)

一時的な通知の後でユーザーが再起動を行わない場合は、閉じることができない最終的なカウントダウン通知が表示されます。 最終通知が表示されるタイミングは、次のクライアント設定に基づきます: **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる、ユーザーが閉じることのできないダイアログ ボックスを表示する (分)]** 。 たとえば、設定が 60 の場合、再起動が強制される前の 1 時間、最終通知がユーザーに対して表示されます。

![ソフトウェア センターの最終カウントダウン通知](media/3555947-1902-final-countdown.png)

以下の設定は、コンピューターに適用される最短の[メンテナンス期間](../manage/collections/use-maintenance-windows.md)より短い期間にする必要があります。

- **ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)**
- **ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる、ユーザーが閉じることのできないダイアログ ボックスを表示する (分)**

> [!IMPORTANT]
> Configuration Manager 1902 の場合、特定の状況下では、ダイアログ ボックスでトースト通知が置き換えられません。 この問題を解決するには、[Configuration Manager バージョン 1902 の更新プログラムのロールアップ](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)をインストールします。 <!--4404715-->

## <a name="device-restart-notifications-starting-in-version-1906"></a>バージョン 1906 以降でのデバイス再起動通知
<!--3976435-->
一部の管理者は、再起動通知をもっと頻繁に行い、短い間隔で再起動を延期できるようにすることを好みます。 他の管理者は、ユーザーが再起動をもっと長い間隔で延期できるようにし、あまり頻繁には保留中再起動をユーザーに通知しません。 Configuration Manager バージョン 1906 では、再起動通知のタイミングと頻度に関する管理者の制御が追加されました。 1906 では、管理者による制御強化のために次の項目が導入されました。

- **[コンピューターの再起動のカウントダウン通知を再通知する期間を指定する (分)]** が、[コンピューターの再起動のクライアント設定](about-client-settings.md#computer-restart)に追加されました。
- **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)]** の最大値が、1440 分 (24 時間) から 20160 分 (2 週間) に増えました。
- 保留中の再起動が 24 時間未満になるまで、ユーザーに再起動通知の進行状況バーが表示されません。

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>期限時または期限後に必要なソフトウェアがインストールされたときの通知

必要なソフトウェアが期限の時点で、または期限後にインストールされると、選択されているクライアント設定に応じた通知がユーザーに表示されます。

設定 **[展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する]** が次のように設定された場合:

- **[いいえ]** - 最終的なカウントダウン通知になるまで、トースト通知が使われます。
- **[はい]** - ソフトウェア センターの通知が表示されます。
  - 再起動までの時間が 24 時間より長い場合は、推定再起動時刻が表示されます。 この通知のタイミングは、次の設定に基づきます: **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)]** 。

     ![再起動時刻まで 24 時間より長い](media/3976435-notification-greater-than-24-hours.png)

  - 再起動までの時間が 24 時間より短い場合は、進行状況バーが表示されます。 この通知のタイミングは、次の設定に基づきます: **ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)**

     ![再起動時刻まで 24 時間より短い](media/3976435-notification-less-than-24-hours.png)

ユーザーが **[再通知]** ボタンを選択した場合、再通知期間が経過した後で、最終的なカウントダウンに到達していないときは、別の一時的な通知が行われます。 次の通知のタイミングは、次の設定に基づきます: **[Specify the snooze duration for computer restart countdown notifications (hours)]\(コンピューターの再起動のカウントダウン通知を再通知する期間 (時間) を指定する\)** 。 ユーザーが **[再通知]** を選択し、再通知間隔が 1 時間の場合、最終的なカウントダウンに到達していないときは、ユーザーは 60 分後に再び通知されます。

最終的なカウントダウンに達すると、ユーザーには閉じることができない通知が表示されます。 進行状況バーは赤で表示され、ユーザーは **[再通知]** をクリックできません。

![バージョン 1906 でのソフトウェア センターの最終カウントダウン通知](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>期限前にユーザーがインストールする

期限になる前に、再起動の必要な必須ソフトウェアをユーザーが事前にインストールすると、別の通知が表示されます。 これらの設定の構成について詳しくは、「[展開の**ユーザー エクスペリエンス**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)」および「[必要な展開のユーザー通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)」をご覧ください。 

ユーザー エクスペリエンスの設定で通知が許可されていて、かつ、展開にトースト通知が使われていない場合は、次の通知が発生します。

![事前にインストールされたソフトウェアに対する通知](media/3976435-proactive-user-restart-notification.png)

ソフトウェアの期限に達したときは、「[期限時または期限後に必要なソフトウェアがインストールされたときの通知](#notifications-when-required-software-is-installed-at-or-after-the-deadline)」の動作のようになります。

## <a name="log-files"></a>ログ ファイル

デバイスの再起動をトラブルシューティングするには、**RebootCoordinator.log** と **SCNotify.log** を使用します。 使われている展開の種類に基づく追加のクライアント [ログ ファイル](../../plan-design/hierarchy/log-files.md)を使用することが必要な場合もあります。

## <a name="next-steps"></a>次のステップ

- [アプリケーション管理の概要](../../../apps/understand/introduction-to-application-management.md)
- [オペレーティング システムの展開の概要](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [ソフトウェア更新管理の概要](../../../sum/understand/software-updates-introduction.md)
