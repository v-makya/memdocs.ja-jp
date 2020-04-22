---
title: アプリケーション管理を計画する
titleSuffix: Configuration Manager
description: Configuration Manager でアプリケーションを展開するために必要な依存関係を実装および構成します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689050"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Configuration Manager のアプリケーション管理の計画と構成

*適用対象:Configuration Manager (Current Branch)*

この記事の情報は、Configuration Manager でアプリケーションを展開するために必要な依存関係を適用するのに役立ちます。  



## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  


### <a name="internet-information-services-iis"></a>インターネット インフォメーション サービス (IIS)

次のサイト システムの役割を実行するサーバーでは IIS が必要です。

- 管理ポイント  
- 配布ポイント  

詳細については、「[サイトとサイト システムの前提条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)」をご覧ください。  

> [!Note]  
> アプリケーション カタログにも IIS が必要です。 ただし、その Silverlight ユーザー エクスペリエンスは、Current Branch バージョン 1806 の時点ではサポートされていません。 バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  
>
> 詳細については、以下の記事を参照してください。
>
> - [ソフトウェア センターの構成](plan-for-software-center.md#bkmk_userex)
> - [削除された機能と非推奨の機能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>モバイル デバイス用にコード署名されたアプリケーションでの証明書

モバイル デバイスに展開するためにアプリケーションをコード署名する場合は、バージョン 3 の証明書テンプレート (**Windows Server 2008 Enterprise Edition**) を使って作成された証明書を使用しないでください。 この証明書テンプレートは、モバイル デバイス用の Configuration Manager アプリケーションと互換性のない証明書を作成します。

Active Directory 証明書サービスを使ってモバイル デバイスのアプリケーションにコード署名する場合は、バージョン 3 の証明書テンプレートを使用しないでください。


### <a name="audit-sign-in-events-for-user-device-affinity"></a>ユーザーとデバイスのアフィニティに対するサインイン イベントを監査する  

ユーザーとデバイスのアフィニティを自動的に作成する場合、サインイン イベントを監査するようにクライアントを構成します。

自動的なユーザーとデバイスのアフィニティを判断するため、Configuration Manager クライアントは Windows のセキュリティ イベント ログから種類が **[成功]** のサインイン イベントを読み取ります。 次の 2 つの監査ポリシーでこれらのイベントを有効にします。

- **アカウント ログオン イベントの監査**
- **ログオン イベントの監査**

ユーザーとデバイス間に自動的に関係を作成するには、クライアント コンピューターでこれら 2 つの設定を有効にします。 Windows グループ ポリシーを使用してこれらの設定を構成できます。

ユーザーとデバイスのアフィニティの詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../deploy-use/link-users-and-devices-with-user-device-affinity.md)」をご覧ください。  



## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係


### <a name="management-point"></a>管理ポイント

クライアントは、管理ポイントに接続し、クライアント ポリシーのダウンロードやコンテンツの検索を行います。

バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。

バージョン 1902 以前では、クライアントは管理ポイントを使用してアプリケーション カタログに接続します。 クライアントが管理ポイントにアクセスできない場合、アプリケーション カタログを使用することはできません。

> [!Note]  
> バージョン 1806 以降では、ユーザーが利用できるアプリケーションをソフトウェア センターに表示するのにアプリケーション カタログの役割は必要なくなりました。 詳しくは、「[ソフトウェア センターの構成](plan-for-software-center.md#bkmk_userex)」をご覧ください。<!--1358309-->  
>
> バージョン 1906 以降では、新しいアプリケーション カタログの役割をインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  
  

### <a name="distribution-point"></a>配布ポイント

アプリケーションをクライアントに展開する前に、階層内に少なくとも 1 つの配布ポイントが必要です。 既定では、標準インストール中に、サイト サーバーに配布ポイント サイトの役割が割り当てられます。 配布ポイントの数と場所は、環境の要件によって異なります。

配布ポイントをインストールして、コンテンツを管理する方法の詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  


### <a name="reporting-services-point"></a>レポート サービス ポイント

Configuration Manager のレポートをアプリケーション管理に使用するには、まずレポート サービス ポイントをインストールして構成します。

詳細については、「[レポートの概要](../../core/servers/manage/introduction-to-reporting.md)」をご覧ください。  


### <a name="client-settings"></a>クライアント設定

クライアント設定の多くは、クライアントがアプリケーションをインストールする方法とデバイス上のユーザー エクスペリエンスを制御します。 これらのクライアント設定には次のようなグループがあります。

- コンピューター エージェント  
- コンピューターの再起動  
- ソフトウェア センター  
- ソフトウェアの展開  
- ユーザーとデバイスのアフィニティ  

詳細については、以下の記事を参照してください。

- [クライアント設定について](../../core/clients/deploy/about-client-settings.md)  
- [クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>アプリケーション管理用のセキュリティのアクセス許可

- **アプリケーション作成者**セキュリティ ロールには、アプリケーションを作成し、変更し、廃止するのに必要なアクセス許可が含まれます。  

- **アプリケーション展開マネージャー** セキュリティ ロールには、アプリケーションを展開するために必要なアクセス許可が含まれます。  

- **[アプリケーション管理者]** セキュリティ ロールには、 **[アプリケーション作成者]** および **[アプリケーション展開マネージャー]** セキュリティ ロール両方のすべてのアクセス許可が含まれます。  

詳細については、「[役割に基づいた管理の構成](../../core/servers/deploy/configure/configure-role-based-administration.md)」を参照してください。  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>App-V 4.6 SP1 以降のクライアント (仮想アプリケーションを実行する場合)

Configuration Manager で仮想アプリケーションを作成するには、App-V 4.6 SP1 以降をデバイスにインストールします。

また、仮想アプリケーションを展開する前に、[サポート技術情報の記事 2645225](https://support.microsoft.com/help/2645225) で説明されている修正プログラムで App-V クライアントを更新します。  


### <a name="application-catalog"></a>アプリケーション カタログ

> [!Important]  
> アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。 詳細については、「[アプリケーション カタログの削除](#bkmk_remove-appcat)」を参照してください。  

#### <a name="application-catalog-web-service-point"></a>アプリケーション カタログ Web サービス ポイント

アプリケーション カタログ Web サービス ポイントは、ソフトウェア ライブラリから入手できるソフトウェアに関する情報を、ユーザーがアクセスするアプリケーション カタログ Web サイトに提供するサイト システムの役割です。

サイト システムの役割を構成する方法について詳しくは、[アプリケーション カタログをインストールして構成する](#bkmk_appcat)に関するセクションをご覧ください。  

#### <a name="application-catalog-website-point"></a>アプリケーション カタログ Web サイト ポイント

アプリケーション カタログ Web サイト ポイントは、利用可能なソフトウェアの一覧をユーザーに提供するサイト システムの役割です。

サイト システムの役割を構成する方法について詳しくは、[アプリケーション カタログをインストールして構成する](#bkmk_appcat)に関するセクションをご覧ください。

#### <a name="discovered-user-accounts-for-application-catalog"></a>アプリケーション カタログに対して検出されたユーザー アカウント

ユーザーがアプリケーション カタログでアプリケーションを表示し、要求できるようになるには、まず Configuration Manager でそのユーザー アカウントが検出されている必要があります。 詳細については、「[探索を実行する](../../core/servers/deploy/configure/run-discovery.md)」を参照してください。  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a> ソフトウェア センターの構成  

ソフトウェア センターの構成とブランド化の詳細については、[ソフトウェア センターの計画](plan-for-software-center.md)に関するセクションを参照してください。


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a> アプリケーション カタログの削除

<!-- SCCMDocs-pr issue 3051 -->

アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。 詳細については、[削除された機能と非推奨の機能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。 変更内容の概要を次の一覧に示します。

- バージョン 1806 以降では、アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**はサポートされていません。<!--1358309--> アプリケーション カタログ Web サービス ポイントの役割は "*必須*" ではなくなりましたが、引き続き "*サポートされています*"。

- バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。

- アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  

ソフトウェア センターと管理ポイントがこのように繰り返し改善されるのは、ご自身のインフラストラクチャを簡略化し、ユーザーが利用可能な展開のためにアプリケーション カタログの必要性をなくすためです。 ソフトウェア センターでは、アプリケーション カタログなしですべてのアプリの展開を配信できます。 また、TLS 1.2 を有効にし、アプリケーション カタログで HTTP を使う場合、ユーザーはユーザーを対象とした利用可能な展開を表示できません。 これらの機能強化のメリットを活かすには、Configuration Manager をバージョン 1906 以降に更新します。

1. すべてのクライアントを 1806 またはそれ以降のバージョンに更新してください。 バージョン 1906 が推奨されます。  

1. アプリケーション カタログ Web サイトの役割のプロパティを使う代わりに、ソフトウェア センターのブランドを設定します。 詳細については、[ソフトウェア センターのクライアント設定](../../core/clients/deploy/about-client-settings.md#software-center)に関するページを参照してください。  

1. 既定および任意のカスタムのクライアント設定を確認します。 **[コンピューター エージェント]** グループで、 **[既定のアプリケーション カタログ Web サイト ポイント]** が `(none)` であることを確認します。  

    バージョン 1902 以前では、階層内にアプリケーション カタログの役割がなかった場合、クライアントは管理ポイントの使用に切り替えるだけです。 それ以外の場合、クライアントは階層内のアプリケーション カタログのいずれかのインスタンスを使用し続けます。 この動作は、別々のプライマリ サイト全体に適用されます。  

1. すべてのプライマリ サイトから**アプリケーション カタログ Web サイト**と**アプリケーション カタログ Web サービス** サイト システムの役割を削除します。

アプリケーション カタログの役割を削除すると、ソフトウェア センターでは、ユーザーを対象とした利用可能な展開に対して管理ポイントが使われ始めます。 バージョン 1902 以前では、この変更が発生するまでに、最大 65 分かかることがあります。 特定のクライアント上でこの動作を確認するには、`SCClient_<username>.log` を確認し、次の行のようなエントリを探します。

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a> アプリケーション カタログをインストールして構成する  

> [!Important]  
> アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。 詳細については、「[アプリケーション カタログの削除](#bkmk_remove-appcat)」を参照してください。  

### <a name="step-1-web-server-certificate-for-https"></a>手順 1:HTTPS 用の Web サーバー証明書

HTTPS 接続を使用する場合は、アプリケーション カタログ Web サイト ポイントおよびアプリケーション カタログ Web サービス ポイント用のサイト システム サーバーに、Web サーバー証明書を展開します。

クライアントにインターネットからアプリケーション カタログを使用させたい場合は、少なくとも 1 つの管理ポイントに Web サーバー証明書を展開します。 それをインターネットからのクライアント接続用に構成します。

証明書の要件の詳細については、[PKI 証明書の要件](../../core/plan-design/network/pki-certificate-requirements.md)に関する記事をご覧ください。  


### <a name="step-2-client-authentication-certificate-for-https"></a>手順 2:HTTPS 用のクライアント認証証明書

管理ポイントへの接続にクライアント PKI 証明書を使用する場合は、クライアント認証証明書をクライアント コンピューターに展開します。 クライアントは、アプリケーション カタログに接続するためにクライアント PKI 証明書を使用することはありませんが、アプリケーション カタログを使用するには、まず管理ポイントに接続する必要があります。

次のシナリオでは、クライアント認証証明書をクライアント コンピューターに展開します。

- イントラネットのすべての管理ポイントが、HTTPS クライアント接続のみを受け付けている。
- クライアントがインターネット経由でアプリケーション カタログに接続している。

証明書の要件の詳細については、[PKI 証明書の要件](../../core/plan-design/network/pki-certificate-requirements.md)に関する記事をご覧ください。  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>手順 3:アプリケーション カタログの役割をインストールして構成する

アプリケーション カタログ Web サービス ポイントおよびアプリケーション カタログ Web サイトの両方の役割を、同じサイトにインストールします。 同じサーバー上または同じ Active Directory フォレスト内にインストールする必要はありません。 しかし、アプリケーション カタログ Web サービス ポイントは、サイト データベースと同じフォレストに置かれている必要があります。

サーバーの配置について詳しくは、「[サイト システム サーバーとサイト システムの役割の計画](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)」をご覧ください。

> [!NOTE]  
> プライマリ サイトにアプリケーション カタログをインストールします。 セカンダリ サイトまたは中央管理サイトにインストールすることはできません。  

新しいサイト システム サーバーまたはサイト内の既存のサーバーに、アプリケーション カタログをインストールします。 一般的な手順について詳しくは、「[サイト システムの役割のインストール](../../core/servers/deploy/configure/install-site-system-roles.md)」をご覧ください。 サイト システムの役割を追加するウィザードまたはサイト システム サーバーを作成するウィザードで、一覧から次の役割を選択します。  

- **アプリケーション カタログ Web サービス ポイント**  
- **アプリケーション カタログ Web サイト ポイント**  

> [!TIP]  
> クライアント コンピューターがインターネット経由でアプリケーション カタログにアクセスできるようにするには、インターネット完全修飾ドメイン名 (FQDN) を指定します。  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>次にサイト システムの役割のインストールを確認する  

- ステータス メッセージ:コンポーネント **SMS_PORTALWEB_CONTROL_MANAGER** および **SMS_AWEBSVC_CONTROL_MANAGER**を使用します。  

    たとえば、**SMS_PORTALWEB_CONTROL_MANAGER** のステータス ID **1015** は、サイト コンポーネント マネージャーがアプリケーション カタログ Web サイト ポイントのインストールに成功したことを示します。  

- ログ ファイル:**SMSAWEBSVCSetup.log** および **SMSPORTALWEBSetup.log**を検索します。  

    詳細については、ログ ファイル、**awebsvcMSI.log** および **portlwebMSI.log** を検索してください。  


### <a name="step-4-configure-client-settings"></a>手順 4:クライアント設定を構成する

すべてのユーザーを同じ設定にする場合は、既定のクライアント設定を構成します。 または、コレクションごとにカスタムのクライアント設定を構成します。

詳細については、以下の記事を参照してください。

- [クライアント設定について](../../core/clients/deploy/about-client-settings.md)  
    - コンピューター エージェント  
    - コンピューターの再起動  
    - ソフトウェア センター  
    - ソフトウェアの展開  
    - ユーザーとデバイスのアフィニティ  
- [クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)  

Configuration Manager クライアントでは、クライアント ポリシーの次回ダウンロード時に、これらの設定でデバイスが構成されます。 1 つのクライアントのポリシーの取得をトリガーする場合は、「[クライアントを管理する方法](../../core/clients/manage/manage-clients.md)」をご覧ください。


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>手順 5:アプリケーション カタログが操作可能であることの確認

アプリケーション カタログが操作可能であることを確認するには、次の手順に従います。

> [!NOTE]  
> アプリケーション カタログのユーザー エクスペリエンスには、Microsoft Silverlight が必要です。 ブラウザーから直接アプリケーション カタログを使用する場合は、まずコンピューターに Microsoft Silverlight がインストールされていることを確認します。  

> [!TIP]  
> 前提条件を満たしていないことは、インストール後にアプリケーション カタログが正常に動作しない理由の中でも最も一般的なものです。 アプリケーション カタログ サイト システムの役割について、役割の前提条件を確認します。 詳細については、「[サイトとサイト システムの前提条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)」をご覧ください。  

ブラウザーで、アプリケーション カタログ Web サイトのアドレスを入力します。 Web ページに **[アプリケーション カタログ]** 、 **[アプリケーションの要求]** 、 **[デバイス]** の 3 つのタブが表示されることを確認します。  

次の一覧から、アプリケーション カタログの適切なアドレスを使用してください。`<server>` は、コンピューター名、イントラネット FQDN、またはインターネット FQDN です。  

- HTTPS クライアント接続および既定のサイト システムの役割設定: `https://<server>/CMApplicationCatalog`  

- HTTP クライアント接続および既定のサイト システムの役割設定: `http://<server>/CMApplicationCatalog`  

- HTTPS クライアント接続およびカスタムのサイト システムの役割設定: `https://<server>:<port>/<web application name>`  

- HTTP クライアント接続およびカスタムのサイト システムの役割設定: `http://<server>:<port>/<web application name>`  

> [!NOTE]  
> ドメイン管理者アカウントを使用してデバイスにサインインした場合、Configuration Manager クライアントの通知メッセージは表示されません。 たとえば、新しいソフトウェアが使用可能なことを示すメッセージなどです。  
