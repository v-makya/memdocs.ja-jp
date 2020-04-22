---
title: サイト間のデータ転送
titleSuffix: Configuration Manager
description: Configuration Manager がサイト間でどのようにデータを移動するか、およびネットワークでデータの転送をどのように管理できるかについて説明します。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703620"
---
# <a name="data-transfers-between-sites"></a>サイト間のデータ転送

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、*ファイルベースのレプリケーション*と*データベース レプリケーション*を使用して、さまざまな種類の情報をサイト間で転送します。 Configuration Manager がサイト間でどのようにデータを移動するか、およびネットワークでデータの転送をどのように管理できるかについて説明します。  

## <a name="types-of-replication"></a>レプリケーションの種類

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /> ファイルベース レプリケーション

Configuration Manager のファイルベースのレプリケーションは、ファイルに入っているデータを階層内のサイト間で転送する方法です。 このデータには、子サイトの配布ポイントに展開するアプリケーションとパッケージが含まれます。 また、親サイトに転送されて処理される未処理の探索データ レコードも処理されます。  

詳細については、「[ファイルベースのレプリケーション](file-based-replication.md)」を参照してください。

### <a name="database-replication"></a><a name="bkmk_dbrep" /> データベース レプリケーション

Configuration Manager のデータベース レプリケーションは SQL Server を使用して階層のデータを転送します。 この方法を使用して、サイト データベースの変更を、階層内の他のサイトのデータベースの情報とマージします。

詳細については、「[データベース レプリケーション](database-replication.md)」を参照してください。

SQL レプリケーションのトラブルシューティングのヘルプについては、「[SQL レプリケーションのトラブルシューティング](../../servers/manage/replication/overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

[レプリケーションの監視](../../servers/manage/monitor-replication.md)
