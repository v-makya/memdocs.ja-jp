---
title: バージョン 2012 からの変更
titleSuffix: Configuration Manager
description: System Center 2012 Configuration Manager と比較した Configuration Manger の新機能と変更をご確認いただけます。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704440"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>System Center 2012 Configuration Manager からの変更点

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の Current Branch には、System Center 2012 Configuration Manager からの重要な変更点があります。 この記事では、Configuration Manager Current Branch の元の基準バージョン 1511 における重要な変更点と新機能について紹介します。 Configuration Manager の最新の更新プログラムで導入された変更の詳細については、「[Configuration Manager の増分バージョンの新機能](whats-new-incremental-versions.md)」を参照してください。

> [!NOTE]
> バージョン 1910 以降、Configuration Manager は Microsoft Endpoint Manager の一部になりました。 詳細については、「[Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem)」を参照してください。

2015 年 12 月リリースの Configuration Manager (バージョン 1511) は、Microsoft から提供される現在の Configuration Manager 製品の最初のリリースでした。 これは一般に Configuration Manager Current Branch と呼ばれます。 *Current Branch* は、これが製品の増分更新をサポートするバージョンであることを示します。 さらに、Configuration Manager のこのリリースと以前のリリースを区別する手段も提供します。  

Configuration Manager Current Branch:  

- Configuration Manager 2007 または System Center 2012 Configuration Manager などの過去のバージョンとは異なり、製品名に年や製品識別子を使用していません。  

- 製品組み込みの増分更新をサポートしているため、更新プログラム バージョンとも呼ばれます。 最初のリリースはバージョン 1511 でした。 その後のバージョンは、バージョン 1910 のように、コンソール内の更新プログラムとして年に数回リリースされています。  

- 基準バージョンを使用してインストールします。 1511 は元の基準バージョンでしたが、新しい基準バージョンも、2002 のように、ときどきリリースされます。 基準バージョンを使用して、新しい Configuration Manager サイトと階層をインストールしたり、サポート対象バージョンの System Center 2012 Configuration Manager からアップグレードしたりすることができます。  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a> コンソール内の更新プログラム

Configuration Manager では、**更新とサービス**と呼ばれるコンソール内でのサービス提供方式が採られています。この方式により、推奨される更新プログラムを簡単に特定し、インストールすることができます。  

バージョンによっては、Configuration Manager コンソール内から既存のサイトに対する更新プログラムとしてしか使用できないものもあります。 これらの更新プログラムを使用して、新しい Configuration Manager サイトをインストールすることはできません。 たとえば、1910 更新プログラムは、Configuration Manager コンソール内からのみ使用可能です。 これはサポートされているバージョンの Configuration Manager を既に実行しているサイトを更新する場合に使用されます。

更新プログラム バージョンも、新しい "*基準*" バージョンとして定期的にリリースされます。 たとえば、更新プログラム 2002 も基準バージョンです。 新しいサイトまたは階層をインストールするには、基準バージョンを使用します。 1802 のような古い基準バージョンを使用しないでください。最新バージョンにアップグレードしてください。 常に最新の基準を使用してください。

詳細については、以下の記事を参照してください。

- [Configuration Manager の更新プログラム](../../servers/manage/updates.md)
- [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a> サービス接続ポイント  

Configuration Manager Current Branch には、新しいサイト システムの役割、**サービス接続ポイント**が含まれています。  

- 多くのクラウド対応機能の接続ポイント

- ご利用のサイトの更新プログラムをダウンロードする

- サイトに関する診断情報と使用状況データを Microsoft クラウドにアップロードする

このサイト システムの役割は、オンラインとオフラインの両方の操作モードをサポートしています。 詳細については、「[About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md)」 (サービスの接続ポイントについて) を参照してください。  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a> 診断結果と使用状況データ

Configuration Manager では、ご利用のサイトとインフラストラクチャに関する診断結果と使用状況データが収集されます。 この情報がコンパイルされ、サービス接続ポイントによって Microsoft クラウド サービスに送信されます。 Configuration Manager では、ご利用の環境に適用できる更新プログラムをダウンロードするためにこのデータが必要です。 サービス接続ポイントを設定するときに、収集するデータのレベルと、そのデータを自動 (オンライン) または手動 (オフライン) で送信するかどうかを指定できます。

詳細については、「[診断結果と使用状況データ](../diagnostics/diagnostics-and-usage-data.md)」を参照してください。  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a> 非推奨機能  

ネイティブな [Intel Active Management Technology (AMT) のサポート](#bkmk_AMT)などのいくつかの機能は、Configuration Manager コンソールから削除されます。 ネットワーク アクセス保護などの他の機能は、完全に削除されます。 さらに、Windows Vista、Windows Server 2008、SQL Server 2008 などの古い Microsoft 製品の一部はサポートされなくなりました。  

非推奨機能の一覧については、[削除された項目と非推奨の項目](deprecated/removed-and-deprecated.md)に関するページを参照してください。  

サポートされる製品、オペレーティング システム、および構成の詳細については、[サポートされる構成](../configs/supported-configurations.md)に関するページを参照してください。  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Intel Active Management Technology (AMT) のサポート  

Configuration Manager の Current Branch では、Configuration Manager コンソール内からの AMT ベースのコンピューターに対するネイティブ サポートが削除されています。 [Microsoft Configuration Manager 用 Intel SCS アドオン](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)を使用すれば、AMT ベースのコンピューターは引き続き完全に管理されます。 アドオンを使用することで、最新の機能にアクセスして AMT を管理できます。Configuration Manager にこれらの変更が組み込まれるまでに適用されていた制限は解除されます。  

Configuration Manager での統合 AMT の削除には、帯域外管理が含まれています。 帯域外管理ポイント サイト システムの役割は、使用できなくなりました。  

> [!Note]
> この変更は、System Center 2012 Configuration Manager での帯域外管理には影響しません。

## <a name="changes-in-functionality"></a>機能の変更

次のセクションでは、System Center 2012 R2 Configuration Manager と Configuration Manager Current Branch のバージョン 1511 機能領域における重要な変更点をいくつかまとめています。 機能の最新の変更点の詳細については、[増分バージョンの新機能](whats-new-incremental-versions.md)に関する記事をご覧ください。

### <a name="client-deployment"></a>クライアント展開  

Configuration Manager では、Configuration Manager クライアントの新しいバージョンをテストしてから、この新しいソフトウェアを使用してサイトの他の部分をアップグレードするようにするための新機能が導入されています。 新しいクライアントをパイロット運用するための実稼働前コレクションをセットアップすることができます。 実稼働前環境で新しいクライアント ソフトウェアが正常に動作することを確認した後、その新しいバージョンを使用してサイトの残りの部分を自動的にアップグレードするようにクライアントを昇格できます。  

クライアントをテストする方法の詳細については、[実稼働前コレクションのクライアント アップグレードをテストする方法](../../clients/manage/upgrade/test-client-upgrades.md)に関するページを参照してください。  

### <a name="os-deployment"></a>OS の展開  

OS の展開に関する次の変更に注意してください。

- タスク シーケンスの作成ウィザードでは、新しいタスク シーケンスの種類を入手できます。**オペレーティング システムをアップグレード パッケージからアップグレードする**。 これにより、コンピューターを Windows 7 または Windows 8.1 から Windows 10 にアップグレードするステップが作成されます。 詳細については、「[Windows を最新バージョンにアップグレードする](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)」をご覧ください。  

- オペレーティング システムを展開するときに、Windows PE ピア キャッシュを利用できるようになりました。 OS を展開するタスク シーケンスを実行しているコンピューターでは、配布ポイントからコンテンツをダウンロードするのではなく、Windows PE ピア キャッシュを使用してピア キャッシュ ソースからコンテンツを取得できます。 この動作により、ローカル配布ポイントが存在しないブランチ オフィス シナリオで WAN のトラフィックが最小限に抑えられます。 詳細については、「[WAN トラフィックを削減するための Windows PE ピア キャッシュの準備](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)」を参照してください。  

- 環境内でサービスとして今すぐ Windows の状態を表示できます。 サービス プランを作成して展開リングを形成し、新しいビルドがリリースされたときに Windows 10 Current Branch を最新の状態に確実に維持することもできます。 また、Windows 10 クライアントのビルドのサポートの終了が近づいたときに、アラートを表示することができます。 詳細については、「[サービスとしての Windows の管理](../../../osd/deploy-use/manage-windows-as-a-service.md)」を参照してください。  

### <a name="application-management"></a>アプリケーション管理  

アプリケーション管理に関する次の変更に注意してください。

- Configuration Manager では、Windows 10 以降を実行しているデバイス用のユニバーサル Windows プラットフォーム (UWP) アプリを展開できます。 詳細については、[Windows アプリケーションを作成する](../../../apps/get-started/creating-windows-applications.md)に関するページをご覧ください。  

- ソフトウェア センターは新しい現代的な外観へと一新されます。 これまではアプリケーション カタログにしか表示されなかったユーザーが利用できるアプリがソフトウェア センターの [アプリケーション] タブに表示されるようになりました。この動作により、これらの展開を見つけやすくなり、ユーザーが別々のアプリケーション カタログを参照する必要がなくなります。 さらに、Silverlight 対応のブラウザーが必要なくなります。 詳細については、「[Plan for and configure application management](../../../apps/plan-design/plan-for-and-configure-application-management.md)」(アプリケーション管理の計画と構成) を参照してください。  

- MDM アプリケーションを介した新しい Windows インストーラーの種類では、Windows インストーラー ベースのアプリを作成して、Windows 10 を実行する登録済み PC に展開できます。 詳細については、[Windows アプリケーションを作成する](../../../apps/get-started/creating-windows-applications.md)に関するページをご覧ください。  

- Configuration Manager 2012 では、Windows ストアのアプリへのリンクを指定する場合、リンクを直接指定するか、またはアプリがインストールされているリモート コンピューターを参照します。 Configuration Manager の Current Branch でも、引き続きリンクを直接入力できますが、参照コンピューターを参照するのではなく、Configuration Manager コンソールから直接アプリのストアを参照できるようになりました。  

### <a name="software-updates"></a>ソフトウェア更新プログラム  

ソフトウェア更新プログラムに関する次の変更に注意してください。

- Configuration Manager では、コンピューターのソフトウェア更新プログラムの管理方法の違いを検出できるようになりました。 具体的には、Windows Update for Business (WUfB) に接続されている Windows 10 コンピューターと、WSUS に接続されているコンピューターとを区別することができます。 **UseWUServer** は新たに導入された属性で、WUfB でコンピューターを管理するかどうかを指定します。 コレクションでこの設定を使用すると、ソフトウェアの更新管理からこれらのコンピューターを除外できます。 詳細については、「 [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)」をご覧ください。  

- Configuration Manager コンソールから WSUS クリーンアップ タスクをスケジュールし、実行できるようになりました。 **ソフトウェアの更新ポイント コンポーネント**のプロパティで、WSUS クリーンアップ タスクを実行することを選ぶと、次回、ソフトウェア更新プログラムを最新に保つときにこのタスクが実行されます。 期限切れのソフトウェアの更新プログラムは WSUS サーバー上で拒否状態に設定され、コンピューター上の Windows Update エージェントでこれらのソフトウェア更新プログラムをスキャンできなくなりました。 詳細については、「 [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md)」をご覧ください。  

### <a name="compliance-settings"></a>コンプライアンス設定  

コンプライアンス設定に関する次の変更に注意してください。

- Configuration Manager では、構成項目を作成するためのワークフローが改良されています。 これで、構成項目を作成し、サポートされているプラットフォームを選択するときに、そのプラットフォームに関連する設定のみが使用できるようになります。 [コンプライアンス設定を使ってみる](../../../compliance/get-started/get-started-with-compliance-settings.md)に関するページを参照してください。  

- **構成項目の作成**ウィザードでは、作成する構成項目の種類が選択しやすくなりました。 さらに、次のものに対して使用できる構成項目が追加および更新されています。  

    - Configuration Manager クライアントを使用して管理されている Windows 10 デバイス  

    - Configuration Manager クライアントを使用して管理されている Mac OS X デバイス  

    - Configuration Manager クライアントを使用して管理されている Windows デスクトップおよびサーバー コンピューター  

    - Configuration Manager クライアントを使用せずに管理されている Windows 8.1 および Windows 10 デバイス  

    詳細については、[構成項目の作成方法](../../../compliance/deploy-use/create-configuration-items.md)に関するページを参照してください。  

- Configuration Manager クライアントなしで管理されている、Mac OS X コンピューター上の設定を管理するためのサポート。

### <a name="on-premises-mobile-device-management"></a>オンプレミス モバイル デバイス管理  

オンプレミス Configuration Manager インフラストラクチャを使用してモバイル デバイスを管理できるようになりました。 すべてのデバイスおよび管理データはオンプレミスで処理され、Microsoft Intune またはその他のクラウド サービスの一部ではなくなります。 この種類のデバイスの管理には、クライアント ソフトウェアは必要ありません。 Configuration Manager では、デバイスの OS に組み込まれている機能を使用してデバイスが管理されます。  

詳しくは、「[オンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」をご覧ください。

## <a name="next-steps"></a>次のステップ

[増分バージョンの新機能](whats-new-incremental-versions.md)
