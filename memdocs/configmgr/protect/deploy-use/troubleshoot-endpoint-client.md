---
title: Endpoint Protection に関するトラブルシューティング
titleSuffix: Configuration Manager
description: Windows Defender および Endpoint Protection の問題をトラブルシューティングする方法について説明します。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709420"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Windows Defender または Endpoint Protection クライアントのトラブルシューティング

*適用対象:Configuration Manager (Current Branch)*

Windows Defender または Endpoint Protection で問題が発生した場合、この記事を使用すると、次の問題をトラブルシューティングできます。  

- [Windows Defender または Endpoint Protection の更新](#update-windows-defender-or-endpoint-protection)  
- [Windows Defender または Endpoint Protection サービスの開始](#starting-windows-defender-or-endpoint-protection-service)  
- [インターネット接続の問題](#internet-connection-issues)  
- [検出された脅威を修復できない](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a>Windows Defender または Endpoint Protection の更新

### <a name="symptoms"></a>現象

Windows Defender または Endpoint Protection は、ウイルスおよびスパイウェアの定義を最新の状態に維持するために、自動的に Microsoft Update と連携して動作します。  

このセクションでは、次の状況を含む、自動更新に関するよくある問題について説明します。  

- 更新が失敗したというエラー メッセージが表示される。  

- 更新プログラムを確認するときに、ウイルスおよびスパイウェア定義の更新を確認、ダウンロード、またはインストールできないというエラー メッセージが表示される。  

- デバイスがインターネットに接続しているのに、更新が失敗する。  

- 更新プログラムがスケジュールどおりに自動的にインストールされない。  

### <a name="causes"></a>原因

更新に関する問題の最も一般的な原因は、インターネット接続の問題です。 他の Web サイトを閲覧できるため、デバイスがインターネットに接続されていることがわかっている場合は、Windows のインターネット設定との競合によって問題が発生している可能性があります。  

### <a name="options-to-resolve"></a>解決するためのオプション

#### <a name="step-1-reset-your-internet-settings"></a>手順 1:インターネットの設定をリセットする  

1. Web ブラウザーなど、開いているすべてのプログラムを終了します。  

    > [!NOTE]  
    > これらのインターネット設定をリセットすると、ブラウザーの一時ファイル、Cookie、閲覧の履歴、およびオンライン パスワードが削除されることがあります。 お気に入りは削除されません。  

2. **スタート** メニューにアクセスし、`inetcpl.cpl` を開きます。  

3. **[詳細設定]** タブに切り替えます。  

4. **[Internet Explorer の設定をリセット]** セクションで、 **[リセット]** を選択し、再び **[リセット]** を選択して確定します。  

5. 設定がリセットされたら **[OK]** を選択します。

6. Windows Defender の更新を再試行します。

問題が解決しない場合は、次の手順に進みます。  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>手順 2:コンピューターの日付と時刻が正しく設定されていることを確認する  

エラー メッセージにコード 0x80072f8f が含まれている場合、問題の原因はおそらく、コンピューターに設定されている日付または時刻が正しくないことです。 **スタート** メニューにアクセスし、 **[設定]** を選択し、 **[時刻と言語]** を選択し、 **[日付と時刻]** を選択します。

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>手順 3:コンピューターにあるソフトウェア配布フォルダーの名前を変更する  

1. **[Windows Update]** サービスを停止します。  

    1. **[スタート]** にアクセスし、**services.msc** を開きます。  

    2. **[Windows Update]** サービスを選択します。 **[操作]** メニューにアクセスし、 **[停止]** を選択します。

2. **SoftwareDistribution** ディレクトリの名前を変更します。  

    1. コマンド プロンプトを管理者として開きます。  

    2. 次のコマンドを入力します。

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. **[Windows Update]** サービスを再起動します。

    1. **[サービス]** ウィンドウに戻ります。  

    2. **[Windows Update]** サービスを選択します。 **[操作]** メニューにアクセスし、 **[開始]** を選択します。

    3. [サービス] ウィンドウを閉じます。  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>手順 4:コンピューターの Microsoft ウイルス対策更新エンジンをリセットする  

1. コマンド プロンプトを管理者として開きます。

2. 次のコマンドを入力します。

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. コンピューターを再起動します。  

4. Windows Defender の更新を再試行します。

問題が解決しない場合は、次の手順に進みます。  

#### <a name="step-5-manually-install-the-definition-updates"></a>手順 5:定義の更新プログラムを手動でインストールする  

[最新の更新プログラムを手動でダウンロードします](https://www.microsoft.com/en-us/wdsi/defenderupdates)。  

#### <a name="step-6-contact-microsoft-support"></a>手順 6:Microsoft サポートに問い合わせる  

これらの手順で問題が解決しなかった場合は、Microsoft サポートにお問い合わせください。 詳細については、「[サポート オプションとコミュニティ リソース](../../core/understand/find-help.md#BKMK_SupportOptions)」を参照してください。  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a>Windows Defender または Endpoint Protection サービスの開始

### <a name="symptom"></a>現象

"**Windows Defender または Endpoint Protection は、プログラムのサービスが停止しているためコンピューターを監視していません。今すぐサービスを再起動してください**" というメッセージが表示されます。

### <a name="solution"></a>解決策:

#### <a name="step-1-restart-your-computer"></a>手順 1:コンピューターを再起動する

すべてのアプリケーションを閉じて、コンピューターを再起動します。  

#### <a name="step-2-check-the-windows-service"></a>手順 2:Windows サービスを確認する

1. **[スタート]** にアクセスし、**services.msc** を開きます。  

2. **[Windows Defender Antivirus Service]** を選択します。  

3. **[スタートアップの種類]** が **[自動]** に設定されていることを確認します。

4. **[操作]** メニューにアクセスし、 **[開始]** を選択します。

    1. この操作が使用できない場合は、 **[停止]** を選択します。 サービスが停止するのを待ち、 **[開始]** 操作を選択してサービスを再起動します。  

このプロセス中にエラーが発生した場合は、そのエラーをメモします。 [Microsoft サポートに連絡し](../../core/understand/find-help.md#BKMK_SupportOptions)、エラー情報を提供します。  

#### <a name="step-3-remove-any-third-party-security-programs"></a>手順 3:サードパーティ製のセキュリティ プログラムを削除する  

> [!NOTE]  
> 一部のセキュリティ アプリケーションは、完全にはアンインストールされません。 完全に削除するには、以前のセキュリティ アプリケーション用のクリーンアップ ユーティリティをダウンロードして実行しなければならない場合があります。  

1. **[スタート]** にアクセスし、**appwiz.cpl** を開きます。  

2. インストールされているプログラムの一覧で、サードパーティのセキュリティ プログラムをすべてアンインストールします。

3. コンピューターを再起動する  

> [!CAUTION]  
> セキュリティ プログラムを削除すると、お使いのコンピューターは保護されなくなる可能性があります。 既存のセキュリティ プログラムを削除した後、Windows Defender のインストールに関して問題が発生した場合は、[Microsoft サポート](https://support.microsoft.com/supportforbusiness/productselection)にお問い合わせください。 **[セキュリティ]** 製品ファミリを選択し、 **[Windows Defender]** 製品を選択します。

## <a name="internet-connection-issues"></a>インターネット接続の問題

コンピューターが Windows Update から最新の更新プログラムを受信できるようにするために、コンピューターをインターネットに接続します。  

1. **[スタート]** にアクセスし、**ncpa.cpl** を開きます。  

2. 接続名を開いて、接続の **[状態]** を表示します。  

3. コンピューターが接続されている場合、 **[IPv4 接続]** 、 **[IPv6 接続]** 、またはこれらの両方の状態は **[インターネット]** です。  

4. コンピューターが接続されていないと思われる場合は、接続名を選択し、 **[この接続を診断する]** を選択します。

開いているプログラムをすべて閉じて、コンピューターを再起動します。  

## <a name="detected-threat-cant-be-remediated"></a>検出された脅威を修復できない

Windows Defender または Endpoint Protection は、潜在的な脅威を検出すると、その脅威を検疫または削除することで脅威を軽減しようとします。 これらの脅威は、圧縮アーカイブ (`.zip`) 内またはネットワーク共有内に隠されている可能性があります。

### <a name="remove-or-scan-the-file"></a>ファイルを削除またはスキャンする  

- 検出された脅威が圧縮アーカイブ ファイル内にあった場合は、そのファイルを参照します。 そのファイルを削除するか、手動でスキャンします。 ファイルを右クリックし、 **[Windows Defender でスキャン]** を選択します。 Windows Defender によってファイル内で追加の脅威が検出された場合は、ユーザーに通知されます。 その後、適切な操作を選択できます。  

- 検出された脅威がネットワーク共有内にあった場合は、共有を開き、手動でスキャンします。 ファイルを右クリックし、 **[Windows Defender でスキャン]** を選択します。 Windows Defender によってネットワーク共有内で追加の脅威が検出された場合は、ユーザーに通知されます。 その後、適切な操作を選択できます。  

- ファイルの出所が明確でない場合、コンピューターのフル スキャンを実行します。 フル スキャンは、完了するまでに時間がかかる場合があります。  

## <a name="see-also"></a>関連項目

[Endpoint Protection クライアントのよく寄せられる質問](endpoint-protection-client-faq.md)

[Endpoint Protection クライアント ヘルプ](endpoint-protection-client-help.md)
