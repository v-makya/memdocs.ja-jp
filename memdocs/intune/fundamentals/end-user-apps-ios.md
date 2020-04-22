---
title: iOS/iPadOS のユーザーがアプリを入手する方法
description: エンド ユーザーが iOS/iPadOS アプリを使用できるようにするための方法
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79344091"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>iOS/iPadOS のユーザーがアプリを入手する方法

Microsoft Intune を通して配布したアプリをエンド ユーザーがどこでどのように取得するかについて説明します。

**必要なアプリ** - 管理者が必須に設定しているアプリと、必要最小限のユーザー操作でデバイスにインストールされるアプリです (プラットフォームによって異なります)。

**使用可能なアプリ** - ポータル サイト アプリの一覧に表示されるアプリおよびユーザーが必要に応じてインストールするアプリです。

**管理対象のアプリ** -- ポリシーによって管理できて、Intune によって "ラップされた" アプリまたは Intune アプリ ソフトウェア開発キット (SDK) で構築されたアプリです。 これらのアプリは Intune によって管理することができます。また、これらのアプリにはアプリ保護ポリシーを適用することができます。

**アンマネージド アプリ** -- Intune アプリ SDK と統合されていない iOS/iPadOS の App Store からユーザーがダウンロードできるアプリです。 Intune では、これらのアプリの配布、管理、または選択的ワイプを制御することはできません。  

登録済みユーザーは、ポータル サイト アプリのアプリ画面で、以下のタイルをタップしてアプリを取得します。

- **[すべてのアプリ]** 。[ポータル Web サイト](https://portal.manage.microsoft.com)の [すべて] タブのすべてのアプリのリストをポイントします。

- **[おすすめアプリ]** 。ポータル Web サイトの [おすすめ] タブを表示します。

- **[カテゴリ]** 。ポータル Web サイトの [カテゴリ] タブをポイントします。

![iOS ポータル サイト アプリの画面](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

アプリを追加する方法の詳細については、「[アプリを Microsoft Intune に追加する方法](../apps/apps-add.md)」を参照してください。

## <a name="app-management-takeover"></a>アプリ管理の引き継ぎ
アプリが既にエンド ユーザーのデバイスにインストールされている場合、iOS/iPadOS デバイスでは、組織によるアプリの管理の許可を求めるアラートが表示されます。 エンド ユーザーは、アプリの構成をマネージド デバイスに適用する前に、組織がアプリを管理するのを許可する必要があります。 ユーザーがアラートをキャンセルした場合、デバイスが管理され、アプリが割り当てられている限り、アラートが定期的に表示されます。  


![[キャンセル] と [管理] のオプションが表示されるアプリ管理変更アラートの画像。](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>関連項目  

[Android ユーザーがアプリを入手する方法](end-user-apps-android.md)

[Windows ユーザーがアプリを入手する方法](end-user-apps-windows.md)
