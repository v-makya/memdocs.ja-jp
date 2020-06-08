---
title: Desktop Analytics のデータのプライバシー
titleSuffix: Configuration Manager
description: Desktop Analytics では、顧客データのプライバシーは確実に保護されています
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 82c8495391dcc22aa2784657bc1461887e412577
ms.sourcegitcommit: 7b8921d3ea6a751de67315771d68e2d2750fa36f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223647"
---
# <a name="desktop-analytics-data-privacy"></a>Desktop Analytics のデータのプライバシー

Desktop Analytics では、以下の信条を軸として、顧客データのプライバシー保護が確約されています。

- **透明性:** Windows 診断イベントは、完全に文書化されます。 会社のセキュリティおよびコンプライアンス チームと共にそれらをレビューしてください。 Windows 診断データ ビューアーを使用して、特定のデバイスから送信された診断データを確認できます。 詳細については、「[診断データ ビューアーの概要](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview)」を参照してください。  

- **制御:** Microsoft と共有する診断データのレベルは、ユーザーが制御します。 Windows 10 バージョン 1709 には、より詳細な診断データの送信を、Desktop Analytics で必要とされる最小限のものに制限する新しいポリシーが追加されています。  

- **セキュリティ:** Microsoft では、お客様のデータを強力なセキュリティと暗号化を使用して保護します。  

- **信頼:** Desktop Analytics では、Microsoft の[プライバシーに関する声明](https://privacy.microsoft.com/privacystatement)と[オンライン サービス利用条件](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)がサポートされています。  

詳細については、[GDPR の下で Microsoft が処理者である Windows サービス](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr)に関する記事を参照してください。<!-- 5353168 -->

## <a name="data-flow"></a>データ フロー

次の図は、個々のデバイスから診断データが Diagnostic Data Service、一時的なストレージ、Log Analytics ワークスペースをどのように経由して流れていくかを示しています。

![デバイスからの診断データのフローを示す図](media/da-data-flow.png)

1. Azure portal にサインインし、Desktop Analytics にオンボードします。 Configuration Manager を使用して接続する Azure AD アプリを作成します。 Desktop Analytics を設定するときに、任意の場所に Azure Log Analytics ワークスペースを作成します。  

2. Configuration Manager に接続してデバイスを登録します。  

    1. Azure AD アプリの詳細を使用して、Configuration Manager に Desktop Analytics クラウド サービスを構成します。  

    2. 15 分以内に、Configuration Manager により、テナント ID を使用して次のデータが Desktop Analytics と同期されます。 このプロセスは、1 時間ごとに繰り返されます。

      - [展開計画の作成](create-deployment-plans.md)に必要なデバイス コレクションに関する情報。 この情報には、コレクション ID、階層 ID、コレクション名、デバイス数が含まれます。 
      - [デバイスの登録](enroll-devices.md)に必要な情報。 この情報には、コレクション ID、SMS 一意識別子、OS ビルド バージョン、デバイス名、シリアル番号が含まれます。
      - [接続の正常性の監視](monitor-connection-health.md)ダッシュボードの情報。 この情報には、正常性状態ごとのデバイスの数と、デバイスのプロパティが含まれます。
      - 展開計画に関する情報。これには、コレクション ID、展開 ID、パイロットまたは運用環境の展開の種類、アップグレードごとのデバイス数の決定が含まれます。

    3. Configuration Manager によって、デバイスの商用 ID、診断データ レベル、およびその他の設定が、ターゲット コレクション内に設定されます。 この構成によって、デバイスが Desktop Analytics ワークスペースに表示されます。  

    4. すべてのターゲット デバイスに、互換性更新プログラムを展開します。  

3. デバイスによって、診断データが Windows の Microsoft 診断データ管理サービスに送信されます。 すべての診断データは HTTPS 経由で暗号化され、デバイスからこのサービスへの転送中は証明書のピン留めを使用します。 Microsoft Data Management Service は米国でホストされています。

4. Microsoft は、毎日、IT に焦点を絞った分析情報のスナップショットを作成します。 このスナップショットは、Windows の診断データと、登録されているデバイスの入力の組み合わせです。 このプロセスは一時的なストレージで発生し、Desktop Analytics によってのみ使用されます。 一時的なストレージは、米国の Microsoft データセンターでホストされます。 すべてのデータは、SSL (HTTPS) で暗号化されたチャネルを介して送信されます。 スナップショットは、商用 ID によって分離されます。  

5. 次に、スナップショットがご利用の Azure Log Analytics ワークスペースにコピーされます。 このデータ転送は、Log Analytics の機能である Webhook インジェスト プロトコルを使用して HTTPS 経由で行われます。 Desktop Analytics には、Log Analytics ストレージに対する読み取りまたは書き込みのアクセス許可がありません。 Desktop Analytics により、Shared Access Signature (SAS) URI を使用して Webhook API が呼び出されます。 次に、Log Analytics により、HTTPS 経由でストレージ テーブルからデータが取得されます。

6. Desktop Analytics によって、入力内容が Log Analytics ストレージに格納されます。 これらの構成には、展開計画と、資産のアップグレードと重要度に関する決定が含まれます。  

## <a name="other-resources"></a>その他のリソース

Desktop Analytics のプライバシー関連のよく寄せられる質問については、[プライバシーに関する FAQ](faq.md#privacy)を参照してください。

関連するプライバシー面の詳細については、次の記事を参照してください。

- [IT 意思決定者向けの Windows 10 と GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7、Windows 8、および Windows 8.1 Appraiser の診断データ イベントとフィールド](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10 バージョン 1809 の基本レベルの Windows 診断イベントとフィールド](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows Analytics で使用される Windows 10 バージョン 1709 の拡張診断データ イベントとフィールド](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [診断データ ビューアーの概要](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [ライセンス条項とドキュメント](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Log Analytics データ セキュリティ](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Microsoft Azure データセンターのセキュリティとプライバシー](https://azure.microsoft.com/global-infrastructure/)  

- [信頼できるクラウドであるという自信](https://azure.microsoft.com/overview/trusted-cloud/)  

- [セキュリティ センター](https://www.microsoft.com/trustcenter)  

- [プライバシー シールド](https://www.privacyshield.gov/)  

Desktop Analytics とは別に、Configuration Manager では、診断および使用状況データが Microsoft に送信されます。 このデータは、Configuration Manager の今後のリリースでインストールのエクスペリエンス、品質、セキュリティを向上させるために Microsoft によって使用されます。 詳細については、[Configuration Manager の診断結果と使用状況データ](../core/plan-design/diagnostics/diagnostics-and-usage-data.md)に関するページをご覧ください。
