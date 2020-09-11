---
title: オンプレミス インフラストラクチャのアップグレード
titleSuffix: Configuration Manager
description: SQL Server やサイト システムの OS などのインフラストラクチャをアップグレードする方法について説明します。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0c2894bcdf80901171cceba96e7829793f899383
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606776"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Configuration Manager をサポートするオンプレミス インフラストラクチャのアップグレード

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager を実行するサーバー インフラストラクチャをアップグレードする場合は、この記事の情報を参考にしてください。  

- 以前のバージョンから Configuration Manager (Current Branch) に*アップグレード*する場合は、「[System Center Configuration Manager へのアップグレード](../deploy/install/upgrade-to-configuration-manager.md)」をご覧ください。  

- Configuration Manager (Current Branch) インフラストラクチャを新しいバージョンに*アップグレード*する場合は、[Configuration Manager の更新プログラム](updates.md)に関するページをご覧ください。  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> サイト システムの OS のアップグレード  

Configuration Manager では、次の状況で、サイト サーバーと任意のサイト システムの役割をホストするサーバー OS のインプレース アップグレードをサポートしています。  

- Configuration Manager でアップグレード後の Windows の Service Pack レベルが引き続きサポートされる場合は、Windows Server の上位 Service Pack へのインプレース アップグレードがサポートされます。  

- 以下の一括アップグレード。  

    - Windows Server 2016 から Windows Server 2019  

    - Windows Server 2012 R2 から Windows Server 2019  

    - Windows Server 2012 R2 から Windows Server 2016  

    - Windows Server 2012 から Windows Server 2016  

    - Windows Server 2012 から Windows Server 2012 R2  

    - Windows Server 2008 R2 から Windows Server 2012 R2  

サーバーをアップグレードするには、アップグレード先の OS によって提供されるアップグレード手順を使用します。 次の記事をご覧ください。  

- [Windows Server アップグレード センター](https://aka.ms/upgradecenter)  

- [Windows Server 2016 のアップグレードと変換オプション](/windows-server/get-started/supported-upgrade-paths)  

- [Windows Server 2012 R2 のアップグレード オプション](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> Windows Server 2016 または 2019 へのアップグレード

次のアップグレード シナリオに対しては、このセクションの手順を実行します。  

- Windows Server 2012 R2 または Windows Server 2016 のいずれかを Windows Server 2019 にアップグレードする  

- Windows Server 2012 または Windows Server 2012 R2 のいずれかを Windows Server 2016 にアップグレードする  

#### <a name="before-upgrade"></a>アップグレードの前に

- (Windows Server 2012 または Windows Server 2012 R2): System Center Endpoint Protection (SCEP) クライアントを削除します。 Windows Server には、SCEP クライアントの代わりとして、Windows Defender が組み込まれています。 SCEP クライアントが存在している場合、Windows Server へのアップグレードが妨げられる可能性があります。  

- WSUS ロールがサーバーにインストールされている場合は削除します。 SUSDB を残しておき、WSUS を再インストールした後で再アタッチできます。  

- サイト サーバーの OS をアップグレードしている場合は、サイトの[ファイルベースのレプリケーション](../../plan-design/hierarchy/file-based-replication.md)が正常であることを確認します。 送信側と受信側両方のサイトで、バックログのすべての受信トレイを確認します。 スタックすなわち保留中のレプリケーション ジョブが多数ある場合は、それらがなくなるまで待ちます。<!-- SCCMDocs#1792 -->
    - 送信側サイトで、**sender.log** を確認します。
    - 受信側サイトで、**despooler log** を確認します。

#### <a name="after-upgrade"></a>アップグレードの後に

- Windows Defender が有効化され、自動開始が設定され、実行されていることを確認します。  

- 次の Configuration Manager のサービスが実行されていることを確認します。  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- **Windows プロセス アクティブ化**サービスと **WWW/W3svc** サービスが有効化されており、自動開始に設定されていることを確認します。 アップグレード プロセスではこれらのサービスが無効化されるため、次のサイト システムの役割に対してこれらが実行されていることを確認します。  

    - サイト サーバー  

    - 管理ポイント  

    - アプリケーション カタログ Web サービス ポイント  

    - アプリケーション カタログ Web サイト ポイント  

- サイト システムの役割をホストする各サーバーが、引き続きすべての[前提条件](../../plan-design/configs/site-and-site-system-prerequisites.md)を満たしていることを確認します。 たとえば、BITS、WSUS を再インストールしたり、IIS の特定の設定を構成したりすることが必要になる場合があります。  

- 不足している前提条件を復元した後で、もう一度サーバーを再起動して、サービスが開始され、動作していることを確認します。  

- プライマリ サイト サーバーをアップグレードしている場合、[サイト リセットを実行](modify-your-infrastructure.md#bkmk_reset)します。  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>リモートの Configuration Manager コンソールに関する既知の問題

サイト サーバー、または SMS プロバイダーのインスタンスをアップグレードすると、Configuration Manager コンソールに接続できなくなります。 この問題を回避するには、WMI の **SMS Admins** グループのアクセス許可を手動で復元します。 サイト サーバーと、SMS プロバイダーのインスタンスをホストする各リモート サーバーで、アクセス許可を設定する必要があります。

1. 該当するサーバー上で Microsoft 管理コンソール (MMC) を開き、**WMI コントロール**のスナップインを追加し、 **[ローカル コンピューター]** を選択します。  

2. MMC で、 **[WMI コントロール (ローカル)]** の **[プロパティ]** を開き、 **[セキュリティ]** タブを選択します。  

3. ルートの下のツリーを展開し、 **[SMS]** ノードを選択して、 **[セキュリティ]** を選択します。  **SMS Admins** グループに次のアクセス許可が付与されていることを確認します。  

    - アカウントの有効化  

    - リモートの有効化  

4. **[セキュリティ] タブ**で、 **[SMS]** ノードの下にある **[site_&lt;sitecode**>] ノードを選択し、次に **[セキュリティ]** を選択します。 **SMS Admins** グループに次のアクセス許可が付与されていることを確認します。  

    - メソッドの実行  

    - プロバイダーによる書き込み  

    - アカウントの有効化  

    - リモートの有効化  

5. アクセス許可を保存して、Configuration Manager コンソールへのアクセスを復元します。  

#### <a name="known-issue-for-remote-site-systems"></a>リモート サイト システムの既知の問題

サイト システムの役割をホストするサーバーをアップグレードした後、`HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths` のレジストリ キーに値 `Software\Microsoft\SMS` がない可能性があります。

サーバーで Windows をアップグレードした後、この値がない場合は、手動で追加します。 そうしないと、サイト システムの役割で、サイト サーバー受信トレイにファイルをアップロードするときに問題が発生する場合があります。

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Windows Server 2012 R2 へのアップグレード

Windows Server 2008 R2 または Windows Server 2012 から Windows Server 2012 R2 にアップグレードする場合は、次の条件が適用されます。

#### <a name="before-upgrade"></a>アップグレードの前に

- Windows Server 2012 の場合: WSUS ロールがサーバーにインストールされている場合は削除します。 SUSDB を残しておき、WSUS を再インストールした後で再アタッチできます。  

- Windows Server 2008 R2 の場合: Windows Server 2012 R2 にアップグレードする前に、サーバーから WSUS 3.2 をアンインストールする必要があります。 SUSDB を残しておき、WSUS を再インストールした後で再アタッチできます。 詳細については、「[Windows Server Update Services の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality)」をご覧ください。  

- サイト サーバーの OS をアップグレードしている場合は、サイトの[ファイルベースのレプリケーション](../../plan-design/hierarchy/file-based-replication.md)が正常であることを確認します。 送信側と受信側両方のサイトで、バックログのすべての受信トレイを確認します。 スタックすなわち保留中のレプリケーション ジョブが多数ある場合は、それらがなくなるまで待ちます。<!-- SCCMDocs#1792 -->
    - 送信側サイトで、**sender.log** を確認します。
    - 受信側サイトで、**despooler log** を確認します。

#### <a name="after-upgrade"></a>アップグレードの後に

- アップグレード プロセスでは、Windows 展開サービスが無効化されます。 次のサイト システムの役割に対し、このサービスが開始されて実行されていることを確認します。  

    - サイト サーバー  

    - 管理ポイント  

    - アプリケーション カタログ Web サービス ポイント  

    - アプリケーション カタログ Web サイト ポイント  

- **Windows プロセス アクティブ化**サービスと **WWW/W3svc** サービスが有効化されており、自動開始に設定されていることを確認します。 アップグレード プロセスではこれらのサービスが無効化されるため、次のサイト システムの役割に対してこれらが実行されていることを確認します。  

    - サイト サーバー  

    - 管理ポイント  

    - アプリケーション カタログ Web サービス ポイント  

    - アプリケーション カタログ Web サイト ポイント  

- サイト システムの役割をホストする各サーバーが、引き続きすべての[前提条件](../../plan-design/configs/site-and-site-system-prerequisites.md)を満たしていることを確認します。 たとえば、BITS、WSUS を再インストールしたり、IIS の特定の設定を構成したりすることが必要になる場合があります。  

    不足している前提条件を復元した後で、もう一度サーバーを再起動して、サービスが開始され、動作していることを確認します。  

### <a name="unsupported-upgrade-scenarios"></a>サポートされていないアップグレードのシナリオ

次の Windows Server のアップグレード シナリオは、よく問い合わせが寄せられますが、Configuration Manager ではサポートされていません。  

- Windows Server 2008 から Windows Server 2012 以降  

- Windows Server 2008 R2 から Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> クライアントの OS のアップグレード  

次の状況で、Configuration Manager は Configuration Manager クライアントの OS の一括アップグレードをサポートします。  

- Configuration Manager でアップグレード後の Service Pack レベルがサポートされる場合は、Windows の上位 Service Pack へのインプレース アップグレードがサポートされます。  

- Windows のサポートされているバージョンから Windows 10 への一括アップグレード。 詳細については、「[Windows を最新バージョンにアップグレードする](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)」をご覧ください。  

- Windows 10 のビルドからビルドへのサービス アップグレード。 詳細については、「[サービスとしての Windows の管理](../../../osd/deploy-use/manage-windows-as-a-service.md)」を参照してください。  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> SQL Server のアップグレード  

Configuration Manager では、サイト データベース サーバー上での SQL Server のインプレース アップグレードがサポートされています。

Configuration Manager でサポートされている SQL Server のバージョンの詳細については、「[SQL Server バージョンのサポート](../../plan-design/configs/support-for-sql-server-versions.md)」をご覧ください。  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>SQL Server のサービス パック バージョンのアップグレード

Configuration Manager でアップグレード後の SQL Server Service Pack レベルが引き続きサポートされる場合は、SQL Server の上位 Service Pack へのインプレース アップグレードがサポートされます。

階層内に複数の Configuration Manager サイトがある場合、各サイトで異なるバージョンの SQL Server の Service Pack を実行できます。 SQL Server の Service Pack のバージョンをアップグレードするサイトの順番に制限はありません。

### <a name="upgrade-to-a-new-version-of-sql-server"></a>SQL Server の新しいバージョンへのアップグレード

Configuration Manager は次のバージョンへの SQL Server の一括アップグレードをサポートしています。

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

これには、セカンダリ サイトで SQL Server Express を新しいバージョンの SQL Server Express にアップグレードすることが含まれます。

各サイトでサイト データベースをホストする SQL Server のバージョンをアップグレードする場合は、サイトで使用される SQL Server のバージョンを、次の順序でアップグレードする必要があります。

1. 最初に中央管理サイトで SQL Server をアップグレードします。  

2. セカンダリ サイトの親プライマリ サイトをアップグレードする前に、セカンダリ サイトをアップグレードします。  

3. 最後に親プライマリ サイトをアップグレードします。 これらのサイトには、中央管理サイトに報告する子プライマリ サイトと、階層の最上位サイトであるスタンドアロンのプライマリ サイトの両方が含まれます。  

### <a name="sql-server-cardinality-estimation-level"></a>SQL Server のカーディナリティ推定レベル

サイト データベースを以前のバージョンの SQL Server からアップグレードすると、既存の SQL カーディナリティ推定レベルが SQL Server のそのインスタンスで許可されている最小レベルである場合に、データベースではそのレベルが保持されます。 許可レベルより低い互換性レベルのデータベースを持つ SQL Server をアップグレードすると、データベースは SQL で許可されている最も低い互換性レベルに設定されます。

次の表に、Configuration Manager サイト データベースで推奨される互換性レベルを示します。

|SQL Server バージョン | サポートされる互換性レベル | 推奨レベル |
|----------------|--------------------|--------|
| SQL Server 2017 | 140、130、120、110  | 140 |
| SQL Server 2016 | 130、120、110  | 130 |
| SQL Server 2014 | 120、110      | 110 |

サイト データベースで使用されている SQL Server のカーディナリティ推定互換性レベルを識別するには、サイト データベース サーバーで次の SQL クエリを実行します。  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

SQL CE の互換性レベルとその設定方法の詳細については、「[ALTER DATABASE 互換性レベル (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)」を参照してください。

SQL Server のアップグレードについて詳しくは、次の SQL Server の記事をご覧ください。  

- [SQL Server 2017 へのアップグレード](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [SQL Server 2016 へのアップグレード](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)  

- [SQL Server 2014 へのアップグレード](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>サイト データベース サーバー上の SQL Server をアップグレードするには  

1. サイトのすべての Configuration Manager サービスを停止します。  

2. SQL Server をサポートされるバージョンにアップグレードします。  

3. Configuration Manager サービスを再起動します。  

> [!NOTE]  
> 中央管理サイトで使用中の SQL Server のエディションを Standard から Datacenter または Enterprise に変更するときに、データベースのパーティションは変更されません。 このデータベース パーティションにより、階層がサポートするクライアントの数が制限されます。