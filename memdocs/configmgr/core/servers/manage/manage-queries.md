---
title: クエリを管理する
titleSuffix: Configuration Manager
description: クエリを管理する方法について説明します。 詳しい参照情報を記載した表が含まれています。
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694470"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Configuration Manager のクエリの管理方法

*適用対象:Configuration Manager (Current Branch)*

この記事は、Configuration Manager でクエリを管理する場合に役立ちます。  

 クエリの作成方法については、「[クエリの作成方法](../../../core/servers/manage/create-queries.md)」を参照してください。  

## <a name="manage-queries"></a>クエリを管理する
 **[監視]** ワークスペースで **[クエリ]** を選択し、管理するクエリと管理タスクを選択します。  

 管理タスクに関する情報を次の表に示します。  

|管理タスク|詳細| 
|---------------------|-------------|
|**実行**|Configuration Manager コンソールで選択されたクエリを実行し、結果を表示します。|
|**クライアントのインストール**|**クライアント インストール ウィザード**を開きます。これを使って、選択したクエリにより返されたコンピューターに構成マネージャー クライアントをインストールできます。<br /><br /> このオプションは、モバイル デバイスやユーザー、またはユーザー グループを返すクエリでは使用できません。 <br /><br /> クライアント プッシュで Configuration Manager をインストールする方法の詳細については、「[How to deploy clients to Windows computers](../../clients/deploy/deploy-clients-to-windows-computers.md)」 (Windows コンピューターにクライアントを展開する方法) を参照してください。| 
|**エクスポート**|**オブジェクトのエクスポート ウィザード**を開きます。 このウィザードを使って、クエリを管理オブジェクト フォーマット (MOF) ファイルにエクスポートできます。その後、これを別のサイトでインポートすることができます。
|**移動**|**[選択した項目の移動]** ダイアログ ボックスを開きます。 このダイアログ ボックスを使って、選択したクエリを、以前に **[クエリ]** ノードの下に作成したフォルダーに移動できます。|

## <a name="next-steps"></a>次のステップ 
 [クエリを作成する](../../../core/servers/manage/create-queries.md)
