---
title: アプリケーションのインストールに関するテクニカル リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager でのアプリケーション インストールのトラブルシューティングに関するテクニカル リファレンスです。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688820"
---
# <a name="application-installation"></a>アプリケーションのインストール

*適用対象:Configuration Manager (Current Branch)*

続行する前に、[アプリケーション展開クライアント コンポーネント](client-components-technical-reference.md)を参照して、DCM と CI エージェントのジョブの処理を理解してください。

アプリケーションのインストールは、展開が適用されるときに、DCM エージェント コンポーネントおよび CI エージェント コンポーネントによって実行されます。 適用時間は、使用可能な展開と必須の展開によって異なります。 割り当てが強制されるタイミングを理解するには、[デバイス コレクションへのアプリケーションの展開についての記事](device-deployment-technical-reference.md)または[ユーザー コレクションへのアプリケーションの展開に関する記事](user-deployment-technical-reference.md)を参照してください。

## <a name="enforcement-initiation"></a>強制開始

アプリケーションのインストールは、**StateEnforcingCIs** フェーズ中に、クライアントの CI エージェント コンポーネントによって開始されます。 このプロセスは、アプリケーションがデバイス コレクションに展開されるか、ユーザー コレクションに展開されるかに関係なく同じです。

- **使用可能**な展開の場合、ユーザーがソフトウェア センターからアプリケーションのインストールを開始すると、アプリケーションがインストールされます。
- **必須**の展開の場合、アプリケーションは展開の期限にインストールされます。 ただし、ユーザーは、期限前にソフトウェア センターからインストールを開始できます。

CI エージェントがアプリケーションのインストールを開始すると、CI タスク マネージャー コンポーネントによって処理されるタスクが作成されます。 次に、CI タスク マネージャーによってインストールが開始されます。 このアクティビティは、展開の種類の一意な ID を使用して **CITaskMgr.log** で追跡できます。

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>アプリケーションの強制適用

アプリケーションの強制適用が開始されると、クライアントはアプリケーションの検出を再度実行して、アプリケーションがまだインストールされていないことを確認します。 アプリケーションがインストールされていないと判断されると、アプリケーションのインストールが開始されます。 このアクティビティは、展開の種類の一意な ID を使用して、クライアントの **AppEnforce.log** で追跡できます。

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>インストールの確認

アプリケーションがインストールされたら、アプリケーションの検出方法を再度使用して、アプリケーションがインストール済みとして検出されたことを確認します。

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

最後に、強制適用が完了した後、CI エージェントはタスク完了通知を受信し、CI エージェント ジョブは次のフェーズに移動します。

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>次のステップ

[アプリケーションの展開のトラブルシューティング](../deploy-use/troubleshoot-application-deployment.md)
