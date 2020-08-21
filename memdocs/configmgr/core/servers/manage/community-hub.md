---
title: コミュニティ ハブと GitHub
titleSuffix: Configuration Manager
description: Configuration Manager のコミュニティ ハブの有効化と使用
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128173"
---
# <a name="community-hub-and-github"></a>コミュニティ ハブと GitHub
<!--3555935, 3555936-->

IT 管理者のコミュニティでは、長年にわたって豊富な知識を作り上げています。 スクリプトやレポートなどの項目を最初から作り直す代わりに、IT 管理者が互いに共有できる **Configuration Manager コミュニティ ハブ**を構築しました。 他のユーザーの作業を活用することで、作業時間を節約できます。 コミュニティ ハブでは、他のユーザーの作業を基礎にし、他のユーザーはあなたの作業を基礎にすることで、創造力が促進されます。 GitHub には、既に共有のために作成された業界標準のプロセスとツールがあります。 コミュニティ ハブでは、この新しいコミュニティを推進するための基本要素として、これらのツールを Configuration Manager コンソールで直接活用します。 最初のリリースでは、コミュニティ ハブで利用できるコンテンツは、Microsoft によってのみアップロードされます。 将来的には、IT 管理者が独自の GitHub アカウントを使用して、自分でコンテンツをアップロードできるようになります。

> [!Note]  
> コミュニティ ハブは、クラウドベースのオプション機能です。 2020 年 6 月に初めて導入されました。 コミュニティ ハブをオプトインする方法の詳細については、[オプション機能](install-in-console-updates.md#bkmk_options)に関する記事をご覧ください。

## <a name="about-community-hub"></a>コミュニティ ハブについて

コミュニティ ハブでは、次のオブジェクトがサポートされています。

- CMPivot クエリ
- アプリケーション
- タスク シーケンス
- 構成項目
- PowerShell スクリプト
- レポート

## <a name="prerequisites"></a>[前提条件]

- コミュニティ ハブへのアクセスに使用する Configuration Manager コンソールを実行するデバイスには、次の項目が必要です。
   - .NET Framework バージョン 4.6 以上
   - Windows 10 ビルド 17110 以上
      - Windows Server はサポートされていないため、Configuration Manager コンソールは、サイト サーバーとは別の Windows 10 デバイスにインストールする必要があります。
   - ログインしたユーザー アカウントをビルトイン管理者アカウントにすることはできません

- Configuration Manager 内の[管理サービス](../../../develop/adminservice/set-up.md)を設定して機能させる必要があります。

- 組織でファイアウォールまたはプロキシ デバイスを使用してインターネットとのネットワーク通信が制限されている場合は、Configuration Manager コンソールによるインターネット エンドポイントへのアクセスを許可する必要があります。 詳細については、「[Internet access requirements (インターネット アクセスの要件)](../../plan-design/network/internet-endpoints.md#community-hub)」を参照してください。

## <a name="permissions"></a>アクセス許可

- スクリプトをインポートするには**SMS_Scripts** クラスに対するアクセス許可を**作成**します。
- レポートをインポートするには完全な権限持つ管理者のセキュリティ ロール。


## <a name="use-the-community-hub"></a>コミュニティ ハブを使用する

1. **[コミュニティ]** ワークスペースの **[コミュニティ ハブ]** ノードに移動します。
1. ダウンロードする項目を選択します。
1. ハブからオブジェクトをダウンロードして、サイトにインポートするには、ご利用の Configuration Manager サイトの適切なアクセス許可が必要になります。
    - スクリプトをインポートするにはSMS_Scripts クラスに対するアクセス許可を**作成**します。
    - レポートをインポートするには完全な権限持つ管理者のセキュリティ ロール。
1. ダウンロードされたレポートは、レポート サービス ポイントで **[ハブ]** というレポート フォルダーに展開されます。 ダウンロードされたスクリプトは、 **[実行スクリプト]** ノードに表示される場合があります。
1. お客様の組織がハブからダウンロードしたすべての項目を表示するには、 **[コミュニティ ハブ]** ノードから **[Your downloads]\(ダウンロード\)** をクリックします。

[![コミュニティ ハブからダウンロードされたすべての項目](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> コミュニティ ハブの項目への直接リンク
<!--4224406-->
" *(バージョン 2006 で導入)* " 直接リンクを使用すると、Configuration Manager コンソールのコミュニティ ハブ ノードの項目に簡単に移動したり、参照したりできます。 この機能の目的は、コラボレーションを簡単にし、コミュニティ ハブの項目へのリンクを同僚と共有できるようにすることです。 現在、これらのディープ リンクは、コンソールのコミュニティ ハブ ノードの項目に対してのみ使用できます。

### <a name="prerequisites-for-direct-links"></a>直接リンクの前提条件

- Configuration Manager コンソール バージョン 2006 以降
- コミュニティ ハブのリンクに従っている場合、ローカルのビルトイン管理者アカウントを使用することはできません。

### <a name="sharing-and-opening-direct-links"></a>直接リンクを共有および開く

項目を共有するには:
1. ハブの項目にアクセスし、 **[共有]** を選択します。
1. コピーしたリンクを貼り付けて、他のユーザーと共有します。

共有リンクを開くには:
1. Configuration Manager コンソールがインストールされているコンピューターからリンクをクリックします。
   - たとえば、このリンクを使用して、[Edge の自動更新を構成するスクリプト](https://communityhub.microsoft.com/item/7200) (`https://communityhub.microsoft.com/item/7200`) を共有できます。
1. プロンプトが表示されたら、 **[Launch the Community hub]\(コミュニティ ハブの起動\)** を選択します。
1. コンソールによって、コミュニティ ハブのスクリプトが直接開かれます。

## <a name="known-issues"></a><a name="bkmk_known"></a> 既知の問題

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>別のユーザーとしてコンソールを実行しているときに、コミュニティ ハブ ノードにアクセスできない
<!--7826897-->
権限の低いユーザーとしてサインインし、 **[別のユーザー として実行]** を選択して Configuration Manager コンソールを開いた場合、**コミュニティ ハブ** ノードにアクセスできない可能性があります。

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>ダウンロードされたレポートがダウンロード ページから削除されない
<!--7851305-->
ダウンロードしたレポートを **[監視]**  >  **[レポート]** ノードから削除した場合、レポートは **[コミュニティ ハブ]**  >  **[Your downloads]\(ダウンロード\)** ページから削除されず、レポートを再度ダウンロードすることはできません。 

## <a name="next-steps"></a>次のステップ

次のオブジェクトの作成および使用方法の詳細を学習します。

- [PowerShell スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)
- [レポートの概要](introduction-to-reporting.md)
- [タスク シーケンスの作成と管理](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [アプリケーションの作成と展開](../../../apps/get-started/create-and-deploy-an-application.md)
- [構成アイテムの作成](../../../compliance/deploy-use/create-configuration-items.md)