---
title: パッケージ定義ファイル
titleSuffix: Configuration Manager
description: パッケージ定義ファイルを使用して Configuration Manager でパッケージとプログラムを作成する方法について説明します
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689330"
---
# <a name="package-definition-files"></a>パッケージ定義ファイル

*適用対象:Configuration Manager (Current Branch)*

パッケージ定義ファイルは、Configuration Manager での[パッケージとプログラム作成](packages-and-programs.md)の自動化に役立つスクリプトです。 このファイルでは、パッケージ ソース ファイルの場所を除き、Configuration Manager がパッケージとプログラムを作成するために必要なすべての情報を提供します。

## <a name="about-the-package-definition-file-format"></a>パッケージ定義ファイルの形式について

各パッケージ定義ファイルは、.ini ファイル形式利用した、ASCII または UTF-8 テキスト ファイルです。 次のセクションが含まれています。  

### <a name="pdf"></a>[PDF]

このセクションでは、パッケージ定義ファイルとしてファイルを指定します。 これには、次の情報が含まれています。  

- **バージョン**:ファイルが使用するパッケージ定義ファイル形式のバージョンを指定します。 このバージョンは、書かれた際の Configuration Manager のバージョンに対応しています。 このエントリは必須です。  

### <a name="package-definition"></a>[Package Definition]

パッケージとプログラムのプロパティを指定します。 次の情報を提供します。  

- **名前**:パッケージ名。50 文字以内で指定します。  

- **バージョン** (省略可能):パッケージのバージョン。32 文字以内で指定します。  

- **アイコン** (省略可能):このパッケージに使用するアイコンを含むファイル。 指定すると、Configuration Manager コンソールの既定のパッケージ アイコンがこのアイコンに置き換わります。

- **パブリッシャー**:パッケージの発行元。32 文字以内で指定します。

- **言語**:パッケージの言語バージョン。32 文字以内で指定します。

- **コメント** (省略可能):パッケージに関する省略可能なコメント。127 文字以内で指定します。

- **ContainsNoFiles**:このエントリは、パッケージにソース ファイルがあるかどうかを示します。  

- **プログラム**:このパッケージに対して定義したプログラムです。 各プログラム名は、パッケージ定義ファイルの **[Program]** セクションに対応しています。  

    例:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**:パッケージ ステータスを含む管理情報フォーマット (MIF) ファイルの名前。50 文字以内で指定します。  

- **MIFName**:MIF 照合用パッケージの名前。50 文字以内で指定します。  

- **MIFVersion**:MIF 照合用パッケージのバージョン番号。32 文字以内で指定します。  

- **MIFPublisher**:MIF 照合用パッケージのソフトウェア発行元。32 文字以内で指定します。  

### <a name="program"></a>[Program]

**[パッケージ定義]** セクションの **[プログラム]** エントリで指定したプログラムごとに [プログラム] セクションを含めます。 このセクションでは、各プログラムを定義します。 各プログラムのセクションでは、次の情報を示します。  

- **名前**:プログラム名。50 文字以内で指定します。 このエントリは、パッケージ内で一意である必要があります。  

- **アイコン** (省略可能):このプログラムに使用するアイコンを含むファイルを指定します。 Configuration Manager コンソールの既定のプログラム アイコンがこのアイコンに置き換わります。 また、プログラムをコレクションにデプロイするときに、このアイコンが表示されます。

- **コメント** (省略可能):プログラムに関するコメント (127 文字以内)。

- **CommandLine**:プログラムのコマンド ラインを指定します (127 文字以内)。 コマンドは、パッケージ ソース フォルダーを基準にしています。

- **StartIn**:プログラムの作業フォルダーを指定します (127 文字以内)。 このエントリには、クライアント コンピューターの絶対パスを指定することも、パッケージ ソース フォルダーを基準としたパスを指定することもできます。

- **Run**:プログラムを実行するプログラム モードを指定します。 **Minimized**、 **Maximized**、または **Hidden**を指定できます。 このエントリを含めない場合、プログラムは通常モードで実行されます。  

- **AfterRunning**:プログラムが正常に完了した後に発生する特別なアクションを指定します。 利用可能なオプションは、 **SMSRestart**、 **ProgramRestart**、または **SMSLogoff**です。 このエントリを含めない場合、プログラムは特別なアクションを実行しません。  

- **EstimatedDiskSpace**:コンピューター上で実行できるソフトウェア プログラムを必要とするディスク領域の量を指定します。 既定値は **Unknown** です。 0 以上の整数を設定することができます。 値を指定する場合は、値の単位も含めます。  

    例:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**:クライアント コンピューターでプログラムを実行する予想時間を分単位で指定します。 既定値は **120** です。 0 以上の整数または**不明**を設定することができます。  

    例:  

    `EstimatedRunTime=25`  

- **SupportedClients**:プログラムが動作するプロセッサとオペレーティング システムを指定します。 プラットフォームをコンマで区切ります。 このエントリを含めない場合、クライアントは、このプログラムのサポートされているプラットフォームを確認しません。  

- **SupportedClientMinVersionX**、**SupportedClientMaxVersionX**:**SupportedClients** エントリで指定されたオペレーティング システムのバージョン番号の範囲の始まりと終わりを指定します。  

    例:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (省略可能):クライアント コンピューターに関するその他の情報または要件を指定します (127 文字以内)。

- **CanRunWhen**:プログラムをクライアント コンピューターで実行するために必要なユーザー ステータスを指定します。 使用できる値は、 **UserLoggedOn**、 **NoUserLoggedOn**、または **AnyUserStatus**です。 既定値は **UserLoggedOn**です。  

- **UserInputRequired**:プログラムにユーザーとの対話が必要かどうかを指定します。 使用できる値は **True** または **False**です。 既定値は **True**です。 **CanRunWhen** が **UserLoggedOn** に設定されていない場合、このエントリは **False**に設定されます。  

- **AdminRightsRequired**:プログラムを実行するためにコンピューターで管理者資格情報が必要であるかどうかを指定します。 使用できる値は **True** または **False**です。 既定値は **False**です。 **CanRunWhen** が **UserLoggedOn** に設定されていない場合、このエントリは **True**に設定されます。  

- **UseInstallAccount**:クライアント コンピューターでのプログラムの実行時にプログラムからクライアント ソフトウェアのインストール アカウントを使用するかどうかを指定します。 既定では、この値は **False**です。 **CanRunWhen** が **UserLoggedOn** に設定されている場合も、このエントリは **False**に設定されます。  

- **DriveLetterConnection**:プログラムが、配布ポイント上のパッケージ ファイルにドライブ文字を接続する必要があるかどうかを指定します。 **True** または **False**を指定できます。 既定値は **False** です。この場合、プログラムは UNC (汎用名前付け規則) 接続を使用できます。 この値が **True** に設定されている場合、クライアントは、次に利用可能なドライブ文字を使用します (Z: から始まり、逆方向に進みます)。  

- **SpecifyDrive** (省略可能):プログラムが配布ポイントのパッケージ ファイルに接続するのに必要とするドライブ文字を指定します。 この設定では、配布ポイントへのクライアント接続の指定したドライブ文字の使用を強制します。

- **ReconnectDriveAtLogon**:ユーザーがサインインしたときにコンピューターが配布ポイントに再接続するかどうかを指定します。 使用できる値は **True** または **False**です。 既定値は **False**です。  

- **DependentProgram**:現在のプログラムの前に実行する必要がある、このパッケージ内のプログラムを指定します。 このエントリでは `DependentProgram=<ProgramName>` の形式が使用されます。ここでは、`<ProgramName>` は、パッケージ定義ファイル内でそのプログラムを表す **Name** エントリです。 依存プログラムがない場合は、このエントリを空にしておきます。  

    例:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Assignment**:プログラムがどのようにユーザーに割り当てられるかを指定します。 この値には、

    - **FirstUser**:クライアントにサインインした最初のユーザーのみがプログラムを実行します
    - **EveryUser**:サインインしたすべてのユーザーがプログラムを実行します

    **CanRunWhen** が **UserLoggedOn**に設定されていない場合、このエントリは **FirstUser**に設定されます。  

- **Disabled**:このプログラムをクライアントにデプロイできるかどうかを指定します。 使用できる値は **True** または **False**です。 既定値は **False**です。  


## <a name="use-a-package-definition-file"></a>パッケージ定義ファイルを使用する  

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[パッケージ]** ノードを選択します。  

2. リボンの **[ホーム]** タブの **[作成]** グループで、 **[定義に基づいたパッケージの作成]** を選択します。  

3. **定義に基づいたパッケージの作成ウィザード**の **[パッケージ定義]** ページで、既存のパッケージ定義ファイルを選択します。 新しいパッケージ定義ファイルを開くには **[参照]** を選択します。 新しいパッケージ定義ファイルを指定したら、 **[パッケージ定義]** 一覧からそのファイルを選択します。

4. **[ソース ファイル]** ページで、パッケージとプログラムに必要なソース ファイルに関する情報を指定します。  

5. パッケージでソース ファイルが必要な場合は、 **[ソース フォルダー]** ページで、ソース ファイルの取得元となる場所を指定します。  

6. ウィザードを完了します。  


## <a name="see-also"></a>関連項目

[パッケージとプログラム](packages-and-programs.md)
