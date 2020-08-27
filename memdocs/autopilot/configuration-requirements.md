---
title: Windows 自動操縦の構成要件
ms.reviewer: ''
manager: laurawi
description: Windows の自動操縦展開の構成要件について通知します。
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
ms.openlocfilehash: 8731532ff052c626514d9f1a80e3a93c0cbde6dc
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908320"
---
# <a name="windows-autopilot-configuration-requirements"></a>Windows 自動操縦の構成要件

**適用対象: Windows 10**

Windows 自動操縦を使用する前に、一般的な自動操縦シナリオをサポートするためにいくつかの構成タスクが必要です。 

- Azure Active Directory の自動登録を構成します。 Microsoft Intune については、「 [Windows 10 の自動登録を有効にする](/intune/windows-enroll#enable-windows-10-automatic-enrollment) 」を参照してください。 別の MDM サービスを使用している場合は、そのサービスに必要な特定の Url または構成についてベンダーに問い合わせてください。
- Azure Active Directory カスタムブランド化を構成します。 組織固有のログオンページを表示するには、表示するイメージとテキストを使用して Azure Active Directory を構成する必要があります。 詳細については、「 [クイックスタート: Azure AD のサインインページに会社のブランドを追加する](/azure/active-directory/fundamentals/customize-branding)」を参照してください。 自動操縦の主要な要素には、"正方形のロゴ"、"サインインページのテキスト"、および Azure Active Directory テナント名が含まれます。 テナント名は、Azure AD テナントのプロパティで個別に構成されます。
- 省略可能: Windows 10 Pro から Windows 10 Enterprise に自動的にステップアップするには、 [Windows サブスクリプションのアクティブ化](/windows/deployment/windows-10-enterprise-subscription-activation)を有効にします。

その場合、特定のシナリオには追加の要件があります。 一般に、次の2つのタスクがあります。

- デバイス登録。 Windows の自動操縦のシナリオをサポートするには、Windows 自動操縦にデバイスを追加する必要があります。 詳細については、「 [Windows 自動操縦にデバイスを追加する](add-devices.md)」を参照してください。
- プロファイルの構成。 デバイスが Windows 自動操縦装置に追加されたら、設定のプロファイルを各デバイスに適用する必要があります。 詳細については、「 [自動操縦プロファイルの構成](profiles.md) 」をご覧ください。  このプロファイル割り当てを自動化 Microsoft Intune ことができます。 詳細については、「 [自動操縦デバイスグループを作成](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) する」および「 [デバイスグループに自動操縦展開プロファイルを割り当てる](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group)」を参照してください。

詳細については、「 [Windows 自動操縦のシナリオ](windows-Autopilot-scenarios.md)」を参照してください。

これらの手順と関連する手順のチュートリアルについては、次のビデオを参照してください。

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


[Windows 10 を実行するための要件](https://www.microsoft.com/windows/windows-10-specifications)以外に、Windows 10 Autopilot を使用するための追加のハードウェア要件はありません

**次の手順**

[Windows 自動操縦の概要](windows-autopilot.md)