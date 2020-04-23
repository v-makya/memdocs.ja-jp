---
title: 現在のブランチにアップグレードする
titleSuffix: Configuration Manager
description: System Center 2012 Configuration Manager を実行しているサイトおよび階層から適切に一括アップグレードを実行するための手順を説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700410"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Configuration Manager Current Branch にアップグレードする

*適用対象:Configuration Manager (Current Branch)*

System Center 2012 Configuration Manager を実行しているサイトと階層から Configuration Manager の Current Branch への一括アップグレードを行います。 System Center 2012 Configuration Manager からアップグレードする前に、サイトを準備する必要があります。 この準備では、正常なアップグレードを妨げる可能性のある特定の構成を削除する必要があります。 その後、複数のサイトが関係しているときのアップグレード シーケンスに従います。  

> [!TIP]  
> Configuration Manager のサイトと階層のインフラストラクチャの管理において、"*アップグレード*"、"*更新*"、"*インストール*" という用語は、3 つの異なる概念を説明するために使用されます。 各用語の使用方法については、「[サイトと階層のインフラストラクチャでのアップグレード、更新、およびインストールについて](../../../understand/upgrade-update-install.md)」を参照してください。

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a> 一括アップグレード パス  

現在は、次のオプションがサポートされている一括アップグレード パスです。

### <a name="upgrade-to-version-2002"></a>バージョン 2002 にアップグレードする

次の製品は、Configuration Manager (Current Branch バージョン 2002) の "*正規ライセンス*" 版にアップグレードできます。

- Configuration Manager (Current Branch バージョン 2002) の "*評価版*" のインストール
- System Center 2012 Configuration Manager Service Pack 1
- System Center 2012 Configuration Manager Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager Service Pack 1

詳細については、「[Configuration Manager のブランチとライセンスに関してよく寄せられる質問](../../../understand/product-and-licensing-faq.md)」をご覧ください。

> [!TIP]  
> System Center 2012 Configuration Manager のバージョンから Current Branch にアップグレードすると、アップグレード プロセスを効率化できる可能性があります。 詳細については、次をご覧ください。  
>
> - [基準バージョンと更新プログラムのバージョン](../../manage/updates.md#bkmk_Baselines)  
> - [CD.Latest フォルダー](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>サポートされていないパス

次のパスはサポートされていません。

- Technical Preview ブランチから正規ライセンス版インストールへのアップグレードはサポートされていません。 Technical Preview バージョンは Technical Preview の新しいバージョンにのみアップグレードできます。  

- Technical Preview から正規ライセンス版への移行はサポートされていません。  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a> アップグレードのチェックリスト  

次のチェック リストは、Configuration Manager への適切なアップグレードの計画に役立ちます。  

### <a name="before-you-upgrade"></a>アップグレードする前に  

Configuration Manager にアップグレードする前に、以下の手順を確認してください。

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>System Center 2012 Configuration Manager の環境を確認する

次の Microsoft サポート記事で詳しく説明されている問題を解決します。[Configuration Manager クライアントで繰り返し発生される再試行タスクにのために 5 時間おきに再インストールされ、不注意によるクライアント アップグレードが引き起こされる可能性があります](https://support.microsoft.com/help/4018655)。

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>対象の環境がサポートされている構成を満たしていることを確認する

- サイト システムの役割をホストするために使用するサーバー OS のバージョンを確認します。  

  - System Center 2012 Configuration Manager によってサポートされている一部の古いオペレーティング システムは、Configuration Manager の Current Branch ではサポートされていません。 アップグレードする前に、これらの OS バージョン上のサイト システムの役割を削除します。 詳細については、[サイト システム サーバーでサポートされるオペレーティング システム](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)に関するページを参照してください。

  - Configuration Manager の前提条件チェッカーでは、サイト サーバーやリモート サイト システムでのサイト システムの役割の前提条件は検証されません  

- サイト システムの役割をホストする各コンピューターについて、必要な前提条件を確認します。 たとえば、Configuration Manager では、OS を展開するために Windows 10 アセスメント & デプロイメント キット (Windows ADK) が使用されます。 セットアップを実行する前に、サイト サーバーと、SMS プロバイダーのインスタンスを実行する各コンピューターに Windows 10 ADK をダウンロードしてインストールする必要があります。  

サポートされているプラットフォームおよび前提条件の構成について詳しくは、[サポートされている構成](../../../plan-design/configs/supported-configurations.md)に関する記事をご覧ください。  

Configuration Manager での Windows ADK の使用について詳しくは、「[Configuration Manager での OS の展開に対するインフラストラクチャ要件](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)」をご覧ください。  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>サイトと階層の状態を検討し、未解決の問題がないことを確認する

サイトをアップグレードする前に、サイト サーバー、サイト データベース サーバー、およびリモート コンピューターにインストールされているサイト システムの役割で、運用上のすべての問題を解決します。 運用に関する既存の問題のため、サイトのアップグレードが失敗することがあります。  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>サイト、サイト データベース サーバー、リモートのサイト システムの役割をホストするコンピューターのオペレーティング システムに適用できる、重要な更新プログラムすべてをインストールする

サイトをアップグレードする前に、該当する各サイト システムの重要な更新プログラムすべてをインストールします。 更新のインストール時に再起動が必要な場合は、サービス パックの更新を開始する前に該当するコンピューターを再起動します。  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Configuration Manager でサポートされていないサイト システムの役割をアンインストールする

以下のサイト システムの役割は、Configuration Manager では使用されなくなっています。 System Center 2012 Configuration Manager からアップグレードする前に、これらをアンインストールします。  

- 帯域外管理ポイント  

- システム正常性検証ツール ポイント  

- アプリケーション カタログ Web サイト ポイントと Web サービス ポイント

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>プライマリ サイトの管理ポイントのデータベース レプリカを無効にする

Configuration Manager では、管理ポイントのデータベース レプリカがあるプライマリ サイトをアップグレードすることはできません。 次の操作を行う前に、データベースのレプリケーションを無効にしてください。  

- データベースのアップグレードをテストするためにサイト データベースのバックアップを作成する  

- 実稼働サイトを Configuration Manager Current Branch にアップグレードする  

詳細については、以下の記事を参照してください。  

- System Center 2012 Configuration Manager:[管理ポイントのデータベース レプリカを構成する](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager、Current Branch: [管理ポイントのデータベース レプリカ](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>NLB を使用するソフトウェアの更新ポイントを再構成する

Configuration Manager では、ネットワーク負荷分散 (NLB) クラスターを使用してソフトウェアの更新ポイントをホストしているサイトは、アップグレードできません。  

ソフトウェアの更新ポイントに NLB クラスターを使用している場合、PowerShell を使用して NLB クラスターを削除してください (System Center 2012 Configuration Manager SP1 以降、Configuration Manager に NLB クラスターを構成するためのオプションはありません)。  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>サイトのアップグレード時に各サイトですべてのサイト メンテナンス タスクを無効にする

Configuration Manager にアップグレードする前に、アップグレード プロセスがアクティブになっている間にそのサイトで実行される可能性があるサイトのメンテナンス タスクをすべて無効にします。 次の一覧のタスクが含まれますが、これらだけではありません。  

- サイト サーバーのバックアップ  
- 期限切れのクライアント操作を削除  
- 期限切れの探索データの削除  

アップグレード プロセス中にサイト データベースのメンテナンス タスクが実行されると、サイトのアップグレードが失敗する可能性があります。  

タスクを無効にする前に、サイトのアップグレードが完了した後で構成を復元できるように、タスクのスケジュールを記録してください。

サイト メンテナンス タスクの詳細については、以下の記事をご覧ください。  

- System Center 2012 Configuration Manager:[サイト運用の計画](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager、Current Branch: [メンテナンス タスクのリファレンス](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>セットアップ前提条件チェッカーを実行する

サイトをアップグレードする前に、セットアップとは別に**前提条件チェッカー**を実行して、サイトが前提条件を満たしていることを検証します。 後でサイトをアップグレードしたときに、前提条件チェッカーが再度実行されます。  

個別の前提条件チェックにより、Configuration Manager の Current Branch と Long-Term Servicing Branch (LTSB) の両方にアップグレードするためにサイトが評価されます。 LTSB でサポートされていない機能がいくつかあるため、次の例のようなエントリが **ConfigMgrPrereq.log** に表示される場合があります。

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Current Branch にアップグレードする予定の場合は、LTSB エディションに関するエラーは無視してかまいません。 これらは、LTSB にアップグレードする予定の場合にのみ当てはまります。

後で、Configuration Manager のセットアップを実行してアップグレードを行うときに、前提条件チェックが再度実行されます。 そこでは、インストールすることを選択した Configuration Manager のブランチ (Current branch または LTSB) に基づいて、サイトが評価されます。 Current Branch にアップグレードする場合は、LTSB でサポートされていない機能のチェックは実行されません。

詳しくは、[前提条件チェッカー](prerequisite-checker.md)および[前提条件の確認の一覧](list-of-prerequisite-checks.md)に関する記事をご覧ください。  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Configuration Manager の前提条件ファイルと再頒布可能ファイルをダウンロードする

**セットアップ ダウンローダー**を使って、Configuration Manager の前提条件の再頒布可能ファイル、言語パック、製品の最新の更新プログラムをダウンロードします。  

詳細については、「[セットアップ ダウンローダー](setup-downloader.md)」を参照してください。  

#### <a name="plan-to-manage-server-and-client-languages"></a>サーバーとクライアントの言語の管理を計画する

サイトのアップグレード時には、アップグレード中に選択した言語パックのバージョンのみがインストールされます。  

- セットアップでは、サイトの現在の言語構成が確認されます。 その後、事前にダウンロードされた前提条件ファイルが保存されているフォルダー内の使用可能な言語パックが識別されます。  

- 現在のサーバー言語パックとクライアント言語パックの選択を確認したり、言語のサポートを追加または削除するように選択を変更したりできます。  

- セットアップの実行時に使用できる言語パックのみを選択できます。  

> [!NOTE]  
> System Center 2012 Configuration Manager の言語パックを使用して、Configuration Manager Current Branch のサイトで言語を有効にすることはできません。  

言語パックについて詳しくは、[言語パック](language-packs.md)に関する記事をご覧ください。  

#### <a name="review-considerations-for-site-upgrades"></a>サイトのアップグレードに関する考慮事項を確認する

サイトをアップグレードすると、一部の機能と構成が既定の構成にリセットされます。 この点と、関連する変更に備えるには、「[アップグレード時の考慮事項](#bkmk_considerations)」をご覧ください。  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>中央管理サイトとプライマリ サイトのサイト データベースのバックアップを作成する

サイトをアップグレードする前に、サイト データベースをバックアップして、ディザスター リカバリーに使用するバックアップを正常に作成できることを確認します。  

詳細については、「[バックアップと回復](../../manage/backup-and-recovery.md)」を参照してください。  

#### <a name="back-up-a-customized-configurationmof-file"></a>カスタマイズされた configuration.mof ファイルをバックアップする

ハードウェア インベントリで使用するデータ クラスを定義するためにカスタマイズされた configuration.mof ファイルを使用する場合は、このファイルのバックアップを作成します。 アップグレード後に、このファイルをサイトに復元します。 詳しくは、[ハードウェア インベントリの構成方法](../../../clients/manage/inventory/extend-hardware-inventory.md)に関するページをご覧ください。  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>最新のサイト データベース バックアップのコピーで、データベースのアップグレード処理をテストする

Configuration Manager の中央管理サイトやプライマリ サイトをアップグレードする前に、サイト データベースのコピーでサイト データベースのアップグレード処理をテストします。  

- サイト データベースのアップグレード プロセスをテストします。 サイトをアップグレードするとき、サイト データベースが変更されることがあります。  

- データベースのアップグレードのテストは必須ではありませんが、テストによって、実稼働データベースが影響を受ける前に、アップグレードの問題を特定することができます  

- サイト データベースのアップグレードに失敗すると、サイト データベースが運用不可能になり、機能を復元するにはサイトの回復が必要になることがあります  

- サイト データベースは階層内のサイト間で共有されますが、各サイトをアップグレードする前に、該当する各サイトのデータベースをテストする計画を立ててください  

- プライマリ サイトで管理ポイントにデータベース レプリカを使う場合、サイト データベースのバックアップを作成する前にレプリケーションを無効にします  

Configuration Manager では、セカンダリ サイトのバックアップとセカンダリ サイト データベースのテスト アップグレードのいずれもサポートされていません。  

運用サイト データベースでテスト データベースのアップグレードを実行することはサポートされていません。 実行するとサイト データベースがアップグレードされ、サイトが機能しなくなる可能性があります。  

詳細については、「 [サイト データベースのアップグレードをテストする](#bkmk_test)」をご覧ください。  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>サイト システムの役割をホストするサイト サーバーと各コンピューターを再起動する

これを実行して、更新プログラムの最近のインストールまたは前提条件から保留中のアクションがないことを確認します。  

#### <a name="upgrade-sites"></a>サイトをアップグレードする

まず、階層内の最上位サイトで、Configuration Manager ソース メディアから Setup.exe を実行します。  

最上位サイトのアップグレードが完了したら、各子サイトのアップグレードを開始できます。 各サイトのアップグレードが完了してから、次のサイトのアップグレードを開始します。  

階層内のすべてのサイトが Configuration Manager にアップグレードされるまで、階層はバージョンが混在したモードで動作します。  

アップグレードを実行する方法については、「[サイトをアップグレードする](#bkmk_upgrade)」を参照してください。  

### <a name="after-you-upgrade"></a>アップグレードの後に  

Configuration Manager にアップグレードした後、以下の手順を確認します。

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>スタンドアロンの Configuration Manager コンソールをアップグレードする

既定では、中央管理サイトまたはプライマリ サイトをアップグレードすると、インストール時にサイト サーバーにインストールされている Configuration Manager コンソールもアップグレードされます。 サイト サーバー以外のコンピューターにインストールされている各コンソールは、手動でアップグレードします。  

> [!TIP]  
> アップグレードを開始する前に、開いているコンソールを閉じてください。  

詳しくは、「[System Center Configuration Manager コンソールをインストールする](install-consoles.md)」をご覧ください。  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>プライマリ サイトで管理ポイント用のデータベース レプリカを再構成する

プライマリ サイトで管理ポイント用のデータベース レプリカを使用する場合、データベース レプリカをアンインストールしてから、サイトをアップグレードします。 プライマリ サイトをアップグレードしたら、管理ポイント用のデータベース レプリカを再構成します。

詳細については、「[管理ポイントのデータベース レプリカ](../configure/database-replicas-for-management-points.md)」を参照してください。  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>アップグレードの前に無効にしたデータベース メンテナンス タスクを再構成する

アップグレードの前にサイトのデータベース [メンテナンス タスク](../../manage/reference-for-maintenance-tasks.md)を無効にした場合、アップグレードの前に使用していたのと同じ設定を使用して、サイトでこれらのタスクを再構成します。  

#### <a name="upgrade-clients"></a>クライアントをアップグレードする

すべてのサイトを Configuration Manager にアップグレードした後、クライアントのアップグレードを計画します。  

クライアントをアップグレードすると、現在のクライアント ソフトウェアはアンインストールされ、新しいクライアント ソフトウェア バージョンがインストールされます。 クライアントのアップグレードには、Configuration Manager がサポートするどの方法でも使うことができます。  

> [!TIP]  
> 最上位サイトの階層をアップグレードすると、その階層内の各配布ポイントにあるクライアント インストール パッケージも更新されます。 プライマリ サイトをアップグレードすると、そのプライマリ サイトから使用できるクライアント アップグレード パッケージが更新されます。  

詳細については、「[Windows コンピューター用クライアントをアップグレードする方法](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)」を参照してください。  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a> アップグレード時の考慮事項  

### <a name="automatic-actions"></a>自動アクション

Configuration Manager にアップグレードすると、自動的に次のアクションが行われます。  

- サイトのリセット。 これには、すべてのサイト システムの役割の再インストールが含まれます。  

- サイトが階層の最上位サイトの場合、その階層内の各配布ポイントでクライアント インストール パッケージが更新されます。 また、Windows アセスメント & デプロイメント キット 10 に含まれている新しい Windows PE バージョンを使うように、サイトで既定のブート イメージが更新されます。 ただし、アップグレードでは、イメージの展開で使用するための既存のメディアはアップグレードされません。  

- サイトがプライマリ サイトの場合、そのサイトのクライアント アップグレード パッケージが更新されます。  

### <a name="manual-actions-after-an-upgrade"></a>アップグレード後の手動操作

サイトをアップグレードした後、必ず次の操作を実行してください。  

- 各プライマリ サイトに割り当てられているクライアントがアップグレードされ、新しいバージョンのクライアントがインストールされていることを確認します  

- サイトに接続し、サイト サーバーのリモート コンピューターで実行されている各 Configuration Manager コンソールをアップグレードします。  

- 管理ポイント用にデータベース レプリカを使うプライマリ サイトで、データベース レプリカを再構成します。  

- サイトをアップグレードした後、CD、DVD、または USB フラッシュ ドライブの ISO ファイルなど、物理メディアを手動でアップグレードします。 それには、ハードウェア ベンダーに提供された事前設定されたメディアも含まれます。 サイトのアップグレードでは、既定のブート イメージが更新されますが、これらのメディア ファイルや外部で使用されたデバイスを Configuration Manager にアップグレードすることはできません。  

- 古いバージョンの Windows PE が必要ないときは、カスタム ブート イメージの更新を計画してください。  

### <a name="actions-that-affect-configurations-and-settings"></a>構成と設定に影響がある操作

サイトを Configuration Manager にアップグレードするとき、一部の構成と設定はアップグレード後に維持されません。 一部の構成は新しい既定値に設定されます。 次の一覧は、維持されない設定または変更される設定です。  

- **ソフトウェア センター**  
    次のソフトウェア センター項目が既定値にリセットされます。  

  - **[勤務先情報]** は、月曜日から金曜日の**午前 5 時**から**午後 10 時**の営業時間にリセットされます。  

  - **[コンピューターのメンテナンス]** の値は **[コンピューターがプレゼンテーション モードのときはソフトウェア センターを停止する]** に設定されます。  

  - **[リモート コントロール]** の値は、そのコンピューターに割り当てられているクライアント設定の値に設定されます。  

- **ソフトウェア更新プログラムの概要作成スケジュール**: ソフトウェア更新プログラムやソフトウェア更新プログラム グループ用のカスタムの概要スケジュールは、1 時間という既定値にリセットされます。 アップグレードが完了した後に、カスタムの概要値を目的の頻度にリセットしてください。  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a> サイト データベースのアップグレードをテストする  

次の情報は、System Center 2012 Configuration Manager などの以前のバージョンを Configuration Manager の Current Branch にアップグレードする場合にのみ適用されます。

サイトをアップグレードする前に、そのサイトのデータベースのコピーでアップグレードをテストします。  

データベースでアップグレードをテストするために、まず、サイト データベースのコピーを Configuration Manager サイトをホストしていない SQL Server インスタンスに復元します。 データベースのコピーをホストするのに使用している SQL Server のバージョンが、Configuration Manager でサポートされている SQL Server のバージョンである必要があります。  

サイト データベースを復元した後、SQL Server コンピューターで、Configuration Manager 用のソース メディア フォルダーから、Configuration Manager のセットアップを実行します。 `/TESTDBUPGRADE` コマンド ライン オプションを使用します。  

詳細については、以下の記事を参照してください。

- [Configuration Manager サイトのバックアップ](../../manage/backup-and-recovery.md)  

- [セットアップに使用されるコマンドライン オプション](command-line-options-for-setup.md#bkmk_setup)  

- [SQL Server バージョンのサポート](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Microsoft Intune と Configuration Manager を統合する場合:  
>
> 5 日以上前のサイト データベースのコピーに対してデータベース アップグレードのテストを実行すると、次のいずれかのメッセージを受け取ることがあります:  
>
> - 警告:アップグレードするとクラウドへの完全同期が実行されます。  
> - エラー: データベースをアップグレードするとクラウドへの完全同期が実行されます。  
>
> データベース アップグレードのテスト中は、どちらも無視してかまいません。 テスト アップグレードの失敗や問題を示すものではありません。 これは、実際のアップグレード中に **Cloud** データベース レプリケーション グループからのデータが Microsoft Intune と同期される可能性があることを示しています。  

### <a name="test-a-site-database-for-upgrade"></a>サイト データベースのアップグレードをテストする  

アップグレードを計画している各中央管理サイトとプライマリ サイトで、以下の手順に従います。  

1. サイト データベースのコピーを作成します。 その後、サイト データベースと同じエディションを使用しており、Configuration Manager サイトをホストしていない SQL Server インスタンスにこのコピーを復元します。 たとえば、サイト データベースで SQL Server Enterprise Edition のインスタンスを実行している場合、同様に SQL Server Enterprise Edition を実行している SQL Server インスタンスにデータベースを復元します。  

2. データベースのコピーを復元した後で、新しいバージョンの Configuration Manager Current Branch のソース メディアからセットアップを実行します。 セットアップを実行する際は、`/TESTDBUPGRADE` コマンド ライン オプションを使用します。 データベースのコピーをホストする SQL Server インスタンスが既定のインスタンスでない場合は、コマンドライン引数を指定して、サイト データベースのコピーをホストするインスタンスも示します。  

    たとえば、SMS_ABC というデータベース名のサイト データベースをアップグレードすることを計画しているとします。 このサイト データベースのコピーを、DBTest というインスタンス名のサポートされている SQL Server インスタンスに復元します。 サイト データベースのこのコピーのアップグレードをテストするには、次のコマンド ラインを使用します: `Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Setup.exe は、Configuration Manager ソース メディアの次の場所にあります: `SMSSETUP\BIN\X64`  

3. データベースのアップグレード テストを実行する SQL Server インスタンスで、システム ドライブのルート内の ConfigMgrSetup.log を確認し、進行状況と成功状態を監視します。  

    - アップグレード テストに失敗した場合は、サイト データベースのアップグレード失敗に関する問題をすべて解決します。 次に、サイト データベースの新しいバックアップを作成し、サイト データベースの新しいコピーのアップグレードをテストします。  

    - プロセスが成功したら、データベース コピーを削除できます。  

        > [!NOTE]  
        > テスト アップグレードに使用したサイト データベースのコピーを復元して、任意のサイトのサイト データベースとして使用することはサポートされていません。  

サイト データベースのコピーのアップグレードが成功したら、Configuration Manager サイトとそのサイト データベースのアップグレードを続けます。  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a> サイトをアップグレードする  

以下のタスクを完了すると、Configuration Manager サイトをアップグレードする準備ができます。

- サイトのアップグレード前の構成
- データベース コピーでのサイト データベースのアップグレードのテスト
- インストールを計画しているバージョンの前提条件ファイルと言語パックのダウンロード

階層内のサイトをアップグレードする際、まず、階層の最上位サイトをアップグレードします。 この最上位サイトは、中央管理サイトまたはスタンドアロンのプライマリ サイトのいずれかです。 中央管理サイトのアップグレードが完了した後で、任意の順序で子プライマリ サイトをアップグレードできます。 プライマリ サイトをアップグレードした後で、そのサイトの子セカンダリ サイトをアップグレードするか、セカンダリ サイトをアップグレードする前に他のプライマリ サイトをアップグレードできます。  

中央管理サイトやプライマリ サイトをアップグレードするには、Configuration Manager のソース メディアからセットアップを実行します。 Setup を実行してセカンダリ サイトをアップグレードしないでください。 代わりに、プライマリ親サイトのアップグレードが完了した後で、Configuration Manager コンソールを使用してセカンダリ サイトをアップグレードします。  

サイトをアップグレードする前に、サイトのアップグレードが完了するまで、サイト サーバーの Configuration Manager コンソールを閉じます。 また、サイト サーバー以外のコンピューターで実行されている各 Configuration Manager コンソールも閉じます。 サイトのアップグレードが完了した後で、コンソールを再接続できます。 ただし、Configuration Manager コンソールを新しいバージョンの Configuration Manager にアップグレードするまで、新しいバージョンの Configuration Manager で使用できる一部のオブジェクトと情報をコンソールに表示できません。  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>中央管理サイトまたはプライマリ サイトをアップグレードする  

1. セットアップを実行するユーザーが、次のセキュリティ権限を持っていることを確認します。  

    - サイト サーバーでのローカル**管理者**権限  

    - サイト データベース サーバーがサイト サーバーからリモートの場合は、そこでのローカル**管理者**権限。  

2. サイト サーバーで、プログラム `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe` を開きます。 これにより、Configuration Manager のセットアップ ウィザードが起動します。  

3. **[開始する前に]** ページの情報を読んだ後、 **[次へ]** を選択します。  

4. **[作業の開始]** ページで **[Upgrade this Configuration Manager site]\(この Configuration Manager サイトをアップグレードする\)** を選択して、 **[次へ]** を選択します。  

5. **[プロダクト キー]** ページでの操作:  

    以前に Configuration Manager 評価版をインストールした場合は、 **[Install the licensed edition of this product]\(この製品の製品版をインストールする\)** を選択できます。 その後、Configuration Manager の完全インストールのプロダクト キーを入力します。 これにより、サイトが完全バージョンに変換されます。  

    ライセンス契約の**ソフトウェア アシュアランスの有効期限**を、その日を通知する便利なアラームとして指定することもできます。 セットアップ時にこの値を入力しなかった場合は、後で Configuration Manager コンソール内から指定できます。  

    > [!NOTE]  
    > Microsoft では、お客様が入力した有効期限の日付を確認していません。また、ライセンスを検証する場合もこの日付を使用しません。 この日付は、有効期限のリマインダーとして使用できます。 Configuration Manager ではオンラインで提供される新しいソフトウェア更新プログラムが定期的に確認され、そのような追加の更新プログラムを使用できるためには、ソフトウェア アシュアランス ライセンスが最新の状態になっている必要があります。

    詳細については、[ライセンスとブランチの詳細](../../../understand/learn-more-editions.md)に関するページを参照してください。

6. **[マイクロソフト ソフトウェア ライセンス条項]** ページで、ライセンス条項を読んで同意し、 **[次へ]** を選択します。  

7. **[必須ライセンス]** ページで、必須ソフトウェアのライセンス条項を読んで同意し、 **[次へ]** を選択します。 ソフトウェアがダウンロードされ、必要に応じて、サイト システムまたはクライアントに自動的にインストールされます。 次のページに進むには、すべての条項に同意する必要があります。  

8. **[必須ファイルのダウンロード]** ページで、インターネットから最新のコンテンツをダウンロードするか、以前にダウンロードしたファイルを使用するかを指定します。 このコンテンツには、前提条件の再頒布可能ファイル、言語パック、製品の最新の更新プログラムが含まれます。 セットアップ ダウンローダーを使用して既にファイルをダウンロードしている場合は、 **[ダウンロード済みのファイルを使用する]** を選択して、ダウンロード先フォルダーを指定します。 詳細については、「[セットアップ ダウンローダー](setup-downloader.md)」を参照してください。  

    > [!NOTE]  
    > 前にダウンロードしたファイルを使用する場合は、ダウンロード先フォルダーに、最新バージョンのファイルが含まれていることを確認してください。  

9. **[サーバーの言語の選択]** ページで、サイトに現在インストールされている言語の一覧を表示します。 このサイトで Configuration Manager コンソールとレポートに使用できる追加の言語を選択します。 このサイトでサポートする必要がなくなった言語をクリアすることもできます。 既定では英語が選択され、選択を解除することはできません。  

    > [!IMPORTANT]  
    > Configuration Manager の各バージョンで、以前のバージョンの Configuration Manager の言語パックは使用できません。 アップグレードする Configuration Manager サイトで言語のサポートを有効にするには、その新しいバージョンの言語パック バージョンを使用する必要があります。 たとえば、System Center 2012 Configuration Manager から Configuration Manager の Current Branch へのアップグレード中に、Current Branch バージョンの言語パックが、ダウンロードした前提条件ファイルで使用できない場合、その言語のサポートをインストールすることはできません。  

10. **[クライアント言語の選択]** ページで、サイトに現在インストールされている言語の一覧を表示します。 このサイトでクライアント コンピューターに使用できるようにする追加の言語を選択するか、このサイトでサポートする必要がなくなった言語をクリアします。 モバイル デバイス クライアントのすべてのクライアント言語を有効にするかどうかを指定して、 **[次へ]** をクリックします。 既定では英語が選択され、選択を解除することはできません。  

11. **[設定の概要]** ページで、構成を確認します。 準備ができたら、 **[次へ]** を選択して前提条件チェッカーを起動し、サイトをアップグレードするサーバーの準備ができているかどうかを確認します。  

12. **[インストールの前提条件チェック]** ページに問題が何も表示されていない場合は、 **[次へ]** を選択して、プライマリ サイトとサイト システムの役割をアップグレードします。

    前提条件チェッカーで問題が見つかった場合は、一覧で項目を選択し、問題の解決方法の詳細を確認します。 セットアップを続行する前に、一覧内でステータスが **[エラー]** になっているすべての問題を解決します。 問題を解決したら、 **[前提条件チェックの実行]** をクリックして、もう一度前提条件チェックを実行します。 システム ドライブのルートにある ConfigMgrPrereq.log ファイルを開いて、前提条件チェッカーの結果を確認することもできます。 ログ ファイルには、ユーザー インターフェイスに表示されていない情報が含まれていることがあります。 インストールの前提条件チェックの規則と説明の一覧については、「[前提条件チェッカー](list-of-prerequisite-checks.md)」を参照してください。

**[アップグレード]** ページに、進行状況の全体的なステータスが表示されます。 コア サイト サーバーとサイト システムのインストールが完了したら、ウィザードを閉じることができます。 サイトの構成がバックグラウンドで続行されます。  

### <a name="upgrade-a-secondary-site"></a>セカンダリ サイトをアップグレードする  

1. セットアップを実行する管理ユーザーが、次のセキュリティ権限を持っていることを確認します。  

    - セカンダリ サイト サーバーでのローカル**管理者**権限  

    - 親プライマリ サイトでの**インフラストラクチャ管理者**または**完全な権限を持つ管理者**のセキュリティ ロール  

    - セカンダリ サイトでのサイト データベースのシステム管理者 (**SA**) の権限  

2. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開してから **[サイト]** ノードを選択します。  

3. アップグレードするセカンダリ サイトを選択します。 リボンの **[ホーム]** タブの **[サイト]** グループで、 **[アップグレード]** を選択します。  

4. **[はい]** を選択して決定を確認し、セカンダリ サイトのアップグレードを開始します。  

セカンダリ サイトのアップグレードは、バックグラウンドで実行されます。 アップグレードが完了した後、Configuration Manager コンソールで状態を確認します。 セカンダリ サイト サーバーを選択し、リボンの **[ホーム]** タブの **[サイト]** グループで、 **[インストール ステータスの表示]** を選択します。  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a> アップグレード後のタスク  

サイトをアップグレードした後、サイトのアップグレードまたは再構成を終了するために、追加のタスクを完了することが必要になる場合があります。 これらのタスクには、次のものが含まれます。

- Configuration Manager クライアントをアップグレードする
- Configuration Manager コンソールをアップグレードする
- 管理ポイントのデータベース レプリカを再度有効にする
- 使用する Configuration Manager の機能でアップグレード後に維持されない設定を復元する  
