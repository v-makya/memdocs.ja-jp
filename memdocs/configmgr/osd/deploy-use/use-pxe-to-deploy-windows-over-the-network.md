---
title: ネットワーク経由で OSD に PXE を使用する
titleSuffix: Configuration Manager
description: PXE による OS の展開を使用して、コンピューターのオペレーティング システムを更新するか、新しいコンピューターに新しいバージョンの Windows をインストールします。
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cff249bf5289ebcf354851258b5c9d598314ce3b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709060"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager で PXE を使用して Windows をネットワーク経由で展開する

*適用対象:Configuration Manager (Current Branch)*

System Center Configuration Manager での PXE (Preboot execution environment) によるオペレーティング システムの展開では、クライアント コンピューターはネットワーク経由でオペレーティング システムを要求し、展開することができます。 この展開シナリオでは、OS イメージとブート イメージを PXE 対応配布ポイントに送信します。

> [!NOTE]  
> x64 BIOS コンピューターのみを対象とする OS の展開を作成する場合は、配布ポイントに x64 ブート イメージと x86 ブート イメージの両方を用意する必要があります。

PXE を使用した OS の展開は、次のシナリオで使用できます。

- [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

いずれかの OS の展開シナリオのステップを完了させてから、この記事のセクションを参照して、PXE による展開を準備します。

> [!WARNING]
> PXE 展開を使用し、最初のブート デバイスとしてネットワーク アダプターを使用するデバイス ハードウェアを構成すると、これらのデバイスでは、ユーザーの操作なしで OS 展開のタスク シーケンスを自動的に開始できます。 展開の検証では、この構成は管理されません。 この構成により、プロセスが簡略化され、ユーザーの操作が減少する可能性がありますが、デバイスが誤って再イメージ化されるリスクが高くなります。

## <a name="configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> PXE 要求を許可するために少なくとも 1 つの配布ポイントを構成する

PXE ブート要求を作成する Configuration Manager クライアントにオペレーティング システムを展開するには、PXE 要求を受け入れるように 1 つ以上の配布ポイントを構成する必要があります。 構成された配布ポイントは、PXE ブート要求に応答し、実行する適切な展開アクションを決定します。 詳細については、[配布ポイントのインストールと変更に関するトピック](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)を参照してください。  

> [!NOTE]  
> 複数のサブネットをサポートする目的で PXE 対応配布ポイントを 1 つ構成するとき、DHCP オプションの使用はサポートされません。 PXE 対応配布ポイントへの PXE 要求の転送を許可するようにルーター上で IP ヘルパーを構成してください。
>
> バージョン 1810 では、DHCP サーバーも実行しているサーバーで、WDS なしで PXE レスポンダーを使用することはサポートされていません。
>
> バージョン 1902 以降では、Windows 展開サービスのない配布ポイントで PXE レスポンダーを有効にするときは、DHCP サービスと同じサーバーでもかまわなくなりました。<!--3734270, SCCMDocs-pr #3416--> この構成をサポートするには、次の設定を追加します。  
>
> - レジストリ キー `HKLM\Software\Microsoft\SMS\DP` で DWord 値 **DoNotListenOnDhcpPort** を `1` に設定します。
> - DHCP オプション 60 を `PXEClient` に設定します。  
> - サーバーで SCCMPXE サービスと DHCP サービスを再起動します。  

## <a name="prepare-a-pxe-enabled-boot-image"></a>PXE 対応のブート イメージの作成

PXE を使用して OS を展開するには、1 つ以上の PXE 対応配布ポイントに配布される、x86 と x64 の両方の PXE 対応ブート イメージが必要です。 この情報を使用して、ブート イメージで PXE を有効にして、配布ポイントにブート イメージを配布します。

- ブート イメージで PXE を有効にするには、 **[データ ソース]** タブのブート イメージ プロパティで、 **[このブート イメージを PXE 対応の配布ポイントから展開する]** を選択します。

- ブート イメージのプロパティを変更する場合は、ブート イメージを更新して配布ポイントに再配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)」をご覧ください。

## <a name="manage-duplicate-hardware-identifiers"></a>重複するハードウェア識別子を管理する

複数のコンピューターが重複する SMBIOS 属性を持っている場合、または共有ネットワーク アダプターを使用している場合は、Configuration Manager で複数のコンピューターが同じデバイスとして認識される場合があります。 階層の設定で重複するハードウェア識別子を管理することにより、これらの問題を軽減できます。 詳細については、「[重複するハードウェア識別子を管理する](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)」を参照してください。

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> PXE 展開の除外リストの作成

> [!Note]  
> 状況によっては、[重複するハードウェア識別子を管理する](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)プロセスが容易になります。<!-- SCCMDocs issue 802 -->
>
> 一部のシナリオでは、動作ごとに結果が異なる場合があります。 除外リストにある MAC アドレスを持つクライアントは、何があっても決して起動されることはありません。
>
> 重複する ID のリストでは、クライアントのタスク シーケンスのポリシーの検索に MAC アドレスは使用されません。 SMBIOS ID と一致する場合、または不明なマシンのタスク シーケンス ポリシーがある場合は、クライアントは引き続き起動します。

PXE を使用してオペレーティング システムを展開する場合、配布ポイントで除外リストを作成できます。 除外リストには、配布ポイントが無視すべきコンピューターの MAC アドレスを追加します。 リストに追加されたコンピューターは、Configuration Manager が PXE 展開で使用する展開タスク シーケンスを受け取りません。

### <a name="process-to-create-the-exclusion-list"></a>除外リストを作成するプロセス

1. PXE 対応の配布ポイントにテキスト ファイルを作成します。 例として、このテキスト ファイルを **pxeExceptions.txt**と名づけます。  

2. メモ帳などのプレーン テキスト エディターを使用して、PXE 対応配布ポイントが無視するべきコンピューターの MAC アドレスを追加します。 MAC アドレス値はコロンを使って区切り、各アドレスを別の行に入力します。 例: `01:23:45:67:89:ab`  

3. PXE 対応の配布ポイント サイト システム サーバーにテキスト ファイルを保存します。 テキスト ファイルはサーバーの任意の場所に保存できます。  

4. PXE 対応配布ポイントのレジストリを編集して、**MACIgnoreListFile** レジストリ キーを作成します。 PXE 対応の配布ポイント サイト システム サーバーでテキスト ファイルのフル パスの文字列値を追加します。 次のレジストリ パスを使用します。  

    `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    > レジストリ エディターの使用方法を誤ると、重大な問題が発生し、Windows の再インストールが必要になることがあります。 レジストリ エディターの使用方法を誤った結果生じた問題については、解決できる保証はありません。 レジストリ エディターは、各自の責任で使用してください。  

5. このレジストリの変更後に、WDS サービスまたは PXE レスポンダー サービスを再起動します。 サーバーを再起動する必要はありません。<!--512129-->  

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a> RamDisk TFTP ブロック サイズとウィンドウ サイズ

PXE 対応配布ポイントの RamDisk TFTP ブロック サイズとウィンドウ サイズをカスタマイズできます。 ネットワークをカスタマイズしている場合、ブロックまたはウィンドウのサイズが大きいと、ブート イメージのダウンロードがタイムアウト エラーで失敗する可能性があります。 RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズにより、特定のネットワーク要件に対応する PXE を使用する場合に、TFTP トラフィックを最適化できます。 最も効率的な構成を判断するには、環境内でカスタマイズした設定をテストします。 詳細については、「[PXE 対応配布ポイント上の RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズ](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)」を参照してください。

## <a name="configure-deployment-settings"></a>展開の設定の構成

PXE による OS の展開を使用するには、OS を PXE ブート要求から使用できるように展開を構成します。 展開のプロパティの **[展開設定]** タブで、使用できるオペレーティング システムを構成します。 **[利用できるようにする項目]** の設定では、次のいずれかのオプションを選択します。

- Configuration Manager クライアント、メディア、PXE

- メディアと PXE のみ

- メディアと PXE のみ (非表示)

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> タスク シーケンスの展開

ターゲット コレクションに OS を展開します。 詳細については、「 [Deploy a task sequence](deploy-a-task-sequence.md)」をご覧ください。 PXE を使用してオペレーティング システムを展開するとき、展開が必須か使用可能かを設定することができます。

- **必要な展開**:必要な展開では、ユーザーの介入なしに、PXE を使用します。 ユーザーは PXE ブートをバイパスできません。 ただし、ユーザーが配布ポイントが応答する前に PXE ブートをキャンセルすれば、OS は展開されません。

- **利用可能な展開**:利用可能な展開では、ユーザーがセットアップ先のコンピューターにいる必要があります。 ユーザーは、PXE ブート プロセスを続けるために **F12** キーを押す必要があります。 **F12** キーを押すユーザーがいない場合、コンピューターは現在の OS、または次に利用可能なブート デバイスから起動します。

Configuration Manager コレクションまたはコンピューターに割り当てられた最終の PXE 展開の状態をクリアすることにより、必要な PXE 展開を再展開することができます。 **必須の PXE 展開の消去**アクションの詳細については、[クライアントの管理](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)または[コレクションの管理](../../core/clients/manage/collections/manage-collections.md#bkmk_device)に関するトピックを参照してください。 この操作でその展開の状態がリセットされ、最新の必要な展開が再インストールされます。

> [!IMPORTANT]  
> PXE プロトコルはセキュリティ保護されていません。 PXE サーバーと PXE クライアントのどちらも、サイトへの不正なアクセスを防御するデータセンターといった物理的に安全なネットワークに置かれていることを確認します。

## <a name="how-the-boot-image-is-selected-for-pxe"></a>PXE にブート イメージが選択されるしくみ

クライアントが PXE で起動する場合、使用するブート イメージが Configuration Manager によってクライアントに提供されます。 Configuration Manager は、アーキテクチャが厳密に一致するブート イメージを使用します。 正確なアーキテクチャのブート イメージがない場合、Configuration Manager は、互換性のあるアーキテクチャを持つブート イメージを使用します。

次の一覧では、PXE ブートのクライアントが使用するブート イメージがどのように選択されるかについて説明します。  

1. Configuration Manager は、ブートしようとしているクライアントの MAC アドレスまたは SMBIOS に一致するシステム レコードをサイト データベースで検索します。  

    > [!NOTE]  
    > サイトに割り当てられているコンピューターを、別のサイトの PXE にブートした場合、そのコンピューターでポリシーを表示できません。 たとえば、クライアントが既にサイト A に割り当てられている場合、サイト B の管理ポイントと配布ポイントは、サイト A のポリシーにアクセスできず、クライアントは正常に PXE ブートしません。  

2. Configuration Manager は、手順 1 で見つかったシステム レコードに展開されているタスク シーケンスを探します。  

3. 手順 2 で見つかったタスク シーケンスの一覧で、Configuration Manager はブートしようとしているクライアントのアーキテクチャに一致するブート イメージを探します。 同じアーキテクチャのブート イメージが見つかった場合は、そのブート イメージを使用します。  

    複数のブート イメージが見つかった場合は、"*最も高い*" または最新のタスク シーケンス展開 ID が使用されます。 複数サイトの階層の場合、その文字列比較で文字が*アルファベット順で後の方*の文字があるサイトが優先されます。 たとえば、他の点では双方が一致している場合、サイト AAA からの昨日の展開よりも、サイト ZZZ からの 1 年前の展開が選択されます。<!-- SCCMDocs issue 877 -->  

4. 同じアーキテクチャのブート イメージが見つからなかった場合、Configuration Manager は、クライアントのアーキテクチャと互換性があるブート イメージを探します。 手順 2. で見つかったタスク シーケンスの一覧で探します。 たとえば、64 ビット BIOS/MBR クライアントは、32 ビットおよび 64 ビットのブート イメージと互換性があります。 32 ビット BIOS/MBR クライアントは、32 ビットのブート イメージのみと互換性があります。 UEFI クライアントは、一致するアーキテクチャとのみ互換性があります。 64 ビット UEFI クライアントは、64 ビットのブート イメージとのみ互換性があり、32 ビット UEFI クライアントは、32 ビットのブート イメージとのみ互換性があります。
