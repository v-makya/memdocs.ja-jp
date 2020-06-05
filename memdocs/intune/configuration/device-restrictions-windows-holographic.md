---
title: Windows Holographic Business デバイスの設定 - Microsoft Intune - Azure | Microsoft Docs
description: Windows Holographic for Business の Microsoft Intune でのデバイス制限設定について説明し、これらの設定を構成します。 登録解除、位置情報、パスワード、アプリ ストアからのアプリのインストール、Microsoft Edge の Cookie とポップアップ、Microsoft Defender、検索、クラウドとストレージ、Bluetooth 接続、システム時刻、使用状況データなどを制御します。
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
ms.openlocfilehash: 301cdd9403b0bb3e2d64c8707782ecbc639dc044
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556050"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune を使用して機能を許可または制限する Windows Holographic for Business デバイスの設定

この記事では、Microsoft Hololens などの Windows Holographic for Business デバイス上で制御できる、さまざまな設定について説明します。 モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使って機能の許可や無効化、セキュリティ管理などを行います。

Intune 管理者は、デバイスに対してこれらの設定を作成し、割り当てることができます。

## <a name="before-you-begin"></a>始める前に

[Windows 10 デバイス制限の構成プロファイルを作成します](device-restrictions-configure.md#create-the-profile)。

Windows 10 デバイス制限の構成プロファイルを作成する場合、この記事に記載されているものよりも多くの設定があります。 この記事の設定は、Windows Holographic for Business デバイスでサポートされています。

## <a name="app-store"></a>アプリ ストア

- **[ストア アプリの自動更新]** : **[ブロック]** を選択すると、更新プログラムが Microsoft Store から自動的にインストールされなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、Microsoft Store からインストールされたアプリの自動更新が OS で許可されている可能性があります。

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **[信頼できるアプリのインストール]** :Microsoft Store 以外のアプリをインストールできる場合に選択します。これはサイドローディングとも呼ばれます。 サイドローディングでは、Microsoft Store によって認定されていないアプリのインストール後に、アプリが実行されるかテストされます。 たとえば、社内でのみ使用されるアプリです。 次のようなオプションがあります。
  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[ブロック]** :サイドローディングを禁止します。 Microsoft Store 以外のアプリをインストールすることはできません。
  - **[許可]** :サイドローディングを許可します。 Microsoft Store 以外のアプリをインストールできます。

  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **[開発者によるロック解除]** :サイドロードされたアプリのユーザーによる変更を許可するなど、Windows の開発者向け設定を許可します。 次のようなオプションがあります。
  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[ブロック]** :開発者モードとアプリのサイドローディングを禁止します。
  - **[許可]** :開発者モードとアプリのサイドローディングを許可します。

  [ApplicationManagement/AllowDeveloperUnlock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>携帯ネットワークと接続性

- **[Bluetooth]** : **[ブロック]** に設定すると、ユーザーは Bluetooth を有効にできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、デバイスの Bluetooth が OS で許可される場合があります。

  [Connectivity/AllowBluetooth CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **[Bluetooth の検出可能性]** : **[ブロック]** に設定すると、このデバイスは他の Bluetooth 対応デバイスで検出されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、ヘッドセットなどの他の Bluetooth 対応デバイスからのこのデバイスの検出が OS で許可されている可能性があります。

  [Bluetooth/AllowDiscoverableMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **[Bluetooth 広告]** : **[ブロック]** に設定すると、デバイスは Bluetooth 広告を送信できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、デバイスによる Bluetooth 広告の送信が OS で許可されている可能性があります。

  [Bluetooth/AllowAdvertising CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>クラウドとストレージ

- **[Microsoft アカウント]** : **[ブロック]** にすると、ユーザーは Microsoft アカウントをデバイスに関連付けることができなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、Microsoft アカウントの追加と使用が OS で許可されている可能性があります。

  [Accounts/AllowMicrosoftAccountConnection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>コントロール パネルと設定

- **[システム時刻の変更]** : **[ブロック]** に設定すると、ユーザーはデバイスの日付と時刻の設定を変更できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、OS により、ユーザーはこれらの設定の変更を許可される場合があります。

  [Settings/AllowDateTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>全般

- **[手動での登録解除]** : **[ブロック]** に設定すると、ユーザーはデバイスでワークプレース コントロール パネルを使用して職場アカウントを削除できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

  [Experience/AllowManualMDMUnenrollment CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **[位置情報]** : **[ブロック]** に設定すると、ユーザーはデバイスで位置情報サービスをオンにできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

  [Experience/AllowFindMyDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **[Cortana]** : **[ブロック]** に設定すると、デバイスで Cortana 音声アシスタントが無効になります。 Cortana がオフの場合でも、ユーザーはデバイス上の項目を検索できます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、Cortana が OS で許可されている可能性があります。

  [Experience/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Microsoft Edge ブラウザー

- **[開始エクスペリエンス]**  >  **[ポップアップを許可する]** : **[はい]** (既定値) に設定すると、Web ブラウザーでポップアップが表示されます。 **[いいえ]** にすると、ブラウザーにポップアップ ウィンドウが表示されなくなります。

  [Browser/AllowPopups CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **[お気に入りと検索]**  >  **[検索候補を表示する]** : **[はい]** (既定値) に設定すると、アドレス バーに検索語句を入力したときに、検索エンジンからサイトが提案されます。 **[いいえ]** にすると、この機能が停止されます。

  [Browser/AllowSearchSuggestionsinAddressBar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **[プライバシーとセキュリティ]**  >  **[Password Manager を許可する]** : **[はい]** (既定値) に設定すると、Microsoft Edge は Password Manager を自動的に使用するようになり、ユーザーはデバイスにパスワードを保存して管理できます。 **[いいえ]** にすると、Microsoft Edge で Password Manager は使用できなくなります。

  [Browser/AllowPasswordManager CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **[プライバシーとセキュリティ]**  >  **[Cookie]** :Web ブラウザーで Cookie を処理する方法を選択します。 次のようなオプションがあります。
  - **[許可]** :Cookie がデバイス上に保存されます。
  - **[すべての Cookie をブロックする]** :Cookie がデバイス上に保存されまません。
  - **[サード パーティの Cookie のみブロックする]** :サード パーティまたはパートナーの Cookie がデバイス上に保存されません。

  [Browser/AllowCookies CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **[プライバシーとセキュリティ]**  >  **[トラッキング拒否ヘッダーを送信する]** : **[はい]** に設定すると、追跡情報を要求している Web サイトにトラッキング拒否ヘッダーが送信されます (推奨)。 **[いいえ]** (既定値) の場合、Web サイトにユーザーの追跡を可能にするヘッダーを送信しません。 ユーザーはこの設定を構成できます。

  [Browser/AllowDoNotTrack CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **[SmartScreen for Microsoft Edge]** : **[必須]** に設定すると、Microsoft Defender SmartScreen がオンになり、ユーザーはそれをオフにすることができなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 OS の既定では、SmartScreen がオンになることがあります。ユーザーはそのオンとオフを切り替えることができます。

  [ブラウザー/AllowSmartScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>パスワード

- **パスワード**: **[必要]** にすると、デバイスにアクセスするユーザーにパスワードの入力が強制されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、パスワードなしでのデバイスへのアクセスが OS で許可されている可能性があります。 ローカル アカウントのみに適用されます。 ドメイン アカウントのパスワードは、Active Directory (AD) および Azure AD によって構成されたままになります。

  [DeviceLock/DevicePasswordEnabled CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **[デバイスがアイドル状態から戻るときにパスワードを必須とする]** : **[必須]** にすると、アイドル状態になった後のデバイスのロックを解除するために、ユーザーにパスワードの入力が強制されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、アイドル状態になった後に PIN またはパスワードが OS で要求されない可能性があります。

  [DeviceLock/AllowIdleReturnWithoutPassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>レポートとテレメトリ

- **[使用状況データの共有]** :送信される診断データのレベルを選択します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。 強制される設定はありません。 ユーザーは、送信されるレベルを選択します。 既定では、OS でデータが共有されない可能性があります。
  - **[セキュリティ]** :Windows のより強力なセキュリティ保護を維持するために必要な情報。接続されたユーザー エクスペリエンスとテレメトリ コンポーネントの設定、悪意のあるソフトウェアの削除ツール、Microsoft Defender に関するデータなどが含まれます
  - **[基本]** : 基本的なデバイス情報。品質に関連するデータ、アプリの互換性、アプリの使用状況データ、およびセキュリティ レベルのデータが含まれます
  - **[拡張]** : 追加の分析情報。Windows、Windows Server、System Center、およびアプリの利用状況、それらのパフォーマンス、詳細な信頼性データ、基本レベルとセキュリティ レベルの両方の情報が含まれます
  - **[完全]** : 問題の特定に必要で、問題の修正にも役立つすべてのデータと、セキュリティ、基本、および拡張レベルのデータ。

  [システム/AllowTelemetry CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>検索

- **場所の検索**: **[ブロック]** に設定すると、Windows Search がその場所を使用できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、OS により、この機能が許可される場合があります。

  [Search/AllowSearchToUseLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当てて](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。
