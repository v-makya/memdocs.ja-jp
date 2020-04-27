---
title: Office 365 クライアント管理ダッシュボード
titleSuffix: Configuration Manager
description: Office 365 クライアント管理ダッシュボードから Office 365 クライアントの情報を確認します
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: 7e6ed38d0f4217bfc70d3ddb196527d421e5d7c1
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110391"
---
# <a name="office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボード

*適用対象:Configuration Manager (Current Branch)*

> [!Note]
> 2020 年 4 月 21 日以降、Office 365 ProPlus は、**Microsoft 365 Apps for enterprise** に名前が変更されます。 詳細については、「[Office 365 ProPlus の名前の変更](https://docs.microsoft.com/deployoffice/name-change)」を参照してください。 コンソールの更新中は、Configuration Manager コンソールやサポート ドキュメントに古い名前へのリファレンスが表示される場合があります。

Configuration Manager バージョン 1802 以降では、Office 365 クライアント管理ダッシュボードから Office 365 クライアントの情報を確認できます。 Office 365 クライアント管理ダッシュボードでは、グラフ セクションを選択すると関連するデバイスの一覧が表示されます。 <!--1357281 -->

## <a name="prerequisites"></a>[前提条件]

### <a name="enable-hardware-inventory"></a>ハードウェア インベントリを有効にする

Office 365 クライアント管理ダッシュ ボードに表示されるデータは、ハードウェア インベントリから取得されます。 データがダッシュボードに表示されるようにするため、ハードウェア インベントリを有効にし、**Office 365 ProPlus 構成**ハードウェア インベントリ クラスを選択します。
 
1. ハードウェア インベントリがまだ有効になっていない場合は、有効にします。 詳細については、「[Configure hardware inventory](../../core/clients/manage/inventory/configure-hardware-inventory.md)」(ハードウェア インベントリを構成する) を参照してください。
2. Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]**  >  **[既定のクライアント設定]** の順に選択します。  
3. **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** をクリックします。  
4. **[既定のクライアント設定]** ダイアログ ボックスで、 **[ハードウェア インベントリ]** をクリックします。  
5. **[デバイス設定]** の一覧で、 **[クラスの設定]** をクリックします。  
6. **[ハードウェア インベントリ クラス]** ダイアログ ボックスで、 **[Office 365 ProPlus 構成]** を選択します。  
7. **[OK]** をクリックして変更を保存し、 **[ハードウェア インベントリ クラス]** ダイアログ ボックスを閉じます。

ハードウェア インベントリが報告されると、Office 365 クライアント管理ダッシュボードにデータが表示されます。

### <a name="connectivity-for-top-level-site-server"></a>最上位サイト サーバーの接続

*(前提条件としてバージョン 1906 で導入)*

ご利用の最上位サイト サーバーから、次のエンドポイントにアクセスして、準備ファイルをダウンロードする必要があります。

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> これらのシナリオでは、クライアント デバイスのインターネット接続は必要ありません。

### <a name="enable-data-collection-for-office-365-proplus"></a>Office 365 ProPlus のデータ収集を有効にする

*(前提条件としてバージョン 1910 で導入)*

バージョン 1910 以降では、 **[Office 365 ProPlus Pilot と正常性] ダッシュボード**に情報を設定するために、Office 365 ProPlus のデータ収集を有効にする必要があります。 データは Configuration Manager サイト データベースに格納され、Microsoft に送信されることはありません。

このデータは、「[Office 365 ProPlus から Microsoft に送信された診断データ](https://docs.microsoft.com/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft)」で説明されている診断データとは異なります。

データ収集を有効にするには、グループ ポリシーを使用するか、レジストリを編集します。

#### <a name="enable-data-collection-from-group-policy"></a>グループ ポリシーからデータ収集を有効にする

1. [Microsoft ダウンロード センターから最新の管理用テンプレート ファイル](https://www.microsoft.com/download/details.aspx?id=49030)をダウンロードします。
2. `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard` で **[テレメトリ データの収集を有効にする]** ポリシー設定を有効にします。
    - または、[Office クラウド ポリシー サービス](https://docs.microsoft.com/DeployOffice/overview-office-cloud-policy-service)を使用してポリシー設定を適用します。
    - このポリシー設定は、このデータ収集用に展開する必要はない Office テレメトリ ダッシュボードでも使用されます。

#### <a name="enable-data-collection-from-the-registry"></a>レジストリからデータ収集を有効にする

次のコマンドは、レジストリからデータ収集を有効にする方法の例です。

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボードの表示

Office 365 クライアント管理ダッシュボードを表示するには、Configuration Manager コンソールで **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[Office 365 クライアント管理]** に移動します。 ダッシュボードの上部にある **[コレクション]** ドロップダウン設定を使用して、特定のコレクションのメンバーでダッシュボードのデータをフィルター処理します。 Configuration Manager バージョン 1802 以降では、Office 365 クライアント管理ダッシュボードに、グラフ セクションが選択されたときに関連するデバイスのリストが表示されます。

Office 365 クライアント管理ダッシュボードには、次の情報のグラフが表示されます。

- Office 365 クライアントの数
- Office 365 クライアントのバージョン
- Office 365 クライアントの言語
- Office 365 クライアントのチャネル。詳細については、「[Office 365 ProPlus 更新プログラム チャネルの概要](/DeployOffice/overview-of-update-channels-for-office-365-proplus)」をご覧ください。


## <a name="integration-for-office-365-proplus-readiness"></a><a name="bkmk_o365_readiness"></a> Office 365 ProPlus の準備の統合
<!--3735402-->
Configuration Manager バージョン 1902 以降では、ダッシュボードを使って Office 365 ProPlus へのアップグレードの準備ができている信頼性の高いデバイスを特定できます。 この統合により、環境内での Office アドインとマクロに関する潜在的な互換性の問題の分析情報が得られます。 そして、Configuration Manager を使用して Office を展開し、デバイスを準備します。

Office 365 クライアント管理ダッシュボードには、 **[O365 ProPlus Upgrade Readiness]** という新しいタイルが含まれています。 このタイルは次の状態のデバイスの横棒グラフです。
- 未評価
- アップグレードの準備完了
- レビューが必要

デバイスの一覧にドリルスルーするには、状態を選択します。 この準備状況レポートは、デバイスに関する詳細を示します。 Office のアドインとマクロの両方の互換性状態の列が含まれています。

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Office 365 ProPlus の準備の統合のための前提条件

- クライアント設定でハードウェア インベントリを有効にしてください。 詳細については、「[前提条件](#prerequisites)」のセクションを参照してください。  

- デバイスでアドインの準備状況ファイルをダウンロードするには、Office コンテンツ配信ネットワーク (CDN) への接続が必要です。 詳しくは、「[コンテンツ配信ネットワーク](https://docs.microsoft.com/office365/enterprise/content-delivery-networks)」を参照してください。 デバイスでこのファイルをダウンロードできない場合、アドインの状態は *[レビューが必要]* です。  

    > [!Note]  
    > この機能のデータは Microsoft に送信されません。  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a> 詳細なマクロの準備状況

既定では、スキャン エージェントは、各デバイスの一番最近使用した (MRU) ファイルの一覧を探します。 この一覧内の、マクロをサポートするファイルをカウントします。 このファイルには次の種類が含まれています。
- Excel マクロ対応のブック (.xlsm) や Word マクロ対応の文書 (.docm) などの、マクロ対応の Office ファイル形式  
- マクロのコンテンツの有無を示さない古い Office 形式。 たとえば、Excel 97-2003 ブック (.xls) などです。

マクロの互換性についてより詳しい情報が必要な場合は、マクロ ファイル内のコードを分析するための **Office 用準備ツールキット**を展開します。 潜在的な互換性の問題の有無が確認されます。 たとえば、最新バージョンの Office で変更された関数をファイルが使用します。 Office 用準備ツールキットを実行して**最近このコンピューター上で使用された Office ドキュメントおよびインストールされたアドイン**に関するオプションを選択するか、コマンド ラインで `-mru` フラグを使用したら、Configuration Manager のハードウェア インベントリ エージェントによって結果を取得できるようになります。 この追加データにより、デバイスの準備状況の計算が強化されます。 詳細については、[Office 用準備ツールキットを使用した Office 365 ProPlus でのアプリケーションの互換性の評価](https://aka.ms/readinesstoolkit)に関する記事をご覧ください。

スキャンを実行するために、すべてのターゲット デバイスに準備ツール キットをインストールすることは必要ないので注意してください。 次のサンプル コマンド ライン オプションを使用すれば、必要な各デバイスをスキャンできます。  出力フラグは必須ですが、ダッシュボードでの結果の生成にファイルは使用されないので、任意の有効な場所を選択できます。

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

詳細については、「[社内の複数ユーザーから準備に関する情報を収集する](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise)」を参照してください。

## <a name="office-365-proplus-upgrade-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a> Office 365 ProPlus アップグレードの準備ダッシュボード

*(バージョン 1906 で導入)*

<!--4021125-->
Office 365 ProPlus にアップグレードする準備ができているデバイスを特定するために、バージョン 1906 以降では準備ダッシュボードが用意されています。 これには、Configuration Manager の Current Branch バージョン 1902 でリリースされた **[Office 365 ProPlus upgrade readiness]\(Office 365 ProPlus アップグレード準備\)** タイルが含まれています。 このダッシュボードの次の新しいタイルは、Office のアドインとマクロの準備評価に役立ちます。

- 展開
- デバイスの準備
- アドインの準備
- アドインのサポート声明
- バージョンの数による上位アドイン
- マクロがあるデバイスの数
- マクロの準備
- マクロのアドバイザリ

次のビデオは、以下に関する詳細情報を含む Ignite 2019 のセッションです。

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Configuration Manager での Office Readiness を使用した互換性評価および Microsoft Office 365 ProPlus のアップグレードのベストプラクティス](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>Office 365 ProPlus アップグレードの準備ダッシュボードの使用

[前提条件](#prerequisites)が満たされていることを確認したら、次の手順に従ってダッシュボードを使用します。
 
1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[Office 365 クライアント管理]** を展開します。
1. **[Office 365 ProPlus Upgrade Readiness]** ノードを選択します。
1. **[コレクション]** と **[Target Office Architecture]\(ターゲット Office アーキテクチャ)** を変更して、ダッシュボードでリレーされる情報を変更します。

![Office 365 ProPlus アップグレードの準備ダッシュボード](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Office 365 ProPlus アップグレードの準備ダッシュボード](./media/4021125-office-365-to-add-ins.png)

![Office 365 ProPlus アップグレードの準備ダッシュボード](./media/4021125-office-365-macro-advisories.png)

### <a name="device-readiness-information"></a>デバイスの準備情報

各デバイス上のアドインとマクロのインベントリが評価されると、次にその情報に従ってデバイスがグループ化されます。 状態が **[アップグレードの準備完了]** と表示されているデバイスには、互換性の問題はほとんどありません。

グラフの **[アップグレードの準備完了]** カテゴリを選択すると、限定コレクション内のデバイスに関する詳細が表示されます。 デバイスの一覧を確認し、ご自分のビジネス要件に応じて選択を行い、その選択を基に新しいデバイス コレクションを作成することができます。 新しいコレクションを使用して、Configuration Manager で Office 365 ProPlus を展開します。

互換性の問題が発生している可能性のあるデバイスは、 **[レビューが必要]** とマークされます。 これらのデバイスでは、Office 365 ProPlus にアップグレードする前に、アクションを実行することが必要な場合があります。 たとえば、重要なアドインをより新しいバージョンに更新します。

### <a name="add-in-information"></a>アドインの情報

 各デバイス上で、インストールされているすべてのアドインのインベントリが収集されます。 次に、このインベントリは、Office 365 ProPlus でのアドインのパフォーマンスに関して Microsoft が持っている情報と比較されます。 アップグレード後に問題を引き起こす可能性があるアドインが見つかった場合は、そのアドインを備えているすべてのデバイスにレビューのフラグが付けられます。

### <a name="macro-information"></a>マクロの情報

Configuration Manager では、各デバイスで最近使用されたファイルが参照されます。 このリストの中で、次の種類を含むマクロをサポートするファイルがカウントされます。

- マクロ対応の Office ファイル形式。
- 以前の Office 形式。これは、マクロのコンテンツがあるかどうかを示すものではありません。

このレポートを使用すると、マクロを含む可能性のあるファイルが最近どのデバイスで使用されたかを特定できます。 次に、Configuration Manager を使用して **Office 用準備ツール キット**を展開することで、より詳細な情報が必要なデバイスをスキャンし、互換性に関する潜在的な問題がないかどうかを確認することができます。 たとえば、より新しいバージョンの Office で変更された関数がファイルで使用されている場合が挙げられます。

スキャンを実行する方法の詳細については、「[詳細なマクロの準備状況](#bkmk_ort)」を参照してください。

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a> [Office 365 ProPlus Pilot と正常性] ダッシュボード
<!--4488272, 4488301-->
*(バージョン 1910 で導入)*

バージョン 1910 以降では、 **[Office 365 ProPlus Pilot と正常性] ダッシュボード**を使用すれば、Office 365 ProPlus 展開を容易に計画し、試作し、実施することができます。 このダッシュボードからは、Office 365 ProPlus がインストールされたデバイスの正常性に関する分析情報が提供され、展開計画に影響を与える可能性のある問題の特定に役立ちます。 **[Office 365 ProPlus Pilot と正常性] ダッシュボード**には、アドイン インベントリに基づくパイロット デバイスの推奨事項が表示されます。 ダッシュボードには、次のタイルがあります。

- パイロット生成
- 推奨されるパイロット デバイス
- パイロットの展開
- 正常性データを送信しているデバイス
- 正常性の目標を満たしていないデバイス
- 正常性の目標を満たしていないアドイン
- 正常性の目標を満たしていないマクロ

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>[Office 365 ProPlus Pilot と正常性] ダッシュボードを使用する

[前提条件](#prerequisites)が満たされていることを確認したら、次の手順に従ってダッシュボードを使用します。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[Office 365 クライアント管理]** を展開します。
1. **[Office 365 パイロットと正常性]** ノードを選択します。

![[Office 365 ProPlus Pilot と正常性] ダッシュボード](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>パイロット生成

ボタンをクリックして、限定コレクションからパイロットの推奨事項を生成します。 アクションが開始されるとすぐに、バックグラウンド タスクによってパイロット コレクションの計算が開始されます。 限定コレクションには、ProPlus 以外の Office バージョンを備えたデバイスが少なくとも 1 つ含まれている必要があります。

### <a name="recommended-pilot-devices"></a>推奨されるパイロット デバイス

**推奨されるパイロット デバイス**は、パイロットの生成時に使用した限定コレクションを通してインストール済みのすべてのアドインを表す、デバイスの最小セットです。 ドリルダウンして、これらのデバイスの一覧を取得します。 次に、詳細を使用して、必要に応じてパイロットからデバイスを除外します。 すべてのアドインが既に Office 365 ProPlus デバイスにインストールされている場合、それらのアドインがインストールされたデバイスは計算に含まれません。 これは、Office 365 ProPlus がインストールされているデバイス上のすべてのアドインが表示されているため、パイロット コレクションでは結果が得られない可能性があることも意味しています。

### <a name="deploy-pilot"></a>パイロットの展開

パイロット デバイスを受け入れたら、段階的展開ウィザードを使用して Office 365 Proplus をパイロット コレクションに展開します。 管理者は、展開を管理するために、ウィザードでパイロットと限定コレクションを定義できます。

### <a name="health-data"></a>正常性データ

Office 365 Proplus をインストールしたら、パイロット デバイスで正常性データを有効にします。 正常性データを使用すると、どのアドインとマクロが正常性の目標を満たしていないかを把握できます。 **[配置準備が完了したデバイス]** グラフでは、正常性の分析情報を使用して、展開の準備ができているパイロット以外のデバイスが識別されます。 **[正常性データを送信しているデバイス]** グラフでは、正常性データを送信しているデバイスの数が取得されます。

### <a name="devices-not-meeting-health-goals"></a>正常性の目標を満たしていないデバイス

このタイルは、アドイン、マクロ、またはその両方に関して問題があるデバイスをまとめたものです。

### <a name="add-ins-not-meeting-health-goals"></a>正常性の目標を満たしていないアドイン

- 読み込みの失敗:アドインを開始できませんでした。
- クラッシュ:実行中にアドインが失敗しました。
- エラー:アドインによってエラーが報告されました。
- 複数の問題:上記の問題のうち複数がアドインに該当します。

### <a name="macros-not-meeting-health-goals"></a>正常性の目標を満たしていないマクロ

- 読み込みの失敗:ドキュメントの読み込みに失敗しました。
- ランタイム エラー:マクロの実行中にエラーが発生しました。 このようなエラーは入力に依存する可能性があるため、常に発生するとは限りません。
- コンパイル エラー:マクロは正常にコンパイルされなかったため、実行は試みられません。
- 複数の問題:上記の問題のうち複数がマクロに該当します。

> [!NOTE]
> マクロ インベントリは、Office 向けの準備ツールキットおよび最近使用したデータ ファイルからのデータによって設定されます。 マクロの正常性は、正常性データによって設定されます。 マクロ インベントリが**スキャンされていない**場合は、さまざまなデータ ソースが原因で、マクロの正常性が **[レビューが必要]** な状態になる可能性があります。 <!--5922845-->

### <a name="known-issues"></a>既知の問題

**[パイロットの展開]** タイルには既知の問題があります。 現時点では、それをパイロットへの展開に使用することはできません。 この回避策は、段階的な展開ウィザードを使用してアプリケーションを展開するための既存のワークフローです。 <!--5525871-->

## <a name="next-steps"></a>次のステップ

[Configuration Manager での Office 365 ProPlus の管理](manage-office-365-proplus-updates.md)
