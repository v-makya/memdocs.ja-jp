---
title: サポートされている構成
titleSuffix: Configuration Manager
description: 機能的な Configuration Manager 展開を計画、展開、および管理するための主要な構成および要件を特定します。
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09618acc1c0950c3eaae79cca59fcf71dc7ef61e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688520"
---
# <a name="supported-configurations-for-configuration-manager"></a>Configuration Manager のサポートされている構成

*適用対象:Configuration Manager (Current Branch)*

オンプレミス ソリューションとして、Configuration Manager では、サーバー、クライアント、ネットワーク構成、および Microsoft Intune、SQL Server、Azure などのその他の製品を使用します。

このドキュメントおよび次のトピックの情報では、機能的な Configuration Manager 展開を計画、展開、および管理するための主要な構成および要件、または制限事項を識別するために不可欠です。  この情報は、Configuration Manager サイト、階層、およびマネージド デバイスのインフラストラクチャに固有です。

Configuration Manager 機能に、さらに明確な構成が必要な場合、その情報は機能固有のドキュメントに含められ、これらのより一般的な構成の詳細を補足します。  

 次のトピックで説明する製品とテクノロジが、Configuration Manager でサポートされています。 ただし、このコンテンツにそれらが含まれていても、その製品の個別のサポート ライフサイクルを超える製品サポートの延長を表すものではありません。 サポート ライフサイクルの範囲を超えた製品は、[延長セキュリティ更新プログラム (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) の対象となるすべての製品も含め、Configuration Manager での使用がサポートされません。 マイクロソフト サポート ライフサイクルの詳細については、 [「マイクロソフト サポート ライフサイクル」](https://go.microsoft.com/fwlink/p/?LinkId=208270) Web サイトを参照してください。 Configuration Manager での延長セキュリティ更新プログラムの詳細については、「[Supported OS versions for clients and devices for Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU)」(Configuration Manager でクライアントとデバイスに対してサポートされる OS のバージョン) を参照してください。

> [!NOTE]  
>  マイクロソフトのサポート ライフサイクル ポリシーについては、[マイクロソフト サポートの「ライフサイクル ポリシー FAQ」](https://go.microsoft.com/fwlink/p/?LinkId=31976)Web サイトを参照してください。  

 さらに、次のトピックに示されていない製品および製品バージョンは、[Enterprise Mobility および Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/)で告知されていない限り、Configuration Manager ではサポートされません。  このブログのコンテンツは、このドキュメントの本文よりも先に更新される場合があります。


-  [サイジングとスケールの数値](../../../core/plan-design/configs/size-and-scale-numbers.md)  
サイトの数、サイトごとのサイト システムの役割、Configuration Manager のさまざまな階層設計でサポートされるクライアントまたはデバイスの詳細について説明します。

-  [サイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Windows Server でさまざまな種類のサイトの種類とサイト システムの役割をサポートするために必要な構成について説明します。

-  [サイト システム サーバーのサポートされるオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
サイト サーバーまたはサイト システム サーバーとして使用できるオペレーティング システムについて説明します。

-  [クライアントとデバイスのサポートされるオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Windows、Windows Embedded、Linux および UNIX、Mac、モバイル デバイスを含む Configuration Manager で管理できるオペレーティング システムについて説明します。

-  [コンソールでサポートされているオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
展開を管理するためのアクセス ポイントを提供する Configuration Manager コンソールをホストできるオペレーティング システムについて説明します。  

-  [SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
サイト データベースとレポート データベースをホストできる SQL Server のバージョン、および必要な構成と使用可能なオプションの構成についても説明します。

-  [高可用性オプション](../../servers/deploy/configure/high-availability-options.md)  
Configuration Manager 展開の高可用性サービスを維持するために、環境の設計時に実装できるオプションについて説明します。

-  [推奨ハードウェア](../../../core/plan-design/configs/recommended-hardware.md)  
Configuration Manager サイトと主要なサービスをホストするための適切なハードウェアおよび構成の識別に役立つガイドラインについて説明します。

-  [Active Directory ドメインのサポート](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Configuration Manager が必要とする Active Directory ドメインのサポートされている構成、およびサポートについて説明します。

-  [Windows の機能とネットワークのサポート](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
サポートされている Windows テクノロジ (BranchCache やデータ重複除去など) および Configuration Manager 使用時の制限について説明します。

-  [仮想環境のサポート](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
サポートされている仮想マシン テクノロジの使用方法について説明します。
