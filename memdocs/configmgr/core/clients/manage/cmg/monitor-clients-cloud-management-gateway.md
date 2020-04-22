---
title: クラウド管理ゲートウェイを監視する
titleSuffix: Configuration Manager
description: クラウド管理ゲートウェイ (CMG) 経由でクライアントおよびネットワーク トラフィックを監視します。
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695150"
---
# <a name="monitor-cloud-management-gateway"></a>クラウド管理ゲートウェイを監視する

*適用対象:Configuration Manager (Current Branch)*

クラウド管理ゲートウェイ (CMG) を実行中で、そのゲートウェイ経由でクライアントが接続されている場合、クライアントおよびネットワーク トラフィックを監視して、サービスのパフォーマンスを把握することができます。


## <a name="monitor-clients"></a>クライアントの監視

CMG 経由で接続されているクライアントは、オンプレミス クライアントと同様に、Configuration Manager コンソールに表示されます。 詳細については、「[System Center Configuration Manager でクライアントを監視する方法](../monitor-clients.md)」を参照してください。


## <a name="monitor-traffic-in-the-console"></a>コンソールでトラフィックを監視する

Configuration Manager コンソールを使用して、CMG のトラフィックを監視する場合は、次の操作を行います。

1. **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[クラウド管理ゲートウェイ]** ノードを選択します。  

2. リスト ウィンドウで CMG を選択します。  

3. 詳細ウィンドウで、CMG 接続ポイントと接続しているサイト システムの役割のトラフィック情報を確認します。 これらの統計情報は、これらの役割に送信されるクライアント要求を示しています。 この要求には、ポリシー、場所、登録、コンテンツ、インベントリ、およびクライアントの通知が含まれます。<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>送信トラフィック アラートの設定

送信トラフィック アラートを使用すると、ネットワーク トラフィックが 14 日のしきい値レベルに達したときに知ることができます。 CMG を作成するときに、トラフィック アラートを設定できます。 この部分をスキップして、サービスの実行後にアラートを設定することもできます。 アラート設定はいつでも調整できます。

1. **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[クラウド管理ゲートウェイ]** ノードを選択します。  

2. リスト ウィンドウで CMG を選択してから、リボンで **[プロパティ]** を選択します。  

3. **[アラート]** タブに移動して、しきい値とアラートを有効にします。 14 日のデータしきい値をギガバイト (GB) 単位で指定します。 また、別のアラート レベルを上げるためにしきい値の割合を指定します。  

4. 完了したら、 **[OK]** を選択します。  


## <a name="monitor-logs"></a>監視ログ

CMG によって、多くのログ ファイルにエントリが生成されます。 詳細については、「[System Center Configuration Manager のログ ファイル](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)」を参照してください。


## <a name="cloud-management-dashboard"></a>クラウド管理ダッシュボード

<!--1358461-->
バージョン 1806 以降では、クラウド管理ダッシュボードでは、CMG の使用量を一元化したビューが提供されます。 クラウド管理のためにサイトが [Azure サービス](../../../servers/deploy/configure/azure-services-wizard.md)にオンボードされている場合、クラウド ユーザーおよびデバイスに関するデータも表示されます。  

次のスクリーンショットは、利用可能な 2 つのタイルを表示したクラウド管理ダッシュ ボードの一部です。  
![クラウド管理ダッシュボード タイルの CMG トラフィックと現在のオンライン クライアント](media/1358461-cmg-dashboard.png)

Configuration Manager コンソールで、 **[監視]** ワークスペースに移動します。 **[クラウド管理]** ノードを選択して、ダッシュボード タイルを表示します。  


## <a name="connection-analyzer"></a>接続アナライザー

バージョン 1806 以降では、トラブルシューティングを支援するリアルタイム検証のために CMG 接続アナライザーを使用します。 コンソール内ユーティリティは、サービスの状態と、CMG 接続ポイント経由で CMG トラフィックを許可する任意の管理ポイントへの通信チャネルをチェックします。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[クラウド サービス]** を展開し、 **[クラウド管理ゲートウェイ]** ノードを選択します。  

2. 対象となる CMG インスタンスを選択して、リボンにある **[接続アナライザー]** を選択します。  

3. [CMG connection analyzer]\(CMG 接続アナライザー\) ウィンドウで、サービスを認証するための次のいずれかのオプションを選択します。  

     1. **Azure AD のユーザー**: このオプションを使用して、Azure AD に参加している Windows 10 デバイスにサインイン済みのクラウド ベースのユーザー ID と同じ通信をシミュレートします。 **[サインイン]** をクリックして、この Azure AD ユーザー アカウントのための資格情報を安全に入力します。  

     2. **クライアント証明書**: このオプションを使用して、[クライアント認証証明書](certificates-for-cloud-management-gateway.md#bkmk_clientauth)を使用した Configuration Manager クライアントと同じ通信をシミュレートします。  

4. **[開始]** を選択して、分析を開始します。 アナライザー ウィンドウに結果が表示されます。 エントリを選択すると、[説明] フィールドにさらに詳しい詳細が表示されます。  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a> しきい値を超えたときに CMG を停止する

<!--3735092-->
バージョン 1902 以降、Configuration Manager では、データ転送の合計が制限を超えたときに、CMG サービスを停止できるようになりました。 使用量が警告レベルまたは重大レベルに達したときに通知をトリガーするには、[アラート](#set-up-outbound-traffic-alerts)を使用します。 使用量の急増による予期しない Azure コストを削減するには、このオプションでクラウド サービスを無効にします。

> [!Important]  
> サービスが実行されていない場合でも、まだクラウド サービスに関連付けられているコストはあります。 サービスを停止しても、関連付けられているすべての Azure コストが削減されるわけではありません。 クラウド サービスのすべてのコストを削除するには、[CMG を削除](setup-cloud-management-gateway.md#modify-a-cmg)します。  
>
> CMG サービスが停止している場合、インターネット ベースのクライアントは Configuration Manager と通信できません。  

データ転送 (エグレス) の合計には、クラウド サービスとストレージ アカウントからのデータが含まれています。 このデータは次のフローから取得されます。

- CMG からクライアント  
- CMG からサイト (CMG ログ ファイルを含む)  
- コンテンツに対して CMG を有効にした場合は、ストレージ アカウントからクライアント  

これらのデータ フローの詳細については、[CMG のポートとデータ フロー](plan-cloud-management-gateway.md#ports-and-data-flow)に関するページを参照してください。

ストレージ アラートのしきい値は別です。 そのアラートでは、Azure ストレージ インスタンスの容量が監視されます。

コンソールの **[クラウド管理ゲートウェイ]** ノードで CMG インスタンスを選択した場合は、詳細ウィンドウでデータ転送の合計を確認できます。

Configuration Manager では、6 分ごとにしきい値が確認されます。 使用量が急増した場合、Configuration Manager では、しきい値が超過したことを検出し、サービスを停止するまで最大 6 分かかることがあります。

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>しきい値を超えたときにクラウド サービスを停止するプロセス

1. [アウトバウンド トラフィック アラートを設定します](#set-up-outbound-traffic-alerts)。  

2. CMG のプロパティ ウィンドウの **[アラート]** タブで、 **[重大なアラートのしきい値を超えたらこのサービスを停止する]** オプションを有効にします。  

この機能をテストするには、次の値のいずれかを一時的に減らします。  

- **送信データ転送の 14 日間のしきい値 (GB)** 。 既定値は `10000` です。  

- **重大なアラートを発生させるしきい値の割合**。 既定値は `90` です。  
