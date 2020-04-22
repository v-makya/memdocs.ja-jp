---
title: サイト サーバーの非推奨機能
titleSuffix: Configuration Manager
description: Configuration Manager でサポートされなくなったサイト サーバーの製品およびオペレーティング システムについて説明します。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702570"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Configuration Manager サイト サーバーで削除され、非推奨となったもの

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager サイト サーバーのサポート対象から削除されたか、今後の更新で削除される予定 (非推奨) の製品およびオペレーティング システムについて説明します。 Configuration Manager の使用に影響する可能性のある将来の変更について早期に注意するものです。  

この情報は将来、変更される可能性があります。 非推奨の機能、製品、オペレーティング システムにはここで取り上げられていないものもある可能性があります。  

## <a name="server-os"></a>サーバー OS  

|オペレーティング システム|最初に非推奨と発表|サポートの削除|
|-|-|-|
|Windows Server 2008 R2 SP1|2015 年 7 月 10 日| バージョン 1702|
|Windows Server 2008 SP2|2015 年 7 月 10 日|バージョン 1511|

## <a name="sql-server"></a>SQL Server

|SQL Server バージョン|最初に非推奨と発表|サポートの削除|
|-|-|-|
|SQL Server 2008 R2|2015 年 7 月 10 日|バージョン 1702|
|SQL Server 2008|2015 年 7 月 10 日|バージョン 1511|

使用している SQL Server のバージョンをアップグレードする必要がある場合は、次の方法 (簡単な方法から順に示されています) を使用することをお勧めします。

1. [SQL Server をインプレースでアップグレードします](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (推奨)。  

2. 新しいコンピューターに新バージョンの SQL Server をインストールします。 次に、Configuration Manager セットアップの[データベースの移動オプションを使用](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig)し、サイト サーバーを新しい SQL Server にポイントします。  

3. [バックアップと回復](../../../servers/manage/backup-and-recovery.md)を使用します。  

## <a name="next-steps"></a>次のステップ

詳細については、以下の記事を参照してください。

- [削除と非推奨](removed-and-deprecated.md)  

- [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)  

- [Configuration Manager の Current Branch バージョンのサポート](../../../servers/manage/current-branch-versions-supported.md)  
