---
title: Microsoft Intune での Surface Hub Windows 10 Team デバイスの制限 - Azure | Microsoft Docs
titleSuffix: ''
description: Intune を使用して、Windows 10 Team を実行している Surface Hub デバイスの設定を追加または構成します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429687"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Intune を使用して Surface Hub デバイスの機能を許可または制限するための Windows 10 Team の設定

この記事では、Windows 10 Team を実行するデバイス (Surface Hub デバイスを含む) に対して構成できる Microsoft Intune デバイスの制限設定について説明します。

## <a name="before-you-begin"></a>始める前に

[デバイス プロファイルを作成します](device-restrictions-configure.md#create-the-profile)。

## <a name="apps-and-experience"></a>アプリとエクスペリエンス

これらの設定には、[SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp) を使用します。

- **[ユーザーの入室時に画面のスリープ状態を解除する]** : **[ブロック]** に設定すると、センサーによって室内に誰かがいることが検出されたときに、画面のスリープ状態が自動的に解除されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[ようこそ画面に表示される会議情報]** :ようこそ画面の [会議] タイルに表示される情報を選択します。 次のようなオプションがあります。
  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[開催者と時間のみ]**
  - **[開催者、時間、件名 (プライベートの会議の場合、件名は非表示)]**
- **[ようこそ画面の背景画像の URL]** :Windows 10 Team デバイスの**ようこそ**画面でカスタムの背景として使用する .png イメージの URL を入力します。 画像は PNG 形式である必要があり、URL は `https://` で始まっている必要があります。
- **[接続の自動起動]** : **[ブロック]** に設定すると、プロジェクションの開始時に接続アプリが自動的に開かなくなります。 ブロックされている場合、ユーザーは Hub の設定から接続アプリを手動で起動できます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[サインイン候補]** : **[ブロック]** に設定すると、スケジュールされている会議に招待された人をサインイン ダイアログに自動入力する機能が無効になります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[会議とファイル]** : **[ブロック]** に設定すると、[スタート] メニューの **[会議とファイル]** 機能が無効になります。 この機能を使用すると、サインインしているユーザーの会議とファイルを Office 365 から確認できます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **[Azure Operational Insights]** : **[有効]** に設定すると、Azure Operational Insights を使用して Windows 10 Team デバイスからログ データを収集、保存、および分析できます。 Azure Operational Insights は、Microsoft Operations Manager スイートの一部です。 Azure Operational Insights に接続するには、 **[ワークスペース ID]** と **[ワークスペース キー]** を入力します。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、OS によってこのデータが収集されない場合があります。

## <a name="maintenance"></a>メンテナンス

これらの設定には、[SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp) を使用します。

- **[更新プログラムのメンテナンス期間]** : **[有効]** に設定すると、更新プログラムをインストールできるメンテナンス期間が作成されます。 メンテナンス期間の **[開始時刻]** と、 **[期間 (時間単位)]** (1 から 5 時間) を入力します。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

## <a name="session"></a>セッション

これらの設定には、[SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp) を使用します。

- **[ボリューム]** :新しいセッションの既定のボリューム値 (0 から 100) を入力します。 空のままにすると、Intune によってこの設定は変更または更新されません。 既定では、OS によってボリュームが 45 に設定される場合があります。
- **[スクリーン タイムアウト]** :ハブ スクリーンがオフになるまでの時間を分単位で入力します。
- **[セッションのタイムアウト]** :セッションがタイムアウトになるまでの時間を分単位で入力します。
- **[スリープ タイムアウト]** :ハブがスリープ モードになるまでの時間を分単位で入力します。
- **[セッションの再開]** : **[ブロック]** に設定すると、セッションがタイムアウトしたときに、ユーザーがセッションを再開できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

## <a name="wireless-projection"></a>ワイヤレス投影

これらの設定には、[SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp) を使用します。

- **[ワイヤレス投影の PIN]** : **[必須]** に設定すると、デバイス上でワイヤレス投影機能を使用する前に、ユーザーに PIN の入力が強制されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[Miracast ワイヤレス投影]** : **[ブロック]** に設定すると、Miracast が有効になっているデバイスを使用して投影できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[Miracast ワイヤレス投影チャネル]** :接続を確立する Miracast チャネルを選択します。

## <a name="next-steps"></a>次のステップ

詳細については、[デバイスの制限設定を構成する方法](device-restrictions-configure.md)に関するページを参照してください。

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。
