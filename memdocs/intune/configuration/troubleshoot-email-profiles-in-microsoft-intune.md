---
title: Microsoft Intune での電子メール プロファイルのトラブルシューティング - Azure | Microsoft Docs
description: 電子メール プロファイルの重複や Samsung KNOX Standard Android デバイスでのエラーなど、Microsoft Intune の電子メール プロファイルに関する一般的な問題と解決方法について説明します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 717ad28625b5eac97c26bcd09a21ef34250a7d39
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565718"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Microsoft Intune の電子メール プロファイルに関する一般的な問題と解決方法

一般的な電子メール プロファイルに関する問題と、そのトラブルシューティングと解決方法について説明します。

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>パスワードの入力がユーザーに繰り返し求められる

ユーザーには、メール プロファイルのパスワードの入力が繰り返し求められます。 証明書を使用してユーザーを認証および承認する場合は、すべての証明書プロファイルの割り当てを確認します。 通常、これらの証明書プロファイルは、デバイス グループではなく、ユーザー グループに割り当てられます。 いずれかの証明書プロファイルがユーザーを対象としていない場合、引き続き Intune によって電子メール プロファイルの展開が再試行されます。

メール プロファイル チェーンがユーザー グループに割り当てられている場合は、証明書プロファイルがユーザー グループにも割り当てられていることを確認してください。

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>デバイス グループに展開されたプロファイルにエラーと待機時間が表示される

通常、メール プロファイルはユーザー グループに割り当てられます。 デバイス グループに割り当てられている場合もあります。

- たとえば、証明書ベースのメール プロファイルを、デスクトップではなく、Surface デバイスのみに展開するとします。 このシナリオでは、デバイス グループが理にかなっている可能性があります。 これらのデバイスは非準拠と表示され、エラーが返され、メール プロファイルがすぐに取得されない場合があることにご注意ください。

  この例では、メール プロファイルを作成し、プロファイルをデバイス グループに割り当てます。 デバイスが再起動され、ユーザーがサインインするまでに遅延が発生します。 この遅延中に、ユーザー グループに割り当てられている PKCS 証明書プロファイルが展開されます。 まだユーザーがいないため、PKCS 証明書プロファイルにより、デバイスは非準拠になります。 イベント ビューアーには、デバイスでのエラーも表示される場合があります。

  コンプライアンスを確保するために、ユーザーはデバイスにサインインし、Intune と同期してポリシーを受信します。 ユーザーは手動で再同期するか、次の同期を待つことができます。

- たとえば、動的なグループを使用しているとします。 Azure AD を使用して動的グループを直ちに更新しない場合、これらのデバイスは非準拠と表示されることがあります。

これらのシナリオでは、デバイス グループを使用することがより重要か、またはすべてのポリシーを準拠していると示すことがより重要かを決定します。

## <a name="device-already-has-an-email-profile-installed"></a>デバイスに電子メール プロファイルが既にインストールされている

ユーザーが Intune または Office 365 MDM に登録する前に電子メール プロファイルを作成すると、Intune によって展開された電子メール プロファイルが想定どおりに動作しない場合があります。

- **iOS および iPadOS**:Intune は、ホスト名と電子メール アドレスに基づいて既存の重複する電子メール プロファイルを検出します。 ユーザーが作成した電子メール プロファイルがあると、Intune で作成されたプロファイルが展開されません。 このシナリオは一般的な問題です。iOS および iPadOS ユーザーは、通常、電子メール プロファイルを作成し、それから登録するためです。 ポータル サイト アプリには、ユーザーが準拠していないと表示され、電子メール プロファイルを削除するようにユーザーが求められる場合があります。

  Intune プロファイルを展開できるように、ユーザーは電子メール プロファイルを削除する必要があります。 この問題を回避するには、電子メール プロファイルを登録し、展開を Intune に許可するようにユーザーに指示します。 これで、ユーザーは電子メール プロファイルを作成できるようになります。

- **Windows**: Intune は、ホスト名と電子メール アドレスに基づいて既存の重複する電子メール プロファイルを検出します。 Intune は、ユーザーによって作成された既存の電子メール プロファイルを上書きします。

- **Samsung KNOX Standard**:Intune は、電子メール アドレスに基づいて重複する電子メール アカウントを識別し、Intune プロファイルで上書きします。 ユーザーがそのアカウントを構成した場合、Intune プロファイルによって再び上書きされます。 この動作によって、アカウントの構成を上書きされたユーザーが混乱する可能性があります。

Samsung KNOX では、プロファイルを識別するためにホスト名が使用されません。 異なるホスト上の同じ電子メール アドレスに展開する複数の電子メール プロファイルは、相互に上書きされるため、作成しないことをお勧めします。

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>KNOX Standard デバイスのエラー 0x87D1FDE8

**問題**: さまざまな Android デバイスで Samsung KNOX Standard の Exchange Active Sync 電子メール プロファイルを作成して展開すると、デバイスの [プロパティ] > [ポリシー] タブに **0x87D1FDE8** または "**修復できませんでした**" というエラーが報告される。

Samsung KNOX の EAS プロファイルおよびソース ポリシーの構成を確認します。 Samsung Note 同期オプションはサポートされなくなったため、このオプションをプロファイルで選択することはできません。 デバイスには、ポリシーを処理するための十分な時間を最大 24 時間設定してください。

## <a name="unable-to-send-images-from--email-account"></a>電子メール アカウントから画像を送信できない

電子メール アカウントを自動的に構成したユーザーが、自分のデバイスから画像を送信することができません。 このシナリオは、 **[サードパーティ アプリケーションからの電子メール送信を許可する]** が有効ではない場合に発生する可能性があります。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]** の順に選択します。
3. 電子メール プロファイル > **[プロパティ]**  >  **[設定]** の順に選択します。
4. **[Allow e-mail to be sent from third-party applications]\(サードパーティ製アプリケーションからの電子メールの送信を許可\)** する設定を **[有効]** に設定します。

## <a name="next-steps"></a>次のステップ

[Microsoft からサポート](../fundamentals/get-support.md)を受けるか、[コミュニティ フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune)を使用します。
