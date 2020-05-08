---
title: Windows Embedded デバイスへのクライアント展開の計画
titleSuffix: Configuration Manager
description: Configuration Manager での Windows Embedded デバイスへのクライアント展開の計画。
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7848e3c0c38391ab61d10ad46cbb772c812539c7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906638"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-configuration-manager"></a>Configuration Manager での Windows Embedded デバイスへのクライアント展開の計画

*適用対象:Configuration Manager (Current Branch)*

<a name="BKMK_DeployClientEmbedded"></a> Windows Embedded デバイスに Configuration Manager クライアントが含まれていない場合、デバイスが必要な依存関係を満たしていれば、任意のクライアント インストール方法を使用できます。 Embedded デバイスで書き込みフィルターがサポートされている場合、クライアントをインストールする前にこれらのフィルターを無効にし、クライアントがインストールされ、サイトに割り当てられた後で、フィルターを再度有効にする必要があります。  

 フィルターを無効にした場合は、フィルター ドライバーを無効にしないことに注意してください。 通常、これらのドライバーは、コンピューターが起動すると、自動的に開始されます。 ドライバーを無効にすると、クライアントのインストールができなくなるか、フィルターのオーケストレーションの書き込みが中断して、クライアント操作の失敗につながります。 実行し続ける必要がある各書き込みフィルターの種類に関連付けられたサービスを次に示します。  

|書き込みフィルターの種類|ドライバー|Type|[説明]|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|カーネル|保護されたボリュームに、セクターレベルの I/O リダイレクトを実装します。|  
|FBWF|FBWF|ファイル システム|保護されたボリュームに、ファイルレベルの I/O リダイレクトを実装します。|  
|UWF|uwfreg|カーネル|UWF レジストリ リダイレクター|  
|UWF|uwfs|ファイル システム|UWF ファイル リダイレクター|  
|UWF|uwfvol|カーネル|UWF ボリューム マネージャー|  

 書き込みフィルターは、ソフトウェアのインストールなど、変更を行う場合に、Embedded デバイスのオペレーティング システムを更新する方法を制御します。 書き込みフィルターが有効な場合、オペレーティング システムは直接変更されず、これらの変更は一時オーバーレイにリダイレクトされます。 変更がオーバーレイに書き込まれただけの場合、Embedded デバイスのシャットダウン時に変更は失われます。 ただし、書き込みフィルターを一時的に無効にすると、Embedded デバイスが再起動するたびに再度変更を行う (またはソフトウェアを再インストールする) 必要がないように、変更を恒久的にすることができます。 書き込みフィルターを一時的に無効にして、再度有効にするには、1 回または複数回の再起動が必要になります。そのため、通常は、再起動が業務時間外になるようにメンテナンス期間を構成して、この操作の実行のタイミングを制御する必要があります。  

 アプリケーション、タスク シーケンス、ソフトウェア更新プログラム、Endpoint Protection クライアントなどのソフトウェアを展開するときに、書き込みフィルターを自動的に無効化して再度有効にするオプションを構成できます。 例外は、自動修復を使用する構成項目が含まれる構成基準です。 このシナリオでは、修復は常にオーバーレイで実行され、デバイスが再起動されるまでの間のみ使用できます。 修復は次回の評価サイクルで再度適用されますが、オーバーレイにのみ適用されるため、再起動時に消去されます。 Configuration Manager で修復の変更を強制的にコミットするには、構成基準を展開してから、変更の即時コミットをサポートする別のソフトウェア展開を展開します。  

 書き込みフィルターが無効な場合、ソフトウェア センターを使用して Windows Embedded デバイスにソフトウェアをインストールできます。 書き込みフィルターが有効な場合、インストールは失敗し、アプリケーションをインストールするための権限が不足していることを示すエラー メッセージが Configuration Manager に表示されます。  

> [!WARNING]  
>  Configuration Manager で変更をコミットするオプションを選択していない場合でも、変更をコミットする別のソフトウェアのインストール、または、変更が行われた場合に、変更がコミットされることがあります。 このシナリオでは、新しい変更に加えて、元の変更がコミットされます。  

 Configuration Manager で、変更を恒久的にするために書き込みフィルターが無効にされた場合、Embedded デバイスにログオンして使用できるのは、ローカル管理権限を持つユーザーだけです。 この間、権限の低いユーザーはロックアウトされ、保守作業中のためコンピューターを使用できないことを示すメッセージが表示されます。 これにより、変更を恒久的に適用できる状態にある間、デバイスを保護します。この保守モードのロックアウト動作も、ユーザーがデバイスにログオンしない時間にメンテナンス期間を構成する理由の 1 つです。  

 Configuration Manager では、次の種類の書き込みフィルターの管理がサポートされています。  

- ファイル ベースの書き込みフィルター (FBWF) - 詳細については、「[ファイル ベースの書き込みフィルター](https://docs.microsoft.com/previous-versions/windows/embedded/aa940926(v=winembedded.5))」を参照してください。  

- 拡張書き込みフィルター (EWF) - 詳細については、「[拡張書き込みフィルター](https://docs.microsoft.com/previous-versions/windows/embedded/ms912906(v=winembedded.5))」を参照してください。  

- 統合書き込みフィルター (UWF) - 詳細については、「[統合書き込みフィルター](https://docs.microsoft.com/windows-hardware/customize/enterprise/unified-write-filter)」を参照してください。  

  Configuration Manager では、Windows Embedded デバイスが EWF RAM Reg モードの場合の書き込みフィルター操作をサポートしていません。  

> [!IMPORTANT]
>  使用できる場合は、効率を高め、スケーラビリティを向上させるため、Configuration Manager でファイル ベースの書き込みフィルター (FBWF) を使用してください。
> 
> **FBWF のみを使用するデバイスの場合:** デバイスを再起動した後でクライアントの状態とインベントリ データを保持するには、次の例外を構成します。  
> 
> - CCMINSTALLDIR\\\*.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
>   Windows Embedded 8.0 以降を実行するデバイスでは、ワイルドカード文字を含む除外はサポートされていません。 これらのデバイスでは、次の除外を個別に構成する必要があります。  
> 
> - CCMINSTALLDIR 内のすべてのファイルには、拡張子 .sdf が付きます。通常は次のようになります。  
> 
>   -   UserAffinityStore.sdf  
>   -   InventoryStore.sdf  
>   -   CcmStore.sdf  
>   -   StateMessageStore.sdf  
>   -   CertEnrollmentStore.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
> **FBWF と UWF のみを使用するデバイスの場合:** ワークグループ内のクライアントが管理ポイントへの認証に証明書を使用する場合は、クライアントが管理ポイントと引き続き通信できるように、秘密キーも除外する必要があります。 これらのデバイスでは、次の例外を構成します。  
> 
> - c:\Windows\System32\Microsoft\Protect  
>   -   c:\ProgramData\Microsoft\Crypto  
>   -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

> [!NOTE]
> 上記の **[重要]** ボックスに記載されている以外の Configuration Manager クライアントでは、追加の例外は不要です。 Configuration Manager や WMI (WBEM) 関連の例外を追加すると、サービス モードでデバイスが停止したり、デバイスが再起動ループに入ったりするなど、Configuration Manager のエラーを招く可能性があります。 不要な例外には、Configuration Manager クライアント ディレクトリ、CCMcache ディレクトリ、CCMSetup ディレクトリ、Task Sequence キャッシュ ディレクトリ、WBEM ディレクトリ、Configuration Manager 関連レジストリ キーがあります。

 Configuration Manager で書き込みフィルターが有効になった Windows Embedded デバイスを展開および管理するシナリオの例については、「[Windows Embedded デバイスで System Center Configuration Manager クライアントを展開および管理するシナリオ例](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md)」を参照してください。  

 Windows Embedded デバイスのイメージを作成し、書き込みフィルターを構成する方法の詳細については、Windows Embedded のドキュメントを参照するか、OEM にお問い合せください。  

> [!NOTE]
>  ソフトウェア展開と構成項目の適用可能なプラットフォームを選択すると、特定のバージョンではなく、Windows Embedded ファミリーが表示されます。 特定バージョンの Windows Embedded と、リスト ボックスのオプションの対応については、次の一覧をご覧ください。  
> 
> - **Windows XP (32-bit) ベースの Embedded オペレーティング システム** には、次のものがあります。  
> 
>   -   Windows XP Embedded  
>   -   Windows Embedded for Point of Service  
>   -   Windows Embedded Standard 2009  
>   -   Windows Embedded POSReady 2009  
>   -   **Windows 7 (32-bit) ベースの Embedded オペレーティング システム** には、次のものがあります。  
> 
>   -   Windows Embedded Standard 7 (32-bit)  
>   -   Windows Embedded POSReady 7 (32-bit)  
>   -   Windows の ThinPC  
>   -   **Windows 7 (64 ビット) ベースの Embedded オペレーティング システム** には、次のものがあります。  
> 
>   -   Windows Embedded Standard 7 (64 ビット)  
>   -   Windows Embedded POSReady 7 (64 ビット)
