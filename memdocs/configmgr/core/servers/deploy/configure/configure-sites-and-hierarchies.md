---
title: サイトと階層の構成
titleSuffix: Configuration Manager
description: このチェックリストを利用し、サイトと階層の両方に影響を与える最も一般的な構成を考慮してください。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704680"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Configuration Manager のサイトと階層の構成

*適用対象:Configuration Manager (Current Branch)*

最初の Configuration Manager サイトのインストールまたは階層へのサイトの追加後に、チェック リストを使用して、サイトと階層の両方に影響する最も一般的な構成を検討しているか確認します。  

次の構成に関する注意事項は、ほとんどの展開に適用されます。  

- Active Directory フォレストの探索、境界、境界グループなどのように、互いに依存しているオプションもあります。  

- 一部の構成には、少なくとも開始時に構成を変更しないで使用できる既定値が設定されています。  

- 境界グループや配布ポイント グループなどのその他の構成は、使用前に構成が必要となります。  

| 操作 | 詳細 |  
|------------|-------------|  
| ロール ベース管理の構成 | Configuration Manager 環境でさまざまなオブジェクトやデータを表示および管理できる管理ユーザーを制御するために、管理の割り当て区分を設定します。<br /><br /> ロール ベース管理の構成は、階層内のすべてのサイトで共有されます。   <br/><br/>詳細については、「[役割に基づいた管理の構成](configure-role-based-administration.md)」を参照してください。 |  
| サイト データを Active Directory Domain Services に発行する | クライアントから簡単にサービスを検出し、サイトのリソースを効率よく使用できるようにします。<br /><br /> 最初に、[Active Directory スキーマを拡張](../../../plan-design/network/extend-the-active-directory-schema.md)します。 次に、各サイトを個別に構成して[サイト データを発行](publish-site-data.md)します。 |  
| サービス接続ポイントを構成する | サービス接続ポイントは、階層の最上位レベルにインストールして構成するようにします。 詳細については、「[About the service connection point](about-the-service-connection-point.md)」 (サービスの接続ポイントについて) を参照してください。 |  
| サイト システムの役割を追加する | 個々のサイトに追加のサイト システムの役割を 1 つ以上インストールします。 詳しくは、「[サイト システムの役割を追加する](add-site-system-roles.md)」をご覧ください。 |  
| サイト境界と境界グループを構成する | イントラネット上で管理対象デバイスを置くことのできるネットワークの場所は、境界を指定することによって定義します。 そのうえで、そうしたネットワークの場所に置かれたクライアントが Configuration Manager のリソースを検出できるように境界グループを構成します。 詳しくは、「[サイト境界と境界グループの定義](define-site-boundaries-and-boundary-groups.md)」をご覧ください。 |  
| 配布ポイント グループを構成する | 展開を管理しやすくするために配布ポイントの論理グループを構成します。 詳細については、「[配布ポイント グループの管理](install-and-configure-distribution-points.md#bkmk_manage)」を参照してください。 |  
| 探索を実行する | 検出を実行して、ネットワーク インフラストラクチャ、デバイス、ユーザーなどのネットワーク上のリソースを見つけます。<br /><br /> 詳細については、「[探索を実行する](run-discovery.md)」を参照してください。 |  
| 管理者のための冗長性と容量を追加する | 追加の SMS プロバイダーと Configuration Manager コンソールをインストールすると、管理者がインフラストラクチャの管理に使用する容量を拡張することができます。<br /><br /> **追加の SMS プロバイダーをインストール**し、サイトへのコンソールと API の接続に対して冗長性を提供します。 詳しくは、「[SMS プロバイダーを管理する](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)」をご覧ください。<br /><br /> **追加の Configuration Manager コンソールをインストール**して、追加の管理ユーザーに対してアクセス許可を与えます。 詳しくは、「[System Center Configuration Manager コンソールをインストールする](../install/install-consoles.md)」をご覧ください。 |  
| サイト コンポーネントを構成する | サイト システムの役割とサイト ステータス レポートの動作は、各サイトでサイト コンポーネントを構成することによって変更できます。 詳しくは、「[サイト コンポーネント](site-components.md)」をご覧ください。 |  
| カスタム コレクションを作成する | デバイスとユーザーについてサイトが検出する情報を使用し、将来の管理タスクを単純化するために、オブジェクトのカスタム コレクションを作成します。 詳しくは、「[コレクションを作成する方法](../../../clients/manage/collections/create-collections.md)」をご覧ください。 |  
| 危険度の高い展開を管理するための設定を構成する | 危険度が高い展開が作成されたら管理者に警告するように、サイトの設定を構成します。 詳細については、「[危険度の高い展開を管理するための設定](../../manage/settings-to-manage-high-risk-deployments.md)」を参照してください。 |  
| 管理ポイントのデータベース レプリカを構成する | 管理ポイントがクライアントからの要求を供給することでサイト データベース サーバーに加えられたプロセッサ負荷を軽減するように、データベース レプリカを構成します。 詳細については、「[管理ポイントのデータベース レプリカ](database-replicas-for-management-points.md)」を参照してください。 |  
| SQL Server Always On 可用性グループを構成する | プライマリ サイトと中央管理サイトでサイト データベースをホストするための高可用性と障害復旧ソリューションとして可用性グループを構成します。 詳しくは、「[高可用性サイト データベースの SQL Server AlwaysOn](sql-server-alwayson-for-a-highly-available-site-database.md)」をご覧ください。 |  
| サイト間のレプリケーションを変更する | 以下のことについては、「[サイト間のデータ転送](../../../plan-design/hierarchy/data-transfers-between-sites.md)」をご覧ください。<br /><br /> セカンダリ サイト間の[ファイルベースのレプリケーション](../../../plan-design/hierarchy/file-based-replication.md)を構成する<br /><br /> [データベース レプリケーション リンク](../../../plan-design/hierarchy/database-replication.md)を構成する<br /><br /> [分散ビュー](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews)を構成する |  
| パッシブ モードでサイト サーバーを構成する | バージョン 1806 以降では、各プライマリ サイトと中央管理サイトのサイト サーバーをパッシブ モードで構成します。 この機能により高可用性のサイト サーバーが提供されます。 詳細については、[サイト サーバーの高可用性](site-server-high-availability.md)に関するページを参照してください。 |  
