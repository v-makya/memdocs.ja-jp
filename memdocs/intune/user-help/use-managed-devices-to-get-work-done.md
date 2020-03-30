---
title: デバイス登録とは | Microsoft Docs
description: Intune ポータル サイトと Microsoft Intune アプリを使用してデバイスを登録するとはどのようなことかを説明します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/13/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 523caa6b-d792-4bb6-bddb-24b2479932d8
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 95f9677b95dc9dde4b12e60e3006b4cee5081471
ms.sourcegitcommit: 670c90a2e2d3106048f53580af76cabf40fd9197
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233415"
---
# <a name="what-is-device-enrollment"></a>デバイス登録とは
お使いのデバイスから職場または学校のリソースにアクセスするには、デバイスを Intune ポータル サイト アプリまたは Microsoft Intune アプリに登録する必要があります。 

デバイスの登録では次のことが行われます。

* お使いのデバイスが組織に登録されます。 このステップにより、組織のメール、アプリ、Wi-Fi にアクセスすることが承認されます。 
* 組織のデバイス管理ポリシーが、お使いのデバイスに適用されます。 ポリシーには、デバイスのパスワードや暗号化などの要件が含まれる場合があります。 これらの要件の目的は、デバイスと組織のデータを承認されていないアクセスから保護することです。

組織の要件に合わせてデバイスの設定を更新すると、登録が完了します。 事実上どこからでも、職場または学校アカウントに安全にサインインできます。  

この記事では、アプリの入手方法、サポートされているデバイス、デバイスの削除やリセッなど、登録に関する他の側面について説明します。  

## <a name="company-portal-and-microsoft-intune-app"></a>Intune ポータル サイト アプリと Microsoft Intune アプリ

Intune ポータル サイト アプリと Microsoft Intune アプリによって、ポリシーや設定の変更が通知されるため、職場または学校にアクセスできなくなるようなことなしに、アクションを実行できます。 

Intune ポータル サイト アプリでは個人情報と作業情報が個別に保持されるため、生産性と集中を維持することができます。 また、ユーザーが職場や学校のアプリを利用できるようになるため、自分の仕事に関連するものを見つけてインストールすることができます。  

### <a name="get-company-portal"></a>ポータル サイトの取得

場合によっては、組織によってデバイスに Intune ポータル サイト アプリがインストールされることがあります。 アプリは、Microsoft Store、App Store、Google Play ストアなどのアプリ ストアからインストールすることもできます。 Web ブラウザーからアプリにアクセスするには、職場または学校アカウントで [Intune ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)にサインインします。  

### <a name="get-microsoft-intune-app"></a>Microsoft Intune アプリの取得

Microsoft Intune アプリを使用する必要がある場合は、組織によってデバイスにインストールされます。  

## <a name="whats-the-difference-between-the-apps-and-the-website"></a>アプリと Web サイトの違い
Intune ポータル サイト アプリは、Windows 10、iOS、macOS、および Android のデバイスで使用できます。 デバイスのプラットフォームとシームレスに統合されます。 Web サイト バージョンには任意のデバイスからアクセスでき、使用しているデバイスに関係なく同じ共通のエクスペリエンスが提供されます。 

Microsoft Intune アプリは、企業所有の Android デバイス用であり、Web サイトはありません。  

## <a name="what-kind-of-devices-can-you-enroll-with-company-portal"></a>Intune ポータル サイトで登録できるデバイスの種類
Intune ポータル サイトを使用すると、次のデバイスを登録できます。  

- Windows デバイス
  - Windows 10 Mobile
  - [Windows] 10 Desktop
  - Windows Phone 8.1
  - Windows 8.1
- Apple デバイス
    - iOS
    - macOS
- Android デバイス


## <a name="what-kind-of-devices-can-you-enroll-with-the-microsoft-intune-app"></a>Microsoft Intune アプリで登録できるデバイスの種類  
組織によってアプリで使用するように設定された会社所有の Android デバイスを登録できます。 アプリでは Android 6.0 以降がサポートされています。 

## <a name="can-you-remove-a-device-from-the-company-portal"></a>ポータル サイトからデバイスを削除できますか
Intune ポータル サイトからデバイスを削除またはリセットすることができます。 **削除**と**リセット**には違いがあります。

デバイスの削除では、Intune ポータル サイトによってデバイスの登録が解除されます。 そのデバイスは Intune ポータル サイトにアクセスできなくなります。 職場または学校のデータも削除される可能性があります。 

デバイスのリセット中に、ポータル サイトによって、コンピューターまたはデバイスの製造元の既定の設定へのリセットが試みられます。 職場または学校のすべてのデータとすべての個人データがデバイスから削除されます。 リセットは、デバイスを紛失した場合などに便利です。 Intune ポータル サイト Web サイトからデバイスをリモートでリセットできます。  

## <a name="can-you-remove-a-device-from-the-microsoft-intune-app"></a>Microsoft Intune アプリからデバイスを削除できますか
いいえ。Microsoft Intune アプリから会社所有のデバイスを削除する方法はありません。  

## <a name="what-if-i-cant-see-my-device-in-the-company-portal-or-microsoft-intune-app"></a>Intune ポータル サイトまたは Microsoft Intune アプリでデバイスを表示できない場合の対処方法
Intune ポータル サイトでデバイスを表示するには、最初にデバイスを登録する必要があります。 登録後もすべてのデバイスが表示されない場合は、Intune ポータル サイトを使用して同期を試みるか、アクセスを確認してください。 お客様の会社によって所有および管理されているデバイスは、表示されません。

Microsoft Intune アプリでは、現在使用しているデバイスのみが表示されます。 他の登録済みデバイスは、アプリには表示されません。  

## <a name="where-else-can-i-go-for-help"></a>サポートを受けられるその他の場所  
一般的な問題のトラブルシューティングについては、次のプラットフォーム固有のドキュメントをご覧ください。  

- [Android デバイスに関する一般的な問題を解決する](check-compliance-on-your-device-android.md)  
- [iOS デバイスに関する一般的な問題を解決する](troubleshoot-your-device-ios.md)
- [macOS デバイスに関する一般的な問題を解決する](troubleshoot-your-device-macos.md)
- [Windows デバイスに関する一般的な問題を解決する](troubleshoot-your-device-windows.md)

IT サポート担当者に問い合わせることもできます。 Intune ポータル サイト アプリおよび Microsoft Intune アプリには、連絡先情報の一覧と問題の報告方法が表示されるヘルプとサポートのページが用意されています。 連絡先の情報は、組織の [Intune ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)でも確認できます。  

## <a name="next-steps"></a>次のステップ  

職場または学校アカウントにアクセスする準備ができたら、組織の指示に従ってデバイスを登録します。 次の記事でも、詳細な登録手順のガイダンスを確認できます。

* [Windows 10 デバイスを登録する](enroll-windows-10-device.md)
* [Android デバイスを登録する](enroll-device-android-company-portal.md)
* [Android 仕事用プロファイルを使用して登録する](enroll-device-android-work-profile.md)
* [Microsoft Intune アプリを使用して登録する](enroll-device-android-microsoft-intune-app.md)
* [iOS デバイスを登録する](enroll-your-device-in-intune-ios.md)
* [組織で提供される iOS デバイスを登録する](enroll-your-device-dep-ios.md)
* [macOS デバイスを登録する](enroll-your-device-in-intune-macos-cp.md)
* [組織で提供される macOS デバイスを登録する](enroll-company-device-macos.md)
