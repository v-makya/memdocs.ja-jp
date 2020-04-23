---
title: サイト障害の影響
titleSuffix: Configuration Manager
description: Configuration Manager サイトでのさまざまな障害の影響について説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708570"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Configuration Manager でのサイト障害の影響

*適用対象:Configuration Manager (Current Branch)*

サイト サーバーおよびその他の任意のサイト システムに障害が発生した場合は、通常提供しているサービスを提供できなくなります。 複数のサイト システムを同一コンピューター上にインストールした場合は、コンピューターに障害が発生すると、これらのサイト システムで通常提供されるすべてのサービスが使用できなくなります。

計画プロセスには、組織に提供するサービスへの影響の把握を含めるようにしてください。 サイト内の各サイト システムは異なる機能を提供するので、障害が発生したサイト システムの役割によってサイト障害の影響は異なります。 

単一システムの障害を軽減するには、[高可用性オプション](../deploy/configure/high-availability-options.md)を使用します。 また、サービスを使用できない時間を短縮するために、[バックアップと回復](backup-and-recovery.md)戦略を計画し、実践します。

以下のセクションでは、指定したサイト システムが動作していない場合の影響について説明します。


### <a name="site-server"></a>サイト サーバー

- サイト管理を実行できません。 コンソールをサイトに接続できません。  

- 管理ポイントでクライアント情報が収集され、サイト サーバーがオンラインに戻るまでその情報がキャッシュされます。  

- ユーザーは既存の展開を実行できます。また、クライアントは配布ポイントからコンテンツをダウンロードできます。  


### <a name="site-database"></a>サイト データベース

- サイト管理を実行できません。  

- Configuration Manager クライアントに既に新しいポリシーが割り当てられ、管理ポイントにそのポリシー本体がキャッシュされている場合、クライアントはポリシー本体を要求したりポリシー本体の応答を受け取ったりできます。 ただし、新しいポリシー割り当て要求があっても、サイトは処理できません。  

- クライアントが既にポリシーを受信していて、関連するソース ファイルが既にクライアントにローカルにキャッシュされている場合に限り、クライアントは展開を実行できます。  


### <a name="management-point"></a>管理ポイント

- 新しい展開を作成することはできますが、クライアントは管理ポイントがオンラインになるまで展開を受信しません。  

- クライアントは、インベントリ、ソフトウェア使用状況測定、および状態情報を引き続き収集します。 管理ポイントが使用可能になるまで、このデータはローカルに格納されます。  

- クライアントが既にポリシーを受信していて、関連するソース ファイルが既にクライアントにローカルにキャッシュされている場合に限り、クライアントは展開を実行できます。  


### <a name="distribution-point"></a>配布ポイント

- 関連するソース ファイルが既にローカルにダウンロードされている場合、またはピア ソースで使用できる場合にのみ、Configuration Manager クライアントは展開を実行できます。

