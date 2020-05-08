---
title: Mac にクライアントを展開する準備
titleSuffix: Configuration Manager
description: Configuration Manager クライアントを Mac コンピューターに展開する前の構成タスク。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2b5bcbce659601e10f44f06af94eb939767a389a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906623"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Mac コンピューターにクライアント ソフトウェアを展開するための準備

*適用対象:Configuration Manager (Current Branch)*

[Configuration Manager クライアントを Mac コンピューターに展開](deploy-clients-to-macs.md)する準備ができていることを確認するには、以下の手順に従ってください。



## <a name="mac-prerequisites"></a>Mac の前提条件

Configuration Manager メディアでは、Mac クライアント インストール パッケージは提供されません。 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=47719)から、**追加のオペレーティング システム用のクライアント**をダウンロードします。  

サポートされるバージョンのリストについては、「[クライアントとデバイスのサポートされるオペレーティング システム](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)」をご覧ください。



## <a name="certificate-requirements"></a>証明書の要件

Mac コンピューターにクライアントをインストールして管理するには、公開キー基盤 (PKI) 証明書が必要です。 PKI 証明書は、相互認証と暗号化データ転送を使用して、Mac コンピューターと Configuration Manager サイト間の通信を保護します。 Configuration Manager では、ユーザー クライアント証明書を要求してインストールできます。 Certificate Services とエンタープライズ証明機関、Configuration Manager 登録ポイントおよび登録プロキシ ポイントを使用します。 Configuration Manager とは独立してコンピューター証明書を要求してインストールすることもできます。 この証明書は、Configuration Manager 証明書の要件を満たしている必要があります。  

Configuration Manager の Mac クライアントは常に証明書失効を確認します。 この機能を無効にすることはできません。  

証明書失効リスト (CRL) が見つからない場合、Mac クライアントは Configuration Manager サイト システムに接続できません。 特に、Mac クライアントが発行側の証明機関とは別のフォレストにある場合、CRL の設計を確認します。 Mac クライアントが CRL の場所を特定し、接続できるようにします。  

Mac コンピューターに構成マネージャー クライアントをインストールする前に、クライアント証明書をインストールする方法を決定します。  

-   [CMEnroll ツール](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll) を使用して Configuration Manager 登録を使用する。 登録プロセスでは自動証明書更新はサポートされていません。 証明書が期限切れになる前に、Mac コンピューターを再登録してください。  

-   [Configuration Manager から独立した証明書の要求とインストールの方法を使用する](deploy-clients-to-macs.md#bkmk_external)。  

Mac クライアントの証明書の要件の詳細については、「[Configuration Manager での PKI 証明書の要件](../../plan-design/network/pki-certificate-requirements.md)」を参照してください。  

Mac クライアントは、クライアントを管理する Configuration Manager サイトに自動的に割り当てられます。 Mac クライアントは、通信がイントラネットに制限されている場合でも、インターネット専用クライアントとしてインストールされます。 この構成は、これらが、割り当て済みサイトのインターネット対応の管理ポイントおよび配布ポイントと通信することを意味します。 Mac コンピューターは、割り当てられたサイト以外のサイト システムと通信しません。  

> [!IMPORTANT]  
>  macOS 用の Configuration Manager クライアントを使用して、[データベース レプリカ](../../servers/deploy/configure/database-replicas-for-management-points.md)を使用するように構成されている管理ポイントに接続することはできません。  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Web サーバー証明書をサイト システム サーバーに展開する  

これらのサイト システムに証明書がない場合は、次のサイト システムの役割があるコンピューターに Web サーバー証明書を展開します。  

-   管理ポイント  

-   配布ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

Web サーバー証明書には、サイト システム プロパティで指定されるインターネット FQDN が含まれている必要があります。 サーバーはインターネットからアクセスできない場合でも Mac コンピューターをサポートできます。 インターネットベースのクライアント管理が不要な場合、インターネット FQDN にイントラネット FQDN 値を指定できます。  

管理ポイント、配布ポイント、および登録プロキシ ポイントの Web サーバー証明書に、サイト システムのインターネット FQDN 値を指定します。

展開例については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)」を参照してください。  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>クライアント認証証明書をサイト システム サーバーに展開する  

これらのサイト システムに証明書がない場合は、クライアント認証証明書を、次のサイト システムの役割をホストするコンピューターに展開します。  

-   管理ポイント  

-   配布ポイント  

管理ポイントのクライアント証明書を作成してインストールする展開例については、「[Windows コンピューター用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)」をご覧ください。  

配布ポイントのクライアント証明書を作成してインストールする展開例については、「[配布ポイント用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)」をご覧ください。  

> [!IMPORTANT]  
>  macOS Sierra を実行しているデバイスにクライアントを展開するには、管理ポイント証明書のサブジェクト名を正しく構成する必要があります。 たとえば、管理ポイント サーバーの FQDN を指定します。  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Mac 用のクライアント証明書テンプレートを準備する  

証明書テンプレートには、Mac コンピューターに証明書を登録するユーザー アカウントに対する**読み取り**と**登録**の権限が必要です。  

詳細については、「[Mac コンピューター用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)」を参照してください。  



## <a name="configure-the-management-point-and-distribution-point"></a>管理ポイントおよび配布ポイントを構成する  

次のオプションを指定して、管理ポイントを構成します。  

-   HTTPS  

-   インターネットからのクライアント接続を許可する。 この構成値は、Mac コンピューターの管理に必要です。 ただし、インターネットからサイト システム サーバーにアクセスする必要があるということではありません。  

-   モバイル デバイスおよび Mac コンピューターでこの管理ポイントを使用できるようにする  

Mac へのクライアントのインストールに配布ポイントは必要ありません。 クライアントをインストールした後で、これらのコンピューターにソフトウェアを展開する場合は、インターネットからのクライアント接続を許可するように配布ポイントを構成します。  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>管理ポイントと配布ポイントで Mac のサポートを構成するには  

この手順を開始する前に、必ずインターネット FQDN を指定して管理ポイントと配布ポイントを構成してください。 これらのサーバーでインターネットベースのクライアント管理をサポートしていない場合は、インターネット FQDN 値としてイントラネット FQDN を指定します。

これらのサイト システムの役割はプライマリ サイト内にある必要があります。  

1.  Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サーバーとサイト システムの役割]** ノードを選択します。 次に、適切なサイト システムの役割があるサーバーを選択します。  

2.  詳細ウィンドウで **[管理ポイント]** 役割を選択して、リボンの **[プロパティ]** を選択します。 **[管理ポイントのプロパティ]** ウィンドウで、次のオプションを構成します。  

    1.  **[HTTPS]** を選択します。  

    2.  **[インターネットのみのクライアント接続を許可する]** または **[イントラネットとインターネット両方のクライアント接続を許可する]** を選択します。 これらのオプションには、インターネットまたはイントラネット FQDN が必要です。  

    3.  **[モバイル デバイスおよび Mac コンピューターでこの管理ポイントを使用できるようにする]** を選択します。  

    4. **[OK]** を選択して、この構成を保存します。  

3.  サーバーとサイト システムの役割ノードの詳細ウィンドウで、 **[配布ポイント]** 役割を選択して、リボンの **[プロパティ]** を選択します。 **[配布ポイントのプロパティ]** ウィンドウで、次のオプションを構成します。  

    -   **[HTTPS]** を選択します。  

    -   **[インターネットのみのクライアント接続を許可する]** または **[イントラネットとインターネット両方のクライアント接続を許可する]** を選択します。 これらのオプションには、インターネットまたはイントラネット FQDN が必要です。  

    -   **[証明書をインポートする]** を選択し、エクスポートされているクライアント配布ポイント証明書ファイルを参照して、パスワードを指定します。  

4.  Mac コンピューターを管理するプライマリ サイトのすべての管理ポイントと配布ポイントに対し、この手順を繰り返します。  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>登録プロキシ ポイントおよび登録ポイントを構成する  

同じサイトに両方の役割をインストールします。 同じサイト システム サーバー内または同じ Active Directory フォレスト内にインストールする必要はありません。  

サイト システムの役割の配置と考慮事項の詳細については、「[サイト システムの役割](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)」を参照してください。  

Mac コンピューターをサポートするサイト システムの役割を追加するには、[サイト システムの役割のインストール](../../servers/deploy/configure/install-site-system-roles.md)に関する記事をご覧ください。

**[システムの役割の選択]** ページの利用可能な役割の一覧で、 **[登録プロキシ ポイント]** および **[登録ポイント]** を選択します。  



## <a name="install-the-reporting-services-point"></a>レポート サービス ポイントをインストールする  

詳細については、[レポート サービス ポイントのインストール](../../servers/manage/configuring-reporting.md)に関するページを参照してください。  



## <a name="next-steps"></a>次のステップ

[Configuration Manager クライアントを Mac コンピューターに展開する](deploy-clients-to-macs.md)  
