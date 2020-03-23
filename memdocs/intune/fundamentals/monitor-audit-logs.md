---
title: Microsoft Intune で変更とイベントを監査する - Azure | Microsoft Docs
description: Microsoft Intune のアクティビティを記録する監査ログを確認する方法について説明します。
keywords: ''
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 03/18/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a9d3ed650f9c366778427cee2f525dc6d9d90f9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79357949"
---
# <a name="use-audit-logs-to-track-and-monitor-events-in-microsoft-intune"></a>監査ログを使用し、Microsoft Intune のイベントを追跡し、監視する

監査ログには、Microsoft Intune で変更を行うアクティビティが含まれています。 ほとんどの Intune ワークロードについて管理者が確認できる監査イベントは、作成、更新 (編集)、削除、割り当て、リモートの操作によって作成できます。 既定では、すべてのお客様に対して監査が有効です。 無効にすることはできません。

> [!NOTE]
> 監査イベントは、2017 年 12 月の機能リリースで記録が開始されました。 それ以前のイベントは入手できません。

## <a name="who-can-access-the-data"></a>データにアクセスできるユーザー

次のアクセス許可を持つユーザーが監査ログを確認できます。

- グローバル管理者
- Intune サービス管理者
- **監査データ** - **読み取り**アクセス許可を持つ、Intune ロールに割り当てられた管理者

## <a name="audit-logs-for-intune-workloads"></a>Intune ワークロードの監査ログ

各 Intune ワークロードの監視グループで監査ログを確認できます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[テナント管理]**  >  **[監査ログ]** を選択します。
3. 結果をフィルター処理するには、 **[フィルター]** を選択し、次のオプションを使用して結果を絞り込みます。
    - **[カテゴリ]** : **[コンプライアンス]** 、 **[デバイス]** 、 **[ロール]** などです。
    - **[アクティビティ]** : ここに一覧表示されるオプションは、 **[カテゴリ]** で選択したオプションによって制限されます。
    - **[日付の範囲]** : 過去の月、週、または日のログを選択できます。
4. **[適用]** を選択します。
4. アクティビティの詳細を見るには、リストで項目を選択します。

## <a name="route-logs-to-azure-monitor"></a>ログを Azure Monitor にルーティングする

監査ログと操作ログは Azure Monitor に転送することもできます。 **[監査ログ]** で **[データ設定のエクスポート]** を選択します。

![Intune で [データ設定のエクスポート] を選択し、Azure Monitor にログ データをエクスポートします。](./media/monitor-audit-logs/audit-logs-export-data-settings.png)

> [!NOTE]
> この機能の詳細と、それを使用するための前提条件については、[ストレージ、イベント ハブ、または Log Analytics へのログ データの送信](review-logs-using-azure-monitor.md)に関するページを参照してください。

> [!NOTE]
> **開始者 (アクター)** には、タスクの実行者と、実行された場所についての情報が含まれます。 たとえば、Azure portal で Intune のアクティビティを実行する場合、 **[アプリケーション]** には常に **[Microsoft Intune portal extension]\(Microsoft Intune ポータル拡張機能\)** が表示され、 **[アプリケーション ID]** には常に同じ GUID が使用されます。
>
> **[ターゲット]** セクションには、複数のターゲットとその変更されたプロパティが一覧表示されます。  

## <a name="use-graph-api-to-retrieve-audit-events"></a>Graph API を使用した監査イベントの取得

Graph API を使用した、最長 1 年間の監査イベントを取得に関する詳細については、「[auditEvents のリスト](https://docs.microsoft.com/graph/api/intune-auditing-auditevent-list?view=graph-rest-1.0)」を参照してください。

## <a name="next-steps"></a>次のステップ

[Intune でストレージ、イベントハブ、または Log Analytics にログ データを送信する (プレビュー)](review-logs-using-azure-monitor.md)。

[クライアント アプリの保護ログを確認します](../apps/app-protection-policy-settings-log.md)。
