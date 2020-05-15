---
title: 展開計画を作成する方法
titleSuffix: Configuration Manager
description: Desktop Analytics で展開計画を作成するためのハウツー ガイド。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ac9b5ddd85904c90709a9450d6d2a9ffd379ddb9
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268761"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Desktop Analytics で展開計画を作成する方法

この記事では、Desktop Analytics で展開計画を作成する手順について説明します。 始める前にまず、[展開計画について学習してください](about-deployment-plans.md)。

## <a name="create-a-plan-for-windows-10"></a>Windows 10 用の計画を作成する

Desktop Analytics を使用して Windows 10 を展開するための計画を作成するには、このセクションの手順に従います。

1. [Desktop Analytics](https://aka.ms/desktopanalytics) ポータルを開きます。 少なくとも**ワークスペースの共同作成者**のアクセス許可を持つ資格情報を使用します。  

2. [管理] グループの **[展開計画]** を選択します。  

3. **[展開計画]** ウィンドウで、 **[作成]** を選択します。  

4. **[展開プランを作成]** ウィンドウで、次の設定を構成します。  

    - **名前**:展開計画の一意の名前  

    - **[製品とバージョン]** : 展開する Windows 10 のバージョンを選択します。 最新バージョンを使用する展開計画を作成することをお勧めします。  

    - **[デバイス グループ]** : 同じ階層から 1 つまたは複数のグループを選択します。 これらのグループは、Configuration Manager から同期される[デバイス コレクション](connect-configmgr.md#bkmk_Collections)です。

        複数の Configuration Manager 階層を同じ Desktop Analytics インスタンスに接続する場合、グローバル パイロット構成で、階層の表示名によってコレクション名のプレフィックスが設定されます。 この名前は、Configuration Manager コンソールの Desktop Analytics 接続の **[表示名]** プロパティです。<!-- 4814075 -->

        > [!NOTE]
        > 複数の階層をサポートするには、Configuration Manager バージョン 1910 以降が必要です。
        >
        > 複数の階層のコレクションを選択すると、ポータルに警告が表示されます。 複数の階層のコレクションを含む展開プランを作成することはできません。<!-- 4814075 -->

    - **[準備ルール]** : これらのルールは、どのデバイスがアップグレードの対象になるかを判断するのに役立ちます。 詳細については、「[準備ルール](#readiness-rules)」をご覧ください。  

    - **[完了日]** : その日までに対象となるすべてのデバイスに Windows を完全に展開する日付を選択します。  

5. **[作成]** を選択します。 新しい計画は、その処理中に展開計画の一覧に表示されます。 処理を早めるには、オンデマンドのデータ更新を要求します。 詳細については、「[Desktop Analytics の FAQ](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)を参照してください。  

6. 展開計画を、その名前を選択して開きます。  

7. [展開計画] メニューの **[準備]** グループで、 **[重要度を指定]** を選択します。  

    1. **[アプリ]** タブで、 **[未プレビュー]** を選択して、プレビューされていない資産のみを表示します。  

    2. 各アプリを選択し、 **[編集]** を選択します。 複数のアプリを選択して、同時に編集できます。  

    3. **[重要度]** の一覧から重要度レベルを選択します。 パイロット中に Desktop Analytics でアプリを検証する場合は、 **[クリティカル]** または **[重要]** を選択します。 **[重要ではない]** とマークされたアプリは検証されません。 重要度レベルを割り当てるときは、その[互換性](compat-assessment.md)と他の計画の分析情報を評価します。  

        重要度レベルを割り当てるときに、アップグレードの決定を選択することもできます。  

    4. 完了したら **[保存]** を選択します。  

8. [展開計画] メニューの **[準備]** グループで、 **[パイロットの識別]** を選択します。  

    1. パイロット用に推奨されているデバイスを確認します。  

    2. 各デバイスを選択し、 **[パイロットに追加]** を選択します。 推奨に同意しない場合は、 **[置換]** を選択します。  

        Desktop Analytics によってこれらのレコメンデーションがどのように行われているかの詳細については、 **[パイロットを指定]** ペインの右上隅にある情報アイコンを選択してください。

## <a name="readiness-rules"></a>準備ルール

これらのルールは、どのデバイスがインプレース アップグレードの対象になるかを判断するのに役立ちます。 これらの規則は、展開計画の作成時に設定することも、後で編集することもできます。

準備ルールを変更するには:

1. Desktop Analytics ポータルで展開計画を選択します。
1. 名前の横にある **[編集]** を選択します。
1. **[準備ルール]** を選択します。
1. **[Windows OS]** を選択します。
1. 必要に応じて変更を行い、 **[保存]** を選択します。

**Windows OS** のアップグレードの場合、次の 2 つのルールを使用できます: デバイス ドライバーと Windows アプリケーション。

### <a name="device-drivers"></a>デバイス ドライバー

デバイスが Windows Update からドライバーを取得するかどうかを構成します。 この値の既定値は **[オフ]** です。 Windows Update for Business を使用してドライバーを含む更新プログラムを管理している場合は、このルールを有効にします。 Configuration Manager を使用してソフトウェアの更新を管理している場合は、このルールを **[オフ]** に設定します。

### <a name="windows-applications"></a>Windows アプリケーション

Desktop Analytics で "*注目*" として表示されるアプリは、インストール数の下限のしきい値に基づいています。 展開計画の準備ルールでこのしきい値を設定します。 既定では、このしきい値は **2.0%** です。 `0.0` から `10.0` の範囲で値を変更できます。


## <a name="next-steps"></a>次のステップ

パイロット デバイスに展開するには、次の記事に進んでください。
> [!div class="nextstepaction"]  
> [パイロットに展開する](deploy-pilot.md)  
