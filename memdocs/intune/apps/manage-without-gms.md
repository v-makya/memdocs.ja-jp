---
title: Google Mobile Services のない環境で Intune を使用する方法
titleSuffix: Microsoft Intune
description: Google Mobile Services のない環境で Intune を使用する方法について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce61f7af7c11fb579e34890700231ca2e59fb5cd
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81267685"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Google Mobile Services のない環境で Intune を使用する方法

Microsoft Intune では、Android デバイスを管理するときに、Google Mobile Services (GMS) を使用して Microsoft Intune ポータル サイトとの通信が行われます。 場合によっては、一時的または永続的に、デバイスから GMS にアクセスできないことがあります。 たとえば、デバイスが GMS なしで出荷される場合や、GMS を使用できない閉じたネットワークにデバイスが接続されている場合などです。 このドキュメントでは、GMS のない Android デバイスを管理するために Intune をインストールして使用する場合に、発生する可能性のある相違点と制限事項の概要について説明します。

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>Google Play ストアへのアクセスなしで Intune ポータル サイト アプリをインストールする 

### <a name="for-users-outside-of-mainland-china"></a>中国大陸以外のユーザーの場合 

Google Play を使用できない場合、Android デバイスでは、 [Android 用 Microsoft Intune ポータル サイト](https://www.microsoft.com/en-us/download/details.aspx?id=49140)をダウンロードし、そのアプリをサイドロードすることができます。 この方法でインストールした場合、アプリに更新プログラムまたは修正プログラムは自動的に提供されません。 ユーザーは、定期的に手動でアプリを更新し、修正プログラムを適用する必要があります。 

### <a name="for-users-in-mainland-china"></a>中国大陸のユーザーの場合 

現時点では、中国大陸では Google Play ストアを利用できないため、Android デバイスでは中国のアプリ マーケットプレースからアプリを入手する必要があります。 詳細については、「[中国大陸でポータル サイト アプリをインストールする](../user-help/install-company-portal-android-china.md)」をご覧ください。

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>GMS を使用できない場合の Intune デバイス管理者の管理の制限事項 

### <a name="unavailable-intune-features"></a>利用できない Intune 機能

一部の Intune 機能は、Google Play ストアや Google Play 開発者サービスなどの GMS のコンポーネントに依存しています。 これらのコンポーネントは GMS のない環境では利用できないため、Intune 管理者コンソールに含まれる次の機能は、使用できない場合があります。  

| 通信の種類  | 機能  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| デバイス コンプライアンス ポリシー  | Android デバイス管理者用のコンプライアンス ポリシーを作成または編集するときに、 **[Google Play プロテクト]** の下に一覧表示されるすべてのオプションは使用できません。  |
| アプリ保護ポリシー (条件付き起動)  | **[SafetyNet デバイスの構成証明]** および **[アプリの脅威のスキャンが必須]** デバイスの条件を、条件付き起動に使用することはできません。  |
| クライアント アプリ  | 種類が **Android** のアプリは使用できません。 アプリの展開と管理を行うには、代わりに**基幹業務アプリ**を使用します。  |
| Mobile Threat Defense  | MTD ベンダーと協力して、そのソリューションが Intune と統合されているかどうか、目的のリージョンで利用可能かどうか、GMS に依存しているかどうかを把握します。  |

### <a name="some-tasks-may-be-delayed"></a>一部のタスクが遅延する可能性がある 

GMS を利用できる環境の場合、Intune では、タスクの完了を高速化するためにプッシュ通知が使用されます。 たとえば、デバイスをリモートでワイプしようとすると、通常は数秒でデバイスに通知が届きます。 GMS を利用できない状況では、プッシュ通知も利用できない場合があります。 そのため、Intune では、タスクを完了するために次回のデバイス チェックイン時まで待機する必要があります。  

登録済みの Android デバイスでは、8 時間ごとに Intune への報告が行われます。 たとえば、デバイスが午後 1 時に Intune に報告して、リモート タスクが午後 1:05 に発行された場合、Intune では、午後 9 時にデバイスに接続してタスクが完了されます。 

次のタスクは、完了までに最大 8 時間かかることがあります。 

**Intune コンソール**:
- フル ワイプ
- 選択的ワイプ
- 新規アプリまたは更新アプリの展開
- リモート ロック
- パスコードのリセット

**Android 用 Intune ポータル サイト アプリ**:
- リモート デバイスの削除
- デバイスのリセット
- 使用可能な基幹業務アプリのインストール

**Intune ポータル サイト Web サイト**:
- デバイスの削除 (ローカルおよびリモート)
- デバイスのリセット
- デバイスのパスコードのリセット

デバイスを登録したばかりの場合は、コンプライアンス、コンプライアンス違反、構成のチェックインの実行頻度が高くなります。 デバイスのチェックインに関する詳細については、「[Microsoft Intune でのデバイス ポリシーとプロファイルの一般的な質問、問題と解決策](../configuration/device-profile-troubleshoot.md)」をご覧ください。 

## <a name="next-steps"></a>次のステップ

- [Microsoft Intune を使用してアプリをグループに割り当てる](../apps/apps-deploy.md)
