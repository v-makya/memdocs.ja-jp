---
title: アプリケーション展開ポリシーに関するテクニカル リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager でのアプリケーション展開ポリシーのトラブルシューティングに関するテクニカル リファレンスです。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688830"
---
# <a name="application-deployment-policy"></a>アプリケーション展開ポリシー

*適用対象:Configuration Manager (Current Branch)*

## <a name="policy-creation"></a>ポリシーの作成

アプリケーションを展開すると、アプリケーションのコレクションへの割り当てを表す [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) クラスのインスタンスが作成されます。 このアクティビティは **SMSProv.log** で追跡できます。

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

Configuration Manager データベースでは、この情報は `CI_CIAssignments` テーブルに格納されます。`AssignmentType` 2 はアプリケーションの展開を表します。 割り当てが作成されると、SMS データベース モニター コンポーネントによってテーブル内の変更が検出され、オブジェクト レプリケーション マネージャーに対して CI 割り当て (CIA) ポリシーを処理するように通知されます。 次に、オブジェクト レプリケーション マネージャー コンポーネントがデータベース内のアプリケーションの割り当てのポリシーを作成します。このポリシーは、データベースの `Policy` テーブルに格納され、ポリシー ID はアプリケーションの一意な ID に基づいています。 このアクティビティは、[作業を開始する準備](app-deployment-technical-reference.md#before-you-begin)に関するセクションで参照されている SQL クエリから取得できる割り当ての一意な ID を参照して **objreplmgr.log** で追跡できます。

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

アプリケーション割り当てのポリシーは、データベースで次のような SQL クエリを使用して確認できます。

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>ポリシーのターゲット設定

ポリシー プロバイダー コンポーネントは、ポリシーが生成された後、このポリシーをアプリケーション展開の対象となるコレクション内のリソースに割り当てます。 ポリシーのターゲット設定情報は、データベースの `ResPolicyMap` テーブルに格納されます。 上記のクエリによって返された PADBID を使用して、**policypv.log** でこのアクティビティを追跡できます。 ただし、複数のポリシーが同時に処理されている場合、ログに記録された PADBID は、上記のクエリによって返される PADBID と常に一致するとは限りません。

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap` テーブルには、ユーザー コレクションに**使用可能**として展開されるアプリケーションのターゲット情報は含まれていません。 ソフトウェア センターでは、これらのアプリケーションの一覧を管理ポイントから照会します。これらのアプリケーションのポリシー ターゲット情報は、ユーザーがソフトウェア センターからアプリケーションを要求したときに動的に生成されます。

## <a name="next-steps"></a>次のステップ

- [デバイス コレクションへのアプリケーションの展開](device-deployment-technical-reference.md)
- [ユーザー コレクションへのアプリケーションの展開](user-deployment-technical-reference.md)
