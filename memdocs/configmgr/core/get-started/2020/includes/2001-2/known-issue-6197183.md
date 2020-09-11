---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: c7fce3664d23d6402d28b053129fb2b15b540a87
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644221"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> 一部のコレクションを作成または編集できない

<!--6197183-->
このバージョンの Technical Preview ブランチでは、新しいコレクションを作成することはできません。 また、既存のユーザー コレクションのプロパティを編集することもできません。

この問題を回避するには、Configuration Manager PowerShell コマンドレットを使用して、新しいコレクションの作成と既存のユーザー コレクションの編集を行います。 コレクションを管理するために使用できるコマンドレットには、次のものがあります。

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)