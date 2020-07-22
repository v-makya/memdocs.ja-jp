---
title: コミュニティ ハブと GitHub
titleSuffix: Configuration Manager
description: Configuration Manager のコミュニティ ハブの有効化と使用
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8aadc391c5c0b259ab1a1736f3654f25b98dbae0
ms.sourcegitcommit: aa876a9b5aa9437ae59a68e1cc6355d7070f89f4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86236411"
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

- レポートをダウンロードするには、インポートするサイトで **[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** オプションをオンにする必要があります。 詳細については、「[拡張 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)」を参照してください。
   1. **[管理]**  >  **[サイトの構成]**  >  **[サイト]** の順に移動します。
   1. サイトを選択して、リボンの **[プロパティ]** を選択します。
   1. **[通信のセキュリティ]** タブで、 **[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** オプションを選択します。

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


## <a name="next-steps"></a>次のステップ

次のオブジェクトの作成および使用方法の詳細を学習します。

- [PowerShell スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)
- [レポートの概要](introduction-to-reporting.md)
- [タスク シーケンスの作成と管理](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [アプリケーションの作成と展開](../../../apps/get-started/create-and-deploy-an-application.md)
- [構成アイテムの作成](../../../compliance/deploy-use/create-configuration-items.md)