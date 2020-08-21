---
title: Windows 10 へのアップグレード
titleSuffix: Configuration Manager
description: Configuration Manager を使用して、OS を Windows 7 以降から Windows 10 にアップグレードする方法について説明します。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eb7e2e5c564263c7172d70ec33bb33c0dd73409c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697825"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Windows を最新バージョンの Configuration Manager にアップグレードする

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager でコンピューター上の OS をアップグレードする手順について説明します。 スタンドアロン メディアやソフトウェア センターなどのさまざまな展開方法の中から選ぶことができます。 一括アップグレード シナリオには、次の機能があります。  

- OS を Windows 10 または Windows Server 2016 以降にアップグレードします

- コンピューター上のアプリケーション、設定、ユーザー データは保持されます。

- Windows ADK などの外部依存関係はありません。

- 従来の OS 展開よりも高速で、回復力があります。

> [!Note]  
> Windows 10 の一括アップグレード タスク シーケンスで、[クラウド管理ゲートウェイ](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)を通して管理されるインターネット ベースのクライアントへの展開がサポートされます。 この機能により、リモート ユーザーはより簡単に Windows 10 にアップグレードでき、イントラネットに接続する必要はありません。 詳細については、「[CMG を通して Windows 10 の一括アップグレードを展開する](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)」を参照してください。 <!-- 1357149 -->


## <a name="supported-versions"></a>サポートされるバージョン

### <a name="upgrade-version"></a>アップグレード バージョン

OS アップグレード パッケージのみを作成し、次の OS バージョンにアップグレードします。

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>元のバージョン

OS のアップグレード タスク シーケンスを対象とするには、デバイスで次の OS バージョンのいずれかを実行する必要があります。

#### <a name="windows-client"></a>Windows クライアント

- Windows 7
- Windows 8.1
- 以前のバージョンの Windows 10。 たとえば、Windows 10 バージョン 1809 を Windows 10 バージョン 1903 にアップグレードできます。  

詳細については、「[Windows 10 アップグレード パス](/windows/deployment/upgrade/windows-10-upgrade-paths)」を参照してください。

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- 以前のバージョンの Windows Server 2016
- 以前のバージョンの Windows Server 2019

Windows Server でサポートされているアップグレード パスの詳細については、「[Windows Server 2016 でサポートされているアップグレード パス](/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016)」と「[Windows Server アップグレード センター](https://aka.ms/upgradecenter)」に関するページを参照してください。


## <a name="plan"></a><a name="BKMK_Plan"></a> プラン  

### <a name="task-sequence-requirements-and-limitations"></a>タスク シーケンスの要件と制限事項

OS をアップグレードするタスク シーケンスの次の要件と制限を確認して、ニーズに合うかどうかを確かめます。  

- OS のアップグレードの主要タスクに関連するタスク シーケンス手順のみを追加します。 この手順には、主にパッケージ、アプリケーション、または更新プログラムのインストールが含まれます。 コマンド ライン、PowerShell を実行する手順、または動的変数を設定する手順も使用します。  

- コンピューターにインストールされているドライバーとアプリケーションを確認します。 アップグレード タスク シーケンスを展開する前に、ドライバーが Windows 10 と互換性があることを確認してください。  

次のタスクは、一括アップグレードとの互換性がありません。 これらのタスクでは、従来の OS 展開方法を使用する必要があります。  

- コンピューターのドメイン メンバーシップを変更する。またはローカル管理者グループを更新する。  

- 次のようなコンピューターの基本的な変更を実装する。

  - ディスク パーティションを変更する
  - x86 から x64 にシステム アーキテクチャを変更する
  - UEFI を実装する (使用できるオプションの詳細については、「[インプレース アップグレード時に BIOS から UEFI に変換する](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)」を参照してください)。
  - 基本の OS 言語を変更する  

- カスタム基本イメージの使用、サードパーティ ディスク暗号化の使用、WinPE オフライン操作の採用などのカスタム要件があります。  

### <a name="infrastructure-requirements"></a>インフラストラクチャの要件  

アップグレード シナリオの唯一の前提条件は、配布ポイントが使用可能であることです。 OS アップグレード パッケージとタスク シーケンスに含めるその他のパッケージを配布します。 詳細については、[配布ポイントのインストールと変更に関するトピック](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)を参照してください。


## <a name="configure"></a><a name="BKMK_Configure"></a> 構成  

### <a name="prepare-the-os-upgrade-package"></a>OS アップグレード パッケージを準備する  

Windows 10 アップグレード パッケージには、セットアップ先のコンピューターの OS をアップグレードするのに必要なソース ファイルが含まれています。 このアップグレード パッケージは、アップグレードするクライアントと同じエディション、アーキテクチャ、言語にする必要があります。 詳しくは、[OS のアップグレード パッケージの管理](../get-started/manage-operating-system-upgrade-packages.md)に関するページをご覧ください。  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>OS をアップグレードするタスク シーケンスを作成する  

「[OS をアップグレードするタスク シーケンスの作成](create-a-task-sequence-to-upgrade-an-operating-system.md)」の手順に従って、OS のアップグレードを自動化します。  

> [!NOTE]  
> OS を Windows 10 にアップグレードするタスク シーケンスを作成するには、通常、「[OS をアップグレードするタスク シーケンスの作成](create-a-task-sequence-to-upgrade-an-operating-system.md)」の手順を使用します。 タスク シーケンスには、**OS のアップグレード**の手順に加えて、エンド ツー エンドのアップグレード プロセスを処理するためのお勧めの追加ステップとグループが含まれます。
>
> カスタム タスク シーケンスを作成し、[OS のアップグレード](../understand/task-sequence-steps.md#BKMK_UpgradeOS) の手順を追加することができます。 これは、OS を Windows 10 にアップグレードするために必要な唯一の手順です。 この方法を選んだ場合は、**OS のアップグレード**の手順の後に、[コンピューターの再起動](../understand/task-sequence-steps.md#BKMK_RestartComputer)の手順も追加してアップグレードを完了します。 必ず **[現在インストールされている既定のオペレーティング システム]** 設定を使用して、Windows PE ではなく、インストール対象の OS でコンピューターを再起動するようにします。  


## <a name="deploy"></a><a name="BKMK_Deploy"></a> デプロイ  

OS を展開するには、次の展開方法のいずれかを使用します。  

- [ソフトウェア センターを使用したネットワーク経由での Windows の展開](use-software-center-to-deploy-windows-over-the-network.md)  

- [ネットワークではなくスタンドアロン メディアを使用した Windows の展開](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > スタンドアロン メディアを使用する場合は、タスク シーケンスにブート イメージを含める必要があります。 この構成により、タスク シーケンス メディア ウィザードでタスク シーケンスを使用できるようになります。


## <a name="monitor"></a>モニター  

OS をアップグレードするために、タスク シーケンスの展開を監視するには、「[OS の展開の監視](monitor-operating-system-deployments.md)」を参照してください。