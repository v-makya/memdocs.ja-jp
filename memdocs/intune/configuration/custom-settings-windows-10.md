---
title: Microsoft Intune で Windows 10 デバイス用のカスタム設定を追加する - Azure | Microsoft Docs
description: Microsoft Intune で Windows 10 を実行するデバイス用の OMA-URI 設定を使用するためのカスタム プロファイルを追加または作成します。 カスタム プロファイルを使用して、カスタム設定を追加します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28a867c735a05cfa4a4765534d200b806711f9b5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913020"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Intune で Windows 10 デバイス用のカスタム設定を使用する

この記事では、Windows 10 以降のデバイスで制御できるさまざまなカスタム設定の一覧を示して説明します。 モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使用して、Intune に組み込まれていない設定を構成します。

カスタム プロファイルの詳細については、[カスタム設定を持つプロファイルの作成](custom-settings-configure.md)に関するページを参照してください。

これらの設定は、Intune でデバイスの構成プロファイルに追加した後、ご使用の Windows 10 デバイスに割り当てたり展開したりします。

この機能は、以下に適用されます。

- Windows 10 以降

Windows 10 のカスタム プロファイルでは、Open Mobile Alliance Uniform Resource Identifier (OMA-URI) の設定を使用してさまざまな機能を構成します。 通常、これらの設定は、デバイスの機能を制御するためにモバイル デバイスの製造元によって使われます。

Windows 10 では、[ポリシー構成サービス プロバイダー (ポリシー CSP)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers) など、多くの構成サービス プロバイダー (CSP) 設定を使用できます。

特定の設定を探している場合、[Windows 10 デバイス制限プロファイル](device-restrictions-windows-10.md)には多くの組み込み設定が含まれることに留意してください。 そのため、カスタム値の入力は必要ない場合があります。

## <a name="before-you-begin"></a>始める前に

[Windows 10 カスタム プロファイルを作成します。](custom-settings-configure.md#create-the-profile)

## <a name="oma-uri-settings"></a>OMA-URI 設定

**[追加]** :次の設定を入力します。

- **名前**:OMA-URI 設定の一意の名前を入力すると、設定リスト内で容易に識別できます。
- **説明**:設定の概要および他の重要な詳細がわかる説明を入力します。
- **[OMA-URI]** (大文字と小文字を区別):設定として使用する OMA-URI を入力します。
- **[データ型]** :この OMA-URI の設定に使用するデータ型を選択します。 次のようなオプションがあります。

  - Base64 (ファイル)
  - ブール型
  - 文字列 (XML ファイル)
  - 日付と時刻
  - 文字列型
  - 浮動小数点
  - 整数型

- **値**:入力した OMA-URI に関連付けるデータ値を入力します。 値は、選択したデータ型に依存します。 たとえば、 **[日付と時刻]** を選択した場合は、日付の選択から値を選択します。

設定を何か追加した後は、 **[エクスポート]** を選択できます。 **[エクスポート]** では、追加した値の一覧がコンマ区切り値 (.csv) ファイルで作成されます。

## <a name="find-the-policies-you-can-configure"></a>構成できるポリシーを見つける

「[Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference)」(構成サービス プロバイダー リファレンス) には、Windows 10 でサポートされているすべての構成サービス プロバイダー (CSP) の詳細な一覧が記載されています。

Windows 10 のバージョンによっては、一部の設定に互換性がありません。 各 CSP でサポートされるバージョンについては、「[Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference)」(構成サービス プロバイダー リファレンス) を参照してください。

また、「[Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference)」(構成サービス プロバイダー リファレンス) に記載されているすべての設定が Intune でサポートされているわけではありません。 Intune で必要な設定がサポートされているかどうかを確認するには、その設定の記事を開きます。 各設定ページには、サポートされている操作が示されます。 Intune で利用するには、その設定で**追加**、**置換**、**取得**の操作がサポートされている必要があります。 **取得**の操作によって返された値が**追加**または**置換**の操作によって得た値と一致しない場合、Intune ではコンプライアンス エラーが報告されます。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Intune のカスタム プロファイルの詳細を確認します](custom-settings-configure.md)。