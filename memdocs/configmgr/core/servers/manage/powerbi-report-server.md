---
title: Power BI Report Server との統合
titleSuffix: Configuration Manager
description: 最新の視覚化とパフォーマンスの向上のために、Power BI Report Server を Configuration Manager レポートと統合します。
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc8aa57bda5f5a29d72af854be9a18e4f32760f8
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432542"
---
# <a name="integrate-with-power-bi-report-server"></a>Power BI Report Server との統合

*適用対象:Configuration Manager (Current Branch)*

<!--3721603-->

バージョン 2002 以降では、[Power BI Report Server](/power-bi/report-server/get-started) を Configuration Manager レポートと統合できるようになりました。 この統合により、最新の視覚化とパフォーマンスの向上が実現します。 SQL Server Reporting Services に既に存在するものと同様の Power BI レポートのコンソールのサポートが追加されます。

Power BI Desktop レポート ファイル (.PBIX) が保存され、Power BI Report Server に配置されます。 このプロセスは、SQL Server Reporting Services レポート ファイル (.RDL) と似ています。 また、Configuration Manager コンソールから直接、ブラウザーでレポートを起動することもできます。

## <a name="prerequisites"></a>[前提条件]

- Power BI Report Server ライセンス。 詳細については、「[Power BI Report Server のライセンス](/power-bi/report-server/get-started#licensing-power-bi-report-server)」を参照してください。

- [Microsoft Power BI Report Server - 2019 年 9 月](https://www.microsoft.com/download/details.aspx?id=57270)以降をダウンロードします。

    > [!NOTE]
    > Power BI Report Server をすぐにインストールしないでください。 ご使用の環境に応じた適切なプロセスについては、「[レポート サービス ポイントを構成する](#configure-the-reporting-services-point)」を参照してください。

- [Microsoft Power BI Desktop (Power BI Report Server 向けに最適化 - 2019 年 9 月)](https://www.microsoft.com/download/details.aspx?id=57271) 以降をダウンロードします。

    > [!IMPORTANT]
    > - [Microsoft ダウンロード センター](https://www.microsoft.com/download/)の Power BI Desktop バージョンのみを使用し、Microsoft Store のバージョンは使用しないでください。
    > - [**Power BI Report Server 用に最適化済み**と記載されている Power BI Desktop](/power-bi/report-server/install-powerbi-desktop) のバージョンのみを使用してください。

- Power BI 統合では、レポートに同じロール ベース管理を使用します。
    > [!NOTE]
    > Power BI Report Server では、RBAC が有効なレポートがサポートされていないため、レポートのすべての閲覧者には、割り当てられたスコープに関係なく同じ結果が表示されます。

## <a name="configure-the-reporting-services-point"></a>レポート サービス ポイントを構成する

このプロセスは、このロールがサイトに既に存在するかどうかによって異なります。

### <a name="you-have-a-reporting-services-point"></a>レポート サービス ポイントがある

サイトにレポート サービス ポイントが既にある場合にのみ、このプロセスを使用してください。 同じサーバー上で、このプロセスのすべての手順を実行します。

1. **Reporting Server Configuration Manager** で、**暗号化キー**をバックアップします。 詳細については、「[SSRS の暗号化キー - 暗号化キーのバックアップと復元](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys)」を参照してください。

    > [!WARNING]
    > この手順を省略すると、SQL Server Reporting Services のカスタム レポートにアクセスできなくなります。

1. サイトからレポート サービス ポイントのロールを削除します。

1. SQL Server Reporting Services をアンインストールしますが、データベースは保持します。

1. Power BI Report Server をインストールします。

1. Power BI Report Server を構成する

    1. 前のレポート サーバー データベースを使用します。

    1. **Reporting Server Configuration Manager** を使用して、**暗号化キー**を復元します。

1. Configuration Manager にレポート サービス ポイントのロールを追加します。

### <a name="you-dont-have-a-reporting-services-point"></a>レポート サービス ポイントがない

サイトにレポート サービス ポイントがまだない場合にのみ、このプロセスを使用してください。 同じサーバー上で、このプロセスのすべての手順を実行します。

1. Power BI Report Server をインストールします。

2. Configuration Manager にレポート サービス ポイントのロールを追加します。 詳しくは、[レポートの構成](configuring-reporting.md)に関するページをご覧ください。

## <a name="configure-the-configuration-manager-console"></a>Configuration Manager コンソールを構成する

1. Configuration Manager コンソールがあるコンピューターで、Configuration Manager コンソールを最新バージョンに更新します。

1. Power BI Desktop をインストールします。 言語が同じであることを確認します。

1. インストール後、Configuration Manager コンソールを開く前に、少なくとも 1 回 Power BI Desktop を起動します。

## <a name="create-power-bi-reports"></a>Power BI レポートを作成する

1. Configuration Manager コンソールで、 **[監視]** ワークスペースに移動して、 **[レポート]** を展開し、新しい **[Power BI レポート]** ノードを選択します。

1. リボンで **[レポートの作成]** を選択します。 このアクションにより Power BI Desktop が開きます。

1. Power BI Desktop でレポートを作成します。

    - Power BI Desktop で、データ ソースに接続するときに、接続設定に **DirectQuery** を選択します。

    - これらのレポートでは、サポートされている SQL ビューのみを使用します。 詳細については、「[Configuration Manager で SQL Server ビューを使用してカスタム レポートを作成する](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md)」を参照してください。

1. レポートを保存する準備ができたら、 **[ファイル]** メニューにアクセスし、 **[名前を付けて保存]** 、 **[Power BI Report Server]** の順に選択します。

1. **[Power BI Report Server の選択]** ウィンドウで、**新しいレポート サーバー アドレス**としてレポート サービス ポイントの URL を入力します。 たとえば、`https://rsp.contoso.com/Reports` となります。 **[OK]** を選択します。

1. **[レポートの保存]** ウィンドウで、`ConfigMgr_<SiteCode>` フォルダーをダブルクリックします。 たとえば、`ConfigMgr_PS1` です (`PS1` は ConfigMgr サイト コード)。 必要に応じて、これを保存するサブ フォルダーを (レポート サーバーから) 選択または作成することもできます。
    > [!TIP]
    > レポートおよび Power BI レポートを含むレポート フォルダーは、レポート サーバー上の `ConfigMgr_<SiteCode>` フォルダーに配置する必要があります。そうしないと、Configuration Manager コンソールに表示されません。

1. **[ファイル名]** にレポートの名前を入力します。

Configuration Manager コンソールで、Power BI レポートの一覧に新しいレポートが表示されます。 レポートが表示されない場合は、レポートを `ConfigMgr_<SiteCode>` フォルダーに保存したことを確認してください。

## <a name="next-steps"></a>次のステップ

レポートを作成したら、Configuration Manager コンソールで次の操作を実行します。

- **ブラウザーで実行**:Web ブラウザーで Power BI レポートを開きます。 この URL を他のユーザーと共有します。例: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > これらのレポートは、Web ブラウザーでのみ表示できます。

- **編集**:Power BI Desktop でレポートに変更を加えます。 既存のレポートの場合は、 **[保存]** オプションを使用して、レポート サーバーに変更を保存します。

レポートに使用するログ ファイルの詳細については、「[ログ ファイルのリファレンス - レポート](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog)」を参照してください。
