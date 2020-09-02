---
title: Microsoft Intune デバイスでデバイスの一括操作を使用する
titleSuffix: ''
description: リモート デバイスの一括操作を使用します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c00e124c9f2741c3b94b08b51a6d1d897086087
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914414"
---
# <a name="use-bulk-device-actions"></a>デバイスの一括操作を使用する

次のリモート操作に対して、デバイスの一括操作を使用できます。
- [Autopilot リセット](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [カスタム通知](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [削除](devices-wipe.md#delete-devices-from-the-intune-portal)
- [名前の変更](device-rename.md)
- [再起動](device-restart.md)
- [同期](device-sync.md)
- [ワイプ](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>デバイスの一括操作を使用する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[すべてのデバイス]**  >  **[デバイスの一括操作]** を選択します。
![デバイスの一括操作](./media/bulk-device-actions/bulk-device-actions.png)
3. **[デバイスの一括操作]** ページで、 **[OS]** と **[デバイス アクション]** を選択します。 一部のデバイス アクションには、設定する追加のオプションやフィールドがあります。 **[次へ]** を選択します。
4. **[デバイス]** ページで 1 から 100 個のデバイスを選択し、 **[次へ]** を選択します。
5. **[確認と作成]** ページで、 **[作成]** を選択します。

## <a name="next-steps"></a>次のステップ
[デバイス管理の概要。](device-management.md)