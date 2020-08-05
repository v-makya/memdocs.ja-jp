---
title: DFCI の管理
ms.reviewer: ''
manager: laurawi
description: Windows 自動操縦の展開と Intune を使用すると、デバイスファームウェア構成インターフェイス (DFCI) を使用して、UEFI (BIOS) 設定を登録した後に管理できます。
keywords: 自動操縦、DFCI、UEFI、Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 8001eda76a9d655ee37f53b903330f74f1ae9919
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757273"
---
# <a name="dfci-management"></a>DFCI の管理

**適用対象**

-   Windows 10

Windows 自動操縦の展開と Intune を使用すると、デバイスファームウェア構成インターフェイス (DFCI) を使用して、Unified Extensible Firmware Interface (UEFI) 設定を登録した後に管理できます。  DFCI を使用すると、Windows は Intune から UEFI に展開されたデバイスに[管理コマンドを渡すことができ](https://docs.microsoft.com/windows/client-management/mdm/uefi-csp)ます。 これにより、エンドユーザーによる BIOS 設定の制御を制限できます。 たとえば、ブートオプションをロックダウンして、ユーザーが別の OS を起動しないようにすることができます。たとえば、同じセキュリティ機能がない場合などです。

ユーザーが以前のバージョンの Windows を再インストールした場合、別の OS をインストールした場合、またはハードドライブをフォーマットした場合、DFCI 管理を上書きすることはできません。 この機能を使用すると、管理者特権での OS プロセスを含む OS プロセスとマルウェアが通信するのを防ぐことができます。 DFCI の信頼チェーンは公開キー暗号化を使用し、ローカルの UEFI パスワードセキュリティには依存しません。 このセキュリティ層は、ローカルユーザーがデバイスの UEFI メニューから管理設定にアクセスするのをブロックします。

DFCI の利点、シナリオ、前提条件の概要については、「 [Device ファームウェア構成インターフェイス (dfci) の概要](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/)」を参照してください。

## <a name="dfci-management-lifecycle"></a>DFCI 管理ライフサイクル

DFCI 管理ライフサイクルは、UEFI 統合、デバイスの登録、プロファイルの作成、登録、管理、提供終了、回復として表示できます。 次の図を参照してください。

   ![ライフサイクル](images/dfci.png)

## <a name="requirements"></a>必要条件

- Windows 10、バージョン1809以降、およびサポートされている UEFI が必要です。
- デバイスの製造元は、製造プロセスの UEFI ファームウェア、またはインストールするファームウェアの更新として、DFCI を追加する必要があります。 デバイスベンダーと協力して、 [DFCI をサポートする製造元](#oems-that-support-dfci)、または dfci を使用するために必要なファームウェアのバージョンを確認します。
- デバイスは Microsoft Intune で管理する必要があります。 詳細については、「 [Windows 自動操縦を使用した Intune での windows デバイスの登録](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)」を参照してください。
- デバイスは、[Microsoft クラウド ソリューション プロバイダー (CSP) パートナー](https://partner.microsoft.com/membership/cloud-solution-provider)によって Windows Autopilot 用に登録されているか、OEM によって直接登録されている必要があります。 

>[!IMPORTANT]
>自動操縦用に手動で登録され[たデバイス (csv ファイルからのインポート](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot#add-devices)など) では、dfci を使用することはできません。 仕様により、DFCI の管理には、OEM または Microsoft CSP パートナーによる Windows Autopilot への登録により、デバイスの商用購入の外部構成証明が必要です。 デバイスが登録されると、Windows 自動操縦デバイスの一覧にシリアル番号が表示されます。

## <a name="managing-dfci-profile-with-windows-autopilot"></a>Windows 自動操縦を使用した DFCI プロファイルの管理

Windows 自動操縦を使用した DFCI プロファイルの管理には、次の4つの基本的な手順があります。

1. 自動操縦プロファイルを作成する
2. 登録ステータスページプロファイルを作成する
3. DFCI プロファイルを作成する
4. プロファイルを割り当てる

詳細について[は、「プロファイルの作成](https://docs.microsoft.com/intune/configuration/device-firmware-configuration-interface-windows#create-the-profiles)と[プロファイルの割り当て」および「再起動](https://docs.microsoft.com/intune/configuration/device-firmware-configuration-interface-windows#assign-the-profiles-and-reboot)」を参照してください。

また、使用中のデバイスの[既存の DFCI 設定を変更](https://docs.microsoft.com/intune/configuration/device-firmware-configuration-interface-windows#update-existing-dfci-settings)することもできます。 既存の DFCI プロファイルで設定を変更し、変更を保存します。 プロファイルは既に割り当てられているため、次にデバイスが同期したとき、またはデバイスが再起動されたときに、新しい DFCI の設定が有効になります。

## <a name="oems-that-support-dfci"></a>DFCI をサポートする Oem

- [Microsoft Surface](https://docs.microsoft.com/surface/surface-manage-dfci-guide)

追加の Oem が保留中です。

## <a name="see-also"></a>関連項目

[Microsoft DFCI のシナリオ](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/)<br>
[Windows Autopilot と Surface デバイス](https://docs.microsoft.com/surface/windows-autopilot-and-surface-devices)<br>