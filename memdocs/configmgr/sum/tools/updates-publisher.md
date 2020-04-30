---
title: Updates Publisher
titleSuffix: Configuration Manager
description: System Center Updates Publisher を使用して、カスタム更新プログラムを管理する
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700030"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*適用対象:System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) は、独立系ソフトウェア ベンダーまたは基幹業務アプリケーション開発者によるカスタム更新プログラムの管理を可能にするスタンドアロン ツールです。 このカスタム更新プログラムの管理には、ドライバーと更新プログラムのバンドルなどの依存関係のある更新プログラムが含まれています。

Updates Publisher を使用すると、次の操作が行えます。

-   外部カタログからの更新プログラムのインポート (Microsoft 以外の更新カタログ)。
-   適用性や展開メタデータなどの更新定義の変更。
-   外部カタログへの更新プログラムのエクスポート。
-   更新サーバーへの更新プログラムの公開。

更新サーバーに更新プログラムを公開した後に、Configuration Manager を使用することで、これらの更新プログラムを検出し、マネージド デバイスに展開できます。

## <a name="workspaces"></a>ワークスペース
Updates Publisher を開くと、 *[更新プログラム] ワークスペース*の概要ノードが既定として設定されています。

![Updates Publisher コンソール](media/console1.png)


Updates Publisher には、整理に役立つ 4 つのワークスペースがあります。


**[更新プログラム] ワークスペース:** このワークスペースは、ソフトウェア更新プログラムの[作成](create-updates-with-updates-publisher.md)と[管理](manage-updates-with-updates-publisher.md)、バンドルの更新などに使用します。 このワークスペースには、パブリケーションへの更新プログラムとバンドルの割り当て、公開、別の Updates Publisher のリポジトリへのエクスポートなどが含まれています。

**[パブリケーション] ワークスペース:** このワークスペースでは、[パブリケーションを管理](updates-publisher-publications.md)します。 パブリケーションは作成した更新プログラムのグループで、更新プログラムのエクスポートと公開を簡略化します。

パブリケーションの管理には、更新プログラムをサーバに公開してクライアントが更新プログラムを見つけてインストールできること、他の Updates Publisher によるインストール用途のために更新プログラムとバンドルをエクスポートすること、またはパブリケーションのコンテンツや詳細を変更することなどが含まれています。

**[動作規則] ワークスペース:** ここでは、[適用規則を管理](updates-publisher-applicability-rules.md)します。この規則は保存でき、展開した更新プログラムと共に使用できます。 規則には以下の 2 種類があります。

-   インストール可能な規則 – この規則は、クライアントによる更新プログラムのインストールの判断に役立ちます。
-   インストール済みの規則 – この規則は、更新プログラムが既にインストールされていることを確認します。

**[カタログ] ワークスペース:** このワークスペースは、[ソフトウェアの更新カタログの管理](updates-publisher-catalogs.md)と追加に使用します。 このワークスペースには、カタログから Updates Publisher のリポジトリへのソフトウェアの更新プログラムのインポートが含まれます。

## <a name="whats-new-in-system-center-updates-publisher"></a>System Center Updates Publisher の新機能

>[!NOTE] 
> 最新バージョンの System Center Updates Publisher は、2019 年 11 月 6 日にリリースされました。 詳細については、「[リリース履歴](#release-history)」セクションを参照してください。

更新プログラムの作成に役立つ新しい作成モード System Center Updates Publisher が用意されています。 作成モードを有効にすると、スタート画面に **[カテゴリ ワークスペース]** が追加されます。 作成モードが有効になっている場合、新しい **[Detectoid]** ボタンが **[更新プログラム ワークスペース]** にも追加されます。

### <a name="to-enable-authoring-mode"></a>作成モードを有効にするには

1. コンソールの左上隅で、 **[Updates Publisher]** **[プロパティ]** タブを開き、 **[オプション]** を選択します。
1. **[作成]** オプションにアクセスします。
1. **[作成モードを有効にする]** チェックボックスをオンにします。

![Updates Publisher の作成モードを有効にする](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>カテゴリ ワークスペースについて

カテゴリ ワークスペースを使用すると、更新作成者は、一緒に属する更新を整理できます。 たとえば、OEM の場合は、モデルまたは製品ラインに基づいて更新プログラムを整理することができます。 複数のカテゴリおよび子カテゴリを定義できますが、2 つのレベルに制限されているので、孫カテゴリは定義できません。

![カテゴリ ワークスペースのスクリーンショット](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>更新プログラムをカテゴリに割り当てる

更新プログラムを作成したら、その更新プログラムを選択し、 **[分類]** ボタンをクリックして、カテゴリに割り当てることができます。 また、更新プログラムを右クリックし、 **[分類]** を選択することもできます。

![更新プログラムの分類のスクリーンショット](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>detectoid について

作成モードを有効にすると、更新プログラムの detectoid を作成できます。 detectoid は、同じ規則 (または一連の規則) を使用して適用性を決定する複数の更新プログラムがある場合に便利です。 これらのインスタンスでは、detectoid を作成し、更新プログラムの前提条件として割り当てます。 作成した更新プログラムには、複数の detectoid を割り当てることができます。


### <a name="create-a-detectoid"></a>detectoid の作成

1. **[更新プログラム] ワークスペース**を開きます。
1. リボンで、 **[Detectoid]** ボタンをクリックします。
1. ウィザードの指示に従って、detectoid を作成します。



![detectoid を使用した前提条件の更新](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>リリース履歴

- [2019 RTW バージョン 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111)。 リリース日: 2019 年 11 月 6 日
- [KB4462765 からの更新プログラムのロールアップ バージョン 6.0.283.0](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher)。 リリース日: 2018 年 9 月 7 日。
- [2017 RTW バージョン 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986)。 リリース日: 2018 年 3 月 26 日。


## <a name="next-steps"></a>次のステップ
作業を始めるには、まず Updates Publisher の[インストール](install-updates-publisher.md)とオプションの[構成](updates-publisher-options.md)を行います。
