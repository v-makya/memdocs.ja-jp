---
title: WAN トラフィックを削減するための Windows PE ピア キャッシュの準備
titleSuffix: Configuration Manager
description: Windows PE ピア キャッシュは、Windows PE で機能し、ローカルの配布ポイントがない場合にローカルのピアからコンテンツを取得して WAN のトラフィックを最小限に抑えます。
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd622c1a54c1dd3cd3b5071cc62d1b6860a118e3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708780"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-configuration-manager"></a>Configuration Manager で WAN トラフィックを削減するための Windows PE ピア キャッシュの準備

*適用対象:Configuration Manager (Current Branch)*

新しいオペレーティング システムを Configuration Manager に展開すると、タスク シーケンスを実行しているコンピューターで、配布ポイントからコンテンツをダウンロードするのではなく、Windows PE ピア キャッシュを使用してローカル ピア (ピア キャッシュ ソース) からコンテンツを取得することができます。 これにより、ローカル配布ポイントが存在しないブランチ オフィス シナリオでワイド エリア ネットワーク (WAN) トラフィックが最小限に抑えられます。  

 Windows PE ピア キャッシュは [Windows BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)に似ていますが、Windows プレインストール環境 (Windows PE) で機能します。 Windows PE ピア キャッシュを使用するクライアントの記述に、以下の用語が使用されています。  

-   **ピア キャッシュ クライアント** は、Windows PE ピア キャッシュを使用するように構成されたコンピューターです。  

-   **ピア キャッシュ ソース** は、ピア キャッシュ用に構成され、コンテンツを要求元の他のピア キャッシュ クライアントが取得できるようにするクライアントです。  

次の手順に従って、ピア キャッシュを管理します。

##  <a name="objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a> ピア キャッシュ ソースに格納されているオブジェクト  
 Windows PE ピア キャッシュを使用するように構成するタスク シーケンスは、Windows PE で実行中に、次のコンテンツ オブジェクトを取得できます。  

- オペレーティング システム イメージ  

- ドライバー パッケージ  

- パッケージとプログラム (タスク シーケンスが Windows PE で実行中にピア キャッシュ用に構成されてから、クライアントが完全なオペレーティング システム上でそのタスク シーケンスの実行を継続する場合には、クライアントはこのコンテンツをピア キャッシュ ソースから取得します)。  

- その他のブート イメージ  

  次のコンテンツ オブジェクトに関しては、ピア キャッシュを使用して転送することはありません。 代わりにこれらのオブジェクトは、配布ポイントから、または、Windows BranchCache によって (環境で Windows BranchCache が構成されている場合) 転送します。  

- アプリケーション  

- ソフトウェア更新プログラム  

##  <a name="how-does--windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a> Windows PE ピア キャッシュのしくみ  
 配布ポイントは存在しないものの、複数のクライアントで Windows PE ピア キャッシュの使用が有効になっている支社オフィスを使用したシナリオを考えてみます。 ピア キャッシュ ソースの一部として構成されている複数のクライアントに、ピア キャッシュを使用するように構成されたタスク シーケンスを展開します。 このタスク シーケンスを実行する最初のクライアントは、対象コンテンツが含まれるピアの要求をブロードキャストします。 それは見つからないため、WAN 経由で配布ポイントからコンテンツを取得します。 このクライアントは、新しいイメージをインストールしてから、コンテンツをその Configuration Manager クライアント キャッシュに保存するため、他のクライアントに対するピア キャッシュ ソースとして機能できます。 次のクライアントがタスク シーケンスを実行するときに、ピア キャッシュ ソース用のサブネット上で要求をブロードキャストし、最初のクライアントが応答してそのキャッシュされたコンテンツを使用できるようにします。  

##  <a name="determine-what--clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a> Windows PE ピア キャッシュ ソースの一部となるクライアントの判別  
 Windows PE ピア キャッシュ ソースとして選択するコンピューターを決定するときに、いくつかの考慮事項があります。  

-   Windows PE ピア キャッシュ ソースは、常に電源が入り、ピア キャッシュ クライアントが使用できるデスクトップ コンピューターにする必要があります。  

-   Windows PE ピア キャッシュには、イメージを格納するための十分なクライアント キャッシュ サイズが必要です。  

##  <a name="requirements-for-a-client-to-use-a--windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a> Windows PE ピア キャッシュ ソースを使用するクライアントの要件  
 Windows PE ピア キャッシュ ソースを使用するクライアントは、次の要件を満たしている必要があります。  

-   Configuration Manager クライアントは、ネットワーク上の次のポートを経由して通信できる必要があります。  

    -   初期ネットワーク ブロードキャストでピア キャッシュ ソースを検索するためのポート。 既定では、これは UDP ポート 8004 です。  

    -   ピア キャッシュ ソースからコンテンツをダウンロードするためのポート (HTTP と HTTPS)。 既定では、これは TCP ポート 8003 です。  
    
        詳細については、「[接続に使用するポート](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp)」を参照してください。  

        > [!TIP]  
        >  クライアントは、HTTPS を使用して、コンテンツが使用可能になるとダウンロードします。 ただし、HTTP と HTTPS で同じポート番号が使用されます。  

-   クライアント上で[Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) することによって、展開されたイメージを保存するのに十分なスペースを確保する必要があります。 Windows PE ピア キャッシュは、クライアント キャッシュの構成にも動作にも影響を与えません。  

-   タスク シーケンス展開用の展開オプションは、タスク シーケンスで必要な場合のコンテンツのローカル ダウンロードとして構成する必要があります。  

##  <a name="configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a> Windows PE ピア キャッシュの構成  
 以下の方法を使用すると、ピア キャッシュ コンテンツを使ってクライアントをプロビジョニングしてピア キャッシュ ソースとして機能させることができます。  

- コンテンツが保存されたピア キャッシュ ソースを見つけられないピア キャッシュ クライアントは、配布ポイントからコンテンツをダウンロードすることになります。  クライアントが、ピア キャッシュを有効にするクライアント設定を受信し、タスク シーケンスが、キャッシュされたコンテンツを保持するように構成されている場合は、そのクライアントがピア キャッシュ ソースになります。  

- ピア キャッシュ クライアントは別のピア キャッシュ クライアント (ピア キャッシュ ソース) からコンテンツを取得することができます。  クライアントはピア キャッシュ用に構成されているため、キャッシュされたコンテンツを保持するように構成されたタスク シーケンスを実行すると、そのクライアントがピア キャッシュ ソースになります。  

- クライアントはオプション ステップの [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)を含むタスク シーケンスを実行します。このオプション ステップは、Windows PE ピア キャッシュ タスク シーケンスに含まれる関連コンテンツの事前設定に使用されます。 この方法を使用する場合:  

  -   クライアントは展開されているイメージをインストールする必要がありません。  

  -   **[パッケージ コンテンツのダウンロード]** オプションに加えて、タスク シーケンスで **[Configuration Manager クライアント キャッシュ]** オプションも使用する必要があります。 このオプションはクライアント キャッシュへのコンテンツの保存に使用されるため、クライアントは他のピア キャッシュ クライアントのピア キャッシュ ソースとして機能できます。  

  次の手順は、クライアント上で Windows PE ピア キャッシュを構成し、ピア キャッシュをサポートするタスク シーケンスを構成するのに役立ちます。  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Windows PE ピア キャッシュ ソース コンピューターを構成するには  

1. Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]** に移動してから、新しい **[カスタム クライアント デバイス設定]** を作成するか、既存の設定オブジェクトを編集します。 これを **[既定のクライアント設定]** オブジェクト用に構成することもできます。  

   > [!TIP]  
   >  カスタム設定オブジェクトを使用して、どのクライアントがこの構成を受信するかを管理します。 たとえば、頻繁に移動するユーザーのラップトップではこの構成が行われないようにしたい場合があります。 モバイル度の高いシステムは、他のピア キャッシュ クライアントにコンテンツを提供するのに不適切なソースになりかねません。  
   >   
   >  この設定を **[既定のクライアント設定]** の一部として構成した場合は、その構成が環境内のすべてのクライアントに適用されることも覚えておいてください。  

2. **[クライアント キャッシュ設定]** で、 **[完全な OS 上の Configuration Manager クライアントにコンテンツの共有を許可する]** を **[はい]** に設定します。  

   -   既定では、HTTP のみが有効になります。 クライアントに HTTPS 経由のコンテンツのダウンロードを許可する場合は、 **[クライアント ピア通信に対して HTTPS を有効にする]** を **[はい]** に設定します。  

   -   既定では、ブロードキャスト用のポートは 8004 に設定され、コンテンツ ダウンロード用のポートは 8003 に設定されます。 どちらも変更することができます。  

3. クライアント設定を保存して、ピア キャッシュ ソースとして選択するクライアントに展開します。  

   この設定オブジェクトを使って構成されたデバイスは、ピア キャッシュ ソースとして機能するように構成されます。 これらの設定を潜在的なピア キャッシュ クライアントに展開して、必要なポートとプロトコルを構成する必要があります。  

###  <a name="configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a> Windows PE ピア キャッシュのタスク シーケンスの構成  
 タスク シーケンスを構成するときに、次のタスク シーケンス変数を、タスク シーケンスが展開されるコレクション上のコレクション変数として使用します。  

- **SMSTSPeerDownload**  

   Value:TRUE  

   クライアントに Windows PE ピア キャッシュの使用を許可します。  

- **SMSTSPeerRequestPort**  

   値: <ポート番号\>  

   クライアント設定で構成された既定のポート (8004) を使用しない場合は、初期ブロードキャストに使用するためのネットワーク ポートのカスタム値を使ってこの変数を構成する必要があります。  

- **SMSTSPreserveContent**  

   Value:TRUE  

   展開後に Configuration Manager クライアント キャッシュに残すタスク シーケンス内のコンテンツにフラグを設定します。 これは、タスク シーケンスの持続期間だけコンテンツを保持して、Configuration Manager クライアント キャッシュではなくタスク シーケンス キャッシュを使用する SMSTSPersisContent の使用とは異なります。  

  詳しくは、「[タスク シーケンス変数](../understand/task-sequence-variables.md)」をご覧ください。  

###  <a name="validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a> Windows PE ピア キャッシュの使用が成功したかどうかの検証  
 Windows PE ピア キャッシュを使用してタスク シーケンスを展開してインストールしたら、タスク シーケンスを実行したクライアント上で **smsts.log** を表示することによって、プロセスでピア キャッシュが正常に使用されたことを確認できます。  

 ログで、次のようなエントリを探します。ここで、<*SourceServerName>* はクライアントがコンテンツを取得したコンピューターを示します。 このコンピューターは、配布ポイント サーバーではなく、ピア キャッシュ ソースにする必要があります。 その他の詳細は、ローカル環境と構成によって異なります。  

-   *<![LOG[Downloaded file from http:// <SourceServerName\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
