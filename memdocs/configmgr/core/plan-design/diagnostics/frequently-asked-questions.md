---
title: 診断および使用状況データに関するよくあるご質問
titleSuffix: Configuration Manager
description: Configuration Manager の診断および使用状況データに関してよく寄せられる質問
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb14f909238e86a7aa4a87493b17a218a21f0909
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700199"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>診断および使用状況データに関してよく寄せられる質問

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager の診断および使用状況データに関してよく寄せられる質問の回答を示します。

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a> 診断および使用状況のデータをオフにすることはできますか。

サイトからデータが送信されるタイミングの管理するには、サービス接続ポイントをオフライン モードで使用します。 次に、サービス接続ツールを使用して、手動でデータを送信します。 詳細については、以下の記事を参照してください。

- [サービス接続ポイントについて](../../servers/deploy/configure/about-the-service-connection-point.md)
- [サービス接続ツールの使用](../../servers/manage/use-the-service-connection-tool.md)

Microsoft Intune などのクラウド サービスおよび Windows 10 の新しいバージョンがサポートされるようにするには、Configuration Manager の現在のブランチを定期的に更新する必要があります。 Microsoft では、少なくとも基本レベルの診断および使用状況データを必要としています。 このデータは、製品を最新の状態に保ち、更新プログラムのエクスペリエンスおよび製品の品質とセキュリティを向上させるために使用されます。

サービス接続ポイントがオフライン モードのとき、データはサービスに送信されません。 オンライン モードに切り替えるか、サービス接続ツールを使用すると、データがサービスに送信され、更新プログラムについて確認が行われます。

Configuration Manager によって収集されるデータのレベルを選択することもできます。 詳細については、「[診断と使用状況のデータのレベル](levels-overview.md)」を参照してください。

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> データの保存期間を教えてください。

Microsoft では、Configuration Manager の診断および使用状況のデータを 1 年間保存します。

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a> 設定の実行時に、診断と使用状況データが送信されますか。

できませんね。 診断および使用状況データは、サイトがインストールされて使用できる状態になったら送信されます。

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> データはどのくらいの頻度で送信されますか。

お客様がサイトをインストールした日から 7 日おきに SQL ストアド プロシージャが実行されます。

- オンライン モードでは、クエリの実行後に、サービス接続ポイントからデータがアップロードされます。

- オフライン モードでは、お客様がサービス接続ツールを使用してデータをアップロードします (サイトをインストールしてから 7 日間経過すると、初めてデータをオフラインで使用できるようにはなります)。  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> データを使用してネットワーク マップを作成できますか。

できませんね。 このデータには、IP アドレスや詳細な地理情報など、ネットワークの詳細情報は含まれません。 詳細については、「[診断と使用状況のデータのレベル](levels-overview.md#bkmk_versions)」を参照し、さらに使用しているバージョンの詳細を確認してください。

データには、各サイトからのタイムゾーン情報が含まれます。 この情報により、階層の複数のサイトの広範な位置情報とグローバル分散を理解できます。

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a> カスタム SQL テーブルのデータを確認できますか。

できませんね。 Configuration Manager では、SQL ストアド プロシージャを使用して、診断と使用状況データを収集します。 このストアド プロシージャは、データベースの既定の製品テーブルに対して実行されます。 これらすべての SQL テーブルには、**TEL_** の接頭語が付きます。 SQL スキーマ検出クエリの一部として、すべてのテーブル名は既知の既定値と比較するためにハッシュされます。 この動作により、データベースにカスタム テーブルが存在することが決定されます。 カスタム テーブルの存在を参照することで、Microsoft は、既定のデータベース スキーマが拡張されたこと把握します。 それには、それらのテーブルに格納されるデータは含まれていません。

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a> 他のデータベースは表示できますか。

できませんね。 データを収集するストアド プロシージャは、Configuration Manager サイト データベースに限定されます。 Microsoft は、他のデータベースの名前も、他のデータベース内のデータも表示することはできません。

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a> 他の統合クラウド サービスに送信されるデータはありますか。

それらのサービスを Configuration Manager と統合した場合は、あります。 任意のクラウド サービスとのやりとりの一環として、Configuration Manager から何らかのデータがそのサービスに送信されます。 このデータは、そのクラウド サービスに固有のものであり、Configuration Manager の診断結果および使用状況データとは区別されます。 別のクラウド サービスとのやりとりに使用される固有のデータの詳細については、そのサービスに関するドキュメントを参照してください。

たとえば、次のクラウド サービスは Microsoft Endpoint Manager に含まれています。

- [Desktop Analytics のデータのプライバシー](../../../desktop-analytics/privacy.md)
- [Intune におけるプライバシーと個人データ](/intune/protect/privacy-personal-data)
- [Windows Autopilot の要件](/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a> Configuration Manager では個人データが収集されますか。

できませんね。 構成によって、個人データまたは顧客データが収集または送信されることはありません。 これはお客様が直接展開、管理、操作するオンプレミスの製品です。 Microsoft が収集する診断結果と使用状況データにより、今後のリリースのインストールのエクスペリエンス、品質、セキュリティが向上します。

Configuration Manager のデータの詳細については、「[診断と使用状況のデータのレベル](levels-overview.md)」を参照してください。