---
title: 状態メッセージ
titleSuffix: Configuration Manager
description: サポートされているバージョンの Configuration Manager での状態メッセージの説明。
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704590"
---
# <a name="state-messages-in-configuration-manager"></a>Configuration Manager の状態メッセージ 

*適用対象:Configuration Manager (Current Branch)*

状態メッセージには、Configuration Manager クライアントの状態に関する簡潔な情報が含まれます。 状態メッセージング システムは、ソフトウェア更新プログラムや構成設定など、Configuration Manager の特定のコンポーネントで使用されます。

Configuration Manager クライアントによって、状態メッセージがフォールバック ステータス ポイントまたは管理ポイント サイト システムに送信され、動作の現在の状態が報告されます。 Configuration Manager クライアントによって送信される状態メッセージを表示するためのレポートを作成できます。

状態メッセージを使用する Configuration Manager の各機能は、状態メッセージのトピックの種類によって特定されます。 この記事にリストされている状態メッセージのトピックの種類を使用することで、状態メッセージが関連する Configuration Manager の機能を定義できます。

> [!NOTE]  
> 状態メッセージの ID 値がゼロ (0) の場合は、通常、トピックの種類が不明な状態であることを示します。

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 0 | コンプライアンスの状態が不明です|
| 1 | [準拠] | 
| 2 | 非対応 | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 0  | 強制状態が不明です |
| 1  | 更新プログラムをインストールしています        | 
| 2  | 再起動を待機しています          | 
| 3  | 他のインストールが完了するのを待機しています         | 
| 4  | 更新は正常にインストールされました (2)          | 
| 5  | システムの再起動を保留しています         | 
| 6  | 更新のインストールに失敗しました         | 
| 7  | 更新をダウンロードしています   | 
| 8  | 更新プログラムをダウンロードしました    | 
| 9  | 更新プログラムのダウンロードに失敗しました     | 
| 10 | インストール前にメンテナンス期間を待機しています         | 
| 11 | オーケストレーションを待機中         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|      
| 0 | 評価状態が不明です|                 
| 1 |評価が有効になりました      |
| 2 |評価に成功しました      |
| 3 |評価に失敗しました      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 0 | 検出状態が不明です|
| 1 | 必要なし   |
| 2 | 検出なし    |
| 3 | 検出   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 0 | コンプライアンスの状態が不明です|
| 1 |[準拠]     |
| 2 |非対応     |
| 3 |競合が検出されました    |
| 4 |エラー      |
| 5 |Unknown     |
| 6 |部分的なコンプライアンス   |
| 7 |コンプライアンスが構成されていません    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 0  | 強制状態が不明です|
| 1  |強制実行が開始されました          |
| 2  |強制実行はコンテンツを待機しています         |
| 3  | 他のインストールが完了するのを待機しています        |
| 4  |インストール前にメンテナンス期間を待機しています         |
| 5  |インストールする前に再起動する必要があります         |
| 6  |一般エラー        |
| 7  |インストール待ち         |
| 8  |更新をインストールしています          |
| 9  |システムの再起動を保留しています        |
| 10 |更新は正常にインストールされました         |
| 11 |更新のインストールに失敗しました        |
| 12 |更新をダウンロードしています        |
| 13 | 更新をダウンロードしました        |
| 14 |更新をダウンロードできませんでした        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
|0 |検出状態が不明です|
| 1 | 更新を行う必要はありません  |
| 2 | 更新を行う必要があります   |
| 3 | 更新プログラムがインストールされました  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 0 |スキャン状態が不明です|
| 1 | スキャンはコンテンツを待っています   |
| 2 | スキャンを実行しています    |
| 3 | スキャンが完了しました    |
| 4 | スキャンは再試行を保留しています   |
| 5 | スキャンに失敗しました   |
| 6 | スキャンは完了しましたがエラーが発生しました |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

状態 ID はありません。

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

状態 ID はありません。

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
状態 ID はありません。

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 100 |クライアントの展開が開始されました      |       
| 101 |ダウンロードを待機しています       |       
| 102 |展開がスケジュールされました       |       
| 103 | 展開する前に期間を待機しています |
| 104 |展開がスキップされました       |       
| 301 |不明なクライアント展開のエラーです |       
| 302 |ccmsetup サービスを作成できませんでした  |       
| 303 |ccmsetup サービスを削除できませんでした |       
| 304 |システム ドライブでファイルベースの書き込みフィルター (FBWF) が有効になっている埋め込みオペレーティング システムを上書きしてインストールすることはできません |       
| 305 |ネイティブのセキュリティ モードは Windows 2000 では無効です  |       
| 306 |ccmsetup ダウンロード処理を開始できませんでした  |       
| 307 |ccmsetup のコマンド ラインが無効です |       
| 308 |WINHTTP によるファイルのダウンロードに失敗したアドレス |       
| 309 |BITS によるファイルのダウンロードに失敗したアドレス |       
| 310 |BITS バージョンのインストールが失敗しました |       
| 311 |前提条件ファイルに MS の署名があることを確認できません  |       
| 312 |ディスクがいっぱいのため、ファイルをコピーできませんでした |       
| 313 |Client.msi のインストールが MSI エラーのために失敗しました |       
| 314 |ccmsetup.xml マニフェスト ファイルを読み込めませんでした |       
| 315 |クライアント証明書を取得できませんでした  |       
| 316 |前提条件ファイルに MS の署名がありません |       
| 317 |インストールを続けるには再起動が必要です  |       
| 318 |MP とクライアントのバージョンが一致しないため、MP にクライアントをインストールできません |       
| 319 |オペレーティング システムまたはサービス パックはサポートされていません  |       
| 320 |展開がサポートされていません       |       
| 321 |BITS がありません        |       
| 322 |ソース フォルダーは利用できません       |       
| 323 |Appv はサポートされていません              |       
| 324 |サイトのバージョンが正しくありません              |       
| 325 |前提条件のハッシュが一致しません       |       
| 326 |MDM の登録を解除できませんでした      |       
| 327 |MDM 登録が検出されました      |       
| 328 |Intune が検出されました       |       
| 329 |従量制課金接続が許可されていません      |       
| 400 |クライアントの展開に成功しました |  
| 401 |展開が正常に完了しました。再起動が必要です     |       
| 402 |展開が正常に完了し、再起動が正常に完了しました     |
| 500 |クライアントの割り当てが開始されました|
| 601 |不明なクライアント割り当てのエラーです|
| 602 |次のサイト コードは無効です|
| 603 |MP に割り当てることができませんでした|
| 604 |既定の管理ポイントを検出できませんでした|
| 605 |サイト署名証明書をダウンロードできませんでした|
| 606 |サイト コードを自動検出できませんでした|
| 607 |サイトの割り当てに失敗しました。クライアントのバージョンがサイトのバージョンより上位になっています|
| 608 |Active Directory Domain Services および SLP からサイト バージョンを取得できませんでした|
| 609 |クライアント バージョンを取得できませんでした|
| 700 |クライアントの割り当てに成功しました|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

状態 ID はありません。

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 100 | 登録ステータス   |
| 101 | 登録がスケジュールされました   |
| 102 | 登録が取り消されました   |
| 105 | 登録が開始されました   |
| 106 | 登録には成功しましたが、プロビジョニングされていません
| 107 | 登録に成功し、プロビジョニングされました
| 108 | アクティブ ユーザーが登録されていません   |
| 110 | 登録できませんでした   |


## <a name="820--state_topictype_client_wufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 | Windows Update for Business クライアントの状態| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 | ディスク領域   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

状態 ID はありません。

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

状態 ID はありません。

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

状態 ID はありません。

## <a name="1000--state_topictype_client_framework_comm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 | クライアントは管理ポイントと正常に通信しています |
| 2 | クライアントは管理ポイントと通信できませんでした |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |クライアントはローカルの証明書ストアから証明書を正常に取得しました    |
| 2 |クライアントはローカルの証明書ストアから証明書を取得できませんでした |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

状態 ID はありません。

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

状態 ID はありません。

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

状態 ID はありません。

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

状態 ID はありません。

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

状態 ID はありません。

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

状態 ID はありません。

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

状態 ID はありません。

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

状態 ID はありません。

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

状態 ID はありません。

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

状態 ID はありません。

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

状態 ID はありません。

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

状態 ID はありません。

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

状態 ID はありません。

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

状態 ID はありません。

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |クライアントはネイティブ モードの準備ができていません  |
| 2 |クライアントはネイティブ モードの準備ができています     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 | 成功|
| 2 | 失敗 |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

状態 ID はありません。

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

状態 ID はありません。

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

状態 ID はありません。

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

状態 ID はありません。 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |ユーザー アフィニティが設定されました       |
| 2 |ユーザー アフィニティが削除されました       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

状態 ID はありません。

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

状態 ID はありません。

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1000  |構成項目に成功           |
| 1001 |構成項目に成功。既にインストール済み         |
| 1002 |構成項目に成功。プレフライト          |
| 1003 |構成項目は高速。状態は成功          |
| 2000 |構成項目が進行中           |
| 2001 |構成項目が進行中。コンテンツの待機中         |
| 2002 |構成項目が進行中。インストール中          |
| 2003 |構成項目が進行中。再起動の待機中         |
| 2004 |構成項目が進行中。メンテナンス期間の待機中        |
| 2005 |構成項目が進行中。スケジュールの待機中         |
| 2006 |構成項目が進行中。依存コンテンツをダウンロード中     |
| 2007 |構成項目が進行中。依存関係をインストール中        |
| 2008 |構成項目が進行中。再起動の保留中         |
| 2009 |構成項目が進行中。コンテンツのダウンロードが完了         |
| 2010 |構成項目が進行中。更新の保留中         |
| 2011 |構成項目が進行中。ユーザー再接続の待機中        |
| 2012 で保護されたプロセスとして起動されました |構成項目が進行中。ユーザー サインアウトの待機中         |
| 2013 |構成項目が進行中。ユーザー サインインの待機中         |
| 2014 |構成項目が進行中。インストールの待機中         |
| 2015 |構成項目が進行中。再試行の待機中         |
| 2016 |構成項目が進行中。presmode の待機中         |
| 2017 |構成項目が進行中。オーケストレーションの待機中        |
| 2018 |構成項目が進行中。ネットワークの待機中         |
| 2019 |構成項目が進行中。VE 更新の保留中         |
| 2020 |構成項目が進行中。VE を更新中         |
| 3000 |構成項目の要件が満たされていません           |
| 3001 |構成項目の要件が満たされていません。ホストを適用できません        |
| 4000 |構成項目が不明           |
| 5000 |構成項目エラー            |
| 5001 |構成項目の評価中のエラー          |
| 5002 |構成項目のインストール中のエラー          |
| 5003 |構成項目のコンテンツ取得中のエラー         |
| 5004 |構成項目の依存関係のインストール中のエラー         |
| 5005 |構成項目のコンテンツ依存関係の取得中のエラー        |
| 5006 |構成項目のルール競合エラー          |
| 5007 |構成項目の再試行待機中のエラー          |
| 5008 |構成項目の置き換えのアンインストール中のエラー        |
| 5009 |構成項目の置き換え済みのダウンロード中のエラー         |
| 5010 |構成項目の VE 更新中のエラー          |
| 5011 |構成項目のライセンス インストール中のエラー         |
| 5012 |構成項目の許可するすべての信頼されたアプリの取得中のエラー       |
| 5013 |構成項目エラー。利用可能なライセンスがありません         |
| 5014 |構成項目エラー。OS がサポートされていません          |
| 6000 |構成項目の起動に成功しました            |
| 6010 |構成項目の起動エラー            |
| 6020 |構成項目の不明な起動|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

状態 ID はありません。

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

状態 ID はありません。

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

状態 ID はありません。

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

状態 ID はありません。

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

状態 ID はありません。

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

状態 ID はありません。

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

状態 ID はありません。

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

状態 ID はありません。

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |Endpoint Protection が管理されていません   |
| 2 |Endpoint Protection のインストールの待機中  |
| 3 |Endpoint Protection は管理されています   |
| 4 |Endpoint Protection のインストールに失敗しました  |
| 5 |Endpoint Protection の再起動の保留中  |
| 6 |Endpoint Protection はサポートされていません   |
| 7 |Endpoint Protection は共同管理されています   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 0 |Endpoint Protection ポリシーの適用状態が不明です    |
| 1 |Endpoint Protection ポリシーの適用に成功しました    |
| 2 |Endpoint Protection ポリシーの適用に失敗しました    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 0 |  Unknown    |
| 1 |  Active    |
| 2 |  非アクティブ    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 | Wakeup Proxy がインストールされていません    |
| 2 | Wakeup Proxy のインストールを待機しています   |
| 3 | Wakeup Proxy がインストールされました    |
| 4 | Wakeup Proxy のインストールに失敗しました   |
| 5 | Wakeup Proxy の再起動を待機しています   |
| 6 | Wakeup Proxy はこの OS でサポートされていません  |
| 7 | Wakeup Proxy サーバーのオプトアウト   |
| 8 | Wakeup Proxy のアンインストールに失敗しました   |
| 9 | Wakeup Proxy ランタイムはサポートされていません   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

状態 ID はありません。

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

状態 ID はありません。

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

状態 ID はありません。

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
|0 | Windows プッシュ通知サービスのチャネル設定|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

状態 ID はありません。

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

状態 ID はありません。

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

状態 ID はありません。

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

状態 ID はありません。

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

状態 ID はありません。

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

状態 ID はありません。

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

状態 ID はありません。

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

状態 ID はありません。

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

状態 ID はありません。

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

状態 ID はありません。

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

状態 ID はありません。

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

状態 ID はありません。

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |チャレンジを発行済み         |
| 2 |チャレンジの発行に失敗        |
| 3 |要求の作成に失敗        |
| 4 |要求の送信に失敗        |
| 5 |チャレンジの検証に成功       |
| 6 |チャレンジの検証に失敗       |
| 7 |発行に失敗         |
| 8 |発行を保留中         |
| 9 |発行済み          |
| 10 |応答の処理に失敗       |
| 11 |応答を保留中         |
| 12 |登録に成功         |
| 13 |登録は不要         |
| 14 |取り消し済み          |
| 15 |コレクションから削除済み        |
| 16 |更新が検証済み         |
| 17 |インストールに失敗        |
| 18 |インストール済み         |
| 19 |削除に失敗         |
| 20 |削除済み         |
| 21 |更新が要求済み        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |チャレンジを発行済み         |
| 2 |チャレンジの発行に失敗        |
| 3 |要求の作成に失敗        |
| 4 |要求の送信に失敗        |
| 5 |チャレンジの検証に成功       |
| 6 |チャレンジの検証に失敗       |
| 7 |発行に失敗         |
| 8 |発行を保留中         |
| 9 |発行済み          |
| 10 |応答の処理に失敗       |
| 11 |応答を保留中         |
| 12 |登録に成功         |
| 13 |登録は不要         |
| 14 |取り消し済み          |
| 15 |コレクションから削除済み        |
| 16 |更新が検証済み         |
| 17 |インストールに失敗        |
| 18 |インストール済み         |
| 19 |削除に失敗         |
| 20 |削除済み         |
| 21 |更新が要求済み        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 | 状態 PIN セットアップに成功       |
| 2 | 状態 PIN セットアップに失敗       |
| 3 | 状態 PIN セットアップはサポートされていません      |
| 4 | 状態 PIN セットアップの処理中      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

状態 ID はありません。

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

状態 ID はありません。

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

状態 ID はありません。

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

状態 ID はありません。

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

状態 ID はありません。

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

状態 ID はありません。

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |チャレンジを発行済み    |
| 2 |チャレンジの発行に失敗   |
| 3 |要求の作成に失敗   |
| 4 |要求の送信に失敗   |
| 5 |チャレンジの検証に成功  |
| 6 |チャレンジの検証に失敗  |
| 7 |発行に失敗    |
| 8 |発行を保留中    |
| 9 |発行済み     |
| 10 |応答の処理に失敗  |
| 11 |応答を保留中    |
| 12 |登録に成功    |
| 13 |登録は不要    |
| 14 |取り消し済み     |
| 15 |コレクションから削除済み   |
| 16 |更新が検証済み    |
| 17 |インストールに失敗   |
| 18 |インストール済み    |
| 19 |削除に失敗    |
| 20 |削除済み    |
| 21 |更新が要求済み   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
|| 1 | コンプライアンスに成功    |
| 2 | mt でのコンプライアンスに失敗   |
| 3 | クライアントでのコンプライアンスに失敗   |
| 4 | Intune でのコンプライアンスに失敗   |
| 5 | AAD でのコンプライアンスに失敗   |
| 6 | コンプライアンスによる Intune の共同管理   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |ピア キャッシュ ソースを追加済み       |
| 2 |ピア キャッシュ ソースを削除済み      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |ピア キャッシュ ソースを非アクティブ化済み       |
| 2 |ピア キャッシュ ソースがアクティブ       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |集計データ アップロードのダウンロード       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |ピア ソース拒否データのアップロード     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

状態 ID はありません。

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

状態 ID はありません。

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

状態 ID はありません。

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

状態 ID はありません。

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     状態メッセージの ID     |  状態メッセージの説明 |
|:-------------|:------|
| 1 |正常性構成証明はサポートされています      |
| 2 |正常性構成証明はサポートされていません      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

状態 ID はありません。

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

状態 ID はありません。

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

状態 ID はありません。

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

状態 ID はありません。

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

状態 ID はありません。

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

状態 ID はありません。

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

状態 ID はありません。

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

状態 ID はありません。

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

状態 ID はありません。

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

状態 ID はありません。

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

状態 ID はありません。

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

状態 ID はありません。

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

状態 ID はありません。

## <a name="next-steps"></a>次のステップ

- [Configuration Manager の状態メッセージの説明](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Configuration Manager のソフトウェア更新管理に関するホワイトペーパー](https://www.microsoft.com/download/details.aspx?id=44578)
