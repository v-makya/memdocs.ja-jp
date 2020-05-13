---
title: Surface デバイス ダッシュボード
titleSuffix: Configuration Manager
description: ダッシュボードを使用して Surface デバイスに関する情報を確認します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: f9b9c49bde16754b7a60112905f14da2cd5e48eb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906294"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Configuration Manager の Surface デバイス ダッシュボード

*適用対象:Configuration Manager (Current Branch)*

バージョン 1802 以降の Surface デバイス ダッシュボードでは、ご利用の環境で検出された Surface デバイスに関する情報がひとめでわかります。 <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Surface デバイス ダッシュボードを開く

Surface デバイス ダッシュボードを開くには、次の手順を使用します。 

1. Configuration Manager コンソールを開きます。 
2. **[監視]** ノードをクリックします。 
3. ダッシュボードを読み込むには、 **[Surface デバイス]** をクリックします。

**Surface デバイス ダッシュボード**
![Surface デバイス ダッシュボード](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Surface デバイス ダッシュボードでの情報の確認

Surface デバイス ダッシュボードには、ご利用の環境の 3 つのグラフが表示されます。 

- **Surface デバイスの割合** - 環境全体の Surface デバイスの割合が示されます。

    ![Surface デバイスの割合のグラフ](media/Percent-Surface-Devices.PNG)
- **Surface モデル** - Surface モデルごとのデバイスの数が表示されます。 
  - グラフ セクションにカーソルを合わせると、選択されたモデルである Surface デバイスの割合が表示されます。 

       ![Surface モデルのグラフ](media/Surface-Models-Hover.PNG)
  - グラフ セクションをクリックすると、モデルのデバイス リストが表示されます。 
      ![Surface モデル デバイスのリスト](media/Surface-Model-Device-List.PNG)

- **上位 5 つのファームウェア バージョン** - 環境内の上位 5 つのファームウェア モデルを示すグラフが表示されます。 
  - グラフ セクションにカーソルを合わせると、選択されたファームウェア バージョンである Surface デバイスの数が表示されます。 Configuration Manager バージョン 1806 以降では、グラフのセクションをクリックすると、関連するデバイスの一覧が表示されます。 <!--1358654-->
     ![Surface モデル デバイスのリスト](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>説明

Surface デバイスの詳細については、[Surface](https://www.microsoft.com/surface) の Web サイトを参照してください。

Configuration Manager に Surface のファームウェアの更新プログラムを配布する方法については、[Surface ドライバーの更新プログラムを管理する方法](https://support.microsoft.com/help/4098906)に関するページを参照してください。




