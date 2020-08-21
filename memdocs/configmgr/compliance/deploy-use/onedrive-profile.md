---
title: OneDrive for Business プロファイル
titleSuffix: Configuration Manager
description: Configuration Manager で OneDrive for Business プロファイルを使って Windows の既知のフォルダーを OneDrive for Business にリダイレクトします。
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d13d9dfd75abb656a765ce8c91ce6f177636cd3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127173"
---
# <a name="onedrive-for-business-profiles"></a>OneDrive for Business プロファイル

Configuration Manager バージョン 1902 以降、 Windows の既知のフォルダーを OneDrive for Business に移動するための OneDrive for Business プロファイルを作成できます。 これらのフォルダーには、デスクトップ、ドキュメント、およびピクチャが含まれます。 各プロファイルで、Windows の既知のフォルダーを移動するための設定を指定できます。 OneDrive for Business の詳細については、「[Redirect and move Windows known folders to OneDrive (Windows の既知のフォルダーを OneDrive にリダイレクトして移動する)](https://docs.microsoft.com/onedrive/redirect-known-folders)」をご覧ください。 <!--3556021-->

## <a name="prerequisites"></a>[前提条件]

- [Microsoft 365 テナント ID を検索します](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- OneDrive 同期クライアント バージョン 18.111.0603.0004 以降を展開します。 詳細については、「[Configuration Manager を使用した OneDrive アプリの展開](https://docs.microsoft.com/onedrive/deploy-on-windows)」を参照してください。  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a> Windows の既知のフォルダーを OneDrive に移動する
<!--3556021-->
Configuration Manager を使用して、Windows の既知のフォルダーを OneDrive for Business に移動します。 これらのフォルダーには、デスクトップ、ドキュメント、およびピクチャが含まれます。 Windows 10 へのアップグレードを簡単にするために、タスク シーケンスを展開する前にこれらの設定を Windows 7 クライアントに展開します。 

1. Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動し、 **[コンプライアンス設定]** を展開して、 **[OneDrive for Business Profiles]\(OneDrive for Business プロファイル\)** ノードを選択します。  

   ![OneDrive for Business プロファイルのノード](media/onedrive-for-business-profiles-node.png)
2. リボンで **[Create OneDrive for Business Profile]\(OneDrive for Business プロファイルの作成\)** を選択します。  

3. このポリシーを識別する名前を指定して、 **[次へ]** を選択します。  

4. OneDrive for Business プロファイルを使用してプロビジョニングするプラットフォームを選択します。 プラットフォームの選択が完了したら、 **[次へ]** をクリックします。

    ![OneDrive for Business プロファイルのプラットフォームを選択する](media/onedrive-for-business-profile-select-platforms.png) 

5. **[設定]** ページで次を実行します。

    1. ご自分の Microsoft 365 テナント ID を指定します。  

    2. 次のオプションのいずれかを選択して、既知のフォルダーを OneDrive に移動します。  

        - **[Windows の既知のフォルダーを OneDrive に移動するかどうかをユーザーに確認する]** : このオプションでは、各自のファイルを移動するためのウィザードがユーザーに表示されます。 フォルダーの移動の延期または拒否を選択した場合、OneDrive では定期的に移動が通知されます。  

        - **[確認を表示せずに Windows の既知のフォルダーを OneDrive に移動する]** : このポリシーをデバイスに適用すると、OneDrive クライアントにより自動的に既知のフォルダーが OneDrive for Business にリダイレクトされます。  

            - **[フォルダーがリダイレクトされた後に、通知がユーザーに表示されます]** : このオプションを有効にすると、フォルダーを移動した後に OneDrive クライアントからユーザーに通知が届きます。  

    3. **[ユーザーが Windows の既知のフォルダーを自分の PC にリダイレクトできないようにする]** : クライアント上の OneDrive for Business で、ユーザーがこのようなフォルダーをデバイスに戻すことができるオプションを無効にします。  

       ![OneDrive for Business の既知のフォルダーの移動設定](media/onedrive-for-business-profile-move-folder-settings.png)

6. ウィザードを完了してポリシーを展開します。  


## <a name="deploy-the-onedrive-for-business-profile"></a>OneDrive for Business プロファイルを展開する

1. Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動し、 **[コンプライアンス設定]** を展開して、 **[OneDrive for Business Profiles]\(OneDrive for Business プロファイル\)** ノードを選択します。  


2. プロファイルを選択した後、リボンの **[展開]** を選択します。

3. ご自身の展開用に以下の設定を指定します。

   1. **コレクション**: **[参照...]** をクリックしてから、プロファイルを展開するコレクションを選択します。  
   1. **アラートを生成する**:

      - **コンプライアンス対応率が指定値を下回った場合**: 準拠しているクライアントの最小パーセント。これを維持しない場合、アラートが生成されます。
      -  **日付と時刻**: プロファイルのコンプライアンスに基づいて生成されるアラートが最初に開始される日付です。
      - **System Center Operations Manager のアラートを生成する**: System Center Operations Manager にコンプライアンスのアラートを送信します。
   1. **スケジュール**:

      - **[簡易スケジュール]** : 既定では、この設定では簡易スケジュールを使って 7 日ごとにコンプライアンスの評価を開始します。
      - **カスタム スケジュール**: コンプライアンスの評価を実行するタイミングを定義します。 開始時刻は、スケジュールの作成時に Configuration Manager コンソールを実行しているコンピューターのローカル時刻に基づきます。または、UTC を使えます。
 
      ![OneDrive for Business プロファイルを展開する](media/onedrive-for-business-deploy-profile.png)

4. **[OK]** をクリックして、OneDrive for Business プロファイルを展開します。


## <a name="next-steps"></a>次のステップ

[リモート接続プロファイルの作成](create-remote-connection-profiles.md)
