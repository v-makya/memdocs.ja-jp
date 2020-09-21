---
title: Intune でのデータの保存と処理
titleSuffix: Microsoft Intune
description: Intune で個人データがどのように格納され、処理されるかについて学習します。
keywords: データ, プライバシー
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c7c597a6d196ab5f8c3170cd5880682a280e73
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076065"
---
# <a name="data-storage-and-processing-in-intune"></a>Intune でのデータの保存と処理

### <a name="storing-customer-data"></a>顧客データの格納

Intune により[データが収集](privacy-data-collect.md)されると、Intune は、顧客データの保存方法と処理方法が指定された Microsoft 365 のデータ処理の標準ポリシーに従います。 「[Microsoft 365 顧客データの保存場所](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations)」を参照してください。 個人データは、[Microsoft オンライン サービス条件 (OST)](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46) によって保証される技術的セキュリティ対策の下、Intune サービスの監査コンプライアンスの範囲内で処理されます。

### <a name="storage-locations"></a>保存場所

Microsoft では、世界中のさまざまな地域で Intune サービスの提供と運用を行っています。 Intune では、顧客データの管理者が選択した保存場所が尊重されます。

詳細については、「[データ センターの場所](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations?view=o365-worldwide#data-center-locations)」を参照してください。

### <a name="personal-data-retention"></a>個人データ保有期間

Microsoft 365 データ処理の標準ポリシーは、顧客データが削除後どのくらいの期間保持されるかを規定します。 顧客データの削除には、次の 2 つのシナリオがあります。

-**アクティブな削除**:テナントにアクティブなサブスクリプションがあり、ユーザーまたは管理者がデータを削除するか、管理者がユーザーを削除する。
-**パッシブな削除**:テナントのサブスクリプションが終了する。

各削除シナリオについては、「[Microsoft 365 でのデータの保持、削除、および破棄](https://docs.microsoft.com/microsoft-365/enterprise/microsoft-365-data-retention-deletion-and-destruction-overview?view=o365-worldwide)」を参照してください。  

一般に、Intune によって収集された個人データは、削除後 30 日以内に削除されます。 監査ログは、セキュリティ目的で最大 1 年間は保持されます。 


## <a name="processing-personal-data"></a>個人データの処理

Intune では、ISO 認定システムを使用して個人データが処理されます。 詳細については、「[Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp)」を参照してください。

### <a name="profiling-and-marketing"></a>プロファイルとマーケティング

Microsoft Intune では、プロファイルまたはマーケティングの目的でサービスを提供する一環として収集された個人データが使用されることはありません。 

## <a name="next-steps"></a>次のステップ

Intune が個人データを[保護および共有](privacy-data-secure-share.md)する方法について確認します。 
