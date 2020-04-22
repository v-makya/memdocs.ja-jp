---
title: Windows クライアントのファイアウォールとポートの設定
titleSuffix: Configuration Manager
description: Configuration Manager のクライアント用に Windows ファイアウォールとポートの設定を選択します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2290899c0159221c5f45ce6c34332b766984e4c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694780"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-configuration-manager"></a>Configuration Manager のクライアント用の Windows ファイアウォールとポートの設定

*適用対象:Configuration Manager (Current Branch)*

Windows ファイアウォールを実行する Configuration Manager のクライアント コンピューターは、サイトとの通信のためにしばしば例外の構成を必要とします。 構成が必要な例外は、構成マネージャー クライアントで使用する管理機能によって異なります。  

 こうした管理機能を特定し、Windows ファイアウォールで例外を構成する方法の詳細については、次のセクションを参照してください。  

##  <a name="modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> Windows ファイアウォールが許可するポートおよびプログラムの変更  
 構成マネージャー クライアント用に Windows ファイアウォール上のポートやプログラムを変更するには、次の手順に従います。  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Windows ファイアウォールが許可するポートおよびプログラムを変更するには  

1.  Windows ファイアウォールを実行しているコンピューターで、コントロール パネルを開きます。  

2.  **[Windows ファイアウォール]** を右クリックし、 **[開く]** をクリックします。  

3.  必要な例外と、必要なカスタム プログラムやポートを構成します。  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Configuration Manager で必要なプログラムとポート  
 次の Configuration Manager 機能では、Windows ファイアウォールで例外を設定する必要があります。  

### <a name="queries"></a>クエリ  
 Windows ファイアウォールを実行するコンピューターで Configuration Manager コンソールを実行する場合、初回実行時のクエリは失敗し、statview.exe のブロックを解除するかどうかを尋ねるダイアログ ボックスが表示されます。 statview.exe のブロックを解除すると、その後のクエリはエラーなしで実行されます。 また、クエリを実行する前に、Windows ファイアウォールの **[例外]** タブで、プログラムおよびサービスの一覧に statview.exe を手動で追加することもできます。  

### <a name="client-push-installation"></a>クライアント プッシュ インストール  
 クライアント プッシュを使用して構成マネージャー クライアントをインストールするには、Windows ファイアウォールに次の例外を追加する必要があります。  

-   送信および受信: **ファイルとプリンターの共有**  

-   受信: **Windows Management Instrumentation (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>グループ ポリシーを使用したクライアント インストール  
 グループ ポリシーを使用して構成マネージャー クライアントをインストールするには、Windows ファイアウォールに例外として **[ファイルとプリンターの共有]** を追加します。  

### <a name="client-requests"></a>クライアントの要求  
 クライアント コンピューターが Configuration Manager サイト システムと通信するには、Windows ファイアウォールに次の例外を追加する必要があります。  

 送信: TCP ポート **80** (HTTP 通信用)  

 送信: TCP ポート **443** (HTTPS 通信用)  

> [!IMPORTANT]  
>  これらは既定のポート番号で、Configuration Manager で変更できます。 詳細については、[クライアント通信ポートの構成方法](../../../core/clients/deploy/configure-client-communication-ports.md)に関するページを参照してください。 ポートを既定値から変更した場合は、対応する例外を Windows ファイアウォールに構成する必要があります。  

### <a name="client-notification"></a>クライアント通知  
 管理ユーザーが Configuration Manager コンソールでクライアント操作を選択したときに、管理ポイントからクライアント コンピューターに対して、実行する必要がある操作 (コンピューター ポリシーのダウンロード、マルウェア スキャンの開始など) を通知する場合、Windows ファイアウォールの例外として次を追加します。  

 送信: TCP ポート **10123**  

 この通信が成功しない場合、Configuration Manager は、代わりに既存のクライアントから管理ポイントへの HTTP または HTTPS 通信ポートを自動的に使用します。  

 送信: TCP ポート **80** (HTTP 通信用)  

 送信: TCP ポート **443** (HTTPS 通信用)  

> [!IMPORTANT]  
>  これらは既定のポート番号で、Configuration Manager で変更できます。 詳細については、[クライアント通信ポートの構成方法](../../../core/clients/deploy/configure-client-communication-ports.md)に関するページを参照してください。 ポートを既定値から変更した場合は、対応する例外を Windows ファイアウォールに構成する必要があります。  

### <a name="remote-control"></a>リモート コントロール  
 Configuration Manager リモート コントロールを使用するには、以下のポートを許可する必要があります。  

-   受信: TCP ポート **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>リモート アシスタンスおよびリモート デスクトップ  
 Configuration Manager コンソールからリモート アシスタンスを開始するには、クライアント コンピューターの Windows ファイアウォールで許可するプログラムおよびサービスの一覧に、カスタム プログラム **Helpsvc.exe** と受信カスタム ポート TCP **135** を追加します。 **リモート アシスタンス** および **リモート デスクトップ**も許可する必要があります。 クライアント コンピューターからリモート アシスタンスを開始する場合、Windows ファイアウォールは **リモート アシスタンス** と **リモート デスクトップ**を自動的に構成して許可します。  

### <a name="wake-up-proxy"></a>ウェイクアップ プロキシ  
 ウェイクアップ プロキシ クライアント設定を有効にすると、ConfigMgr ウェイクアップ プロキシという新しいサービスは、ピア間のプロトコルを使用して、サブネット上の他のコンピューターが起動しているかどうかを確認し、必要に応じて起動することができます。 この通信には次のポートを使用します。  

 送信: UDP ポート **25536**  

 送信: UDP ポート **9**  

 これらは既定のポート番号で、Configuration Manager では、 **[電源管理]** クライアント設定の **[ウェイクアップ プロキシのポート番号 (UDP)]** と **[Wake On LAN ポート番号 (UDP)]** を使用して変更できます。 **[電源管理]** を指定した場合、 **[ウェイクアップ プロキシ用の Windows ファイアウォールの例外です]** クライアント設定を指定すると、これらのポートは Windows ファイアウォールでクライアント用に自動的に構成されます。 ただし、クライアントが別のファイアウォールを実行する場合、これらのポート番号の例外を手動で構成する必要があります。  

 ウェイクアップ プロキシは、これらのポートに加え、クライアント コンピューター間の Internet Control Message Protocol (ICMP) のエコー要求メッセージも使用します。 この通信は、他のクライアント コンピューターがネットワークで起動しているかどうかを確認するために使用します。 ICMP は TCP/IP Ping コマンドとも呼ばれます。  

 ウェイクアップ プロキシの詳細については、[クライアントをウェイク アップする方法の計画](../../../core/clients/deploy/plan/plan-wake-up-clients.md)に関するページを参照してください。  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Windows イベント ビューアー、Windows パフォーマンス モニター、および Windows 診断  
 Configuration Manager コンソールから Windows イベント ビューアー、Windows パフォーマンス モニター、および Windows 診断にアクセスするには、Windows ファイアウォールの例外として、 **[ファイルとプリンターの共有]** を有効にします。  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Configuration Manager クライアントの展開で使用されるポート  
 次の表に、クライアント インストールの処理中に使用されるポートを一覧表示します。  

> [!IMPORTANT]  
>  サイト システム サーバーとクライアント コンピューターとの間にファイアウォールがある場合、選択したクライアント インストール方法に必要な通信がそのファイアウォールによって許可されていることを確認します。 たとえば、ファイアウォールがサーバー メッセージ ブロック (SMB) とリモート プロシージャ コール (RPC) をブロックするため、クライアント プッシュ インストールが失敗することがあります。 その場合、CCMSetup.exe を使用した手動インストールやグループ ポリシーに基づくクライアント インストールなどの、別のクライアント インストール方法を使用します。 これらの代替のクライアント インストール方法では SMB や RPC は必要ありません。  

 クライアント コンピューターで Windows ファイアウォールを構成する方法については、「 [Windows ファイアウォールが許可するポートおよびプログラムの変更](#BKMK_ModifyingWindowsFirewall)」を参照してください。  

### <a name="ports-that-are-used-for-all-installation-methods"></a>すべてのインストール方法で使用されるポート  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|クライアントにフォールバック ステータス ポイントが割り当てられている場合、クライアント コンピューターからフォールバック ステータス ポイントへのハイパーテキスト転送プロトコル (HTTP)。|--|80 (注1「 **代替ポートを利用可能**」を参照)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>クライアント プッシュ インストールで使用されるポート  
 次の表に一覧表示されているポートに加えて、クライアント プッシュ インストールでは、クライアント コンピューターがネットワークで利用可能であるかを確認するためにサイト サーバーからクライアント コンピューターへの ICMP (Internet Control Message Protocol) のエコー要求メッセージも使用します。 ICMP は TCP/IP Ping コマンドとも呼ばれます。 ICMP には UDP または TCP プロトコル番号がないため、次の表には記載されていません。 クライアント プッシュ インストールを成功させるには、ファイアウォールなどのすべての介在するネットワーク デバイスで ICMP トラフィックが許可されている必要があります。  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|サイト サーバーとクライアント コンピューター間のサーバー メッセージ ブロック (SMB)。|--|445|  
|サイト サーバーとクライアント コンピューター間の RPC エンドポイント マッパー。|135|135|  
|サイト サーバーとクライアント コンピューター間の RPC 動的ポート。|--|DYNAMIC|  
|ハイパーテキスト転送プロトコル (HTTP) を介して接続される場合、クライアント コンピューターから管理ポイントへの HTTP。|--|80 (注1「 **代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS) を介して接続される場合、クライアント コンピューターから管理ポイントへの HTTPS。|--|443 (注 1「 **代替ポートを利用可能**」を参照)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>ソフトウェアの更新ポイントを使用したインストールで使われるポート  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|クライアント コンピューターからソフトウェアの更新ポイントへのハイパーテキスト転送プロトコル (HTTP)。|--|80 または 8530 (注 2「 **Windows Server Update Services**」を参照)|  
|クライアント コンピューターからソフトウェアの更新ポイントへのセキュア ハイパーテキスト転送プロトコル (HTTPS)。|--|443 または 8531 (注 2「 **Windows Server Update Services**」を参照)|  
|CCMSetup のコマンドライン プロパティ **/source:&lt;Path\>** を指定するときの、ソース サーバーとクライアント コンピューター間のサーバー メッセージ ブロック (SMB)。|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>グループ ポリシーを使用したインストールで使われるポート  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP) を介して接続される場合、クライアント コンピューターから管理ポイントへの HTTP。|--|80 (注1「 **代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS) を介して接続される場合、クライアント コンピューターから管理ポイントへの HTTPS。|--|443 (注 1「 **代替ポートを利用可能**」を参照)|  
|CCMSetup のコマンドライン プロパティ **/source:&lt;Path\>** を指定するときの、ソース サーバーとクライアント コンピューター間のサーバー メッセージ ブロック (SMB)。|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>手動インストールおよびログオン スクリプトを使用したインストールで使われるポート  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|クライアント コンピューターと、CCMSetup.exe の実行元のネットワーク共有との間のサーバー メッセージ ブロック (SMB)。<br /><br /> Configuration Manager のインストール時、クライアント インストールのソース ファイルが、管理ポイントの *&lt;インストール パス\>* \Client フォルダーからコピーされて自動的に共有されます。 ただし、これらのファイルをコピーして、ネットワーク上の任意のコンピューターに新しい共有を作成することもできます。 または、リムーバブル メディアを使用するなどして CCMSetup.exe をローカルで実行し、このネットワーク トラフィックを回避することも可能です。|--|445|  
|ハイパーテキスト転送プロトコル (HTTP) を介して接続され、CCMSetup のコマンドライン プロパティ **/source:&lt;Path\>** を指定しない場合の、クライアント コンピューターから管理ポイントへの HTTP。|--|80 (注1「 **代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS) を介して接続され、CCMSetup のコマンドライン プロパティ **/source:&lt;Path\>** を指定しない場合の、クライアント コンピューターから管理ポイントへの HTTPS。|--|443 (注 1「 **代替ポートを利用可能**」を参照)|  
|CCMSetup のコマンドライン プロパティ **/source:&lt;Path\>** を指定するときの、ソース サーバーとクライアント コンピューター間のサーバー メッセージ ブロック (SMB)。|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>ソフトウェアの配布によるインストールで使われるポート  

|[説明]|UDP|TCP|  
|-----------------|---------|---------|  
|配布ポイントとクライアント コンピューター間のサーバー メッセージ ブロック (SMB)。|--|445|  
|ハイパーテキスト転送プロトコル (HTTP) を介して接続される場合、クライアントから配布ポイントへの HTTP。|--|80 (注1「 **代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS) を介して接続される場合、クライアントから配布ポイントへの HTTPS。|--|443 (注 1「 **代替ポートを利用可能**」を参照)|  

## <a name="notes"></a>注  
 **1 代替ポートを利用可能** Configuration Manager で、この値に対して代替ポートを定義できます。 カスタム ポートを定義済みの場合、IPsec ポリシー用またはファイアウォール構成用の IP フィルター情報を定義するときは、そのカスタム ポートを代わりに使用してください。  

 **2 Windows Server Update Services** Windows Server Update Services (WSUS) は、既定の Web サイト (ポート 80) 上にインストールすることも、カスタム Web サイト (ポート 8530) 上にインストールすることもできます。  

 ポートはインストールした後に変更できます。 サイト階層全体で同じポート番号を使用する必要はありません。  

 HTTP ポートが 80 の場合、HTTPS ポートは 443 の必要があります。  

 HTTP ポートがその他の場合、HTTPS ポートは 1 大きくする必要があります。 たとえば、8530 と 8531 などです。
