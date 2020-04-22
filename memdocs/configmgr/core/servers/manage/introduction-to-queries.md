---
title: クエリの概要
titleSuffix: Configuration Manager
description: クエリを作成して実行すると、Configuration Manager 階層内で、クエリ条件に一致するオブジェクトを見つけることができます。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694570"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Configuration Manager のクエリの概要

*適用対象:Configuration Manager (Current Branch)*

クエリを作成して実行すると、Configuration Manager 階層内で、クエリ条件に一致するオブジェクトを見つけることができます。 このようなオブジェクトとしては、特定の種類のコンピューターやユーザー グループなどの項目があります。 クエリは、サイト、コレクション、アプリケーション、インベントリ データなど、ほとんどの種類の Configuration Manager オブジェクトを返すことができます。  

## <a name="query-creation-overview"></a>クエリ作成の概要

 クエリを作成するときは、少なくとも 2 つのパラメーター、つまり検索する場所と検索する対象を指定する必要があります。 たとえば、Configuration Manager サイトのすべてのコンピューター上にある利用可能なハード ドライブ領域の量を確認するには、利用可能なハード ドライブ領域について、 **[論理ディスク]** 属性クラスと **[空き領域 (MB)]** 属性を検索するクエリを作成します。  

 最初のクエリを作成した後、追加のクエリ条件を指定できます。 たとえば、クエリ結果が特定のサイトに割り当てられたコンピューターのみを含むように指定することができます。 また、結果の表示方法を変更して、自分にとって役立つ順序で結果を表示することもできます。 たとえば、ハード ドライブの空き領域の量を基準にして結果を並べ替え、昇順または降順で表示するように指定できます。  

 作成したクエリは Configuration Manager によって並び替えられ、 **[監視]** ワークスペースの **[クエリ]** ノードに表示されます。 この場所から、新しいクエリの作成や、既存のクエリの実行、更新、管理を行えます。  

 また、クエリを Configuration Manager コレクションのクエリ規則にインポートすることもできます。 詳しくは、「[コレクションを作成する方法](../../../core/clients/manage/collections/create-collections.md)」をご覧ください。  

## <a name="next-steps"></a>次のステップ

 [クエリを作成する方法](../../../core/servers/manage/create-queries.md)
