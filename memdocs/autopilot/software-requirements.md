---
title: Windows の自動操縦ソフトウェアの要件
ms.reviewer: ''
manager: laurawi
description: Windows 自動操縦展開のソフトウェア要件について通知します。
keywords: mdm、セットアップ、windows、windows 10、oobe、管理、展開、自動操縦、ztd、ゼロタッチ、パートナー、msfb、intune
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
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 2eb4f23fbe6126c095f049f36b08adac15c1e02c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907940"
---
# <a name="windows-autopilot-software-requirements"></a>Windows の自動操縦ソフトウェアの要件

**適用対象: Windows 10**

Windows の自動操縦は、Windows 10、Azure Active Directory、MDM サービス (Microsoft Intune など) で使用できる特定の機能に依存します。 Windows の自動操縦を使用してこれらの機能にアクセスするには、いくつかのソフトウェア要件を満たす必要があります。

**注**: Windows 自動操縦を現在サポートしている oem の一覧については、「 [windows 自動操縦](https://aka.ms/windowsAutopilot)」の「参加者のデバイス製造元」セクションを参照してください。

## <a name="software-requirements"></a>ソフトウェア要件

- [サポートされているバージョン](/windows/release-information/)の Windows 10 半期チャネルが必要です。 Windows 10 Enterprise 2019 長期的なサービスチャネル (LTSC) もサポートされています。
- 次のエディションがサポートされています。
  - Windows 10 Pro
  - Windows 10 Pro Education
  - Windows 10 Pro for Workstations
  - Windows 10 Enterprise
  - Windows 10 Education
  - Windows 10 Enterprise 2019 LTSC

>[!NOTE]
>Windows 自動操縦を展開する手順は、特定の製品とバージョンを参照している場合があります。 これらの製品をこのコンテンツに含めることは、サポートライフサイクルを超えるバージョンのサポートの拡張を意味するものではありません。 Windows 自動操縦では、サポートライフサイクルを超える製品はサポートされていません。 詳しくは、「[Microsoft ライフサイクル ポリシー](https://go.microsoft.com/fwlink/p/?LinkId=208270)」をご覧ください。

## <a name="next-steps"></a>次のステップ

[Windows Autopilot ネットワーク要件](networking-requirements.md)