---
title: ユーザーへのアプリ展開のテクニカル リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager でのユーザーへのアプリケーション展開に関するテクニカル リファレンスです。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690270"
---
# <a name="application-deployment-policy-for-users"></a>ユーザー向けアプリケーション展開ポリシー

*適用対象:Configuration Manager (Current Branch)*

アプリケーションをユーザー コレクションに展開する場合、展開のポリシーは、必要な展開に対してのみ作成されます。 利用可能な展開の場合、ユーザーがソフトウェア センターからアプリケーションをインストールしようとすると、ポリシーが作成されます。 この記事では、必要な展開と、利用可能な展開の両方のプロセスについて説明します。

> [!TIP]
> クライアント ログを確認するために必要なすべての情報は、[始める前に](app-deployment-technical-reference.md#before-you-begin)セクションで参照されている SQL クエリを実行することで取得できます。

## <a name="required-deployments"></a>必要な展開

ユーザー コレクションに対する必要なアプリケーション展開のポリシーは、展開の作成時にコレクション内のすべてのユーザーを対象とします。 これらの展開のクライアント側の処理は、デバイス コレクションへの必要な展開に似ています。 展開のアクティブ化は、定義された利用可能な時間に実行され、強制は定義された期限の時間に実行されます。 詳細については、[デバイス コレクションへのアプリケーションの展開](device-deployment-technical-reference.md)をご覧ください。

## <a name="available-deployments"></a>利用可能な展開

ユーザー コレクションに利用可能として展開されているアプリケーションの動作は異なります。 この動作の違いにより、管理者はポリシーのリソースの競合を発生させることなく、ユーザーがアプリケーションを使用できるようにすることができます。 ユーザーがソフトウェア センターを起動すると、ユーザーが使用できるアプリケーションの一覧が、管理ポイントからリアルタイムで照会されます。 この要求は、管理ポイントの `CMUserService_WindowsAuth` 仮想ディレクトリに対して行われ、**SCClient_[UserName].log** クライアントで確認できます。

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

管理ポイントがこの要求を受け取ると、`usp_GetApplicationPropertyValuesFiltered` ストアド プロシージャを実行して、ユーザーが使用できるアプリケーションの一覧に対してクエリを実行します。 このアクティビティは、管理ポイントの **UserService.log** で追跡できます。

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

ソフトウェア センターは一覧を受け取り、ユーザーがインストールできるアプリケーションを表示します。 ユーザーがアプリケーションをクリックすると、アプリケーションに関する追加情報が管理ポイントから照会されます。これには、usp_GetApplicationInfo、usp_GetAppModelApplicationSupersedence、usp_GetDeploymentTypeForAnApp などのストアド プロシージャの実行が含まれます。

展開は、ユーザーがアプリケーションを選択し、 **[インストール]** ボタンをクリックして、アプリケーションを評価する DCM エージェント ジョブが作成されたときにアクティブ化されます。 アプリケーションが適用可能な場合は、アプリケーションをダウンロードして適用するための別の DCM エージェント ジョブが作成されます。 このアクティビティは、クライアントの **DCMAgent.log** で追跡できます。

## <a name="next-steps"></a>次のステップ

- [アプリケーション展開クライアント コンポーネントを理解する](client-components-technical-reference.md)
