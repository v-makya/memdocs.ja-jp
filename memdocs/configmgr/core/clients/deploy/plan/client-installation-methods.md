---
title: クライアント インストール方法
titleSuffix: Configuration Manager
description: Configuration Manager クライアントをインストールする方法について説明します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693840"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Configuration Manager でのクライアントのインストール方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager クライアント ソフトウェアはさまざまな方法でインストールできます。 1 つの方法を利用することも、複数の方法を組み合わせることもできます。 この記事では、各方法について説明するので、どれが組織に最適か学習できます。  

## <a name="client-push-installation"></a>クライアント プッシュ インストール  

**サポートされるクライアント プラットフォーム**:Windows  

#### <a name="advantages"></a>長所  

-   単一コンピューター、コンピューターのコレクション、またはクエリの結果に対してクライアントをインストールするのに使用できます。  

-   検出されたすべてのコンピューターにクライアントを自動インストールするときに使用できます。  

-   **[クライアント プッシュ インストールのプロパティ]** ダイアログ ボックスの **[クライアント]** タブで定義したクライアント インストールのプロパティが自動的に使用されます。  

#### <a name="disadvantages"></a>短所  

-   大きなコレクションにプッシュするとき、ネットワーク トラフィックの量が増加する可能性があります。  

-   Configuration Manager で検出されたコンピューターでしか使用できません。  

-   ワークグループにクライアントをインストールするときに使用することはできません。  

-   クライアント プッシュ インストールのアカウントでは、どのアカウントに目的のクライアント コンピューターに対する管理者権限を付与するかを指定する必要があります。  

-   クライアント コンピューターで、例外を使用して、Windows ファイアウォールを構成する必要があります。   

-   クライアント プッシュ インストールはキャンセルできません。 Configuration Manager は、検出されたすべてのリソースにクライアントをインストールしようとします。 最大 7 日間、失敗した操作を再試行します。  

詳細については、「[クライアント プッシュを使用したクライアントのインストール方法](../deploy-clients-to-windows-computers.md#BKMK_ClientPush)」を参照してください。  



## <a name="software-update-point-based-installation"></a>ソフトウェアの更新ポイント経由のインストール  

**サポートされるクライアント プラットフォーム**:Windows  

#### <a name="advantages"></a>長所  

-   既存のソフトウェアの更新のインフラストラクチャを使用して、クライアント ソフトウェアを管理できます。  

-   Windows Server Update Services (WSUS) および Active Directory ドメイン サービスのグループ ポリシー設定が正しく構成されている場合は、新しいコンピューターにクライアント ソフトウェアを自動的にインストールできます。  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   コンピューターは、Active Directory ドメイン サービスに公表されたクライアント インストール プロパティを読み取ることができます。  

-   この方法では、クライアントが削除された場合、再インストールされます。  

-   目的のクライアント コンピューターのインストール アカウントを構成してメンテナンスを行う必要はありません。  

#### <a name="disadvantages"></a>短所  

-   ソフトウェアの更新のインフラストラクチャが機能していることが前提条件です。  

-   クライアントのインストールとソフトウェアの更新に同じサーバーを使用する必要があります。 このサーバーは、プライマリ サイトに存在する必要があります。  

-   新しいクライアントをインストールするには、クライアントのアクティブなソフトウェアの更新ポイントおよびポートを使用して、Active Directory Domain Services 内のグループ ポリシー オブジェクトを構成する必要があります。  

-   Active Directory スキーマが Configuration Manager 向けに拡張されていない場合、グループ ポリシー設定を使用してクライアント インストールのプロパティをコンピューターにプロビジョニングする必要があります。  

詳細については、「[ソフトウェアの更新に基づいたインストールを使用したクライアントのインストール方法](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP)」を参照してください。  



## <a name="group-policy-installation"></a>グループ ポリシーによるインストール  

**サポートされるクライアント プラットフォーム**:Windows  

#### <a name="advantages"></a>長所  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   新しいクライアントのインストールまたは更新で使用できます。  

-   コンピューターは、Active Directory ドメイン サービスに公表されたクライアント インストール プロパティを読み取ることができます。  

-   目的のクライアント コンピューターのインストール アカウントを構成してメンテナンスを行う必要はありません。  

#### <a name="disadvantages"></a>短所  

-   多数のクライアントがインストールされた場合、ネットワーク トラフィックの量が増加する可能性があります。  

-   Active Directory スキーマが Configuration Manager 向けに拡張されていない場合、グループ ポリシー設定を使用してサイト内のコンピューターにクライアント インストール プロパティを追加する必要があります。  

詳細については、「[グループ ポリシーを使用したクライアントのインストール方法](../deploy-clients-to-windows-computers.md#BKMK_ClientGP)」を参照してください。  



## <a name="logon-script-installation"></a>ログオン スクリプトによるインストール  

**サポートされるクライアント プラットフォーム**:Windows  

#### <a name="advantages"></a>長所  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   CCMSetup のコマンド ライン プロパティを使用してサポートします。  

#### <a name="disadvantages"></a>短所  

-   多数のクライアントが短時間にインストールされた場合、ネットワーク トラフィックの量が増加する可能性があります。  

-   ユーザーがネットワークに頻繁にログオンしない場合は、すべてのクライアント コンピューターにインストールするのに長時間かかる場合があります。  

詳細については、「[ログオン スクリプトを使用したクライアントのインストール方法](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript)」を参照してください。  



## <a name="manual-installation"></a>手動インストール  

**サポートされるクライアント プラットフォーム**:Windows、UNIX、Linux、Mac OS X  

#### <a name="advantages"></a>長所  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   テストの目的で役立ちます。  

-   CCMSetup のコマンド ライン プロパティを使用してサポートします。  

#### <a name="disadvantages"></a>短所  

-   自動化されていないため、時間を削減できます。  

各プラットフォームのクライアントを手動でインストールする方法の詳細については、次の記事をご覧ください。  

-   [Windows コンピューターにクライアントを展開する方法](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [UNIX および Linux サーバーにクライアントを展開する方法](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Mac にクライアントを展開する方法](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM のインストール

**サポートされるクライアント プラットフォーム**:Windows 10

#### <a name="advantages"></a>長所  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   目的のクライアント コンピューターのインストール アカウントを構成してメンテナンスを行う必要はありません。  

-   Azure Active Directory での先進認証を使用できます。  

-   インターネット上のコンピューターにインストールして割り当てることがことができます。  

-   共同管理用に Windows AutoPilot と Microsoft Intune で自動化できます。  

#### <a name="disadvantages"></a>短所  

-   Configuration Manager の外部での他のテクノロジーが必要です。  

-   デバイスは、インターネット ベースでない場合でもインターネットにアクセスできる必要があります。  

詳細については、以下の記事を参照してください。  

-   [Intune に登録されている MDM 管理対象 Windows デバイスへのクライアントのインストール方法](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](../deploy-clients-cmg-azure.md)  

