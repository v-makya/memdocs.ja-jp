---
title: Microsoft Intune で Windows Phone 8.1 デバイスにカスタム設定を追加する - Azure | Microsoft Docs
titleSuffix: ''
description: Microsoft Intune で Windows Phone 8.1 を実行するデバイス用の OMA-URI 設定を使用するためのカスタム プロファイルを追加または作成します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0adb573dbb40f00a1b43b9fb356cdc20b97b669
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910079"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Intune で Windows Phone 8.1 デバイス用のカスタム設定を使用する

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Microsoft Intune では、"カスタム プロファイル" を使用して Windows Phone 8.1 デバイス用のカスタム設定を追加または作成できます。 カスタム プロファイルは Intune の機能です。 Intune に組み込まれていないデバイスの設定と機能を追加するように設計されています。

Windows Phone 8.1 のカスタム プロファイルでは、Open Mobile Alliance Uniform Resource Identifier (OMA-URI) の設定を使用してさまざまな機能を構成します。 通常、これらの設定は、デバイスの機能を制御するためにモバイル デバイスの製造元によって使われます。 この設定は、「[Windows Phone 8.1 の MDM プロトコルのドキュメント](/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10))」に記載されています。

この記事では、Windows Phone 8.1 デバイス用のカスタム プロファイルを作成する方法を示します。 

## <a name="before-you-begin"></a>始める前に

[Windows Phone 8.1 カスタム プロファイルを作成します](custom-settings-configure.md)。

## <a name="custom-oma-uri-settings"></a>OMA-URI のカスタム設定

- **OMA-URI 設定**:以下の設定を**追加**します。

  - **名前**:OMA-URI 設定の一意の名前を入力すると、設定リスト内で容易に識別できます。
  - **説明**:設定の概要と、プロファイルを特定するために役立つその他の関連情報についての説明を入力します。
  - **[OMA-URI]** (大文字と小文字を区別):設定として使用する OMA-URI を入力します。
  - **[データ型]** :この OMA-URI の設定に使用するデータ型を選択します。 次のようなオプションがあります。

    - 文字列型
    - 文字列 (XML ファイル)
    - 日付と時刻
    - 整数型
    - 浮動小数点
    - ブール型
    - Base64 (ファイル)

  - **[値]** :入力した OMA-URI に関連付けるデータ値を入力します。 値は、選択したデータ型に依存します。 たとえば、 **[日付と時刻]** を選択した場合は、日付の選択から値を選択します。

  設定を何か追加した後は、 **[エクスポート]** を選択できます。 **[エクスポート]** では、追加した値の一覧がコンマ区切り値 (.csv) ファイルで作成されます。

## <a name="example"></a>例

次の例では、Windows 8.1 Phone デバイスが通信事業者の範囲外に移動したときに、携帯ネットワークを変更できなくなります。

- **名前**:携帯データのローミングを許可する
- **説明**:携帯データネットワークのローミングを許可または禁止します
- **[OMA-URI]** (大文字と小文字を区別): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **[データ型]** :整数型
- **値**:0

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当てて](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Windows 10 デバイスでカスタム プロファイル](custom-settings-windows-10.md)を作成します。