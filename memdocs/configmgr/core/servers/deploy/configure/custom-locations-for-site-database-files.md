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
ms.openlocfilehash: cc7eb1a8ba721545bdee50d45887ab9d3aa8e952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704700"
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

-   該当するバージョンの SQL Server のドキュメントを参照し、説明に従ってユーザー データベースを移動します。 たとえば、SQL Server 2014 を使用する場合は、TechNet の「 [ユーザー データベースの移動](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) 」をご覧ください。  

-   データベース ファイルの移動が完了したら、Configuration Manager サイト サーバーで **SMS_Executive** サービスを再起動します。  
