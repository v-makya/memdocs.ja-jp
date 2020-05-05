---
title: オンプレミス MDM
titleSuffix: Configuration Manager
description: Configuration Manager でのオンプレミスモバイルデバイス管理 (MDM) について説明します。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724676"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>Configuration Manager でのオンプレミス MDM

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager オンプレミスモバイルデバイス管理 (MDM) は、Windows の組み込みの管理機能に依存するデバイス管理ソリューションです。 この機能は、Open Mobile アライアンス (OMA) デバイス管理 (DM) 標準に基づいています。 組織の Configuration Manager インフラストラクチャを使用して、デバイスの管理と保守を行います。 組織でこの機能を使用するには Microsoft Intune ライセンスが必要ですが、クラウド接続は必要ありません。 Configuration Manager には、デバイスに関するすべてのデータがオンプレミスのサイトデータベースに格納されます。

オンプレミスの MDM は、組み込みの OMA DM 機能にも依存する Microsoft Intune とは異なります。 Intune のすべての管理機能は、クラウドサービスを通じて配信されます。 オンプレミス MDM は、以前 Configuration Manager によって提供されていたクライアントベースの管理ソリューションとも異なります。 これは同様のインフラストラクチャに依存しますが、管理対象のデバイスに個別にインストールされたクライアントソフトウェアを使用しません。  

## <a name="comparison"></a>比較

次のセクションでは、従来のクライアントベースの管理と比較した場合のオンプレミス MDM の長所と短所について説明します。  

### <a name="advantages"></a>長所

- **簡素化**されたインフラストラクチャ: 必要なサイトシステムの役割が減少します。

- 管理が**容易**: デバイス OS に管理機能が組み込まれているため、新しい管理機能をサイトに導入するときに、新しいバージョンの Configuration Manager クライアントは必要ありません。

- **オンプレミス**: すべての管理とデータがオンプレミスに保持されます。

### <a name="disadvantages"></a>短所

**クライアント管理機能が少ない**: オーケストレーション、ソフトウェアメータリング、サードパーティ統合、タスクシーケンス、またはソフトウェアセンターのサポートはありません。

- **デバイスサポートの制限**: オンプレミス MDM では、Configuration Manager クライアントと同じ数の OS バージョンをサポートしていません。 詳しくは、[クライアントとデバイスに対してサポートされる OS のバージョン](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)に関する記事をご覧ください。

## <a name="next-step"></a>次のステップ

Configuration Manager インフラストラクチャを設定し、オンプレミス MDM でデバイス登録を計画するときの考慮事項について説明します。

> [!div class="nextstepaction"]
> [オンプレミス MDM の計画](../plan-design/plan-on-premises-mdm.md)  
