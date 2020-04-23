---
title: リモート コントロールの前提条件
titleSuffix: Configuration Manager
description: Configuration Manager のリモート コントロールの前提条件を確認します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696420"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Configuration Manager のリモート コントロールの前提条件

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のリモート コントロールには、外部依存関係と製品内部依存関係があります。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|コンピューター ビデオ カード ドライバー|リモート コントロールのパフォーマンスを最適化するため、最新のビデオ ドライバーがクライアント コンピューターにインストールされていることを確認します。|  

 Windows Embedded、Windows Embedded for Point of Service (POS)、および Windows Fundamentals for Legacy PCs を実行しているデバイスは、リモート コントロール ビューアーをサポートしませんが、リモート コントロール クライアントはサポートします。  

 Configuration Manager のリモート コントロールは、Systems Management Server 2003 または Configuration Manager 2007 を実行しているクライアント コンピューターのリモート管理には使用できません。  

> [!NOTE]  
>  Windows サービスのリモート制御の外部の依存関係として必要はありません。  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>リモート コントロール ビューアーでサポートされるオペレーティング システム  
リモート コントロール ビューアーは、Configuration Manager コンソールでサポートされるすべてのオペレーティング システムでサポートされています。 詳細については、「[Configuration Manager コンソールのサポートされている構成](../../../../core/plan-design/configs/supported-operating-systems-consoles.md)」をご覧ください。   

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|クライアントでリモート コントロールが有効になっている必要があります。|既定では、Configuration Manager をインストールする場合にリモート コントロールは有効化されていません。 電源管理を有効化して構成する方法の詳細については、「[リモート コントロールを構成する](../../../../core/clients/manage/remote-control/configuring-remote-control.md)」を参照してください。|  
|レポート サービス ポイント|リモート コントロールに対してレポートを実行するには、事前に Reporting Services ポイント サイト システムの役割がインストールされている必要があります。 詳細については、「[レポートの概要](../../../servers/manage/introduction-to-reporting.md)」をご覧ください。|  
|リモート コントロールを管理するためのセキュリティのアクセス許可|Configuration Manager コンソールからコレクション リソースにアクセスしてリモート コントロール セッションを開始する場合:**コレクション** オブジェクトに対する **読み取り**、**リソースの読み取り**、**リモート コントロール**のアクセス許可。<br /><br /> **[リモート ツール オペレーター]** セキュリティ ロールには、Configuration Manager でリモート コントロールを管理するのに必要な、これらのアクセス許可が含まれます。<br /><br /> 詳細については、「[Configuration Manager の役割ベースの管理の構成](../../../../core/servers/deploy/configure/configure-role-based-administration.md)」を参照してください。<br /><br /> さらに、許可されたビューアーには、リモート コントロールを使用するアクセス許可を付与する必要があります。この操作を行うには、 **[リモート ツール]** クライアント設定の **[リモート コントロールとリモート アシスタンス セッションを表示できるユーザー]** の一覧に該当ユーザーを追加します。
