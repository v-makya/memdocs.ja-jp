---
title: 正常性構成証明書
titleSuffix: Configuration Manager
description: Configuration Manager コンソールに表示できるデバイス正常性構成証明書の機能について説明します。
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d57be201274c347e5dcd492734b2141c64d579b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700012"
---
# <a name="health-attestation-for-configuration-manager"></a>Configuration Manager の正常性構成証明書

*適用対象:Configuration Manager (Current Branch)*

管理者は Configuration Manager コンソールで [Windows 10 デバイス正常性構成証明](/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices)の状態を確認できます。  デバイスの正常性構成証明で、管理者はクライアント コンピューターで次の信頼できる BIOS、TPM、およびブート ソフトウェアの構成が有効になっていることを確認できます。  

-   起動時マルウェア対策 - 起動時マルウェア対策 (ELAM) により、サードパーティのドライバーが初期化される前の起動時にコンピューターが保護されます。 [ELAM を有効にする方法](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - Windows BitLocker ドライブ暗号化は、Windows オペレーティング システムのボリュームに格納されているすべてのデータを暗号化できるソフトウェアです。  [BitLocker を有効にする方法](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   セキュア ブート - セキュア ブートは、PC 業界のメンバーによって開発されたセキュリティ標準で、PC の製造元によって信頼されているソフトウェアのみを使用して PC が起動されるようにするのに役立ちます。 [セキュア ブートの詳細](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824987(v=win.10))  
-   コードの整合性 - コードの整合性は、メモリに読み込まれるたびに、ドライバーまたはシステム ファイルの整合性を検証することによって、オペレーティング システムのセキュリティを強化する機能です。 [コードの整合性の詳細](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348642(v=ws.10))  

この機能は、Configuration Manager によって管理されている PC と内部設置型リソース、および Microsoft Intune で管理されているモバイル デバイスで利用できます。 管理者は、報告がクラウドを使用して行われるか、内部設置型インフラストラクチャを使用して行われるかを指定できます。 オンプレミスのデバイス正常性構成証明書の監視により、インターネット アクセスがなくても管理者がクライアント PC を監視することができます。

## <a name="enable-health-attestation"></a>正常性構成証明書を有効にする

 **要件:**  

-   [デバイス正常性構成証明書が有効になっている](/windows-server/security/device-health-attestation)、Windows 10 バージョン 1607 または Windows Server 2016 バージョン 1607 を実行しているクライアント デバイス。
-   TPM 1.2 または TPM 2 が有効になっているデバイス。
-   クラウド管理を使用する場合は、Configuration Manager クライアント エージェントと、*has.spserv.microsoft.com* (ポート 443) 正常性構成証明書サービス (クラウド管理) の管理ポイントとの間の通信。 オンプレミスのときは、クライアントはデバイス正常性構成証明書が有効になっている管理ポイントと通信できる必要があります。

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Configuration Manager クライアント コンピューターの正常性構成証明書サービスの通信を有効にする方法

次の手順を使用して、インターネットに接続するデバイスのデバイス正常性構成証明書の監視を有効にします。

1.  Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クライアント設定]** を選択します。  **[コンピューター エージェント]** 設定のタブを選択します。  
2.  **[既定の設定]** ダイアログ ボックスで、 **[コンピューター エージェント]** を選択して、 **[正常性構成証明書サービスとの通信を有効にする]** まで下にスクロールします。  
3.  **[正常性構成証明書サービスとの通信を有効にする]** を **[はい]** に設定し、 **[OK]** をクリックします。  
4. デバイスの正常性を報告するデバイスのコレクションのターゲットを設定します。

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Configuration Manager クライアント コンピューターの内部設置型正常性構成証明書サービスの通信を有効にする方法
次の手順を使用して、インターネットに接続しない、オンプレミスのデバイスのデバイス正常性構成証明書の監視を有効にします。

Configuration Manager 1702 から、インターネット アクセスのないクライアント デバイスをサポートするために、管理ポイントにオンプレミスのデバイス正常性構成証明書のサービス URL を構成できるようになりました。

1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[サイト構成]**  >  **[サイト]** の順に移動します。
2. オンプレミスのデバイス正常性構成証明書クライアントをサポートしている管理ポイントを含むプライマリまたはセカンダリ サイトを右クリックして、 **[サイト コンポーネントの構成]**  >  **[管理ポイント]** を選択します。 **[管理ポイント コンポーネントのプロパティ]** ページが開きます。
3. **[詳細オプション]** タブで **[追加]** を選択し、有効なオンプレミスのデバイス正常性構成証明書のサービス URL を指定します。 複数の URL を追加できます。 オンプレミスの URL が複数指定されると、クライアントはそのすべてを受け取り、どれを使用するかをランダムに選択します。
4.  Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クライアント設定]** を選択します。  **[コンピューター エージェント]** 設定のタブを選択します。  
5.  下にスクロールして **[正常性構成証明書サービスとの通信を有効にする]** を表示し、 **[はい]** に設定します。
7.  **[オンプレミスの正常性構成証明サービスを使用する]** オプションをクリックし、 **[はい]** に設定します。
8. クライアント エージェントの設定でデバイス正常性構成証明書のレポートが有効に設定されている、デバイスの正常性をレポートするデバイスのコレクションのターゲットを設定します。

デバイス正常性構成証明書サービスの URL を**編集**または**削除**することもできます。

> [!NOTE]
> Configuration Manager 1702 にアップグレードする前にデバイス正常性構成証明書を使用した場合は、クライアント エージェント設定で指定されたオンプレミスの URL がアップグレード中に管理ポイントのプロパティに事前に設定されます。 オンプレミスのクライアントはアップグレードされるまで、クライアント エージェント設定で指定された URL を引き続き使用します。 その後、管理ポイントで指定された URL のいずれかに切り替えます。

## <a name="monitor-device-health-attestation"></a>Windows のデバイス正常性構成証明書

1.  デバイス正常性構成証明書ビューを表示するには、Configuration Manager コンソールで **[監視]** ワークスペースに移動し、 **[セキュリティ]** ノードをクリックしてから **[正常性構成証明書]** をクリックします。  
2.  デバイス正常性構成証明書が表示されます。  

Configuration Manager デバイス正常性構成証明書には、次の情報が表示されます。  

-   **正常性構成証明書のステータス** - 対応、非対応、エラー、および不明な状態のデバイスの共有を表示します。  
-   **正常性構成証明書を報告するデバイス** - 正常性構成証明書のステータスを報告するデバイスの割合を示します。  
-   **クライアントの種類別の非対応のデバイス** - 非対応のモバイル デバイスとコンピューターの共有を表示します。  
-   **最も不足している正常性構成証明書の設定** - 正常性構成証明書の設定のないデバイスの数を設定ごとに表示します。