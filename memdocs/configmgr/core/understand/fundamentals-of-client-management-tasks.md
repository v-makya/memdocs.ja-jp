---
title: コンテンツ管理の基礎
titleSuffix: Configuration Manager
description: Configuration Manager クライアントを管理するために実行するタスクについて学習します。
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d58a0da25d98089a54694a21d47d1ef8583acb81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707100"
---
# <a name="fundamentals-of-client-management-tasks-for-configuration-manager"></a>Configuration Manager のクライアント管理タスクの基礎

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager クライアントをインストールした後、クライアントを管理するために実行するタスクがいくつかあります。  一部のタスクは、Configuration Manager コンソールから実行されます。 それ以外のタスクは、Configuration Manager クライアント アプリケーションから実行されます。 Configuration Manager クライアント アプリケーションは、Configuration Manager クライアント ソフトウェアと共にインストールされます。

## <a name="configuration-manager-console-tasks"></a>Configuration Manager コンソールのタスク
 Configuration Manager コンソールでは、次のようなさまざまなクライアント管理タスクを実行できます。  

-   アプリケーション、ソフトウェア更新プログラム、メンテナンス スクリプト、およびオペレーティング システムの展開。 特定の日時にインストールするように構成したり、ユーザーが要求したときにソフトウェアをインストールできるようにしたり、アプリケーションをアンインストールするように構成したりする。  

-   マルウェアおよびセキュリティの脅威からコンピューターを保護し、問題が検出されたときに通知を出力する。  

-   コンプライアンスに準拠しているかどうかを監視して修復するためのクライアントの構成設定を定義する。  

-   ハードウェアおよびソフトウェアのインベントリ情報の収集。これには、Microsoft のライセンス情報の監視および調整が含まれます。  

-   リモート コントロールを使用してコンピューターをトラブルシューティングします。  

-   コンピューターの電力消費を管理および監視するための電源管理設定の実装。  

Configuration Manager コンソールでは、ほぼリアルタイムで前のタスクを監視します。 各タスクの通知と状態情報は、Configuration Manager コンソールで使用できます。 データおよび過去の傾向を取得するには、SQL Server Reporting Services の統合レポート機能を使用します。 クライアントは、クライアントのステータスとしての詳細をサイトに送信します。  クライアント ステータス情報では、クライアントとクライアント アクティビティの正常性に関するデータが提供されます。これらのデータはコンソールで、または Configuration Manager の組み込みレポートを使用して表示できます。 このデータを使用すると、応答していないコンピューターを識別できます。また、問題が自動的に修復されることもあります。  

 クライアントの管理タスクに関する詳細については、[クライアントを管理する方法](../../core/clients/manage/manage-clients.md)に関するページおよび [Linux および UNIX サーバーのクライアントを管理する方法](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)に関するページを参照してください。 レポートの使用の詳細については、   
            [レポートの概要](../../core/servers/manage/introduction-to-reporting.md)に関するページを参照してください。  

## <a name="configuration-manager-client-application"></a>Configuration Manager クライアント アプリケーション  
 Configuration Manager クライアント ソフトウェアをインストールすると、Configuration Manager クライアント アプリケーションもインストールされます。 ソフトウェア センターとは異なり、Configuration Manager クライアント アプリケーションはエンドユーザーではなく、ヘルプ デスク用に設計されています。 一部の構成オプションにはローカルの管理アクセス許可が必要であり、ほとんどのオプションには Configuration Manager クライアント アプリケーションの機能についての技術的な知識が必要です。 このアプリケーションを使用すると、クライアントで次のタスクを実行できます。  

-   クライアントに関するプロパティ (ビルド番号、割り当てられているサイト、通信する管理ポイント、およびクライアントが公開キー基盤 (PKI) 証明書と自己署名入り証明書のどちらを使用するかなど) を表示する。  

-   クライアントの初回インストール後に、クライアントでクライアント ポリシーが正常にダウンロードされたかどうかを確認する。 また、Configuration Manager コンソールで構成されているクライアント設定に従って、予期したとおりにクライアント設定が有効または無効になっているかどうかを確認します。  

-   クライアント アクションを開始する。 たとえば、Configuration Manager コンソールで最近構成の変更が行われ、次のスケジュール時間まで待機しない場合に、クライアント ポリシーをダウンロードします。  

-   手動で Configuration Manager サイトにクライアントを割り当てる、またはサイトの検索を試みる。 その後、DNS (ドメイン ネーム システム) に発行する、管理ポイントの DNS サフィックスを指定します。  

-   ファイルを一時的に格納するクライアント キャッシュを構成する。 ソフトウェアをインストールするためにさらにディスク容量が必要な場合は、キャッシュ内のファイルを削除します。  

-   インターネット ベースのクライアント管理のための設定の構成  

-   クライアントに展開されている構成基準の表示、コンプライアンスの評価の開始、およびコンプライアンス レポートの表示。  
