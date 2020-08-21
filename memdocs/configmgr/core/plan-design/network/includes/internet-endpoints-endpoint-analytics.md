---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126465"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Configuration Manager マネージド デバイスに必要なエンドポイント

Configuration Manager マネージド デバイスからは、Configuration Manager ロールのコネクタ経由で Intune にデータが送信され、Microsoft パブリック クラウドに直接アクセスする必要はありません。

| エンドポイント  | 関数  |
|-----------|-----------|
| `https://graph.windows.net` | Configuration Manager サーバー ロールで階層をエンドポイント分析にアタッチするときに、設定を自動的に取得するために使用されます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。 |
| `https://*.manage.microsoft.com` | Configuration Manager サーバー ロールのみで、デバイス コレクションおよびデバイスをエンドポイント分析に同期するために使用されます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。 |

### <a name="endpoints-required-for-intune-managed-devices"></a>Intune マネージド デバイスに必要なエンドポイント

エンドポイント分析にデバイスを登録する場合、デバイスから Microsoft パブリック クラウドに必要な機能データが送信される必要があります。 エンドポイント分析では、Windows 10 と Windows Server の接続ユーザーのエクスペリエンスと利用統計情報コンポーネント (DiagTrack) を利用して、Intune マネージド デバイスからデータが収集されます。 デバイス上の**接続ユーザー エクスペリエンスとテレメトリ** サービスが実行されていることを確認してください。

| エンドポイント  | 関数  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | [必要な機能データ](../../../../../analytics/data-collection.md#bkmk_datacollection)を Intune データ収集エンドポイントに送信するために Intune マネージド デバイスによって使用されます。 |
