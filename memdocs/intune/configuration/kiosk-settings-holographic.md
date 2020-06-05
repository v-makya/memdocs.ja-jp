---
title: Microsoft Intune での Windows Holographic for Business 用のキオスク設定 - Azure | Microsoft Docs
description: Microsoft Intune でシングル アプリおよびマルチ アプリ キオスクとして Windows Holographic for Business デバイスを構成し、スタート メニューのカスタマイズ、アプリの追加、タスク バーの表示、および Web ブラウザーの構成を行います。
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
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d54e02c7bb88354ec59a9a8ce780ff559377466
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556100"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Intune でキオスクとして実行するための Windows Holographic for Business デバイスの設定

Windows Holographic for Business デバイスでは、シングル アプリ キオスク モード、またはマルチ アプリ キオスク モードで実行するようにこれらのデバイスを構成することができます。 一部の機能は、Windows Holographic for Business ではサポートされていません。

この記事では、Windows Holographic for Business デバイス上で制御できるさまざまな設定について説明します。 モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使用して、Windows Holographic for Business デバイスをキオスク モードで実行するように構成します。

Intune 管理者は、デバイスに対してこれらの設定を作成し、割り当てることができます。

Intune での Windows キオスク機能の詳細については、[キオスク設定の構成](kiosk-settings.md)に関するページを参照してください。

## <a name="before-you-begin"></a>始める前に

- [Windows 10 キオスク デバイス構成プロファイルを作成します](kiosk-settings.md#create-the-profile)。

  Windows 10 キオスク デバイス構成プロファイルを作成する場合、この記事に記載されているものよりも多くの設定があります。 この記事には、Windows Holographic for Business デバイスでサポートされている設定が記載されています。

- このキオスク プロファイルは、[Microsoft Edge のキオスク設定](device-restrictions-windows-holographic.md#microsoft-edge-browser)を使用して作成するデバイス制限プロファイルに直接関連付けられます。 まとめ

  1. このキオスク プロファイルを作成し、キオスク モードでデバイスを実行します。
  2. [デバイスの制限プロファイル](device-restrictions-windows-holographic.md#microsoft-edge-browser)を作成し、Microsoft Edge で許可された特定の機能と設定を構成します。

> [!IMPORTANT]
> このキオスク プロファイルは必ず [Microsoft Edge プロファイル](device-restrictions-windows-holographic.md#microsoft-edge-browser)と同じデバイスに割り当ててください。

## <a name="single-app-full-screen-kiosk"></a>シングル アプリ、全画面表示キオスク

デバイス上でアプリを 1 つのみ実行します。 ユーザーがサインインすると、特定のアプリが起動します。 また、このモードでは、ユーザーによる新しいアプリを開く操作や、実行中のアプリを変更する操作が制限されます。

- **[ユーザーのログオンの種類]** :アプリを実行するアカウントの種類を選択します。 次のようなオプションがあります。

  - **[自動ログオン]\(Windows 10 バージョン 1803 以降)** :Windows Holographic for Business ではサポートされていません。
  - **[ローカル ユーザー アカウント]** :(デバイスの) ローカル ユーザー アカウントを入力します。 または、キオスク アプリに関連付けられている Microsoft アカウント (MSA) のアカウントを入力します。 入力したアカウントでキオスクにサインインします。

    公開環境でキオスクを使用する場合は、最小限の特権を持つユーザーの種類を使用する必要があります。

- **[アプリケーションの種類]** : **[ストア アプリの追加]** を選択します。

  - **[キオスク モードで実行するアプリ]** :一覧からアプリを選択します。

    アプリが何も表示されない場合は、 [クライアント アプリ](../apps/apps-add.md)ごとの手順を使用して追加してください。

## <a name="multi-app-kiosk"></a>マルチ アプリ キオスク

このモードのアプリはスタート メニューから使用できます。 ユーザーはこれらのアプリのみを開くことができます。 あるアプリが別のアプリに依存している場合、許可されているアプリの一覧に両方が含まれている必要があります。

- **[S モード デバイスで Windows 10 を対象とする]** : **[いいえ]** を選択します。 S モードは、Windows Holographic for Business ではサポートされていません。

- **[ユーザーのログオンの種類]** :追加したアプリを使用できるユーザー アカウントを追加します。 次のようなオプションがあります。

  - **[自動ログオン]\(Windows 10 バージョン 1803 以降)** :Windows Holographic for Business ではサポートされていません。
  - **[ローカル ユーザー アカウント]** :(デバイスの) ローカル ユーザー アカウントを**追加**します。 入力したアカウントでキオスクにサインインします。
  - **[Azure AD user or group (Windows 10 version 1803 and later)]\(Azure AD ユーザーまたはグループ (Windows 10 バージョン 1803 以降)\)** :デバイスへのサインインにはユーザーの資格情報が必要です。 一覧から Azure AD のユーザーまたはグループを選択するには、 **[追加]** を選択します。 複数のユーザーおよびグループを選択することができます。 **[選択]** を選んで変更を保存します。
  - **[HoloLens の訪問者]** :訪問者のアカウントはゲスト アカウントであり、「[共有 PC モードの概念](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts)」の説明のとおり、ユーザーの資格情報や認証は必要ありません。

- **[ブラウザーとアプリケーション]** : キオスク デバイスで実行するアプリを追加します。 複数のアプリを追加することができます。

  - **ブラウザー**
    - **[Microsoft Edge の追加]** : Microsoft Edge がアプリ グリッドに追加されます。このキオスクでは、あらゆるアプリケーションを実行できます。 Microsoft Edge キオスク モードの種類を選択します。

      - **[通常モード (通常版の Microsoft Edge)]** : すべての参照機能を使って完全版の Microsoft Edge を実行します。 ユーザー データと状態がセッション間で保存されます。
      - **[公共閲覧用 (InPrivate)]** : マルチタブ版の Microsoft Edge InPrivate を実行します。キオスク用の操作に変更されており、全画面モードで実行されます。

      以上のオプションの詳細については、「[Microsoft Edge キオスク モードの展開](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types)」を参照してください。

      > [!NOTE]
      > この設定を行うことで、デバイス上で Microsoft Edge ブラウザーを有効にできます。 Microsoft Edge 固有の設定を構成するには、デバイス制限プロファイルを作成します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Windows 10]** (プラットフォームとして) > **[デバイス制限]**  >  **[Microsoft Edge ブラウザー]** )。 [Microsoft Edge ブラウザー](device-restrictions-windows-holographic.md#microsoft-edge-browser)には、使用可能な Holographic for Business の設定の一覧と説明が表示されます。

    - **[キオスク ブラウザーの追加]** : Windows Holographic for Business ではサポートされていません。

  - **アプリケーション**
    - **[ストア アプリの追加]** :[[クライアント アプリ]](../apps/apps-add.md) として、Intune に追加または展開した既存のアプリを選択します。これには LOB アプリが含まれます。 一覧にアプリが何も表示されない場合、Intune では [Intune に追加](../apps/store-apps-windows.md)する[アプリの種類](../apps/apps-add.md)が多数サポートされています。
    - **[Add Win32 App]\(Win32 アプリの追加\)** :Windows Holographic for Business ではサポートされていません。
    - **[AUMID による追加]** :このオプションを使用して、メモ帳や電卓などの受信トレイ Windows アプリを追加します。 次のプロパティを入力します。

      - **[アプリケーション名]** :必須。 アプリケーションの名前を入力します。
      - **[アプリケーション ユーザー モデル ID (AUMID)]** :必須。 Windows アプリのアプリケーション ユーザー モデル ID (AUMID) を入力します。 この ID を取得する場合は、「[Find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app)」 (インストール済みアプリのアプリケーション ユーザー モデル ID を見つける) を参照してください。

    - **[自動起動]** : 任意。 アプリとブラウザーを追加した後、ユーザーがサインインしたときに自動的に開くアプリまたはブラウザーを 1 つ選択します。 自動的に起動できるアプリまたはブラウザーは 1 つだけです。
    - **[タイル サイズ]** :必須。 アプリを追加した後、アプリのタイル サイズを小、中、ワイド、または大から選択します。

- **[代替のスタート画面のレイアウトを使用する]** :アプリの順序を含む、アプリをスタート メニューに表示する方法を説明する XML ファイルを入力するには、 **[はい]** を選択します。 [スタート] メニューでさらにカスタマイズが必要な場合は、このオプションを使用します。 [[スタート画面のレイアウトのカスタマイズとエクスポート]](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens) ではいくつかのガイダンスが提供され、Windows Holographic for Business デバイス用の特定の XML ファイルが含まれます。

- **[Windows タスク バー]** :Windows Holographic for Business ではサポートされていません。
- **[ダウンロード フォルダーへのアクセスを許可する]** : Windows Holographic for Business ではサポートされていません。
- **[アプリの再起動のためのメンテナンス期間の指定]** : Windows Holographic for Business ではサポートされていません。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Android](device-restrictions-android.md#kiosk)、[Android エンタープライズ](device-restrictions-android-for-work.md#dedicated-devices)、および [Windows 10 以降](kiosk-settings-windows.md)のデバイス用にキオスク プロファイルを作成することもできます。
