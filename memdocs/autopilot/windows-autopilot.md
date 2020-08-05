---
title: Windows Autopilot の概要
description: Windows Autopilot は、新しいデバイスのセットアップと事前構成に使用されるテクノロジのコレクションで、生産性の高い使用ができるようにデバイスを準備するためのものです。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 171070e1560796763f3c3851afe239237098f756
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757002"
---
# <a name="overview-of-windows-autopilot"></a>Windows Autopilot の概要

**適用対象**

-   Windows 10

Windows Autopilot は、新しいデバイスのセットアップと事前構成に使用されるテクノロジのコレクションで、生産性の高い使用ができるようにデバイスを準備するためのものです。 また、Windows Autopilot を使用して、デバイスのリセット、用途変更、回復を行うこともできます。 このソリューションでは、管理するインフラストラクチャをほとんどあるいはまったく使用せずに、IT 部門は上記の機能を実現できます。また、そのプロセスは簡単でシンプルです。

Windows Autopilot は、最初の展開から最終的なサポート終了まで、IT とエンド ユーザーの両方にとって Windows デバイスのライフサイクルのあらゆる部分を簡略化することを目的としています。 クラウド ベースのサービスを利用すると、あらゆる種類のエンド ユーザーにとって使いやすいものとしながら、IT がプロセスにかける時間と維持が必要なインフラストラクチャの量を減らすことにより、デバイスの展開、管理、廃棄にかかる全体的なコストを削減できます。 次のビデオと図を参照してください。

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![プロセスの概要](images/image1.png)

Windows 自動運用では、新しい Windows デバイスを初めて展開するときに、デバイスにプレインストールされている OEM 向けに最適化されたバージョンの Windows 10 を利用します。これにより、使用されているデバイスのすべてのモデルに対してカスタムイメージとドライバーを維持する手間を省くことができます。 デバイスを再イメージングする代わりに、既存の Windows 10 のインストールを "ビジネス対応" 状態に変換したり、設定とポリシーを適用したり、アプリをインストールしたりできます。また、使用されている Windows 10 のエディション (Windows 10 Pro から Windows 10 Enterprise など) を変更して高度な機能をサポートすることもできます。

Windows 10 デバイスを展開すると、Microsoft Intune、Windows Update for Business、Microsoft エンドポイント Configuration Manager などのツールで管理できるようになります。 また、windows 自動操縦を利用して、新しいユーザー用にデバイスを迅速に準備するための Windows 自動操縦リセットを活用したり、デバイスを迅速にビジネス対応状態に戻すことができるようにすることで、デバイスを再利用することもできます。

Windows Autopilot では、次のことを実行できます。
* Azure Active Directory (Azure AD) または Active Directory (Hybrid Azure AD Join による) へデバイスを自動的に参加させる。  これらの 2 つの参加オプションの違いについて詳しくは、「[Azure Active Directory のデバイス管理の概要](https://docs.microsoft.com/azure/active-directory/device-management-introduction)」をご覧ください。
* Microsoft Intune などの MDM サービスにデバイスを自動登録します ([*構成には Azure AD Premium サブスクリプションが必要です*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067))。
* 管理者アカウントの作成を制限する。
* デバイスのプロファイルに基づいて構成グループを作成し、デバイスをこのグループに自動的に割り当てる。
* 組織に固有の OOBE コンテンツをカスタマイズする。

## <a name="benefits-of-windows-autopilot"></a>Windows Autopilot の利点

従来、IT 技術者は、イメージの構築やカスタマイズに多くの時間を費やしてきました。こうしたイメージは、後でデバイスに展開されます。 Windows Autopilot には、新しいアプローチが導入されています。

ユーザー側から見ると、数回の簡単な操作を行うだけで、デバイスを使用する準備が整います。

IT 担当者側から見ると、エンド ユーザーから要求される作業は、ネットワークへの接続とユーザーの資格情報の確認だけです。 それ以外のすべてが自動化されます。

## <a name="requirements"></a>必要条件

Windows 自動操縦を使用するには、[サポートされているバージョン](https://docs.microsoft.com/windows/release-information/)の windows 10 半期チャネルが必要です。 Windows 10 Enterprise LTSC 2019 もサポートされています。 ソフトウェア、構成、ネットワーク、およびライセンスの要件の詳細については、「 [Windows の自動操縦要件](windows-autopilot-requirements.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

[Windows Autopilot を使用して、Intune での Windows デバイスを登録する](https://docs.microsoft.com/intune/enrollment-autopilot)<br>
[Windows の自動操縦のシナリオと機能](windows-autopilot-scenarios.md)
