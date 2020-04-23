---
title: スキーマ拡張
titleSuffix: Configuration Manager
description: Configuration Manager をサポートするように Active Directory スキーマを拡張します。
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c78bb5876455e68292e4a69d86a256fa9e5172d0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701470"
---
# <a name="schema-extensions-for-configuration-manager"></a>Configuration Manager のスキーマ拡張

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager をサポートするように Active Directory スキーマを拡張することができます。 これにより、フォレストの Active Directory スキーマを編集し、新しいコンテナーといくつかの属性を追加します。これらは、Configuration Manager サイトにより、キー情報を Active Directory に発行するために使用されます。Active Directory でクライアントは安全にキー情報を使用できます。 この情報はクライアントの展開と構成を簡略化し、クライアントがサイト リソース (展開するコンテンツがあるサーバーや、クライアントに各種サービスを提供するサーバーなど) を見つけるときに役立ちます。  

-   Active Directory スキーマは拡張することをお勧めしますが、必須ではありません。  

[Active Directory スキーマを拡張する](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema)前に、Active Directory ドメイン サービスに精通し、 [Active Directory スキーマの変更](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx)に慣れておく必要があります。  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Configuration Manager 向けの Active Directory スキーマの拡張に関する考慮事項  

-   Configuration Manager 用の Active Directory スキーマの拡張は、Configuration Manager 2007 と Configuration Manager 2012 で使用されているものから変更されていません。 どちらかのバージョンでスキーマを拡張した場合は、もう一度拡張する必要はありません。  

-   スキーマの拡張は、フォレスト全体で 1 回限り行う操作で、元に戻すことはできません。  

-   スキーマを拡張できるのは、スキーマ管理グループのメンバーと、スキーマを変更するのに十分なアクセス許可を委任されたユーザーのみです。  

-   スキーマの拡張を行うのは Configuration Manager のセットアップ実行の前でも後でも構いませんが、サイトと階層の設定の構成を始める前に行うことをお勧めします。 これによって、後で行う多くの構成手順が簡単になります。  

-   スキーマの拡張後、Active Directory グローバル カタログがフォレスト全体にレプリケートされます。 そのため、レプリケーションのトラフィックにより、ネットワークに依存する他のプロセスに悪影響が及ばない時間帯に、スキーマの拡張をご計画ください。  

    -   Windows 2000 フォレストでは、スキーマを拡張するとグローバル カタログ全体が完全に同期化されます。  

    -   Windows 2003 フォレスト以降、新しく追加された属性だけが複製されます。  

**Active Directory スキーマを使用しないデバイスとクライアント:**  

-   Exchange Server コネクタで管理されているモバイル デバイス  

-   Mac コンピューター用クライアント  

-   Linux および UNIX サーバー用クライアント  

-   Configuration Manager に登録されたモバイル デバイス  

-   Microsoft Intune で登録されるモバイル デバイス  

-   モバイル デバイス レガシ クライアント  

-   インターネットのみのクライアント管理用に構成した Windows クライアント  

-   Configuration Manager でインターネットで検出される Windows クライアント  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>スキーマの拡張によってメリットを受ける機能  
**クライアント コンピューターのインストールとサイトの割り当て** - Windows コンピューターに新しいクライアントがインストールされると、クライアントが Active Directory Domain Services を検索して、インストールのプロパティを見つけます。  

-   **回避策:** スキーマを拡張しない場合は、次のいずれかのオプションを使って、コンピューターにインストールが必要な構成詳細を提示する必要があります。  

    -   **クライアント プッシュ インストールを使用する**。 クライアント インストール方法を使用する前に、すべての前提条件が満たされていることを確認してください。 詳細については、「[Windows コンピューターにクライアントを展開するための前提条件](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)」の「インストール方法の依存関係」セクションを参照してください。  

    -   **クライアントを手動でインストールし**、CCMSetup インストールのコマンドライン プロパティを使用してクライアント インストールのプロパティを指定する。 以下の手順を実行する必要があります。  

        -   クライアントのインストール時に CCMSetup コマンド ラインで、CCMSetup プロパティ **/mp:=&lt;管理ポイント名のコンピューター名\>** または **/source:&lt; クライアント ソース ファイルへのパス\>** を使用して、インストール ファイルのダウンロード元となる管理ポイントまたはソース パスを指定します。  

        -   クライアントがサイトを割り当て、クライアントのポリシーとサイト設定をダウンロードするために必要となる初期管理ポイントのリストを指定します。 その際、CCMSetup Client.msi プロパティ SMSMP を使用してください。  

    -   **DNS または WINS に管理ポイントを発行** し、このサービスの場所の方法を使用するようにクライアントを構成します。  

**クライアント - サーバー間の通信用のポート構成** - クライアントのインストール時に、Active Directory に格納されているポート情報によって構成されます。 その後にサイトのクライアント - サーバー間の通信ポートが変更された場合は、クライアントは Active Directory Domain Services からこの新しいポート設定を取得できます。  

-   **回避策:** スキーマを拡張しない場合、以下のいずれかのオプションを使用して既存のクライアントに新しいポート構成を提供します。  

    -   新しいポートを構成するオプションを使用して**クライアントを再インストール**します。  

    -   **ポート情報を更新するカスタム スクリプトをクライアントに展開します**。 ポートが変更されたためにクライアントがサイトと通信できない場合は、Configuration Manager を使用してこのスクリプトを展開することはできません。 たとえば、グループ ポリシーを使用できます。  

**コンテンツの展開方法** - 特定のサイトでコンテンツを作成し、そのコンテンツを階層内の別のサイトに展開する場合、受信側のサイトは署名付きコンテンツ データの署名を検証する必要があります。 そのためには、データの作成元のソース サイトの公開キーへのアクセスが必要となります。 Configuration Manager 用に Active Directory スキーマを拡張すると、サイトの公開キーが階層内の全サイトでアクセス可能になります。  

-   **回避策:** スキーマを拡張しない場合は、階層のメンテナンス ツール **preinst.exe** を使用して、サイト間でセキュリティ キー情報を交換します。  

     たとえば、プライマリ サイトでコンテンツを作成し、別のプライマリ サイト下にあるセカンダリ サイトにそのコンテンツを展開する場合は、セカンダリ サイトでソース プライマリ サイトの公開キーを取得できるように Active Directory スキーマを拡張するか、preinst.exe を使用して 2 つのサイト間で直接キーを共有することができます。  

## <a name="active-directory-attributes-and-classes"></a>Active Directory 属性とクラス  
Configuration Manager のスキーマを拡張すると、次のクラスと属性がスキーマに追加され、Active Directory フォレスト内のすべての Configuration Manager サイトで利用できるようになります。  

-   属性:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        場所:  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   クラス:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]
> 
>  スキーマの拡張には、旧バージョンの製品から継承されたものの、Configuration Manager では使用されなくなった属性とクラスが含まれる場合があります。 次に例を示します。  
> 
> 
> - 属性: cn=MS-SMS-Site-Boundaries  
>   -   クラス: cn=MS-SMS-Server-Locator-Point  

上記のリストが最新のものであることをご確認ください。そのためには、Configuration Manager インストール メディアの **\SMSSETUP\BIN\x64** フォルダーから **ConfigMgr_ad_schema.LDF** ファイルを確認します。  
