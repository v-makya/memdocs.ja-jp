---
title: レポートの計画
titleSuffix: Configuration Manager
description: インストールの詳細からセキュリティとネットワーク帯域幅まで、Configuration Manager でレポートを計画することが重要です。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694370"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Configuration Manager のレポートを計画する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のレポート機能には、SQL Server Reporting Services または Power BI Report Server の高度なレポート機能を利用する助けとなる一連のツールとリソースが用意されています。 Configuration Manager のレポートを計画するときは、次のセクションを参考にしてください。

## <a name="where-to-install-the-reporting-services-point"></a>レポート サービス ポイントをインストールする場所

サイトで Configuration Manager レポートを実行するとき、レポートは接続先のサイト データベース内の情報にアクセスできます。 次のセクションを参考に、レポート サービス ポイントのインストール場所と使用するデータ ソースを決定してください。

> [!NOTE]
> サイト システムの計画の詳細については、「[サイト システムの役割を追加する](../deploy/configure/add-site-system-roles.md)」を参照してください。

### <a name="supported-site-system-servers"></a>サポートされるサイト システム サーバー

レポート サービス ポイントは、中央管理サイト (CAS) やプライマリ サイトにインストールできます。 1 つのサイトと、階層内のその他のサイトにある複数のサイト システムで機能します。 Configuration Manager では、セカンダリ サイトのレポート サービス ポイントはサポートされません。 サイトの最初のレポート サービス ポイントが、既定のレポート サーバーとして設定されます。 1 つのサイトに、より多くのレポート サービス ポイントを追加することは可能ですが、Configuration Manager レポートでは、各サイトの既定のレポート サーバーが積極的に使用されます。 レポート サービス ポイントは、サイト サーバーまたはリモート サイト システムにインストールします。 最大のパフォーマンスを得るには、リモート サイト システム サーバーで SQL Server Reporting Services を使用します。

### <a name="data-replication-considerations"></a>データ レプリケーションに関する注意事項

レポート サービス ポイントのインストール場所を決定するにあたり、以下の要素を考慮してください。

- CAS データベースがレポート データ ソースとなっているレポート サービス ポイントは、グローバル データと、Configuration Manager 階層内のサイト データのすべてにアクセスできます。 階層内の複数のサイトのサイト データを含むレポートが必要な場合は、CAS にあるサイト システムにレポート サービス ポイントをインストールすることを検討してください。 その後、そのデータベースをレポート データ ソースとして使用します。

- 子プライマリ サイトのデータベースをレポート データ ソースとしているレポート サービス ポイントは、グローバル データと、ローカルのプライマリ サイトおよび子セカンダリ サイトのみのサイト データにアクセスできます。 Configuration Manager 階層内の他のプライマリ サイトについては、サイト データがこのプライマリ サイトにレプリケートされません。 Reporting Services では、他のプライマリ サイトのサイト データにアクセスできません。 特定のプライマリ サイトのサイト データまたはグローバル データを含むレポートが必要で、ユーザーには他のプライマリ サイトのサイト データへのアクセスを許可したくない場合は、プライマリ サイトのサイト システムにレポート サービス ポイントをインストールします。 その後で、プライマリ サイトのデータベースをレポート データ ソースとして使用します。

グローバル データとサイト データの詳細については、「[データの種類](../../plan-design/hierarchy/database-replication.md#types-of-data)」を参照してください。

### <a name="network-bandwidth-considerations"></a>ネットワークの帯域幅に関する考慮事項

同じサイト内のサイト システムは、サイトの構成方法に応じて、サーバー メッセージ ブロック (SMB)、HTTP、または HTTPS を使用して相互に通信します。 Configuration Manager では、この通信は管理されません。 ネットワーク帯域幅の制御を行わないと、これはいつでも発生する可能性があります。 サイト システムにレポート サービス ポイントの役割をインストールする前に、使用可能なネットワーク帯域幅を確認してください。

サイト システムの計画の詳細については、「[サイト システムの役割を追加する](../deploy/configure/add-site-system-roles.md)」を参照してください。

## <a name="plan-for-role-based-administration"></a>ロールベース管理の計画

レポートのセキュリティは、セキュリティ ロールとアクセス許可を管理ユーザーに割り当てることができる Configuration Manager のその他のオブジェクトと同様に機能します。 管理ユーザーは、適切なセキュリティ権限が付与されたレポートのみの実行と変更が可能です。 Configuration Manager コンソールでレポートを実行するには、**サイト**のアクセス許可と、特定のオブジェクトに対して構成されているアクセス許可に関して、**読み取り**権限が必要です。

Configuration Manager のその他のオブジェクトとは異なり、Configuration Manager コンソールで管理ユーザーに対して設定するセキュリティ権限は、Reporting Services でも構成されます。 Configuration Manager コンソールでセキュリティ権限を構成すると、レポート サービス ポイントは Reporting Services に接続して、レポート用に適切なアクセス許可を設定します。

たとえば、**ソフトウェア更新マネージャー**のセキュリティ ロールに付与されるアクセス許可は、**レポートの実行**と**レポートの変更**です。 **ソフトウェア更新マネージャー**の役割を持つユーザーは、ソフトウェア更新プログラムについてのレポートの実行と変更のみを行えます。 Configuration Manager コンソールでは、この役割に対して、その他のオブジェクトについてのレポートは表示されません。 この動作の例外として、一部のレポートは、Configuration Manager のセキュリティ保護可能な特定のオブジェクトに関連付けられていません。 これらのレポートについて、管理ユーザーには、レポートを実行する場合は **サイト** の **読み取り** 権限アクセス許可が、レポートを変更する場合は **サイト** の **変更** 権限アクセス許可が必要です。  

> [!IMPORTANT]
> レポート サービス ポイント アカウントとは異なるドメインのユーザーがレポートを正常に実行するためには、それらの 2 つのドメイン間に双方向の信頼を確立します。

レポートはロール ベース管理に対応しています。 Configuration Manager では、レポートを実行するユーザーのアクセス許可に基づいて、含められるすべてのレポートのデータがフィルター処理されます。 特定の役割を持つユーザーが参照できるのは、その役割に対して定義されている情報のみです。

レポートのセキュリティ権限について詳しくは、「[Configure reporting](configuring-reporting.md)」(レポートを構成する) を参照してください。

Configuration Manager の役割に基づいた管理の詳細については、「[Configure role-based administration](../deploy/configure/configure-role-based-administration.md)」(役割に基づいた管理の構成) を参考にしてください。

## <a name="reporting-recommendations"></a>レポートに関する推奨事項

Configuration Manager のレポートについては、以下の推奨事項とヒントを考慮に入れてください。

- 最大のパフォーマンスを得るには、レポート サービス ポイントをリモート サイト システム サーバーにインストールします。 レポート サービスポイントは、サイト サーバーへのインストールは可能ですが、リモート サイト システムにインストールすると最大のパフォーマンスが得られます。 この役割がバックグラウンド処理を行うときには、他の役割とのシステム リソースの競合が発生する可能性があります。 サイトおよび役割のパフォーマンスについて考慮する変数は多数ありますが、一般に、この構成によって、レポートとサイト全体のパフォーマンスが向上します。

- SQL Server Reporting Services のクエリを最適化します。 通常、レポートの遅延は、クエリの実行と結果の取得にかかる時間に起因します。 クエリ アナライザーや Profiler などの Microsoft SQL Server ツールが、クエリの最適化に役立つ可能性があります。

- レポートのサブスクリプション処理は、標準の業務時間帯以外に実行するようにスケジュールします。 可能な限り営業時間外にサブスクリプションを処理することで、Configuration Manager サイト データベース サーバーでの CPU 処理を最小限にできます。 これにより、予定外のレポート要求に対する可用性も向上されます。

- サイトの更新では、組み込みのレポートが保持されます。 標準レポートを変更すると、サイトの更新時に、レポートはアンダースコアのプレフィックス (`_`) が付いた名前に変更されます。 このような動作なので、変更したレポートが、サイトの更新によって標準レポートで上書きされることはありません。

## <a name="security-and-privacy"></a>セキュリティとプライバシー

Configuration Manager レポートには、Configuration Manager の標準的な管理操作中に収集される情報が表示されます。 たとえば、Configuration Manager で検出やインベントリから収集された情報をレポートに表示できます。 ソフトウェアの展開やコンプライアンス対応状況の確認などの、クライアント管理操作の現在のステータスをレポートに含めることもできます。

レポートに表示できるデータを生成する場合がある Configuration Manager の操作についての、セキュリティ上の推奨事項とプライバシー情報の詳細については、「[Configuration Manager のセキュリティとプライバシー](../../plan-design/security/security-and-privacy.md)」を参照してください。  

## <a name="next-steps"></a>次のステップ

[レポートの前提条件](prerequisites-for-reporting.md)
