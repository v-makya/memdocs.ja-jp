---
title: プロキシ サーバーのサポート
titleSuffix: Configuration Manager
description: Configuration Manager サイト システム サーバーがプロキシ サーバーを使用する方法について説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5581214dd786bdefd29d0e4d2626de536ad26ace
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701480"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Configuration Manager でのプロキシ サーバーのサポート

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の一部のサイト システム サーバーでは、インターネット接続が必要です。 お使いの環境でプロキシ サーバーを使用するためにインターネット トラフィックが必要になる場合、プロキシを使用するようにこれらのサイト システムの役割を構成します。  

- サイト システム サーバーをホストするコンポーネントは、1 つのプロキシ サーバー構成をサポートします。 そのコンピューター上のすべてのサイト システムの役割が、この同じプロキシ構成を共有します。 異なる役割または役割のインスタンスごとに別々のプロキシ サーバーが必要な場合は、別々のサイト システム サーバーにそれらの役割を配置します。  

- 既にプロキシ サーバー構成が存在するサイト システム サーバーで新しいプロキシ サーバーの設定を構成すると、元の構成が上書きされます。  

- 既定では、プロキシへの接続では、サイト システムの役割をホストするコンピューターの**システム** アカウントが使用されます。  

- コンピューター アカウントが認証できない場合、サイト システム サーバーがユーザーの資格情報を格納してプロキシ サーバーに接続できます。 これらの資格情報は、**サイト システムのプロキシ サーバー アカウント**です。  

## <a name="site-system-roles-that-use-a-proxy"></a>プロキシを使用するサイト システムの役割

次のサイト システムの役割はインターネットに接続し、必要な場合は、プロキシ サーバーを使用できます。  

### <a name="asset-intelligence-synchronization-point"></a>資産インテリジェンス同期ポイント

このサイト システムの役割は、マイクロソフトに接続して、資産インテリジェンス同期ポイントをホストするコンピューターのプロキシ サーバー構成を使用します。  

### <a name="cloud-distribution-point"></a>クラウド配布ポイント

クラウド配布ポイントの役割は Microsoft Azure で実行されます。 このサイト システムの役割はプロキシを使用するように構成しません。 クラウド配布ポイントを管理するプライマリ サイト サーバーでプロキシの構成を設定します。  

この構成では、プライマリ サイト サーバーは次のようになります。  

- Microsoft Azure に接続してクラウド配布ポイントのセットアップと監視およびクラウド配布ポイントへのコンテンツの配布を実行できる必要があります。  

- 既定では、コンピューターの**システム** アカウントを使用して接続を確立します。 必要に応じて、サイト システムのプロキシ サーバー アカウントも使用できます。  

- Windows Web ブラウザー API を使用します。  

### <a name="distribution-point"></a>配布ポイント

<!-- 5856396 -->

バージョン 2002 以降では、Microsoft 接続キャッシュで Configuration Manager 配布ポイントを有効にすると、インターネット アクセスのために、認証されていないプロキシ サーバーを通して通信できます。 詳細については、[Microsoft 接続済みキャッシュ](../hierarchy/microsoft-connected-cache.md)に関するページを参照してください。

### <a name="exchange-server-connector"></a>Exchange Server コネクタ

このサイト システムの役割は Exchange Server に接続します。 Exchange Server コネクタをホストするコンピューターのプロキシ サーバー構成を使用します。  

### <a name="service-connection-point"></a>[サービス接続ポイント]

このサイト システムの役割を Configuration Manager クラウド サービスに接続すると、Configuration Manager のバージョンの更新プログラムをダウンロードできます。 サービス接続ポイントをホストするコンピューターで構成されているプロキシ サーバーを使用します。  

### <a name="software-update-point"></a>ソフトウェアの更新ポイント

このサイト システムの役割は、Microsoft Update に接続するときにプロキシを使用して、修正プログラムをダウンロードし、更新プログラムに関する情報を同期します。 他のすべてのサイト システムの役割と同じように、最初にサイト システムのプロキシ設定を構成します。 次に、ソフトウェアの更新ポイントに固有の次のオプションを構成します。  

- **[ソフトウェア更新プログラムを同期するときにプロキシ サーバーを使用する]**  

- **[自動展開規則を使用してコンテンツをダウンロードするときにプロキシ サーバーを使用する]**  

    > [!NOTE]
    > 使用することはできますが、セカンダリ サイトのソフトウェアの更新ポイントではこの設定は使用されません。  

これらの設定は、ソフトウェアの更新ポイントのプロパティの **[プロキシとアカウントの設定]** タブにあります。  

> [!NOTE]
> 自動展開ルールが実行されているときは、インターネットへの接続およびソフトウェア更新プログラムのダウンロードに、自動展開ルールが作成されたサイトのサイト サーバーの**システム** アカウントが既定で使用されます。 または、サイト システムのプロキシ サーバー アカウントを構成して使用します。 
>
> このアカウントがインターネットにアクセスできない場合、ソフトウェア更新プログラムのダウンロードは失敗します。 次のエントリが **ruleengine.log** に記録されます。  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a> サイト システム サーバー用のプロキシを使用するその他の機能

*(バージョン 2002 で導入)*

Configuration Manager バージョン 2002 以降、以下の機能は、[サービス接続ポイント](#service-connection-point)の役割をホストするサイト システムのプロキシを使用します。 <!--5913817-->

- [Azure Active Directory (Azure AD) ユーザー探索](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Azure AD ユーザー グループの探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [コレクション メンバーシップの結果を Azure Active Directory グループに同期する](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>サイト システム サーバー用にプロキシを構成する  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[サイトの構成]** を展開し、 **[サーバーとサイト システムの役割]** ノードを選択します。  

2. 編集するサイト システム サーバーを選択します。 詳細ウィンドウで、 **[サイト システム]** の役割を右クリックし、 **[プロパティ]** を選択します。  

3. サイト システムのプロパティで、 **[プロキシ]** タブに切り替えます。次のプロキシ設定を構成します。  

    - **[インターネットから情報を同期するときにプロキシ サーバーを使用する]** :サイト システム サーバーがプロキシ サーバーを使用できるようにするには、このオプションを選択します。  

    - **[プロキシ サーバー名]** :お使いの環境でのプロキシ サーバーのホスト名または FQDN を指定します。  

    - **[ポート]** :プロキシ サーバーと通信するネットワーク ポートを指定します。 既定では、ポート **80** が使われます。  

    - **[資格情報を使用してプロキシ サーバーに接続する]** :多くのプロキシ サーバーでは、ユーザーの認証が必要です。 既定では、サイト システム サーバーはそのコンピューター アカウントを使用してプロキシ サーバーに接続します。 必要に応じて、このオプションを有効にし、 **[設定]** をクリックして、 **[既存のアカウント]** を選択するか、 **[新しいアカウント]** を指定します。 これらの資格情報は、**サイト システムのプロキシ サーバー アカウント**です。  詳細については、「[System Center Configuration Manager で使用されるアカウント](../hierarchy/accounts.md)」を参照してください。  

4. **[OK]** をクリックして新しいプロキシ サーバー構成を保存します。  
