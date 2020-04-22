---
title: Linux および UNIX コンピューターへのクライアント展開の計画
titleSuffix: Configuration Manager
description: Configuration Manager で Linux コンピューターおよび UNIX コンピューターへのクライアント展開を計画します。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693730"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Configuration Manager での Linux コンピューターおよび UNIX コンピューターへのクライアント展開の計画

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> バージョン 1902 以降の Configuration Manager では、Linux または UNIX クライアントはサポートされていません。 
> 
> Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。

Configuration Manager クライアントは、Linux または UNIX を実行しているコンピューターにインストールできます。 このクライアントは、ワークグループ コンピューターとして動作するサーバー用に設計されており、ログオンしたユーザーとの対話はサポートしていません。 クライアント ソフトウェアをインストールし、クライアントが Configuration Manager サイトとの通信を確立した後で、Configuration Manager コンソールとレポートを使用して、クライアントを管理します。  

> [!NOTE]
>  Linux および UNIX コンピューター向けの Configuration Manager クライアントでは、次の管理機能はサポートされていません。  
> 
> - クライアント プッシュ インストール  
>   -   オペレーティング システムの展開  
>   -   アプリケーションの展開 (代わりに、パッケージとプログラムを使ってソフトウェアを展開)  
>   -   ソフトウェア インベントリ  
>   -   ソフトウェア更新プログラム  
>   -   コンプライアンス設定  
>   -   リモート コントロール  
>   -   電源管理  
>   -   クライアント ステータスのクライアント チェックと修復  
>   -   インターネット ベースのクライアント管理  

 サポートされる Linux ディストリビューションと UNIX ディストリビューション、および Linux と UNIX 用のクライアントをサポートするために必要となるハードウェアについては、「[System Center Configuration Manager の推奨ハードウェア](../../../../core/plan-design/configs/recommended-hardware.md)」を参照してください。  

 この記事の情報を使用して、Linux および UNIX 用のConfiguration Manager クライアントの展開の計画に役立てます。  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a> Linux および UNIX サーバーへのクライアントの展開の前提条件  
 前提条件が正常に適切な場所にいる必要がありますが Linux および UNIX 用クライアントをインストールするのにには、次の情報を使用します。  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a> Configuration Manager 外部の依存関係:  
 次の表は、必要な UNIX および Linux オペレーティング システムおよびパッケージ依存関係を示しています。  

 **Red Hat Enterprise Linux Server リリース 5.1 (Tikanga)**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|glibc|C 標準ライブラリ|2.5-12|  
|Openssl|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル|0.9.8b-8.3.el5|  
|PAM|プラグ可能な認証モジュール|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server リリース 6**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|glibc|C 標準ライブラリ|2.12-1.7|  
|Openssl|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル|1.0.0-4|  
|PAM|プラグ可能な認証モジュール|1.1.1-4|  

 **Red Hat Enterprise Linux Server リリース 7**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|glibc|C 標準ライブラリ|2.17|  
|Openssl|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル|1.0.1|  
|PAM|プラグ可能な認証モジュール|1.1.1-4|  

 **Solaris 10 SPARC**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|必要なオペレーティング システムの修正プログラム|PAM メモリ リーク|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking Libraries (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|SUNopenssl-librararies (Usr)<br /><br /> Sun は Solaris 10 SPARC の OpenSSL ライブラリを提供しています。 これらは、オペレーティング システムにバンドルされています。|11.10.0,REV=2005.01.21.15.53|  
|PAM|プラグ可能な認証モジュール<br /><br /> SUNWcsr、Core Solaris、(Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|必要なオペレーティング システムの修正プログラム|PAM メモリ リーク|117464-04|  
|SUNWlibC|Sun Workshop コンパイラー バンドル libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris、(共有 Libs) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Core Solaris ライブラリ (ルート) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|SUNWopenssl ライブラリです。OpenSSL ライブラリ (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|プラグ可能な認証モジュール<br /><br /> SUNWcsr Core Solaris、(Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop コンパイラー バンドル libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking ライブラリ (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris ライブラリ (ルート)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris、(共有 Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris (ルート)|11.11, REV=2009.11.11|  
|SUNWopenssl-ライブラリ|SUNopenssl ライブラリ (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop コンパイラー バンドル libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking ライブラリ (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris ライブラリ (ルート)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris、(共有 Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris (ルート)|11.11, REV=2009.11.11|  
|SUNWopenssl-ライブラリ|SUNopenssl ライブラリ (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|glibc-2.4-31.30|C 標準共有ライブラリ|2.4-31.30|  
|Openssl|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル|0.9.8a-18.15|  
|PAM|プラグ可能な認証モジュール|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|C 標準共有ライブラリ|2.9-13.2|  
|PAM|プラグ可能な認証モジュール|pam-1.0.2-20.1|  

 **Universal Linux (Debian パッケージ) Debian、Ubuntu サーバー**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|libc6|C 標準共有ライブラリ|2.3.6|  
|Openssl|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル|0.9.8 または 1.0|  
|PAM|プラグ可能な認証モジュール|0.79-3|  

 **Universal Linux (RPM パッケージ) CentOS、Oracle Linux**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|glibc|C 標準共有ライブラリ|2.5-12|  
|Openssl|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル|0.9.8 または 1.0|  
|PAM|プラグ可能な認証モジュール|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|OS のバージョン|オペレーティング システムのバージョン|AIX 6.1: 任意のテクノロジ レベルとサービス パック|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|OS のバージョン|オペレーティング システムのバージョン|AIX 7.1: 任意のテクノロジ レベルとサービス パック|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル||  


 **HP-UX 11i v3 IA64**  

|必須パッケージ|[説明]|最小バージョン|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX 基本操作環境|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|特定 IA 開発のライブラリ|B.11.31|  
|SysMgmtMin|最小ソフトウェア展開ツール|B.11.31.0709|  
|SysMgmtMin.openssl|OpenSSL ライブラリ、セキュア ネットワーク通信プロトコル|A.00.09.08d.002|  
|PAM|プラグ可能な認証モジュール|HP-UX では、PAM はコア オペレーティング システム コンポーネントの一部です。 これ以外には依存関係はありません。|  

 **Configuration Manager の依存関係:** 次の表に、Linux および UNIX クライアントをサポートするサイト システムの役割を示します。 これらのサイト システムの役割の詳細については、「[Configuration Manager クライアントのサイト システムの役割の決定](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)」を参照してください。  

|Configuration Manager サイト システム|説明|  
|---------------------------------------|----------------------|  
|管理ポイント|Linux および UNIX 用の Configuration Manager クライアントをインストールするのに管理ポイントは必要ありませんが、クライアント コンピューターと Configuration Manager サーバーの間で情報を転送するには管理ポイントが必要です。 管理ポイントがないと、クライアント コンピューターを管理できません。|  
|配布ポイント|Linux および UNIX 用の Configuration Manager クライアントをインストールするのに配布ポイントは必要ありません。 ただし、Linux および UNIX サーバーにソフトウェアを展開する場合は、サイト システムの役割が必要です。<br /><br /> Linux および UNIX 用の Configuration Manager クライアントは SMB を使用する通信をサポートしないため、クライアントで使用する配布ポイントは HTTP または HTTPS 通信をサポートしている必要があります。|  
|フォールバック ステータス ポイント|Linux および UNIX 用の Configuration Manager クライアントをインストールするのにフォールバック ステータス ポイントは必要ありません。 ただし、Configuration Manager サイトのコンピューターは、管理ポイントとやり取りできないときに、フォールバック ステータス ポイントを使用して状態メッセージを送信できます。 クライアントでは、フォールバック ステータス ポイントにもインストール ステータスを送信できます。|  

 **ファイアウォールの要件**:ファイアウォールがクライアントの要求ポートとして指定するポートの間で通信をブロックしないことを確認します。 Linux および UNIX 用のクライアントは、管理ポイント、配布ポイント、フォールバック ステータス ポイントと直接通信します。  

 クライアントの通信および要求のポートの詳細については、「  [管理ポイントを検出するために Linux および UNIX 用のクライアントを構成する](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP)」を参照してください。  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a> Linux および UNIX サーバーのフォレストの信頼間の通信の計画  
 Configuration Manager で管理する Linux および UNIX サーバーはワークグループ クライアントとして動作するため、ワークグループに含まれる Windows ベースのクライアントと同様の構成が必要です。 ワークグループに含まれるコンピューターからの通信については、「[複数の Active Directory フォレスト間での通信](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest)」をご覧ください。  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a> Linux および UNIX 用のクライアントによるサービスの場所  
 クライアントにサービスを提供するサイト システム サーバーを特定のタスクは、サービスの場所と呼ばれます。 Windows ベースのクライアントと異なり、Linux および UNIX 用クライアントでは、サービスの場所の Active Directory は使用されません。 さらに、Linux および UNIX 用の Configuration Manager クライアントでは、管理ポイントのドメイン サフィックスを指定するクライアント プロパティはサポートされていません。 代わりに、クライアントは、クライアント ソフトウェアをインストールするときに割り当てる、既知の管理ポイントからクライアントにサービスを提供する追加のサイト システム サーバーについて学習します。  

 詳しくは、「[ サービスの場所とクライアントが割り当てられた管理ポイントを特定する方法](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)」をご覧ください。  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a> Linux および UNIX サーバーのセキュリティと証明書の計画  
 Configuration Manager サイトとセキュリティで保護された認証済みの通信を行うために、Linux および UNIX 用の Configuration Manager クライアントは、Windows 用の Configuration Manager クライアントと同じ通信モデルを使用します。  

 Linux および UNIX クライアントのインストール時に、Configuration Manager サイトとの HTTPS を使用した通信を可能にする PKI 証明書をクライアントに割り当てることができます。 PKI 証明書を割り当てないと、クライアントでは自己署名証明書が作成され、通信は HTTP のみで行われます。  

 インストールするときに、PKI 証明書を用意されているクライアントは、管理ポイントと通信するために、HTTPS を使用します。 クライアントは、HTTPS をサポートするための管理ポイントを見つけることが場合、は、指定された PKI 証明書で HTTP を使用するフォールバックはします。  

 Linux または UNIX クライアント PKI 証明書を使用するときに、それらを承認する必要はありません。 クライアントが自己署名証明書を使用する場合は、Configuration Manager コンソールで階層設定を確認してクライアントを承認する必要があります。 クライアントの認証方法がない場合 **(推奨されません) のすべてのコンピューターを自動的に承認**, 、クライアントを手動で承認する必要があります。  

 クライアントを手動で承認する方法について詳しくは、「[[デバイス] ノードを使用してクライアントを管理する](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)」をご覧ください。  

 Configuration Manager で証明書を使用する方法については、「[PKI 証明書の要件](../../../plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a> Linux および UNIX サーバーで使用するための証明書について  
 Linux および UNIX 用の Configuration Manager クライアントは、Windows ベースのクライアントと同じように自己署名証明書または X.509 PKI 証明書を使用します。 Linux および UNIX クライアントを管理する際の Configuration Manager サイト システムの PKI 要件に変更はありません。  

 Configuration Manager サイト システムと通信する Linux および UNIX クライアントに使用する証明書は、公開キー証明書標準 (PKCS #12) 形式でなければなりません。また、パスワードは、PKI 証明書を指定するときにクライアントに指定できるように既知である必要があります。  

 Linux および UNIX 用の Configuration Manager クライアントでは、単一の PKI 証明書がサポートされており、複数の証明書はサポートされていません。 したがって、Configuration Manager サイトに構成する証明書の選択基準は適用されません。  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a> Linux および UNIX サーバーの証明書の構成  
 HTTPS 通信を使用するように Linux および UNIX サーバー対応の Configuration Manager クライアントを構成するには、クライアントのインストール時に、PKI 証明書を使用するようにクライアントを構成する必要があります。 クライアント ソフトウェアのインストール前に証明書をプロビジョニングすることはできません。  

 PKI 証明書を使用するクライアントをインストールするときは、コマンド ライン パラメーター `-UsePKICert` を使用して、PKI 証明書が含まれている PKCS#12 ファイルの場所と名前を指定します。 さらに、コマンドライン パラメーター `-certpw` を使用して、証明書のパスワードを指定する必要もあります。  

 `-UsePKICert` を指定しないと、クライアントでは自己署名証明書が生成され、HTTP のみを使用してサイト システム サーバーとの通信が試みられます。  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a> SHA-256 をサポートしていないバージョン  
 Configuration Manager のクライアントとしてサポートされている以下の Linux および UNIX オペレーティング システムは、SHA-256 をサポートしないバージョンの OpenSSL でリリースされました。  

-   Solaris バージョン 10 (SPARC/x86)  


 これらのオペレーティング システムを Configuration Manager で管理するには、クライアントに SHA-256 の検証をスキップするよう指示するコマンド ライン スイッチを使用して、Linux および UNIX 用の Configuration Manager クライアントをインストールする必要があります。 これらのオペレーティング システム バージョンで実行される Configuration Manager クライアントは、SHA-256 をサポートしているクライアントに比べ、安全性の低いモードで動作します。 このような安全性の低い操作モードには、次のような動作があります。  

-   クライアントでは、管理ポイントから要求するポリシーに関連付けられているサイト サーバー署名は検証されません。  

-   クライアントでは、配布ポイントからダウンロードしたパッケージのハッシュは検証されません。  

> [!IMPORTANT]  
>  `ignoreSHA256validation` オプションを使用して、Linux および UNIX コンピューター用のクライアントを低セキュリティの保護モードで実行することができます。 これは sha-256 のサポートが含まれていません古いプラットフォームで使用するためのものです。 これはセキュリティ設定をオーバーライドするため、Microsoft では推奨していませんが、セキュリティで保護された信頼できるデータ センター環境で使用するためにサポートされています。  

 Linux および UNIX 用の Configuration Manager クライアントをインストールする際に、インストール スクリプトがオペレーティング システムのバージョンを確認します。 既定では、オペレーティング システムのバージョンが SHA-256 をサポートしているバージョンの OpenSSL でリリースされていないことが識別されると、Configuration Manager クライアントのインストールが失敗します。  

 SHA-256 をサポートするバージョンの OpenSSL でリリースされていない Linux および UNIX オペレーティング システムに Configuration Manager クライアントをインストールするには、インストール コマンド ライン スイッチ `ignoreSHA256validation` を使用する必要があります。 このコマンド ライン オプションを該当する Linux または UNIX オペレーティング システムで使用すると、Configuration Manager クライアントは SHA-256 の検証をスキップします。この場合、インストール後のクライアントは、HTTP を使用してサイト システムに送信するデータに SHA-256 を使用して署名しません。 証明書を使用するように Linux および UNIX クライアントを構成する方法については、「[Linux および UNIX サーバーのセキュリティと証明書の計画](#BKMK_SecurityforLnU)」をご覧ください。 SHA-256 の要求について詳しくは、「[署名と暗号化の構成](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption)」をご覧ください。  

> [!NOTE]  
>  コマンド ライン オプション `ignoreSHA256validation` は、SHA-256 がサポートされるバージョンの OpenSSL と共にリリースされた Linux および UNIX のバージョンを実行しているコンピューターでは無視されます。  
