---
title: カスタム タスク シーケンスの作成
titleSuffix: Configuration Manager
description: Configuration Manager でカスタム タスク シーケンスを編集して、タスク シーケンスにステップを追加します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f390c3857ad5a277002839c4c14ab1307d9ab281
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125578"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Configuration Manager を使用したカスタム タスク シーケンスの作成

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager で作成したばかりのカスタム タスク シーケンスにはタスク シーケンス ステップが含まれていません。 タスク シーケンスの作成後に編集し、必要なタスク シーケンス ステップを追加します。  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a> カスタム タスク シーケンスの作成

カスタム タスク シーケンスを作成するには、次の手順に従います。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[オペレーティング システム]** を展開して **[タスク シーケンス]** ノードを選択します。  

1. リボンの **[ホーム]** タブにある **[作成]** グループで、 **[タスク シーケンスの作成]** を選択します。 このアクションにより、タスク シーケンスの作成ウィザードが起動します。  

1. **[新しいタスク シーケンスの作成]** ページで **[新しいカスタム タスク シーケンスを作成する]** を選択します。  

1. **[タスク シーケンス情報]** ページで次を指定します。

    - タスク シーケンスの名前
    - タスク シーケンスの説明
    - タスク シーケンスが使用するオプションのブート イメージ

タスク シーケンスの作成ウィザードを完了すると、Configuration Manager によってカスタム タスク シーケンスが **[タスク シーケンス]** ノードに追加されます。 これで、タスク シーケンスを編集してタスク シーケンス ステップを追加できるようになります。  

## <a name="see-also"></a>関連項目

使用可能なタスク シーケンス ステップの一覧については、「[タスク シーケンスのステップ](../understand/task-sequence-steps.md)」をご覧ください。  

タスク シーケンスの編集方法の詳細については、「[Use the task sequence editor](../understand/task-sequence-editor.md)」 (タスク シーケンス エディターの使用) を参照してください。  

タスク シーケンスを使用することが最も多いのは OS の展開のタスクを自動化する場合ですが、カスタム タスク シーケンスはさまざまなタスクを自動化するために作成できます。 詳細については、「[OS 以外の展開用タスク シーケンスの作成](create-a-task-sequence-for-non-operating-system-deployments.md)」を参照してください。

バージョン 2002 以降では、アプリケーション モデルを介してタスク シーケンスを使用し、複雑なアプリケーションをインストールできます。 アプリのインストールまたはアンインストールに、タスク シーケンスである展開の種類をアプリに追加します。 詳しくは、「[Windows アプリケーションを作成する](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)」をご覧ください。<!-- 3555953 -->

## <a name="next-steps"></a>次のステップ

[タスク シーケンスの展開](deploy-a-task-sequence.md)
