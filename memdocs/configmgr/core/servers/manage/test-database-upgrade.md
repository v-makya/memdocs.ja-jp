---
title: データベース アップグレードをテストする
titleSuffix: Configuration Manager
description: Configuration Manager 用の更新プログラムをインストールする際に、サイト データベースのアップグレードをテストします。
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56c1422f4157b255f4f7a8624e36d10e01f28fc0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703290"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>更新プログラムをインストールする際にデータベース アップグレードをテストする

*適用対象:Configuration Manager (Current Branch)*

このトピックの情報は、現在のブランチの Configuration Manager 用のコンソール内の更新プログラムをインストールする前にデータベース アップグレードのテストを実行するのに役立ちます。 ただし、データベースが未確認である場合や、Configuration Manager で明示的にサポートされていないカスタマイズで変更されている場合を除き、アップグレードのテストは必須の手順あるいは推奨される手順ではなくなりました。

## <a name="do-i-need-to-run-a-test-upgrade"></a>アップグレードのテストを実行する必要がありますか?
このアップグレードのテストは、Configuration Manager Current Branch で導入される変更に伴い、非推奨となります。 これらの変更により、プロセスが簡略化され、実稼働環境を新しいバージョンに短時間で更新できるようになります。 この再設計の目的は、常にお客様のリスクを軽減し、新しい更新プログラムをそれぞれインストールする際の運用のオーバーヘッドを減らせるようにすることです。

サイトの回復を実行することなく、失敗した更新プログラムを自動的にロールバックするロジックを含む、更新プログラムのインストール方法が変更されています。 これらの変更により、コンソールを使用して、更新プログラムのインストールを管理できるようになります。また、これらの変更には、[失敗した更新プログラムのインストールを再試行する](install-in-console-updates.md#bkmk_retry)オプションが含まれます。

> [!TIP]
> System Center 2012 Configuration Manager などの古い製品から Configuration Manager Current Branch にアップグレードする場合、[データベース アップグレードのテストは引き続き推奨される手順](../deploy/install/upgrade-to-configuration-manager.md#bkmk_test)です。

コンソール内の更新プログラムをインストールするときでもサイト データベースのアップグレードをテストする予定の場合、以下の情報は[コンソール内更新プログラムのインストールに関するガイダンス](install-in-console-updates.md#bkmk_install)を補足するものとなります。

## <a name="prepare-to-run-a-test-database-upgrade"></a>データベース アップグレードのテストを実行するための準備  
1702 の更新など、階層内に新しい更新プログラムをインストールする前に、サイト データベースのアップグレードをテストできます。

アップグレードのテストを実行するには、更新対象バージョンの Configuration Manager を実行しているサイトの [CD.Latest フォルダー](the-cd.latest-folder.md)にあるソース ファイルの Configuration Manager セットアップを使用します。 この要件は、1702 に更新するためにデータベースの更新をテストすることを意味します。
-   CD.Latest フォルダーを取得できる、バージョン 1702 を実行する 1 つ以上のサイトが必要です。
-   必要なバージョンを実行するサイトがない場合は、ラボ環境でのサイトのインストールを検討し、そのサイトを新しいバージョンに更新します。 これにより、正しいバージョンのソース ファイルを含む CD.Latest フォルダーを作成することができます。

アップグレードのテストは、SQL Server の別のインスタンスに復元したサイト データベースのバックアップに対して実行されます。  データベースのコピーを復元したアップグレードをテストするには、**testdbupgrade** コマンド ライン スイッチを使用して **CD.Latest** フォルダーからセットアップを実行します。 アップグレード テストの完了後、アップグレードされたデータベースは破棄されます。 これを Configuration Manager サイトで使用することはできません。

更新プログラムのインストールが失敗した場合に、サイトを回復する必要はありません。 代わりに、コンソール内から更新プログラムのインストールを再試行できます。

##  <a name="run-the-test-upgrade"></a>アップグレードのテストを実行する    
1. Configuration Manager セットアップと、更新する予定のバージョンを実行するサイトの **CD.Latest** フォルダーにあるソース ファイルを使用します。  

2. データベース アップグレードのテストを実行するために使用する SQL Server インスタンスの場所に **CD.Latest** フォルダーをコピーします。

3. アップグレードをテストするサイト データベースのバックアップを作成します。 次に、Configuration Manager サイトをホストしていない SQL Server のインスタンスにそのデータベースのコピーを復元します。 SQL Server インスタンスは、サイト データベースと同じエディションの SQL Server を使用する必要があります。  

4. データベースのコピーを復元したら、更新するバージョンのソース ファイルを含む CD.Latest フォルダーから**セットアップ**を実行します。 セットアップを実行する際は、 **/TESTDBUPGRADE** コマンド ライン オプションを使います。 データベースのコピーをホストする SQL Server インスタンスが既定のインスタンスでない場合は、コマンドライン引数を指定して、サイト データベースのコピーをホストするインスタンスを識別します。   

   たとえば、データベース名が *SMS_ABC* のサイト データベースがあるとします。 このサイト データベースのコピーを、インスタンス名が *DBTest* の SQL Server のサポートされているインスタンスに復元します。 サイト データベースのこのコピーのアップグレードをテストするには、次のコマンド ラインを使用します。**Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**。  

   Setup.exe は、Configuration Manager のソース メディアの **SMSSETUP\BIN\X64** にあります。  

5. アップグレード テストを実行する SQL Server インスタンスで、システム ドライブのルート内の *ConfigMgrSetup.log* を確認し、進行状況と成功状態を監視します。  

    アップグレード テストに失敗した場合は、サイト データベースのアップグレード失敗に関する問題をすべて修正します。 次に、サイト データベースの新しいバックアップを作成し、データベースの新しいコピーのアップグレードをテストします。  



## <a name="next-steps"></a>次のステップ
データベースの更新テストが正常に完了したら、更新されたデータベースを破棄します。 これを Configuration Manager サイトで使用することはできません。 その後、アクティブなサイトに戻り、[更新プログラムのインストール](install-in-console-updates.md)を開始できます。
