---
title: Power Viewer Tool
titleSuffix: Configuration Manager
description: Power Viewer Tool を使用すると、Configuration Manager クライアントで電源管理機能の状態を確認できます。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707570"
---
# <a name="power-viewer-tool"></a>Power Viewer Tool

*適用対象:Configuration Manager (Current Branch)*

Power Viewer Tool は、[Configuration Manager のツール](tools.md)の 1 つです。 これを使用すると、Configuration Manager クライアントの電源管理機能の状態を確認できます。

管理者として **PowerVwr.exe** を実行します。 ツールが起動されると、ローカル コンピューターの **[Power Config]\(電源構成\)** タブに電源機能と電源設定が表示されます。 

リモート コンピューターの電源管理データを表示するには:  

1. **[ファイル]** メニューに移動し、 **[接続]** をクリックします。 

2. **[コンピューター]** 名と必要に応じて **[ユーザー名]** と **[パスワード]** を入力します。 

Power Viewer にはタブが 3 つあります。  

- **Power Config (電源構成)** :対象のコンピューターの電源機能と電源設定を参照できます。  

- **Daily Activity (毎日のアクティビティ)** :次の情報を含むクライアントの毎日のアクティビティ グラフを参照できます。  

    - **コンピューター オン**:コンピューターの 1 日の電源状態です。 スリープ モードは、電源がオフになっていると見なされます。  

    - **モニター オン**:モニターの 1 日のオンまたはオフの状態です。  

    - **User Active (アクティブなユーザー)** :1 日のユーザー アクティビティ情報です。  

- **Power Events (電源イベント)** :電源イベントを日単位ですべて表示します。 これらのイベントは、クライアントによって午前 12:00 時にまとめられます。 このまとめによって、日単位のアクティビティ グラフのデータが生成されます。  
