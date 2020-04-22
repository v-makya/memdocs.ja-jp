---
title: バージョン間の相互運用性
titleSuffix: Configuration Manager
description: 同じネットワーク上に複数の Configuration Manager 階層がある場合に競合を回避する方法について説明します。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693520"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>異なるバージョンの Configuration Manager 間の相互運用性

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の複数の独立した階層を、同じネットワークにインストールして動作させることができます。 ただし、移行プロセス以外では Configuration Manager の異なる階層は相互運用されないため、各階層に階層間の競合を防ぐ構成が必要です。 また、管理対象のリソースが正しい階層のサイト システムと対話できるように、特定の構成を作成することができます。  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a> Current Branch と以前のバージョンとの間の相互運用性  

異なるバージョンのサイトを同じ Configuration Manager 階層に共存させることはできません。 唯一の例外は、次のアップグレード シナリオの処理中です。

- System Center 2012 Configuration Manager から Configuration Manager Current Branch へ
- コンソール内更新プログラムを使用して、Configuration Manager Current Branch のあるバージョンから新しいバージョンへ

Configuration Manager Current Branch のサイトおよび階層は、既存の System Center 2012 Configuration Manager のサイトまたは階層と並列展開できます。 一方のバージョンのサイトにもう一方のバージョンのクライアントが参加することがないように計画してください。

たとえば、同じネットワークの場所が含まれる、複数の Configuration Manager 階層に[重複する境界](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries)がある場合、サイトの自動割り当てを使用する代わりに、新しい各クライアントを特定のサイトに割り当てます。 詳細については、「[サイトにクライアントを割り当てる方法](../../clients/deploy/assign-clients-to-a-site.md)」を参照してください。  

また、Configuration Manager Current Branch のサイト システムの役割をホストするコンピューターでは、System Center 2012 Configuration Manager のクライアントをインストールすることはできません。 また、System Center 2012 Configuration Manager のサイト システムの役割をホストするコンピューターに、Configuration Manager Current Branch クライアントをインストールすることもできません。  

次のクライアントと接続はサポートされていません。  

- System Center 2012 Configuration Manager 以前のコンピューター クライアント バージョン  

- System Center 2012 Configuration Manager 以前のデバイス管理クライアント  

- Windows CE Platform Builder デバイス管理クライアント (すべてのバージョン)  

- System Center Mobile Device Manager VPN 接続  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> クライアントのサイト割り当てに関する考慮事項  

Configuration Manager クライアントは、1 つのプライマリ サイトにのみ割り当てることができます。 次の条件がすべて該当する場合、クライアントの実際のサイト割り当てを予測することはできません。

- クライアントのインストール中にクライアントをサイトに割り当てるために、自動サイト割り当てを使用している
- 複数の境界グループに同じ境界が含まれている
- 境界グループには異なる割り当て済みサイトがある

Configuration Manager の複数のサイトと階層で境界が重複している場合、予期したとおりのサイトにクライアントが割り当てられなかったり、サイトにまったく割り当てられない可能性があります。  

Configuration Manager Current Branch クライアントでは、サイトの割り当てを完了する前にサイトのバージョンの確認が行われます。 サイトの境界が重なっている場合は、以前のバージョンのサイトにクライアントを割り当てることはできません。 ただし、以前の System Center 2012 Configuration Manager クライアントが、新しい Configuration Manager Current Branch サイトに間違って割り当てられる場合があります。  

2 つの階層に重複する境界がある場合に、クライアントが正しくないサイトに割り当てられるのを防ぐため、クライアントを特定のサイトに割り当てるようにクライアント インストール パラメーターを構成します。  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a> バージョンが混在している階層内の Configuration Manager の制限  

Configuration Manager Current Branch 階層のアップグレード時に、サイトごとにバージョンが異なることがあります。 たとえば、最初に中央管理サイトをアップグレードします。 サイトのメンテナンス期間なので、後の日時になるまでプライマリ サイトをアップグレードしません。  

特定の階層内にある各種サイトのバージョンが異なる場合、一部の機能は利用できません。 この動作は、Configuration Manager コンソールで Configuration Manager オブジェクトを管理する方法と、クライアントで使用できる機能に影響する可能性があります。 通常、Configuration Manager の新しいバージョンの機能を、古い Service Pack バージョンを実行しているサイトまたはクライアントで使用することはできません。  

### <a name="network-access-account"></a>ネットワーク アクセス アカウント

中央管理サイトを Configuration Manager Current Branch にアップグレードします。 この更新されたサイトに接続されている Configuration Manager コンソールからネットワーク アクセス アカウントの詳細を表示します。 まだ System Center 2012 Configuration Manager を実行しているサイトのアカウントの詳細は表示されません。

プライマリ サイトを中央管理サイトと同じバージョンにアップグレードすると、コンソールにアカウントの詳細が表示されます。

Configuration Manager のバージョン間で更新する場合も、同じ動作が適用されます。

### <a name="boot-images-for-os-deployment"></a>OS 展開用ブート イメージ

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>System Center 2012 Configuration Manager から Configuration Manager Current Branch へのアップグレード時

階層の最上位サイトが Configuration Manager Current Branch にアップグレードされると、既定のブート イメージが自動的に更新され、Windows アセスメント & デプロイ キット (ADK) バージョン 10 が使用されます。 これらのブート イメージは、Configuration Manager Current Branch サイトのクライアントへの展開にのみ使用してください。 詳細については、「[OS の展開の相互運用性に関する計画](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md)」をご覧ください。

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>Configuration Manager Current Branch バージョン間でのアップグレード時

新しいバージョンの Configuration Manager で使用中のバージョンの Windows ADK が更新されない限り、ブート イメージには影響ありません。

### <a name="new-task-sequence-steps"></a>新しいタスク シーケンス ステップ

以前のバージョンでは利用できないあるバージョンの Configuration Manager で導入された手順を使用してタスク シーケンスを作成すると、次の問題が生じる可能性があります。

- 以前のバージョンの Configuration Manager を実行しているサイトからタスク シーケンスを編集しようとするとエラーが発生する。

- 以前のバージョンの Configuration Manager クライアントを実行するコンピューターでタスク シーケンスが実行されない。

### <a name="client-to-down-level-management-point-communications"></a>ダウン レベルの管理ポイント通信のクライアント

クライアントよりも古いバージョンを実行しているサイトの管理ポイントと通信する Configuration Manager クライアントでは、ダウン レベルのバージョンの Configuration Manager がサポートしている機能のみ使用できます。 たとえば、最近アップグレードされた Configuration Manager Current Branch サイトのコンテンツを、そのバージョンにまだアップグレードされていない管理ポイントとの通信が行われているクライアントに展開する場合、そのクライアントでは最新バージョンの新しい機能を利用することができません。

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>レガシ クライアントへのパッケージとタスク シーケンスの展開

<!-- SCCMDocs-pr issue #3493 -->

バージョン 1902 以降では、5.7730 以前のクライアント バージョンにパッケージまたはタスク シーケンスを展開することはできません。 この制限を回避するには、以降のバージョンにクライアントをアップグレードします。

## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="orchestration-groups"></a>オーケストレーション グループ

バージョン 2002 で導入されたオーケストレーション グループは、バージョンが混在している階層では使用できません。 <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a> Configuration Manager コンソールの相互運用性  

このセクションでは、複数のバージョンの Configuration Manager が存在する環境での Configuration Manager の使用についてまとめます。  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>System Center 2012 Configuration Manager と Configuration Manager Current Branch の両方がある環境

Configuration Manager サイトを管理するには、コンソール、およびそのコンソールが接続するサイトの両方が、同じバージョンの Configuration Manager でなければなりません。 たとえば、2012 Configuration Manager コンソールを使って、Configuration Manager Current Branch サイトを管理することはできません。また、その逆も同様です。

同じコンピューターに、System Center 2012 Configuration Manager コンソールと Configuration Manager Current Branch コンソールの両方をインストールすることはできません。

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>Configuration Manager の複数のバージョンがある環境

Configuration Manager Current Branch では、1 台のコンピューターに複数の Configuration Manager コンソールをインストールすることはできません。 Configuration Manager のさまざまなバージョンに対して固有な複数のコンソールを使用する場合は、それぞれ別のコンピューターにそれぞれに異なるコンソールをインストールします。

階層内のサイトを更新しているときに、コンソールを、新しいバージョンを実行しているサイトに接続して、その階層にある他のサイトの情報を見ることができます。 ただし、この構成はお勧めしません。 コンソール バージョンと Configuration Manager サイト バージョンが異なることでデータの問題が発生する可能性があります。 最新の製品版で利用できる機能の一部がコンソールでは利用できなくなります。

サイトのバージョンと一致しないバージョンのコンソールを使用している場合は、サイトの管理がサポートされません。 これによりデータが失われ、サイトが危険にさらされる可能性があります。 たとえば、バージョン 1610 のコンソールを使用して、バージョン 1606 を実行しているサイトを管理することはサポートされません。
