---
title: デバイス コレクションへのアプリの展開に関するテクニカル リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager でのデバイス コレクションへのアプリケーション展開に関するテクニカル リファレンスです。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688790"
---
# <a name="application-deployment-for-device-collections"></a>デバイス コレクションへのアプリケーションの展開

*適用対象:Configuration Manager (Current Branch)*

アプリケーションがデバイス コレクションに展開されると、ポリシーは展開の目的に関係なく、コレクション内のすべてのデバイスを対象とします。 この記事では、クライアントでのポリシーのダウンロードと展開の処理について説明します。

> [!TIP]
> クライアント ログを確認するために必要なすべての情報は、[始める前に](app-deployment-technical-reference.md#before-you-begin)セクションで参照されている SQL クエリを実行することで取得できます。

## <a name="policy-download"></a>ポリシーのダウンロード

アプリケーション展開のポリシーがクライアントを対象とした後、クライアントは次のポリシーのポーリング サイクルでポリシーをダウンロードします。 クライアントは、ポリシーをダウンロードするときに、展開ポリシーに加えて関連するポリシーをダウンロードします。 これらの関連ポリシーには、アプリケーションのポリシー、展開の種類、グローバル条件などが含まれます。ポリシーのダウンロード アクティビティは、アプリケーションまたは割り当ての一意の ID のいずれかを使用して、クライアントの **Policyagent.log** で追跡できます。

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

ポリシーがクライアントにダウンロードされると、Scheduler コンポーネントによって、展開のアクティブ化と適用のスケジュールが作成されます。

## <a name="deployment-activation"></a>展開のアクティブ化

展開がアクティブ化されるとアプリケーションの評価が開始されます。 Scheduler コンポーネントは、割り当てを展開で構成されている使用可能な時間にアクティブ化するスケジュールを作成します。 このアクティビティは、アプリケーション割り当ての一意の ID を使用して、クライアントの **Scheduler.log** で追跡できます。

- **必要な**展開では、ライセンス認証スケジュールが作成されますが、サイト サーバーと配布ポイントでのリソースの競合を避けるために最大 2 時間の遅延があります。 アプリケーションが定義済みの要件に基づいて適用可能な場合は、評価中にアプリケーションのコンテンツがダウンロードされる可能性があるため、この遅延によって競合を回避できます。

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- **使用可能な**展開の場合は、展開で構成されている利用可能な時間に起動されるように、アクティブ化スケジュールが作成されます。

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

スケジュール時間が来ると、Scheduler コンポーネントは、アプリケーション評価を実行するために、DCM エージェントにアクティブ化メッセージを送信します。

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

DCM エージェントは、アクティブ化メッセージを受信し、アプリケーションを評価するジョブを作成します。

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>展開の強制

展開が強制されるとアプリケーションのインストールが開始されます。

- **必要な**展開では、ポリシーがダウンロードされた後に Scheduler が期限のスケジュールを作成し、展開期限にアプリケーションが強制されるようにします。 既定では、期限スケジュールはランダム化されません。 アクティブ化のランダム化は、クライアント設定の [[期限のランダム化を無効にする]](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization) によって制御できます。

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    期限になると、Scheduler コンポーネントによって、期限のメッセージが DCM エージェントに送信されます。 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    DCM エージェントは、期限のメッセージを受信し、アプリケーションを強制するジョブを作成します。
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > 期限が過去である展開の場合、アプリケーションは、評価、ダウンロード、およびインストールの各操作を実行する同じ DCM エージェント ジョブによって直ちにアクティブ化され、適用されます。

- **使用可能な** 展開では、ソフトウェア センターでユーザーがアプリケーションのインストールを開始したときに実施が行われるため、期限のスケジュールはありません。 ユーザーがインストールを開始すると、アプリケーションの評価、ダウンロード、およびインストールを実行するための DCM エージェント ジョブが作成されます。 このアクティビティは、クライアントの **DCMAgent.log** で追跡できます。

## <a name="next-steps"></a>次のステップ

- [アプリケーション展開クライアント コンポーネントを理解する](client-components-technical-reference.md)
