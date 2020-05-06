---
title: MSfB 統合の問題解決
titleSuffix: Configuration Manager
description: ビジネス向けおよび教育機関向け Microsoft Store の統合における最も一般的な問題のトラブルシューティングを行うための推奨事項と解決策について説明します。
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149115"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Configuration Manager を使用したビジネス向けおよび教育機関向け Microsoft Store の統合のトラブルシューティング

この記事では、Configuration Manager を使用した、ビジネス向けおよび教育機関向け Microsoft Store (MSfB) の統合の主なトラブルシューティングのヒントと修正について説明します。

Configuration Manager によるビジネス向けおよび教育機関向け Microsoft Store の使用の詳細については、「[Configuration Manager を使用してビジネス向けおよび教育機関向け Microsoft Store のアプリを管理する](manage-apps-from-the-windows-store-for-business.md)」を参照してください。

## <a name="monitor"></a>モニター

### <a name="component-status"></a>コンポーネントの状態

Configuration Manager コンソールで、 **[監視]** ワークスペースに移動し、 **[システム ステータス]** を展開し、 **[コンポーネントのステータス]** ノードを選択します。 次のコンポーネントについて状態をモニターします。

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>同期の状態

Configuration Manager コンソールで **[管理]** ワークスペースに進み、 **[クラウド サービス]** を展開して **[ビジネス向け Microsoft Store]** ノードを選択します。 **[最後の同期の状態]** 列を確認します。

### <a name="view-synchronized-apps"></a>同期されたアプリの表示

Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開し、 **[ストア アプリのライセンス情報]** を選択します。


## <a name="log-files"></a>ログ ファイル

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker.log

このログ ファイルはサービス接続ポイントにあり、Configuration Manager インストール ディレクトリの `\Logs` にあります。 クラウド サービスとの通信に関する情報を記録します。 この情報には、メタデータ、アイコン、パッケージ、およびライセンス ファイルの取得が含まれます。

ログ レベルを変更するには、`HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` レジストリキーで `LoggingLevel` の値を `0` に変更します。 詳細については、「[ログのオプションの構成](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site)」を参照してください。

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION.log

このログ ファイルはサービス接続ポイントにあり、Configuration Manager インストール ディレクトリの `\Logs` にあります。 WSfBSyncWorker サービスが開始されていないか、繰り返し開始および停止されている場合は、このログ ファイル内のエントリを確認します。

> [!NOTE]
> このログ ファイルは、他の機能と共有されています。

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker.log

このログ ファイルは、階層内の最上位サイトのサイト サーバーにあります。 Configuration Manager インストール ディレクトリの `\Logs` にあります。 次のプロセスに関する情報を記録します。

- BusinessAppProcessWorker コンポーネントによって同期されたメタデータ情報のデータベースへの挿入
- `\InstallDir\inboxes\businessappprocess.box` のファイルの処理

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER.log

このログ ファイルは、階層内の最上位サイトのサイト サーバーにあります。 Configuration Manager インストール ディレクトリの `\Logs` にあります。 BusinessAppProcessWorker サービスが開始されていないか、繰り返し開始および停止されている場合は、このログ ファイル内のエントリを確認します。



## <a name="last-sync-failed"></a>前回の同期は失敗しました

最後の同期の状態が*失敗*の場合は、次の[ログ ファイル](#log-files)を確認して、症状を特定します。

- WSfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

一般的な問題については、次のいずれかのセクションを参照してください。

- [承認エラー](#bkmk_fail-symptom1)
- [秘密鍵が無効](#bkmk_fail-symptom2)
- [アプリケーション トークンの取得エラー](#bkmk_fail-symptom3)
- [コンテンツの場所が存在しないかアクセス許可が正しくない](#bkmk_fail-symptom4)
- ['GET' メソッドを呼び出している http 要求を実行中にエラーが発生](#bkmk_fail-symptom5)
- [バッファーにさらにバイトを書き込むことができない](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a> 承認エラー

#### <a name="cause"></a>原因

この問題は、構成された Azure Active Directory (Azure AD) アプリケーションに、このテナントのビジネス向けおよび教育機関向け Microsoft Store を管理するための権限がない場合に発生する可能性があります。

#### <a name="workaround"></a>回避策

1. ビジネス向けまたは教育機関向け Microsoft Store ポータルに管理者としてサインインします。
1. **[設定]** にアクセスし、 **[管理ツール]** を選択します。
1. アプリケーションが一覧に表示されない場合は、 **[管理ツールの追加]** を選択します。 次に、名前で検索し、Configuration Manager と同じ ClientID に関連付けられている Azure AD アプリケーションを選択します。
1. 状態が **[アクティブ]** と表示されない場合は、 **[アクション]** セクションで **[アクティブ化]** を選択します。
1. Configuration Manager コンソールで **[管理]** ワークスペースに進み、 **[クラウド サービス]** を展開して **[ビジネス向け Microsoft Store]** ノードを選択します。 ストアと同期するか、次の同期間隔が発生するまで待機します。

> [!Tip]
> Configuration Manager で ClientID を検索するには、次のようにします。
>
> 1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[クラウド サービス]** を展開して **[Azure Active Directory テナント]** ノードを選択します。
> 1. ビジネス向けおよび教育機関向け Microsoft Store に使用するテナントを選択します。
> 1. 詳細ウィンドウで、対応するアプリケーションを見つけ、 **[クライアント ID]** 列を確認します。

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a> 秘密鍵が無効

#### <a name="cause"></a>原因

この問題が発生する可能性があるのは、Azure AD アプリでビジネス向けおよび教育機関向け Microsoft Store に対する秘密鍵の有効期限が切れている場合です。

#### <a name="resolution"></a>解決策

Azure AD アプリケーションの秘密鍵を更新します。 詳細については、[秘密鍵の更新](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew)に関するページを参照してください。

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a> アプリケーション トークンの取得エラー

#### <a name="cause"></a>原因

この問題は、接続されているアプリが Azure AD に存在しなくなった場合に発生する可能性があります。

#### <a name="resolution"></a>解決策

ビジネス向けおよび教育機関向け Microsoft Store への接続を削除し、再作成します。

1. Configuration Manager コンソールで **[管理]** ワークスペースに進み、 **[クラウド サービス]** を展開して **[ビジネス向け Microsoft Store]** ノードを選択します。
1. 既存の接続を選択します。
1. リボンで **[削除]** を選択します。

次に、接続を再作成します。 詳細については、以下の記事を参照してください。

- [Azure サービスの構成](../../core/servers/deploy/configure/azure-services-wizard.md)
- [ビジネス向けおよび教育機関向け Microsoft Store の同期を設定する](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a> コンテンツの場所が存在しないかアクセス許可が正しくない

#### <a name="cause"></a>原因

ビジネス向けおよび教育機関向け Microsoft Store の接続を設定する場合は、同期されたコンテンツを格納するためのネットワーク共有を指定します。 この共有が存在しない場合、またはアクセス許可が正しくない場合に、この問題が発生する可能性があります。 サービス接続ポイントのコンピューター アカウントは、このディレクトリおよびすべてのサブディレクトリの所有者にするようにします。<!-- memdocs#146 --> そうしないと、次のようなエラーが表示されます。

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

構成した場所を確認するには、次のようにします。

1. Configuration Manager コンソールで **[管理]** ワークスペースに進み、 **[クラウド サービス]** を展開して **[ビジネス向け Microsoft Store]** ノードを選択します。

1. アカウントを選択し、 **[プロパティ]** を開きます。

1. **[構成]** タブに切り替えます。 **[場所]** 設定には、ビジネス向けおよび教育用 Microsoft Store からダウンロードしたアプリケーション コンテンツを格納するためのネットワーク パスが表示されます。

#### <a name="workaround"></a>回避策

1. まだ存在しない場合は、共有を作成します。

1. フォルダーに対する NTFS アクセス許可と、ネットワーク共有に対するアクセス許可を確認します。 サービス接続ポイントのコンピューター アカウントに**読み取り**と**書き込み**のアクセス許可を付与します。

場所を再構成する場合は、接続を削除し、新しいコンテンツの場所との接続を再作成します。

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a> 'GET' メソッドを呼び出している http 要求を実行中にエラーが発生

#### <a name="cause"></a>原因

この問題は、ストアからのアプリケーションの同期に時間がかかりすぎ、コンテンツ URL の有効期限が切れた場合に発生する可能性があります。

#### <a name="workaround"></a>回避策

同期プロセスの再試行

1. Configuration Manager コンソールで **[管理]** ワークスペースに進み、 **[クラウド サービス]** を展開して **[ビジネス向け Microsoft Store]** ノードを選択します。
1. 接続を選択します。 リボンで、 **[ビジネス向け Microsoft Store からの同期]** を選択します。

行うたび、さらに進みます。 次の要因によっては、いくつかの再試行が必要になる場合があります。

- オフライン アプリケーションの数
- パッケージのサイズ
- ネットワーク速度

各試行で、エラーの発生回数が減少するはずです。 エラーの数が減少しない場合は、別の問題があります。

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a> バッファーにさらにバイトを書き込むことができない

#### <a name="cause"></a>原因

この問題は、アプリケーションのパッケージが 500 MB を超えている場合に発生する可能性があります。 Configuration Manager は、パッケージが 500 MB 未満のオフライン アプリケーションの自動同期のみをサポートしています。

#### <a name="workaround"></a>回避策

これらのアプリを自動的に同期することはできませんが、コンテンツをダウンロードし、アプリケーションを手動で作成することができます。

1. **WSfbSynWorker.log** の次の行から、失敗したアプリケーション ID を取得します。

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. ビジネス向けまたは教育機関向け Microsoft Store ポータルに管理者としてサインインします。 このアプリケーションのページを検索します。

    > [!Tip]
    > ページの URL は `https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID` のようになります。 

    1. 既に選択されていない場合は **[オフライン]** を選択します。 その後、 **[管理]** を選択します。

    1. サポートされているすべてのプラットフォームについて、アプリケーション コンテンツ共有に別々のフォルダーを作成します。

    1. パッケージをパッケージ フォルダーにダウンロードします。

    1. エンコードされたライセンス ファイルを `.bin` ファイルとしてパッケージ フォルダーにダウンロードします。

    1. 必要なすべてのフレームワークをパッケージ フォルダーにダウンロードします。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** ノードを選択します。

1. [アプリケーションを作成](create-applications.md)し、アプリケーションの情報を手動で指定します。

    1. 以前にダウンロードした、サポートされているプラットフォームごとに、展開の種類を作成します。

    1. 種類:**Windows アプリ パッケージ (\*.appx、\*.appxbundle)**

    1. 必須の依存関係パッケージではなく、実際のアプリ パッケージの appx/appxbundle を指定します。

最後の **[情報のインポート]** ページで、次の詳細を確認します。

- **ライセンス ファイル:** `.bin` ファイルを指定します。 このライセンス ファイルは、オフライン アプリに必要です。
- **Windows アプリケーションの依存関係:** このパッケージに必要なすべての依存関係がダウンロードされていることを確認します。


## <a name="sync-doesnt-run"></a>同期が実行されない

このセクションでは、次の同期の問題を取り上げます。

- 同期プロセスを手動で開始したが、実行されない
- サイトが毎日自動的に同期されない

まず次の[ログ ファイル](#log-files)を確認して、症状を特定します。

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER.log
- WsfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

一般的な問題については、次のいずれかのセクションを参照してください。

- [手動同期が開始しない](#bkmk_sync-symptom1)
- [毎日の自動同期は実行されず、SMS_BUSINESS_APP_PROCESS_MANAGER.log で "# のワーカーをシャットダウンしています" というエラーが発生する](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a> 手動同期が開始しない

#### <a name="cause"></a>原因

この問題は、前回の同期後 10 分未満に同期を開始した場合に発生する可能性があります。10 分ごとよりも多く同期することはできません。

#### <a name="resolution"></a>解決策

別の同期を開始する前に、少なくとも 10 分間待機します。

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a> 毎日の自動同期は実行されず、SMS_BUSINESS_APP_PROCESS_MANAGER.log で "# のワーカーをシャットダウンしています" というエラーが発生する

#### <a name="cause"></a>原因

この問題は、SMS_BUSINESS_APP_PROCESS_MANAGER コンポーネントが WsfbSyncWorker スレッドを停止した場合に発生する可能性があります。 このエラーでは、`2` または `4` のワーカーが指定されている可能性があります。

#### <a name="workaround"></a>回避策

**SMS_EXECUTIVE** サービスを再起動します。

このメイン サービスを再起動できない場合は、MSfB ワーカーで両方のコンポーネントを停止した後、両方を開始します。

1. サービス接続ポイントを実行しているサーバーで Windows レジストリを開きます。

1. `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION` に移動します。

    1. 要求された操作を**停止**に設定します。

    1. 最新の状態が**停止**であることを確認するために更新します。

1. `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER` に移動します。

    1. 要求された操作を**停止**に設定します。

    1. 最新の状態が**停止**であることを確認するために更新します。

1. **SMS_CLOUDCONNECTION** で、要求された操作を**開始**に設定します。

1. **SMS_BUSINESS_APP_PROCESS_MANAGER** で、要求された操作を**開始**に設定します。


## <a name="language-related-issues"></a>言語関連の問題

このセクションには次の一般的な問題が含まれます。

- [言語選択の変更が適用されていない](#bkmk_lang-symptom1)
- [すべてのライセンス情報に対して選択された言語が存在していない場合がある](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a> 言語選択の変更が適用されていない

#### <a name="cause"></a>原因

この問題は、言語の選択がキャッシュされ、プロパティ値が変更された後にクリアされていない場合に発生する可能性があります。

#### <a name="workaround"></a>回避策

この問題を解決するには **SMS_Executive** サービスを再起動します。

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a> すべてのライセンス情報に対して選択された言語が存在していない場合がある

#### <a name="cause"></a>原因

この問題は、ビジネス向けおよび教育機関向け Microsoft Store のアプリケーションのライセンス情報に、指定言語のローカライズされたデータが含まれていない場合に発生する可能性があります。

#### <a name="workaround"></a>回避策

作成されたアプリケーションに不足している言語を手動で追加します。


## <a name="offline-applications"></a>オフライン アプリケーション

このセクションには次の一般的な問題が含まれます。

- [コンテンツを検証できないため、オフライン アプリケーションを作成できない](#bkmk_off-symptom1)
- [オフライン ライセンス情報から作成されたアプリケーションをインストールできない](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a> コンテンツを検証できないため、オフライン アプリケーションを作成できない

#### <a name="cause"></a>原因

この問題は、オフライン アプリケーションの同期されたコンテンツが壊れているか変更されている場合に発生する可能性があります。

#### <a name="workaround"></a>回避策

新しく同期を開始します。同期が完了すると、正しくないコンテンツ ファイルを検証してダウンロードするはずです。

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a> オフライン ライセンス情報から作成されたアプリケーションをインストールできない

#### <a name="cause"></a>原因

この問題は、バージョン 1511 より前のバージョンの Windows 10 を実行しているクライアントにアプリケーションを展開した場合に発生する可能性があります。 ビジネス向けおよび教育機関向け Microsoft Store のオフライン ライセンス アプリは、Windows 10 バージョン 1511 以降でのみサポートされています。

#### <a name="resolution"></a>解決策

最新バージョンの Windows 10 をインストールします。


## <a name="next-steps"></a>次のステップ

「[Configuration Manager の使用に関するヘルプの検索](../../core/understand/find-help.md)」を参照してください。
