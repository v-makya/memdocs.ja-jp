---
title: コレクションの概要
titleSuffix: Configuration Manager
description: Configuration Manager でのコレクションの使用に関する概要を取得します。
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e43f5a36f2a1bf44959b9645c2fb48a22cc71f1
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126775"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Configuration Manager のコレクションの概要

*適用対象:Configuration Manager (Current Branch)*

コレクションを使用すると、リソースを管理しやすい単位に整理できます。 コレクションを作成すると、クライアント管理のニーズを満たし、複数のリソースで操作を同時に実行することができます。 

管理タスクのほとんどは、1 つ以上のコレクションに依存、または使用する必要があります。 組み込みのコレクションである [すべてのシステム] を使用することもできますが、管理タスクでこのコレクションを使用することはお勧めしません。 タスクに対するデバイスまたはユーザーをより具体的に識別できるようにカスタム コレクションを作成します。  

 組み込みコレクションおよびカスタム コレクションは、Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースの **[ユーザー コレクション]** ノードと **[デバイス コレクション]** ノードに表示されます。  

 最近確認したコレクションは、 **[資産とコンプライアンス]** ワークスペースの **[ユーザー]** ノードと **[デバイス]** ノードに表示されます。  

コレクションの使用例を次に示します。  

|操作|例|  
|---------|-------|  
|リソースのグループ化|組織の階層に基づいてリソースをグループ化したコレクションを作成できます。<br /><br /> たとえば、"ロンドン本社" Active Directory 組織単位 (OU) にあるすべてのコンピューターのコレクションを作成することができます。 この種類のコレクションを作成する方法の詳細については、[コレクションの作成方法](../../../../core/clients/manage/collections/create-collections.md)に関するページを参照してください。<br /><br /> このコレクションは、たとえば、Endpoint Protection の設定を構成したり、デバイス電源管理設定を構成したり、Configuration Manager クライアントをインストールしたりする場合に使用できます。|  
|アプリケーションの展開|Microsoft 365 Apps がインストールされていないすべてのコンピューターのコレクションを作成し、このソフトウェアをそのコレクションのすべてのコンピューターにインストールすることができます。<br /><br /> アプリケーションの要件を使用してこのタスクを実行することもできます。 詳細については、[Configuration Manager でアプリケーションを作成する方法](../../../../apps/deploy-use/create-applications.md)に関するページを参照してください。|  
|[クライアント設定の管理](../../../../core/clients/deploy/about-client-settings.md)|Configuration Manager の既定のクライアント設定はすべてのデバイスとすべてのユーザーに適用されますが、デバイスのコレクションまたはユーザーのコレクションに適用されるカスタム クライアント設定を作成することもできます。<br /><br /> たとえば、リモート コントロールを一部のデバイスを除くすべてのデバイスで使用可能にする場合、リモート コントロールを許可するよう既定のクライアント設定を構成し、その後、リモート コントロールを許可しないカスタム クライアント設定を構成し、それらを例外的なクライアントのコレクションに展開することができます。 |  
|[電源管理](../power/introduction-to-power-management.md)|コレクションごとに特定の電源設定を構成することができます。|  
|[役割に基づいた管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|コレクションを使用して Configuration Manager コンソールの各種機能にアクセスできるユーザーのグループを制御します。|  
|[メンテナンス期間](../../../../core/clients/manage/collections/use-maintenance-windows.md)|メンテナンス期間を使用すると、デバイス コレクションのメンバーに対して Configuration Manager の各種の操作が実行できる期間を定義できます。 |  


## <a name="collection-types-in-configuration-manager"></a>Configuration Manager のコレクションの種類について  
 Configuration Manager には、一般的な操作のコレクションが組み込まれています。カスタム コレクションを作成することもできます。   

### <a name="built-in-collections"></a>組み込みコレクション  
 既定では、Configuration Manager は、次の変更できないコレクションを含みます。  

|**コレクション名**|[説明]|  
|-------------------------|-----------------|  
|**すべてのユーザー グループ**|Active Directory セキュリティ グループの探索を使用して検出されたユーザー グループを含みます。|  
|**すべてのユーザー**|Active Directory ユーザー探索を使用して検出されたユーザーを含みます。|  
|**すべてのユーザーおよびユーザー グループ**|すべてのユーザーとすべてのユーザー グループのコレクションを含みます。 このコレクションには、ユーザーおよびユーザー グループのリソースの最大スコープが含まれています。|  
|**すべてのデスクトップ クライアントおよびサーバー クライアント**|Configuration Manager クライアントをインストールした、サーバー デバイスとデスクトップ デバイスを含みます。 メンバーシップは、定期探索で保守されます。|  
|**すべてのモバイル デバイス**|Configuration Manager が管理するモバイル デバイスが含まれます。 メンバーシップは、正常にサイトに割り当てられている、あるいは Exchange Server コネクタによって検出されたモバイル デバイスに制限されます。|  
|**すべてのシステム**|すべてのデスクトップ クライアントおよびサーバー クライアントのコレクション、すべてのモバイル デバイスのコレクション、すべての不明なコンピューターのコレクション、および Microsoft Intune によって登録されているすべてのモバイル デバイスを含みます。 このコレクションには、デバイス リソースの最大限のスコープが含まれます。|  
|**すべての不明なコンピューター**|複数のコンピューター プラットフォームの一般的コンピューター レコードを含みます。 このコレクションを使用すると、タスク シーケンスと、PXE ブート、起動可能メディア、または事前設定されたメディアを使用して、オペレーティング システムを展開することができます。|  

### <a name="custom-collections"></a>カスタム コレクション  
 [コレクションの作成方法](../../../../core/clients/manage/collections/create-collections.md)に関するページで説明されているように、Configuration Manager にカスタム コレクションを作成すると、そのコレクションのメンバーシップは 1 つまたは複数の収集ルールによって決定されます。 

