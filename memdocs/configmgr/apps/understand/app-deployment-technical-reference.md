---
title: アプリケーション展開のトラブルシューティングに関するテクニカル リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager でのアプリケーション展開のトラブルシューティングに関するテクニカル リファレンスです。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688870"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Configuration Manager アプリケーション展開のテクニカル リファレンス

*適用対象:Configuration Manager (Current Branch)*

この記事では、アプリケーション展開のしくみについて説明します。

## <a name="before-you-begin"></a>作業を開始する準備

アプリケーション展開のトラブルシューティングを行う場合は、クライアント ログを確認するときに役立つ項目が複数あります。 各項目は、次のとおりです。

- アプリケーション CI ID
- アプリケーションの一意の ID
- 展開の種類の一意の ID
- アプリケーション展開の一意の ID (割り当ての一意の ID とも呼ばれます)
- アプリケーション展開の目的
- コンテンツの一意の ID
- コレクション ID と名前
- コレクション型

トラブルシューティングを簡単にするために、次のような SQL クエリを Configuration Manager データベースに対して実行し、上記の情報を取得できます。

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> このクエリを実行する場合は、[アプリケーションのプロパティ] の [ソフトウェア センター] タブに表示されるローカライズされたアプリケーション名を使用するのではなく、[アプリケーションのプロパティ] の [全般情報] タブに表示されているアプリケーション名を使用する**必要**があります。

## <a name="next-steps"></a>次のステップ

- [アプリケーション展開ポリシー](deployment-policy-technical-reference.md)
