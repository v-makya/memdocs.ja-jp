---
title: 'ハードウェア インベントリ '
titleSuffix: Configuration Manager
description: Configuration Manager のハードウェア インベントリの概要を取得します。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695410"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Configuration Manager のハードウェア インベントリの概要

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のハードウェア インベントリを使用して、組織内のクライアント デバイスのハードウェア構成に関する情報を収集します。 ハードウェア インベントリを収集するには、クライアント設定で **[クライアントのハードウェア インベントリを有効にする]** 設定を選択する必要があります。  

 ハードウェア インベントリが有効化され、クライアントによってハードウェア インベントリ サイクルが実行されたら、クライアント サイトの管理ポイントにクライアントから情報が送信されます。 インベントリ情報は、さらに管理ポイントによって Configuration Manager サイト サーバーに転送され、ここでサイト データベースに保存されます。 ハードウェア インベントリは、クライアント設定で指定されたスケジュールに従って、クライアントに対して実行されます。  
## <a name="view-hardware-inventory"></a>ハードウェア インベントリを表示する 

 Configuration Manager によって収集されたハードウェア インベントリ データは、いくつかの方法で確認することができます。次の方法などがあります。  

- [特定のハードウェア構成に基づいたデバイスを返すクエリを作成する](../../../../core/servers/manage/introduction-to-queries.md)。  

- [特定のハードウェア構成に基づいたクエリベースのコレクションを作成する](../../../../core/clients/manage/collections/introduction-to-collections.md)。 クエリベースのコレクションのメンバーシップは、スケジュールに従って自動的に更新されます。 コレクションは、ソフトウェアの展開など、各種のタスクに使用できます。

- [組織内のハードウェア構成に関する特定の詳細情報を表示するレポートを実行する](../../../servers/manage/introduction-to-reporting.md)。

- [リソース エクスプローラーを使用](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)して、クライアント デバイスから収集されたハードウェア インベントリに関する詳細情報を表示する。

ハードウェア インベントリをクライアント デバイス上で実行するときは、最初に返されるインベントリ レポートは必ず、完全なインベントリとなります。 後続のインベントリ データには、差分インベントリ情報のみが含まれます。 サイト サーバーによって、受け取った順番に差分インベントリ情報が処理されます。 クライアントの差分情報が不足している場合は、サイト サーバーによりさらなる差分情報が拒否され、完全なインベントリ サイクルを実行するようクライアントに指示が出されます。  

 Configuration Manager のデュアル ブート コンピューターに対するサポートは限定的です。 Configuration Manager ではデュアル ブート コンピューターを検出できますが、インベントリ情報が返されるのは、インベントリ サイクルの実行時にアクティブだったオペレーティング システムからのみです。  

> [!NOTE]  
>  Linux および UNIX を実行しているクライアントでハードウェア インベントリを使用する方法については、[Linux および UNIX のハードウェア インベントリ](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)に関するページを参照してください。  

## <a name="extending-configuration-manager-hardware-inventory"></a>Configuration Manager のハードウェア インベントリの拡張  
 Configuration Manager に組み込まれたハードウェア インベントリに加え、次の方法のいずれかを使って、さらなる情報を収集するようハードウェア インベントリを拡張することもできます。  

- Configuration Manager コンソールから、ハードウェア インベントリのインベントリ クラスの有効化、無効化、追加、削除を行う。  
- NOIDMIF ファイルを使って、Configuration Manager ではインベントリできないクライアント デバイスに関する情報を収集する。 たとえば、デバイス上にラベルとしてのみ存在するデバイス資産番号情報を収集できます。 NOIDMIF のインベントリは、収集元のクライアント デバイスに自動的に関連付けられます。  
- IDMIF ファイルを使って、プロジェクター、複写機、ネットワーク プリンターなど、構成マネージャー クライアントに関連付けられていない資産に関する情報を収集する。


## <a name="next-steps"></a>次のステップ
これらの方法を使用して Configuration Manager ハードウェア インベントリを拡張する方法の詳細については、[ハードウェア インベントリを構成する方法](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)に関するページを参照してください。  
