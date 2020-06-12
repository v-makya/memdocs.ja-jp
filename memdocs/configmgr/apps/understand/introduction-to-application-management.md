---
title: アプリ管理の概要
titleSuffix: Configuration Manager
description: Configuration Manager でアプリケーションを管理および展開するために必要となる基本的な情報について説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b2fc0dfe37ad51ce1a549545c3eaa716395438d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347111"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Configuration Manager でのアプリケーション管理の概要

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager アプリケーションで作業を開始する前に基礎を学習します。  

> [!TIP]  
> Configuration Manager でアプリケーションを管理する方法を既に理解している場合は、この記事をスキップします。 サンプル アプリケーション:[アプリケーションの作成と展開](../get-started/create-and-deploy-an-application.md)の作成に進みます。  

## <a name="what-is-an-application"></a>アプリケーションとは

*アプリケーション*または*アプリ*は、広く使用されているコンピューター用語ですが、Configuration Manager では固有の意味があります。 アプリケーションを 1 つの箱だと考えてみてください。 この箱には、ソフトウェア パッケージ (*展開の種類*と呼ばれる) のインストール ファイルが 1 つ以上入っており、さらにソフトウェアの展開方法に関する指示が付属しています。  

アプリケーションをデバイスに展開すると、Configuration Manager がデバイスにインストールする展開の種類が**要件**に応じて決まります。  

アプリケーションを使ってさらに多くの操作を行うことができます。 このガイドを読むと、これらの操作について学習できます。 以下のセクションに、あらかじめ理解しておく必要があるいくつかの概念を示します。  

### <a name="deployment-type"></a>展開の種類

"*アプリケーション*" がボックスの場合、"*展開の種類*" はボックスのコンテンツのセットです。 アプリのインストール方法を決定するため、アプリケーションには少なくとも 1 つの展開の種類が必要です。 同じアプリケーションに対して別のコンテンツとインストール プログラムを構成するには、複数の展開の種類を使用します。

たとえば、会社に Astoria という基幹業務アプリケーションがあるとします。 アプリケーション開発者は、アプリのインストールについて次の方法を提供します。

- Windows 10 デバイス上のすべての機能を含む Windows インストーラー パッケージ
- ターミナル サーバー ファームで使用するための App-V パッケージ
- モバイル ユーザー向けの Web アプリ  

Configuration Manager で Astoria のアプリケーションを 1 つ作成します。 アプリケーションでは、すべてのインストール方法およびプラットフォームに共通の、アプリに関する高レベルのメタデータを定義します。 次に、使用可能なインストールの方法に対して 3 つの展開の種類を作成し、すべてのユーザーにアプリケーションを展開します。 展開の種類に対する要件とその他の構成に基づいて、Configuration Manager は各ユース ケースに適切な方法を決定します。

詳細については、「[アプリケーションの展開の種類を作成する](../deploy-use/create-applications.md#bkmk_create-dt)」を参照してください。

### <a name="requirements"></a>要件

以前のバージョンの Configuration Manager では、アプリケーションの展開先デバイスのコレクションを作成していました。 コレクションを引き続き作成することはできますが、"*要件*" を使ってアプリケーションの展開に詳細な条件を指定します。

たとえば、Windows 10 を実行しているデバイスにのみアプリケーションをインストールするように指定します。 アプリケーションをすべてのデバイスに展開した場合、Windows 10 を実行しているデバイスにのみインストールされます。

Configuration Manager は、要件を評価して、アプリケーションとその展開の種類のいずれかがインストールされるかどうかを判別します。 その後、適切な展開の種類を判別します。この展開の種類を使用して、アプリケーションがインストールされます。 既定では 7 日ごとに、クライアント設定の **[展開の再評価スケジュールを指定する]** に従って、コンプライアンスを確認するために要件の規則が Configuration Manager クライアントによって再評価されます。

詳細については、「[アプリケーションの作成と展開](../get-started/create-and-deploy-an-application.md)」および[展開の種類の要件](../deploy-use/create-applications.md#bkmk_dt-require)に関するページを参照してください。

### <a name="global-conditions"></a>グローバル条件

単一のアプリケーションの特定の展開の種類では要件を使用しますが、"*グローバル条件*" を作成することもできます。 これらの条件は、任意のアプリケーションと展開の種類で使用できる定義済みの要件のライブラリです。 Configuration Manager には、一連の組み込みグローバル条件が用意されていますが、独自の条件を作成することもできます。

詳細については、「[グローバル条件の作成](../deploy-use/create-global-conditions.md)」を参照してください。

### <a name="simulated-deployment"></a>展開シミュレーション

"*展開のシミュレーション*" では、アプリケーションの要件、検出方法、依存関係を評価します。 クライアントは、アプリケーションを実際にインストールすることなく結果を報告します。

詳細については、「[System Center Configuration Manager でアプリケーションの展開をシミュレートする](../deploy-use/simulate-application-deployments.md)」をご覧ください。  

### <a name="deployment-action"></a>展開の操作

"*展開の操作*" は、展開しているアプリケーションをインストールするかアンインストールするかを指定します。 すべての展開の種類でアンインストール操作がサポートされるとは限りません。

詳細については、「[アプリケーションの展開](../deploy-use/deploy-applications.md)」をご覧ください。  

### <a name="deployment-purpose"></a>展開の目的

"*展開の目的*" は、展開アプリが**必須**であるか**利用可能**であるかを指定します。  

- 設定したスケジュールに従って、"*必須*" の展開がクライアントによって自動的にインストールされます。 アプリケーションが非表示でない場合、ユーザーは展開状態を追跡できます。 ソフトウェア センターを使用して、期限前にアプリケーションをインストールすることもできます。  

- ユーザーにアプリケーションを "*利用可能*" として展開する場合、そのアプリケーションはソフトウェア センターに表示され、オンデマンドで要求できます。  

詳細については、「[アプリケーションの展開](../deploy-use/deploy-applications.md)」をご覧ください。  

### <a name="revisions"></a>リビジョン

アプリケーションまたは展開の種類に "*リビジョン*" を作成すると、Configuration Manager はそのアプリケーションの新しいバージョンを作成します。 Configuration Manager コンソールで、次のアクションを実行します。

- 各アプリケーションのリビジョン履歴を表示します
- プロパティを表示します
- アプリケーションの以前のバージョンを復元します
- 以前のバージョンを削除します

詳しくは、[アプリケーションの修正](../deploy-use/revise-and-supersede-applications.md#application-revisions)に関するページをご覧ください。  

### <a name="detection-method"></a>検出方法

"*検出方法*" は、デバイスにアプリケーションが既にインストールされているかどうかを確認するために使用されます。 検出方法によってアプリケーションがインストール済みであることが判明した場合、Configuration Manager はそのアプリケーションをもう一度インストールしようとはしません。

詳細については、[展開の種類の検出方法のオプション](../deploy-use/create-applications.md#bkmk_dt-detect)に関する記事を参照してください。

### <a name="dependencies"></a>の依存関係

"*依存関係*" では、クライアントでこの展開の種類をインストールする前にインストールする必要がある、別のアプリケーションからの 1 つまたは複数の展開の種類が定義されます。

詳細については、[展開の種類の依存関係](../deploy-use/create-applications.md#bkmk_dt-depend)に関するページを参照してください。  

### <a name="supersedence"></a>置き換え

Configuration Manager を使用すると、"*置き換え*" の関係を使用して、既存のアプリケーションをアップグレードするか置き換えることができます。 アプリケーションを置き換える場合は、置換対象のアプリケーションの展開の種類を置き換える新しい展開の種類を指定します。 また、既存のものを置き換えるアプリケーションをクライアントがインストールする前に、新しいもので置き換えられるアプリケーションをアップグレードするかアンインストールするかを決定することもできます。

詳細については、「[アプリケーションの置き換え](../deploy-use/revise-and-supersede-applications.md#application-supersedence)」を参照してください。  

### <a name="user-centric-management"></a>ユーザー中心の管理

Configuration Manager のアプリケーションでは、特定のユーザーを特定のデバイスに関連付けることができる、"*ユーザー主体の管理*" がサポートされます。 ユーザーのデバイスの名前を記憶する代わりに、アプリをユーザーとデバイスに展開します。 この機能により、ユーザーの各デバイスで、最も重要なアプリを常に使用可能にすることができます。 ユーザーが新しいコンピューターを入手した場合、Configuration Manager は、ユーザーがサインインする前に、そのデバイスにユーザーのアプリを自動的にインストールします。

詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。  

### <a name="application-group"></a>アプリケーション グループ

バージョン 1906 以降では、1 つの展開としてユーザーまたはデバイス コレクションに送信できるアプリケーションのグループを作成します。 アプリ グループについて指定したメタデータは、ソフトウェア センターでは 1 つのエンティティとして表示されます。 アプリがクライアントに特定の順序でインストールされるように、グループ内のアプリに順序を付けることができます。

詳しくは、「[アプリケーション グループの作成](../deploy-use/create-app-groups.md)」をご覧ください。

## <a name="what-application-types-can-you-deploy"></a>展開可能なアプリケーションの種類

Configuration Manager では、次の種類のアプリケーションを展開できます。  

- Windows インストーラー (msi)  

- Windows アプリ パッケージおよびアプリ バンドル (appx、appxbundle、msix、msixbundle)  

- Microsoft Store 内の Windows アプリ パッケージ  

- サードパーティのインストーラーおよびスクリプト ラッパー用のスクリプト インストーラー

- Microsoft App-V v4 および v5  

- macOS  

- 複雑なアプリ用の、OS 以外の展開タスク シーケンス

また、Configuration Manager の[オンプレミス デバイス管理](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)でデバイスを管理する場合、さらに次のアプリの種類も管理します。  

- Windows Phone アプリ パッケージ (xap)  

- Microsoft Store 内の Windows Phone アプリ パッケージ  

- MDM を介した Windows インストーラー (msi)  

- Web アプリケーション

## <a name="state-based-applications"></a>状態ベースのアプリケーション  

Configuration Manager アプリケーションでは、状態ベースの監視を使用します。 ユーザーとデバイスの最新のアプリケーション展開状態を追跡できます。 これらの状態メッセージには、個々のデバイスに関する情報が表示されます。 たとえば、アプリケーションをユーザーのコレクションに展開する場合、Configuration Manager コンソールで展開のコンプライアンスの状態と展開の目的を表示できます。 すべてのソフトウェアの展開は、Configuration Manager コンソールの **[監視]** ワークスペースから監視します。 詳細については、「[アプリケーションの監視](../deploy-use/monitor-applications-from-the-console.md)」を参照してください。  

Configuration Manager クライアントはアプリケーションの展開を定期的に再評価します。 次に例を示します。  

- ユーザーは、展開されたアプリケーションをアンインストールします。 次の評価サイクルで、Configuration Manager はアプリが存在していないことを検出します。 クライアントはアプリを自動的に再インストールします。  

- Configuration Manager は、要件を満たしていないためアプリケーションをデバイスにインストールしませんでした。 その後、デバイスが変更され、要件を満たすようになります。 Configuration Manager はその変更を検出し、クライアントはアプリケーションをインストールします。  

アプリケーションの展開の再評価間隔を設定することができます。 **[ソフトウェアの展開]** グループの **[展開の再評価スケジュールを指定する]** クライアント設定を使用します。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#software-deployment)」を参照してください。  

## <a name="get-started-creating-an-application"></a>アプリケーション作成の概要  

すぐにアプリケーションを作成する場合は、「[アプリケーションの作成と展開](../get-started/create-and-deploy-an-application.md)」の記事にチュートリアルがあります。  

基礎知識があり、使用可能なすべてのオプションについて詳しい参照情報を探している場合は、[アプリケーションの作成](../deploy-use/create-applications.md)を開始します。  

## <a name="software-center"></a>ソフトウェア センター  

ソフトウェア センターは、Configuration Manager クライアントでインストールされる Windows アプリケーションです。 これを使用して次の操作を実行します。  

- デバイスまたはユーザーに展開されるアプリケーションの参照と要求
- ソフトウェアのインストールとインストールのスケジュール
- アプリケーション、ソフトウェア更新プログラム、およびオペレーティング システムのインストール状態の表示
- リモート コントロール設定の構成
- 電源管理の設定

詳細については、以下の記事を参照してください。  

- [アプリケーション管理の計画と構成](../plan-design/plan-for-and-configure-application-management.md)
- [ソフトウェア センターの計画](../plan-design/plan-for-software-center.md)
- [ソフトウェア センターのユーザー ガイド](../../core/understand/software-center.md)

> [!Note]  
> アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。 詳細については、「[アプリケーション カタログの削除](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)」を参照してください。  

## <a name="packages-and-programs"></a>パッケージとプログラム  

Configuration Manager は、以前のバージョンの製品で使用されていたパッケージおよびプログラムを引き続きサポートします。

詳細については「[Packages and programs](../deploy-use/packages-and-programs.md)」(パッケージとプログラム) を参照してください。  

## <a name="next-steps"></a>次のステップ

Configuration Manager でのアプリケーション管理の基本的な概念を理解したところで、次の記事に進みます。

- [サンプル アプリケーションの作成と展開](../get-started/create-and-deploy-an-application.md)
- [アプリケーション管理の計画と構成](../plan-design/plan-for-and-configure-application-management.md)
- [アプリケーションの作成](../deploy-use/create-applications.md)
