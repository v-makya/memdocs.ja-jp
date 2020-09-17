---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 27436e7cd782ca910049007d52f37e2d7945f01e
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606322"
---
- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742-->

- `https://dc.services.visualstudio.com` <!--7541816-->

サービス接続ポイントでは、`https://*.manage.microsoft.com` でホストされている通知サービスに対して長期間の送信接続を行います。 サービス接続ポイントで使用しているプロキシによる送信接続のタイムアウトが早すぎないことを確認してください。 このインターネット エンドポイントへの発信接続には 3 分を設定することをお勧めします。 <!--7820969-->