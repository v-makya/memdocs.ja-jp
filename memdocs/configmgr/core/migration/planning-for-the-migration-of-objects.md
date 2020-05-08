---
title: オブジェクトの移行
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch 環境での階層間でオブジェクトの移行を計画する方法について説明します。
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 93c3887307c32ea636a6dbb064cda13f4b9130c6
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905131"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Configuration Manager オブジェクトの Configuration Manager の現在のブランチへの移行を計画する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch では、ソース サイトで見つかったさまざまな機能に関連する、さまざまなオブジェクトの多くを移行できます。

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a> ソフトウェア更新プログラムの移行の計画  
 ソフトウェア更新プログラム パッケージやソフトウェア更新プログラムの展開などのソフトウェア更新プログラム オブジェクトを移行できます。  

 ソフトウェア更新プログラム オブジェクトを移行するには、まず、ソース階層の環境と一致する構成を使用して、移行先階層を設定する必要があります。 そのためには、次の操作が必要です。  

-   移行先階層にアクティブなソフトウェアの更新ポイントを展開する  

-   ソース階層の構成と一致する、製品と言語のカタログを設定する  

-   移行先階層のソフトウェアの更新ポイントと Windows Server Update Services (WSUS) を同期する  

ソフトウェア更新プログラムを移行する際には、以下の点を考慮してください。  

-   ソース階層の構成と一致するように移行先階層の情報を同期していない場合、ソフトウェア更新プログラム オブジェクトの移行が失敗する可能性があります。  

    > [!WARNING]  
    >  Configuration Manager は、WSUSutil ツールを使用したソース階層と移行先階層間のデータの同期をサポートしていません。  

-   System Center Updates Publisher を使用して発行されたカスタム更新プログラムを移行することはできません。 代わりに、カスタム更新プログラムを移行先階層に再発行できます。  

Configuration Manager 2007 ソース階層から移行する場合、移行処理で、一部のソフトウェア更新プログラム オブジェクトが、移行先階層で使用される形式に変更されます。 Configuration Manager 2007 からのソフトウェア更新プログラム オブジェクトの移行を計画する際には、次の表を参考にしてください。  

|Configuration Manager 2007 オブジェクト|移行後のオブジェクト名|  
|-----------------------------------|---------------------------------|  
|ソフトウェア更新プログラム一覧|ソフトウェア更新プログラムのリストがソフトウェア更新プログラム グループに変換されます。|  
|ソフトウェア更新プログラムの展開|ソフトウェア更新プログラムの展開が、展開と更新プログラムのグループに変換されます。<br /><br /> Configuration Manager 2007 からソフトウェア更新プログラムの展開を移行した後、このソフトウェア更新プログラムを展開するには、まず移行先サイトで有効にする必要があります。|  
|ソフトウェア更新プログラム パッケージ|ソフトウェア更新プログラム パッケージは、ソフトウェア更新プログラム パッケージのまま維持されます。|  
|ソフトウェア更新プログラム テンプレート|ソフトウェア更新プログラム テンプレートは、ソフトウェア更新プログラム テンプレートのまま維持されます。<br /><br /> Configuration Manager 2007 の展開テンプレートの **[期間]** 値は移行されません。|  

System Center 2012 Configuration Manager または Configuration Manage Current Branch ソース階層からオブジェクトを移行するときは、ソフトウェア更新オブジェクトは変更されません。  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a> コンテンツの移行の計画  
 サポートされているソース階層から移行先階層にコンテンツを移行できます。 Configuration Manager 2007 ソース階層では、このコンテンツには、ソフトウェアの配布パッケージとプログラム、および Microsoft Application Virtualization (App-V) などの仮想アプリケーションが含まれます。 System Center 2012 Configuration Manager および Configuration Manager Current Branch のソース階層の場合、このコンテンツには、アプリケーションおよび App-V 仮想アプリケーションが含まれています。 階層間でコンテンツを移行すると、圧縮ソース ファイルが移行先階層に移行されます。  

### <a name="packages-and-programs"></a>パッケージとプログラム  
 パッケージとプログラムを移行しても、移行処理により変更されません。 ただし移行前に、ソース ファイルの場所に汎用名前付け規則 (UNC) パスを使用するように各パッケージを設定しておく必要があります。 パッケージとプログラムを移行するための構成の一環として、移行先階層内にこのコンテンツを管理するサイトを割り当てる必要があります。 割り当てたサイトからコンテンツは移行されませんが、移行後、割り当てたサイトが UNC マッピングを使用して元のソース ファイルの場所にアクセスします。  

 移行先階層にパッケージとプログラムを移行した後で、ソース階層からの移行が引き続きアクティブになっている間は、共有配布ポイントを使用して、その階層内のクライアントでコンテンツを利用できるようにすることができます。 共有配布ポイントを使用するには、ソース サイトの配布ポイントで、コンテンツに引き続きアクセスできる必要があります。 共有配布ポイントの詳細については、[コンテンツ展開移行戦略の計画](../../core/migration/planning-a-content-deployment-migration-strategy.md)に関する記事の「[ソース階層と移行先階層での配布ポイントの共有](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)」を参照してください。  

 移行済みのコンテンツでは、ソース階層または移行先階層のいずれかでコンテンツのバージョンが変更されると、クライアントが移行先階層の共有配布ポイントからコンテンツにアクセスできなくなります。 その場合は、コンテンツを移行し直して、ソース階層と移行先階層間で、一貫したバージョンのパッケージを復元する必要があります。 この情報は、データ収集時に同期されます。  

> [!TIP]  
>  移行するパッケージごとに、移行先階層でパッケージを更新します。 このアクションで、移行先階層での配布ポイントへのパッケージの展開に関する問題を防ぐことができます。 ただし、移行先階層の配布ポイントでパッケージを更新すると、その階層のクライアントが共有配布ポイントからそのパッケージを取得できなくなります。 移行先階層でパッケージを更新するには、Configuration Manager コンソールで、ソフトウェア ライブラリに移動し、パッケージを右クリックしてから **[配布ポイントの更新]** を選択します。 移行したパッケージごとにこのアクションを実行します。  

> [!TIP]  
> Package Conversion Manager を使用して、パッケージとプログラムを Configuration Manager アプリケーションに変換します。 詳細については、[Package Conversion Manager](../../apps/pcm/package-conversion-manager.md) に関するページを参照してください。  

### <a name="virtual-applications"></a>仮想アプリケーション  
サポートされている Configuration Manager 2007 サイトから App-V パッケージを移行すると、移行処理でこのパッケージは移行先階層のアプリケーションに変換されます。 さらに、App-V パッケージの既存の開示通知を基に、移行先階層で次のように展開の種類が作成されます。  

-   開示通知がない場合は、展開の種類の既定設定を使用する展開の種類が 1 つ作成されます。  

-   公開通知が 1 つある場合は、Configuration Manager 2007 の公開通知と同じ設定を使用する展開の種類が 1 つ作成されます。  

-   公開通知が複数ある場合は、各公開通知の設定を使用して、Configuration Manager 2007 の公開通知ごとに展開の種類が 1 つ作成されます。  

> [!IMPORTANT]  
>  前に移行済みの Configuration Manager 2007 App-V パッケージを再移行することはできません。これは、仮想アプリケーション パッケージは、上書き移行をサポートしていないためです。 その場合、移行済みの仮想アプリケーション パッケージを移行先階層から削除してから、新規の移行ジョブを作成して、仮想アプリケーションを移行する必要があります。  

> [!NOTE]  
>  App-V パッケージの移行後、コンテンツの更新ウィザードを使用して、App-V の展開の種類のソース パスを変更できます。 展開の種類のコンテンツを更新する方法については、「[Configuration Manager アプリケーションの管理タスク](../../apps/deploy-use/management-tasks-applications.md)」の「展開の種類の管理方法」を参照してください。  

System Center 2012 Configuration Manager または Configuration Manager Current Branch のソース階層から移行するときに、App-V の展開の種類とアプリケーションに加えて、App-V 仮想環境のオブジェクトも移行することができます。 App-V 環境の詳細については、[App-V 仮想アプリケーションの展開](../../apps/get-started/deploying-app-v-virtual-applications.md)に関する記事を参照してください。  

### <a name="advertisements"></a>開示通知 (旧称「提供情報」)  
コレクション ベースの移行を使用して、サポートされている Configuration Manager 2007 ソース サイトから移行先階層に開示通知を移行できます。 クライアントをアップグレードする場合は、クライアントで移行済みの開示通知が再実行されないように、以前に実行された開示通知の履歴が保持されます。  

> [!NOTE]  
>  仮想パッケージの開示通知は移行できません。 これは、開示情報の移行の例外となります。  

### <a name="applications"></a>アプリケーション  
 サポートされている System Center 2012 Configuration Manager または Configuration Manager Current Branch のソース階層から移行先階層にアプリケーションを移行できます。 ソース階層から移行先階層にクライアントを再割り当てする場合は、クライアントで移行済みのアプリケーションが再実行されないように、以前にインストールされたアプリケーションの履歴がクライアントに保持されます。  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a> コレクションの移行の計画  
 サポートされている System Center 2012 Configuration Manager または Configuration Manager Current Branch のソース階層からコレクションの条件を移行できます。 コレクションの条件を移行するには、オブジェクト ベースの移行ジョブを使用します。 コレクションを移行する際、コレクションの規則を移行します。コレクションのメンバーの情報や、コレクションのメンバーに関連する情報やオブジェクトは移行しません。  

 コレクションのオブジェクトの移行は、Configuration Manager 2007 ソース階層から移行する場合はサポートされていません。  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a> オペレーティング システムの展開の移行の計画  
サポートされているソース階層から、次のオペレーティング システムの展開オブジェクトを移行できます。  

-   オペレーティング システムのイメージとパッケージ。 ブート イメージのソース パスは、移行先サイトの Windows 自動インストール キット (Windows AIK) の既定のイメージの場所に更新されます。 以下に、オペレーティング システムのイメージとパッケージを移行する際の要件と制限事項を示します。  

    -   イメージ ファイルを移行するには、移行先階層の最上位サイトの SMS プロバイダー サーバーのコンピューター アカウントに、ソース サイトの Windows AIK の場所にあるイメージ ソース ファイルの**読み取り**アクセス許可と**書き込み**アクセス許可が必要です。  

    -   オペレーティング システムのインストール パッケージを移行するときに、ソース サイトのパッケージの構成で、WIM ファイル自体ではなく、WIM ファイルが含まれているフォルダーを指定していることを確認してください。 インストール パッケージが WIM ファイルを指定している場合、インストール パッケージの移行は失敗します。  

    -   Configuration Manager 2007 ソース サイトからブート イメージ パッケージを移行する場合、パッケージのパッケージ ID は移行先サイトに保持されません。 そのため、移行先階層のクライアントでは、共有配布ポイントで提供されているブート イメージ パッケージを使用することができません。  

-   タスク シーケンス クライアント インストール パッケージへの参照が含まれているタスク シーケンスを移行すると、この参照が移行先階層のクライアント インストール パッケージへの参照に置き換えられます。  

    > [!NOTE]  
    >  タスク シーケンスを移行する場合、Configuration Manager によって、移行先階層では必要ないオブジェクトが移行されることがあります。 このようなオブジェクトには、ブート イメージと Configuration Manager 2007 クライアント インストール パッケージがあります。  

-   ドライバーとドライバー パッケージ。 ドライバー パッケージを移行する場合、移行先階層内の SMS プロバイダーのコンピューター アカウントでパッケージ ソースを完全に制御できる必要があります。

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a> 必要な構成管理の移行の計画  
構成項目と構成基準を移行できます。  

> [!NOTE]  
>  移行では、Configuration Manager 2007 ソース階層の解釈なしの構成項目はサポートされていません。 これらの構成項目は、移行先階層に移行もインポートもできません。 解釈なしの構成項目については、Configuration Manager 2007 ドキュメント ライブラリの「[必要な構成管理の構成項目について](https://docs.microsoft.com/previous-versions/system-center/configuration-manager-2007/bb694136(v=technet.10)#uninterpreted-configuration-item)」トピックの「解釈なしの構成項目」セクションを参照してください。  

Configuration Manager 2007 構成パックをインポートすることができます。 インポート処理により、自動的に構成パックが Configuration Manager Current Branch と互換性を持つように変換されます。  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a> 境界の移行の計画  
 階層間の境界を移行できます。 Configuration Manager 2007 から境界を移行する場合、ソース サイトの各境界が同時に移行されて、移行先階層に作成される新しい境界グループに追加されます。 System Center 2012 Configuration Manager または Configuration Manager Current Branch 階層から境界を移行する場合、選択した各境界が移行先階層の新しい境界グループに追加されます。  

 自動作成される各境界グループでは、サイトの割り当てではなく、コンテンツの場所が有効になります。 これにより、ソース階層と移行先階層の間のサイトの割り当てで境界が重複するのを防止できます。 Configuration Manager 2007 ソース サイトから移行する場合、これにより、インストールする新しい Configuration Manager 2007 クライアントが移行先階層に誤って割り当てられるのを防止できます。 既定では、Configuration Manager Current Branch クライアントによって Configuration Manager 2007 サイトには自動的に割り当てられません。  

 移行中に、配布ポイントを移行先階層と共有する場合は、その配布ポイントに関連付けられているすべての境界が移行先階層に自動的に移行されます。 移行先階層では、移行によって、共有配布ポイントごとに新しい読み取り専用の境界グループが作成されます。 ソース階層の配布ポイントの境界を変更すると、次回のデータ収集サイクル中に、これらの変更を反映して移行先階層の境界グループが更新されます。  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a> レポートの移行の計画  
Configuration Manager では、レポートの移行をサポートしていません。 代わりに、SQL Server Reporting Services レポート ビルダーを使用して、ソース階層からレポートをエクスポートしてから移行先階層にインポートします。  

> [!NOTE]  
>  Configuration Manager 2007 と Configuration Manager Current Branch の間ではレポートのスキーマが変更されているため、Configuration Manager 2007 階層からインポートした各レポートをテストして正しく機能していることを確認してください。  

レポートの詳細については、[レポートの概要](../servers/manage/introduction-to-reporting.md)に関するページを参照してください。  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a> 組織フォルダーと検索フォルダーの移行の計画  
 サポートされているソース階層から移行先階層に組織フォルダーと検索フォルダーを移行できます。 さらに、System Center 2012 Configuration Manager または Configuration Manager Current Branch のソース階層から保存されている検索の条件を移行先階層に移行できます。  

 既定では、移行時に移行処理によって、オブジェクトとコレクションの検索フォルダーと管理フォルダーの構造が維持されます。 ただし、移行ジョブの作成ウィザードの **[設定]** ページで、オブジェクトの組織構造を移行するオプションをオフにして、オブジェクトの組織構造が移行されないように移行ジョブを設定することができます。 コレクションの組織構造は常に維持されます。  

 ただし、仮想アプリケーションを含む検索フォルダーはその唯一の例外となります。 App-V パッケージの移行時に、App-V パッケージは Configuration Manager でアプリケーションに変換されます。 このように App-V パッケージが移行時にアプリケーションに変換されるため、検索フォルダーの移行後は残存するパッケージのみが検出され、検索フォルダーは App-V パッケージを見つけることができません。  

 System Center 2012 Configuration Manager または Configuration Manager Current Branch ソース階層から保存済みの検索を移行する際、検索の条件を移行し、検索結果の情報は移行しません。 保存済みの検索の移行は、Configuration Manager 2007 ソース サイトからは使用できません。  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a> 資産インテリジェンスのカスタマイズ設定の移行の計画  
 サポートされているソース階層から移行先階層に資産インテリジェンスのカスタマイズ設定を移行できます。 Configuration Manager 2007 と Configuration Manager Current Branch の間では、資産インテリジェンスのカスタマイズ設定の構造に大きな変更はありません。  

> [!NOTE]  
> Configuration Manager Current Branch は、Asset Intelligence Service 2.0 (AIS 2.0) を使用している Configuration Manager 2007 サイトからの資産インテリジェンス オブジェクトの移行をサポートしません。  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a> ソフトウェア使用状況測定規則のカスタマイズ設定の移行の計画  
 Configuration Manager 2007 と Configuration Manager Current Branch の間では、ソフトウェア使用状況測定に大きな変更はありません。 サポートされているソース階層から移行先階層にソフトウェア使用状況測定規則を移行できます。  

 既定では、移行先階層に移行するソフトウェア使用状況測定規則は、移行先階層の特定のサイトには関連付けられません。代わりに、階層内のすべてのクライアントに適用されます。 ソフトウェア使用状況測定規則を特定のサイトのクライアントに適用するには、移行後に使用状況測定規則を編集する必要があります。  
