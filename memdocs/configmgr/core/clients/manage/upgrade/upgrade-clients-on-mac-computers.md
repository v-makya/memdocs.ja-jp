---
title: macOS クライアントのアップグレード
titleSuffix: Configuration Manager
description: Configuration Manager クライアントを Mac コンピューターでアップグレードする。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696260"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Configuration Manager で Mac コンピューターのクライアントをアップグレードする方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager アプリケーションを使用して Mac コンピューター用のクライアントをアップグレードするには、この記事の基本手順に従います。 Mac クライアントのインストール ファイルをダウンロードし、共有のネットワーク フォルダーまたは Mac コンピューターのローカル フォルダーにコピーし、手動でインストールするようにユーザーに指示することもできます。  

> [!NOTE]  
> これらの手順を実行する前に、Mac コンピューターが前提条件を満たしていることをご確認ください。 「[Mac コンピューターでサポートされるオペレーティング システム](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)」を参照してください。  

## <a name="download-the-latest-mac-client"></a>最新 Mac クライアントをダウンロードする

Configuration Manager 向け Mac クライアントは、Configuration Manager インストール メディアには同梱されていません。 Microsoft ダウンロード センターからダウンロードしてください ([Microsoft Endpoint Configuration Manager - macOS クライアント (64 ビット)](https://www.microsoft.com/download/details.aspx?id=100850))。 Mac クライアント インストール ファイルは **ConfigmgrMacClient.msi** という名称の Windows インストーラー ファイルに含まれています。  

## <a name="create-the-mac-client-installation-file"></a>Mac クライアント インストール ファイルを作成する

Windows を実行しているコンピューターで **ConfigmgrMacClient.msi** を実行します。 このインストーラーにより、**Macclient.dmg** という名称の Mac クライアント インストール ファイルが解凍されます。 このファイルは既定で、次のフォルダに格納されています。**C:\Program Files\Microsoft\System Center Configuration Manager for Mac client**。  

## <a name="extract-the-client-installation-files"></a>クライアント インストール ファイルを抽出する

**Macclient.dmg** を Mac コンピューターにコピーします。 macOS で Macclient.dmg ファイルをマウントし、Mac コンピューターのフォルダーにコンテンツをコピーします。  

## <a name="create-a-cmmac-file"></a>.cmmac ファイルを作成する

1. Mac クライアント インストール ファイルの **[ツール]** フォルダーを開きます。 **CMAppUtil** ツールを使用し、クライアント インストール パッケージから .cmmac ファイルを作成します。 このファイルは Configuration Manager アプリケーションの作成に使用します。  

2. 新しい **CMClient.pkg.cmmac** ファイルを、Configuration Manager コンソールを実行しているコンピューターから使用できるネットワーク上の場所にコピーします。  

    詳細については、「[Mac コンピューターのアプリケーションを作成および展開するための補足手順](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers)」を参照してください。  

## <a name="create-and-deploy-the-app"></a>アプリを作成して展開する

1. Configuration Manager コンソールで、**CMClient.pkg.cmmac** ファイルから[アプリケーションを作成](../../../../apps/get-started/creating-mac-computer-applications.md)します。  

2. 階層内の Mac コンピューターに[このアプリケーションを展開](../../../../apps/deploy-use/deploy-applications.md)します。  

## <a name="install-the-updated-client"></a>更新されたクライアントをインストールする

Mac コンピューターの既存の Configuration Manager クライアントから、更新プログラムをインストールできることがユーザーに通知されます。 ユーザーは、クライアントをインストールした後に Mac コンピューターを再起動する必要があります。  

コンピューターを再起動すると、**コンピューターの登録**ウィザードが自動的に実行され、新しいユーザー証明書が要求されます。

Configuration Manager の登録を使用せず、Configuration Manager とは独立したクライアント証明書をインストールする場合は、[クライアントが既存の証明書を使用するように構成する](#BKMK_UpgradingClient_MachineEnrollment)方法に関するページを参照してください。  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a> クライアントが既存の証明書を使用するように構成する

この手順を使用し、コンピューターの登録ウィザードの実行を回避し、アップグレードしたクライアントが既存のクライアント証明書を使用するように構成します。  

1. Configuration Manager コンソールで、種類が **Mac OS X** の[構成項目を作成](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)します。  

1. **[スクリプト]** という設定の種類を使用して、この構成項目に設定を追加します。  

1. 次のスクリプトを設定に追加します。  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. [構成基準](../../../../compliance/deploy-use/create-configuration-baselines.md)に構成項目を追加します。 すべての Mac コンピューターに、Configuration Manager とは独立して証明書をインストールする[構成基準を展開](../../../../compliance/deploy-use/deploy-configuration-baselines.md)します。  
