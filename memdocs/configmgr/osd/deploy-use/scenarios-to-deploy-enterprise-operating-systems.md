---
title: エンタープライズ オペレーティング システムを展開するシナリオ
titleSuffix: Configuration Manager
description: Configuration Manager を使用して、エンタープライズ オペレーティング システムを展開するいくつかのシナリオについて学習します。
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07e8623928cbfe0bcd562d3d6efdf3a9ceee85ae
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708390"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Configuration Manager を使用して、エンタープライズ オペレーティング システムを展開するシナリオ

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、次の OS 展開シナリオを使用することができます。  

#### <a name="upgrade-windows-to-the-latest-version"></a>Windows を最新バージョンにアップグレードする
このシナリオでは、現在、Windows 7、Windows 8.1、または Windows 10 を実行しているコンピューターで OS をアップグレードします。 アップグレード プロセスでは、コンピューター上のアプリケーション、設定、およびユーザー データが保持されます。 Windows ADK などの外部依存関係はありません。 このプロセスは、従来の OS 展開よりも高速となり、回復力が強化される可能性があります。  

詳細については、「[Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md)」をご覧ください。


#### <a name="windows-autopilot-for-existing-devices"></a>既存のデバイス向け Windows Autopilot
<!--3607717, fka 1358333-->
バージョン 1810 以降では、既存のデバイス向けの Windows Autopilot を、Windows 10 バージョン 1809 以降で利用できます。 この機能を利用すると、単一の Configuration Manager タスク シーケンスを使用して、Windows Autopilot ユーザー駆動モード用に Windows 7 デバイスを再イメージ化およびプロビジョニングできます。

詳細については、「[Windows Autopilot for existing devices](windows-autopilot-for-existing-devices.md)」 (既存のデバイス向け Windows Autopilot) を参照してください。


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>新しいバージョンの Windows で既存のコンピューターを更新する
このシナリオでは、既存のコンピューターにパーティションを作成してフォーマット (ワイプ) し、コンピューターに新しい OS をインストールします。 OS をインストールした後、設定とユーザー データを移行できます。  

詳細については、[新しいバージョンの Windows での既存のコンピューターの更新](refresh-an-existing-computer-with-a-new-version-of-windows.md)に関するページを参照してください。


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする
このシナリオでは、新しいコンピューターに OS をインストールします。 これは、OS の新規インストールであり、設定やユーザー データの移行は含まれません。  

詳細については、[新しいコンピューター (ベア メタル) への新しいバージョンの Windows のインストール](install-new-windows-version-new-computer-bare-metal.md)に関するページを参照してください。


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>既存のコンピューターの置き換えと設定の転送
このシナリオでは、新しいコンピューターに OS をインストールします。 必要に応じて、古いコンピューターから新しいコンピューターに設定およびユーザー データを移行できます。  

詳細については、「[Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md)」(既存のコンピューターの置き換えと設定の転送) を参照してください。


