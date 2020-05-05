---
title: デバイスアクションのトラブルシューティング
titleSuffix: Configuration Manager
description: Configuration Manager のデバイスアクションのテクニカルリファレンスに関するトラブルシューティング
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "82140277"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Configuration Manager デバイスのデバイスアクションのトラブルシューティング

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager 2002 以降では、Configuration Manager のクライアントを Microsoft Endpoint Manager 管理センターに同期させることができます。 一部のクライアントアクションは、同期されたクライアントで Microsoft Endpoint Manager 管理センターから実行できます。

使用できるアクションは次のとおりです。
- コンピューターポリシーの同期
- ユーザーポリシーの同期
- アプリの評価サイクル


[![Microsoft Endpoint Manager 管理センターのデバイスの概要](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
管理者が Microsoft Endpoint Manager 管理センターからアクションを実行すると、通知要求は Configuration Manager サイトおよびサイトからクライアントに転送されます。

## <a name="configuration-manager-components"></a>Configuration Manager コンポーネント

- **SMS_SERVICE_CONNECTOR**: Microsoft Endpoint Manager 管理センターからの通知を処理するためにゲートウェイ通知ワーカーを使用します。
- **SMS_NOTIFICATION_SERVER**: 通知を取得し、クライアント通知を作成します。
- **Bgbagent**: クライアントはタスクを取得し、要求されたアクションを実行します。

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Microsoft Endpoint Manager 管理センターからアクションが開始されると、 **Cmgatewaynotificationworker .log**が要求を処理します。  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Microsoft Endpoint Manager 管理センターから通知を受信しました。

   ```text
   Received new notification. Validating basic notification details..
   ```

1. ユーザーとデバイスの操作が検証されます。

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. リモートタスクが SMS_NOTIFICATION_SERVER に転送されます。

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

メッセージが SMS_NOTIFICATION_SERVER に送信されると、管理ポイントから対応するクライアントにタスクが送信されます。 次のものが、管理ポイントにある**Bgbserver .log**に表示されます。

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

最後の手順は、クライアントで発生し、 **Ccmnotificationagent .log**に表示されます。 タスクが受信されると、アクションを実行するようにスケジューラに要求します。 アクションが実行されると、次の確認メッセージが表示されます。

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>一般的な問題

管理者が Configuration Manager に必要なアクセス許可を持っていない場合`Unauthorized`は、 **Cmgatewaynotificationworker .log**に応答が表示されます。

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Microsoft Endpoint Manager 管理センターから操作を実行するユーザーに、Configuration Manager サイトに対する必要なアクセス許可があることを確認します。 詳細については、「 [Microsoft Endpoint Manager テナントの接続の前提条件](device-sync-actions.md#prerequisites)」を参照してください。

## <a name="next-steps"></a>次のステップ

[共同管理を有効](../comanage/overview.md)にすると、条件付きアクセスなどのクラウドを利用した追加機能を利用できます。
