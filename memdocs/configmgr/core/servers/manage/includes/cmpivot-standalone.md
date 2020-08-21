---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128336"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

バージョン 1906 以降では、CMPivot をスタンドアロン アプリとして使用できます。 CMPivot スタンドアロンは、英語でのみ利用できます。 CMPivot を Configuration Manager コンソールの外で実行して、環境内にあるデバイスの状態をリアルタイムで表示することができます。 この変更により、最初にコンソールをインストールしなくてもデバイスで CMPivot を使用できます。

> [!Tip]  
> この機能はバージョン 1906 で[プレリリース機能](../pre-release-features.md)として初めて導入されました。 バージョン 2002 以降、プレリリース機能ではなくなりました。  

CMPivot の機能を、ヘルプデスクやセキュリティ管理者など、コンソールをコンピューターにインストールしていない他のユーザーと共有できます。 他のユーザーは今まで使用していた他のツールと共に CMPivot を使用し、Configuration Manager にクエリを実行できます。 この充実した管理データを共有することで、職務をまたぐビジネス上の問題を同僚と共に事前解決できます。

#### <a name="install-cmpivot-standalone"></a>CMPivot スタンドアロンのインストール

1. CMPivot の実行に必要なアクセス許可を設定します。 詳細については、「[前提条件](../cmpivot.md#prerequisites)」を参照してください。 [セキュリティ管理者のロール](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906)がユーザーに適している場合、そのアクセス許可を使用することもできます。
2. CMPivot アプリのインストーラは、`<site install path>\tools\CMPivot\CMPivot.msi`にあります。 アプリはこのパスから実行するか、別の場所にコピーできます。
3. CMPivot スタンドアロン アプリを実行すると、サイトに接続するように求められます。 中央管理サイトまたはプライマリ サイトのサーバーの完全修飾ドメイン名またはコンピューター名を指定します。
   - CMPivot スタンドアロンを開くたびにサイト サーバーに接続するように求められます。
4. CMPivot を実行するコレクションを参照して、クエリを実行します。

   ![クエリを実行するコレクションを参照します。](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - アクションを右クリックします。**スクリプトの実行**、**リソース エクスプローラー**、Web 検索などは、CMPivot スタンドアロンでは使用できません。 CMPivot スタンドアロンの主な用途は、Configuration Manager インフラストラクチャとは別にクエリを実行することです。 セキュリティ管理者を支援するために、CMPivot スタンドアロンには Microsoft Defender セキュリティ センターに接続する機能が含まれています。 <!--5605358-->
> - バージョン 1910 以降では、[CMPivot スタンドアロンを使用したローカル デバイスのクエリ評価](../cmpivot-changes.md#bkmk_local-eval)を行えます。 <!--3197353--> 