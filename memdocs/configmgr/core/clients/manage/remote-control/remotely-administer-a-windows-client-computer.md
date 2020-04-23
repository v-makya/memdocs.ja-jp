---
title: Windows クライアント コンピューターのリモート管理
titleSuffix: Configuration Manager
description: Configuration Manager を使用してリモートの Windows クライアント コンピューターを管理します。
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696410"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>Configuration Manager を使用して Windows クライアント コンピューターをリモート管理する方法

*適用対象:Configuration Manager (Current Branch)* Configuration Manager では、 **[Configuration Manager リモート コントロール]** を使用して、クライアント コンピューターに接続できます。 リモート制御を使用し始める前に、次の記事の情報を確認してください。  

-   [リモート コントロールの前提条件](prerequisites-for-remote-control.md)  

-   [リモート コントロールの構成](configuring-remote-control.md)  

リモート コントロール ビューアーを起動するには、次の 3 つの方法があります。  

-   Configuration Manager コンソールを使用する。  

-   Windows のコマンド プロンプトを使用する。  

-   **Microsoft System Center** プログラム グループ内にある Configuration Manager コンソールを実行するコンピューター上の Windows **[スタート]** メニューを使用する。  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Configuration Manager コンソールからクライアント コンピューターをリモート管理するには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[デバイス]** または **[ユーザー コレクション]** の順に選択します。  

3.  リモートで管理するコンピューターを選択し、 **[ホーム]** タブの **[デバイス]** グループで、 **[開始]**  >  **[リモート コントロール]** を選択します。  

    > [!IMPORTANT]  
    >  場合、クライアント設定 **リモート制御のプロンプトのユーザー** にアクセス許可が設定されている **True**, 、接続では、リモート コンピューターのユーザーがリモート コントロール プロンプトに同意するまでは開始されません。 詳しくは、「[リモート コントロールの構成](configuring-remote-control.md)」を参照してください。  

4.  **[Configuration Manager リモート コントロール]** ウィンドウが開いたら、クライアント コンピューターをリモート管理できます。 接続を構成するには、次のオプションを使用します。  

    > [!NOTE]  
    >  接続するコンピューターに複数のモニターがある場合は、すべてのモニターの表示画面がリモート コントロール ウィンドウに表示されます。  

    -   **File**
        - **[接続]** - 別のコンピューターに接続します。 このオプションはリモート コントロール セッションがアクティブな間は使用できません。  
        -   **[切断]** - アクティブリモート制御セッションを切断しますが、 **[Configuration Manager リモート コントロール]** ウィンドウは閉じません。  
        - **[終了]** - アクティブなリモート制御セッションを切断し、 **[Configuration Manager リモート コントロール]** ウィンドウを閉じます。  

        > [!NOTE]  
        >  リモート コントロール セッションを切断すると、見ているコンピューターの Windows クリップボードのコンテンツは削除されます。


    - **[表示]**
      - **[色の深度]** - ピクセルあたり 16 ビットまたは 32 ビットを選択します。
      -  **[全画面]** - **[Configuration Manager リモート コントロール]** ウィンドウを最大化します。 全画面表示モードを終了するには、Ctrl+Alt+Break を押します。  
      - **[低帯域幅の接続の最適化]** - 接続が低帯域幅の場合は、このオプションを選択します。
      - **[Display:]\(表示:\)**
        - **[全スクリーン]** - Configuration Manager 1902 で追加されました。 接続するコンピューターに複数のモニターがある場合は、すべてのモニターの表示画面がリモート コントロール ウィンドウに表示されます。 **[全スクリーン]** は、1902 より前のマルチ モニタ対応コンピューターに唯一のビューです。
        -  **[最初の画面]** - Configuration Manager 1902 で追加されました。 Windows のディスプレイ設定に表示されるように、"*最初の画面*" は一番上の左端にあります。 特定の画面を選択することはできません。 ビューアーの構成を切り替えるときは、リモート セッションを再接続してください。 ビューアーに設定が保存され、今後の接続に使用されます。
        -  **[画面に合わせて倍率を変更]** - リモート コンピューターの画面を、 **[Configuration Manager リモート コントロール]** ウィンドウのサイズに合わせて拡大縮小します。
        - **[ステータス バー]** - **[Configuration Manager リモート コントロール]** ウィンドウのステータス バーの表示を切り替えます。  

       > [!NOTE]  
       >  ビューアーに設定が保存され、今後の接続に使用されます。

    -   **操作**
        - **[Ctrl+Alt+Del キーの送信]** - Ctrl+Alt+Del キーの組み合わせをリモート コンピューターに送信します。 
        - **[Enable Clipboard Sharing]\(クリップボードの共有を有効にする\)** - リモート コンピューターとの間で項目のコピーと貼り付けを可能にします。 この値を変えた場合は、その変更を有効にするには、リモート コントロールのセッションを再起動する必要があります   
          - Configuration Manager コンソールでクリップボードを共有できないようにするには、そのコンソールを実行しているコンピューター上で、レジストリ キー **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** の値を **0** に設定します。
        - **[キーボード変換を有効にする]** - コンソールを実行中のコンピューターのキーボード レイアウトを、接続されているデバイスのレイアウトに変換します。
        - **[リモートのキーボードとマウスのロック]** - リモート キーボードとマウスをロックして、ユーザーがリモート コンピューターを操作するのを防ぎます。  

    -   **[ヘルプ]**
        - **[バージョン情報]** - ビューアーの現在のバージョンが表示されます。  

5.  リモート コンピューターのユーザーは、Configuration Manager の **[リモート コントロール]** アイコンをクリックすると、リモート コントロール セッションについて、詳細な情報を表示できます。 このアイコンは、Windows 通知領域内、またはリモート制御セッション バー上に表示されます。  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Windows のコマンド ラインから、リモート コントロール ビューアーを起動するには  

-   Windows のコマンド プロンプトで、「 _<Configuration Manager のインストール フォルダー\>_ **\AdminConsole\Bin\i386\CmRcViewer.exe**」と入力します  

CmRcViewer.exe は次のコマンドライン オプションをサポートします。  

- *アドレス* - 接続先クライアント コンピューターの NetBIOS 名、完全修飾ドメイン名 (FQDN)、または IP アドレスを指定します。
- *サイト サーバー名* - リモート制御セッションに関連するステータス メッセージの送信先の Configuration Manager サイト サーバーの名前を指定します。
- **/?** - リモート コントロール ビューアーのコマンド ライン オプションを表示します。  
     
**例: CmRcViewer.exe** *<Address\>* *<\\\Site Server Name>* 

> [!NOTE]  
> リモート コントロール ビューアーは、Configuration Manager コンソールでサポートされるすべてのオペレーティング システムでサポートされています。 詳細については、[Configuration Manager コンソールのサポートされる構成](../../../plan-design/configs/supported-operating-systems-consoles.md)と[リモート コントロールの前提条件](prerequisites-for-remote-control.md)に関する記事を参照してください。

## <a name="next-steps"></a>次のステップ

[リモート コントロール使用状況の監査](audit-remote-control-usage.md)
