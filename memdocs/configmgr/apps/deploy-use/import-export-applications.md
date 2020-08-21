---
title: アプリケーションのインポートとエクスポート
titleSuffix: Configuration Manager
description: Configuration Manager でアプリケーションをインポートおよびエクスポートし、個別の階層間で共有する方法について説明します。
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3db127deb353f30566a1f03cbc6ac0eef666cb37
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695258"
---
# <a name="import-and-export-applications"></a>アプリケーションのインポートとエクスポート

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager を使用して、2 つの階層間でアプリケーションをインポートおよびエクスポートします。 たとえば、アプリケーションをテスト環境から運用環境にコピーします。

## <a name="export"></a>エクスポート

1. Configuration Manager コンソールで、 **[アプリケーション]** ノードを選択します。 リボンの [作成] グループで **[アプリケーションのエクスポート]** を選択します。
1. **[全般]** 画面で、エクスポート先の新しい ZIP ファイルのパスを入力します。 必要に応じて、"*依存関係、置き換え関係、条件、および仮想環境*" のほか、"*選択したアプリケーションと依存関係のコンテンツ*" をエクスポートするかどうかを指定します。  必要に応じて、管理者のコメントを入力し、 **[次へ]** を選択します。
1. アプリケーションと依存関係が **[関連オブジェクト]** ページに一覧表示されていることを確認して、 **[次へ]** を選択します。
1. [概要] ページで、 **[次へ]** を選択します。
1. プロセスが完了すると、ZIP ファイルが作成され、ウィザードを閉じることができます。

> [!IMPORTANT]
> このアプリケーションを別の環境にコピーする場合、ZIP ファイルとそれに付属するフォルダーの両方を取得します。 ZIP ファイルは、作成したフォルダーと同じディレクトリに存在する必要があります。

## <a name="import"></a>インポート

> [!NOTE]
> アプリケーションは、UNC パスからのみインポートでき、ローカル ディスクから直接インポートすることはできません。

1. Configuration Manager コンソールで、 **[アプリケーション]** ノードを選択します。 リボンの [作成] グループで、 **[アプリケーションのインポート]** を選択します。
1. インポートする ZIP ファイルを選択し、 **[次へ]** を選択します。
1. [ファイル コンテンツ] ウィンドウに、アプリケーションをインポートしたときに何が行われるかが示されます。 **[次へ]** を選択します。
1. 概要画面を確認し、 **[次へ]** を選択します。
1. ウィザードを閉じます。 サイトで、アプリケーションを使用できるようになりました。

## <a name="see-also"></a>関連項目
 
PowerShell を使用してアプリケーションのインポートとエクスポートを自動化します。

* [Import-CMApplication](/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](/powershell/module/configurationmanager/export-cmapplication)