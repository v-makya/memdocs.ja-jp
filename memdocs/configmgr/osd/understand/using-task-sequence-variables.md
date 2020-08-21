---
title: タスク シーケンス変数の使用方法
titleSuffix: Configuration Manager
description: Configuration Manager のタスク シーケンスで変数を使用する方法について説明します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7013ae10de753cbcb664771bd30dc51b259aa390
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697553"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Configuration Manager でタスク シーケンス変数を使用する方法

*適用対象:Configuration Manager (Current Branch)*

 Configuration Manager の OS 展開機能のタスク シーケンス エンジンでは、その動作を制御するために多くの変数が使用されます。 次の目的にこれらの変数を使用します。

- ステップでの条件を設定する  
- 特定のステップの動作を変更する  
- より複雑なアクションのためにスクリプトで使用する  

使用可能なすべてのタスク シーケンス変数の参照については、「[タスク シーケンス変数](task-sequence-variables.md)」をご覧ください。

## <a name="types-of-variables"></a><a name="bkmk_types"></a> 変数の種類

変数には複数の種類があります。  

- [組み込み](#bkmk_built-in)  
- [操作](#bkmk_action)  
- [カスタム](#bkmk_custom)  
- [読み取り専用](#bkmk_read-only)  
- [配列](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a> 組み込み変数

組み込み変数では、タスク シーケンスの実行環境に関する情報が提供されます。 これらの値は、タスク シーケンス全体で使用できます。 通常、組み込み変数はタスク シーケンス エンジンによってステップの実行前に初期化されます。

たとえば、`_SMSTSLogPath` は、Configuration Manager コンポーネントによってログ ファイルが書き込まれるパスを指定する環境変数です。 この環境変数には、すべてのタスク シーケンス ステップからアクセスできます。

タスク シーケンスでは、各ステップの前にいくつかの変数が評価されます。 たとえば、`_SMSTSCurrentActionName` には現在のステップの名前がリストされています。

### <a name="action-variables"></a><a name="bkmk_action"></a> アクション変数

タスク シーケンス アクション変数では、単一のタスク シーケンス ステップで使用される構成設定が指定されています。 既定では、ステップはその設定を初期化してから実行します。 これらの設定は、関連付けられているタスク シーケンス ステップの実行中にのみ使用できます。 タスク シーケンスでは、ステップを実行する前に、環境にアクション変数の値が追加されます。 ステップの実行後には、環境から値が削除されます。

たとえば、**コマンド ラインの実行**ステップをタスク シーケンスに追加します。 このステップには、**作業フォルダー** プロパティが含まれます。 タスク シーケンスでは、このプロパティの既定値が `WorkingDirectory` 変数として格納されています。 タスク シーケンスは、**コマンド ラインの実行**ステップを実行する前に、この値を初期化します。 このステップの実行中は、`WorkingDirectory` の値から **[開始するまでの時間]** プロパティの値にアクセスします。 ステップの完了後、タスク シーケンスによってこの環境から `WorkingDirectory` 変数の値が削除されます。 タスク シーケンスに別の "**コマンド ラインの実行**" ステップが含まれている場合は、新しい `WorkingDirectory` 変数が初期化されます。 その時点で、タスク シーケンスは現在のステップの開始値に変数を設定します。 詳しくは、「[WorkingDirectory](task-sequence-variables.md#WorkingDirectory)」をご覧ください。  

ステップが実行すると、アクション変数の "*既定の*" 値が示されます。 "*新しい*" 値を設定した場合、タスク シーケンスの複数のステップで使用できます。 既定値をオーバーライドした場合、新しい値は環境内で維持されます。 この新しい値は、タスク シーケンス内の他のステップの既定値をオーバーライドします。 たとえば、タスク シーケンスの最初のステップとして、**タスク シーケンス変数の設定**ステップを追加します。 このステップでは、`WorkingDirectory` 変数が `C:\` に設定されます。 タスク シーケンス内のすべての**コマンド ラインの実行**ステップでは、新しい開始ディレクトリ値が使用されます。  

一部のタスク シーケンス ステップでは、特定のアクション変数が "*出力*" としてマークされています。 タスク シーケンスの後続のステップでは、これらの出力変数が読み取られます。

> [!Note]  
> アクション変数を持たないタスク シーケンス ステップもあります。 たとえば、**BitLocker の有効化**アクションには関連付けれた変数がありますが、**BitLocker の無効化**アクションには関連付けられた変数はありません。  

### <a name="custom-variables"></a><a name="bkmk_custom"></a> カスタム変数

カスタム変数は、Configuration Manager で作成されない変数です。 条件として使用するにはコマンド ラインまたはスクリプトで独自の変数を初期化します。

新しいタスク シーケンス変数の名前を指定する際、次のガイドラインに従います。  

- タスク シーケンス変数名には、文字、数字、下線 (`_`)、およびハイフン (`-`) を含めることができます。  

- タスク シーケンス変数名の最低の長さは 1 文字、最大の長さは 256 文字です。  

- ユーザー定義変数は、文字 (`A-Z` または `a-z`) で始まる必要があります。  

- ユーザー定義変数名を下線で始めることはできません。 下線で始まるのは、読み取り専用タスク シーケンス変数のみです。  

- タスク シーケンス変数名では大文字と小文字が区別されません。 たとえば、`OSDVAR` と `osdvar` は同じタスク シーケンス変数です。  

- タスク シーケンス変数名をスペースで始めたり終わらせたりすることはできません。 また、変数名にスペースを埋め込むこともできません。 変数名の先頭または末尾のスペースは、タスク シーケンスでは無視されます。  

作成できるタスク シーケンス変数の数に制限はありません。 ただし、タスク シーケンス環境のサイズによって制限されます。 タスク シーケンス環境の合計サイズの制限は、8 KB です。 詳細については、「[タスク シーケンスのポリシーのサイズを小さくする](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize)」を参照してください。

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a> 読み取り専用変数

一部の変数の値は変更できず、読み取り専用です。 通常、そのような変数の名前は下線 (`_`) で始まっています。 タスク シーケンスでは、操作に読み取り専用変数が使用されます。 読み取り専用変数は、タスク シーケンス環境内で可視です。

これらの変数はスクリプトまたはコマンド ラインで役に立ちます。 たとえば、コマンド ラインを実行し、`_SMSTSLogPath` のログ ファイルへの出力を別のログ ファイルにパイプします。

> [!NOTE]  
> 読み取り専用タスク シーケンス変数は、タスク シーケンスのステップで読み取ることができますが、設定することはできません。 たとえば、**コマンド ラインの実行**ステップのコマンド ラインの一部として読み取り専用変数を使用します。 **タスク シーケンス変数の設定**ステップを使用して読み取り専用変数を設定することはできません。  

### <a name="array-variables"></a><a name="bkmk_array"></a> 配列変数

タスク シーケンスは、一部の変数を配列として格納します。 配列内の各要素は、1 つのオブジェクトに対する設定を表します。 デバイスに構成するオブジェクトが複数ある場合は、これらの変数を使用します。 次のタスク シーケンス ステップでは、配列変数が使用されます。

- [ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [ディスクのフォーマットとパーティション作成](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a> 変数を設定する方法

カスタム変数または読み取り専用ではない変数の場合は、変数の値を初期化および設定する方法がいくつかあります。  

- [タスク シーケンス変数の設定](#bkmk_set-ts-step)ステップ
- [動的変数の設定](#bkmk_set-dyn-step)ステップ
- [PowerShell スクリプトの実行](#bkmk_run-ps)ステップ
- [コレクションとデバイスの変数](#bkmk_set-coll-var)  
- [TSEnvironment COM オブジェクト](#bkmk_set-com)  
- [起動前コマンド](#bkmk_set-prestart)  
- [タスク シーケンス ウィザード](#bkmk_set-tswiz)
- [タスク シーケンス メディア ウィザード](#bkmk_set-media)  

環境から変数を削除するには、変数の作成と同じ方法を使用します。 変数を削除するには、変数の値を空の文字列に設定します。  

この方法を組み合わせて、同じシーケンスでタスク シーケンス変数をさまざまな値に設定できます。 たとえば、タスク シーケンス エディターを使用して既定値を設定し、スクリプトを使用してカスタム値を設定することができます。

異なる方法で同じ変数を設定する場合、タスク シーケンス エンジンでは次の順序が使用されます。  

1. 最初にコレクション変数を評価します。  

2. デバイス固有の変数は、コレクションで設定されている同じ変数をオーバーライドします。  

3. タスク シーケンス中に何らかの方法によって設定された変数は、コレクションまたはデバイスの変数より優先されます。  

### <a name="general-limitations-for-task-sequence-variable-values"></a>タスク シーケンス変数の値に関する一般的な制限事項

- タスク シーケンス変数の値は、4,000 文字を超えることはできません。  

- 読み取り専用タスク シーケンス変数を変更することはできません。 読み取り専用変数の名前は、下線 (`_`) で始まっています。  

- タスク シーケンス変数の値は、値の使用方法によっては、大文字と小文字が区別されることがあります。 ほとんどの場合、タスク シーケンス変数の値では、大文字と小文字が区別されません。 パスワードを含む変数は、大文字と小文字が区別されます。  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a> タスク シーケンス変数の設定

1 つの変数を 1 つの値に設定するには、タスク シーケンスでこのステップを使用します。

詳しくは、「[タスク シーケンス変数の設定](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)」をご覧ください。

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a> 動的変数の設定

1 つまたは複数のタスク シーケンス変数を設定するには、タスク シーケンスでこのステップを使用します。 このステップでは使用する変数と値を決定する規則を定義します。

詳細については、「[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)」を参照してください。

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a> PowerShell スクリプトの実行

<!-- 6315548 -->

タスク シーケンスでこのステップを使用し、PowerShell スクリプトを使用してタスク シーケンス変数を設定します。

パッケージからスクリプト名を指定することも、このステップの PowerShell スクリプトを直接入力することもできます。 次に、 **[タスク シーケンス変数に出力]** するこのステップのプロパティを使用して、スクリプトの出力をカスタム タスク シーケンス変数に保存します。

このステップの詳細については、「[PowerShell スクリプトの実行](task-sequence-steps.md#BKMK_RunPowerShellScript)」をご覧ください。

> [!NOTE]
> PowerShell スクリプトを使用して、**TSEnvironment** オブジェクトで 1 つ以上の変数を設定することもできます。 詳しくは、Configuration Manager SDK の「[How to use variables in a running task sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)」(実行中のタスク シーケンスで変数を使用する方法) をご覧ください。

#### <a name="example-scenario-with-run-powershell-script-step"></a>[PowerShell スクリプトの実行] ステップを使用したシナリオ例

使用する環境内に複数の国や地域のユーザーがいるため、複数の言語に固有の **[Apply OS]\(OS の適用\)** ステップの条件として、設定する OS の言語に対してクエリを実行する必要があるとします。

1. **[Apply OS]\(OS の適用\)** ステップの前に、タスク シーケンスに **[Powershell スクリプトの実行]** のインスタンスを追加します。

1. **[PowerShell スクリプトを入力します]** オプションを使用して、次のコマンドを指定します。

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    このコマンドレットの詳細については、「[Get-Culture](/powershell/module/microsoft.powershell.utility/get-culture)」をご覧ください。 2 文字の ISO 言語名の詳細については、「[ISO 639-1 コード一覧](https://wikipedia.org/wiki/List_of_ISO_639-1_codes)」をご覧ください。

1. **[タスク シーケンス変数に出力]** オプションに対して、`CurrentOSLanguage` を指定します。

    ![[PowerShell スクリプトの実行] ステップの例のスクリーンショット](media/run-powershell-script-example-language.png)

1. 英語のイメージ用の **[Apply OS]\(OS の適用\)** ステップで、次の条件を作成します: `Task Sequence Variable CurrentOSLanguage equals "en"`

    ![[Apply OS]\(OS の適用\) ステップの条件例のスクリーンショット](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > ステップの条件を作成する方法の詳細については、[変数へのアクセス方法に関する記事の「ステップの条件」](#bkmk_access-condition)をご覧ください。

1. タスク シーケンスを保存して展開します。

Windows の英語版が使用されているデバイスで **[Powershell スクリプトの実行]** ステップを実行した場合、コマンドによって値 `en` が返されます。 次に、その値がカスタム変数に保存されます。 英語のイメージ用の **[Apply OS]\(OS の適用\)** ステップが同じデバイスに対して実行されると、条件は true と評価されます。 異なる言語に対して **[Apply OS]\(OS の適用\)** ステップのインスタンスが複数ある場合、タスク シーケンスによってその OS の言語と一致するステップが動的に実行されます。

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a> コレクション変数とデバイス変数

デバイスおよびコレクションのカスタム タスク シーケンス変数を定義することができます。 デバイスに対して定義する変数は、デバイスごとのタスク シーケンス変数と呼ばれます。 コレクションについて定義される変数を、コレクションごとのタスク シーケンス変数といいます。 競合が発生する場合は、デバイスごとの変数がコレクションごとの変数より優先されます。 この動作は、特定のデバイスに自動的に割り当てられるタスク シーケンス変数が、そのデバイスを含むコレクションに割り当てられる変数よりも優先されることを意味します。  

たとえば、デバイス XYZ はコレクション ABC のメンバーであるものとします。 MyVariable を値 1 でコレクション ABC に割り当てます。 また、MyVariable を値 2 でデバイス XYZ にも割り当てます。 優先順位は、XYZ に割り当てられた変数の方が、コレクション ABC に割り当てられた変数より高くなります。 この変数を含むタスク シーケンスを XYZ で実行すると、MyVariable の値は 2 になります。

デバイスごとの変数およびコレクションごとの変数を非表示にして、Configuration Manager コンソールに表示されないようにすることができます。 **[この値を Configuration Manager コンソールに表示しない]** オプションを使用すると、コンソールに変数の値は表示されません。 タスク シーケンス ログ ファイル (**smsts.log**) またはタスク シーケンス デバッガーを使用しても、変数の値は表示されません。 この値は、実行時にタスク シーケンスで引き続き使用できます。 これらの変数を非表示にしておく必要がなくなった場合は、最初に削除します。 その後、非表示にするオプションを選択しないで変数を再定義します。  

> [!WARNING]  
> **[コマンド ラインの実行]** ステップのコマンド ラインに変数を含めた場合、タスク シーケンス ログ ファイルには、変数の値を含む完全なコマンド ラインが表示されます。 機密データがログ ファイルに表示されないようにするには、タスク シーケンスの変数 **OSDDoNotLogCommand** を `TRUE` に設定します。

デバイスごとの変数は、プライマリ サイトまたは中央管理サイトで管理することができます。 Configuration Manager では、デバイスあたり 1000 を超える変数の割り当てはサポートされていません。  

> [!IMPORTANT]  
> タスク シーケンスにコレクションごとの変数を使用する際には、次の動作を考慮してください。  
>
> - コレクションに対する変更は常に階層全体でレプリケートされます。 コレクション変数に加えられた変更は、現在のサイトのメンバーだけでなく、階層全体のコレクションのすべてのメンバーに適用されます。  
>  
> - コレクションを削除すると、そのアクションにより、コレクションに構成したタスク シーケンス変数も削除されます。  

#### <a name="create-task-sequence-variables-for-a-device"></a>"*デバイス*" 用にタスク シーケンス変数を作成する

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス]** ノードを選択します。  

2. ターゲット デバイスを選択し、 **[プロパティ]** を選択します。  

3. **[プロパティ]** ダイアログ ボックスで、 **[変数]** タブに切り替えます。  

4. 作成する変数ごとに、 **[新規]** アイコンを選択します。 タスク シーケンス変数の **[名前]** と **[値]** を指定します。 変数が Configuration Manager コンソールに表示されないように変数を非表示にする場合は、 **[この値を Configuration Manager コンソールに表示しない]** オプションを選択します。  

5. すべての変数をデバイスのプロパティに追加したら、 **[OK]** を選択します。  

#### <a name="create-task-sequence-variables-for-a-collection"></a>"*コレクション*" 用にタスク シーケンス変数を作成する

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動して、 **[デバイス コレクション]** ノードを選択します。 ターゲット コレクションを選択し、 **[プロパティ]** を選択します。  

2. **[プロパティ]** ダイアログ ボックスで、 **[コレクション変数]** タブに切り替えます。  

3. 作成する変数ごとに、 **[新規]** アイコンを選択します。 タスク シーケンス変数の **[名前]** と **[値]** を指定します。 変数が Configuration Manager コンソールに表示されないように変数を非表示にする場合は、 **[この値を Configuration Manager コンソールに表示しない]** オプションを選択します。  

4. 必要に応じて、タスク シーケンス変数の評価時に Configuration Manager で使用される優先度を指定します。  

5. すべての変数をコレクションのプロパティに追加したら、 **[OK]** を選択します。  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a> TSEnvironment COM オブジェクト

スクリプトから変数を使用するには、**TSEnvironment** オブジェクトを使用します。

詳しくは、Configuration Manager SDK の「[How to use variables in a running task sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)」(実行中のタスク シーケンスで変数を使用する方法) をご覧ください。

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a> 起動前コマンド

起動前コマンドは、ユーザーがタスク シーケンスを選択する前に Windows PE で実行されるスクリプトまたは実行可能ファイルです。 起動前コマンドでは、変数のクエリを行ったり、ユーザーに情報の指定を求めたりした後、それを環境に保存することができます。 起動前コマンドで変数を読み書きするには、[TSEnvironment](#bkmk_set-com) COM オブジェクトを使用します。

詳細については、「[タスク シーケンス メディアの起動前コマンド](prestart-commands-for-task-sequence-media.md)」を参照してください。

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a> タスク シーケンス ウィザード

バージョン 1906 以降では、タスク シーケンス ウィザード ウィンドウでタスク シーケンスを選択すると、タスク シーケンス変数を編集するページに **[編集]** ボタンが含まれるようになります。 アクセス可能なキーボード ショートカットを使用して、変数を編集できます。 この変更は、マウスが使用できない場合に役立ちます。<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a> タスク シーケンス メディア ウィザード

メディアから実行されるタスク シーケンスの変数を指定します。 メディアを使用して OS を展開する場合、メディアを作成するときに、タスク シーケンス変数を追加して値を指定します。 変数とその値はメディアに格納されます。  

> [!NOTE]  
> タスク シーケンスは、スタンドアロン メディアに保存されます。 ただし、事前設定メディアなどのその他のすべての種類のメディアは、管理ポイントからタスク シーケンスを取得します。  

メディアからタスク シーケンスを実行するときに、ウィザードの **[カスタマイズ]** ページで変数を追加することができます。

コレクションごとの変数またはコンピューターごとの変数の代わりに、メディア変数を使用してください。 タスク シーケンスをメディアから実行している場合、コンピューターごとの変数およびコレクションごとの変数は適用されず、使用されません。  

> [!TIP]  
> タスク シーケンスは、パッケージ ID と起動前コマンド ラインを、Configuration Manager コンソールを実行しているコンピューターの **CreateTSMedia.log** ファイルに書き込みます。 このログ ファイルには、任意のタスク シーケンス変数の値が含まれています。 このログ ファイルで、タスク シーケンス変数の値を確認します。  

詳しくは、「[タスク シーケンス メディアの作成](../deploy-use/create-task-sequence-media.md)」をご覧ください。

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a> 変数にアクセスする方法

前のセクションの方法のいずれかを使用して変数とその値を指定した後、タスク シーケンス内でそれを使用できます。 たとえば、組み込みタスク シーケンス変数の既定値にアクセスしたり、ステップを変数の値の条件に基づくようにしたりします。  

タスク シーケンス環境の変数値にアクセスするには、次の方法を使用します。

- [ステップでの使用](#bkmk_access-step)  
- [ステップの条件](#bkmk_access-condition)  
- [カスタム スクリプト](#bkmk_access-script)  
- [Windows セットアップ応答ファイル](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a> ステップでの使用

タスク シーケンスのステップで設定に対して変数の値を指定します。 タスク シーケンス エディターで、ステップを編集し、フィールドの値として変数名を指定します。 変数名は、パーセント記号 (`%`) で囲みます。

たとえば、**コマンド ラインの実行**ステップの **[コマンド ライン]** フィールドの一部として変数名を使用します。 次のコマンド ラインは、コンピューター名をテキスト ファイルに書き込みます。

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a> ステップの条件

ステップまたはグループの条件の一部として、組み込みまたはカスタムのタスク シーケンス変数を使用します。 タスク シーケンスは、ステップまたはグループを実行する前に、変数の値を評価します。

変数値を評価する条件を追加するには、次の手順のようにします。  

1. タスク シーケンス エディターで、条件を追加するステップまたはグループを選択します。  

2. ステップまたはグループの **[オプション]** タブに切り替えます。 **[条件の追加]** をクリックし、 **[タスク シーケンス変数]** を選択します。  

3. **[タスク シーケンス変数]** ダイアログ ボックスで、次の設定を指定します。  

    - **[変数]** :変数の名前です。 たとえば、`_SMSTSInWinPE` となります。  

    - **条件**: 変数の値を評価する条件です。 たとえば、 **[が次の値と等しい]** などです。  

    - **値**:チェックする変数の値です。 たとえば、`false` となります。  

上の 3 つの例では、タスク シーケンスが Windows PE のブート イメージから実行されているかどうかをテストする一般的な条件を設定しています。

> **タスク シーケンス変数** `_SMSTSInWinPE equals "false"`

既存の OS イメージをインストールする既定のタスク シーケンス テンプレートの **[ファイルと設定のキャプチャ]** グループで、この条件を確認してください。

条件の詳細については、[タスク シーケンス エディターの条件](task-sequence-editor.md#bkmk_conditions)に関する記事をご覧ください。

### <a name="custom-script"></a><a name="bkmk_access-script"></a> カスタム スクリプト

タスク シーケンスの実行中に、**Microsoft.SMS.TSEnvironment** COM オブジェクトを使用して、変数を読み書きします。

次の Windows PowerShell の例では、 **_SMSTSLogPath** 変数のクエリを行って、現在のログの場所を取得しています。 このスクリプトではカスタム変数も設定されます。

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a> Windows セットアップ応答ファイル

ユーザーが提供する Windows セットアップ応答ファイルには、タスク シーケンス変数を埋め込むことができます。 `%varname%` の形式を使用します。ここで、*varname* は変数の名前です。 **Windows と ConfigMgr のセットアップ** ステップでは、変数名の文字列が実際の変数値に置き換えられます。 これらの埋め込みタスク シーケンス変数は、unattend.xml 応答ファイルの数値のみのフィールドでは使うことができません。

詳細については、「[Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)」(Windows と ConfigMgr のセットアップ) を参照してください。

## <a name="see-also"></a>関連項目

- [タスク シーケンスのステップ](task-sequence-steps.md)

- [タスク シーケンス変数](task-sequence-variables.md)

- [タスクの自動化計画に関する考慮事項](../plan-design/planning-considerations-for-automating-tasks.md)

- [タスク シーケンス エディター](task-sequence-editor.md)