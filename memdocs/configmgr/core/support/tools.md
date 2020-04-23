---
title: Configuration Manager ツール
titleSuffix: Configuration Manager
description: Configuration Manager インフラストラクチャの管理とトラブルシューティングに役立つツールについて説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 06e308a54ee9636a7781667823e7b7f98ae6f25c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701270"
---
# <a name="configuration-manager-tools"></a>Configuration Manager ツール

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager ツールには、[クライアント ベースのツール](#client-tools)と[サーバー ベースのツール](#server-tools)があります。 これらのツールは、Configuration Manager インフラストラクチャのサポートとトラブルシューティングに役立ちます。

Configuration Manager バージョン 1806 以降、これらのツールはサイト サーバーの `CD.Latest\SMSSETUP\Tools` フォルダーに含まれるようになりました。 追加でインストールする必要はありません。<!--1357145--> これらのバージョンのツールは、Configuration Manager バージョン 1806 以降で使用してください。

[クライアントとデバイスでサポートされるオペレーティング システム](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)に関するページでサポート対象クライアントとして示されているすべての Windows オペレーティング システムは、これらのツールを使用できます。

> [!Note]  
> [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) は、Microsoft ダウンロード センターから引き続き入手できます。 Configuration Manager バージョンが 1806 以降の場合は、サイト サーバーの CD.Latest フォルダーにあるツールのバージョンを使用してください。 一部のツールは以前はツールキットに含まれていましたが、バージョン 1806 には含まれていませんでした。 これらの以前のバージョンのツールはサポートされなくなりました。


## <a name="client-tools"></a>クライアント ツール

これらのツールは、`ClientTools` サブフォルダー内にあります。

- [CMTrace](cmtrace.md):Configuration Manager ログ ファイルの表示、監視、および分析を行います  

- [Client Spy](clispy.md):ソフトウェアの配布、インベントリ、および測定に関する問題を解決します

- [Deployment Monitoring Tool](deployment-monitoring-tool.md):アプリケーション、更新プログラム、およびベースラインの展開の問題を解決します  

- [Policy Spy](policy-spy.md):ポリシーの割り当てを表示します  

- [Power Viewer Tool](power-viewer-tool.md):電源管理機能の状態を表示します  

- [Send Schedule Tool](send-schedule-tool.md):構成基準のスケジュールと評価をトリガーします  

> [!Note]  
> `ClientTools` フォルダーには、Microsoft.Diagnostics.Tracing.EventSource.dll ファイルも含まれています。 一部のクライアント ツールにはこのライブラリが必要です。 直接使用することはできません。  


## <a name="server-tools"></a>サーバー ツール

これらのツールは、`ServerTools` サブフォルダー内にあります。

- [DP Job Queue Manager](dp-job-manager.md):配布ポイントに対するコンテンツ配布ジョブの問題を解決します  

- [Collection Evaluation Viewer](ceviewer.md):コレクション評価の詳細を表示します  

- [Content Library Explorer](content-library-explorer.md):コンテンツ ライブラリの単一インスタンス ストアのコンテンツを表示します  

- [Content Library Transfer](content-library-transfer.md):ドライブ間でコンテンツ ライブラリを転送します  

- [Content Ownership Tool](content-ownership-tool.md):孤立したパッケージの所有権を変更します。 これらのパッケージは、所有するサイト サーバーがないサイトに存在します。

- [Role-based Administration and Auditing Tool](rbaviewer.md):管理者の監査ロールの構成を支援します  

- [Run Meter Summarization Tool](run-meter-summ.md):使用状況測定の概要作成タスクを実行し、使用状況測定データを分析します

> [!Note]  
> ServerTools フォルダーには、以下のファイルも含まれています。
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> 一部のサーバー ツールにはこれらのライブラリが必要です。 直接使用することはできません。  

## <a name="other-tools-and-toolkits"></a>その他のツールとツールキット

- [サポート センター](support-center.md): トラブルシューティングの際に分析を容易にするためクライアントから情報を収集します。

    バージョン 1906 以降、**OneTrace** は、サポート センターの新しいログ ビューアーです。 CMTrace と同様に機能しますが、いくつかの点が改善されています。 詳しくは、「[サポート センターの OneTrace](support-center-onetrace.md)」をご覧ください。

- [オンプレミスのサイトを拡張して Microsoft Azure に移行する](azure-migration-tool.md): Configuration Manager 用の Azure 仮想マシン (VM) をプログラムで作成するのに役立ちます。 <!--3556022--> 

- [Content Library Cleanup Tool](../plan-design/hierarchy/content-library-cleanup-tool.md):`CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` で **ContentLibraryCleanup.exe** を使用して、配布ポイントから孤立したコンテンツを削除します。  

- [Hierarchy Maintenance Tool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md):サイト サーバー上の `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` 共有フォルダーで **Preinst.exe** を使用して、階層マネージャー コンポーネントにコマンドを渡します。  

- [Update Reset Tool](../servers/manage/update-reset-tool.md):コンソール内の更新プログラムにダウンロードやレプリケートの問題がある場合に、`CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` で **CMUpdateReset.exe** を使用して問題を解決します。  

- [Service Connection Tool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md):サービス接続ポイントがオフラインの場合に、`CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` で **ServiceConnectionTool.exe** を使用してサイトを最新の状態に保ちます。   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): デスクトップ OS とサーバー OS のデプロイを自動化するための、ツール、プロセス、ガイダンスのコレクションです。

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): カスタム ソフトウェアの更新プログラムを管理してインポートするためのスタンドアロン ツールです。

- [パッケージ変換マネージャー](../../apps/pcm/package-conversion-manager.md): レガシ パッケージをアプリケーションに変換します。
