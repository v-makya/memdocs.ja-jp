---
title: ソフトウェア更新プログラムの前提条件
titleSuffix: Configuration Manager
description: Configuration Manager でのソフトウェア更新プログラムの前提条件について説明します。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 4604b6d2c0396b9192c031264cffef8b8641d557
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696683"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Configuration Manager でのソフトウェア更新の前提条件

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager でのソフトウェア更新プログラムの前提条件の一覧を示します。 前提条件ごとに、外部の依存関係と内部の依存関係を別の表にまとめています。  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Configuration Manager 外部のソフトウェア更新プログラムの依存関係  
 次のセクションに、ソフトウェア更新の外部の依存関係の一覧を示します。  

### <a name="internet-information-services"></a>インターネット インフォメーション サービス  
 ソフトウェアの更新ポイント、管理ポイント、および配布ポイントを実行するには、サイト システム サーバーにインターネット インフォメーション サービス (IIS) がインストールされている必要があります。 詳細については、「[サイト システムの役割の前提条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)」を参照してください。  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 ソフトウェア更新プログラムの同期と、クライアントでのソフトウェア更新プログラムの適用性スキャンを行うには、Windows Server Update Services (WSUS) が必要です。 WSUS サーバーは、ソフトウェア更新ポイントの役割を作成する前にインストールする必要があります。 ソフトウェアの更新ポイントでは、次のバージョンの WSUS がサポートされています。  

- WSUS 10.0.14393 (Windows Server 2016 における役割)
- WSUS 10.0.17763 (Windows Server 2019 における役割) (Configuration Manager 1810 以降が必要)
- WSUS 6.2 および 6.3 (Windows Server 2012 および Windows Server 2012 R2 における役割)
  - Windows 10 のアップグレードを展開する場合、WSUS 6.2 および 6.3 には、[KB 3095113 および KB 3159706 (または同等の更新プログラム)](#BKMK_wsus2012) が必要です。

> [!NOTE]
> - 1 つのサイトにソフトウェアの更新ポイントが複数ある場合、すべてのポイントが同じバージョンの WSUS を実行するようにします。

### <a name="wsus-administration-console"></a>WSUS 管理コンソール  
ソフトウェアの更新ポイントがリモート サイトのシステム サーバー上にあり、WSUS がそのサイト サーバーにインストールされていない場合、Configuration Manager サイト サーバーには WSUS 管理コンソールが必要です。  

> [!IMPORTANT]  
> - サイト サーバーの WSUS バージョンは、ソフトウェアの更新ポイントで実行されている WSUS バージョンと同じにする必要があります。
> - WSUS 管理コンソールを使って WSUS の設定を構成しないでください。 Configuration Manager はソフトウェアの更新ポイントで実行されている WSUS のインスタンスに接続し、適切な設定を構成します。  


### <a name="windows-update-agent"></a>Windows 更新エージェント  
 クライアントが WSUS サーバーに接続できるようにするには、Windows Update エージェント (WUA) クライアントが必要です。 WUA は、コンプライアンスのスキャンに必要なソフトウェア更新プログラムの一覧を取得します。  

 Configuration Manager をインストールすると、最新バージョンの WUA がダウンロードされます。 次に、Configuration Manager クライアントをインストールすると、必要に応じて WUA がアップグレードされます。 インストールに失敗した場合は、別の方法で WUA をアップグレードする必要があります。  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Configuration Manager 内部のソフトウェア更新プログラムの依存関係  
 次のセクションに、Configuration Manager のソフトウェア更新の内部の依存関係の一覧を示します。  

### <a name="management-points"></a>管理ポイント  
 管理ポイントは、クライアント コンピューターと Configuration Manager サイト間で情報を転送します。 管理ポイントは、ソフトウェア更新プログラムに必要です。  

### <a name="software-update-points"></a>ソフトウェアの更新ポイント  
 Configuration Manager でソフトウェア更新プログラムを展開するには、ソフトウェアの更新ポイントを WSUS サーバーにインストールする必要があります。 詳細については、「[ソフトウェアの更新ポイントのインストールと構成](../get-started/install-a-software-update-point.md)」を参照してください。

### <a name="distribution-points"></a>配布ポイント  
 ソフトウェア更新プログラムのコンテンツを保存できる配布ポイントが必要です。 配布ポイントをインストールして、コンテンツを管理する方法の詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

### <a name="client-settings-for-software-updates"></a>ソフトウェア更新プログラムのクライアントの設定  
既定では、クライアントのソフトウェア更新プログラムは有効です。 クライアントがソフトウェア更新プログラムのコンプライアンスを評価する方法とタイミングを制御し、ソフトウェア更新プログラムのインストール方法を制御するために使用できるその他の設定があります。  

 詳細については、以下の記事を参照してください。  

- [ソフトウェア更新プログラムのクライアントの設定](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [ソフトウェア更新プログラムのクライアントの設定](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>レポート サービス ポイント  
 レポート サービス ポイントのサイト システムの役割は、ソフトウェア更新プログラムのレポートを表示できます。 この役割は任意ですが、使用することをお勧めします。 レポート サービス ポイントの作成方法の詳細については、[レポートの構成](../../core/servers/manage/configuring-reporting.md)に関するページを参照してください。  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a> WSUS 6.2 および 6.3 で必要な更新プログラム

WSUS 6.2 および 6.3 で**アップグレード**分類を同期するには、2 つの更新プログラムが必要です。 KB3095113 と KB3159706 がインストールされる前にこれらが同期されていた場合は、アップグレードのダウンロードまたは展開でエラーが発生することがあります。 考えられる問題に関する情報は、次のセクションにあります。  

- **アップグレード**分類を同期する前に、ソフトウェアの更新ポイントとサイト サーバーに、2015 年 10 月にリリースされた [KB 3095113](https://support.microsoft.com/kb/3095113) をインストールする必要があります。
  - この更新プログラムにより、**アップグレード**分類が有効になります。
- Windows 10 バージョン 1607 以降をサービスするには、[KB 3159706](https://support.microsoft.com/help/3159706) をインストールして構成する必要があります。 KB 3159706 は、2016 年 5 月にリリースされました。
  - この更新プログラムにより、WSUS が Windows 10 バージョン 1607 以降のアップグレードに使用されるファイルをネイティブに復号化できるようになります。

>[!IMPORTANT]
> KB 3095113 と KB 3159706 は、どちらも 2017 年 7 月以降の **Security Monthly Quality Rollup** に含まれています。 つまり、KB 3095113 および KB 3159706 は、ロールアップでインストールされている可能性があるため、インストール済みの更新プログラムとして表示されない可能性があります。 ただし、これらの更新プログラムのいずれかが必要な場合は、2017 年 10 月以降にリリースされた **Security Monthly Quality Rollup** をインストールすることをお勧めします。これには、WSUS の clientwebservice でのメモリ使用率を減らすための追加の WSUS 更新プログラムが含まれているからです。

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a> Windows 10 のアップグレードのダウンロードが、"エラー:証明書の署名が無効です" または 0xc1800118 で失敗する

このセクションに記載されている更新プログラムと問題は、Windows Server 2012 または Windows Server 2012 R2 のマシン (WSUS 6.2 および 6.3) で実行されている WSUS にのみ適用されます。 通常、このセクションに記載されている問題は、2017 年 7 月より前に WSUS をインストールし、最近**アップグレード**分類を有効にした場合にのみ表示されます。 ただし、他の状況でもこれらの問題が表示される場合があります。

### <a name="historical-information-about-kb-3095113"></a>KB 3095113 に関する履歴情報

 [KB 3095113](https://support.microsoft.com/kb/3095113) は、Windows 10 のアップグレードのサポートを WSUS に追加するために、2015 年 10 月に[修正プログラムとしてリリース](/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113)されました。 この更新プログラムにより、WSUS は Windows 10 の**アップグレード**分類で更新プログラムを同期および配布できるようになりました。

[KB 3095113](https://support.microsoft.com/kb/3095113) を最初にインストールせずにアップグレードを同期する場合、WSUS データベース (SUSDB) に使用できないデータを読み込みます。 アップグレードを適切に展開するには、そのデータをクリアする必要があります。 この状態の Windows 10 アップグレードは、ソフトウェア更新プログラムのダウンロード ウィザードを使用してダウンロードすることはできません。

ソフトウェア更新プログラムのダウンロード ウィザードの [完了] ページには、次のようなエラーが表示されます。

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

さらに、次のようなエラーが、PatchDownloader.log ファイルに記録されます。

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

以前は、これらのエラーが発生すると、[WSUS の解決手順](/archive/blogs/wsus/how-to-delete-upgrades-in-wsus)の変更されたバージョンを実行することで解決されました。 これらの手順は、KB 3159706 のインストール後に必要な手動の手順を実行しない場合の解決策に似ているため、両方の手順を 1 つの解決策として次のセクションにまとめました。

- [KB 3095113 または KB 3159706 をインストールする前にアップグレードの同期から回復するには](#bkmk_fix-upgrades)

### <a name="historical-information-about-kb-3159706"></a>KB 3159706 に関する履歴情報

KB 3148812 は、WSUS が Windows 10 パッケージのアップグレードに使用される .esd ファイルをネイティブに復号化できるようにするため、2016 年 4 月に最初にリリースされました。 [KB 3148812 は、一部の顧客で問題が発生](/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues)したため、[KB 3159706](https://support.microsoft.com/help/3159706) に置き換えられました。 Windows 10 バージョン 1607 以降のデバイスをサービスするには、すべてのソフトウェアの更新ポイントとサイト サーバーに KB 3159706 をインストールする必要があります。 ただし、KB をインストールした後に次の手動の手順を実行する必要があることを理解していないと、問題が発生する可能性があります。

1. 管理者特権でのコマンド プロンプトから `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` を実行します。
1. すべての WSUS サーバーで WSUS サービスを再起動します。

KB 3159706 にはインストール後に手動で実行する手順があること、または KB 3159706 をインストールする前に Windows 10 1607 のアップグレードで同期させることを理解していないと、WSUS コンソールへの接続に問題が発生し、アップグレードをそれぞれ展開することになります。 クライアントがアップグレード ファイルをダウンロードすると、[**0xC1800118** エラー コード](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus)が返されます。

解決手順は、KB 3095113 をインストールする前にアップグレードを同期する場合の解決策に似ているため、両方の手順を 1 つの解決策として次のセクションにまとめました。
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a> KB 3095113 または KB 3159706 をインストールする前にアップグレードの同期から回復するには

次の手順に従って、0xc1800118 エラーと "エラー:証明書の署名が無効です" の両方を解決します。

1. WSUS と Configuration Manager の両方で、**アップグレード**分類を無効にします。 この手順で指示されるまで同期が行われないようにします。  
   - 最上位サイトのソフトウェアの更新ポイント コンポーネントのプロパティで**アップグレード**分類をオフにします。
     - 詳細については、「[分類と製品の構成](../get-started/configure-classifications-and-products.md)」を参照してください。
   - [ **[オプション]** ページ](/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations)の **[製品と分類]** の下にある WSUS からの**アップグレード**分類をオフにするか、管理者として実行している PowerShell ISE を使用します。
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - WSUS データベースを複数の WSUS サーバー間で共有する場合は、データベースごとに 1 回だけ**アップグレード**をオフにする必要があります。  
1. 各 WSUS サーバーで、管理者特権でのコマンド プロンプトから `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` を実行します。 次に、すべての WSUS サーバーで WSUS サービスを再起動します。
   -  WSUS では、サービスが必要かどうかをチェックする前に、データベースが[シングル ユーザー モード](/sql/relational-databases/databases/set-a-database-to-single-user-mode)にされます。 サービスは、チェックの結果に基づいて実行されるか、実行されません。 その後、データベースはマルチユーザー モードに戻されます。 
   - WSUS データベースを複数の WSUS サーバー間で共有する場合は、データベースごとに 1 回だけこのサービスを行う必要があります。
1. 管理者として実行している PowerShell ISE を使用して、各 WSUS データベースからすべての Windows 10 アップグレードを削除します。
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. ソフトウェアの更新ポイントで使用されている各 WSUS データベースの tbFile テーブルからファイルを削除します。 WSUS データベースで、SQL Server Management Studio から次のコマンドを実行します。
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Configuration Manager の最上位サイトでソフトウェア更新プログラムの同期を開始し、完了するまで待ちます。 **アップグレード**を削除したときに Configuration Manager 分類を変更したため、完全な同期が発生します。 詳細については、「[ソフトウェア更新プログラムの同期](../get-started/synchronize-software-updates.md)」を参照してください。
1. ソフトウェアの更新ポイント コンポーネントのプロパティで**アップグレード**分類を選択します。 次に、別のソフトウェア更新プログラムの同期を開始して、**アップグレード**を WSUS と Configuration Manager に戻します。 WSUS で**アップグレード**分類を有効にする必要はありません。これは、Configuration Manager によって実行されます。
1. アップグレードのダウンロード時にクライアントが **0xC1800118** エラー コードを受信した場合は、Windows Update エージェントで使用されているデータ ストアを削除する必要があります。 デバイス上の非表示の ~BT フォルダーを削除することが必要になる場合もあります。 次回クライアントでスキャンが実行されるときは、差分ではなく WSUS サーバーに対してフル スキャンが実行されます。 次のサンプル スクリプトのような PowerShell スクリプトを使用することができます。  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>次のステップ
[ソフトウェア更新管理の準備](../get-started/prepare-for-software-updates-management.md)