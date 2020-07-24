---
title: Android Enterprise 専用、フル マネージド、または会社所有の仕事用プロファイル デバイスを Intune で登録する
titleSuffix: Microsoft Intune
description: Android Enterprise 専用、フル マネージド、または会社所有の仕事用プロファイル デバイスを Intune で登録する方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 858d813d3df2b020a869e1f18327d35e68bde7e0
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461727"
---
# <a name="enroll-your-android-enterprise-dedicated-fully-managed-or-corporate-owned-with-work-profile-devices"></a>Android Enterprise 専用、フル マネージド、または仕事用プロファイルを備えた会社所有のデバイスを登録する

Intune で Android Enterprise [専用デバイス](android-kiosk-enroll.md)、[フル マネージド デバイス](android-fully-managed-enroll.md)、または[会社所有の仕事用プロファイル デバイス](android-corporate-owned-work-profile-enroll.md)を設定すると、デバイスを登録できます。 専用デバイスとフル マネージド デバイスの両方とも Intune 登録は、工場出荷時の設定に戻すことから始まります。 Android Enterprise デバイスの登録方法は、オペレーティング システムによって異なります。

| 登録方法 | 専用およびフル マネージド デバイスの最小 Android OS バージョン |
| ----- | ----- |
| 近距離無線通信 | 6.0 |
| トークン エントリ | 6.0 |
| QR コード | 7.0 |
| ゼロ タッチ  | 8.0<br><br> 参加製造元で。 |
| [Knox Mobile Enrollment](https://docs.microsoft.com/mem/intune/enrollment/android-samsung-knox-mobile-enroll)  | 6.0<br><br> Samsung Knox 2.8 以上のデバイスでのみ。 |

## <a name="enroll-by-using-near-field-communication-nfc"></a>近距離無線通信 (NFC) を利用して登録する

NFC 対応の 6 以降のデバイスについては、特殊な形式の NFC タグを作成して、デバイスをプロビジョニングできます。 独自のアプリや任意の NFC タグ作成ツールを利用できます。 詳細については、「[C-based Android Enterprise device enrollment with Microsoft Intune](https://blogs.technet.microsoft.com/cbernier/2018/10/15/nfc-based-android-enterprise-device-enrollment-with-microsoft-intune/)」 (C ベースの Android エンタープライズ デバイスを Microsoft Intune で登録する) と「[Google's Android Management API documentation](https://developers.google.com/android/management/provision-device#nfc_method)」 (Google の Android 管理 API ドキュメント) を参照してください。

## <a name="enroll-by-using-a-token"></a>トークンを利用して登録する

Android 6 以降のデバイスについては、トークンを利用してデバイスを登録できます。 Android 6.1 以降のバージョンでは、**afw#setup** の登録方法を使用して QR コードのスキャンを活用することもできます。

1. ワイプされたデバイスをオンにします。
2. **[ようこそ]** 画面で、言語を選択します。
3. お使いの **Wifi** に接続し、 **[次へ]** を選択します。
4. Google の利用規約に同意し、 **[次へ]** を選択します。
5. Google サインイン画面で、Gmail アカウントの代わりに「**afw#setup**」を入力し、 **[次へ]** を選択します。
6. **Android デバイス ポリシー** アプリの **[インストール]** を選択します。
7. このポリシーのインストールを続行します。  一部のデバイスでは、追加の規約同意が要求されることがあります。
8. **[このデバイスを登録]** 画面で、QR コードのスキャンをデバイスに許可するか、トークンの手動入力を選択します。
9. 画面の指示に従って登録を完了します。

## <a name="enroll-by-using-a-qr-code"></a>QR コードを利用して登録する

Android 7 以降のデバイスでは、登録プロファイルから QR コードをスキャンすることでデバイスを登録できます。

> [!Note]
> ブラウザーをズームすると、デバイスが QR コードをスキャンできない可能性があります。 ブラウザーをさらにズームすると、問題が解決します。

1. Android デバイスで QR 読み取りを起動するには、ワイプした後、最初に表示される画面を複数回タップします。
2. Android 7 デバイスと Android 8 デバイスの場合、QR リーダーをインストールするように求められます。 Android 9 以降のデバイスの場合、QR リーダーが既にインストールされています。
3. QR リーダーを使用して登録プロファイルの QR コードをスキャンし、画面の指示に従って登録します。

## <a name="enroll-by-using-google-zero-touch"></a>Google ゼロ タッチを使用して登録する

Google のゼロ タッチ システムを使用するには、デバイスがそれに対応している必要があり、サービスに関与しているサプライヤーとの提携が必要です。  詳細については、[Google のゼロ タッチ プログラム Web サイト](https://www.android.com/enterprise/management/zero-touch/)をご覧ください。

1. ゼロ タッチ コンソールで新しい構成を作成します。
2. EMM DPC ドロップダウンから **[Microsoft Intune]** を選択します。
3. Google のゼロ タッチ コンソールで、次の JSON をコピーして DPC 追加フィールドに貼り付けます。 *YourEnrollmentToken* 文字列を、登録プロファイルの一部として作成した登録トークンに置き換えます。 登録トークンは二重引用符で囲んでください。

    ```json
    {
        "android.app.extra.PROVISIONING_DEVICE_ADMIN_COMPONENT_NAME": "com.google.android.apps.work.clouddpc/.receivers.CloudDeviceAdminReceiver",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_SIGNATURE_CHECKSUM": "I5YvS0O5hXY46mb01BlRjq4oJJGs2kuUcHvVkAPEXlg",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION": "https://play.google.com/managed/downloadManagingApp?identifier=setup",

        "android.app.extra.PROVISIONING_ADMIN_EXTRAS_BUNDLE": {
            "com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "YourEnrollmentToken"
        }
    }
    ```

4. **[適用]** を選択します。

## <a name="enroll-by-using-knox-mobile-enrollment"></a>Knox Mobile Enrollment を利用して登録する
Samsung の Knox Mobile Enrollment を使用するには、デバイスで Android OS バージョン 6 以降と Samsung Knox 2.8 以上を実行している必要があります。 詳細については、「[Samsung の Knox Mobile Enrollment を使用して Android デバイスを自動的に登録する](https://docs.microsoft.com/mem/intune/enrollment/android-samsung-knox-mobile-enroll)」を参照してください。

## <a name="next-steps"></a>次のステップ
- [Android アプリを展開する](../apps/apps-deploy.md)
- [Android 構成ポリシーを追加する](../configuration/device-profiles.md)

