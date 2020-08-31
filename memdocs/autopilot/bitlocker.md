---
title: 自動操縦デバイスの BitLocker 暗号化アルゴリズムの設定
ms.reviewer: ''
manager: laurawi
description: Microsoft Intune には、Windows 10 デバイスで BitLocker を管理するための包括的な構成オプションのセットが用意されています。
keywords: 自動操縦、BitLocker、暗号化、256ビット、Windows 10
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
ms.openlocfilehash: f72410d0570e1b9ebbc324f26a288100e744f422
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056991"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>自動操縦デバイスの BitLocker 暗号化アルゴリズムの設定

**適用対象**

-  Windows 10

Windows 自動操縦では、自動暗号化を開始する前に、BitLocker 暗号化の設定を適用するように構成できます。 この構成により、既定の暗号化アルゴリズムが自動的に適用されないようにします。 BitLocker の自動暗号化を開始する前に、他の BitLocker ポリシーを適用することもできます。 

Bitlocker 暗号化アルゴリズムは、BitLocker が最初に有効になったときに使用されます。 このアルゴリズムは、フルボリューム暗号化の強度を設定します。 使用できる暗号化アルゴリズムは、AES-CBC 128-bit、AES-CBC 256-bit、XTS-AES 128 ビット、または XTS-AES-AES 256 ビット暗号化です。 既定値は、XTS-AES-AES 128 ビット暗号化です。 使用する推奨暗号化アルゴリズムの詳細については、「 [BITLOCKER CSP](/windows/client-management/mdm/bitlocker-csp) 」を参照してください。

自動で暗号化する前に、必要な BitLocker 暗号化アルゴリズムが次のように設定されていることを確認します。

1. Windows 10 Endpoint Protection プロファイルの [暗号化方法設定](/intune/endpoint-protection-windows-10#windows-encryption) を、必要な暗号化アルゴリズムに構成します。 
2. Autopilot デバイス グループに[ポリシーを割り当てます](/intune/device-profile-assign)。 暗号化ポリシーは、ユーザーではなく、グループ内の **デバイス** に割り当てる必要があります。
3. これらのデバイスについて、Autopilot の[登録ステータス ページ](enrollment-status.md) (ESP) を有効にします。 ESP が有効になっていない場合は、暗号化が開始される前にポリシーが適用されません。

Microsoft Intune Windows 暗号化設定の例を次に示します。

![BitLocker 暗号化の設定](images/bitlocker-encryption.png)

暗号化アルゴリズムを変更する前に、自動的に暗号化されるデバイスを復号化する必要があります。

設定は、[**デバイス構成**] [プロファイル] [  >  **Profiles**  >  **プロファイルの作成**]  >  **Platform** 、[windows 10 以降]、[プロファイルの種類]、[Endpoint protection > **Configure**  >  **Windows 暗号化**  >  **BitLocker の基本設定**を構成する]、[暗号化メソッドを構成する] = [有効] の下で使用できます。

**Windows 暗号化**の  >  **windows 設定**  >  **Encrypt** = Require を設定することもお勧めします。

## <a name="requirements"></a>要件

Windows 10 バージョン1809以降。

## <a name="next-steps"></a>次の手順

[BitLocker の概要](/windows/security/information-protection/bitlocker/bitlocker-overview)