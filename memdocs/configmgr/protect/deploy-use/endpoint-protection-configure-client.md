---
title: Endpoint Protection のクライアント設定
titleSuffix: Configuration Manager
description: Endpoint Protection のカスタム クライアント設定を構成する方法を説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709180"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Endpoint Protection のカスタム クライアント設定を構成する

*適用対象:Configuration Manager (Current Branch)*

この手順では、階層内のデバイスのコレクションに展開できる Endpoint Protection のカスタム クライアント設定を構成します。

> [!IMPORTANT]  
>  階層内のすべてのコンピューターに適用する場合にのみ、既定の Endpoint Protection クライアント設定を構成します。 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Endpoint Protection を有効にしてカスタム クライアント設定を構成するには

1. Configuration Manager コンソールで、 **[管理]** をクリックします。  

2. **[管理]** ワークスペースで **[クライアント設定]** をクリックします。  

3. **[ホーム]** タブの **[作成]** グループで、 **[カスタム クライアント デバイス設定の作成]** をクリックします。  

4. **[カスタム クライアント デバイス設定の作成]** ダイアログ ボックスで、設定のグループの名前と説明を指定し、 **[Endpoint Protection]** を選択します。  

5. 必要な Endpoint Protection クライアント設定を構成します。 構成できる Endpoint Protection クライアント設定の完全な一覧については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#endpoint-protection)」の「Endpoint Protection」セクションを参照してください。  

   > [!IMPORTANT]  
   >  Endpoint Protection のクライアント設定を構成するには、事前に Endpoint Protection サイト システムの役割をインストールします。  

6. **[OK]** をクリックして **[カスタム クライアント デバイス設定の作成]** ダイアログ ボックスを閉じます。 新しいクライアント設定は、 **[管理]** ワークスペースの **[クライアント設定]** ノードに表示されます。  

7. 次に、カスタム クライアント設定をコレクションに展開します。 展開するカスタム クライアント設定を選択します。 **[ホーム]** タブの **[クライアント設定]** グループで、 **[展開]** をクリックします。  

8. **[コレクションの選択]** ダイアログ ボックスで、クライアント設定を展開するコレクションを選択し、 **[OK]** をクリックします。 新しい展開は、詳細ウィンドウの **[展開]** タブに表示されます。  

クライアントは、次回クライアント ポリシーをダウンロードしたときに、これらの設定を使用して構成されます。 詳細については、「[Configuration Manager クライアントのポリシーの取得開始](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」を参照してください。  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Endpoint Protection クライアントをディスク イメージにプロビジョニングする方法

Configuration Manager の OS の展開でディスク イメージ ソースとして使用するコンピューターに、Endpoint Protection クライアントをインストールします。 このコンピューターは通常、参照コンピューターと呼ばれます。 OS イメージを作成した後、Configuration Manager の OS 展開を使用してイメージを展開します。

> [!Important]  
> Windows 10 および Windows Server 2016 には Windows Defender が既定でインストールされています。 これらのバージョンの Windows では、この手順は不要です。  

次の手順に従って、参照コンピューターに Endpoint Protection クライアントをインストールして構成できます。


### <a name="prerequisites"></a>[前提条件]

以下に、参照コンピューターに Endpoint Protection クライアント ソフトウェアをインストールするために必要な前提条件を示します。

- Endpoint Protection クライアント インストール パッケージ **scepinstall.exe** にアクセスできる必要があります。 サイト サーバー上の Configuration Manager インストール フォルダーの **Client** フォルダーでこのパッケージを探します。  

- 組織の必須の構成で Endpoint Protection クライアントを展開するには、マルウェア対策ポリシーを作成し、エクスポートします。 その後、Endpoint Protection クライアントを手動でインストールするときに、このポリシーを指定します。 詳細については、[マルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)に関する記事を参照してください。  

  > [!NOTE]  
  >  **[既定のクライアント マルウェア対策ポリシー]** をエクスポートすることはできません。  

- Endpoint Protection クライアントを最新の定義でインストールする場合は、[Windows Defender Security Intelligence](https://www.microsoft.com/wdsi) のページからダウンロードします。  

> [!NOTE]  
> Configuration Manager 1802 以降、Windows 10 デバイスには、Endpoint Protection エージェント (SCEPInstall) をインストールする必要がありません。 Windows 10 デバイスに既にインストールされている場合、Configuration Manager では削除されません。 管理者は、少なくとも 1802 クライアント バージョンで実行されている Windows 10 デバイス上の Endpoint Protection エージェントを削除できます。 SCEPInstall.exe は、一部のマシンの C:\Windows\ccmsetup 上に引き続き存在する可能性がありますが、新しいクライアントのインストールにはダウンロードされない必要があります。 <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>参照コンピューターに Endpoint Protection クライアントをインストールする方法

コマンド プロンプトから、Endpoint Protection クライアントを参照コンピューターにローカルにインストールします。 まず、インストール ファイル **scepinstall.exe** を取得します。 詳細については、「[コマンド プロンプトで Endpoint Protection クライアントをインストールするには](#bkmk_manual-install)」を参照してください。

必要に応じて、事前に構成したマルウェア対策ポリシーまたは先にエクスポートしたマルウェア対策ポリシーを含めることもできます。 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a> コマンド プロンプトで Endpoint Protection クライアントをインストールするには

1. Configuration Manager インストール フォルダーの **Client** フォルダーから、Endpoint Protection クライアント ソフトウェアをインストールするコンピューターに **scepinstall.exe** をコピーします。  

2. コマンド プロンプトを管理者として開きます。 ディレクトリをインストーラーが格納されているフォルダーに変更します。 次に、必要な他のコマンド ライン プロパティを追加して `scepinstall.exe` を実行します。


   |  プロパティ   |                                  [説明]                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           インストーラーをサイレント モードで実行します                           |
   |    `/q`     |                        セットアップ ファイルをサイレント モードで抽出します                        |
   |    `/i`     |                           インストーラーを通常どおり実行します                           |
   |  `/policy`  | インストール時にクライアントを構成するためのマルウェア対策ポリシー ファイルを指定します |
   | `/sqmoptin` |     カスタマー エクスペリエンス向上プログラム (CEIP) に参加することを選択します     |


3. 画面に表示される指示に従って、クライアントのインストールを完了します。  

4. 最新の更新定義パッケージをダウンロードしている場合、パッケージをクライアント コンピューターにコピーしてから、定義パッケージをダブルクリックしてインストールします。  

   > [!NOTE]  
   >  Endpoint Protection クライアントのインストールが完了すると、クライアントで定義の更新チェックが自動的に実行されます。 この更新チェックが成功した場合は、最新の定義更新パッケージを手動でインストールする必要はありません。  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>例: マルウェア対策ポリシーを使用してクライアントをインストールする

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Endpoint Protection クライアントのインストールの確認

参照コンピューターに Endpoint Protection クライアントをインストールしたら、クライアントが正しく機能していることを確認します。

1.  参照コンピューターで、Windows 通知領域から **[System Center Endpoint Protection]** を開きます。  

2.  **[System Center Endpoint Protection]** ダイアログ ボックスの **[ホーム]** タブで、 **[リアルタイム保護]** が **[オン]** に設定されていることを確認します。  

3.  **[ウイルス定義およびスパイウェアの定義]** で **[最新]** が表示されていることを確認します。  

4.  参照コンピューターのイメージングの準備ができていることを確認するには、 **[スキャン オプション]** で **[フル]** を選択してから、 **[今すぐスキャン]** をクリックします。  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Endpoint Protection クライアントのイメージングの準備

Endpoint Protection クライアントのイメージングを準備するには、次の手順を実行します。

1. 参照コンピューターで管理者としてサインインします。  

2. **PsExec** を [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec) からダウンロードしてインストールします。  

3. コマンド プロンプトを管理者として実行し、PsTools をインストールしたフォルダーにディレクトリを変更し、次のコマンドを入力します。  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  この方法でレジストリ エディターを実行する場合は、ご注意ください。 PsExec.exe は、これを LocalSystem のコンテキストで実行します。  

4. レジストリ エディターで、次のレジストリ キーを削除します。  

   > [!IMPORTANT]  
   >  これらのレジストリ キーの削除は、参照コンピューターをイメージングする前の最後の手順として行います。 Endpoint Protection クライアントでは、開始時にこれらのキーが再作成されます。 参照コンピューターを再起動する場合は、レジストリ キーをもう一度削除します。  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

これで、参照コンピューターのイメージングを準備できるようになりました。

Endpoint Protection クライアントを含む OS イメージを展開するときに、デバイスの割り当て済み Configuration Manager サイトに情報が自動的に報告されます。 クライアントは、任意の対象となるマルウェア対策ポリシーをダウンロードし、適用します。  



## <a name="see-also"></a>関連項目

Configuration Manager での OS の展開について詳しくは、[OS イメージの管理](../../osd/get-started/manage-operating-system-images.md)に関する記事をご覧ください。

