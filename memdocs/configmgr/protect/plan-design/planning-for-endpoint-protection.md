---
title: Endpoint Protection の計画
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
description: マルウェア対策ポリシーと Windows ファイアウォールのセキュリティを計画します
ms.openlocfilehash: 2e3904b7b7232e92fd4a246d2e0519ef32fb67f6
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606835"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager の Endpoint Protection の計画

*適用対象:Configuration Manager (Current Branch)*


Configuration Manager の Endpoint Protection を使用して、Configuration Manager 階層内のクライアント コンピューターのマルウェア対策ポリシーと Windows ファイアウォールのセキュリティを管理できます。  

> [!IMPORTANT]  
>  Configuration Manager 階層内のクライアントの管理に Endpoint Protection を使用するにはライセンスが必要です。  

Configuration Manager で Endpoint Protection を使用すると、次のようなメリットがあります。  

-   マルウェア対策ポリシーと Windows ファイアウォールの設定を構成し、選択したコンピューターのグループに対する Microsoft Defender Advanced Threat Protection を管理します  

-   Configuration Manager ソフトウェア更新プログラムを使用して最新のマルウェア対策の定義ファイルをダウンロードし、クライアント コンピューターを最新の状態に保ちます。  

-   クライアント コンピューターでマルウェアが検出された場合は、電子メールによる通知送信、コンソール内の監視機能の使用、およびレポートの表示を行うことで管理ユーザーに通知することができます。  

Windows 10 コンピューターでは、Endpoint Protection 管理のために追加のクライアントは不要です。 Windows 8.1 およびそれ以前のコンピューターでは、Endpoint Protection により、構成マネージャー クライアントに加え、独自のクライアントもインストールされます。 Endpoint Protection クライアントには、次の機能があります。  

-   マルウェアとスパイウェアの検出と修復  

-   ルートキットの検出と修復  

-   重大な脆弱性の評価、および定義とエンジンの自動更新  

-   ネットワーク検査システム経由のネットワークの脆弱性の検出  

-   Cloud Protection Service との統合によりマルウェアを Microsoft に報告。 このサービスに加入すると、コンピューターで不明なマルウェアが検出された場合に、Endpoint Protection クライアントまたは Windows Defender がマルウェア プロテクション センターから最新の定義をダウンロードできます。  

> [!NOTE]  
>  Endpoint Protection クライアントは、Hyper-V を実行しているサーバーと、サポートされているオペレーティング システムを搭載したゲスト仮想マシンにインストールできます。 CPU の過剰使用を避けるため、Endpoint Protection のアクションには複数の保護サービスが同時に実行されないように遅延をランダムに発生させる機能が組み込まれています。  

  さらに、Configuration Manager の Endpoint Protection を使用すると、Configuration Manager コンソールで Windows ファイアウォールの設定を管理することができます。  

 [シナリオ例: System Center Endpoint Protection を使用してマルウェアからコンピューターを保護する](../deploy-use/scenarios-endpoint-protection.md)」は、Endpoint Protection および Windows ファイアウォールを構成および管理する方法を示しています。  

## <a name="managing-malware-with-endpoint-protection"></a>Endpoint Protection によるマルウェアの管理  

Configuration Manager の Endpoint Protection を使用すれば、Endpoint Protection クライアント構成用の設定を含むマルウェア対策ポリシーを作成することができます。 その後、このマルウェア対策ポリシーをクライアント コンピューターに展開し、**[監視]** ワークスペースの **[Endpoint Protection のステータス]** ノードで監視するか、Configuration Manager レポートを使って監視できます。  

 追加情報:  

-   [Endpoint Protection 用のマルウェア対策ポリシーの作成および展開](../deploy-use/endpoint-antimalware-policies.md) - 構成可能な設定の一覧を使用してマルウェア対策ポリシーを作成、展開、監視します。  

-   [Endpoint Protection の監視](../deploy-use/monitor-endpoint-protection.md) - アクティビティ レポート、感染したクライアント コンピューターなどを監視します。   

-   [Endpoint Protection のためのマルウェア対策ポリシーとファイアウォール設定の管理](../deploy-use/endpoint-antimalware-firewall.md) - [マルウェア対策](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies)または[ファイアウォール](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies)のポリシーの優先順位の変更、[クライアント コンピューターで検出されたマルウェアの修復](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware)、その他のタスクを実行できます。

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Endpoint Protection による Windows ファイアウォールの管理  
 Configuration Manager の Endpoint Protection には、クライアント コンピューター上の Windows ファイアウォールの基本管理機能が備わっています。 各ネットワーク プロファイルごとに、次の設定を構成できます。  

-   Windows ファイアウォールを有効または無効にする。  

-   許可されたプログラムの一覧にあるプログラムも含め、着信接続をブロックする。  

-   Windows ファイアウォールが新しいプログラムをブロックしたときにユーザーに通知する。  

> [!NOTE]  
>  Endpoint Protection は Windows ファイアウォールの管理のみをサポートします。  

  Endpoint Protection 用の Windows ファイアウォール ポリシーを作成および展開する方法の詳細については、「[Endpoint Protection 用 Windows ファイアウォール ポリシーを作成および展開する方法](../deploy-use/create-windows-firewall-policies.md)」をご覧ください。  

## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Configuration Manager のバージョン 1606 (Current Branch) 以降では、Endpoint Protection を使用して、Microsoft Defender Advanced Threat Protection (ATP) (旧称 Windows Defender ATP) を管理および監視できるようになりました。 Microsoft Defender ATP は、企業が自社のネットワークに対する高度な攻撃を検出して調査し、対応するのに役立つサービスです。 「[Microsoft Defender Advanced Threat Protection](../deploy-use/defender-advanced-threat-protection.md)」を参照してください。

## <a name="endpoint-protection-workflow"></a>Endpoint Protection のワークフロー  
 次の図を使用して、Endpoint Protection を Configuration Manager 階層に実装するワークフローの理解に役立ててください。  

 ![Endpoint Protection のワークフロー](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Mac コンピューターと Linux サーバー用の Endpoint Protection クライアント  
 System Center には、Linux コンピューターと Mac コンピューター用の Endpoint Protection クライアントが付属しています。 Configuration Manager にはこれらのクライアントが付属していないため、[Microsoft ボリューム ライセンス サービス センター](https://www.microsoft.com/licensing/servicecenter/default.aspx)から次の製品をダウンロードする必要があります。  

> [!IMPORTANT]  
>  Mac 用と Linux 用の Endpoint Protection インストール ファイルをダウンロードするには、Microsoft ボリューム ライセンスを購入する必要があります。  

 これらの製品は、Configuration Manager コンソールから管理することができません。 ただし、System Center Operations Manager 管理パックがインストール ファイルに付属しているため、Operations Manager を使用して Linux 用のクライアントを管理することができます。  

 Linux コンピューターと Mac コンピューター用の Endpoint Protection クライアントをインストールして管理する方法については、 **Documentation** フォルダーに配置されたこれらの製品に付属のマニュアルを参照してください。

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager の Endpoint Protection の推奨する運用方法  
 System Center 2012 Configuration Manager の Endpoint Protection に関する次のベスト プラクティスを使用してください。  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Endpoint Protection のカスタム クライアント設定を構成する  
 Endpoint Protection のクライアント設定を構成する場合、既定のクライアント設定は、階層内のすべてのコンピューターに設定が適用されてしまうため、使用しないでください。 その代わり、カスタム クライアント設定を構成して、階層内のコンピューターのコレクションに割り当てます。  

 カスタム クライアント設定を構成するときには、次の項目を実行できます。  

-   組織内のさまざまな部分に応じてマルウェア対策とセキュリティ設定をカスタマイズする。  
-   階層全体に展開する前に、コンピューターの小さなグループで Endpoint Protection を実行して、効果をテストする。  
-   時間をかけて、さらに多くのクライアントをコレクションに追加して、Endpoint Protection クライアントを段階的に展開する。  

### <a name="distributing-definition-updates-by-using-software-updates"></a>ソフトウェア更新プログラムを使用した定義ファイルの更新の配布  
 Configuration Manager のソフトウェア更新プログラムを使用して定義ファイルの更新を配布する場合は、他のソフトウェア更新プログラムを含まないパッケージに定義ファイルの更新を配置することを検討します。 これによって、定義ファイルの更新パッケージのサイズが小さくなり、配布ポイントへより短時間でレプリケートすることができます。
