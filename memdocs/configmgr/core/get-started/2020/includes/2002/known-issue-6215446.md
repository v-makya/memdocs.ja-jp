---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 54e00688c1375f9ec54ada86d2b2c4b9347d5405
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691850"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> コレクションを削除できない

<!--6245446-->
このバージョンの Technical Preview Branch では、コレクションを削除することはできません。

この問題を回避するには、次の Configuration Manager の PowerShell コマンドレットを使用してコレクションを削除します。

- [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps)
