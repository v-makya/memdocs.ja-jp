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
ms.openlocfilehash: 8c339e2a55fd8876ce8a144bb72c7c0a37de8346
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907836"
---
# <a name="overview-of-windows-autopilot"></a>Windows Autopilot の概要

**適用対象**

-  Windows 10

Windows Autopilot は、新しいデバイスのセットアップと事前構成に使用されるテクノロジのコレクションで、生産性の高い使用ができるようにデバイスを準備するためのものです。 Windows 自動操縦を使用して、デバイスのリセット、転用、および回復を行うこともできます。 このソリューションでは、管理するインフラストラクチャをほとんどあるいはまったく使用せずに、IT 部門は上記の機能を実現できます。また、そのプロセスは簡単でシンプルです。

Windows の自動操縦により、Windows デバイスのライフサイクルが、IT とエンドユーザーの両方にとって、初期のデプロイから終了までの期間に簡略化されます。 クラウドベースのサービスの使用、Windows 自動操縦:
- デバイスの展開、管理、およびインベントリからの削除にかかる時間を短縮します。
- デバイスを管理するために必要なインフラストラクチャを削減します。
- すべての種類のエンドユーザーにとって使いやすさが最大になります。

次のビデオと図を参照してください。

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![プロセスの概要](images/image1.png)

Windows 自動操縦では、新しい Windows デバイスを初めて展開するときに、OEM が最適化したバージョンの Windows 10 を使用します。 このバージョンはデバイスにプレインストールされているため、すべてのデバイスモデルでカスタムイメージとドライバーを維持する必要はありません。 デバイスを再イメージングするのではなく、既存の Windows 10 のインストールを "ビジネス対応" 状態に変換して、次のことが可能になります。
- 設定とポリシーを適用する
- アプリのインストール
- 拡張機能をサポートするために、使用されている Windows 10 のエディション (たとえば、Windows 10 Pro から Windows 10 Enterprise) を変更します。

展開後、次のものを使用して Windows 10 デバイスを管理できます。
- Microsoft Intune
- Windows Update for Business
- Microsoft Endpoint Configuration Manager
- その他の同様のツールもあります。

Windows 自動操縦を使用すると、Windows 自動操縦リセットを使用して新しいユーザーのデバイスをすばやく準備できます。 中断/修正シナリオでリセットを使用して、デバイスをすぐにビジネス対応状態に戻すこともできます。

Windows Autopilot では、次のことを実行できます。
* Azure Active Directory (Azure AD) または Active Directory (Hybrid Azure AD Join による) へデバイスを自動的に参加させる。 これら2つの結合オプションの相違点の詳細については、「 [Azure Active Directory でのデバイス管理の概要](/azure/active-directory/device-management-introduction)」を参照してください。
* Microsoft Intune などの MDM サービスにデバイスを自動登録します ([*構成には Azure AD Premium サブスクリプションが必要です*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067))。
* 管理者アカウントの作成を制限する。
* デバイスのプロファイルに基づいて構成グループを作成し、デバイスをこのグループに自動的に割り当てる。
* 組織に固有の OOBE コンテンツをカスタマイズする。

## <a name="benefits-of-windows-autopilot"></a>Windows Autopilot の利点

従来、IT 担当者は、後でデバイスに展開されるイメージの構築とカスタマイズにかなりの時間を費やしていました。 Windows Autopilot には、新しいアプローチが導入されています。

ユーザー側から見ると、数回の簡単な操作を行うだけで、デバイスを使用する準備が整います。

IT 担当者側から見ると、エンド ユーザーから要求される作業は、ネットワークへの接続とユーザーの資格情報の確認だけです。 それ以外のすべてが自動化されます。

## <a name="requirements"></a>必要条件

Windows 自動操縦を使用するには、 [サポートされているバージョン](/windows/release-information/) の windows 10 半期チャネルが必要です。 Windows 10 Enterprise LTSC 2019 もサポートされています。 詳細については、「 [Windows 自動操縦用ソフトウェア](software-requirements.md)、 [ネットワーク](networking-requirements.md)、 [構成](configuration-requirements.md)、および [ライセンス](licensing-requirements.md) の要件」を参照してください。

## <a name="related-topics"></a>関連トピック

[Windows Autopilot を使用して、Intune での Windows デバイスを登録する](/intune/enrollment-autopilot)<br>
[Windows の自動操縦のシナリオと機能](windows-autopilot-scenarios.md)