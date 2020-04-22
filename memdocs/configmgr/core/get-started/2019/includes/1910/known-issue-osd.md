---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697850"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a> タスク シーケンスは、PXE またはメディアでは使用できません

<!--5578298-->
PXE またはメディア (USB または DVD) 用のタスク シーケンスを展開する場合、クライアントはポリシーを受け取りません。 次のメッセージは **smsts.log** にあります。

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>回避策

ソフトウェア センターからタスク シーケンスを開始する。
