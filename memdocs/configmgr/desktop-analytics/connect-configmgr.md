---
title: Configuration Manager を接続する
titleSuffix: Configuration Manager
description: Configuration Manager を Desktop Analytics に接続するためのハウツー ガイド。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0835892788f86e9c246ed98d46658025fbc4180d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708320"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Configuration Manager を Desktop Analytics に接続する方法

Desktop Analytics は、Configuration Manager と密接に統合されています。 まず、最新の機能をサポートするために、確実にサイトを最新の状態にします。 次に、Configuration Manager で Desktop Analytics 接続を作成します。 最後に、接続の正常性を監視します。

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a> サイトを更新する

まず、お使いの Configuration Manager サイトでバージョン 1902 以降が実行されていることを確認します。 詳細については、[コンソール内の更新プログラムのインストール](../core/servers/manage/install-in-console-updates.md)に関するページを参照してください。

また、Desktop Analytics との統合をサポートするために、バージョン 1902 の更新プログラムのロールアップ (4500571) もインストールする必要があります。 この更新プログラムの詳細については、「[Configuration Manager Current Branch、バージョン 1902 の更新プログラムのロールアップ 3](https://support.microsoft.com/help/4500571)」を参照してください。

1. バージョン 1902 の更新プログラムのロールアップを使用してサイトを更新します。 詳細については、[コンソール内の更新プログラムのインストール](../core/servers/manage/install-in-console-updates.md)に関するページを参照してください。

2. クライアントを更新します。 このプロセスを簡単にするには、自動クライアント アップグレードの使用を検討します。 詳細については、「[クライアントをアップグレードする](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)」をご覧ください。

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a> サービスに接続する

> [!TIP]
> ウィザードを起動するとウィザードの外部で選択することができなくなるため、ウィザードを開始する前に手順 8 で説明したターゲット コレクションを作成します。

次の手順を使用して、Configuration Manager を Desktop Analytics に接続し、デバイス設定を構成します。 この手順は、階層をクラウド サービスにアタッチするための 1 回限りのプロセスです。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。 リボンの **[Azure サービスの構成]** を選択します。

    > [!TIP]
    > **[Desktop Analytics サービス]** ノードから、サービスに直接接続します。 Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[Desktop Analytics サービス]** ノードを選択します。 *[Desktop Analytics は初めてですか?]* ボックスで、 *[Connect Configuration Manager to the Desktop Analytics service]\(Configuration Manager を Desktop Analytics サービスに接続する\)* の 2 番目のリンクを選択します。

2. Azure サービス ウィザードの **[Azure サービス]** ページで、次の設定を構成します。

    - Configuration Manager でオブジェクトの**名前**を指定します。

    - 省略可能な**説明**を指定すれば、サービスを特定するのに役立ちます。

    - 利用可能なサービスの一覧から **[Desktop Analytics]** を選択します。

   **[次へ]** を選択します。

3. **[アプリ]** ページで、適切な **[Azure 環境]** を選択します。 次に、Web アプリの **[参照]** を選択します。

4. このサービスに再利用したい既存のアプリがある場合は、一覧からそれを選択して、 **[OK]** を選択します。

5. ほとんどの場合、このウィザードを使用して Desktop Analytics 接続用のアプリを作成できます。 **[作成]** を選択します。<!-- 3572123 -->

    > [!TIP]
    > このウィザードからアプリを作成できない場合は、Azure AD で手動でアプリを作成してから、Configuration Manager にインポートすることができます。 詳細については、「[Configuration Manager 用アプリの作成とインポート](troubleshooting.md#create-and-import-app-for-configuration-manager)」をご覧ください。

6. **[サーバー アプリケーションの作成]** ウィンドウで、次の設定を構成します。

    - **アプリケーション名**:Azure AD 内のアプリのフレンドリ名。

    - **ホームページ URL**:この値は Configuration Manager では使用されませんが、Azure AD で必要になります。 既定値は `https://ConfigMgrService` です。

    - **アプリ ID URI**:この値は、Azure AD テナント内で一意である必要があります。 これは、サービスへのアクセスを要求するために Configuration Manager クライアントで使用されるアクセス トークンに含まれます。 既定値は `https://ConfigMgrService` です。

    - **秘密鍵の有効期間**: ドロップダウン リストから、 **[1 年]** または **[2 年]** を選択します。 1 年が既定値です。

    **[サインイン]** を選択します。 Azure への認証が正常に行われると、ページに参照用の **Azure AD テナント名**が表示されます。

    > [!NOTE]
    > この手順は、**グローバル管理者**として実行してください。 これらの資格情報は Configuration Manager では保存されません。 この管理者には Configuration Manager のアクセス許可は必要ありません。また、Azure サービス ウィザードを実行するアカウントと同じものである必要もありません。

    **[OK]** を選択して Azure AD で Web アプリを作成し、サーバー アプリケーションの作成ダイアログを閉じます。 [サーバー アプリ] ダイアログで、 **[OK]** を選択します。 次に、Azure サービス ウィザードの **[アプリ]** ページで、[次へ] を選択します。

7. **[診断データ]** ページで、次の設定を構成します。

    - **[商用 ID]** : この値には、ご自分の組織の ID が自動的に入力されます。 そうでない場合は、お使いのプロキシ サーバーが、必要なすべての[エンドポイント](enable-data-sharing.md#endpoints)が許可されるように構成されていることを確認してから、次に進んでください。 または、[Desktop Analytics ポータル](monitor-connection-health.md#bkmk_ViewCommercialID)から、手動で商用 ID を取得します。

    - **[Windows 10 診断データ レベル]** : 最低でも **[基本]** を選択します。 「[診断データのレベル](enable-data-sharing.md#diagnostic-data-levels)」をご覧ください
  
    - **[診断データでデバイス名を許可する]** : **[有効にする]** を選択します

        > [!NOTE]
        > Windows 10 バージョン 1803 からは、既定ではデバイス名が Microsoft に送信されません。 デバイス名を送信しない場合、それは Desktop Analytics で "不明" として表示されます。 この動作によって、デバイスの特定と評価が困難になる場合があります。

   **[次へ]** を選択します。 **[利用可能な機能]** ページには、前のページの診断データの設定で使用できる Desktop Analytics 機能が表示されます。 **[次へ]** を選択して続行するか、 **[前へ]** を選択して変更を加えます。

    ![Azure サービス ウィザードの [利用可能な機能] ページの例](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. **[コレクション]** ページで、次の設定を構成します。

    - **[表示名]** :Desktop Analytics ポータルでは、この Configuration Manager 接続が、この名前を使用して表示されます。 これは、異なる階層を区別し、別の階層からコレクションを識別するために使用します。 環境内の複数の階層を簡単に区別できる用語を使用します。たとえば、"*テスト ラボ*" や "*実稼働*" などです。

    - **ターゲット コレクション**:このコレクションには、商用 ID と診断データの設定を使用して Configuration Manager によって構成されるすべてのデバイスが含まれます。 それは、Configuration Manager によって Desktop Analytics サービスに接続されるデバイスの完全なセットです。

    - **ターゲット コレクション内のデバイスでは、送信方向の通信にユーザー認証済みプロキシが使用されます**:既定では、この値は **[いいえ]** です。 環境内で必要な場合は、 **[はい]** に設定します。

    - **[Select specific collections to synchronize with Desktop Analytics]\(Desktop Analytics と同期する特定のコレクションを選択する\)** :ご自分の **[ターゲット コレクション]** 階層のコレクションを追加するには、 **[追加]** を選択します。 これらのコレクションは、Desktop Analytics ポータルで展開計画を使用してグループ化するために使用できます。 パイロット コレクションとパイロット除外コレクションが含まれていることを確認してください。  <!-- 4097528 -->

        > [!TIP]
        > [コレクションの選択] ウィンドウには、 **[ターゲット コレクション]** によって制限されているコレクションのみが表示されます。
        >
        > 次の例では、使用するターゲット コレクションとして CollectionA を選択します。 その後、さらにコレクションを追加すると、CollectionA、CollectionB、および CollectionC が表示されます。 CollectionD を追加することはできません。
        >
        > - CollectionA: **[すべてのシステム]** コレクションによって制限されます
        >     - CollectionB: CollectionA によって制限されます
        >         - CollectionC: CollectionB によって制限されます
        > - CollectionD: **[すべてのシステム]** コレクションによって制限されます
        >
        > Desktop Analytics で展開プランを使用してグループ化するために利用できるコレクションを管理するには、Configuration Manager コンソールで **[管理]** ワークスペースにアクセスし、 **[クラウド サービス]** を展開して、 **[Azure サービス]** ノードを選択します。 **Desktop Analytics** Azure サービスに関連付けられているエントリを選択し、 **[Desktop Analytics コレクション]** ページでご利用の設定を更新します。

        > [!IMPORTANT]
        > これらのコレクションは、メンバーシップが変更されても引き続き同期されます。 たとえば、ご利用のターゲット コレクションで、Windows 7 のメンバーシップ規則付きのコレクションを使用するとします。 これらのデバイスが Windows 10 にアップグレードされ、Configuration Manager によってコレクションのメンバーシップが評価されると、これらのデバイスはコレクションと Desktop Analytics から削除されます。

9. ウィザードを完了します。

Configuration Manager によって、ターゲット コレクション内にデバイスを構成するための設定ポリシーが作成されます。 このポリシーには、デバイスが Microsoft にデータを送信できるようにする診断データの設定が含まれています。 既定では、クライアントでのポリシーの更新は 1 時間ごとに行われます。 新しい設定を受信した後、Desktop Analytics でデータが使用できるようになるまでに数時間以上かかる可能性があります。

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a> 接続の正常性の監視

Desktop Analytics 用のデバイスの構成を監視します。 Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースにアクセスし、 **[Desktop Analytics サービス]** ノードを展開し、 **[接続の正常性]** ダッシュボードを選択します。

詳細については、「[接続の正常性の監視](monitor-connection-health.md)」をご覧ください。

接続の作成後、コレクションが、Configuration Manager によって 60 分以内に同期されます。 Desktop Analytics ポータルで、 **[グローバル パイロット]** にアクセスし、Configuration Manager デバイス コレクションを確認します。

> [!NOTE]
> Desktop Analytics への Configuration Manager 接続は、サービス接続ポイントに依存します。 このサイトシステムの役割に対する変更は、クラウド サービスとの同期に影響する可能性があります。 詳細については、「[About the service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move)」 (サービスの接続ポイントについて) を参照してください。

## <a name="next-steps"></a>次のステップ

次の記事に進み、デバイスを Desktop Analytics に登録します。
> [!div class="nextstepaction"]
> [デバイスの登録](enroll-devices.md)
