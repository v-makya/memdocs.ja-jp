---
title: Intune のエンドポイント セキュリティのアカウント保護ポリシー設定 | Microsoft Docs
description: Microsoft Intune のエンドポイント セキュリティのアカウント保護ポリシー設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431996"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのアカウント保護ポリシー設定

[エンドポイント セキュリティ ポリシー](../protect/endpoint-security-policy.md)の一部として、Intune のエンドポイント セキュリティ ノードにある*アカウント保護*ポリシーのプロファイルで構成できる設定を確認します。

サポートされているプラットフォームとプロファイルは、次のとおりです。

- **Windows 10 以降**:
  - プロファイル:**アカウント保護** *(プレビュー)*


## <a name="account-protection-profile"></a>アカウント保護プロファイル

### <a name="account-protection"></a>アカウント保護

- **Windows Hello for Business をブロックする**

  Windows Hello for Business は、パスワード、スマート カード、および仮想スマート カードを置き換えることで Windows にサインインする代替方法です。
  - **未構成** (*既定値*) - デバイスによって Windows Hello for Business がプロビジョニングされます。
  - **無効** - デバイスによって Windows Hello for Business がプロビジョニングされます。
  - **有効** - デバイスでは、どのユーザーに対しても Windows Hello for Business がプロビジョニングされません。
  
- **サインインのセキュリティ キーの使用を有効にする**

  テナント内のすべての PC のサインイン情報として、Windows Hello セキュリティ キーを有効にします。
  - **[未構成]** ("*既定値*")
  - **あり**

- **Credential Guard を有効にする**  
  [CSP: []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard は、Windows ハイパーバイザーを使用して保護を提供します。 Credential Guard でのセキュア ブートと DMA 保護でハードウェア サポートが必要です。 この設定は、ハードウェア要件を満たすデバイスでのみ成功します。
  - **未構成** (*既定値*) - Credential Guard の使用を無効にします。Windows ではこれが既定値です。
  - **UEFI ロックで有効にする** - Credential Guard を有効にし、それをリモートでオフにできないようにします。UEFI で永続化された構成は手動でクリアする必要があるためです。
  - **UEFI ロックなしで有効にする** - Credential Guard を有効にし、コンピューターへの物理的なアクセスなしにオフにすることを許可します。

## <a name="next-steps"></a>次のステップ

[アカウント保護のエンドポイント セキュリティ ポリシー](../protect/endpoint-security-account-protection-policy.md)
