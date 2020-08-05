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
ms.openlocfilehash: 137001d443ba9d5d8e4a8532000a976778e7f818
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757305"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>自動操縦デバイスの BitLocker 暗号化アルゴリズムの設定

**適用対象**

-   Windows 10

Windows 自動操縦を使用すると、自動暗号化を開始する前に適用する BitLocker 暗号化設定を構成できます。 これにより、これが目的の設定でない場合に、既定の暗号化アルゴリズムが自動的に適用されないようになります。 暗号化の前に適用する必要があるその他の BitLocker ポリシーは、BitLocker の自動暗号化を開始する前に配信することもできます。 

Bitlocker 暗号化アルゴリズムは、BitLocker が最初に有効になったときに使用され、ボリューム全体の暗号化を行う強度を設定します。 使用できる暗号化アルゴリズムは、AES-CBC 128-bit、AES-CBC 256-bit、XTS-AES 128 ビット、または XTS-AES-AES 256 ビット暗号化です。 既定値は、XTS-AES-AES 128 ビット暗号化です。 使用する推奨暗号化アルゴリズムの詳細については、「 [BITLOCKER CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) 」を参照してください。

自動暗号化を行う前に、必要な BitLocker 暗号化アルゴリズムが設定されていることを確認するには、次のようにします。

1. Windows 10 の Endpoint Protection プロファイルで[暗号化方法の設定](https://docs.microsoft.com/intune/endpoint-protection-windows-10#windows-encryption)を構成して、目的の暗号化アルゴリズムを選択します。 
2. Autopilot デバイス グループに[ポリシーを割り当てます](https://docs.microsoft.com/intune/device-profile-assign)。 
    - **重要**: 暗号化ポリシーは、ユーザーではなくグループ内の**デバイス**に割り当てる必要があります。
3. これらのデバイスについて、Autopilot の[登録ステータス ページ](enrollment-status.md) (ESP) を有効にします。 
    - **重要**: ESP が有効になっていないと、暗号化の開始前にポリシーが適用されません。

Microsoft Intune Windows 暗号化設定の例を次に示します。

   ![BitLocker 暗号化の設定](images/bitlocker-encryption.png)

**注**: 暗号化アルゴリズムを変更する前に、自動で暗号化されたデバイスの暗号化を解除する必要があります。

この設定は、[デバイスの構成-> プロファイル-> プロファイルの作成-> Platform = Windows 10 以降、プロファイルの種類 = Endpoint protection-> 構成-> Windows 暗号化-> BitLocker 基本設定]、[暗号化メソッドを構成する] = [構成] の下にあります。

**注**: windows 暗号化を設定することもお勧めします。 Windows の設定 > > Encrypt = **Require**です。

## <a name="requirements"></a>必要条件

Windows 10 バージョン1809以降。

## <a name="see-also"></a>関連項目

[BitLocker の概要](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview)
