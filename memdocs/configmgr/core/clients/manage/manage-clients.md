---
title: クライアントを管理する
titleSuffix: Configuration Manager
description: Configuration Manager でクライアントを管理する方法について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b6d1ee82e116a6d4375e37ccca84c8b35707f8e1
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334591"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Configuration Manager でクライアントを管理する方法

*適用対象:Configuration Manager (Current Branch)*

デバイスに Configuration Manager クライアントがインストールされてサイトに正常に割り当てられると、 **[デバイス]** ノードの **[資産とコンプライアンス]** ワークスペース、および **[デバイス コレクション]** ノードの 1 つまたは複数のコレクションにデバイスが表示されます。 デバイスまたはコレクションを選択し、管理操作を実行します。 ただし、コンソールの他のワークスペースを使用するか、コンソールの外部のタスクを実行して、別の方法でクライアントを管理することもできます。  

> [!NOTE]  
> Configuration Manager クライアントをインストールするが、まだサイトには正常に割り当てられていない場合、コンソールに表示されない可能性があります。 クライアントがサイトに割り当てられたら、コレクション メンバーシップを更新し、コンソール ビューを更新します。  
>
> Configuration Manager クライアントがインストールされていないとき、デバイスがコンソールに表示されることもあります。 この動作は、サイトでデバイスが検出されても、クライアントがインストールされておらず、割り当てられていない場合に発生します。
>
> [Exchange Server コネクタ](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)または[オンプレミス MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) で管理されるモバイル デバイスでは、Configuration Manager クライアントはインストールされません。  
>
> コンソールからデバイスを管理するには、 **[デバイス]** ノードの **[クライアント]** 列を使用し、クライアントがインストールされているかどうかを判断します。  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> **[デバイス]** ノードからクライアントを管理する  

デバイスの種類によっては、一部のオプションを使用できません。  

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス]** ノードを選択します。  

2. 1 つまたは複数のデバイスを選択し、リボンからクライアント管理タスクのいずれかを選択します。 デバイスを右クリックする方法もあります。  

### <a name="import-user-device-affinity"></a>ユーザーとデバイスのアフィニティのインポート

ユーザーとデバイスの関連付けを構成して、ユーザーにソフトウェアを効率的に展開することができます。  

詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。

### <a name="import-computer-information"></a>[コンピューター情報のインポート]

**コンピューター情報のインポート ウィザード**を起動し、新しいコンピューター情報を Configuration Manager データベースにインポートします。 ファイルを使用して複数のコンピューターをインポートしたり、1 台のコンピューターの情報を指定したりすることができます。

### <a name="add-selected-items"></a>選択された項目の追加

次のオプションが提供されます。

- **[選択した項目を既存のデバイス コレクションに追加する]** : **[コレクションの選択]** ダイアログ ボックスを開きます。 このデバイスを追加するコレクションを選択します。 **ダイレクト** メンバーシップの規則を使用することで、デバイスがこのコレクションに含まれます。  

- **[選択した項目を新しいデバイス コレクションに追加する]** :新しいコレクションを作成できる**デバイス コレクションの作成ウィザード**を開きます。 **ダイレクト** メンバーシップの規則を使用することで、選択したコレクションがこのコレクションに含まれます。  

詳しくは、「[コレクションを作成する方法](collections/create-collections.md)」をご覧ください。

### <a name="install-client"></a>クライアントのインストール

**クライアントのインストール ウィザード**を開きます。 このウィザードでは、クライアント プッシュのインストールを使用し、選択したデバイスに Configuration Manager クライアントをインストールまたは再インストールします。

> [!TIP]  
> Configuration Manager クライアントをインストールするには、さまざまな方法があります。 クライアント プッシュ ウィザードにはコンソールからクライアントをインストールする便利な方法がありますが、この方法にはさまざまな依存関係があり、すべての環境に適しているわけではありません。 依存関係の詳細については、[Windows コンピューターにクライアントを展開するための前提条件](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation)に関するページを参照してください。 その他のクライアント インストール方法について詳しくは、[クライアントのインストール方法](../deploy/plan/client-installation-methods.md)に関するページをご覧ください。

詳細については、[クライアント プッシュを使用した Configuration Manager クライアントのインストール方法](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)に関する記述を参照してください。

### <a name="run-script"></a>スクリプトの実行

**スクリプトの実行**ウィザードを起動し、選択したデバイスで PowerShell スクリプトを実行します。

詳しくは、「[PowerShell スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)」をご覧ください。

### <a name="install-application"></a>アプリケーションのインストール

アプリケーションをデバイスにリアルタイムでインストールします。 この機能により、アプリケーションごとにコレクションを用意する必要性が減ります。

詳しくは、「[デバイスへのアプリケーションのインストール](../../../apps/deploy-use/install-app-for-device.md)」をご覧ください。

### <a name="reassign-site"></a>サイトの再割り当て

1 つまたは複数のクライアント (管理しているモバイル デバイスを含む) を、階層内の別のプライマリ サイトに再割り当てします。 クライアントを個別に再割り当てするか、複数のクライアントを選択して一括で再割り当てをすることができます。  

### <a name="client-settings---resultant-client-settings"></a>クライアント設定 - クライアントの設定の結果

同じデバイスに複数のクライアント設定を展開すると、設定の優先順位と組み合わせが複雑になります。 このオプションを使用すると、このデバイスに展開されるクライアント設定の結果セットが表示されます。

詳しくは、「[クライアント設定を構成する方法](../deploy/configure-client-settings.md)」をご覧ください。

### <a name="start"></a>開始

- **リソース エクスプローラー**を実行し、Windows クライアントからのハードウェアとソフトウェアのインベントリ情報を表示します。 詳細については、以下の記事を参照してください。

  - [リソース エクスプローラーを使用してハードウェア インベントリを表示する方法](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [リソース エクスプローラーを使用してソフトウェア インベントリを表示する方法](inventory/use-resource-explorer-to-view-software-inventory.md)

- **リモート制御**、**リモート アシスタンス**、または**リモート デスクトップ クライアント**を使用し、デバイスをリモートで管理します。 詳細については、「[Windows クライアント コンピューターをリモート管理する方法](remote-control/remotely-administer-a-windows-client-computer.md)」を参照してください。

### <a name="approve"></a>承認

クライアントが HTTP および自己署名証明書を使用してサイト システムと通信する場合、信頼されるコンピューターとして識別されるように、これらのクライアントを承認する必要があります。 既定では、サイト構成により、同じ Active Directory フォレスト、信頼済みフォレスト、接続済み Azure Active Directory (Azure AD) テナントからのクライアントは自動的に承認されます<!-- MEMDocs#318 -->。 この既定の動作により、各クライアントを手動で承認する必要がありません。 信頼できるワークグループ コンピューターと、信頼できるが承認されていないその他のコンピューターは手動で承認します。

> [!IMPORTANT]  
> 一部の管理機能は承認されていないクライアントでも動作する可能性がありますが、このシナリオは Configuration Manager ではサポートされていません。  

常に HTTPS を使用してサイト システムと通信するクライアントや、HTTP を使用してサイト システムと通信する際に PKI 証明書を使用するクライアントは、承認する必要はありません。 これらのクライアントは、PKI 証明書を使用して信頼を確立します。

### <a name="block-or-unblock"></a>ブロックまたはブロック解除する

信頼できなくなったクライアントをブロックします。 ブロックすると、クライアントはポリシーを受信できなくなり、サイト システムはクライアントと通信できなくなります。  

> [!IMPORTANT]  
> クライアントをブロックすると、クライアントから Configuration Manager サイト システムへの通信のみ防ぐことができます。 他のデバイスへの通信を防ぐことはできません。 HTTPS の代わりに HTTP を使用してクライアントがサイト システムに通信する場合、セキュリティ上の制限がいくつか生じます。  

ブロックされているクライアントのブロックを解除することもできます。

詳しくは、[クライアントをブロックするかどうかの判断](../deploy/plan/determine-whether-to-block-clients.md)に関するページをご覧ください。

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>必須の PXE 展開の消去

Configuration Manager コレクションまたはコンピューターに割り当てられた最終の PXE 展開の状態をクリアすることにより、必要な PXE 展開を再展開することができます。 この操作でその展開の状態がリセットされ、最新の必要な展開が再インストールされます。

詳細については、「[PXE を使用したネットワーク経由での Windows の展開](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。

### <a name="client-notification"></a>クライアント通知

詳細については、[クライアント通知](client-notification.md#client-notification)に関するページをご覧ください。

### <a name="endpoint-protection"></a>Endpoint Protection

詳細については、[クライアント通知](client-notification.md#endpoint-protection)に関するページをご覧ください。

### <a name="edit-primary-users"></a>プライマリ ユーザーの編集

過去 90 日間を対象にこのデバイスのユーザーを表示するか、このデバイスのプライマリ ユーザーを指定します。

詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。

### <a name="wipe-a-mobile-device"></a>モバイル デバイスをワイプする

ワイプ コマンドをサポートするモバイル デバイスをワイプできます。 この操作により、個人設定や個人データを含め、モバイル デバイスのすべてのデータが削除されます。 通常、この操作で、モバイル デバイスが工場出荷時の設定にリセットされます。 信頼されなくなったモバイル デバイスをワイプします。 たとえば、デバイスの紛失時や盗難時などです。  

> [!TIP]  
> モバイル デバイスでリモート ワイプ コマンドがどのように処理されるかについては、製造元のドキュメントを参照してください。  

モバイル デバイスがワイプ コマンドを受信するまで、通常、待ち時間が発生します。  

- モバイル デバイスが Configuration Manager によって登録されている場合、クライアントはそのクライアント ポリシーのダウンロード時にコマンドを受信します。

- モバイル デバイスが Exchange Server コネクタによって管理されている場合、Exchange との同期時にコマンドを受信します。  

デバイスがワイプ コマンドを受信するタイミングを監視するには、 **[ワイプのステータス]** 列を使用します。 デバイスが Configuration Manager にワイプ確認を送信するまで、ワイプ コマンドをキャンセルできます。  

### <a name="retire-a-mobile-device"></a>モバイル デバイスをインベントリから削除する

**[インベントリから削除する]** オプションをサポートしているのは、オンプレミス MDM によって登録されたモバイル デバイスのみです。  

詳細については、[リモート ワイプ、リモート ロック、パスコードのリセットを使用したデータの保護](../../../mdm/deploy-use/wipe-lock-reset-devices.md)に関するページを参照してください。

### <a name="change-ownership"></a>所有権の変更

デバイスがドメインに参加しておらず、Configuration Manager クライアントがインストールされていない場合は、このオプションを使用し、所有権を **[会社]** または **[個人]** に変更できます。  

アプリケーションの要件にこの値を使用して、展開を制御できます。また、ユーザー デバイスから収集するインベントリの量を制御できます。  

また、必要に応じて、列見出しを右クリックして選択し、ビューに **[デバイスの所有者]** 列を追加することもできます。

### <a name="delete"></a>削除

> [!WARNING]  
> Configuration Manager クライアントをアンインストールする場合やコレクションから削除する際、クライアントを削除しないでください。  

**削除**操作では、Configuration Manager データベースからクライアント レコードを手動で削除します。 この操作は、問題を解決する目的でのみ使用します。 オブジェクトを削除しても、クライアントがまだインストールされており、サイトと通信している場合は、定期探索によりクライアント レコードが再作成されます。 クライアント履歴とすべての以前の関連付けは失われますが、Configuration Manager コンソールにはクライアント レコードが再表示されます。  
> [!NOTE]  
> Configuration Manager によって登録されたモバイル デバイス クライアントを削除すると、発行された PKI 証明書も失効します。 この証明書は、IIS で証明書失効リスト (CRL) が確認されなくても、管理ポイントによって拒否されます。
>
> モバイル デバイス レガシ クライアントを削除しても、これらのクライアントの証明書は失効しません。

クライアントをアンインストールするには、[Configuration Manager クライアントのアンインストール](#BKMK_UninstalClient)に関するセクションを参照してください。  

クライアントを新しいプライマリ サイトに割り当てるには、[サイトにクライアントを割り当てる方法](../deploy/assign-clients-to-a-site.md)に関するページをご覧ください。

クライアントをコレクションから削除するには、コレクションのプロパティを再構成します。 詳しくは、「[コレクションを管理する方法](collections/manage-collections.md)」をご覧ください。

### <a name="refresh"></a>最新の情報に更新

データベースの最新データでコンソール ビューを更新します。 たとえば、デバイスが検出からの一覧に表示されるが、インストール済みとして表示されないことがあります。 クライアントをインストールし、サイトに割り当てられていることを確認したら、 **[最新の情報に更新]** を選択します。

### <a name="properties"></a>プロパティ

クライアントを対象とした探索データと展開を表示します。

また、OS をデバイスに展開するためにタスク シーケンスで使用される変数を構成できます。 詳細については、[デバイスおよびコレクションのタスク シーケンスの変数の作成](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var)に関する記事を参照してください。


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> **[デバイス コレクション]** ノードからクライアントを管理する

**[デバイス]** ノードのデバイスで使用可能なタスクの多くは、コレクションでも使用可能です。 コンソールは、コレクション内の対象となるすべてのデバイスに操作を自動的に適用します。 コレクション全体でのこのアクションにより、追加のネットワーク パケットが生成され、サイト サーバー上の CPU 使用率が増加します。  

コレクション レベルのタスクを実行する前に、次の点を考慮してください。 タスクの開始後にコンソールからタスクを停止することはできません。

- コレクション内のデバイス数
- デバイスが低帯域幅のネットワーク接続で接続されているかどうか
- すべてのデバイスでこのタスクを完了するのに必要な時間はどれくらいか

詳しくは、「[コレクションを管理する方法](collections/manage-collections.md)」をご覧ください。


## <a name="restart-clients"></a>クライアントの再起動

Configuration Manager コンソールを使用して、再起動が必要なクライアントを識別します。 その後、クライアント通知アクションを使用して、再開します。

> [!Tip]
> 自動クライアント アップグレードを有効にすると、より少ない作業量でクライアントを最新の状態に保つことができます。 詳しくは、「[自動クライアント アップグレードについて](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)」をご覧ください。

再起動が保留されているデバイスを識別するには、Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス]** ノードを選択します。 次に、詳細ウィンドウの **[再起動を保留中]** という名前の新しい列で、各デバイスの状態を表示します。 各デバイスには次の 1 つ以上の値が示されます。

- **いいえ**: 再起動は保留されていません
- **Configuration Manager**: この値は、クライアントの再起動コーディネーター コンポーネント (RebootCoordinator.log) からのものです
- **ファイル名の変更**: この値は Windows から、ファイル名の変更操作が保留中であることが報告されているものです (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
- **Windows Update**: この値は Windows Update エージェントから、1 つ以上の更新プログラムに対して再起動の保留が必要であることが報告されているものです (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **機能の追加または削除**: この値は Windows コンポーネント ベースのサービスから、Windows 機能を追加または削除するには再起動が必要であることが報告されているものです (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending)

### <a name="create-the-client-notification-to-restart-a-device"></a>クライアント通知を作成してデバイスを再起動する

1. コンソールの **[デバイス コレクション]** ノードで、コレクション内の再起動するデバイスを選択します。
2. リボンで **[クライアント通知]** を選択し、 **[再起動]** を選択します。 再起動に関する情報ウィンドウが開きます。 **[OK]** を選択し、再起動要求を確定します。

クライアントが通知を受信すると、 **[ソフトウェア センター]** 通知ウィンドウが開き、ユーザーに再起動について通知されます。 既定では、再起動は 90 分後に行われます。 [クライアント設定](../deploy/configure-client-settings.md)を構成すると、再起動の時間を変更できます。 再起動の動作に関する設定は、既定の設定の [[コンピューターの再起動]](../deploy/about-client-settings.md#computer-restart) タブにあります。


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a> クライアント キャッシュを構成する

クライアントでアプリケーションとプログラムをインストールすると、一時ファイルがクライアント キャッシュに格納されます。 ソフトウェアの更新ではクライアント キャッシュも使用されますが、サイズ設定に関係なく、常にキャッシュへのダウンロードが試みられます。 クライアントを手動でインストールする場合、クライアント プッシュ インストールを使用する場合、またはインストール後に、サイズや場所など、キャッシュ設定を構成します。

Configuration Manager コンソールのクライアント設定を利用し、キャッシュ フォルダーのサイズを指定できます。 詳細については、「[クライアントのキャッシュ設定](../deploy/about-client-settings.md#client-cache-settings)」を参照してください。

Configuration Manager クライアント キャッシュの規定の場所は `%windir%\ccmcache` であり、既定のディスク容量は 5,120 MB です。  

> [!IMPORTANT]  
> クライアント キャッシュに使用するフォルダーは暗号化しないでください。 Configuration Manager では、暗号化されているフォルダーにコンテンツをダウンロードできません。  

### <a name="about-the-client-cache"></a>クライアント キャッシュについて  

Configuration Manager クライアントは、展開の使用可能な時間直後に要求されたソフトウェアのコンテンツをダウンロードしますが、展開のスケジュールされた時刻まで、それを実行しません。 スケジュールされた時刻になると、Configuration Manager クライアントはコンテンツがキャッシュで利用可能かどうかを確認します。 コンテンツがキャッシュ内にあり、バージョンが正しい場合、クライアントではキャッシュされたコンテンツが使用されます。 要求されたコンテンツのバージョンが変更されたり、クライアントが別のパッケージのためにコンテンツを削除したりした場合、クライアントは再びコンテンツをキャッシュにダウンロードします。  

クライアントがキャッシュのサイズより大きいプログラムまたはアプリケーションのコンテンツをダウンロードしようとすると、キャッシュ サイズが十分でないため、展開が失敗します。 キャッシュ サイズが十分でない場合、クライアントはステータス メッセージ 10050 を生成します。 後でキャッシュ サイズを増やすと、結果は次のようになります。  

- 要求されるプログラムの場合:クライアントでは、コンテンツのダウンロードが自動的に再試行されることはありません。 クライアントにパッケージとプログラムを再展開します。  
- 要求されるアプリケーションの場合:クライアントは、クライアント ポリシーをダウンロードするときに、自動的にコンテンツのダウンロードを再試行します。  

クライアントがダウンロードしようとするコンテンツのサイズがキャッシュ サイズより小さくても、キャッシュに空きがない場合、次の状態になるまで、*要求された*すべての展開は再試行を繰り返します。

- キャッシュ領域が利用可能になる
- ダウンロードがタイムアウトする
- 再試行回数の制限に達する

後でキャッシュ サイズを増やせば、クライアントでは、次回の再試行時にコンテンツの再ダウンロードが試行されます。 クライアントは試行回数が 18 回になるまで 4 時間ごとにコンテンツのダウンロードを試みます。  

キャッシュされたコンテンツが自動的に削除されることはありません。 クライアントでそのコンテンツが使用された後、少なくとも 1 日はキャッシュに残ります。 クライアント キャッシュにコンテンツを保持するオプションでコンテンツを構成すると、それがクライアントによって自動的に削除されることはありません。 キャッシュ領域が、24 時間以内にダウンロードされたコンテンツによって使用されているときに、クライアントが新しいコンテンツをダウンロードする必要がある場合は、キャッシュ サイズを増やすか、保持しているキャッシュ コンテンツを削除するためのオプションを選択します。

アプリケーションの場合のみ、関連する展開のコンテンツが現在キャッシュに存在する場合は、新しいまたは変更されたファイルのみがクライアントによってダウンロードされます。 関連する展開には、同じ種類の展開のより古いリビジョンのもの、および置き換えられたアプリケーションのものが含まれます。

手動によるクライアントのインストール中またはクライアントのインストール後に、クライアント キャッシュを構成するには、次の手順を使用します。  

### <a name="configure-the-cache-during-manual-client-installation"></a>クライアントの手動インストール中にキャッシュを構成する  

必要に応じて次のプロパティを指定して、インストール ソースの場所から CCMSetup.exe コマンドを実行します。プロパティはスペースで区切ります。  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > SMSCACHESIZE ではなく Configuration Manager コンソールの **[クライアント設定]** で使用可能なキャッシュ サイズ設定を使用します。 詳細については、「[クライアントのキャッシュ設定](../deploy/about-client-settings.md#client-cache-settings)」を参照してください。

CCMSetup.exe のこれらのコマンド ライン プロパティの使用方法の詳細については、「[クライアント インストールのプロパティについて](../deploy/about-client-installation-properties.md)」を参照してください。

### <a name="configure-the-cache-during-client-push-installation"></a>クライアントのプッシュ インストール中にキャッシュを構成する  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2. 適切なサイトを選択します。 リボンの **[ホーム]** タブの **[設定]** グループで、 **[クライアント インストール設定]** を選択し、 **[クライアント プッシュ インストール]** を選択します。 **[インストールのプロパティ]** タブに切り替えます。  

3. スペース区切りで次のプロパティを指定します。  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > SMSCACHESIZE ではなく Configuration Manager コンソールの **[クライアント設定]** で使用可能なキャッシュ サイズ設定を使用します。 詳細については、「[クライアントのキャッシュ設定](../deploy/about-client-settings.md#client-cache-settings)」を参照してください。

     CCMSetup.exe のこれらのコマンド ライン プロパティの使用方法の詳細については、「[クライアント インストールのプロパティについて](../deploy/about-client-installation-properties.md)」を参照してください。  

### <a name="configure-the-cache-on-the-client-computer"></a>クライアント コンピューターでキャッシュを構成する  

1. クライアント コンピューターで **[Configuration Manager]** コントロール パネルを開きます。  

2. **[キャッシュ]** タブに切り替えます。領域と場所のプロパティを設定します。 既定の場所は `%windir%\ccmcache` です。  

3. キャッシュ フォルダーのファイルを削除するには、 **[ファイルの削除]** を選択します。  

### <a name="configure-client-cache-size-in-client-settings"></a>[クライアント設定] でクライアント キャッシュ サイズを構成する

クライアント キャッシュ フォルダーのサイズを調整するとき、クライアントを再インストールする必要がありません。 Configuration Manager コンソールの **[クライアント設定]** で使用可能なキャッシュ サイズ設定を使用します。 詳細については、「[クライアントのキャッシュ設定](../deploy/about-client-settings.md#client-cache-settings)」を参照してください。


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a> クライアントをアンインストールする

**/Uninstall** プロパティを付けて **CCMSetup.exe** を使用すると、Configuration Manager クライアント ソフトウェアをコンピューターからアンインストールできます。 個々のコンピューター上でコマンド プロンプトから CCMSetup.exe を実行するか、パッケージを展開して、コンピューターのコレクションからクライアントをアンインストールします。  

> [!NOTE]  
> Configuration Manager クライアントをモバイル デバイスからアンインストールすることはできません。 Configuration Manager クライアントをモバイル デバイスから除去する必要がある場合は、デバイスをワイプする必要があります。ワイプはモバイル デバイス上のすべてのデータを削除します。  

1. Windows コマンド プロンプトを管理者として開きます。 CCMSetup.exe のある場所にフォルダーを変更します (例: `cd %windir%\ccmsetup`)。

2. 次のコマンドを実行します。`CCMSetup.exe /uninstall`

> [!TIP]  
> アンインストールを実行しても、画面に結果は表示されません。 クライアントが正常にアンインストールされたことを確認するには、ログ ファイル `%windir%\ccmsetup\logs\CCMSetup.log` を参照します。  
>
> 別の何かを行う前にアンインストール プロセスの完了を待たなければならない場合、PowerShell で `Wait-Process CCMSetup` を実行します。 このコマンドでは、CCMSetup プロセスが完了する前にスクリプトを一時停止できます。


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a> 競合しているレコードを管理する

Configuration Manager はハードウェア ID を使用して、重複している可能性のあるクライアントを特定し、競合するレコードについて警告を発します。 たとえば、コンピューターを再インストールする場合、ハードウェア ID が同じであっても Configuration Manager で使用される GUID が異なる可能性があります。  

Configuration Manager は、コンピューター アカウントの Windows 認証または信頼されたソースからの PKI 証明書を使用して、競合を自動的に解決します。 重複するハードウェア識別子の競合を Configuration Manager で解決できないとき、階層設定により動作が決定されます。

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>競合しているレコードの管理に関する階層の設定を変更する  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。

1. リボンで **[階層設定]** を選択します。

1. **[クライアントの承認と競合レコードの処理]** タブに切り替え、次のいずれかのオプションを選択します。

    - **競合しているレコードを自動で解決する**
    - **競合しているレコードを手動で解決する**

### <a name="manually-resolve-conflicting-records"></a>競合しているレコードを手動で解決する  

1. Configuration Manager コンソールで、 **[監視]** ワークスペースに移動し、 **[システム ステータス]** を展開し、 **[競合しているレコード]** ノードを選択します。  

1. 1 つまたは複数の競合しているレコードを選択し、 **[競合しているレコード]** をクリックします。  

1. 次のいずれかのオプションを選択します。  

    - **[結合]** :新しく検出されたレコードを既存のクライアント レコードと結合します。  

    - **[新規]** :競合しているクライアント レコードに対して新しいレコードを作成します。  

    - **[ブロック]** :競合しているクライアント レコードに対して新しいレコードを作成しますが、ブロックに設定します。  


## <a name="manage-duplicate-hardware-identifiers"></a>重複するハードウェア識別子を管理する

PXE ブートとクライアント登録で Configuration Manager に無視されるハードウェア ID の一覧を指定できます。 この一覧は、次の 2 つの一般的な問題に対処するのに役立ちます。

1. 新しいデバイスの多くにイーサネット ポートが搭載されていません。 技術者は、OS 展開のために有線接続を確立する場合、USB/イーサネット アダプターを使用します。 コストや汎用性に起因し、多くの場合、これらのアダプターは共有されます。 サイトでは、このアダプターの MAC アドレスを使用してデバイスが識別されます。 そのため、展開のたびに管理者が追加措置を行わなければ、アダプターの再利用が問題を引き起こします。 このシナリオでアダプターを再利用するには、その MAC アドレスを除外します。

2. SMBIOS 属性を一意にする必要がありますが、専門的なハードウェア デバイスには ID が重複するものもあります。 この重複する ID を除外し、各デバイスの一意の MAC アドレスに依存します。

Configuration Manager で無視するハードウェア識別子は次の手順で追加します。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。

2. リボンの **[ホーム]** タブの **[サイト]** グループで、 **[階層設定]** を選択します。

3. **[クライアントの承認と競合レコードの処理]** タブに切り替えます。新しいハードウェア識別子を追加するには、 **[重複するハードウェア ID]** セクションで **[追加]** を選択します。

> [!TIP]
> バージョン 1910 以降、次の PowerShell コマンドレットを使用して、重複するハードウェア識別子の管理を自動化します。<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a> ポリシーの取得を開始する

Configuration Manager クライアントでは、クライアント設定として構成されているスケジュールに従ってクライアント ポリシーがダウンロードされます。 クライアントからオンデマンド ポリシー取得を開始することもできます。 たとえば、トラブルシューティングやテストの場合に行います。  

- [クライアント通知](#bkmk_policy-notify)
- [クライアント コントロール パネル](#bkmk_policy-manual)
- [サポート センター](#bkmk_policy-support)
- [スクリプト](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a> クライアント通知を使用してクライアント ポリシーの取得を開始する  

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動し、 **[デバイス]** を選択します。  

1. ポリシーをダウンロードするデバイスを選択します。 リボンの **[ホーム]** タブの **[デバイス]** グループで、 **[クライアント通知]** を選択し、 **[コンピューター ポリシーのダウンロード]** を選択します。  

    > [!NOTE]  
    > クライアント通知を使用し、あるコレクション内のすべてのデバイスを対象にポリシー取得を開始することもできます。  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a> Configuration Manager のクライアント コントロール パネルからクライアント ポリシー取得を開始する

1. コンピューターで **Configuration Manager** コントロール パネルを開きます。  

2. **[操作]** タブに切り替えます。 **[コンピューター ポリシーの取得および評価サイクル]** を選択してコンピューター ポリシーを開始し、 **[直ちに実行]** を選択します。  

3. **[OK]** を選択してプロンプトを確定します。  

4. その他の操作については、前の手順を繰り返します。 たとえば、ユーザー クライアント設定の**ユーザー ポリシーの取得および評価サイクル**に対して行います。  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a> サポート センターを使用してクライアント ポリシーの取得を開始する

サポート センターを使用し、クライアント ポリシーを要求し、表示する 詳しくは、[サポート センターのリファレンス](../../support/support-center-ui-reference.md#bkmk_support-policy) ページをご覧ください。

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a> スクリプトを使用してクライアント ポリシーの取得を開始する  

1. メモ帳や Windows PowerShell ISE などのスクリプト エディターを開きます。  

2. 次のサンプル PowerShell コードをコピーし、<!-- SCCMDocs#1591 --> ファイルに挿入します。  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > スケジュール ID の詳細については、「[メッセージ ID](../../support/send-schedule-tool.md#bkmk_sendschedule-guids)」を参照してください。

3. 拡張子 .ps1 を使ってファイルを保存します。  

4. クライアントでスクリプトを実行します。
