---
title: 診断と使用状況データのレベル
titleSuffix: Configuration Manager
description: Configuration Manager で収集される診断と使用状況データのレベルについて説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9de63280786d620229c7d408f09ef2fe583e231d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703800"
---
# <a name="levels-of-diagnostic-usage-data"></a>診断と使用状況データのレベル

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、**基本**、**エンハンス**、**フル**の 3 つのレベルの診断結果と使用状況データが収集されます。 既定では、この機能は、エンハンス レベルに設定されます。

> [!IMPORTANT]
> Configuration Manager は、基本レベルとエンハンス レベルでは、サイト コード、サイト名、IP アドレス、ユーザー名、コンピューター名、物理アドレス、電子メール アドレスを収集しません。 フル レベルで収集したこの情報に特別な目的はありません。 ログ ファイルやメモリ スナップショットなどの詳細な診断情報に含まれる可能性があります。 Microsoft が個人の特定、連絡、広告作成の目的でこの情報を使用することはありません。

## <a name="levels"></a>レベル

### <a name="basic"></a>基本

基本レベルには、階層に関するデータが含まれています。 インストールまたはアップグレードのエクスペリエンスを向上させるために必要です。 また、このデータは、階層に適用できる Configuration Manager の更新プログラムの確認にも役立ちます。

### <a name="enhanced"></a>拡張

エンハンス レベルはセットアップ終了後の既定値です。 このレベルには、基本レベルで収集されるデータと、機能固有のデータが含まれます。 さまざまな機能の使用の頻度と期間が示されます。 また、Configuration Manager のクライアント設定データ (コンポーネント名、状態、およびポーリング間隔などの特定の設定) も含まれています。 ソフトウェア更新プログラムに関する情報は、機能の使用状況に関する基本的な情報であり、このレベルでの更新プログラムの対応に関するデータは含まれていません。

製品とサービスを改善するための最小限のデータが提供されるため、このレベルをお勧めします。

このレベルで収集されないデータの例としては、次のようなものがあります。

- サイト、ユーザー、コンピューター、またはその他のオブジェクトの名前

- セキュリティ関連オブジェクトのオブジェクトの詳細

- ソフトウェア更新プログラムを必要とするシステムの数などの脆弱性

### <a name="full"></a>完全

フル レベルには、基本レベルとエンハンス レベルのすべてのデータが含まれます。 また、Endpoint Protection の詳細情報、更新プログラムの対応率、およびソフトウェア更新プログラム情報も含まれています。 このレベルには、システム ファイルやメモリ スナップショットなどの高度な診断情報も含まれることがあります。 この高度なデータには、キャプチャの時点でメモリやログ ファイルに存在する個人情報が含まれる可能性があります。

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> レベルを変更する方法

データ収集レベルを変更するには、**サイト** オブジェクト クラスでアクセス許可を**変更**する必要があります。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。
1. リボンの **[階層設定]** を選択します。
1. **[診断と使用状況データ]** タブに切り替え、データ レベルを選択します。

## <a name="version-specific-details"></a><a name="bkmk_versions"></a> バージョン固有の詳細

以下の記事では、サポートされている各バージョンで、Configuration Manager によって各レベルで収集される特定のデータについて詳しく説明しています。

- [2002 での診断情報と使用状況データ](levels-of-diagnostic-usage-data-collection-2002.md)
- [1910 での診断情報と使用状況データ](levels-of-diagnostic-usage-data-collection-1910.md)
- [1906 での診断情報と使用状況データ](levels-of-diagnostic-usage-data-collection-1906.md)
- [1902 での診断情報と使用状況データ](levels-of-diagnostic-usage-data-collection-1902.md)
- [1810 での診断情報と使用状況データ](levels-of-diagnostic-usage-data-collection-1810.md)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [よく寄せられる質問](frequently-asked-questions.md)
