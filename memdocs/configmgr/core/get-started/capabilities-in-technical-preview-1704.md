---
title: Technical Preview 1704 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1704 で使用できる機能について説明します。
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705270"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Configuration Manager の Technical Preview 1704 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1704 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    


**このバージョンでお試しいただける新機能を次に示します。**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>アプリ構成ポリシーを使用した Android アプリの構成
Configuration Manager のアプリ構成ポリシーを使用し、ユーザーが Android for Work デバイスでアプリを実行するときに必要となるような設定を配布できます。 Android アプリ構成ポリシーは、Android for Work デバイス上でのみ使用でき、Play for Work ストアの承認済みアプリに適用されます。

### <a name="try-it-out"></a>試してみましょう                 

Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]**  >  **[アプリケーション管理]**  >  **[アプリ構成ポリシー]** の順に選択し、 **[アプリ構成ポリシーの作成]** を選択します。 ウィザードの **[全般]** ページで、 **[構成ポリシーの種類の選択]** ができます。 アプリ構成ポリシーの対象となるプラットフォームを指定します ( **[Android for Work アプリ用の構成ポリシー]** )。 次に、 **[名前と値のペアを指定します]** または **[プロパティ一覧 JSON ファイルを参照します]** を選択します。 新しいアプリ構成ポリシーが **[ソフトウェア ライブラリ]** ワークスペースの **[アプリ構成ポリシー]** ノードに表示されます。 アプリ構成ポリシーと Android for Work アプリの展開を関連付けるには、「[アプリケーションの展開](../../apps/deploy-use/deploy-applications.md)」トピックの手順に従い、通常どおりにアプリを展開します。

## <a name="hardware-inventory-collects-secure-boot-information"></a>ハードウェア インベントリでのセキュア ブート情報の収集
ハードウェア インベントリは、クライアントでセキュア ブートが有効になっているかどうかの情報を収集します。 この情報は、**SMS_Firmware** クラス (バージョン 1702 で導入) に格納されており、ハードウェア インベントリでは既定で有効になっています。 ハードウェア インベントリの詳細については、[ハードウェア インベントリを構成する方法](../clients/manage/inventory/configure-hardware-inventory.md)に関する記事を参照してください。

## <a name="add-child-task-sequences-to-a-task-sequence"></a>子タスク シーケンスをタスク シーケンスに追加する
このバージョンでは、別のタスク シーケンスを実行する新しいタスク シーケンスのステップを追加することができ、タスク シーケンス間に親子関係を作成できます。 これにより、再利用可能なモジュール型のタスク シーケンスをより多く作成できます。  

タスク シーケンスに子タスク シーケンスを追加する場合は、以下の点を考慮してください。

- 親と子のタスク シーケンスが、クライアントが実行する 1 つのポリシーに効率的に結合されていること。
- 別のタスク シーケンスの親になっている子タスク シーケンスを追加することはできないこと。
- 環境がグローバルであること。 たとえば、親タスク シーケンスによって変数が設定され、その変数が子タスク シーケンスによって変更された場合、変数はそれ以降変更されたままになります。 同様に、子タスク シーケンスによって新しい変数が作成された場合、親タスク シーケンスの残りのステップでその変数を使用できます。
- ステータス メッセージは、通常どおり 1 つのタスク シーケンス操作で複数送信されること。
- タスク シーケンスは、エントリを smsts.log ファイルに書き込み、新しいログ エントリによって子タスク シーケンスの開始タイミングを明確にするということ。
- Configuration Manager バージョン 1704 の Technical Preview で、子タスク シーケンスがパッケージを参照している状態で親タスク シーケンスがソフトウェア センターから実行された場合、子タスク シーケンスが実行されるときにクライアントはそのパッケージ コンテンツを検出できないということ。 このシナリオでは、タスク シーケンスをメディア (ブート メディア、PXE など) から実行する必要があります。  

    子タスク シーケンスが、**コマンド ラインの実行** (パッケージ参照なし) や**形式**、**BitLocker** などのステップを使用している場合は、そのタスク シーケンスをソフトウェア センターから正常に実行できます。

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>子タスク シーケンスをタスク シーケンスに追加するには
1. タスク シーケンス エディターで、 **[追加]** をクリックし、 **[全般]** を選択してから **[タスク シーケンスの実行]** をクリックします。
2. **[参照]** をクリックして子タスク シーケンスを選択します。  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>最新バージョンの Windows PE を使用してブート イメージを再読み込みする
選択したブート イメージ上で **[配布ポイントの更新]** を実行した場合、そのブート イメージ内の (Windows ADK インストール ディレクトリにある) 最新バージョンの Windows PE を再読み込みできます。 ウィザードの **[全般]** ページには、サイト サーバーにインストールされた Windows ADK のバージョン情報、ブート イメージ内の Windows PE を使用した Windows ADK のバージョン情報、Configuration Manager クライアントのバージョン情報が表示されます。 この情報はブート イメージを再読み込みするかどうかを決めるのに役立ちます。 また、 **[ブート イメージ]** ノードでブート イメージを表示すると、新しい列 ( **[クライアント バージョン]** ) が追加されているため、各ブート イメージがどのバージョンの Configuration Manager クライアントを使用しているかを確認できます。

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>最新バージョンの Windows PE を使用してブート イメージを再読み込みするには

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]**  >  **[オペレーティング システム]**  >  **[ブート イメージ]** に移動します。
2. ブート イメージを選択し、 **[配布ポイントの更新]** をクリックします。
3. ウィザードの **[全般]** ページで、 **[Reload boot image using the current version of Windows PE from the installed Windows ADK]\(インストール済みの Windows ADK にある最新バージョンの Windows PE を使用してブート イメージを再読み込みする)** を選択します。

## <a name="improvements-to-operating-system-deployment"></a>オペレーティング システムの展開に関する機能拡張
オペレーティング システムの展開について、皆さまからのフィードバックを基に、次のような機能拡張を行いました。

- [オペレーティング システム イメージに使用される新しい **[OS バージョン]** 列](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): **[オペレーティング システム イメージ]** ノードや **[オペレーティング システム アップグレード パッケージ]** ノードで情報を表示したときに、イメージのオペレーティング システムのバージョンを表示するように、 **[OS バージョン]** という名前の新しい列を追加しました。 .WIM ファイル内の最初のインデックスのバージョンだけが表示されます。 他のインデックスのオペレーティング システムのバージョンを確認するには、そのイメージの **[詳細]** タブに移動してください。

- [smsts.log によるより効率的なログの記録](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): このバージョンから、CCM_CIVersionInfo.PolicyID 情報のために smsts.log ファイルにエントリを書き込む必要はなくなりました。 以前のバージョンでは、この情報のために多くのエントリが書き込まれ、ログ ファイル内で関連情報を探しにくくなっていました。
