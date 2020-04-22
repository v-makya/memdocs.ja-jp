---
title: Azure でのラボの作成
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview ラボまたは Current Branch 評価ラボの作成を Azure テンプレートを使用して自動化する
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd2a8b3bfb7c4b8af277616c7eaed329bc143bb7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691400"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Configuration Manager ラボを Azure で作成する

*適用対象:Configuration Manager (Technical Preview Branch)*

<!--3556017-->

このガイドでは、Microsoft Azure で Configuration Manager ラボ環境を構築する方法について説明します。 Azure テンプレートを使用して、Azure リソースを用いたラボの作成が簡略化および自動化されます。 次の 2 つの Azure テンプレートが用意されています。 

- Configuration Manager Technical Preview Azure テンプレート。最新バージョンの Configuration Manager Technical Preview Branch をインストールします。
- Configuration Manager Current Branch Azure テンプレート。Configuration Manager Current Branch の最新バージョンの評価がインストールされます。 

詳細については、[Azure での Configuration Manager](../understand/configuration-manager-on-azure.md) に関するページを参照してください。



## <a name="prerequisites"></a>[前提条件]

このプロセスでは、次のオブジェクトを作成できる Azure サブスクリプションが必要です。 
- ドメイン コントローラーと MP ロールと DP ロール用の 2 台の Standard_B2s 仮想マシン
- プライマリ サイト サーバーと SQL データベース サーバー用の 1 台の Standard_B2ms 仮想マシン
- Standard_LRS ストレージ アカウント

> [!Tip]  
> 予想されるコストについては、「[Azure の料金計算ツール](https://azure.microsoft.com/pricing/calculator/)」を参照してください。  



## <a name="process"></a>プロセス

1. [Configuration Manager Technical Preview テンプレート](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/)または [Configuration Manager Current Branch テンプレート](https://azure.microsoft.com/resources/templates/sccm-currentbranch/)のページに移動します。  

2. **[Deploy to Azure]\(Azure にデプロイ\)** を選択すると、Azure ポータルが開きます。  

3. 次の情報を使用して、Azure クイック スタート テンプレートを完了します。

    - 基本  

        - **サブスクリプション**:VM を作成するサブスクリプションの名前  

        - **リソース グループ**:これらの VM に使用するリソース グループを選択します  

        - **場所**: このラボ環境をホストする Azure データ センターを選択します  

    - Settings  

        - **プレフィックス**:マシンのプレフィックス名。 詳細については、「[Azure VM の情報](#azure-vm-info)」を参照してください。  

        - **管理者ユーザー名**:管理者権限を持つ、VM のユーザーの名前。 このユーザーを使用して、VM にサインインします。  

        - **管理者パスワード**:パスワードは、Azure の複雑さの要件を満たす必要があります。 詳細については、[adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile) に関するページを参照してください。  

    > [!Important]  
    > Azure では次の設定が必要です。 既定値を使用します。 これらの値は変更しないでください。  
    > 
    > - **[\_artifacts Location]\(_artifacts の場所\)** :このテンプレートのスクリプトの場所 <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **[\_artifacts Location Sas Token]\(_artifacts の場所の SAS トークン\)** :成果物の場所にアクセスするには、sasToken が必要です  
    > 
    > - **場所**: すべてのリソースの場所

4. 使用条件を読みます。 同意する場合は、 **[上記の使用条件に同意する]** を選択します。 その後、 **[購入]** を選択して続行します。 

Azure では設定を検証してから、デプロイを開始します。 Azure ポータルでデプロイの状態を確認します。 

> [!NOTE]
> プロセスには、2 時間から 4 時間かかる場合があります。 Azure ポータルにデプロイが正常に行われたことが示されても、構成スクリプトは引き続き実行されます。 プロセス中に VM を再起動しないでください。

構成スクリプトの状態を確認するには、`<prefix>PS1` サーバーに接続し、`%windir%\TEMP\ProvisionScript\PS1.json` ファイルを表示します。 すべての手順が完了と示されたら、プロセスは完了です。

VM に接続するには、まず、Azure ポータルから各 VM のパブリック IP アドレスを取得します。 VM に接続する場合、ドメイン名は `contoso.com` となります。 デプロイ テンプレートで指定した資格情報を使用します。 詳細については、「[Windows が実行されている Azure 仮想マシンに接続してログオンする方法](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon)」を参照してください。



## <a name="azure-vm-info"></a>Azure VM の情報

3 つのすべての VM には、次の仕様があります。
- 150 GB のディスク領域
- パブリックとプライベートの両方の IP アドレス。 パブリック IP は、TCP ポート 3389 でのリモート デスクトップ接続のみを許可するネットワーク セキュリティ グループにあります。 

デプロイ テンプレートで指定したプレフィックスは、VM 名のプレフィックスです。 たとえば、プレフィックスとして "contoso" を設定した場合、ドメイン コントローラーのコンピューター名は `contosoDC` となります。


### `<prefix>DC01`

- Active Directory ドメイン コントローラー
- Standard_B2s (CPU 2 個、メモリ 4 GB)
- Windows Server 2019 Datacenter Edition

#### <a name="windows-features-and-roles"></a>Windows の機能と役割
- Active Directory Domain Services (ADDS)
- .NET
- Remote Differential Compression (RDC)


### `<prefix>PS01`

- Standard_B2ms (CPU 2 個、メモリ 8 GB)
- Windows Server 2016 Datacenter Edition
- SQL Server
- Windows 10 ADK (Windows PE を含む) 
- Configuration Manager プライマリ サイト

#### <a name="windows-features-and-roles"></a>Windows の機能と役割
- .NET
- Remote Differential Compression (RDC) 
- インターネット インフォメーション サービス (IIS)


### `<prefix>DPMP01`

- Standard_B2s (CPU 2 個、メモリ 4 GB)
- Windows Server 2019 Datacenter Edition
- 配布ポイント
- 管理ポイント

#### <a name="windows-features-and-roles"></a>Windows の機能と役割
- .NET
- Remote Differential Compression (RDC) 
- インターネット インフォメーション サービス (IIS)
- バックグラウンド インテリジェント転送サービス (BITS)

### `<prefix>CL01`

- Configuration Manager Current Branch 評価テンプレート専用
- Windows 10
- Configuration Manager クライアント
