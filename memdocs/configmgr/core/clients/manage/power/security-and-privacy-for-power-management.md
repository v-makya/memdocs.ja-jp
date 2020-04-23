---
title: 電源管理のセキュリティとプライバシー
titleSuffix: Configuration Manager
description: Configuration Manager の電源管理のセキュリティとプライバシーの情報を確認します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696510"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Configuration Manager の電源管理のセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

このセクションには、Configuration Manager の電源管理のセキュリティとプライバシーの情報が含まれています。  

## <a name="security-best-practices-for-power-management"></a>電源管理に関するセキュリティのベスト プラクティス  
 電源管理に関してセキュリティ関連の推奨する運用方法はありません。  

## <a name="privacy-information-for-power-management"></a>電源管理のプライバシー情報  
 電源管理では、電力使用量を監視し、営業時間内と業務時間中に、コンピューターに電源設定を適用する、Windows に組み込まれている機能を使用します。 Configuration Manager は、コンピューターを使用するユーザーのデータを含む電力使用状況に関する情報を、コンピューターから収集します。 Configuration Manager は、各コンピューターではなく、コレクションの電力使用状況を監視しますが、コレクションは、1 台のコンピューターのみを含むことができます。 電源管理は、既定では有効になっておらず、管理者による構成が必要です。  

 Configuration Manager データベースに格納される電力使用状況情報は、Microsoft に送信されることはありません。 データベースに、詳細情報は 31 日間保持され、概要情報は 13 か月間保持されます。 削除間隔は構成できません。  

 電源管理を構成する前に、プライバシー要件について検討してください。  
