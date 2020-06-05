---
title: Microsoft Intune での Windows 10 の教育設定 - Azure | Microsoft Docs
description: Windows 10 デバイス用のすべての教育設定を一覧で示します。 テスト アプリでデバイス構成プロファイルにこれらの設定を使用する、ユーザーまたは学生のサインイン方法を選択する、テスト中に画面を監視するなどの機能が Intune にはあります。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55e38ac8b5503e98df4878529ac892b55a52be47
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429617"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Windows 10 デバイス上で Intune を使用してテスト アプリを構成する

テスト アプリを使用すると、教室の Windows 10 デバイスでオンライン テストを安全に管理できます。 テスト アプリを設定するには、Intune でデバイス構成プロファイルを作成し、セキュリティで保護された評価の設定を構成する必要があります。 この記事では、テスト アプリのために使用する設定について説明します。 

プロファイルを構成したら、学生に対して割り当てと展開を行います。 

[Intune のテスト アプリ](education-settings-configure.md)は、この機能に関する詳細情報を提供しています。

## <a name="before-you-begin"></a>始める前に

[デバイス構成プロファイルを作成します](education-settings-configure.md#create-a-device-profile)。

## <a name="take-a-test-settings"></a>テストの設定

- **アカウントの種類**:ユーザーがテストにサインインする方法を選択します。 次のようなオプションがあります。
  - Azure AD アカウント
  - ドメイン アカウント
  - ローカル アカウント
  - ローカルのゲスト アカウント:Windows 10 バージョン 1903 以降を稼働しているデバイスでのみ使用できます。
- **アカウント ユーザー名**:テスト アプリで使用したアカウントのユーザー名を入力します。 次の形式でアカウントを入力できます。
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **[アカウント名]** :ローカルのゲスト アカウントの種類を設定するには、テスト アプリで使用するアカウントの名前を入力します。 このアカウント名は、サインイン画面にタイルとして表示されます。 学生は、このタイルをクリックしてテストを開始します。  
- **評価 URL**:ユーザーに受けさせるテストの URL を入力します。 URL の取得の詳細については、[テストに関するドキュメント](https://docs.microsoft.com/education/windows/take-tests-in-windows-10)を参照してください。
- **[プリンター接続]** :プリンターに接続されているデバイスからのみテスト アプリへのアクセスを許可するには、 **[必要]** を選択します。 また、この設定により、テストを受けるユーザーがアプリの印刷ボタンを使用できるようになります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、学生がプリンターに接続されていないデバイスからアプリにアクセスすることが OS によって許可される場合があります。  
- **画面の監視**: **[許可]** に設定すると、ユーザーがテストを受けているときに、画面の動作を監視できます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、テスト中に画面を監視することが OS によって禁止される場合があります。
- **[テキスト候補]** :受験者がテキストの候補を表示できるようにするには、 **[許可]** を選択します。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、ユーザーがテストを受けているときに、OS によってテキストの候補がブロックされる可能性があります。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

詳細については、[テスト アプリの使用](education-settings-configure.md)に関するページを参照してください。
