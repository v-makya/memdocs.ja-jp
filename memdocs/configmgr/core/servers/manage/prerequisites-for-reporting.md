---
title: レポートの前提条件
titleSuffix: Configuration Manager
description: Configuration Manager のレポートの使用に影響するさまざまな依存関係について理解します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b082ae578052a92c0afacd3d1f62fdb2e21bd6d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699536"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Configuration Manager のレポートの前提条件

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のレポートには、以下の依存関係があります。

- SQL Server Reporting Services
- レポート サービス ポイント
- Power BI Report Server (オプション、バージョン 2002 以降)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Configuration Manager のレポートを使用するには、事前に SQL Server Reporting Services をインストールして構成します。

Reporting Services の計画と展開の詳細については、「[SQL Server Reporting Services をインストールする](/sql/reporting-services/install-windows/install-reporting-services)」を参照してください。

64 ビット SQL Server インストールの既定のインスタンスまたは名前付きインスタンスに、Reporting Services のデータベースをインストールします。 SQL Server インスタンスは、サイト システム サーバーと併置するか、リモート コンピューター上に構成します。

Configuration Manager では、レポート用に、サイト データベースの場合と同じバージョンの SQL Server がサポートされています。 詳細については、[サポートされている SQL Server のバージョン](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions)に関するページを参照してください。

## <a name="reporting-services-point"></a>レポート サービス ポイント

Configuration Manager のレポートを使用する前に、レポート サービス ポイントのサイト システムの役割を構成します。

詳細については、「[サイトとサイト システムの前提条件](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint)」をご覧ください。

## <a name="power-bi-report-server"></a>Power BI Report Server

バージョン 2002 以降では、Power BI Report Server をレポートと統合できるようになりました。 前提条件を含む詳細については、「[Power BI Report Server との統合](powerbi-report-server.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

[レポートの構成](configuring-reporting.md)