---
title: コレクションの前提条件
titleSuffix: Configuration Manager
description: Configuration Manager でコレクションを使用するための前提条件を取得します。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695540"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Configuration Manager のコレクションの前提条件

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のコレクションには、製品内依存関係のみが含まれます。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|レポート サービス ポイント|コレクションに対してレポートを実行するには、事前に レポート サービス ポイント サイト システムの役割がインストールされている必要があります。 詳細については、「[レポートの概要](../../../servers/manage/introduction-to-reporting.md)」をご覧ください。|  
|コレクションを管理するには、特定のセキュリティ アクセス許可が付与されている必要があります|コンプライアンス設定を管理するには、次のセキュリティのアクセス許可が必要です。<br /><br /> - コレクションを作成し、管理する場合:**コレクション** オブジェクトに対する**作成**、**削除**、**変更**、**フォルダーの変更**、**オブジェクトの移動**、**読み取り**、および**リソースの読み取り**のアクセス許可。<br /><br /> - コレクションの設定を管理する場合:**コレクション** オブジェクトに対する**コレクション設定の変更**のアクセス許可。<br /><br /> **フォルダーの変更** のアクセス許可は、ルート フォルダーを含む、すべてのコレクション フォルダーに必要です。|  
