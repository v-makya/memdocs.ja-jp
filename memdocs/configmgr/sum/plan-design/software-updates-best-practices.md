---
title: ソフトウェア更新プログラムについて推奨する運用方法
titleSuffix: Configuration Manager
description: Configuration Manager でのソフトウェア更新プログラムについては、これらのベスト プラクティスを使ってください。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 3a48ce044f3d1aecbebf2ba93e936dd34b904140
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696640"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Configuration Manager でのソフトウェア更新プログラムのベスト プラクティス

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager でのソフトウェア更新プログラムに関するベスト プラクティスを説明します。 情報は、最初のインストール時のベスト プラクティスと、運用時のベスト プラクティスに分かれています。  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a> インストールについてのベスト プラクティス  

Configuration Manager にソフトウェア更新プログラムをインストールするときには、次のベスト プラクティスを使用してください。  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a> ソフトウェアの更新ポイントには共有 WSUS データベースを使用する  

プライマリ サイトに複数のソフトウェアの更新ポイントをインストールする場合、同じ Active Directory フォレストの各ソフトウェアの更新ポイントで、同じ WSUS データベースを使用します。 同じデータベースを共有すると、クライアントが新しいソフトウェアの更新ポイントに切り替えるときに発生することがあるネットワークのパフォーマンスへの影響を大幅に低減できますが、完全に排除することはできません。 クライアントが、古いソフトウェアの更新ポイントとデータベースを共有する新しいソフトウェアの更新ポイントに切り替えるときには、やはりデルタ スキャンが発生しますが、WSUS サーバーが固有のデータベースを持っている場合よりも、スキャンは大幅に軽くなります。 ソフトウェアの更新ポイントの切り替えについて詳しくは、「[ソフトウェアの更新ポイントの切り替え](plan-for-software-updates.md#BKMK_SUPSwitching)」をご覧ください。  

> [!IMPORTANT]  
>  また、ソフトウェアの更新ポイントに共有の WSUS データベースを使用する場合は、ローカルの WSUS コンテンツ フォルダーを共有します。  

WSUS データベースの共有について詳しくは、次のブログ投稿をご覧ください。  

- [Configuration Manager のソフトウェアの更新ポイント用に共有 SUSDB を実装する方法](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Configuration Manager を使用するときにコンテンツ データベースを共有する、複数の WSUS インスタンスに関する考慮事項](/archive/blogs/wsus/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb)。


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a> Configuration Manager と WSUS が同じ SQL Server を使用する場合は、一方は名前付きインスタンスを使用するように構成し、もう一方は既定のインスタンスを使用するように構成する  

Configuration Manager と WSUS のデータベースが SQL Server の同じインスタンスを共有する場合は、この 2 つのアプリケーション間のリソースの使用状況を容易に判別できなくなります。 Configuration Manager と WSUS には異なる SQL Server インスタンスを使ってください。 このように構成すると、それぞれのアプリケーションで発生する可能性のあるリソース使用の問題のトラブルシューティングおよび診断が容易になります。  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a> 設定 [更新プログラムをローカルに保存する] を指定する  

WSUS をインストールするときに、設定 **[更新プログラムをローカルに保存する]** をオンにします。 この設定を指定すると、WSUS はソフトウェア更新プログラムに関連付けられているライセンス条項をダウンロードします。 同期処理中に条項をダウンロードして、WSUS サーバーのローカル ハード ドライブに格納します。 この設定を選択しないと、クライアント コンピューターはライセンス条項が含まれるソフトウェア更新プログラムのコンプライアンス スキャンで失敗する可能性があります。 ソフトウェアの更新ポイントの **WSUS 同期マネージャー** コンポーネントは、既定では、この設定が有効になっていることを 60 分ごとに確認します。  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a> 運用に関するベスト プラクティス  

ソフトウェア更新プログラムを使用するときには、次の推奨する運用方法を使用してください。  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a> 単一のソフトウェア更新プログラムの展開を 1000 までに制限する  

ソフトウェア更新プログラムの展開ごとのソフトウェア更新プログラムの数を 1000 以下に制限します。 自動展開規則を作成するときに、指定する条件によってソフトウェア更新プログラムの数が 1000 を超えないことを確認します。 ソフトウェア更新プログラムを手動で展開する場合は、1000 を超える更新プログラムを選択しないでください。  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a> "月例パッチ" および一般の展開で ADR が実行するごとに、新しいソフトウェア更新プログラム グループを作成する  

展開内のソフトウェア更新プログラムの数には 1000 の制限があります。 自動展開規則 (ADR) を作成するときに、既存の更新グループを使用するか、規則が実行されるたびに更新グループを新しく作成するかを指定します。 ADR で、複数のソフトウェア更新プログラムが該当する条件を指定し、その規則を定期的に実行する場合、規則を実行するたびに新しいソフトウェア更新プログラム グループを作成します。 こうすることで、1 回の展開でソフトウェア更新プログラムが 1,000 の制限を超えないようにすることができます。  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a> Endpoint Protection 定義更新の ADR に対して既存のソフトウェア更新プログラム グループを使用する  

ADR を使って頻繁に Endpoint Protection の定義の更新プログラムを展開する場合は、既存のソフトウェア更新プログラム グループを常に使用します。 そうしないと、時間の経過とともに、ADR によって多くのソフトウェア更新プログラム グループが作成される可能性があります。 通常、定義の更新プログラムの発行元は、定義の更新プログラムがより新しい 4 件の更新プログラムで置き換えられると期限切れになるように設定します。 そのため、ADR によって作成されたソフトウェア更新プログラム グループには、発行元に対して 4 件 (1 件がアクティブ、3 件が置き換え済み) を超える定義更新プログラムが含まれることはありません。  



## <a name="see-also"></a>関連項目  
 [ソフトウェア更新プログラムの計画](plan-for-software-updates.md)