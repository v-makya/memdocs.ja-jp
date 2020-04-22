---
title: Active Directory のクライアント インストール プロパティ
titleSuffix: Configuration Manager
description: Active Directory Domain Services に Configuration Manager クライアント インストールのプロパティを発行します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692070"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Active Directory Domain Services に発行されたクライアント インストールのプロパティについて

*適用対象:Configuration Manager (Current Branch)*

Active Directory スキーマを Configuration Manager 用に拡張して、サイトが Active Directory Domain Services に公開されるとき、多くのクライアント インストール プロパティが Active Directory Domain Services に公開されます。 コンピューターでこれらのクライアント インストール プロパティを見つけることができる場合は、Configuration Manager クライアントの展開時にそれらを使用できます。  

 クライアント インストール プロパティの発行に Active Directory ドメイン サービスを使用すると、次の利点があります。  

-   ソフトウェアの更新ポイントベースのクライアント インストールとグループ ポリシーのクライアント インストールで、セットアップ パラメーターを各コンピューターで設定する必要がありません。  

-   この情報は自動的に生成されるため、インストール プロパティを手動で入力するために発生する人的ミスのリスクが排除されます。  

> [!NOTE]  
>  Configuration Manager 用に Active Directory スキーマを拡張する方法、およびサイトの公開方法の詳細については、「[System Center Configuration Manager のスキーマ拡張](../../plan-design/network/schema-extensions.md)」を参照してください。  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Active Directory Domain Services に発行されたクライアント インストール プロパティ  
クライアント インストール プロパティの一覧を次に示します。 以下の各項目の詳細については、[クライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)に関するページを参照してください。  

- Configuration Manager サイト コード。  

- サイト サーバー署名証明書。  

- 信頼されたルート キー。  

- HTTP おようび HTTPS 用のクライアント通信ポート。  

- フォールバック ステータス ポイント。 サイトに複数のフォールバック ステータス ポイントがある場合は、最初にインストールしたフォールバック ステータス ポイントのみが Active Directory Domain Services に発行されます。  

- クライアントが HTTPS のみを使用して通信する必要があることを示す設定。  

- PKI 証明書に関する設定:  

  -   クライアントの PKI 証明書を使用するかどうか。  

  -   証明書の選択条件。 これは、Configuration Manager に使用できる有効な PKI 証明書がクライアントに複数ある場合に必要になります。  

  -   どの証明書を使用するかを判断する設定（証明書選択プロセスの後に有効な証明書がクライアントに複数ある場合）。  

  -   信頼されたルート（CA）証明書の一覧を含む証明書発行者の一覧  

- ｃlient.msi インストール プロパティは、 **[クライアント プッシュ インストールのプロパティ]** ダイアログ ボックスの **[クライアント]** タブで指定します。

クライアント インストール (CCMSetup) では、次のいずれかを使用して指定されたプロパティが他にない場合にのみ、Active Directory Domain Services に発行されたプロパティを使用します。  

-   手動のインストール方法 (この記事で後述)

-   グループ ポリシーによるインストール方法 (この記事で後述)

> [!NOTE]  
>  クライアント インストールにはクライアント インストール プロパティを使用します。 これらのプロパティは、クライアントがインストールされて Configuration Manager サイトに割り当てられると、割り当てられたサイトの新しい設定で上書きされる場合があります。  

 どの Configuration Manager クライアント インストール方法で Active Directory Domain Services を使用してクライアント インストール プロパティを取得するかを判断するには、以下のセクションの詳細を使用します。  

## <a name="client-push-installation"></a>クライアント プッシュ インストール  
 クライアント プッシュ インストールでは、インストール　プロパティの取得に Active Directory ドメイン サービスは使用されません。  

 その代わりに、 **[クライアント プッシュ インストールのプロパティ]** ダイアログ ボックスの **[インストールのプロパティ]** タブで、クライアント インストール プロパティを指定することができます。 これらのオプションとクライアント関連のサイト設定は、クライアントがクライアント インストールの際に読み込むファイルに保存されています。  

> [!NOTE]  
>  クライアント プッシュ インストール、フォールバック ステータス ポイント、または信頼されたルート キーでは、 **[インストールのプロパティ]** タブで CCMSetup プロパティを設定する必要はありません。これらの設定はクライアント プッシュ インストールを使用してインストールをしたときに、自動で行われます。
Client.msi プロパティに加えて、CCMSetup では /forcereboot、/skipprereq、/logon、/BITSPriority、/downloadtimeout、/forceinstall の各パラメーターがサポートされます

 **[インストールのプロパティ]** タブで指定したプロパティは、サイトが Active Directory Domain Services に公開されると、Active Directory Domain Services に発行されます。 これらの設定は CCMSetup がインストール プロパティなしで実行されるクライアント インストールで読み込まれます。  

## <a name="software-update-point-based-installation"></a>ソフトウェアの更新ポイント経由のインストール  
 ソフトウェアの更新ポイント ベースのインストール方法では、CCMSetup コマンド ラインへのインストール プロパティの追加はサポートされていません。  

 グループ ポリシーを使用してクライアント コンピューターでコマンド ライン プロパティが提供されなかった場合は、CCMSetup は Active Directory ドメイン サービス でインストール プロパティを検索します。  

## <a name="group-policy-installation"></a>グループ ポリシーによるインストール  
 グループ ポリシーのインストール方法では、CCMSetup コマンド ラインへのインストール プロパティの追加はサポートされていません。  

 クライアント コンピューターでコマンド ライン プロパティが提供されなかった場合は、CCMSetup は Active Directory ドメイン サービス でインストール プロパティを検索します。  

## <a name="manual-installation"></a>手動インストール  
 CCMSetup は、次の状況で Active Directory ドメイン サービスのインストール プロパティを検索します。  

-   CCMSetup.exe コマンドの後にコマンド ライン プロパティが指定されていない。  

-   コンピューターにグループ ポリシーを使用してインストール プロパティが提供されていない。  

## <a name="logon-script-installation"></a>ログオン スクリプトによるインストール  
 CCMSetup は、次の状況で Active Directory ドメイン サービスのインストール プロパティを検索します。  

-   CCMSetup.exe コマンドの後にコマンド ライン プロパティが指定されていない。  

-   コンピューターにグループ ポリシーを使用してインストール プロパティが提供されていない。  

## <a name="software-distribution-installation"></a>ソフトウェアの配布によるインストール  
 CCMSetup は、次の状況で Active Directory ドメイン サービスのインストール プロパティを検索します。  

-   CCMSetup.exe コマンドの後にコマンド ライン プロパティが指定されていない。  

-   コンピューターにグループ ポリシーを使用してインストール プロパティが提供されていない。  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Active Directory Domain Services にアクセスできないクライアントのインストール  
こうしたクライアント コンピューターは、Active Directory Domain Services から発行されたインストール プロパティを読み込むことも、プロパティにアクセスすることもできません。

 これらのクライアントには次のものがあります。  

-   ワークグループ コンピューター。  

-   Active Directory Domain Services に公開されていない Configuration Manager サイトに割り当てられたクライアント。  

-   インターネット上にあるときにインストールされたクライアント。  
