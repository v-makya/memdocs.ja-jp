---
title: Microsoft Intune での macOS カーネル拡張機能の設定 - Azure | Microsoft Docs
titleSuffix: ''
description: macOS デバイスでカーネル拡張機能を使用するための設定を追加、構成、作成します。 また、承認された拡張機能をユーザーがオーバーライドできるようにしたり、チーム識別子からすべての拡張機能を許可したり、Microsoft Intune で特定の拡張機能またはアプリを許可したりします。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e18fad8f1112681a62bcdacd63c652cfd4ad3ac
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359286"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>Intune でカーネル拡張機能を構成して使用するための macOS デバイスの設定

この記事では、macOS デバイスで制御できるさまざまなカーネル拡張機能の設定の一覧を示して説明します。 モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使用してデバイスでカーネル拡張機能を追加および管理します。

Intune でのカーネル拡張機能と前提条件について詳しくは、[macOS カーネル拡張機能の追加](kernel-extensions-overview-macos.md)に関するページをご覧ください。

これらの設定は、Intune でデバイスの構成プロファイルに追加した後、ご使用の macOS デバイスに割り当てたり展開したりします。

## <a name="before-you-begin"></a>始める前に

[デバイスのカーネル拡張機能構成プロファイルを作成します](kernel-extensions-overview-macos.md)。

> [!NOTE]
> これらの設定は、さまざまな登録の種類に適用されます。 さまざまな登録の種類の詳細については、[macOS の登録](../enrollment/macos-enroll.md)に関する記事を参照してください。

## <a name="kernel-extensions"></a>カーネル拡張機能

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>これらの設定は次に適用されます。ユーザーが承認したデバイス登録と、自動化されたデバイス登録

- **[ユーザーによる上書きを許可]** : **[許可]** を選択すると、ユーザーは構成プロファイルに含まれていないカーネル拡張機能を承認できます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、OS により、ユーザーは構成プロファイルに含まれていない拡張機能を許可されない可能性があります。 つまり、構成プロファイルに含まれている拡張機能のみが許可されます。

  この機能について詳しくは、「[ユーザーが承認したカーネル拡張機能の読み込み](https://developer.apple.com/library/archive/technotes/tn2459/_index.html)」(Apple の Web サイトが開きます) をご覧ください。

- **[許可するチーム識別子]** : 1 つまたは複数のチーム ID を許可するには、この設定を使用します。 入力したチーム ID で署名されたカーネル拡張機能は、許可されて信頼されます。 つまり、同じチーム ID (特定の開発者またはパートナーにできます) 内のすべてのカーネル拡張を許可するには、このオプションを使用します。

  読み込む対象の有効で署名されたカーネル拡張機能のチーム識別子を**追加**します。 複数のチーム識別子を追加できます。 チーム識別子は、10 文字の英数字 (文字と数字) である必要があります。 たとえば、「`ABCDE12345`」と入力します。

  チーム識別子を追加した後は、削除することもできます。

  詳細については、「[チーム ID を確認する](https://help.apple.com/developer-account/#/dev55c3c710c)」 (Apple の Web サイトが開きます) を参照してください。

- **[許可するカーネル拡張機能]** : 特定のカーネル拡張機能を許可するには、この設定を使用します。 入力したカーネル拡張機能のみが許可または信頼されます。

  読み込むカーネル拡張機能のバンドル識別子とチーム識別子を**追加**します。 署名されていないレガシ カーネル拡張機能の場合は、空のチーム識別子を使用します。 複数のカーネル拡張機能を追加できます。 チーム識別子は、10 文字の英数字 (文字と数字) である必要があります。 たとえば、 **[バンドル ID]** に「`com.contoso.appname.macos`」と入力し、 **[チーム識別子]** に「`ABCDE12345`」と入力します。

  > [!TIP]
  > macOS デバイスでカーネル拡張機能 (Kext) のバンドル ID を取得するには、次のようにします。
  >
  > 1. ターミナルで `kextstat | grep -v com.apple` を実行し、出力を確認します。 必要なソフトウェアまたは Kext をインストールします。 `kextstat | grep -v com.apple` をもう一度実行し、変わったところを探します。
  >
  >    ターミナルで `kextstat` を実行すると、OS のすべてのカーネル拡張機能が一覧表示されます。 
  >
  > 2. デバイスで、Kext の情報プロパティ リスト ファイル (Info.plist) を開きます。 バンドル ID が表示されます。 各 Kext の内部には、Info.plist ファイルが格納されています。

> [!NOTE]
> チーム識別子とカーネル拡張機能を追加する必要はありません。 どちらか一方を構成できます。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。
