---
title: タスク シーケンス メディアの起動前コマンド
titleSuffix: Configuration Manager
description: 起動前コマンドに使用するスクリプトを作成し、起動前コマンドに関連付けられたコンテンツを配布し、メディアで起動前コマンドを構成します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9dd921d58e6ef777017af3e2eb24dbf4bd611fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699770"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>Configuration Manager でのタスク シーケンス メディアの起動前コマンド

*適用対象:Configuration Manager (Current Branch)*

ブート メディア、スタンドアロン メディア、および事前設定されたメディアと併用するように、Configuration Manager の起動前コマンドを作成できます。 起動前コマンドとは、Windows PE でタスク シーケンスを選択する前に実行され、ユーザーとやり取りできるスクリプトまたは実行可能ファイルのことです。 起動前コマンドでは、ユーザーに情報入力を求めるプロンプトを表示して、その情報をタスク シーケンス環境に保存したり、タスク シーケンス変数の情報を照会したりすることができます。 移行先コンピューターが起動すると、ポリシーが管理ポイントからダウンロードされる前にコマンド ラインが実行されます。 起動前コマンドに使用するスクリプトを作成し、起動前コマンドに関連付けられたコンテンツを配布し、メディアで起動前コマンドを構成するには、次の手順を実行してください。  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>起動前コマンドに使用するスクリプト ファイルを作成する  
 タスク シーケンス変数は、タスク シーケンスの実行中に、Microsoft.SMS.TSEnvironment COM オブジェクトを使用して読み書きできます。 次の例は、_SMSTSLogPath タスク シーケンス変数を照会して現在のログの場所を取得する Visual Basic スクリプト ファイルを示しています。 このスクリプトではカスタム変数も設定されます。  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>スクリプト ファイルのパッケージを作成してコンテンツを配布する  
 起動前コマンド用にスクリプトまたは実行可能ファイルを作成したら、スクリプトまたは実行可能ファイル用のファイルをホストするパッケージ ソースを作成し、ファイルのパッケージを作成し (プログラムは不要)、そのコンテンツを配布ポイントに配布する必要があります。  

 パッケージを作成する方法の詳細については、「[Packages and programs](../../apps/deploy-use/packages-and-programs.md)」(パッケージとプログラム) を参照してください。  

 コンテンツ配布の詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)」を参照してください。  

## <a name="configure-the-prestart-command-in-media"></a>メディアで起動コマンドを構成する  
 タスク シーケンス メディアの作成ウィザードでは、スタンドアロン メディア、起動可能なメディア、または事前設定されたメディア用に起動前コマンドを構成できます。 メディアの種類の詳細については、「[タスク シーケンス メディアの作成](../deploy-use/create-task-sequence-media.md)」を参照してください。 メディアで起動前コマンド作成するには、次の手順を実行します。  

#### <a name="to-create-a-prestart-command-in-media"></a>メディアで起動前コマンドを作成するには  

1.  Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。  

2.  **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、 **[タスク シーケンス]** をクリックします。  

3.  **[ホーム]** タブの **[作成]** グループで **[タスク シーケンス メディアの作成]** をクリックして、タスク シーケンス メディアの作成ウィザードを起動します。  

4.  **[メディアの種類の選択]** ページで、 **[スタンドアロン メディア]** 、 **[起動可能なメディア]** 、または **[事前設定されたメディア]** をクリックして、 **[次へ]** をクリックします。  

5.  ウィザードの **[カスタマイズ]** ページに進みます。 ウィザードの他のページを構成する方法の詳細については、「[タスク シーケンス メディアの作成](../deploy-use/create-task-sequence-media.md)」を参照してください。  

6.  **[カスタマイズ]** ページで、次の情報を指定して **[次へ]** をクリックします。  

    -   **[起動前コマンドを有効にする]** を選択します。  

    -   **[コマンド ライン]** テキスト ボックスに、起動前コマンド用に作成したスクリプトまたは実行可能ファイルを入力します。  

        > [!IMPORTANT]  
        >  **cmd /C <prestart command\>** を使用して、起動前コマンドを指定します。 たとえば、起動前コマンド スクリプトに TSScript.vbs と名前を付けた場合、コマンド ラインには「 **cmd /C TSScript.vbs** 」と入力します。 **cmd /C** は新しい Windows コマンド インタープリター ウィンドウを開き、Path 環境変数を使用して、起動前コマンドのスクリプトまたは実行可能ファイルを検索することを示します。 起動前コマンドのフル パスを指定することもできますが、ドライブ構成が異なるコンピューターでは、ドライブ文字が異なる可能性があります。  

    -   **[起動前コマンドにファイルを含める]** を選択します。  

    -   **[設定]** をクリックし、起動前コマンド ファイルと関連付けられているパッケージを選択します。  

    -   **[参照]** をクリックして、起動前コマンドのコンテンツをホストする配布ポイントを選択します。  

7.  ウィザードを完了します。  
