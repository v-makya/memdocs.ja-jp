---
title: ユーザー補助
titleSuffix: Configuration Manager
description: すべての人に Configuration Manager を利用してもらうための機能について説明します。
ms.date: 05/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a6e406d55524caca71bf75b087c9fd78a470c939
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699383"
---
# <a name="accessibility-features-in-configuration-manager"></a>Configuration Manager でのユーザー補助機能

*適用対象:Configuration Manager (Current Branch)*


Configuration Manager には、すべての人に利用してもらうための機能があります。

> [!Note]  
> バージョン 1902 以降では、Configuration Manager コンソールのユーザー補助機能向上のため、コンソールが実行されているコンピューターの .NET がバージョン 4.7 以降に更新されます。 <!-- SCCMDocs-pr issue #3228 -->  
> 
> .NET 4.7.1 および 4.7.2 で行われたユーザー補助の変更について詳しくは、「[.NET Framework のアクセシビリティの新機能](/dotnet/framework/whats-new/whats-new-in-accessibility)」をご覧ください。  



## <a name="keyboard-shortcuts"></a>キーボード ショートカット

### <a name="console-workspaces"></a>コンソール ワークスペース

次のショートカット キーを使用して、ワークスペースにアクセスできます。  

|ショートカット キー| ワークスペース|
|--------|--------|  
|Ctrl + 1| 資産とコンプライアンス|
|Ctrl + 2|  ソフトウェア ライブラリ|
|Ctrl + 3|  監視|
|Ctrl + 4|  管理|


### <a name="other-console-shortcuts"></a>その他のコンソール ショートカット

|ショートカット キー|  目的|
|--------|--------|  
|Ctrl + M|フォーカスをメイン (中央) ウィンドウに設定します。|
|Ctrl + T|フォーカスをナビゲーション ウィンドウの最上位ノードに設定します。 フォーカスが既にそのウィンドウにある場合、フォーカスは最後にアクセスしたノードに設定されます。|
|Ctrl + I|フォーカスをリボンの下の階層リンク バーに設定します。|
|Ctrl + L|フォーカスを **[検索]** フィールドに設定します (使用可能な場合)。|
|Ctrl + D|フォーカスを [詳細] フィールドに設定します (使用可能な場合)。|
|Alt     |リボンのフォーカスのインとアウトを変更します。|

### <a name="cmpivot-shortcuts"></a><a name="bkmk_cmpshortcuts"></a> CMPivot のショートカット

ほとんどの [Web ブラウザーのキーボード ショートカット](https://support.microsoft.com/help/17456/windows-internet-explorer-ease-of-access-options)は、CMPivot で機能します。

|ショートカット キー|目的|
|--------|--------|  
|Ctrl + 1|最初のタブにフォーカスを設定します。|
|Alt + &lt;|アドレスに戻ります|


## <a name="other-accessibility-features"></a>その他のユーザー補助機能

- ナビゲーション ウィンドウ内を移動するには、ノード名の文字を入力します。

- メイン ビューとリボンのキーボード ナビゲーションは循環します。

- 詳細ウィンドウのキーボード ナビゲーションは循環します。 前のオブジェクトまたはウィンドウに戻るには、Ctrl + D キーを押してから Shift + TAB キーを押します。

- [ワークスペース] ビューを更新すると、フォーカスがそのワークスペースのメイン ウィンドウに設定されます。

- ワークスペース メニューを表示するには、展開/折りたたみのアイコンにフォーカスが移動するまで Tab キーを選択します。 下矢印キーを選択すると、ワークスペースのメニューが開きます。  

- ワークスペース メニュー間を移動するには、矢印キーを使用します。  

- ワークスペースの別のエリアに移動するには、Tab キーおよび Shift + Tab キーを使用します。 リボンなどワークスペースのエリア内を移動するには、矢印キーを使用します。  

- フォーカスがツリー ノードにある場合にアドレス バーにアクセスするには、Shift + Tab キーを 3 回押します。  

- ウィザードまたはプロパティ ページでは、キーボード ショートカットを使用してボックスを移動できます。 Alt キーと下線付き文字 (Alt+_) を選択すると、特定のボックスが選択されます。     

- ワークスペースのさまざまなノードに移動するには、ノード名の最初の文字を入力します。 キーを押すたびに、その文字で始まる次のノードにカーソルが移動します。 スクリーン リーダーを使用している場合は、リーダーがそのノードの名前を読み上げます。



## <a name="see-also"></a>関連項目

Configuration Manager ユーザー インターフェイスのナビゲーションの基礎について詳しくは、次の記事をご覧ください。
- [Configuration Manager コンソールの使用](../servers/manage/admin-console.md)
- [ソフトウェア センターのユーザー ガイド](software-center.md)

> [!NOTE]  
> この記事の情報は、米国内で Microsoft 製品のライセンスを入手したユーザーにのみ適用されることがあります。 米国以外でこの製品を入手した場合には、ソフトウェア パッケージに付属している子会社の情報カードを使用するか、または [Microsoft アクセシビリティ Web サイト](https://www.microsoft.com/accessibility/)で Microsoft サポート サービスの窓口を参照してください。 このセクションに記載されている製品とサービスが利用できるかどうかを確認するには、各地の子会社にお問い合わせください。 アクセシビリティに関する情報は、日本語やフランス語などの他の言語でも提供されています。