---
title: Microsoft Intune でエンドポイント セキュリティ ポリシーを使用して攻撃のアカウント保護設定を管理する | Microsoft Docs
description: Microsoft Endpoint Manager でエンドポイント セキュリティのアカウント保護ポリシー設定を使用して管理するデバイスのポリシーを構成および展開します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 6fb5702b7c809c7810004a53d084f19fa94dea9e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431853"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのアカウント保護ポリシー

アカウント保護の Intune エンドポイント セキュリティ ポリーを使用して、ユーザーの ID とアカウントを保護します。 アカウント保護ポリシーは、Windows の ID とアクセスの管理の一部である Windows Hello および Credential Guard の設定に焦点を置いています。

- *Windows Hello for Business* は、パスワードを PC やモバイル デバイスでの強力な 2 要素認証に置き換えます。
- *Credential Guard* は、デバイスで使用する資格情報とシークレットの保護に役立ちます。

詳細については、Windows の ID およびアクセス管理に関するドキュメントの「[ID およびアクセス管理](https://docs.microsoft.com/windows/security/identity-protection/)」をご覧ください。

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) の**エンドポイント セキュリティ** ノードにある *[管理]* で、アカウント保護のエンドポイント セキュリティ ポリシーを見つけます。

[アカウント保護プロファイルの設定](../protect/endpoint-security-asr-profile-settings.md)を表示します。

## <a name="prerequisites-for-account-protection-profiles"></a>アカウント保護プロファイルの前提条件

- Windows 10 以降

## <a name="account-protection-profiles"></a>アカウント保護プロファイル

*アカウント保護プロファイルはプレビュー段階です*。

**Windows 10 プロファイル**:

- **アカウント保護** *(プレビュー)* - アカウント保護ポリシーの設定により、ユーザーの資格情報を保護できます。

## <a name="next-steps"></a>次のステップ

[エンドポイント セキュリティ ポリシーを構成する](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
