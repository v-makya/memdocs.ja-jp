---
title: 電源管理の概要
titleSuffix: Configuration Manager
description: Configuration Manager の電源管理の概要を確認します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 400fe3113207217504317eeb8ef8bbce4ab6a298
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696570"
---
# <a name="introduction-to-power-management-in-configuration-manager"></a>Configuration Manager の電源管理の概要

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の電源管理は、組織内のコンピューターの電力消費量を監視し、削減するという、多くの組織が抱えているニーズに対応することができます。 この機能は、Windows に組み込まれている電源管理機能を利用して、組織内のコンピューターに適切で一貫性のある設定を適用します。 業務時間内と業務時間外でそれぞれ異なる電源設定をコンピューターに適用できます。 たとえば業務時間外には、より制限された電源プランを適用することが可能です。 コンピューターを常にオンにしておく必要がある場合は、電源管理設定の適用から除外できます。  

 Configuration Manager の電源管理には、組織における電力消費量やコンピューターの電源設定を分析するのに役立つ複数のレポート機能が含まれています。 また、こうしたレポートは、電源管理にかかわる問題のトラブルシューティングにも利用できます。  

 電源管理の構成と使用のワークフローの詳細については、「[電源管理の管理者チェックリスト](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md)」を参照してください。  

> [!IMPORTANT]  
>  Configuration Manager の電源管理は仮想マシンではサポートされていません。 仮想マシンには電源プランを適用できません。また仮想マシンの電源データをレポートすることもできません。  

## <a name="the-power-management-workflow"></a>電源管理のワークフロー  
 Configuration Manager で電源管理を計画し、実装するには、次の 3 つの段階を使用します。  

### <a name="monitoring-and-planning-phase"></a>監視および計画段階  
 電源管理は、Configuration Manager のハードウェア インベントリを使用してサイト内のコンピューターの使用状況と電源設定に関するデータを収集します。 このデータを分析して、これらのコンピューターに最適な電源管理設定を特定するのに利用できる各種のレポートがあります。 たとえば、電源管理ワークフローの監視および計画段階では、 **[電源機能]** レポートに含まれるデータに基づいてコレクションを作成し、このデータを使って電源管理できないコンピューターを特定することができます。 これにより、これらのコンピューターを電源管理対象から排除できます。  

> [!IMPORTANT]  
>  クライアント コンピューターの電源データを収集して分析するまでは、サイト内のコンピューターに電源プランを適用しないでください。 既存の設定について調査を行わずに新しい電源管理設定を適用すると、電力消費量が増える結果になる可能性があります。  

### <a name="enforcement-phase"></a>実施段階  
 電源管理を使用すると、サイト内のコンピューターのコレクションに適用できる電源プランを作成することができます。 これらの電源プランは、複数のコンピューター上で Windows の電源管理設定を構成します。 Configuration Manager に付属の電源プランを使用するか、カスタムの電源プランを構成することができます。 監視および計画段階で収集された電源データは、コンピューターに電源プランを適用した後の省電力効果を評価するための基準として使用できます。 詳細については、「[電源管理の管理者チェックリスト](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md)」を参照してください  

### <a name="compliance-phase"></a>対応評価段階  
 対応評価段階では、組織における電力の使用状況と電力コストの削減効果を評価するためのレポートを実行します。 コンピューターが生成する CO2 量の改善状態を説明するレポートも実行できます。 コンピューターに電源設定が正しく適用されているかどうかを確認したり、電源管理機能の問題のトラブルシューティングをするために役立つレポートを作成することもできます。  
