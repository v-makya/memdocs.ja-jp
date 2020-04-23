---
title: 既存のデバイス向け Windows Autopilot
titleSuffix: Configuration Manager
description: Configuration Manager タスク シーケンスを使用して、Windows Autopilot ユーザー駆動モード用に Windows 7 デバイスを再イメージ化およびプロビジョニングします
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709020"
---
# <a name="windows-autopilot-for-existing-devices"></a>既存のデバイス向け Windows Autopilot
<!--3607717, fka 1358333-->

*適用対象:Configuration Manager (Current Branch)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) では、組織がエンド ユーザーに新しい Windows 10 デバイスをそのままの状態で出荷し、ユーザーが安全で生産性の高い Windows 10 デバイスを取得するためにたどるプロビジョニング フローを定義する方法が提供されます。 デバイスは Windows Autopilot サービスに登録されるため、必要な Windows Autopilot プロファイルを割り当てることができます。 このプロファイルで、そのデバイスの out-of-box experience (OOBE) が定義されます。 

[既存のデバイス向けの Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) は、Windows 10 バージョン 1809 以降で利用できます。 この機能を利用すると、単一のネイティブな Configuration Manager タスク シーケンスを使用して、[Windows Autopilot ユーザー駆動モード](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven)用に Windows 7 デバイスを再イメージ化およびプロビジョニングできます。 



## <a name="prerequisites"></a>[前提条件]

- Windows 10 バージョン 1809 以降のインストール メディアを取得します。 その後、Configuration Manager の OS イメージを作成します。 詳しくは、[OS イメージの管理](../get-started/manage-operating-system-images.md)に関するページをご覧ください。

- Microsoft Intune で、Windows Autopilot 用のプロファイルを作成します。 詳細については、「[Enroll Windows devices in Intune by using Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)」(Windows Autopilot を使用して Intune に Windows デバイスを登録する) を参照してください。

- Windows Autopilot サービスにまだ登録されていないデバイス。 デバイスが既に登録されている場合、割り当てられているプロファイルが優先されます。 既存のデバイス プロファイルに対する Autopilot は、オンライン プロファイルがタイムアウトした場合にのみ適用されます。



## <a name="create-the-configuration-file"></a>構成ファイルを作成する

1. インターネットに接続された Windows デバイスで、管理用の PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  

    1. 必要なモジュールをインストールし、プロンプトを受け入れて続行します  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. 管理者の資格情報を使用して Intune にサインインします  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Intune テナントに関連付けられているすべての Windows Autopilot プロファイルを取得します  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. 各プロファイルの構成ファイルを作成します。 ファイルはプロファイルの表示名で、現在のユーザーのデスクトップ上に保存されます。<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > 構成ファイルに含めることができるプロファイルは 1 つだけです。 各プロファイルは中かっこ `{}` で囲む必要があります。  

2. プロファイルの 1 つを、**AutopilotConfigurationFile.json** という名前の ANSI エンコード ファイルに保存します。 それを Configuration Manager パッケージ ソースとして適した場所に保存します。  

    > [!Tip]  
    > PowerShell コマンドレット **Out-File** を使用して JSON 出力をファイルにリダイレクトする場合、既定では Unicode エンコードが使用されます。 このコマンドレットでは長い行が切り詰められる場合もあります。 `-Encoding ASCII` パラメーターを指定した **Set-Content** コマンドレットを使用し、適切なテキスト エンコードを設定します。   
    > 
    > Windows のメモ帳では、既定で ANSI エンコードが使われます。  

3. このファイルを含む Configuration Manager パッケージを作成します。 プログラムは必要ありません。 詳しくは、[パッケージの作成](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program)に関する記事をご覧ください。  

    > [!NOTE]  
    > Windows では、このファイルを **AutopilotConfigurationFile.json** という名前にする必要があります。 複数の Autopilot プロファイルを使用するには、別の Configuration Manager パッケージを作成します。  



## <a name="create-the-task-sequence"></a>タスク シーケンスを作成する

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[オペレーティング システム]** を展開して **[タスク シーケンス]** ノードを選択します。 リボンの **[タスク シーケンスの作成]** を選択します。  

2. **[新しいタスク シーケンスの作成]** ページで、 **[既存のデバイス向けに Windows Autopilot を展開する]** オプションを選択します。  

3. **[タスク シーケンス情報]** ページで、名前を指定し、必要に応じて説明を追加して、ブート イメージを選択します。 サポートされているブート イメージのバージョンについて詳しくは、[Windows 10 のサポート](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)に関する記事をご覧ください。  

4. **[Windows のインストール]** ページで、Windows 10 の**イメージ パッケージ**を選択します。 次に、以下の設定を構成します。  

    - **イメージ インデックス**:組織で必要な、Enterprise、Education、または Professional を選択します  

    - **[オペレーティング システムをインストールする前にターゲット コンピューターのパーティションを作成してフォーマットする]** オプションを有効にします  

    - **BitLocker で使用するタスク シーケンスを構成する**:このオプションを有効にする場合、タスク シーケンスに BitLocker を有効にするために必要な手順が含まれます  

    - **プロダクト キー**:Windows ライセンス認証のためのプロダクト キーを指定する必要がある場合は、ここに入力します  

    - Windows 10 でローカル管理者アカウントを構成するには、次のオプションのいずれかを選択します。  
        - **ローカルの管理者パスワードをランダムに生成し、サポートされているすべてのプラットフォームのアカウントを無効にする (推奨)**
        - **アカウントを有効にし、ローカル管理者パスワードを指定する**

5. **[ネットワークの構成]** ページで、 **[ワークグループに参加]** オプションを選択します。 このタスク シーケンスでは Windows システム準備ツール (sysprep) を使用します。 デバイスがドメインに参加している場合は、sysprep が失敗します。  

6. **[Configuration Manager のインストール]** ページで、お使いの環境に必要なインストール プロパティを追加します。  

    > [!Tip]  
    > タスク シーケンスでこの情報が必要になるのは、sysprep が実行される前にタスク シーケンス中に Configuration Manager クライアント コンポーネントが必要な場合のみです。 たとえば、ソフトウェア更新プログラムやアプリケーションをインストールする場合です。 これらの操作を行わない場合、クライアントは必要ありません。 タスク シーケンスで sysprep が実行される前にアンインストールされます。  

7. **[更新プログラムを含める]** ページでは、 **[ソフトウェア更新プログラムをインストールしない]** オプションが既定で選択されています。  

    > [!Tip]  
    > オフライン イメージ サービスを使用して、イメージを Windows 10 の最新の品質更新プログラムに保ちます。 詳しくは、「[ソフトウェア更新プログラムをオペレーティング システム イメージに適用する](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)」をご覧ください。  

8. **[アプリケーションのインストール]** ページでは、タスク シーケンス中にインストールするアプリケーションを選択できます。 ただし、このシナリオではシグネチャ イメージ アプローチをミラーリングすることをお勧めします。 Autopilot でデバイスをプロビジョニングした後、すべてのアプリケーションと構成を Microsoft Intune または Configuration Manager の共同管理から適用します。 このプロセスでは、新しいデバイスを受け取るユーザーと、既存デバイス向けの Windows Autopilot を使用するユーザーに、一貫したエクスペリエンスが提供されます。  

8. **[システムの準備]** ページで、Autopilot 構成ファイルを含むパッケージを選択します。 既定では、タスク シーケンスは Windows Sysprep を実行した後でコンピューターを再起動します。 **[Shutdown computer after this task sequence completes]\(このタスク シーケンスの完了後にコンピューターをシャットダウンする\)** オプションを選択することもできます。 このオプションでは、一貫した Autopilot エクスペリエンスのために、デバイスを準備してそれをユーザーに配布できます。  

9. ウィザードを完了します。  

タスク シーケンスを編集する場合は、既存の OS イメージを適用する既定のタスク シーケンスに似ています。 このタスク シーケンスには、次の追加手順が含まれています。  

- **Windows Autopilot の構成を適用する**:この手順では、指定したパッケージから Autopilot 構成ファイルを適用します。 これは新しい種類の手順ではなく、ファイルをコピーするための**コマンド ラインの実行**手順です。  

- **Windows のキャプチャの準備**:この手順では Windows Sysprep を実行します。設定は、 **[この操作の実行後にコンピューターをシャットダウンする]** になっています。 詳細については、「[Windows のキャプチャの準備](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture)」を参照してください。  

既存のデバイス向け Windows Autopilot タスク シーケンスでは、デバイスは Azure Active Directory (Azure AD) に参加します。 

> [!NOTE]  
> Windows 10 バージョン 1903 およびバージョン 1909 の場合、Autopilot には、Sysprep によって **AutopilotConfigurationFile.json** ファイルが削除されるという既知の問題があります。 この方法を使用して Windows 10 バージョン 1903 またはバージョン 1909 を展開する場合は、このタスク シーケンスを編集し、次の変更を加えてください。
>
> 1. **Windows のキャプチャの準備**ステップを無効にします。
> 2. 無効にした **Windows のキャプチャの準備**ステップの直後に、新しい**コマンド ラインの実行**ステップを追加します。 それを構成して、次のコマンド ラインを実行するようにします: `c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> 詳細については、「[Windows Autopilot - 既知の問題](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues)」をご覧ください。

OneDrive for Business の[既知のフォルダーの移動](https://docs.microsoft.com/onedrive/redirect-known-folders)を使用して、Windows 10 のアップグレード前にユーザーのデータがバックアップされていることを確認してください。



## <a name="next-steps"></a>次のステップ

共同管理を使用して、Windows 10 デバイスの管理機能を強化します。 共同管理への 2 つ目のパスでは、Windows Autopilot による最新のプロビジョニングを使用します。 詳細については、以下の記事を参照してください。

- [共同管理とは](../../comanage/overview.md)
- [共同管理へのパス](../../comanage/quickstart-paths.md)
- [Windows Autopilot と共同管理](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>関連項目

- [Windows Autopilot を使用して Intune に Windows デバイスを登録する](https://docs.microsoft.com/intune/enrollment-autopilot)
