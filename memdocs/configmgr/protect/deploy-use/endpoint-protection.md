---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: クライアントのマルウェア対策ポリシーと Windows ファイアウォールのセキュリティを管理する方法について説明します。
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b74a8c1daff31a8ffca8a38e6449aeeef1bb9b2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697180"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*適用対象:Configuration Manager (Current Branch)*

Endpoint Protection では、Configuration Manager 階層内のクライアント コンピューターのマルウェア対策ポリシーと Windows ファイアウォールのセキュリティを管理します。  

> [!IMPORTANT]  
>  Configuration Manager 階層内のクライアントの管理に Endpoint Protection を使用するにはライセンスが必要です。  

 Configuration Manager で Endpoint Protection を使用すると、次のようなメリットがあります。  

-   マルウェア対策ポリシーと Windows ファイアウォールの設定を構成し、選択したコンピューターのグループに対する Microsoft Defender Advanced Threat Protection を管理します  
-   Configuration Manager ソフトウェア更新プログラムを使用して最新のマルウェア対策の定義ファイルをダウンロードし、クライアント コンピューターを最新の状態に保ちます。  
-   メール通知を送信し、コンソール内の監視機能を使用して、レポートを表示します。 これらのアクションを行うことで、クライアント コンピューターでマルウェアが検出された場合に管理ユーザーに通知します。  

Windows 10 と Windows Server 2016 以降のコンピューターには、Windows Defender があらかじめインストールされています。 これらのオペレーティング システムの場合、Windows Defender の管理クライアントは、Configuration Manager クライアントと共にインストールされます。 Windows 8.1 以前のコンピューターでは、Endpoint Protection をインストールすると、Configuration Manager クライアントがインストールされます。 Windows Defender と Endpoint Protection クライアントは、次の機能を備えています。  

-   マルウェアとスパイウェアの検出と修復  
-   ルートキットの検出と修復  
-   重大な脆弱性の評価、および定義とエンジンの自動更新  
-   ネットワーク検査システム経由のネットワークの脆弱性の検出  
-   Cloud Protection Service との統合によりマルウェアを Microsoft に報告。 このサービスに加入すると、コンピューターで不明なマルウェアが検出された場合に、Endpoint Protection クライアントまたは Windows Defender がマルウェア プロテクション センターから最新の定義をダウンロードします。  

> [!NOTE]  
>  Endpoint Protection クライアントは、Hyper-V を実行しているサーバーと、サポートされているオペレーティング システムを搭載したゲスト仮想マシンにインストールできます。 CPU の過剰使用を避けるため、Endpoint Protection のアクションには複数の保護サービスが同時に実行されないように遅延をランダムに発生させる機能が組み込まれています。  

 さらに、Configuration Manager コンソールで Endpoint Protection を使用して、Windows ファイアウォールの設定を管理します。  

 [シナリオ例: System Center Endpoint Protection を使用してマルウェアからコンピューターを保護する](scenarios-endpoint-protection.md) Endpoint Protection および Windows ファイアウォール。  


## <a name="managing-malware-with-endpoint-protection"></a>Endpoint Protection によるマルウェアの管理  
 Configuration Manager の Endpoint Protection を使用すれば、Endpoint Protection クライアント構成用の設定を含むマルウェア対策ポリシーを作成することができます。 これらのマルウェア対策ポリシーをクライアント コンピューターに展開します。 その後、 **[監視]** ワークスペースの **[セキュリティ]** の **[Endpoint Protection のステータス]** ノードでコンプライアンスを監視します。 **[レポート]** ノードの Endpoint Protection レポートも使用します。  

 追加情報:  

-   [Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md) - 構成可能な設定の一覧を使用してマルウェア対策ポリシーを作成、展開、監視します。  

-   [Endpoint Protection を監視する方法](monitor-endpoint-protection.md) - アクティビティ レポート、感染したクライアント コンピューターなどを監視します。  

-   [Endpoint Protection のためのマルウェア対策ポリシーとファイアウォール設定の管理方法](endpoint-antimalware-firewall.md) - クライアント コンピューター上で検出されたマルウェアを修復します  

-   [Endpoint Protection のログ ファイル](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Endpoint Protection による Windows ファイアウォールの管理  
 Configuration Manager の Endpoint Protection には、クライアント コンピューター上の Windows ファイアウォールの基本管理機能が備わっています。 各ネットワーク プロファイルごとに、次の設定を構成できます。  

-   Windows ファイアウォールを有効または無効にする。  

-   許可されたプログラムの一覧にあるプログラムも含め、着信接続をブロックする。  

-   Windows ファイアウォールが新しいプログラムをブロックしたときにユーザーに通知する。  

> [!NOTE]  
>  Endpoint Protection は Windows ファイアウォールの管理のみをサポートします。  


 詳細については、[Endpoint Protection 用 Windows ファイアウォール ポリシーの作成および展開方法](create-windows-firewall-policies.md)に関するページを参照してください。  


## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection を使用すると、Microsoft Defender Advanced Threat Protection (ATP) (旧称 Windows Defender ATP) を管理および監視することができます。 Microsoft Defender ATP サービスは、企業が企業ネットワークに対する高度な攻撃を検出して調査し、対応するのに役立ちます。 詳細については、「[Microsoft Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md)」をご覧ください。

## <a name="endpoint-protection-workflow"></a>Endpoint Protection のワークフロー  
 次の図を使用して、Endpoint Protection を Configuration Manager 階層に実装するワークフローの理解に役立ててください。  

 ![Endpoint Protection のワークフロー](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Mac コンピューターと Linux サーバー用の Endpoint Protection クライアント  

> [!Important]  
> Mac と Linux (すべてのバージョン) の System Center Endpoint Protection (SCEP) のサポートは 2018 年 12 月 31 日で終了します。 Mac 用の SCEP および Linux 用の SCEP の新しいウイルスの定義の可用性は、サポートの終了後に停止される可能性があります。 詳しくは、[サポートの終了ブログ投稿](https://go.microsoft.com/fwlink/?linkid=870182)をご覧ください。  

 System Center Endpoint Protection には、Linux コンピューターと Mac コンピューター用の Endpoint Protection クライアントが付属しています。 これらのクライアントは、Configuration Manager には付属していません。 [Microsoft ボリューム ライセンス サービス センター](https://www.microsoft.com/licensing/servicecenter/default.aspx)から次の製品をダウンロードする必要があります。  

-   System Center Endpoint Protection for Mac  

-   System Center Endpoint Protection for Linux  


> [!Note]  
>  Mac 用と Linux 用の Endpoint Protection インストール ファイルをダウンロードするには、Microsoft ボリューム ライセンスを購入する必要があります。  

 これらの製品は、Configuration Manager のコンソールから管理することができません。 System Center Operations Manager 管理パックがインストール ファイルに付属しているため、Linux 用のクライアントを管理することができます。  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Mac コンピューターと Linux サーバー用の Endpoint Protection クライアントを取得する方法

次の手順で、Mac コンピューターと Linux サーバー用の Endpoint Protection クライアント ソフトウェアとドキュメントを含む画像ファイルをダウンロードします。
1. [Microsoft ボリューム ランセンス サービス センター](https://www.microsoft.com/licensing/servicecenter/default.aspx)にサインインします。
2. Web サイトの上部にある **[Downloads and Keys]** (ダウンロードとキー) タブを選択します。
3. 製品 **System Center Endpoint Protection (Current Branch)** でフィルター処理します。
4. **[ダウンロード]** リンクをクリックします。
5. **[続行]** をクリックします。 いくつかのファイル (**System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage 32/64 bit 1878 MB ISO** など) が表示されるはずです。
6. ファイルをダウンロードするには、矢印アイコンをクリックします。 ファイル名は **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO** です。

2018 年 1 月の更新 (X21-67050) には、次のバージョンが含まれます。

- System Center Endpoint Protection for Mac 4.5.32.0 (macOS 10.13 High Sierra のサポート)
- System Center Endpoint Protection for Linux 4.5.20.0 

  Linux コンピューターと Mac コンピューター用の Endpoint Protection クライアントをインストールして管理する方法の詳細については、これらの製品に付属のドキュメントを参照してください。 この製品ドキュメントは、.ISO ファイルの **Documentation** フォルダーにあります。
