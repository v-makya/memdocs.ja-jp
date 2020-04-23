---
title: Client Spy
titleSuffix: Configuration Manager
description: Client Spy を使用すると、ソフトウェアの配布、インベントリおよび Configuration Manager クライアントのソフトウェア使用状況の測定のトラブルシューティングを行うことができます。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707910"
---
# <a name="client-spy"></a>Client Spy

*適用対象:Configuration Manager (Current Branch)*

Client Spy は、[Configuration Manager ツール](tools.md)の 1 つです。 これは、ソフトウェアの配布、インベントリおよび Configuration Manager クライアントのソフトウェア使用状況の測定のトラブルシューティング用のツールです。 

ツールが受信する情報の多くは、ソフトウェアの展開に関するものです。
- 現在展開されているすべてのソフトウェア 
- ソフトウェアの配布履歴
- クライアントのキャッシュ構成
- キャッシュされた項目
- 保留中の展開する必要のあるもの
- 利用可能な展開  

次のインベントリ情報も表示されます。
- インベントリの最新のサイクル日
- 最終レポート日
- ソフトウェア インベントリのメジャーおよびマイナー バージョン
- ファイル コレクション
- ハードウェア インベントリ
- IDMIF コレクション
- データ探索レコード (DDR) 

ソフトウェア使用状況測定規則も表示されます。 

> [!Note]   
> このツールでは、パフォーマンス向上のために、各タブを選択したときのみ情報を収集します。 また、 **[更新]** をクリックした場合も、タブに現在表示されている情報のみを更新します。



## <a name="usage"></a>使用方法


### <a name="tools-menu"></a>[ツール] メニュー

**[ツール]** メニューでは、次のアクションを利用できます。  

#### <a name="connect"></a>接続
別のコンピューターから情報を取得します。  

- 既定では、このツールは現在のコンピューターの情報を表示します。 

- リモート コンピューター名、アカウントのユーザー名とパスワードを使用して接続します。 このツールは、リモート コンピューターの IPC$ 共有に接続します。 ツールが存在する場合、または別のコンピューターに接続する場合、接続は削除されます。  

- この情報を取得するには、十分な資格情報を持つアカウントが必要です。  

- ユーザー名とパスワードを指定しない場合、Client Spy は現在サインインしているユーザーのセキュリティ コンテキストを使用して、接続を試行します。  

- リモート コンピューターに接続する場合、表示されているすべてのタブには、リモート コンピューターからの情報が表示されます。

#### <a name="software-distribution"></a>ソフトウェアの配布
[[ソフトウェアの配布]](#software-distribution) タブを表示し、他のタブは非表示になります。 既定で、Client Spy は [ソフトウェアの配布] タブを表示します。

#### <a name="inventory"></a>インベントリ
[インベントリ] タブを表示し、その他のタブを非表示にします。

#### <a name="software-metering"></a>ソフトウェア使用状況測定
[ソフトウェア使用状況の測定] タブを表示し、他のタブを非表示にします。

#### <a name="save-current-tab-to-file"></a>Save current tab to file (現在のタブをファイルに保存する)
現在表示されているタブの情報を、指定のテキスト ファイルに保存します。 

#### <a name="save-all-tabs-to-file"></a>Save all tabs to file (すべてのタブをファイルに保存する)
すべてのタブの情報を、指定のテキスト ファイルに保存します。 アカウントで表示できる情報のみが保存されます。



## <a name="software-distribution-tab"></a>[ソフトウェアの配布] タブ

次の 4 つのタブで、設定を構成します。
- [Software Distribution Execution Requests (ソフトウェアの配布の実行要求)](#bkmk_exec-requests)
- [Software Distribution History (ソフトウェアの配布履歴)](#bkmk_history)
- [Software Distribution Cache Information (ソフトウェアの配布のキャッシュ情報)](#bkmk_cache-info)
- [Software Distribution Pending Executions (ソフトウェアの配布の実行の保留)](#bkmk_pending-exec)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a> Software Distribution Execution Requests (ソフトウェアの配布の実行要求)

このタブには、デバイスとユーザーを対象とした展開を含む既存のすべての展開が表示されます。

[Software Distribution Execution Requests]\(ソフトウェアの配布の実行要求\) タブの各ツリー項目には、次の 4 つの属性が含まれています。
- 公開通知 ID。 利用可能な展開の場合、この値は空白である場合があります。 
- パッケージ ID 
- プログラム名 
- ユーザー。 これは、対象とするユーザーの SID または要求を開始したユーザーの SID である場合があります。 いずれもシステム要求である場合、表示されるユーザーは System です。 

実行される要求ごとに、サブツリー構造に次の情報も表示されます。
- プログラム名 
- パッケージ ID 
- パッケージ名 
- 要求の作成時刻 
- 状態 
- 状態が実行中であるときの実行の状態 
- 実行コンテキスト (ユーザーまたは管理者) 
- 履歴の状態 (成功、失敗、または NotRun) 
- LastRunTime (プログラムを実行したことがない場合は Never) 
- 状態が WaitingRetry のときの RetryCount 
- ContentAccess (状態が WaitingRetry のときの Retry Count) 
- 状態が WaitingRetry のときの FailureCode 
- 状態が WaitingRetry のときの FailureReason 

要求にコンテンツが必要な場合、状態は WaitingContent です。 [Software Distribution Cache Information]\(ソフトウェアの配布のキャッシュ情報\) タブには、このダウンロード情報の詳細が表示されます。

実行要求がダウンロード要求である場合、ダウンロードされたバイト数も表示されます。

> [!Note]   
> 実行要求のさまざまな状態には別のアイコンが使用されます。


### <a name="software-distribution-history"></a><a name="bkmk_history"></a> Software Distribution History (ソフトウェアの配布履歴)

このタブには以前に実行しているすべてのプログラムの情報が含まれます。 この情報はレジストリに保存されます。

このツリーのメイン ブランチは、System を含む異なるユーザー履歴です。 これは、各ユーザー用にどのプログラムが実行されたか、パッケージの一覧を含むサブツリーを表示します。 

各パッケージ サブツリーのパッケージ ID とパッケージ名には、実行されたプログラムの一覧が表示されます。 それぞれに対して以下の次の属性が表示されます。 
- プログラム名
- 実行の状態
- 前回の実行時間
- エラー コード
- エラーの理由  

プログラムが正常に実行されると、エラー コードとエラーの理由は空白になります。


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a> Software Distribution Cache Information (ソフトウェアの配布のキャッシュ情報)

#### <a name="cache-config"></a>Cache Config (キャッシュの構成)
Configuration Manager クライアント キャッシュの情報が含まれます。 この情報には、キャッシュの場所、キャッシュのサイズ、それが現在使用されているかが含まれます。 

#### <a name="cached-items"></a>Cached Items (キャッシュされた項目)
現在キャッシュされているすべての項目のサブツリーを含みます。 各ツリー項目には、各項目に対する次の情報が含まれています。 
- キャッシュ内の項目の場所 (フォルダー)
- 現在の状態
- パッケージ ID
- パッケージ名
- パッケージ バージョン
- パッケージ サイズ
- 現在の参照カウント
- 最終参照日時刻 (UTC)  

#### <a name="downloading-items"></a>Downloading Items (ダウンロードしている項目)
これらは、クライアントが現在ダウンロードしている項目です。 それぞれには、キャッシュ項目によって表示されたのと同じ情報と、ダウンロードされたキロバイト数が表示されます。 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a> Software Distribution Pending Executions (ソフトウェアの配布の実行の保留)

このタブには、過去および今後必要な展開と利用可能な展開の一覧の詳細情報が含まれています。

各ツリー ブランチは、各ユーザー アカウント用のシステムを含む利用可能な展開です。

サブ ツリーには、各ユーザーに次の 3 つの項目が含まれます。  

#### <a name="mandatory-advertisements-with-future-executions"></a>Mandatory Advertisements With Future Executions (今後実行する必須の公開通知)
これらは、まだ実行されていないプログラムがある必須の公開通知です。 これは、繰り返すことも、1 回限りでも、複数のスケジュール公開通知でもかまいません。 それぞれが公開通知 ID、次回の実行時間、公開通知の実行スケジュールを表示します。 

#### <a name="optional-advertisements"></a>Optional Advertisements (オプションの公開通知)
公開されているすべての公開通知一覧が表示されます。 それぞれの公開通知 ID、プログラム名、パッケージ名などの詳細も表示されます。 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Past Mandatory Advertisements With No Future Scheduled Executions (今後実行がスケジュールされていない過去の必須の公開通知)
実行するプログラムがスケジューリングされていないクライアント上にある公開通知の一覧です。 公開通知 ID、パッケージ名、プログラム名が表示されます。 省略可能なすべての公開通知に対し、サブツリー項目が表示されます。

> [!Note]  
> パッケージ名の情報は、参照しているコンピューター上で関連付けられている公開されているポリシーがあるパッケージのみ用に用意されています。 利用可能なポリシーが関連付けられていないパッケージには、"Package Name No Longer Available"(パッケージ名は利用できません) というメッセージが表示されます。  



## <a name="inventory-tab"></a>インベントリ タブ

インベントリ情報を含むタブは 1 つしかありません。 メインのツリーは、次の 5 つの項目を含みます。  

- **ソフトウェア インベントリ**:最後のサイクルが開始された日付、最終レポートの日付、最終レポートのマイナーおよびメジャー バージョンが含まれます。  

- **ファイル コレクション**:最後のサイクルが開始された日付、最終レポートの日付、最終レポートのマイナーおよびメジャー バージョンが含まれます。  

- **ハードウェア インベントリ**:最後のサイクルが開始された日付、最終レポートの日付、最終レポートのマイナーおよびメジャー バージョンが含まれます。  

- **IDMIF コレクション**:最後のサイクルが開始された日付、最終レポートの日付、最終レポートのマイナーおよびメジャー バージョンが含まれます。  

- **DDR**: 最後のサイクルが開始された日付、最終レポートの日付、最終レポートのマイナーおよびメジャー バージョンが含まれます。 サブツリーには DDR 情報も含まれています。



## <a name="software-metering-tab"></a>[ソフトウェア使用状況測定] タブ

このタブには、情報がサブツリーとして表示されており、すべてのソフトウェア使用状況測定規則が含まれています。 各規則は、ファイル名および規則 ID によって識別されるノードとして表示されます。 ツリーの各ノードを拡張し、次の情報を参照します。
- エクスプローラー ファイル名 
- 元のファイル名
- ルール ID
- ファイルのバージョン
- 言語


