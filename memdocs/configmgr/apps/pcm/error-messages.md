---
title: エラー メッセージ
titleSuffix: Configuration Manager
description: Package Conversion Manager からのエラー メッセージについて説明します。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688970"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Package Conversion Manager のエラー メッセージのテクニカル リファレンス

*適用対象:Configuration Manager (Current Branch)*

<!--1357861-->

この記事では、Package Conversion Manager に表示されるエラー メッセージについて説明します。 また、考えられるエラーの原因と、エラーを修正するための方法についても取り上げています。 Package Conversion Manager では、**PCMTrace.log** にエラー メッセージを記録します。 詳細レベルを制御する方法など、詳細については「[Log files](troubleshoot-pcm.md#log-files)」(ログ ファイル) を参照してください。


#### <a name="application-creation-failed-with-the-following-exception"></a>アプリケーションの作成は次の例外で失敗しました

特定された例外が、Configuration Manager へのアプリケーション オブジェクトの送信中に発生しました。

Configuration Manager のアクセス許可を確認して、接続を確認してから、再試行します。 これらの操作で問題が解決しない場合は、**PCMtrace.log** ファイル (詳細レベル 4) と **SMSProv.log** を確認します。


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>変換エラー – パッケージ移行ステータスに適用します

パッケージの変換中に一般的な例外が発生しました。 **PCMtrace.log** ファイル (詳細レベル 4) を確認します。

ネットワーク共有 (パッケージ データ ソース) のユーザーのアクセス許可を確認してから、接続を確認して再試行します。 これらの操作で問題が解決しない場合は、**PCMtrace.log** ファイル (詳細レベル 4) を確認します。


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>変換されたパッケージと結果アプリケーションがワークフロー出力で見つかりません
アプリケーション (変換されたパッケージまたはプログラム) が削除されました。

依存パッケージまたはプログラムを変更して、依存パッケージまたはプログラムが存在することを確認します。


#### <a name="objects-were-not-created-successfully"></a>オブジェクトは正常に作成されませんでした
複数の原因が考えられます。

Configuration Manager のアクセス許可を確認して、接続を確認してから、再試行します。 これらの操作で問題が解決しない場合は、**PCMtrace.log** ファイル (詳細レベル 4) と **SMSProv.log** ファイルを確認します。


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>ウィザードを閉じて、選択したパッケージの問題を解決してください。 詳細については、PCMTrace.Log を参照してください
複数の原因が考えられます。

Configuration Manager のアクセス許可を確認して、接続を確認してから、再試行します。 これらの操作で問題が解決しない場合は、**PCMtrace.log** ファイル (詳細レベル 4) と **SMSProv.log** ファイルを確認します。


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>検出方法が不足している展開の種類があります。 すべての展開の種類には検出方法が必要です
プログラムに検出方法がありません。

**[修正と変換]** プロセス中に 1 つ以上の検出方法を追加します。


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>パッケージの変換準備中にエラーが発生しました
複数の原因が考えられます。

Configuration Manager のアクセス許可を確認して、接続を確認してから、再試行します。 これらの操作で問題が解決しない場合は、**PCMtrace.log** ファイル (詳細レベル 4) と **SMSProv.log** ファイルを確認します。


