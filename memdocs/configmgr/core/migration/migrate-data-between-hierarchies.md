---
title: データの移行
titleSuffix: Configuration Manager
description: ソース階層から Configuration Manager の移行先階層にデータを転送する方法について説明します。
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701750"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Configuration Manager の階層間でのデータの移行

*適用対象:Configuration Manager (Current Branch)*

サポートされるソース階層から Configuration Manager (現在のブランチ) の移行先階層にデータを転送するには、移行を使用します。 ソース階層からデータを移行すると、次のようになります。  

- ソース インフラストラクチャのサイト データベースからデータにアクセスし、そのデータを現在の環境に転送します。  

- 移行によってソース階層内のデータが変わることはありません。 代わりに、データが検出され、移行先階層のデータベースにコピーが格納されます。  

移行戦略を計画するときは、次の点を考慮してください。  

- 既存の Configuration Manager 2007 SP2 インフラストラクチャを、Configuration Manager (現在のブランチ) に移行できます。  

- サポートされるデータの一部またはすべてをソース サイトから移行することができます。  

- 1 つのソース サイトから移行先階層の複数のサイトにデータを移行することができます。  

- 複数のソース サイトから移行先階層内の 1 つのサイトにデータを移動することができます。  


次のビデオでは、2 つの一般的な[移行シナリオ](#BKMK_MigrationScenarios)について説明し、例を示します。 また、移行計画に Microsoft Azure を含めるオプションもあります。
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a> 概念  

 Configuration Manager は、移行時に以下の概念と用語を使用します。  

#### <a name="source-hierarchy"></a>ソース階層
Configuration Manager のサポートされているバージョンを実行していて、移行するデータを含む階層。 移行を構成する場合、ソース階層の最上位サイトを指定するときにソース階層を識別します。 ソース階層の指定後、移行先階層の最上位サイトは、指定されたソース サイトのデータベースからデータを収集して、移行可能なデータを特定します。 

詳細については、「[ソース階層](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies)」を参照してください。

#### <a name="source-sites"></a>ソース サイト
移行先階層に移行できるデータを含むソース階層のサイト。 

詳細については、「[ソース サイト](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites)」を参照してください。

#### <a name="destination-hierarchy"></a>移行先階層
ソース階層からのデータのインポートが実行される Configuration Manager 階層 (現在のブランチ)。

#### <a name="data-gathering"></a>データ収集
移行先階層に移行可能なソース階層内の情報を特定する継続的な処理。 Configuration Manager は、スケジュールに従ってソース階層を確認します。 このプロセスで、移行済みのソース階層内の情報に対する変更や、移行先階層で更新する可能性があるデータを識別します。

詳細については、「[データ収集](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)」を参照してください。

#### <a name="migration-jobs"></a>移行ジョブ
移行する特定のオブジェクトを構成してから、そのオブジェクトの移行先階層への移行を管理する処理。

詳細については、[移行ジョブ戦略の計画](planning-a-migration-job-strategy.md)に関するページを参照してください。

#### <a name="client-migration"></a>クライアントの移行
クライアントが使用する情報をソース サイトのデータベースから移行先階層のデータベースに転送する処理。 データの移行後、デバイス上のクライアント ソフトウェアを、移行先階層のクライアント ソフトウェアにアップグレードします。

詳細については、[クライアント移行戦略の計画](planning-a-client-migration-strategy.md)に関するページを参照してください。

#### <a name="shared-distribution-points"></a>共有配布ポイント
移行期間中に Configuration Manager が移行先階層と共有するソース階層の配布ポイント。

移行期間中に、移行先階層内のサイトに割り当てられたクライアントは、共有配布ポイントからコンテンツを取得できます。

詳細については、「[ソース階層と移行先階層で配布ポイントを共有する](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)」を参照してください。

#### <a name="monitoring-migration"></a>移行の監視
移行処理を監視する処理。 **[管理]** ワークスペースの **[移行]** ノードから、移行の進行状況と成功状態を監視します。

詳細については、[移行アクティビティの監視の計画](planning-to-monitor-migration-activity.md)に関するページを参照してください。

#### <a name="stop-gathering-data"></a>データ収集の停止
ソース サイトからのデータ収集を停止する処理。 ソース階層から移行するデータがなくなった場合や、移行関連のアクティビティを一時停止する場合、ソース階層からのデータ収集を停止するように移行先階層を構成できます。

詳細については、「[データ収集](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)」を参照してください。

#### <a name="clean-up-migration-data"></a>移行データのクリーンアップ
移行先階層のデータベースから移行関連情報を削除することで、ソース階層からの移行を終了する処理。

詳細については、[移行完了の計画](planning-to-complete-migration.md)に関するページを参照してください。



## <a name="typical-workflow"></a>一般的なワークフロー  

移行のワークフローを設定するには:

1.  サポートされるソース階層を指定します。  

2.  データ収集を設定します。 データ収集によって、Configuration Manager は、ソース階層から移行できるデータに関する情報を収集できます。  

     データ収集プロセスを停止するまで、Configuration Manager は、簡単なスケジュールに基づいてデータを収集するプロセスを自動的に繰り返します。 既定では、データ収集プロセスは 4 時間間隔で繰り返されるため、Configuration Manager は、ソース階層内のデータの変更を特定できます。 配布ポイントを共有するには、データ収集も必要です。  

3.  ソース階層と移行先階層間でデータを移行する移行ジョブを作成します。  

4.  データ収集プロセスは、 **[データ収集の停止]** アクションを使用していつでも停止できます。 データ収集を停止すると、Configuration Manager はソース階層内のデータに対する変更内容を特定する処理も停止されるため、配布ポイントは共有できなくなります。 通常、この操作は、ソース階層からのデータ移行や配布ポイントの共有を行う予定がなくなった場合に使用します。  

5.  必要に応じて、ソース階層のすべてのサイトでデータ収集を停止した後に、 **[移行データのクリーン アップ]** アクションを使用して移行データをクリーン アップすることができます。 このアクションで、ソース階層の移行に関する階層データが移行先階層のデータベースから削除されます。  

データを移行し、環境内のデバイスを管理するソース階層が不要になった場合は、そのソース階層とインフラストラクチャの使用を停止することができます。  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a> シナリオ  

 Configuration Manager は次の移行シナリオをサポートします。
- [Configuration Manager 2007 階層からの移行](#bkmk_2007)  
- [Configuration Manager 2012 または他の Configuration Manager 階層からの移行](#bkmk_2012)

> [!NOTE]  
>  スタンドアロン サイトを含む階層を、中央管理サイトを含む階層に拡張することは、移行に分類されません。 階層の拡張の詳細については、「[スタンドアロン プライマリ サイトを拡張する](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)」を参照してください。  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a> Configuration Manager 2007 階層からの移行  

 Configuration Manager 2007 からデータを移行する場合、既存のサイト インフラストラクチャの投資を保護できるだけでなく、次の利点があります。  

#### <a name="site-database-improvements"></a>サイト データベースの向上点
Configuration Manager (現在のブランチ) データベースは、Unicode を完全にサポートします。

#### <a name="database-replication-between-sites"></a>サイト間のデータベース レプリケーション
Configuration Manager (現在のブランチ) のレプリケーションは、Microsoft SQL Server に基づいています。 この動作によって、サイト間のデータ転送のパフォーマンスが改善されます。

#### <a name="user-centric-management"></a>ユーザー中心の管理
Configuration Manager (現在のブランチ) での管理タスクの中心はユーザーです。 たとえば、ユーザーのデバイス名が不明な場合にも、ユーザーにソフトウェアを配布することができます。 また、Configuration Manager では、ユーザーのデバイスにインストールできるソフトウェアやインストールのタイミングの管理だけでなく、さまざまな管理機能を利用できます。

#### <a name="hierarchy-simplification"></a>階層の簡略化
Configuration Manager (現在のブランチ) では、よりシンプルなサイト階層を構築できます。 これは、中央管理サイトの種類の導入と、プライマリ サイトとセカンダリ サイトの動作の変更による改善です。 Configuration Manager (現在のブランチ) は使用するネットワーク帯域幅が少ないため、以前のバージョンよりも必要なサーバー数が少なく済みます。

#### <a name="role-based-administration"></a>役割に基づいた管理
Configuration Manager (現在のブランチ) の中央管理型のセキュリティ モデルにより、それぞれの管理要件と業務要件に合わせた階層全体のセキュリティと管理機能が提供されます。

> [!NOTE]  
>  System Center 2012 Configuration Manager で初めて導入された設計の変更のため、Configuration Manager 2007 を Configuration Manager (現在のブランチ) にアップグレードすることはできません。 System Center 2012 Configuration Manager から Configuration Manager (現在のブランチ) へのインプレース アップグレードはサポートされています。  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a> Configuration Manager 2012 または他の Configuration Manager 階層からの移行  
 System Center 2012 Configuration Manager 階層または Configuration Manager 階層からデータを移行するプロセスは同じです。 このプロセスには、複数のソース階層から単一の移行先階層にデータを移行することが含まれます。 このプロセスは、既に Configuration Manager で管理されている追加のリソースを会社が取得する場合に使用することがあります。 さらに、テスト環境のデータを Configuration Manager 運用環境に移行することもできます。 このプロセスでは、Configuration Manager テスト環境への投資を維持できます。  



## <a name="see-also"></a>関連項目  

-   [Configuration Manager への移行の計画](planning-for-migration.md)  

-   [移行のためにソース階層とソース サイトを構成する](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [移行のための操作](operations-for-migration.md)  

-   [移行のセキュリティとプライバシー](security-and-privacy-for-migration.md)  

-   [Configuration Manager の使用の開始](../servers/deploy/start-using.md)
