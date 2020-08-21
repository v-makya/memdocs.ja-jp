---
title: 仮想化のサポート
titleSuffix: Configuration Manager
description: 仮想化環境で Configuration Manager クライアントとサイト システムの役割をインストールするための要件。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f7d774d620916f3d735a3545db5fe1e41988731d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126683"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Configuration Manager での仮想環境のサポート

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、特定の仮想環境内で仮想マシン (VM) として実行するサポート対象オペレーティング システムに、クライアントの役割およびサイト システムの役割をインストールすることがサポートされています。 このサポートは、仮想ホスト (仮想化環境) が、クライアントまたはサイト サーバーとしてサポートされていない場合でも存続します。

たとえば、Windows Server 2019 を実行する VM をホストするのに Microsoft Hyper-V Server 2016 を使用します。 Windows Server 2019 を実行する VM には、クライアントまたはサイト システムの役割をインストールできます。 Microsoft Hyper-V Server 2016 を実行しているホスト上で、クライアントをインストールすることはできません。

## <a name="virtualization-environments"></a>仮想化環境

- Windows Server 2019  
- Windows Server 2016 <sup>[注 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[注 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager では、Windows Server 2016 の新機能である[入れ子の仮想化](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new)はサポートされていません。

### <a name="virtualization-environment-support"></a>仮想化環境のサポート

各仮想コンピューターでは、物理的な Configuration Manager コンピューターに使用する場合のハードウェアおよびソフトウェアの要件と同じか、それ以上の要件が必要とされます。

お使いの仮想化環境が Configuration Manager でサポートされていることを確認するには、サーバー仮想化検証プログラムを使用します。 これには、オンライン版の Virtualization Program Support Policy ウィザードが含まれます。 詳細については、[Windows Server 仮想化検証プログラム](https://www.windowsservercatalog.com/svvp.aspx)に関するページを参照してください。

Configuration Manager では、VM がオフラインの場合、そのマシンを管理できません。 ホスト コンピューター上の Configuration Manager クライアントでは、オフライン VM イメージを管理できません。 たとえば、ソフトウェア更新プログラムをインストールしたり、ハードウェア インベントリを収集したりできません。

Configuration Manager には一般的に、VM に関する特別な考慮事項はありません。 たとえば、VM を停止し、その状態を保存しない場合、Configuration Manager では、ソフトウェア更新プログラムを再インストールする必要があるかどうかを判断しないことがあります。

複数のユーザー セッションをサポートする仮想環境で Configuration Manager クライアントのパフォーマンスを上げるため、既定ではユーザー ポリシーが無効になります。 バージョン 1910 以降、このシナリオでユーザー ポリシーを有効にすることができます。 詳細については、クライアント設定に関するページの「[複数のユーザー セッションに対してユーザー ポリシーを有効にします](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions)」を参照してください。

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a> Microsoft Azure VM

Configuration Manager は、ご利用のデータ センター内でオンプレミスで実行するのと同様に、Azure 内の VM でも実行することができます。 Azure VM では、次のシナリオで Configuration Manager を使用します。

- **シナリオ 1**: Azure VM 上で Configuration Manager を実行します。 それを使用して、他の Azure VM 上のクライアントを管理します。

- **シナリオ 2**: Azure VM 上で Configuration Manager を実行します。 それを使用して、Azure 上で実行されていないクライアントを管理します。

- **シナリオ 3**: Azure VM 上で Configuration Manager サイト システムのさまざまな役割を実行します。 Azure に正しく接続されている、オンプレミスのデータ センター内で他の役割を実行します。

ネットワーク、サポートされる構成、ハードウェアの要件に関する Configuration Manager 要件と同じものが Azure VM にも適用されます。

詳細については、[Azure での Configuration Manager](../../understand/configuration-manager-on-azure.md) に関するページを参照してください。

> [!IMPORTANT]
> Azure VM で実行している Configuration Manager サイトおよびクライアントには、オンプレミス インストールと同じライセンス要件が課されます。

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) は、Microsoft Azure 上で実行されるデスクトップおよびアプリの仮想化サービスです。 バージョン 1906 以降では、Configuration Manager を使用して、Azure で Windows が実行されているこれらの仮想デバイスを管理できます。 詳細については、「[クライアントとデバイスのサポートされるオペレーティング システム](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)」をご覧ください。

## <a name="next-steps"></a>次のステップ

[仮想デスクトップ インフラストラクチャ (VDI) で Configuration Manager クライアントを管理する](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)