---
title: Mac クライアントを展開する
titleSuffix: Configuration Manager
description: Configuration Manager でクライアントを Mac コンピューターに展開する方法を説明します。
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694030"
---
# <a name="how-to-deploy-clients-to-macs"></a>Mac にクライアントを展開する方法

*適用対象:Configuration Manager (Current Branch)*

この記事では、Mac コンピューターに構成マネージャー クライアントを展開して管理する方法について説明します。 Mac コンピューターにクライアントを展開する前に構成する必要がある内容の詳細については、「[Mac コンピューターにクライアント ソフトウェアを展開するための準備](prepare-to-deploy-mac-clients.md)」を参照してください。

Mac コンピューター用の新しいクライアントをインストールする場合は、Configuration Manager の更新プログラムをインストールして、Configuration Manager コンソールで新しいクライアント情報を反映する必要もあります。

これらの手順には、クライアント証明書をインストールするための 2 つのオプションがあります。 Mac コンピューターのクライアント証明書の詳細については、「[Mac コンピューターにクライアント ソフトウェアを展開するための準備](prepare-to-deploy-mac-clients.md#certificate-requirements)」を参照してください。  

- [CMEnroll ツール](#bkmk_enroll) を使用して Configuration Manager 登録を使用する。 登録プロセスでは自動証明書更新はサポートされていません。 インストールされている証明書の有効期限が切れる前に、Mac コンピューターを再登録します。    

- [Configuration Manager とは独立した証明書の要求とインストールの方法を使用する](#bkmk_external)。  

> [!IMPORTANT]  
> macOS Sierra を実行しているデバイスにクライアントを展開するには、管理ポイント証明書の**サブジェクト名**を正しく構成します。 たとえば、管理ポイント サーバーの FQDN を指定します。



## <a name="configure-client-settings"></a>クライアント設定を構成する  

Mac コンピューターの登録を構成するには、[既定のクライアント設定](about-client-settings.md)を使用します。 カスタムのクライアント設定は使用できません。 証明書を要求してインストールするには、Mac 向けの構成マネージャー クライアントに既定のクライアント設定が必要です。  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[クライアント設定]** ノード、 **[既定のクライアント設定]** の順に選択します。  

2. リボンの **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** を選択します。  

3. **[登録]** セクションを選択し、次の設定を構成します。  

    1. **ユーザーがモバイル デバイスと Mac コンピューターを登録できるようにする**:**はい**  

    2. **[登録プロファイル]:** **[プロファイルの設定]** を選択します。  

4. **[モバイル デバイス登録プロファイル]** ダイアログ ボックスで、 **[作成]** をクリックします。  

5. **[登録プロファイルの作成]** ダイアログ ボックスで、この登録プロファイルの名前を入力します。 次に、 **[管理サイト コード]** を構成します。 これらの Mac コンピューターを管理する管理ポイントを含む Configuration Manager プライマリ サイトを選択します。  

    > [!NOTE]  
    >  サイトを選択できない場合は、そのサイト内で少なくとも 1 つの管理ポイントがモバイル デバイスをサポートするように構成されていることを確認してください。  

6. **[追加]** を選びます。  

7. **[モバイル デバイスの証明機関の追加]** ウィンドウで、Mac コンピューターに証明書を発行する認証機関サーバーを選択します。  

8. **[登録プロファイルの作成]** ダイアログ ボックスで、以前に作成した Mac コンピューター証明書テンプレートを選択します。  

9. **[OK]** を選択して **[登録プロファイル]** ダイアログ ボックスを閉じ、 **[既定のクライアント設定]** ダイアログ ボックスを閉じます。  

    > [!TIP]  
    > クライアント ポリシーの間隔を変更する場合、 **[クライアント ポリシー]** クライアント設定グループの **[クライアント ポリシーのポーリング間隔]** を使用します。  

次回、デバイスがクライアント ポリシーをダウンロードするときに、Configuration Manager によってこれらの設定がすべてのユーザーに対して適用されます。 1 つのクライアントのポリシーの取得を開始するには、「[構成マネージャー クライアントのポリシーの取得開始](../manage/manage-clients.md#BKMK_PolicyRetrieval)」をご覧ください。  

登録クライアント設定の他に、次のクライアント デバイス設定が構成されていることを確認します。  

- **[ハードウェア インベントリ]** :Mac および Windows クライアント コンピューターからハードウェア インベントリを収集する場合、この機能を有効にして構成します。 詳しくは、[ハードウェア インベントリの構成方法](../manage/inventory/extend-hardware-inventory.md)に関するページをご覧ください。  

- **[コンプライアンス設定]** :Mac および Windows クライアント コンピューターの設定を評価して修復する場合、この機能を有効にして構成します。 詳細については、「[コンプライアンス設定の計画と構成](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)」をご覧ください。  

詳しくは、「[クライアント設定を構成する方法](configure-client-settings.md)」をご覧ください。  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a> macOS 用のクライアントをダウンロードする

1. macOS クライアント ファイル パッケージ ([Microsoft Endpoint Configuration Manager - macOS クライアント (64 ビット)](https://www.microsoft.com/download/details.aspx?id=100850)) をダウンロードします。 **ConfigmgrMacClient.msi** を Windows を実行しているコンピューターに保存します。 このファイルは Configuration Manager インストール メディアには含まれていません。  

2. Windows コンピューターでインストーラーを実行します。 Mac クライアント パッケージ (**Macclient.dmg**) をローカル ディスク上のフォルダーに展開します。 既定のパスは、`C:\Program Files\Microsoft\System Center Configuration Manager for Mac client` です。  

3. **Macclient.dmg** ファイルを Mac コンピューターのフォルダーにコピーします。  

4. Mac コンピューターで、**Macclient.dmg** を実行して、ローカル ディスクのフォルダーにファイルを抽出します。  

5. フォルダー内に次のファイルが含まれているいることを確認します。 

    - **Ccmsetup**:**CMClient.pkg** を使用して Mac コンピューターに構成マネージャー クライアントをインストールします  

    - **CMDiagnostics**:Mac コンピューターの構成マネージャー クライアントに関連する診断情報を収集します  

    - **CMUninstall**:Mac コンピューターからクライアントをアンインストールします  

    - **CMAppUtil**:Apple アプリケーション パッケージを Configuration Manager アプリケーションとして展開できる形式に変換します  

    - **CMEnroll**:Mac コンピューター用のクライアント証明書を要求してインストールし、構成マネージャー クライアントをインストールできるようにします  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a> Mac クライアントを登録する  

[Mac コンピューターの登録ウィザード](#enroll-the-client-with-the-mac-computer-enrollment-wizard)を使用して、個々のクライアントを登録します。

多くのクライアントの登録を自動化するには、[CMEnroll ツール](#client-and-certificate-automation-with-cmenroll)を使用します。   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Mac コンピューターの登録ウィザードを使用してクライアントを登録する  

1. クライアントをインストールすると、コンピューターの登録ウィザードが開きます。 ウィザードを手動で起動するには、**Configuration Manager** の環境設定ページで、 **[登録]** を選択します。  

2. ウィザードの 2 番目のページで、次の情報を指定します。  

   - **ユーザー名**:ユーザー名は、次の形式で入力できます。  

     - `domain\name` にする必要があります。 例: `contoso\mnorth`  

     - `user@domain` にする必要があります。 例: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  メール アドレスを使用して **[ユーザー名]** フィールドを指定すると、Configuration Manager により **[サーバー名]** フィールドが自動的に指定されます。 これには、登録プロキシ ポイント サーバーの既定の名前とメール アドレスのドメイン名が使用されます。 これらの名前が登録プロキシ ポイント サーバーの名前と一致しなていない場合は、登録時に**サーバー名**を修正します。  

       ユーザー名と、対応するパスワードは、Mac クライアント証明書テンプレートに対する**読み取り**および**登録**のアクセス許可を持つ Active Directory ユーザー アカウントと一致している必要があります。  

   - **サーバー名**:登録プロキシ ポイント サーバーの名前を入力します。  


### <a name="client-and-certificate-automation-with-cmenroll"></a>CMEnroll によるクライアントと証明書の自動化  

CMEnroll ツールでクライアントのインストール、クライアント証明書の要求と登録を自動化する場合に、この手順を使用します。 ツールを実行するには、Active Directory ユーザー アカウントが必要です。

1. Mac コンピューターで、**Macclient.dmg** ファイルのコンテンツを抽出したフォルダーに移動します。  

2. 次のコマンドを入力します。`sudo ./ccmsetup`  

3. 「 **Completed installation (インストール完了)** 」メッセージが表示されるまで待ちます。 インストーラーでは、再起動が必要というメッセージが表示されますが、ここでは再起動せず、次の手順に進みます。  

4. Mac コンピューターの **Tools** フォルダーで、次のコマンドを入力します。`sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    クライアントのインストール後に、Mac コンピューターの登録ウィザードを使用して Mac コンピューターを登録できます。 詳細については、[Mac コンピューターの登録ウィザードを使用したクライアントの登録](#bkmk_enroll)に関するトピックを参照してください。  

     例:登録プロキシ ポイント サーバーの名前が **server02.contoso.com** で、Mac クライアント証明書テンプレートに対して **contoso\mnorth** アクセス許可を付与している場合は、次のコマンドを入力します。`sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > ユーザー名に、`<>"+=,` のいずれかの文字が含まれている場合、登録は失敗します。 帯域外証明書とこれらの文字が含まれていないユーザー名を使用します。  
    >  
    > ユーザー エクスペリエンスを単純化するには、インストール手順をスクリプト化します。 こうすると、ユーザーはユーザー名とパスワードを指定するだけで済みます。  

5. Active Directory ユーザー アカウントのパスワードを入力します。 このコマンドを入力すると、2 つのパスワードが要求されます。 最初のパスワードは、コマンドを実行するスーパー ユーザー アカウント用です。 2 つ目のプロンプトは、Active Directory ユーザー アカウント用です。 プロンプトは似ているため、正しい順番で指定するように気を付けてください。  

6. 「 **Successfully enrolled (正常に登録されました)** 」メッセージが表示されるまで待ちます。  

7. Mac コンピューターで、登録する証明書を Configuration Manager に制限するには、ターミナル ウィンドウを開き、次のように変更します。  

    1. コマンド `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access` を入力します  

    2. **[Keychain Access]\(キーチェーン アクセス\)** ウィンドウの **[Keychains]\(キーチェーン\)** セクションで、 **[System]\(システム\)** を選択します。 次に、 **[Category]\(カテゴリ\)** セクションで、 **[Keys]\(キー\)** を選択します。  

    3. キーを展開してクライアント証明書を表示します。 インストールした秘密キーを持つ証明書を検索して、キーを開きます。  

    4. **[アクセス制御]** タブで、 **[アクセスを許可する前に確認する]** を選択します。  

    5. **/Library/Application Support/Microsoft/CCM** を参照し、 **[CCMClient]** を選択して **[追加]** を選択します。  

    6. **[変更を保存]** をクリックし、 **[キーチェーン アクセス]** ダイアログ ボックスを閉じます。  

8. Mac コンピューターを再起動します。  

クライアントのインストールが正常に完了したことを確認するには、Mac コンピューターの **[システム環境設定]** で **[Configuration Manager]** 項目を開きます。 また、Configuration Manager コンソールで **[すべてのシステム]** コレクションを更新して表示します。 このコレクションに Mac コンピューターが管理されたクライアントとして表示されることを確認します。  

> [!TIP]  
> Mac クライアントのトラブルシューティングをするには、Mac クライアント パッケージに付属している **CMDiagnostics** ツールを使用します。 それを使用して、次の診断情報を収集します。  
>   
> - 実行中のプロセスの一覧  
> - Mac OS X オペレーティング システムのバージョン  
> - 構成マネージャー クライアントに関連する Mac OS X のクラッシュ レポート (**CCM\*.crash** と **System Preference.crash** を含む)  
> - 構成マネージャー クライアントのインストールで作成される Bill of Materials (BOM) ファイルとプロパティ一覧 (.plist) ファイル  
> - **/Library/Application Support/Microsoft/CCM/Logs** フォルダーの内容  
>   
> CmDiagnostics で収集された情報は、コンピューターのデスクトップに保存される zip ファイルに追加され、`cmdiag-<hostname>-<datetime>.zip` という名前が付けられます。



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a> Configuration Manager 外部の証明書を管理する

Configuration Manager から独立した証明書の要求とインストールの方法を使用できます。 同じ一般的なプロセスを使用しますが、次の追加の手順が含まれます。 

- 構成マネージャー クライアントをインストールする場合は、**MP** と **SubjectName** のコマンド ライン オプションを使用します。 次のコマンドを入力します。`sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>` 証明書のサブジェクト名は大文字と小文字が区別されるので、証明書の詳細に表示されるとおりに入力してください。  

     例:管理ポイントのインターネット FQDN は **server03.contoso.com** です。 Mac クライアント証明書には、証明書サブジェクトの共通名として **mac12.contoso.com** の FQDN があります。 次のコマンドを使います。`sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- 同じサブジェクト値を含む証明書が複数ある場合、構成マネージャー クライアントに使用する証明書のシリアル番号を指定します。 次のコマンドを使います。`sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`  

     例: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Mac クライアント証明書を更新する  

この手順で SMSID を削除します。 Mac 用の構成マネージャー クライアントで新規または更新された証明書を使用するには、新しい ID が必要です。  

> [!IMPORTANT]  
> クライアント SMSID を置き換えたら、Configuration Manager コンソール内の古いリソースを削除するときに、保存されているクライアント履歴も削除します。 たとえば、そのクライアントのハードウェア インベントリ履歴などです。  


1. ユーザー証明書を更新する必要がある Mac コンピューターのデバイス コレクションを作成します。  

2. **[資産とコンプライアンス]** ワークスペースで、 **構成項目の作成ウィザード** を開始します。  

3. ウィザードの **[全般]** ページで、次の情報を指定します。  

    - **名前**:**Mac の SMSID の削除**  

    - **[種類]** :**Mac OS X**  

4. **[サポートされているプラットフォーム]** ページで、すべての Mac OS X バージョンを選択します。  

5. **[設定]** ページで、 **[新規作成]** を選択します。 **[設定の作成]** ウィンドウで次の情報を指定します。  

    - **名前**:**Mac の SMSID の削除**  

    - **[設定の種類]** :**スクリプト**  

    - **[データ型]** :**文字列**  

6. **[設定の作成]** ウィンドウの **[検索スクリプト]** で **[スクリプトの追加]** を選択します。 この操作により、SMSID が構成されている Mac コンピューターを検出するスクリプトが指定されます。  

7. **[探索スクリプトの編集]** ウィンドウで、次のシェル スクリプトを入力します。  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. **[OK]** を選択して、 **[探索スクリプトの編集]** ウィンドウを閉じます。  

9. **[設定の作成]** ウィンドウの **[修復スクリプト (オプション)]** で、 **[スクリプトの追加]** を選択します。 この操作により、Mac コンピューターで見つかった SMSID を削除するスクリプトが指定されます。  

10. **[修復スクリプトの作成]** ウィンドウで、次のシェル スクリプトを入力します。  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. **[OK]** を選択して **[修復スクリプトの作成]** ウィンドウを閉じます。  

12. **[コンプライアンス規則]** ページで **[新規]** を選択します。 次に、 **[規則の作成]** ウィンドウで次の情報を指定します。  

    - **名前**:**Mac の SMSID の削除**  

    - **[選択した設定]:** **[参照]** を選択し、前に指定した探索スクリプトを選びます。  

    - **[次の値]** フィールドに「**存在しないドメインと既定のペア (com.microsoft.ccmclient, SMSID)** 」と入力します。  

    - オプション **[この設定が対応していない場合に指定した修復スクリプトを実行する]** を有効にします。  

13. ウィザードを完了します。  

14. この構成項目を含む構成基準を作成します。 ターゲット コレクションに、基準を展開します。  

     詳細については、[構成基準の作成方法](../../../compliance/deploy-use/create-configuration-baselines.md)に関するページを参照してください。  

15. SMSID を削除した Mac コンピューターに新しい証明書をインストールしたら、次のコマンドを実行して、新しい証明書を使用するクライアントを構成します。  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>関連項目

[Mac にクライアントを展開する準備](prepare-to-deploy-mac-clients.md)

[Mac クライアントを維持する](../manage/maintain-mac-clients.md)
