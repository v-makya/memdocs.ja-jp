---
title: 特徴と機能
titleSuffix: Configuration Manager
description: Configuration Manager の主な管理機能について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 74b150b5a2157104b6a380489202fd309224a3bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129037"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Configuration Manager の特徴と機能

*適用対象:Configuration Manager (Current Branch)*

この記事は、Configuration Manager の主な管理機能をまとめたものです。 各機能には独自の前提条件があり、それぞれの使用方法によって、Configuration Manager 階層の設計と実装に影響する可能性があります。 たとえば、階層内のデバイスにソフトウェア更新プログラムを展開する場合は、ソフトウェアの更新ポイント サイト システムの役割が必要です。  

ご使用の環境でこれらの管理機能がサポートされるように Configuration Manager の計画とインストールを行う方法の詳細については、[Configuration Manager の準備](../get-ready.md)に関するページをご覧ください。  

## <a name="co-management"></a>共同管理

共同管理は、既存の Configuration Manager の展開を Microsoft 365 のクラウドにアタッチするための主要な方法の 1 つです。 これによって、Configuration Manager と Microsoft Intune の両方を使って Windows 10 デバイスを同時に管理することができます。 共同管理を使うと、条件付きアクセスなどの新しい機能を追加して、Configuration Manager 内の既存の投資をクラウドにアタッチできます。 詳細については、「[共同管理とは](../../../comanage/overview.md)」をご覧ください。

## <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics は、Configuration Manager に統合されているクラウドベースのサービスです。 そのサービスでは、Windows クライアントの更新準備に関して豊富な情報に基づく意思決定をするために役立つ分析情報やインテリジェンスが提供されます。 組織からのデータと、Microsoft クラウド サービスに接続された何百万ものデバイスから収集されたデータが結合されます。 詳細については、「[Desktop Analytics とは](../../../desktop-analytics/overview.md)」を参照してください。

## <a name="cloud-attached-management"></a>クラウド接続の管理

クラウド管理ゲートウェイ、クラウドベースの配布ポイント、Azure Active Directory などの機能を使用して、インターネット ベースのクライアントを管理します。

詳細については、以下の記事を参照してください。

- [インターネット上のクライアントを管理する](../../clients/manage/manage-clients-internet.md)
- [Azure AD の計画](../security/plan-for-security.md#bkmk_planazuread)
- [Azure サービス](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>リアルタイムの管理

CMPivot を使用してすぐにオンラインのデバイスを照会し、詳細な分析情報を得るためにデータのフィルター処理とグループ化を実行します。 また、Configuration Manager コンソールを使用して、Windows PowerShell スクリプトを管理してクライアントに展開します。 詳しくは、[CMPivot](../../servers/manage/cmpivot.md)に関するページと、[PowerShell スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)に関するページを参照してください。

## <a name="application-management"></a>アプリケーション管理

管理しているさまざまなデバイスに対して、アプリケーションを作成、管理、展開、監視するのに役立ちます。 Configuration Manager コンソールから Microsoft 365 Apps を展開、更新、管理します。 さらに、Configuration Manager をビジネス向けおよび教育機関向け Microsoft Store と統合することで、クラウドベースのアプリが提供されます。 詳細については、[アプリケーション管理の概要](../../../apps/understand/introduction-to-application-management.md)に関するページを参照してください。

## <a name="os-deployment"></a>OS の展開

Windows 10 のインプレース アップグレードを展開するか、OS イメージをキャプチャして展開します。 イメージの展開では、PXE、マルチキャスト、または起動可能なメディアを使用できます。 また、Windows Autopilot を使用して既存のデバイスを再展開することもできます。 詳細については、[OS の展開の概要](../../../osd/understand/introduction-to-operating-system-deployment.md)に関するページを参照してください。  

## <a name="software-updates"></a>ソフトウェア更新プログラム

組織内のソフトウェア更新プログラムを管理、展開、監視します。 Windows 配信の最適化を他のピア キャッシュ テクノロジと統合して、ネットワークの使用を制御します。 詳しくは、「[ソフトウェア更新プログラムの概要](../../../sum/understand/software-updates-introduction.md)」をご覧ください。  

## <a name="company-resource-access"></a>会社のリソースへのアクセス

組織内のユーザーがリモートの場所からデータとアプリケーションにアクセスできるようにします。 この機能には、Wi-Fi、VPN、メール、証明書プロファイルが含まれます。 詳細については、「[データとサイト インフラストラクチャの保護](../../../protect/understand/protect-data-and-site-infrastructure.md)」を参照してください。

## <a name="compliance-settings"></a>コンプライアンス設定

組織内のクライアント デバイスの構成コンプライアンスを評価、追跡、修復するのに役立ちます。 さらに、コンプライアンス設定を使用すると、管理対象デバイスでさまざまな機能とセキュリティ設定を構成できます。 詳細については、[デバイス コンプライアンスの確保](../../../compliance/understand/ensure-device-compliance.md)に関するページを参照してください。  

## <a name="endpoint-protection"></a>Endpoint Protection

組織内のコンピューターにセキュリティ、マルウェア対策、Windows ファイアウォール管理を提供します。 この領域には、次の Windows Defender スイートの機能との管理と統合が含まれます。

- Windows Defender ウイルス対策
- Microsoft Defender Advanced Threat Protection
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Windows Defender Application Control
- Windows Defender ファイアウォール

詳しくは、「[Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)」をご覧ください。  

## <a name="inventory"></a>インベントリ

資産の特定と監視に役立ちます。

### <a name="hardware-inventory"></a>ハードウェア インベントリ

組織内のデバイスのハードウェアに関する詳細情報を収集します。 詳しくは、「[ハードウェア インベントリの概要](../../clients/manage/inventory/introduction-to-hardware-inventory.md)」をご覧ください。  

### <a name="software-inventory"></a>ソフトウェア インベントリ

組織内のクライアント コンピューターに保存されているファイルに関する情報を収集およびレポートします。 詳しくは、「[ソフトウェア インベントリの概要](../../clients/manage/inventory/introduction-to-software-inventory.md)」をご覧ください。  

### <a name="asset-intelligence"></a>資産インテリジェンス

インベントリ データを収集し、組織内のソフトウェア ライセンスの使用状況を監視するためのツールを提供します。 詳細については、[資産インテリジェンスの概要](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)に関するページをご覧ください。  

## <a name="on-premises-mobile-device-management"></a>オンプレミス モバイル デバイス管理

デバイス プラットフォームに組み込まれている管理機能を備えたオンプレミスの Configuration Manager インフラストラクチャを使用して、デバイスを登録および管理します (一般的な管理では、個別にインストールされた Configuration Manager クライアントを使用します)。この機能により、現時点で、Windows 10 Enterprise および Windows 10 Mobile デバイスの管理がサポートされています。 詳しくは、「[オンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」をご覧ください。  

## <a name="power-management"></a>電源管理

組織内のクライアント コンピューターの電力消費を管理および監視します。 電源プランを構成し、Wake on LAN を使用して営業時間外にメンテナンスを行います。 詳細については、「[電源管理の概要](../../clients/manage/power/introduction-to-power-management.md)」を参照してください。  

## <a name="remote-control"></a>リモート コントロール

Configuration Manager コンソールからクライアント コンピューターをリモート管理するためのツールを提供します。 詳細については、「[リモート コントロールの概要](../../clients/manage/remote-control/introduction-to-remote-control.md)」をご覧ください。  

## <a name="reporting"></a>レポート

Configuration Manager コンソールから SQL Server Reporting Services の高度なレポート機能を使用します。 この機能により、何百もの既定のレポートが提供されます。 詳細については、「[レポートの概要](../../servers/manage/introduction-to-reporting.md)」をご覧ください。  

## <a name="software-metering"></a>ソフトウェア使用状況測定

構成マネージャー クライアントからソフトウェア使用状況データを監視および収集します。 このデータを使用して、インストールされたソフトウェアが使用されているかどうかを判断できます。 詳細については、[ソフトウェア使用状況測定によるアプリの使用状況の監視](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)に関するページを参照してください。  
