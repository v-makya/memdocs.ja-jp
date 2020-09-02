---
title: Microsoft Intune での Windows Holographic for Business へのアップグレード - Azure | Microsoft Docs
description: Microsoft Intune のデバイス構成プロファイルを使用して、Windows 10 Holographic for Business にアップグレードします。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65a45b13a91671c1de9bcf04f23156d75313285f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907771"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Windows Holographic を実行するデバイスを Windows Holographic for Business にアップグレードする

Microsoft Intune には、デバイスの管理と保護に役立つ多くの設定が含まれています。 この記事では、Windows Holographic デバイスを Windows Holographic for Business にアップグレードするための設定の一覧を示して説明します。

モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使用して Windows Holographic デバイスをアップグレードします。 Microsoft HoloLens の場合、Commercial Suite を購入してアップグレードに必要なライセンスを入手できます。 詳細については、「[Windows Holographic for Business 機能のロック解除](/hololens/hololens1-upgrade-enterprise)」を参照してください。

Intune 管理者は、デバイスに対してこれらの設定を作成し、割り当てることができます。

この機能の詳細については、[Windows 10 エディションのアップグレードまたは S モードの有効化](edition-upgrade-configure-windows-10.md)に関するページを参照してください。

## <a name="before-you-begin"></a>始める前に

[Windows 10 エディションのアップグレードとモードの切り替えデバイス構成プロファイルを作成します](edition-upgrade-configure-windows-10.md#create-the-profile)。

Windows 10 エディションのアップグレードとモードの切り替えデバイス構成プロファイルを作成する場合、この記事に記載されているものよりも多くの設定があります。 この記事の設定は、Windows Holographic for Business デバイスでサポートされています。

## <a name="edition-upgrade"></a>エディションのアップグレード

- **アップグレード後のエディション**: **[Windows 10 Holographic for Business]** を選択します。
- **ライセンス ファイル**:提供された XML ライセンス ファイルを参照して選択します。

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="Intune で、Holographic for Business のライセンス情報を含む XML ファイル名を入力します。":::

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当てて](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Windows 10 以降](edition-upgrade-windows-settings.md)のデバイス用にエディションのアップグレード プロファイルを作成することもできます。