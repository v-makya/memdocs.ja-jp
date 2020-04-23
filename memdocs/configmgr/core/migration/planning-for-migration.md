---
title: 移行の計画
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch の移行先階層にデータを移行する前に、サイトと階層について学んでください。
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702830"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Configuration Manager Current Branch への移行を計画する

*適用対象:Configuration Manager (Current Branch)*

データを Configuration Manager Current Branch 移行先階層に移行する前に、Configuration Manager のサイトと階層を把握しておく必要があります。 サイトと階層の詳細については、「[Configuration Manager の基本情報](../../core/understand/fundamentals.md)」を参照してください。  

サポートされているソース階層からデータを移行する前に、移行先階層として Configuration Manager Current Branch 階層をインストールします。  

移行先階層をインストールしたら、移行先階層で使用する管理機能を設定してから、データの移行を開始します。  

さらに、状況に応じて、ソース階層と移行先階層で重複が発生した場合についても計画する必要があります。 たとえば、移行先階層と同じネットワークの場所または境界を使用するようにソース階層が設定されている場合に、移行先階層に新しいクライアントをインストールして、自動サイト割り当てを使用するとします。 このシナリオでは、新しくインストールした Configuration Manager クライアントが、いずれかの階層から参加するサイトを選択できるため、クライアントがソース階層に誤って割り当てられる可能性があります。 そのため、移行先階層内の新しい各クライアントは、自動サイト割り当てを使用せずに、その階層内の特定のサイトに割り当てるように計画してください。  

サイトの割り当ての詳細については、「[異なるバージョンの Configuration Manager 間の相互運用性](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)」の「[クライアントのサイト割り当てに関する考慮事項](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment)」を参照してください。  

サポートされるソース階層を Configuration Manager 移行先階層に移行する方法を計画する際には、次の記事を参照してください。

-   [移行の前提条件](../../core/migration/prerequisites-for-migration.md)  

-   [移行計画の管理者チェックリスト](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Configuration Manager Current Branch にデータを移行するかどうかを判断する](../../core/migration/determine-whether-to-migrate-data.md)  

-   [ソース階層戦略を計画する](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [移行計画の管理者チェックリスト](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [クライアント移行戦略を計画する](../../core/migration/planning-a-client-migration-strategy.md)  

-   [コンテンツ展開移行戦略を計画する](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Configuration Manager Current Branch への Configuration Manager オブジェクトの移行を計画する](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [移行アクティビティの監視を計画する](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [移行の完了を計画する](../../core/migration/planning-to-complete-migration.md)  
