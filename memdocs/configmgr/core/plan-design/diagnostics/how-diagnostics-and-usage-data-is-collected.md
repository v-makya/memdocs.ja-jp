---
title: 診断データを収集する
titleSuffix: Configuration Manager
description: Configuration Manager がそれ自体に関する診断と使用状況データを収集する方法について説明します。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688470"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Configuration Manager が診断結果と使用状況データを収集する方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の診断と使用状況データを収集するため、毎週、各プライマリ サイトで SQL Server のクエリが実行されます。 複数サイトの階層では、データは中央管理サイトにレプリケートされます。  

階層の最上位のサイトでは、サービス接続ポイントによって、更新プログラムをチェックするときに、この情報が送信されます。 サービス接続ポイントのモードは、データの転送方法によって決まります。

- **オンライン**:診断結果と使用状況データは、週に 1 回、サービス接続ポイントからクラウド サービスに自動送信されます。

- **オフライン**:[サービス接続ツール](../../servers/manage/use-the-service-connection-tool.md)を使用して、診断結果と使用状況データを手動で転送します。

詳細については、「[About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md)」 (サービスの接続ポイントについて) を参照してください。

> [!div class="nextstepaction"]
> [診断および使用状況データを使用する方法](view-diagnostics-and-usage-data.md)
