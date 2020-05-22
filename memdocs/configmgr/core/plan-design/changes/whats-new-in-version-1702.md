---
title: 新バージョン 1702
titleSuffix: Configuration Manager
description: Configuration Manager のバージョン 1702 で導入された変更点および新機能について説明します。
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: eacf64245f4cfc779dc92be73e8d7e387b34f909
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427935"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>Configuration Manager のバージョン 1702 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1702 は、バージョン 1602、1606、または 1610 を実行しているインストール済みのサイトで、コンソール内の更新プログラムとして利用可能です。 また、新しい展開をインストールするときに使用する基準のバージョンとしても利用可能です。

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用する必要があります。  
>
> 詳細については、下記のリンクをクリックしてください。    
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md)  
> - [サイトで更新プログラムをインストールする](../../servers/manage/updates.md)  
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)

次の各セクションでは、Configuration Manager のバージョン 1702 で導入された変更点および新機能について詳しく説明します。  

## <a name="deprecated-features-and-operating-systems"></a>非推奨の機能とオペレーティング システム
[削除された項目と非推奨の項目](deprecated/removed-and-deprecated.md)で実装される前のサポートに関する変更点について説明します。

バージョン 1702 では、次の製品のサポートを廃止します。
- **SQL Server 2008 R2** (サイト データベース サーバー用)。 サポートの廃止が[最初に発表された](deprecated/removed-and-deprecated-server.md#sql-server)のは、2015 年 7 月 10 日でした。 使用している Configuration Manager のバージョンが 1702 より前のバージョンである場合、このバージョンの SQL Server は引き続きサポートされます。
- **Windows Server 2008 R2** (サイト システム サーバーとほとんどのサイト システムの役割用)。 サポートの廃止が[最初に発表された](deprecated/removed-and-deprecated-server.md#server-os)のは、2015 年 7 月 10 日でした。 使用している Configuration Manager のバージョンが 1702 より前のバージョンである場合、このバージョンの Windows は引き続きサポートされます。  
- **Windows Server 2008** (サイト システム サーバーとほとんどのサイト システムの役割用)。 サポートの廃止が[最初に発表された](deprecated/removed-and-deprecated-server.md#server-os)のは、2015 年 7 月 10 日でした。
- **Windows XP Embedded** (クライアント オペレーティング システムとして)。 廃止が[最初に発表された](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems)のは、2015 年 7 月 10 日でした。 使用している Configuration Manager のバージョンが 1702 より前のバージョンである場合、このバージョンの Windows は引き続きサポートされます。




## <a name="site-infrastructure"></a>サイトのインフラストラクチャ

### <a name="improvements-for-in-console-search"></a>コンソール内検索の機能強化
Configuration Manager コンソールでの検索機能の強化の内容を次に示します。
- **オブジェクトのパス:**  
  多くのオブジェクトが**オブジェクトのパス**という名前の列をサポートするようになりました。  検索時に、この列を表示結果に含めると、各オブジェクトへのパスを表示できます。 たとえば、[アプリケーション] ノードでアプリの検索を実行し、さらにサブノードも検索する場合、結果ウィンドウの *オブジェクトのパス*列には、返された各オブジェクトへのパスが表示されます。   

- **検索テキストの保持**  
  検索テキスト ボックスにテキストを入力した後で、検索対象をサブノードから現在のノードに切り替えた場合 (逆の場合も)、入力したテキストは保持されるようになったため、新しい検索でテキストを再入力せずにそのまま使用できます。

- **サブノードを検索するかどうかの選択の保持**  
  *現在のノード*または*すべてのサブノード*を検索するために選択するオプションは、作業するノードを変更しても保持されるようになりました。 この新しい動作により、コンソール内を移動するたびに、オプションを再設定する必要がなくなりました。 既定では、コンソールを開くと、オプションは現在のノードのみを検索する設定となります。


### <a name="send-feedback-from-the-configuration-manager-console"></a>Configuration Manager コンソールからフィードバックを送信する

コンソール内のフィードバック オプションを使用すれば、開発チームに直接フィードバックを送信することができます。

**[フィードバック]** オプションは、次の場所に表示されます。
- 各ノードのリボンの [ホーム] タブの左端。  
  ![リボン](./media/feedback-home.png)

- コンソールのオブジェクトを右クリックしたとき。   
   ![右クリック オプション](./media/feedback-option.png)   

  **[フィードバック]** を選択すると、ブラウザーが開いて [Configuration Manager UserVoice フィードバック Web サイト](https://configurationmanager.uservoice.com/forums/300492-ideas) が表示されます。


###  <a name="changes-for-updates-and-servicing"></a>更新プログラムとサービスの変更
更新プログラムとサービスの変更を次に示します。

- **ノードの場所**   
  バージョン 1702 をインストールすると、 **[管理]** の下に **[更新プログラムとサービス]** ノードが最上位ノードとして表示されます。 **[クラウド サービス]** の子ノードではなくなりました。

- **新しい更新プログラムの状態**  
  コンソール内で使用可能な更新プログラムを確認する場合、次の 2 つの状態が表示されるようになりました。  
  - **インストールが可能** - これは、ダウンロードが完了していて、いつでもインストールできる状態にある更新プログラムです。
  - **ダウンロードの準備ができました** - この更新プログラムは使用できますが、まだダウンロードされていません。 この更新プログラムのダウンロードを選択することもできますが、より新しい更新プログラムによって置き換えられています。


- **簡単になった更新プログラムの選択**  
  次の更新時に、お使いのインフラストラクチャで複数の更新プログラムが適用対象になった場合、最新の更新プログラムのみがダウンロードされます。 たとえば、現在のサイト バージョンが、リリースされている最新バージョンよりも 2 つ以上古い場合、その最新の更新プログラム バージョンのみが自動的にダウンロードされます。  

  リリース済みのその他の更新プログラムが最新バージョンではない場合でも、ダウンロードしてインストールすることができます。 古い更新プログラムをダウンロードした場合、その更新プログラムは新しい更新プログラムで置き換えられたという警告が表示されます。 *[ダウンロード可能]* と表示される更新プログラムをダウンロードするには、コンソールで更新プログラムを選択し、 **[ダウンロード]** をクリックします。

- **古い更新プログラムのクリーンアップの改善**   
  サイト サーバー上の 'EasySetupPayload' フォルダーから不要なダウンロードを削除する自動クリーンアップ機能を追加しました。 クリーンアップ機能は、バージョン 1702 で導入されているため、更新プログラムのロールアップや今後の更新プログラムのバージョンなど、後続の更新プログラムをインストールした後で動作し始めます。  


### <a name="data-warehouse-service-point"></a>データ ウェアハウス サービス ポイント
データ ウェアハウス サービス ポイントを使用して、Configuration Manager 展開の長期的な履歴データを格納およびレポートできるようになりました。

データ ウェアハウスでは、最大 2 TB のデータをサポートし、変更追跡にはタイムスタンプが使用されます。 データの格納は、Configuration Manager サイト データベースからデータ ウェアハウス データベースへの自動化された同期によって達成されます。 この情報には、レポート サービス ポイントからアクセスできます。

詳細については、「[データ ウェアハウス サービス ポイント](../../servers/manage/data-warehouse.md)」を参照してください。


### <a name="peer-cache-improvements"></a>ピア キャッシュの改善
バージョン 1702 以降、ピア キャッシュ ソース コンピューターが次のいずれかの条件を満たす場合、ピア キャッシュ ソース コンピューターはコンテンツの要求を拒否するようになります。  
-  バッテリ低下モードの場合。
-  コンテンツの要求時に CPU 負荷が 80% を超えている場合。
-  ディスク I/O の *AvgDiskQueueLength* が 10 を超えている場合。
-  新たにコンピューターに接続できない場合。   
詳細については、[「Configuration Manager クライアントのピア キャッシュ」](../hierarchy/client-peer-cache.md) の「**Limited access to a peer cache source**」 (ピア キャッシュ ソースへのアクセスの制限) を参照してください。   

さらに、3 つの新しいレポートがレポート ポイントに追加されます。 これらのレポートを使用すれば、問題のあった境界グループ、コンピューター、コンテンツなど、拒否されたコンテンツ要求に関する詳細を把握することができます。 ピア キャッシュ トピックの [「Monitoring」](../hierarchy/client-peer-cache.md#monitoring) (監視) を参照してください。

### <a name="content-library-cleanup-tool"></a>コンテンツ ライブラリのクリーンアップ ツール
コンテンツが既にアプリケーションに関連していない場合は、[コンテンツ ライブラリのクリーンアップ ツール](../hierarchy/content-library-cleanup-tool.md) を使用して、配布ポイントから該当するコンテンツを削除します。


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Azure Government Cloud で OMS コネクタを使用する
OMS コネクタを使用すれば、Microsoft Azure Government Cloud 内の OMS Log Analytics に接続することができます。 そのためには、OMS コネクタが Government Cloud と連携するように構成ファイルを変更してから OMS コネクタをインストールする必要があります。 詳細については、[「Use the OMS connector with the Azure Government cloud」](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) (Azure Government Cloud で OMS コネクタを使用する) を参照してください。

### <a name="software-update-points-are-added-to-boundary-groups"></a>境界グループへのソフトウェア更新ポイントの追加
バージョン 1702 以降では、クライアントは境界グループを使用して、新しいソフトウェアの更新ポイントを検索します。また、現在のソフトウェアの更新ポイントにアクセスできなくなっている場合は、フォールバックして新しいソフトウェアの更新ポイントを検索します。 ソフトウェアの更新ポイントをそれぞれ異なる境界グループに追加して、クライアントで検索できるサーバーを制御できます。 詳細については、[境界グループの構成](../../servers/deploy/configure/boundary-groups.md)に関するトピックの[ソフトウェアの更新ポイント](../../servers/deploy/configure/boundary-groups.md#software-update-points)の記述を参照してください。


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>コンプライアンス設定

### <a name="new-compliance-settings-for-ios"></a>iOS 用の新しいコンプライアンス設定

Microsoft Intune で使用できるように整合させるために、iOS デバイス用の新しい設定を多数追加しました。


## <a name="application-management"></a>アプリケーション管理

### <a name="improved-support-for-windows-store-for-business-apps"></a>ビジネス向け Windows ストアのアプリのサポート強化

オンラインでライセンスされたアプリを、ビジネス向け Windows ストアから、Configuration Manager クライアントを使用して管理する Windows 10 PC に展開できるようになりました。
詳細については、[「ビジネス向け Windows ストアからのアプリの管理」](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) を参照してください。

### <a name="check-for-running-executable-files-before-installing-an-application"></a>アプリケーションをインストールする前に実行中の実行可能ファイルを確認する

展開の種類の **[プロパティ]** ダイアログ ボックスの **[インストールの処理]** タブで、実行可能ファイルが実行中の場合、その展開の種類のインストールをブロックする実行可能ファイルの 1 つを指定できるようになりました。 ユーザーは、その展開の種類をインストールするには、実行中の実行可能ファイルを終了する必要があります (または、展開の目的が必須の場合は自動的に終了することができます)。

アプリケーションの展開が **[使用可能]** で、エンド ユーザーがアプリケーションをインストールしようとすると、インストールを続行する前に、指定した実行中の実行可能ファイルを終了するようにユーザーに求めます。

アプリケーションの展開が **[必須]** で、オプション **[[展開の種類プロパティ] ダイアログ ボックスの [インストールの処理] タブで指定した実行中の実行可能ファイルをすべて自動的に閉じる]** がオンの場合、アプリケーションのインストール期限に達したときに、指定した実行可能ファイルが自動的に閉じられることを通知するダイアログ ボックスが表示されます。

### <a name="app-management-improvements-for-hybrid-mdm"></a>ハイブリッド MDM でのアプリケーション管理の強化

- [ボリューム購入 iOS アプリをデバイス コレクションに展開する](#deploy-volume-purchased-ios-apps-to-device-collections)
- [iOS Volume Purchase Program for Education のサポート](#support-for-ios-volume-purchase-program-for-education)
- [複数の Volume Purchase Program トークンのサポート](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>オペレーティング システムの展開

### <a name="expire-stand-alone-media"></a>スタンドアロン メディアの有効期限の設定
スタンドアロン メディアを作成する場合に、メディアに対して、必要に応じて開始日と有効期限を設定するための新しいオプションが追加されました。 これらの設定は既定では無効になっています。 スタンドアロン メディアが実行される前に、この日付はコンピューター上のシステム時刻と比較されます。 システム時刻が開始時刻より前か、有効期限より後の場合、スタンドアロン メディアは開始されません。 これらのオプションは、New-CMStandaloneMedia PowerShell コマンドレットを使用して利用することもできます。 詳細については、[スタンドアロン メディアの作成](../../../osd/deploy-use/create-stand-alone-media.md)に関するトピックを参照してください。

### <a name="package-id-displayed-in-task-sequence-steps"></a>タスク シーケンス ステップでのパッケージ ID の表示
パッケージ、ドライバー パッケージ、オペレーティング システム イメージ、ブート イメージ、またはオペレーティング システム アップグレード パッケージを参照するすべてのタスク シーケンス ステップで、参照されるオブジェクトのパッケージ ID が表示されるようになりました。 タスク シーケンス ステップでは、アプリケーションの参照時にオブジェクト ID が表示されます。

### <a name="support-for-additional-content-in-stand-alone-media"></a>スタンドアロン メディアでの追加のコンテンツのサポート
スタンドアロン メディアで追加のコンテンツがサポートされるようになりました。 追加のパッケージ、ドライバー パッケージ、およびアプリケーションを選択し、タスク シーケンスで参照される他のコンテンツと共にメディアにステージングすることができます。 以前は、タスク シーケンスで参照されるコンテンツのみがスタンドアロン メディアにステージングされていました。 詳細については、[スタンドアロン メディアの作成](../../../osd/deploy-use/create-stand-alone-media.md)に関するトピックを参照してください。

### <a name="hardware-inventory-collects-uefi-information"></a>ハードウェア インベントリでの UEFI 情報の収集
新しいハードウェア インベントリ クラス (**SMS_Firmware**) とプロパティ (**UEFI**) は、コンピューターが UEFI モードで起動しているかどうかを判別するのに役立ちます。 コンピューターが UEFI モードで起動している場合、**UEFI** プロパティは **TRUE** に設定されています。 これはハードウェア インベントリでは既定で有効になっています。 ハードウェア インベントリの詳細については、「[ハードウェア インベントリを構成する方法](../../clients/manage/inventory/configure-hardware-inventory.md)」を参照してください。

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>影響の大きいタスク シーケンスに関するソフトウェア センターの警告メッセージの改善
このリリースでは、影響の大きい展開タスク シーケンスに関するソフトウェア センターの警告メッセージについて、次の点が改善されています。

- タスク シーケンスのプロパティで、危険性が高い展開として、オペレーティング システム以外のタスク シーケンスを含め、任意のタスク シーケンスを構成できます。 特定の条件を満たす任意のタスク シーケンスは、影響度大として自動的に定義されます。 詳細については、「[System Center Configuration Manager の危険度の高い展開を管理するための設定](../../servers/manage/settings-to-manage-high-risk-deployments.md)」を参照してください。
- タスク シーケンスのプロパティでは、影響の大きい展開について既定の通知メッセージを使用するか、独自のカスタム通知メッセージを作成することができます。
- タスク シーケンスのプロパティでは、ソフトウェア センターのプロパティ (再起動を必須にする、タスク シーケンスのダウンロード サイズ、推定実行時間など) を構成できます。
- インプレース アップグレードの既定の影響の大きい展開のメッセージには、アプリ、データ、および設定が自動的に移行されると表示されるようになりました。 以前のバージョンでは、オペレーティング システムのインストールに関する既定のメッセージには、すべてのアプリ、データ、および設定が失われると表示されていましたが、これはインプレース アップグレードの場合は該当しない内容でした。

詳細については、[影響の大きいタスク シーケンス設定の構成](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence)に関するトピックを参照してください。

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>タスク シーケンスが失敗した場合に前のページに戻る
タスク シーケンスを実行し、エラー害が発生した場合に、前のページに戻ることができるようになりました。 これより前のリリースでは、エラーが発生すると、タスク シーケンスを再起動する必要があります。 たとえば、次のシナリオでは **[前へ]** ボタンを使用できます。

- Windows PE でコンピューターを起動する場合、タスク シーケンスが使用できるようになる前に、タスク シーケンス ブートス トラップ ダイアログ ボックスが表示される場合があります。 このシナリオで [次へ] をクリックすると、タスク シーケンスの最終ページが表示され、使用できるタスク シーケンスがないことを示すメッセージが示されます。 ここで、 **[前へ]** をクリックすれば、使用できるタスク シーケンスをもう一度検索することができます。 タスク シーケンスが使用可能になるまで、このプロセスを繰り返すことができます。
- タスク シーケンスを実行しても、依存するコンテンツ パッケージが配布ポイントでまだ使用できない場合、タスク シーケンスは失敗します。 不足しているコンテンツを配布するか (そのコンテンツがまだ配布されていない場合)、またはコンテンツが配布ポイントで使用できるようになるまで待機してから、 **[前へ]** をクリックして、もう一度タスク シーケンスでコンテンツを検索します。

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>利用可能な展開とタスク シーケンスのコンテンツを事前キャッシュする
バージョン 1702 以降、利用可能な展開とタスク シーケンスのコンテンツを事前キャッシュする機能を使用できるようになりました。 コンテンツの事前キャッシュ機能には、クライアントが展開を受信してすぐに適用可能なコンテンツのみをダウンロードできるようにするオプションが用意されています。 したがって、ユーザーがソフトウェア センターで **[インストール]** をクリックすると、コンテンツはローカルのハード ドライブ上にあるため、コンテンツは準備完了の状態にあり、インストールが迅速に開始されます。 詳細については、[「Configure pre-cache content」](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content) (コンテンツの事前キャッシュを構成する) を参照してください。

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>インプレース アップグレード時に BIOS から UEFI に変換する
Windows 10 Creators Update では、EFI 対応ハードウェアのハード ディスクのパーティションを再分割するプロセスを自動化する簡単な変換ツールが導入され、変換ツールは Windows 7 から Windows 10 へのインプレース アップグレード プロセスに統合されます。 このツールをオペレーティング システムのアップグレード タスク シーケンスと、ファームウェアを BIOS から UEFI に変換する OEM ツールと組み合わせて使用する場合、Windows 10 Creators Update へのインプレース アップグレード時にコンピューターを BIOS から UEFI に変換することができます。 詳細については、「[Task sequence steps to manage BIOS to UEFI conversion](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)」(BIOS からUEFI への変換を管理するためのタスク シーケンス手順) を参照してください。

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>[アプリケーションのインストール] タスク シーケンスのステップの向上
このバージョンでは、次の機能強化が実施されています。
- **[アプリケーションのインストール**] タスク シーケンス ステップで、インストールできるアプリケーションの最大数が 99 に増えました。 以前のアプリケーションの最大数は 9 でした。
- タスク シーケンス エディターで**アプリケーションのインストール** タスク シーケンス ステップにアプリケーションを追加する場合に、 **[インストールするアプリケーションの選択]** ウィンドウから複数のアプリケーションを選択できるようになりました。

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>[ドライバーの自動適用] タスク シーケンスの機能強化
HTTP カタログの要求時に [ドライバーの自動適用] タスク シーケンス ステップでタイムアウト値を構成する場合に、新しいタスク シーケンス変数を使用できるようになりました。 次の変数と既定値 (秒) を使用できます。
- SMSTSDriverRequestResolveTimeOut  
  既定:60
- SMSTSDriverRequestConnectTimeOut  
  既定:60
- SMSTSDriverRequestSendTimeOut  
  既定:60
- SMSTSDriverRequestReceiveTimeOut  
  既定:480

### <a name="windows-10-adk-tracked-by-build-version"></a>ビルド バージョンによる Windows 10 ADK の追跡
ビルド バージョンで Windows 10 ADK を追跡できるようになりました。これで、Windows 10 ブート イメージのカスタマイズ時により多くの操作がサポートされるようになります。 たとえば、サイトで Windows ADK for Windows 10 バージョン 1607 を使用する場合、コンソールでカスタマイズできるのはバージョン 10.0.14393 のブート イメージのみになります。 WinPE バージョンのカスタマイズの詳細については、「[ブート イメージのカスタマイズ](../../../osd/get-started/customize-boot-images.md)」を参照してください。

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>既定のブート イメージのソース パスを変更できなくなりました
既定のブート イメージは Configuration Manager で管理され、既定のブート イメージのソース パスは Configuration Manager コンソールや Configuration Manager SDK を使用して変更できなくなりました。 カスタム ブート イメージのカスタム ソース パスは引き続き構成可能です。

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Configuration Manager を新しいバージョンにアップグレードした後、既定のブート イメージが再生成される
このリリース以降、Windows ADK のバージョンをアップグレードし、更新プログラムとサービスを使用して、Configuration Manager の最新バージョンをインストールするときに、Configuration Manager によって既定のブート イメージが再生成されます。 これには、更新された Windows ADK の新しい Windows PE バージョン、新しいバージョンの Configuration Manager クライアント、ドライバー、カスタマイズが含まれます。カスタム ブート イメージは変更されません。 詳細については、「[ブート イメージの管理](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault)」を参照してください。

## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="deploy-office-365-apps-to-clients"></a>クライアントに Office 365 アプリを展開する
1702 以降、Office 365 クライアント管理ダッシュボードから Office 365 のインストーラーを起動できます。インストーラーを使用すると、Office 365 のインストール設定を構成し、Office コンテンツ配信ネットワーク (CDN) からファイルをダウンロードし、Configuration Manager でファイルをアプリケーションとして展開できます。 詳細については、[Office 365 ProPlus の更新プログラムの管理](../../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps)に関するページを参照してください。

> [!IMPORTANT]
> Configuration Manager で Office 365 アプリケーション ウィザードを使用して作成し、展開した Office 365 は、 **[Office 365 クライアント エージェントの管理を有効にする]** ソフトウェア更新プログラム クライアント エージェント設定を有効にしない限り、Configuration Manager で自動的に管理されません。 詳細については、「[System Center Configuration Manager のクライアント設定について](../../clients/deploy/about-client-settings.md)」を参照してください。

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Windows 10 更新プログラムに対する高速インストール ファイルの管理
バージョン 1702 以降、Configuration Manager では Windows 10 更新プログラムに対する高速インストール ファイルがサポートされています。 サポートされているバージョンの Windows 10 を使用する場合は、当月の Windows 10 累積的な更新プログラムと、前月の更新プログラムとの差分のみをダウンロードする Configuration Manager 設定を使用できます。 高速インストール ファイルを使用しない場合、Configuration Manager では完全な Windows 10 累積的な更新プログラム (以前の月の更新プログラムをすべて含む) が毎月ダウンロードされます。 高速インストール ファイルを使用すると、クライアント上でのダウンロード量を少なくし、インストールに要する時間を短縮できます。 詳細については、[「Windows 10 更新プログラムに対する高速インストール ファイルの管理」](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md) を参照してください。


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>モバイル デバイス管理

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>ハイブリッド MDM の作成ウィザードで Android と iOS のバージョン指定が不要に

ハイブリッド モバイル デバイス管理 (MDM) のバージョン 1702 以降、Intune で管理されるデバイスの新しいポリシーとプロファイルを作成する場合に Android および iOS の特定のバージョンを指定する必要がなくなりました。 代わりに、次のデバイス タイプのいずれかを選択します。

- Android
- Samsung KNOX Standard 4.0 以降
- iPhone
- iPad

この変更は、次の項目を作成するウィザードに影響します。

- 構成項目
- コンプライアンス ポリシー
- 証明書プロファイル
- 電子メール プロファイル
- VPN プロファイル
- Wi-Fi プロファイル

この変更により、新しい Configuration Manager のリリースまたは拡張機能を必要とせずに、ハイブリッド展開で新しい Android および iOS のバージョンによりすばやくサポートを提供できます。 Intune スタンドアロンで新しいバージョンがサポートされると、ユーザーはモバイル デバイスをそのバージョンにアップグレードできるようになります。

以前のバージョンの Configuration Manager からアップグレードする場合の問題を防ぐため、モバイルのオペレーティング システムのバージョンが各項目の [プロパティ] ページに表示されています。 特定のバージョンを対象にする必要がある場合は、新しい項目を作成し、新しく作成された項目の [プロパティ] ページで、対象のバージョンを指定します。 

> [!NOTE]
> プロパティ ページで使用可能な最新のモバイル オペレーティング システム バージョンは、そのバージョンとすべての後続バージョンに適用されます。 プロパティ ページには次の選択肢があり、Android 7 および iOS 10 以降のオペレーティング システムを対象としています。 
> - **Android 7 以降**
> - **iOS 10 以降のすべての iPhone または iPod touch デバイス**
> - **iOS 10 以降のすべての iPad デバイス**

### <a name="android-for-work-support"></a>Android for Work のサポート
1702 以降、Microsoft Intune を使用したハイブリッド モバイル デバイスの管理では、Android for Work デバイスの登録と管理をサポートするようになりました。

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>ボリューム購入 iOS アプリをデバイス コレクションに展開する

ライセンスされたアプリをユーザーだけでなくデバイスにも展開できるようになりました。 デバイス ライセンスをサポートするアプリ機能に応じて、次のように、展開時に適切なライセンスが要求されます。

|||||
|-|-|-|-|
|Configuration Manager バージョン|アプリでのデバイス ライセンスのサポート|展開コレクションの種類|要求されるライセンス|
|1702 より前|はい|ユーザー|ユーザー ライセンス|
|1702 より前|いいえ|ユーザー|ユーザー ライセンス|
|1702 より前|はい|デバイス|ユーザー ライセンス|
|1702 より前|いいえ|デバイス|ユーザー ライセンス|
|1702 以降|はい|ユーザー|ユーザー ライセンス|
|1702 以降|いいえ|ユーザー|ユーザー ライセンス|
|1702 以降|はい|デバイス|デバイス ライセンス|
|1702 以降|いいえ|デバイス|ユーザー ライセンス|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>iOS Volume Purchase Program for Education のサポート

iOS Volume Purchase Program for Education から購入したアプリを展開し追跡できるようになりました。

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>複数の Volume Purchase Program トークンのサポート

複数の Apple Volume Purchase Program トークンを Configuration Manager に関連付けることができるようになりました。

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>ビジネス向け Windows ストアで基幹業務アプリをサポートする

ビジネス向け Windows ストアから、カスタマイズされた基幹業務アプリを同期できるようになりました。

### <a name="conditional-access-device-compliance-policy-improvements"></a>条件付きアクセス デバイス コンプライアンス ポリシーの改善

ユーザーがアプリのコンプライアンス非対応リストに含まれているアプリを使用している場合、新しいデバイスのコンプライアンス ポリシー ルールを使用して、条件付きアクセスをサポートする会社のリソースへのアクセスをブロックできます。 アプリのコンプライアンス非対応リストは、管理者が新しい準拠ルール **[インストールできないアプリ]** の追加時に定義できます。 このルールを使用するには、管理者がコンプライアンス非対応リストにアプリを追加するときに、**アプリ名**、**アプリ ID**、**アプリの発行元** (省略可能) を入力する必要があります。 この設定は、iOS および Android デバイスにのみ適用されます。

また、組織はこの設定を使用して、セキュリティで保護されていないアプリを介したデータ漏えいを軽減し、特定のアプリ経由の過度なデータ使用を防ぐことができます。


### <a name="new-mobile-threat-defense-monitoring-tools"></a>新しい Mobile Threat Defense 監視ツール

バージョン 1702 から、Mobile Threat Defense サービス プロバイダーでコンプライアンス状態を監視する新しい方法を利用できます。


## <a name="protect-devices"></a>デバイスを保護する

### <a name="detect-outdated-antimalware-client-versions"></a>古くなったマルウェア対策クライアント バージョンを検出する
バージョン 1702 から、Endpoint Protection クライアントが古くならないようにするためのアラートを構成することができます。 詳細については、[古くなったマルウェア クライアントの警告](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client) に関するページを参照してください。

### <a name="device-health-attestation-updates"></a>デバイス正常性証明書の更新プログラム
オンプレミス用のデバイス正常性証明書サービスを管理ポイントから構成および管理ポイントできるようになりました。 詳細については、[正常性構成証明書](../../servers/manage/health-attestation.md) に関するページを参照してください。

### <a name="certificate-profiles-for-windows-hello-for-business"></a>ビジネス向け Windows Hello の証明書プロファイル

ビジネス向け Windows Hello キー コンテナーに証明書プロファイルを保存する場合、証明書プロファイルでスマート カード ログオン EKU が使用されているときには、キー登録で証明書が正しく検証されるようにアクセス許可を構成する必要があります。
詳細については、[Windows Hello for Business の設定](../../../protect/deploy-use/windows-hello-for-business-settings.md) に関するページを参照してください。

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>エンド ユーザーを対象とした新しい Windows Hello for Business 通知
新しい Windows 10 通知は、Windows Hello for Business のセットアップ (たとえば、PIN の設定) を完了するには追加の操作が必要である旨をエンドユーザーに通知します。
