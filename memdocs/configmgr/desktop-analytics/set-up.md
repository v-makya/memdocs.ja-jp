---
title: Desktop Analytics の設定
titleSuffix: Configuration Manager
description: Desktop Analytics を設定してオンボードするためのハウツー ガイド。
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: a90f3260782f08fdf8f7424a95e09b34e38e97d3
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268150"
---
# <a name="how-to-set-up-desktop-analytics"></a>Desktop Analytics の設定方法

次の手順に従って、Desktop Analytics にサインインし、サブスクリプション内に構成します。 この手順は、ご自分の組織用に Desktop Analytics を設定するための 1 回限りのプロセスです。  

> [!Important]  
> Configuration Manager での Desktop Analytics に関する一般的な前提条件について詳しくは、「[前提条件](overview.md#prerequisites)」を参照してください。  

## <a name="initial-onboarding"></a>最初のオンボード

1. Microsoft 365 デバイス管理で、**グローバル管理者**ロールを持つユーザーとして、[Desktop Analytics ポータル](https://aka.ms/desktopanalytics)を開きます。 **[スタート]** を選択します。 または、Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースにアクセスし、 **[Desktop Analytics サービス]** ノードを選択して、 **[配置の計画]** を選択します。

2. **[サービス契約に同意する]** ページで、サービス契約を確認し、 **[同意する]** を選択します。  

3. **[サブスクリプションを確認してください]** ページで、必要な使用条件を満たしているライセンスの一覧を確認します。 **[サポート対象のサブスクリプションをお持ちですか?]** の隣で設定を **[はい]** に切り替えてから、 **[次へ]** を選択します。  

4. **[ユーザーにアクセス許可を付与する]** ページで:

    - **[Allow Desktop Analytics to manage Directory roles on your behalf]\(Desktop Analytics による自動的なディレクトリ ロールの管理を許可する\)** :Desktop Analytics によって、**ワークスペースの所有者**に **Desktop Analytics 管理者**ロールが自動的に割り当てられます。 これらのグループが既に**グローバル管理者**である場合、変更はありません。

        このオプションを選択しない場合でも、Desktop Analytics によって、セキュリティ グループのメンバーとしてユーザーが追加されます。 **グローバル管理者**が、ユーザーに **Desktop Analytics 管理者**ロールを手動で割り当てる必要があります。

        Azure Active Directory での管理者ロールのアクセス許可の割り当てと、**Desktop Analytics 管理者**に割り当てられるアクセス許可の詳細については、「[Azure Active Directory での管理者ロールのアクセス許可](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)」を参照してください。  

    - ワークスペースと展開計画を作成して管理するために、Desktop Analytics によって、 **[ワークスペースの所有者]** セキュリティ グループが Azure Active Directory 内に事前構成されます。

        グループにユーザーを追加するには、 **[名前または電子メールアドレスを入力してください]** セクションに名前または電子メール アドレスを入力します。 完了したら **[次へ]** を選択します。

5. **[ワークスペースの設定]** ページで:  

    > [!NOTE]  
    > 次の手順を完了するには、**ワークスペースの所有者**のアクセス許可と、Azure サブスクリプションとリソース グループへの追加のアクセス権が必要です。 詳細については、「[前提条件](overview.md#prerequisites)」を参照してください。  

    - 既存のワークスペースを Desktop Analytics で使用するには、それを選択し、次の手順に進みます。  

        > [!TIP]  
        > Azure AD テナントごとに、1 つの Desktop Analytics ワークスペースのみを使用できます。 デバイスは、1 つのワークスペースにのみ診断データを送信できます。  

    - Desktop Analytics 用のワークスペースを作成するには、 **[ワークスペースの追加]** を選択します。  

        1. グローバルに一意の **[ワークスペース名]** を入力します。

        2. **このワークスペース用の Azure サブスクリプションの名前を選択する**ためのドロップダウン リストから、このワークスペース用の Azure サブスクリプションを選択します。  

        3. リソース グループを **[新規作成]** するか、 **[既存のものを使用]** します。

        4. 一覧から **[リージョン]** を選択し、 **[追加]** を選択します。  

6. 新規または既存のワークスペースを選択し、 **[Set as Desktop Analytics workspace]\(Desktop Analytics ワークスペースとして設定\)** を選択します。  次に、 **[確認してアクセス権を付与する]** ダイアログで **[続行]** を選択します。  

7. 新しいブラウザーのタブで、サインインに使用するアカウントを選択します。 **[組織の代理として同意する]** オプションを選択し、 **[同意する]** を選択します。  

    > [!Note]  
    > この同意は、ワークスペース用の Log Analytics 閲覧者ロールを MALogAnalyticsReader アプリケーションに割り当てるためのものです。 このアプリケーション ロールは、Desktop Analytics で必要です。 詳細については、「[MALogAnalyticsReader アプリケーション ロール](troubleshooting.md#bkmk_MALogAnalyticsReader)」を参照してください。  

8. **[ワークスペースの設定]** ページに戻り、 **[次へ]** を選択します。  

9. **[最後の手順]** ページで、 **[Desktop Analytics に移動]** を選択します。

Azure portal に、Desktop Analytics の **[ホーム]** ページが表示されます。

## <a name="next-steps"></a>次のステップ

次の記事に進み、Configuration Manager を Desktop Analytics に接続します。
> [!div class="nextstepaction"]  
> [Configuration Manager を接続する](connect-configmgr.md)  
