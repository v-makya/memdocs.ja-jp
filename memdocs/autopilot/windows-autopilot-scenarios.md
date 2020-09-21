---
title: Windows の自動操縦のシナリオと機能
description: ビジネスに対応した状態でデバイスを再展開するなど、一般的な Windows 自動操縦の展開シナリオに従ってください。
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
ms.openlocfilehash: 1755399ad67cd073c71f2a26ef4305bec5a53f51
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814874"
---
# <a name="windows-autopilot-scenarios-and-capabilities"></a>Windows の自動操縦のシナリオと機能

**適用先:Windows 10**

## <a name="scenarios"></a>シナリオ

Windows の自動操縦は、組織が一般的に必要とするシナリオのリストをサポートします。 これらのニーズは次によって異なります。
- 組織の種類。
- Windows 10 への移行の進行状況。
- [最新の管理に](/windows/client-management/manage-windows-10-in-your-organization-modern-management)どの程度移行したか。

このガイドでは、次の Windows 自動操縦シナリオについて説明します。

| シナリオ | 説明 |
| --- | --- |
| エンドユーザーが自分で設定できるようにデバイスをデプロイおよび構成する | [Windows Autopilot ユーザードリブン モード](user-driven.md) |
| 共有使用、キオスク、またはデジタル看板デバイスとして自動的に構成されるデバイスを展開します。| [Windows Autopilot の自己展開モード](self-deploying.md) |
| デバイスをビジネス対応の状態で再デプロイします。| [Windows Autopilot のリセット](windows-autopilot-reset.md) |
| 最新のアプリケーション、ポリシー、および設定を使用してデバイスを事前にプロビジョニングします。| [ホワイト グローブ](white-glove.md) |
| 既存の Windows 7 または8.1 デバイスに Windows 10 を展開する | [既存のデバイス向け Windows Autopilot](existing-devices.md) |

次のビデオでは、これらのシナリオについてまとめています。

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4Ci1b?autoplay=false]

## <a name="windows-autopilot-capabilities"></a>Windows 自動操縦機能

### <a name="windows-autopilot-is-self-updating-during-oobe"></a>Windows 自動操縦は、OOBE 中に自己更新する

Windows 10 バージョン1903以降のデバイスでは、自動操縦機能と重要な更新プログラムが、両方の後に OOBE 中に自動的にダウンロードされます。
- デバイスはネットワークに接続されています。
- [重要なドライバーおよび Windows のゼロデイ修正プログラム (ZDP) の更新](/windows-hardware/customize/desktop/windows-updates-during-oobe)が完了しました。

これらの自動操縦の更新プログラムは、Windows の自動操縦展開に必要であるため、オプトアウトすることはできません。 Windows は、デバイスが更新プログラムを確認し、ダウンロードし、インストールしていることをユーザーに通知します。

詳細については、「 [Windows 自動操縦更新](autopilot-update.md)」を参照してください。

### <a name="cortana-voiceover-and-speech-recognition-during-oobe"></a>OOBE 中の Cortana voiceover と音声認識

Windows 10 バージョン1903以降では、OOBE 中の Cortana voiceover と音声認識は既定で無効になっています。 この既定値は、すべての Windows 10 Pro、教育、および Enterprise Sku に適用されます。

次のレジストリキーを作成して、OOBE 中に Cortana voiceover と音声認識を有効にすることもできます。 既定では、このキーは存在しません。

HKLM\Software\Microsoft\Windows\CurrentVersion\OOBE\EnableVoiceForAllEditions

キー値は、 **0** = disabled で **1** = enabled の DWORD です。

| [値] | 説明 |
| --- | --- |
| 0 | Cortana voiceover が無効になっています |
| 1 | Cortana voiceover が有効になっています |
| 値なし | デバイスは、エディションの既定の動作にフォールバックします。 |

このキー値を変更するには、WCD ツールを使用して、 [ここ](/windows/configuration/wcd/wcd-oobe#nforce)に記載されているように ppkg として作成します。

### <a name="bitlocker-encryption"></a>BitLocker 暗号化

Windows 自動操縦を使用すると、自動暗号化を開始する前に適用する BitLocker 暗号化設定を構成できます。 詳細については、「[自動操縦デバイスの BitLocker 暗号化アルゴリズムの設定](bitlocker.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

[Windows 自動操縦: 新機能](windows-autopilot-whats-new.md)