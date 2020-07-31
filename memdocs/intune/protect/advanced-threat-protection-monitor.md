---
title: Microsoft Intune で Microsoft Defender Advanced Threat Protection (ATP) の統合を監視する - Azure | Microsoft Docs
description: Intune で Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を監視します。これには、デバイスのコンプライアンスやオンボードの状態が含まれます。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264536"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>Microsoft Defender ATP を Intune と統合する場合にデバイスの状態を監視する

Microsoft Intune と Microsoft Defender Advanced Threat Protection (ATP) を統合すると、Microsoft Endpoint Manager admin center でデバイスのコンプライアンスとオンボードに関する情報を表示できます。

## <a name="monitor-device-compliance"></a>デバイス コンプライアンスを監視する

Microsoft Defender ATP コンプライアンス ポリシーを持つデバイスの状態を監視します。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[モニター]**  >  **[ポリシー コンプライアンス]** の順に選択します。

3. 一覧から Microsoft Defender ATP ポリシーを探し、どのデバイスが準拠または非準拠なのかを確認します。

また、同じ場所から非準拠デバイスに対する "*運用*" レポートを使用することもできます。

- **[デバイス]**  >  **[モニター]**  >  **[非準拠デバイス]** を選択します。

レポートについて詳しくは、「[Intune のレポート](../fundamentals/reports.md)」をご覧ください。

## <a name="view-onboarding-status"></a>オンボードの状態を表示する

Intune マネージド デバイスのオンボード状態を確認するには、 **[エンドポイント セキュリティ]**  >  **[Microsoft Defender ATP]** の順に移動します。 このページからデバイス構成プロファイルを作成し、さらに多くのデバイスを Microsoft Defender ATP にオンボードすることもできます。

## <a name="next-steps"></a>次のステップ

[Intune で条件付きアクセスによる Microsoft Defender ATP のコンプライアンスを強制する](../protect/advanced-threat-protection.md)
