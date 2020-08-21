---
title: デバイス管理ソリューションの選択
titleSuffix: Configuration Manager
description: PC、サーバー、およびデバイスを管理するための Microsoft によって提供されるソリューションについて説明します。
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877345e64045530193a4cdd735cdd399235b90c7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700267"
---
# <a name="choose-a-device-management-solution"></a>デバイス管理ソリューションの選択

Microsoft では、PC、サーバー、デバイスを管理するためのさまざまなソリューションが提供されています。 これらのソリューションは、オンプレミス、クラウドベース、またはその両方の組み合わせで利用できます。 ご自身の組織のビジネス要件に最適な管理ソリューションを選択してください。 管理する必要のあるデバイス プラットフォームや、必要な管理機能に基づいて判断します。

## <a name="overview"></a>[概要]

さまざまなシナリオに合わせて最適に機能するいくつかの Microsoft ソリューションがあります。 1 つだけを選択する必要はありません。

- 小規模な組織では、Windows 管理センターのようなツールが最適である場合があります。
- IT 組織の約 75% では、デバイスを管理するために Configuration Manager が使用されています。
- Microsoft Azure には、Azure Stack を使用した、クラウドまたはオンプレミスのさまざまなソリューションが用意されています。これは主にサーバー管理を対象とします。
- Microsoft Intune では、クライアントのクラウド管理を利用できます。
- Configuration Manager と Intune を共同管理と組み合わせることができます。

次の表は、これらの管理テクノロジを比較するのに役立ちます。

|  | クラウド専用 | クラウド接続 | オンプレミス | 切断 |
|---------|---------|---------|---------|---------|
| **Hyper-V ホスト** | 適用なし | - Azure Stack<br/> - Windows 管理センター<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows 管理センター<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows 管理センター<br/> - Virtual Machine Manager |
| **Windows Server** | - Azure の管理<br/> - Configuration Manager | - Azure の管理<br/> - Configuration Manager | - Azure の管理<br/> - Configuration Manager | Configuration Manager |
| **Linux サーバー** | Azure の管理 | Azure の管理 | Azure の管理 |  |
| **Windows 10** | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | Configuration Manager |
| **Windows 7 または 8.1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows Virtual Desktop** | Configuration Manager | 適用なし | 適用なし | 適用なし |

詳細については、以下の記事を参照してください。

- [Azure Stack とは](/azure-stack/operator/azure-stack-overview)
- [Windows 管理センターとは](/windows-server/manage/windows-admin-center/understand/what-is)
- [Virtual Machine Manager とは](/system-center/vmm/overview)
- [Azure の管理製品](/azure/)
- [Windows Virtual Desktop とは](/azure/virtual-desktop/overview)

Configuration Manager および Intune ソリューションについて詳しくは、次のセクションに進んでください。

## <a name="client-management"></a>クライアント管理

このセクションでは、次の 4 つのクライアント管理ソリューションを比較します。

- [構成マネージャー クライアント](#bkmk_sccm)
- [Configuration Manager でのオンプレミス モバイル デバイス管理 (MDM)](#bkmk_opmdm)
- [Microsoft Intune での共同管理](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

これらのソリューションは、単独で使用することも、相互に組み合わせて使用することもできます。 たとえば、クライアント ベースの管理方法を使用して組織内のコンピューターとサーバーの管理を行いつつ、共同管理を使用してインターネット ベースのラップトップを管理することができます。 このようにアプローチを組み合わせることによって、デバイス管理のすべてのニーズに対応することができます。  

また、次の要素で管理ソリューションを比較した 2 つの表も記載されています。

- [サポートされているプラットフォームによる比較](#bkmk_comp1)
- [管理機能による比較](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> 構成マネージャー クライアント  

このオプションを使うには、デバイス上に Configuration Manager クライアントをインストールする必要があります。 これにより、環境内の PC、サーバー、およびその他のデバイスを管理するための機能のほとんどが提供されます。

詳細については、[クライアントのインストール方法](../clients/deploy/plan/client-installation-methods.md)に関する記事をご覧ください。  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> オンプレミス MDM  

このオプションでは、Windows 10 に組み込まれているデバイス管理機能が使われます。 クライアント ベースの管理と同様のフル機能は提供されませんが、オンプレミスの MDM では簡略化された方法で管理を行うことができます。 デバイスを管理するために、オンプレミスの Configuration Manager リソースが使われます。  

詳しくは、「[オンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」をご覧ください。  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a> Microsoft Intune での共同管理

共同管理は、既存の Configuration Manager の展開を Microsoft 365 のクラウドにアタッチするための主要な方法の 1 つです。 これによって、Configuration Manager と Microsoft Intune の両方を使って Windows 10 デバイスを同時に管理することができます。 共同管理を使うと、新しい機能を追加して、Configuration Manager 内の既存の投資をクラウドにアタッチできます。

詳細については、「[共同管理とは](../../comanage/overview.md)」をご覧ください。  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Microsoft Exchange  

このオプションでは、Exchange Server コネクタを使用して、Configuration Manager に複数の Exchange サーバーを接続します。 これにより、Exchange ActiveSync に接続できるデバイスが一元的に管理されます。 Configuration Manager コンソールから Exchange のモバイル デバイス管理機能を構成できます。 機能の例としては、複数の Exchange サーバー向けのリモート デバイス ワイプや設定コントロールなどがあります。

詳しくは、「[Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」をご覧ください。  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> サポートされているプラットフォームでソリューションを比較する  

|プラットフォーム|Configuration Manager クライアント|オンプレミス MDM|Configuration Manager と Exchange の併用| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |[はい]| [はい] |
|iOS| | |[はい]| [はい] |
|Mac OS X|[はい]| |[はい]| [はい] |
|Windows 10|[はい]|[はい]|[はい]| [はい] |
|[Windows] 10 Mobile| |[はい]|[はい]| [はい] |
|Windows (以前のバージョン)|[はい]| |[はい]|  |
|Windows Server|[はい]| |[はい]|  |
|Windows Embedded|[はい]| | |  |

サポートされるプラットフォームの完全な一覧については、次の記事をご覧ください。

- [Configuration Manager のクライアントとデバイスのサポートされるオペレーティング システム](configs/supported-operating-systems-for-clients-and-devices.md)
- [Intune でサポートされる構成](/intune/supported-devices-browsers)

Microsoft では、Intune を使って Android、iOS、および Windows 10 モバイル デバイスを管理することをお勧めします。 詳細については、[Microsoft Intune の概要](/intune/what-is-intune)に関する記事をご覧ください。

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a> 管理機能でソリューションを比較する  

|管理機能|Configuration Manager クライアント|オンプレミス MDM|Configuration Manager と Exchange の併用|  
|--------|----------------------------|---------------|-----------------------------------|  
|証明書ベースの相互認証|[はい]|[はい]| |
|クライアントのインストール|[はい]| | |
|インターネット経由のサポート|[はい]| | |
|探索|[はい]| |[はい]|
|ハードウェア インベントリ|[はい]|[はい]|[はい]|
|ソフトウェア インベントリ|[はい]| |[はい]|
|設定|[はい]|[はい]|[はい]|
|ソフトウェアの展開|[はい]|[はい]| |
|ソフトウェア更新管理|[はい]| | |
|OS の展開|[はい]| | |
|Configuration Manager からのブロック|[はい]|[はい]| |
|Exchange Server (および Configuration Manager) からの検疫とブロック| | |[はい]|
|リモート ワイプ| |[はい]|[はい]|