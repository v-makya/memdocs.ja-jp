---
title: SMS プロバイダーの計画
titleSuffix: Configuration Manager
description: Configuration Manager の SMS プロバイダー サイト システムの役割について説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c83d0da07474c8b078ee226d249b73f00562e0f5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700165"
---
# <a name="plan-for-the-sms-provider"></a>SMS プロバイダーの計画

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager を管理するには、**SMS プロバイダー**のインスタンスに接続する Configuration Manager コンソールを使用します。 既定では、中央管理サイトまたはプライマリ サイトのインストール時に、SMS プロバイダーがサイト サーバーにインストールされます。

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> SMS プロバイダーについて  

SMS プロバイダーは、サイトで Configuration Manager データベースの**読み取り**と**書き込み**アクセス権を割り当てる、Windows Management Instrumentation (WMI) プロバイダーの 1 つです。  

- それぞれの中央管理サイトとプライマリ サイトには、SMS プロバイダーが少なくとも 1 つなければなりません。 必要に応じて、さらにプロバイダーをインストールできます。  

- **SMS Admins** セキュリティ グループには、SMS プロバイダーへのアクセス権が与えられています。 SMS プロバイダーのインスタンスがインストールされている各コンピューターとサイト サーバーには、このグループが Configuration Manager によって自動的に作成されます。 詳細については、「[SMS Admins](accounts.md#sms-admins)」 (SMS 管理者) を参照してください。  

- セカンダリ サイトでは SMS プロバイダーの役割はサポートされていません。  

Configuration Manager の管理ユーザーは、SMS プロバイダーを使用して、データベースに格納されている情報にアクセスします。 そのための手段として、管理者は Configuration Manager コンソールやリソース エクスプローラー、ツール、カスタム スクリプトを利用できます。 SMS プロバイダーは、Configuration Manager クライアントとは動作しません。 Configuration Manager コンソールがサイトに接続されると、使用する SMS プロバイダーのインスタンスを見つけるためにサイト サーバーで WMI のクエリが実行されます。  

SMS プロバイダーは、Configuration Manager にセキュリティを強制するのを助けます。 コンソール ユーザーが見ることのできる情報のみが返されます。  

SMS プロバイダーでも、HTTPS での API 相互運用性アクセスが提供されます (**管理サービス**と呼ばれます)。 この REST API をカスタム Web サービスの代わりに使って、サイトからの情報にアクセスできます。 詳細については、「[管理サービスとは何ですか](../../../develop/adminservice/overview.md)」をご覧ください。

> [!IMPORTANT]  
> サイトの SMS プロバイダーのインスタンスがそれぞれオフラインの場合、Configuration Manager コンソールからそのサイトに接続することはできません。  

SMS プロバイダーを管理する方法の詳細については、「[SMS プロバイダーを管理する](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)」を参照してください。  

## <a name="installation-prerequisites"></a>インストールの前提条件  

SMS プロバイダーをサポートするには、ターゲット サーバーが次の前提条件を満たす必要があります。  

- サイト サーバーおよびサイト データベース サイト システムと同じドメイン内にある  

- 別のサイトからのサイト システムの役割を持つことができない  

- まだどのサイトの SMS プロバイダーも持つことができない  

- サポートされている OS バージョンを実行する  

- Windows ADK コンポーネントをサポートするための 650 MB 以上の空きディスク領域。 Windows ADK と SMS プロバイダーの詳細については、「[OS deployment requirements](#BKMK_WAIKforSMSProv)」 (OS 展開の要件) を参照してください。  

- [管理サービス](../../../develop/adminservice/overview.md)の REST API について:

  - .NET 4.5 以降

  - Windows サーバー ロール **Web Server (IIS)** を有効にする

    > [!Note]  
    > すべての SMS プロバイダーで管理サービスのインストールが試みられます。このインストールには証明書が必要です。 その証明書を HTTPS ポート 443 にバインドするため、このサービスは IIS に依存します。 [拡張 HTTP](enhanced-http.md) を有効にすると、サイトでは IIS API を利用してその証明書がバインドされます。 サイトで PKI が使用される場合、SMS プロバイダーの IIS で PKI 証明書を手動でバインドする必要があります。 バージョン 2002 以降、サイトでは自動的に、サイトの自己署名証明書が使用されます。

## <a name="locations"></a><a name="bkmk_location"></a> 場所  

サイトをインストールするときに、そのサイトの 1 つ目の SMS プロバイダーが自動的にインストールされます。 SMS プロバイダーのインストール先として、次のいずれかを指定できます。  

- サイト サーバー  

- サイト データベース サーバー  

- [インストールの前提条件](#installation-prerequisites)を満たす、別のサーバー  

サイトの各 SMS プロバイダーの場所を表示するには、次のようにします。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開してから **[サイト]** ノードを選択します。  

2. リストから目的のサイトを選択し、リボンで **[プロパティ]** を選択します。  

3. サイトの **[プロパティ]** の **[全般]** タブで、 **[SMS プロバイダーの場所]** フィールドを表示します。  

1 つの SMS プロバイダーが同時に複数の要求を受信できます。 この接続に関する唯一の制限は、Windows で使用できるサーバー接続の数と、接続要求を処理するためにサーバーで使用可能なリソースです。  

サイトをインストールした後、サイト サーバーで Configuration Manager セットアップをもう一度実行できます。 セットアップを使用して、既存の SMS プロバイダーの場所を変更したり、同じサイトに追加の SMS プロバイダーをインストールしたりします。 コンピューターには 1 つの SMS プロバイダーのみをインストールします。 コンピューターでは、複数のサイトからの SMS プロバイダーをホストすることはできません。  

### <a name="choosing-a-location"></a>場所の選択

以下のセクションでは、サポートされているそれぞれの場所に SMS プロバイダーをインストールすることの利点と欠点について説明します。  

#### <a name="configuration-manager-site-server"></a>Configuration Manager サイト サーバー

- **利点:**  

  - SMS プロバイダーでは、サイト データベース コンピューターのシステム リソースを使用しません。  

  - サイト サーバーまたはサイト データベース以外のコンピューターに SMS プロバイダーをインストールした場合より、パフォーマンスが高くなります。  

- **欠点:**  

  - SMS プロバイダーが、サイト サーバーで占有できるはずのシステム リソースとネットワーク リソースを使用します。  

#### <a name="sql-server-that-hosts-the-site-database"></a>サイト データベースをホストする SQL Server

- **利点:**  

  - SMS プロバイダーでは、サイト サーバーのシステム リソースを使用しません。  

  - サーバーのリソースが十分ある場合は、3 つのインストール先のうち、一番高いパフォーマンスが得られます。  

- **欠点:**  

  - SMS プロバイダーが、サイト データベースで占有できるはずのシステム リソースとネットワーク リソースを使用します。  

  - サイト データベースが SQL Server のクラスター化されたインスタンスでホストされている場合、この場所を使用することはできません。  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>サイト サーバーまたはサイト サーバー データベース以外のコンピューター

- **利点:**  

  - SMS プロバイダーでは、サイト サーバーやサイト データベースのシステム リソースを使用しません。  

  - 追加の SMS プロバイダーをインストールして、接続の可用性を上げるのに便利です。  

- **欠点:**  

  - SMS プロバイダーのパフォーマンスが低下する可能性があります。 この動作は、サイト サーバーおよびサイト データベース コンピューターと連携する必要がある追加のネットワーク アクティビティが原因です。  

  - サイト データベース サーバー、および Configuration Manager コンソールがインストールされているすべてのコンピューターから、常にこのサーバーにアクセスできなければなりません。  

  - SMS プロバイダーが、他のサービスで占有できるはずのシステム リソースを使用します。  

## <a name="authentication"></a><a name="bkmk_auth"></a> 認証

<!--1357013-->
バージョン 1810 以降では、Configuration Manager サイトにアクセスする管理者の最低限の認証レベルを指定することができます。 この機能では、Windows にサインインする管理者には必要なレベルを持つことが強制されます。 SMS プロバイダーにアクセスするすべてのコンポーネントに適用されます。 たとえば、Configuration Manager コンソール、SDK メソッド、Windows PowerShell コマンドレットなどです。

### <a name="configure-authentication"></a>認証の構成

この設定を構成するには、最初に目的の認証レベルで Windows にサインインします。

> [!Important]  
> この構成は階層全体の設定です。 この設定を変更する前に、すべての Configuration Manager 管理者が必要な認証レベルで Windows にサインインできることを確認してください。

この設定を構成するには、次の手順を使用します。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2. リボンの **[階層設定]** を選択します。  

3. **[認証]** タブに切り替えます。必要な[認証レベル](#authentication-levels)、 **[OK]** の順に選択します。  

    - 必要な場合にのみ、 **[追加]** を選択して特定のユーザーまたはグループを除外します。 詳細については、「[除外](#exclusions)」を参照してください。  

### <a name="authentication-levels"></a>認証レベル

次のレベルを使用できます。

- **Windows 認証**:Active Directory ドメイン資格情報による認証が必要です。 この設定は以前の動作であり、現在の既定の設定です。 サイトを更新するとき、認証レベルは変更されません。  

- **証明書認証**:信頼された PKI 証明機関によって発行された有効な証明書による認証が必要です。 この証明書は Configuration Manager では構成しません。 Configuration Manager では、管理者は PKI を使用して Windows にサインインする必要があります。  

- **Windows Hello for Business 認証**:デバイスに関連付けられた、生体認証か PIN を使用する強力な 2 要素認証による認証が必要です。 詳細については、「[Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification)」を参照してください。  

### <a name="exclusions"></a>除外

[階層設定] の **[認証]** タブでは、特定のユーザーまたはグループを除外することもできます。 このオプションは慎重に使用してください。 たとえば、Configuration Manager コンソールにアクセスする必要がある特定のユーザーが、Windows での認証に必要なレベルを持たないような場合です。 また、システム アカウントのコンテキストで実行されるオートメーションまたはサービスに対しても必要な場合があります。

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> SMS プロバイダーの言語について  

SMS プロバイダーは、そのインストール先のサーバーの表示言語とは独立して動作します。  

管理ユーザーまたは Configuration Manager プロセスで SMS プロバイダーを使用してデータが要求されると、要求元のコンピューターの OS 言語と一致する形式でそのデータを返すことが試されます。

言語と一致させるために試される方法は間接的です。 SMS プロバイダーで情報が別の言語に翻訳されることはありません。 Configuration Manager コンソールで表示するデータが返される場合、そのデータの表示言語はオブジェクトのソースとストレージの種類によって異なります。  

Configuration Manager によってデータベースにオブジェクトのデータが格納される場合、使用可能な言語は次の要因によって異なります。  

- Configuration Manager では、複数言語のサポートを使用して作成されるオブジェクトを格納します。 セットアップの実行時にサイトに対して構成された言語を使用して、サイト データベースにオブジェクトを格納します。 Configuration Manager コンソールでは、要求元のコンピューターの表示言語がオブジェクトで使用できる場合、その言語でこれらのオブジェクトが表示されます。 コンソールでオブジェクトを要求元のコンピューターの表示言語で表示できない場合は、既定の言語 (英語) でオブジェクトが表示されます。  

- Configuration Manager では、管理ユーザーが作成したオブジェクトを、そのオブジェクトの作成時に使用された言語を使って格納します。 これらのオブジェクトが Configuration Manager コンソールに表示されるときにも、同じ言語が使われます。 SMS プロバイダーでそれらを翻訳することはできず、それらに複数言語のオプションはありません。  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> 複数の SMS プロバイダーの使用  

サイトのインストールが完了したら、そのサイト用に追加の SMS プロバイダーをインストールすることができます。 追加の SMS プロバイダーをインストールするには、サイト サーバーで Configuration Manager のセットアップを実行します。

次のいずれかに該当する場合は、追加の SMS プロバイダーのインストールを検討してください。  

- 多くの管理ユーザーが Configuration Manager コンソールを使用して、サイトに同時に接続する必要がある。  

- SMS プロバイダーを頻繁に呼び出す可能性がある、Configuration Manager SDK、または同様の製品を使用する。  

- SMS プロバイダーの高可用性に関するビジネス要件がある。  

サイトに複数の SMS プロバイダーをインストールした場合に、接続要求が行われると、サイトでは、インストールされた SMS プロバイダーを使用するために新しい接続要求がそれぞれランダムに割り当てられます。 特定の接続セッションで使用するように SMS プロバイダーを指定することはできません。  

> [!NOTE]  
> SMS プロバイダーの各場所の長所と欠点を考慮してください。 詳細については、「[場所](#bkmk_location)」を参照してください。 新しい接続ごとに使用される SMS プロバイダーを制御できないということと考え合わせて、これらの使用を計画してください。  

初めて Configuration Manager コンソールをサイトに接続する場合、その接続時にサイト サーバーで WMI のクエリが実行されます。 このクエリでは、コンソールで使用される SMS プロバイダーのインスタンスを識別します。 SMS プロバイダーのこの特定のインスタンスは、セッションが終了するまでコンソールで使用されたままになります。 ネットワーク上で SMS プロバイダー サーバーを使用できないためにセッションが終了した場合、コンソールをサイトに再接続すると、最初のクエリが繰り返されます。 サイトでは、使用できない同じ SMS プロバイダー インスタンスが割り当てられる可能性があります。 この動作が発生した場合は、サイトから使用可能な SMS プロバイダーが返されるまで、コンソールの再接続を試します。  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> SMS プロバイダーの名前空間について  

Configuration Manager の WMI スキーマでは、SMS プロバイダーの構造を定義します。 SMS プロバイダーのスキーマ内の Configuration Manager データの場所は、スキーマの名前空間で記述します。 次の表には、SMS プロバイダーで使用される一般的な名前空間がいくつか含まれています。  

|Namespace|[説明]|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|Configuration Manager コンソール、リソース エクスプローラー、Configuration Manager のツール、スクリプトによって使用される SMS プロバイダー。|  
|`Root\SMS\SMS_ProviderLocation`|サイトの SMS プロバイダーのコンピューターの場所。|  
|`Root\CIMv2`|ハードウェアとソフトウェアのインベントリ中に、WMI 名前空間情報がインベントリされる場所。|  
|`Root\CCM`|Configuration Manager クライアントの構成ポリシーとクライアント データ。|  
|`Root\CIMv2\SMS`|インベントリのクライアント エージェントによって収集されるインベントリ レポート クラスの場所。 クライアントでは、コンピューター ポリシーの評価中にこれらの設定をコンパイルします。 これらの設定は、コンピューターに対するクライアント設定の構成に基づいています。|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a> OS の展開の要件

SMS プロバイダーのインスタンスをインストールするコンピューターには、サポートされているバージョンの Windows ADK が必要です。  

この要件の詳細については、「[OS の展開のインフラストラクチャ要件](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)」と、[Windows 10 のサポート](../configs/support-for-windows-10.md)に関するページを参照してください。  

OS の展開を管理する場合、Windows ADK を使用することで、SMS プロバイダーでは次のようなさまざまなタスクを行うことができます。  

- WIM ファイルの詳細を表示する  

- 既存のブート イメージにドライバー ファイルを追加する  

- ブート用 ISO ファイルを作成する  

Windows ADK をインストールするには、SMS プロバイダーのインストール先コンピューターに 650 MB 以上の空きディスク領域が必要です。 このような大きな空きディスク領域が必要なのは、Configuration Manager によって Windows PE ブート イメージがインストールされるためです。  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a> 管理サービス

<!--3607711, fka 1321523-->

SMS プロバイダーでは、HTTPS OData 接続での API 相互運用性アクセスが提供されます (**管理サービス**と呼ばれます)。 この REST API をカスタム Web サービスの代わりに使って、サイトからの情報にアクセスできます。

詳細については、「[管理サービスとは何ですか](../../../develop/adminservice/overview.md)」をご覧ください。