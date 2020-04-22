---
title: VDI クライアントを管理する
titleSuffix: Configuration Manager
description: 仮想デスクトップ インフラストラクチャ (VDI) で Configuration Manager クライアントを管理します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01348695ac5b3b64ca87a9b42aa52ac235b533d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693860"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>仮想デスクトップ インフラストラクチャ (VDI) で Configuration Manager クライアントを管理します

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、次の仮想デスクトップ インフラストラクチャ (VDI) シナリオでの Configuration Manager クライアントのインストールがサポートされています。  

- **パーソナル仮想マシン** - パーソナル仮想マシンは、一般的に、セッション間でユーザーのデータと設定を仮想マシンに保持する場合に使用します。  

- **リモート デスクトップ サービス セッション** - リモート デスクトップ サービスを使用して、1 つのサーバーで複数の同時クライアント セッションをホストできます。 ユーザーはセッションに接続し、そのサーバーでアプリケーションを実行できます。  

- **プール仮想マシン** - プール仮想マシンはセッション間で保持されません。 セッションを閉じると、すべてのデータと設定が破棄されます。 プール仮想マシンは、クライアント セッションをホストする Windows Server で必要なビジネス アプリケーションを実行できないことが原因で、リモート デスクトップ サービスを使用できない場合に有用です。  

  仮想デスクトップ インフラストラクチャで Configuration Manager クライアントを管理する場合の考慮事項の一覧を次の表に示します。  

|仮想マシンの種類|考慮事項|  
|--------------------------|--------------------|  
|パーソナル仮想マシン|Configuration Manager ではパーソナル仮想マシンを物理コンピューターと同じものとして扱います。 Configuration Manager クライアントは、仮想マシン イメージに事前インストールするか、仮想マシンの事前準備の後に展開できます。|  
|リモート デスクトップ サービス|Configuration Manager クライアントは、個別のリモート デスクトップ セッション用にインストールされません。 クライアントは、リモート デスクトップ サービス サーバーに一度だけインストールされます。 リモート デスクトップ サービス サーバーではすべての Configuration Manager 機能を使用できます。|  
|プール仮想マシン|プール仮想マシンを使用停止すると、Configuration Manager を使用して行った変更はすべて失われます。<br /><br /> 仮想マシンは短時間のみ運用されることがあるため、ハードウェア インベントリ、ソフトウェア インベントリ、ソフトウェア メータリングなどの Configuration Manager 機能から返されるデータはニーズと関係がない可能性があります。 インベントリ タスクからプール仮想マシンを除外することを考慮してください。|  

 仮想化では、同一の物理コンピューターでの複数の Configuration Manager クライアントの実行がサポートされるため、多くのクライアント操作には、ハードウェアおよびソフトウェア インベントリ、マルウェア対策スキャン、ソフトウェアのインストール、ソフトウェア更新プログラムのスキャンなどのスケジュールされた操作で、組み込みのランダム待機時間があります。 この待機時間に、Configuration Manager クライアントを実行する複数の仮想マシンを持つコンピューターの CPU 処理とデータ転送を分散することができます。  

> [!NOTE]  
>  保守モードの Windows Embedded クライアントを除き、仮想化環境で実行されていない Configuration Manager クライアントも、このランダム待機時間を使用します。 多くのクライアントが展開されている場合、この動作によって、ネットワーク帯域幅のピークを回避し、管理ポイントやサイト サーバーなどの Configuration Manager サイト システムの CPU 処理要件を減らすことができます。 待機時間の間隔は、Configuration Manager の機能によって変わります。  
>   
>  必要なソフトウェア更新プログラムのランダム待機時間を既定で無効にするには、"**コンピューター エージェント**: **期限のランダム化を無効にする**" というクライアント設定を使用します。
