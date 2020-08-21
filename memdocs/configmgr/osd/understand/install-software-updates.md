---
title: ソフトウェア更新プログラムのインストール
titleSuffix: Configuration Manager
description: Configuration Manager でソフトウェア更新プログラムのインストールのタスク シーケンス ステップを使用するための推奨事項。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 73acd43ef9d7924682de9df66487c5a04297e640
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697502"
---
# <a name="install-software-updates"></a>ソフトウェア更新プログラムのインストール

*適用対象:Configuration Manager (Current Branch)*

**ソフトウェア更新プログラムのインストール** ステップは、Configuration Manager のタスク シーケンスでよく使用されます。 OS をインストールまたは更新すると、更新プログラムをスキャンして展開するようにソフトウェアの更新コンポーネントがトリガーされます。 一部のお客様には、このステップにより長いタイムアウトの遅延や更新プログラムの失敗などの問題が発生する場合があります。 この記事の情報を使用して、このステップで生じる一般的な問題を軽減し、問題が発生した時のトラブルシューティングに役立ててください。

このステップの詳細については、「[ソフトウェア更新プログラムのインストール](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)」を参照してください。



## <a name="recommendations"></a>推奨事項

このプロセスを成功させるため、次の推奨事項を使用してください。

- [オフライン サービスを使用する](#use-offline-servicing)
- [1 つのインデックス](#single-index)
- [イメージ サイズの削減](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>オフライン サービスを使用する

Configuration Manager を使用して、適用可能なソフトウェア更新プログラムを定期的にイメージ ファイルにインストールします。 これにより、タスク シーケンス中にインストールする必要のある更新プログラムの数が減ります。

詳しくは、「[ソフトウェア更新プログラムをイメージに適用](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)」をご覧ください。

### <a name="single-index"></a>1 つのインデックス

多くのイメージ ファイルには、Windows の各エディションなど、複数のインデックスが含まれています。 イメージ ファイルを減らして必要な 1 つのインデックスにします。 これにより、イメージにソフトウェア更新プログラムを適用する時間が短縮されます。 また、次の推奨事項でイメージ サイズを削減できるようになります。

バージョン 1902 以降では、OS イメージをサイトに追加すると、このプロセスが自動化されます。 詳細については、「[Add an OS image](../get-started/manage-operating-system-images.md#BKMK_AddOSImages)」 (OS イメージの追加) を参照してください。<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a> イメージ サイズの削減

イメージにソフトウェア更新プログラムを適用するときに、置き換えられた更新プログラムを削除することによって出力を最適化します。 DISM コマンドライン ツールを使用します。次に例を示します。

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

バージョン 1902 以降では、このプロセスを自動化する新しいオプションがあります。 詳細については、「[Optimized image servicing](../get-started/manage-operating-system-images.md#bkmk_resetbase)」 (最適化されたイメージ サービス) を参照してください。<!--3555951-->


## <a name="image-engineering-decisions"></a>イメージ エンジニアリングの決定

イメージ プロセスを設計するときに、ソフトウェア更新プログラムのインストールに影響する可能性があるオプションがいくつかあります。

- [イメージを定期的に再キャプチャする](#bkmk_goldimage)  
- [オフライン サービスを使用する](#bkmk_offline)  
- [既定のイメージのみを使用する](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a> イメージを定期的に再キャプチャする

カスタム OS イメージを定期的にキャプチャするために自動化されたプロセスがあります。 このキャプチャ タスク シーケンスでは、最新のソフトウェア更新プログラムがインストールされます。 これらの更新プログラムには、累積的および非累積的な更新プログラムに加え、サービス スタックの更新プログラム (SSU) などのその他の重要な更新プログラムを含めることができます。 展開タスク シーケンスでは、キャプチャ後に追加されたすべての更新プログラムがインストールされます。

このプロセスの詳細については、[OS をキャプチャするタスク シーケンスの作成](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)に関するページをご覧ください。

#### <a name="advantages"></a>長所

- 展開時にクライアントあたりに適用する更新プログラムの数が少なくなるため、展開時の時間と帯域幅を節約できる
- 再起動が発生する更新プログラムが少なくなる
- 組織用にカスタマイズされたイメージ
- 展開時の変数が少なくなる

#### <a name="disadvantages"></a>短所

- ほぼ自動化されている場合でも、イメージの作成とキャプチャに時間がかかる
- イメージを配布ポイントに配布する時間が長くなるため、アクティブな展開が停止しているとみなされる可能性がある
- 実稼働前環境でテストを完了する時間が OS のパッチ サイクルよりも長くなる場合があり、更新されたイメージが無関係になる場合がある


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a> オフライン サービスを使用する

ソフトウェア更新プログラムをイメージに適用するように Configuration Manager をスケジュールします。

詳しくは、「[ソフトウェア更新プログラムをイメージに適用](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)」をご覧ください。

#### <a name="advantages"></a>長所

- 展開時にクライアントあたりに適用する更新プログラムの数が少なくなるため、展開時の時間と帯域幅を節約できる
- 再起動が発生する更新プログラムが少なくなる
- サイトでサービス プロセスをスケジュールすることができる

#### <a name="disadvantages"></a>短所

- 更新プログラムを手動で選択する
- イメージを配布ポイントに配布する時間が長くなる
- CBS ベースの更新プログラムしかサポートされない。 Microsoft 365 アプリの更新プログラムを適用することはできません。

> [!Tip]  
> PowerShell を使用してソフトウェア更新プログラムの選択を自動化することができます。 [Get-CMSoftwareUpdate](/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) コマンドレットを使用して、更新プログラムのリストを取得します。 [New-CMOperatingSystemImageUpdateSchedule](/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) コマンドレットを使用して、オフライン サービスのスケジュールを作成します。 次の例は、このアクションを自動化する 1 つのメソッドを示しています。
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a> 既定のイメージのみを使用する

展開タスク シーケンスで既定の Windows install.wim イメージ ファイルを使用します。

#### <a name="advantages"></a>長所

- イメージ破損のリスクを潜在的な問題として軽減する既知の正常なソース
- イメージへの変更を潜在的な問題として排除する

#### <a name="disadvantages"></a>短所

- 展開時に更新プログラムのボリュームが大きくなる可能性がある
- すべてのデバイスで展開時間が増える
- カスタマイズが必要ない場合でも、カスタマイズするための追加のタスク シーケンス ステップが要求される



## <a name="flowchart"></a>フローチャート

このフローチャート図は、タスク シーケンスにソフトウェア更新プログラムのインストール ステップを含める場合のプロセスを示しています。

[図をフル サイズで表示する](media/ts-step-install-software-updates.svg)

![ソフトウェア更新プログラムのインストール タスク シーケンス ステップのフローチャート図](media/ts-step-install-software-updates.svg)  

1. **クライアントでプロセスを開始する**:クライアントで実行されるタスク シーケンスには、ソフトウェア更新プログラムのインストールのステップが含まれています。
2. **コンパイルと評価ポリシー**:クライアントがすべてのソフトウェア更新プログラム ポリシーを WMI RequestedConfigs 名前空間にコンパイルします。 (CIAgent.log)
3. *これは初めて呼び出されたインスタンスか?*  
    1. **Yes**:**フル スキャン**に進む  
    2. **No**:*ステップがオプションにより [[キャッシュされているスキャン結果からソフトウェア更新プログラムを評価する]](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results) ように構成されているか?*
        1. **Yes**:**キャッシュされた結果からのスキャン**に進む
        2. **No**:**フル スキャン**に進む
4. スキャン プロセス: フル スキャンまたはキャッシュされた結果からのスキャンを、監視処理と並列で実行します。
    1. **フル スキャン**:タスク シーケンス エンジンが Update Scan API を使用してソフトウェア更新プログラム エージェント呼び出し、*フル*スキャンを実行します。 (WUAHandler.log、ScanAgent.log)  
        1. **SUM エージェント スキャン - フル**:WSUS を実行しているソフトウェアの更新ポイントと通信する Windows Update エージェント (WUA) を使用した通常のスキャン プロセス。 適用可能な任意の更新プログラムをローカルの更新ストアに追加します。 (WindowsUpdate.log、UpdateStore.log)
    2. **キャッシュされた結果からのスキャン**:タスク シーケンス エンジンが Update Scan API を使用してソフトウェア更新プログラム エージェント呼び出し、キャッシュされたメタデータに対してスキャンを実行します。 (WUAHandler.log、ScanAgent.log)
        1. **SUM エージェント スキャン - キャッシュ済み**:Windows Update エージェント (WUA) がローカルの更新ストアにすでにキャッシュされている更新プログラムに対して更新プログラムのチェックを行います。 (WindowsUpdate.log、UpdateStore.log)
    3. **スキャン タイマーの開始**:タスク シーケンス エンジンがタイマーを開始して待機します。 (このプロセスは、フル スキャンまたはキャッシュされた結果からのスキャンのいずれかと並列で実行されます。)
        1. **監視**:タスク シーケンス エンジンが SUM エージェントの状態を監視します。
        2. *SUM エージェントからの応答は何か?*
            - **進行中**:タイマーがタスク シーケンス変数 [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout) の値に達しているか? (既定値は 1 時間)
                - **Yes**:ステップが失敗
                - **No**:**監視**に進む
            - **失敗**:ステップが失敗
            - **完了**: **更新リストの列挙**に進む
5. **更新リストの列挙**:SUM エージェントが、スキャンによって返された更新プログラムのリストを列挙し、使用可能または必須の更新プログラムを判断します。
6. *スキャン結果のリストに、更新プログラムはあるか?*
    - **Yes**:**更新プログラムのインストール**に進む
    - **No**:何もインストールされず、ステップは正常に完了します。
7. 展開プロセス:更新プログラムのインストール プロセスは、展開の監視プロセスと並列で行われます。
    1. **更新プログラムのインストール**:タスク シーケンス エンジンが Update Scan API を使用して SUM エージェント呼び出し、使用可能なすべての更新プログラムまたは必須の更新プログラムのみをインストールします。 この動作は、ステップの構成で、 **[インストールが必要 - 必須のソフトウェア更新プログラムのみ]** または **[インストールが可能 - すべてのソフトウェア更新プログラム]** を選択したかどうかによって決まります。 この動作は、[SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget) 変数を使用して指定することもできます。
        1. **SUM エージェントのインストール**:標準のコンテンツをダウンロードする、更新プログラムのキャッシュされた既存のリストを使用した標準のインストール プロセス。 Windows Update エージェント (WUA) を使用して更新プログラムをインストールします。 (UpdatesDeployment.log、UpdatesHandler.log、WuaHandler.log、WindowsUpdate.log)
    2. **展開タイマーを開始して進行状況を表示する**:タスク シーケンス エンジンがインストール タイマーを開始し、TS 進行状況 UI に 10% 間隔でサブの進行状況を表示して待機します。
        1. **監視**:タスク シーケンス エンジンが SUM エージェントをポーリングして状態を確認します。
        2. *SUM エージェントからの応答は何か?*
            - **進行中**:*インストール プロセスが 8 時間非アクティブになっているか?*
                - **Yes**:ステップが失敗
                - **No**:**監視**に進む
            - **失敗**:ステップが失敗
            - **完了**: *ステップがオプションにより **[キャッシュされているスキャン結果からソフトウェア更新プログラムを評価する]** ように構成されているか?* に進む


### <a name="timeouts"></a>タイムアウト

図には、このステップに適用される 2 つのタイムアウト変数が含まれています。 他にも、このプロセスに影響するその他のコンポーネントからの標準的なタイマーがあります。

- 更新プログラム スキャンのタイムアウト:1 時間 (smsts.log)  
- 場所の要求のタイムアウト:1 時間 (LocationServices.log、CAS.log)  
- コンテンツ ダウンロードのタイムアウト:1 時間 (DTS.log)  
- 非アクティブの配布ポイントのタイムアウト:1 時間 (LocationServices.log、CAS.log)  
- インストールの非アクティブなタイムアウト合計:8 時間 (smsts.log)  



## <a name="troubleshooting"></a>トラブルシューティング

このステップでの問題のトラブルシューティングに役立つリソースと追加情報を次に示します。

- ソフトウェアの更新プログラムの展開先が、タスク シーケンスの展開と同じコレクションになっていることを確認します。  

- 境界グループにソフトウェアの更新ポイントが含まれていることを確認します。 詳細については、[Microsoft サポート記事](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager)を参照してください。  

- ソフトウェア更新プログラムの管理プロセスをトラブルシューティングするには、[ソフトウェアの更新管理のトラブルシューティング](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager)に関するページを参照してください。  

- 全体的なパフォーマンスを向上させるには、ソフトウェア更新プログラム カタログのサイズを小さくします。 次に例を示します。  

    - 不要な分類、製品、および言語を削除します。 詳細については、「[同期する分類と製品の構成](../../sum/get-started/configure-classifications-and-products.md)」を参照してください。  

    - サイト データベースのインデックスを再作成し、統計を再構築します。 詳細については、[Configuration Manager のパフォーマンスとスケールのガイダンス ホワイトペーパー](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e)を参照してください。  

    - 不要な更新プログラムを拒否します。次に例を示します。
        - 置き換え済み (バージョン 1810 以降では、このアクションは Configuration Manager で実行されます。 詳細については、「[バージョン 1810 以降の WSUS クリーンアップ動作](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)」を参照してください。)
        - Itanium
        - ベータ版
        - 次のバージョン
        - ARM
        - 展開していない Windows のバージョン