---
title: リソース アクセス プロファイルの展開
titleSuffix: Configuration Manager
description: Configuration Manager で Wi-Fi、VPN、証明書のプロファイルを展開する方法について学習します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709460"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Configuration Manager にリソース アクセス プロファイルを展開する

*適用対象:Configuration Manager (Current Branch)*

次のいずれかのリソース アクセス プロファイルを作成した後、1 つまたは複数のコレクションに展開します。

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [証明書](create-certificate-profiles.md)

これらのプロファイルを展開するときに、ターゲット コレクションを指定し、クライアントがプロファイルのコンプライアンスを評価する頻度を指定します。  

## <a name="deploy-a-profile"></a>プロファイルを展開する

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動します。 **[コンプライアンス設定]** 、 **[会社リソースのアクセス]** の順に展開し、適切なプロファイル ノードを選択します。 たとえば、 **[Wi-Fi プロファイル]** です。

1. プロファイルの一覧で、展開するプロファイルを選択します。 次に、リボンの **[ホーム]** タブの **[展開]** グループで、 **[展開]** を選択します。  

1. プロファイルの展開ウィンドウで、次の情報を指定します。  

    - **コレクション**:プロファイルを展開するコレクションを選択します。

    - **アラートを生成する**:アラートを構成するには、このオプションを有効にします。 プロファイルのコンプライアンスが、指定された日時までに指定された割合に満たない場合は、サイトによってこのアラートが生成されます。 アラートを System Center Operations Manager に送信するかどうかを選択することもできます。

    - **ランダム遅延 (時間)** : SCEP (Simple Certificate Enrollment Protocol) 設定を含む証明書プロファイルについては、ネットワーク デバイス登録サービス (NDES) で処理量が過度にならないように、遅延期間を指定します。 既定値は、`64` 時間です。  

    - **この...プロファイルのコンプライアンス評価スケジュールを指定します**:クライアントがこのプロファイルのコンプライアンスを評価する頻度を指定します。 **[単純なスケジュール]** を選択するか、 **[カスタム スケジュール]** を構成します。 既定では、単純なスケジュールは `12` 時間ごとになります。

1. **[OK]** を選択してウィンドウを閉じ、展開を作成します。

## <a name="delete-a-deployment"></a>デプロイの削除

展開を削除する場合は、一覧から選択します。 詳細ウィンドウで、 **[展開]** タブに切り替えます。展開を選択し、リボンの **[展開]** タブで **[削除]** を選択します。

> [!IMPORTANT]
> VPN プロファイルの展開を削除しても、Configuration Manager によって Windows からその VPN プロファイルが削除されることはありません。 デバイスからプロファイルを削除する場合、手動で削除します。

## <a name="next-steps"></a>次のステップ

[Wi-Fi プロファイルと VPN プロファイルの監視](monitor-wifi-email-vpn-profiles.md)

[証明書プロファイルの監視](monitor-certificate-profiles.md)
