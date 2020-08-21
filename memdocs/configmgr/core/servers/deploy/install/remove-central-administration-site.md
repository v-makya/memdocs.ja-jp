---
title: CAS を削除する
titleSuffix: Configuration Manager
description: 中央管理サイト (CAS) を削除して、Configuration Manager インフラストラクチャを 1 つのスタンドアロンのプライマリ サイトに簡素化します。
ms.date: 06/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a1d9d4ce8cdd19efb440d4d73fafdc96a514bcd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699162"
---
# <a name="remove-the-central-administration-site"></a>中央管理サイトを削除する

*適用対象:Configuration Manager (Current Branch)*

<!-- 3607277 -->

バージョン 2002 以降、階層が中央管理サイト (CAS) と 1 つの子プライマリ サイトで構成されている場合に CAS を削除できるようになりました。 この操作により、Configuration Manager インフラストラクチャが 1 つのスタンドアロンのプライマリ サイトに簡素化されます。 これにより、サイト間レプリケーションの複雑さが解消され、管理タスクが 1 つのサイトに集中されます。

> [!IMPORTANT]
> このバージョンの Configuration Manager では、この機能はプレリリース版であり、既定では有効になりません。 現在、Microsoft Premier のお客様にご利用いただけます。
>
> この機能を有効にするには、テクニカル アカウント マネージャーにお問い合わせください。
>
> - TAM によって、Microsoft Premier 時間を使用するアドバイザリ ケースがオープンされます。
> - ケースの重要度を変更することはできません。
> - Microsoft サポートでは、通常の平日営業時間内に、これらのアドバイザリ ケースを支援します。

## <a name="plan"></a>プラン

- 階層は、CAS と 1 つの子プライマリ サイトで構成されている必要があります。 プライマリ サイトは、セカンダリ サイトを持つことができます。 他の子プライマリ サイトを階層から削除するには、[プライマリ サイトをアンインストール](uninstall-sites-and-hierarchies.md#bkmk_primary)するための計画手順と前提条件を確認してください。

- 子プライマリ サイトが、[スタンドアロン プライマリ サイト](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri)のサイズとスケールの要件を満たしていることを確認します。

- サービス接続ポイントとソフトウェア更新ポイントを除き、CAS にあるサイトの役割をすべて移動または削除します。 これらの 2 つの役割は、CAS を削除するときに、Configuration Manager のセットアップで処理されます。

  次の役割は CAS で最も一般的です。これらは、削除するか、プライマリ サイトに移動する必要があります。

  - 資産インテリジェンス同期ポイント
  - Endpoint Protection ポイント
  - レポート サービス ポイント
  - データ ウェアハウス サービス ポイント
  - クラウド管理ゲートウェイ (CMG)

    > [!NOTE]
    > コンテンツに対して CMG を有効にした場合は、プライマリ サイトに CMG を再作成した後にコンテンツを再配布するように計画してください。<!-- 6608659 -->

- 分散ビューをオフにします

- Configuration Manager は、Configuration Manager クライアントと同様に、組み込みパッケージのパッケージ ソースの場所を自動的に処理します。 他のすべてのコンテンツ ソースの場所を確認して、それらが CAS の共有を使用していないことを確認してください。

- すべてのアクティブな移行ジョブを停止し、移行のすべての構成を削除します。 詳細情報については、「[別の階層からのアクティブな移行を停止する](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy)」を参照してください。

- ソフトウェア更新プログラムの自動展開規則を使用する場合は、それらを子プライマリ サイトに再作成します。

- Configuration Manager または System Center Updates Publisher を使用して[サードパーティ製のソフトウェア更新プログラム](../../../../sum/deploy-use/third-party-software-updates.md)を管理する場合は、CAS のソフトウェア更新ポイントから WSUS 署名証明書をエクスポートします。

  - CAS を削除する前に、サードパーティ製ソフトウェア更新プログラムの必要な展開の期限までお待ちください。 クライアントは必要な展開のコンテンツを事前にダウンロードし、ユーザーがソフトウェアの更新ポイントを変更すると、ソフトウェア更新プログラムの "*ローカル発行*" によってコンテンツのハッシュが変更されます。 (この動作は他のコンテンツの種類には影響せず、サードパーティ製ソフトウェア更新プログラムのローカル発行のみに影響します。)これらの必要な展開がまだ進行中であるときに CAS を削除すると、それらはハッシュの不一致エラーによって、クライアントで失敗します。

- CAS への依存関係を持っている可能性のあるサードパーティ製ソフトウェアを確認してください。

## <a name="prerequisites"></a>[前提条件]

- Configuration Manager のセットアップを実行する管理ユーザーには、次のセキュリティ権限が必要です。

  - CAS サーバーでのローカル**管理者**権限

  - CAS データベース サーバーがサイト サーバーからリモートにある場合は、CAS のリモート サイト データベース サーバーのローカル**管理者**権限。

  - CAS サイト データベースでの **Sysadmin** 権限

  - プライマリ サイト サーバーでのローカル**管理者**権限

  - プライマリ サイト データベース サーバーがプライマリ サイト サーバーからリモートにある場合は、プライマリ サイトのリモート サイト データベース サーバーのローカル**管理者**権限。

  - プライマリ サイト データベースの **Sysadmin** 権限

  - CAS およびプライマリ サイトでの**インフラストラクチャ管理者**または**完全な権限を持つ管理者**のセキュリティ ロール

- 階層内の子プライマリ サイトは 1 つだけです。 詳細については、「[プライマリ サイトのアンインストール](uninstall-sites-and-hierarchies.md#bkmk_primary)」を参照してください。

## <a name="process"></a>プロセス

1. 次のいずれかの方法を使用して、CAS サーバーで Configuration Manager のセットアップを開始します。

    - **[開始]** メニューで、 **[Configuration Manager のセットアップ]** を選択します。

    - Configuration Manager の*インストール メディア*のディレクトリで、`\SMSSETUP\BIN\X64\setup.exe` を開きます。 このバージョンがサイトのバージョンと同じであることを確認します。

    - Configuration Manager が*インストールされている*ディレクトリで、`\BIN\X64\setup.exe` を開きます。

1. **[開始する前に]** ページの情報を確認します。

1. **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** を選択します。

1. **[サイトのメンテナンス]** ページで、 **[中央管理サイトの削除]** を選択します。 <!-- or is it still "delete"? -->

1. **[Reconfiguring Existing Site System Roles]\(既存のサイト システムの役割の再構成\)** ページで、次のようにします。

    - **サービス接続ポイント**: この必須の役割をホストするプライマリ サイト内のサイトシステムの完全修飾ドメイン名を入力します。 詳細については、「[About the service connection point](../configure/about-the-service-connection-point.md)」 (サービスの接続ポイントについて) を参照してください。

    - **ソフトウェアの更新ポイント**: プライマリ サイト内の既存のソフトウェアの更新ポイントを選択します。 セットアップで、このソフトウェアの更新ポイントは、CAS 構成と同じように同期するように構成されます。

    セットアップで、指定したサーバーが前提条件を満たしているかどうかが確認されます。 続行する準備ができたら、 **[インストールの開始]** を選択します。

セットアップで問題が発生した場合は、ウィザードを使用してプロセスを再試行してください。

セットアップが完了すると、プライマリ サイトがリセットされます。 詳細については、「[サイト リセットの実行](../../manage/modify-your-infrastructure.md#bkmk_reset)」を参照してください。

## <a name="monitor-and-verify"></a>監視と検証

セットアップ プロセス中に、次のログを確認します。

- CAS サーバーの `C:\ConfigMgrSetup.log`

- プライマリ サイト サーバーの Configuration Manager のログ ディレクトリにある **hman.log**

**[監視]** ワークスペースの **[サイト階層]** ノードを使用して、階層への変更を視覚化します。 たとえば、次の図は、**SHY** CAS、**HAW** プライマリ サイト、および **VWT** セカンダリ サイトの変更前と後の比較を示しています。

| 以前  | これらの手順の完了後、   |
|---------|---------|
|![CAS、プライマリ サイト、およびセカンダリ サイトのサイト階層ビューの例](media/3607277-cas-primary-secondary.png)|![プライマリ サイト、およびセカンダリ サイトのサイト階層ビューの例](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>セットアップ後のタスク

CAS を削除した後、お使いの環境に適用される次の手順を確認します。

- プライマリ サイトのローカル グループから、CAS サーバー コンピューター アカウントを手動で削除します。

- 信頼されたルート キーが変更されたため、追加のアクションが必要になる場合があります。

  - OS 展開のブート イメージを更新して、最新の Configuration Manager バイナリを含めます。

  - [OS 展開メディア](../../../../osd/deploy-use/create-task-sequence-media.md)を再作成します。

- Configuration Manager を [Azure Monitor](/azure/azure-monitor/platform/collect-sccm?context=/mem/configmgr/core/context/core-context) に接続している場合は、接続をリセットする必要があります。 問題を解決するには、まず[秘密鍵を更新](../configure/azure-services-wizard.md#bkmk_renew)します。 それでも問題が解決しない場合は、接続を再作成します。<!-- 5584635 -->

- バージョン 2002 では、Surface のドライバーの同期を有効にしている場合は、CAS を削除した後にこの機能を再構成します。 詳細については、[Microsoft Surface のドライバーとファームウェアの更新プログラム](../../../../sum/deploy-use/surface-drivers.md)に関するページを参照してください。<!-- 5728727 -->

- サード パーティ製のソフトウェア更新プログラムを管理する場合は、次のようにします。

  1. WSUS 署名証明書を CAS のソフトウェアの更新ポイントからエクスポートします (まだ行っていない場合)。

  1. 新しい展開を作成する前に、既存の展開およびソフトウェア更新プログラムのパッケージから更新プログラムを削除します。

  1. ソフトウェア更新プログラムのメタデータを使用可能な状態に回復するには、サブスクライブしたカタログを再同期します。 また、Configuration Manager が自動的に再同期するのを待つこともできます。

  1. 通常のソフトウェア更新プログラムの同期プロセスによる、WSUS からの現在の状態を使用した Configuration Manager の更新を開始するか待ちます。 必要に応じて、SCUP または WSUS の PowerShell コマンドレットを使用して、更新プログラムを削除し、再度追加します。

  1. 展開する必要がある更新プログラムのコンテンツを再パブリッシュします。