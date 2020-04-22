---
title: 仮想化のサポート
titleSuffix: Configuration Manager
description: 仮想化環境で Configuration Manager クライアントとサイト システムの役割をインストールするための要件。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688550"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Configuration Manager での仮想環境のサポート

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、この記事で説明する仮想環境内で仮想マシンとして実行するサポート対象オペレーティング システムに、クライアントの役割およびサイト システムの役割をインストールすることがサポートされています。 このサポートは、仮想マシンのホスト (仮想化環境) が、クライアントまたはサイト サーバーとしてサポートされていない場合でも存続します。  

たとえば、Windows Server 2012 を実行する仮想マシンをホストするのに Microsoft Hyper-V Server 2012 を使用します。 Windows Server 2012 を実行する仮想マシンには、クライアントまたはサイト システムの役割をインストールできます。 Microsoft Hyper-V Server 2012 を実行しているホスト上で、クライアントをインストールすることはできません。  

## <a name="virtualization-environments"></a>仮想化環境

- Windows Server 2019  
- Windows Server 2016 <sup>[注 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[注 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a> 注 1:入れ子になった仮想化

Configuration Manager では、Windows Server 2016 の新機能である[入れ子の仮想化](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new)はサポートされていません。

### <a name="virtualization-environment-support"></a>仮想化環境のサポート

各仮想コンピューターでは、物理的な Configuration Manager コンピューターに使用する場合のハードウェアおよびソフトウェアの要件と同じか、それ以上の要件が必要とされます。  

Configuration Manager においてご利用の仮想化環境がサポートされているかどうかを検証するには、サーバー仮想化検証プログラムを使用します。 これには、オンライン版の Virtualization Program Support Policy ウィザードが含まれます。 詳細については、[Windows Server 仮想化検証プログラム](https://www.windowsservercatalog.com/svvp.aspx)に関するページを参照してください。  

> [!NOTE]  
> Configuration Manager では、Mac コンピューター上で稼働される仮想 PC または仮想サーバー ゲスト オペレーティング システムはサポートされていません。  

Configuration Manager では、仮想マシンがオフラインの場合、そのマシンを管理できません。 ホスト コンピューター上の Configuration Manager クライアントを使用して、オフラインの仮想マシン イメージを更新したり、インベントリを収集したりすることはできません。  

仮想マシンについて特別に考慮することはありません。 たとえば、更新プログラムが適用された仮想マシンの状態を保存せずに仮想マシンを停止して再起動した場合、Configuration Manager は仮想マシン イメージに更新プログラムを再適用する必要があるかどうかを判断できない可能性があります。  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Microsoft Azure 仮想マシン  

Configuration Manager は、ご利用のデータ センター内でオンプレミスで実行するのと同様に、Azure 内の仮想マシンでも実行することができます。 Azure 仮想マシンでは、次のシナリオで Configuration Manager を使用します。  

- **シナリオ 1**: Azure 仮想マシン上で Configuration Manager を実行します。 それを使用して、他の Azure 仮想マシン上のクライアントを管理します。  

- **シナリオ 2**: Azure 仮想マシン上で Configuration Manager を実行します。 それを使用して、Azure 上で実行されていないクライアントを管理します。  

- **シナリオ 3**: Azure 仮想マシン上で Configuration Manager サイト システムのさまざまな役割を実行します。 Azure に正しく接続されている、オンプレミスのデータ センター内で他の役割を実行します。  

オンプレミスで Configuration Manager をインストールするときに適用されるのと同じ、ネットワークに対する Configuration Manager の要件、サポートされる構成、およびハードウェア要件が、Azure 仮想マシンへのインストールにも適用されます。  

詳細については、[Azure での Configuration Manager](../../understand/configuration-manager-on-azure.md) に関するページを参照してください。

> [!IMPORTANT]  
> Azure Virtual Machines で実行している Configuration Manager サイトおよびクライアントには、オンプレミス インストールと同じライセンス要件が課されます。  

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) は Microsoft Azure と Microsoft 365 のプレビュー機能です。 バージョン 1906 以降では、Configuration Manager を使用して、Azure で Windows が実行されているこれらの仮想デバイスを管理できます。 詳細については、「[クライアントとデバイスのサポートされるオペレーティング システム](supported-operating-systems-for-clients-and-devices.md)」をご覧ください。
