---
title: Windows PE での BitLocker の事前準備
titleSuffix: Configuration Manager
description: Configuration Manager の BitLocker の事前準備タスクでは、オペレーティング システムを展開する前に Windows プレインストール環境で BitLocker を有効にします。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9e9acb35354e9962fe838964d3afad0bacceace
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124945"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-configuration-manager"></a>Configuration Manager で Windows PE での BitLocker を事前に準備する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のタスク シーケンスの **BitLocker の事前プロビジョニング** ステップで、オペレーティング システムを展開する前に Windows プレインストール環境 (Windows PE) で BitLocker を有効にすることができます。 使用されているドライブ領域のみが暗号化されるため、暗号化にかかる時間が大幅に短くなります。 Windows のセットアップ プロセスを実行する前に、フォーマットしたボリュームを、無作為に作成されたクリア キーによるキー保護機能を使って暗号化します。 BitLocker を事前プロビジョニングする機能は、Windows 8 と Windows Server 2012 に導入されています。 BitLocker をハード ドライブに事前プロビジョニングして Windows 7 をインストールできますが、これには特別な手順が必要です。 Windows 7 のセットアップが終わったら、BitLocker のキー保護機能を設定する必要があります。これは、Windows 7 の BitLocker コントロール パネルでは、クリア キーによるキー保護と一緒に BitLocker を使えないからです。 したがって、 **BitLocker の有効化** ステップか、manage-bde.exe コマンドライン ツールを使って、キー保護機能を追加する必要があります。  

 通常、BitLocker を事前プロビジョニングして Windows 7 をインストールするには、次の作業を行う必要があります。  

- Windows PE でコンピューターを再起動します。  

  > [!IMPORTANT]  
  >  BitLocker を事前プロビジョニングするには、Windows PE 4 以降のブート イメージを使用する必要があります。 Configuration Manage がサポートしている Windows PE のバージョンの詳細については、「[Configuration Manager 外部の依存関係](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies)」を参照してください。  

- ハード ドライブのパーティションを作成してフォーマットします。  

- のタスク シーケンスの  

- オペレーティング システムとネットワークの特定の設定を行って、Windows 7 をインストールします。  

- BitLocker にキー保護機能を追加します。  

  Configuration Manager でハード ドライブに BitLocker を事前プロビジョニングして Windows 7 をインストールする場合、新しいタスク シーケンスを作成して、**タスク シーケンスの作成ウィザード**の **[新しいタスク シーケンスの作成]** ページで **[既存のイメージ パッケージをインストールする]** を選択する方法をお勧めします。 次の表に示すステップから成るタスク シーケンスが作成されます。  

> [!NOTE]  
>  ウィザードで選択した設定によっては、他のステップが含まれることがあります。 たとえば、ウィザードの **[状態移行]** ページで **[キャプチャした Microsoft Windows 設定]** を選択した場合は、 **[Windows 設定のキャプチャ]** というステップが追加されます。  

|タスク シーケンスのステップ|詳細|  
|------------------------|-------------|  
|BitLocker の無効化|現在、BitLocker による暗号化が有効になっている場合は、無効にします。 詳細については、「[BitLocker の無効化](../understand/task-sequence-steps.md#BKMK_DisableBitLocker)」を参照してください。|  
|Windows PE でのコンピューターの再起動|タスク シーケンスに割り当てられている Windows PE ブート イメージを実行することにより、コンピューターを再起動します。 BitLocker を事前プロビジョニングするには、Windows PE 4 以降のブート イメージを使用する必要があります。 詳細については、「[コンピューターの再起動](../understand/task-sequence-steps.md#BKMK_RestartComputer)」を参照してください。|  
|ディスク 0 のパーティション作成 - BIOS<br /><br /> ディスク 0 のパーティション作成 - UEFI|BIOS または UEFI を使って、目的のコンピューターの指定されたドライブをフォーマットしてパーティションを作成します。 目的のコンピューターが UEFI モードになっている場合は、UEFI が使われます。 詳細については、「[ディスクのフォーマットとパーティション作成](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk)」を参照してください。|  
|のタスク シーケンスの|この手順により、Windows PE で動作している間は、ドライブで BitLocker が有効になります。 ドライブの使用済みの領域だけが暗号化されます。 前のステップでハード ドライブのパーティションを作成してフォーマットしているので、データはありません。したがって、暗号化はすぐに完了します。 詳細については、「[Pre-provision BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker)」(BitLocker の事前プロビジョニング) を参照してください。|  
|オペレーティング システムの適用|目的のコンピューターにオペレーティング システムをインストールするための応答ファイルを準備して、タスク シーケンスの OSDTargetSystemDrive 変数を、オペレーティング システム ファイルが含まれているパーティションのドライブ文字に設定します。 この応答ファイルと変数は、Windows と ConfigMgr のセットアップ ステップでオペレーティング システムをインストールするために使われます。 詳細については、「 [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)」を参照してください。|  
|Windows 設定の適用|応答ファイルに Windows 設定を追加します。 この応答ファイルは、Windows と ConfigMgr のセットアップ ステップでオペレーティング システムをインストールするために使われます。 詳細については、「[Windows 設定の適用](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings)」を参照してください。|  
|ネットワーク設定の適用|応答ファイルにネットワーク設定を追加します。 この応答ファイルは、Windows と ConfigMgr のセットアップ ステップでオペレーティング システムをインストールするために使われます。 詳細については、「[ネットワーク設定の適用](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings)」を参照してください。|  
|デバイス ドライバーの適用|オペレーティング システムの展開の一部としてドライバーを検出してインストールします。 詳細については、「[Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers)」(ドライバーの自動適用) を参照してください。|  
|Windows と ConfigMgr のセットアップ|Windows PE から新しいパーティション システムに移行します。 このタスク シーケンス ステップはあらゆるオペレーティング システム展開に必要です。 このステップでは、Configuration Manager クライアントを新しいオペレーティング システムにインストールして、新しいオペレーティング システムでタスク シーケンスの実行を継続できるようにします。 詳細については、「[Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)」(Windows と ConfigMgr のセットアップ) を参照してください。|  
|BitLocker の有効化|BitLocker によるハード ドライブの暗号化を有効にして、キー保護機能を設定します。 ハード ドライブには BitLocker が事前プロビジョニングされているので、このステップはすぐに完了します。 Windows 7 では、キー保護機能を追加する必要があります。 このステップを使用しない場合は、manage-bde.exe コマンドライン ツールを使って、キー保護機能を設定してください。 詳細については、「[BitLocker の有効化](../understand/task-sequence-steps.md#BKMK_EnableBitLocker)」を参照してください。|  
