---
title: ソフトウェア更新プログラムのメンテナンス
titleSuffix: Configuration Manager
description: Configuration Manager の更新プログラムをメンテナンスするには、WSUS クリーンアップ タスクをスケジュールするか、手動で実行します。
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 560b432bb90f99207fd15bc07e7aff98ffd59ebf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703010"
---
# <a name="software-updates-maintenance"></a>ソフトウェア更新プログラムのメンテナンス

*適用対象:Configuration Manager (Current Branch)*

WSUS クリーンアップ タスクは、Configuration Manager コンソールから、またはソフトウェアの更新ポイント コンポーネントのプロパティから、スケジュールして実行することができます。 最初に WSUS クリーンアップ タスクを実行することを選ぶと、次回から、ソフトウェア更新プログラムを最新に保つときにこのタスクが実行されます。  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>WSUS クリーンアップ ジョブをスケジュールし、実行するには

次の手順を行い、WSUS クリーンアップ ジョブをスケジュールします。

1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[サイト構成]**  >  **[サイト]** の順に移動します。
2. Configuration Manager 階層の最上位サイトを選択します。

3. **[設定]** グループで **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** をクリックして、ソフトウェアの更新ポイント コンポーネントのプロパティを開きます。  

4. **更新プログラムが置き換えられる場合の処理**を確認します。 必要に応じて処理を変更します。

   ![更新プログラムが置き換えられる場合の処理のスクリーンショット](media/supersedence-behavior.png)

5. **[置き換えの規則]** タブをクリックし、 **[WSUS クリーンアップ ウィザードの実行]** を選びます。 バージョン 1806 では、オプションの名前が **[Run WSUS cleanup after synchronization]\(同期後に WSUS クリーンアップを実行する\)** に変更されています。

6. **[OK]** (バージョン 1806 を実行している場合は、 **[閉じる]** ) をクリックします。

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>バージョン 1802 以前の WSUS クリーンアップの動作

Configuration Manager バージョン 1806 より前のバージョンでは、WSUS クリーンアップ オプションで次の項目が実行されます。

- WSUS クリーンアップ ウィザードの **[期限切れの更新プログラム]** オプションは、最上位サイトの WSUS サーバーでのみ実行されます。

  ![WSUS 期限切れの更新プログラムのクリーンアップのスクリーンショット](media/wsus-cleanup-expired.PNG)

- Configuration Manager データベースでのソフトウェアの更新プログラムの構成アイテムのクリーンアップは、7 日ごとに実行され、コンソールから不要な更新プログラムが削除されます。
  - このクリーンアップでは、期限切れの更新プログラムが現在展開されている場合には、その更新プログラムは Configuration Manager コンソールから削除されません。

最上位の WSUS データベースと環境内の他のすべての WSUS データベースには、追加のメンテナンスが引き続き必要です。 詳細と手順については、ブログ記事「[The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/)」 (Microsoft WSUS と Configuration Manager SUP のメンテナンスの完全ガイド) を参照してください。

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>バージョン 1806 以降の WSUS クリーンアップ動作

バージョン 1806 以降では、WSUS クリーンアップのオプションは同期の後に毎回実行され、次のクリーンアップ項目を実行します。
<!--1357898 -->

- CAS およびプライマリ サイトでの WSUS サーバーの **[期限切れの更新プログラム]** オプション。
  - セカンダリ サイトの WSUS サーバーでは、期限切れの更新プログラムに対して WSUS のクリーンアップは実行されません。
- Configuration Manager により、そのデータベースから置き換えられる更新プログラムのリストがビルドされます。 このリストは、ソフトウェアの更新ポイント コンポーネントのプロパティの置き換え動作に基づきます。
  - 置き換えの動作条件を満たす更新プログラムの構成項目は、Configuration Manager コンソールでは期限切れです。
  - 更新プログラムは、CAS とプライマリ サイトの WSUS では拒否されますが、セカンダリ サイトの WSUS では拒否されません。
- Configuration Manager データベースでのソフトウェアの更新プログラムの構成アイテムのクリーンアップは、7 日ごとに実行され、コンソールから不要な更新プログラムが削除されます。
  - このクリーンアップでは、期限切れの更新プログラムが現在展開されている場合には、その更新プログラムは Configuration Manager コンソールから削除されません。

> [!NOTE]
> "置き換えられる更新プログラムが期限切れになるまで待機する月数"は、置き換える更新プログラムの作成日に基づきます。 たとえば、この設定を 2 か月にすると、置き換える更新プログラムが 2 か月経過した時に、置き換えられた更新プログラムは WSUS で拒否され、Configuration Manager で期限切れになります。

すべての WSUS メンテナンスは、セカンダリ サイトの WSUS データベース上で手動で実行する必要があります。 次の **WSUS サーバー クリーンアップ ウィザード**のオプションは、CAS とプライマリ サイトでは実行されません。

- 使用されていない更新プログラムと更新プログラムのリビジョン
- サーバーに接続しないコンピューター
- 不要な更新ファイル

  詳細と手順については、ブログ記事「[The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/)」 (Microsoft WSUS と Configuration Manager SUP のメンテナンスの完全ガイド) を参照してください。

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>バージョン 1810 以降の WSUS クリーンアップ動作

バージョン 1810 以降では、ソフトウェアの更新ポイント コンポーネントのプロパティで、機能以外の更新プログラムとは別に、機能更新プログラムに対して置き換え規則を指定できます。 WSUS クリーンアップのオプションは同期の後に毎回実行され、次のクリーンアップ項目を実行します。
<!--2839349,3098809, 2977644-->

- CAS、プライマリ サイト、セカンダリ サイトでの WSUS サーバーの **[期限切れの更新プログラム]** オプション。
- Configuration Manager により、そのデータベースから置き換えられる更新プログラムのリストがビルドされます。 このリストは、ソフトウェアの更新ポイント コンポーネントのプロパティの置き換え動作に基づきます。
  - 置き換えの動作条件を満たす更新プログラムの構成項目は、Configuration Manager コンソールでは期限切れです。
  - 更新プログラムは、CAS、プライマリ サイト、セカンダリ サイトの WSUS で拒否されます。
- Configuration Manager データベースでのソフトウェアの更新プログラムの構成アイテムのクリーンアップは、7 日ごとに実行され、コンソールから不要な更新プログラムが削除されます。
  - このクリーンアップでは、期限切れの更新プログラムが現在展開されている場合には、その更新プログラムは Configuration Manager コンソールから削除されません。

> [!NOTE]
> "置き換えられる更新プログラムが期限切れになるまで待機する月数"は、置き換える更新プログラムの作成日に基づきます。 たとえば、この設定を 2 か月にすると、置き換える更新プログラムが 2 か月経過した時に、置き換えられた更新プログラムは WSUS で拒否され、Configuration Manager で期限切れになります。

次の **WSUS サーバー クリーンアップ ウィザード**のオプションは、CAS、プライマリ サイト、セカンダリ サイトでは実行されません。

- 使用されていない更新プログラムと更新プログラムのリビジョン
- サーバーに接続しないコンピューター
- 不要な更新ファイル

  詳細と手順については、ブログ記事「[The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/)」 (Microsoft WSUS と Configuration Manager SUP のメンテナンスの完全ガイド) を参照してください。

## <a name="wsus-cleanup-starting-in-version-1906"></a>バージョン 1906 以降の WSUS クリーンアップ
<!--41101009-->

 ソフトウェアの更新ポイントの正常性を維持するために Configuration Manager で実行できる、WSUS メンテナンス タスクが追加されました。 WSUS で更新が期限切れになる事態を減らすだけでなく、Configuration Manager では、WSUS データベースに非クラスター化インデックスを追加すること、および WSUS データベースから古い更新プログラムを削除することができます。 WSUS のメンテナンスは、各同期後に行われます。

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>置き換え規則に従って、WSUS で期限切れの更新プログラムを拒否する

WSUS で更新プログラムを拒否すると、クライアントに送信されるカタログからそれらの更新プログラムを削除することで、パフォーマンスが向上します。 Configuration Manager によって置き換え済みとしてマークされている更新プログラムを拒否すると、さらにカタログが最小化され、パフォーマンスが向上します。

1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[サイト構成]**  >  **[サイト]** の順に移動します。
2. Configuration Manager 階層の最上位サイトを選択します。
3. [設定] グループで **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** をクリックして、ソフトウェアの更新ポイント コンポーネントのプロパティを開きます。
4. **[WSUS メンテナンス]** タブで、 **[Decline expired updates in WSUS according to supersedence rules]\(置き換え規則に従って、WSUS で期限切れの更新プログラムを拒否する\)** を選択します。

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>WSUS データベースに非クラスター化インデックスを追加して、WSUS のクリーンアップのパフォーマンスを向上させる

非クラスター化インデックスを追加すると、Configuration Manager が行う WSUS クリーンアップのパフォーマンスが向上します。

1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[サイト構成]**  >  **[サイト]** の順に移動します。
2. Configuration Manager 階層の最上位サイトを選択します。
3. [設定] グループで **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** をクリックして、ソフトウェアの更新ポイント コンポーネントのプロパティを開きます。
4. **[WSUS メンテナンス]** タブで **[Add non-clustered indexes to the WSUS database]\(WSUS データベースに非クラスター化インデックスを追加する\)** を選択します。
5. Configuration Manager で使用される SUSDB ごとに、インデックスが次のテーブルに追加されます。
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>インデックスを作成するための SQL アクセス許可

WSUS データベースがリモートの SQL サーバー上にある場合は、インデックスを作成するために SQL でのアクセス許可を追加することが必要になる場合があります。 WSUS データベースへの接続に使用するアカウントとインデックスの作成に使用するアカウントは、異なる場合があります。 [ソフトウェアの更新ポイントのプロパティで WSUS サーバー接続アカウント](../get-started/install-a-software-update-point.md#wsus-server-connection-account)を指定する場合は、接続アカウントに SQL アクセス許可があることを確認します。 WSUS サーバー接続アカウントを指定しない場合は、サイト サーバーのコンピューター アカウントに SQL アクセス許可が必要です。

- インデックスを作成するためには、テーブルまたはビューに対する `ALTER` アクセス許可が必要です。 アカウントは、`sysadmin` 固定サーバー ロールか、`db_ddladmin` および `db_owner` 固定データベース ロールのメンバーである必要があります。 インデックスの作成とアクセス許可について詳しくは、[CREATE INDEX (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions) に関する記事をご覧ください。
- アカウントには、`CONNECT SQL` サーバー アクセス許可が付与されている必要があります。 詳細については、「[GRANT (サーバーの権限の許可) (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017)」をご覧ください。

> [!NOTE]  
>  既定以外のポートを使用するリモート SQL サーバー上に WSUS データベースがある場合、インデックスは追加されないことがあります。 このシナリオには、[SQL Server Configuration Manager を使用してサーバー エイリアス](https://docs.microsoft.com/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017)を作成できます。 エイリアスが追加され、Configuration Manager で WSUS データベースに接続できるようになると、インデックスが追加されます。

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>WSUS データベースから古い更新プログラムを削除する

古い更新プログラムは、WSUS データベース内の使用されていない更新プログラムと更新プログラムのリビジョンです。 一般に、更新プログラムは、[Microsoft Update カタログ](https://www.catalog.update.microsoft.com/)に存在しなくなった場合には廃止されたと見なされ、他の更新プログラムで前提条件または依存関係として必要になることはありません。

1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[サイト構成]**  >  **[サイト]** の順に移動します。
2. Configuration Manager 階層の最上位サイトを選択します。
3. [設定] グループで **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** をクリックして、ソフトウェアの更新ポイント コンポーネントのプロパティを開きます。
4. **[WSUS Maintenance]\(WSUS メンテナンス\)** タブで、 **[Remove obsolete updates from the WSUS database]\(WSUS データベースから古い更新プログラムを削除する\)** を選択します。
   - 古い更新プログラムの削除は、停止されるまで最長 30 分間実行できます。 これは、次の同期が行われた後に再び開始されます。  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>古い更新プログラムを削除するための SQL アクセス許可

WSUS データベースがリモートの SQL サーバー上にある場合、サイト サーバーのコンピューター アカウントには SQL に関する次のアクセス許可が必要です。

- `db_datareader` および `db_datawriter` 固定データベース ロール。 詳細については、[データベース レベルのロール](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles)に関する記事をご覧ください。
- サイト サーバーのコンピューター アカウントに `CONNECT SQL` サーバー アクセス許可を付与する必要があります。 詳細については、「[GRANT (サーバーの権限の許可) (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017)」をご覧ください。

#### <a name="wsus-cleanup-wizard"></a>WSUS クリーンアップ ウィザード

バージョン 1906 以降では、次の **WSUS サーバー クリーンアップ ウィザード**のオプションは、CAS、プライマリ サイト、セカンダリ サイトでは実行されません。

- サーバーに接続しないコンピューター
- 不要な更新ファイル

  詳細と手順については、ブログ記事「[The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/)」 (Microsoft WSUS と Configuration Manager SUP のメンテナンスの完全ガイド) を参照してください。


### <a name="known-issues-for-version-1906"></a>バージョン 1906 の既知の問題

次のシナリオを想定してください。
<!--5418148-->
- Configuration Manager バージョン 1906 を使用している
- Windows Internal Database を使用するリモートのソフトウェアの更新ポイントがある
- **[ソフトウェアの更新ポイント コンポーネントのプロパティ]** の **[WSUS メンテナンス]** タブに、選ばれた次のいずれかのオプションが表示されます。
   - 非クラスター化インデックスを WSUS データベースに追加する
   - WSUS データベースから古い更新プログラムを削除する

このシナリオでは、Windows Internal Database を使用するリモートのソフトウェアの更新ポイントに対して、Configuration Manager によって上記の WSUS メンテナンス タスクを実行することはできません。 この問題は、Windows Internal Database でリモート接続が許可されていないために発生します。 サイト サーバーの `WSyncMgr.log` に次のエラーが表示されます。

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

この問題を回避するには、Windows Internal Database を使用して、リモートのソフトウェアの更新ポイントに対する WSUS メンテナンスを自動化します。 詳細と詳しい手順については、「[Microsoft WSUS および構成マネージャー SUPメンテナンスの完全なガイド](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)」をご覧ください。

## <a name="updates-cleanup-log-entries"></a>更新プログラムのログ エントリのクリーンアップ

このクリーンアップは、次のエントリの wsyncmgr.log で確認することができます。

- このログ エントリが表示されたら、WSUS での置き換えられる更新プログラムの拒否は完了です。`Cleanup processed <number> total updates and declined <number>`
- このエントリが表示されたら、WSUS クリーンアップは開始しています。`Calling WSUS Cleanup.`
- このエントリが表示されたら、期限切れの更新プログラムの WSUS のクリーンアップは完了です。`Successfully completed WSUS Cleanup.`
- このエントリが表示されたら、Configuration Manager の期限切れの更新プログラムの構成アイテムのクリーンアップが開始しています。`Deleting old expired updates...`
- このエントリが表示されたら、Configuration Manager の期限切れの更新プログラムの構成アイテムのクリーンアップは完了です。`Deleted <number> expired updates total`
