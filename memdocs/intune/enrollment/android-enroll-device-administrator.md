---
title: Microsoft Intune での Android デバイス管理者の登録
titleSuffix: ''
description: デバイス管理者の登録を使用して、Android デバイスを Intune に登録します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e44fa26c84537fdcf801192ce8cc22790f320b9
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80438785"
---
# <a name="android-device-administrator-enrollment"></a>Android デバイス管理者の登録

Android デバイス管理者 ("従来の" Android 管理とも呼ばれ、Android 2.2 でリリースされました) は、Android デバイスを管理する方法の 1 つです。 しかし、[Android Enterprise](https://www.android.com/enterprise/management/) (Android 5.0 でリリース) では、強化された管理機能を使用できるようになりました。 Google では、より豊富で安全な最新のデバイス管理に移行するための努力の一環として、新しい Android リリースでのデバイス管理者のサポートを縮小させています。

そのため、このような縮小された機能を回避するために、新しいデバイスは、以下で説明するデバイス管理者のプロセスを使って登録しないようにすることをお勧めします。

また、同じ理由から、デバイスを Android 10 に更新する場合は、そのデバイスをデバイス管理者の管理以外に移行することもお勧めします。 

それでもユーザーがデバイス管理者の管理を使って各自の Android デバイスを登録するようにしたい場合は、次のセクションに進みます。  

Google の Android Enterprise 機能について詳しくは、次の記事をご覧ください。
- [デバイス管理者から Android Enterprise への移行に関する Google のガイダンス](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [デバイス管理者 API の廃止計画に関する Google のドキュメント](https://developers.google.com/android/work/device-admin-deprecation)

## <a name="set-up-device-administrator-enrollment"></a>デバイス管理者の登録を設定する

1. モバイル デバイスの管理を準備するには、MDM (モバイル デバイス管理) 機関を **Microsoft Intune** に設定する必要があります。 手順については、[MDM 機関の設定](../fundamentals/mdm-authority-set.md)に関するページを参照してください。 この項目は、モバイル デバイス管理について初めて Intune を設定するときに一度だけ設定します。
2. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインし、 **[デバイス]**  >  **[Android]**  >  **[Android の登録]**  >  **[デバイス管理者特権を持つ個人所有のデバイスと会社所有のデバイス]**  >  **[デバイス管理者によってデバイスを管理します]** の順に選択します。
3. [デバイスを登録する方法をユーザーに知らせます](../user-help/enroll-device-android-company-portal.md)。  

ユーザーが登録した後に、[コンプライアンス ポリシーの割り当て](../protect/compliance-policy-create-android.md)、[アプリの管理](../apps/app-management.md)など、Intune でのデバイスの管理を開始することができます。

その他のユーザー タスクについては、次の記事を参照してください。
- [Microsoft Intune を使用したエンドユーザー エクスペリエンスに関するリソース](../fundamentals/end-user-educate.md)
- [Android デバイスを Intune で使用する](https://docs.microsoft.com/mem/intune/user-help/why-enroll-android-device)


## <a name="block-device-administrator-enrollment"></a>デバイス管理者の登録をブロックする
Android デバイス管理者のデバイスをブロックする場合や、個人所有の Android デバイス管理者のデバイスの登録のみをブロックする場合は、[デバイスの種類の制限の設定](enrollment-restrictions-set.md)に関するページをご覧ください。


## <a name="next-steps"></a>次のステップ
- [コンプライアンス ポリシーの割り当て](../protect/compliance-policy-create-android.md)
- [アプリの管理](../apps/app-management.md)
