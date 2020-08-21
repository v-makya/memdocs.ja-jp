---
title: 追加のプライバシー情報
titleSuffix: Configuration Manager
description: Configuration Manager からデータを Microsoft が収集して使用する方法について説明します。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6d3f6dbbbb407ee63eb8253cbf3ca740a10479c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699791"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Configuration Manager のプライバシーに関する詳細

*適用対象:Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>更新プログラムとサービス

Configuration Manager では、最新の更新プログラムと機能を使用して環境を最新の状態に保つのに役立つ更新モデルが使用されています。 この機能では、サービス接続ポイントと呼ばれるサイト システムの役割が使用されます。 この役割をインストールするサーバーを選択します。 

収集される情報とその使用方法について詳しくは、「[使用状況データ](#usage-data)」をご覧ください。



## <a name="usage-data"></a>使用状況データ

Configuration Manager では、自身の診断および使用状況データが収集されます。このデータは、今後のリリースでインストールのエクスペリエンス、品質、セキュリティを向上させるために Microsoft によって使用されます。
診断および使用状況データは、それぞれの Configuration Manager 階層で有効になります。 これは、各プライマリ サイトと中央管理サイトで毎週実行される SQL Server クエリで構成されます。 階層が中央管理サイトを使用している場合、プライマリ サイトからのデータはそのサイトに複製されます。 階層の最上位のサイトでは、サービス接続ポイントが、更新プログラムをチェックするときに、この情報を送信します。 サービス接続ポイントがオフライン モードの場合、情報は、サービス接続ツールを使用して転送されます。

Configuration Manager は、サイトの SQL Server データベースからのみデータを収集します。クライアントやサイト サーバーから直接データを収集することはありません。

管理者は、Configuration Manager コンソールの **[使用状況データ]** セクションで、収集されるデータのレベルを変更できます。

使用状況データのレベルと設定について詳しくは、「[診断結果と使用状況データ](../diagnostics/diagnostics-and-usage-data.md)」をご覧ください。



## <a name="log-analytics-connector"></a>Log Analytics コネクタ

Log Analytics コネクタは、Configuration Manager から Azure クラウド サービスに、コレクションなどのデータを同期します。 Azure サブスクリプション ID と秘密鍵は、管理者が機能を構成するときに Configuration Manager データベースに保管されます。 Azure Active Directory のクライアント シークレットと Azure ワークスペースの共有キーは、オンプレミスの Configuration Manager データベースに保存されます。 Configuration Manager と Azure の間のすべての通信では、HTTPS が使用されます。 無作為に選択された診断と使用状況のデータを除き、コレクションに関する追加情報は Microsoft に提供されません。 

Log Analytics で収集される情報について詳しくは、「[Log Analytics データのセキュリティ](/azure/log-analytics/log-analytics-data-security)」をご覧ください。



## <a name="asset-intelligence"></a>資産インテリジェンス

資産インテリジェンスによって、管理者が構成標準への適合性を定義し、追跡して積極的に管理することができます。 物理アプリケーションおよび仮想アプリケーションの展開と使用に関するメータリング機能やレポート機能を使用して、組織は情報を十分に把握したうえでソフトウェア ライセンスに関する決定を下し、ライセンス上のコンプライアンス要件を遵守できます。 Configuration Manager クライアントから使用状況データを収集した後で、各種の機能を使用してコレクション、クエリ、レポートなどのデータを表示できます。

毎回の同期時に、既知のソフトウェアのカタログが Microsoft からダウンロードされます。 組織で検出され、調査してカタログに追加する予定の分類されていないソフトウェア タイトルに関する情報を、Microsoft に送信することもできます。 この情報をアップロードする前に、アップロードされるデータがダイアログ ボックスに表示されます。 アップロードされたデータを取り消すことはできません。 資産インテリジェンスからは、Microsoft にユーザーおよびコンピューターに関する情報やライセンスの使用状況は送信されません。

ソフトウェア タイトルがアップロードされると、Microsoft の調査担当者が特定および分類し、この機能を使用するすべてのお客様とカタログのその他のお客様がソフトウェアの情報を利用できるようにします。 アップロードされたソフトウェア タイトルは公開されます。 アプリケーションとその分類は、カタログの一部となり、カタログの他の利用者がダウンロードできるようになります。 資産インテリジェンス データの収集を構成し、Microsoft に送信する情報を決める前に、組織のプライバシーに関する要件を考慮してください。

既定では、資産インテリジェンスは Configuration Manager で有効になっていません。 分類されていないタイトルは自動的にアップロードされません。また、システムはこのタスクを自動化するように設計されていません。 各ソフトウェア タイトルのアップロードを手動で選択および承認する必要があります。



## <a name="endpoint-protection"></a>Endpoint Protection

Microsoft Cloud Protection Service は、以前は Microsoft Active Protection Service (MAPS) という名称でした。

該当製品は、System Center Endpoint Protection と Configuration Manager の Endpoint Protection 機能 (System Center Endpoint Protection と Windows Defender for Windows 10 の管理用) です。 System Center Endpoint Protection for Linux または System Center Endpoint Protection for Mac の場合、この機能は実装されていません。

Microsoft Cloud Protection Service のマルウェア対策コミュニティは、System Center Endpoint Protection のユーザーが世界各地から参加している自発的なオンライン コミュニティです。 Microsoft Cloud Protection Service に参加すると、System Center Endpoint Protection によって情報が Microsoft に自動的に送信されます。 Microsoft ではこの情報を使用して、潜在的な脅威を調査し、System Center Endpoint Protection の有効性の向上に役立つソフトウェアを決定します。 このコミュニティは、悪意のある新しいソフトウェアへの大量感染の阻止に役立ちます。 Microsoft Cloud Protection Service のレポートに、Endpoint Protection クライアントが削除できる可能性があるマルウェアまたは望ましくない可能性があるソフトウェアの詳細が含まれている場合、Microsoft Cloud Protection Service がこれに対処するために最新の署名をダウンロードします。 Microsoft Cloud Protection Service は、"偽陽性" を探して修正することもできます (偽陽性とは、最初はマルウェアと判断されたものがマルウェアではないと判明することです)。 

Microsoft Cloud Protection Service レポートには、ファイル名、暗号化ハッシュ、ベンダー、サイズ、日付スタンプなど、マルウェアの可能性があるファイルに関する情報が含まれています。 また、Microsoft Cloud Protection Service はファイルの出所を示す完全 URL を収集することがあります。 そのような URL には、検索用語やフォームに入力されたデータなど、個人情報が含まれることがあります。 望ましくないソフトウェアに関する通知が Endpoint Protection から届いたときに行った措置がレポートに含まれることもあります。 Microsoft Cloud Protection Service レポートに含まれるその情報は、マルウェアと望ましくない可能性があるソフトウェアがどの程度効率的に Endpoint Protection で検出され、駆除されるかを Microsoft が計測したり、新しいマルウェアを特定したりするときに役立ちます。

基本メンバーシップまたは上級メンバーシップをお持ちであれば、Microsoft Cloud Protection Service に参加できます。 基本メンバーのレポートには上記の情報が含まれています。 上級メンバーのレポートにはさらに、ソフトウェアの場所、ファイル名、ソフトウェアの動作、およびコンピューターに与える影響など、Endpoint Protection で検出されたソフトウェアに関する詳細情報が記載されます。 マイクロソフトの調査担当者は、これらのレポートを Microsoft Cloud Protection Service に参加する他の Endpoint Protection ユーザーからのレポートと併せて、新たな脅威を迅速に検知するために役立てています。 その後、分析条件を満たすプログラムについてマルウェア定義を作成し、更新した定義ファイルを Microsoft Update 経由ですべてのユーザーに提供します。

特定の種類のマルウェア感染を検知して修正するため、製品からお客様の PC のセキュリティ状態に関する情報が定期的に Microsoft Cloud Protection Service に送信されます。 この情報には、お客様の PC のセキュリティ設定や、PC の起動時に読み込まれるドライバーと他のソフトウェアを記録しているログ ファイルが含まれます。

PC を一意に識別する番号も送信されます。 また、Microsoft Cloud Protection Service が潜在的なマルウェア ファイルが接続する IP アドレスを収集することがあります。

Microsoft Cloud Protection Service レポートは、マイクロソフトのソフトウェアおよびサービスを向上させるために使用されます。 さらに、統計またはその他のテストや分析、および定義を生成するために使用される場合もあります。 レポートにアクセスできるのは、業務上その使用が不可欠な Microsoft の従業員、契約社員、パートナー、および製造元に限られています。

Microsoft Cloud Protection Service が意図的に個人情報を収集することはありません。 Microsoft Cloud Protection Service によって個人情報が収集された場合でも、Microsoft がその情報を使用してお客様の身元を特定したりお客様に連絡したりすることはありません。

詳しくは、「[Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)」をご覧ください。



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>サイト階層 – Bing Maps を使用した地図

Configuration Manager コンソールで、 **[監視]** ワークスペースに移動し、 **[サイト階層]** ノードを選択して、 **[地図]** に切り替えます。 この表示では、Microsoft Bing Maps の提供する地図を使って Configuration Manager 物理サーバー トポロジを表示できます。 この機能を実現するために、お客様の入力した場所情報が、サーバーから Bing Maps の Web サービスに送信されます。

マイクロソフトではこの情報を、Microsoft Bing Maps およびその他の Microsoft のサイトとサービスを提供および向上するために役立てています。 詳細については、「[Microsoft のプライバシーに関する声明](https://privacy.microsoft.com/privacystatement)」を参照してください。

サイト階層で地図を使用しないように選択できます。 既定の階層図では、Bing Maps サービスを使用せずに階層を表示することができます。