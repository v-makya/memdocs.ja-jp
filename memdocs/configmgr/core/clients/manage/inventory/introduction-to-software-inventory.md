---
title: ソフトウェア インベントリ
titleSuffix: Configuration Manager
description: Configuration Manager のソフトウェア インベントリの概要を取得します。
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695390"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Configuration Manager のソフトウェア インベントリの概要

*適用対象:Configuration Manager (Current Branch)*

ソフトウェア インベントリを利用し、クライアント デバイスでファイルに関する情報を収集します。 また、ソフトウェア インベントリはクライアント デバイスからファイルを収集し、サイト サーバーに格納することができます。 クライアント設定で **[クライアントのソフトウェア インベントリを有効にする]** 設定を選択すると、ソフトウェア インベントリが収集されます。 この操作をクライアント設定でスケジュールすることもできます。  

ソフトウェア インベントリを有効にし、クライアントによってソフトウェア インベントリが実行されると、クライアント サイトの管理ポイントにクライアントから情報が送信されます。 インベントリ情報は、さらに管理ポイントによって Configuration Manager サイト サーバーに転送され、そこでサイト データベースに保存されます。

 ソフトウェア インベントリ データを表示する方法はいくつかあります。  

- 指定のファイルとデバイスを返す[クエリを作成](../../../../core/servers/manage/create-queries.md)する。   

- 指定のファイルとデバイスを含む[クエリベース コレクション](../../../../core/clients/manage/collections/introduction-to-collections.md)を作成する。   

- デバイスでファイルに関する詳細を提供する[レポートを実行](../../../servers/manage/introduction-to-reporting.md)する。

- [リソース エクスプローラー](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)を使用して、クライアント デバイスから収集され、インベントリされたファイルに関する詳細情報を表示する。   

 ソフトウェア インベントリをクライアント デバイス上で実行するとき、最初のレポートは完全なインベントリとなります。 後続のレポートには差分インベントリ情報のみが含まれます。 サイト サーバーは受け取った順番にデルタ情報を処理します。 クライアントの差分情報が不足している場合は、サイト サーバーによりさらなる差分情報が拒否され、完全なインベントリを実行するようクライアントに指示が出されます。  

 Configuration Manager ではデュアル ブート コンピューターを検出できますが、インベントリ情報が返されるのは、インベントリの実行時にアクティブだったオペレーティング システムからのみです。  
