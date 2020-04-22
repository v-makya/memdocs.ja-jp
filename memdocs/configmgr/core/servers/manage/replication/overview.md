---
title: SQL レプリケーションのトラブルシューティング
titleSuffix: Configuration Manager
description: 次の図を使用すると、Configuration Manager サイト間での SQL レプリケーションの理解とトラブルシューティングに役立ちます。
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703990"
---
# <a name="troubleshoot-sql-replication"></a>SQL レプリケーションのトラブルシューティング

複数サイト階層では、Configuration Manager は SQL レプリケーションを使用してサイト間でデータを転送します。 詳細については、「[データベース レプリケーション](../../../plan-design/hierarchy/database-replication.md)」を参照してください。

SQL レプリケーションの問題をよく理解し、トラブルシューティングに役立てるために次の図を使用します。

- [SQL レプリケーション](sql-replication.md)
- [SQL の構成](sql-configuration.md)
- [SQL パフォーマンス](sql-performance.md)
- [SQL レプリケーションの再初期化](sql-replication-reinit.md)
- [グローバル データの再初期化](global-data-reinit.md)
- [サイト データの再初期化](site-data-reinit.md)
- [再初期化の不明メッセージ](reinit-missing-message.md)

これらのトラブルシューティングの図は互いに関連しています。 関係を理解するには次の図を使用します。

![SQL レプリケーションのトラブルシューティング プロセスの概要図](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

詳細については、Microsoft サポートの次の一連のブログを参照してください。

- [ConfigMgr DRS 同期の内部](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [ConfigMgr 2012 データ レプリケーション サービス (DRS) の解放](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS – トラブルシューティングの FAQ](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [ConfigMgr 2012 DRS 初期化の内部](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012:DRS および SQL Service Broker 証明書の問題](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
