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
ms.openlocfilehash: eb591206ad61878bc2637bf1a10c2a1cec17ddba
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057364"
---
# <a name="windows-autopilot-device-guidelines"></a>Windows 自動操縦用デバイスのガイドライン

**適用対象**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>Windows 自動操縦のハードウェアとファームウェアのベストプラクティスガイドライン

Windows 自動操縦を使用するすべてのデバイスは、Windows 10 の [最小ハードウェア要件](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) を満たしている必要があります。  

次のベストプラクティスでは、デバイスを Windows 自動操縦展開プロセスの一部として簡単にプロビジョニングできます。 
- Windows 自動操縦用自己展開モードを使用するデバイスでは、TPM 2.0 が有効であり、( **機能が制限モード**ではなく) 良好な状態になっています。
- OEM は、次のいずれかの情報を [SMBIOS フィールド](/windows-hardware/drivers/bringup/smbios)にプロビジョニングする必要があります。 この情報は、Microsoft の仕様 (製造元、製品名、および SMBIOS Type 1 04h に格納されているシリアル番号) に従う必要があります。また、「1 05h」と入力し、「1 07h」と入力します。
    - 一意のタプル情報 (SmbiosSystemManufacturer、Smbiossystemmanufacturer、Smbiossystemmanufacturer)
    - PKID + SmbiosSystemSerialNumber
- デバイスを自動操縦顧客またはチャネルパートナーに発送する前に、OEM は CBR レポートを使用して4K ハードウェアハッシュを Microsoft にアップロードする必要があります。 完全な OS では、OA3 Tool RS3 + run in Audit mode を使用してハッシュを収集する必要があります。
- Microsoft は、OEM 出荷用ドライバーが、CBR 送信日から30日以内に Windows Update に公開されることを必須としています。 システムのファームウェアとドライバーの更新プログラムは、14日以内に Windows Update に発行されます。
- OEM は、SMBIOS でプロビジョニングされた PKID がチャネルに渡されることを保証します。

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>Windows 自動操縦のソフトウェアのベストプラクティスガイドライン

- Windows 自動操縦用デバイスには、Windows 10 の基本イメージとドライバーだけがプレインストールされている必要があります。
- [Enterprise 用 Microsoft 365 アプリ](/deployoffice/about-office-365-proplus-in-the-enterprise)など、ライセンスされているバージョンの Office をプレインストールできます。
- 顧客によって明示的に要求された場合を除き、他にプレインストールされたソフトウェアは含まれません。
  - OEM ポリシーごとに、組み込みアプリを含む Windows 10 の機能を無効にしたり、削除したりしないでください。

## <a name="next-steps"></a>次の手順

[Windows 自動操縦顧客の同意](registration-auth.md)<br>
[マザーボード交換シナリオのガイダンス](autopilot-mbr.md)<br>