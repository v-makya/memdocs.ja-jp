---
title: OS アップグレード パッケージの管理
titleSuffix: Configuration Manager
description: Configuration Manager での OS アップグレード パッケージの管理方法について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc50fc60601b63bca7b4a4b01ba3fb4a39fd8b91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708870"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Configuration Manager で OS アップグレード パッケージを管理する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の OS アップグレード パッケージには、コンピューターの既存の OS をアップグレードする Windows セットアップのソース ファイルが含まれています。 この記事では、OS アップグレード パッケージを追加、配布、およびサービスを提供する方法について説明します。

> [!NOTE]
> OS アップグレード パッケージは、Windows の新規インストールのためにも使用できます。 ただし、これはこの方法と互換性があるドライバーに依存しています。 OS アップグレード パッケージから Windows の新規インストールを実行する場合、ドライバーは、単純に Windows PE にいる間に挿入されるのと比較して、Windows PE にいる間にインストールされます。 一部のドライバーは、Windows PE にいる間のインストールと互換性がありません。 ドライバーが Windows PE にいる間のインストールと互換性がない場合は、代わりに **install.wim** などの [OS イメージ](manage-operating-system-images.md)を使います。

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a> OS アップグレード パッケージを追加する  

OS アップグレード パッケージを使用するには、最初にご使用の Configuration Manager サイトにパッケージを追加します。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[オペレーティング システム]** を展開して、 **[オペレーティング システム アップグレード パッケージ]** ノードを選択します。  

2. リボンの **[ホーム]** タブの **[作成]** グループで、 **[オペレーティング システム アップグレード パッケージの追加]** を選択します。 このアクションにより、オペレーティング システム アップグレード パッケージの追加ウィザードが開始されます。  

3. **[データ ソース]** ページで、次の設定を行います。

    - OS アップグレード パッケージのインストール ソース ファイルへのネットワーク**パス**。 たとえば、`\\server\share\path` となります。  

        > [!NOTE]  
        >  インストール ソース ファイルには、OS をインストールするための setup.exe やその他のファイルとフォルダーが含まれています。  

        > [!IMPORTANT]  
        >  不要な改ざんを防ぐため、これらのインストール ソース ファイルへのアクセスを制限します。  

    - **選択したアップグレード パッケージの install.wim ファイルから特定のイメージ インデックスを抽出**し、次にイメージ インデックスを一覧から選択します。<!--4931110--> バージョン 1910 以降では、このオプションにより、ファイル内のすべてのイメージ インデックスではなく、1 つのインデックスが自動的にインポートされます。 このオプションを使用すると、イメージ ファイルが小さくなり、オフライン サービスが高速になります。 さらに、ソフトウェア更新プログラムの適用後に小さくなったイメージ ファイルに対して、[イメージ サービスを最適化する](#bkmk_resetbase)プロセスもサポートされます。  

        > [!IMPORTANT]  
        > Configuration Manager では、OS アップグレード パッケージ内の既存の install.wim が上書きされます。 イメージ インデックスが一時的な場所に抽出されてから、元のソース ディレクトリに移動されます。 OS アップグレード パッケージをインポートしてこのオプションを有効にする前に、元のソース ファイルをバックアップしてください。

    - クライアントでコンテンツを事前キャッシュする場合は、イメージの**アーキテクチャ**と**言語**を指定します。 詳細については、「[コンテンツの事前キャッシュを構成する](../deploy-use/configure-precache-content.md)」を参照してください。  

4. **[全般]** ページで、以下の情報を指定します。 この情報は、複数の OS アップグレード パッケージがあるときに区別するのに役立ちます。  

    - **名前**:OS アップグレード パッケージの一意の名前。  

    - **バージョン**:省略可能なバージョン識別子。 このプロパティは、アップグレード パッケージの OS バージョンにする必要はありません。 多くの場合は、パッケージの組織のバージョンです。  

    - **コメント**:省略可能な簡単な説明。  

5. ウィザードを完了します。  

次に、配布ポイントに OS アップグレード パッケージを配布します。  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a> 配布ポイントにコンテンツを配布する  

他のコンテンツと同じように、配布ポイントに OS アップグレード パッケージを配布します。 タスク シーケンスを展開する前に、少なくとも 1 つの配布ポイントに OS アップグレード パッケージを配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)」をご覧ください。  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>次のステップ

[OS をアップグレードするタスク シーケンスの作成](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
