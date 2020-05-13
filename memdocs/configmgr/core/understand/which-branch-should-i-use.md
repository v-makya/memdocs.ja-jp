---
title: 適切なブランチを選択する
titleSuffix: Configuration Manager
description: Configuration Manager の使用可能な各ブランチの相違点について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 542069b82ea4c68a48ccc47b79007fd2fa25322a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906022"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>適切な Configuration Manager のブランチを選択する

*適用対象:Configuration Manager (Current Branch と Technical Preview Branch)、System Center Configuration Manager (Long-Term Servicing Branch)*

Configuration Manager の 3 つのブランチを使用できます。

- Current Branch
- Long Term Servicing Branch
- Technical Preview Branch

この記事は、適切なブランチを選択するのに役立ちます。

> [!TIP]  
> 階層内のすべてのサイトは同じブランチを実行する必要があります。 階層内でサイトがそれぞれ異なるブランチをもつことはサポートされません。

## <a name="current-branch"></a>Current Branch

このブランチは、運用環境での使用のためにライセンスされます。 最新の機能を利用するにはこのブランチを使用します。 次のいずれかのライセンスがある場合、このブランチを使用できます。  

- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- 同等のサブスクリプション権限  

ソフトウェア アシュアランスとライセンスのオプションの詳細については、「[Configuration Manager のライセンスとブランチ](learn-more-editions.md)」および「[Configuration Manager のブランチとライセンスに関してよく寄せられる質問](product-and-licensing-faq.md)」をご覧ください。

Microsoft は、Configuration Manager の Current Branch に対し、年に数回の更新プログラムのリリースを予定しています。 更新プログラムの各バージョンは、一般公開 (GA) リリース日から 18 か月間サポートされます。 この期間中、テクニカル サポートが提供されます。 ただし、弊社のサポート体制は、最新の Current Branch バージョンの利用状況に応じて 2 種類のサービス提供フェーズのいずれかが適用されるしくみに変わっています。 (詳細については、「[Configuration Manager の Current Branch バージョンのサポート](../servers/manage/current-branch-versions-supported.md)」をご覧ください。 新しいバージョンへの更新プログラムは、コンソール内の更新プログラムとして利用できます。

新しいサイトとして Current Branch をインストールするには、[構成基準メディア](../servers/manage/updates.md#bkmk_Baselines)を使います。 System Center 2012 Configuration Manager Service Pack 2 または System Center 2012 R2 Configuration Manager Service Pack 1 からアップグレードする場合も、構成基準メディアを使います。 このメディアへのアクセス方法は、組織の Configuration Manager のライセンス形態によって異なります。

この基準メディアを使用して、Current Branch の評価版の新しいサイトをインストールすることもできます。 評価版にはライセンスは不要です。 評価版は 180 日間使用できます。 Current Branch の製品版へのアップグレードをサポートします。 評価版のみをインストールするには、[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) から入手します。

> [!NOTE]
> 新しい Configuration Manager 階層のサイトをインストールするには、基準メディアを使用します。 基準バージョンをインストール済みの場合は、コンソール内の更新プログラムを使用して、サイトを新しいバージョンに更新します。  
>
> コンソール内の更新プログラムを使用して更新されたサイトは、基準メディアを使用してインストールされた新しいサイトと同一になります。
>
> 詳細については、[Configuration Manager の更新プログラム](../servers/manage/updates.md)に関するページをご覧ください。  

### <a name="features-of-the-current-branch"></a>Current Branch の機能

- 新機能を利用できるようにする[コンソール内の更新プログラム](../servers/manage/install-in-console-updates.md)を受信します。
- 既存の機能にセキュリティと品質に関する修正を適用するコンソール内の更新プログラムを受信します。
- 必要に応じてアウトオブバンドの更新プログラムをサポートします。 詳細については、「[更新登録ツールの使用](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)」または「[修正プログラム インストーラーの使用](../servers/manage/use-the-hotfix-installer-to-install-updates.md)」をご覧ください。
- クラウドベースのサービスと統合されます。
- 他の Configuration Manager インストール環境との間で[データの移行](../migration/migrate-data-between-hierarchies.md)をサポートします。
- 以前のバージョンの Configuration Manager からのアップグレードをサポートします。
- 評価版としてのインストールをサポートしており、後でフル ライセンスのインストールにアップグレードすることができます。

Microsoft では、最新バージョンがリリースされたら、すぐにそのリリースに更新することをお勧めします。 新しいバージョンに更新するまで、最大 18 か月間待つことができます。 ある更新プログラムをスキップして、その後に利用可能になる最新バージョンをインストールすることもできます。 各バージョンは累積的な内容となっており、ある更新プログラムをスキップしてから最新バージョンをインストールしても、以前のバージョン以降に追加されたすべての機能と改善点を利用できます。

詳細については、「[Current Branch バージョンのサポート](../servers/manage/current-branch-versions-supported.md)」をご覧ください。

### <a name="current-branch-update-options"></a>Current branch の更新オプション

- 有効なソフトウェア アシュアランスがある場合、Current Branch バージョンにコンソール内の更新プログラムをインストールできます。  
- Current Branch を Technical Preview Branch に変換するオプションはありません。 Technical Preview Branch は、ライセンスを必要としない個別のインストールです。
- Current Branch を Long-Term Servicing Branch (LTSB) に変換するオプションはありません。 Current Branch をアンインストールしてから、新規インストールとして LTSB をインストールする必要があります。

## <a name="long-term-servicing-branch"></a>Long Term Servicing Branch

このブランチは、運用環境で使用するためにライセンスされており、Current Branch を使用しており Configuration Manager ソフトウェア アシュアランス (SA) またはそれと同等のサブスクリプション権が 2016 年 10 月 1 日以降に失効することに同意した Configuration Manager ユーザーが対象となります。 ソフトウェア アシュアランスとライセンスのオプションの詳細については、「[Configuration Manager のライセンスとブランチ](learn-more-editions.md)」および「[Configuration Manager のブランチとライセンスに関してよく寄せられる質問](product-and-licensing-faq.md)」をご覧ください。

LTSB はバージョン 1606 に基づいています。 このブランチは、新機能の提供や既存の機能の更新を行うコンソール内の更新プログラムを受信しません。 ただし、重要なセキュリティ修正プログラムは提供されます。 LTSB をインストールするには、System Center 2016 で入手したバージョン 1606 の [基準メディア](../servers/manage/updates.md#bkmk_Baselines)を使用する必要があります。 それより新しい基準バージョンでは、LTSB のインストールはサポートされません。

新しいサイトとして、またはサポートされる System Center 2012 Configuration Manager サイトからのアップグレードとして、LTSB をインストールするには、System Center 2016 で入手するバージョン 1606 の[基準メディア](../servers/manage/updates.md#bkmk_Baselines)を使用します。 基準メディアを使用して、Current Branch のバージョン 1606 を実行する新しいサイトをインストールするか、Long-Term Servicing Branch を実行する新しいサイトをインストールすることができます。

> [!TIP]  
> System Center 2016 の詳細については、[System Center 2016 のドキュメント](https://docs.microsoft.com/system-center/index)をご覧ください。 このドキュメントでは、System Center 2016 の入手方法についても説明しています。この製品を入手するには、Microsoft ライセンス契約または同様の権利が必要です。  
>  
> ボリューム ライセンス サービス センター (VLSC) で Configuration Manager バージョン 1606 を見つけるには、[VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) の **[Downloads and Keys]\(ダウンロードとキー\)** タブに移動し、`System Center 2016` を検索して、**System Center 2016 Datacenter** または **System Center 2016 Standard** を選択します。  
>  
> System Center 2016 の評価版は、[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview) から入手することもできます。  

### <a name="features-of-the-ltsb"></a>LTSB の機能

- 重要なセキュリティ修正プログラムを提供するコンソール内の更新プログラムを受信します。
- Configuration Manager の SA 契約または同等の権利が期限切れになったときにインストール オプションを提供します。
- Configuration Manager の有効な SA 契約または同等の権利を保有している場合は、Current Branch へのアップグレード (変換) をサポートします。

### <a name="ltsb-limitations"></a>LTSB の制限事項

LTSB は Current Branch のバージョン 1606 をベースにしており、次の制限があります。

- LTSB は、一般公開 (2016 年 10 月) 後の 10 年間、重要なセキュリティ更新プログラムのサポート対象となり、その後、このブランチのサポートは失効します。 サポート ライフサイクルの詳細については、「[Microsoft ライフサイクル ポリシー](https://support.microsoft.com/lifecycle)」をご覧ください。
- サーバーおよびクライアントのオペレーティング システムと SQL Server バージョンのような関連テクノロジの限定されたセットのリストをサポートしています。 詳細については、[Long-Term Servicing Branch のサポートされている構成](supported-configurations-for-ltsb.md)に関する記事をご覧ください。
- 新しい機能の更新プログラムを受信しません。
- 以下の機能はサポートされていません。
  - 共同管理や Desktop Analytics などのクラウドに接続された機能
  - オンプレミス MDM
  - Windows 10 サービス ダッシュボード、サービス プラン、または Windows 10 半期チャネル
  - Windows 10 LTSB および Windows Server の今後のリリース
  - 資産インテリジェンス
  - すべてのプレリリース機能

### <a name="ltsb-update-options"></a>LTSB の更新オプション

- LTSB インストールは、Current Branch インストールに変換できます。 Current Branch への変換は、LTSB のサポートが終了する前または後にかかわらずサポートされます。

  変換には、Microsoft との有効なソフトウェア アシュアランス契約が必要です。 詳細については、以下の記事を参照してください。

  - [Long-Term Servicing Branch の Current Branch へのアップグレード](convert-to-current-branch.md)
  - [Configuration Manager のライセンスとブランチ](learn-more-editions.md)
  - [基準バージョンと更新プログラムのバージョン](../servers/manage/updates.md#bkmk_Baselines)

- LTSB を Technical Preview Branch に変換するオプションはありません。 Technical Preview Branch は、ライセンスを必要としない個別のインストールです。

- Current Branch の評価版を LTSB インストールにアップグレードすることはできません。

## <a name="technical-preview-branch"></a>Technical Preview Branch

Technical Preview Branch は、ラボ環境での使用を意図しています。 Configuration Manager 用に開発されている最新機能を学習して試すためのものです。 運用環境ではサポートされないため、ソフトウェア アシュアランス ライセンス契約は必要ありません。

Technical Preview Branch を実行する新しいサイトをインストールするには、最新の [Technical Preview Branch 用基準メディア](../get-started/technical-preview.md#bkmk_install)を使います。 Technical Preview Branch をインストールすると、毎月新しいバージョンがコンソール内の更新プログラムとして利用できます。

### <a name="features-of-the-technical-preview-branch"></a>Technical Preview Branch の機能

- Current Branch の最近の基準バージョンに基づいています。
- インストールを Technical Preview Branch の最新バージョンに更新するコンソール内の更新プログラムを受信します。
- Microsoft がフィードバックを希望する、開発中の新機能が含まれています。
- Technical Preview Branch にのみ適用される更新プログラムを受信します。

### <a name="technical-preview-limitations"></a>Technical Preview の制限事項

- [サポートは限定的](../get-started/technical-preview.md#bkmk_reqs)です (単一のプライマリ サイトと最大 10 クライアントのみをサポートするなど)。  
- Current Branch または LTSB インストールにアップグレードまたは移行することはできません。
- 以下の動作はサポートされていません。
  - 移行機能を使用して、別の Configuration Manager インストールとの間でデータをインポートまたはエクスポートすること
  - 以前のバージョンの Configuration Manager からのアップグレード
  - 評価版としてのインストール

Technical Preview Branch に最初に導入された機能は、多くの場合、以降の更新プログラムで Current Branch に追加されます。 それぞれの新しい Technical Preview Branch バージョンには、以前の Technical Preview Branch の機能が Current Branch に追加された後も、それらの機能が引き続き含まれます。

詳細については、「[Configuration Manager の Technical Preview](../get-started/technical-preview.md)」をご覧ください。

### <a name="technical-preview-update-options"></a>Technical Preview の更新オプション

- 新しい Technical Preview Branch バージョン向けのコンソール内の更新プログラムをインストールできます。

- Technical Preview Branch を Current Branch または LTSB に変換するオプションはありません。

## <a name="identify-your-version-and-branch"></a>使っているバージョンとブランチを識別する

### <a name="version"></a>バージョン

お使いのサイトのバージョンを確認するには、コンソールの左上にある **[Configuration Manager のバージョン情報]** に移動します。 このダイアログには、 **[サイトのバージョン]** が表示されます。 サイトのバージョンの一覧については、「[基準バージョンと更新プログラムのバージョン](../servers/manage/updates.md#bkmk_Baselines)」をご覧ください。

### <a name="branch"></a>ブランチ

サイトのブランチを確認するには、コンソールで **[管理]**  >  **[サイトの構成]**  >  **[サイト]** を選択し、 **[階層設定]** を開きます。 Current Branch に変換するためのアクティブなオプションがある場合、サイトでは LTSB バージョンが実行されています。 サイトで Current Branch が実行されている場合、コンソールでこのオプションは無効にされています。

Configuration Manager のさまざまなバージョンについては、「[基準バージョンと更新プログラムのバージョン](../servers/manage/updates.md#bkmk_Baselines)」をご覧ください。
