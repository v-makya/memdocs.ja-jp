---
title: 電源管理の前提条件
titleSuffix: Configuration Manager
description: Configuration Manager の電源管理の前提条件を確認します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696520"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Configuration Manager の電源管理の前提条件

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の電源管理には、外部依存関係と製品内部依存関係があります。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  
 次の表は、電源管理を使用する場合の Configuration Manager 外部の依存関係の一覧です。  

|依存関係|説明|  
|----------------|----------------------|  
|クライアント コンピューターが、必要な電源状態をサポートできる必要があります。|電源管理のすべての機能を使用するには、クライアント コンピューターがスリープ、休止、スリープ状態からの復帰、および休止状態からの復帰、をサポートしている必要があります。 コンピューターがこれらの操作をサポートしているかどうかを判断するには、 **[電源機能]** レポートを使用できます。 詳細については、「[電源管理を監視および計画する方法](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)」トピックの「[電源機能レポート](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites)」を参照してください|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  
 次の表は、電源管理を使用する場合の Configuration Manager 内部の依存関係の一覧です。  

|依存関係|説明|  
|----------------|----------------------|  
|電源プランを作成し監視するには、事前に電源管理を有効化することが必要です。|電源管理を有効化して構成する方法の詳細については、「[電源管理の構成](../../../../core/clients/manage/power/configuring-power-management.md)」を参照してください。|  
|レポート サービス ポイント|電源管理レポートを表示するには、事前にレポート サービス ポイントを構成する必要があります。 詳細については、「[レポートの概要](../../../servers/manage/introduction-to-reporting.md)」をご覧ください。|  
