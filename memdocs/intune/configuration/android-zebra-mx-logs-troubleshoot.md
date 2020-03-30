---
title: Microsoft Intune で Android Zebra デバイスに StageNow ログを使用する - Azure | Microsoft Docs
description: Microsoft Intune で Android デバイスに対して StageNow を使用する際の、よくある問題と解決策を説明します。 また、ログを取得する方法についても説明し、成功またはエラーのログを読み取る方法の例を示します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 607e2303cbec9ec7fc069db602d51684b71e6575
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083838"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Microsoft Intune で Android Zebra デバイスのトラブルシューティングを行い、潜在的な問題を確認する



Microsoft Intune では、[Android Zebra デバイスを管理するために Zebra モビリティ拡張 (MX)](android-zebra-mx-overview.md) を使用することができます。 Zebra デバイスを使用する場合は、設定を管理するために StageNow でプロファイルを作成し、それらを Intune にアップロードします。 Intune では、デバイスに設定を適用するために、StageNow アプリが使用されます。 また、StageNow アプリによって、トラブルシューティングに使用されるデバイスについての詳細なログ ファイルも作成されます。

この機能は、以下に適用されます。

- Android

たとえば、デバイスを構成するために StageNow でプロファイルを作成したとします。 StageNow プロファイルを作成すると、最後のステップによってプロファイルをテストするためのファイルが生成されます。 このファイルを、デバイス上の StageNow アプリで使用します。

別の例では、StageNow でプロファイルを作成し、テストします。 Intune で、StageNow プロファイルを追加した後、それを Zebra デバイスに割り当てます。 割り当てられたプロファイルの状態を確認すると、プロファイルには大まかな状態が表示されます。

どちらの場合も、StageNow ログ ファイルからより詳しい情報を取得できます。これは、StageNow プロファイルが適用されるたびにデバイスに保存されます。

一部の問題は StageNow プロファイルの内容とは関係ないため、ログに反映されません。

この記事では、StageNow ログの読み方について説明します。また、ログに反映されない可能性がある、Zebra デバイスのその他の潜在的な問題をいくつか示します。

この機能の詳細については、[Zebra モビリティ拡張での Zebra デバイスの使用および管理](android-zebra-mx-overview.md)に関する記事をご覧ください。

## <a name="get-the-logs"></a>ログを取得する

### <a name="use-the-stagenow-app-on-the-device"></a>デバイスで StageNow アプリを使用する
[プロファイルを展開するために Intune](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow) を使用するのではなく、コンピューター上で StageNow を使用して直接プロファイルをテストする場合、デバイス上の StageNow アプリによってテストのログが保存されます。 このログ ファイルを取得するには、デバイス上の StageNow アプリで **[詳細] (...)** オプションを使用します。

### <a name="get-logs-using-android-debug-bridge"></a>Android Debug Bridge を使用してログを取得する
Intune で既にプロファイルが展開された後にログを取得するには、[Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb) (Android の Web サイトが開きます) を使用してデバイスをコンピューターに接続します。

デバイス上で、ログは `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files` に保存されます

### <a name="get-logs-from-email"></a>メールからログを取得する
Intune で既にプロファイルが展開された後にログを取得する場合、エンド ユーザーがデバイス上のメール アプリを使用して、ご自身にログをメールで送信することができます。 Zebra デバイスでポータル サイト アプリを開き、[ログを送信します](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android)。 ログの送信機能を使用すると、PowerLift インシデント ID も作成されます。これは、Microsoft サポートに問い合わせる場合に参照することができます。

## <a name="read-the-logs"></a>ログを読む

ログを確認する場合、`<characteristic-error>` タグが付いていたらエラーが発生しています。 エラーの詳細は、`<parm-error>` タグ > `desc` プロパティに書き込まれています。

## <a name="error-types"></a>エラーの種類

Zebra デバイスには、さまざまなエラー報告レベルがあります。

- デバイスで CSP がサポートされていない。 たとえば、デバイスが携帯電話デバイスではなく、携帯電話マネージャーを備えていません。
- MX または OSX のバージョンが一致しない。 各 CSP はバージョン管理されます。 完全なサポート マトリックスについては、[Zebra のドキュメント](http://techdocs.zebra.com/mx/) (ゼブラの Web サイトが開きます) を参照してください。
- デバイスによって別の問題またはエラーが報告される。

## <a name="examples"></a>例

たとえば、次の入力プロファイルがあるとします。

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

ログでは、XML が入力と同じです。 この出力の一致は、プロファイルがエラーなしで正常にデバイスに適用されたことを意味します。

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

別の例では、次の入力があるとします。

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

このログには `<characteristic-error>` タグが含まれているため、エラーが表示されています。 このシナリオでは、プロファイルによって、指定されたパスに存在しない Android パッケージ (APK) のインストールが試みられました。

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Zebra デバイスに関するその他の潜在的な問題

このセクションでは、デバイス管理者と共に Zebra デバイスを使用する場合に、発生する可能性のあるその他の問題について説明します。 これらの問題は、StageNow ログでは報告されません。

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView が最新ではない

古いデバイスがポータル サイト アプリを使用してサインインすると、ユーザーに、System WebView のコンポーネントが古く、アップグレードが必要であるというメッセージが表示されることがあります。 デバイスに Google Play がインストールされている場合は、それをインターネットに接続し、更新プログラムを確認します。 デバイスに Google Play がインストールされていない場合は、更新されたバージョンのコンポーネントを入手し、デバイスに適用します。 または、Zebra によって発行された最新のデバイス OS に更新します。

### <a name="management-actions-take-a-long-time"></a>管理アクションに長い時間がかかる

Google Play サービスを利用できない場合は、一部のタスクが完了するまでに最大 8 時間かかります。 [Android 用 Intune ポータル サイト アプリの制限事項](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (別の Microsoft Web サイトが開きます) は、優れたリソースとして役に立つ場合があります。

### <a name="device-spoofing-suspected-shows-in-intune"></a>Intune に "デバイス スプーフィングの疑い" が表示される

このエラーは、Zebra Android 以外のデバイスが、Zebra デバイスとしてそのモデルと製造元を報告している疑いがあると Intune が推測していることを意味します。

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>ポータル サイト アプリが最低限必要なバージョンよりも古い

Intune によって、ポータル サイト アプリの最低限必要なバージョンが更新される場合があります。 デバイスに Google Play がインストールされていない場合、ポータル サイト アプリは自動的に更新されません。 最低限必要なバージョンがインストールされているバージョンよりも新しい場合、ポータル サイト アプリは動作を停止します。 [Zebra デバイスでのサイドローディング](android-zebra-mx-overview.md#sideload-the-company-portal-app)を使用して、最新のポータル サイト アプリに更新してください。

## <a name="next-steps"></a>次のステップ

[Zebra のディスカッション掲示板](https://developer.zebra.com/community/home/discussions) (Zebra の Web サイトが開きます)

[Intune で Zebra モビリティ拡張機能を備えた Zebra デバイスを使用および管理する](android-zebra-mx-overview.md)
