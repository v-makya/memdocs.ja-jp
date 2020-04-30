---
title: プロビジョニング モード
titleSuffix: Configuration Manager
description: Configuration Manager タスク シーケンス中のクライアント プロビジョニング モードについて説明します。
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 815b32ecf7e9cd315c2365cb5ed73004b2a48718
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708650"
---
# <a name="provisioning-mode"></a>プロビジョニング モード

*適用対象:Configuration Manager (Current Branch)*

OS 展開タスク シーケンスの間に、クライアントは Configuration Manager によってプロビジョニング モードにされます。 (OS 展開タスク シーケンスには、Windows 10 へのインプレース アップグレードが含まれます)。この状態のクライアントでは、サイトからのポリシーは処理されません。 この動作により、タスク シーケンスの実行中に、クライアントで別の展開が実行されリスクがなくなります。 タスク シーケンスが成功または失敗で完了すると、クライアントのプロビジョニング モードは終了されます。

タスク シーケンスが予期せず失敗した場合、クライアントがプロビジョニング モードのままになる可能性があります。 たとえば、タスク シーケンス処理の途中でデバイスが再起動し、復旧できないような場合です。 管理者は、この状態のクライアントを手動で識別し、修正する必要があります。


## <a name="manually-remove-provisioning-mode"></a>プロビジョニング モードを手動で削除する

クライアントがプロビジョニング モードのままになっている場合は、この手動のプロセスを使用して、クライアントを通常の運用に戻します。

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> この WMI メソッドによって行われる変更の 1 つは、レジストリ値の設定ですが、他の変更も行われます。 レジストリ値を変更するだけでは、クライアントがプロビジョニング モードを完全に終了できません。 レジストリを手動で編集した場合、クライアントは予期しない動作を示すことがあります。  


## <a name="client-provisioning-mode-timeout"></a>クライアント プロビジョニング モードのタイムアウト

バージョン 1902 以降、タスク シーケンスでは、クライアントをプロビジョニング モードにすると、タイムスタンプが設定されます。 60 分ごとに、プロビジョニング モードのクライアントでは、タイムスタンプからの経過時間が確認されます。 48 時間より長くプロビジョニング モードになっている場合、クライアントは自動的にプロビジョニング モードを終了し、そのプロセスを再起動します。

48 時間は、プロビジョニング モードの既定のタイムアウト値です。 ユーザーは、レジストリ キー `HKLM\Software\Microsoft\CCM\CcmExec` の値 **ProvisioningMaxMinutes** を設定することにより、デバイスでのこのタイマーを調整できます。 この値が存在しないか `0` の場合、クライアントでは既定値の 48 時間が使用されます。

タイムスタンプ **ProvisioningEnabledTime** がレジストリ キー `HKLM\Software\Microsoft\CCM\CcmExec` にあります。 このタイムスタンプには、マシンがプロビジョニング モードに最後に移行したときの時刻の値が含まれます。 形式はエポック (Unix タイムスタンプ) で、UTC です。

また、このタイムスタンプは、次のコマンドを使用して、マシンをプロビジョニング モードに手動で移行したときに現在の時刻にリセットされます。

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>プロセス フロー図

これらの図は、タスク シーケンスとクライアントのプロセス フローを示しています。

### <a name="task-sequence"></a>タスク シーケンス

次の図は、タスク シーケンスがプロビジョニング モードを設定する方法を示しています。

![プロビジョニング モードを設定するタスク シーケンスのフロー図](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>クライアントの修復

次の図は、クライアントがプロビジョニング モードを終了する方法を示しています。

![プロビジョニング モードを終了するクライアントのフロー図](media/3197824-client-flow.png)


## <a name="see-also"></a>関連項目

[Windows と ConfigMgr のセットアップ](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[オペレーティング システムのアップグレード](task-sequence-steps.md#BKMK_UpgradeOS)
