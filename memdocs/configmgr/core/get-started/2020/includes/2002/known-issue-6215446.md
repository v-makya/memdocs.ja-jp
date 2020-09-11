---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 979760d1ebdd9d8f91993361921ae437ed5b81b1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644249"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> コレクションを削除できない

<!--6245446-->
このバージョンの Technical Preview Branch では、コレクションを削除することはできません。

この問題を回避するには、次の Configuration Manager の PowerShell コマンドレットを使用してコレクションを削除します。

- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection)