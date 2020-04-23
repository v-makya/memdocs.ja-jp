---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1711 で使用できる機能について説明します。
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e6f8ed1562392899b46a082bf8f64872c7e1b67d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705100"
---
# <a name="capabilities-in-technical-preview-1711-for-configuration-manager"></a>Configuration Manager の Technical Preview 1711 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1711 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**この Technical Preview の既知の問題:**
- **Windows 10、バージョン 1709 (Fall Creators Update とも呼ばれます) のサポート**。  この Windows リリース以降、Windows メディアには複数のエディションが含まれます。 オペレーティング システム アップグレード パッケージまたはオペレーティング システム イメージを使用するようにタスク シーケンスを構成する場合は、必ず [Configuration Manager による使用をサポートしているエディション](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)を選択してください。
- **サイト サーバーがパッシブ モードの場合、新しいプレビュー バージョンへの更新に失敗します**。 [プライマリ サイト サーバーがパッシブ モード](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)であるプレビュー バージョンを実行する場合は、プレビュー サイトをこの新しいプレビュー バージョンに正常に更新するため、あらかじめパッシブ モードのサイト サーバーをアンインストールしておく必要があります。 パッシブ モードのサイト サーバーは、サイトの更新を完了したあとに再インストールできます。

  パッシブ モードのサイト サーバーをアンインストールするには、次の手順を実行します。
  1. コンソールで **[管理]**  >  **[概要]**  >  **[サイトの構成]**  >  **[サーバーとサイト システムの役割]** の順に移動し、パッシブ モードのサイト サーバーを選択します。
  2. **[サイト システムの役割]** ウィンドウで、 **[サイト サーバー]** の役割を右クリックし、 **[役割の削除]** を選択します。
  3. パッシブ モードのサイト サーバーを右クリックし、 **[削除]** を選択します。
  4. サイト サーバーのアンインストール後に、アクティブなプライマリ サイト サーバーで **CONFIGURATION_MANAGER_UPDATE** のサービスを再起動します。

**このバージョンでお試しいただける新機能を次に示します。**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>タスク シーケンスを実行するための機能強化
<!-- 1261338 -->

この Technical Preview は、タスク シーケンスの実行ステップを改善します。 また、次の項目も改善されています。

- ソフトウェア センター、PXE、およびメディアからのすべてのオペレーティング システムの展開シナリオのサポート。
- オブジェクトの削除中にコピー、インポート、エクスポート、および警告などのコンソール操作の改善。
- **事前設定コンテンツの作成**ウィザードのサポート。
- 展開の検証との統合。
- タスク シーケンスの実行ステップが、単一の親子関係だけでなく、タスク シーケンスの複数のレベル間で使用できるようになりました。 複数レベルの関係は複雑さが増すため、注意して使用してください。 これらの関係は引き続き循環参照がチェックされます。

### <a name="try-it-out"></a>試してみましょう。  

次のタスクを試した後、どのように動作したかについて、リボンの **[ホーム]** タブから **[フィードバック]** を送信してください。

1. タスク シーケンス エディターで、 **[追加]** をクリックし、 **[全般]** を選択してから **[タスク シーケンスの実行]** をクリックします。
2. **[参照]** をクリックして子タスク シーケンスを選択します。

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>アプリケーションをインストールするときに、ユーザー操作を許可する <!-- 1356976 -->

この Preview では、タスク シーケンスの実行中にアプリケーションのインストールと対話することをエンド ユーザーに許可できます。 たとえば、さまざまなオプションの入力をエンド ユーザーに求めるセットアップ プロセスを実行します。 一部のアプリケーション インストーラーでは、ユーザー プロンプトを消せなかったり、インストール プロセスでユーザーだけが知っている特定の構成値が求められたりする場合があります。 この機能では、これらのインストール シナリオを処理することができます。

### <a name="try-it-out"></a>試してみましょう。

次のタスクを試した後、どのように動作したかについて、リボンの **[ホーム]** タブから **[フィードバック]** を送信してください。

1.  アプリケーションを作成または編集します。 詳細については、「[Configuration Manager でアプリケーションを作成する](../../apps/deploy-use/create-applications.md)」を参照してください。

    a. **Windows インストーラー (\*msi ファイル) プロパティ**で **[ユーザー エクスペリエンス]** タブを選択します。

    b. **[インストールの処理]** に **[システム用にインストールする]** を選択します。

    c. **[Log on requirement]\(ログオン要件\)** に **[ユーザーのログオン状態に関係なし]** を選択します。

    d. **[インストール プログラムの表示]** に **[ノーマル]** を選択します。 次の 3 つのオプション、 **[最小化]** 、 **[標準]** 、または **[最大化]** から選択できます。

    e. **[Allow users to interact with the program installation]\(プログラムのインストールの対話をユーザーに許可する\)** ボックスを選択します。

2.  タスク シーケンスを作成または編集して、**アプリケーションのインストール** ステップを使用してアプリケーションをインストールします。 詳細については、「[タスク シーケンスのステップ](../../osd/understand/task-sequence-steps.md)」の「[アプリケーションのインストール](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication)」をご覧ください。

    a. Windows と Configuration Manager のセットアップ ステップの後の、イメージング タスク シーケンス。

    b. 処理後グループ内のインプレース アップグレード タスク シーケンス。

3.  クライアントにタスク シーケンスを展開します。
4.  タスク シーケンスをソフトウェア センターからインストールします。

タスク シーケンスの進行中に、アプリケーションのインストール インターフェイスがターゲットのエンドユーザーのデバイスに表示されます。 タスク シーケンスの進行は、エンドユーザーがアプリケーション インストール ワークフローを完了するまで一時停止されます。

### <a name="install-using-the-wizard"></a>ウィザードを使用したインストール

ウィザードを使用してアプリを展開するときもこの機能を使用できます。

1. アプリケーションを作成または編集します。
2. アプリケーションをクライアントに展開します。
3. ソフトウェア センターからアプリケーションをインストールします。 アプリケーションのインストール インターフェイスが表示されます。 エンドユーザーはアプリケーションのインストール ウィザードに従うことで、アプリケーションが正常にインストールされます。




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。    
