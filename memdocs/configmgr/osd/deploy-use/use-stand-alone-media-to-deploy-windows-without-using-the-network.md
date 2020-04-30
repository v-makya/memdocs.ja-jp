---
title: スタンドアロン メディアを使用した Windows の展開
titleSuffix: Configuration Manager
description: 帯域幅が制限されている場合にコンピューターを更新、インストール、またはアップグレードするためのオプションとして、Configuration Manager のスタンドアロン メディアを使用して Windows を展開します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709040"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>ネットワークではなくスタンドアロン メディアを使用した Windows の展開

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のスタンドアロン メディアには、コンピューター上にオペレーティング システムを展開するために必要なものがすべて含まれています。 これには、アプリケーションやドライバーなどを含めてオペレーティング システムをインストールするための、ブート イメージ、オペレーティング システム イメージ、およびタスク シーケンスが含まれます。 スタンドアロン メディアによる展開では、次のような状況でオペレーティング システムを展開できます。  

-   オペレーティング システム イメージまたはファイルサイズの大きなパッケージをネットワークを通じてコピーするのが実用的ではない環境。  

-   ネットワーク接続がない、または低帯域幅のネットワーク接続しかできない環境。  

スタンドアロン メディアは、次のオペレーティング システム展開シナリオで使用できます。  

- [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

- [Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md)  

  いずれかのオペレーティング システムの展開シナリオのステップを完了させてから、次のセクションを参照して、スタンドアロン メディアを準備および作成します。  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>スタンドアロン メディアを使用する場合にサポートされないタスク シーケンス アクション  
 サポートされているいずれかのオペレーティング システム展開シナリオのステップが完了している場合は、オペレーティング システムを展開またはアップグレードするためのタスク シーケンスが作成され、関連するすべてのコンテンツが配布ポイントに配布されています。 スタンドアロン メディアを使用した場合、タスク シーケンスでは、次のアクションはサポートされません。  

-   タスク シーケンスでのドライバーの自動適用のステップ ドライバー カタログからのデバイス ドライバーの自動適用はサポートされていませんが、[ドライバー パッケージの適用] ステップを選択して、指定された一連のドライバーを Windows セットアップで使用できるようにします。  

-   ソフトウェア更新プログラムのインストール  

-   オペレーティング システム展開前のソフトウェアのインストール  

-   ユーザーとデバイスのアフィニティをサポートする展開先のコンピューターとユーザーの関連付け  

-   動的なパッケージはパッケージのインストール タスクを使用してインストールします。  

-   動的なアプリケーションはアプリケーションのインストール タスクを使用してインストールします。  

> [!NOTE]  
>  オペレーティング システムを展開するタスク シーケンスに [[パッケージのインストール]](../understand/task-sequence-steps.md#BKMK_InstallPackage) ステップが含まれる場合に、中央管理サイトでスタンドアロン メディアを作成すると、エラーが発生する可能性があります。 中央管理サイトには、タスク シーケンスの実行中に、ソフトウェアの配布エージェントを有効にするために必要なクライアント構成ポリシーがありません。 CreateTsMedia.log ファイルに次のエラーが表示される場合があります。  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  **[パッケージのインストール]** ステップを含むスタンドアロン メディアの場合、ソフトウェアの配布エージェントが有効なプライマリ サイトにスタンドアロン メディアを作成するか、または [[Windows と ConfigMgr のセットアップ]](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) ステップの後かつタスク シーケンスの最初の **[パッケージのインストール]** ステップの前に [[コマンド ラインの実行]](../understand/task-sequence-steps.md#BKMK_RunCommandLine) ステップを追加する必要があります。 **[コマンド ラインの実行]** ステップでは、最初の [パッケージのインストール] ステップを実行する前に、ソフトウェアの配布エージェントを有効にする WMIC コマンドを実行します。 **[コマンド ラインの実行]** タスク シーケンス ステップでは、次のコマンド ラインを使用できます。  
>   
>  **コマンド ライン**:**WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>展開の設定の構成  
 スタンドアロン メディアを使用してオペレーティング システムの展開プロセスを開始する場合、オペレーティング システムをメディアから使用できるように展開を構成する必要があります。 これはソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで構成することができます。  **[利用できるようにする項目]** の設定では、次のいずれかを設定します。  

-   **Configuration Manager クライアント、メディア、PXE**  

-   **メディアと PXE のみ**  

-   **メディアと PXE のみ (非表示)**  

## <a name="create-the-stand-alone-media"></a>スタンドアロン メディアの作成  
 スタンドアロン メディアとして USB フラッシュ ドライブと CD/DVD セットのどちらかを指定できます。 起動可能なドライブに選ぶオプションは、メディアを起動するコンピューターがサポートするものでなければなりません。 詳細については、「[スタンドアロン メディアの作成](create-stand-alone-media.md)」を参照してください。  

## <a name="install-the-operating-system-from-stand-alone-media"></a>スタンドアロン メディアからのオペレーティング システムのインストール  
 コンピューターの起動可能なドライブにスタンドアロン メディアを挿入し、電源を入れてオペレーティング システムをインストールします。  
