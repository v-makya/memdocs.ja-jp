---
title: Windows Autopilot のライセンス要件
ms.reviewer: ''
manager: laurawi
description: Windows 自動操縦展開のライセンス要件について通知します。
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
ms.openlocfilehash: 22f9b5f8e93339bc41403b2acf6e4ce53395a139
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993779"
---
# <a name="windows-autopilot-licensing-requirements"></a>Windows Autopilot のライセンス要件

**適用対象: Windows 10**

Windows の自動操縦は、Windows 10 および Azure Active Directory で使用できる特定の機能に依存します。 また、Microsoft Intune などの MDM サービスも必要です。 これらの機能は、さまざまなエディションおよびサブスクリプション プログラムを通じて入手できます。

必要な Azure Active Directory (MDM の自動登録と会社のブランド化機能) と MDM 機能を提供するには、次のいずれかのサブスクリプションが必要です。
- [Premium サブスクリプションの Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1 または F3 サブスクリプション](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 アカデミック A1、A3、または A5 サブスクリプション](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise E3 または E5 サブスクリプション](https://www.microsoft.com/microsoft-365/enterprise)。すべての Windows 10、Microsoft 365、および EM + S の機能 (Azure AD および Intune) が含まれます。
- [Enterprise Mobility + Security E3 または E5 サブスクリプション](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)。必要なすべての Azure AD と Intune の機能が含まれています。
- [Intune for Education サブスクリプション](/intune-education/what-is-intune-for-education)。必要なすべての Azure AD と Intune の機能が含まれます。
- [Azure Active Directory Premium P1、P2](https://azure.microsoft.com/services/active-directory/) 、 [Microsoft Intune サブスクリプション](https://www.microsoft.com/cloud-platform/microsoft-intune) (または代替 MDM サービス)。

> [!NOTE]
> Microsoft 365 サブスクリプションを使用している場合でも、 [Intune のライセンスをユーザーに割り当てる](/intune/fundamentals/licenses-assign)必要があります。

また、次のものも推奨されます (必須ではありません)。
- [Microsoft 365 enterprise 用アプリ](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0)。 Intune (またはその他の MDM サービス) を使用して簡単に展開できます。
- Windows 10 Pro から Windows 10 Enterprise にデバイスを自動的にステップアップする[Windows サブスクリプションのライセンス認証](/windows/deployment/windows-10-enterprise-subscription-activation)。

**次の手順**

[Windows 自動操縦の構成要件](configuration-requirements.md)