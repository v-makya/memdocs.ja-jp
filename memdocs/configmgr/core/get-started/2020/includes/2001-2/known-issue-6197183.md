---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692100"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> 一部のコレクションを作成または編集できない

<!--6197183-->
このバージョンの Technical Preview ブランチでは、新しいコレクションを作成することはできません。 また、既存のユーザー コレクションのプロパティを編集することもできません。

この問題を回避するには、Configuration Manager PowerShell コマンドレットを使用して、新しいコレクションの作成と既存のユーザー コレクションの編集を行います。 コレクションを管理するために使用できるコマンドレットには、次のものがあります。

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
