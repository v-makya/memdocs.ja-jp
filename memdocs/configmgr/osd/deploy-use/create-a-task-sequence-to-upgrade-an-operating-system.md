---
title: OS の更新タスク シーケンスを作成する
titleSuffix: Configuration Manager
description: タスク シーケンスを使用して、自動的に Windows 7 以降から Windows 10 にアップグレードします。
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 907c36b6f06bbf4fbbabb9ee1b2df6cadb0acb75
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125459"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Configuration Manager で OS をアップグレードするタスク シーケンスを作成する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager でタスク シーケンスを使用して、OS をインストール先のコンピューターで自動的にアップグレードします。 Windows 7 以降から Windows 10 に、または Windows Server 2012 以降から Windows Server 2016 にアップグレードできます。 アプリケーションまたはソフトウェア更新プログラムなど、OS のアップグレード パッケージやインストールする他のコンテンツを参照するタスク シーケンスを作成します。 OS をアップグレードするタスク シーケンスは、「[Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md)」シナリオの一部です。  


## <a name="prerequisites"></a>[前提条件]

タスク シーケンスを作成する前に、以下の要件を満たす必要があります。

### <a name="required"></a>必須

- [OS のアップグレード パッケージ](../get-started/manage-operating-system-upgrade-packages.md)が Configuration Manager コンソールで使用可能である必要があります。  

- Windows Server 2016 にアップグレードする場合は、オペレーティング システムのアップグレードのタスク シーケンス ステップで、 **[Ignore any dismissable compatibility messages]\(互換性に関する却下可能なメッセージをすべて無視する\)** 設定を選択します。 そうしないと、アップグレードは失敗します。  

### <a name="required-if-used"></a>必須 (使用する場合)  

- [ソフトウェア更新プログラム](../../sum/get-started/synchronize-software-updates.md)が Configuration Manager コンソールで同期されている必要があります。  

- [アプリケーション](../../apps/deploy-use/create-applications.md)が Configuration Manager コンソールに追加されている必要があります。  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a> OS をアップグレードするタスク シーケンスを作成する  

クライアント上の OS をアップグレードするには、タスク シーケンスを作成し、タスク シーケンスの作成ウィザードで **[オペレーティング システムをアップグレード パッケージからアップグレードする]** を選択します。 ウィザードにより、OS のアップグレード、ソフトウェア更新プログラムの適用、アプリケーションのインストールのタスク シーケンス ステップが追加されます。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[オペレーティング システム]** を展開して **[タスク シーケンス]** を選択します。  

2. リボンの **[ホーム]** タブにある **[作成]** グループで、 **[タスク シーケンスの作成]** を選択します。  

3. タスク シーケンスの作成ウィザードの **[新しいタスク シーケンスの作成]** ページで、 **[オペレーティング システムをアップグレード パッケージからアップグレードする]** を選択してから、 **[次へ]** を選択します。  

4. **[タスク シーケンス情報]** ページで次の設定を指定します。  

    - **タスク シーケンス名**:タスク シーケンスを識別する名前を指定します。  

    - **説明**:必要に応じて、説明を指定します。  

5. **[Windows オペレーティング システムのアップグレード]** ページで次の設定を指定します。  

    - **[アップグレード パッケージ]** :OS のアップグレードのソース ファイルを含むアップグレード パッケージを指定します。 **[プロパティ]** ウィンドウの情報を参照して、正しいアップグレード パッケージが選択されていることを確認します。 詳しくは、[OS のアップグレード パッケージの管理](../get-started/manage-operating-system-upgrade-packages.md)に関するページをご覧ください。  

    - **[エディション インデックス]** :複数の OS のエディション インデックスをパッケージから入手できる場合、希望のエディション インデックスを選択します。 既定では、最初のインデックスが選択されます。  

    - **プロダクト キー**:インストールする OS の Windows プロダクト キーを指定します。 エンコードされたボリューム ライセンス キーまたは標準のプロダクト キーを指定します。 標準のプロダクト キーを使う場合は、5 つの各文字グループをダッシュ (`-`) で区切ります。 例: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`。 ボリューム ライセンス版のアップグレードの場合、プロダクト キーは必要ないことがあります。  

        > [!Note]  
        > このプロダクト キーは、マルチ ライセンス認証キー (MAK) または汎用ボリューム ライセンス キー (GVLK) でもかまいません。 GVLK は、キー管理サービス (KMS) クライアント セットアップ キーとも呼ばれます。 詳細については、「[ボリューム ライセンス認証の計画](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)」を参照してください。 KMS クライアント セットアップ キーの一覧については、Windows Server のライセンス認証ガイドの「[付録 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)」を参照してください。

    - **[互換性に関するメッセージが無視できる場合、すべて無視する]** :Windows Server 2016 にアップグレードする場合は、この設定を選択します。 この設定を選択しないと、Windows アプリの互換性ダイアログで、ユーザーが **[確認]** を選択するのを Windows セットアップが待機してしまうため、タスク シーケンスを完了できません。  

6. **[更新プログラムを含める]** ページで、必要なソフトウェア更新プログラムまたはすべてのソフトウェア更新プログラムをインストールするか、まったくインストールしないかを指定します。 その後、 **[次へ]** を選択します。 ソフトウェア更新プログラムをインストールするように指定する場合、Configuration Manager は、セットアップ先のコンピューターがメンバーとなっているコレクション向けの更新プログラムのみをインストールします。  

7. **[アプリケーションのインストール]** ページで、展開先コンピューターにインストールするアプリケーションを指定してから、 **[次へ]** を選択します。 複数のアプリケーションを選択する場合は、特定のアプリケーションのインストールが失敗したときにタスク シーケンスを続行するかどうかも指定します。  

8. ウィザードを完了します。  

> [!Important]  
> タスク シーケンスがデバイス上で実行すると、構成マネージャー クライアントはさまざまなシナリオでタスク シーケンスの動作を制御するいくつかのスクリプトを作成します。 タスク シーケンスが完了しても、クライアントはコンピューターが再起動するまでこれらのスクリプトを削除しません。 これらのスクリプト ファイルには、機密情報は含まれません。  

Windows 10 の一括アップグレード用の既定のタスク シーケンス テンプレートに、アップグレード プロセスの前後に追加する推奨アクションを含む追加グループが含まれます。 これらのアクションは、Windows 10 にデバイスを正常にアップグレードしている多くのユーザーに共通するものです。 詳細については、[アップグレードの準備](#recommended-task-sequence-steps-to-prepare-for-upgrade)および[処理後](#recommended-task-sequence-steps-for-post-processing)の推奨されるタスク シーケンス ステップを参照してください。

バージョン 1806 以降では、このタスク シーケンス テンプレートには、アップグレード プロセスが失敗した場合に追加する推奨アクションを備えたグループも含まれます。 これらのアクションによって、トラブルシューティングが容易になりました。 詳しくは、「[失敗時の推奨されるタスク シーケンス ステップ](#recommended-task-sequence-steps-on-failure)」をご覧ください。<!--1358500-->  


## <a name="configure-pre-cache-content"></a>コンテンツの事前キャッシュを構成する

<!--1021244-->
タスク シーケンスの利用可能な展開について、事前キャッシュ機能を使用することで、ユーザーがタスク シーケンスをインストールする前に、関連する OS アップグレード パッケージ コンテンツをクライアントにダウンロードさせることができます。  

詳細については、「[コンテンツの事前キャッシュを構成する](configure-precache-content.md)」を参照してください。


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>アップグレードを準備する推奨されるタスク シーケンスのステップ

Windows 10 の一括アップグレード用の既定のタスク シーケンス テンプレートに、アップグレード プロセスの前に追加する推奨アクションを含む追加グループが含まれます。 **[アップグレードの準備]** グループのこれらのアクションは、Windows 10 にデバイスを正常にアップグレードしている多くのユーザーに共通するものです。 これらの操作がまだ含まれていない既存のタスク シーケンスがある場合は、タスク シーケンスの **[アップグレードの準備]** グループにこれらを手動で追加します。  

### <a name="battery-checks"></a>バッテリのチェック

このグループにステップを追加して、コンピューターがバッテリまたは有線の電源を使用しているかどうかを確認します。 このアクションには、このチェックを実行するためのカスタム スクリプトまたはユーティリティが必要です。

#### <a name="battery-check-example"></a>バッテリのチェックの例

WbemTest を使用し、`root\cimv2` 名前空間に接続します。 その後、次のクエリを実行します。

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

結果が返された場合、デバイスはバッテリで稼働しています。 それ以外の場合、デバイスは有線の電源に接続されています。  

### <a name="networkwired-connection-checks"></a>ネットワーク接続およびワイヤード接続のチェック

コンピューターがネットワークに接続されているか、またワイヤレス接続を使っていないかどうかを確認するには、このグループにステップを追加します。 このアクションには、このチェックを実行するためのカスタム スクリプトまたはユーティリティが必要です。

#### <a name="network-check-example"></a>ネットワークのチェックの例

WbemTest を使用し、`root\cimv2` 名前空間に接続します。 その後、次のクエリを実行します。

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

結果が返された場合、デバイスは Wi-Fi で稼働しています。 それ以外の場合、デバイスは有線ネットワーク接続につながっています。

### <a name="remove-incompatible-applications"></a>互換性のないアプリケーションを削除する

このグループにステップを追加して、この Windows 10 のバージョンと互換性のないすべてのアプリケーションを削除します。 アプリケーションをアンインストールする方法はさまざまです。  

アプリケーションが Windows インストーラーを使っている場合は、アプリケーションの Windows インストーラー展開の種類プロパティの **[プログラム]** タブから、 **[アンインストール プログラム]** コマンド ラインをコピーします。 そして、アンインストール プログラムのコマンド ラインの **[コマンド ラインの実行]** ステップを、このグループに追加します。 次に例を示します。

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>互換性のないドライバーを削除する

このグループにステップを追加して、この Windows 10 のバージョンと互換性のないすべてのドライバーを削除します。  

### <a name="removesuspend-third-party-security"></a>サード パーティ セキュリティの削除/停止

このグループにステップを追加して、サード パーティ セキュリティ プログラム (ウイルス対策など) を削除または停止します。  

サード パーティのディスク暗号化プログラムを使用している場合は、`/ReflectDrivers`[コマンド ライン オプション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers)で、Windows セットアップにその暗号化ドライバーを提供します。 [[タスク シーケンス変数の設定]](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) ステップを、このグループのタスク シーケンスに追加します。 タスク シーケンス変数を **OSDSetupAdditionalUpgradeOptions** に設定します。 値をドライバーへのパス `/ReflectDrivers` に設定します。 この[タスク シーケンス変数](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)は、タスク シーケンスで使用される Windows セットアップ コマンド ラインを追加します。 このプロセスの他のガイダンスについては、ソフトウェアの製造元にお問い合わせください。  

### <a name="download-package-content-task-sequence-step"></a>パッケージ コンテンツのダウンロードのタスク シーケンスのステップ  

以下のシナリオでは、**オペレーティング システムのアップグレード**のステップの前に、[パッケージ コンテンツのダウンロード](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)のステップを使います。  

- X86 と x64 の両方のプラットフォームで 1 つのアップグレード タスク シーケンスを使用します。 **[アップグレードの準備]** グループで 2 つの **[パッケージ コンテンツのダウンロード]** ステップを含めます。 クライアント アーキテクチャを検出するために各ステップで条件を設定します。 この条件により、ステップでは適切な OS アップグレード パッケージのみがダウンロードされるようになります。 同じ変数を使用するようにそれぞれの **[パッケージ コンテンツのダウンロード]** ステップを構成して、 **[オペレーティング システムのアップグレード]** ステップ上のメディア パスにその変数を使用します。  

- 該当するドライバー パッケージを動的にダウンロードするには、ドライバー パッケージごとに適切なハードウェアの種類を検出する条件を含む 2 つの **[パッケージ コンテンツのダウンロード]** ステップを使用します。 同じ変数を使用するように **[パッケージ コンテンツのダウンロード]** ステップをそれぞれ構成します。 その後、 **[オペレーティング システムのアップグレード]** ステップのドライバー セクションの **[ステージング済みコンテンツ]** 値でその変数を使用します。  

    > [!NOTE]  
    > Configuration Manager によって、この変数名に数字のサフィックスが追加されます。 たとえば、カスタム変数として `%mycontent%` を指定した場合、クライアントは参照されているすべてのコンテンツをこの場所に格納します。 **[オペレーティング システムのアップグレード]** などのサブシーケンス ステップで変数を参照するときに、数字のサフィックスと共にこの変数を使用します。 この例では、`%mycontent01%` または `%mycontent02%` のようになります。この数字は、 **[パッケージ コンテンツのダウンロード]** ステップでこの特定のコンテンツがリストされる順序に対応しています。  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>推奨される処理後のタスク シーケンス ステップ

タスク シーケンスを作成した後で、これらの追加ステップを、**後処理**のタスク シーケンスのグループに追加します。  

> [!NOTE]  
> このタスク シーケンスは直線的ではありません。 タスク シーケンスの結果に影響を与えるステップの条件があります。 この動作は、クライアント コンピューターを正常にアップグレードするかどうか、または元の OS にクライアント コンピューターをロールバックする必要があるかによって異なります。  

Windows 10 の一括アップグレード用の既定のタスク シーケンス テンプレートに、アップグレード プロセスの後に追加する推奨アクションを含む追加グループが含まれます。 **[後処理]** グループのこれらのアクションは、Windows 10 にデバイスを正常にアップグレードしている多くのユーザーに共通するものです。 これらの操作がまだ含まれていない既存のタスク シーケンスがある場合は、タスク シーケンスの **[後処理]** グループにこれらを手動で追加します。  

### <a name="apply-setup-based-drivers"></a>セットアップ ベースのドライバーを適用する

このグループにステップを追加して、パッケージからセットアップ ベースのドライバー (.exe) をインストールします。  

### <a name="installenable-third-party-security"></a>サード パーティ セキュリティのインストール/有効化

このグループにステップを追加して、サード パーティ セキュリティ プログラム (ウイルス対策など) をインストールまたは有効にします。  

### <a name="set-windows-default-apps-and-associations"></a>Windows の既定のアプリと関連付けを設定する

このグループにステップを追加して、Windows の既定のアプリとファイルの関連付けを設定します。

1. 必要なアプリの関連付けで参照コンピューターを準備します。
1. 次のコマンド ラインを実行してエクスポートします。  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. XML ファイルをパッケージに追加します。
1. [[コマンド ラインの実行]](../understand/task-sequence-steps.md#BKMK_RunCommandLine) ステップをこのグループに追加します。 XML ファイルを含むパッケージを指定し、次のコマンド ラインを指定します。  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

詳細については、「[Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)」(既定のアプリケーションの関連付けをエクスポートまたはインポートする) を参照してください。

### <a name="apply-customizations-and-personalization"></a>カスタマイズと個人用設定を適用する

このグループにステップを追加して、[スタート] メニューのカスタマイズ (プログラム グループの整理など) を適用します。 詳細については、「[Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen)」(スタート画面をカスタマイズする) を参照してください。  


## <a name="optional-task-sequence-steps-for-rollback"></a>オプションのロールバックのタスク シーケンスのステップ  

コンピューターの再起動後にアップグレード プロセスで問題が発生すると、Windows セットアップは前の OS にシステムをロールバックします。 その後、タスク シーケンスは**ロールバック** グループのすべてのステップを続行します。 タスク シーケンスの作成後に、必要に応じてこのグループにステップを追加します。 たとえば、互換性のないソフトウェアをアンインストールするなど、[アップグレードの準備] グループで、システムに加えられた変更を取り消します。


## <a name="recommended-task-sequence-steps-on-failure"></a>失敗時の推奨されるタスク シーケンス ステップ

<!--1358500-->
バージョン 1806 以降では、Windows 10 の一括アップグレード用の既定のタスク シーケンス テンプレートには、**失敗時にアクションを実行**するためのグループが含まれます。 このグループには、アップグレード プロセスが失敗した場合に追加することが推奨されるアクションが含まれます。 これらのアクションによって、トラブルシューティングが容易になりました。

### <a name="collect-logs"></a>ログの収集

クライアントからログを収集するには、このグループに手順を追加します。  

- 通常は、ログ ファイルをネットワーク共有にコピーします。 この接続を確立するには、[ネットワーク フォルダーへの接続](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)の手順を使用します。  

- コピー操作を実行するには、「[コマンド ラインの実行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)」または「[PowerShell スクリプトの実行](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)」の手順のどちらかに従って、カスタム スクリプトまたはユーティリティを使用します。  

- 収集するファイルには、次のログ ファイルが含まれる可能性があります。  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- setupact.log および他の Windows Setup ログ ファイルの詳細については、[Windows 設定ログ ファイル](https://docs.microsoft.com/windows/deployment/upgrade/log-files)に関するページをご覧ください。  

- 構成マネージャー クライアントのログ ファイルについて詳しくは、「[Configuration Manager クライアントのログ ファイル](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs)」をご覧ください。  

- **_SMSTSLogPath** および他の便利な変数について詳しくは、「[タスク シーケンス変数](../understand/task-sequence-variables.md)」をご覧ください。  

### <a name="run-diagnostic-tools"></a>診断ツールの実行

追加の診断ツールを実行するには、このグループで手順を追加します。 失敗後すぐにシステムから追加情報を収集するために、これらのツールを自動化します。  

このようなツールの 1 つが、Windows の [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) です。 これは、Windows 10 がアップグレードに失敗した詳細な理由を取得する、スタンドアロンの診断ツールです。  

- Configuration Manager で、ツールの[パッケージを作成](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program)します。  

- [コマンド ラインの実行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)手順を、タスク シーケンスのこのグループに追加します。 **[パッケージ]** オプションを使用して、ツールを参照します。 次の文字列は、**コマンド ライン**のサンプルです。  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`  

> [!TIP]
> 最新の機能と既知の問題の修正を利用するために、常に最新バージョンの SetupDiag を使用してください。 詳細については、「[SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag)」をご覧ください。

## <a name="additional-recommendations"></a>その他の推奨事項

### <a name="windows-documentation"></a>Windows のドキュメント

Windows のドキュメント「[Windows 10 のアップグレード エラーの解決](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)」を参照してください。 この記事には、アップグレード プロセスに関する詳細情報も含まれています。  

### <a name="check-minimum-disk-space"></a>最小ディスク領域を確認する

既定の **[準備の確認]** ステップで、 **[最小空きディスク容量 (MB) を満たすことを確認する]** を有効にします。 値を、32 ビット OS のアップグレード パッケージの場合は **16384** (16 GB) 以上、64 ビットの場合は **20480** (20 GB) 以上に設定します。  

### <a name="retry-downloading-policy"></a>ポリシーのダウンロードを再試行する

**SMSTSDownloadRetryCount**[ タスク シーケンス変数](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount)を使用して、ポリシーのダウンロードを再試行します。 現在の既定では、クライアントは 2 回再試行します。この変数は 2 に設定されます。 クライアントがイントラネット ネットワークに有線接続されていない場合は、再試行回数を増やすと、クライアントがポリシーを取得するのに役立ちます。 この変数を使っても、ポリシーをダウンロードできない場合の障害の遅延以外に、悪影響はありません。<!--501016--> また、**SMSTSDownloadRetryDelay** 変数を既定値の 15 秒から増やします。  

### <a name="perform-an-inline-compatibility-assessment"></a>インライン互換性評価を実行する

1. **[アップグレードの準備]** グループの早い段階に、第 2 の **[オペレーティング システムのアップグレード]** ステップを追加します。  

    1. その名前を "*アップグレード評価*" にします。
    1. 同じアップグレード パッケージを指定し、 **[アップグレードを開始せずに Windows セットアップの互換性スキャンを実行する]** オプションを有効にします。
    1. [オプション] タブで **[エラー時に続行する]** を有効にします。  

1. この "*アップグレード評価*" ステップの直後に、 **[コマンド ラインの実行]** ステップを追加します。 次のコマンド ラインを指定します。

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

    このコマンドによって、コマンド プロンプトが指定されたゼロ以外の終了コードで終了されます。これは、タスク シーケンスによってエラーと見なされます。

1. **[オプション]** タブで、次の条件を追加します。

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

    この条件は、リターン コードが成功コードではない場合、タスク シーケンスによってこの **[コマンド ラインの実行]** ステップのみが実行されることを意味します。

リターン コード `3247440400` は MOSETUP_E_COMPAT_SCANONLY (0xC1900210) に相当する 10 進数で、互換性スキャンが成功して問題がなかったことを示します。 "*アップグレード評価*" ステップが成功して `3247440400` が返された場合、タスク シーケンスではこの **[コマンド ラインの実行]** ステップがスキップされ、続行されます。 評価手順から他のリターン コードが返された場合は、この **[コマンド ラインの実行]** ステップが実行されます。 コマンドはゼロ以外のリターン コードで終了するため、タスク シーケンスも失敗します。 タスク シーケンスのログとステータス メッセージには、Windows セットアップ互換性スキャンからのリターン コードが含まれます。 **_SMSTSOSUpgradeActionReturnCode** について詳しくは、「[タスク シーケンス変数](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)」をご覧ください。

詳細については、「[オペレーティング システムのアップグレード](../understand/task-sequence-steps.md#BKMK_UpgradeOS)」タスク シーケンス ステップを参照してください。

### <a name="convert-from-bios-to-uefi"></a>BIOS から UEFI に変換する

このタスク シーケンスの間にデバイスを BIOS から UEFI に変更する場合は、「[インプレース アップグレード時に BIOS から UEFI に変換する](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)」を参照してください。  

### <a name="manage-bitlocker"></a>BitLocker の管理

<!--SCCMDocs issue #494-->
BitLocker Disk Encryption を使っている場合、Windows セットアップはアップグレード中にそれを既定で自動的に一時停止します。 Windows 10 バージョン 1803 以降、Windows セットアップにはこの動作を制御するための `/BitLocker` コマンド ライン パラメーターが含まれます。 セキュリティ要件のためディスク暗号化を常にアクティブに維持する必要がある場合は、**アップグレードの準備**グループの **OSDSetupAdditionalUpgradeOptions** [タスク シーケンス変数](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)を使用して、`/BitLocker TryKeepActive` を含めます。 詳しくは、「[Windows セットアップ コマンド ライン オプション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker)」をご覧ください。

### <a name="remove-default-apps"></a>既定のアプリを削除する

<!--SCCMDocs issue #526-->
お客様によっては、Windows 10 に既定でプロビジョニングされるアプリを削除することがあります。 たとえば、Bing 天気アプリや Microsoft Solitaire Collection などです。 状況によっては、Windows 10 の更新後にこれらのアプリが戻る場合があります。 詳しくは、「[How to keep apps removed from Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update)」(Windows 10 から削除されたアプリを維持する方法) をご覧ください。

**アップグレードの準備**グループのタスク シーケンスに**コマンド ラインの実行**ステップを追加します。 次の例のようなコマンド ラインを指定します。

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
