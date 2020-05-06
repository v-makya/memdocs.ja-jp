---
title: WSUS からの Endpoint Protection のマルウェア定義
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: 定義ファイルの更新を自動的に承認するように Windows Server Update Services を構成する方法を説明します。
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126035"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Configuration Manager で Endpoint Protection のマルウェア定義を WSUS からダウンロードできるようにする

*適用対象:Configuration Manager (Current Branch)*

マルウェア対策の定義を最新に保つために WSUS を使用する場合は、定義ファイルの更新を自動的に承認するように構成できます。 定義ファイルを最新に保つ方法として Configuration Manager ソフトウェア更新プログラムの使用をお勧めしますが、ユーザーが手動で定義ファイルを更新できるようにする方法として、WSUS を構成することもできます。 次の手順を使用して、WSUS を定義ファイルの更新ソースとして構成します。

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Configuration Manager の定義ファイルの更新を同期する

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** を選択します。

1. ソフトウェアの更新ポイントが含まれているサイトを選びます。 リボンの **[設定]** グループで **[サイト コンポーネントの構成]** を選択し、 **[ソフトウェアの更新ポイント]** を選択します。

1. **[ソフトウェアの更新ポイント コンポーネントのプロパティ]** ウィンドウで **[分類]** タブに切り替えます。 **[定義ファイルの更新]** を選択します。

1. WSUS で更新される **[製品]** を指定するには、 **[製品]** タブに切り替えます。

    - Windows 10 以降: [Microsoft] > [Windows] で **[Windows Defender]** を選択します。

    - Windows 8.1 以前: [Microsoft] > [Forefront] で **[System Center Endpoint Protection]** を選択します。

1. **[OK]** を選択して、 **[ソフトウェアの更新ポイント コンポーネントのプロパティ]** ウィンドウを閉じます。

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>スタンドアロン WSUS の定義ファイルの更新を同期する

次の手順を使用して、WSUS サーバーが Configuration Manager 環境に統合されていない場合の Endpoint Protection 更新ファイルを構成します。

1. WSUS 管理コンソールで **[コンピューター]** を展開し、 **[オプション]** を選択し、 **[製品と分類]** を選択します。

1. WSUS で更新される **[製品]** を指定するには、 **[製品]** タブに切り替えます。

    - Windows 10 以降: [Microsoft] > [Windows] で **[Windows Defender]** を選択します。

    - Windows 8.1 以前: [Microsoft] > [Forefront] で **[System Center Endpoint Protection]** を選択します。

1. **[分類]** タブに切り替えます。 **[定義ファイルの更新]** と **[更新プログラム]** を選択します。

## <a name="approve-definition-updates"></a>定義ファイルの更新を承認する

Endpoint Protection 定義ファイルの更新を承認して、WSUS サーバーにダウンロードしてからでないと、使用可能な更新の一覧を要求するクライアントに対して更新を提供することはできません。 クライアントは WSUS サーバーに接続して、適用できる更新プログラムをチェックし、最新の承認済み定義ファイルの更新を要求します。

### <a name="approve-definitions-and-updates-in-wsus"></a>WSUS で定義ファイルと更新を承認する

1. WSUS 管理コンソールで **[更新プログラム]** を選択します。 次に、 **[すべての更新]** 、または承認する更新プログラムの分類を選択します。

1. 更新の一覧で、インストールを承認する更新を右クリックして **[承認]** を選択します。

1. **[更新プログラムの承認]** ウィンドウで更新を承認するコンピューター グループを選択し、 **[インストールの承認]** を選択します。

### <a name="configure-an-automatic-approval-rule"></a>自動承認規則を構成する

定義ファイルの更新と Endpoint Protection の更新プログラムに関する自動承認規則を設定することもできます。 この操作によって、WSUS でダウンロードした Endpoint Protection 定義ファイルの更新が自動的に承認されるように WSUS が構成されます。

1. WSUS 管理コンソールで、 **[オプション]** を選択し、 **[自動承認]** を選択します。

1. **[更新規則]** タブの **[新しい規則]** を選択します。

1. **[規則の追加]** ウィンドウの **[ステップ 1: プロパティの選択]** でオプション **[更新が特定の分類に含まれる場合]** を選択します。

    1. 「**手順 2: プロパティを変更します** で **任意の分類** を選択します。

    1. **[定義ファイルの更新]** を除くすべてのオプションをオフにして **[OK]** を選択します。

1. **[規則の追加]** ウィンドウの **[ステップ 1: プロパティの選択]** でオプション **[更新が特定の製品に含まれる場合]** を選択します。

    1. 「**手順 2: プロパティを変更します** で **任意の製品** を選択します。

    1. Windows 8.1 以前の場合は **[System Center Endpoint Protection]** 、Windows 10 以降の場合は **[Windows Defender]** を除くすべてのオプションをオフにします。 次に、 **[OK]** を選択します。

1. 「**手順 3: 名前を指定する** で、規則の名前を入力して、**OK** を選択します。

1. **[自動承認]** ダイアログ ボックスで、新しく作成したルールを選択し、 **[規則の実行]** を選択します。

> [!NOTE]
> WSUS サーバーとクライアント コンピューターのパフォーマンスを最大化するには、前の定義ファイルの更新を拒否します。 このタスクを実行するには、リビジョンの自動承認と、有効期限が切れた更新プログラムの自動拒否を構成します。 詳細については、[Microsoft サポート記事 938947](https://support.microsoft.com/kb/938947) を参照してください。

> [!div class="nextstepaction"]
> [マルウェア対策ポリシーの作成と展開](endpoint-antimalware-policies.md)
