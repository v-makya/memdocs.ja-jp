---
title: インターナショナル サポート
titleSuffix: Configuration Manager
description: 外国の特定の要件に準拠するように Configuration Manager を構成します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704600"
---
# <a name="international-support-in-configuration-manager"></a>Configuration Manager のインターナショナル サポート

*適用対象:Configuration Manager (Current Branch)*

次のセクションでは、Configuration Manager を外国の特定の要件に準拠させるための技術詳細について説明します。  

## <a name="gb18030-requirements"></a>GB18030 の要件  
 Configuration Manager は、GB18030 で定義された規格に対応しているため、中国で Configuration Manager を使用することができます。 GB18030 の要件を満たすには、Configuration Manager 展開に次の構成が必要です。  

-   Configuration Manager で使用する各サイト サーバー コンピューターと SQL Server コンピューターが中国語のオペレーティング システムを使用している必要があります。  

-   階層内の各サイト データベースと SQL Server の各インスタンスが同じ照合順序を使用する必要があります。以下のいずれかが使用されていなければなりません。  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  これらのデータベース照合順序は、[Configuration Manager の SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)に関する記事に記載されている要件の例外となります。  

-   **GB18030.SMS** という名前のファイルを、階層内の各サイト サーバー コンピューターのシステム ボリュームのルート フォルダーに配置する必要があります。 このファイルにはデータは保存されません。この要件を満たす名前が付けられた空のテキスト ファイルを使用できます。  
