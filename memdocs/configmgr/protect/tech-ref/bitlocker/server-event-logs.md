---
title: サーバー イベント ログ
titleSuffix: Configuration Manager
description: Windows イベント ログで使用可能な BitLocker (MBAM) サーバー エントリのテクニカル リファレンス
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe7d24bc1cad27094d720a5cb5aa487caec9199d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127867"
---
# <a name="server-event-logs"></a>サーバー イベント ログ

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

Windows イベント ビューアーを使用して、Configuration Manager で次の BitLocker 管理サーバー コンポーネントのイベント ログを表示します。

- 管理ポイントでの回復サービス
- セルフサービス ポータル
- 管理と Web サイトの監視

これらのコンポーネントを 1 つ以上ホストしているサーバーで、イベント ビューアーを開きます。 次に、 **[アプリケーションとサービス ログ]** 、 **[Microsoft]** 、 **[Windows]** の順に移動し、 **[MBAM-Web]** を展開します。 既定では、[管理](#admin)と[操作](#operational)のイベント ログがあります。

以降のセクションには、BitLocker 管理サーバー コンポーネントで発生する可能性があるイベント ID のメッセージとトラブルシューティング情報が含まれています。

## <a name="admin"></a>管理者

### <a name="1-webappspnerror"></a>1:WebAppSpnError

アプリケーション: {SiteName}{VirtualDirectory} で次のサービス プリンシパル名 (SPN):{ListOfSpns}: {ListOfSpns} が見つかりません。アカウント: {ExecutionAccount} に必要な SPN を登録してください。

統合 Windows 認証を成功させるには、必要な SPN を準備しておく必要があります。 このメッセージは、アプリケーションに必要な SPN が正しく構成されていないことを示します。 このイベントに含まれる詳細によって、さらに多くの情報が提供されます。

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100:AdminServiceRecoveryDbError

考えられるエラー メッセージ:

- GetMachineUsers:データベースからユーザー情報を取得中にエラーが発生しました。
- GetRecoveryKey: データベースから回復キーを取得中にエラーが発生しました。
- GetRecoveryKey: データベースからユーザー情報を取得中にエラーが発生しました。
- GetRecoveryKeyIds: データベースから回復キー ID を取得中にエラーが発生しました。
- GetTpmHashForUser:回復データベースから TPM ハッシュ データを取得中にエラーが発生しました。
- GetTpmHashForUser:回復データベースから TPM ハッシュ データを取得中にエラーが発生しました。
- QueryDriveRecoveryData:データベースからドライブの回復データを取得中にエラーが発生しました。
- QueryRecoveryKeyIdsForUser:データベースから回復キー ID を取得中にエラーが発生しました。
- QueryVolumeUsers:データベースからユーザー情報を取得中にエラーが発生しました。

このメッセージは、回復データベースとの通信中に例外が発生するたびに記録されます。 例外に関する特定の詳細情報を取得するには、トレースに含まれている情報に目を通してください。

### <a name="101-adminservicecompliancedberror"></a>101:AdminServiceComplianceDbError

考えられるエラー メッセージ:

- GetRecoveryKey:監査イベントを準拠データベースに記録中にエラーが発生しました。
- GetRecoveryKeyIds:監査イベントを準拠データベースに記録中にエラーが発生しました。
- GetTpmHashForUser:監査イベントを準拠データベースに記録中にエラーが発生しました。
- QueryRecoveryKeyIdsForUser:監査イベントを準拠データベースに記録中にエラーが発生しました。
- QueryDriveRecoveryData:監査イベントを準拠データベースに記録中にエラーが発生しました。

このメッセージは、準拠データベースとの通信中に例外が発生するたびに記録されます。 例外に関する特定の詳細情報を取得するには、トレースに含まれている情報に目を通してください。

### <a name="102-agentservicerecoverydberror"></a>102:AgentServiceRecoveryDbError

このメッセージは、サービスが回復データベースと通信しようとした場合の例外を示します。 例外に関する特定の情報を取得するには、イベントに含まれているメッセージに目を通してください。

MBAM アプリケーション プール アカウントに、回復データベースに接続するために必要なアクセス許可があることを確認します。

### <a name="103-agentserviceerror"></a>103:AgentServiceError

考えられるエラー メッセージ:

- クライアント コンピューター アカウントまたはデータ移行ユーザー アカウントを検出できません。

    `PostKeyRecoveryInfo`、`IsRecoveryKeyResetRequired`、`CommitRecoveryKeyRest`、`GetTpmHash` のいずれかの Web メソッドに対して呼び出しが行われるたびに、呼び出し元の資格情報を取得するために呼び出し元のコンテキストが取得されます。 呼び出し元のコンテキストが null または空の場合、サービスによりこのメッセージがログに記録されます。

- 呼び出し元 ID のアカウントの検証に失敗しました。

    このメッセージは、Web メソッドが呼び出し元がコンピューター アカウントであることを予期していて、それ以外の場合にログに記録されます。 また、Web メソッドが呼び出し元がユーザー アカウントであることを予期していて、ユーザー アカウントまたはデータ移行グループ アカウントのメンバーではない場合にも発生する可能性があります。

### <a name="104-statusservicecompliancedbconfigerror"></a>104:StatusServiceComplianceDbConfigError

レジストリ内の準拠データベース接続文字列が空です。

このメッセージは、準拠データベース接続文字列が無効な場合にログに記録されます。 レジストリ キー `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` の値を確認します。

### <a name="105-statusservicecompliancedberror"></a>105:StatusServiceComplianceDbError

このエラーは、Web サイトまたは Web サービスが準拠データベースに接続できなかったことを示します。 IIS アプリケーション プール アカウントがデータベースに接続できることを確認します。

### <a name="106-helpdeskerror"></a>106:HelpdeskError

既知のエラーと考えられる原因:

- URL への要求により、内部エラーが発生しました。

    Administration and Monitoring Web サイト (ヘルプデスク) 用のアプリケーションで、ハンドルされない例外が発生しました。 **管理者**イベント ログでログ エントリを確認して、特定の例外を見つけます。

- 実行コンテキスト情報の取得中にエラーが発生しました。 サービス プリンシパル名 (SPN) の登録を確認できません。

    最初のヘルプデスク Web サイトの読み込み操作中に、SPN が確認されます。 SPN を確認するには、アカウント情報、IIS Sitename、およびヘルプデスクの Web サイトに対応する ApplicationVirtualPath が必要です。 このエラー メッセージは、これらの属性の 1 つ以上が無効であるか見つからない場合にログに記録されます。

- サービス プリンシパル名 (SPN) の登録の検証中にエラーが発生しました。

    このメッセージは、SPN の検証時にセキュリティ例外がスローされることを示します。 イベントの詳細に含まれている例外を参照してください。

### <a name="107-selfserviceportalerror"></a>107:SelfServicePortalError

既知のエラーと考えられる原因:

- ユーザーの回復キーを取得中にエラーが発生しました。

    回復キーを取得する要求が行われたときに、予期しない例外がスローされたことを示します。 イベントの詳細にある例外メッセージを参照してください。 ヘルプデスク アプリでトレースが有効になっている場合は、トレース データを参照して詳細な例外メッセージを取得してください。

- 実行コンテキスト情報の取得中にエラーが発生しました。 サービス プリンシパル名 (SPN) の登録を確認できません。

    セルフサービス ポータルでは、最初の読み込み操作中に、SPN を検証するために、セルフサービス Web サイトのアカウント情報、IIS Sitename、および ApplicationVirtualPath が取得されます。 このエラー メッセージは、これらの属性の 1 つ以上が無効な場合にログに記録されます。

- サービス プリンシパル名 (SPN) の登録の検証中にエラーが発生しました。 EventDetails:{ExceptionMessage}

    このメッセージは、SPN の検証中にセキュリティ例外がスローされたことを示します。 イベントの詳細に含まれている例外を参照してください。

### <a name="108-domaincontrollererror"></a>108:DomainControllerError

既知のエラーと考えられる原因:

- ドメイン名 {DomainName} の解決中にエラーが発生し、メモリ割り当てエラーが発生しました。

    ドメイン名を解決するには、`DsGetDcName` Windows API を呼び出します。 このメッセージは、この API がメモリ割り当てエラーを示す `ERROR_NOT_ENOUGH_MEMORY` を返したときにログに記録されます。

- DsGetDcName メソッドを呼び出せませんでした

    このメッセージは、`DsGetDcName` API がホストで使用できないことを示します。

### <a name="109-webapprecoverydberror"></a>109:WebAppRecoveryDbError

既知のエラーと考えられる原因:

- 回復データベースの構成の読み取り中にエラーが発生しました。 回復データベースへの接続文字列が構成されていません。

    このメッセージは、`HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` にある回復データベースの接続文字列情報が無効であることを示します。 指定されたレジストリ キーの値を確認してください。

次のいずれかのメッセージが表示された場合は、IIS サーバーからのアプリケーション プールの資格情報が回復データベースに接続できるかどうかを確認します。

- DoesUserHaveMatchingRecoveryKey: ユーザーの回復キー ID を取得中にエラーが発生しました。
- QueryDriveRecoveryData: ドライブの回復データを取得中にエラーが発生しました。
- QueryRecoveryKeyIdsForUser: ユーザーの回復キー ID を取得中にエラーが発生しました。
- 回復データベースから TPM パスワード ハッシュを取得中にエラーが発生しました。

### <a name="110-webappcompliancedberror"></a>110:WebAppComplianceDbError

既知のエラーと考えられる原因:

- 準拠データベースの構成を読み取り中にエラーが発生しました。 準拠データベースへの接続文字列が構成されていません。

    このメッセージは、`HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` にある準拠データベースの接続文字列情報が無効であることを示します。 このレジストリ キーの値を確認します。

次のいずれかのメッセージが表示された場合は、IIS サーバーからのアプリケーション プールの資格情報が準拠データベースに接続できるかどうかを確認します。

- GetRecoveryKeyForCurrentUser: 監査イベントを準拠データベースに記録中にエラーが発生しました。
- QueryRecoveryKeyIdsForUser: 監査イベントを準拠データベースに記録中にエラーが発生しました。
- QueryRecoveryKeyIdsForUser: 監査イベントを準拠データベースに記録中にエラーが発生しました。

### <a name="111-webappdberror"></a>111:WebAppDbError

これらのエラーは、次の 2 つの状態のいずれかを示します。

- MBAM Web サイトまたは Web サービスが、準拠データベースまたは回復データベースに接続できませんでした
- MBAM Web サイトまたは Web サービスの実行アカウント (アプリケーション プール アカウント) が、準拠データベースまたは回復データベースで `GetVersion` ストアド プロシージャを実行できませんでした

イベントに含まれるメッセージは、例外の詳細を提供します。

アプリケーション プール アカウントが、準拠データベースまたは回復データベースに接続できることを確認します。 `GetVersion` ストアド プロシージャを実行する権限があることを確認します。

### <a name="112-webapperror"></a>112:WebAppError

サービス プリンシパル名 (SPN) の登録の検証中にエラーが発生しました。

SPN を検証するには、Active Directory に対してクエリを実行して、SPN がマップされた実行アカウントの一覧を取得します。 また、`ApplicationHost.config` に対してクエリを行い、Web サイトのバインドを取得します。 このエラー メッセージは、Active Directory と通信できなかったか、`ApplicationHost.config` ファイルを読み込めなかったことを示します。

アプリケーション プール アカウントに、Active Directory または `ApplicationHost.config` ファイルに対してクエリを実行する権限があることを確認します。 また、`ApplicationHost.config` ファイル内のサイト バインド エントリも確認します。

## <a name="operational"></a>操作可

### <a name="4-performancecountererror"></a>4:PerformanceCounterError

パフォーマンス カウンターの取得中にエラーが発生しました。

トレース メッセージには、実際の例外メッセージが含まれています。その一部を次に示します。

- ArgumentNullException:この例外は、要求されたパフォーマンス カウンターのカテゴリ、カウンター、またはインスタンスが無効な場合にスローされます。
- System.InvalidOperationException: categoryName は空の文字列 ("") です。 counterName は空の文字列 ("") です。
- 要求された読み取り/書き込みアクセス許可の設定は、このカウンターでは無効です。
- 指定されたカテゴリが存在しません (readOnly が true の場合)。
- 指定されたカテゴリは .NET Framework カスタム カテゴリではありません (readOnly が false の場合)。
- 指定されたカテゴリは複数インスタンスとしてマークされており、インスタンス名を使用してパフォーマンス カウンターを作成する必要があります。
- instanceName が 127 文字を超えています。
- categoryName と counterName が、異なる言語にローカライズされています。
- System.ComponentModel.Win32Exception:システム API へのアクセス中にエラーが発生しました。
- System.UnauthorizedAccessException:管理者特権を使用せずに実行されているコードが、パフォーマンス カウンターを読み取ろうとしました。

イベントに含まれるメッセージでは、例外の詳細が提供されます。

`System.UnauthorizedAccessException` については、アプリケーション プール アカウントにパフォーマンス カウンター API へのアクセス権があることを確認します。

### <a name="200-helpdeskinformation"></a>200:HelpDeskInformation

管理 Web サイト アプリケーションが正常に検出され、サポートされているバージョンの回復データベースまたは準拠データベースに接続されました。

ヘルプデスク Web サイトから回復データベースまたは準拠データベースに正常に接続されたことを示します。

### <a name="201-selfserviceportalinformation"></a>201:SelfServicePortalInformation

セルフサービス ポータル アプリケーションが正常に検出され、サポートされているバージョンの回復データベースまたは準拠データベースに接続されました。

セルフサービス ポータルから回復データベースまたは準拠データベースに正常に接続されたことを示します。

### <a name="202-webappinformation"></a>202:WebAppInformation

アプリケーションに SPN が正しく登録されています。

ヘルプデスク Web サイトに必要な SPN が、実行中のアカウントに正しく登録されていることを示します。

## <a name="see-also"></a>関連項目

これらのログの使用方法の詳細については、「[BitLocker イベント ログ](about-event-logs.md)」を参照してください。

トラブルシューティングに関する詳細については、「[BitLocker のトラブルシューティング](troubleshoot.md)」をご覧ください。

これらの Web サイトのインストールの詳細については、「[BitLocker のレポートとポータルのセットアップ](../../deploy-use/bitlocker/setup-websites.md)」を参照してください。
