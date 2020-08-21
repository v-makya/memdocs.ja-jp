---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703852"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> 一部のコレクションを作成または編集できない

<!--6197183-->
このバージョンの Technical Preview ブランチでは、新しいコレクションを作成することはできません。 また、既存のユーザー コレクションのプロパティを編集することもできません。

この問題を回避するには、Configuration Manager PowerShell コマンドレットを使用して、新しいコレクションの作成と既存のユーザー コレクションの編集を行います。 コレクションを管理するために使用できるコマンドレットには、次のものがあります。

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)