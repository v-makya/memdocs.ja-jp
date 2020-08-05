---
title: 自動操縦デプロイのデモンストレーション
ms.reviewer: ''
manager: laurawi
description: Windows 自動操縦展開を使用して仮想マシンをセットアップする手順について説明します。
keywords: mdm、セットアップ、windows、windows 10、oobe、管理、展開、自動操縦、ztd、ゼロタッチ、パートナー、msfb、intune、アップグレード
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom: autopilot
ms.openlocfilehash: 7ff25816c0398389fc23bbde4983f4bc9556d192
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757756"
---
# <a name="demonstrate-autopilot-deployment"></a>自動操縦デプロイのデモンストレーション

**適用対象**

- Windows 10

Windows 自動操縦を開始するには、仮想マシン (VM) を使用して試してみるか、ワイプされる物理デバイスを使用して Windows 10 を新規にインストールする必要があります。

このトピックでは、Hyper-v を使用して VM の Windows 自動操縦の展開をセットアップする方法について説明します。

> [!NOTE]
> 自動操縦を可能にする[複数のプラットフォーム](add-devices.md#registering-devices)がありますが、このラボでは主に Intune を使用します。

> Hyper-v と VM は、このラボには必要ありません。 物理デバイスを使用することもできます。 ただし、この手順では、VM を使用していることを前提としています。 物理デバイスを使用するには、Hyper-v をインストールして VM を作成する手順をスキップします。 ガイド内の "デバイス" へのすべての参照は、クライアントデバイス (物理または仮想) を参照します。

次のビデオでは、プロセスの概要を説明します。

</br>
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/KYVptkpsOqs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

> このガイドで使用されている用語の一覧については、「[用語集](#glossary)」を参照してください。

## <a name="prerequisites"></a>前提条件

このラボを完成させるために必要なものは次のとおりです。
<table><tr><td>Windows 10 のインストールメディア</td><td>サポートされているバージョンの Windows 10 (半期チャネル) 用の windows 10 Professional または Enterprise (ISO ファイル)。 ISO をまだ使用していない場合は、 <a href="https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise" data-raw-source="[evaluation version of Windows 10 Enterprise](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)">Windows 10 Enterprise の評価版</a>をダウンロードするためのリンクが用意されています。</td></tr>
<tr><td>インターネットへのアクセス</td><td>ファイアウォールの内側にいる場合は、詳細な<a href="windows-autopilot-requirements.md#networking-requirements" data-raw-source="[networking requirements](windows-autopilot-requirements.md#networking-requirements)">ネットワーク要件</a>を参照してください。 それ以外の場合は、インターネットに接続していることを確認してください。</td></tr>
<tr><td>Hyper-v または Windows 10 を実行する物理デバイス</td><td>このガイドでは、Hyper-v VM を使用することを前提としており、必要に応じて Hyper-v をインストールして構成する手順について説明します。 物理デバイスを使用するには、Hyper-v をインストールして構成する手順をスキップします。</td></tr>
<tr><td>Premium Intune アカウント</td><td>このガイドでは、30日間無料試用版 premium アカウントを入手して、ラボを完成させる方法について説明します。</td></tr></table>

## <a name="procedures"></a>手順

ラボのセクションと手順の概要については、以下を参照してください。 記載されている順序で各セクションに従い、適用されないセクションはスキップします。 省略可能な手順については、付録をご紹介します。

[Hyper-v のサポートを確認する](#verify-support-for-hyper-v)
<br>[Hyper-V の有効化](#enable-hyper-v)
<br>[デモ VM の作成](#create-a-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[ISO ファイルの場所の設定](#set-iso-file-location)
<br>&nbsp;&nbsp;&nbsp;[ネットワークアダプター名の確認](#determine-network-adapter-name)
<br>&nbsp;&nbsp;&nbsp;  [Windows PowerShell を使用してデモ VM を作成する](#use-windows-powershell-to-create-the-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[Windows 10 をインストール](#install-windows-10)する
<br>[ハードウェア ID をキャプチャする](#capture-the-hardware-id)
<br>[VM を既定のエクスペリエンス (OOBE) に戻します。](#reset-the-vm-back-to-out-of-box-experience-oobe)
<br>[サブスクリプションレベルの確認](#verify-subscription-level)
<br>[会社のブランドの構成](#configure-company-branding)
<br>[Microsoft Intune の自動登録を構成する](#configure-microsoft-intune-auto-enrollment)
<br>[VM を登録する](#register-your-vm)
<br>&nbsp;&nbsp;&nbsp;[Intune を使用した自動操縦登録](#autopilot-registration-using-intune)
<br>&nbsp;&nbsp;&nbsp;[MSfB を使用した自動操縦登録](#autopilot-registration-using-msfb)
<br>[Windows 自動操縦展開プロファイルを作成して割り当てる](#create-and-assign-a-windows-autopilot-deployment-profile)
<br>&nbsp;&nbsp;&nbsp;[Intune を使用して Windows 自動操縦展開プロファイルを作成する](#create-a-windows-autopilot-deployment-profile-using-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[プロファイルを割り当てる](#assign-the-profile)
<br>&nbsp;&nbsp;&nbsp;[MSfB を使用して Windows 自動操縦展開プロファイルを作成](#create-a-windows-autopilot-deployment-profile-using-msfb)する
<br>[「Windows 自動操縦の動作」を参照してください。](#see-windows-autopilot-in-action)
<br>[自動操縦からデバイスを削除する](#remove-devices-from-autopilot)
<br>&nbsp;&nbsp;&nbsp;[自動操縦用デバイスの削除 (登録解除)](#delete-deregister-autopilot-device)
<br>[付録 A: Hyper-v のサポートを確認する](#appendix-a-verify-support-for-hyper-v)
<br>[付録 B: プロファイルへのアプリの追加](#appendix-b-adding-apps-to-your-profile)
<br>&nbsp;&nbsp;&nbsp;[Win32 アプリを追加する](#add-a-win32-app)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Intune 用にアプリを準備](#prepare-the-app-for-intune)する
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Intune でアプリを作成する](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Intune プロファイルにアプリを割り当てる](#assign-the-app-to-your-intune-profile)
<br>&nbsp;&nbsp;&nbsp;[Office 365 の追加](#add-office-365)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Intune でアプリを作成する](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Intune プロファイルにアプリを割り当てる](#assign-the-app-to-your-intune-profile)
<br>[用語集](#glossary)

## <a name="verify-support-for-hyper-v"></a>Hyper-v のサポートを確認する

Hyper-v をまだ所有していない場合は、まず、Windows 10 または Windows Server (2012 R2 以降) を実行しているコンピューターでこれを有効にする必要があります。

> 既に Hyper-v が有効になっている場合は、[デモ VM の作成](#create-a-demo-vm)手順に進みます。 VM ではなく物理デバイスを使用している場合は、「 [Windows 10 のインストール](#install-windows-10)」に進みます。

デバイスで Hyper-v がサポートされていることが確認できない場合、または hyper-v のインストールに問題がある場合は、次の[付録 a](#appendix-a-verify-support-for-hyper-v)を参照してください。 hyper-v が正常にインストールされていることの確認についての詳細が記載されています。

## <a name="enable-hyper-v"></a>Hyper-V の有効化

Hyper-v を有効にするには、管理者特権の Windows PowerShell プロンプトを開き、次のコマンドを実行します。

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

このコマンドは、Hyper-v をサポートするすべてのオペレーティングシステムで動作しますが、Windows Server オペレーティングシステムでは、追加のコマンド (下記) を入力して、Hyper-v Windows PowerShell モジュールと Hyper-v マネージャーコンソールを追加する必要があります。 次のコマンドは、Hyper-v がまだインストールされていない場合にもインストールします。そのため、Windows Server を使用している場合は、WindowsOptionalFeature コマンドを使用する代わりに、次のコマンドを入力するだけで済みます。

```powershell
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools
```

コンピューターを再起動するよう求めるメッセージが表示されたら、**はい**を選択します。 コンピューターは複数回再起動する場合があります。

> または、以下に示すように、クライアントのオペレーティング システムの **[Windows の機能の有効化または無効化]** で Windows のコントロール パネルを使用するか、サーバーのオペレーティング システム上でサーバー マネージャーの **[役割と機能の追加ウィザード]** を使用して Hyper-V をインストールすることができます。

   ![Hyper-v の機能](images/hyper-v-feature.png)

   ![Hyper-V](images/svr_mgr2.png)

<P>サーバー マネージャーを使用して Hyper-V インストールする場合、既定の選択項目をすべてそのまま使用してください。 また、<strong>Role Administration Tools\Hyper-V Management Tools</strong> の下の両方の項目をインストールしてください。

インストールが完了したら、管理者特権のコマンドプロンプトで「 **virtmgmt** 」と入力するか、[スタート] メニューの検索ボックスに「 **hyper-v** 」と入力して、hyper-v マネージャーを開きます。

Hyper-v の詳細については、「windows [10 の hyper-v の概要](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/)」および「 [windows Server での](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)hyper-v」を参照してください。

## <a name="create-a-demo-vm"></a>デモ VM の作成

Hyper-v が有効になったので、Windows 10 を実行する VM を作成する必要があります。 Hyper-v マネージャーを使用して VM と[仮想ネットワーク](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)[を作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine)できますが、Windows PowerShell を使用する方が簡単です。

Windows PowerShell を使用するには、次の2つの点を知る必要があります。

1. Windows 10 ISO ファイルの場所。
   - この例では、場所が**c:\**であることを前提としています。
2. インターネットに接続するネットワークインターフェイスの名前。
   - この例では、Windows PowerShell コマンドを使用して、これを自動的に決定します。

ISO ファイルの場所を設定し、適切なネットワークインターフェイスの名前を決定したら、Windows 10 をインストールできます。

### <a name="set-iso-file-location"></a>ISO ファイルの場所の設定

Windows 10 Enterprise の最新リリースの評価版については、ISO ファイルを[こちら](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)からダウンロードできます。
- プラットフォームの選択を求められたら、 **64 ビット**を選択します。

このファイルをダウンロードすると、名前が非常に長くなります (例: 17763.107.101029-rs5_release_svc_refresh_CLIENTENTERPRISEEVAL_OEMRET_x64FRE_en 1455)。

1. 簡単に入力して覚えやすいように、ファイルの名前を**win10-eval**に変更します。
2. コンピューター上に**c:\ iso**という名前のディレクトリを作成し、 **win10-eval**ファイルを移動します。そのため、ファイルへのパスは**c:\. iso**になります。
3. ファイルに別の名前と場所を使用する場合は、以下の Windows PowerShell コマンドを変更して、カスタムの名前とディレクトリを使用する必要があります。

### <a name="determine-network-adapter-name"></a>ネットワークアダプター名の確認

次に、NetAdaper コマンドレットを使用して、インターネットへの接続に使用する可能性が最も高いネットワークアダプターを自動的に検出します。 管理者特権の Windows PowerShell プロンプトで次のコマンドを実行して、このコマンドを最初にテストする必要があります。

```powershell
(Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
```

このコマンドの出力は、インターネットへの接続に使用するネットワークインターフェイスの名前にする必要があります。 これが正しいインターフェイス名であることを確認してください。 正しいインターフェイス名でない場合は、以下の最初のコマンドを編集して、ネットワークインターフェイス名を使用する必要があります。

たとえば、上のコマンドでイーサネットが表示されていても、Ethernet2 を使用する場合、次の最初のコマンドは AutopilotExternal-AllowManagementOS $true-NetAdapterName **Ethernet2**になります。

### <a name="use-windows-powershell-to-create-the-demo-vm"></a>Windows PowerShell を使用してデモ VM を作成する

すべての VM データは、PowerShell プロンプトで現在のパスの下に作成されます。 次のコマンドを実行する前に、新しいフォルダーに移動することを検討してください。

> [!IMPORTANT]
> **Vm スイッチ**: vm スイッチは、Hyper-v が vm をネットワークに接続する方法です。 <br><br>以前に Hyper-v を有効にしており、インターネットに接続されたネットワークインターフェイスが既に VM スイッチにバインドされている場合、以下の PowerShell コマンドは失敗します。 この場合は、既存の VM スイッチを削除して (以下のコマンドで作成できます)、この VM スイッチを再利用することができます。次のコマンドをスキップし、2番目のコマンドを変更してスイッチ名**AutopilotExternal**をスイッチの名前に置き換えるか、既存のスイッチの名前を "AutopilotExternal" に変更します。<br><br>これまでに外部 VM スイッチを作成したことがない場合は、次のコマンドを実行します。

```powershell
New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal
Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
Start-VM -VMName WindowsAutopilot
```

これらのコマンドを入力したら、先ほど作成した VM に接続し、キーを押して DVD からブートするように求めるプロンプトが表示されるまで待ちます。  VM に接続するには、Hyper-v マネージャーでダブルクリックします。

次のサンプル出力を参照してください。 このサンプルでは、VM は**c:\ 自動**ディレクトリに作成され、vmconnect.exe コマンドが使用されます (Windows Server でのみ使用できます)。 Windows 10 に Hyper-v をインストールした場合は、Hyper-v マネージャーを使用して VM に接続します。

<pre style="overflow-y: visible">
PS C:\autopilot&gt; dir c:\iso


    Directory: C:\iso


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/12/2019   2:46 PM     4627343360 win10-eval.iso

PS C:\autopilot&gt; (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name
Ethernet
PS C:\autopilot&gt; New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name

Name              SwitchType NetAdapterInterfaceDescription
----              ---------- ------------------------------
AutopilotExternal External   Intel(R) Ethernet Connection (2) I218-LM

PS C:\autopilot&gt; New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal

Name             State CPUUsage(%) MemoryAssigned(M) Uptime   Status             Version
----             ----- ----------- ----------------- ------   ------             -------
WindowsAutopilot Off   0           0                 00:00:00 Operating normally 8.0

PS C:\autopilot&gt; Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
PS C:\autopilot&gt; Start-VM -VMName WindowsAutopilot
PS C:\autopilot&gt; vmconnect.exe localhost WindowsAutopilot
PS C:\autopilot&gt; dir

    Directory: C:\autopilot

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/12/2019   3:15 PM                VMData
d-----        3/12/2019   3:42 PM                VMs

PS C:\autopilot&gt;
</pre>

### <a name="install-windows-10"></a>Windows 10 をインストールする

VM がインストール ISO からブートされていることを確認し、[**次へ**]、[**今すぐインストール**] の順にクリックして、Windows のインストールプロセスを完了します。 次の例を参照してください。

   ![Windows セットアップ ](images/winsetup1.png) ![ windows セットアップ ](images/winsetup2.png) ![ windows セットアップ ](images/winsetup3.png) ![ ](images/winsetup4.png) ![ ](images/winsetup5.png) windows セットアップ windows ![ セットアップ windows セットアップ](images/winsetup6.png)

VM が再起動された後、OOBE 中に [**個人用に設定**] または [ドメインへの**参加**] を選択して、**サインイン**画面でオフラインアカウントを選択してもかまいません。  これにより、デスクトップへの最速の方法が提供されます。 次に例を示します。

   ![Windows セットアップ](images/winsetup7.png)

インストールが完了したら、サインインし、Windows 10 デスクトップでサインインしていることを確認してから、最初の Hyper-v チェックポイントを作成します。 チェックポイントは、VM を以前の状態に復元するために使用されます。 このラボでは複数のチェックポイントを作成します。これを後で使用して、プロセスを再度実行することができます。

   ![Windows セットアップ](images/winsetup8.png)

最初のチェックポイントを作成するには、(VM ではなく) Hyper-v を実行しているコンピューターで、管理者特権で Windows PowerShell プロンプトを開き、次のコマンドを実行します。

```powershell
Checkpoint-VM -Name WindowsAutopilot -SnapshotName "Finished Windows install"
```

Hyper-v マネージャーで**Windowsautopilot 操縦**VM をクリックし、[チェックポイント] ウィンドウに [完了した**Windows インストール**] が表示されていることを確認します。

## <a name="capture-the-hardware-id"></a>ハードウェア ID をキャプチャする

> [!NOTE]
> 通常、デバイス ID は、ファクトリの各デバイスで OA3 ツールを実行するときに、OEM によってキャプチャされます。  次に、OEM は、OA3 ツールによって作成された 4K HH を、コンピュータービルドレポート (CBR) と共に送信して Microsoft に送信します。  このラボでは、OEM として機能していますが (4K HH をキャプチャ)、さまざまな理由で OA3 ツールを使用して 4K HH 全体をキャプチャすることはありません (OA3 ツールをインストールする必要があります。デバイスには、Windows のボリュームライセンスバージョンがないため、PS スクリプトを使用するよりも複雑です)。  代わりに、OA3 ツールと同様に、デバイス4K をキャプチャする PowerShell スクリプトを実行して、OA3 ツールの実行をシミュレートします。

PS スクリプトを実行するには、次の手順に従います。

1. 管理者特権の Windows PowerShell プロンプトを開き、次のコマンドを実行します。 これらのコマンドは、VM と物理デバイスのどちらを使用しているかに関係なく同じです。

    ```powershell
    md c:\HWID
    Set-Location c:\HWID
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
    Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
    ```

NuGet パッケージのインストールを求めるメッセージが表示されたら、[**はい]** を選択します。

次のサンプル出力を参照してください。

<pre>
PS C:\> md c:\HWID

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/14/2019  11:33 AM                HWID

PS C:\> Set-Location c:\HWID
PS C:\HWID> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
PS C:\HWID> Install-Script -Name Get-WindowsAutopilotInfo -Force

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\user1\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and
import the NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
PS C:\HWID> $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
PS C:\HWID> Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
PS C:\HWID> dir

    Directory: C:\HWID

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/14/2019  11:33 AM           8184 AutopilotHWID.csv

PS C:\HWID>
</pre>

**C:\HWID**ディレクトリに、サイズが約 8 KB の**AutopilotHWID.csv**ファイルがあることを確認します。  このファイルには、4K の完全な HH が含まれています。

> [!NOTE]
> .Csv 拡張子は Microsoft Excel に関連付けられている場合がありますが、ファイルをダブルクリックすることで適切に表示することはできません。 コンマ区切り記号を正しく解析し、excel でファイルを表示するには、 **Data**  >  excel の**Text/CSV**関数のデータを使用して、適切なデータ列をインポートする必要があります。 関心がある場合を除き、Excel でファイルを表示する必要はありません。 ファイル形式は、自動操縦にインポートされるときに検証されます。 このファイルのデータの例を次に示します。

![シリアル番号とハードウェアハッシュ](images/hwid.png)

このデータを Intune にアップロードして自動操縦用にデバイスを登録する必要があります。そのため、Azure portal にアクセスするために使用するコンピューターに転送する必要があります。  VM ではなく物理デバイスを使用している場合は、ファイルを USB スティックにコピーできます。  VM を使用している場合は、AutopilotHWID.csv ファイルを右クリックしてコピーし、右クリックして、ファイルをデスクトップ (VM の外部) に貼り付けることができます。

ファイルのコピーと貼り付けに問題がある場合は、VM 上のメモ帳の内容を表示し、VM の外部にあるメモ帳にテキストをコピーするだけです。 別のテキストエディターを使用してこの操作を行うことはできません。

> [!NOTE]
> Vm との間でコピーと貼り付けを行う場合は、コピーと貼り付けのプロセス間でマウスカーソルを使用して他の項目をクリックしないようにします。これは、クリップボードを空にしたり、上書きしたりしてからやり直す必要があるためです。 コピーから直接コピーして貼り付けます。

## <a name="reset-the-vm-back-to-out-of-box-experience-oobe"></a>VM を既定のエクスペリエンス (OOBE) に戻します。

ファイルでキャプチャされたハードウェア ID を使用して、Windows 自動操縦用の仮想マシンを準備します。これを行うには、OOBE に戻します。

仮想マシンで、**[設定]、[更新とセキュリティ]、[回復]** の順に移動し、**[この PC を初期状態に戻す]** の **[開始する]** をクリックします。
**[すべて削除する]** と **[ファイルの削除のみ行う]** を選びます。 最後に、**[リセット]** をクリックします。

![[この PC を初期状態に戻す] の最後のプロンプト](images/autopilot-reset-prompt.jpg)

VM またはデバイスのリセットには時間がかかることがあります。 リセットプロセス中に、次の手順 (サブスクリプションレベルの確認) に進みます。

![[この PC を初期状態に戻す] 画面のキャプチャ](images/autopilot-reset-progress.jpg)

## <a name="verify-subscription-level"></a>サブスクリプションレベルの確認

このラボでは、AAD Premium サブスクリプションが必要です。  Premium サブスクリプションがあるかどうかは、 [MDM の登録構成](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility)ブレードに移動することで確認できます。 次の例を参照してください。

**Azure Active Directory**  > **モビリティ (MDM および MAM)**  > **Microsoft Intune**

![MDM と Intune](images/mdm-intune2.png)

上記の構成ブレードが表示されない場合は、 **Premium**サブスクリプションを持っていない可能性があります。  自動登録は、AAD Premium でのみ使用できる機能です。

Intune 試用版アカウントを無料の Premium 試用版アカウントに変換するには、[ **Azure Active Directory**  >  **ライセンス**  >  **All products**  >  ] [すべての製品] [試用 **/購入**] の順に移動し、[Azure AD Premium] または [EMS E5] の**無料試用版**を選択します。

![[この PC を初期状態に戻す] の最後のプロンプト](images/aad-lic1.png)

## <a name="configure-company-branding"></a>会社のブランドの構成

Azure Active Directory で既に会社のブランドが構成されている場合、この手順をスキップすることができます。

> [!IMPORTANT]
> 必ず、グローバル管理者アカウントでサインインしてください。

[Azure Active Directory で [会社のブランド](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding)] に移動し、[**構成**] をクリックして、OOBE 中に表示する任意の種類の会社のブランド化を構成します。

![会社のブランドの構成](images/branding.png)

操作が終了したら、 **[OK]** をクリックします。

> [!NOTE]
> 会社のブランドの変更は、適用されるまで最大 30 分かかります。

## <a name="configure-microsoft-intune-auto-enrollment"></a>Microsoft Intune の自動登録を構成する

Azure Active Directory で既に MDM の自動登録が構成されている場合、この手順をスキップすることができます。

[Azure Active Directory でモビリティ (MDM および MAM)](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility)を開き、[ **Microsoft Intune**] を選択します。 Microsoft Intune が表示されない場合は、[**アプリケーションの追加**] をクリックし、[ **Intune**] を選択します。

このデモの目的では、**[MDM ユーザー スコープ]** で **[すべて]** を選び、**[保存]** をクリックします。

![モビリティ ブレードの MDM ユーザー スコープ](images/autopilot-aad-mdm.png)

## <a name="register-your-vm"></a>VM を登録する

VM (またはデバイス) は、Intune または Microsoft Store for Business (MSfB) のいずれかで登録できます。  どちらのプロセスもここに表示されますが、このラボの目的のために<u>1 つだけ選択</u>します。 MSfB ではなく Intune を使用することを強くお勧めします。

### <a name="autopilot-registration-using-intune"></a>Intune を使用した自動操縦登録

1. Azure portal の Intune で、[**デバイスの登録**] [  >  **Windows 登録**  >  **デバイス**] [  >  **インポート**] の順に選択します。

    ![Intune デバイスのインポート](images/device-import.png)

    > [!NOTE]
    > **Windows の登録**などのメニュー項目がアクティブになっていない場合は、UI の右端のブレードに注目します。  表示されたチャレンジウィンドウで、Intune 構成の特権を提供する必要がある場合があります。

2. 右側のウィンドウで、[ **Windows の自動操縦用デバイスの追加**] で、前にローカルコンピューターにコピーした**AutopilotHWID.csv**ファイルを参照します。  ファイルには、仮想マシン (またはデバイス) のシリアル番号と 4K HH が含まれている必要があります。  他のフィールド (Windows 製品 ID) が空白のままになっている場合でも問題ありません。

    ![HWID CSV](images/hwid-csv.png)

    上記のように、アップロードする前に、ファイルが正しくフォーマットされていることを確認する必要があります。

3. [**インポート**] をクリックして、インポートプロセスが完了するまで待ちます。 この処理には最大 15 分かかることがあります。

4. [**同期**] をクリックして、先ほど登録したデバイスを同期します。 更新する前にしばらく待ってから、VM またはデバイスが追加されたことを確認します。 次の例を参照してください。

   ![HWID のインポート](images/import-vm.png)

### <a name="autopilot-registration-using-msfb"></a>MSfB を使用した自動操縦登録

> [!IMPORTANT]
> Intune を使用して VM (またはデバイス) を既に登録している場合は、この手順をスキップします。

省略可能: プロセスの概要については、次のビデオを参照してください。

&nbsp;

> [!video https://www.youtube.com/embed/IpLIZU_j7Z0]

まず、MSfB アカウントが必要です。  Intune で作成したものと同じものを使用することも、[次の手順](https://docs.microsoft.com/microsoft-store/windows-store-for-business-overview)に従って新しいものを作成することもできます。

次に、メインページの右上隅にある [**サインイン**] をクリックして、テストアカウントを使用して[Microsoft Store for Business](https://businessstore.microsoft.com/en-us/store)にサインインします。

上部のメニューから [**管理**] を選択し、[**デバイス**] カードの下にある [ **Windows 自動操縦展開プログラム**] リンクをクリックします。 次の例を参照してください。

![ビジネス向け Microsoft Store](images/msfb.png)

[**デバイスの追加**] リンクをクリックして CSV ファイルをアップロードします。 リクエストが処理されていることを示すメッセージが表示されます。 新しいデバイスが追加されたことを確認するには、しばらく待ってから更新してください。

![デバイス](images/msfb-device.png)

## <a name="create-and-assign-a-windows-autopilot-deployment-profile"></a>Windows 自動操縦展開プロファイルを作成して割り当てる

> [!IMPORTANT]
> 自動操縦プロファイルを作成し、Intune または MSfB を使用して、登録済みの VM またはデバイスに割り当てることができます。  どちらのプロセスもここに表示されますが、<U>このラボの目的のために1つだけ選択</U>します。

1つ選択します。
- [Intune を使用してプロファイルを作成する](#create-a-windows-autopilot-deployment-profile-using-intune)
- [MSfB を使用してプロファイルを作成する](#create-a-windows-autopilot-deployment-profile-using-msfb)

### <a name="create-a-windows-autopilot-deployment-profile-using-intune"></a>Intune を使用して Windows 自動操縦展開プロファイルを作成する

> [!NOTE]
> デバイスを MSfB に登録しても、Intune には引き続き表示されますが、最初にデバイスの一覧を**同期**してから**更新**する必要がある場合があります。

![デバイス](images/intune-devices.png)

> 上記の例では、物理デバイスと VM の両方が一覧表示されます。 リストに含めることができるのは、これらのうちの1つだけです。

Windows 自動操縦プロファイルを作成するには、[**デバイスの登録**] [windows の登録] [  >  **Windows enrollment**  >  **展開プロファイル**] を選択します。

![展開プロファイル](images/deployment-profiles.png)

[**プロファイルの作成**] をクリックします。

![展開プロファイルの作成](images/create-profile.png)

[**プロファイルの作成**] ブレードで、次の値を使用します。

| 設定 | 値 |
|---|---|
| 名前 | 自動操縦ラボプロファイル |
| 説明 | blank |
| すべての対象デバイスを自動操縦に変換する | いいえ |
| 展開モード | ユーザー主導 |
| Azure AD に参加 | Azure AD 参加済み |

イン**ボックスエクスペリエンス (OOBE)** をクリックし、次の設定を構成します。

| 設定 | 値 |
|---|---|
| EULA | 非表示 |
| プライバシー設定 | 非表示 |
| アカウントの変更オプションを非表示にする | 非表示 |
| ユーザー アカウントの種類 | Standard |
| デバイス名テンプレートの適用 | いいえ |

次の例を参照してください。

![展開プロファイル](images/profile.png)

[ **OK]** をクリックし、[**作成**] をクリックします。

> Intune を使用してプロファイルにアプリを追加する場合は、 [「付録 B: プロファイルへのアプリの追加](#appendix-b-adding-apps-to-your-profile)」に記載されている手順に従ってください。

#### <a name="assign-the-profile"></a>プロファイルを割り当てる

プロファイルはグループにのみ割り当てることができるため、まずプロファイルを適用するデバイスを含むグループを作成する必要があります。 このガイドでは、プロファイルを割り当てるための簡単な手順について説明します。詳細な手順については、「[自動操縦装置グループの作成](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group)」および「[デバイスグループへの自動展開プロファイルの割り当て](https://docs.microsoft.com/intune/enrollment-autopilot#assign-an-autopilot-deployment-profile-to-a-device-group)」を参照してください (省略可能)。

グループを作成するには、Azure portal を開き、[ **Azure Active Directory**グループ] [すべてのグループ] を選択し  >  **Groups**  >  **All groups**ます。

![すべてのグループ](images/all-groups.png)

[グループ] ブレードで [新しいグループ] を選択し、[新しいグループ] UI を開きます。  "セキュリティ" グループの種類を選択し、グループに名前を付けて、[割り当て済み] メンバーシップの種類を選択します。

[**作成**] をクリックしてから [**メンバー** ] パネルを展開し、デバイスのシリアル番号 ([**選択したメンバー**] の下に表示されます) をクリックしてから、[**選択**] をクリックしてそのデバイスをこのグループに追加します。

![新しいグループ](images/new-group.png)

次に、[**作成**] をクリックして、新しいグループの作成を完了します。

[**すべてのグループ**] をクリックし、[最新の状態に**更新**] をクリックして、新しいグループが正常に作成されたことを確認します。

デバイスを含むグループを作成したら、戻ってそのグループにプロファイルを割り当てることができるようになります。 Azure portal の Intune ページに戻ります (1 つは、上部のバナー検索バーに「 **intune** 」と入力し、結果から [ **intune** ] を選択する方法です)。

Intune から [**デバイスの登録**] [  >  **Windows の登録**] [展開プロファイル] を選択し、[  >  **Deployment Profiles**プロファイル] ブレードを開きます。  前に作成したプロファイルの名前 (「自動操縦ラボプロファイル」) をクリックして、そのプロファイルの [詳細] ブレードを開きます。

![ラボプロファイル](images/deployment-profiles2.png)

[**管理**]、[**割り当て**] の順にクリックし、[**含める**] タブを強調表示した状態で [**グループの選択**] ブレードを展開し、[ **AP ラボグループ 1** ] をクリックします (グループは [**選択したメンバー**] の下に表示されます)。

![グループを含める](images/include-group.png)

**[選択]** をクリックし、**[保存]** をクリックします。

![グループを含める](images/include-group2.png)

特定のユーザーをプロファイルに割り当てることもできますが、ラボではこのシナリオについては説明しません。 詳細については、「 [Windows 自動操縦を使用した Intune での windows デバイスの登録](https://docs.microsoft.com/intune/enrollment-autopilot)」を参照してください。

### <a name="create-a-windows-autopilot-deployment-profile-using-msfb"></a>MSfB を使用して Windows 自動操縦展開プロファイルを作成する

既に上記の手順を使用して Intune でプロファイルを作成して割り当てている場合は、このセクションをスキップします。

MSfB でプロファイルを作成して割り当てるために必要な手順を説明する[ビデオ](https://www.youtube.com/watch?v=IpLIZU_j7Z0)が用意されています。 これらの手順についても以下にまとめます。

まず、このラボ用に最初に作成した Intune アカウントを使用して、[ビジネス向け Microsoft Store](https://businessstore.microsoft.com/manage/dashboard)にサインインします。

上部のメニューから [**管理**] をクリックし、左側のナビゲーションツリーの [**デバイス**] をクリックします。

![MSfB 管理](images/msfb-manage.png)

[**デバイス**] タイルの [ **Windows 自動操縦展開プログラム**] リンクをクリックします。

プロファイルを作成するには:

[**デバイス**] ボックスの一覧からデバイスを選択します。

![MSfB 作成](images/msfb-create1.png)

[自動展開] ドロップダウンメニューで、[**新しいプロファイルの作成**] を選択します。

![MSfB 作成](images/msfb-create2.png)

プロファイルに名前を指定し、目的の設定を選択して、[**作成**] をクリックします。

![MSfB 作成](images/msfb-create3.png)

新しいプロファイルが [自動展開] の一覧に追加されます。

プロファイルを割り当てるには:

デバイスにプロファイルを割り当てる (または再割り当てする) には、このラボ用に登録したデバイスの横にあるチェックボックスをオンにし、次に示すように、[**自動展開**] ドロップダウンメニューから割り当てたいプロファイルを選択します。

![MSfB 割り当て](images/msfb-assign1.png)

**プロファイル列の**内容を確認して、プロファイルが目的のデバイスに正常に割り当てられたことを確認します。

![MSfB 割り当て](images/msfb-assign2.png)

> [!IMPORTANT]
> 新しいプロファイルは、デバイスが起動されていない場合にのみ適用され、OOBE を通じて削除されます。 別のプロファイルが適用されているとき、それとは異なるプロファイルの設定は適用できません。 2 つ目のプロファイルをデバイスに適用するには、Windows をデバイスに再インストールする必要があります。

## <a name="see-windows-autopilot-in-action"></a>「Windows 自動操縦の動作」を参照してください。

最後にリセットした後に VM をシャットダウンした場合は、もう一度バックアップを開始します。これにより、再構成の OOBE エクスペリエンスを実行できますが、Intune のデバイスの**プロファイル状態**が [**割り当てなし**] から [割り当て済み]**に変更**され、最終的に**割り当てら**れるまで、デバイスの起動は行われません。

![デバイスの状態](images/device-status.png)

また、[会社のブランド](#configure-company-branding)化を構成した時点から少なくとも30分待ってください。そうしないと、これらの変更が表示されない可能性があります。

> [!TIP]
> 4K HH 情報を収集した後にデバイスをリセットしてから最初の OOBE 画面に戻るようにした場合は、デバイスを再起動して、デバイスが自動操縦デバイスとして認識されることを確認し、想定している自動操縦用の OOBE エクスペリエンスを表示する必要があります。  自動操縦 OOBE エクスペリエンスが表示されない場合は、デバイスをもう一度リセットし (設定 > 更新 & セキュリティ > 回復] をクリックし、[開始] をクリックします。  [この PC をリセットする] で、[すべて削除] を選択し、[ファイルの削除] だけを選択します。 [リセット] をクリックします)。

- デバイスがインターネットに接続されていることを確認します。
- デバイスをオンにする
- 適切な OOBE 画面が表示されていることを確認します (適切な会社のブランドを持つ)。  [地域の選択] 画面、[キーボードの選択] 画面、2番目のキーボード選択画面 (スキップできる) が表示されます。

![OOBE サインイン ページ](images/autopilot-oobe.jpg)

デスクトップに到達するとすぐに、デバイスは**有効な**自動操縦デバイスとして Intune に表示されます。  Intune Azure portal にアクセスし、[デバイス **> すべてのデバイス**] を選択します。次に、データを**更新**して、デバイスが [無効] から [有効] に変更されていることを確認し、デバイスの名前を更新します。

![有効なデバイス](images/enabled-device.png)

言語とキーボード レイアウトを選択すると、会社のブランドのサインイン画面が表示されます。 Azure Active Directory の資格情報を入力するとすべて完了です。

Windows の自動操縦によってデバイスが Azure Active Directory に自動的に参加し、Microsoft Intune に登録されるようになります。 このプロセスを別の設定で繰り返すには、チェックポイントを使用します。

## <a name="remove-devices-from-autopilot"></a>自動操縦からデバイスを削除する

このラボの完了後にデバイス (または VM) を他の目的で使用するには、Intune または MSfB を使用して自動操縦からデバイスを削除 (登録解除) してからリセットする必要があります。  デバイスの登録を解除する手順につい[ては](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal) [、こちらと以下を参照し](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group)てください。

### <a name="delete-deregister-autopilot-device"></a>自動操縦用デバイスの削除 (登録解除)

デバイスを自動操縦から登録解除する前に、Intune からデバイスを削除 (または、または工場出荷時にリセット) する必要があります。 Intune から (Azure Active Directory ではなく) デバイスを削除するには、Intune Azure portal にログインし、[ **intune > デバイス > すべてのデバイス**] に移動します。  削除するデバイスの横にあるチェックボックスをオンにし、上部のメニューにある [削除] ボタンをクリックします。

![デバイスの削除](images/delete-device1.png)

操作を完了するには、[ **X** ] をクリックします。

![デバイスの削除](images/delete-device2.png)

これにより、Intune の管理からデバイスが削除され、**すべてのデバイス > intune > デバイス**に表示されなくなります。 ただし、この方法では、デバイスが自動操縦から登録解除されることはありません。そのため、デバイスは [ **Intune > デバイスの登録 > windows の登録 > Windows 自動展開プログラム > デバイス**] に表示されます。

![デバイスの削除](images/delete-device3.png)

**Intune > デバイス > すべてのデバイス**] の一覧と**intune > デバイスの登録 > windows の登録 > Windows 自動展開プログラム > デバイス**の一覧は異なるものであり、データストアは完全に分離されています。  前者 (すべてのデバイス) は、現在 Intune に登録されているデバイスの一覧です。

> [!NOTE]
> デバイスは、起動されると、[すべてのデバイス] の一覧にのみ表示されます。  後者 (Windows 自動操縦展開プログラム > デバイス) は、その Intune アカウントから自動操縦プログラムに現在登録されているデバイスの一覧です。 Intune に登録されていない場合や、登録されていない場合もあります。

自動操縦プログラムからデバイスを削除するには、デバイスを選択し、[削除] をクリックします。

![デバイスの削除](images/delete-device4.png)

前に行った Intune からデバイスを削除することを通知する警告メッセージが表示されます。

![デバイスの削除](images/delete-device5.png)

この時点で、デバイスは Intune から登録解除され、自動操縦から登録解除されています。  数分後に [**同期**] ボタンをクリックし、[**更新**] ボタンをクリックして、デバイスが自動操縦プログラムに表示されないことを確認します。

![デバイスの削除](images/delete-device6.png)

デバイスが表示されなくなったら、他の目的で再利用することができます。

また、(必要に応じて) AAD からデバイスを削除する場合は、[ **Azure Active Directory > デバイス**] に移動して [すべてのデバイス] >、デバイスを選択し、[削除] ボタンをクリックします。

![デバイスの削除](images/delete-device7.png)

## <a name="appendix-a-verify-support-for-hyper-v"></a>付録 A: Hyper-v のサポートを確認する

Windows 8 以降では、Hyper-V をインストールするため、ホスト コンピューターのマイクロプロセッサが第 2 レベルのアドレス変換 (SLAT) をサポートしている必要があります。 詳細については、「[Hyper-V: List of SLAT-Capable CPUs for Hosts](https://social.technet.microsoft.com/wiki/contents/articles/1401.hyper-v-list-of-slat-capable-cpus-for-hosts.aspx)」を参照してください。

コンピューターが SLAT をサポートしていることを確認するには、管理者のコマンドプロンプトを開き、「 **systeminfo**」と入力し、enter キーを押しながら下へスクロールして、出力の下部にある [Hyper-v の要件] の横に表示されるセクションを確認します。 次の例を参照してください。

<pre style="overflow-y: visible">
C:>systeminfo

...
Hyper-V Requirements:      VM Monitor Mode Extensions: Yes
                           Virtualization Enabled In Firmware: Yes
                           Second Level Address Translation: Yes
                           Data Execution Prevention Available: Yes
</pre>

この例では、コンピューターは SLAT と Hyper-V をサポートします。

> 1 つまたは複数の要件が **いいえ** と評価される場合、そのコンピューターは Hyper-V のインストールをサポートしていません。  ただし、仮想化設定のみに互換性がない場合は、BIOS で仮想化を有効にすることで、**[ファームウェアで仮想化が有効になっています]** 設定を **[いいえ]** から **[はい]** に変更できる場合があります。 この設定の場所は製造元および BIOS バージョンにより異なりますが、通常は BIOS のセキュリティの設定に関連付けられています。

また、次の例に示すように、プロセッサの製造元や[msinfo32](https://technet.microsoft.com/library/cc731397.aspx)ツールで提供されている[ツール](https://blogs.msdn.microsoft.com/taylorb/2008/06/19/hyper-v-will-my-computer-run-hyper-v-detecting-intel-vt-and-amd-v/)を使用して hyper-v のサポートを特定したり、 [coreinfo](https://technet.microsoft.com/sysinternals/cc835722)ユーティリティをダウンロードして実行したりすることもできます。

<pre style="overflow-y: visible">
C:>coreinfo -v

Coreinfo v3.31 - Dump information on system CPU and memory topology
Copyright (C) 2008-2014 Mark Russinovich
Sysinternals - www.sysinternals.com

Intel(R) Core(TM) i7-2600 CPU @ 3.40GHz
Intel64 Family 6 Model 42 Stepping 7, GenuineIntel
Microcode signature: 0000001B
HYPERVISOR      -       Hypervisor is present
VMX             *       Supports Intel hardware-assisted virtualization
EPT             *       Supports Intel extended page tables (SLAT)
</pre>

> [!NOTE]
> Hyper-v を実行するには、64ビットのオペレーティングシステムが必要です。

## <a name="appendix-b-adding-apps-to-your-profile"></a>付録 B: プロファイルへのアプリの追加

### <a name="add-a-win32-app"></a>Win32 アプリを追加する

#### <a name="prepare-the-app-for-intune"></a>Intune 用にアプリを準備する

アプリケーションを Intune にプルして、AP プロファイルの一部にする前に、 [IntuneWinAppUtil.exe コマンドラインツール](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool)を使用して、アプリケーションを配布用に "パッケージ化" する必要があります。  ツールをダウンロードした後、ツールを使用するには、次の3ビットの情報を収集します。

1. アプリケーションのソースフォルダー
2. セットアップ実行可能ファイルの名前
3. 新しいファイルの出力フォルダー

このラボでは、Win32 アプリとしてメモ帳 + + ツールを使用します。

[ここで](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available)メモ帳 + + msi パッケージをダウンロードし、ファイルを既知の場所 (c:\ Notepad + + msi など) にコピーします。

次のように、IntuneWinAppUtil ツールを実行して、3つの質問に対する回答を提供します。

![アプリを追加する](images/app01.png)

ツールの実行が完了すると、出力フォルダーに intunewin ファイルが作成されます。これは、次の手順を使用して Intune にアップロードできます。

#### <a name="create-app-in-intune"></a>Intune でアプリを作成する

Azure portal にログインし、[ **Intune**] を選択します。

**Intune > クライアントアプリ > アプリ**] に移動し、[**追加**] ボタンをクリックして新しいアプリケーションパッケージを作成します。

![アプリを追加する](images/app02.png)

[**アプリの種類**] で、[ **Windows アプリ (Win32)**] を選択します。

![アプリを追加する](images/app03.png)

[**アプリのパッケージファイル**] ブレードで、出力フォルダー内の**7.6.3**ファイルを参照して開き、[ **OK**] をクリックします ()。

![アプリを追加する](images/app04.png)

[**アプリ情報の構成**] ブレードで、次のようなフレンドリ名、説明、および発行元を指定します。

![アプリを追加する](images/app05.png)

[**プログラムの構成**] ブレードで、インストールとアンインストールのコマンドを指定します。

インストール: msiexec/i "npp.7.6.3.installer.x64.msi"/q Uninstall: msiexec/x "{F188A506-C3C6-4411-BE3A-DA5BF1EA6737}"/q

> [!NOTE]
> 場合によっては、インストールとアンインストールのコマンドを自分で記述する必要はありません。これは、 [IntuneWinAppUtil.exe コマンドラインツール](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool)が .msi ファイルを intunewin ファイルに変換したときに自動的に生成されるためです。

![アプリを追加する](images/app06.png)

単に "notepad + + .exe/S" のようなインストールコマンドを使用しても、メモ帳は実際にはインストールされません。アプリを起動するだけです。  プログラムを実際にインストールするには、代わりに .msi ファイルを使用する必要があります。  メモ帳 + + には、実際には .msi バージョンのプログラムはありませんが、[サードパーティプロバイダー](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available)の .msi バージョンがあります。

[ **OK]** をクリックして入力を保存し、[**要件**] ブレードをアクティブにします。

[**要件の構成**] ブレードで、 **Os アーキテクチャ**と**最小 os バージョン**を指定します。

![アプリを追加する](images/app07.png)

次に、**検出規則**を構成します。  ここでは、手動形式を選択します。

![アプリを追加する](images/app08.png)

[**追加**] をクリックして、ルールのプロパティを定義します。  [**ルールの種類**] で、[ **msi**] を選択します。これにより、適切な msi 製品コードがルールに自動的にインポートされます。

![アプリを追加する](images/app09.png)

[ **OK]** を2回クリックして、最後の構成のメインの [**アプリの追加**] ブレードに戻り、もう一度保存します。

**リターンコード**: このため、リターンコードは既定値のままにしておきます。

![アプリを追加する](images/app10.png)

**[OK]** をクリックして終了します。

最終的な**スコープ (タグ)** ブレードの構成は省略できます。

[**追加**] ボタンをクリックして、アプリパッケージを確定して保存します。

インジケーターメッセージには、追加が完了したことが示されます。

![アプリを追加する](images/app11.png)

アプリの一覧でアプリを見つけることができます。

![アプリを追加する](images/app12.png)

#### <a name="assign-the-app-to-your-intune-profile"></a>Intune プロファイルにアプリを割り当てる

> [!NOTE]
> 次の手順は、以前に[Intune でグループを作成し、そのグループにプロファイルを割り当て](#assign-the-profile)た場合にのみ機能します。  まだ行っていない場合は、ラボのメイン部分に戻り、これらの手順を完了してから、ここに戻ってください。

[ **Intune > クライアントアプリ > アプリ**] ウィンドウで、既に作成したアプリパッケージを選択して、[プロパティ] ブレードを表示します。  次に、メニューから [**割り当て**] をクリックします。

![アプリを追加する](images/app13.png)

**[グループの追加]** を選んで、アプリに関連する **[グループの追加]** ウィンドウを開きます。

このため、[**割り当ての種類**] ドロップダウンメニューから [**必須**] を選択します。

> **登録されているデバイスで使用できる**ということは、ユーザーがポータルサイトアプリまたはポータルサイト web サイトからアプリをインストールすることを意味します。

[**含まれているグループ**] を選択し、このアプリを使用する前に作成したグループを割り当てます。

![アプリを追加する](images/app14.png)

![アプリを追加する](images/app15.png)

[**グループの選択**] ウィンドウで、[**選択**] ボタンをクリックします。

[**グループの割り当て**] ウィンドウで、[ **OK]** を選択します。

**[グループの追加]** ウィンドウで **[OK]** を選択します。

アプリの **[割り当て]** ウィンドウで、 **[保存]** を選びます。

![アプリを追加する](images/app16.png)

この時点で、Intune に Win32 アプリを追加する手順が完了しました。

アプリを Intune に追加する方法の詳細については、「 [Intune スタンドアロン-Win32 アプリ管理](https://docs.microsoft.com/intune/apps-win32-app-management)」を参照してください。

### <a name="add-office-365"></a>Office 365 の追加

#### <a name="create-app-in-intune"></a>Intune でアプリを作成する

Azure portal にログインし、[ **Intune**] を選択します。

**Intune > クライアントアプリ > アプリ**] に移動し、[**追加**] ボタンをクリックして新しいアプリケーションパッケージを作成します。

![アプリを追加する](images/app17.png)

[**アプリの種類**] で、[ **Office 365 Suite > Windows 10**] を選択します。

![アプリを追加する](images/app18.png)

[**アプリスイートの構成**] ウィンドウで、インストールする Office アプリを選択します。  この labe では、Excel のみを選択しています。

![アプリを追加する](images/app19.png)

**[OK]** をクリックします。

[**アプリスイートの情報**] ウィンドウで、<i>一意</i>のスイート名と適切な説明を入力します。

> 会社のポータルに表示される、アプリ スイートの名前を入力します。 使用するスイート名はすべて一意にします。 同じアプリ スイート名が 2 つ存在する場合、会社のポータルではそのアプリのいずれかのみがユーザーに表示されます。

![アプリを追加する](images/app20.png)

**[OK]** をクリックします。

[**アプリスイートの設定**] ウィンドウで、**更新チャネル**の [**毎月**] を選択します (このラボの目的では、どのような選択でも問題ありません)。  また、[**はい]** を選択して **、アプリの使用許諾契約書に自動的に同意**します。

![アプリを追加する](images/app21.png)

[ **OK]** をクリックし、[**追加**] をクリックします。

#### <a name="assign-the-app-to-your-intune-profile"></a>Intune プロファイルにアプリを割り当てる

> [!NOTE]
> 次の手順は、以前に[Intune でグループを作成し、そのグループにプロファイルを割り当て](#assign-the-profile)た場合にのみ機能します。  まだ行っていない場合は、ラボのメイン部分に戻り、これらの手順を完了してから、ここに戻ってください。

[ **Intune > クライアントアプリ > アプリ**] ウィンドウで、既に作成した Office パッケージを選択して、[プロパティ] ブレードを表示します。  次に、メニューから [**割り当て**] をクリックします。

![アプリを追加する](images/app22.png)

**[グループの追加]** を選んで、アプリに関連する **[グループの追加]** ウィンドウを開きます。

このため、[**割り当ての種類**] ドロップダウンメニューから [**必須**] を選択します。

> **登録されているデバイスで使用できる**ということは、ユーザーがポータルサイトアプリまたはポータルサイト web サイトからアプリをインストールすることを意味します。

[**含まれているグループ**] を選択し、このアプリを使用する前に作成したグループを割り当てます。

![アプリを追加する](images/app23.png)

![アプリを追加する](images/app24.png)

[**グループの選択**] ウィンドウで、[**選択**] ボタンをクリックします。

[**グループの割り当て**] ウィンドウで、[ **OK]** を選択します。

**[グループの追加]** ウィンドウで **[OK]** を選択します。

アプリの **[割り当て]** ウィンドウで、 **[保存]** を選びます。

![アプリを追加する](images/app25.png)

この時点で、Office を Intune に追加する手順は完了しました。

Office アプリを Intune に追加する方法の詳細については、「Microsoft Intune を使用して[Windows 10 デバイスに office 365 アプリを割り当てる](https://docs.microsoft.com/intune/apps-add-office365)」を参照してください。

このラボの指示に従って、win32 アプリ (メモ帳 + +) と Office (Excel のみ) の両方をインストールした場合、VM はアプリの一覧に表示されます。ただし、データの読み込みには数分かかる場合があります。

![アプリを追加する](images/app26.png)

## <a name="glossary"></a>用語集

<table border="1">
<tr><td>OEM</td><td>Original Equipment Manufacturer (相手先ブランド供給)</td></tr>
<tr><td>CSV</td><td>コンマ区切り値</td></tr>
<tr><td>MPC</td><td>Microsoft パートナー センター</td></tr>
<tr><td>CSP</td><td>クラウド ソリューション プロバイダー</td></tr>
<tr><td>MSfB</td><td>ビジネス向け Microsoft Store</td></tr>
<tr><td>AAD</td><td>Azure Active Directory</td></tr>
<tr><td>4K HH</td><td>4K ハードウェアハッシュ</td></tr>
<tr><td>CBR</td><td>コンピュータービルドレポート</td></tr>
<tr><td>EC</td><td>Enterprise コマース (サーバー)</td></tr>
<tr><td>DDS</td><td>デバイスディレクトリサービス</td></tr>
<tr><td>OOBE</td><td>すぐに使えるエクスペリエンス</td></tr>
<tr><td>VM</td><td>仮想マシン</td></tr>
</table>
