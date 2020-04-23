---
title: '[サービス接続ポイント]'
titleSuffix: Configuration Manager
description: この Configuration Manager サイト システムの役割について学習し、その使用範囲を理解し計画します。
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704950"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Configuration Manager のサービス接続ポイントについて

*適用対象:Configuration Manager (Current Branch)*

サービス接続ポイントは、階層のいくつかの重要な機能を提供するサイト システムの役割です。 サービス接続ポイントを設定する前に、その使用範囲を理解し、計画を立ててください。 使用計画によっては、このサイト システムの役割の設定方法に影響がある可能性があります。

- ご利用の Configuration Manager インフラストラクチャに適用される更新プログラムをダウンロードします。 アップロードする使用データに基づいて、インフラストラクチャに関連する更新プログラムのみを入手することができます。

- ご利用の Configuration Manager インフラストラクチャからの使用データをアップロードします。 アップロードする詳細のレベルと量を制御することができます。 詳細については、「[使用状況データのレベルと設定](../install/setup-reference.md#bkmk_usage)」を参照してください。

- [クラウド管理ゲートウェイを](../../../clients/manage/cmg/plan-cloud-management-gateway.md) Azure にデプロイします。

- [ビジネスおよび教育機関向け Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) からのアプリを同期します

- [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc) でユーザーとグループを探索します。

- [Desktop Analytics](../../../../desktop-analytics/overview.md) を使用して、Windows 10 の更新プログラムとアプリ対応性に関する分析情報を取得します

各階層では、この役割の単一のインスタンスがサポートされます。 これは、ご利用の階層の最上位層サイト (中央管理サイト (CAS) またはスタンドアロン プライマリ サイト) のみにインストールできます。 スタンドアロン プライマリ サイトをより大きな階層に拡張する場合は、この役割をプライマリ サイトからアンインストールしてから、CAS にインストールします。

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a> 操作モード

サービス接続ポイントは、操作の 2 つのモードをサポートしています。

- **オンライン**: サービス接続ポイントでは 24 時間ごとに更新プログラムが自動的にチェックされます。 そして、現在のインフラストラクチャおよび製品バージョンで使用可能な新しい更新プログラムをダウンロードし、Configuration Manager コンソールで使用できるようにします。

- **オフライン**: サービス接続ポイントは Microsoft クラウド サービスに接続されません。 使用可能な更新プログラムを手動でインポートするには、[サービス接続ツール](../../manage/use-the-service-connection-tool.md)を使用します。

### <a name="change-mode"></a>モードの変更

サービス接続ポイントをインストールした後でオンライン モードとオフライン モードを変更する場合は、SMS_Executive サービスの **SMS_DMP_DOWNLOADER** スレッドを再起動します。 このスレッドを再起動することにより、変更が有効になります。 このスレッドを再起動するには、Configuration Manager サービス マネージャーを使用します。

> [!TIP]
> また、Configuration Manager の SMS_Executive サービスを再起動することもでき、それによりほとんどのサイト コンポーネントが再起動されます。 または、サイトのバックアップなどのスケジュールされたタスクを待つこともできます。この場合は、SMS_Executive サービスが自動的に停止され、再起動されます。

Configuration Manager サービス マネージャーを使用して SMS_DMP_DOWNLOADER スレッドを再起動するには、次のようにします。

1. Configuration Manager コンソールで、 **[監視]** ワークスペースに移動し、 **[システム ステータス]** を展開し、 **[コンポーネントのステータス]** ノードを選択します。 リボンで **[開始]** を選択して、 **[Configuration Manager サービス マネージャー]** を選択します。

1. サービス マネージャーのナビゲーション ウィンドウで、サイトを展開し、 **[コンポーネント]** を展開してから、再起動するコンポーネントを選択します: **SMS_DMP_DOWNLOADER**。

1. **[コンポーネント]** メニューにアクセスし、 **[クエリ]** を選択します。

1. コンポーネントの現在の状態を確認します。 次に、 **[コンポーネント]** メニューにアクセスし、 **[停止]** を選択します。  

1. コンポーネントに対して再び **[クエリ]** を実行して、それが停止していることを確認します。 次に、 **[Start]** コンポーネント アクションを選択して再起動します。

## <a name="remote-site-system-requirements"></a>リモート サイト システムの要件

サイト サーバーから離れた場所にあるサイト システム サーバー上にサービス接続ポイントをインストールする場合は、次の要件を構成します。

- サイト サーバーのコンピューター アカウントは、リモート サービス接続ポイントをホストするコンピューターのローカル管理者とする必要があります。

- [サイト システムのインストール アカウント](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)を使用してこの役割をホストするサイト システム サーバーを設定します。 サイト サーバー上の配布マネージャーは、サイト システムのインストール アカウントを使って、サービス接続ポイントから更新プログラムを転送します。

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a> インターネット アクセス要件

組織がファイアウォールまたはプロキシ デバイスを使用してインターネットとのネットワーク通信を制限している場合は、サービス接続ポイントからインターネット エンドポイントへのアクセスを許可する必要があります。

詳細については、「[Internet access requirements (インターネット アクセスの要件)](../../../plan-design/network/internet-endpoints.md#bkmk_scp)」を参照してください。

## <a name="install"></a>[インストール]

**[セットアップ]** を実行して階層の最上位サイトをインストールする場合、サービス接続ポイントをインストールすることができます。

セットアップが実行された後、または役割をインストールする場合には、 **[サイト システムの役割の追加]** ウィザードまたは **[サイト システム サーバーの作成]** ウィザードを使用します (サービス接続ポイントは、ご利用の階層の最上位層にのみインストールします)。詳しくは、「[サイト システムの役割のインストール](install-site-system-roles.md)」をご覧ください。

## <a name="move-the-role"></a><a name="bkmk_move"></a> 役割を移動する

<!-- SCCMDocs#922 -->
いくつかのシナリオでは、サービス接続ポイントを別のサーバーに移動することが必要になる場合があります。

- [復元](../../manage/recover-sites.md)
- [サイト サーバーの高可用性](site-server-high-availability.md)
- [サイトの拡張](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

サービス接続ポイントを移動したら、すべてのサイト機能を確認します。 たとえば、Azure Active Directory (Azure AD) テナントへの接続については、秘密キーの更新が必要になる場合があります。 詳細については、[秘密鍵の更新](azure-services-wizard.md#bkmk_renew)に関するページを参照してください。

## <a name="log-files"></a>ログ ファイル

Microsoft へのアップロードに関する情報については、サービス接続ポイントを実行するサーバーの **Dmpuploader.log** をご覧ください。 更新プログラムのダウンロード進捗状については、**Dmpdownloader.log** をご覧ください。 サービス接続ポイント関連のログの完全な一覧については、[ログ ファイル - サービス接続ポイント](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

プロセス フローとキー ログ エントリを理解するには、次のフローチャートを使用します。 このプロセスには、更新プログラムのダウンロードと、他のサイトへの更新プログラムのレプリケーションが含まれます。

- [フローチャート - 更新プログラムのダウンロード](../../manage/download-updates-flowchart.md)

- [フローチャート - レプリケーションの更新](../../manage/update-replication-flowchart.md)
