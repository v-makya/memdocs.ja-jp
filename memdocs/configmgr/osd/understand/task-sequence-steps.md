---
title: タスク シーケンスのステップ
titleSuffix: Configuration Manager
description: Configuration Manager タスク シーケンスに追加できるステップについて説明します。
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61070d98c5b7d453f493cf7ea2995705ee43f325
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546622"
---
# <a name="task-sequence-steps"></a>タスク シーケンスのステップ

*適用対象:Configuration Manager (Current Branch)*

次のタスク シーケンス ステップは、Configuration Manager のタスク シーケンスに追加できます。 詳細については、「[タスク シーケンス エディターを使用する](task-sequence-editor.md)」を参照してください。  

## <a name="common-settings"></a>共通設定

次の設定は、タスク シーケンスのすべてのステップに共通です。

### <a name="properties-for-all-steps"></a>すべてのステップのプロパティ

- **名前**:タスク シーケンス エディターでは、このステップを説明する短い名前を指定する必要があります。 新しいステップを追加するとき、タスク シーケンス エディターは既定で名前を Type に設定します。 **[名前]** の長さは 50 文字以下です。  

- **説明**: 必要に応じて、このステップについての詳細な情報を指定します。 **[説明]** の長さは 256 文字以下です。  

この記事の残りの部分では、各タスク シーケンス ステップの **[プロパティ]** タブにある他の設定について説明します。

### <a name="options-for-all-steps"></a>すべてのステップのオプション

- **このステップを無効にする**: タスク シーケンスはコンピューターで実行するときにこのステップをスキップします。 タスク シーケンス エディターでは、このステップのアイコンはグレー表示になります。  

- **エラー時に続行する**: ステップの実行中にエラーが発生した場合でも、タスク シーケンスを続行します。 詳しくは、「[タスクの自動化計画に関する考慮事項](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups)」をご覧ください。  

- **条件の追加**: タスク シーケンスでは、これらの条件付きステートメントを評価して、ステップを実行するかどうかが決定されます。 条件としてタスク シーケンス変数を使用する例については、「[How to use task sequence variables](using-task-sequence-variables.md#bkmk_access-condition)」(タスク シーケンス変数を使用する方法) をご覧ください。 条件の詳細については、[タスク シーケンス エディターの条件](task-sequence-editor.md#bkmk_conditions)に関する記事をご覧ください。

特定のタスク シーケンス ステップに関する以下のセクションでは、 **[オプション]** タブで指定できる他の設定について説明します。



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a> データ イメージの適用

このステップでは、データ イメージを指定した挿入先パーティションにコピーします。  

このステップは Windows PE でのみ実行されます。 完全な OS では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[イメージ]** を選んで、 **[データ イメージの適用]** を選びます。

### <a name="variables-for-apply-data-image"></a>データ イメージの適用の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>データ イメージの適用のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage?view=sccm-ps)
- [New-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDataImage?view=sccm-ps)
- [Remove-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage?view=sccm-ps)
- [Set-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage?view=sccm-ps)

### <a name="properties-for-apply-data-image"></a>データ イメージの適用のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="image-package"></a>イメージ パッケージ

**[参照]** を選び、このタスク シーケンスで使う**イメージ パッケージ**を指定します。 **[パッケージの選択]** ダイアログ ボックスでインストールするパッケージを選択します。 ダイアログ ボックスの下部に、既存の各イメージ パッケージに関連付けられているプロパティの情報が表示されます。 ドロップダウン リストを使用して、選択した **イメージ パッケージ** からインストールする **イメージ** を選択します。  

> [!NOTE]  
> このタスク シーケンス アクションは、画像をデータ ファイルとして扱います。 このアクションでは、イメージを OS として起動するための設定は何も行われません。  

#### <a name="destination"></a>Destination

次のいずれかのオプションを構成します。

- **次に利用可能なパーティション**: このタスク シーケンスの**オペレーティング システムの適用**ステップまたは**データ イメージの適用**ステップの対象にまだなっていない次のシーケンシャル パーティションを使います。  

- **特定のディスクとパーティション**: **ディスク**番号 (0 から開始) と**パーティション**番号 (1 から開始) を選びます。  

- **特定の論理ドライブ文字**: Windows PE によりパーティションに割り当てられた**ドライブ文字**を指定します。 このドライブ文字は、新しく展開される OS によって割り当てられるドライブ文字と異なっていてもかまいません。  

- **変数に格納されている論理ドライブ文字**: Windows PE によりパーティションに割り当てられたドライブ文字を含むタスク シーケンス変数を指定します。 この変数は通常、**ディスクのフォーマットとパーティション作成**タスク シーケンス ステップの **[パーティションのプロパティ]** ダイアログ ボックスの [詳細設定] セクションで設定されます。  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>イメージを適用する前にパーティションのすべてのコンテンツを削除する  

イメージをインストールする前に対象パーティションのすべてのファイルをタスク シーケンスで削除することを指定します。 パーティションのコンテンツを削除しないことにより、このアクションを使用して、以前にターゲットにしたパーティションに追加コンテンツを適用できます。  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> ドライバー パッケージの適用  

このステップでは、ドライバー パッケージ内のすべてのドライバーをダウンロードして、Windows OS にインストールします。

**[ドライバー パッケージの適用]** タスク シーケンス ステップでは、ドライバー パッケージ内のすべてのデバイス ドライバーを Windows セットアップで使用できるようにします。 パッケージ内のドライバーを Windows で使用できるようにするには、 **[オペレーティング システムの適用]** ステップと **[Windows と ConfigMgr のセットアップ]** ステップの間に、このステップを追加します。 **[ドライバー パッケージの適用]** タスク シーケンス ステップは、スタンドアロンのメディア展開シナリオでも便利です。  

似たデバイス ドライバーを 1 つのドライバー パッケージに格納し、適切な配布ポイントに配布します。 たとえば、1 つの製造元からのすべてのドライバーをドライバー パッケージに格納します。 その後、関連付けられたコンピューターがアクセスできる配布ポイントにパッケージを配布します。

**[ドライバー パッケージの適用]** ステップは、スタンドアロン メディアの場合に便利です。 このステップは、特定のドライバー セットをインストールする場合にも役立ちます。 このような種類のドライバーとしては、ネットワーク プリンターのような Windows プラグ アンド プレイで検出されないドライバーなどがあります。  

このタスク シーケンス ステップは Windows PE でのみ実行されます。 完全な OS では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ドライバー]** を選んで、 **[ドライバー パッケージの適用]** を選びます。

> [!TIP]
> Configuration Manager のドライバーの概要については、「[タスク シーケンスを使用してドライバーをインストールする](../get-started/manage-drivers.md#BKMK_TSDrivers)」を参照してください。
>
> ユーザーがタスク シーケンスをインストールする前に、コンテンツの事前キャッシュを使用して該当するドライバー パッケージをダウンロードします。 詳細については、「[コンテンツの事前キャッシュを構成する](../deploy-use/configure-precache-content.md)」を参照してください。

### <a name="variables-for-apply-driver-package"></a>ドライバー パッケージの適用の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>ドライバー パッケージの適用のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage?view=sccm-ps)
- [New-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Remove-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Set-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage?view=sccm-ps)

### <a name="properties-for-apply-driver-package"></a>ドライバー パッケージの適用のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="driver-package"></a>ドライバー パッケージ

必要なデバイス ドライバーを含むドライバー パッケージを指定します。 **[参照]** を選び、 **[パッケージの選択]** ダイアログ ボックスを開きます。 適用する既存のドライバー パッケージを選択します。 ダイアログ ボックスの下部に、関連付けられているパッケージのプロパティが表示されます。  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>再帰オプションを使用して DISM を実行し、ドライバー パッケージをインストールする

Windows がドライバー パッケージを適用するときに、DISM コマンド ラインに `/recurse` パラメーターを追加するには、このオプションを選択します。

このオプションを有効にすると、追加の DISM コマンド ライン パラメーターを指定することもできます。 [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) タスク シーケンス変数を使用して、より多くのオプションを含めることができます。 詳しくは、「[Windows 10 DISM Command-Line Options](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options)」(Windows 10 DISM のコマンド ライン オプション) をご覧ください。<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Vista 以前のオペレーティング システムをセットアップする前にインストールする必要がある大容量記憶装置ドライバーをパッケージから選択する

古い OS をインストールするために必要な大容量記憶装置ドライバーを指定します。  

##### <a name="driver"></a>ドライバー

古い OS をセットアップする前にインストールする大容量記憶装置ドライバーのファイルを選びます。 ドロップダウン リストの項目は指定したパッケージから設定されます。  

##### <a name="model"></a>モデル

Windows Vista 以前の OS の展開に必要となる、起動に不可欠なデバイスを指定します。  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>署名されていないドライバーの無人インストールが許可されているバージョンの Windows でドライバーの無人インストールを行う

このオプションを指定すると、Windows はデジタル署名のないドライバーをインストールできます。  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a> ネットワーク設定の適用  

このステップでは、対象のコンピューターのネットワークまたはワークグループの構成情報を指定します。 タスク シーケンスは、これらの値を適切な応答ファイルに格納します。 Windows セットアップは、**Windows と ConfigMgr のセットアップ** アクションの間にこの応答ファイルを使います。  

このタスク シーケンス ステップは Windows PE でのみ実行されます。 完全な OS では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[設定]** を選んで、 **[ネットワーク設定の適用]** を選びます。

> [!NOTE]
> タスク シーケンスにこのステップの複数のインスタンスを含めると、条件は適用されません。 このタスク シーケンス ステップの最後のインスタンスでの設定が、デバイスに適用されます。 この動作を回避するには、個別のグループにグループの条件を含む各ステップを含めます。

### <a name="variables-for-apply-network-settings"></a>ネットワーク設定の適用の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>ネットワーク設定の適用のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [New-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Remove-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Set-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting?view=sccm-ps)

### <a name="properties-for-apply-network-settings"></a>ネットワーク設定の適用のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="join-a-workgroup"></a>ワークグループに参加

対象コンピューターを指定したワークグループに参加させるには、このオプションを選択します。 **[ワークグループ]** 行にワークグループの名前を入力します。 この値は、**ネットワーク設定のキャプチャ** タスク シーケンス ステップでキャプチャされた値によってオーバーライドできます。

#### <a name="join-a-domain"></a>ドメインに参加

対象コンピューターを指定したドメインに参加させるには、このオプションを選択します。 ドメイン (`fabricam.com` など) を指定するか参照します。 組織単位の LDAP (Lightweight Directory Access Protocol) パスを指定または参照します。 例: `LDAP//OU=computers, DC=Fabricam.com, C=com`。  

#### <a name="account"></a>アカウント

コンピューターをドメインに参加させるには、 **[設定]** を選択して必要なアクセス許可を持つアカウントを指定します。 **[Windows ユーザー アカウント]** ダイアログ ボックスで、ユーザー名を `Domain\User` という形式で入力します。 詳しくは、[ドメイン参加アカウント](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)に関するページをご覧ください。

#### <a name="adapter-settings"></a>アダプター設定

コンピューターの各ネットワーク アダプターのネットワーク構成を指定します。 **[新規]** を選択して **[ネットワーク設定]** ダイアログ ボックスを開き、ネットワーク設定を指定します。

- **[ネットワーク設定のキャプチャ]** ステップも使った場合、タスク シーケンスは前のステップでキャプチャした設定をネットワーク アダプターに適用します。
- タスク シーケンスでそれまでにネットワークの設定がキャプチャされていない場合は、このステップで指定した設定が適用されます。
- タスク シーケンスは、Windows デバイスの列挙の順序でネットワーク アダプターにこれらの設定を適用します。  
- このステップで指定した設定はすぐにはコンピューターに適用されません。



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> オペレーティング システム イメージの適用  

このステップでは、OS を対象コンピューターにインストールします。

**オペレーティング システムの適用**アクションが実行された後、**OSDTargetSystemDrive** 変数には OS が含まれるパーティションのドライブ文字が設定されます。  

このタスク シーケンス ステップは Windows PE でのみ実行されます。 完全な OS では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[イメージ]** を選んで、 **[オペレーティング システム イメージの適用]** を選びます。

> [!TIP]
> Windows 10 バージョン 1709 以降では、メディアに複数のエディションが含まれます。 タスク シーケンスが OS アップグレード パッケージまたは OS イメージを使うように構成するときは、[サポートされているエディション](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)を必ず選んでください。  
>
> ユーザーがタスク シーケンスをインストールする前に、コンテンツの事前キャッシュを使用して該当する OS アップグレード パッケージをダウンロードします。 詳細については、「[コンテンツの事前キャッシュを構成する](../deploy-use/configure-precache-content.md)」を参照してください。
>
> **[Windows と ConfigMgr のセットアップ]** ステップによって、Windows のインストールが開始されます。

### <a name="variables-for-apply-os-image"></a>OS イメージの適用の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>OS イメージの適用のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [New-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Remove-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Set-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem?view=sccm-ps)

### <a name="behaviors-for-apply-os-image"></a>OS イメージの適用の動作

このステップは、OS イメージまたは OS アップグレード パッケージを使うかどうかに応じてさまざまなアクションを実行します。  

#### <a name="os-image-actions"></a>OS イメージのアクション

OS イメージを使うと、 **[オペレーティング システム イメージの適用]** ステップは次のアクションを実行します。  

1. **\_SMSTSUserStatePath** 変数で指定されているフォルダー内のファイルを除く、対象ボリューム上のすべてのコンテンツを削除します。  

2. 指定された .wim ファイルのコンテンツを、指定された挿入先パーティションに抽出します。  

3. 応答ファイルを準備します。  

    1. 展開する OS 用に既定の Windows セットアップ応答ファイル (sysprep.inf または unattend.xml) を新しく作成します。  

    2. ユーザーが提供する応答ファイルから値をマージします。  

4. Windows ブート ローダーをアクティブなパーティションにコピーします。  

5. 新しくインストールした OS を参照するよう boot.ini またはブート構成データベース (BCD) を設定します。  

#### <a name="os-upgrade-package-actions"></a>OS アップグレード パッケージのアクション

OS アップグレード パッケージを使うと、 **[オペレーティング システム イメージの適用]** ステップは次のアクションを実行します。  

1. **\_SMSTSUserStatePath** 変数で指定されているフォルダー内のファイルを除く、対象ボリューム上のすべてのコンテンツを削除します。  

2. 応答ファイルを準備します。  

    1. Configuration Manager によって作成された標準値を使って、新しい応答ファイルを作成します。  

    2. ユーザーが提供する応答ファイルから値をマージします。  

### <a name="properties-for-apply-os-image"></a>OS イメージの適用のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="apply-operating-system-from-a-captured-image"></a>キャプチャしたイメージからオペレーティング システムを適用する

キャプチャした OS イメージをインストールします。 **[参照]** を選択して、 **[パッケージの選択]** ダイアログ ボックスを開きます。 その後、インストールする既存のイメージ パッケージを選択します。 指定した**イメージ パッケージ**に複数のイメージが関連付けられている場合は、ドロップダウン リストから、この展開に使う、関連付けられているイメージを選択します。 イメージを選択することで、既存の各イメージの基本情報を表示できます。  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>元のインストール ソースからオペレーティング システムを適用する

OS アップグレード パッケージを使用して、OS をインストールします。このパッケージは元のインストール ソースでもあります。 **[参照]** を選択して、 **[Select an Operating System Upgrade Package]** \(オペレーティング システムのアップグレード パッケージの選択\) ダイアログ ボックスを開きます。 その後、使う既存の OS アップグレード パッケージを選びます。 イメージを選択することで、既存の各イメージ ソースの基本情報を表示できます。 ダイアログ ボックスの下部にある結果ウィンドウに、関連付けられているイメージ ソースのプロパティが表示されます。 指定したパッケージに複数のエディションが関連付けられている場合は、ドロップダウン リストを使用して、使用する**エディション**を選択します。  

> [!NOTE]  
> **オペレーティング システム アップグレード パッケージ**は、Windows の新規インストールではなく、主にインプレース アップグレードに使用するためにあります。 Windows の新規インストールを展開する場合、 **[Apply operating system from a captured image]** \(キャプチャしたイメージからオペレーティング システムを適用する\) オプションとインストール ソース ファイルの **install.wim** を使用します。
>
> **オペレーティング システム アップグレード パッケージ**を使用して Windows の新しいインストールを展開することは引き続きサポートされますが、これはこの方法と互換性があるドライバーに依存しています。 OS アップグレード パッケージから Windows をインストールする場合、ドライバーは、単純に Windows PE にいる間に挿入されるのと比較して、Windows PE にいる間にインストールされます。 一部のドライバーは、Windows PE で動作している間にインストールすることはできません。
>
> ドライバーが Windows PE で動作している間のインストールに対応していない場合、元のインストール ソース ファイルから **install.wim** 使用して**オペレーティング システム イメージ**を作成します。 次いで **[Apply operating system from a captured image]** \(キャプチャしたイメージからオペレーティング システムを適用する\) オプションを使用して展開します。

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>カスタム インストールに無人ファイルまたは sysprep 応答ファイルを使用する

OS のバージョンおよびインストール方法によって異なる Windows セットアップ応答ファイル (**unattend.xml**、**unattend.txt**、または **sysprep.inf**) を提供するには、このオプションを使用します。 指定するファイルには、Windows 応答ファイルがサポートする任意の標準の構成オプションを含めることができます。 たとえば、この構成オプションを使用して既定の Internet Explorer のホーム ページを指定できます。 応答ファイルを含むパッケージ、およびパッケージ内のファイルへの関連付けられたパスを指定します。  

> [!NOTE]  
> 指定する Windows セットアップ応答ファイルには、`%varname%` という形式の埋め込みタスク シーケンス変数を含めることができます。*varname* は変数の名前です。 **Windows と ConfigMgr のセットアップ** ステップでは、変数の文字列が変数の実際の値に置き換えられます。 これらの埋め込みタスク シーケンス変数を、unattend.xml 応答ファイルの数値のみのフィールドで使用することはできません。  

Windows セットアップ応答ファイルを指定しないと、タスク シーケンスで自動的に応答ファイルが生成されます。  

#### <a name="destination"></a>Destination

次のいずれかのオプションを構成します。  

- **次に利用可能なパーティション**: このタスク シーケンスの**オペレーティング システムの適用**ステップまたは**データ イメージの適用**ステップの対象にまだなっていない次のシーケンシャル パーティションを使います。  

- **特定のディスクとパーティション**: **ディスク**番号 (0 から開始) と**パーティション**番号 (1 から開始) を選びます。  

- **特定の論理ドライブ文字**: Windows PE によりパーティションに割り当てられた**ドライブ文字**を指定します。 このドライブ文字は、新しく展開される OS によって割り当てられるドライブ文字と異なっていてもかまいません。  

- **変数に格納されている論理ドライブ文字**: Windows PE によりパーティションに割り当てられたドライブ文字を含むタスク シーケンス変数を指定します。 この変数は通常、**ディスクのフォーマットとパーティション作成**タスク シーケンス ステップの **[パーティションのプロパティ]** ダイアログ ボックスの [詳細設定] セクションで設定されます。  

### <a name="options-for-apply-os-image"></a>OS イメージの適用のオプション

このタスク シーケンス ステップの **[オプション]** タブでは、既定のオプションだけでなく、以下の追加設定を構成します。  

#### <a name="access-content-directly-from-the-distribution-point"></a>配布ポイントからコンテンツに直接アクセスする

配布ポイントから OS イメージに直接アクセスするようにタスク シーケンスを構成します。 たとえば、記憶域の容量が限られている組み込みデバイスにオペレーティング システムを展開するときに、このオプションを使います。 また、このオプションを選択するときに、OS イメージのプロパティの **[データ アクセス]** タブでパッケージ共有設定も構成します。  

> [!NOTE]  
> この設定は、**ソフトウェアの展開ウィザード**の **[配布ポイント]** ページで構成される展開オプションをオーバーライドします。 このオーバーライドは、すべてのタスク シーケンス コンテンツではなく、このステップで指定されている OS イメージに対してのみ適用されます。  

> [!IMPORTANT]  
> セキュリティを最大限に高めるため、このオプションを選択しないことを強くお勧めします。 このオプションは、主にストレージ容量が限られたデバイスで使用するために設計されています。 このオプションは、タスク シーケンスの速度の向上に役立つものではありません。 このオプションを選択すると、オペレーティング システム パッケージに対してパッケージ ハッシュが検証されません。 このため、管理者権限があるユーザーがパッケージ コンテンツの変更または改ざんを行うことができるので、パッケージの整合性は保証できません。



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Windows 設定の適用

このステップでは、対象コンピューターに対して Windows の設定を構成します。 タスク シーケンスは、これらの値を適切な応答ファイルに格納します。 Windows セットアップは、**Windows と ConfigMgr のセットアップ** ステップの間にこの応答ファイルを使います。  

このタスク シーケンス ステップは Windows PE でのみ実行されます。 完全な OS では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[設定]** を選んで、 **[Windows 設定の適用]** を選びます。

### <a name="variables-for-apply-windows-settings"></a>Windows 設定の適用の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>Windows 設定の適用のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [New-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Remove-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Set-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting?view=sccm-ps)

### <a name="properties-for-apply-windows-settings"></a>Windows 設定の適用のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="user-name"></a>ユーザー名

対象のコンピューターに関連付ける登録済みユーザー名を指定します。 この値は、**Windows 設定のキャプチャ** タスク シーケンス ステップでキャプチャされた値によってオーバーライドできます。  

#### <a name="organization-name"></a>組織名

対象のコンピューターに関連付ける登録済みの組織名を指定します。 この値は、**Windows 設定のキャプチャ** タスク シーケンス ステップでキャプチャされた値によってオーバーライドできます。  

#### <a name="product-key"></a>プロダクト キー  

対象のコンピューターで Windows インストールに使用するプロダクト キーを指定します。  

#### <a name="server-licensing"></a>サーバー ライセンス

サーバー ライセンス モードを指定します。

- ライセンス モードとして **[同時使用ユーザー数]** または **[ユーザーごと]** を選択します。  
- **[同時使用ユーザー数]** を選ぶ場合は、ライセンス契約ごとに許可される接続の最大数も指定します。  
- 対象のコンピューターがサーバーではない場合、またはライセンス モードを指定しない場合は、 **[指定しない]** を選択します。  

#### <a name="maximum-connections"></a>最大接続数

> [!NOTE]
> この設定は、現在サポートされていない Windows のレガシ バージョンにのみ適用されます。<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>ローカルの管理者パスワードをランダムに生成し、サポートされているすべてのプラットフォームのアカウントを無効にする (推奨)  

ローカルの管理者パスワードをランダムに生成される文字列に設定するには、このオプションを選びます。 また、このオプションを選ぶと、この機能をサポートするプラットフォームでのローカル管理者アカウントが無効になります。  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>アカウントを有効にし、ローカル管理者パスワードを指定する  

指定したパスワードを使うローカル管理者アカウントを有効にするには、このオプションを選びます。 パスワードを **[パスワード]** 行に入力し、 **[パスワードの確認入力]** 行にパスワードを確認入力します。  

#### <a name="time-zone"></a>タイム ゾーン

対象のコンピューターに構成するタイム ゾーンを指定します。 この値は、**Windows 設定のキャプチャ** タスク シーケンス ステップでキャプチャされた値によってオーバーライドできます。  

#### <a name="language-settings"></a>言語の設定

<!--5411057, 5138936-->

バージョン 1910 以降では、OS 展開中に言語構成を制御できます。 これらの言語設定を既に適用している場合は、この変更によって OS 展開のタスク シーケンスを簡略化することができます。 言語ごとに複数のステップを使ったり、個別のスクリプトを使ったりする代わりに、このステップのインスタンスを、言語につき 1 つ、その言語の条件と共に使います。

次の設定を構成します。

- 入力ロケール (既定のキーボード レイアウト)
- システム ロケール
- UI 言語
- UI 言語のフォールバック
- ユーザー ロケール

これらの Windows セットアップ応答ファイルの値について詳しくは、「[Microsoft Windows International コア](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core)」をご覧ください。

> [!NOTE]
> カスタムの Windows セットアップ応答ファイル (unattend.xml) を作成した場合、この手順によって既存の値がすべて上書きされます。 これらの設定に対する動的プロセスを自動化するには、関連するタスク シーケンス変数を使用します。 たとえば、[OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale) です。 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> ドライバーの自動適用

このステップでは、OS の展開の一部としてドライバーを照合してインストールします。  

> [!IMPORTANT]  
> スタンドアロン メディアは、**ドライバーの自動適用**ステップを使用できません。 このシナリオでは、タスク シーケンスは Configuration Manager サイトに接続できません。  

このタスク シーケンス ステップは Windows PE でのみ実行されます。 完全な OS では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ドライバー]** を選んで、 **[ドライバーの自動適用]** を選びます。

> [!TIP]
> Configuration Manager のドライバーの概要については、「[タスク シーケンスを使用してドライバーをインストールする](../get-started/manage-drivers.md#BKMK_TSDrivers)」を参照してください。

### <a name="behaviors-for-auto-apply-drivers"></a>ドライバーの自動適用の動作

**[ドライバーの自動適用]** タスク シーケンス ステップでは次の手順を実行します。  

1. ハードウェアをスキャンし、システム上に存在するすべてのデバイスのプラグ アンド プレイ ID を検索します。  

2. デバイスとプラグ アンド プレイ ID の一覧を管理ポイントに送信します。 管理ポイントは、各ハードウェア デバイス用にドライバー カタログから互換ドライバーの一覧を返します。 一覧には、含まれるドライバー パッケージに関係なく有効になっているすべてのドライバーと、指定したドライバー カテゴリでタグ付けされたドライバーが含まれます。  

3. ハードウェア デバイスごとに、タスク シーケンスは最適なドライバーを選びます。 このドライバーは、展開される OS に適しており、アクセス可能な配布ポイント上にあります。  

4. タスク シーケンスは、選んだドライバーを配布ポイントからダウンロードし、対象の OS にドライバーをステージングします。  

    1. OS イメージを使用すると、タスク シーケンスは OS ドライバー ストアにドライバーを配置します。  

    2. OS アップグレード パッケージを元のインストール ソースとして使用すると、タスク シーケンスはドライバーの場所で Windows セットアップを構成します。  

5. タスク シーケンスの **Windows と ConfigMgr のセットアップ** ステップの間に、Windows セットアップはこのステップによってステージングされたドライバーを検索します。  

### <a name="variables-for-auto-apply-drivers"></a>ドライバーの自動適用の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>ドライバーの自動適用のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver?view=sccm-ps)
- [New-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Remove-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Set-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver?view=sccm-ps)

### <a name="properties-for-auto-apply-drivers"></a>ドライバーの自動適用のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>最適な互換ドライバーのみをインストールする

タスク シーケンス ステップで、検出された各ハードウェア デバイスに最適なドライバーのみをインストールするように指定します。  

#### <a name="install-all-compatible-drivers"></a>すべての互換ドライバーをインストールする

タスク シーケンスは検出された各ハードウェア デバイスごとに、互換性のあるすべてのドライバーをインストールします。 その後、Windows セットアップが最善のドライバーを選びます。 このオプションでは、他のオプションより多くのネットワーク帯域幅とディスク領域が使われます。 タスク シーケンスによってダウンロードされるドライバーの数は多くなりますが、Windows はより適切なドライバーを選べます。  

#### <a name="consider-drivers-from-all-categories"></a>すべてのカテゴリのドライバーを検討する

タスク シーケンスは、利用可能なすべてのドライバー カテゴリから適切なデバイス ドライバーを検索します。  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>ドライバーの一致条件を制限して、選択したカテゴリに属するドライバーだけを検討する

タスク シーケンスは、指定したドライバー カテゴリから適切なデバイス ドライバーを検索します。  

複数のカテゴリを選択した場合は、任意のカテゴリに存在するすべての一致するドライバーが返されます。 これは `OR` 操作と同じです。<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>署名されていないドライバーの無人インストールが許可されているバージョンの Windows でドライバーの無人インストールを行う

このオプションを指定すると、Windows はデジタル署名のないドライバーをインストールできます。  

> [!IMPORTANT]  
> このオプションは、ドライバーの署名ポリシーを構成できないオペレーティング システムには適用されません。  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> ネットワーク設定のキャプチャ

このステップでは、タスク シーケンスを実行しているコンピューターから Microsoft ネットワーク設定をキャプチャします。 タスク シーケンスは、これらの設定をタスク シーケンス変数に保存します。 これらの設定は、 **[ネットワーク設定の適用]** ステップで構成された既定の設定をオーバーライドします。  

このタスク シーケンス ステップは完全な OS でのみ実行されます。 Windows PE では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[設定]** を選んで、 **[ネットワーク設定のキャプチャ]** を選びます。

### <a name="variables-for-capture-network-settings"></a>ネットワーク設定のキャプチャの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>ネットワーク設定のキャプチャのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [New-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Remove-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Set-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings?view=sccm-ps)

### <a name="properties-for-capture-network-settings"></a>ネットワーク設定のキャプチャのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="migrate-domain-and-workgroup-membership"></a>ドメインとワークグループのメンバーシップを移行する

対象のコンピューターのドメインおよびワークグループ メンバーシップ情報をキャプチャします。  

#### <a name="migrate-network-adapter-configuration"></a>ネットワーク アダプター構成を移行する

対象のコンピューターのネットワーク アダプター構成をキャプチャします。 次の情報をキャプチャします。

- グローバルなネットワーク設定  
- アダプターの数  
- 各アダプターに関連付けられている次のネットワーク設定: DNS、WINS、IP、およびポート フィルター



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> オペレーティング システム イメージのキャプチャ

このステップは、参照コンピューターから 1 つまたは複数のイメージをキャプチャします。 タスク シーケンスは、指定したネットワーク共有上に Windows イメージ (.wim) ファイルを作成します。 その後、**オペレーティング システム イメージの追加**ウィザードを使って、イメージ ベースの OS の展開用に、このイメージを Configuration Manager にインポートします。  

Configuration Manager は、参照コンピューターから各ボリューム (ドライブ) を、.wim ファイル内の個別のイメージにキャプチャします。 参照コンピューターに複数のボリュームがある場合、作成される .wim ファイルには、ボリュームごとに異なるイメージが含まれています。 このステップでは、NTFS または FAT32 としてフォーマットされているボリュームのみがキャプチャされます。 その他のフォーマットのボリュームおよび USB のボリュームはスキップされます。  

参照コンピューターにインストールされている OS は、Configuration Manager がサポートするバージョンの Windows である必要があります。 SysPrep ツールを使って、参照コンピューターの OS を準備します。 インストールされた OS のボリュームとブート ボリュームは同じである必要があります。  

選んだネットワーク共有への書き込みアクセス許可を持つアカウントを指定します。 OS イメージ キャプチャのアカウントについて詳しくは、[アカウント](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account)に関するページをご覧ください。

このタスク シーケンス ステップは Windows PE でのみ実行されます。 完全な OS では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[イメージ]** を選んで、 **[オペレーティング システム イメージのキャプチャ]** を選びます。

### <a name="variables-for-capture-os-image"></a>OS イメージのキャプチャの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>OS イメージのキャプチャのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage?view=sccm-ps)
- [New-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Remove-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Set-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage?view=sccm-ps)

### <a name="properties-for-capture-os-image"></a>OS イメージのキャプチャのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="target"></a>Target  

キャプチャした OS イメージの保存時に Configuration Manager が使用する場所へのファイル システムのパス。  

#### <a name="description"></a>[説明]  

イメージ ファイルに格納されるキャプチャされた OS イメージについて、ユーザーが任意に定義した説明。  

#### <a name="version"></a>バージョン  

キャプチャした OS イメージに割り当てる、ユーザーが任意に定義したバージョン番号。 この値は、文字および数値の任意の組み合わせにすることができます。 イメージ ファイルに格納されます。  

#### <a name="created-by"></a>作成者  

OS イメージを作成したユーザーの省略可能な名前。 イメージ ファイルに格納されます。  

#### <a name="capture-operating-system-image-account"></a>オペレーティング システム イメージのキャプチャ アカウント  

指定したネットワーク共有へのアクセス許可がある Windows アカウントを入力します。 **[設定]** を選択して、Windows アカウントの名前を指定します。  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a> ユーザー状態のキャプチャ

このステップでは、ユーザー状態移行ツール (USMT) を使って、タスク シーケンスを実行しているコンピューターからユーザーの状態と設定がキャプチャされます。 このタスク シーケンス ステップは、 **[ユーザー状態の復元]** タスク シーケンス ステップと共に使用します。 このステップでは常に、Configuration Manager が生成および管理する暗号化キーを使用して、USMT 状態ストアが暗号化されます。  

オペレーティング システムを展開するときに、ユーザー状態の移行を管理する方法の詳細については、「[Manage user state](../get-started/manage-user-state.md)」 (ユーザー状態の管理) を参照してください。  

ユーザーの状態設定を状態移行ポイントに保存したり、状態移行ポイントから復元したりする場合は、このステップと共に**状態ストアの要求**ステップおよび**状態ストアのリリース**ステップを使用します。  

このステップでは、最も一般的に使われるオプションの限定されたサブセットを制御できます。 その他のコマンド ライン オプションは、**OSDMigrateAdditionalCaptureOptions** タスク シーケンス変数を使用して指定します。  

このタスク シーケンス ステップは Windows PE でのみ実行されます。 完全な OS では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ユーザー状態]** を選んで、 **[ユーザー状態のキャプチャ]** を選びます。

### <a name="variables-for-capture-user-state"></a>ユーザー状態のキャプチャの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>ユーザー状態のキャプチャのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState?view=sccm-ps)
- [New-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureUserState?view=sccm-ps)
- [Remove-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState?view=sccm-ps)
- [Set-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState?view=sccm-ps)

### <a name="properties-for-capture-user-state"></a>ユーザー状態のキャプチャのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="user-state-migration-tool-package"></a>ユーザー状態移行ツール パッケージ

ユーザー状態移行ツール (USMT) を含むパッケージを指定します。 タスク シーケンスは、このバージョンの USMT を使って、ユーザーの状態と設定をキャプチャします。 このパッケージにはプログラムは必要ありません。 32 ビット バージョンまたは 64 ビット バージョンの USMT を含むパッケージを指定します。 USMT のアーキテクチャは、タスク シーケンスが状態をキャプチャする OS のアーキテクチャによって異なります。  

#### <a name="capture-all-user-profiles-with-standard-options"></a>すべてのユーザー プロファイルを標準オプションでキャプチャする

すべてのユーザー プロファイル情報を移行します。 これが既定のオプションです。  

このオプションを選んでも、 **[ユーザー状態の復元]** ステップで **[ローカル コンピューターのユーザー プロファイルを復元する]** を選ばないと、タスク シーケンスは失敗します。 新しいアカウントにパスワードを割り当てないと、Configuration Manager は新しいアカウントを移行できません。

**タスク シーケンスの新規作成**ウィザードの **[既存のイメージ パッケージをインストールする]** オプションを使うと、作成されるタスク シーケンスでは **[すべてのユーザー プロファイルを標準オプションでキャプチャする]** が既定でオンになります。 この既定のタスク シーケンスでは、 **[ローカル コンピューターのユーザー プロファイルを復元する]** オプション (非ドメイン ユーザー アカウント) は選択されません。  

**[ローカル コンピューターのユーザー プロファイルを復元する]** を選択し、移行するアカウントのパスワードを指定します。 手動で作成したタスク シーケンスでは、この設定は **[ユーザー状態の復元]** ステップにあります。 **タスク シーケンスの新規作成** ウィザードで作成したタスク シーケンスでは、この設定は、 **[ユーザー ファイルと設定の復元]** ステップのウィザードのページにあります。  

ローカル ユーザー アカウントがない場合、この設定は適用されません。  

#### <a name="customize-how-user-profiles-are-captured"></a>ユーザー プロファイルのキャプチャ方法をカスタマイズする

カスタム プロファイル ファイルの移行を指定するには、このオプションを選択します。 **[ファイル]** を選択して、このステップで使用する USMT の構成ファイルを選択します。 移行するユーザー状態ファイルを定義する規則を含むカスタムの .xml ファイルを指定します。  

#### <a name="click-here-to-select-configuration-files"></a>構成ファイルを選択するには、ここをクリックします

ユーザー プロファイルをキャプチャするために使用する、USMT パッケージ内の構成ファイルを選択するには、このオプションを選択します。 **[ファイル]** を選択して、 **[構成ファイル]** ダイアログ ボックスを表示します。 構成ファイルを指定するには、 **[ファイル名]** 行にファイルの名前を入力し、 **[追加]** ボタンを選択します。  

#### <a name="enable-verbose-logging"></a>詳細ログ記録を有効にする

詳細なログ ファイル情報を生成するには、このオプションを有効にします。 状態をキャプチャすると、タスク シーケンスは既定でタスク シーケンス ログ フォルダー `%WinDir%\ccm\logs` に **ScanState.log** を生成します。  

#### <a name="skip-files-using-encrypted-file-system"></a>暗号化されたファイル システム (EFS) を使用するファイルをスキップする

暗号化されたファイル システム (EFS) で暗号化されたファイルのキャプチャをスキップするには、このオプションを有効にします。 このようなファイルには、ユーザー プロファイル ファイルが含まれます。 OS や USMT バージョンによっては、暗号化されたファイルを復元しても読み取れない場合があります。 詳細については、USMT のドキュメントを参照してください。  

#### <a name="copy-by-using-file-system-access"></a>ファイル システム アクセスを使用してコピーする

次の設定のいずれかを指定する場合にこのオプションを有効にします。  

- **キャプチャできないファイルがあっても続行する**: 一部のファイルをキャプチャできない場合でも移行処理を続行するには、この設定を有効にします。 このオプションを無効にした場合、ファイルをキャプチャできないと、このステップは失敗します。 既定では、このオプションは有効になっています。  

- **ファイルをコピーする代わりに、リンクを使用してローカルでキャプチャする**: NTFS ハードリンクを使用してファイルをキャプチャするには、この設定を有効にします。  

    ハードリンクを使用したデータ移行について詳しくは、「[Hard-Link Migration Store](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store)」(ハードリンク移行ストア) をご覧ください。  

- **オフライン モードでキャプチャする (Windows PE のみ)** : 完全な OS ではなく、Windows PE でユーザー状態をキャプチャするには、この設定を有効にします。  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>ボリューム シャドウ コピー サービス (VSS) を使用してキャプチャする

このオプションを指定すると、ファイルが他のアプリケーションによる編集のためにロックされている場合でもそのファイルをキャプチャできます。  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Windows 設定のキャプチャ

このステップでは、タスク シーケンスを実行しているコンピューターから Windows の設定をキャプチャします。 タスク シーケンスは、これらの設定をタスク シーケンス変数に保存します。 これらのキャプチャされた設定は、**Windows 設定の適用**ステップで構成された既定の設定をオーバーライドします。  

このタスク シーケンス ステップは、Windows PE または完全な OS のいずれかで実行されます。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[設定]** を選んで、 **[Windows 設定のキャプチャ]** を選びます。

### <a name="variables-for-capture-windows-settings"></a>Windows 設定のキャプチャの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>Windows 設定のキャプチャのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [New-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Remove-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Set-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings?view=sccm-ps)

### <a name="properties-for-capture-windows-settings"></a>Windows 設定のキャプチャのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="migrate-computer-name"></a>コンピューター名を移行する

コンピューターの NetBIOS コンピューター名をキャプチャします。  

#### <a name="migrate-registered-user-and-organization-names"></a>登録されているユーザーと組織名を移行する

登録されているユーザーと組織名をコンピューターからキャプチャします。  

#### <a name="migrate-time-zone"></a>タイム ゾーンを移行する

コンピューターのタイム ゾーンの設定をキャプチャします。  



## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a> 準備の確認

このステップでは、指定した展開の前提条件をターゲット コンピューターが満たしていることを確認します。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[準備の確認]** を選びます。

バージョン 2002 以降では、このステップには 8 つの新しいチェックが追加されています。 このステップの新規または既存のインスタンスでは、これらの新しいチェックはいずれも既定では選択されていません。<!--6005561--> 各チェックの詳細については、以下の特定のセクションを参照してください。

- **現在の OS のアーキテクチャ**
- **最小 OS バージョン**
- **最大 OS バージョン**
- **最小クライアント バージョン**
- **現在の OS の言語**
- **AC 電源の接続**
- **接続されているネットワーク アダプター**
  - **ネットワーク アダプターがワイヤレスではない**

> [!IMPORTANT]
> Configuration Manager のこの新機能を利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

**smsts.log** には、すべてのチェックの結果が含まれています。 1 つのチェックが失敗すると、タスク シーケンス エンジンで、引き続き他のチェックが評価されます。 すべてのチェックが完了するまで、ステップは失敗しません。 少なくとも 1 つのチェックが失敗した場合、ステップは失敗し、エラー コード **4316** が返されます。 このエラー コードは、"この操作に必要なリソースが存在しません" に変換されます。

### <a name="variables-for-check-readiness"></a>準備の確認の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED)

### <a name="cmdlets-for-check-readiness"></a>準備の確認のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck?view=sccm-ps)
- [New-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrestartCheck?view=sccm-ps)
- [Remove-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck?view=sccm-ps)
- [Set-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck?view=sccm-ps)

### <a name="properties-for-check-readiness"></a>準備の確認のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="minimum-memory-mb"></a>最小メモリ (MB)

メモリの量 (メガバイト (MB) 単位) が指定した量以上であることを確認します。 この設定は既定で有効になります。  

#### <a name="minimum-processor-speed-mhz"></a>最小プロセッサ速度 (MHz)  

プロセッサの速度 (メガヘルツ (MHz) 単位) が指定した速度以上であることを確認します。 この設定は既定で有効になります。  

#### <a name="minimum-free-disk-space-mb"></a>最小空きディスク領域 (MB)

空きディスク領域 (メガバイト (MB) 単位) が指定した量以上であることを確認します。  

#### <a name="current-os-to-be-refreshed-is"></a>現在の OS の更新

ターゲット コンピューターにインストールされている OS が指定した要件を満たすことを確認します。 この設定は既定で **[クライアント]** に設定されます。  

#### <a name="architecture-of-current-os"></a>現在の OS のアーキテクチャ

バージョン 2002 以降では、現在の OS が **32 ビット**か、**64 ビット**かどうかを確認します。

#### <a name="minimum-os-version"></a>最小 OS バージョン

バージョン 2002 以降では、現在の OS が、指定されたよりも後のバージョンを実行していることを確認します。 メジャー バージョン、マイナー バージョン、およびビルド番号を使用してバージョンを指定します。 たとえば、`10.0.16299` となります。

#### <a name="maximum-os-version"></a>最大 OS バージョン

バージョン 2002 以降では、現在の OS が、指定されたよりも前のバージョンを実行していることを確認します。 メジャー バージョン、マイナー バージョン、およびビルド番号を使用してバージョンを指定します。 たとえば、`10.0.18356` となります。

#### <a name="minimum-client-version"></a>最小クライアント バージョン

バージョン 2002 以降では、Configuration Manager クライアントのバージョンが、指定されたバージョン以上であることを確認します。 次の形式でクライアントのバージョンを指定してください: `5.00.8913.1005`。

#### <a name="language-of-current-os"></a>現在の OS の言語

バージョン 2002 以降では、現在の OS 言語が指定したものと一致することを確認します。 言語名を選択すると、このステップでは関連付けられている言語コードが比較されます。 このチェックでは、選択した言語と、クライアントの **Win32_OperatingSystem** の WMI クラスの **OSLanguage** プロパティが比較されます。

#### <a name="ac-power-plugged-in"></a>AC 電源の接続

バージョン 2002 以降では、デバイスがバッテリではなくコンセントに接続されていることを確認します。

#### <a name="network-adapter-connected"></a>接続されているネットワーク アダプター

バージョン 2002 以降では、ネットワークに接続されているネットワーク アダプターがデバイスにあることを確認します。 また、依存チェックを選択して、**ネットワーク アダプターがワイヤレス**でないことを確認することもできます。

### <a name="options-for-check-readiness"></a>準備の確認のオプション

> [!NOTE]  
> このステップの **[オプション]** タブで **[エラー時に続行する]** の設定を有効にした場合、準備の確認結果の記録だけが行われます。 確認が失敗しても、タスク シーケンスは停止しません。  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> ネットワーク フォルダーへの接続

このステップでは、共有ネットワーク フォルダーへの接続を作成します。  

このタスク シーケンス ステップは、完全な OS または Windows PE で実行されます。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[ネットワーク フォルダーに接続]** を選びます。

### <a name="variables-for-connect-to-network-folder"></a>ネットワーク フォルダーへの接続の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>ネットワーク フォルダーへの接続のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [New-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Remove-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Set-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder?view=sccm-ps)

### <a name="properties-for-connect-to-network-folder"></a>ネットワーク フォルダーへの接続のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="path"></a>パス  

**[参照]** を選択して、ネットワーク フォルダーのパスを指定します。 「`\\server\share`」の形式を使用します。

#### <a name="drive"></a>ドライブ  

この接続に割り当てるローカル ドライブ文字を選びます。

#### <a name="account"></a>アカウント

**[設定]** を選択して、このネットワーク フォルダーに接続するアクセス許可を持つユーザー アカウントを指定します。 タスク シーケンスのネットワーク フォルダー接続アカウントについて詳しくは、[アカウント](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account)に関するページをご覧ください。



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> BitLocker の無効化

このステップでは、現在の OS ドライブまたは特定のドライブでの BitLocker 暗号化を無効にします。 このアクションでは、ハード ドライブ上のキー プロテクターはクリア テキストのままになります。 ドライブの内容は暗号化解除されません。 このアクションはほとんど瞬時に完了します。  

> [!NOTE]  
> BitLocker ドライブ暗号化とは、ディスク ボリュームの内容を低レベルで暗号化する処理のことです。  

暗号化されたドライブが複数存在する場合は、OS ドライブで BitLocker を無効にする前に、すべてのデータ ドライブで BitLocker を無効にする必要があります。  

このステップは完全な OS でのみ実行されます。 Windows PE では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ディスク]** を選んで、 **[BitLocker の無効化]** を選びます。

### <a name="variables-for-disable-bitlocker"></a>BitLocker の無効化の変数

バージョン 1906 からは、このステップで次のタスク シーケンス変数を使用します。  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>BitLocker の無効化のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker?view=sccm-ps)
- [New-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker?view=sccm-ps)
- [Remove-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker?view=sccm-ps)
- [Set-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker?view=sccm-ps)

### <a name="properties-for-disable-bitlocker"></a>BitLocker の無効化のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="current-operating-system-drive"></a>現在のオペレーティング システム ドライブ

現在の OS ドライブで BitLocker を無効にします。  

#### <a name="specific-drive"></a>特定のドライブ  

特定のドライブで BitLocker を無効にします。 ドロップダウン リストを使用して、BitLocker を無効にするドライブを指定します。  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>保護を再開するまでの Windows の再起動回数

<!-- 4512937 -->
バージョン 1906 以降では、このオプションを使用することで、BitLocker の無効状態を維持する再起動数を指定できます。 このステップのインスタンスを複数追加する代わりに、1 (既定) から 15 までの値を設定します。

この動作を設定および変更するには、タスク シーケンス変数 [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) と [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride) を使用します。


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> パッケージ コンテンツのダウンロード

このステップでは、次のいずれかの種類のパッケージをダウンロードします。  

- OS イメージ  
- OS アップグレード パッケージ  
- ドライバー パッケージ  
- パッケージ  
- ブート イメージ <sup>[注 1](#bkmk_note1)</sup>  

このステップは、次のシナリオで OS をアップグレードするためのタスク シーケンスに適しています。  

- x86 と x64 の両方のプラットフォームで動作する 1 つのアップグレード タスク シーケンスを使用する。 **[アップグレードの準備]** グループで 2 つの **[パッケージ コンテンツのダウンロード]** ステップを含めます。 **[オプション]** タブでクライアント アーキテクチャを検出する条件を指定し、適切な OS アップグレード パッケージのみをダウンロードします。 同じ変数を使用するように **[パッケージ コンテンツのダウンロード]** ステップをそれぞれ構成します。 **[オペレーティング システムのアップグレード]** ステップでメディア パスにその変数を使います。  

- 該当するドライバー パッケージを動的にダウンロードするには、ドライバー パッケージごとに適切なハードウェアの種類を検出する条件を含む 2 つの **[パッケージ コンテンツのダウンロード]** ステップを使用します。 同じ変数を使用するように **[パッケージ コンテンツのダウンロード]** ステップをそれぞれ構成します。 **[オペレーティング システムのアップグレード]** ステップの [ドライバー] セクションの **[ステージング済みコンテンツ]** の値にその変数を使います。  

> [!NOTE]  
> このステップを含むタスク シーケンスを展開する場合、ソフトウェアの展開ウィザードの **[配布ポイント]** ページで、 **[展開オプション]** に **[タスク シーケンスを開始する前にすべてのコンテンツをローカルにダウンロードする]** または **[配布ポイントからコンテンツに直接アクセスする]** を選ばないでください。  

このステップは、完全な OS または Windows PE のいずれかで実行されます。 Configuration Manager クライアント キャッシュにパッケージを保存するオプションは、Windows PE ではサポートされません。

> [!NOTE]  
> スタンドアロン メディアでの **[パッケージ コンテンツのダウンロード]** タスクの使用はサポートされていません。 詳細については、「[スタンドアロン メディアでサポートされていないアクション](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media)」をご覧ください。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ソフトウェア]** を選んで、 **[パッケージ コンテンツのダウンロード]** を選びます。

### <a name="cmdlets-for-download-package-content"></a>パッケージ コンテンツのダウンロードのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent?view=sccm-ps)
- [New-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Remove-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Set-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent?view=sccm-ps)

### <a name="properties-for-download-package-content"></a>パッケージ コンテンツのダウンロードのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="select-package"></a>パッケージの選択  

アイコンを選択して、ダウンロードするパッケージを選択します。 1 つのパッケージを選択した後、別のパッケージを選択するにはアイコンをもう一度クリックします。  

#### <a name="place-into-the-following-location"></a>次の場所に保存する

次のいずれかの場所にパッケージを保存する場合に選択します。  

- **タスク シーケンス作業ディレクトリ**: この場所は、タスク シーケンス キャッシュとも呼ばれます。  

- **Configuration Manager クライアント キャッシュ**: このオプションを使用して、クライアント キャッシュにコンテンツを格納します。 既定では、このパスは `%WinDir%\ccmcache` です。  

- **カスタム パス**: タスク シーケンス エンジンは、最初に、タスク シーケンス作業ディレクトリにパッケージをダウンロードします。 次に、ここで指定したパスにコンテンツを移動します。 タスク シーケンス エンジンが、パッケージ ID を使用してパスを追加します。  

#### <a name="save-path-as-a-variable"></a>パスを変数として保存する

パッケージのパスをカスタム タスク シーケンス変数に保存します。 その後、別のタスク シーケンス ステップでこの変数を使用します。

Configuration Manager によって、数字のサフィックスが変数名に追加されます。 たとえば、`%MyContent%` の変数をカスタム変数として指定します。 これは、タスク シーケンスがこのステップに対するすべての参照コンテンツを格納する場所のルートになります。 このコンテンツには、複数のパッケージを含めることができます。 変数を参照するときは、数字のサフィックスを追加します。 最初のパッケージの場合は、`%MyContent01%` を参照します。 **オペレーティング システムのアップグレード**など、後続のステップで変数を参照するときは、`%MyContent02%` または `%MyContent03%` を使います。この数字は、**パッケージ コンテンツのダウンロード** ステップでのパッケージのリスト順に対応します。  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>パッケージのダウンロードに失敗した場合に、リストにある他のパッケージのダウンロードを続行する

タスク シーケンスでパッケージのダウンロードが失敗した場合は、リスト内の次のパッケージのダウンロードを開始します。  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> 注 1:[パッケージ コンテンツのダウンロード] ステップでのブート イメージの使用

*適用対象: バージョン 1910 以降*<!-- SCCMDocs-pr #4202 -->

[タスク シーケンスのプロパティ](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced)を **[ブート イメージを使用する]** に構成した場合、このステップへのブート イメージの追加は冗長です。 タスク シーケンスのプロパティで指定していない場合にのみ、このステップにブート イメージを追加してください。

#### <a name="example-use-case"></a>ユース ケースの例

- コンテンツを事前にダウンロードする単一のタスク シーケンス:
  - 関連付けられたブートイ メージがありません。
  - 完全な OS でのみ実行され、ユーザー操作なしで実行される可能性があります。
  - 条件と共に、複数の **[パッケージ コンテンツのダウンロード]** ステップを使用します。 特定の言語とアーキテクチャによっては、OS 展開のタスク シーケンスを準備するために、クライアント キャッシュにコンテンツがダウンロードされます。
  - このタスク シーケンスのインスタンスは 1 つだけで、可能なコンテンツ オプションがすべて含まれます。

- 複数の OS 展開のタスク シーケンス:
  - 通常の OS 展開のタスク シーケンス。
  - そのプロパティで参照されるブート イメージがあります。
  - このタスク シーケンスのインスタンスは複数あり、アーキテクチャと言語の必要に応じて異なるブート イメージが含まれます

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> BitLocker の有効化

このステップでは、BitLocker 暗号化をハード ドライブの少なくとも 2 つのパーティションで有効にします。 片方のアクティブなパーティションには Windows のブートストラップ コードを格納します。 もう 1 つのパーティションには OS を格納します。 ブートストラップのパーティションは暗号化されていない必要があります。  

Windows PE のドライブで BitLocker を有効にするには、**BitLocker の事前プロビジョニング** ステップを使用します。 詳細については、「[Pre-provision BitLocker](#BKMK_PreProvisionBitLocker)」(BitLocker の事前プロビジョニング) を参照してください。  

> [!NOTE]  
> BitLocker ドライブ暗号化とは、ディスク ボリュームの内容を低レベルで暗号化する処理のことです。  

このステップは完全な OS でのみ実行されます。 Windows PE では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ディスク]** を選んで、 **[BitLocker の有効化]** を選びます。

**[TPM のみ]** 、 **[TPM と、USB 上のスタートアップ キー]** 、または **[TPM および PIN]** を指定する場合、 **[BitLocker の有効化]** ステップを実行するには、先にトラステッド プラットフォーム モジュール (TPM) を次の状態にする必要があります。  

- Enabled  
- アクティブ  
- 所有権を許可  

このステップは、残りの TPM 初期化をすべて完了します。 残りのステップでは、物理的な操作や再起動は必要ありません。 必要な場合、**BitLocker の有効化**ステップでは以降の残りの TPM 初期化ステップが透過的に完了されます。  

- 承認キー ペアの作成  
- 所有権の承認値の作成、およびこの値をサポートするために拡張されている Active Directory への仲介  
- 所有権の取得  
- ストレージ ルート キーの作成、または既に存在しているが互換性がない場合は、リセット  

**[BitLocker の有効化]** ステップがドライブの暗号化処理を完了するまでタスク シーケンスを待機させる場合は、 **[待機]** オプションを選びます。 **[待機]** オプションを選ばないと、ドライブの暗号化処理はバックグラウンドで行われます。 タスク シーケンスは、すぐに次のステップに進みます。  

BitLocker を使用して、コンピューター システムの複数のドライブ (OS ドライブとデータ ドライブの両方) を暗号化することができます。 データ ドライブを暗号化するには、最初に OS ドライブを暗号化して、暗号化処理を完了します。 このような手順が必要であるのは、OS ドライブがデータ ドライブのキー プロテクターを格納しているためです。 OS ドライブとデータ ドライブを同じタスク シーケンスで暗号化する場合は、OS ドライブの **BitLocker の有効化** ステップで **[待機]** オプションを選びます。  

ハード ドライブが既に暗号化されている場合に、BitLocker を無効にすると、 **[BitLocker の有効化]** ステップはキー プロテクターを再度有効にして、すぐに完了します。 この場合、ハード ドライブの再暗号化は不要です。  

### <a name="variables-for-enable-bitlocker"></a>BitLocker の有効化の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)  

### <a name="cmdlets-for-enable-bitlocker"></a>BitLocker の有効化のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker?view=sccm-ps)
- [New-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker?view=sccm-ps)
- [Remove-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker?view=sccm-ps)

### <a name="properties-for-enable-bitlocker"></a>BitLocker の有効化のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="choose-the-drive-to-encrypt"></a>暗号化するドライブの指定

暗号化するドライブを指定します。 現在の OS ドライブを暗号化するには、 **[現在のオペレーティング システム ドライブ]** を選択します。 次に、キー管理に関する以下のオプションの 1 つを構成します。  

- **TPM のみ**: トラステッド プラットフォーム モジュール (TPM) のみを使用する場合に選択します。  

- **USB 上のスタートアップ キーのみ**: USB フラッシュ ドライブに格納されているスタートアップ キーを使用する場合に選択します。 このオプションを選択すると BitLocker は、BitLocker スタートアップ キーが含まれている USB デバイスがコンピューターに接続されるまで、通常のブート プロセスをロックします。  

- **TPM と、USB 上のスタートアップ キー**: TPM と、USB フラッシュ ドライブに格納されているスタートアップ キーを使用する場合に選択します。 このオプションを選択すると BitLocker は、BitLocker スタートアップ キーが含まれている USB デバイスがコンピューターに接続されるまで、通常のブート プロセスをロックします。  

- **TPM および PIN**: TPM と個人識別番号 (PIN) を使用する場合に選択します。 このオプションを選択すると BitLocker は、ユーザーが PIN を入力するまで、通常のブート プロセスをロックします。  

特定のドライブ (OS データ ドライブ以外) を暗号化するには、 **[特定のドライブ]** を選択します。 その後、一覧からドライブを選択します。  

#### <a name="use-full-disk-encryption"></a>ディスク全体の暗号化を使用する

<!--SCCMDocs-pr issue 2671-->
既定では、このステップではドライブ上の使用済み領域のみが暗号化されます。 高速であり、効率性に優れているため、この既定の動作をお勧めします。 組織でセットアップ中、ドライブ全体の暗号化が要求される場合、このオプションを有効にしてください。 Windows セットアップでは、ドライブ全体が暗号化されるのを待ちます。これには、特に大きなドライブで、時間がかかります。

> [!TIP]
> バージョン 1910 以降では、"*ディスク全体*" の暗号化が使用される BitLocker 管理ポリシーを作成して展開することができます。 タスク シーケンスによって OS が展開された後でデバイスの BitLocker を管理するには、このオプションを有効にします。 詳細については、「[BitLocker 管理の計画](../../protect/plan-design/bitlocker-management.md)」を参照してください。

#### <a name="choose-where-to-create-the-recovery-key"></a>リカバリ キーの作成先の選択

BitLocker に対してリカバリ パスワードを作成して Active Directory にエスクローするよう指定するには、 **[In Active Directory]\(Active Directory 内\)** を選択します。 このオプションを使用するには、BitLocker キー エスクロー用に Active Directory を拡張する必要があります。 そうすると、BitLocker は関連付けられているリカバリ情報を Active Directory に保存できます。 パスワードを作成しない場合は、 **[Do not create recovery key]\(リカバリ キーを作成しない\)** を選びます。 パスワードの作成をお勧めします。  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>BitLocker がすべてのドライブの暗号化処理を完了してから、タスク シーケンスを実行する

このオプションを選ぶと、BitLocker のドライブ暗号化が完了してから、タスク シーケンスの次のステップが実行されます。 このオプションを選んだ場合は、ユーザーがコンピューターにサインインできるようになる前に、BitLocker はディスク ボリューム全体を暗号化します。  

大容量のハード ドライブを暗号化する場合、暗号化処理の完了に数時間かかることがあります。 このオプションを選ばないと、タスク シーケンスは直ちに続行されます。  



## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> ディスクのフォーマットとパーティション作成

このステップでは、対象のコンピューター上の指定したディスクをフォーマットしてパーティションを作成します。  

> [!IMPORTANT]  
> このステップで指定するすべての設定は、1 つの指定されたディスクにだけ適用されます。 対象コンピューターの別のディスクのフォーマットとパーティション作成を行う場合は、別の **[ディスクのフォーマットとパーティション作成]** ステップをタスク シーケンスに追加します。  

このステップは Windows PE でのみ実行されます。 完全な OS では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ディスク]** を選んで、 **[ディスクのフォーマットとパーティション作成]** を選びます。

### <a name="variables-for-format-and-partition-disk"></a>ディスクのフォーマットとパーティション作成の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>ディスクのフォーマットとパーティション作成のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteppartitiondisk?view=sccm-ps)
- [New-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteppartitiondisk?view=sccm-ps)
- [Remove-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteppartitiondisk?view=sccm-ps)
- [Set-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteppartitiondisk?view=sccm-ps)

### <a name="properties-for-format-and-partition-disk"></a>ディスクのフォーマットとパーティション作成のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="disk-number"></a>ディスク番号

フォーマットするディスクの物理ディスク番号です。 この番号は、Windows のディスク列挙の順番に基づいています。  

#### <a name="disk-type"></a>ディスクの種類

フォーマットするディスクの種類です。 ドロップダウン リストには次の 2 つのオプションがあります。

- **標準 (MBR)** : マスター ブート レコード  
- **GPT**: GUID パーティション テーブル  

> [!NOTE]  
> ディスクの種類を **[標準 (MBR)]** から **[GPT]** に変更し、パーティション レイアウトの中に拡張パーティションが存在している場合、タスク シーケンスはすべての拡張パーティションと論理パーティションをレイアウトから削除します。 タスク シーケンス エディターでは、ディスクの種類が変更される前に、このアクションを実行するかどうかを確認するメッセージが表示されます。  

#### <a name="volume"></a>ボリューム

タスク シーケンスで作成されるパーティションまたはボリュームに関する詳細な情報です。次の情報が含まれます。  

- 名前  
- ディスクの空き容量  

新しいパーティションを作成するには、 **[新規]** ボタンを選択して、 **[パーティションのプロパティ]** ダイアログ ボックスを開きます。 パーティションの種類とサイズ、およびブート パーティションかどうかを指定します。 既存のパーティションを変更するには、変更するパーティションを選択してから、 **[プロパティ]** ボタンを選択します。 ハード ドライブのパーティションを構成する方法については、次のいずれかの記事を参照してください。  

- [UEFI/GPT ベースのハード ドライブ パーティション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [BIOS/MBR ベースのハード ドライブ パーティション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

パーティションを削除するには、パーティションを選択してから、 **[削除]** を選択します。  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a> アプリケーションのインストール

このステップでは、指定したアプリケーション、またはタスク シーケンス変数の動的なリストによって定義したアプリケーションのセットがインストールされます。 タスク シーケンスがこのステップを実行すると、アプリケーションのインストールはポリシーのポーリング間隔を待たずにすぐ開始されます。  

アプリケーションは次の条件を満たす必要があります。  

- アプリケーションの展開の種類は、**Windows インストーラー**または**スクリプト** インストーラーでなければなりません。 Windows アプリ パッケージ (.appx ファイル) の展開の種類はサポートされていません。  

- ユーザー アカウントではなく、ローカル システム アカウントで実行する必要があります。  

- デスクトップと通信してはいけません。 プログラムは、サイレントまたは無人モードで実行する必要があります。  

- 自動的に再起動を開始させてはいけません。 アプリケーションは、標準再起動コードの 3010 を使用して再起動を要求する必要があります。 この動作により、このステップで再起動が正しく処理されます。 アプリケーションが 3010 終了コードを返さない場合、タスク シーケンス エンジンはコンピューターを再起動します。 再起動後にタスク シーケンスは自動的に続行されます。  

> [!Note]
> アプリケーションによって[実行中の実行可能ファイルが確認される](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check)場合、タスク シーケンスによるインストールは失敗します。 このステップをエラー時に続行するように構成しなかった場合、タスク シーケンス全体が失敗します。

このステップが実行されると、アプリケーションは、アプリケーションの展開の種類で要件ルールと検出方法が適用可能かどうかを確認します。 この確認の結果によって、アプリケーションは適用される展開の種類をインストールします。 展開の種類が依存関係を含んでいる場合は、このステップの一環として依存する展開の種類が評価され、インストールされます。 スタンドアロン メディアでは、アプリケーションの依存関係はサポートされていません。  

> [!NOTE]  
> 別のアプリケーションを置き換えるアプリケーションをインストールするには、置換対象のアプリケーションのコンテンツ ファイルを使用可能である必要があります。 使用できない場合、タスク シーケンス ステップは失敗します。 たとえば、Microsoft Visio 2010 は、クライアント、または、キャプチャされたイメージ内にインストールされます。 **[アプリケーションのインストール]** ステップで Microsoft Visio 2013 をインストールする場合は、Microsoft Visio 2010 (置換対象のアプリケーション) のコンテンツ ファイルが配布ポイントで利用できる必要があります。 クライアントまたはキャプチャされたイメージに Microsoft Visio がインストールされていない場合、タスク シーケンスは Microsoft Visio 2010 のコンテンツ ファイルのチェックを行わずに、Microsoft Visio 2013 をインストールします。  
>
> 置き換えられたアプリをインベントリから削除し、新しいアプリがタスク シーケンスで参照されている場合、タスク シーケンスは起動に失敗します。
この動作は仕様です。タスク シーケンスには、すべてのアプリの参照が必要です。<!-- SCCMDocs 1711 -->  

このタスク シーケンス ステップは完全な OS でのみ実行されます。 Windows PE では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ソフトウェア]** を選んで、 **[アプリケーションのインストール]** を選びます。

### <a name="variables-for-install-application"></a>アプリケーションのインストールの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> クライアントで場所サービスからの管理ポイント一覧の取得が失敗する場合は、**SMSTSMPListRequestTimeoutEnabled** および **SMSTSMPListRequestTimeout** タスク シーケンス変数を使用します。 これらの変数では、アプリケーションのインストールを再試行する前に、タスク シーケンスが待機するミリ秒数を指定します。 詳しくは、「[タスク シーケンス変数](task-sequence-variables.md)」をご覧ください。

### <a name="cmdlets-for-install-application"></a>アプリケーションのインストールのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallapplication?view=sccm-ps)
- [New-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallapplication?view=sccm-ps)
- [Remove-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallapplication?view=sccm-ps)
- [Set-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallapplication?view=sccm-ps)

### <a name="properties-for-install-application"></a>アプリケーションのインストールのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="install-the-following-applications"></a>次のアプリケーションをインストールする

タスク シーケンスは、指定した順序でこれらのアプリケーションをインストールします。  

Configuration Manager は、無効なアプリケーションまたは次のように設定されたアプリケーションを除外します。  

- ユーザーがログオンしているときのみ  
- ユーザーの権限で実行する  

これらのアプリケーションは、 **[インストールするアプリケーションの選択]** ダイアログ ボックスには表示されません。

#### <a name="install-applications-according-to-dynamic-variable-list"></a>動的な変数一覧に従ってアプリケーションをインストールする

タスク シーケンスは、この基本変数名を使ってアプリケーションをインストールします。 基本変数名は、コレクションまたはコンピューターに対して定義されているタスク シーケンス変数のセットに対するものです。 これらの変数では、タスク シーケンスがそのコレクションまたはコンピューターに対してインストールするアプリケーションを指定します。 各変数名は、共通のベース名と「01」で始まる数字のサフィックスで構成されます。 各変数の値にはアプリケーションの名前以外は何も含んではいけません。  

動的な変数一覧を使ってアプリケーションをインストールするタスクシーケンスの場合は、アプリケーションの **[プロパティ]** の **[全般]** タブ上で、次の設定を有効にします: **このアプリケーションを展開せずに [アプリケーションのインストール] タスク シーケンスでインストールできるようにする**。  

> [!NOTE]  
> スタンドアロン メディアによる展開では動的な変数一覧を使用してアプリケーションをインストールすることはできません。  

たとえば、AA01 というタスク シーケンス変数を使用して 1 つのアプリケーションをインストールするには、次の変数を指定します。  

|変数名|変数値|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

2 つのアプリケーションをインストールするには、次の変数を指定します。  

|変数名|変数値|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

次の条件は、タスク シーケンスによってインストールされるアプリケーションに影響を与えます。  

- 変数の値にアプリケーションの名前以外が含まれている場合。 タスク シーケンスはアプリケーションをインストールせず、タスク シーケンスが続行します。  

- タスク シーケンスは、指定された基本名とサフィックス "01" を持つ変数が見つからない場合は、どのアプリケーションもインストールしません。  

> [!Important]  
> これらの値では大文字と小文字が区別されます。 たとえば、"install" と "Install" は区別されます。 値を変更する必要がある場合、タスク シーケンス エディターでは大文字と小文字の変更が検出されません。 別の編集を同時に行います (たとえば、ステップの説明の変更)。<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>アプリケーションのインストールに失敗した場合は、一覧にあるその他のアプリケーションのインストールを続行します。

この設定は、個々のアプリケーションのインストールが失敗してもステップを続行することを指定します。 この設定を指定すると、タスク シーケンスはインストール エラーに関係なく続行されます。 この設定を指定しないと、インストールが失敗した場合はステップが直ちに終了します。  

#### <a name="clear-application-content-from-cache-after-installing"></a>インストール後にキャッシュからアプリケーションのコンテンツをクリアする

<!--4485675-->
バージョン 1906 以降では、ステップの実行後にクライアント キャッシュからアプリ コンテンツを削除します。 この動作は、ハード ドライブの容量が少ないデバイスや、連続して多くの大規模なアプリをインストールするときに役立ちます。


### <a name="options-for-install-application"></a>アプリケーションのインストールのオプション

> [!NOTE]  
> このステップの **[オプション]** タブで **[エラー時に続行する]** を選ぶと、アプリケーションのインストールが失敗した場合でも、タスク シーケンスは続行されます。 このオプションを有効にしないと、タスク シーケンスは失敗し、残りのアプリケーションはインストールされません。  

このタスク シーケンス ステップの **[オプション]** タブでは、既定のオプションだけでなく、以下の追加設定を構成します。  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>コンピューターが予期せず再起動した場合にこの手順を再試行する

アプリケーションのインストールのいずれかでコンピューターが予期せず再起動された場合は、このステップを再試行します。 この設定は既定で有効になり、再試行回数は 2 回に設定されます。 再試行回数は 1 から 5 回の範囲で指定できます。  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a> パッケージのインストール

このステップでは、タスク シーケンスの一部としてソフトウェア パッケージをインストールします。 このステップが実行されると、インストールはポリシーのポーリング間隔を待たずにすぐ開始されます。  

パッケージは次の条件を満たす必要があります。  

- ユーザー アカウントではなく、ローカル システム アカウントで実行する必要があります。  

- デスクトップと通信してはいけません。 プログラムは、サイレントまたは無人モードで実行する必要があります。  

- 自動的に再起動を開始させてはいけません。 ソフトウェアは、標準再起動コードの 3010 を使用して再起動を要求する必要があります。 この動作により、タスク シーケンスは再起動を適切に処理するようになります。 ソフトウェアが 3010 終了コードを返さない場合、タスク シーケンス エンジンはコンピューターを再起動します。 再起動後にタスク シーケンスは自動的に続行されます。  

依存プログラムのインストールに **[別のプログラムを最初に実行する]** オプションを使用するプログラムは、OS の展開ではサポートされていません。 パッケージ オプション **[別のプログラムを最初に実行する]** が有効になっていて、依存プログラムが対象のコンピューターで既に実行された場合は、依存プログラムが実行されて、タスク シーケンスは続行します。 一方、依存プログラムが対象のコンピューターでまだ実行されていない場合は、タスク シーケンスは失敗します。  

> [!NOTE]  
> 中央管理サイトには、タスク シーケンスの間にソフトウェア配布エージェントを有効にするために必要なクライアント構成ポリシーがありません。 中央管理サイトのタスク シーケンス用にスタンドアロン メディアを作成し、タスク シーケンスに **[パッケージのインストール]** ステップが含まれる場合、CreateTsMedia.log ファイルに次のエラーが表示される場合があります。  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> **[パッケージのインストール]** ステップを含むスタンドアロン メディアの場合は、ソフトウェア配布エージェントが有効になっているプライマリ サイトでスタンドアロン メディアを作成します。 または、 **[Windows と ConfigMgr のセットアップ]** ステップの後、最初の **[パッケージのインストール]** ステップの前に、 **[コマンド ラインの実行]** ステップを追加します。 **[コマンド ラインの実行]** ステップは、最初の **[パッケージのインストール]** ステップの前に、WMIC コマンドを実行してソフトウェア配布エージェントを有効にします。 **[コマンド ラインの実行]** ステップでは次のコマンドを使います。  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> スタンドアロン メディアの作成の詳細については、「[スタンドアロン メディアの作成](../deploy-use/create-stand-alone-media.md)」を参照してください。  

このタスク シーケンス ステップは完全な OS でのみ実行されます。 Windows PE では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ソフトウェア]** を選んで、 **[パッケージのインストール]** を選びます。

### <a name="variables-for-install-package"></a>パッケージのインストールの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>パッケージのインストールのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallsoftware?view=sccm-ps)
- [New-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallsoftware?view=sccm-ps)
- [Remove-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware?view=sccm-ps)
- [Set-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallsoftware?view=sccm-ps)

> [!TIP]
> ユーザーがタスク シーケンスをインストールする前に、コンテンツの事前キャッシュを使用して該当する OS アップグレード パッケージをダウンロードします。 詳細については、「[コンテンツの事前キャッシュを構成する](../deploy-use/configure-precache-content.md)」を参照してください。

### <a name="properties-for-install-package"></a>パッケージのインストールのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="install-a-single-software-package"></a>ソフトウェア パッケージを 1 つだけインストールする

この設定では、Configuration Manager ソフトウェア パッケージを指定します。 ステップはインストールが完了するまで待ちます。  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>動的な変数一覧に従ってソフトウェア パッケージをインストールする

タスク シーケンスは、この基本変数名を使ってパッケージをインストールします。 基本変数名は、コレクションまたはコンピューターに対して定義されているタスク シーケンス変数のセットに対するものです。 これらの変数では、タスク シーケンスがそのコレクションまたはコンピューターに対してインストールするパッケージを指定します。 各変数名は、共通のベース名と「001」で始まる数字のサフィックスで構成されます。 各変数の値にはパッケージ ID およびソフトウェアの名前をコロンで区切って含んでいる必要があります。  

動的な変数一覧を使ってソフトウェアをインストールするタスクシーケンスの場合は、パッケージの **[プロパティ]** ダイアログ ボックスの **[詳細設定]** タブで次の設定を有効にします: **このソフトウェアを展開しないで、ソフトウェアのインストール タスク シーケンスからこのプログラムをインストールする**。  

> [!NOTE]  
> スタンドアロン メディアによる展開では動的な変数一覧を使用してソフトウェア パッケージをインストールすることはできません。  

たとえば、AA001 というタスク シーケンス変数を使用して 1 つのソフトウェア パッケージをインストールするには、次の変数を指定します。  

|変数名|変数値|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

3 つのソフトウェア パッケージをインストールするには、次の変数を指定します。  

|変数名|変数値|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|Package CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

次の条件は、タスク シーケンスによってインストールされるパッケージに影響を与えます。  

- 変数の値が正しい形式で作成されていない場合、または有効なパッケージ ID と名前が指定されていない場合は、ソフトウェアのインストールは失敗します。  

- パッケージ ID に小文字が含まれている場合は、ソフトウェアのインストールは失敗します。  

- タスク シーケンスは、指定された基本名とサフィックス "001" を持つ変数が見つからない場合は、どのパッケージンもインストールしません。 タスク シーケンスは続行します。  

> [!Important]  
> これらの値では大文字と小文字が区別されます。 たとえば、"install" と "Install" は区別されます。 値を変更する必要がある場合、タスク シーケンス エディターでは大文字と小文字の変更が検出されません。 別の編集を同時に行います (たとえば、ステップの説明の変更)。<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>ソフトウェア パッケージのインストールに失敗した場合に、一覧にある他のパッケージのインストールを続行する

この設定は個々のソフトウェア パッケージのインストールが失敗してもステップを続行することを指定します。 この設定を指定すると、タスク シーケンスはインストール エラーに関係なく続行されます。 この設定を指定しないと、インストールが失敗した場合はステップが直ちに終了します。  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> ソフトウェア更新プログラムのインストール

このステップでは、ソフトウェア更新プログラムを対象コンピューターにインストールします。 このタスク シーケンス ステップが実行されるまで、対象のコンピューターは適用可能なソフトウェア更新プログラムが評価されません。 実行されると、他の Configuration Manager クライアントと同様に、対象コンピューターでソフトウェアの更新状態が評価されます。 このステップでソフトウェア更新プログラムをインストールするには、最初に、ターゲット コンピューターがメンバーであるコレクションに、更新プログラムを展開します。  

> [!IMPORTANT]  
> パフォーマンスを最善にするには、最新バージョンの Windows Update エージェントをインストールします。  

このタスク シーケンス ステップは完全な OS でのみ実行されます。 Windows PE では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ソフトウェア]** を選んで、 **[ソフトウェア更新プログラムのインストール]** を選びます。

### <a name="variables-for-install-software-updates"></a>ソフトウェア更新プログラムのインストールの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> クライアントで場所サービスからの管理ポイント一覧の取得が失敗する場合は、**SMSTSMPListRequestTimeoutEnabled** および **SMSTSMPListRequestTimeout** 変数を使用します。 これらの変数では、アプリケーションまたはソフトウェアの更新のインストールを再試行する前に、タスク シーケンスが待機するミリ秒数を指定します。 詳しくは、「[タスク シーケンス変数](task-sequence-variables.md)」をご覧ください。  

### <a name="cmdlets-for-install-software-updates"></a>ソフトウェア更新プログラムのインストールのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallupdate?view=sccm-ps)
- [New-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallupdate?view=sccm-ps)
- [Remove-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallupdate?view=sccm-ps)
- [Set-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallupdate?view=sccm-ps)

その他の推奨事項とこのステップのテクニカル フロー チャート図については、「[Install Software Updates](install-software-updates.md)」 (ソフトウェア更新プログラムのインストール) を参照してください。

### <a name="properties-for-install-software-updates"></a>ソフトウェア更新プログラムのインストールのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>インストールが必要 - 必須のソフトウェア更新プログラムのみ

管理者が定義したインストール期限ですべての必須ソフトウェア更新プログラムをインストールするには、このオプションを選びます。  

#### <a name="available-for-installation---all-software-updates"></a>インストールが可能 - すべてのソフトウェア更新プログラム

利用可能なソフトウェア更新プログラムをすべてインストールするには、このオプションを選びます。 最初に、コンピューターがメンバーであるコレクションにこれらの更新プログラムを展開します。 タスク シーケンスでは、利用可能なすべてのソフトウェア更新プログラムが対象コンピューターにインストールされます。  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>キャッシュされたスキャン結果からのソフトウェア更新プログラムの評価

既定では、このステップでは Windows Update エージェントにあるキャッシュされたスキャン結果が使用されます。 最新のカタログをソフトウェアの更新ポイントからダウンロードするよう Windows Update エージェントに指示するには、このオプションを無効にします。 タスク シーケンスを使って [OS イメージをキャプチャして構築する](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)場合は、このオプションを有効にします。 このシナリオでは、ソフトウェア更新プログラムの数が多くなる可能性があります。

これらの更新プログラムの多くには依存関係があります。 たとえば、更新プログラム XYZ が該当するものと表示される前に、更新プログラム ABC をインストールします。 この設定を無効にして、多数のクライアントにタスク シーケンスを展開すると、すべてのクライアントが同時にソフトウェアの更新ポイントに接続します。 これにより、更新プログラム カタログの処理とダウンロードの間にパフォーマンスの問題が発生します。

ほとんどの状況では既定の設定を使用し、キャッシュされたスキャン結果を使用します。

**SMSTSSoftwareUpdateScanTimeout** 変数は、このステップでのソフトウェア更新プログラムのスキャンのタイムアウトを制御します。 既定値は 60 分です。 詳しくは、「[タスク シーケンス変数](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)」をご覧ください。

### <a name="options-for-install-software-updates"></a>ソフトウェア更新プログラムのインストールのオプション

このタスク シーケンス ステップの **[オプション]** タブでは、既定のオプションだけでなく、以下の追加設定を構成します。  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>コンピューターが予期せず再起動した場合にこの手順を再試行する

更新プログラムのいずれかでコンピューターが予期せず再起動された場合は、このステップを再試行します。 この設定は既定で有効になり、再試行回数は 2 回に設定されます。 再試行回数は 1 から 5 回の範囲で指定できます。  

> [!NOTE]  
> このシナリオでコンピューターの再起動後にタスク シーケンスが一時停止する秒数を指定するには、**SMSTSWaitForSecondReboot** 変数を構成します。 詳しくは、「[タスク シーケンス変数](task-sequence-variables.md#SMSTSWaitForSecondReboot)」をご覧ください。  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> ドメインまたはワークグループへの参加

このステップでは、対象コンピューターをワークグループまたはドメインに追加します。  

このタスク シーケンス ステップは完全な OS でのみ実行されます。 Windows PE では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[ドメインまたはワークグループに参加]** を選びます。

### <a name="variables-for-join-domain-or-workgroup"></a>ドメインまたはワークグループに参加の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>ドメインまたはワークグループに参加のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [New-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Remove-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Set-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup?view=sccm-ps)

### <a name="properties-for-join-domain-or-workgroup"></a>ドメインまたはワークグループに参加のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="join-a-workgroup"></a>ワークグループに参加

対象コンピューターを指定したワークグループに参加させるには、このオプションを選択します。 コンピューターが現在ドメインのメンバーである場合は、このオプションを選ぶとコンピューターが再起動します。  

#### <a name="join-a-domain"></a>ドメインに参加

対象コンピューターを指定したドメインに参加させるには、このオプションを選択します。  

必要に応じて、コンピューターが参加する、指定したドメインの組織単位 (OU) を入力または参照して指定します。 現在、コンピューターが他のドメインまたはワークグループのメンバーである場合は、このオプションを選ぶとコンピューターが再起動します。 コンピューターが既に別の OU のメンバーになっている場合、Active Directory Domain Services ではこの方法で OU を変更することはできないので、Windows セットアップはこの設定を無視します。  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>ドメインに参加する権限のあるアカウントを入力してください

**[設定]** を選択し、ドメインに参加するアクセス許可を持つアカウントのユーザー名とパスワードを入力します。 `Domain\account` の形式でアカウントを入力します。 タスク シーケンスのドメイン参加アカウントについて詳しくは、[アカウント](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)に関するページをご覧ください。  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> ConfigMgr クライアントのキャプチャの準備

このステップでは、参照コンピューター上の Configuration Manager クライアントを削除または構成します。 このアクションは、イメージ作成プロセスの一部としてキャプチャできるようにコンピューターを準備します。

このステップでは、キー情報だけではなく、Configuration Manager クライアントが完全に削除されます。 タスク シーケンスは、キャプチャされた OS イメージを展開するとき、毎回新しい Configuration Manager クライアントをインストールします。  

> [!Note]  
> タスク シーケンス エンジンは、 **[参照オペレーティング システム イメージを構築およびキャプチャする]** タスク シーケンスの間にだけ、クライアントを削除します。 タスク シーケンス エンジンでは、メディアのキャプチャやカスタム タスク シーケンスなど、他のキャプチャ方法でクライアントは削除されません。  

このタスク シーケンス ステップは完全な OS でのみ実行されます。 Windows PE では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[イメージ]** を選んで、 **[ConfigMgr クライアントのキャプチャの準備]** を選びます。

### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>ConfigMgr クライアントのキャプチャの準備のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [New-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Remove-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Set-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient?view=sccm-ps)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Windows のキャプチャの準備

このステップでは、参照コンピューターの OS イメージをキャプチャするときの Sysprep オプションを指定します。 このステップは、Sysprep が実行され、タスク シーケンスに指定した Windows PE ブート イメージでコンピューターが再起動されます。 参照コンピューターがドメインに参加している場合、このアクションは失敗します。  

このステップは完全な OS でのみ実行されます。 Windows PE では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[イメージ]** を選んで、 **[Windows のキャプチャの準備]** を選びます。

### <a name="variables-for-prepare-windows-for-capture"></a>Windows のキャプチャの準備の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>Windows のキャプチャの準備のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows?view=sccm-ps)
- [New-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareWindows?view=sccm-ps)
- [Remove-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows?view=sccm-ps)
- [Set-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows?view=sccm-ps)

### <a name="properties-for-prepare-windows-for-capture"></a>Windows のキャプチャの準備のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="automatically-build-mass-storage-driver-list"></a>大容量記憶装置ドライバーのリストを自動作成する

このオプションをオンにすると、Sysprep によって参照コンピューターから大容量記憶装置ドライバーのリストが自動的に作成されます。 このオプションでは、参照コンピューターの sysprep.inf ファイルにある [大容量記憶装置ドライバーの作成] オプションが有効になります。 この設定については、Sysprep のドキュメントを参照してください。  

#### <a name="do-not-reset-activation-flag"></a>アクティブ化フラグをリセットしない

このオプションをオンにすると、Sysprep によってプロダクト アクティベーション フラグがリセットされなくなります。  

#### <a name="shutdown-the-computer-after-running-this-action"></a>この操作の実行後にコンピューターをシャットダウンする

<!--SCCMDocs-pr issue 2695-->
このオプションは、その既定の再起動動作ではなく、コンピューターをシャットダウンするよう Sysprep に指示します。

このオプションでは、このステップは[既存のデバイス向け Windows Autopilot](../../../autopilot/existing-devices.md) タスク シーケンスで使用されます。

- タスク シーケンスでデバイスを更新した後すぐに OOBE for Autopilot を起動する場合は、このオプションをオフのままにします。  

- イメージング後にこのオプションを有効にしてデバイスをシャットダウンします。 これでデバイスをユーザーに提供できます。ユーザーがデバイスを初めてオンにすると、Autopilot で OOBE が起動されます。  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> BitLocker の事前プロビジョニング

このステップでは、Windows PE のドライブで BitLocker を有効にします。 既定では、使用されているドライブ領域のみが暗号化されるため、暗号化にかかる時間が大幅に短くなります。 OS のインストール後に [BitLocker の有効化](#BKMK_EnableBitLocker)ステップを使用することで、キー管理オプションを適用します。

> [!IMPORTANT]
> BitLocker を事前プロビジョニングするには、コンピューターにサポートされているトラステッド プラットフォーム モジュール (TPM) が必要です。

このステップは Windows PE でのみ実行されます。 完全な OS では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ディスク]** を選んで、 **[BitLocker の事前プロビジョニング]** を選びます。

### <a name="cmdlets-for-pre-provision-bitlocker"></a>BitLocker の事前プロビジョニングのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [New-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Remove-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker?view=sccm-ps)

### <a name="properties-for-pre-provision-bitlocker"></a>BitLocker の事前プロビジョニングのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>BitLocker を指定のドライブに適用します

BitLocker を有効にするドライブを指定します。 ドライブ上の使用領域のみが暗号化されます。  

#### <a name="use-full-disk-encryption"></a>ディスク全体の暗号化を使用する

<!--SCCMDocs-pr issue 2671-->
既定では、このステップではドライブ上の使用済み領域のみが暗号化されます。 高速であり、効率性に優れているため、この既定の動作をお勧めします。 組織でセットアップ中、ドライブ全体の暗号化が要求される場合、このオプションを有効にしてください。 Windows セットアップでは、ドライブ全体が暗号化されるのを待ちます。これには、特に大きなドライブで、時間がかかります。

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>TPM がないか、TPM が有効ではない場合は、コンピューターでこの手順はスキップされます。

サポートされる TPM または有効な TPM が含まれないコンピューターでのドライブ暗号化をスキップする場合は、このオプションを選びます。 たとえば、仮想マシンに OS を展開するときは、このオプションを使います。  



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> 状態ストアのリリース

このステップでは、キャプチャ アクションまたは復元アクションが完了した状態移行ポイントを通知します。 このステップは、 **[状態ストアの要求]** 、 **[ユーザー状態のキャプチャ]** 、 **[ユーザー状態の復元]** の各ステップと組み合わせて使います。 状態移行ポイントおよびユーザー状態移行ツール (USMT) を使ってユーザー状態データを移行するには、これらのステップを使います。  

オペレーティング システムを展開するときに、ユーザー状態の移行を管理する方法の詳細については、「[Manage user state](../get-started/manage-user-state.md)」 (ユーザー状態の管理) を参照してください。  

**[状態ストアの要求]** ステップを使ってユーザー状態を "*キャプチャ*" するための状態移行ポイントへのアクセスを要求する場合、このステップはキャプチャ プロセスが完了したことを状態移行ポイントに通知します。 状態移行ポイントは、復元に利用可能としてユーザー状態データをマークします。 状態移行ポイントは、復元中のコンピューターのみが読み取り専用でアクセスできるように、ユーザー状態データに対するアクセス制御のアクセス許可を設定します。  

**[状態ストアの要求]** ステップを使ってユーザー状態を "*復元*" するための状態移行ポイントへのアクセスを要求する場合、このステップは復元プロセスが完了したことを状態移行ポイントに通知します。 その後、状態移行ポイントはその構成済みのデータ保有設定をアクティブにします。  

> [!IMPORTANT]  
> **状態ストアの要求**ステップと**状態ストアのリリース** ステップの間のすべてのステップで、 **[エラー時に続行する]** オプションを設定します。 すべての **[状態ストアの要求]** ステップに、対応する **[状態ストアのリリース]** ステップが存在する必要があります。  

このステップは完全な OS でのみ実行されます。 Windows PE では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ユーザー状態]** を選んで、 **[状態ストアのリリース]** を選びます。

### <a name="variables-for-release-state-store"></a>状態ストアのリリースの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>状態ストアのリリースのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore?view=sccm-ps)
- [New-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore?view=sccm-ps)
- [Remove-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore?view=sccm-ps)
- [Set-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore?view=sccm-ps)

### <a name="properties-for-release-state-store"></a>状態ストアのリリースのプロパティ

このステップでは、 **[プロパティ]** タブでの設定は何も必要ありません。



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a> 状態ストアの要求

このステップでは、状態をキャプチャまたは復元するときに、状態移行ポイントへのアクセスを要求します。  

オペレーティング システムを展開するときに、ユーザー状態の移行を管理する方法の詳細については、「[Manage user state](../get-started/manage-user-state.md)」 (ユーザー状態の管理) を参照してください。  

このステップは、 **[状態ストアのリリース]** 、 **[ユーザー状態のキャプチャ]** 、 **[ユーザー状態の復元]** の各ステップと組み合わせて使います。 状態移行ポイントおよびユーザー状態移行ツール (USMT) を使ってコンピューターの状態を移行するには、これらのステップを使います。  

> [!NOTE]  
> 新しい状態移行ポイントを作成するとき、ユーザー状態ストレージが利用できるようになるまで最大で 1 時間かかることがあります。 利用できるようになるまでの時間を短縮するには、いずれかの状態移行ポイントのプロパティ設定を調整して、サイト コントロール ファイルの更新を開始します。  

このステップは、完全な OS と、オフライン USMT の Windows PE で実行されます。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ユーザー状態]** を選んで、 **[状態ストアの要求]** を選びます。

### <a name="variables-for-request-state-store"></a>状態ストアの要求の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>状態ストアの要求のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore?view=sccm-ps)
- [New-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRequestStateStore?view=sccm-ps)
- [Remove-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore?view=sccm-ps)
- [Set-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore?view=sccm-ps)

### <a name="properties-for-request-state-store"></a>状態ストアの要求のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="capture-state-from-the-computer"></a>状態をコンピューターからキャプチャする

状態移行ポイントの設定で構成されている最小要件を満たす状態移行ポイントを検索します。 たとえば、**最大クライアント数**や**空きディスク領域の最小量**などです。 このオプションでは、状態移行時に十分な空き領域があることは保証されません。 このオプションは、ユーザー状態と設定をコンピューターからキャプチャするために状態移行ポイントにアクセスすることを要求します。  

Configuration Manager サイトに複数のアクティブな状態移行ポイントがある場合、このステップは、使用可能なディスク領域のある状態移行ポイントを検索します。 タスク シーケンスは、状態移行ポイントの一覧で管理ポイントを照会してから、最小要件を満たすものが見つかるまで各ポイントを評価します。  

#### <a name="restore-state-from-another-computer"></a>状態を他のコンピューターから復元する

以前にキャプチャされたユーザー状態と設定を対象コンピューターに復元するため、状態移行ポイントへのアクセスを要求します。  

複数の状態移行ポイントが存在する場合、このステップは、対象コンピューターに対する状態を持つ状態移行ポイントを検索します。  

#### <a name="number-of-retries"></a>再試行回数

このステップが適切な状態移行ポイントを検索する試行回数です。この回数を超えるとステップは失敗します。  

#### <a name="retry-delay-in-seconds"></a>再試行の待ち時間 (秒)

タスク シーケンス ステップが再試行を行うまで待機する時間 (秒単位) です。  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>コンピューター アカウントで状態ストアに接続できない場合、ネットワーク アクセス アカウントを使用する

タスク シーケンスは、コンピューター アカウントを使って状態移行ポイントにアクセスできない場合、ネットワーク アクセス アカウントの資格情報を使って接続します。 他のコンピューターがネットワーク アクセス アカウントを使って格納されている状態にアクセスできるため、このオプションを使うと安全性が低下します。 対象コンピューターがドメインに参加していない場合、このオプションが必要になる可能性があります。  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a> コンピューターの再起動

このステップでは、タスク シーケンスを実行しているコンピューターを再起動します。 コンピューターは再起動後、タスク シーケンスの次のステップから自動的に続行します。  

このステップは、完全な OS または Windows PE のいずれかで実行できます。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[コンピューターの再起動]** を選びます。

### <a name="variables-for-restart-computer"></a>コンピューターの再起動の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>コンピューターの再起動のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepreboot?view=sccm-ps)
- [New-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepreboot?view=sccm-ps)
- [Remove-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepreboot?view=sccm-ps)
- [Set-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepreboot?view=sccm-ps)

### <a name="properties-for-restart-computer"></a>コンピューターの再起動のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>このタスク シーケンスに割り当てられているブート イメージ

タスク シーケンスに割り当てられているブート イメージを対象コンピューターで使うには、このオプションを選びます。 タスク シーケンスはブート イメージを使って、Windows PE で以降の手順を実行します。  

#### <a name="the-currently-installed-default-operating-system"></a>現在インストールされている既定のオペレーティング システム

インストールされている OS で対象コンピューターを起動するには、このオプションを選択します。  

#### <a name="notify-the-user-before-restarting"></a>再起動する前にユーザーに通知する

対象コンピューターを再起動する前にユーザーに通知を表示するには、このオプションを選びます。 このオプションは既定で有効になります。  

#### <a name="notification-message"></a>通知メッセージ

対象コンピューターの再起動前にユーザーに表示する通知メッセージを入力します。  

#### <a name="message-display-time-out"></a>メッセージ表示のタイムアウト

対象コンピューターを再起動するまでの秒数を指定します。 既定値は 60 秒です。  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a> ユーザー状態の復元

このステップでは、ユーザー状態移行ツール (USMT) を開始して、対象コンピューターにユーザーの状態と設定を復元します。 このステップは、 **[ユーザー状態のキャプチャ]** ステップと組み合わせて使います。  

オペレーティング システムを展開するときに、ユーザー状態の移行を管理する方法の詳細については、「[Manage user state](../get-started/manage-user-state.md)」 (ユーザー状態の管理) を参照してください。  

状態移行ポイントで状態の設定を保存または復元するには、このステップと共に **[状態ストアの要求]** および **[状態ストアのリリース]** ステップを使います。 このオプションでは常に、Configuration Manager が生成および管理する暗号化キーを使用して、USMT 状態ストアが暗号解除されます。  

**[ユーザー状態の復元]** ステップでは、最も一般的に使われるオプションの限定されたサブセットを制御できます。 その他のコマンド ライン オプションは、**OSDMigrateAdditionalRestoreOptions** 変数で指定します。  

> [!IMPORTANT]  
> OS 展開シナリオとは関係のない目的にこのステップを使っている場合は、**ユーザー状態の復元**ステップの直後に[コンピューターの再起動](#BKMK_RestartComputer)ステップを追加します。  

このステップは完全な OS でのみ実行されます。 Windows PE では実行されません。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[ユーザー状態]** を選んで、 **[ユーザー状態の復元]** を選びます。

### <a name="variables-for-restore-user-state"></a>ユーザー状態の復元の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>ユーザー状態の復元のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState?view=sccm-ps)
- [New-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRestoreUserState?view=sccm-ps)
- [Remove-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState?view=sccm-ps)
- [Set-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState?view=sccm-ps)

### <a name="properties-for-restore-user-state"></a>ユーザー状態の復元のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="user-state-migration-tool-package"></a>ユーザー状態移行ツール パッケージ

このステップで使うバージョンの USMT を含むパッケージを指定します。 このパッケージにはプログラムは必要ありません。 ステップ実行時に、タスク シーケンスは指定したパッケージに含まれる USMT のバージョンを使います。 32 ビット バージョンまたは 64 ビット バージョンの USMT を含むパッケージを指定します。 USMT のアーキテクチャは、タスク シーケンスが状態を復元する OS のアーキテクチャによって異なります。

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>キャプチャしたすべてのユーザー プロファイルを標準オプションを使用して復元する

キャプチャしたユーザー プロファイルを標準オプションを使用して復元します。 USMT が復元するオプションをカスタマイズするには、 **[ユーザー プロファイルのキャプチャ方法をカスタマイズする]** を選びます。  

#### <a name="customize-how-user-profiles-are-restored"></a>ユーザー プロファイルの復元方法をカスタマイズする

対象のコンピューターに復元するファイルをカスタマイズできます。 **[ファイル]** を選択して、ユーザー プロファイルの復元に使用する、USMT パッケージ内の構成ファイルを指定します。 構成ファイルを追加するには、 **[ファイル名]** ボックスにファイル名を入力し、 **[追加]** を選択します。 [ファイル] ウィンドウには、USMT が使う構成ファイルが一覧表示されます。 USMT によって復元されるユーザー ファイルが定義されている .xml ファイルを指定します。  

#### <a name="restore-local-computer-user-profiles"></a>ローカル コンピューターのユーザー プロファイルを復元する

ローカル コンピューターのユーザー プロファイルを復元します。 これらのプロファイルは、ドメイン ユーザーのものではありません。 復元されるローカル ユーザー アカウントには、新しいパスワードを割り当てます。 USMT では元のパスワードを移行できません。 **[パスワード]** ボックスに新しいパスワードを入力し、 **[パスワードの確認入力]** ボックスに確認のために同じパスワードを入力します。  

#### <a name="continue-if-some-files-cannot-be-restored"></a>復元できないファイルがあっても続行する

USMT が一部のファイルを復元できない場合でも、ユーザー状態と設定の復元を続行します。 このオプションは既定で有効になります。 このオプションを無効にした場合、ファイルの復元中に USMT でエラーが発生すると、このステップはすぐに失敗します。 USMT は、すべてのファイルを復元しません。

#### <a name="enable-verbose-logging"></a>詳細ログ記録を有効にする

詳細なログ ファイル情報を生成するには、このオプションを有効にします。 状態を復元すると、タスク シーケンスは既定でタスク シーケンス ログ フォルダー `%WinDir%\ccm\logs` に **Loadstate.log** を生成します。  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a> コマンド ラインの実行

このステップでは、指定したコマンド ラインを実行します。  

実行するコマンドは、次の条件を満たす必要があります。  

- デスクトップと通信してはいけません。 コマンドは、サイレント モードまたは無人モードで実行する必要があります。  

- 自動的に再起動を開始させてはいけません。 コマンドは、標準再起動コードの 3010 を使用して再起動を要求する必要があります。 この動作により、タスク シーケンスは再起動を適切に処理するようになります。 コマンドから 3010 終了コードが返されると、タスク シーケンス エンジンによってコンピューターが再起動されます。 再起動後にタスク シーケンスは自動的に続行されます。

このステップは、完全な OS または Windows PE のいずれかで実行できます。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[コマンド ラインの実行]** を選びます。

### <a name="variables-for-run-command-line"></a>コマンド ラインの実行の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) (バージョン 1902 以降)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (バージョン 2002 以降)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>コマンド ラインの実行のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepruncommandline?view=sccm-ps)
- [New-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepruncommandline?view=sccm-ps)
- [Remove-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepruncommandline?view=sccm-ps)
- [Set-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepruncommandline?view=sccm-ps)

### <a name="properties-for-run-command-line"></a>コマンド ラインの実行のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="command-line"></a>コマンド ライン

タスク シーケンスが実行するコマンド ラインを指定します。 このフィールドは必須です。 .vbs や .exe などのファイル名拡張子も含めます。 必要な設定ファイルとコマンド ライン オプションをすべて含めます。  

ファイル名拡張子を指定しないと、.com、.exe、.bat が試されます。 ファイル名に拡張子が付いていても、それが実行可能ファイルの種類でない場合は、ローカルの関連付けが試されます。 たとえば、コマンド ラインが readme.gif の場合は、Configuration Manager では .gif ファイルを開くために対象のコンピューターで指定されたアプリケーションを起動します。  

例:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> 正常に実行するには、コマンド ライン アクションの前に **cmd.exe /c** コマンドを付加します。 このようなアクションの例は、出力のリダイレクト、パイプ処理、コピーなどのコマンドです。  

#### <a name="output-to-task-sequence-variable"></a>タスク シーケンス変数への出力

<!--user story 4977616/bug 4798352-->

バージョン 1910 以降では、コマンド出力をカスタム タスク シーケンス変数に保存します。

> [!Note]  
> Configuration Manager によって、この出力が最後の 1000 文字に制限されます。

#### <a name="disable-64-bit-file-system-redirection"></a>64 ビット ファイル システムのリダイレクトを無効にする

既定では、64 ビット オペレーティング システムは、WOW64 ファイル システム リダイレクターを使って、コマンド ラインを実行します。 この動作は、32 ビット バージョンの OS の実行可能ファイルとライブラリを正しくを検索するためです。 WOW64 ファイル システム リダイレクターの使用を無効にするには、このオプションを選びます。 Windows は、ネイティブの 64 ビット バージョンの OS の実行可能ファイルとライブラリを使って、コマンドを実行します。 32 ビット OS で実行している場合、このオプションによる影響はありません。  

#### <a name="start-in"></a>作業フォルダー

プログラムの実行可能フォルダーを 127 文字以内で指定します。 このフォルダーには、対象のコンピューターの絶対パスを指定することも、パッケージを含む配布ポイント フォルダーを基準としたパスを指定することもできます。 このフィールドは省略可能です。  

例:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> **[参照]** ボタンは、ローカル コンピューターでファイルとフォルダーを参照します。 選択するものはすべて、対象のコンピューターにも存在する必要があります。 同じ場所に、同じファイル名とフォルダー名で、存在する必要があります。  

#### <a name="package"></a>パッケージ

対象のコンピューターにまだ存在しないファイルまたはプログラムをコマンド ラインで指定する場合、このオプションを選択して必要なファイルを含む Configuration Manager パッケージを指定します。 パッケージにはプログラムは必要ありません。 指定するファイルが対象のコンピューターに存在する場合、このオプションは必要ありません。  

#### <a name="time-out"></a>タイムアウト

Configuration Manager で、コマンド ラインに許容される実行時間を表す値を指定します。 可能な値は 1 ～ 999 分です。 既定値は 15 分です。 既定では、このオプションは無効になっています。  

> [!IMPORTANT]  
> 指定したコマンドが正常に完了するのに十分な余裕のない時間値を入力すると、このステップは失敗します。 ステップまたはグループの状態によっては、タスク シーケンス全体が失敗する可能性があります。 タイムアウトに達すると、Configuration Manager はコマンド ライン プロセスを終了します。  

#### <a name="run-this-step-as-the-following-account"></a>このステップを次のアカウントで実行する

ローカル システム アカウント以外の Windows ユーザー アカウントとして実行されるコマンド ラインを指定します。  

> [!NOTE]  
> OS をインストールした後、別のアカウントで簡単なスクリプトまたはコマンドを実行するには、先にアカウントをコンピューターに追加します。 さらに、Windows インストーラーなどのより複雑なプログラムを実行するには、Windows ユーザー プロファイルを復元する必要があります。  

#### <a name="account"></a>アカウント

このステップでコマンド ラインを実行するために使う Windows ユーザー アカウントを指定します。 コマンド ラインは、指定されたアカウントのアクセス許可で実行します。 **[設定]** を選択して、ローカル ユーザーまたはドメイン アカウントを指定します。 タスク シーケンスの実行アカウントについて詳しくは、[アカウント](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)に関するページをご覧ください。

> [!IMPORTANT]  
> このステップでユーザー アカウントを指定し、Windows PE でステップを実行した場合、アクションは失敗します。 Windows PE をドメインに参加させることはできません。 このエラーは **smsts.log** ファイルに記録されます。  

### <a name="options-for-run-command-line"></a>コマンド ラインの実行のオプション

このタスク シーケンス ステップの **[オプション]** タブでは、既定のオプションだけでなく、以下の追加設定を構成します。  

#### <a name="success-codes"></a>成功コード

ステップで成功として評価する必要のある、スクリプトからの他の終了コードを指定します。



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> PowerShell スクリプトの実行

このステップでは、指定した Windows PowerShell スクリプトを実行します。  

スクリプトは次の条件を満たす必要があります。  

- デスクトップと通信してはいけません。 スクリプトは、サイレント モードまたは無人モードで実行する必要があります。  

- 自動的に再起動を開始させてはいけません。 スクリプトは、標準再起動コードの 3010 を使用して再起動を要求する必要があります。 この動作により、タスク シーケンスは再起動を適切に処理するようになります。 スクリプトから 3010 終了コードが返されると、タスク シーケンス エンジンによってコンピューターが再起動されます。 再起動後にタスク シーケンスは自動的に続行されます。

このステップは、完全な OS または Windows PE のいずれかで実行できます。 Windows PE でのこのステップを実行するには、ブート イメージで PowerShell を有効にします。 ブート イメージのプロパティの **[オプション コンポーネント]** タブで、WinPE-PowerShell コンポーネントを有効にします。 ブート イメージを変更する方法について詳しくは、「[Manage boot images](../get-started/manage-boot-images.md)」 (ブート イメージの管理) を参照してください。  

> [!NOTE]  
> PowerShell は、Windows Embedded オペレーティング システムでは既定では無効です。  

> [!WARNING]
> 特定のマルウェア対策ソフトウェアでは、Configuration Manager の PowerShell スクリプトの実行タスク シーケンス ステップに対してイベントが誤ってトリガーされることがあります。 %windir%\temp\smstspowershellscripts を除外することをお勧めします。これにより、マルウェア対策ソフトウェアで、これらのスクリプトを干渉なしで実行できます。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[PowerShell スクリプトの実行]** を選びます。

### <a name="variables-for-run-powershell-script"></a>PowerShell スクリプトの実行の変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters) (バージョン 1902 以降)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (バージョン 2002 以降)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>PowerShell スクリプトの実行のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteprunpowershellscript?view=sccm-ps)
- [New-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteprunpowershellscript?view=sccm-ps)
- [Remove-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript?view=sccm-ps)
- [Set-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteprunpowershellscript?view=sccm-ps)

> [!Note]  
> Unicode 形式の署名済みの PowerShell スクリプトを使用します。 このステップでは、既定の ANSI 形式では動作しません。

### <a name="properties-for-run-powershell-script"></a>PowerShell スクリプトの実行のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="package"></a>パッケージ

PowerShell スクリプトを含む Configuration Manager パッケージを指定します。 1 つのパッケージに複数の PowerShell スクリプトを含めることができます。  

#### <a name="script-name"></a>スクリプト名

実行する PowerShell スクリプトの名前を指定します。 このフィールドは必須です。  

#### <a name="enter-a-powershell-script"></a>PowerShell スクリプトの入力

<!-- 3556028 -->
バージョン 1902 以降では、このステップで Windows PowerShell コードを直接入力できるようになりました。 この機能により、最初にスクリプトを使用してパッケージを作成して配布しなくても、タスク シーケンス中に PowerShell コマンドを実行することができます。

スクリプトを追加または編集するときに、PowerShell スクリプト ウィンドウでは、次のアクションが提供されます。  

- スクリプトを直接編集する  

- ファイルから既存のスクリプトを開く  

- Configuration Manager で既存の承認された[スクリプト](../../apps/deploy-use/create-deploy-scripts.md)を参照する

> [!Important]  
> Configuration Manager のこの新機能を利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

#### <a name="parameters"></a>パラメーター

PowerShell スクリプトに渡すパラメーターを指定します。 これらのパラメーターは、コマンド ラインでの PowerShell スクリプトのパラメーターと同じです。  

Windows PowerShell のコマンド ラインで使用するパラメーターではなく、スクリプトで使用するパラメーターを指定します。  
次の例には、有効なパラメーターが含まれています。  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

次の例には、無効なパラメーターが含まれています。 最初の 2 つの項目は、Windows PowerShell のコマンド ライン パラメーターです ( **-NoLogo** と **-ExecutionPolicy Unrestricted**)。 スクリプトはこれらのパラメーターを使いません。  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
パラメーター値に特殊文字が含まれている場合は、一重引用符 (`'`) を使用して値を囲みます。 二重引用符 (`"`) を使用すると、タスク シーケンス ステップでパラメーターが適切に処理されなくなる場合があります。

例: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

バージョン 2002 以降では、このプロパティを変数に設定します。<!-- 5690481 --> たとえば、`%MyScriptVariable%` を指定した場合、タスク シーケンスでスクリプトが実行されるときに、このカスタム変数の値が PowerShell コマンド ラインに追加されます。

#### <a name="powershell-execution-policy"></a>PowerShell 実行ポリシー

コンピューターでの実行を許可する PowerShell スクリプト (ある場合) を決定します。 次のいずれかの実行ポリシーを選択します。  

- **AllSigned**: 信頼できる発行元によって署名されたスクリプトのみを実行します  

- **Undefined**: 実行ポリシーを何も定義しません  

- **Bypass**: すべての構成ファイルを読み込み、すべてのスクリプトを実行します。 未署名のスクリプトをインターネットからダウンロードする場合、Windows PowerShell はスクリプトを実行する前にアクセス許可を要求するメッセージを表示しません。  

> [!IMPORTANT]  
> PowerShell 1.0 では、Undefined および Bypass の実行ポリシーはサポートされていません。  

#### <a name="output-to-task-sequence-variable"></a>タスク シーケンス変数への出力

<!-- 3556028 -->
バージョン 1902 以降では、スクリプト出力をカスタム タスク シーケンス変数に保存します。

> [!Note]  
> バージョン 1910 以降では、Configuration Manager によって、この出力が最後の 1000 文字に制限されます。

このステップのプロパティを使用する方法の例については、[変数の設定方法](using-task-sequence-variables.md#bkmk_run-ps)に関する記事を参照してください。

#### <a name="start-in"></a>作業フォルダー

<!-- 3556028 -->
バージョン 1902 以降では、スクリプトの開始フォルダーを指定します (最大 127 文字)。 このフォルダーには、対象のコンピューターの絶対パスを指定することも、パッケージを含む配布ポイント フォルダーを基準としたパスを指定することもできます。 このフィールドは省略可能です。  

> [!NOTE]  
> **[参照]** ボタンは、ローカル コンピューターでファイルとフォルダーを参照します。 選択するものはすべて、対象のコンピューターにも存在する必要があります。 同じ場所に、同じファイル名とフォルダー名で、存在する必要があります。  

#### <a name="time-out"></a>タイムアウト

<!-- 3556028 -->
バージョン 1902 以降では、Configuration Manager が PowerShell スクリプトの実行を許可する期間を表す値を指定します。 可能な値は 1 ～ 999 分です。 既定値は 15 分です。 既定では、このオプションは無効になっています。  

> [!IMPORTANT]  
> 指定したスクリプトが正常に完了するのに十分な余裕のない時間値を入力すると、このステップは失敗します。 ステップまたはグループの状態によっては、タスク シーケンス全体が失敗する可能性があります。 タイムアウトに達すると、Configuration Manager は PowerShell プロセスを終了します。  

#### <a name="run-this-step-as-the-following-account"></a>このステップを次のアカウントで実行する

<!-- 3556028 -->
バージョン 1902 以降では、ローカル システム アカウント以外の Windows ユーザー アカウントとして実行される PowerShell スクリプトを指定します。  

> [!NOTE]  
> OS をインストールした後、別のアカウントで簡単なスクリプトまたはコマンドを実行するには、先にアカウントをコンピューターに追加します。 さらに、より複雑なプログラムを実行するには、Windows ユーザー プロファイルの復元が必要な場合があります。  

#### <a name="account"></a>アカウント

<!-- 3556028 -->
バージョン 1902 以降では、PowerShell スクリプトを実行するためにこのステップで使用する Windows ユーザー アカウントを指定します。 指定したアカウントは、システムのローカル管理者である必要があり、スクリプトはこのアカウントのアクセス許可で実行されます。 **[設定]** を選択して、ローカル ユーザーまたはドメイン アカウントを指定します。 タスク シーケンスの実行アカウントについて詳しくは、[アカウント](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)に関するページをご覧ください。

> [!IMPORTANT]  
> このステップでユーザー アカウントを指定し、Windows PE でステップを実行した場合、アクションは失敗します。 Windows PE をドメインに参加させることはできません。 このエラーは **smsts.log** ファイルに記録されます。  

### <a name="options-for-run-powershell-script"></a>PowerShell スクリプトの実行のオプション

このタスク シーケンス ステップの **[オプション]** タブでは、既定のオプションだけでなく、以下の追加設定を構成します。  

#### <a name="success-codes"></a>成功コード

<!-- 3556028 -->
バージョン 1902 以降では、ステップで成功として評価する必要のある、スクリプトからの他の終了コードを指定します。



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> タスク シーケンスの実行

> [!Note]  
> バージョン 1910 では、この機能は Configuration Manager で既定で有効となっています。 バージョン 1906 以前の場合、Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にします。 詳細については、「[Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。

このステップは別のタスク シーケンスを実行します。 これによりタスク シーケンス間に親子のリレーションシップが作成されます。 子タスク シーケンスを使うと、よりモジュール性の高い、再利用可能なタスク シーケンスを作成できます。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[タスク シーケンスの実行]** を選びます。

### <a name="specifications-and-limitations-for-run-task-sequence"></a>タスク シーケンスの実行の仕様と制限事項

タスク シーケンスに子タスク シーケンスを追加する場合は、以下の点を考慮してください。  

- 親と子のタスク シーケンスが、クライアントが実行する 1 つのポリシーに効率的に結合されていること。  

- 環境がグローバルであること。 親タスク シーケンスが変数を設定し、子タスク シーケンスがその変数を変更し場合は、最新の値が保持されます。 子タスク シーケンスが新しい変数を作成した場合、それ以降の親タスク シーケンスはその変数を使うことができます。  

- ステータス メッセージは、通常どおり 1 つのタスク シーケンス操作で複数送信されること。  

- タスク シーケンスは、エントリを **smsts.log** ファイルに書き込み、新しいログ エントリによって子タスク シーケンスの開始タイミングを明確にするということ。  

<!--the following points are from SCCMdocs issue #1079-->

- ブート イメージの参照があるタスク シーケンスを選択することはできません。 ブート イメージを必要とするすべての展開に対し、親タスク シーケンスでそれを指定します。  

- 子タスク シーケンスが無効になっていると、展開は失敗します。 **[エラーがあっても続行する]** オプションを使用してこの制限を回避することはできません。  

- 子タスク シーケンスに*影響が大きい*と見なされるステップが含まれている場合、ソフトウェア センターではそれが検出されず、影響が大きいという通知が表示されます。 [ユーザー通知] タブで親タスク シーケンスのプロパティを変更し、 **[これは、インパクトのあるタスク シーケンスです]** を指定します。  

- 子タスク シーケンスにパッケージ参照が不足している場合、親タスク シーケンスを表示すると、この状態が検出されません。 親タスク シーケンスを編集すると、親に変更を行ったときに、子タスク シーケンス内で不足しているすべての参照が検出されます。  

### <a name="cmdlets-for-run-task-sequence"></a>タスク シーケンスの実行のコマンドレット

バージョン 1906 以降では、次の PowerShell コマンドレットを使用してこのステップを管理します。<!-- 2839943, SCCMDocs#1118 -->

- **Get-CMTSStepRunTaskSequence**
- **New-CMTSStepRunTaskSequence**
- **Remove-CMTSStepRunTaskSequence**
- **Set-CMTSStepRunTaskSequence**

詳細については、[1906 リリース ノートの新しいコマンドレット](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps#new-cmdlets)に関する記事をご覧ください。

### <a name="properties-for-run-task-sequence"></a>タスク シーケンスの実行のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="select-task-sequence-to-run"></a>実行するタスク シーケンスの選択

**[参照]** を選択して子タスク シーケンスを選択します。 **[タスク シーケンスの選択]** ダイアログ ボックスでは、親タスク シーケンスは表示されません。



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> 動的変数の設定

このステップでは、次のアクションを実行します。  

1. コンピューターとその環境から情報が収集されます。 その後、指定したタスク シーケンス変数に情報が設定されます。  

2. 定義されている規則が評価されます。 true と評価された規則に基づいて、タスク シーケンス変数が設定されます。  

このステップは、完全な OS または Windows PE のいずれかで実行できます。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[動的変数の設定]** を選びます。

### <a name="variables-for-set-dynamic-variables"></a>動的変数の設定の変数

タスク シーケンスによって、次の読み取り専用のタスク シーケンス変数が自動的に設定されます。  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>動的変数の設定のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable?view=sccm-ps)
- [New-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Remove-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Set-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable?view=sccm-ps)

### <a name="properties-for-set-dynamic-variables"></a>動的変数の設定のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="dynamic-rules-and-variables"></a>動的規則と変数

タスク シーケンスで使うための動的変数を設定するには、規則を追加します。 その後、規則で指定されている各変数に値を設定します。 さらに、規則を追加せずに、1 つまたは複数の変数を追加します。 規則を追加するときは、次のカテゴリから選びます。  

- **コンピューター**: ハードウェア資産タグ、UUID、シリアル番号、または MAC アドレスの値を評価します。 必要に応じて、複数の値を設定します。 いずれかの値が true の場合、その規則は true と評価されます。 たとえば、デバイスのシリアル番号が 5892087 で MAC アドレスが 22-A4-5A-13-78-26 の場合、次の規則は true と評価されます。  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **場所**: 既定のネットワーク ゲートウェイの値を評価します。  

- **製造元およびモデル**: コンピューターの製造元およびモデルの値を評価します。 規則を true と評価するには、製造元とモデルの両方が true と評価される必要があります。

    ワイルドカード文字としてアスタリスク (`*`) と疑問符 (`?`) を指定します。 アスタリスクは複数の文字と一致し、疑問符は 1 つの文字と一致します。 たとえば、文字列 `DELL*900?` は `DELL-ABC-9001` と `DELL9009` の両方と一致します。  

- **タスク シーケンス変数**: 評価するタスク シーケンス変数、条件、および値を追加します。 変数に設定された値が指定した条件を満たしている場合、規則は true と評価されます。  

    true と評価される規則に対して設定する 1 つ以上の変数を指定するか、規則を使わずに変数を設定します。 既存の変数を選ぶか、カスタム変数を作成します。  

    - **既存のタスク シーケンス変数**: 既存のタスク シーケンス変数の一覧から 1 つまたは複数の変数を選びます。 配列変数は選択できません。  

    - **カスタム タスク シーケンス変数**: カスタム タスク シーケンス変数を定義します。 既存のタスク シーケンス変数を指定することもできます。 この設定は、変数の配列は既存のタスク シーケンス変数の一覧に含まれないため、**OSDAdapter** などの既存の変数配列を指定する場合に便利です。  

規則に変数を選択した後、各変数の値を指定します。 規則が true と評価されると、変数は指定された値に設定されます。 変数ごとに **[秘密の値]** を選択して変数の値を非表示にできます。 既定では、**OSDCaptureAccountPassword** 変数など、いくつかの既存の変数の値を非表示にします。  

> [!IMPORTANT]  
> Configuration Manager は、**動的変数の設定**ステップでタスク シーケンスをインポートするとき、**シークレット値**としてマークされているすべての変数値を削除します。 タスク シーケンスをインポートした後で、動的変数の値を再入力します。  



## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> タスク シーケンス変数の設定

このステップでは、タスク シーケンスで使われる変数の値を設定します。  

このステップは、完全な OS または Windows PE のいずれかで実行できます。

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[全般]** を選んで、 **[タスク シーケンス変数の設定]** を選びます。

### <a name="variables-for-set-task-sequence-variable"></a>タスク シーケンス変数の設定の変数

タスク シーケンス変数はタスク シーケンス アクションによって読み取られます。また、これらのアクションの動作はタスク シーケンス変数によって指定されます。 特定のタスク シーケンス変数とその使用方法について詳しくは、次の記事をご覧ください。  

- [タスク シーケンス変数の使用方法](using-task-sequence-variables.md)  
- [タスク シーケンス変数](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>タスク シーケンス変数の設定のコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetvariable?view=sccm-ps)
- [New-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetvariable?view=sccm-ps)
- [Remove-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetvariable?view=sccm-ps)
- [Set-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetvariable?view=sccm-ps)

### <a name="properties-for-set-task-sequence-variable"></a>タスク シーケンス変数の設定のプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="task-sequence-variable"></a>タスク シーケンス変数

タスク シーケンスの組み込み変数またはアクション変数の名前を指定するか、独自のユーザー定義変数の名前を指定します。  

#### <a name="do-not-display-this-value"></a>この値を表示しない

<!--1358330-->
このオプションを有効にすると、タスク シーケンス変数に格納される機密データがマスクされます。 たとえば、パスワードを指定するときに使用します。

> [!Note]  
> このオプションを有効にしてから、タスク シーケンス変数の値を設定します。 そうしないと、変数の値が意図したとおりに設定されず、タスク シーケンスを実行したときに予期しない動作を引き起こす可能性があります。<!--SCCMdocs issue #800-->

#### <a name="value"></a>値  

タスク シーケンスは、変数をこの値に設定します。 このタスク シーケンス変数を別のタスク シーケンス変数の値に設定するには、`%varname%` という構文を使います。  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Windows と ConfigMgr のセットアップ

このステップでは、Windows PE から新しい OS への移行を実行します。 このタスク シーケンス ステップはあらゆる OS 展開に必要です。 このステップでは、Configuration Manager クライアントを新しい OS にインストールして、新しい OS でタスク シーケンスの実行を継続できるようにします。  

このステップでは、タスク シーケンスを Windows PE から完全な OS に移行します。 この移行により、Windows PE と完全な OS の両方でステップが実行されます。 ただし、移行は Windows PE で開始されるため、これはタスク シーケンスの Windows PE 部分の間にのみ追加できます。  

このステップでは、sysprep.inf または unattend.xml のディレクトリ変数 (`%WINDIR%` や `%ProgramFiles%` など) が、Windows PE のインストール ディレクトリ `X:\Windows` に置き換えられます。 タスク シーケンスは、これらの環境変数を使って指定されている変数を無視します。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[イメージ]** を選んで、 **[Windows と ConfigMgr のセットアップ]** を選びます。

### <a name="behaviors-for-setup-windows-and-configmgr"></a>Windows と ConfigMgr のセットアップの動作

このステップでは次のアクションを実行します。  

#### <a name="preliminaries-windows-pe"></a>準備: Windows PE  

1. unattend.xml ファイルのタスク シーケンス変数を置換します。  

2. Configuration Manager クライアントを含むパッケージをダウンロードします。 展開されるイメージにパッケージを追加します。  

#### <a name="set-up-windows"></a>Windows の設定  

- イメージ ベースのインストール  

    1. イメージで Configuration Manager クライアントを無効にします (存在する場合)。 つまり、Configuration Manager クライアント サービスの自動開始を無効にします。  

    2. 展開されるイメージのレジストリを更新して、展開される OS が、参照コンピューターと同じドライブ文字で起動されるようにします。  

    3. 展開された OS を再起動します。  

    4. 前に指定した sysprep.inf または unattend.xml 応答ファイルを使って、Windows ミニセットアップが実行されます。このとき、エンド ユーザーの操作はすべて抑制されます。 **[ネットワーク設定の適用]** ステップを使ってドメインに参加する場合、その情報は応答ファイル内にあります。 Windows ミニセットアップがドメインにコンピューターを参加させます。  

- Setup.exe ベースのインストール。 通常の Windows セットアップ プロセスに続く Setup.exe を実行します。  

    1. **[オペレーティング システムの適用]** ステップで指定されている OS アップグレード パッケージを、ハード ディスク ドライブにコピーします。  

    2. 新しく展開された OS を再起動します。  

    3. 前に指定した sysprep.inf または unattend.xml 応答ファイルを使って、Windows ミニセットアップが実行されます。このとき、ユーザーのインターフェイス設定はすべて抑制されます。 **[ネットワーク設定の適用]** ステップを使ってドメインに参加する場合、その情報は応答ファイル内にあります。 Windows ミニセットアップがドメインにコンピューターを参加させます。  

#### <a name="set-up-the-configuration-manager-client"></a>Configuration Manager クライアントの設定  

1. Windows ミニセットアップが完了すると、setupcomplete.cmd を使用して、タスク シーケンスが再開されます。 詳細については、「[セットアップの完了後にスクリプトを実行する (SetupComplete.cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd)」をご覧ください。  

2. **Windows 設定の適用**ステップで選んだオプションに応じて、ローカルの管理者アカウントが有効または無効になります。  

3. 前にダウンロードしたパッケージとこのステップで指定したインストール プロパティを使って、Configuration Manager クライアントがインストールされます。 クライアントは、"プロビジョニング モード" でインストールされます。 このモードでは、タスク シーケンスが完了するまで、クライアントは新しいポリシー要求を処理しません。 詳細については、「[Provisioning mode (プロビジョニング モード)](provisioning-mode.md)」を参照してください。  

4. クライアントが完全に動作可能な状態になるまで待ちます。  

#### <a name="the-step-completes"></a>ステップが完了する

タスク シーケンスは次のステップの実行を続けます。  

> [!Note]  
> Windows グループ ポリシーは通常、タスク シーケンスが完了するまで処理を行いません。 この動作は、Windows のさまざまなバージョンで一貫しています。 タスク シーケンス中に他のカスタム アクションは、グループ ポリシーの評価をトリガーできます。 操作の順序について詳しくは、「[セットアップの完了後にスクリプトを実行する (SetupComplete.cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd)」をご覧ください。 <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>Windows と ConfigMgr のセットアップの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>Windows と ConfigMgr のセットアップのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [New-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Set-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)

### <a name="properties-for-setup-windows-and-configmgr"></a>Windows と ConfigMgr のセットアップのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="client-package"></a>クライアント パッケージ

**[参照]** を選択し、このステップで使う Configuration Manager クライアント インストール パッケージを選びます。  

#### <a name="use-pre-production-client-package-when-available"></a>使用可能な場合に実稼働前クライアント パッケージを使用する

使用可能な実稼働前クライアント パッケージがあり、コンピューターがパイロット コレクションのメンバーである場合、タスク シーケンスは実稼働クライアント パッケージではなく、このパッケージを使います。 実稼働前クライアントは、実稼働環境でのテスト用の新しいバージョンです。 **[参照]** を選択し、このステップで使う実稼働前クライアント インストール パッケージを選びます。  

#### <a name="installation-properties"></a>インストールのプロパティ

タスク シーケンスのステップでは、サイトの割り当てと既定の構成が自動的に指定されます。 このフィールドを使用して、クライアントのインストール時に使用する追加のインストールのプロパティを指定します。 複数のインストールのプロパティを入力するには、各プロパティの間にスペースを入力します。  

クライアントのインストール時に使用するコマンド ライン オプションを指定します。 たとえば、「`/skipprereq: silverlight.exe`」と入力すると、CCMSetup.exe に Microsoft Silverlight 前提条件をインストールしないように通知します。 CCMSetup.exe の使用可能なコマンド ライン オプションの詳細については、「[クライアント インストールのプロパティについて](../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

### <a name="options-for-setup-windows-and-configmgr"></a>Windows と ConfigMgr のセットアップのオプション

> [!NOTE]  
> **[オプション]** タブで **[エラー時に続行する]** を有効にしないでください。このステップの間にエラーが発生した場合は、この設定が有効かどうかにかかわらず、タスク シーケンスは失敗します。  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> オペレーティング システムのアップグレード

このステップでは、古いバージョンの Windows を新しいバージョンの Windows 10 にアップグレードします。  

このタスク シーケンス ステップは完全な OS でのみ実行されます。 Windows PE では実行されません。  

タスク シーケンス エディターでこのステップを追加するには、 **[追加]** を選び、 **[イメージ]** を選んで、 **[オペレーティング システムのアップグレード]** を選びます。

> [!TIP]
> Windows 10 バージョン 1709 以降では、メディアに複数のエディションが含まれます。 タスク シーケンスが OS アップグレード パッケージまたは OS イメージを使うように構成するときは、[サポートされているエディション](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)を必ず選んでください。  
>
> ユーザーがタスク シーケンスをインストールする前に、コンテンツの事前キャッシュを使用して該当する OS アップグレード パッケージをダウンロードします。 詳細については、「[コンテンツの事前キャッシュを構成する](../deploy-use/configure-precache-content.md)」を参照してください。

### <a name="variables-for-upgrade-os"></a>OS のアップグレードの変数

このステップでは、次のタスク シーケンス変数を使用します。  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>OS のアップグレードのコマンドレット

次の PowerShell コマンドレットを使用して、このステップを管理します。<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [New-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Remove-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Set-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem?view=sccm-ps)

### <a name="properties-for-upgrade-os"></a>OS のアップグレードのプロパティ

このステップの **[プロパティ]** タブでは、このセクションで説明する設定を構成します。  

#### <a name="upgrade-package"></a>パッケージのアップグレード

アップグレードに使用する Windows 10 OS アップグレード パッケージを指定するには、このオプションを選択します。  

#### <a name="source-path"></a>ソース パス

Windows セットアップが使う Windows 10 メディアへのローカル パスまたはネットワーク パスを指定します。 この設定は、Windows セットアップのコマンド ライン オプション `/InstallFrom` に対応します。

`%MyContentPath%`、`%DPC01%` などの変数を指定することもできます。 ソース パスに変数を使用する場合は、タスク シーケンスの早い段階でその変数を設定しておきます。 たとえば、[パッケージ コンテンツのダウンロード](#BKMK_DownloadPackageContent) ステップを使用して、OS アップグレード パッケージの場所に対する変数を指定します。 その後、このステップのソース パスに変数を使用します。  

#### <a name="edition"></a>エディション

アップグレードに使用する OS メディア内のエディションを指定します。  

#### <a name="product-key"></a>プロダクト キー

アップグレード プロセスに適用するプロダクト キーを指定します。  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>アップグレードの際に、Windows セットアップに次のドライバー コンテンツを指定してください

アップグレード プロセスの間に、対象コンピューターにドライバーを追加します。 ドライバーは、Windows 10 と互換性がある必要があります。 この設定は、Windows セットアップのコマンド ライン オプション `/InstallDriver` に対応します。 詳細については、「[Windows セットアップ コマンド ライン オプション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers)」を参照してください。

次のいずれかのオプションを指定します。  

- **ドライバー パッケージ**: **[参照]** を選択し、一覧から既存のドライバー パッケージを選択します。

- **ステージング済みコンテンツ**: ドライバー コンテンツの場所を指定するには、このオプションを選択します。 ローカル フォルダー、ネットワーク パス、またはタスク シーケンス変数を指定できます。 ソース パスに変数を使用する場合は、タスク シーケンスの早い段階でその変数を設定しておきます。 たとえば、[パッケージ コンテンツのダウンロード](task-sequence-steps.md#BKMK_DownloadPackageContent) ステップを使用します。  

> [!TIP]
> 複数の種類のハードウェアに動的なコンテンツを使用する場合は、次のようにします。
>
> - このステップの複数のインスタンスを、ハードウェアの種類と個別のドライバー コンテンツの条件と共に使用します。
>
> - [パッケージ コンテンツのダウンロード](task-sequence-steps.md#BKMK_DownloadPackageContent) ステップの複数のインスタンスを使用します。 コンテンツを共通の場所に配置し、 **[ステージング済み コンテンツ]** オプションを使用します。 この方法の利点は、タスク シーケンスの **OS のアップグレード** ステップが 1 つであることです。

#### <a name="time-out-minutes"></a>タイムアウト (分)

Configuration Manager がこのステップを失敗とするまでの分数を指定します。 このオプションは、Windows セットアップが処理を停止しても終了はしない場合に便利です。  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>アップグレードを開始しない Windows セットアップ互換性スキャンの実行

アップグレード プロセスを開始せずに、Windows セットアップの互換性スキャンを実行します。 この設定は、Windows セットアップのコマンド ライン オプション `/Compat ScanOnly` に対応します。 このオプションを使用して OS アップグレード パッケージ全体を展開します。

<!--SCCMDocs-pr issue 2812-->
このオプションを有効にすると、このステップで Configuration Manager クライアントがプロビジョニング モードになりません。 Windows セットアップはバックグラウンドでサイレントに実行し、クライアントは引き続き通常どおり機能します。 詳細については、「[Provisioning mode](provisioning-mode.md)」 (プロビジョニング モード) を参照してください。

セットアップでは、スキャンの結果として終了コードが返されます。 次の表に一般的な終了コードをいくつか示します。  

|終了コード|詳細|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|互換性の問題なし ("成功")。|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|対応可能な互換性の問題。|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|選択された移行オプションが使用できない。 Enterprise から Professional へのアップグレードなど。|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Windows 10 に適合しない。|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|ディスクの空き領域が不足している。|  

このパラメーターについて詳しくは、「[Windows Setup Command-Line Options](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat)」(Windows セットアップ コマンド ライン オプション) をご覧ください。  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>互換性に関するメッセージが無視できる場合、すべて無視する

無視できる互換性に関するメッセージをすべて無視して、セットアップがインストールを完了するように指定します。 この設定は、Windows セットアップのコマンド ライン オプション `/Compat IgnoreWarning` に対応します。  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Windows Update で Windows セットアップを動的に更新する

検索、ダウンロード、更新プログラムのインストールなどの動的な更新操作をセットアップが実行できるようにします。 この設定は、Windows セットアップのコマンド ライン オプション `/DynamicUpdate` に対応します。 この設定は、Configuration Manager のソフトウェア更新プログラムと互換性がありません。 スタンドアロンの Windows Server Update Services (WSUS) または Windows Update for Business で更新プログラムを管理する場合は、このオプションを有効にします。  

#### <a name="override-policy-and-use-default-microsoft-update"></a>ポリシーをオーバーライドして既定の Microsoft Update を使う

リアルタイムで一時的にローカル ポリシーをオーバーライドし、動的更新操作を実行します。 コンピューターは、Windows Update から更新されます。
