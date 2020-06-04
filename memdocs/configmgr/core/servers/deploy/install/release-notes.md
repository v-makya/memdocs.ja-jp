---
title: リリース ノート
titleSuffix: Configuration Manager
description: 製品でまだ修正されていないまたは Microsoft サポート技術情報の記事で説明されていない緊急の問題について説明します。
ms.date: 05/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 131b6104d5724c8a4eeb0bb68c4afd9a5319abb7
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823964"
---
# <a name="release-notes-for-configuration-manager"></a>Configuration Manager のリリース ノート

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager 製品のリリース ノートには、緊急の問題のみが記載されています。 これらの問題はまだ、製品で修正されていないか、または Microsoft サポート技術情報の記事で詳しく説明されていません。  

機能固有のドキュメントには、主要なシナリオに影響を与える既知の問題に関する情報が含まれます。  

この記事には、Configuration Manager の現在のブランチのリリース ノートが含まれています。 Technical Preview ブランチについては、「[Technical Preview](../../../get-started/technical-preview.md)」を参照してください。  

異なるバージョンで導入された新しい機能については、以下の記事をご覧ください。

- [バージョン 2002 の新機能](../../../plan-design/changes/whats-new-in-version-2002.md)
- [バージョン 1910 の新機能](../../../plan-design/changes/whats-new-in-version-1910.md)
- [バージョン 1906 の新機能](../../../plan-design/changes/whats-new-in-version-1906.md)  
- [バージョン 1902 の新機能](../../../plan-design/changes/whats-new-in-version-1902.md)

Desktop Analytics の新機能の詳細については、「[Desktop Analytics の新機能](../../../../desktop-analytics/whats-new.md)」を参照してください。

> [!Tip]  
> このページが更新されたときに通知を受け取るには、次の URL をコピーして RSS フィード リーダーに貼り付けます。`https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>セットアップしてアップグレードする  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>すべてのクライアントについて、クライアントの自動アップグレードが直ちに行われます。

<!-- 6040412 -->

"*適用対象: バージョン 1910*"

ご利用のサイトで[自動クライアント アップグレード](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)が使用されている場合、そのサイトをバージョン 1910 に更新すると、サイトの更新が正常に行われた後で直ちにすべてのクライアントがアップグレードされます。 ランダム化が唯一行われるのはクライアントでポリシーが受信されたときであり、既定値は 1 時間ごとです。 クライアントを多く含む大規模なサイトでは、この動作によって大量のネットワーク トラフィックとストレス配布ポイントが消費される可能性があります。

影響を受けるバージョンの詳細については、「[Configuration Manager Current Branch、バージョン 1910 のクライアント更新プログラム](https://support.microsoft.com/help/4538166)」をご覧ください。

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>パッシブ モードのサイト サーバーでは configuration.mof が更新されない

<!-- 5787848 -->

"*適用対象: バージョン 1910*"

サイトに[パッシブ モードのサイト サーバー](../configure/site-server-high-availability.md)が含まれている場合は、サイトの更新時にインベントリのカスタマイズ内容が失われることがあります。 現時点では、サイト サーバーをフェールオーバーするときにサイトの configuration.mof は同期されません。

この問題を回避するには、サイトの configuration.mof を手動でバックアップして復元します。

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Server 2019 のドメイン機能レベルに関する前提条件の警告を設定する

<!-- 4904376 -->

*適用対象: バージョン 1906 以降*

Windows Server 2019 を実行しているドメイン コントローラーを使用する環境にバージョン 1906 の更新プログラムをインストールする場合、ドメイン機能レベルの前提条件チェックにより次の警告が返されます。

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

この問題を回避するには、警告を無視します。

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>サイト拡張後、Azure AD のユーザー探索とコレクション グループの同期が機能しない

<!-- 4797313 -->
*適用対象: バージョン 1906 以降*

次の機能のいずれかを構成後:

- Azure Active Directory ユーザー グループの探索
- コレクションのメンバーシップの結果の Azure Active Directory グループとの同期

スタンドアロン プライマリ サイトを中心管理サイトがある階層に拡張すると、SMS_AZUREAD_DISCOVERY_AGENT.log に次のエラーが記録されています。

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

この問題を回避するには、Azure AD で、アプリの登録に関連付けられたキーを更新します。 詳細については、[秘密鍵の更新](../configure/azure-services-wizard.md#bkmk_renew)に関するページを参照してください。

## <a name="role-based-administration"></a>役割に基づいた管理

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>特定のフォルダーのセキュリティ スコープが CAS からプライマリ サイトにレプリケートされない
<!--6306759-->
"*適用対象: バージョン 1910*"

バージョン 1910 へのアップグレード後、ユーザー コレクションおよびデバイス コレクション内の[フォルダーのセキュリティ スコープ](../configure/configure-role-based-administration.md#bkmk_config-folder)は、CAS からプライマリ サイトにレプリケートされません。

## <a name="application-management"></a>アプリケーション管理

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Microsoft Edge バージョン 77 以降を展開するときの、PowerShell の証明書を取得できないというエラー
<!--5769384-->
*適用対象:Configuration Manager バージョン 1910*

言語がスウェーデン語、ハンガリー語、または日本語の OS で Configuration Manager コンソールを実行している場合は、Microsoft Edge バージョン 77 以降を展開するときに次のエラーが表示されます。

`Unable to get certificate for Powershell`

このエラーは、スウェーデン語、ハンガリー語、または日本語の `AdminConsole\bin` ディレクトリに `scripts` フォルダーが存在しないために発生します。 これらの OS 言語では scripts フォルダーがローカライズされています。

この問題を回避するには、`AdminConsole\bin` ディレクトリに `scripts` という名前のフォルダーを作成します。 ローカライズされたフォルダーのファイルを、新しく作成した `scripts` フォルダーにコピーします。 ファイルがコピーされたら、Microsoft Edge バージョン 77 以降を展開します。

## <a name="os-deployment"></a>OS の展開

### <a name="task-sequences-cant-run-over-cmg"></a>タスクシーケンスが CMG で実行できない

*適用対象:Configuration Manager バージョン 2002*

クラウド管理ゲートウェイ (CMG) を介して通信するデバイスでタスクシーケンスを実行できない場合が 2 つあります。

- 拡張 HTTP 用にサイトを構成し、管理ポイントが HTTP に設定されている。<!-- 6358851 -->

    この問題を回避するには、管理ポイントを HTTP または HTTPS に構成します。

- 認証用の一括登録トークンを使用してクライアントをインストールし、登録した。<!-- 6377921 -->

    この問題を回避するには、次のいずれかの認証方法を使用します。

  - 内部ネットワークにデバイスを事前登録する
  - クライアント認証証明書を使用してデバイスを構成する
  - デバイスを Azure AD に参加させる

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>パッシブ サイト サーバーの昇格後も、既定のブート イメージ パッケージには前のアクティブ サーバー上のパッケージ ソースが含まれています

<!--3453224, SCCMDocs-pr issue 3097-->
*適用対象:Configuration Manager バージョン 1810*

パッシブ モードのサイト サーバー (サーバー B) がある場合、これをアクティブに昇格しても、既定のブート イメージのコンテンツの場所として引き続き前のアクティブ サーバー(サーバー A) が参照されます。 サーバー A にハードウェア障害がある場合は、既定のブート イメージを更新したり変更したりできません。

この問題の回避策はありません。

## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="security-roles-are-missing-for-phased-deployments"></a>段階的展開のためのセキュリティ ロールがない

<!--3479337, SCCMDocs-pr issue 3095-->
*適用対象:Configuration Manager バージョン 1810、1902*

**OS 展開マネージャー**組み込みセキュリティ ロールには、[段階的展開](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)のためのセキュリティ ロールがあります。 次のロールには、これらのアクセス許可がありません。  

- **アプリケーション管理者**  
- **アプリケーション展開マネージャー**  
- **ソフトウェア更新マネージャー**  

**アプリ作成者**ロールは段階的展開のためのアクセス許可を持っているように見えますが、展開を作成することはできません。

これらのロールのいずれかを持つユーザーは、段階的な展開の作成ウィザードを開始して、アプリケーションまたはソフトウェアの更新プログラムの段階的な展開を表示することはできます。 ウィザードを完了したり、既存の展開を変更したりすることはできません。

この問題を回避するには、カスタム セキュリティ ロールを作成します。 既存のセキュリティ ロールをコピーし、**段階的展開**オブジェクト クラスに対する次のアクセス許可を追加します。

- 作成  
- 削除  
- 変更  
- 読み取り  

詳しくは、「[カスタム セキュリティ ロールの作成](../configure/configure-role-based-administration.md#BKMK_CreateSecRole)」をご覧ください

## <a name="desktop-analytics"></a>Desktop Analytics

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a> Windows 7 向けの拡張セキュリティ更新プログラムによって、**登録できない**と表示される

<!-- 7283186 -->
_適用対象:Configuration Manager バージョン 1902、1906、1910、および 2002_

2020 年 4 月の Windows 7 向け拡張セキュリティ更新プログラム (ESU) では、diagtrack.dll の最低限必要なバージョンが 10586 から 10240 に変更されました。 この変更により、Windows 7 デバイスが、Desktop Analytics **接続正常性**ダッシュボードに、**登録できない**と表示されます。 この状態のデバイス ビューにドリルダウンすると、**DiagTrack サービス構成**プロパティにより、次の状態が表示されます: `Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`。

この問題は、解決策を必要としません。 4 月の ESU はアンインストールしないでください。 適切に構成されている場合、Windows 7 デバイスにより診断データが Desktop Analytics サービスに引き続き報告され、デバイスはポータルに引き続き表示されます。

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>分散ビューのハードウェア インベントリを使用する場合、Desktop Analytics にオンボードすることはできない

<!-- 4950335 -->
*適用対象:更新プログラムのロールアップが適用された Configuration Manager バージョン 1902、バージョン 1906*

階層があり、サイト レプリケーション リンクで[分散ビュー](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews)の**ハードウェア インベントリ** サイト データを有効にしている場合、Configuration Manager で Desktop Analytics 接続を構成した後、M365UploadWorker.log に次のエラーが記録されます。

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

この問題を回避するには、すべてのサイト レプリケーション リンクで、分散ビューの**ハードウェア インベントリ** サイト データを無効にします。

### <a name="console-unexpectedly-closes-when-removing-collections"></a>コレクションを削除すると、コンソールが突然終了する

<!-- 4749443 -->
*適用対象:更新プログラムのロールアップが適用された Configuration Manager バージョン 1902*

サイトを [Desktop Analytics](../../../../desktop-analytics/connect-configmgr.md) に接続した後、**特定のコレクションを選択して Desktop Analytics と同期する**ことができます。 コレクションを削除し、変更を適用した場合、すぐに新しいコレクションを追加すると未処理の例外が発生します。 コンソールが突然終了します。

この問題を回避するには、コレクションを削除したら、 **[OK]** を選択してプロパティ ウィンドウを閉じます。 次にもう一度プロパティを開き、 **[Desktop Analytics 接続]** タブで新しいコレクションを追加します。

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>パイロット ステータス タイルに一部のデバイスが "未定義" と表示される

<!-- 4547783 -->
*適用対象:更新プログラムのロールアップが適用された Configuration Manager バージョン 1902*

Configuration Manager コンソールを使用してパイロット展開ステータスを監視するときに、パイロット デバイスがその展開計画の Windows のターゲット バージョンと同じであるにもかかわらず、そのデバイスがパイロット ステータス タイルに**未定義**と表示されます。  

このような**未定義**デバイスは、その展開計画の OS のターゲット バージョンと同じ**最新**バージョンです。 特に対応は必要ありません。

## <a name="cloud-services"></a>クラウド サービス

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>米国政府機関向けクラウドの Azure サービスがパブリック クラウドとして表示される

<!-- 6036748 -->

"*適用対象: バージョン 1910*"

Azure サービスへの接続を作成し、 **[Azure 環境]** を政府機関向けクラウドに設定した場合、接続のプロパティで環境が Azure パブリック クラウドとして表示されます。 この問題は、コンソールの表示のみに関する問題であり、サービスは政府機関向けクラウド内にあります。 構成を確認するには、サイト データベースで次の SQL クエリを実行します。

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

政府機関向けクラウドの場合、このクエリの結果はこの特定のテナントに対して `2` になります。

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>TLS 1.2 が有効になっているクラウド管理ゲートウェイからコンテンツをダウンロードできない

<!-- 5771680 -->

*バージョン 1906、1910 早期更新リングに適用*

クラウド管理ゲートウェイ (CMG) を**クラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする**と共に、**TLS 1.2 を強制する**と、コンテンツのダウンロードが失敗することがあります。

クライアント上の DataTransferService.log に次のエラーが表示されます。

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

サーバー上の CMGContentService.log に次のエラーが表示されます。

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

この問題の回避方法:

- 2019 年 12 月 20 にリリースされた、1910 のグローバルで利用できるバージョンにサイトを更新します。 (1910 早期更新リングに以前更新した場合、利用できるとき、このビルドに更新する必要があります。)

- あるいは、従来の[クラウド配布ポイント](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)を使用します。 そのロールで TLS 1.2 は強制されませんが、そのロールは TLS 1.2 を必要とするクライアントと互換性があります。

## <a name="protection"></a>保護

### <a name="bitlocker-management-appears-in-version-1906"></a>バージョン 1906 で BitLocker 管理が表示される

*適用対象: バージョン 1906 以降*

<!-- 5984688 -->

2019 年 11 月 21 日以降、バージョン 1902 以前からバージョン 1906 に更新した場合、BitLocker 管理機能が有効になり、利用可能になります。 この機能はバージョン 1910 からのオプション機能です。 バージョン 1906 ではサポートされていません。 これをバージョン 1906 で使用しようとすると、予期しない結果が発生することがあります。 この機能を使用しない場合、影響はありません。

[BitLocker 管理機能](../../../../protect/plan-design/bitlocker-management.md)を使用するには、バージョン 1910 に更新してください。

<!--
## Backup and recovery

## Client deployment and upgrade
-->
