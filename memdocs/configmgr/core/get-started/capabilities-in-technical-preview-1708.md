---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1708 で使用できる機能について説明します。
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705160"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Configuration Manager の Technical Preview 1708 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1708 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**この Technical Preview の既知の問題:**
- **サイト サーバーがパッシブ モードの場合、プレビュー バージョン 1708 への更新に失敗します**。 プレビュー バージョン 1706 または 1707 を実行し、[プライマリ サイト サーバーがパッシブ モード](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)の場合、プレビュー サイトをバージョン 1708 に正常に更新するには、パッシブ モードのサイト サーバーをアンインストールする必要があります。 パッシブ モードのサイト サーバーは、サイトでバージョン 1708 が実行された後に再インストールできます。

  パッシブ モードのサイト サーバーをアンインストールするには、次の手順を実行します。
  1. コンソールで **[管理]**  >  **[概要]**  >  **[サイトの構成]**  >  **[サーバーとサイト システムの役割]** の順に移動し、パッシブ モードのサイト サーバーを選択します。
  2. **[サイト システムの役割]** ウィンドウで、 **[サイト サーバー]** の役割を右クリックし、 **[役割の削除]** を選択します。
  3. パッシブ モードのサイト サーバーを右クリックし、 **[削除]** を選択します。
  4. サイト サーバーのアンインストール後に、アクティブなプライマリ サイト サーバーで **CONFIGURATION_MANAGER_UPDATE** のサービスを再起動します。




**このバージョンでお試しいただける新機能を次に示します。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Configuration Manager から PowerShell スクリプトを展開するときのスクリプト パラメーターの指定を改善
<!-- 1236459 -->

Configuration Manager 1706 以降では、「[Configuration Manager コンソールから PowerShell スクリプトを作成して実行する](../../apps/deploy-use/create-deploy-scripts.md)」ことができます。

[Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) ではこの機能が拡張され、Configuration Manager がスクリプトのパラメーターを読み取るようになりました。

この Technical Preview ではスクリプト パラメーターの機能が拡張され、必須のパラメーターと省略可能なパラメーターを検出して、ユーザーに入力を求めるようになりました。

### <a name="try-it-out"></a>試してみましょう。

1. 指示に従い、[Configuration Manager コンソールから PowerShell スクリプトを作成し、実行](../../apps/deploy-use/create-deploy-scripts.md)してください。
2. **スクリプトの作成ウィザード**の新しい **[スクリプト パラメーター]** ページで、パラメーターを選択し、値を編集します。
ウィザードにより、どのパラメーターが必須で、どれが省略可能であるかが表示されます。
4. パラメーターの編集が終わったら、ウィザードを完了します。

スクリプトを実行すると、設定したパラメーター値があればそれが使用されます。 必須のパラメーターを構成しなかった場合、エンド ユーザーはスクリプトの実行時にパラメーターを指定するように求められます。

## <a name="management-insights"></a>管理分析情報
<!-- 1353967 -->
お使いの環境の現在の状態に関して、サイト データベース内のデータ分析に基づく情報を得られるようになりました。 分析情報を利用することで、ご利用の環境についての理解を深め、その情報に基づいてアクションを実行できます。 Configuration Manager コンソールで **[管理]**  >  **[Management Insights]\(管理分析情報\)**  >  **[All Insights]\(すべての分析情報\)** の順に移動して、管理分析情報を確認します。 このリリースでは、次の分析情報が使用可能になりました。

- **展開されていないアプリケーション**:ご利用の環境内でアクティブに展開されていないアプリケーションを一覧表示します。 この情報により、使用されていないアプリケーションの発見と削除が容易になり、コンソール上に表示されるアプリケーションの一覧を把握しやすくなります。
- **空のコレクション**:ご利用の環境内でメンバーがいないコレクションを一覧表示します。 たとえば、これらのコレクションを削除して、オブジェクトを展開するときに表示されるコレクションの一覧を把握しやすくできます。


## <a name="restart-computers-from-the-configuration-manager-console"></a>Configuration Manager コンソールからコンピューターを再起動   
<!-- 1356283 -->
これ以降のリリースでは、Configuration Manager コンソールを使用して再起動を必要とするクライアント デバイスを識別し、再起動するようにクライアント通知を行うアクションを使用できます。

再起動を保留しているデバイスを識別するには、 **[資産とコンプライアンス]**  >  **[デバイス]** の順に移動し、再起動が必要な可能性のあるデバイスが含まれるコレクションを選択します。 コレクションを選択すると、 **[再起動待ち]** という名前の新しい列にある詳細ウィンドウで、各デバイスの状態を表示できます。 各デバイスには、 **[はい]** または **[いいえ]** の値があります。

クライアント通知を作成してデバイスを再起動するには、次のようにします。
1. コンソールの [デバイス] ノードで再起動するデバイスを見つけます。
2. デバイスを右クリックして、 **[クライアント通知]** を選択してから **[再起動]** を選択します。 これにより、再起動に関する情報ウィンドウが開きます。 **[OK]** をクリックして再起動要求を確定します。

クライアントが通知を受信すると、 **[ソフトウェア センター]** 通知ウィンドウが開き、ユーザーに再起動について通知されます。 既定では、再起動は 90 分後に行われます。 [[クライアント設定]](../clients/deploy/configure-client-settings.md) を構成すると、再起動の時間を変更できます。 再起動の動作に関する設定は、既定の設定の [[コンピューターの再起動]](../clients/deploy/about-client-settings.md#computer-restart) タブにあります。


### <a name="try-it-out"></a>試してみましょう。
次のタスクを試した後、どのように動作したかについて、リボンの **[ホーム]** タブから **[フィードバック]** を送信してください。
1. デバイスでアプリを展開するか、更新します。インストールを完了するには、デバイスの再起動が必要です。
2. コンソールの **[資産とコンプライアンス]**  >  **[デバイス]** ノードの順に移動してデバイスを見つけ、 **[再起動待ち]** 列に **[はい]** が表示されることを確認します。 再起動待ち状態がコンソールに反映されるまでには、最大 20 分かかることがあります。
3. デバイスを監視して、ソフトウェア センターの通知が開いており、デバイスが正常に再起動することを確認します。


## <a name="software-center-customization"></a>ソフトウェア センターのカスタマイズ
<!-- 1351224 -->
エンタープライズ ブランド要素を追加して、ソフトウェア センターのタブの表示を指定できます。 ソフトウェア センターに特定の会社名を追加したり、ソフトウェア センターの構成の基調となる色を設定したり、会社のロゴを設定したり、またはクライアント デバイスに表示されるタブを設定したりできます。

### <a name="customize-software-center"></a>ソフトウェア センターのカスタマイズ

ソフトウェア センターを変更する方法

1. **Configuration Manager** コンソールで、 **[管理]**  >  **[クライアント設定]** の順に選択します。 対象のクライアント設定のインスタンスをクリックします。
2. **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** を選択します。
3. **[既定の設定]** ダイアログ ボックスで、 **[ソフトウェア センター]** を選択します。
4. **[Select new settings to specify company information] (新しい設定を選択して会社情報を指定する\)** に対して **[はい]** を選択し、ソフトウェア センターのカスタマイズ設定を有効にします。
5. **[会社名]** を入力します。
6. **[Color Scheme for Software Center] (ソフトウェア センターのカラー スキーマ\)** を選択します。
7. **[参照]** をクリックしてソフトウェア センターのロゴに移動します。 ロゴは 400 x 100 ピクセルの JPEG または PNG とし、サイズは 750 KB までとする必要があります。
8. **[はい]** を選択して、クライアント デバイスにソフトウェア センターのタブが表示されるようにします。 少なくとも 1 つのタブが表示されている必要があります。

    -  [アプリケーション] タブを有効にする
    -  [アップデート] タブを有効にする
    -  [オペレーティング システム] タブを有効にする
    -  [インストールのステータス] タブを有効にする
    -  [デバイスのポリシー準拠] タブを有効にする
    -  [オプション] タブを有効にする

### <a name="next-steps"></a>次のステップ

Configuration Manager のアプリケーション管理の詳細については、「[アプリケーション管理の概要](../../apps/understand/introduction-to-application-management.md)」を参照してください
