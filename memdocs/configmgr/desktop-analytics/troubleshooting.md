---
title: Desktop Analytics のトラブルシューティング
titleSuffix: Configuration Manager
description: Desktop Analytics に関する問題のトラブルシューティングに役立つ技術的な詳細。
ms.date: 07/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 68506ba11e356a1e9f14d58880a80bdf3cfcb5f4
ms.sourcegitcommit: fb03634b8494903fc6855ad7f86c8694ffada8df
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85828977"
---
# <a name="troubleshoot-desktop-analytics"></a>Desktop Analytics のトラブルシューティング

この記事の詳細な情報を使って、Configuration Manager と統合された Desktop Analytics の問題のトラブルシューティングに役立ててください。

## <a name="confirm-prerequisites"></a>前提条件を確認する

多くの一般的な問題は、前提条件が不足していることが原因で発生します。 最初に、以下の構成を確認してください。

- [必要条件](overview.md#prerequisites)  

- [Windows コンポーネントの更新プログラム](enroll-devices.md#update-devices)  

- [データ共有を有効にする方法](enable-data-sharing.md)に関する記事。次のトピックについて説明されています。  

  - クライアントが接続する必要のあるインターネット エンドポイント  

  - プロキシ サーバー認証  

  - 診断データのレベル  

## <a name="monitor-connection-health"></a>接続の正常性の監視

Configuration Manager の **[接続の正常性]** ダッシュボードを使用して、デバイスの正常性別のカテゴリにドリルダウンします。 Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースにアクセスし、 **[Desktop Analytics サービス]** ノードを展開し、 **[接続の正常性]** ダッシュボードを選択します。  

詳細については、「[接続の正常性の監視](monitor-connection-health.md)」をご覧ください。

> [!NOTE]
> Desktop Analytics への Configuration Manager 接続は、サービス接続ポイントに依存します。 このサイトシステムの役割に対する変更は、クラウド サービスとの同期に影響する可能性があります。 詳細については、「[About the service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move)」 (サービスの接続ポイントについて) を参照してください。

バージョン 2002 以降、Configuration Manager サイトがクラウド サービスに必要なエンドポイントへの接続に失敗すると、クリティカルなステータス メッセージ ID 11488 が生成されます。 サービスに接続できない場合、SMS_SERVICE_CONNECTOR コンポーネントのステータスがクリティカルに変わります。 Configuration Manager コンソールの[コンポーネントのステータス](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) ノードに、詳細なステータスが表示されます。<!-- 5566763 -->

## <a name="log-files"></a>ログ ファイル

詳細については、[Desktop Analytics のログ ファイル](../core/plan-design/hierarchy/log-files.md#desktop-analytics)に関する記事を参照してください

Configuration Manager バージョン 1906 以降では、Desktop Analytics のトラブルシューティングを行うには、Configuration Manager のインストール ディレクトリの **DesktopAnalyticsLogsCollector.ps1** ツールを使います。 いくつかの基本的なトラブルシューティング手順が実行され、関連するログが 1 つの作業ディレクトリに収集されます。 詳しくは、[ログ コレクター](log-collector.md)に関する記事をご覧ください。

### <a name="enable-verbose-logging"></a>詳細ログ記録を有効にする

1. サービス接続ポイントで、次のレジストリ キーにアクセスします: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. **LoggingLevel** の値を `0` に設定します  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a> Azure AD アプリケーション

Desktop Analytics では、次のアプリケーションが Azure AD に追加されます。

- **Configuration Manager マイクロサービス**: Configuration Manager と Desktop Analytics を接続します。 このアプリにはアクセス要件はありません。  

- **MALogAnalyticsReader**: ご利用の Azure Log Analytics ワークスペースを監視して、毎日のスナップショットが正常にコピーされることを保証します。 詳細については、「[MALogAnalyticsReader アプリケーション ロール](#bkmk_MALogAnalyticsReader)」を参照してください。  

- **Desktop Analytics**: Configuration Manager で Desktop Analytics から展開計画に関する情報とデバイスの準備状態を取得できるようにします。

セットアップの完了後にこれらのアプリをプロビジョニングする必要がある場合は、 **[接続済みサービス]** ペインに移動します。 **[ユーザーとアプリのアクセスを構成]** を選択し、アプリをプロビジョニングします。  

- **Configuration Manager 用の Azure AD アプリ**。 セットアップの完了後に接続の問題をプロビジョニングまたはトラブルシューティングする必要がある場合は、「[Configuration Manager用のアプリを作成してインポートする](#create-and-import-app-for-configuration-manager)」をご覧ください。 このアプリでは、**Configuration Manager Service** API での **CM コレクションデータの書き込み**と **CM コレクション データの読み取り**が必要です。  

### <a name="create-and-import-app-for-configuration-manager"></a>Configuration Manager用のアプリを作成してインポートする

Azure サービスの構成ウィザードから Configuration Manager 用の Azure AD アプリを作成できない場合、または既存のアプリを再利用する場合は、手動で作成してインポートする必要があります。 Desktop Analytics ポータルで[初期オンボード](set-up.md#initial-onboarding)を完了した後、次の手順のようにします。

#### <a name="create-app-in-azure-ad"></a>Azure AD でアプリを作成する

1. "*グローバル管理者*" アクセス許可を持つユーザーとして [Azure portal](https://portal.azure.com) を開き、 **[Azure Active Directory]** に移動して、 **[アプリの登録]** を選択します。 次に、 **[新しい登録]** を選択します。  

2. **[作成]** パネルで、次の設定を構成します。  

    - **[名前]** : アプリを識別する一意の名前 (例: `Desktop-Analytics-Connection`)  

    - **[サポートされているアカウントの種類]** : **この組織ディレクトリ内のアカウントのみ (Contoso)**

    - **[リダイレクト URI (省略可能)]** : **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    **[登録]** を選択します。  

3. アプリを選択し、 **[アプリケーション (クライアント) ID]** と **[ディレクトリ (テナント) ID]** を記録しておきます。 値は、Configuration Manager の接続を構成するために使用される GUID です。  

4. **[管理]** メニューで **[証明書とシークレット]** を選択します。 **[新しいクライアント シークレット]** を選択します。 **[説明]** を入力し、有効期限を指定して、 **[追加]** を選択します。 Configuration Manager 接続を構成するために使用されるキーの **[値]** をコピーします。

    > [!Important]  
    > これは、キーの値をコピーする唯一の機会です。 ここでコピーしないと、別のキーを作成する必要があります。  
    >
    > キーの値を安全な場所に保存します。  

5. **[管理]** メニューで、 **[API のアクセス許可]** を選択します。  

    1. **[API のアクセス許可]** パネルで、 **[アクセス許可の追加]** を選択します。  

    2. **[API アクセス許可の要求]** パネルで、 **[所属する組織で使用している API]** に切り替えます。  

    3. **Configuration Manager Microservice** API を検索して選択します。  

    4. **[アプリケーションのアクセス許可]** グループを選択します。 **CmCollectionData** を展開し、次の両方のアクセス許可を選択します: **[Write CM Collection Data]\(CM コレクションデータの書き込み\)** と **[Read CM Collection Data]\(CM コレクション データの読み取り\)** 。  

    5. **[アクセス許可の追加]** を選択します。  

6. **[API のアクセス許可]** パネルで、 **[管理者の同意を与える]** を選択します。 **[はい]** を選択します。  

#### <a name="import-app-in-configuration-manager"></a>Configuration Manager でアプリをインポートする

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。 リボンの **[Azure サービスの構成]** を選択します。  

2. Azure サービス ウィザードの **[Azure サービス]** ページで、次の設定を構成します。  

    - Configuration Manager でオブジェクトの**名前**を指定します。  

    - 省略可能な**説明**を指定すれば、サービスを特定するのに役立ちます。  

    - 利用可能なサービスの一覧から **[Desktop Analytics]** を選択します。  
  
   **[次へ]** を選択します。  

3. **[アプリ]** ページで、適切な **[Azure 環境]** を選択します。 次に、Web アプリの **[インポート]** を選択します。 **[アプリのインポート]** ウィンドウで、次の設定を構成します。  

    - **[Azure AD テナント名]** : この名前が Configuration Manager で使用されます  

    - **[Azure AD テナント ID]** : Azure AD からコピーした**ディレクトリ ID**  

    - **クライアント ID**: Azure AD アプリからコピーした**アプリケーション ID**  

    - **[秘密キー]** : Azure AD アプリからコピーしたキーの**値**  

    - **秘密鍵の有効期限**:キーの同じ有効期限日  

    - **アプリ ID URI**:この設定には、次の値が自動的に入力されます: `https://cmmicrosvc.manage.microsoft.com/`  
  
   **[検証]** を選択し、 **[OK]** を選択して、[アプリのインポート] ウィンドウを閉じます。 Azure サービス ウィザードの [アプリ] ページで、 **[次へ]** を選択します。  

**[診断データ]** ページでウィザードの残りの部分を続けるには、「[サービスに接続する](connect-configmgr.md#bkmk_connect)」を参照してください。

#### <a name="troubleshoot-app-in-configuration-manager"></a>Configuration Manager でアプリのトラブルシューティングを行う

アプリの作成またはインポートで問題が発生した場合は、まず、**SMSAdminUI.log** で具体的なエラーを確認します。 それから、次の構成を確認します。

- Desktop Analytics サービスにテナントを正常に登録してあること。 詳しくは、「[Desktop Analytics を設定する方法](set-up.md)」をご覧ください。

- 必要なすべてのエンドポイントにアクセスできること。 詳しくは、「[エンドポイント](enable-data-sharing.md#endpoints)」をご覧ください。

- サインインするユーザーが適切なアクセス許可を持っていることを確認します。 詳細については、「[前提条件](overview.md#prerequisites)」を参照してください。

- ユーザーが一般に Azure にサインインできることを確認します。 この操作では、Azure AD 認証に関する一般的な問題があるかどうかを判断します。

- *Desktop Analytics worker* に関する **SMS_SERVICE_CONNECTOR** コンポーネントのステータス メッセージを確認します。

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a> Maloalyalosreader アプリケーション ロール

Desktop Analytics を設定するときは、組織の代理として同意します。 この同意は、ワークスペース用の Log Analytics 閲覧者ロールを MALogAnalyticsReader アプリケーションに割り当てるためのものです。 このアプリケーション ロールは、Desktop Analytics で必要です。

セットアップ中のこのプロセスに問題がある場合は、次のプロセスを使用して、このアクセス許可を手動で追加します。

1. [Azure portal](https://portal.azure.com) にアクセスし、 **[すべてのリソース]** を選択します。 種類が **[Log Analytics]** のワークスペースを選択します。  

2. ワークスペースのメニューで、 **[アクセス制御 (IAM)]** を選択し、 **[追加]** を選択します。  

3. **[アクセス許可の追加]** パネルで、次の設定を構成します。  

    - **[ロール]** : **閲覧者**  

    - **[アクセスの割り当て先]** : **Azure AD のユーザー、グループ、またはアプリケーション**  

    - **[選択]** : **MALogAnalyticsReader**  

4. **[保存]** を選択します。

ポータルに、ロールの割り当てを追加したことを示す通知が表示されます。

## <a name="data-latency"></a>データの遅延時間

<!-- 3846531 -->
初めて Desktop Analytics をセットアップするとき、新しいクライアントを登録するとき、または新しい展開計画を構成するときは、Configuration Manager と Desktop Analytics ポータルのレポートで、完全なデータがすぐに表示されない場合があります。 次の手順が行われるまで、2 から 3 日かかることがあります。

- アクティブなデバイスによって診断データが Desktop Analytics サービスに送信されます
- サービスでデータが処理されます
- サービスと Configuration Manager サイトが同期されます

デバイス コレクションを Configuration Manager の階層から Desktop Analytics に同期するときは、コレクションが Desktop Analytics ポータルに表示されるまでに、最大で 1 時間かかることがあります。 同様に、Desktop Analytics で展開計画を作成するときは、展開計画に関連付けられている新しいコレクションが Configuration Manager の階層に表示されるまで、最大で 1 時間かかることがあります。 プライマリ サイトでコレクションが作成され、中央管理サイトが Desktop Analytics と同期されます。 Configuration Manager によってコレクションのメンバーシップが評価されて更新されるまで、最大 24 時間かかることがあります。 このプロセスを短縮するには、コレクションのメンバーシップを手動で更新します。<!-- 4984639 -->

> [!Note]
> 変更を反映するために手動でコレクションを更新するには、SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker コンポーネントを最初に同期する必要があります。 このプロセスが実行されるまでに、最大で 1 時間かかることがあります。 詳しくは、**M365ADeploymentPlanWorker.log** をご覧ください。

Desktop Analytics ポータル内には、次の 2 種類のデータがあります: **管理者データ**と**診断データ**。

- **管理者データ**は、ワークスペースの構成に対して行われた変更を示します。 たとえば、資産の **[アップグレードの決定]** または **[重要度]** を変更すると 管理者データが変更されます。 これらの変更では、問題の資産がインストールされているデバイスの準備状態が変更されることがあるため、多くの場合は複合的な影響があります。

- **診断データ**は、クライアント デバイスから Microsoft にアップロードされたシステム メタデータを示します。 このデータは、Desktop Analytics で利用されます。 それには、デバイス インベントリや、セキュリティおよび機能の更新状態などの属性が含まれます。

既定では、Desktop Analytics ポータルのすべてのデータが、毎日自動的に更新されます。 この更新には、2 日前の診断データの変更と、ユーザーが構成に対して行った変更 (管理者データ) が含まれます。 毎日 UTC の午前 08:00 までには、Desktop Analytics ポータルに表示されるはずです。

管理者データを変更するときは、ワークスペース内の管理者データのオンデマンド更新をトリガーできます。 Desktop Analytics ポータルの任意のページで、データ更新状態ポップアップを開きます。

![Desktop Analytics ポータルのデータ更新状態ポップアップ タブのスクリーンショット](media/data-currency-flyout.png)

次に、 **[変更の適用]** を選択します。

![Desktop Analytics ポータルの展開されたデータ更新状態ポップアップのスクリーンショット](media/data-currency-flyout-expand.png)

通常、このプロセスには 15 から 60 分かかります。 タイミングは、ワークスペースのサイズと、処理が必要な変更の範囲によって異なります。 オンデマンド データ更新を要求しても、診断データが変更されることはありません。  詳しくは、「[Desktop Analytics の FAQ](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)」をご覧ください。

上で示した時間内に変更が反映されない場合は、次の日次更新までさらに 24 時間待ってください。 それより長く遅れる場合は、サービス正常性ダッシュボードを確認します。 サービスは正常であると報告されている場合は、Microsoft サポートにお問い合わせください。<!-- 3896921 -->

> [!IMPORTANT]
> **[最近のデータを表示]** の Desktop Analytics のオプションは非推奨です。 このアクションは、Desktop Analytics サービスの今後のリリースで削除される予定です。 詳しくは、「[非推奨の機能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)」をご覧ください。<!--7080949-->  

## <a name="service-notifications"></a>サービスの通知

<!-- 4982509 -->

Desktop Analytics ポータルで、管理者に通知バナーを表示できるようになりました。 これらの通知を使って、Microsoft は重要なイベントや問題についてユーザーに連絡することができます。 以下のセクションで、表示される可能性のある通知について詳しく説明します。

### <a name="see-whats-new-this-month-in-desktop-analytics"></a>Desktop Analytics の今月の新機能を確認します

この情報通知によって、サービスの変更を知ることができます。 詳細については、「[Desktop Analytics の新機能](whats-new.md)」 (`https://aka.ms/danews`) を参照してください。

### <a name="there-are-new-prerequisites-to-continue-using-desktop-analytics-review-the-new-requirements"></a>新しい前提条件があります。 引き続き Desktop Analytics を使用するには、新しい要件を確認してください

この情報通知によって、前提条件の変更を知ることができます。 たとえば、新しいインターネット エンドポイントやソフトウェアの更新などです。 詳細については、「[前提条件](overview.md#prerequisites)」 (`https://aka.ms/daprereqs`) を参照してください。

### <a name="were-investigating-an-issue-that-impacts-desktop-analytics"></a>Desktop Analytics に影響を与える問題を調査しています

この警告通知は、Microsoft が Desktop Analytics サービスに影響する問題を認識していることを示しています。 この問題は、通常、スナップショットを生成する場合に発生します。 この通知が表示された場合、Microsoft は、影響の範囲と発生源を特定するため、問題を調査しています。 Microsoft サポートに連絡する必要はありません。 詳細については、「[データ フロー](privacy.md#data-flow)」を参照してください。

### <a name="were-investigating-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>Microsoft がデータ待機時間の問題を調査しています。 過去 24 時間以内に新しいデバイスを登録したか、何らかの資産を変更した場合は、すぐに表示されないことがあります

この警告通知は、Microsoft が Desktop Analytics サービスに影響する問題を認識していることを示しています。 Microsoft はサービスを継続的に監視して、すべてのコンポーネントがスナップショットを正しい時刻に更新することを確認します。 この監視中に、これらのコンポーネントの 1 つが想定どおりに完了しませんでした。 この通知が表示された場合、Microsoft が問題を調査しています。 Microsoft サポートに連絡する必要はありません。 詳細については、「[データ フロー](privacy.md#data-flow)」を参照してください。

最近[デバイスを登録](enroll-devices.md)した、または[資産](about-assets.md)を変更した場合は、Microsoft が問題を解決するまでお待ちください。 操作を繰り返す必要はありません。

### <a name="weve-resolved-a-temporary-issue-with-data-latency-daily-refresh-of-portal-data-is-delayed"></a>データ待機時間の一時的な問題を解決しました。 ポータル データの毎日の更新が遅れています

この通知により、データ待機時間に関する問題が発生したことを知ることができます。 サービスにより、スナップショットが引き続き処理されていますが、データの更新が遅れています。 詳細については、「[データ待機時間](#data-latency)」をご覧ください。

### <a name="weve-resolved-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>データ待機時間の問題を解決しました。 過去 24 時間以内に新しいデバイスを登録したか、何らかの資産を変更した場合は、すぐに表示されないことがあります

この通知により、Microsoft が、以前に報告されたデータの待機時間に関する問題を解決したことを知ることができます。 明日のスナップショットに対して古いデータが表示される場合があります。 過去 24 時間に[デバイスを登録](enroll-devices.md)したか、デバイスの構成を変更した場合、ポータルにすぐに表示されないことがあります。 引き続き Desktop Analytics を使用して、[資産](about-assets.md)を分類し、[展開計画](about-deployment-plans.md)を準備することができます。 これらのアクションでは、前のスナップショットのデータを使用できます。

### <a name="weve-resolved-an-issue-with-desktop-analytics-daily-refresh-of-the-portal-data-is-on-track"></a>Desktop Analytics の問題を解決しました。 ポータル データの毎日の更新が順調に行われています

この通知により、Microsoft が、処理中に動作を停止したスナップショット コンポーネントを特定したことを知ることができます。 Microsoft がコンポーネントを再起動しましたが、スナップショットの処理には時間がかかります。 Microsoft はサービスを継続的に監視して、すべてのコンポーネントがスナップショットを正しい時刻に更新することを確認します。
