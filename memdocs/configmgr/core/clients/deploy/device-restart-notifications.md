---
title: デバイスの再起動の通知
titleSuffix: Configuration Manager
description: Configuration Manager のさまざまなクライアント設定に対する再起動通知の動作。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feb9f4206df65ee34228577a9e589ddd1be72870
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127251"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Configuration Manager でのデバイスの再起動通知

*適用対象:Configuration Manager (Current Branch)*

保留中のデバイス再起動に関してユーザーが受け取る通知は、[コンピューターの再起動のクライアント設定](#client-settings)と、使用している Configuration Manager のバージョンによって異なります。 この記事は、保留中のデバイス再起動通知に関するユーザー エクスペリエンスを構成するのに役立ちます。

## <a name="deployment-types-for-restart-notifications"></a>再起動通知の展開の種類

[コンピューターの再起動のクライアント設定](#client-settings)により、再起動を必要とする以下の種類のすべての必要な展開に対するユーザー エクスペリエンスが変更されます。

- [アプリケーション](../../../apps/deploy-use/deploy-applications.md)。
- [タスク シーケンス](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [ソフトウェア更新プログラム](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>再起動通知の種類

デバイスを再起動する必要がある場合、再起動しようとしていることがクライアントからエンド ユーザーに向けて示されます。

### <a name="toast-notification"></a>トースト通知

Windows のトースト通知では、デバイスを再起動する必要があることをユーザーに知らせます。 トースト通知の情報は、実行されている Configuration Manager のバージョンによって異なる場合があります。 この種類の通知は、Windows OS に元々備わっているものです。 この種類の通知を使用しているサード パーティ製のソフトウェアもあるかもしれません。

:::image type="content" source="media/3555947-restart-toast.png" alt-text="保留中再起動のトースト通知":::

### <a name="software-center-notification-with-snooze"></a>再通知機能が付いたソフトウェア センターの通知

ソフトウェア センターにより、通知とともに、再通知オプションとデバイス再起動が強制されるまでの残り時間が表示されます。 メッセージは、Configuration Manager のバージョンによって異なる場合があります。

:::image type="content" source="media/3976435-snooze-restart-countdown.png" alt-text="再通知ボタンのある保留中再起動のソフトウェア センター通知":::

### <a name="software-center-final-countdown-notification"></a>ソフトウェア センターの最終カウントダウン通知

ソフトウェア センターは次の最終カウントダウン通知を表示します。ユーザーが通知を閉じたり、再通知を選択したりすることはできません。

:::image type="content" source="media/3976435-final-restart-countdown.png" alt-text="ソフトウェア センターの最終カウントダウン通知":::

バージョン 1906 以降では、保留中の再起動までの時間が 24 時間未満になるまで、再起動通知の進行状況バーはユーザーに対して表示されません。

### <a name="software-center-notification-before-deadline"></a>期限前のソフトウェア センター通知

期限より前に、ユーザーが事前に必要なソフトウェアをインストールし、再起動が必要な場合は、別の通知が表示されます。 ユーザー エクスペリエンスの設定で通知が許可されていて、かつ、展開にトースト通知が使われていない場合は、次の通知が発生します。 これらの設定の構成について詳しくは、「[展開の**ユーザー エクスペリエンス**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)」および「[必要な展開のユーザー通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)」をご覧ください。

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="事前にインストールされたソフトウェアに対する通知":::

#### <a name="available-apps"></a>Available apps

トースト通知を使っていない場合、**利用可能**とマークされたソフトウェアに対するダイアログは、事前にインストールされたソフトウェアのものと似ています。 **利用可能**なソフトウェアの場合、通知に再起動の期限はなく、ユーザーは独自に再通知間隔を選択できます。 詳しくは、「[承認設定](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)」をご覧ください。

:::image type="content" source="media/3555947-deployment-marked-available-restart.png" alt-text="利用可能なソフトウェアの再起動の期限が通知にない":::

### <a name="software-center-notification-of-required-restart"></a>必要な再起動に関するソフトウェア センターの通知

<!--3601213-->

バージョン 2006 以降では、デバイスの再起動が展開で要求されても自動的に実行されないように、クライアント設定を構成できます。 必須の展開でデバイスの再起動が必要な場合に、クライアント設定 **[Configuration Manager can force a device to restart]\(Configuration Manager でデバイスの再起動を強制できる\)** を無効にしていると、次の通知が表示されます。

:::image type="content" source="media/3601213-restart-your-computer.png" alt-text="コンピューターを再起動するためのソフトウェア センターの通知":::

この通知を **[再通知]** した場合は、どのように再起動リマインダー通知の頻度を構成したかに基づいて再表示されます。 **[再起動]** を選択するか、手動で Windows を再起動するまで、デバイスは再起動されません。

> [!NOTE]
> 既定では、引き続き Configuration Manager でデバイスを強制的に再起動できます。

## <a name="client-settings"></a>クライアント設定

クライアントの再起動の動作を制御するには、 **[コンピューターの再起動]** グループで、次のデバイス クライアント設定を構成してください。 詳しくは、「[クライアント設定を構成する方法](configure-client-settings.md)」をご覧ください。

### <a name="configuration-manager-can-force-a-device-to-restart"></a>Configuration Manager でデバイスの再起動を強制できる

<!--3601213-->

バージョン 2006 以降では、デバイスの再起動が展開で要求されても自動的に実行されないように、クライアント設定を構成できます。 この設定は Configuration Manager で既定で有効になっています。

> [!IMPORTANT]
> このクライアント設定は、すべてのアプリケーション、ソフトウェア更新プログラム、およびデバイスへのパッケージの展開に適用されます。 ユーザーが手動でデバイスを再起動するまで、次のようになります。
>
> - ソフトウェア更新プログラムとアプリ リビジョンが完全にインストールされない可能性があります
> - 追加のソフトウェアのインストールが行われない場合があります

この設定を無効にした場合、期限後にデバイスが再起動される、またはユーザーに最後のカウントダウン通知が提示されるまでの時間の長さを指定することはできません。

> [!NOTE]
> Configuration Manager の新機能をすべて利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>期限後からデバイスが再起動されるまでの経過時間を指定します (分)

この設定は、コンピューターに適用される最短のメンテナンス期間より短い期間にする必要があります。 メンテナンス期間について詳しくは、「[メンテナンス期間を使用する方法](../manage/collections/use-maintenance-windows.md)」を参照してください。

既定値は 90 分です。 バージョン 1906 以降、最大値が 1440 分 (24 時間) から 20160 分 (2 週間) に拡大されました。

> [!NOTE]
> この設定は、以前は **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)]** というタイトルでした。

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>デバイスが再起動されるまでの最終カウントダウン通知をユーザーに表示する時間を指定します (分)

この設定は、コンピューターに適用される最短のメンテナンス期間より短い期間にする必要があります。 メンテナンス期間について詳しくは、「[メンテナンス期間を使用する方法](../manage/collections/use-maintenance-windows.md)」を参照してください。

既定値は 15 分です。

> [!NOTE]
> この設定は、以前は **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる、ユーザーが閉じることのできないダイアログ ボックスを表示する (分)]** というタイトルでした。

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>期限後からデバイスが再起動されるまでにアラーム通知をユーザーに表示する頻度を指定します (分)
<!--3976435-->
_バージョン 1906 以降_

頻度を示す値は、 **[期限後からデバイスが再起動されるまでの経過時間を指定します (分)]** の値から、 **[デバイスが再起動されるまでの最終カウントダウン通知をユーザーに表示する時間を指定します (分)]** の値を引いた値よりも短くする必要があります。 そうしないと、アラーム通知は動作しません。

既定値は 240 分です。

> [!NOTE]
> この設定は、以前は **[コンピューターの再起動のカウントダウン通知を再通知する期間を指定する (分)]** というタイトルでした。

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する
<!--3555947-->
バージョン 1902 以降、この設定を **[はい]** にすると、ポップアップ表示が増え、煩わしくなります。 この設定は、アプリケーション、タスク シーケンス、ソフトウェア更新プログラムのすべての展開に適用されます。 詳細については、[ソフトウェア センターの計画](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)に関するセクションを参照してください。

> [!IMPORTANT]
> Configuration Manager 1902 の場合、特定の状況下では、ダイアログ ボックスでトースト通知が置き換えられません。 この問題を解決するには、[Configuration Manager バージョン 1902 の更新プログラムのロールアップ](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)をインストールします。 <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>デバイス再起動通知 (バージョン 1906)
<!--3976435-->
一部のお客様は、再起動通知を頻繁に行い、ユーザーが短い間隔で再起動を延期できるようにすることを好みます。 他のお客様は、ユーザーが再起動をより長い間隔で延期できるようにし、あまり頻繁には保留中再起動をユーザーに通知しません。 Configuration Manager バージョン 1906 以降では、再起動通知のタイミングと頻度に関する制御が追加されました。

### <a name="install-required-software-at-or-after-the-deadline"></a>必要なソフトウェアを期限の時点か期限後にインストールする

必要なソフトウェアが期限の時点で、または期限後にインストールされると、選択されているクライアント設定に応じた通知がユーザーに表示されます。

設定 **[展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する]** が次のように設定された場合:

- **No**:展開が最終カウントダウン通知に到達するまで Windows にトースト通知が表示されます。

- **Yes**:ソフトウェア センターに通知が表示されます。

  - 再起動までの時間が 24 時間より長い場合は、推定再起動時刻が表示されます。 この通知のタイミングは、次の設定に基づきます: **[期限後からデバイスが再起動されるまでの経過時間を指定します (分)]**

    :::image type="content" source="media/3976435-notification-greater-than-24-hours.png" alt-text="再起動時刻まで 24 時間より長い":::

  - 再起動までの時間が 24 時間より短い場合は、進行状況バーが表示されます。 この通知のタイミングは、次の設定に基づきます: **[期限後からデバイスが再起動されるまでの経過時間を指定します (分)]**

    :::image type="content" source="media/3976435-notification-less-than-24-hours.png" alt-text="再起動時刻まで 24 時間より短い":::

ユーザーが **[再通知]** を選択する場合、再通知の期間が経過した後に別の一時的な通知が表示されます。 この動作は、まだ最終カウントダウンに到達していないことを前提としています。 次の通知のタイミングは、次の設定に基づきます: **[期限後からデバイスが再起動されるまでにアラーム通知をユーザーに表示する頻度を指定します (分)]** 。 ユーザーが **[再通知]** を選択し、再通知の期間が 1 時間である場合、ソフトウェア センターは 60 分後にユーザーに再び通知します。 この動作は、まだ最終カウントダウンに到達していないことを前提としています。

最終カウントダウンに到達すると、ソフトウェア センターはユーザーに対して、閉じることができない通知を表示します。 進行状況バーは赤で表示され、ユーザーは **[再通知]** を選択できません。

:::image type="content" source="media/3976435-1906-final-restart-countdown.png" alt-text="バージョン 1906 でのソフトウェア センターの最終カウントダウン通知":::

### <a name="proactively-install-required-software-before-the-deadline"></a>期限より前に、事前に必要なソフトウェアをインストールする

期限より前に、再起動を必要とする必須ソフトウェアをユーザーが事前にインストールすると、別の通知が表示されます。 これらの設定の構成について詳しくは、「[展開の**ユーザー エクスペリエンス**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)」および「[必要な展開のユーザー通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)」をご覧ください。

ユーザー エクスペリエンスの設定で通知が許可されていて、かつ、展開にトースト通知が使われていない場合は、次の通知が発生します。

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="事前にインストールされたソフトウェアに対する通知":::

展開が期限に到達すると、ソフトウェア センターの動作は「[必要なソフトウェアを期限の時点か期限後にインストールする](#install-required-software-at-or-after-the-deadline)」で説明されているのと同じになります。

## <a name="example-configurations"></a>構成例

次の例では、特定の動作を実現するためにクライアント設定を構成する方法について説明します。

### <a name="reminders-are-off"></a>アラームがオフの場合

| 設定 | 値 |
|---------|---------|
|期限後からデバイスが再起動されるまでの経過時間を指定します (分)|180|
|デバイスが再起動されるまでの最終カウントダウン通知をユーザーに表示する時間を指定します (分)|60|
|期限後からデバイスが再起動されるまでにアラーム通知をユーザーに表示する頻度を指定します (分)|240|
|展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する|いいえ|

デバイスは、展開期限の 3 時間 (**180** 分) 後に再起動します。 再起動の 1 時間 (**60** 分) 前になるとユーザーにカウントダウンが表示され、これを閉じたり、再通知を選択したりすることはできません。 最初のアラーム通知は期限の 4 時間 (**240** 分) 後に開始するように設定されていますが、これは再起動の後です。 そのため、ユーザーにアラームは表示されません。

### <a name="low-reminder-frequency"></a>アラームの頻度が低い場合

| 設定 | 値 |
|---------|---------|
|期限後からデバイスが再起動されるまでの経過時間を指定します (分)|7200|
|デバイスが再起動されるまでの最終カウントダウン通知をユーザーに表示する時間を指定します (分)|120|
|期限後からデバイスが再起動されるまでにアラーム通知をユーザーに表示する頻度を指定します (分)|900|
|展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する|はい|

デバイスは、展開期限の 5 日 (**7200** 分) 後に再起動します。 再起動の 2 時間 (**120** 分) 前になるとユーザーにカウントダウンが表示され、これを閉じたり、再通知を選択したりすることはできません。 この構成では、アラームを表示する時間が 118 時間あります (`(7200 - 120) / 60`)。 ソフトウェア センターは、期限から 15 時間 (**900** 分) 後に最初のアラームを表示します。 15 時間 (**900 分**) ごとに、最大で 6 回の追加のアラームを表示します。 ユーザーには、数秒間で消える通知ではなく、画面上のウィンドウとしてアラームが表示されます。

### <a name="high-reminder-frequency"></a>アラームの頻度が高い場合

| 設定 | 値 |
|---------|---------|
|期限後からデバイスが再起動されるまでの経過時間を指定します (分)|2880|
|デバイスが再起動されるまでの最終カウントダウン通知をユーザーに表示する時間を指定します (分)|60|
|期限後からデバイスが再起動されるまでにアラーム通知をユーザーに表示する頻度を指定します (分)|30|
|展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する|はい|

デバイスは、展開期限の 2 日 (**2880** 分) 後に再起動します。 再起動の 1 時間 (**60** 分) 前になるとユーザーにカウントダウンが表示され、これを閉じたり、再通知を選択したりすることはできません。 この構成では、アラームを表示する時間が 47 時間あります (`(2880 - 60) / 60`)。 ソフトウェア センターは、期限から **30** 分後に最初のアラームを表示します。 **30 分**ごとに、最大で 92 回の追加のアラームを表示します。 ユーザーには、数秒間で消える通知ではなく、画面上のウィンドウとしてアラームが表示されます。

## <a name="device-restart-notifications-version-1902"></a>デバイス再起動通知 (バージョン 1902)

<!--3555947-->
再起動や必須の展開に関する Windows のトースト通知が表示されないことがあります。 また、リマインダーを再通知するエクスペリエンスが表示されません。 クライアントが期限に達すると、この動作が原因でユーザー エクスペリエンスが低下する可能性があります。

バージョン 1902 以降では、ソフトウェアの変更が必要な場合、または展開で再起動が必要な場合に、より頻繁に表示されるダイアログ ウィンドウを使用できるようになりました。

クライアント設定の [[コンピューターの再起動]](#client-settings) グループで、次のオプションを有効にします。 **[When a deployment requires a restart, show a dialog window to the user instead of a toast notification]\(展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する\)** 。  

このクライアント設定を構成すると、トースト通知からの再起動が必要な、すべての必要な展開のユーザー エクスペリエンスが変更されます。

:::image type="content" source="media/3555947-restart-toast-initial.png" alt-text="再起動が必要 というトースト通知":::

さらに詳細なソフトウェア センターのダイアログ ウィンドウになります。

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="コンピューターを再起動するためのダイアログ ウィンドウ":::

インストール後にユーザーがデバイスを再起動しなかった場合、リマインダーとして通知が送られます。 この一時的なリマインダーは、次のクライアント設定に基づいてユーザーに表示されます: **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)]** 。 この設定は、再起動が強制される前に、ユーザーがコンピューターを再起動する必要がある全体的な時間です。

- トースト通知を使用したときの一時的な通知:

    :::image type="content" source="media/3555947-restart-toast.png" alt-text="保留中再起動のトースト通知":::

- トーストではなく、ソフトウェア センターのダイアログ ウィンドウを使用したときの一時的な通知:

    :::image type="content" source="media/3555947-1902-hide-notification.png" alt-text="再通知ボタンのある保留中再起動のソフトウェア センター通知":::

一時的な通知の後でユーザーが再起動を行わない場合は、閉じることができない最終的なカウントダウン通知が表示されます。 最終通知が表示されるタイミングは、次のクライアント設定に基づきます: **[ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる、ユーザーが閉じることのできないダイアログ ボックスを表示する (分)]** 。 たとえば、設定が 60 の場合、再起動が強制される前の 1 時間、最終通知がユーザーに対して表示されます。

:::image type="content" source="media/3555947-1902-final-countdown.png" alt-text="ソフトウェア センターの最終カウントダウン通知":::

以下の設定は、コンピューターに適用される最短の[メンテナンス期間](../manage/collections/use-maintenance-windows.md)より短い期間にする必要があります。

- **ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)**
- **ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる、ユーザーが閉じることのできないダイアログ ボックスを表示する (分)**

> [!IMPORTANT]
> Configuration Manager 1902 の場合、特定の状況下では、ダイアログ ボックスでトースト通知が置き換えられません。 この問題を解決するには、[Configuration Manager バージョン 1902 の更新プログラムのロールアップ](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)をインストールします。 <!--4404715-->

## <a name="log-files"></a>ログ ファイル

デバイスの再起動のトラブルシューティングを行うには、クライアント上の **RebootCoordinator.log** ファイルと **SCNotify.log** ファイルを使用します。 特定の種類の展開では、追加のクライアント [ログ ファイル](../../plan-design/hierarchy/log-files.md)も使用することが必要な場合があります。

## <a name="next-steps"></a>次のステップ

- [クライアント設定を構成する方法](configure-client-settings.md)
- [アプリケーション展開の**ユーザー エクスペリエンス**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [必要なアプリ展開のユーザー通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
