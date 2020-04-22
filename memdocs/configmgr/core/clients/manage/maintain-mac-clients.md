---
title: Mac クライアントを維持する
titleSuffix: Configuration Manager
description: Configuration Manager の Mac クライアントのメンテナンス タスク
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 520315c4bb740f23a9534e532f75c3bd3ee66a2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690060"
---
# <a name="maintain-mac-clients"></a>Mac クライアントを維持する
*適用対象:Configuration Manager (Current Branch)*

ここでは、Mac クライアントをアンインストールし、その証明書を更新するための手順を示します。

##  <a name="uninstalling-the-mac-client"></a>Mac クライアントをアンインストールする  

1.  Mac コンピューターで、ターミナル ウィンドウを開き、**macclient.dmg** が置かれているフォルダーに移動します。  

2.  ツール フォルダーに移動し、次のコマンドラインを入力します。  

     `./CMUninstall -c`

    > [!NOTE]  
    >  **-c** プロパティは、クライアントのアンインストールで、クライアントのクラッシュ ログとログ ファイルも削除するように指示します。 クライアントを後で再インストールする場合に混乱が生じるのを避けるためにも、この処置をお勧めします。  

3.  必要に応じて、Configuration Manager が使用していたクライアント認証証明書を手動で削除するか、失効させます。 CMUnistall では、この証明書は削除または失効されません。  

##  <a name="renewing-the-mac-client-certificate"></a>Mac クライアント証明書の更新  
 Mac クライアント証明書を更新する方法は、次の 2 通りあります。  

-   [証明書の更新ウィザード](#renew-certificate-wizard)  

-   [証明書を手動で更新する](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>証明書の更新ウィザード  

1. ccmclient.plist ファイルで "*文字列*" として次の値を構成して、証明書の更新ウィザードがいつ開くかを制御します。  

   - **RenewalPeriod1**: ユーザーが証明書を更新できる 1 番目の更新期間を秒単位で指定します。 既定値は 3,888,000 秒 (45 日) です。 期間は既定値に戻されるため、300 より小さい値に構成しないでください。 

   - **RenewalPeriod2**: ユーザーが証明書を更新できる 2 番目の更新期間を秒単位で指定します。 既定値は 259,200 秒 (3 日) です。 この値を 300 秒以上、**RenewalPeriod1** の値以下に設定した場合は、その値が使われます。 **RenewalPeriod1** の値が 3 日より大きい場合は、 **RenewalPeriod2**の値として 3 日が使われます。  **RenewalPeriod1** の値が 3 日より小さい場合は、 **RenewalPeriod2** が **RenewalPeriod1**と同じ値に設定されます。  

   - **RenewalReminderInterval1**: 1 番目の更新期間中に、証明書の更新ウィザードがユーザーに表示される頻度を秒単位で指定します。 既定値は 86,400 秒 (1 日) です。 **RenewalReminderInterval1** を 300 秒以上、 **RenewalPeriod1**の値未満に設定した場合は、その値が使われます。 それ以外の場合は、既定値の 1 日が使われます。  

   - **RenewalReminderInterval2**: 2 番目の更新期間中に、証明書の更新ウィザードがユーザーに表示される頻度を秒単位で指定します。 既定値は 28,800 秒 (8 時間) です。 **RenewalReminderInterval2** を 300 秒以上、 **RenewalReminderInterval1** の値以下、且つ **RenewalPeriod2**の値以下に設定した場合は、その値が使われます。 それ以外の場合は、8 時間が使われます。  

     **例:** 既定値のままにすると、証明書が失効する 45 日前から、24 時間ごとにウィザードが開きます。  証明書が失効する 3 日前になると、8 時間に 1 回ウィザードが開くようになります。  

     **例:** 1 回目の更新期間を 20 日に設定するには、次のコマンドライン (またはスクリプト) を使用します。  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. 証明書の更新ウィザードが開いたときには、通常、 **[ユーザー名]** フィールドと **[サーバー名]** フィールドに既に値が挿入されており、ユーザーはパスワードを入力するだけで証明書を更新できます。  

   > [!NOTE]  
   >  ウィザードが表示されなかった場合や、間違ってウィザードを閉じてしまった場合は、 **Configuration Manager** の環境設定ページで **[更新]** をクリックして、ウィザードを開いてください。  

###  <a name="renew-certificate-manually"></a>証明書を手動で更新する  
 Mac クライアント証明書の一般的な有効期間は 1 年間です。 Configuration Manager への登録時に必要なユーザー証明書は、自動的に更新されません。そのため、次の手順に従って証明書を手動で更新する必要があります。  

> [!IMPORTANT]  
>  証明書が期限切れになった場合、Mac クライアントのアンインストール、再インストール、および再登録を行う必要があります。  

 この手順で SMSID が削除されます。SMSID は、同じ Mac コンピューターの新しい証明書を要求するために必要です。 クライアント SMSID を削除して置き換えると、Configuration Manager コンソールからクライアントが削除された後に、インベントリなどの保存されているクライアント履歴も削除されます。  

1.  ユーザー証明書を更新する必要がある Mac コンピューターのデバイス コレクションを作成します。  

    > [!WARNING]  
    >  Configuration Manager は、Mac コンピューター用に登録されている証明書の有効期間を監視しません。 Configuration Manager とは関係なく有効期間を監視して、このコレクションに追加する Mac コンピューターを特定する必要があります。  

2.  **[資産とコンプライアンス]** ワークスペースで、**構成項目の作成ウィザード**を開始します。  

3.  **[全般]** ページで、以下の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[種類]:Mac OS X**  

4.  **[サポートされているプラットフォーム]** ページで、すべての Mac OS X バージョンが選択されていることを確認します。  

5.  **[設定]** ページで **[新規作成]** を選択し、 **[設定の作成]** ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[設定の種類]:スクリプト**  

    -   **[データ型]:文字列**  

6.  **[設定の作成]** ダイアログ ボックスの **[検索スクリプト]** で **[スクリプトの追加]** を選択し、SMSID が構成されている Mac コンピューターを検出するスクリプトを指定します。  

7.  **[探索スクリプトの編集]** ダイアログ ボックスで、次のシェル スクリプトを入力します。  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  **[OK]** を選択して、 **[探索スクリプトの編集]** ダイアログ ボックスを閉じます。  

9. **[設定の作成]** ダイアログ ボックスの **[修復スクリプト (オプション)]** で、 **[スクリプトの追加]** を選択して、Mac コンピューターで見つかった SMSID を削除するスクリプトを指定します。  

10. **[修復スクリプトの作成]** ダイアログ ボックスで、次のシェル スクリプトを入力します。  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. **[OK]** を選択して **[修復スクリプトの作成]** ダイアログ ボックスを閉じます。  

12. ウィザードの **[コンプライアンス規則]** ページで **[新規作成]** をクリックし、 **[規則の作成]** ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **選択された設定:** **[参照]** を選んで、前に指定した探索スクリプトを選択します。  

    -   **[次の値]** フィールドに「**存在しないドメインと既定のペア (com.microsoft.ccmclient, SMSID)** 」と入力します。  

    -   オプション **[この設定が対応していない場合に指定した修復スクリプトを実行する]** を有効にします。  

13. 構成項目の作成ウィザードを完了します。  

14. 作成した構成項目を含む構成基準を作成し、それを手順 1 で作成したデバイス コレクションに展開します。  

     構成基準の作成方法と展開方法の詳細については、[構成基準の作成方法](../../../compliance/deploy-use/create-configuration-baselines.md)に関するページと[構成基準を展開する方法](../../../compliance/deploy-use/deploy-configuration-baselines.md)に関するページを参照してください。  

15. SMSID を削除した Mac コンピューターで、次のコマンドを実行して新しい証明書をインストールします。  

    ``` Shell
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     プロンプトが表示されたら、コマンドを実行するスーパー ユーザー アカウントのパスワードを指定し、Active Directory ユーザー アカウントのパスワードを指定します。  

16. Mac コンピューターで、登録する証明書を Configuration Manager に制限するには、ターミナル ウィンドウを開き、次のように変更します。  

    a.  コマンド `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access` を入力します

    b.  **[キーチェーン アクセス]** ダイアログの **[キーチェーン]** セクションで、 **[システム]** を選択し、 **[カテゴリ]** セクションの **[キー]** を選択します。  

    c.  キーを展開してクライアント証明書を表示します。 インストールした秘密キーの証明書を特定したら、そのキーをダブルクリックします。  

    d.  **[アクセス制御]** タブで、 **[アクセスを許可する前に確認する]** を選択します。  

    e.  **/Library/Application Support/Microsoft/CCM** を参照し、 **[CCMClient]** を選択して **[追加]** を選択します。  

    f.  **[変更を保存]** をクリックし、 **[キーチェーン アクセス]** ダイアログ ボックスを閉じます。  

17. Mac コンピューターを再起動します。  

