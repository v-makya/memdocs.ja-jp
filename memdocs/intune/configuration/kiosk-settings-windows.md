---
title: Microsoft Intune - Azure での Windows 10 用のキオスクの設定 | Microsoft Docs
description: Microsoft Intune でシングル アプリおよびマルチ アプリ キオスクとして Windows 10 (およびそれ以降) デバイスを構成し、スタート メニューのカスタマイズ、アプリの追加、タスク バーの表示、および Web ブラウザーの構成を行います。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc3ef945351529ce0db3e40108fef135414c4fab
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093614"
---
# <a name="windows-10-and-later-device-settings-to-run-as-a-kiosk-in-intune"></a>Intune で Windows 10 以降のデバイスをキオスクとして実行するための設定

Windows 10 以降のデバイスでは、シングル アプリ キオスク モード、またはマルチ アプリ キオスク モードで実行するようにこれらのデバイスを構成することができます。

この記事では、Windows 10 以降のデバイスで制御できるさまざまな設定の一覧を示して説明します。 モバイル デバイス管理 (MDM) ソリューションの一環として、これらの設定を使って Windows 10 以降のデバイスを構成し、キオスク モードで実行させます。

Intune 管理者は、デバイスに対してこれらの設定を作成し、割り当てることができます。

Intune での Windows キオスク機能の詳細については、[キオスク設定の構成](kiosk-settings.md)に関するページを参照してください。

## <a name="before-you-begin"></a>始める前に

- [プロファイルを作成します](kiosk-settings.md#create-the-profile)。

- このキオスク プロファイルは、[Microsoft Edge のキオスク設定](device-restrictions-windows-10.md#microsoft-edge-browser)を使用して作成するデバイス制限プロファイルに直接関連付けられます。 まとめ

  1. このキオスク プロファイルを作成し、キオスク モードでデバイスを実行します。
  2. [デバイスの制限プロファイル](device-restrictions-windows-10.md#microsoft-edge-browser)を作成し、Microsoft Edge で許可された特定の機能と設定を構成します。

- すべてのファイル、スクリプト、ショートカットがローカル システム上にあることを確認してください。 その他の Windows 要件などの詳細については、「[スタート画面のレイアウトのカスタマイズとエクスポート](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout)」を参照してください。

> [!IMPORTANT]
> このキオスク プロファイルは必ず [Microsoft Edge プロファイル](device-restrictions-windows-10.md#microsoft-edge-browser)と同じデバイスに割り当ててください。

## <a name="single-app-full-screen-kiosk"></a>シングル アプリ、全画面表示キオスク

デバイス上でアプリを 1 つのみ実行します。

- **[キオスク モードを選択]** : **[シングル アプリ、全画面表示キオスク]** を選択します。

- **[ユーザーのログオンの種類]** :アプリを実行するアカウントの種類を選択します。 次のようなオプションがあります。

  - **[自動ログオン]\(Windows 10 バージョン 1803 以降)** :ゲスト アカウントと同様、ユーザーのサインインを必要としないパブリックに公開された環境のキオスクで使用します。 この設定では [AssignedAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp) を使用します。
  - **[ローカル ユーザー アカウント]** :(デバイスの) ローカル ユーザー アカウントを入力します。 入力したアカウントでキオスクにサインインします。

- **[アプリケーションの種類]** :アプリケーションの種類を選択します。 次のようなオプションがあります。

  - **[Microsoft Edge ブラウザーの追加]** : **[Microsoft Edge ブラウザー]** を選択し、 **[Microsoft Edge キオスク モードの種類]** を選択します。

    - **[デジタル/インタラクティブ サイネージ]** : URL 全画面を開きます。その Web サイトのコンテンツのみが表示されます。 [デジタル署名の設定](https://docs.microsoft.com/windows/configuration/setup-digital-signage)に関するページでは、この機能に関する詳細情報を提供しています。
    - **[公共閲覧用 (InPrivate)]** : 制限付きマルチタブ バージョンの Microsoft Edge を実行します。 ユーザーは、公共で閲覧したり、自分の閲覧セッションを終了したりすることができます。

    以上のオプションの詳細については、「[Microsoft Edge キオスク モードの展開](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types)」を参照してください。

    > [!NOTE]
    > この設定を行うことで、デバイス上で Microsoft Edge ブラウザーを有効にできます。 Microsoft Edge 固有の設定を構成するには、デバイス制限プロファイルを作成します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Windows 10]** (プラットフォームとして) > **[デバイス制限]**  >  **[Microsoft Edge ブラウザー]** )。 [Microsoft Edge ブラウザー](device-restrictions-windows-10.md#microsoft-edge-browser)には、利用できる設定の一覧と説明が表示されます。

  - **[キオスク ブラウザーの追加]** : **[キオスク ブラウザーの設定]** を選択します。 これらの設定で、キオスクの Web ブラウザー アプリを制御します。 [キオスク ブラウザー アプリ](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP)をストアから取得し、それを[クライアント アプリ](../apps/apps-add.md)として Intune に追加します。 次に、アプリをキオスク デバイスに割り当てます。

    次の設定を入力します。

    - **[既定のホーム ページ URL]** :キオスク ブラウザーが開いたときや再起動したときに表示される、既定の URL を入力します。 たとえば、「`http://bing.com`」や「`http://www.contoso.com`」と入力します。

    - **[ホーム ボタン]** :キオスク ブラウザーの [ホーム] ボタンを**表示**または**非表示**にします。 既定では、ボタンは表示されません。

    - **ナビゲーション ボタン**:[進む] および [戻る] ボタンを**表示**または**非表示**にします。 既定では、ナビゲーション ボタンは表示されません。

    - **[セッションの終了] ボタン**:[セッションの終了] ボタンを**表示**または**非表示**にします。 表示されている場合、ユーザーがボタンを選択すると、アプリでセッションの終了が求められます。 確認すると、ブラウザーで閲覧データ (Cookie やキャッシュなど) がすべてクリアされ、既定の URL が開きます。 既定では、ボタンは表示されません。

    - **[アイドル時間が経過した後、ブラウザーを更新する]** :キオスク ブラウザーを初期状態で再起動するまでのアイドル時間を、1 - 1,440 分で入力します。 アイドル時間は、ユーザーが最後に操作してからの分数です。 既定では、値は空または空白となります。これは、アイドル タイムアウトがないことを意味します。

    - **[許可された Web サイト]** :特定の Web サイトを開けるようにするには、この設定を使用します。 つまり、デバイス上で Web サイトを制限またはブロックするには、この機能を使用します。 たとえば、`http://contoso.com` のすべての Web サイトが開くようにすることができます。 既定では、すべての Web サイトが許可されます。

      特定の web サイトを許可するには、許可される Web サイトが 1 行に 1 つずつ列記されているファイルをアップロードします。 ファイルを追加しない場合、すべての Web サイトが許可されます。 既定では、Intune によって Web サイトのすべてのサブドメインが許可されます。 たとえば、`sharepoint.com` ドメインを入力するとします。 Intune により、`contoso.sharepoint.com` や `my.sharepoint.com` など、すべてのサブドメインが自動的に許可されます。 アスタリスク (`*`) などのワイルドカードは入力しないでください。

      ファイルの例を次に示します。

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > Microsoft キオスク ブラウザーを使用する自動ログオンが有効な Windows 10 キオスクでは、ビジネス向け Microsoft Store のオフライン ライセンスを使用する必要があります。 このような要件があるのは、自動ログオンでは、Azure Active Directory (AD) 資格情報のないローカル ユーザー アカウントが使用されるためです。 そのため、オンライン ライセンスを評価することはできません。 詳しくは、「[オフライン アプリの配布](https://docs.microsoft.com/microsoft-store/distribute-offline-apps)」をご覧ください。

  - **[ストア アプリの追加]** : **[ストア アプリの追加]** を選択し、一覧からアプリを選択します。

    アプリが何も表示されない場合は、 [クライアント アプリ](../apps/apps-add.md)ごとの手順を使用して追加してください。

- **[アプリの再起動のためのメンテナンス期間の指定]** : アプリのインストールを完了するため、または更新プログラムのインストールを完了するために、再起動が必要となるアプリもあります。 **[必須]** とすると、メンテナンス期間を作成します。 アプリの再起動が必要な場合は、この期間の間に再起動されます。

  次の項目も入力します。

  - **[メンテナンス期間の開始時刻]** : 再起動が必要なアプリの更新プログラムのチェックをクライアントで開始する日付と時刻を選択します。 既定の開始時間は午前 0 時、または 0 分です。 空白とした場合は、アプリの更新プログラムがインストールされてから 3 日後のスケジュールされていない時間に、アプリが再起動します。

  - **[メンテナンス期間の繰り返し]** : 既定値は毎日です。 アプリの更新のためのメンテナンス期間を設ける頻度を選択します。 予期しないアプリの再起動を避けるため、**毎日**に設定することをお勧めします。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="multi-app-kiosk"></a>マルチ アプリ キオスク

このモードのアプリはスタート メニューから使用できます。 ユーザーはこれらのアプリのみを開くことができます。 あるアプリが別のアプリに依存している場合、許可されているアプリの一覧に両方が含まれている必要があります。 たとえば、Internet Explorer 64 ビット版は Internet Explorer 32 ビット版に依存するため、"C:\Program Files\internet explorer\iexplore.exe" および "C:\Program Files (x86)\Internet Explorer\iexplore.exe" に対して両方を許可する必要があります。 

- **[キオスク モードを選択]** : **[マルチ アプリ キオスク]** を選択します。

- **[S モード デバイスで Windows 10 を対象とする]** :
  - **Yes**:キオスク プロファイルで、ストア アプリと AUMID アプリを許可します。 Win32 アプリは除外されます。
  - **No**:キオスク プロファイルでストア アプリ、Win32 アプリ、AUMID アプリを許可します。 このキオスク プロファイルは S モードのデバイスには展開されません。

- **[ユーザーのログオンの種類]** :アプリを実行するアカウントの種類を選択します。 次のようなオプションがあります。

  - **[Auto logon (Windows 10 version 1803 and later)]\(自動ログオン (Windows 10 バージョン 1803 以降)\)** :ゲスト アカウントと同様、ユーザーのサインインを必要としないパブリックに公開された環境のキオスクで使用します。 この設定では [AssignedAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp) を使用します。
  - **[ローカル ユーザー アカウント]** :(デバイスの) ローカル ユーザー アカウントを**追加**します。 入力したアカウントでキオスクにサインインします。
  - **[Azure AD user or group (Windows 10 version 1803 and later)]\(Azure AD ユーザーまたはグループ (Windows 10 バージョン 1803 以降)\)** : **[追加]** を選択して、一覧から Azure AD のユーザーまたはグループを選択します。 複数のユーザーおよびグループを選択することができます。 **[選択]** を選んで変更を保存します。
  - **[HoloLens の訪問者]** :訪問者のアカウントはゲスト アカウントであり、「[共有 PC モードの概念](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts)」の説明のとおり、ユーザーの資格情報や認証は必要ありません。

- **[ブラウザーとアプリケーション]** : キオスク デバイスで実行するアプリを追加します。 複数のアプリを追加することができます。

  :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-add-applications-browser.png" alt-text="Microsoft Intune のマルチ アプリ キオスクのプロファイルにブラウザーまたはアプリを追加します。":::  

  - **ブラウザー**

    - **[Microsoft Edge の追加]** : Microsoft Edge がアプリ グリッドに追加されます。このキオスクでは、あらゆるアプリケーションを実行できます。 **[Microsoft Edge キオスク モードの種類]** を選択します。

      - **[通常モード (通常版の Microsoft Edge)]** : すべての参照機能を使って完全版の Microsoft Edge を実行します。 ユーザー データと状態がセッション間で保存されます。
      - **[公共閲覧用 (InPrivate)]** : マルチタブ版の Microsoft Edge InPrivate を実行します。キオスク用の操作に変更されており、全画面モードで実行されます。

      以上のオプションの詳細については、「[Microsoft Edge キオスク モードの展開](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types)」を参照してください。

      > [!NOTE]
      > この設定を行うことで、デバイス上で Microsoft Edge ブラウザーを有効にできます。 Microsoft Edge 固有の設定を構成するには、デバイス制限プロファイルを作成します ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** > > **[Windows 10]** (プラットフォームとして) > **[デバイス制限]**  >   **[Microsoft Edge ブラウザー]** )。 [Microsoft Edge ブラウザー](device-restrictions-windows-10.md#microsoft-edge-browser)には、利用できる設定の一覧と説明が表示されます。

    - **[キオスク ブラウザーの追加]** : これらの設定で、キオスクの Web ブラウザー アプリを制御します。 [クライアント アプリ](../apps/apps-add.md)を使用してキオスク デバイスに Web ブラウザー アプリを展開したことを確認してください。

      次の設定を入力します。

      - **[既定のホーム ページ URL]** :キオスク ブラウザーが開いたときや再起動したときに表示される、既定の URL を入力します。 たとえば、「`http://bing.com`」や「`http://www.contoso.com`」と入力します。

      - **[ホーム ボタン]** :キオスク ブラウザーの [ホーム] ボタンを**表示**または**非表示**にします。 既定では、ボタンは表示されません。

      - **ナビゲーション ボタン**:[進む] および [戻る] ボタンを**表示**または**非表示**にします。 既定では、ナビゲーション ボタンは表示されません。

      - **[セッションの終了] ボタン**:[セッションの終了] ボタンを**表示**または**非表示**にします。 表示されている場合、ユーザーがボタンを選択すると、アプリでセッションの終了が求められます。 確認すると、ブラウザーで閲覧データ (Cookie やキャッシュなど) がすべてクリアされ、既定の URL が開きます。 既定では、ボタンは表示されません。

      - **[アイドル時間が経過した後、ブラウザーを更新する]** :キオスク ブラウザーを初期状態で再起動するまでのアイドル時間 (1 から 1,440 分) で入力します。 アイドル時間は、ユーザーが最後に操作してからの分数です。 既定では、値は空または空白となります。これは、アイドル タイムアウトがないことを意味します。

      - **[許可された Web サイト]** :特定の Web サイトを開けるようにするには、この設定を使用します。 つまり、デバイス上で Web サイトを制限またはブロックするには、この機能を使用します。 たとえば、`contoso.com*` のすべての Web サイトが開くようにすることができます。 既定では、すべての Web サイトが許可されます。

        特定の web サイトを許可するには、許可されている Web サイトの一覧が含まれる .csv ファイルをアップロードします。 .csv ファイルを追加しない場合、すべての Web サイトが許可されます。

      > [!NOTE]
      > Microsoft キオスク ブラウザーを使用する自動ログオンが有効な Windows 10 キオスクでは、ビジネス向け Microsoft Store のオフライン ライセンスを使用する必要があります。 このような要件があるのは、自動ログオンでは、Azure Active Directory (AD) 資格情報のないローカル ユーザー アカウントが使用されるためです。 そのため、オンライン ライセンスを評価することはできません。 詳しくは、「[オフライン アプリの配布](https://docs.microsoft.com/microsoft-store/distribute-offline-apps)」をご覧ください。

  - **アプリケーション**

    - **[ストア アプリの追加]** :ビジネス向け Microsoft Store からアプリを追加します。 アプリが何も表示されない場合は、アプリを取得して [Intune に追加する](../apps/store-apps-windows.md)ことができます。 たとえば、キオスク ブラウザー、Excel、OneNote などを追加できます。

    - **[Add Win32 App]\(Win32 アプリの追加\)** :Win32 アプリは Visual Studio Code や Google Chrome などの従来のデスクトップ アプリです。 次のプロパティを入力します。

      - **[アプリケーション名]** :必須。 アプリケーションの名前を入力します。
      - **[アプリの実行可能ファイルへのローカル パス]** :必須。 `C:\Program Files (x86)\Microsoft VS Code\Code.exe` や `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe` などの、実行可能ファイルのパスを入力します。
      - **Win32 アプリのアプリケーション ユーザー モデル ID (AUMID)** :Win32 アプリのアプリケーション ユーザー モデル ID (AUMID) を入力します。 この設定により、デスクトップ上のタイルのスタート画面のレイアウトが決まります。 この ID を取得するには、「[Get-StartApps](https://docs.microsoft.com/powershell/module/startlayout/get-startapps?view=win10-ps)」を参照してください。

    - **[AUMID による追加]** :このオプションを使用して、メモ帳や電卓などの受信トレイ Windows アプリを追加します。 次のプロパティを入力します。

      - **[アプリケーション名]** :必須。 アプリケーションの名前を入力します。
      - **[アプリケーション ユーザー モデル ID (AUMID)]** :必須。 Windows アプリのアプリケーション ユーザー モデル ID (AUMID) を入力します。 この ID を取得する場合は、「[Find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app)」 (インストール済みアプリのアプリケーション ユーザー モデル ID を見つける) を参照してください。

    - **[自動起動]** : 任意。 アプリとブラウザーを追加した後、ユーザーがサインインしたときに自動的に開くアプリまたはブラウザーを 1 つ選択します。 自動的に起動できるアプリまたはブラウザーは 1 つだけです。
    - **[タイル サイズ]** :必須。 アプリを追加した後、アプリのタイル サイズを小、中、ワイド、または大から選択します。

      :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-autolaunch-tiles.png" alt-text="Microsoft Intune のマルチ アプリ キオスクのプロファイルでアプリまたはブラウザーを自動的に起動し、タイル サイズを選択します。":::

  > [!TIP]
  > すべてのアプリを追加したら、一覧内のアプリをクリックしてドラッグすることで、表示順序を変更することができます。  

- **[代替のスタート画面のレイアウトを使用する]** :アプリの順序を含む、アプリをスタート メニューに表示する方法を説明する XML ファイルを入力するには、 **[はい]** を選択します。 [スタート] メニューでさらにカスタマイズが必要な場合は、このオプションを使用します。 ガイダンスおよび XML のサンプルについては、「[スタート画面のレイアウトのカスタマイズとエクスポート](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout)」をご覧ください。

- **[Windows タスク バー]** :タスク バーを**表示**または**非表示**にします。 既定では、タスク バーは表示されません。 Wi-Fi アイコンなどのアイコンが表示されますが、エンドユーザーが設定を変更することはできません。

- **[ダウンロード フォルダーへのアクセスを許可する]** : **[はい]** を選択すると、ユーザーは Windows Explorer の [ダウンロード] フォルダーにアクセスできます。 既定では、[ダウンロード] フォルダーへのアクセスは無効になっています。 この機能は一般的に、エンド ユーザーがブラウザーからダウンロードしたアイテムにアクセスするために使用されます。

- **[アプリの再起動のためのメンテナンス期間の指定]** : アプリのインストールを完了するため、または更新プログラムのインストールを完了するために、再起動が必要となるアプリもあります。 **[必須]** とすると、メンテナンス期間を作成します。 アプリの再起動が必要な場合は、この期間中に再起動されます。

  次の項目も入力します。

  - **[メンテナンス期間の開始時刻]** : 再起動が必要なアプリの更新プログラムのチェックをクライアントで開始する日付と時刻を選択します。 既定の開始時間は午前 0 時、または 0 分です。 空白とした場合は、アプリの更新プログラムがインストールされてから 3 日後のスケジュールされていない時間に、アプリが再起動します。

  - **[メンテナンス期間の繰り返し]** : 既定値は毎日です。 アプリの更新のためのメンテナンス期間を設ける頻度を選択します。 予期しないアプリの再起動を避けるため、**毎日**に設定することをお勧めします。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

また、[Android](device-restrictions-android.md#kiosk)、[Android エンタープライズ](device-restrictions-android-for-work.md#device-experience)、[Windows Holographic for Business](kiosk-settings-holographic.md) デバイス用のキオスク プロファイルを作成することもできます。

また、Windows のガイダンスで「[シングル アプリ キオスクの設定](https://docs.microsoft.com/windows/configuration/kiosk-single-app)」または「[複数アプリ キオスクの設定](https://docs.microsoft.com/windows/configuration/lock-down-windows-10-to-specific-apps)」も参照してください。
