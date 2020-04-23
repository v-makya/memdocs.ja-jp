---
title: サイト コンポーネント
titleSuffix: Configuration Manager
description: サイト コンポーネントを構成して、サイト システムの役割とサイト ステータス レポートの動作を変更する方法について説明します。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700930"
---
# <a name="site-components-for-configuration-manager"></a>Configuration Manager のサイト コンポーネント

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager サイトごとにサイト コンポーネントを構成し、サイト システムの役割とサイト ステータス レポートの動作を変更できます。 サイト コンポーネントの構成はサイトと、サイトで適用可能なサイト システムの役割の各インスタンスに適用されます。  

Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。 サイトを選択します。 リボンの **[設定]** グループで、 **[サイト コンポーネントの構成]** を選択します。 次のいずれかのオプションを選択します。

- [ソフトウェアの配布](#software-distribution)  
- [ソフトウェアの更新ポイント](#software-update-point) 
- [オペレーティング システムの展開](#operating-system-deployment)
- [管理ポイント](#management-point)  
- [ステータス レポート](#status-reporting)  
- [電子メール通知](#email-notification)
- [コレクション メンバーシップの評価](#bkmk_colleval)


## <a name="about-site-components"></a>サイト コンポーネントについて  

 さまざまなサイト コンポーネントのオプションのほとんどは、Configuration Manager コンソールに表示すると、ひとめでわかります。 より複雑な構成であれば、以下で紹介する場所で一部の構成の詳細を確認できます。あるいは、追加のコンテンツに移動できます。  

> [!Note]  
> 一部のコンポーネントで利用できるオプションは、中央管理サイト、プライマリ サイト、セカンダリ サイトのどれを選択したかによって変わります。 サイトの種類によっては、一部のコンポーネントをまったく利用できません。  



### <a name="software-distribution"></a>ソフトウェアの配布  

#### <a name="content-distribution-settings"></a>コンテンツ配布設定
**[全般]** タブで、サイト サーバーから配布ポイントへのコンテンツの転送方法を変更する設定を指定します。 同時配布設定に使用する値を増やすと、コンテンツの配布でより多くのネットワーク帯域幅を使用できます。  

#### <a name="pull-distribution-point"></a>プル配布ポイント
詳細については、「[プル配布ポイントの使用](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)」をご覧ください。

#### <a name="network-access-account"></a>ネットワーク アクセス アカウント
詳細については、「[ネットワーク アクセス アカウント](../../../plan-design/hierarchy/accounts.md#network-access-account)」を参照してください。  


### <a name="software-update-point"></a>ソフトウェアの更新ポイント  

詳細については、「[Install a software update point](../../../../sum/get-started/install-a-software-update-point.md)」 (ソフトウェアの更新ポイントのインストール) をご覧ください。  


### <a name="operating-system-deployment"></a>オペレーティング システムの展開

詳細については、「[オフライン OS イメージ サービス用のドライブを指定する](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive)」をご覧ください。


### <a name="management-point"></a>管理ポイント  

**[全般]** タブで、管理ポイントに関する情報を Active Directory Domain Services に発行するようにサイトを設定します。  

Configuration Manager クライアントは、管理ポイントを使用してサービスを特定し、境界グループのメンバーシップや PKI 証明書の選択オプションなどのサイト情報を検索します。 また、クライアントは、サイト内の他の管理ポイントの検索や、ソフトウェアのダウンロード元の配布ポイントの検索にも管理ポイントを使用します。 クライアントは、管理ポイントを使用して、サイト割り当ての実行、クライアント ポリシーのダウンロード、クライアント情報のアップロードも行うことができます。  

クライアントが管理ポイントを見つける最も安全な方法は、Active Directory Domain Services で管理ポイントを公開することです。 このサービスの場所検索方法では、次の条件を満たしている必要があります。

- Configuration Manager のスキーマが拡張されている。
- **System Management** コンテナーがあり、サイト サーバーがこのコンテナーに発行するための適切なセキュリティ アクセス許可が設定されている。
- Configuration Manager サイトが Active Directory Domain Services に発行するように設定されている。
- クライアントが、サイト サーバーと同じ Active Directory フォレストに属している  

イントラネット上のクライアントが管理ポイントの検索に Active Directory Domain Services を使用できない場合は、[DNS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) 発行を使用します。  

サービスの場所の概要については、[クライアントがサイト リソースやサービスを検索する](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)方法に関するページを参照してください。  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>選択したイントラネット管理ポイントを DNS に発行する
イントラネット上のクライアントで Active Directory Domain Services から管理ポイントを見つけられないときにこのオプションを指定します。 代わりに、DNS サービスの場所リソース レコード (SRV RR) を使用して、割り当てられたサイト内の管理ポイントを検索できます。  

Configuration Manager がイントラネットの管理ポイントを DNS に発行するには、次の条件が満たされていなければなりません。  

-   DNS サーバーが、バージョン 8.1.2 以降の BIND を使用している。  

-   DNS サーバーが自動更新用に設定されていて、サービスの場所のリソース レコードをサポートする。  

-   Configuration Manager 内の管理ポイント用に指定された完全修飾ドメイン名 (FQDN) に DNS のホスト エントリ (A または AAA レコード) がある。  

> [!WARNING]  
>  クライアントが DNS で発行された管理ポイントを見つけるには、自動サイト割り当てを使用せずに、クライアントを特定のサイトに割り当てる必要があります。 管理ポイントのドメイン サフィックスを持つサイト コードを使用するには、これらのクライアントを設定します。 詳細については、「[管理ポイントを検出する](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points)」をご覧ください。  

Configuration Manager クライアントがイントラネット上の管理ポイントの検索に Active Directory Domain Services も DNS も使用できない場合は、[WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins) を使用します。 イントラネット上の HTTP クライアント接続を受信するように設定されている場合、サイトで最初にインストールされた管理ポイントが自動的に WINS に発行されます。  


### <a name="status-reporting"></a>ステータス レポート  

これらの設定は、サイトとクライアントからの状態レポートに含まれている詳細のレベルを直接設定します。  


### <a name="email-notification"></a>電子メール通知  

アカウントと電子メール サーバーの詳細を指定して、Configuration Manager を有効にし、アラートとして電子メール通知を送信します。  

詳細については、「[アラートとステータス システムの使用](../../manage/use-alerts-and-the-status-system.md)」を参照してください。


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a> コレクション メンバーシップの評価  

このコンポーネントは、コレクションのメンバーシップの変更箇所を評価する頻度を設定する場合に使用します。 変更箇所の評価は、新しいリソースが追加された場合またはリソースが変更された場合にのみコレクションのメンバーシップを更新します。  

詳細については、[コレクションのベスト プラクティス](../../../clients/manage/collections/best-practices-for-collections.md)に関するページを参照してください。



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Configuration Manager サービス マネージャーによるサイト コンポーネントの管理  

Configuration Manager サービス マネージャーを使用して、Configuration Manager サービスを管理し、Configuration Manager サービスや実行中のスレッドのステータスを確認できます。 これらのサービスとスレッドはまとめて Configuration Manager コンポーネントと呼ばれています。 Configuration Manager コンポーネントについて次のことを理解してください。  

-   コンポーネントは任意のサイト システムで実行できます。  

-   コンポーネントは、Windows のサービスを管理する場合と同じ方法で管理されます。 Configuration Manager コンポーネントの開始、停止、一時停止、再開、または照会を行うことができます。  

Configuration Manager サービスは、このサービスが実行するものが存在するときに実行されます。 これは一般的に、構成ファイルがコンポーネントの受信トレイに書き込まれるときのアクションとなります。 


### <a name="use-the-configuration-manager-service-manager"></a>Configuration Manager サービス マネージャーを使用する  

1.  Configuration Manager コンソールで、 **[監視]** ワークスペースに移動し、 **[システム ステータス]** を展開し、 **[コンポーネントのステータス]** ノードを選択します。  

2.  リボンの **[コンポーネント]** グループで **[起動]** を選択し、 **[Configuration Manager サービス マネージャー]** を選択します。  

3.  Configuration Manager サービス マネージャーが開いたら、管理したいサイトに接続します。  

     管理するサイトが表示されない場合、 **[サイト]** メニューに進み、 **[接続]** を選択します。 次に、正しいサイトのサイト サーバーの名前を入力します。  

4.  サイトを展開して、管理したいコンポーネントのある場所に応じて、 **[コンポーネント]** または **[サーバー]** に移動します。  

5.  右側のウィンドウで、1 つまたは複数のコンポーネントを選択します。 次に、 **[コンポーネント]** メニューの **[クエリ]** を選択し、選択項目の状態を更新します。  

6.  コンポーネントのステータスを更新したら、 **[コンポーネント]** メニューの 4 つのアクション ベースのオプションのいずれかを使用して、コンポーネントの操作を変更します。 アクションを要求したら、コンポーネントを照会して、コンポーネントの新しいステータスを表示する必要があります。  

7.  コンポーネントの操作の状態の変更が完了したら、Configuration Manager サービス マネージャーを閉じます。  
