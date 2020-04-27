---
title: サイトのサイズとパフォーマンスに関する FAQ
titleSuffix: Configuration Manager
description: サイトのサイジングとパフォーマンスに関する Configuration Manager の一般的な質問に対する回答。
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073264"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Configuration Manager サイトのサイジングとパフォーマンスに関する FAQ

*適用対象:Configuration Manager (Current Branch)*

このドキュメントでは、Configuration Manager サイトのサイジングのガイダンスと一般的なパフォーマンスの問題についてよく寄せられる質問を取り上げます。

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>マシンとディスクの構成に関する FAQ と例

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>サイト サーバーと SQL Server 上のディスクはどのようにフォーマットする必要がありますか?

Configuration Manager の受信トレイと SQL ファイルを少なくとも 2 つの異なるボリュームに分けます。 この分離により、それらによって実行されるさまざまな種類の I/O に対してクラスター割り当てサイズを最適化できます。 

サイト サーバーの受信トレイをホストするボリュームには、4K または 8K のアロケーション ユニットを指定した NTFS を使用します。 ReFS では、小さなファイルの場合でも 64k を書き込みます。 Configuration Manager には多数の小さなファイルがあるため、ReFS では不要なディスク オーバーヘッドが発生する可能性があります。

SQL データベース ファイルを含むディスクには、64K のアロケーション ユニットを指定した NTFS または ReFS のいずれかのフォーマットを使用します。

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>SQL データベース ファイルは、どのような方法で、どこに配置すればよいですか?

最新のソリッド ステート ドライブ (SSD) と Azure Premium Storage のアレイを使用すると、少数ディスクの単一ボリュームで高い IOPS を得ることができます。 通常は、追加のスループットではなく、追加のストレージのためにドライブをアレイに追加します。 スピンドルベースの物理ディスクを使用している場合は、単一ボリュームで生成できるよりも多くの IOPS が必要になることがあります。 推奨される合計の IOPS とディスク領域の 60% を *.mdf* ファイルに、20% を *.ldf* ファイルに、20% をログおよびデータの一時ファイルに割り当てる必要があります。 *.ldf* および一時ファイルはすべて、割り当てられた IOPS の 40% (20% + 20%) を使用する単一ボリュームに配置できます。

SQL Server 2016 より前の SQL Server では、既定で、作成される一時データ ファイルが 1 つだけでした。 SQL ロックと単一ファイルへのアクセス待機を回避するために、もっと作成する必要があります。 作成する一時データ ファイルの最適な個数に関して、コミュニティの意見はさまざまです (4 から 8)。 テストの結果、4 から 8 の間には違いがほとんどないことが判明したため、*同じサイズの*一時データ ファイルを 4 個作成することができます。 tempdb データ ファイルは、データベース全体の最大 20 - 25% のサイズにする必要があります。

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>ディスクのセットアップに関する他の推奨事項はありますか?

構成可能な場合は、RAID コントローラー メモリの割り当てを書き込み操作用に 70%、読み取り操作用に 30% に設定します。 一般に、サイト データベース用には RAID 10 アレイ構成を使用します。 RAID 1 は、I/O 要件が低い小規模サイトや、高速 SSD 使用時にも許容できます。 大容量のディスク アレイでは、故障したディスクを自動的に交換するようにスペア ディスクを設定します。

**例: 物理ディスクがある物理マシン** 

クライアント数 **100,000** の併置されたサイト サーバーと SQL サーバーの場合、[サイジングのガイドライン](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)は、サイト サーバー受信トレイ用に 1200 IOPS、SQL Server ファイル用に 5000 IOPS です。

結果として得られるディスク構成は次のようになります。

| ドライブ<sup>1</sup> | RAID | フォーマット | ボリュームの内容 | 必要な最小 IOPS| 提供されるおよその IOPS<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | ConfigMgr 受信トレイ    |     1,700            | 1751             |
| 12x15k         | 10        | 64k ReFS    | SQL .mdf             | 60%*5000 = 3000     | 3476             |
| 8x15k          | 10        | 64k ReFS    | SQL .ldf、一時ファイル | 40%*5000 = 2000     | 2322             |

1. 推奨されるスペア ディスクは含まれません。 
2. この値は[ディスク構成の例](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)からのものです。 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Windows Server 上で Hyper-V を使用しています。 最適なパフォーマンスを得るには、Configuration Manager VM 用にディスクをどのように構成する必要がありますか?

Hyper-V では、ハードウェア リソース (CPU コアとパススルー ストレージ) が 100% 仮想マシン (VM) 専用である場合、物理サーバーと同様のパフォーマンスが得られます。 固定サイズの *.vhd* または *.vhdx* ディスク ファイルを使用すると、発生する I/O パフォーマンスへの影響は最小限の 1 - 5% です。 動的に拡張する *.vhd* または *.vhdx* ディスク ファイルを使用すると、Configuration Manager のワークロードの I/O パフォーマンスが最大 25% 低下します。 動的に拡張するディスクが必要な場合は、アレイに 25% の IOPS パフォーマンスを追加することによって補完します。

VM 内で Configuration Manager サイト サーバーまたは SQL を実行している場合は、Hyper-V ホスト OS ドライブを VM の OS およびデータ ドライブから分離します。

VM の最適化の詳細については、「[Hyper-V サーバーのパフォーマンス チューニング](/windows-server/administration/performance-tuning/role/hyper-v-server/)」を参照してください。

**例: Hyper-V VM ベースのサイト サーバー** 

クライアント数 **150,000** の併置されたサイト サーバーと SQL サーバーの場合、[サイジングのガイドライン](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)は、サイト サーバー受信トレイ用に 1800 IOPS、SQL Server ファイル用に 7400 IOPS です。

結果として得られるディスク構成は次のようになります。

| ドライブ<sup>1</sup> | RAID | フォーマット<sup>2</sup> | ボリュームの内容 | 必要な最小 IOPS| 提供されるおよその IOPS<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Hyper-V ホスト OS           | -                    | -                |
| 2x10k          | 1         | -              | (VM) サイト サーバー OS       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | (VM) ConfigMgr 受信トレイ    | 1,800                 | 7539             |
| 4xSSD SAS      | 10        | 64k ReFS       | (VM) ホスト SQL (すべてのファイル) | 7,400                 | 14346            |

1. 推奨されるスペア ディスクは含まれません。 
2. 基礎となるボリューム専用の VM ドライブ用の固定サイズのパススルー *.vhdx*。 
3. この値は[ディスク構成の例](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)からのものです。 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Microsoft Azure 上の Configuration Manager 環境に関する提案はありますか?

まず「[Azure の Configuration Manager - よく寄せられる質問](configuration-manager-on-azure.md)」を読むことから始めてください。

Premium Storage ベースのディスクを利用する Azure IaaS (サービスとしてのインフラストラクチャ) VM では、高い IOPS を得ることができます。 これらの VM では、追加の IOPS ではなく、予想されるディスク領域のニーズに合わせて追加のディスクを構成します。

Azure Storage は本質的に冗長であり、可用性のために複数のディスクを必要としません。 追加の領域とパフォーマンスを提供するために、ディスク マネージャーまたは記憶域スペースでディスクをストライピングすることができます。

Premium Storage のパフォーマンスを最大化し、Azure IaaS VM で SQL サーバーを実行する方法の詳細と推奨事項については、以下を参照してください。

- [アプリケーションのパフォーマンスの最適化](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [ディスクのガイダンス](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**例: Azure ベースのサイト サーバー** 

クライアント数 **50,000** の併置されたサイト サーバーと SQL サーバーの場合、[サイジングのガイドライン](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)は、サイト サーバー受信ボックス用に 8 コア、32 GB、1200 IOPS で、SQL Server ファイル用に 2800 IOPS です。

結果として得られる Azure マシンは、DS13v2 (8 コア、56 GB) で次のディスク構成になることが考えられます。

| ドライブ | フォーマット | 次の値を含む | 必要な最小 IOPS| 提供されるおよその IOPS<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;標準&gt; | -             | サイト サーバー OS     | -                    | -                |
| 1xP20 (512 GB)    | NTFS 8k       | ConfigMgr 受信トレイ  | 1,200                 | 2334             |
| 1xP30 (1024 GB)   | 64k ReFS      | SQL (すべてのファイル<sup>2</sup>) | 2,800                 | 3112             |

1. この値は[ディスク構成の例](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)からのものです。
2. [Azure のガイダンス](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)では、使用可能な容量を超えず、追加のディスク I/O 分散が可能になることを前提に、ローカルの SSD ベースの *D:* ドライブに配置することができます。

**例: Azure ベースのサイト サーバー (即時パフォーマンス向上のため)** 

Azure ディスクのスループットは、VM のサイズによって制限されます。 上記の Azure の例の構成では、将来の拡張または追加のパフォーマンスが制限される可能性があります。 Azure VM の最初のデプロイ時にディスクを追加した場合は、最小限の初期費用で、将来的に処理能力を高めるために Azure VM をアップサイズすることができます。 要件の変化に応じたサイトのパフォーマンス向上を事前に計画する方がずっと簡単で、より複雑な移行を後で行う必要がありません。

上記の Azure の例のディスクを変更して、IOPS がどのように変わるかを確認します。

**DS13v2** 

| ドライブ<sup>1</sup> | フォーマット | 次の値を含む | 必要な最小 IOPS| 提供されるおよその IOPS<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;標準&gt; | -             | サイト サーバー OS     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | ConfigMgr 受信トレイ  | 1,200                 | 3984             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL (すべてのファイル<sup>3</sup>) | 2,800                 | 3984             |

1. 記憶域スペースを使用してディスクをストライピングします。
2. この値は[ディスク構成の例](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)からのものです。 VM のサイズによってパフォーマンスが制限されます。
3. [Azure のガイダンス](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)では、使用可能な容量を超えず、追加のディスク I/O 分散が可能になることを前提に、ローカルの SSD ベースの *D:* ドライブに配置することができます。

将来さらにパフォーマンス向上が必要な場合は、VM を DS14v2 にアップサイズして CPU とメモリを 2 倍にすることができます。 その VM サイズで許容される追加のディスク帯域幅によって、以前に構成したディスク上の使用可能なディスク IOPS も即座に向上します。

**DS14v2**

| ドライブ<sup>1</sup> | RAID | フォーマット | 次の値を含む | 必要な最小 IOPS| 提供されるおよその IOPS<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;標準&gt; | -             | サイト サーバー OS     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | ConfigMgr 受信トレイ  | 1,200                 | 4639             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL (すべてのファイル<sup>3</sup>) | 2,800                 | 6182             |

1. 記憶域スペースを使用してディスクをストライピングします。
2. この値は[ディスク構成の例](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)からのものです。 VM のサイズによってパフォーマンスが制限されます。
3. [Azure のガイダンス](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)では、使用可能な容量を超えず、追加のディスク I/O 分散が可能になることを前提に、ローカルの SSD ベースの *D:* ドライブに配置することができます。

## <a name="other-common-sql-server-related-performance-questions"></a>SQL Server に関連するその他の一般的なパフォーマンスの質問 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>SQL は、サイト サーバーと併置して実行するのとリモート サーバー上で実行するのと、どちらがよいでしょうか?

1 台のサーバーのサイズが適切であるか、2 台のサーバー間でのネットワーク接続が十分であれば、どちらも適切に機能します。

リモート SQL は、追加サーバーの初期費用と運用コストが必要になるものの、大多数の大規模ユーザーの間では一般的です。 この構成の利点は次のとおりです。

- SQL Always On などのサイト可用性オプションの向上
- サイト処理のオーバーヘッドを減らしながら負荷の高いレポート作成を実行できること
- 状況によっては、より簡素化されたディザスター リカバリー
- より簡単なセキュリティ管理
- 個別の DBA チームなどによる、SQL 管理のための役割の分離

併置された SQL は、必要なサーバーが 1 台であり、ほとんどの小規模ユーザーにとって一般的なものです。 この構成の利点は次のとおりです。

- マシン、ライセンス、メンテナンスのコストを削減
- サイト内の障害ポイントの減少
- ダウンタイムを計画するための制御を強化

### <a name="how-much-ram-should-i-allocate-for-sql"></a>SQL 用にどれだけの量の RAM を割り当てる必要がありますか?

既定では、ご使用のサーバー上で使用可能なすべてのメモリが SQL に使用され、マシン上で OS やその他のプロセス用のメモリが不足する可能性があります。 潜在的なパフォーマンスの問題を回避するには、SQL にメモリを明示的に割り当てることが重要です。 SQL サーバーと併置されたサイト サーバーでは、ファイル キャッシュやその他の操作用に十分な RAM が OS にあることを確認してください。 SMSExec およびその他の Configuration Manager プロセス用に十分な RAM があることを確認します。 リモート サーバー上で SQL を実行するときは、全部ではなく "*大部分*" のメモリを SQL に割り当てることができます。 最初のガイダンスとして、[サイジングのガイドライン](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)を確認してください。 

SQL Server のメモリ割り当ては、整数の GB に丸める必要があります。 また、RAM が大容量になるほど、より高い比率を SQL に持たせることができます。 たとえば、256 GB 以上の RAM が使用可能な場合は、SQL を最大 95% に構成できます。そうすれば、OS 用にまだ十分なメモリが保持されます。 ページ ファイルを監視することは、OS およびすべての Configuration Manager プロセス用に十分なメモリがあることを確認するための良い方法です。

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>コアは最近安くなっています。 SQL サーバーに多数追加すればよいのでしょうか?

SQL サーバーに 16 個を超える物理コアがあり、十分な RAM がない場合は、メモリ競合の問題が発生する可能性があります。 Configuration Manager のワークロードは、1 コアあたり少なくとも 3 - 4 GB の RAM が SQL 用に使用可能な場合に、実行のパフォーマンスが向上します。 SQL サーバーにコアを追加するときは、必ず RAM の量を比例的に増やしてください。

### <a name="will-sql-always-on-impact-my-performance"></a>SQL Always On はパフォーマンスに影響しますか?

一般に、SQL レプリカ サーバー間で十分なネットワークが使用可能な場合、システムのパフォーマンスに対する SQL Always On の影響はほとんどありません。 処理量の多い SQL Always On 環境では、データベース ログ ( *.ldf*) ファイルが急速に大きくなることがあります。 ただし、データベース バックアップの正常終了後、ログ ファイルの領域は自動的に解放されます。 Configuration Manager データベースの SQL ジョブを追加して、たとえば 24 時間ごとにバックアップを実行し、6 時間ごとに *.ldf* のバックアップを実行します。 SQL バックアップ戦略の詳細など、SQL Always On と Configuration Manager の詳細については、[高可用性サイト データベース用の SQL Server Always On](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) に関するページを参照してください。

### <a name="should-i-enable-sql-compression-on-my-database"></a>データベースで SQL 圧縮を有効にする必要がありますか?

SQL 圧縮は Configuration Manager データベース用には推奨されません。 Configuration Manager データベースの圧縮を有効にすることに機能的な問題はありませんが、テスト結果には、システムのパフォーマンスに生じる可能性がある大幅な影響に比べて、大きなサイズ削減は示されていません。

### <a name="should-i-enable-sql-encryption-on-my-database"></a>データベースで SQL 暗号化を有効にする必要がありますか?

Configuration Manager データベース内のシークレットは既に安全に保存されていますが、SQL 暗号化を追加することで、さらに別のセキュリティ レイヤーを追加できます。 データベースに対する暗号化を有効にすることに機能的な問題はありませんが、暗号化の対象として選択するテーブルと、使用している SQL のバージョンによっては、最大 25% のパフォーマンス低下が発生する可能性があります。 そのため、特に大規模な環境では慎重に暗号化してください。 また、暗号化されたデータを正常に回復できるように、必ずバックアップと回復の計画を更新してください。

### <a name="what-version-of-sql-should-i-run"></a>どの SQL バージョンを実行する必要がありますか?

サポートされている SQL のバージョンについては、[SQL Server バージョンのサポート](../plan-design/configs/support-for-sql-server-versions.md)に関するページを参照してください。 パフォーマンスの観点からは、SQL のサポートされているすべてのバージョンで、必要なパフォーマンス基準が満たされています。 ただし、SQL 2012 および SQL 2016 以降では、Configuration Manager ワークロードの一部の機能で SQL 2014 を上回る傾向があります。 また、SQL 2014 を SQL 2012 互換性レベル (110) で実行すると、一般にパフォーマンスが向上します。 インストール時に、SQL 2012 および SQL 2014 で実行されている Configuration Manager データベースは、互換性レベル 110 に設定されます。 SQL 2016 以降では、その SQL バージョンの既定の互換性レベルに設定されます (SQL 2016 の場合は 130 など)。 SQL のインプレース アップグレードでは、次の Configuration Manager Current Branch メジャー バージョンをインストールするまで互換性レベルは更新されません。 

SQL 2016 以降において、管理コンソールでの RBAC 使用時などに、特定の SQL クエリに関して通常とは異なるタイムアウトやパフォーマンス低下が見られた場合は、Configuration Manager データベースの SQL 互換性レベルを 110 に変更してください。 SQL 2014 以降のバージョンでは、SQL 互換性レベル 110 での実行が完全にサポートされています。 詳細については、「[SQL query times out or console slow on certain Configuration Manager database queries](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d)」(特定の Configuration Manager データベース クエリで SQL クエリがタイムアウトする、またはコンソールが遅くなる) を参照してください。

2018 年 1 月の時点では、以下の SQL バージョンは*避けてください*。パフォーマンスに関連したさまざまな既知の問題や、その他の潜在的な問題があるためです。

- SQL 2012 SP3 CU1 から CU5 まで
- SQL 2014 SP1 CU6 から SP2 CU2 まで
- SQL 2016 RTM から CU3 まで、SP1 CU3 から CU5 まで

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>追加の SQL インデックス作成タスクを実装する必要はありますか?

はい。SQL のパフォーマンスを向上させるために、週に 1 回インデックスを更新し、1 日に 1 回統計情報を更新してください。 これらのタスクを最適化するには、サード パーティ製のスクリプトと、Configuration Manager および SQL コミュニティから入手できる追加情報が役立ちます。

大規模なサイトでは、CI\_CurrentComplianceStatusDetails、HinvChangeLog などの一部の SQL テーブルは、使用パターンに応じて大きくなる可能性があります。 それらの 1 つ 1 つを小さくするかメンテナンス方法を変更することが必要な場合があります。

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>どのような場合に、セカンダリ サイトで SQL Express ではなくフル機能の SQL Server を使用する必要がありますか?

SQL Express は、セカンダリ サイトでパフォーマンスに大きな影響を与えることはなく、ほとんどのお客様に適しています。 展開や管理も簡単で、あらゆる規模のほぼすべてのお客様に推奨される構成です。

フル機能 SQL Server のインストールが必要になる状況が 1 つあります。 ご使用の環境に多数の配布ポイントとパッケージ、またはソースがある場合は、SQL Express の 10 GB のサイズ制限を超える可能性があります。 パッケージの数と配布ポイントの数を掛けると 4,000,000 を超える場合 (2,000 個のコンテンツを含む配布ポイントが 2,000 個など)、セカンダリ サイトでフル機能の SQL Server を使用することを検討してください。 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>データベースの MaxDOP の設定を変更する必要はありますか?

設定を 0 (使用可能なすべてのプロセッサを使用する) のままにすることが、ほとんどの状況での全体的な処理パフォーマンスにとって最適です。

多くの Configuration Manager 管理者が、[SQL Server の "並列処理の最大限度" 構成オプションに関する推奨事項とガイドライン](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi)に従っています。 ほとんどの最新の大規模ハードウェアでは、このガイダンスに従うと、推奨される最大値の設定は 8 になります。 ただし、プロセッサの数に比べて多数の小さなクエリを実行する場合は、もっと大きい数値に設定すると役に立つことがあります。 より多くのコアが使用できる場合、8 に制限することは、必ずしも大規模サイトに最適な設定ではありません。 

8 個より多くのコアを搭載した SQL サーバーでは、最初は 0 に設定し、パフォーマンスの問題または過剰なロックが発生した場合にのみ変更します。 0 でパフォーマンスの問題が発生しているために MaxDOP を変更する必要がある場合は、少なくともそのサイトの SQL サーバーのサイジングとして推奨される最小コア数以上の新しい値から始めます。 この値より小さくすると、ほぼ確実にパフォーマンスに悪影響があります。 たとえば、クライアント数 100,000 のサイトのリモート SQL サーバーには、少なくとも 12 個のコアが必要です。 SQL サーバーに 16 個のコアがある場合は、MaxDOP の値を 12 に設定してテストを開始します。

## <a name="other-common-performance-related-questions"></a>その他の一般的なパフォーマンス関連の質問

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>サイト サーバー (またはその他の役割) のどのフォルダーをウイルス対策ソフトウェアから除外する必要がありますか?

どのシステムでも、ウイルス対策保護を無効にするときは注意してください。 大容量で安全な環境では、最適なパフォーマンスを得るために "*アクティブな監視*" を無効にすることをお勧めします。

推奨されるウイルス対策除外の詳細については、「[Recommended antivirus exclusions for Configuration Manager 2012 and Current Branch Site Servers, Site Systems, and Clients](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu)」(Configuration Manager 2012 および Current Branch のサイト サーバー、サイト システム、クライアントに対して推奨されるウイルス対策の除外) を参照してください。

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>Configuration Manager と組み合わせて使用するときに WSUS のパフォーマンスを向上させるには、どうすればよいですか?

WsusPool キューの長さや WsusPool プライベート メモリの制限など、いくつかの重要な IIS 設定を変更すると、小規模なインストールでも WSUS のパフォーマンスを向上させることができます。 詳細については、[推奨ハードウェア](../plan-design/configs/recommended-hardware.md)に関するページを参照してください。

また、WSUS を実行するオペレーティング システムに最新の更新プログラムをインストール済みであることを確認してください。

- Windows Server 2012:2017 年 10 月以降にリリースされた、"セキュリティ専用" 以外の累積的更新プログラム。 ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: 2017 年 8 月以降にリリースされた、"セキュリティ専用" 以外の累積的更新プログラム。 ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Windows Server 2016: 2017 年 8 月以降にリリースされた、"セキュリティ専用" 以外の累積的更新プログラム。 ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>WSUS サーバーに対して、どのような種類のメンテナンスを実行する必要がありますか?

「[Microsoft WSUS と Configuration Manager SUP のメンテナンスの完全ガイド](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)」を参照してください。

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>自分のサイトに基本的なパフォーマンスの監視を設定したいと考えています。 何を監視すればよいですか?

従来のサーバー パフォーマンス監視は、一般的な Configuration Manager に対して効果的に機能します。 Configuration Manager、SQL Server、および Windows Server 用のさまざまな System Center Operations Manager 管理パックを使用して、サーバーの基本的な正常性を監視することもできます。 Configuration Manager によって提供される Windows パフォーマンス モニター (PerfMon) のカウンターを直接監視することもできます。 さまざまな受信トレイのバックログを監視して、サイトのパフォーマンスに関する潜在的な問題やバックログの兆候を早期に警告します。

## <a name="see-also"></a>関連項目

- [サイトのサイズとパフォーマンスのガイドライン](../plan-design/configs/site-size-performance-guidelines.md)
- [Azure の Configuration Manager - よく寄せられる質問](configuration-manager-on-azure.md)
