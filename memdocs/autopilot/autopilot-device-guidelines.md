---
title: Windows 自動操縦用デバイスのガイドライン
ms.reviewer: ''
manager: laurawi
description: Windows 自動操縦の展開に関するハードウェア、ファームウェア、およびソフトウェアのベストプラクティスについて説明します。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
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
ms.openlocfilehash: 328886f0fac3fad55c2e8bc26769784fd3d8b910
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757426"
---
# <a name="windows-autopilot-device-guidelines"></a>Windows 自動操縦用デバイスのガイドライン

**適用対象**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>Windows 自動操縦のハードウェアとファームウェアのベストプラクティスガイドライン

Windows 自動操縦装置で使用するすべてのデバイスは、Windows 10 の[最小ハードウェア要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)を満たしている必要があります。  

次のベストプラクティスでは、デバイスを Windows 自動操縦展開プロセスの一部として簡単にプロビジョニングできます。 
- Windows 自動操縦用の自己展開モード用のデバイスで、TPM 2.0 が有効であり、(**機能が制限**されていない) 良好な状態であることを確認します。
- OEM は、一意のタプル情報 (SmbiosSystemManufacturer、Smbiossystemmanufacturer、Smbiossystemmanufacturer) または PKID + Smbiossystemmanufacturer[を、Microsoft](https://docs.microsoft.com/windows-hardware/drivers/bringup/smbios)仕様 (製造元、製品名、および smbios type 1 04h に格納されているシリアル番号) にプロビジョニングします。
- OEM は、OA3 Tool RS3 + を使用して取得した4K ハードウェアハッシュを、システム全体で CBR レポートを通じて Microsoft にアップロードしてから、デバイスを自動操縦顧客またはチャネルパートナーに発送します。
- Microsoft では、送信されている CBR から30日以内に、OEM 出荷用ドライバーが Windows Update に公開されることを必須としています。 システムのファームウェアとドライバーの更新プログラムは、14日以内に Windows Update に発行されます。
- OEM は、SMBIOS でプロビジョニングされた PKID がチャネルに渡されることを保証します。

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>Windows 自動操縦のソフトウェアのベストプラクティスガイドライン

- Windows 自動操縦用デバイスには、Windows 10 の基本イメージとドライバーだけがプレインストールされている必要があります。
- [Enterprise 用 Microsoft 365 アプリ](https://docs.microsoft.com/deployoffice/about-office-365-proplus-in-the-enterprise)など、ライセンスされているバージョンの Office をプレインストールできます。
- 顧客によって明示的に要求された場合を除き、他にプレインストールされたソフトウェアは含まれません。
  - OEM ポリシーごとに、組み込みアプリを含む Windows 10 の機能を無効にしたり、削除したりしないでください。

## <a name="related-topics"></a>関連トピック

[Windows 自動操縦顧客の同意](registration-auth.md)<br>
[マザーボード交換シナリオのガイダンス](autopilot-mbr.md)<br>
