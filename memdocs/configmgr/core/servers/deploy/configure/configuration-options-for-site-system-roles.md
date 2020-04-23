---
title: サイト システムの役割オプション
titleSuffix: Configuration Manager
description: この記事では、必ずしも説明の必要がないとは言えない、Configuration Manager サイト システム役割の詳細を示します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704810"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Configuration Manager でのサイト システムの役割の構成オプション

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のサイト システムの役割のほとんどの構成オプションについては、説明の必要がないか、構成時にウィザードかダイアログ ボックスで説明されます。 以下のセクションでは、追加情報を必要とする設定があるサイト システムの役割について説明します。  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a> アプリケーション カタログ Web サイト ポイント  

> [!Important]
> アプリケーション カタログの Silverlight ユーザー エクスペリエンスは、Current Branch バージョン 1806 以降では、サポートされません。 バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  
>
> 詳細については、以下の記事を参照してください。
>
> - [ソフトウェア センターの構成](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [削除された機能と非推奨の機能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

アプリケーション カタログ Web サイト ポイントの設定方法について詳しくは、「[アプリケーション管理の計画と構成](../../../../apps/plan-design/plan-for-and-configure-application-management.md)」を参照してください。  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a> アプリケーション カタログ Web サービス ポイント  

> [!Important]
> アプリケーション カタログの Silverlight ユーザー エクスペリエンスは、Current Branch バージョン 1806 以降では、サポートされません。 バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  
>
> 詳細については、以下の記事を参照してください。
>
> - [ソフトウェア センターの構成](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [削除された機能と非推奨の機能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

アプリケーション カタログ Web サービス ポイントの設定方法について詳しくは、「[アプリケーション管理の計画と構成](../../../../apps/plan-design/plan-for-and-configure-application-management.md)」をご覧ください。  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a> 証明書登録ポイント  

証明書登録ポイントの設定方法の詳細については、「[証明書プロファイルの概要](../../../../protect/deploy-use/introduction-to-certificate-profiles.md)」を参照してください。  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a> 配布ポイント  

コンテンツ展開の配布ポイントの構成方法については、[コンテンツとコンテンツ インフラストラクチャの管理](manage-content-and-content-infrastructure.md)に関するページをご覧ください。  

PXE 展開の配布ポイントの設定方法については、[PXE を使用したネットワーク経由での Windows の展開](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)に関するページをご覧ください。  

マルチキャスト展開の配布ポイントの設定方法については、[マルチキャストを使用したネットワーク経由での Windows の展開](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)に関するページをご覧ください。  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Configuration Manager で必要な場合は IIS をインストールして構成する

IIS がまだインストールされていない場合に、Configuration Manager で自動的に IIS をインストールして設定するには、このオプションを選択します。 IIS はすべての配布ポイントにインストールする必要があり、ウィザードを続行するにはこの設定を選択する必要があります。  

### <a name="site-system-installation-account"></a>サイト システムのインストール アカウント

サイト サーバーにインストールされている配布ポイントでは、サイト システムのインストール アカウントとしての使用がサポートされているのは、サイト サーバーのコンピューター アカウントだけです。 詳細については、[アカウント](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)に関するページを参照してください。  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a> 登録ポイント  

登録ポイントは、macOS コンピューターをインストールし、オンプレミスのモバイル デバイス管理で管理するデバイスを登録するために使用します。 詳細については、以下の記事を参照してください。  

- [Mac にクライアントを展開する方法](../../../clients/deploy/deploy-clients-to-macs.md)  

- [ユーザーがオンプレミス MDM にデバイスを登録する方法](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>許可される接続

HTTPS 設定が自動的に選択されます。HTTPS 設定では、登録プロキシ ポイントに対するサーバーの認証と SSL 経由でのデータの暗号化のために、サーバー上に PKI 証明書が必要です。 詳細については、「[PKI 証明書の要件](../../../plan-design/network/pki-certificate-requirements.md)」を参照してください。  

サーバー証明書の展開例と、それをインターネット インフォメーション サービス (IIS) で構成する方法については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)」をご覧ください。  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a> 登録プロキシ ポイント  

モバイル デバイスの登録プロキシ ポイントの構成方法について詳しくは、「[ユーザーがオンプレミス MDM にデバイスを登録する方法](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)」をご覧ください。  

### <a name="client-connections"></a>クライアント接続

HTTPS 設定が自動的に選択されます。 サーバーで次の PKI 証明書が必要です。

- Configuration Manager で登録するモバイル デバイスおよび Mac コンピューターに対するサーバー認証用
- Secure Sockets Layer (SSL) を介したデータの暗号化用

証明書の要件のについては、「[PKI 証明書の要件](../../../plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

サーバー証明書の展開例と、それをインターネット インフォメーション サービス (IIS) で構成する方法については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)」をご覧ください。  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a> フォールバック ステータス ポイント  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>状態メッセージの数と調整間隔 (秒)

これらのオプションの既定の設定は、状態メッセージ数が 10,000、調整間隔が 3,600 秒です。 これらの設定はほとんどの状況に十分に対応できますが、次の両方の条件に一致する場合は、変更が必要になることがあります。  

- フォールバック ステータス ポイントがイントラネットからのみ接続を受け入れる。  

- 多数のコンピューターを対象としたクライアント展開のロールアウト中に、フォールバック ステータス ポイントを使用する。  

この場合は、状態メッセージの継続的なストリームのために状態メッセージのバックログが生成され、サイト サーバーのプロセッサ使用率が長時間高くなることがあります。 さらに、Configuration Manager コンソールとクライアント展開レポートに、クライアント展開の最新情報が表示されない場合もあります。  

これらのフォールバック ステータス ポイント設定は、クライアント展開中に生成される状態メッセージ用に設定するように設計されています。 これらの設定は、インターネット上のクライアントがインターネットベースの管理ポイントに接続できないなどの、クライアントの通信問題用に設定するようには設計されていません。 フォールバック ステータス ポイントは、クライアント展開中に生成された状態メッセージだけに設定を適用することができないため、フォールバック ステータス ポイントがインターネットからの接続を受け入れる場合には、これらの設定は構成しないでください。  

Configuration Manager クライアントを正常にインストールする各コンピューターは、次の 4 つの状態メッセージをフォールバック ステータス ポイントに送信します。  

- クライアントの展開が開始されました  

- クライアントの展開に成功しました  

- クライアントの割り当てが開始されました  

- クライアントの割り当てに成功しました  

インストールできないコンピューター、または Configuration Manager クライアントを割り当てることができないコンピューターは、追加の状態メッセージを送信します。  

たとえば、Configuration Manager クライアントを 20,000 台のコンピューターに展開する場合、フォールバック ステータス ポイントへの状態メッセージが 80,000 個送信されるとします。 既定のスロットル構成では、3,600 秒 (1 時間) ごとに 10,000 の状態メッセージをフォールバック ステータス ポイントに送信できるため、状態メッセージはフォールバック ステータス ポイント上でバックログされる可能性があります。 また、フォールバック ステータス ポイントとサイト サーバー間の利用可能なネットワーク帯域幅と、サイト サーバーが大量の状態メッセージを扱う処理能力も考慮します。  

このような問題を防止するため、状態メッセージの数を増やして、調整間隔を短くすることを検討してください。  

次の状態のいずれかが該当する場合は、フォールバック ステータス ポイントの調整値を再設定します。  

- 現在のスロットル値が、フォールバック ステータス ポイントからの状態メッセージの処理に必要な値より大きいことが計算される場合。  

- 現在の調整設定では、サイト サーバーのプロセッサ負荷が高くなる場合。  

結果について理解していない場合は、フォールバック ステータス ポイントの調整設定を変更しないでください。 たとえば、調整設定を高くすると、サイト サーバーのプロセッサ負荷が高くなり、すべてのサイト操作の速度が遅くなります。  
