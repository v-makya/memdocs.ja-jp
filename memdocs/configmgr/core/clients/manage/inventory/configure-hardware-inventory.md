---
title: ハードウェア インベントリを構成する
titleSuffix: Configuration Manager
description: Configuration Manager ですべてのクライアントまたは 1 つのコレクションに対してハードウェア インベントリを設定します。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695450"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>Configuration Manager でハードウェア インベントリを構成する方法

*適用対象:Configuration Manager (Current Branch)*

この手順により、ハードウェア インベントリの既定のクライアント設定を構成し、階層内のすべてのクライアントに適用します。 いくつかのクライアントにのみこの設定を適用するには、カスタムのデバイス クライアント設定を作成し、ハードウェア インベントリを使用するデバイスが含まれるコレクションにそれを割り当てます。 [クライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)に関するページを参照してください。  

> [!NOTE]  
>  クライアント デバイスが複数のクライアント設定をハードウェア インベントリを受信した場合は、各設定のハードウェア インベントリのクラスは、クライアントがハードウェア インベントリをレポートするときに結合されます。 さらに、優先順位が高いカスタム クライアント設定でクラスをオンにしないと、クライアントでのそのクラスのインベントリ作成は無効になりません。 

一部を除く大部分のシステムで特定のハードウェア インベントリ クラスを無効にするには、既定のクライアント設定でそのクラスをオフにする必要があります。 その後、そのクラスを有効にするカスタム クライアント設定を作成して、それをターゲット システムにデプロイします。


### <a name="to-configure-hardware-inventory"></a>ハードウェア インベントリを構成するには  

1.  Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]**  >  **[既定のクライアント設定]** の順に選択します。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** を選択します。  

5.  **[既定の設定]** ダイアログ ボックスで、 **[ハードウェア インベントリ]** を選択します。  

6.  **[デバイスの設定]** 一覧で、次を構成します。  

    -   **クライアントのハードウェア インベントリを有効にする** - **[はい]** を選択します。  

    -   **ハードウェア インベントリのスケジュール** - **[スケジュール]** をクリックしてクライアントがハードウェア インベントリを収集する間隔を指定します。  

7.  必要なその他の[ハードウェア インベントリのクライアント設定](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory)を構成します。  

クライアント デバイスは、次の機会にクライアント ポリシーをダウンロードしたときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「[クライアントを管理する方法](../../../../core/clients/manage/manage-clients.md)」を参照してください。  
