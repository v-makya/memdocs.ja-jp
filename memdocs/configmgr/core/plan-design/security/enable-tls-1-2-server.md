---
title: サイト サーバーとリモート サイト システムでトランスポート層セキュリティ (TLS) 1.2 を有効にする
titleSuffix: Configuration Manager
description: Configuration Manager サイト サーバーで TLS 1.2 を有効にする方法に関する情報。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704100"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>サイト サーバーとリモート サイト システムで TLS 1.2 を有効にする方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager 環境で TLS 1.2 を有効にするときは、最初に[クライアントで TLS 1.2 を有効にします](enable-tls-1-2-client.md)。 次に、サイト サーバーとリモート サイト システムで TLS 1.2 を有効にします。 最後に、必要に応じてサーバー側で古いプロトコルを無効にする前に、クライアントとサイト システムの間の通信をテストします。 サイト サーバーとリモート サイト システムで TLS 1.2 を有効にするには、次の作業を行う必要があります。

- オペレーティング システム レベルで SChannel のプロトコルとして TLS 1.2 を確実に有効にする
- TLS 1.2 をサポートするように .NET Framework を更新して構成する
- SQL Server とクライアント コンポーネントを更新する
- Windows Server Update Services (WSUS) を更新する

Configuration Manager の特定の機能とシナリオに対する依存関係について詳しくは、[TLS 1.2 の有効化](enable-tls-1-2.md)に関する記事をご覧ください。 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> オペレーティング システム レベルで SChannel のプロトコルとして TLS 1.2 を確実に有効にする

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> TLS 1.2 をサポートするように .NET Framework を更新して構成する

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a> SQL Server とクライアント コンポーネントを更新する

Microsoft SQL Server 2016 以降では、TLS 1.1 および TLS 1.2 がサポートされています。 以前のバージョンと依存ライブラリでは、更新プログラムが必要な可能性があります。 詳細については、「[KB 3135244:Microsoft SQL Server 用の TLS 1.2 のサポート](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)」を参照してください。

セカンダリ サイト サーバーでは、最低でも SQL Server 2016 Express Service Pack 2 (13.2.50.26) 以上を使用する必要があります。

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a> SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) には、SQL Server クライアント コンポーネントの要件も記載されています。

SQL Server Native Client も、最低でも SQL 2012 SP4 (11.*.7001.0) 以上のバージョンに必ず更新してください。 バージョン 1810 以降、この要件は[前提条件の確認 (警告)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client) となります。

Configuration Manager では、次のサイト システムの役割で SQL Server Native Client を使用します。

- サイト データベース サーバー
- サイト サーバー: 中央管理サイト、プライマリ サイト、またはセカンダリ サイト
- 管理ポイント
- デバイス管理ポイント
- 状態移行ポイント
- SMS プロバイダー
- ソフトウェアの更新ポイント
- マルチキャスト対応の配布ポイント
- 資産インテリジェンスの更新サービス ポイント
- レポート サービス ポイント
- アプリケーション カタログ Web サービス
- 登録ポイント
- Endpoint Protection ポイント
- [サービス接続ポイント]
- 証明書登録ポイント
- データ ウェアハウス サービス ポイント


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a> Windows Server Update Services (WSUS) を更新する

以前のバージョンの WSUS で TLS 1.2 をサポートするには、WSUS サーバーに次の更新プログラムをインストールします。

- Windows Server 2012 が稼働している WSUS サーバーの場合は、[更新プログラム 4022721](https://support.microsoft.com/help/4022721) 以降のロールアップ更新プログラムをインストールします。
- Windows Server 2012 R2 が稼働している WSUS サーバーの場合は、[更新プログラム 4022720](https://support.microsoft.com/help/4022720) 以降のロールアップ更新プログラムをインストールします。

Windows Server 2016 以降の WSUS では、TLS 1.2 が既定でサポートされています。  TLS 1.2 の更新プログラムは、Windows Server 2012 サーバーと Windows Server 2012 R2 WSUS サーバーでのみ必要です。

## <a name="next-steps"></a>次のステップ

- [TLS 1.2 を有効にしたときの一般的な問題](enable-tls-1-2-troubleshoot.md)
