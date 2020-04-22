---
title: オペレーティング システムの展開の概要
titleSuffix: Configuration Manager
description: Configuration Manager 環境にオペレーティング システムを展開する前に理解する必要がある概念について説明します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703870"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Configuration Manager でのオペレーティング システム展開方法の概要

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager を使用してオペレーティング システムを展開する方法は数多くあります。 オペレーティング システムを展開し、タスクを自動化する方法については、このセクションの情報を参照してください。 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a> オペレーティング システム展開プロセス  
 Configuration Manager では、オペレーティング システムの展開で使用できる数種類の方法を提供します。 次に示す操作は、使用する展開方法に関係なく必要となります。  

-   ブート イメージを起動するか、または展開するオペレーティング システム イメージをインストールするために必要となる Windows デバイス ドライバーを特定します。  

-   対象となるコンピューターを起動するのに使用するブート イメージの特定。  

-   タスク シーケンスを使用して、展開するオペレーティング システムのイメージをキャプチャします。 または、既定のオペレーティング システム イメージを使用することができます。  

-   ブート イメージ、オペレーティング イメージ、その他関連するコンテンツの配布ポイントへの配布。  

-   ブート イメージおよびオペレーティング システム イメージを展開するステップを含むタスク シーケンスを作成します。  

-   コンピューターのコレクションにタスク シーケンスを展開します。  

-   展開を監視します。  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a> オペレーティング システムの展開シナリオ  
 Configuration Manager には数多くのオペレーティング システムの展開シナリオがあり、環境やオペレーティング システムをインストールする目的に応じて、そこから選択できます。  たとえば、新しいバージョンの Windows で既存のコンピューターをフォーマットおよびパーティション作成したり、Windows を最新のバージョンにアップグレードしたりすることができます。 ニーズを満たす展開方法の決定に役立てるために、[エンタープライズ オペレーティング システムを展開するシナリオ](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)を確認します。  次のオペレーティング システムの展開シナリオから選択できます。  

-   [Windows を最新バージョンにアップグレードする](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [新しいバージョンの Windows で既存のコンピューターを更新する](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [既存のコンピューターの置き換えと設定の転送](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a> オペレーティングシステムを展開する方法  
 Configuration Manager クライアント コンピューターにオペレーティング システムを展開するのに使用できる方法にはいくつかあります。  

- **PXE による展開**: PXE による展開では、クライアント コンピューターはネットワークを通じて展開を要求できます。 この展開方法では、オペレーティング システム イメージと Windows PE ブート イメージは、PXE ブート要求を許可するように構成された配布ポイントに送信されます。 詳細については、「[Configuration Manager で PXE を使用して Windows をネットワーク経由で展開する](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。  

- **オペレーティング システムをソフトウェア センターで使用できるようにする**: オペレーティング システムを展開し、ソフトウェア センターで使用できるようにすることができます。 Configuration Manager クライアントでは、ソフトウェア センターから、オペレーティング システムのインストールを開始できます。 詳細については、「[Replace an existing computer and transfer settings](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)」(既存のコンピューターの置き換えと設定の転送) を参照してください。  

- **マルチキャスト展開**: マルチキャスト展開では、別々の接続で各クライアントにデータのコピーを送信する代わりに、複数のクライアントに同時にデータを送信することで、ネットワークの帯域幅を節約します。 この展開方法では、オペレーティング システム イメージは配布ポイントに送信されます。 クライアント コンピューターから展開が要求されると、イメージが展開されます。 詳細については、「[Use multicast to deploy Windows over the network](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)」(マルチキャストを使用した、ネットワーク経由での Windows の展開) を参照してください。  

- **ブート メディアによる展開**: ブート メディアによる展開では、対象となるコンピューターの起動と同時にオペレーティング システムを展開できます。 対象となるコンピューターが立ち上がると、タスク シーケンス、オペレーティング システム イメージ、およびその他の要求されたコンテンツをネットワークから取得します。 そのコンテンツはメディアには含まれていないため、メディアを再作成せずにコンテンツを更新することができます。 詳細については、「[起動可能なメディアの作成](../deploy-use/create-bootable-media.md)」を参照してください。  

- **スタンドアロン メディアによる展開**: スタンドアロン メディアによる展開では、次のような状況でオペレーティング システムを展開できます。  

  - オペレーティング システム イメージまたはファイルサイズの大きなパッケージをネットワークを通じてコピーするのが実用的ではない環境。  

  - ネットワーク接続がない、または低帯域幅のネットワーク接続しかできない環境。  

    詳細については、「[スタンドアロン メディアの作成](../deploy-use/create-stand-alone-media.md)」を参照してください。  

- **事前設定されたメディアによる展開**: 事前設定されたメディアによる展開では、完全にはプロビジョニングされていないコンピューターにオペレーティング システムを展開できます。 事前設定されたファイルは、Windows Imaging Format (WIM) と呼ばれる形式のファイルであり、製造元によるベア メタル コンピューター、または Configuration Manager 環境に接続していない企業の準備センターにインストールすることができます。  

   その後、Configuration Manager 環境で、メディアが提供するブート イメージを使用してコンピューターが起動し、サイト管理ポイントに接続して利用可能なタスク シーケンスを取得し、ダウンロード プロセスを完了します。 ブート イメージとオペレーティング システム イメージが展開先のコンピューターに存在するので、この展開の方法はネットワーク トラフィックを軽減します。 事前設定メディアに含めるアプリケーション、パッケージ、ドライバー パッケージを指定できます。 詳細については、「[事前設定されたメディアの作成](../deploy-use/create-prestaged-media.md)」を参照してください。  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a> ブート イメージ  
 Configuration Manager のブート イメージは、オペレーティング システムの展開中に使用される Windows PE (WinPE) のイメージです。 ブート イメージは、WinPE でコンピューターを起動するために使用されます。WinPE は、セットアップ先のコンピューターで Windows のインストールを準備する限られたコンポーネントとサービスが含まれた、最小限のオペレーティング システムです。 Configuration Manager には、x86 プラットフォームをサポートするブート イメージが 1 つ、x64 プラットフォームをサポートするブート イメージが 1 つ用意されています。 これらは、既定のブート イメージと見なされます。 作成して Configuration Manager に追加したブート イメージは、カスタム イメージと見なされます。 Configuration Manager を更新するときに、既定のブート イメージが自動的に置換されるようにできます。 ブート イメージの詳細については、「[ブート イメージの管理](../get-started/manage-boot-images.md)」を参照してください。  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a> オペレーティング システム イメージ  
 Configuration Manager のオペレーティング システム イメージは、Windows Imaging (WIM) ファイル形式で格納され、コンピューターのオペレーティング システムを正常にインストールおよび構成するのに必要な参照ファイルおよびフォルダーのコレクションを圧縮したものです。 オペレーティング システムのすべての展開シナリオで、オペレーティング システム イメージを選択する必要があります。 既定のオペレーティング システム イメージを使用するか、構成する参照コンピューターからオペレーティング システム イメージを構築することができます。 詳細については、「[オペレーティング システム イメージの管理](../get-started/manage-operating-system-images.md)」をご覧ください。  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a> オペレーティング システムのアップグレード パッケージ  
 オペレーティング システム アップグレード パッケージは、オペレーティング システムをアップグレードするために使用し、セットアップによって開始されるオペレーティング システム展開です。 オペレーティング システム アップグレード パッケージは、DVD またはマウントされている ISO ファイルから、Configuration Manager にインポートします。 詳細については、「[オペレーティング システムのアップグレード パッケージの管理](../get-started/manage-operating-system-upgrade-packages.md)」を参照してください。  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a> オペレーティングシステムの展開のためのメディア  
 オペレーティング システムの展開に使用するために作成するメディアには数種類があります。 これには、オペレーティング システム イメージをキャプチャするために使用するキャプチャ メディア、オペレーティング システムを展開するために使用するスタンドアロン メディア、事前設定されたメディア、および起動可能なメディアが含まれます。 メディアを使用することによって、展開の対象となるコンピューターがネットワークに未接続、または Configuration Manager サイトへ低帯域幅で接続していても、オペレーティング システムを展開できます。 タスク シーケンス メディアの使用方法の詳細については、「[Create task sequence media](../deploy-use/create-task-sequence-media.md)」(タスク シーケンス メディアの作成) を参照してください。  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> デバイス ドライバー  
 展開するオペレーティング システム イメージにデバイス ドライバーを含まなくても、対象となるコンピューターにインストールできます。 Configuration Manager は、Configuration Manager にインポートするすべてのデバイス ドライバーへの参照を含むドライバー カタログを提供します。 ドライバー カタログは **[ソフトウェア ライブラリ]** ワークスペースに保存されており、2 つのノード、**ドライバー**と**ドライバー パッケージ**で構成されます。 **[ドライバー]** ノードにはドライバー カタログにインポートしたすべてのドライバーが一覧になっています。 このノードを使用して、インポートした各ドライバーの詳細を参照したり、ドライバーが属するドライバー パッケージやブート イメージを変更したり、ドライバーを有効または無効にしたりできます。 詳細については、「[Manage drivers](../get-started/manage-drivers.md)」(ドライバーの管理) を参照してください。  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a> ユーザー状態の保存と復元  
 オペレーティング システムを展開する際は、対象となるコンピューターのユーザー状態を保存し、オペレーティング システムを展開して、オペレーティング システムを展開し終わったらユーザー状態を復元することができます。 このプロセスは、通常、Configuration Manager クライアント コンピューターにオペレーティング システムをインストールするときに使用します。  

 ユーザー状態情報はタスク シーケンスを使用してキャプチャし復元します。 ユーザー状態情報をキャプチャしたら、次のいずれかの方法でこの情報を保存できます。  

- 状態移行ポイントを構成することによって、リモートにユーザー状態データを保存することができます。 キャプチャのタスク シーケンスが状態移行ポイントへデータを送信します。 そして、オペレーティング システムが展開されると、復元のタスク シーケンスがデータを取得し、展開先のコンピューターにユーザー状態を復元します。  

- ユーザー状態データは特定の場所にローカルに保存できます。 このシナリオでは、キャプチャのタスク シーケンスはユーザー データを対象となるコンピューターの特定の場所にコピーします。 そして、オペレーティング システムが展開されると、復元のタスク シーケンスがその場所からユーザー データを取得します。  

- ユーザー データを元の場所に復元するために使用するハード リンクを指定できます。 このシナリオでは、古いオペレーティング システムが消去されてもユーザー状態データはドライブに保持されます。 そして、オペレーティング システムが展開されると、復元のタスク シーケンスがハード リンクを使用して、元の場所にユーザー状態データを復元します。  

  詳細については、「[Manage user state](../get-started/manage-user-state.md)」(ユーザー状態の管理) を参照してください。  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a> 不明なコンピューターへの展開  
 Configuration Manager で管理されていないコンピューターにオペレーティング システムを展開できます。 これらのコンピューターのレコードは Configuration Manager データベースには存在しません。 このようなコンピューターは「不明なコンピューター」と呼ばれます。 不明なコンピューターには次のようなものがあります。  

- Configuration Manager クライアントがインストールされていないコンピューター  

- Configuration Manager にインポートされていないコンピューター  

- Configuration Manager で検出されていないコンピューター  

  詳細については、「[不明なコンピューターの展開の準備](../get-started/prepare-for-unknown-computer-deployments.md)」を参照してください。  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a> ユーザーとデバイスの関連付け  
 オペレーティング システムを展開する際に、ユーザーを展開先のコンピューターに関連付け、ユーザーとデバイスのアフィニティ操作に対応できます。 ユーザーを展開先のコンピューターに関連付けると、管理者ユーザーが後から、特定のユーザーのコンピューターへのアプリケーションの展開など、そのユーザーに関連付けられたコンピューターに対して操作を実行できます。 しかし、オペレーティング システムを展開する際は、特定のユーザーのコンピューターに対してオペレーティング システムを展開することはできません。 詳細については、「[展開先のコンピューターにユーザーを関連付ける](../get-started/associate-users-with-a-destination-computer.md)」をご覧ください。  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a> ステップを自動化するためのタスク シーケンスの使用  
 Configuration Manager 環境内でさまざまなタスクを実行するためのタスク シーケンスを作成できます。 タスク シーケンス アクションは、シーケンスの個別のステップで定義されます。 タスク シーケンスを実行する際、各ステップの操作がコマンドライン レベルで実行され、ユーザー操作は不要です。 タスク シーケンスを使用して、次のことを行うことができます。  

-   [オペレーティング システムをインストールするタスク シーケンスの作成](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [オペレーティング システム以外の展開用タスク シーケンスの作成](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [オペレーティング システムをキャプチャするタスク シーケンスの作成](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [ユーザー状態をキャプチャおよび復元するタスク シーケンスの作成](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [カスタム タスク シーケンスの作成](../deploy-use/create-a-custom-task-sequence.md)  
