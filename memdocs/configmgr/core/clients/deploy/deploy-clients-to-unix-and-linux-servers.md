---
title: Unix または Linux クライアントを展開する
titleSuffix: Configuration Manager
description: Configuration Manager で UNIX または Linux サーバーにクライアントを展開する方法を説明します。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9e8e40a6bdfa129a03e6042985e4956ffb21b5c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906313"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Configuration Manager で UNIX および Linux サーバーにクライアントを展開する方法

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> バージョン 1902 以降の Configuration Manager では、Linux または UNIX クライアントはサポートされていません。 
> 
> Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。


Linux または UNIX サーバーを Configuration Manager で管理するには、その前に各 Linux または UNIX サーバー上に Linux および UNIX 用の構成マネージャー クライアントをインストールする必要があります。 各コンピューターでクライアントのインストールを手動で実行することも、シェル スクリプトを使用してクライアントをリモートでインストールすることもできます。 Configuration Manager では、Linux または UNIX サーバーのクライアント プッシュ インストールを使用することはできません。 必要に応じて、Linux または UNIX サーバーへのクライアントのインストールを自動化するように System Center Orchestrator の Runbook を構成することができます。  

 使用するインストール方法に関わりなく、インストール プロセスでは、インストール プロセスを管理するために **install** という名前のスクリプトを使用する必要があります。 このスクリプトは、Linux および UNIX 用クライアントをダウンロードするときに含まれます。  

 Linux および UNIX 用の構成マネージャー クライアントのインストール スクリプトでは、コマンド ライン プロパティがサポートされています。 一部のコマンド ライン プロパティは必須ですが、それ以外は省略可能です。 たとえば、クライアントをインストールするときに、サイトとその初期の連絡先の Linux または UNIX サーバーで使用するサイトの管理ポイントを指定する必要があります。 コマンド ライン プロパティの完全な一覧については、「[Linux サーバーおよび UNIX サーバーにクライアントをインストールするためのコマンド ライン プロパティ](#BKMK_CmdLineInstallLnUClient)」をご覧ください。  

 クライアントをインストールした後、Configuration Manager コンソールでクライアント設定を指定して、Windows ベースのクライアントと同じ方法でクライアント エージェントを構成します。 詳細については、「  [Linux および UNIX サーバーのクライアント設定](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU)」をご覧ください。  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a> クライアント インストール パッケージとユニバーサル エージェントについて  
 特定のプラットフォーム上に Linux および UNIX 用クライアントをインストールするには、クライアントをインストールするコンピューターに適したクライアント インストール パッケージを使用する必要があります。 適切なクライアント インストール パッケージは、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=47719)から各クライアントにダウンロードされるデータの一部として含まれています。 クライアント インストール パッケージに加え、クライアント ダウンロードには、各コンピューター上でクライアントのインストールを管理する **install** スクリプトも含まれています。  

 クライアントをインストールする場合は、使用するクライアント インストール パッケージに関係なく同じプロセスとコマンド ライン プロパティを使用できます。  

 Linux および UNIX 用の構成マネージャー クライアントの各リリースでサポートされるオペレーティング システム、プラットフォーム、およびクライアント インストール パッケージの詳細については、「[Linux and UNIX servers](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers)」 (Linux および UNIX サーバー) をご覧ください。  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a> Linux および UNIX サーバーにクライアントをインストールする  
 Linux および UNIX 用クライアントをインストールするには、各 Linux または UNIX コンピューターでスクリプトを実行します。 スクリプトは **install** という名前で、インストール動作を変更したり、クライアント インストール パッケージを参照したりするコマンド ライン プロパティがサポートされています。 クライアントには、インストール スクリプトとクライアントのインストール パッケージを配置する必要があります。 クライアント インストール パッケージには、特定の Linux または UNIX オペレーティング システムおよびプラットフォーム用の構成マネージャー クライアント ファイルが含まれています。
各クライアント インストール パッケージには、クライアントのインストールを完了するために必要なすべてのファイルが含まれており、Windows ベースのコンピューターとは異なり、管理ポイントまたはその他のソースの場所から追加ファイルがダウンロードされることはありません。  

 Linux および UNIX 用の構成マネージャー クライアントをインストールした後、コンピューターを再起動する必要はありません。 ソフトウェアのインストールが完了するとすぐには、クライアントが動作します。 コンピューターを再起動すると、構成マネージャー クライアントは自動的に再起動します。  

 インストール済みのクライアントは、ルート資格情報を実行します。 ルート資格情報は、ハードウェア インベントリを収集し、ソフトウェアの展開を行うために必要です。  

 次の形式のコマンドを使用します。  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install` は、Linux および UNIX 用クライアントをインストールするスクリプト ファイルの名前です。 このファイルには、クライアント ソフトウェアが付属しています。  

-   `-mp <computer>` では、クライアントによって使用される最初の管理ポイントを指定します。 例: `smsmp.contoso.com`  

-   `-sitecode <site code>` では、クライアントが割り当てられているサイト コードを指定します。 例: `S01`  

-   `<property #1> <property #2>` では、インストール スクリプトで使用するコマンド ライン プロパティを指定します。  

    > [!NOTE]  
    >  詳しくは、「[Linux サーバーおよび UNIX サーバーにクライアントをインストールするためのコマンド ライン プロパティ](#BKMK_CmdLineInstallLnUClient)」をご覧ください。  

-   **client installation package** は、このコンピューターのオペレーティング システム、バージョン、CPU アーキテクチャのクライアント インストール .tar パッケージの名前を指定します。 最後に、クライアント インストールの .tar ファイルを指定する必要があります。 例: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a> Linux および UNIX サーバーに構成マネージャー クライアントをインストールするには  

1.  Windows コンピューターで、管理する [Linux または UNIX サーバーの適切なクライアント ファイルをダウンロードします](https://www.microsoft.com/download/details.aspx?id=47719) 。  

2.  Windows コンピューターで自己解凍型の .exe ファイルを実行して、インストール スクリプトとクライアントのインストール .tar ファイルを抽出します。  

3.  **インストール** スクリプトおよび .tar ファイルを管理するサーバー上のフォルダーにコピーします。  

4.  UNIX または Linux サーバー上で次のコマンドを実行し、スクリプトをプログラムとして実行できるようにします: `chmod +x install`  

    > [!IMPORTANT]  
    >  ルート資格情報を使用すると、クライアントをインストールするのに必要があります。  

5.  次に、次のコマンドを実行して、構成マネージャー クライアントをインストールします。`./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     このコマンドを入力する場合は、必要なその他のコマンド ライン プロパティを使用します。 コマンド ライン プロパティの一覧については、「[Linux サーバーおよび UNIX サーバーにクライアントをインストールするためのコマンド ライン プロパティ](#BKMK_CmdLineInstallLnUClient)」をご覧ください  

6.  スクリプトを実行した後は、 **/var/opt/microsoft/scxcm.log** ファイルを確認することで、インストールを検証します。 さらに、Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノードでクライアントの詳細を表示することによって、クライアントがインストールされ、サイトと通信していることを確認できます。  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a> Linux サーバーおよび UNIX サーバーにクライアントをインストールするためのコマンド ライン プロパティ  
 次のプロパティを使って、インストール スクリプトの動作を変更することができます。  

> [!NOTE]  
>  サポートされているプロパティのこの一覧を表示するには、`-h` プロパティを使用します。  

-   `-mp <server FQDN>`  

     必須。 クライアントが最初の接続ポイントとして使用する管理ポイント サーバーの FQDN を指定します。  

    > [!IMPORTANT]  
    >  このプロパティでは、インストール後にクライアントが割り当てられる管理ポイントは指定しません。  

    > [!NOTE]  
    >  `-mp` プロパティを使用して HTTPS クライアント接続のみを受け入れるように構成された管理ポイントを指定する場合は、`-UsePKICert` プロパティも使用する必要があります。  

-   `-sitecode <sitecode>`  

     必須。 構成マネージャー クライアントを割り当てる Configuration Manager プライマリ サイトを指定します。 例: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     任意。 状態メッセージを送信するクライアントが使用するフォールバック ステータス ポイント サーバーの FQDN を指定します。 詳しくは、[フォールバック ステータス ポイントが必要かどうかの判断](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)に関する記事をご覧ください。  

-   `-dir <directory>`  

     任意。 構成マネージャー クライアント ファイルをインストールする別の場所を指定します。 既定では、次の場所にインストールされます。`/opt/microsoft`  

-   `-nostart`  

     任意。 クライアントのインストールが完了した後、構成マネージャー クライアント サービス (**ccmexec.bin**) が自動的に起動しないようにします。  

     クライアントのインストール後に、クライアント サービスを手動で開始する必要があります。  

     既定では、クライアント サービスは、クライアントのインストールが完了すると、し、毎回、コンピューターの再起動した後を開始します。  

-   `-clean`  

     任意。 新規インストールを開始する前に、Linux および UNIX では、すべてのクライアントのファイルと、以前にインストールしたクライアントからのデータの削除を指定します。 このアクションにより、クライアントのデータベースと証明書ストアが削除されます。  

-   `-keepdb`  

     任意。 クライアントのローカル データベースを保持し、クライアントを再インストールするときに再利用することを指定します。 既定では、クライアントを再インストールすると、このデータベースが削除されます。  

-   `-UsePKICert <parameter>`  

     任意。 公開キーの証明書標準 (PKCS #12) 形式では、X.509 の PKI 証明書に完全なパスとファイル名を指定します。 この証明書は、クライアント認証に使用されます。 証明書がインストール時に指定されていない場合、また証明書を追加または変更する必要がある場合、 **certutil** ユーティリティを使用します。 詳しくは、「[Linux および UNIX 用のクライアントで証明書を管理する方法](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts)」をご覧ください。  

     `-UsePKICert` を使用するときは、`-certpw` コマンド ライン パラメーターを使用して、PKCS#12 ファイルに関連付けられているパスワードも指定する必要があります。  

     このプロパティを使用して PKI 証明書を指定しないと、クライアントでは自己署名証明書が使用され、サイト システムへのすべての通信は HTTP 経由で行われます。  

     無効な証明書を指定する場合は、コマンドラインのインストール、クライアント、エラーは返されません。 証明書の検証は、クライアントのインストールの後で行われます。 クライアントの起動時に、管理ポイントで証明書が検証されます。 証明書の検証が失敗した場合、**scxcm.log** に「**Failed validate the certificate for Management Point**」(管理ポイントでの証明書の検証が失敗しました) というメッセージが表示されます。 既定のログ ファイルの場所は、  **/var/opt/microsoft/scxcm.log**です。  

     > [!NOTE]  
     > クライアントをインストールし、`-mp` プロパティを使用して HTTPS クライアント接続のみを許可するように構成された管理ポイントを指定する場合は、このプロパティを指定する必要があります。  

     例: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     任意。 `-UsePKICert` プロパティを使用して指定した PKCS #12 ファイルに関連付けられているパスワードを指定します。  

     例: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     任意。 PKI 証明書を使用して HTTPS で通信するときは、クライアントが証明書失効リスト (CRL) をチェックしないように指定します。 このオプションを指定しないと、クライアントでは、PKI 証明書を使用して HTTPS 接続を確立する前に、CRL がチェックされます。 詳細については、クライアントの CRL チェック、PKI 証明書失効の計画を参照してください。  

     例: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     任意。 Configuration Manager の信頼されたルート キーへの完全パスとファイル名を指定します。 Configuration Manager の信頼されたルート キーは、適切な階層に属しているサイト システムに接続されていることを確認するために Linux および UNIX クライアントで使用されるメカニズムを提供します。  

     コマンド ラインで信頼されたルート キーを指定しない場合、クライアントは、通信する最初の管理ポイントを信頼し、その管理ポイントから信頼されたルート キーを自動的に取得します。  

     詳細については、「[Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。  

     例: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     任意。 クライアントが HTTP 経由で、管理ポイントと通信する際に使用する管理ポイントに構成されているポートを指定します。 ポートが指定されていない場合は、既定値の 80 が使用されます。  

     例: `-httpport 80`  

-   `-httpsport <port>`  

     任意。 クライアントが HTTPS 経由で、管理ポイントと通信する際に使用する管理ポイントに構成されているポートを指定します。 ポートが指定されていない場合は、既定値の 443 が使用されます。  

     例: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     任意。 クライアントのインストールで sha-256 検証をスキップすることを指定します。 SHA-256 をサポートする OpenSSL のバージョンがリリースされていないオペレーティング システムにクライアントをインストールする場合に、このオプションを使用します。 詳しくは、[SHA-256 をサポートしていない Linux および UNIX オペレーティング システム](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256)に関する記事をご覧ください。  

-   `-signcertpath <file location>`  

     任意。 完全パスを指定し、 **.cer** サイト サーバーにエクスポートされた自己署名証明書のファイル名。 PKI 証明書を使用できない場合、Configuration Manager サイト サーバーでは自己署名証明書が自動的に生成されます。  

     これらの証明書を使用して、目的のサイトから管理ポイントからダウンロードするクライアント ポリシーが送信されたことを検証します。 自己署名証明書がインストール時に指定されていない場合、また証明書を変更する必要がある場合、 **certutil** ユーティリティを使用します。 詳しくは、「[Linux および UNIX 用のクライアントで証明書を管理する方法](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts)」をご覧ください。  

     この証明書は、 **SMS** 証明書ストアから取得することができます。サブジェクト名は **Site Server** 、フレンドリ名は **Site Server Signing Certificate**です。  

     インストールの間にこのオプションを指定しないと、Linux および UNIX クライアントでは、最初に通信した管理ポイントを信頼します。 その管理ポイントから署名証明書が自動的に取得されます。  

     例: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     任意。 管理ポイントの証明機関 (CA) 階層の一部ではない、インポートする追加の PKI 証明書を指定します。 コマンドラインで複数の証明書を指定する場合は、コンマ区切りがあります。  

     サイト管理ポイントによって信頼されているルート CA 証明書にチェーンされない PKI クライアントの証明書を使用する場合は、このオプションを使用します。 クライアント証明書がサイトの証明書発行者リストの信頼されたルート証明書にチェーンされていない場合、管理ポイントはそのクライアントを拒否します。  

     このオプションを使用しない場合、Linux および UNIX クライアントは、`-UsePKICert` オプションの証明書のみを使用して信頼階層を検証します。  

     例: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a> Linux および UNIX サーバーからクライアントをアンインストールする  
 Linux および UNIX 用の構成マネージャー クライアントをアンインストールするには、アンインストール ユーティリティ **uninstall** を使用します。 既定では、このファイルにある、 **/選択/microsoft/configmgr/bin/** 、クライアント コンピューター上のフォルダーです。 この uninstall コマンドでは、コマンド ライン パラメーターはサポートされておらず、クライアント ソフトウェアに関連するすべてのファイルがサーバーから削除されます。  

 クライアントをアンインストールするには、次のコマンドラインを使用します **/opt/microsoft/configmgr/bin/uninstall**。  

 Linux および UNIX 用の構成マネージャー クライアントをアンインストールした後、コンピューターを再起動する必要はありません。  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a> Linux および UNIX 用のクライアントの要求ポートを構成します。  
 Windows ベースのクライアントと同様に、Linux および UNIX 用の構成マネージャー クライアントは、HTTP および HTTPS を使用して Configuration Manager サイト システムと通信します。 構成マネージャー クライアントが通信に使用するポートは、要求ポートと呼ばれます。  

 Linux および UNIX 用の構成マネージャー クライアントをインストールするときに、 **-httpport** および **-httpsport** インストール プロパティを指定することによって、クライアントの既定の要求ポートを変更することができます。 インストールのプロパティとカスタム値を指定しなかった場合、クライアントでは既定値が使用されます。 既定値は **80** HTTP トラフィック用と **443** HTTPS トラフィック用です。  

 クライアントをインストールした後で、要求ポートの構成を変更することはできません。 代わりに、ポートの構成を変更するには、クライアントを再インストールし、新しいポートの構成を指定する必要があります。 クライアントを再インストールして要求ポート番号を変更するときは、新しいクライアントをインストールするときと同様、**install** コマンドを実行しますが、追加のコマンド ライン プロパティ **-keepdb** を使用します。 このスイッチは、クライアント データベースおよびクライアントの GUID と証明書ストアを含むファイルを保持するよう、インストールに指示します。  

 クライアント通信のポート番号の詳細については、[クライアント通信ポートの構成方法](../../../core/clients/deploy/configure-client-communication-ports.md)に関するページを参照してください。  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a> 管理ポイントを探すには、Linux および UNIX 用クライアントを構成します。  
 Linux および UNIX 用の構成マネージャー クライアントをインストールする場合、最初の接続ポイントとして使用する管理ポイントを指定する必要があります。  

 Linux および UNIX 用の構成マネージャー クライアントは、クライアントのインストール時にこの管理ポイントに接続します。 クライアントによる管理ポイントへの接続が失敗した場合、クライアント ソフトウェアは成功するまで試行し続けます。  

 クライアントが管理ポイントを検出する方法の詳細については、「 [管理ポイントを検出する](assign-clients-to-a-site.md#locating-management-points)」を参照してください。
