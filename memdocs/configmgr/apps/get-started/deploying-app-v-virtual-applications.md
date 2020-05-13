---
title: App-V 仮想アプリケーションの展開
titleSuffix: Configuration Manager
description: 仮想アプリケーションを作成して展開するときに検討する必要がある考慮事項について説明します。
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df6f550b21523e365055f6a4cdafadca7603c4bf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906366"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Configuration Manager での App-V 仮想アプリケーションの展開

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager を使用して仮想アプリケーションを管理すると、次のような利点があります。  

-   単一の管理インフラストラクチャ  

-   スケーラビリティ、展開、およびコレクションとユーザー デバイスのアフィニティなどのコンテンツ配布機能  

-   高度なアプリケーション管理機能  

-   オペレーティング システムの展開、ソフトウェアとハードウェアのインベントリ、ソフトウェア使用状況測定、資産インテリジェンスを使用した仮想アプリケーションのサポート  

Microsoft Application Virtualization (App-V) を使用したアプリケーションの作成方法とシーケンス方法については、[Application Virtualization 4 のドキュメント](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v4/)を参照してください。  

アプリケーションを作成するための Configuration Manager の他の要件と手順に加えて、仮想アプリケーションを作成および展開するときには以下の考慮事項について検討する必要があります。

-   コンピューターに仮想アプリケーションを展開するには、使用するコンピューターに構成マネージャー クライアントと App-V クライアントがインストールされている必要があります。 クライアント デバイスには、デスクトップ コンピューター、ポータブル コンピューター、仮想デスクトップ インフラストラクチャ (VDI) クライアントを利用できます。 Configuration Manager と App-V クライアント ソフトウェアは連携して動作し、仮想アプリケーション パッケージの配信、特定、起動を行います。 構成マネージャー クライアントは、App-V クライアントへの仮想アプリケーション パッケージの配信を管理します。 App-V クライアントは、クライアントの仮想アプリケーションを実行します。  

-   仮想アプリケーションを展開するには、まず、App-V Application Virtualization Sequencer を使って仮想アプリケーションを作成する必要があります。 Sequencer によって、アプリケーションのインストールおよびセットアップのプロセスが監視され、アプリケーションを仮想環境で実行するのに必要な情報が記録されます。 また、Sequencer を使用して、どのファイルと構成をすべてのユーザーに適用するのかや、どの構成をユーザーがカスタマイズできるようにするのかを設定することもできます。  

-   アプリケーションをシーケンスするときには、Configuration Manager がアクセスできる場所にパッケージを保存する必要があります。 その後で、この仮想アプリケーションを含むアプリケーション展開を作成できます。  

-   Configuration Manager では、App-V 4.6 の読み取り専用の共有キャッシュ機能の使用はサポートしていません。  

-   Configuration Manager では、App-V 5 の共有コンテンツ格納機能をサポートしています。  

-   仮想アプリケーションの展開の種類を作成すると、アプリケーション マニフェスト ファイルのコンテンツを使って Configuration Manager によって展開の種類が作成されます。 これは、仮想アプリケーションの情報が含まれた XML ファイルです。 また、Configuration Manager によって、仮想アプリケーションでサポートされるオペレーティング システムの情報が含まれた App-V の .osd ファイルのコンテンツに基づいて、展開の種類の要件も作成されます。  

-   Configuration Manager で仮想アプリケーションを展開するには、クライアント コンピューターに、最低でも App-V 4.6 SP1 以降のバージョンのクライアントがインストールされている必要があります。  

-   仮想アプリケーションを正常に展開できるようにするには、最新の修正プログラムを使って App-V クライアントを更新してください。 詳細については、「[App-V 4.5 および App-v 4.6 ファイルバージョンの最新一覧](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions)」を参照してください。

-   App-V 5.0 の接続グループを使用して、展開した仮想アプリケーションでクライアント コンピューター上の同じファイル システムとレジストリを共有できます。 標準の仮想アプリケーションとは異なり、これらのアプリケーションで相互にデータを共有できます。 また、接続グループは、含まれるアプリケーションのユーザー設定を保存します。 Configuration Manager の App-V 仮想環境は、クライアント コンピューターで接続グループを設定するために使用されます。 アプリケーションがインストールされると、クライアント コンピューターに仮想環境が作成されます。また、インストールされたアプリケーションがクライアントで次回評価されたときに、クライアント コンピューターの仮想環境が変更されます。 複数のアプリケーションでファイル システムやレジストリ値の変更が試みられた場合は、優先順位の最も高いアプリケーションが優先されるように、これらのアプリケーションに優先順位を設定することができます。 詳細については、「[Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md)」 (App-V 仮想環境の作成) をご覧ください。  

##  <a name="supported-app-v-versions"></a>サポートされる App-V のバージョン  
 Configuration Manager では、次のバージョンの App-V がサポートされます。  

-   **App-V 4.6:** 仮想アプリケーションを Configuration Manager で使用するには、クライアント コンピューターに、App-V 4.6 SP1、App-V 4.6 SP2、または App-V 4.6 SP3 のクライアントがインストールされている必要があります。  

     仮想アプリケーションを正常に展開できるようにするには、最新の修正プログラムを使って App-V 4.6 クライアントを更新してください。 詳細については、「[App-V 4.5 および App-v 4.6 ファイルバージョンの最新一覧](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions)」を参照してください。  

-   **App-V 5、App-V 5.0 SP1、App-V 5.0 SP2、App-V 5.0 SP3、および App-V 5.1:** App-V 5.0 SP2 については、[修正プログラム パッケージ 5](https://support.microsoft.com/help/2963211) をインストールするか、App-V 5.0 SP3 を使用する必要があります。  
-   **App-V 5.2**:これは、Windows 10 Education (1607 以降)、Windows 10 Enterprise (1607 以降)、Windows Server 2016 に組み込まれています。

Windows 10 の App-V の詳細については、次のトピックを参照してください。

- [App-V の新着情報](https://docs.microsoft.com/windows/application-management/app-v/appv-about-appv)
- [Windows 10 向け App-V の概要](https://docs.microsoft.com/windows/application-management/app-v/appv-getting-started)
- [既存のインストールから Windows 10 向け App-V へのアップグレード](https://docs.microsoft.com/windows/application-management/app-v/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>App-V 仮想アプリケーションの管理の手順  
 App-V 仮想アプリケーションを管理するには、次の手順を実行します。  

1.   **シーケンス**:シーケンスは、App-V Sequencer を使用して、アプリケーションを仮想アプリケーションに変換するプロセスです。

2.   **作成**: 展開の種類の作成ウィザードを使用して、シーケンスしたアプリケーションを Configuration Manager の展開の種類にインポートします。その後、この展開の種類をアプリケーションに追加できます。 複数の仮想アプリケーションで設定を共有できる仮想環境を作成することもできます。

3.   **配布**:配布は、Configuration Manager の配布ポイントで App-V アプリケーションを使用できるようにするプロセスです。

4.   **展開**: 展開は、クライアント コンピューターでアプリケーションを使用できるようにするプロセスです。 これは、App-V の完全なインフラストラクチャでは、公開およびストリーミングと呼ばれます。  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Configuration Manager の仮想アプリケーション配信方法  
Configuration Manager では、仮想アプリケーションをクライアントに配信する方法として、ストリーミング配信とローカル配信 (ダウンロードして実行) の 2 つをサポートしています。

使用する配信方法を決定する場合、ストリーミング配信では必要なディスク容量が少なくなることと、ローカル配信では App-V アプリケーションの可用性が保証されることを比較してください。 ローカル配信ではクライアントで必要なディスク容量は増えますが、どのような場所からでも常にアプリケーションを使用できるため、ストリーミング配信よりも理想的です。  

###  <a name="streaming-delivery"></a>ストリーミング配信
Configuration Manager を使用して App-V クライアントを管理すると、配布ポイントからの HTTP または HTTPS による仮想アプリケーションのストリーミングがサポートされます。 HTTP または HTTPS によるストリーミングは既定で有効で、[配布ポイントのプロパティ] ダイアログ ボックスで設定します。 仮想アプリケーションをクライアント コンピューターに展開し、ユーザーがその仮想アプリケーションを実行すると、構成マネージャー クライアントは管理ポイントと通信し、使用する配布ポイントを決定します。 その後、アプリケーションが配布ポイントからストリーミングされます。  

ストリーミング配信が最適な配信方法かを判断する場合、次の表の情報を参考にしてください。

|長所|短所|  
|----------------|-------------------|  
|この方法では、標準のネットワーク プロトコルを使用して、配布ポイントからパッケージのコンテンツをストリーミングします。<br /><br /> 仮想アプリケーションのプログラム ショートカットをクリックすると、配布ポイントへの接続が起動されます。仮想アプリケーションの配信はオンデマンドです。<br /><br /> この方法は、配布ポイントへの接続の帯域幅が広いクライアントに向いています。<br /><br /> 企業全体に配信される、更新された仮想アプリケーションは、現在のバージョンが置き換えられたことを通知するポリシーをクライアントが受信したときに利用可能になります。クライアントは、前のバージョンからの変更点のみをダウンロードします。<br /><br /> 配布ポイントではアクセス権限が定義され、ユーザーは、承認されていないアプリケーションやパッケージにアクセスできません。|ユーザーが初めてアプリケーションを実行するまで、仮想アプリケーションはストリーミングされません。 このシナリオでは、ユーザーに仮想アプリケーションのプログラム ショートカットが送信され、仮想アプリケーションの初回実行前にネットワークから切断されることがあります。 クライアントがオフラインのときにユーザーが仮想アプリケーションを実行しようとすると、アプリケーションをストリーミングする Configuration Manager 配布ポイントを使用できないため、エラーが表示され、仮想化アプリケーションを実行できません。 アプリケーションは、ユーザーがネットワークに再接続して、アプリケーションを実行するまで使用できません。<br /><br /> これを回避するには、クライアントへの仮想アプリケーションの配信にローカル配信方法を使用するか、ストリーミング配信でインターネット ベースのクライアント管理を有効にします。|  

###  <a name="local-delivery-download-and-execute"></a>ローカル配信 (ダウンロードして実行)  
Configuration Manager を使用するときの最も一般的なアプローチはダウンロードして実行することです。このアプローチが、Configuration Manager により他のアプリケーション形式が配信される方法にとても似ているためです。 ローカル配信方法を使用すると、Configuration Manager クライアントは、最初に全体の仮想アプリケーション パッケージを Configuration Manager クライアントのキャッシュにダウンロードします。 次に、Configuration Manager は、Configuration Manager キャッシュから APP-V キャッシュにアプリケーションをストリーミングするよう APP-V クライアントに指示します。 仮想アプリケーションをクライアント コンピューターに展開するときに、そのコンテンツが App-V キャッシュにない場合、App-V クライアントは、構成マネージャー クライアント キャッシュから App-V キャッシュにアプリケーションのコンテンツをストリーミングしてから、アプリケーションを実行します。 アプリケーションが正常に実行された後、次の削除サイクルで古いバージョンのパッケージをすべて削除するか、構成マネージャー クライアント キャッシュに保持するかを、構成マネージャー クライアントで設定できます。 コンテンツをローカルで永続化する場合、BranchCache と PeerCache のようなパッケージ コンテンツの配信を最適化するメソッドを利用できます。

ローカル配信が最適な配信方法かを判断する場合、次の表の情報を参考にしてください。   

|長所|短所|  
|----------------|-------------------|  
|パッケージのダウンロードには、バックグラウンド インテリジェント転送サービス (BITS) を使用した標準の配布ポイントの機能が使用されます。<br /><br /> 仮想アプリケーション パッケージのコンテンツは、クライアントにローカルに配信されます。 つまり、コンピューターがネットワークに接続されていない場合にアプリケーションを実行できます。<br /><br /> この方法は、低速または信頼されないネットワーク接続と、ネットワークに接続する頻度が低いコンピューターに適しています。<br /><br /> Configuration Manager は、Remote Differential Compression (RDC) を使用して、仮想アプリケーション パッケージのコンテンツの更新時に変更されたファイル内のデータのみを、クライアントに送信します。 構成マネージャー クライアントは、RDC を使用して、現在のバージョンのパッケージと、クライアントに送信された変更を基に、新しいバージョンの仮想アプリケーション パッケージを作成します。<br /><br /> この方法では、モバイル ユーザーやネットワークに接続されていないユーザーに対して、アプリケーションの回復力が高くなります。 管理者は、仮想アプリケーションがインストール操作で展開された場合に、配信後も Configuration Manager キャッシュにパッケージを保持することを選択できます。 構成マネージャー クライアント キャッシュに保存されたパッケージは、App-V クライアントがパッケージをキャッシュにプルする場合に、ローカルの信頼できるストリーミング ソースとして使用できます。|仮想アプリケーションを Configuration Manager キャッシュに保持する場合、クライアントには、仮想アプリケーション パッケージのサイズの最大 2 倍のディスク容量が必要です。|  

###  <a name="deployment-from-an-image"></a>イメージからの展開

コンピューターに仮想アプリケーションを事前インストールし、その他のコンピューターへの展開用に、そのコンピューターのイメージを作成することもできます。 ただし、仮想アプリケーション パッケージを別のサイトで作成した場合、アプリケーションの更新プログラムをダウンロードするときに、バイナリ差分レプリケーションは使用されません。 このオプションは、ユーザーのログオン後にアプリケーションをダウンロードせず、すぐにアプリケーションを使用できるようにする場合に、仮想デスクトップ インフラストラクチャで有用です。    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>App-V インフラストラクチャから Configuration Manager および App-V インフラストラクチャへの移行  
既存の App-V インフラストラクチャから Configuration Manager による仮想アプリケーションの管理に移行する計画を立てる場合、次の表をご覧ください。  

|手順|説明|  
|----------|----------------------|  
|現在の仮想アプリケーションを検討して、Configuration Manager インフラストラクチャに移行するアプリケーションを選択します。|詳細情報はありません。|  
|仮想アプリケーションを展開する先のユーザーとデバイスを評価する|Configuration Manager コレクションを作成して、仮想アプリケーションの展開先のユーザーとデバイスをグループ化します。 「[コレクションの概要](../../core/clients/manage/collections/introduction-to-collections.md)」をご覧ください。|  
|App-V 5 接続グループを Configuration Manager 仮想環境に移行する|このトピックの「[App-V 5 接続グループを Configuration Manager 仮想環境に移行する](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments)」セクションをご覧ください。|  
|仮想アプリケーションのいずれかが、Configuration Manager インフラストラクチャにフル アプリケーションとして存在しているかどうかを調査して検出する|管理を簡単にするために、仮想アプリケーションを、新しい展開の種類として既存のフル アプリケーションに追加できます。 「[Create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md)」 (System Center Configuration Manager でアプリケーションを作成する) を参照してください。|  
|既存の App-V パッケージの代わりとなるアプリケーションを作成する|「[アプリケーション管理の概要](../understand/introduction-to-application-management.md)」および「[Create applications](../../apps/deploy-use/create-applications.md)」 (アプリケーションを作成する) をご覧ください。|  
|Configuration Manager で、仮想アプリケーションの最初の展開後に、クライアントでの仮想アプリケーションの管理を開始する。 その後、Configuration Manager はコンピューター上のすべての App-V アプリケーションを管理する必要があります。|詳細情報はありません。|  
|コンテンツを適切な配布ポイントに配布し、アプリケーションのローカル配信を有効にする|「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。|  
|アプリケーションを構成マネージャー クライアントに展開する<br /><br /> App-V アプリケーションが、マニフェスト XML ファイルを作成しない以前のバージョンの Sequencer で作成されている場合、新しいバージョンの Sequencer でアプリケーションを開いて保存し、マニフェスト XML ファイルを作成できます。 このファイルは、Configuration Manager で仮想アプリケーションを展開するために必要です。<br /><br /> App-V は、SoftGrid 4.1 SP1 または 4.2 バージョンの Sequencer で作成された仮想アプリケーション パッケージをサポートします。<br /><br /> アプリケーションが以前にローカルでインストールされている場合、仮想バージョンのアプリケーションを展開する前に、そのアプリケーションをアンインストールする必要があります。|「[Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)」 (System Center Configuration Manager でアプリケーションを展開する) を参照してください。|  
|Configuration Manager では、仮想アプリケーションを含むパッケージとプログラムの使用をサポートしなくなりました。 Configuration Manager 2007 から Configuration Manager Current Branch に移行すると、Configuration Manager によってこれらのパッケージがアプリケーションに変換されます。<br /><br /> Configuration Manager 2007 公開通知は、次の展開の種類に変換されます。<br /><br /> - 移行する App-V パッケージに公開通知がない場合:既定の展開の種類の設定を使用する 1 つの展開の種類<br /><br /> - 移行する App-V パッケージの公開通知が 1 つの場合:Configuration Manager 2007 の公開通知と同じ設定を使用する <br />                展開の種類が 1 つ作成されます。<br /><br /> - 移行する App-V パッケージの公開通知が複数の場合:Configuration Manager 2007 の各公開通知に対して展開の種類が 1 つ作成されます。 <br />                それぞれの展開の種類で使用する設定は、公開通知と同じになります。|[Configuration Manager の現在のブランチにオブジェクトを移行するための計画策定](../../core/migration/planning-for-the-migration-of-objects.md)に関するページを参照してください。|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>App-V 5 接続グループの Configuration Manager 仮想環境への移行  
Configuration Manager の App-V 仮想環境を使用すると、展開した仮想アプリケーションで、クライアント コンピューター上の同一のファイル システムとレジストリを共有できます。 つまり、標準の仮想アプリケーションとは異なり、これらのアプリケーションは、相互にデータを共有できます。 アプリケーションがインストールされると、クライアント コンピューターに仮想環境が作成されます。また、インストールされたアプリケーションがクライアントで次回評価されたときに、クライアント コンピューターの仮想環境が変更されます。 仮想環境は、スタンドアロンの App-V 5 の接続グループと同様です。  

スタンドアロンの App-V 5 から Configuration Manager 仮想環境に接続グループを移行する場合、クライアント コンピューターに既に存在する接続グループが Configuration Manager によって適切に管理されるようにし、これらの接続グループ内のユーザーの環境が維持されるようにする必要があります。  

App-V 5 接続グループを Configuration Manager 仮想環境に変換するには、次の手順を実行します。  

1.  App-V に存在するすべてのアプリケーションに対して、Configuration Manager アプリケーションを作成します。  

2.  展開の目的が **[必須]** のアプリケーションをユーザーまたはデバイスインスタンスに展開します。 ユーザーに対する展開は、APP-V でアプリケーションを使用したのと同じユーザーに展開する必要があります。 コンピューターに対する展開は、APP-V でアプリケーションを使用したのと同じコンピューターに展開する必要があります。  

3.  展開が終わったら、スタンドアロン App-V で発行された接続グループと一致する仮想環境を作成します。 仮想環境には、同じ順で同じパッケージ (特に、App-V 5 の展開の種類) を含める必要があります。  

App-V 仮想環境を作成する方法については、「[App-V 仮想環境を作成する方法](../../apps/deploy-use/create-app-v-virtual-environments.md)」をご覧ください。  

または、App-V クライアントからすべての接続グループを削除してから、Configuration Manager を使用してアプリケーションを展開することができます。 ただし、ユーザーが App-V 接続グループに保存した設定は失われます。  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>App-V 4.6 の Dynamic Suite Composition  
Dynamic Suite Composition は、1 つの仮想アプリケーション パッケージが別の仮想アプリケーション パッケージと依存関係があると定義できる機能です。 このアプリケーションを実行すると、App-V クライアントは、プライマリ パッケージとその依存パッケージをアプリケーションの同じ仮想環境でホストします。  

Configuration Manager でこの機能を使用するには、両方のパッケージを展開し、App-V クライアントに登録する必要があります。 依存パッケージのコンテンツをクライアント コンピューターのローカルでホストするために、ローカル配信用 (ダウンロードおよび実行) にアプリケーションの展開を設定します。  

App-V Dynamic Suite Composition の詳細については、App-V のドキュメントをご覧ください。  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>App-V 4.6 アプリケーションから App-V 5 アプリケーションへの変換  
App-V 5 のアプリケーション パッケージの形式は、App-V 4.6 から変わりました。 App-V 4.6 を使用してシーケンス処理されたアプリケーションは、サポートされなくなりました。 ただし、App-V 5 には、アプリケーションの変換に使用できるパッケージ変換ツールがあります。 詳細については、[以前の App-V バージョンで作成されたパッケージを変換する方法](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/how-to-convert-a-package-created-in-a-previous-version-of-app-v)に関するページを参照してください。  

App-V 4.6 アプリケーションを App-V 5 アプリケーションに変換するには、次の手順を実行します。  

1.  App-V 4.6 パッケージを App-V 5 形式に変換するか、シーケンス処理を再実行します。  

2.  App-V 5 クライアントを階層内のコンピューターに展開します。  

3.  App-V 5 アプリケーション用の展開の種類を含む新しいアプリケーションを作成し、置き換えの規則を作成して、App-V 4.6 アプリケーションを置き換えます。  

4.  必要に応じて仮想環境を作成します。  

5.  新しい App-V 5 アプリケーションをコンピューターに展開します。  

##  <a name="user-and-deployment-configuration-files"></a>ユーザーおよび展開構成ファイル  
ユーザーおよび展開構成ファイルには、アプリケーションの動作を制御する設定が含まれます。 これらのファイルを使用すると、アプリケーションのシーケンス処理を再実行せずにアプリケーション設定を変更できます。  

一般的な App-V 5 アプリケーションには、次のファイルが含まれます。  

-   アプリケーション パッケージ (.appv) ファイル  

-   ユーザー構成ファイル  

-   展開構成ファイル  

ユーザー構成ファイルには、ログオンしたユーザーにのみ適用される設定が含まれます。 たとえば、構成ファイルを編集して、ユーザーに展開されるアプリケーション ショートカットに関する情報を変更できます。 複数の展開の種類で Configuration Manager アプリケーションを作成することもできます。 また、各展開の種類に異なるユーザー構成ファイルを含め、要件の規則を使用することで、関連するユーザーに確実にインストールされるようにすることができます。  

展開構成ファイルには、コンピューターに適用される設定 (レジストリ設定など) が含まれます。 また、すべてのユーザーに適用されるユーザー設定も含まれます。  

Configuration Manager を使用して App-V 5 仮想アプリケーションを展開する場合、App-V 5 の展開の種類を作成するときに、3 つのファイルすべてが同じフォルダーに配置されている必要があります。 フォルダー内に複数のファイルがある場合、Configuration Manager は最新のファイルを使用します。  

詳細については、[App-V 5.0 動的構成の概要](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/about-app-v-50-dynamic-configuration)に関するページを参照してください。  

##  <a name="app-v-local-interaction"></a>App-V ローカル通信  
アプリケーションの展開のシナリオによっては、アプリケーションがクライアント コンピューターのローカルにインストールされ、他のアプリケーションが仮想アプリケーションとして同じクライアント コンピューターに展開されることがあります。 既定では、ローカルにインストールされたアプリケーションは、仮想化されたアプリケーションを直接表示または通信することはできません。 これは、App-V が提供しているアプリケーションの分離機能の意図的な動作です。 ローカル通信は、各アプリケーションで有効にすることができる App-V クライアントの機能です。有効にすると、クライアント コンピューターのローカルにインストールされ、実行されているアプリケーションが、仮想化されたアプリケーションを表示して通信できるようになります。 Configuration Manager および App-V はローカル通信を完全にサポートしています。  

App-V のローカル通信機能の詳細については、App-V のドキュメントをご覧ください。  

##  <a name="app-v-5-shared-content-store"></a>App-V 5 共有コンテンツ ストア  
Configuration Manager では、App-V 5 共有コンテンツ格納機能をサポートしています。 詳細については、「 [App-v 5.0 共有コンテンツ ストア (SCS) の計画](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/planning-for-the-app-v-50-sequencer-and-client-deployment#planning-for-the-app-v-50-shared-content-store-scs)」をご覧ください。  

##  <a name="monitoring-virtual-applications"></a>仮想アプリケーションの監視  

### <a name="virtual-application-reports"></a>仮想アプリケーション レポート  
Configuration Manager 環境で App-V を監視するには、次のレポートを使用できます。  

|レポート名|[説明]|  
|-----------------|-----------------|  
|App-V 仮想環境の結果|選択したコレクションに対して指定した状態にある仮想環境に関する情報を表示します (App-V 5 のみ)。|  
|資産に関する App-V 仮想環境の結果|指定した資産の仮想環境と、選択した仮想環境の任意の展開の種類に関する情報を表示します (App-V 5 のみ)。|  
|App-V 仮想環境のステータス|選択したコレクションの選択した仮想環境のコンプライアンス情報を表示します。 このレポートの **[保持総数]** 列には、以前に設定した仮想環境を適用できなくなった資産が表示されますが、引き続き、仮想環境で実行されるアプリケーションにユーザー設定が維持されます (App-V 5 のみ)。|  
|特定の仮想アプリケーションが存在するコンピューター|Application Virtualization Management Sequencer で作成された指定の App-V ショートカットがあるコンピューターの概要が表示されます (App-V 4.6 のみ)。|  
|特定の仮想アプリケーション パッケージが存在するコンピューター|指定した App-V アプリケーション パッケージがインストールされているコンピューターの一覧が表示されます (App-V 4.6 のみ)。|  
|仮想アプリケーション パッケージのすべてのインスタンスのカウント|すべての検出された App-V アプリケーション パッケージの数が表示されます (App-V 4.6 のみ)。|  
|仮想アプリケーションのすべてのインスタンスのカウント|すべての検出された App-V アプリケーションの数が表示されます (App-V 4.6 のみ)。|  

### <a name="log-files"></a>ログ ファイル  
Configuration Manager は、仮想アプリケーションの展開に関する情報をログ ファイルに記録します。 仮想アプリケーションと Configuration Manager アプリケーション管理で使用されるログ ファイルについては、「[ログ ファイル](../../core/plan-design/hierarchy/log-files.md)」をご覧ください。  

Windows 8.1 の場合、App-V クライアントのログは C:\ProgramData\Microsoft\Application Virtualization Client にあります。  
