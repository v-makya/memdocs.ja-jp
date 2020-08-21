---
title: データベース ファイルのカスタムの場所
titleSuffix: Configuration Manager
description: SQL Server データベース ファイルのカスタムの場所を指定する方法について説明します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff992361959fcaad51acf3b78f5618e95f5af9e0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692606"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Configuration Manager のサイト データベース ファイルのカスタムの場所

*適用対象:Configuration Manager (Current Branch)*

 Configuration Manager は、SQL Server データベース ファイルのカスタムの場所をサポートしています。  

> [!NOTE]  
>  既定以外のファイルの場所を指定するオプションは、SQL Server クラスターを使用する場合は使用できません。  

 新しいプライマリ サイトまたは中央管理サイトの**セットアップ中**に、次のことができます。  

-   **サイト データベースの既定以外のファイルの場所の指定**:Configuration Manager のセットアップによって、これらの場所を使用してサイト データベースが作成されます。  

-   **カスタムのファイルの場所を使用する、事前に作成した SQL Server データベースの使用の指定**:Configuration Manager のセットアップでは、事前に作成したデータベースとその構成済みのファイルの場所を使用します。  

**セットアップ後に**、サイト データベース ファイルの場所を変更できます。 これには、次のようにサイトを停止して、SQL Server でファイルの場所を編集する必要があります。  

-   Configuration Manager サイト サーバーで、**SMS_Executive** サービスを停止します。  

-   ユーザー データベースを移動する方法の詳細については、[ユーザー データベースの移動](/sql/relational-databases/databases/move-user-databases?view=sql-server-2014)に関するページを参照してください。  

-   データベース ファイルの移動が完了したら、Configuration Manager サイト サーバーで **SMS_Executive** サービスを再起動します。