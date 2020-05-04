---
title: クライアント通知
titleSuffix: Configuration Manager
description: 中央の Configuration Manager コンソールから早急な対応を行うことで、クライアントを管理します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a00f77a5a902728a7c41905314511cffcfa81a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694960"
---
# <a name="client-notification-in-configuration-manager"></a>Configuration Manager のクライアント通知

*適用対象:Configuration Manager (Current Branch)*

リモート クライアントで早急な対応を行うには、Configuration Manager コンソールからクライアント通知アクションを送信します。 個別のデバイスまたはデバイスのコレクションでこれらのアクションを開始します。

## <a name="actions"></a>操作

次のアクションは、[ホーム] タブの [デバイス] または [コレクション] グループのリボンにあります。

### <a name="install-client"></a>クライアントのインストール

**クライアントのインストール ウィザード**を開きます。 このウィザードでは、クライアント プッシュ インストールを使用して、Configuration Manager クライアントをインストールします。 詳しくは、「[クライアント プッシュ インストール](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)」をご覧ください。

#### <a name="permissions---install-client"></a>アクセス許可 - クライアントのインストール

このアクションには、**コレクション** オブジェクトに対する**リソースの変更**と**読み取り**のアクセス許可が必要です。

次の組み込みロールには、既定でこれらのアクセス許可があります。

- アプリケーション管理者  
- 完全な権限を持つ管理者  
- インフラストラクチャ管理者  
- オペレーション管理者  
- OS 展開マネージャー  

これらのアクセス許可を、クライアントをプッシュする必要がある任意のカスタム ロールに追加します。

### <a name="run-script"></a>スクリプトの実行

**スクリプトの実行**ウィザードを開き、コレクション内のすべてのクライアントで PowerShell スクリプトを実行します。 詳しくは、「[PowerShell スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)」をご覧ください。

#### <a name="permissions---run-script"></a>アクセス許可 - スクリプトの実行

このアクションには、**コレクション** オブジェクトに対する**スクリプトの実行**アクセス許可が必要です。

次の組み込みロールには、既定でこのアクセス許可があります。

- 完全な権限を持つ管理者  
- インフラストラクチャ管理者  
- オペレーション管理者  

このアクセス許可を、スクリプトを実行する必要があるカスタム ロールに追加します。

### <a name="start-cmpivot"></a>CMPivot の開始

対象のデバイスに対してリアルタイムでクエリを実行する **CMPivot** を開始します。 詳細については、[CMPivot](../../servers/manage/cmpivot.md) に関するページを参照してください。

#### <a name="permissions---start-cmpivot"></a>アクセス許可 - CMPivot の開始

このアクションには、[スクリプトの実行](#run-script)アクションと同じアクセス許可が必要です。

バージョン 1906 以降では、**コレクション** オブジェクトに対して **CMPivot の実行**アクセス許可を使用できます。

## <a name="client-notification"></a>クライアント通知

これらのアクションは、[ホーム] タブの [デバイス] または [コレクション] グループのリボンにある、 **[クライアント通知]** メニューにあります。

バージョン 1806 以前では、 **[クライアント通知]** オプションは、デバイス コレクション ノードから利用できるか、またはデバイス コレクションのメンバーシップを表示するときに利用できるだけでした。 バージョン 1810 以降、 **[デバイス]** ノードから直接 **[クライアント通知]** を開始することができます。 コレクション メンバーシップ ビュー内に要件は存在しなくなりました。 <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>アクセス許可 - クライアント通知

<!--SCCMDocs-pr issue #2972-->
バージョン 1810 以降では、クライアント通知アクションに、コレクション オブジェクトに対する**リソースの通知**アクセス許可が必要になりました。 このアクセス許可は、 **[クライアント通知]** メニューの下のすべてのアクションに適用されます。

次の組み込みロールには、既定でこのアクセス許可があります。

- 完全な権限を持つ管理者  
- オペレーション管理者  

クライアント通知アクションを使用する必要があるカスタム ロールには、このアクセス許可を追加してください。

### <a name="download-computer-policy"></a>コンピューター ポリシーのダウンロード

デバイス ポリシーを更新します。 詳細については、「[Configuration Manager クライアントのポリシーの取得開始](manage-clients.md#BKMK_PolicyRetrieval)」を参照してください。  

### <a name="download-user-policy"></a>ユーザー ポリシーのダウンロード

ユーザー ポリシーを更新します。  

### <a name="collect-discovery-data"></a>検出データの収集

クライアントによる探索データ レコード (DDR) の送信をトリガーします。 詳しくは、「[定期探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)」をご覧ください。  

### <a name="collect-software-inventory"></a>ソフトウェア インベントリの収集

クライアントによるソフトウェア インベントリ サイクルの実行をトリガーします。 詳しくは、「[ソフトウェア インベントリの概要](inventory/introduction-to-software-inventory.md)」をご覧ください。  

### <a name="collect-hardware-inventory"></a>ハードウェア インベントリの収集

クライアントによるハードウェア インベントリ サイクルの実行をトリガーします。 詳しくは、「[ハードウェア インベントリの概要](inventory/introduction-to-hardware-inventory.md)」をご覧ください。  

### <a name="evaluate-application-deployments"></a>アプリケーション展開の評価

クライアントによるアプリケーション展開評価サイクルの実行をトリガーします。 詳しくは、「[展開の再評価スケジュールを指定する](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments)」をご覧ください。  

### <a name="evaluate-software-update-deployments"></a>ソフトウェア更新プログラム展開の評価

クライアントによるソフトウェア更新プログラム展開の評価サイクルの実行をトリガーします。 詳しくは、「[ソフトウェア更新プログラムの概要](../../../sum/understand/software-updates-introduction.md)」をご覧ください。  

### <a name="switch-to-the-next-software-update-point"></a>次のソフトウェアの更新ポイントに切り替える

クライアントによる次の利用可能なソフトウェア更新ポイントへの切り替えをトリガーします。 詳しくは、「[ソフトウェアの更新ポイントの切り替え](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)」をご覧ください。  

### <a name="evaluate-device-health-attestation"></a>デバイス正常性構成証明の評価

Windows 10 クライアントによる最新のデバイスの正常性状態の確認と送信をトリガーします。 詳細については、[正常性構成証明書](../../servers/manage/health-attestation.md)に関するページを参照してください。  

### <a name="wake-up"></a>ウェイク アップ

バージョン 1810 以降では、同じサブネット上の他のデバイスを使用して Wake-on-LAN パッケージを送信し、Wake-on-LAN をサポートするように構成されているデバイスのウェイクアップをトリガーします。 詳細については、[Wake On LAN を構成する方法](../deploy/configure-wake-on-lan.md)に関するページを参照してください。

### <a name="restart"></a>再起動

選択したデバイスの再起動をトリガーします。 詳細については、「[クライアントの再起動](manage-clients.md#restart-clients)」を参照してください。

## <a name="client-diagnostics"></a>クライアント診断
<!--4433455-->

バージョン 1910 以降、Configuration Manager コンソールの **[クライアント診断]** には新しいデバイス アクションがあります。 次のアクションが追加されました。

- **詳細なログ記録の有効化**:CCM コンポーネントのグローバル ログ レベルを詳細に変更し、デバッグ ログ記録を有効にします。
- **詳細なログ記録の無効化**:グローバル ログ レベルを既定に変更し、デバッグ ログ記録を無効にします。
- **クライアント ログの収集** (2002 以降):クライアント通知メッセージが、CCM ログを収集するために選択したクライアントに送信されます。 ログは、ソフトウェア インベントリ ファイル コレクションを使用して返されます。 <!--4226618-->
   - 圧縮されたクライアント ログのサイズの上限は 100 MB です。 <!--6366098-->
   - これらのファイルを管理および表示するには、[リソース エクスプローラー](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag)を使用します。

   [![コンソールからクライアント ログを収集する](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - 以上のアクションではログの詳細度のみが変更され、サイズや履歴は変更されません。 ログ記録の詳細度が上がると、生成されるログ コンテンツが増えます。
> - 管理ポイント ロールでは、CCM コンポーネントも使用されます。 ターゲット デバイスが管理ポイントでもある場合、この操作はそのロールにも適用されます。

これらの設定の詳細については、「[ログ ファイルについて](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client)」を参照してください。

クライアントの **diagnostics.log** でタスクの状態を追跡記録します。 クライアント ログが収集されると、追加情報が管理ポイントの **MP_SinvCollFile.log** と、サイト サーバーの **sinvproc.log** に記録されます。

### <a name="prerequisites---client-diagnostics"></a>前提条件 - クライアント診断

- ターゲット クライアントを最新版に更新します。

- Configuration Manager 管理ユーザーには、 **[リソースの通知]** アクセス許可が必要です。

  次の組み込みロールには、既定でこのアクセス許可があります。

  - 完全な権限を持つ管理者  
  - インフラストラクチャ管理者  

  クライアント通知アクションを使用する必要があるカスタム ロールには、このアクセス許可を追加してください。


## <a name="endpoint-protection"></a>Endpoint Protection

次のアクションは、 **[Endpoint Protection]** メニューの下にあります。 このメニューは、[ホーム] タブの [コレクション] グループのリボンにあります。1 つまたは複数のデバイスを選択すると、これらのアクションがリボンの **[選択したオブジェクト]** タブに表示されます。

詳細については、[Configuration Manager のエンドポイント保護](../../../protect/deploy-use/endpoint-protection.md)に関するページを参照してください。

### <a name="permissions---endpoint-protection"></a>アクセス許可 - エンドポイント保護

このアクションには、**コレクション** オブジェクトに対する**セキュリティ ポリシーの実施**アクセス許可が必要です。

次の組み込みロールには、既定でこのアクセス許可があります。

- 完全な権限を持つ管理者  
- Endpoint Protection マネージャー  
- オペレーション管理者  

Endpoint Protection アクションをトリガーする必要があるカスタム ロールには、このアクセス許可を追加してください。

### <a name="full-scan"></a>フル スキャン

Endpoint Protection または Windows Defender によるマルウェア対策の*フル* スキャンの実行をトリガーします。  

### <a name="quick-scan"></a>クイック スキャン

Endpoint Protection または Windows Defender によるマルウェア対策の*クイック* スキャンの実行をトリガーします。  

### <a name="download-definition"></a>定義のダウンロード

Endpoint Protection または Windows Defender による最新のマルウェア対策定義のダウンロードをトリガーします。  

## <a name="see-also"></a>関連項目

- [クライアントを管理する方法](manage-clients.md)
- [コレクションを管理する方法](collections/manage-collections.md)
