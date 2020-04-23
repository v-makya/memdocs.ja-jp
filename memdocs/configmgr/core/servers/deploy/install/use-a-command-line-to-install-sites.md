---
title: コマンドライン インストール
titleSuffix: Configuration Manager
description: さまざまなサイトのインストールで、コマンド プロンプトから Configuration Manager セットアップを実行する方法について説明します。
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700400"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>コマンド ラインを使用して Configuration Manager サイトをインストールする

*適用対象:Configuration Manager (Current Branch)*

 さまざまなサイトのインストールで、コマンド プロンプトから Configuration Manager セットアップを実行できます。

## <a name="supported-tasks-for-command-line-installations"></a>コマンド ラインでのインストールでサポートされているタスク
 この方法でセットアップを実行する場合、次のサイト インストール タスクとサイト メンテナンス タスクがサポートされます。

- **コマンド プロンプトから中央管理サイトまたはプライマリ サイトをインストールする**  
  [セットアップのコマンド ライン オプション](../../../../core/servers/deploy/install/command-line-options-for-setup.md)を表示する

- **中央管理サイトまたはプライマリ サイトで使用する言語を変更する**  
   サイトにインストールされている言語 (モバイル デバイスの言語を含む) をコマンド プロンプトから変更するには、次の操作を実行する必要があります。  

  - サイト サーバーの **&lt;ConfigMgrInstallationPath\>\Bin\X64** からセットアップを実行します
  - **/MANAGELANGS** コマンド ライン オプションを使用します
  - 追加または削除する言語を指定した言語スクリプト ファイルを指定します  

    たとえば、次のコマンド構文を使用します: **setupwpf.exe/MANAGELANGS &lt;言語スクリプト ファイル\>**  

    言語スクリプト ファイルを作成するには、「[Command line options to manage languages](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)」(言語を管理するためのコマンド ライン オプション) に記載されている情報を参考にしてください。  

- **サイトの無人インストールまたはサイトの回復にインストール スクリプト ファイルを使用する**  
   インストール スクリプトを使用してコマンド プロンプトからセットアップを実行し、サイトの無人インストールを実行できます。 また、この方法で、サイトを回復することもできます。    

   セットアップでスクリプトを使用するには:  

  - コマンド ライン オプション **/SCRIPT** を使用してセットアップを実行し、スクリプト ファイルを指定します。  

  - スクリプト ファイルは、必要なキーと値を使用して構成する必要があります。  

    中央管理サイトまたはプライマリ サイトの無人インストールの場合は、次のセクションがスクリプト ファイルに含まれている必要があります。  

  - Identification    
  - オプション    
  - SQLConfigOptions    
    -   HierarchyOptions    
  - CloudConnectorOptions   

    サイトを回復するには、スクリプト ファイルの次のセクションも含める必要があります。  

  - Identification  
  - 復元

詳細については、「[Configuration Manager のサイトの無人回復](../../manage/unattended-recovery.md)」を参照してください。  

無新インストールのスクリプト ファイルで使用するキーと値の一覧を確認するには、「[Unattended Setup script file keys](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended)」(無人セットアップ スクリプト ファイルのキー) を参照してください。  

## <a name="about-the-command-line-script-file"></a>コマンド ライン スクリプト ファイルについて  
 Configuration Manager の無人インストールの場合は、コマンド ライン オプション **/SCRIPT** を使用してセットアップを実行し、インストール オプションを含むスクリプト ファイルを指定できます。 この方法では、次のタスクがサポートされています。  

-   中央管理サイトをインストールする  
-   プライマリ サイトをインストールする  
-   Configuration Manager コンソールをインストールする  
-   サイトを回復する  

> [!NOTE]  
>  評価サイトを製品版の Configuration Manager にアップグレードする場合、無人スクリプト ファイルを使用することはできません。  

### <a name="the-cdlatest-key-name"></a>CDLatest キー名
CD.Latest フォルダーのメディアを使用して、次の 4 つのインストール オプションのスクリプト インストールを実行する場合は、値が **1** の **CDLatest** キーを含める必要があります。
- 新しい中央管理サイトをインストールする
- 新しいプライマリ サイトをインストールする
- 中央管理サイトを回復する
- プライマリ サイトを回復する

この値は、Microsoft ボリューム ライセンス サイトから取得したインストール メディアでは使用できません。
スクリプト ファイルでこのキー名を使用する方法の詳細については、[コマンド ライン オプション](command-line-options-for-setup.md)を参照してください。



### <a name="create-the-script"></a>スクリプトを作成する
[サイトをインストールするためにユーザー インターフェイスを使用してセットアップを実行する](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)と、インストール スクリプトが自動的に作成されます。  ウィザードの **[概要]** ページで設定を確認するときに、次の処理が実行されます。  

-   スクリプト **%TEMP%\ConfigMgrAutoSave.ini**が作成されます。  このファイルは使用する前に名前を変更できますが、.ini ファイル拡張子は保持する必要があります。  
-   無人インストール スクリプトには、ウィザードで選択した設定が含まれています。  
-   スクリプトが作成された後、そのスクリプトを変更して、階層に別のサイトをインストールできます。  
-   このスクリプトを使用して、Configuration Manager の無人セットアップを実行できます。  

このスクリプト ファイルで、セットアップ ウィザードで入力するのと同じ情報を指定します。ただし、既定の設定はありません。   
使用する種類のインストールに適用されるセットアップ キーのすべての値を指定する必要があります。   

セットアップで作成される無人インストール用スクリプトには、セットアップ中に入力したプロダクト キーの値が指定されます。 この値は、有効なプロダクト キーか、評価版の Configuration Manager をインストールする場合は **EVAL** になります。 スクリプト内のプロダクト キーの値は、前提条件チェックを完了できるようにするために指定されます。   

セットアップで実際のサイトのインストールが開始されると、自動的に作成されたスクリプトに再度書き込みが行われ、スクリプトのプロダクト キーの値は消去されます。 新しいサイトの無人インストールでスクリプトを使用する前に、スクリプトを編集して、正しいプロダクト キーを指定するか、評価版の Configuration Manager のインストールを指定できます。  

### <a name="section-names-key-names-and-values"></a>セクション名、キー名、値
スクリプトは、セクション名、キー名、値で構成します。 次の情報にご注意ください。
-   セクションの必須キーは、スクリプトを記述しているインストールの種類によって異なります。
-   セクション内でのキーの順序、およびファイル内でのセクションの順序は重要ではありません。     
-   キー名の大文字と小文字は区別されません。  
-   キーの値を指定するときは、キー名の後ろに等号 (=) を入力してから、キーの値を続けます。    

> [!TIP]  
>  すべてのオプションについては、「[Command-line options for Setup and scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md)」(セットアップのコマンド ライン オプションとスクリプト) を参照してください。  

## <a name="use-the-script-setup-command-line-option"></a>/SCRIPT セットアップ コマンドライン オプションを使用する

-   セットアップ スクリプト ファイルを使用し、 **/SCRIPT** セットアップ コマンド ライン オプションの後にファイル名を指定する必要があります。 次の情報にご注意ください。   
    -   ファイルの名前には、ファイル名拡張子 **.ini** が含まれている必要があります。  
    -   コマンド プロンプトでセットアップ スクリプト ファイルを指定するときは、ファイルの完全パスを入力する必要があります。 たとえば、C:\Setup フォルダーにある Setup.ini というセットアップ初期化ファイルの場合は、コマンド プロンプトに次のように入力します。 **setup /script c:\setup\setup.ini**  

-   セットアップを実行するアカウントには、コンピューターの**管理者**の権限が必要です。 無人インストールを使用してセットアップを実行する場合は、 **[管理者として実行]** を使用してコマンド プロンプト ウィンドウを開いてください。   
