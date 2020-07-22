---
title: Role-based Administration Tool
titleSuffix: Configuration Manager
description: Role-based Administration and Auditing Tool を使用して、Configuration Manager のセキュリティ ロールとスコープをモデル化し、監査します。
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4cf9d4d3f9d1b2f439d2e87d41cc280e7af0805a
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86239710"
---
# <a name="role-based-administration-and-auditing-tool"></a>Role-based Administration and Auditing Tool

*適用対象:Configuration Manager (Current Branch)*

Role-based Administration and Auditing Tool は、[Configuration Manager ツール](tools.md)の 1 つです。 このツールは、次のタスクに使用します。

- 特定のアクセス許可を持つセキュリティ ロールをモデル化する  

- 他のユーザーが持っているセキュリティ スコープとセキュリティ ロールを監査する



## <a name="requirements"></a>要件

- Configuration Manager サイト サーバーと同じコンピューターで実行します 

- **完全な権限を持つ管理者**、**読み取り専用アナリスト**、または**セキュリティ管理者**のロールを持っています  

- **すべての**セキュリティ スコープとすべてのコレクションにアカウントを割り当てます  

- (*省略可能*) レポート フォルダーのセキュリティを分析するには、SQL のアクセス権が必要です  

- (*省略可能*) レポートのドリルスルーを分析するには、レポート ポイント ロールを使用してサイト システム サーバー上でこのツールを実行します



## <a name="procedures"></a>手順


### <a name="model-permissions-for-a-new-role"></a>新しいロールのアクセス許可をモデル化する

作成する新しいロールのアクセス許可をモデル化するには、次の手順を実行します。 

1. **RBAViewer.exe** を実行します。  

2. 構築する基本のセキュリティ ロールを選択するか、空のアクセス許可セットから開始します。 必要なアクセス許可を選択します。  

3. **[分析]** をクリックすると、このカスタム ロールに表示されるユーザー インターフェイスが表示されます。  

    > [!Note]  
    > 要件に合った既存のセキュリティ ロールが存在するかどうかを確認するには、 **[Similarity]\(類似性\)** タブに切り替えます。  

4. ロールを XML ファイルとして保存するには、 **[エクスポート]** をクリックします。 Configuration Manager コンソールにインポートします。 詳細については、「[カスタム セキュリティ ロールの作成](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)」をご覧ください。


### <a name="audit-existing-security-scopes"></a>既存のセキュリティ スコープを監査する

Configuration Manager の既存の管理ユーザー、コレクション、およびセキュリティ スコープをすべて監査するには、次の手順を実行します。

1. **RBAViewer.exe** を実行します。  

2. ツール バーの **[Audit RBA]\(RBA の監査\)** ボタンを選択します。  

    1. コレクション限定の関係をツリー ビューで表示するには、 **[Collection Summary]\(コレクションの概要\)** タブに切り替えます。  

    2. セキュリティ ロールに割り当てられたオブジェクトを表示するには、 **[スコープの概要**] タブに切り替えます。  


### <a name="audit-a-specific-user"></a>特定のユーザーを監査する

特定のユーザーについてロールベース管理構成を監査するには、次の手順を実行します。

1. **RBAViewer.exe** を実行します。  

2. ツールバーの **[実行者]** ボタンを選択します。  

3. 特定のユーザー名を入力して、そのアカウントのアクセス許可を確認します。  

4. このツールでは、ユーザーまたはユーザーが属するセキュリティ グループに割り当てられたセキュリティ ロールが表示されます。 また、このユーザーが表示できるオブジェクトと、コンソールで実行できるアクションも表示されます。  



## <a name="see-also"></a>関連項目

- [ロール ベース管理の基礎](../understand/fundamentals-of-role-based-administration.md)
- [ロール ベース管理の構成](../servers/deploy/configure/configure-role-based-administration.md)
