---
title: UUP プレビュー
titleSuffix: Configuration Manager
description: UUP 統合のプレビューについての説明
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c37fab775cdb90667ff1bc9f77dbbcaa1864b6f0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696788"
---
# <a name="uup-private-preview-instructions"></a>UUP プライベート プレビューの説明

> [!Note]  
> この情報は、製品版のリリース前に大幅に変更される可能性があるプレビュー機能に関連します。 Microsoft は、ここで提供される情報に関して、明示または黙示を問わず、いかなる保証も行いません。  

## <a name="introduction"></a>概要

統合更新プラットフォーム (UUP) は、コンシューマー デバイスおよびエンタープライズ デバイスが Windows Update for Business から更新プログラムを受信するために使用するパッケージ化および発行プラットフォームです。 UUP プライベート プレビュー プログラムは、Microsoft が Configuration Manager で UUP 更新プログラムの使用を検証することに同意したお客様を対象としており、現在、お客様から報告されている Windows サービスに関する問題を解決するのに役立ちます。 これらの更新プログラムは、現在公開されていません。

UUP に関する詳細については、Windows ブログ投稿の「[統合更新プラットフォーム (UUP) の更新](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/)」を参照してください。

## <a name="benefits"></a>利点

Windows 10 の UUP 機能更新プログラムと累積的更新プログラムは、現在、お客様から報告されている Windows サービスに関する複数の問題を解決するのに役立ちます。

### <a name="feature-updates"></a>機能更新プログラム

- Windows Update プロセスは、UUP 機能更新プログラムを使用して、オンデマンド機能 (FOD) と言語パックを保持します。

- 最新のセキュリティ準拠レベルに直接更新します。 機能更新プログラムの直後にセキュリティ更新プログラムをインストールする必要はありません。 Microsoft は、最新の累積的セキュリティ更新プログラムを収めた新しい機能更新プログラムを毎月公開しています。 機能更新プログラムのほとんどのコンテンツは毎月ダウンロードまたは配布する必要はありません。 セキュリティ更新プログラムをダウンロードするだけで、累積的更新プログラムと共有されます。

### <a name="cumulative-updates"></a>累積的更新プログラム

- UUP での累積的更新プログラムには、毎月の累積的なセキュリティ更新プログラムと共に、サービス スタックの更新プログラム (SSU) が含まれます。 この動作によって、これら 2 つの更新プログラムの調整に伴う問題が解決されます。 累積的更新プログラムをインストールするために、サービス スタックの更新プログラムが適用されていることが確認されます。 これらの関係を管理および調整する必要はありません。

- UUP での累積的更新プログラムを使用すると、FOD および言語パックのコンテンツをオフラインで配布できます。 この動作により、ユーザーはオンデマンドで追加することができます。 ユーザーはインターネットからダウンロードする必要がなく、このコンテンツを事前設定する方法を判断する必要はありません。

## <a name="set-up"></a>設定

### <a name="1-send-your-wsus-id-to-microsoft"></a>1.Microsoft への WSUS ID の送信

UUP プライベート プレビューに参加するには、お使いの WSUS ID を UUP プレビューの連絡先と共有します。 Microsoft は、お使いの WSUS 環境の UUP プレビュー プログラムへの参加を承認します。 この ID がないと、プレビューが公開されるまで、UUP の更新プログラムを表示することはできません。

WSUS ID を取得するには、次の PowerShell スクリプトを実行します。

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

**MUUrl** プロパティは `https://sws.update.microsoft.com` である必要があります。 これを変更する場合は、サポート記事の「[WSUS synchronization fails with SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)」 (WSUS の同期が SoapException で失敗する) の解決方法を参照してください。

### <a name="2-update-configuration-manager"></a>2.Configuration Manager の更新

Configuration Manager サイトに以下の変更を加えて、この UUP プレビューをサポートします。

#### <a name="diagnostics-and-usage-data-level"></a>診断結果と使用状況データのレベル

このプレビュー期間中に、Configuration Manager の診断結果とデータの使用状況のレベルを上げることを検討します。 **フル**  レベルは、Microsoft でこの新機能に関する問題をより適切に分析し、トラブルシューティングするのに役立ちます。 詳細については、「[バージョン 1906 での診断の使用状況データ収集のレベル](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md)」を参照してください。

#### <a name="install-the-latest-update"></a>最新の更新プログラムをインストールする

1. 次のいずれかの更新プログラムを使用してサイトを更新します。

    - バージョン 1902 と[更新プログラムのロールアップ](https://support.microsoft.com/help/4500571)
    - [バージョン 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    詳細については、[コンソール内の更新プログラムのインストール](../../core/servers/manage/install-in-console-updates.md)に関するページを参照してください。

2. クライアントを更新します。  

    - このプロセスを簡単にするには、自動クライアント アップグレードの使用を検討します。 詳細については、「[クライアントをアップグレードする](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)」をご覧ください。  

    - クライアントに対して、使用されないコンテンツに関する*約 6 GB の不要なダウンロード*が実行されないようにするには、UUP 更新プログラムの対象であるすべてのクライアントをアップグレードします。

### <a name="3-update-windows-clients-to-a-supported-version"></a>3.サポートされているバージョンに Windows クライアントを更新します

UUP 更新プログラムを正常にインストールするには、次の更新プログラムの両方をインストールします。

1. 月単位の最小累積的準拠レベル。

2. Microsoft Update カタログの、累積的以外かつセキュリティ以外の特定の更新プログラム。 展開のために Configuration Manager 内に更新プログラムをインポートするには、「[Microsoft Update カタログから更新プログラムをインポートする](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog)」をご覧ください。

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>サポートされている Windows 10 のバージョンと必要な更新プログラム

| Windows 10 バージョン | 最小準拠レベル | 追加のカタログ更新 |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10 バージョン1903** | RTM | 2019 年 11 月 7 日、[KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10 バージョン 1809** | 2019 年 8 月、[KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 2019 年 11 月 7 日、[KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10 バージョン 1803** | 2019 年 4 月、[KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 2019 年 11 月 7 日、[KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10 バージョン 1709** | 2019 年 4 月、[KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 2019 年 11 月 7 日、[KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - 2019 年 11 月 7 日の追加のカタログ更新を適用する前に、クライアントに 2019 年 11 月 12 日の更新プログラムを適用すると、UUP をサポートするために必要な Windows 更新エージェントの変更が上書きされます。 このシナリオでクライアントを修復するには、2019 年 11 月 12 日の更新プログラムがインストールされた後に、追加のカタログ更新を適用します。
> - 機能更新プログラムをクライアントに適用する場合は、アップグレードの完了後に追加のカタログ更新を再インストールする必要があります。
> - 機能更新プログラムを簡単にテストできるようにするには、Configuration Manager に更新プログラムをインポートします。 詳細については、「[Microsoft Update カタログから更新プログラムをインポートする](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog)」を参照してください。 機能更新プログラムが完了すると、追加のカタログ更新が**必要**と表示されます。これにより、上位レベルの OS バージョンへの自動展開が可能になります。

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4.使用可能な場合、クライアントが差分コンテンツをダウンロードできるようにする

UUP 更新プログラムが正しくダウンロードされるようにするには、クライアント設定 **[使用可能な場合、クライアントが差分コンテンツをダウンロードできるようにする]** を有効にします。 この設定により、Configuration Manager で、Windows 更新エージェント (WUA) がクライアントにダウンロードする必要があるコンテンツを決定できるようになります。 この動作は、Configuration Manager クライアントが、UUP 更新プログラムに関連付けられているすべてのコンテンツをダウンロードする既定の動作ではありません。 この設定を有効にすると、各 UUP 更新プログラムに必要な追加のコンテンツが WUA によって決定されます。 たとえば、必須の FOD と言語パックだけなどです。

この設定を有効にした場合、インターネットからのサーバー コンテンツのダウンロードには影響しません。 クライアントのダウンロードにのみ適用されます。 クライアントに UUP 更新プログラムを展開する前に、UUP がサポートされているバージョンに適合するクライアントにこの設定を適用します。 前提条件のクライアント更新プログラムによって、WSUS および Configuration Manager での UUP 更新プログラムの互換性の問題が修正されます。

このクライアント設定について詳しくは、[クライアント設定について - ソフトウェア更新プログラム](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)に関するページをご覧ください

### <a name="5-review-your-software-update-infrastructure"></a>5.ソフトウェア更新プログラムのインフラストラクチャを確認する

UUP 更新プログラムを同期する前に、自動展開規則 (ADR) とサービス プランを確認してください。 これらの更新プログラムが自動的に展開されないようにするには、ADR を修正してフィルターで除外します。詳細については、「[同期されている UUP を検索する方法](#how-to-find-synced-uup-updates)」を参照してください。 既定では、既存のサービス プランでは UUP 以外の更新プログラムのみが展開されます。 サービス プランを変更して、この動作を変更することができます。

コンプライアンス レポートを確認し、必要に応じて変更します。 たとえば、すべての製品に対してコンプライアンスを測定すると、UUP の累積的更新プログラムと UUP 以外の累積的更新プログラムの両方が表示されるようになります。 デバイスは、両方の種類の更新プログラムに対してコンプライアンスをレポートします。 コンプライアンス レポートがこの変更に対応していることを確認します。

## <a name="enable-uup-and-start-testing"></a>UUP を有効にしてテストを開始する

### <a name="select-products-and-classifications-to-sync"></a>同期する製品と分類を選択する

UUP 更新プログラムの同期を開始する準備ができ、Microsoft が WSUS ID を承認したら、次のように新しい製品を有効にします。

1. [ソフトウェア更新プログラムを同期](../get-started/synchronize-software-updates.md)して、新しい製品を設定します。  

2. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。

3. 最上位サイトを選択します。これは、中央管理サイト (CAS)、スタンドアロンのプライマリ サイトのどちらかです。

4. リボンの **[サイト コンポーネントの構成]** を選択し、 **[ソフトウェアの更新ポイント]** を選択します。

5. **[製品]** タブに切り替えて、次の製品の 1 つまたは複数を選択します。 

    - **Windows 10 UUP プレビュー**
    - **Windows Server UUP プレビュー**

6. **[分類]** タブに切り替えて、次のオプションを選択します。  

    - **セキュリティ更新プログラム:** UUP の累積的更新プログラムを表示するには  
    - **アップグレード**:UUP の機能更新プログラムを表示するには  

7. ソフトウェア更新プログラムをもう一度同期して、新しい UUP 更新プログラムを表示します。

### <a name="how-to-find-synced-uup-updates"></a>同期されている UUP を検索する方法

UUP 更新プログラムを環境に同期したら、テストのために Configuration Manager コンソールでそれらを検索します。 プレビュー更新プログラムを見つけるには 2 つの方法があります。

- これらのプレビュー更新プログラムは別の製品なので、これらの更新プログラムを検索するには、製品を使用してフィルター処理します。 サービス プランの製品フィルターを使用して、UUP または UUP 以外の機能更新プログラムを展開します。  

- **[ソフトウェア ライブラリ]** の **[すべてのソフトウェア更新プログラム]** ノードと **[すべての Windows 10 更新プログラム]** ノード内に、新しいオプションの列 **[タグ]** があります。 このプロパティは、ADR でフィルターとして使用することもできます。 UUP 更新プログラムの場合は、このフィールドで `UUP` を検索します。 UUP 以外の更新プログラムの場合は空白です。  

### <a name="updates-available-during-preview"></a>プレビュー期間中に使用可能な更新プログラム

Microsoft によってリリースされたすべての Windows 10 更新プログラムの詳細については、「[Windows 10 のリリース情報](/windows/release-information/)」を参照してください。

#### <a name="cumulative-updates-to-test"></a>テストする累積的更新プログラム

複数の UUP タグ付き更新プログラムが利用可能になっている可能性がありますが、**2019 年 9 月** (2019-09) の更新プログラム以降のバージョンから開始してください。 次に例を示します。

- 2019-09 x64 ベース システム用 Windows 10 Version 1809 の累積更新プログラム (KB4512578)
- 2019-09 x64 ベース システム用 Windows 10 Version 1803 の累積更新プログラム (KB4516058)
- 2019-09 x64 ベース システム用 Windows 10 Version 1709 の累積更新プログラム (KB4516066)

#### <a name="feature-updates-to-test"></a>テストする機能更新プログラム

複数の UUP タグ付き更新プログラムが利用可能になっている可能性がありますが、**2019 年 9 月** (2019-09B) の更新プログラム以降のバージョンから開始してください。 次に例を示します。

- Windows 10 バージョン 1809 x64 2019-09B への機能更新プログラム
- Windows 10 バージョン 1803 x64 2019-09B への機能更新プログラム

## <a name="scenarios-to-test"></a>テストするシナリオ

### <a name="test-feature-updates"></a>機能更新プログラムのテスト

- 選択したセキュリティ準拠レベルへの直接更新  

- 更新プログラムの前に、FOD および言語パックをインストールします。 更新プログラムによってこれらのコンポーネントが保持されていることを確認します。  

### <a name="test-cumulative-updates"></a>累積的更新プログラムのテスト

プレビュー期間中は、複数の連続する更新プログラムに対して UUP 型の更新プログラムを使用してクライアントの準拠を維持します。 このテストは、実行中の動作を理解するのに役立ちます。

### <a name="test-content"></a>コンテンツのテスト

各メジャー バージョン (1809、1803、1709)、アーキテクチャ、言語の組み合わせの最初の更新プログラムは、サイズが大きくなっているように見えます。 このサイズは、以前の UUP 以外の更新プログラムのサイズと比較して、ファイルの数とディスク領域の両方で大きくなっています。 この余分なコンテンツは、主に累積的更新プログラムに対するすべての FOD と言語パックによるものです。 機能更新プログラムの場合は、その最初の更新プログラムに対して追加の大きなコンテンツがあります。

将来の累積的更新プログラムおよび機能更新プログラムでは、サイトがダウンロードおよび配布する新しいコンテンツの量が大幅に少なくなります。 UUP は、更新プログラムの間ですべての FOD と言語パックのコンテンツをインテリジェントに共有します。 この共有コンテンツを再ダウンロードしたり、再配布したりする必要はありません。 プレビュー期間中の Windows 10 バージョン 1709 と 1803 では、この月単位のダウンロードのサイズは、非 UUP のシナリオでの累積的更新プログラムのサイズとほぼ同じになります。 Windows 10 バージョン 1809 以降では、累積的更新プログラムの増分ダウンロードは月ごとに大幅に小さくなります。

*非高速*に対して 12 か月の期間にわたってダウンロードおよび配布されたコンテンツの合計を確認すると、UUP を使用しない Windows 10 バージョン 1803 は、UUP を使用したバージョン 1809 とほぼ同じになります。 リリースの有効期間全体にわたってダウンロードおよび配布されるコンテンツの合計は、UUP を使用したバージョン 1809 の方が小さくなります。

### <a name="supported-content-channels"></a>サポートされているコンテンツ チャネル

プレビューでは、典型的な実際のシナリオをテストします。 UUP では、以下のすべてのコンテンツ チャネルがサポートされます。

- Windows 配信の最適化 (DO)
  - DO を使用する場合は、適切に構成されていることを確認します。 詳しくは、「[Windows 10 更新プログラムの配信の最適化](optimize-windows-10-update-delivery.md)」をご覧ください。
- Configuration Manager のピア キャッシュ
- Windows BranchCache
- **[展開パッケージなし]** オプションを使用します。クライアントは Microsoft Update から直接ダウンロードします。 配信の最適化には、このオプションを使用します。
- サード パーティの代替コンテンツ プロバイダー

コンテンツ チャネルの詳細については、[Windows 10 更新プログラムの配信の最適化](optimize-windows-10-update-delivery.md)に関するページをご覧ください。

<!-- TODO: Addlink to WSUS Perf documentation-->