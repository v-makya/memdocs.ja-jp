---
title: オンプレミス MDM の登録を設定する
titleSuffix: Configuration Manager
description: Configuration Manager でオンプレミスモバイルデバイス管理 (MDM) のデバイスを登録するためのアクセス許可をユーザーに付与します。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724686"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager でオンプレミス MDM のデバイス登録を設定する

*適用対象:Configuration Manager (Current Branch)*

オンプレミスモバイルデバイス管理 (MDM) を設定する最後の手順は、ユーザーが自分のデバイスを登録できるようにすることです。 Configuration Manager クライアント設定を使用して、オンプレミス MDM にデバイスを登録するためのアクセス許可をユーザーに付与します。

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a> 登録プロファイルの作成

ユーザーがモバイルデバイスを登録できるようにするために必要な設定をプッシュするには、既定のクライアント設定に新しい登録プロファイルを追加します。 このプロファイルは、Configuration Manager サイト内のすべてのユーザーに適用されます。

> [!NOTE]
> このプロセスでは、**既定のクライアント設定**を使用します。これは、すべてのデバイスとユーザーに自動的に適用されます。 または、カスタムクライアント設定を作成してから、任意のコレクションに展開することもできます。 この代替方法には、少なくとも2つのカスタムクライアント設定が必要です。1つは*デバイス*設定用、もう1つは*ユーザー*設定用です。 詳しくは、「[クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)」をご覧ください。

1. Configuration Manager コンソールで、[**管理**] ワークスペースにアクセスし、[**クライアント設定**] ノードを選択します。 [**既定のクライアント設定**] を開き、**登録**グループを選択します。

1. [デバイスの設定] で、**最新のデバイスのポーリング間隔 (分)** を指定します。 既定では、この間隔は60分です。

1. [ユーザー設定] で、ユーザーが**最新のデバイスを登録できる**ようにするオプションを有効にします。

1. 最新の**デバイス登録プロファイル**の場合は、[**プロファイルの設定**] を選択します。 [登録プロファイル] ウィンドウで、[**作成**] を選択します。

1. [登録プロファイルの作成] ウィンドウで、次の情報を指定します。

    - 登録プロファイルの一意でわかりやすい**名前**。

    - プロファイルに関する追加情報を提供するための**説明**です (省略可能)。

    - デバイス管理ポイントが含まれている**管理サイトコード**を選択します。 [ **OK]** を選択して保存して閉じます。

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>追加のクライアント設定を構成する

登録後にデバイスを構成するための追加のクライアント設定があります。 一般的な情報については、「[クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)」を参照してください。

Configuration Manager は、オンプレミス MDM に対して次のクライアント設定をサポートしています。

- **クライアントポリシー**: これらの設定は、デバイスにクライアントポリシーをダウンロードする頻度を指定します。 また、ユーザーポリシーの設定を有効にすることもできます。 詳細については、「[クライアントの設定について-クライアントポリシー](../../core/clients/deploy/about-client-settings.md#client-policy)」を参照してください。

- **ソフトウェアの展開**: ソフトウェアの展開を評価する間隔を設定します。 詳細については、「[クライアント設定について-ソフトウェアの展開](../../core/clients/deploy/about-client-settings.md#software-deployment)」を参照してください。

    > [!NOTE]
    > オンプレミス MDM の場合、ソフトウェア展開の設定は、既定のクライアント設定としてのみ使用できます。

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>ユーザーの探索

ユーザーがオンプレミス MDM の登録プロファイルを使用してクライアント設定を受信するには、Active Directory でそのユーザーアカウントを探索します。 必要とする全員が登録プロファイルを取得できるように、Active Directory ユーザーの探索を実行します。 詳細については、「 [Active Directory ユーザー探索](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)」を参照してください。

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>信頼されたルート証明書をインストールする

ドメインに参加しているデバイスは、サイトシステムの役割をホストするサーバーとの信頼された通信のための信頼されたルート証明書を取得します。 Active Directory 証明書サービスは、信頼されたルート証明書を自動的に配布します。 ドメインに参加していないコンピューターとモバイルデバイスでは、登録を許可するために、この証明書を他の方法でインストールする必要があります。

> [!NOTE]
> Web サーバー証明書が公開証明機関によって発行されている場合、ほとんどのデバイスはこれらの Ca を既に信頼しています。 これらのパブリック Ca のいずれかを使用する設計がある場合は、この手順を実行する必要はありません。

[信頼されたルート証明書をエクスポート](set-up-certificates-on-premises-mdm.md#bkmk_exportCert)したら、それを登録する必要があるデバイスにインストールする必要があります。 たとえば、ドメインに参加していないデバイスは、Active Directory から自動的に取得することはできません。 使用するプロセスは、次の要因によって異なります。

- 特定のデバイスの種類と技術的な機能
- OS バージョン
- ビジネス、セキュリティ、およびユーザーエクスペリエンスの要件

次の一覧に、信頼されたルート証明書をデバイスに配布してインストールする方法の例を示します。

- ファイル共有

- メールの添付ファイル

- [メモリ カード]

- テザリングされたデバイス

- クラウドの記憶域 (OneDrive など)

- 近距離無線通信 (NFC) 接続

- バーコード スキャナー

- Out of Box Experience (OOBE) プロビジョニング パッケージ

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Windows での信頼されたルート証明書の手動インストール

1. 登録するデバイスで、エクスプローラーで信頼されたルート証明書ファイル (.cer) を参照し、ファイルを**開き**ます。

1. [証明書] ウィンドウで、[**証明書のインストール**] を選択します。

1. 証明書のインポートウィザードで、[**ローカルコンピューター**] を選択し、[**次**へ] を選択して管理者として続行します。

1. [証明書ストア] ページで、[**証明書をすべて次のストアに配置する**] を選択し、[**参照**] を選択します。

1. [証明書ストアの選択] ウィンドウで、[**信頼されたルート証明機関**] を選択し、[ **OK]** を選択します。

1. 完了とウィザード。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [デバイスの登録](../deploy-use/enroll-devices-on-premises-mdm.md)
