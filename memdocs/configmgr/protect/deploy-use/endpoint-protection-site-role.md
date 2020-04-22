---
title: Endpoint Protection ポイント サイト システムの役割を作成する
titleSuffix: Configuration Manager
description: 構成マネージャー クライアント コンピューターのセキュリティとマルウェアを管理するように Endpoint Protection を構成する方法について説明します。
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a8714f5bacf97e440bae07834ee6df5430a3d37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690320"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Endpoint Protection ポイント サイト システムの役割を作成する

*適用対象:Configuration Manager (Current Branch)*

Endpoint Protection を使用するには、事前に Endpoint Protection ポイント サイト システムの役割をインストールしておく必要があります。 これは、1 つのサイト システム サーバーのみにインストールします。また、中央管理サイトまたはスタンドアロンのプライマリ サイトの階層の最上位にインストールしなければなりません。

Endpoint Protection 用に新しいサイト システム サーバーをインストールするか、または既存のサイト システム サーバーを使用するかに応じて、次のいずれかの手順に従います。
- [新しいサイト システム サーバーにインストールする](#new-site-system-server)
- [既存のサイト システム サーバーにインストールする](#existing-site-system-server)

> [!IMPORTANT]
>  Endpoint Protection ポイントをインストールするときに、Endpoint Protection クライアントは、Endpoint Protection ポイントをホストするサーバーにインストールされます。 サーバーにインストールされている既存のマルウェア対策ソリューションとの共存を有効にするサービスとスキャンは、このクライアント上で無効になっています。 後で Endpoint Protection による管理用にこのサーバーを有効にする際、サードパーティのマルウェア対策ソリューションを削除するオプションを選択しても、サードパーティ製品は削除されません。 サードパーティ製品は手動でアンインストールする必要があります。

## <a name="new-site-system-server"></a>(新しいサイト システム サーバーの場合)

1.  Configuration Manager コンソールで、 **[管理]** をクリックします。

2.  **[管理]** ワークスペースで **[サイトの構成]** を展開して、 **[サーバーとサイト システムの役割]** をクリックします。

3.  **[ホーム]** タブの **[作成]** グループで、 **[サイト システム サーバーの作成]** をクリックします。

4.  **[全般]** ページで、サイト システムの全般設定を指定し、 **[次へ]** をクリックします。

5.  **[システムの役割の選択]** ページの利用可能な役割の一覧で **[Endpoint Protection ポイント]** を選択し、 **[次へ]** をクリックします。

6.  **[Endpoint Protection]** ページで **[Endpoint Protection のライセンス条項に同意します]** チェック ボックスをオンにし、 **[次へ]** をクリックします。

    > [!IMPORTANT]
    >  Endpoint Protection を Configuration Manager で使用するには、ライセンス条項に同意する必要があります。

7.  **[Cloud Protection Service]** ページで、新しい定義の作成に役立つようにマイクロソフトに送信する情報のレベルを選択し、 **[次へ]** をクリックします。

    > [!NOTE]
    >  このオプションで、既定で使用する Cloud Protection Service (旧称: Microsoft Active Protection Service (MAPS)) の設定を構成します。 その後で、作成した各マルウェア対策ポリシーのカスタム設定を構成できます。 Cloud Protection Service に参加すると、常に最新のマルウェア対策定義を提供するのに役立つマルウェア サンプルをマイクロソフトに提供して、コンピューターのセキュリティを強化できます。 また、Cloud Protection Service に参加すると、Endpoint Protection クライアントが動的シグネチャ サービスを使用して、Windows Update に公開される前に新しい定義をダウンロードできます。 詳細については、「[Endpoint Protection のマルウェア対策ポリシーを作成し、展開する方法](endpoint-antimalware-policies.md)」をご覧ください。

8.  ウィザードを完了します。


## <a name="existing-site-system-server"></a>既存のサイト システム サーバー

1.  Configuration Manager コンソールで、 **[管理]** をクリックします。

2.  **[管理]** ワークスペースで **[サイトの構成]** を展開し、 **[サーバーとサイト システムの役割]** をクリックしてから、Endpoint Protection に使用するサーバーを選択します。

3.  **[ホーム]** タブの **[サーバー]** グループで、 **[サイト システムの役割の追加]** をクリックします。

4.  **[全般]** ページで、サイト システムの全般設定を指定し、 **[次へ]** をクリックします。

5.  **[システムの役割の選択]** ページの利用可能な役割の一覧で **[Endpoint Protection ポイント]** を選択し、 **[次へ]** をクリックします。

6.  **[Endpoint Protection]** ページで **[Endpoint Protection のライセンス条項に同意します]** チェック ボックスをオンにし、 **[次へ]** をクリックします。

    > [!IMPORTANT]
    >  Endpoint Protection を Configuration Manager で使用するには、ライセンス条項に同意する必要があります。

7.  **[Cloud Protection Service]** ページで、新しい定義の作成に役立つようにマイクロソフトに送信する情報のレベルを選択し、 **[次へ]** をクリックします。

    > [!NOTE]
    >  このオプションで、既定で使用する Cloud Protection Service (旧称: MAPS) の設定を構成します。 構成した各マルウェア対策ポリシーのカスタム設定を構成できます。 詳細については、「[Endpoint Protection のマルウェア対策ポリシーを作成し、展開する方法](endpoint-antimalware-policies.md)」をご覧ください。

8.  ウィザードを完了します。
