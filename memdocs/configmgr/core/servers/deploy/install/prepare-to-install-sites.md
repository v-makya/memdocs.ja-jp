---
title: サイトのインストールの準備
titleSuffix: Configuration Manager
description: 複数の Configuration Manager サイトをインストールする予定がある場合は、時間を節約し、エラーを防ぐため、次の情報を参照してください。
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700720"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Configuration Manager サイトのインストールを準備する

*適用対象:Configuration Manager (Current Branch)*

1 つ以上の Configuration Manager サイトの適切な展開を準備するには、この記事の詳細を理解してください。 次の手順で、複数のサイトのインストールの時間を節約し、1 つ以上のサイトの再インストールが必要になるような失敗を防ぎます。

> [!TIP]
> Configuration Manager のサイトと階層のインフラストラクチャの管理において、"*アップグレード*"、"*更新*"、"*インストール*" という用語は、3 つの異なる概念を説明するために使用されます。 各用語の使用方法については、「[サイトと階層のインフラストラクチャでのアップグレード、更新、およびインストールについて](../../../understand/upgrade-update-install.md)」を参照してください。

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> 異なる種類のサイトをインストールするためのオプション
新しい Configuration Manager サイトをインストールする場合、使用可能なソース ファイルのバージョンは、既に階層内にあるサイトのバージョン (存在する場合) に依存します。 使用可能なインストール方法はインストールするサイトの種類に依存します。  

サイトをインストールする前に、階層を計画していることを確認し、インストールするサイトの種類を理解してください。 詳細については、「[Design a hierarchy of sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)」(サイトの階層の設計) を参照してください。


### <a name="first-site"></a>最初のサイト
階層にインストールするこの最初のサイトは、スタンドアロンのプライマリ サイトまたは中央管理サイトのいずれかです。

**インストール メディア**:中央管理サイトまたはスタンドアロンのプライマリ サイトを新しい階層で最初のサイトとしてインストールするには、Configuration Manager の[基準バージョンを使用する](../../../../core/servers/manage/updates.md#bkmk_Baselines)必要があります。 サイトの [CD.Latest フォルダー](../../../../core/servers/manage/the-cd.latest-folder.md)から更新されたソース ファイルを使用して、新しい階層の最初のサイトをインストールしないでください。

**インストール方法**:[Configuration Manager のセットアップ ウィザード](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)を使用していずれかの種類のサイトをインストールするか、[スクリプトを使用してコマンドラインからインストール](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)するために使用するスクリプトを構成することができます。


### <a name="additional-sites"></a>追加のサイト
最初のサイトをインストールした後、いつでもサイトを追加することができます。 サイトを追加するには次のオプションがあります ([サポートされている制限](../../../../core/plan-design/configs/size-and-scale-numbers.md)以内)。

|既存のサイト|インストール可能な追加サイトの種類|
|---|---|
|中央管理サイト|子プライマリ サイト|
|子プライマリ サイト|セカンダリ サイト|
|スタンドアロン プライマリ サイト|セカンダリ サイト (プライマリ サイトを拡張でき、それにより、スタンドアロン プライマリ サイトが子プライマリ サイトに変換されます)|

**インストール メディア**:中央管理サイトをスタンドアロン プライマリ サイトにインストールして拡張する場合、または新しい子プライマリ サイトを既存の階層にインストールする場合は、既存のサイトのバージョンに対応するインストール メディア (ソース ファイルを格納する) を使用する必要があります。

> [!IMPORTANT]
> コンソール内の更新プログラムをインストールした結果、以前にインストールしたサイトのバージョンが変更された場合は、元のインストール メディアを使用しないでください。 代わりに、そのシナリオでは、更新されたサイトの [CD.Latest フォルダー](../../../../core/servers/manage/the-cd.latest-folder.md)にあるソース ファイルを使用してください。 Configuration Manager では、新しいサイトが接続する既存のサイトのバージョンに対応したソース ファイルを使用する必要があります。

セカンダリ サイトは、Configuration Manager コンソールからインストールする必要があります。 このように、セカンダリ サイトは常に親プライマリ サイトのソース ファイルを使用してインストールします。

**インストール方法**:追加のサイトのインストールに使用する方法は、インストールするサイトの種類によって異なります。
- **中央管理サイトを追加する**:Configuration Manager のセットアップ ウィザードまたはスクリプト化されたコマンド ラインを使用すると、既存のスタンドアロン プライマリ サイトに親サイトとして新しい中央管理サイトをインストールすることができます。 詳細については、「[スタンドアロン プライマリ サイトを拡張する](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)」を参照してください。
- **子プライマリ サイトを追加する**:Configuration Manager のセットアップ ウィザードまたはコマンド ライン インストールを使用すると、中央管理サイトの下に子プライマリ サイトを追加することができます。
- **セカンダリ サイトを追加する**:Configuration Manager コンソールを使用して、プライマリ サイトの下に子サイトとしてセカンダリ サイトをインストールします。 セカンダリ サイトの追加では、その他の方法はサポートされていません。

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a> インストールを開始する前に完了する一般的なタスク
- **展開に使用する階層トポロジを把握します**    
詳細については、「[Configuration Manager のサイト階層の設計](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)」を参照してください。  

- **Configuration Manager で使用するための前提条件とサポートされる構成を満たす個別のサーバーを準備および構成します**         
詳細については、「[サイトとサイト システムの前提条件](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md)」をご覧ください。  

- **サイト データベースをホストするように SQL Server をインストールして構成します**     
詳細については、「[Configuration Manager の SQL Server バージョンのサポート](../../../../core/plan-design/configs/support-for-sql-server-versions.md)」をご覧ください。  

- **Configuration Manager をサポートするネットワーク環境を準備します**      
詳細については、「[System Center Configuration Manager のファイアウォール、ポート、ドメインの設定](../../../../core/plan-design/network/configure-firewalls-ports-domains.md)」を参照してください。  

- **公開キー基盤 (PKI) を使用する場合は、インフラストラクチャと証明書を準備します**      
詳細については、「[Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。

- **サイト サーバーまたはサイト システム サーバーとして使用するコンピューターに最新のセキュリティ更新プログラムをインストールし、必要な場合はそれらを再起動します**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>  サイト名とサイト コードについて
サイト コードとサイト名は、Configuration Manager 階層内でサイトを識別および管理するために使用します。 Configuration Manager コンソールには、サイト コードとサイト名が、&lt;*サイト コード*\> - &lt;*サイト名*\>の形式で表示されます。 階層にあるサイトごとに固有なサイト コードが付いている必要があります。 Active Directory スキーマが Configuration Manager 用に拡張されており、サイトがデータを発行する場合は、Active Directory フォレスト内で使用するサイト コードは、必ず固有でなければなりません。サイトが Configuration Manager の別の階層や以前の Configuration Manager のインストールで使用されていても、同じサイト コードを付けることはできません。 階層を展開する前に、どのようなサイト コードとサイト名を使用するかを、十分検討してください。

### <a name="specify-a-site-code-and-site-name"></a>サイト コードとサイト名の指定
Configuration Manager セットアップの実行時に、インストールする中央管理サイト、プライマリ サイト、セカンダリ サイトのサイト コードとサイト名を指定する必要があります。 サイト コードは、階層にある各サイトを識別できる固有のコードでなければなりません。 サイト コードはフォルダー名の一部になるので、次の名前 ( Configuration Manager や Windows で予約されている名前など) をサイト コードに使用しないでください。
- AUX
- CON
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Configuration Manager セットアップでは、サイト コードが既に使用されていないかどうかは検証されません。

Configuration Manager のセットアップの実行中にサイトのサイト コードを指定するときは、必ず 3 文字の英数字を入力してください。 サイト コードでは、文字 *A* から *Z* および数字 *0* から *9* のみを任意の組み合わせで使用できます。 文字や数字の順序は、サイト間の通信には影響しません。 たとえば、プライマリ サイトに *ABC*、セカンダリ サイトに *DEF* という名前を付ける必要はありません。

サイト名とは、サイトを識別するわかりやすい名前のことです。 サイト名には、*A* から *Z*、*a* から *z*、*0* から *9*、およびハイフン ( *-* ) だけを使用できます。

> [!IMPORTANT]
> サイトをインストールした後のサイト コードまたはサイト名の変更はサポートされていません。

### <a name="reuse-a-site-code"></a>サイト コードの再利用
Configuration Manager 階層内で中央管理サイトまたはプライマリ サイトにサイト コードを複数回使用することはできません。元のサイトとサイト コードがアンインストールされた場合でも同じです。 サイト コードを再利用すると、オブジェクト ID が階層で競合する危険があります。 セカンダリ サイトやサイト コードを Configuration Manager の階層や Active Directory フォレストで使用しなくなった場合は、そのセカンダリ サイトのサイト コードを再利用することができます。

## <a name="limits-and-restrictions-for-installed-sites"></a>インストール後のサイトの制限と制約
サイトをインストールする前に、サイトとサイトの階層に適用される次の制限事項を理解することが重要です。
- セットアップの実行後は、サイトをアンインストールしてから新しい値を使用して再インストールしない限り、次のサイトのプロパティを変更することはできません。  
  - プログラム ファイルのインストール ディレクトリ  
  - サイト コード  
  - サイトの説明  
- 階層に中央管理サイトが含まれている場合:  
  - Configuration Manager では、階層から子プライマリ サイトを移動して、スタンドアロン プライマリ サイトを作成したり異なる階層に接続したりすることはできません。 代わりに、子プライマリ サイトをアンインストールし、新しいスタンドアロンのプライマリ サイトまたは別の階層の中央管理サイトの子サイトとして再インストールします。  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a> セットアップを実行する前のオプションの手順
**セットアップ ダウンローダーを[手動で実行する](../../../../core/servers/deploy/install/setup-downloader.md)**

Configuration Manager の更新されたセットアップ ファイルをダウンロードするために、セットアップ ダウンローダーを実行することができます。 セットアップを実行するコンピューターがインターネットに接続されていない場合、または複数のサイト サーバーをインストールする場合は、セットアップ ダウンローダーを使用して、セットアップに必要な更新プログラムをダウンロードすることをご検討ください。 追加情報を次に示します。
- 既定では、セットアップはインターネットに接続して、更新されたセットアップ ファイルをダウンロードします。
- 既定では、Redist フォルダーにファイルが格納されます。
- 以前にこれらのファイルのコピーを格納したネットワーク上の場所を指定できます。

**前提条件チェッカー[を手動で実行する](../../../../core/servers/deploy/install/prerequisite-checker.md)**

問題を特定して修正するために、セットアップを実行してサイトをインストールする前、およびサーバーにサイト システムの役割をインストールする前に、前提条件チェッカーを実行できます。 前提条件チェッカーにより、コンピューターがサイトまたはサイト システムの役割をホストするための要件を満たしていることを確認できます。 追加情報を次に示します。
- 既定では、セットアップは前提条件チェッカーを実行します。
- エラーが発生した場合は、問題が解決するまでセットアップは停止します。

**オプションのポートを特定する**

サイト システムとクライアントが使用するオプションのポートを特定できます。 追加情報を次に示します。
- 既定では、サイト システムとクライアントは通信に定義済みのポートを使用します。
- セットアップ時に、代替ポートを構成することができます。

詳細については、「[使用されるポート](../../../../core/plan-design/hierarchy/ports.md)」を参照してください。
