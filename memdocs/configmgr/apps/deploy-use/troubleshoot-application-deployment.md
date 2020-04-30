---
title: アプリ展開のトラブルシューティングのヒント
titleSuffix: Configuration Manager
description: Configuration Manager でアプリケーションの展開の問題をトラブルシューティングする場合のヒント
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689970"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>アプリケーション展開のトラブルシューティングのヒント

*適用対象:Configuration Manager (Current Branch)*

アプリケーションの展開の一般的な問題は、次のいずれかのカテゴリに分類されます。

- アプリケーションのダウンロード エラー

- アプリケーション展開のコンプライアンスが 0% でスタックする

これらのいずれかの問題が発生した場合に、この記事では、トラブルシューティングに使用できるいくつかの手順について説明します。 さらに詳細なトラブルシューティングについては、「[アプリケーション展開のトラブルシューティングに関するテクニカル リファレンス](../understand/app-deployment-technical-reference.md)」をご覧ください。


## <a name="download-failures"></a>ダウンロードの失敗

アプリケーションのダウンロードの失敗には、次の問題が含まれます。

- クライアントで、アプリケーションのダウンロードがスタックする

- クライアントで、アプリケーションのコンテンツのダウンロードに失敗する

- クライアントがアプリケーションのダウンロード中に 0% でスタックする

アプリケーションのダウンロードが失敗した場合、存在しない、または正しく構成されていない境界および境界グループがないか、まず確認します。 たとえば、クライアントがイントラネット上にあり、インターネット専用クライアント管理用に構成されていない場合、そのネットワークの場所は構成済みの境界内にある必要があります。 クライアントがコンテンツをダウンロードするには、この境界に割り当てられた境界グループも存在する必要があります。 詳しくは、「[サイト境界と境界グループの定義](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)」をご覧ください。

クライアントの境界を構成できない場合、または特定の境界グループを、別の境界グループのメンバーにすることができない場合:

1. Configuration Manager コンソールで、 **[展開の種類]** のプロパティを開きます。  

1. **[コンテンツ]** タブに切り替えます。

1. 近隣境界グループまたは既定のサイト境界グループからの配布ポイントを使用するためのセクションで、 **[展開オプション]** を **[配布ポイントからコンテンツをダウンロードしてローカルで実行する]** に変更します。 (既定でこの設定は、 **[コンテンツをダウンロードしない]** です)。

クライアントがアプリケーションのコンテンツをダウンロードできない場合、それが配布ポイントに配布されていることを確認します。 この構成を確認するには、コンソール内機能を使用して、配布ポイントへのコンテンツの配布を監視します。 詳細については、[配布したコンテンツの監視](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)に関するページを参照してください。  


## <a name="compliance-stuck-at-0"></a>コンプライアンスが 0% でスタックする

アプリケーションの展開コンプライアンスが 0% の場合、 **[展開]** ノードの下の **[監視]** ワークスペースで、アプリケーションの展開状態を確認します。

- **進行中**: クライアントで[コンテンツのダウンロード](#download-failures)がスタックしている可能性があります

- **エラー**: この問題のトラブルシューティングの詳細については、ブログ投稿の「[ヒントとテクニック:展開の失敗が報告されたアセットで是正措置を取る方法](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)」を参照してください。

- **不明**: この状態は通常、クライアントがポリシーを受け取っていないことを意味します。 クライアントが受け取ったかどうかを確認するには、クライアント ポリシーを手動で更新します。 詳細については、「[Configuration Manager クライアントのポリシーの取得開始](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」を参照してください。
  
これらのアクションによって問題が解決しない場合は、クライアントの状態を確認します。 クライアントに深い根本的な問題がある可能性があります。 詳細については、[クライアントを監視する方法](../../core/clients/manage/monitor-clients.md)に関するページを参照してください。


## <a name="next-steps"></a>次のステップ

- [アプリケーションの監視](monitor-applications-from-the-console.md)
- [アプリケーションの展開](deploy-applications.md)
- [アプリケーションの管理タスク](management-tasks-applications.md)
- [アプリケーションの展開のトラブルシューティングに関するテクニカル リファレンス](../understand/app-deployment-technical-reference.md)
