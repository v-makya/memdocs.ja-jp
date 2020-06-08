---
title: Microsoft Intune でエンドポイント セキュリティ ポリシーを使用してディスクの暗号化を管理する | Microsoft Docs
description: Microsoft Endpoint Manager でエンドポイント セキュリティのディスクの暗号化ポリシーを使用して、管理するデバイスのポリシーを構成および展開します。
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
ms.openlocfilehash: b988e4ddeb306c7da290c87e8a32fa0571627257
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431671"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのディスクの暗号化ポリシー

エンドポイント セキュリティのディスクの暗号化プロファイルは、FileVault や BitLocker など、デバイスに組み込まれている暗号化方法に関連する設定のみに焦点を置いています。 そのため、セキュリティ管理者は、関連性のないさまざまな設定に移動することなく、ディスク暗号化の設定を簡単に管理できます。

デバイス構成の "*Endpoint Protection*" プロファイルを使用して同じデバイス設定を構成できますが、デバイス構成プロファイルには、追加の設定カテゴリがあります。 これらの追加の設定はディスクの暗号化とは関係がなく、ディスクの暗号化のみを構成するタスクが複雑になる可能性があります。

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) の **[エンドポイント セキュリティ]** ノードにある *[管理]* で、ディスクの暗号化ポリシーのためのエンドポイント セキュリティ ポリシーを見つけます。

## <a name="prerequisites-for-disk-encryption-policy"></a>ディスクの暗号化ポリシーの前提条件

- **macOS** - macOS 10.13 以降
- **Windows** - Windows 10 以降

## <a name="disk-encryption-profiles"></a>ディスクの暗号化プロファイル

**macOS プロファイル**:

- **FileVault** - FileVault には、macOS デバイス用の組み込みのディスク全体の暗号化機能が備わっています。

  macOS 用の [FileVault の設定](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault)を管理します。

  FileVault プロファイルを作成する場合は、[macOS 用の FileVault ディスク暗号化の使用](../protect/encrypt-devices-filevault.md)に関する記事をご覧ください。

**Windows 10 プロファイル**:

- **BitLocker** - BitLocker ドライブ暗号化とは、オペレーティング システムと統合され、紛失または盗難に遭ったか、不適切に使用停止になったコンピューターからのデータの盗難や漏えいの脅威に対処するデータ保護機能です。

  Windows 10 用の[BitLocker の設定](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)を管理します。

  BitLocker プロファイルを作成する場合は、[Windows 10 用の BitLocker ディスク暗号化の使用](../protect/encrypt-devices.md)に関する記事をご覧ください。

## <a name="manage-device-encryption"></a>デバイスの暗号化の管理

デバイスのディスクを暗号化するポリシーを展開した後は、暗号化の管理について、次の記事をご覧ください。

- [BitLocker の管理](../protect/encrypt-devices.md#manage-bitlocker)
- [FileVault の管理](../protect/encrypt-devices-filevault.md#manage-filevault)
- [デバイスの暗号化の監視](../protect/encryption-monitor.md)

## <a name="next-steps"></a>次のステップ

- [FileVault プロファイルを作成するには](../protect/encrypt-devices-filevault.md#create-an-endpoint-security-policy-for-filevault)
- [BitLocker プロファイルを作成するには](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
