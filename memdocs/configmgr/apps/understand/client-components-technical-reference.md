---
title: アプリケーション展開クライアント コンポーネントに関するテクニカル リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager でのアプリケーション展開のトラブルシューティングに使用されるクライアント コンポーネントです。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688850"
---
# <a name="understanding-application-deployment-client-components"></a>アプリケーション展開クライアント コンポーネントを理解する

*適用対象:Configuration Manager (Current Branch)*

アプリケーション展開の評価と強制実行の操作は、クライアント上の DCM エージェント コンポーネントと CI エージェント コンポーネントによって処理されます。 この記事では、一般的な DCM と CI エージェント ジョブの動作について説明します。

## <a name="dcm-agent"></a>DCM エージェント

DCM エージェントは、構成アイテムの評価を担当する上位レベルのクライアント コンポーネントです。これには、アプリケーションが含まれます。 展開がアクティブ化または強制実行されると、DCM エージェント ジョブが作成されて、割り当てポリシーが読み取られ、実行する必要があるアクションが決定されます。 このアクティビティは、DCM エージェント ジョブ ID を使用してクライアント上の **DCMAgent.log** で追跡できます。これは、アプリケーションの一意の ID を検索することによって識別できます。

### <a name="device-deployments"></a>デバイスの展開

- **必要**な展開については、DCMAgent.log に該当するアクションが示されます。 これらのアクションは、展開の期限が既に過ぎているかどうかによって異なる場合があります。

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- **使用可能**な展開については、DCMAgent.log に展開が`is not mandatory`ことが示されます。 これらの展開では、アプリケーションの評価は実行されますが、ユーザーがインストールを開始しない限り、強制実行はスキップされます。

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>ユーザー展開

- **必要**な展開については、DCMAgent.log に該当するアクションが示されます。 これらのアクションは、展開の期限が既に過ぎているかどうかによって異なる場合があります。

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- **使用可能**な展開では、アプリケーションのインストールがユーザーによって開始されたときに、DCM エージェント ジョブが評価および強制実行のために作成されます。

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>CI エージェント

CI エージェントは、構成アイテムの評価と修復を行うクライアント コンポーネントです。 DCM エージェントは割り当てポリシーを読み取り、CI エージェント コンポーネントが要求されたアクションを実行するためのジョブを作成します。 **DCMAgent.log** は、CI エージェント ジョブ ID を記録します。これは、クライアント上の **CIAgent.log** で CI エージェントの活動を追跡する場合に便利です。

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

一般的な CI エージェント ジョブは、複数のフェーズを通過します。これは、**CIAgent.log** を CI エージェント ジョブ ID でフィルター処理して、`TransitionState` を探すことで確認できます。 アプリケーション展開の CI エージェント ジョブの主要なフェーズは次のとおりです。

- **DownloadingCIs**
  - このフェーズでは、アプリケーションの評価に必要なアプリケーション メタデータがダウンロードされます。 メタデータには、検出方法、要件規則、グローバル条件などが含まれます。この活動は **CIDownloader.log** と **DataTransferService.log** で追跡できます。 **使用可能**な展開の場合、このプロセスはアプリケーションの最初の評価中に発生します。 ただし、**必要**な展開では、ポリシーのダウンロード直後にこのプロセスが発生します。

- **InvokingSdmMethod**
  - このフェーズでは、アプリケーションの検出方法を使用して、アプリケーションがインストールされていて、目的の状態が決定されているかどうかを確認します。 この活動は、**AppDiscovery.log** と **AppIntentEval.log** で追跡できます。 このフェーズの詳細については、「[アプリケーションの評価](deployment-evaluation-technical-reference.md)」を参照してください。

- **StateDownloadingContents**
  - このフェーズでは、必要に応じてアプリケーションのコンテンツがダウンロードされます。 この活動は、**CA.log**、**ContentTransferManager.log**、**LocationServices.log**、**DataTransferService.log** で追跡できます。 このフェーズの詳細については、「[アプリケーションのダウンロード](deployment-download-technical-reference.md)」を参照してください。

- **StateEnforcingCIs**
  - このフェーズでは、アプリケーションのインストールが開始されます。 この活動は、**AppEnforce.log** で追跡できます。 このフェーズの詳細については、「[アプリケーションのインストール](deployment-install-technical-reference.md)」を参照してください。

- **StateEnforcementReporting**
  - このフェーズでは、管理ポイントにレポートするために、アプリケーションのインストール状態が記録されます。 この活動は、**StateMessage.log** で追跡できます。

CI エージェント ジョブはすべてのフェーズを通過しますが、必要でない場合はフェーズをスキップします。 例として、**使用可能**な展開では、ユーザーがソフトウェア センターからアプリケーションをインストールしようとするまで、StateDownloadingContents と StateEnforcingCIs の各フェーズがスキップされます。 ただし、**必要**な展開では、StateDownloadingContents フェーズは、割り当てがアクティブ化されたときに (必要に応じて) アプリケーションのコンテンツをダウンロードしますが、期限が未来である場合、StateEnforcingCIs フェーズはスキップされます。 この動作は、CIAgent.log を CI エージェント ジョブ ID でフィルター処理し、`Skipping policy` を探すことで確認できます。

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>次のステップ

- [アプリケーションの評価](deployment-evaluation-technical-reference.md)
- [アプリケーションのダウンロード](deployment-download-technical-reference.md)
- [アプリケーションのインストール](deployment-install-technical-reference.md)
