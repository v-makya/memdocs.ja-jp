---
title: リソース エクスプローラーを使用してソフトウェア インベントリを表示する
titleSuffix: Configuration Manager
description: Configuration Manager のソフトウェア インベントリをリソース エクスプローラーを使用して表示します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690070"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Configuration Manager のソフトウェア インベントリをリソース エクスプローラーを使用して表示する方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のリソース エクスプローラーを使用して、階層内のコンピューターから収集されたソフトウェア インベントリに関する情報を表示します。  

> [!NOTE]  
>  クライアントでソフトウェア インベントリ サイクルが実行されるまで、リソース エクスプローラーにインベントリ データは表示されません。  

 リソース エクスプローラーは、次のソフトウェアのインベントリ情報を提供します。  

-   **ソフトウェア**:  

    -   **[収集するファイル]** – ソフトウェア インベントリ中に収集されたファイル。  

    -   **[ファイルの詳細]** – ソフトウェア インベントリ中にインベントリされた、特定の製品または製造元に関連付けられていないファイル。  

    -   **[最後のソフトウェア スキャン]** – クライアント コンピューターの最後のソフトウェア インベントリとファイル コレクションの日付と時刻。  

    -   **[製品の詳細]** – ソフトウェア インベントリでインベントリされ、製造元別にグループ化されたソフトウェア製品の情報。  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Configuration Manager コンソールからリソース エクスプローラーを実行するには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** を選択します。

2.  **[資産とコンプライアンス]** ワークスペースで **[デバイス]** を選択するか、デバイスを表示するコレクションを開きます。  

3.  表示するインベントリが含まれているコンピューターをクリックしたら、 **[ホーム]** タブの **[デバイス]** グループで **[開始]**  >  **[リソース エクスプローラー ]** の順に選択します。

4.  [リソース エクスプローラー] の右ペインで、項目のどれかを右クリックしてから、 **[プロパティ]** を選択すると、より読みやすい形式で、収集されたインベントリ情報が表示されます。  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> 収集した診断ファイルの表示と管理

Configuration Manager バージョン 2002 以降では、クライアント通知を使用して[クライアント ログを収集する](../client-notification.md#client-diagnostics)際に、収集されたファイルを表示および管理するためにリソース エクスプローラーを使用します。 

1. **[デバイス]** ノードから、ログを表示するデバイスを右クリックします。
1. **[開始]** 、 **[リソース エクスプローラー]** の順に選択します。
1. **リソース エクスプローラー**で、 **[診断ファイル]** をクリックします。
1. **[診断ファイル]** の一覧で、ファイルの収集日を確認できます。 クライアント ログの名前の形式は `Support_<guid>.zip` です。
1. ZIP ファイルを右クリックし、次のオプションのいずれかを選択します。
    - **サポート センターを開く**:[サポート センター](../../../support/support-center.md)を起動します。
    - **コピー**:リソース エクスプローラーから行情報をコピーします。
    - **ファイルの表示**:ファイル エクスプローラーを使用して ZIP ファイルが配置されているフォルダーを開きます。
    - **保存**:選択したファイルの [ファイルの保存] ダイアログを開きます。
    - **エクスポート**:**診断ファイル**に表示されているリソース エクスプローラー列を保存します。
    - **更新**:ファイルの一覧を更新します。
    - **プロパティ**:選択したファイルのプロパティを返します。 

[![リソース エクスプローラーからクライアント ログを確認して保存する](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>次のステップ

収集した診断ファイルを表示するには、[サポート センターを使用します](../../../support/support-center.md)。
