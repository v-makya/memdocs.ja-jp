---
title: Technical Preview 1603 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1603 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3a60134e33449f2de181dd2dd39f4783383a889d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705640"
---
# <a name="capabilities-in-technical-preview-1603-for-configuration-manager"></a>Configuration Manager の Technical Preview 1603 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1603 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 代わりに、System Center Technical Preview 5 を使用すると、このバージョンは Configuration Manager Technical Preview の基準バージョンとしてインストールされます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。  

 **この Technical Preview の既知の問題:**  

- このリリースには、以前にリリースされた機能の更新プログラムが含まれていますが、新機能は導入していません。 そのため、以前に 1602 にアップグレードし、1602 に含まれる機能をすべて有効にした場合、更新プログラム ウィザードの [機能] ページは空になります。  

- サイト サーバーが Technical Preview 1603 に更新されたら、クライアントもバージョン 1603 に更新されるまで、リモート制御機能を使用できません。  

  **このバージョンでお試しいただける新機能を次に示します。**  

##  <a name="improvements-to-software-center"></a><a name="BKMK_SC1603"></a> ソフトウェア センターの機能強化  

### <a name="new-tiled-view-for-apps"></a>アプリの新しいタイル化されたビュー  
 エンドユーザーは、ソフトウェア センターの **[アプリケーション]** タブでアプリのリストまたはアプリのタイル化されたビューを選択できるようになりました。  

### <a name="select-multiple-updates-in-software-center"></a>ソフトウェア センターでの複数の更新プログラムの選択  
 ソフトウェア センターの **[更新]** タブで、複数の更新プログラムを選択したり、 **[すべて更新]** を選択したりして、同時に複数の更新プログラムのインストールを開始できるようになりました。  

##  <a name="improvements-to-remote-control"></a><a name="BKMK_RC1603"></a> リモート制御の機能強化  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>リモート制御セッションでの共有クリップボードへのアクセスの制限  
 新しいリモート ツール クライアントの設定 「**Prompt user for shared clipboard file transfer permission**」 (ユーザーに共有クリップボードのファイル転送のアクセス許可を要求する) を有効にして、リモート コントロール セッションで共有クリップボードへのアクセスを制限できます。  

 有効な場合、リモート セッションを共有しているエンドユーザーは、ビューア―が共有クリップボードを使用して、セッションからローカル コンピューターにファイルを転送できるように、そのセッションのビューア―にアクセス許可を与える必要があります。  

 前述のように、これにより、ビューア―にエンドユーザーのコンピューターのフル コントロールが付与された場合、エンドユーザーに完全に透過的な方法で、共有クリップボードを使用してセッションからローカル コンピューターにファイルを転送できるように、エンドユーザーに保護レイヤーが追加されます。  

##  <a name="customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> PXE 対応配布ポイント上の RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズ  
 1603 Technical Preview では、PXE 対応配布ポイントの RamDisk TFTP ブロック サイズとウィンドウ サイズをカスタマイズできます。 ネットワークをカスタマイズしている場合、ブロックまたはウィンドウのサイズが大きすぎるために、ブート イメージのダウンロードがタイムアウト エラーで失敗する可能性があります。 RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズにより、特定のネットワーク要件に対応する PXE を使用する場合に、TFTP トラフィックを最適化できます。   
最も効率的な内容を確認するために、環境内でカスタマイズした設定をテストする必要があります。  

-   **TFTP ブロック サイズ**:ブロック サイズは、ファイルをダウンロードしているクライアントにサーバーによって送信されるデータ パケットのサイズです (RFC 2347 に記載)。 ブロック サイズを大きくすると、サーバーとクライアントの間のラウンド トリップ遅延が少なくなるように、サーバーが送信するパケットを少なくすることができます。 ただし、大きいサイズのブロックにより、ほとんどの PXE クライアントの実装がサポートしていない、断片化されたパケットが生成されます。  

-   **TFTP ウィンドウ サイズ**:TFTP では、送信されるデータの各ブロックの確認 (ACK) パケットが必要です。 前のブロックの ACK パケットを受信するまで、サーバーは、シーケンス内の次のブロックを送信しません。 TFTP ウィンドウは、ウィンドウがいっぱいになるまでのデータ ブロックの数を定義できる、Windows 展開サービスの機能です。 サーバーは、ウィンドウがいっぱいになるまでデータ ブロックを連続で送信し、その後クライアントが ACK パケットを送信します。 このウィンドウのサイズを増やすことで、クライアントとサーバーの間のラウンド トリップ遅延回数が減少し、ブート イメージをダウンロードするために必要な全体の時間が短縮します。  

### <a name="try-it-out"></a>試してみましょう。  
 次のタスクを実行してから、このトピックの先頭付近にあるフィードバック情報を使用してその動作を報告してください。  

-   PXE 対応配布ポイント上の RamDisk TFTP ウィンドウ サイズをカスタマイズできる。  

-   PXE 対応配布ポイント上の RamDisk TFTP ブロック サイズをカスタマイズできる。  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>RamDisk TFTP ウィンドウ サイズを変更するには  

- RamDisk TFTP ウィンドウ サイズをカスタマイズするには、PXE 対応配布ポイント上に次のレジストリ キーを追加します。  

   **[場所]** :HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  名前:RamDiskTFTPWindowSize  

   **種類**:REG_DWORD  

   **値**: &lt;カスタマイズされたウィンドウのサイズ\>  

  既定値は 1 (1 つのデータ ブロックでウィンドウがいっぱいになります)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>RamDisk TFTP ブロック サイズを変更するには  

- RamDisk TFTP ウィンドウ サイズをカスタマイズするには、PXE 対応配布ポイント上に次のレジストリ キーを追加します。  

   **[場所]** :HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  名前:RamDiskTFTPBlockSize  

   **種類**:REG_DWORD  

   **値**: &lt;カスタマイズされたブロック サイズ\>  

  既定値は 4096 (4k) です。  
