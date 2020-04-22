---
title: Content Library Transfer ツール
titleSuffix: Configuration Manager
description: Content Library Transfer ツールを使用して、あるディスク ドライブから Configuration Manager 配布ポイント上の別のディスク ドライブにコンテンツを転送します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703440"
---
# <a name="content-library-transfer-tool"></a>Content Library Transfer ツール

*適用対象:Configuration Manager (Current Branch)*

Content Library Transfer ツールは、[Configuration Manager ツール](tools.md)の 1 つです。 あるディスク ドライブから別のディスク ドライブにコンテンツを転送するツールです。 このツールは、配布ポイント サイト システム上で動作するように設計されています。 サイトまたはリモート サイト システムと併置された配布ポイントをサポートしています。  

このツールは、コンテンツ ライブラリをホストしているディスク ドライブがいっぱいになった場合のシナリオに役立ちます。 まず、コンテンツ ライブラリをホストできる十分な容量がある別のハード ディスクを追加または指定します。 次に、**ContentLibraryTransfer.exe** を使用して、古い、容量がいっぱいのハード ディスクから新しい空のドライブにコンテンツを転送します。
 
転送が完了すると、新しい場所のクライアント コンピューターからコンテンツにアクセスできるようになります。



## <a name="usage"></a>使用方法 

配布ポイント上で管理アクセス許可を持つユーザーとして **ContentLibraryTransfer.exe** を実行します。 

#### <a name="syntax"></a>構文 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>例
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>制限事項

- 配布ポイントのローカルでツールを実行します。 リモート コンピューターからは実行できません。  

- クライアントが配布ポイントにアクティブにアクセスしていない場合にのみ使用します。 クライアントがコンテンツにアクセスしているときにツールを実行すると、転送先のドライブのコンテンツ ライブラリに不完全なデータが保存される可能性があります。 データ転送が失敗し、使用できないコンテンツ ライブラリが作成される可能性があります。  

- ツールを実行するときには、配布ポイントにコンテンツを配布しないでください。 コンテンツが配布ポイントに書き込まれているときにツールを実行すると、転送先ドライブ上のコンテンツ ライブラリに不完全なデータが保存される可能性があります。 データ転送が失敗し、使用できないコンテンツ ライブラリが作成される可能性があります。



## <a name="see-also"></a>関連項目

- [コンテンツ管理の基本的な概念](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [コンテンツ ライブラリ](../plan-design/hierarchy/the-content-library.md)
