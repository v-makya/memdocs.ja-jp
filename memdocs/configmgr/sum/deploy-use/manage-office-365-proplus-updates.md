---
title: Office 365 ProPlus の更新プログラムの管理
titleSuffix: Configuration Manager
description: Configuration Manager が WSUS カタログからサイト サーバーに Office 365 のクライアント更新プログラムを同期したら、その更新プログラムをクライアントに展開できるようになります。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 09d8f0a37e9ed4308c5c8ffcf005c788612be235
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709504"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Configuration Manager での Office 365 ProPlus の管理

*適用対象:Configuration Manager (Current Branch)*

> [!Note]
> 2020 年 4 月 21 日以降、Office 365 ProPlus は、**Microsoft 365 Apps for enterprise** に名前が変更されます。 詳細については、「[Office 365 ProPlus の名前の変更](https://docs.microsoft.com/deployoffice/name-change)」を参照してください。 コンソールの更新中は、Configuration Manager コンソールやサポート ドキュメントに古い名前へのリファレンスが表示される場合があります。

Configuration Manager では、次の方法で Office 365 ProPlus アプリを管理できます。

- [Office 365 アプリを展開する](#deploy-office-365-apps):[Office 365 クライアント管理ダッシュボード](office-365-dashboard.md)から Office 365 インストーラーを起動すると、Office 365 アプリの最初のインストール操作をより簡単にすることができます。 ウィザードに従って、Office 365 のインストール設定を構成し、Office コンテンツ配信ネットワーク (CDN) からファイルをダウンロードして、コンテンツを含むスクリプト アプリケーションを作成して展開することができます。

- [Office 365 更新プログラムを展開する](#deploy-office-365-updates):ソフトウェア更新プログラム管理ワークフローを使用して、Office 365 のクライアント更新プログラムを管理できます。 マイクロソフトが Office コンテンツ配信ネットワーク (CDN) に対する新しい Office 365 のクライアント更新プログラムを公開するときには、Windows Server Update Services (WSUS) に対する更新パッケージも公開します。 Configuration Manager が WSUS カタログからサイト サーバーに Office 365 クライアント更新プログラムを同期したら、その更新プログラムをクライアントに展開できるようになります。

   > [!NOTE]
   > Configuration Manager バージョン 2002 以降では、接続されていない環境に Office 365 更新プログラムをインポートできます。 詳細については、「[切断されているソフトウェアの更新ポイントからの Office 365 更新プログラムの同期](../get-started/synchronize-office-updates-disconnected.md)」を参照してください。   

- [Office 365 更新プログラムのダウンロード対象言語を追加する](#bkmk_o365_lang):Office 365 でサポートされている言語であれば、その言語の更新プログラムをダウンロード対象に含めることができます。 つまり、Office 365 がその言語をサポートしている限り、Configuration Manager でサポートする必要はありません。 バージョン 1610 より前の Configuration Manager では、Office 365 クライアントに構成されているものと同じ言語の更新プログラムをダウンロードして展開する必要があります。

- [更新チャネルを変更する](#bkmk_channel):グループ ポリシーを使用して、レジストリ キー値の変更を Office 365 クライアントに配信して、更新チャネルを変更することができます。

Office 365 クライアントの情報を確認し、これらの Office 365 管理アクションのいくつかを開始するには、[Office 365 クライアント管理ダッシュボード](office-365-dashboard.md)を使います。

## <a name="deploy-office-365-apps"></a>Office 365 アプリを展開する  
最初の Office 365 アプリのインストールのために、Office 365 クライアント管理ダッシュボードから Office 365 インストーラーを起動します。 ウィザードに従って、Office 365 のインストール設定を構成し、Office コンテンツ配信ネットワーク (CDN) からファイルをダウンロードして、そのファイルのスクリプト アプリケーションを作成して展開することができます。 Office 365 がクライアントにインストールされて [Office 自動更新タスク](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus)が実行されるまで、Office 365 の更新プログラムは適用できません。 テスト目的で、更新タスクを手動で実行することができます。

Configuration Manager の以前のバージョンでは、次の手順で最初にクライアントに Office 365 アプリをインストールする必要があります。
- Office 365 展開ツール (ODT) のダウンロード
- Office 365 のインストール ソース ファイルを、必要なすべての言語パックを含めてダウンロードします。
- Office の正しいバージョンとチャネルを指定する Configuration.xml を生成します。
- 従来のパッケージまたはスクリプト アプリケーションのどちらかを作成して展開し、クライアントが Office 365 アプリをインストールできるようにします。

### <a name="requirements"></a>要件
- Office 365 インストーラーを実行しているコンピューターではインターネット アクセスが必要になります。  
- Office 365 インストーラーを実行しているユーザーには、ウィザードで示されるコンテンツの場所の共有に対する**読み取り**および**書き込み**アクセス権が必要です。
- 404 ダウンロード エラーが発生した場合は、次のファイルをユーザーの %temp% フォルダーにコピーします。
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Configuration Manager バージョン 1806 またはそれ以降を使用して Office 365 アプリを展開します。 
Configuration Manager 1806 以降では、Office カスタマイズ ツールが、Configuration Manager コンソールの Office 365 インストーラーと統合されています。 Office 365 の展開を作成するときに、最新の Office の管理容易性設定を動的に構成できます。 <!--1358149-->

1. Configuration Manager コンソールで **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[Office 365 クライアント管理]** に移動します。
2. 右上のウィンドウで **[Office 365 インストーラー]** をクリックします。 Office 365 クライアントのインストール ウィザードが開きます。
3. **[アプリケーションの設定]** ページでアプリの名前と説明を入力し、ファイルをダウンロードする場所を入力して、 **[次へ]** をクリックします。 場所は &#92;&#92;*server*&#92;*share* として指定する必要があります。
4. **[Office の設定]** ページで、 **[Office カスタマイズ ツールに移動します]** をクリックします。 これにより、[Office カスタマイズ ツール クイック実行](https://config.office.com)が開きます。
5. Office 365 のインストールに必要な設定を構成します。 構成が完了したら、ページの右上にある **[送信]** をクリックします。 
6. **[展開]** ページで、今すぐ展開するか後で展開するかを決定します。 後で展開することを選択した場合は、 **[ソフトウェア ライブラリ]**  >  **[アプリケーション管理]**  >  **[アプリケーション]** でアプリケーションを検索できます。  
7. **[概要]** ページで、設定を確認します。 
8. Office 365 クライアントのインストール ウィザードが完了したら、 **[次へ]** をクリックし、 **[閉じる]** をクリックします。 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Configuration Manager バージョン 1802 またはそれより前のバージョンを使用して Office 365 アプリを展開します。

1. Configuration Manager コンソールで **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[Office 365 クライアント管理]** に移動します。
2. 右上のウィンドウで **[Office 365 インストーラー]** をクリックします。 Office 365 クライアントのインストール ウィザードが開きます。
3. **[アプリケーションの設定]** ページでアプリの名前と説明を入力し、ファイルをダウンロードする場所を入力して、 **[次へ]** をクリックします。 場所は &#92;&#92;*server*&#92;*share* として指定する必要があります。
4. **[クライアント設定のインポート]** ページで、Office 365 クライアントの設定を既存の XML 構成ファイルからインポートするか、手動で設定を指定するかを選択します。 完了したら、 **[次へ]** をクリックします。  

    既存の構成ファイルを使用する場合は、ファイルの場所を入力し、ステップ 7 に進みます。 場所は &#92;&#92;*server*&#92;*share*&#92;*filename*.XML の形式で指定する必要があります。
    > [!IMPORTANT]    
    > XML 構成ファイルには、[Office 365 ProPlus クライアントでサポートされる言語](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016)のみを含める必要があります。

5. **[クライアント製品]** ページで、使用する Office 365 スイートを選択します。 含めるアプリケーションを選択します。 含める必要がある追加の Office 製品を選択し、 **[次へ]** をクリックします。
6. **[クライアント設定]** ページで、含める設定を選び、 **[次へ]** をクリックします。
7. **[展開]** ページで、アプリケーションを展開するかどうかを選び **[次へ]** をクリックします。 <br/>ウィザードでパッケージを展開しないことを選択した場合は、ステップ 9 に進みます。
8. 一般的なアプリケーション展開の場合と同様に、ウィザードの残りのページを構成します。 詳細については、「[アプリケーションの作成手順と展開手順](../../apps/get-started/create-and-deploy-an-application.md)」を参照してください。
9. ウィザードを完了します。
10. アプリケーションは **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[アプリケーション管理]**  >  **[アプリケーション]** から展開または編集することができます。    

Office 365 インストーラーを使用して Office 365 アプリケーションを作成して展開した場合、既定では Configuration Manager で Office 更新プログラムが管理されません。 Office 365 クライアントで Configuration Manager から更新プログラムを受信できるようにする場合は、「[Configuration Manager で Office 365 の更新プログラムを展開する](#deploy-office-365-updates)」を参照してください。

Office 365 アプリを展開すると、アプリを維持するための自動展開規則を作成できます。 Office 365 アプリの自動展開規則を作成するには、[Office 365 クライアント管理ダッシュボード](office-365-dashboard.md)から **[ADR の作成]** をクリックします。 製品を選択するときに **[Office 365 クライアント]** を選択します。 詳細については、「[ソフトウェア更新プログラムの自動展開](automatically-deploy-software-updates.md)」を参照してください。


## <a name="drill-through-required-office-365-updates"></a>必要な Office 365 更新プログラムをドリルスルーする
<!--4224414-->
*(バージョン 1906 で導入)*

特定の Office 365 ソフトウェア更新プログラムが必要なデバイスを確認するため、コンプライアンスに関する統計情報をドリルダウンできます。 デバイスの一覧を表示するには、更新プログラムとデバイスが属するコレクションを表示するアクセス許可が必要です。 デバイスの一覧にドリルダウンするには、次のようにします。

1. **[ソフトウェア ライブラリ]**  >  **[Office 365 クライアント管理]**  >  **[Office 365 の更新プログラム]** の順に移動します。
1. 少なくとも 1 つのデバイスによって必要とされる任意の更新プログラムを選択します。
1. **[概要]** タブを表示して、 **[統計情報]** で円グラフを見つけます。
1. 円グラフの横にある **[View Required]\(必須の表示\)** ハイパーリンクを選択して、デバイスの一覧にドリルダウンします。
1. このアクションによって、更新プログラムが必要なデバイスを確認できる **[デバイス]** の下の一時ノードに移動されます。 一覧から新しいコレクションを作成するなど、ノードに対して操作を行うこともできます。


## <a name="deploy-office-365-updates"></a>Office 365 更新プログラムを展開する

Configuration Manager で Office 365 の更新プログラムを展開するには、次の手順を使用します。

1. Configuration Manager を使用して Office 365 クライアントの更新プログラムを管理するための[要件を確認します](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) (この記事の「**構成マネージャーを使用して Office 365 クライアントの更新を管理するための要件**」セクションを参照してください)。  

2. Office 365 のクライアント更新プログラムを同期するための[ソフトウェア更新ポイントを構成します](../get-started/configure-classifications-and-products.md)。 分類の**更新プログラム**を設定して、製品の **Office 365 クライアント**を選択します。 分類の**更新プログラム**を使用するには、ソフトウェア更新ポイントの構成後にソフトウェア更新プログラムを同期します。
3. Office 365 クライアントが Configuration Manager から更新プログラムを受信できるようにします。 クライアントを有効にするには、Configuration Manager クライアント設定またはグループ ポリシーを使用します。

    **方法 1**:Configuration Manager バージョン 1606 以降では、Configuration Manager クライアント設定を使用して Office 365 のクライアント エージェントを管理できます。 この設定を構成し、Office 365 の更新プログラムを展開すると、Configuration Manager クライアント エージェントは、Office 365 のクライアント エージェントと通信して、配布ポイントから更新プログラムをダウンロードしてインストールします。 Configuration Manager は、Office 365 ProPlus クライアント エージェント設定のインベントリを取得します。    

      1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クライアント設定]** の順にクリックします。  

      2. クライアント エージェントを有効にする適切なデバイスの設定を開きます。 既定とカスタムのクライアント設定の詳細については、[クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)に関するページをご覧ください。  

      3. **[ソフトウェアの更新]** を選択し、 **[Office 365 クライアント エージェントの管理を有効にする]** の設定に **[はい]** を設定します。  

    **方法 2**:Office 展開ツールまたはグループ ポリシーを使用して、Configuration Manager から [Office 365 クライアントが更新プログラムを受信できるようにします](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient)。  

4. [Office 365 の更新プログラムをクライアントに展開します](deploy-software-updates.md)。

> [!Important]
> - Configuration Manager バージョン 1706 以降では、Office 365 のクライアント更新プログラムは **[Office 365 クライアント管理]**  > **[Office 365 の更新プログラム]** ノードに移動されています。 この移動による現在の ADR 構成への影響はありません。 
> - バージョン 1610 より前の Configuration Manager では、Office 365 クライアントに構成されているものと同じ言語の更新プログラムをダウンロードして展開する必要があります。 たとえば、Office 365 クライアントに en-us と de-de の言語を構成しているとします。 サイト サーバーで、適用可能な Office 365 更新プログラムに対して en-us のコンテンツのみをダウンロードして展開します。 ユーザーがソフトウェア センターからこの更新プログラムのインストールを開始すると、更新プログラムは de-de のコンテンツのダウンロード中にハングします。 

> [!NOTE]  
>
> Office 365 ProPlus が最近インストールされた場合、そのインストール方法によっては、更新チャネルがまだ設定されていない可能性があります。 その場合、展開された更新プログラムは適用外として検出されます。 Office 365 ProPlus をインストールするときに、[スケジュール済みの自動更新タスク](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus)が作成されます。 この状況では、更新チャネルを設定し、更新プログラムが適用可能として検出されるようにするために、このタスクを少なくとも 1 回実行する必要があります。
>
> Office 365 ProPlus が最近インストールされていて、展開された更新プログラムが検出されない場合は、クライアント上で、テストのために Office 自動更新タスクを手動で起動してから、[ソフトウェア更新プログラムの展開評価サイクル](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process)を開始できます。 タスク シーケンスでこれを実行する手順について詳しくは、「[タスク シーケンスでの Office 365 ProPlus の更新](manage-office-365-proplus-updates.md#updating-office-365-proplus-in-a-task-sequence)」を参照してください。

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Office 365 の更新プログラムの動作とクライアント通知を再起動する
Office 365 クライアントに更新プログラムを展開する場合、再起動の動作とクライアント通知は、Configuration Manager のバージョンによって異なります。 次の表では、クライアントが Office 365 の更新プログラムを受け取るときのエンド ユーザーのエクスペリエンスに関する情報を示します。

|Configuration Manager バージョン |エンド ユーザー エクスペリエンス|  
|----------------|---------------------|
|1706、1710|クライアントは、ポップアップとアプリ内通知、および更新プログラムをインストールする前にカウント ダウン ダイアログを受け取ります。|
|1802| クライアントは、ポップアップとアプリ内通知、および更新プログラムをインストールする前にカウント ダウン ダイアログを受け取ります。 </br>Office 365 アプリケーションが Office 365 クライアント更新プログラムの適用時に実行されている場合、Office アプリケーションは強制的に閉じられません。 代わりに、更新プログラムのインストールでシステムの再起動が必要であることが示されます <!--510006-->|


> [!Important]
>
>Configuration Manager バージョン 1706 では、次の詳細に注意してください。
>
>- 今後 48 時間以内に期限に達し、コンテンツの更新がダウンロードされていることを通知するアイコンが、必要なアプリのタスク バーの通知領域に表示されます。 
>- 今後 7.5 時間以内に期限に達し、更新プログラムがダウンロードされている必要なアプリに対し、カウントダウン ダイアログが表示されます。 ユーザーは、期限に達する前に、カウントダウン ダイアログを 3 回まで延期することができます。 延期すると、2 時間後にもう一度カウントダウンが表示されます。 延期しない場合は、30 分のカウントダウンの終了後、更新プログラムがインストールされます。
>- ユーザーが通知領域内のアイコンをクリックするまで、ポップアップ通知が表示されない場合があります。 さらに、通知領域に最小限のスペースがある場合、ユーザーが通知領域を開くか展開しない限り、通知アイコンが表示されない場合があります。 
>- 通知とカウントダウン ダイアログは、ユーザーがデバイスでアクティブに作業していない間に開始する場合があります。 たとえば、デバイスが一晩中ロックされている場合、デバイス上で実行中の Office アプリを強制的に閉じて更新プログラムをインストールすることができます。 アプリを閉じる前に、Office はデータ損失を防ぐため、アプリ データを保存します。 
>- 期限が過去またはできるだけ早く開始するように設定されている場合は、実行中の Office アプリが通知なく強制的に閉じられる場合があります。 
>- ユーザーが期限前に Office 更新プログラムをインストールすると、Configuration Manager は、期限に達したときに、更新プログラムがインストールされていることを確認します。 デバイスで更新プログラムが検出されない場合、更新プログラムがインストールされます。 
>- アプリ内通知バーは、更新プログラムがダウンロードされる前に実行されている Office アプリでは表示されません。 更新プログラムをダウンロードすると、アプリ内通知は新しく開いたアプリに対してのみ表示されます。
>- サービス ウィンドウによってトリガーされるまたは営業時間外にスケジュールされている Office 更新プログラムの場合、実行中の Office アプリを強制的に閉じて、通知せずに更新プログラムをインストールすることがあります。 
>- 詳細については、[Office 365 のエンド ユーザー更新通知](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)に関する記事を参照してください


## <a name="add-languages-for-office-365-update-downloads"></a><a name="bkmk_o365_lang"></a> Office 365 更新プログラムのダウンロード対象言語を追加する
Configuration Manager のサポートを追加して、Office 365 でサポートされている任意の言語の更新プログラムをダウンロードできます。

### <a name="download-updates-for-additional-languages-in-version-1902"></a>バージョン 1902 で追加言語の更新プログラムをダウンロードする
<!--3555955-->

Configuration Manager 1902 以降、更新のワークフローは、**Windows Update** では 38 の言語に分割される一方、**Office 365 クライアント更新**では多数の言語が追加されます。

必要な言語を選択するには、次の場所にある **[言語の選択]** ページを使用します。
- 自動展開規則の作成ウィザード
- ソフトウェアの更新の展開ウィザード
- ソフトウェア更新プログラムのダウンロード ウィザード
- 自動展開規則のプロパティ

**[言語の選択]** ページで、 **[Office 365 Client Update]\(Office 365 クライアント更新プログラム\)** を選択してから、 **[編集]** をクリックします。 Office 365 に必要な言語を追加してから、 **[OK]** をクリックします。

![Office 365 の追加言語を追加するスクリーンショット](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>バージョン 1810 およびそれ以前で追加言語の更新プログラムをダウンロードするためのサポートを追加するには

以下の手順は、中央管理サイトまたはスタンドアロンのプライマリ サイトにあるソフトウェアの更新ポイントで実行してください。

> [!IMPORTANT]  
> Office 365 更新プログラムの言語を追加するための構成設定はサイト全体に適用されます。 以下の手順に従って言語を追加すると、その言語における Office 365 のすべての更新プログラムが、ソフトウェア更新プログラムの展開ウィザードまたはソフトウェア更新プログラムのダウンロード ウィザードの **[言語の選択]** ページで選択した言語に加えてダウンロードされます。

1. 管理ユーザーとしてコマンド プロンプトから「*wbemtest*」と入力し、Windows Management Instrumentation テストを開きます。
2. **[接続]** をクリックして「*root\sms\site_&lt;siteCode&gt;* 」と入力します。
3. **[クエリ]** をクリックして、「*select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"* 」というクエリを実行します。  
   ![WMI query](../media/1-wmiquery.png)
4. 結果ウィンドウで、目的のサイト コード (中央管理サイトまたはスタンドアロンのプライマリ サイト) に該当するオブジェクトをダブルクリックします。
5. **Props** プロパティを選択し、 **[プロパティの編集]** をクリックして、 **[埋め込みを表示]** をクリックします。
   ![Property editor](../media/2-propeditor.png)
6. 1 つ目のクエリ結果から順に各オブジェクトを開いていき、**PropertyName** プロパティが **AdditionalUpdateLanguagesForO365** であるオブジェクトを見つけます。
7. **[Value2]** を選択し、 **[プロパティの編集]** をクリックします。  
   ![Edit the Value2 property](../media/3-queryresult.png)
8. 新しい言語を **Value2** プロパティに追加して **[プロパティの保存]** をクリックします。 <br/> たとえば、pt-pt (ポルトガル語 - ポルトガル)、af-za (アフリカーンス語 - 南アフリカ)、nn-no (ノルウェー語 (ニーノシク) - ノルウェー) を追加します。例の言語の場合は「`pt-pt,af-za,nn-no`」と入力します。 言語間にはスペースを使用しないでください。
 
   ![プロパティ エディターでの言語の追加](../media/4-props.png)  
9. **[閉じる]** 、 **[閉じる]** 、 **[プロパティの保存]** 、 **[オブジェクトの保存]** の順にクリックします (ここで **[閉じる]** をクリックした場合、値は破棄されます)。 **[閉じる]** 、 **[終了]** の順にクリックして、Windows Management Instrumentation Tester を終了します。
10. Configuration Manager コンソールで **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[Office 365 クライアント管理]**  >  **[Office 365 Updates (Office 365 更新プログラム)]** に移動します。
11. 以後、Office 365 更新プログラムをダウンロードすると、ウィザードで選択した言語およびこの手順で構成した言語の更新プログラムがダウンロードされます。 正しい言語の更新プログラムがダウンロードされたことを確認するには、その更新プログラムのパッケージ ソースにアクセスし、その言語コードを名前に含んだファイルを探します。  
    ![Filenames with additional languages](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>タスク シーケンスでの Office 365 ProPlus の更新
Office 365 の更新プログラムをインストールするために[ソフトウェア更新プログラムのインストール](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) タスク シーケンスの手順を使う場合、展開された更新プログラムが適用外として検出される可能性があります。  これは、スケジュールされている Office 自動更新タスクが一度も実行されていない場合に発生する可能性があります (「[Office 365 更新プログラムを展開する](manage-office-365-proplus-updates.md#deploy-office-365-updates)」の注を参照)。 たとえば、この手順を実行する直前に Office 365 ProPlus をインストールした場合、これが発生する可能性があります。

展開された更新プログラムが正しく検出されるように、更新チャネルを確実に設定するためには、次の方法のいずれかを使います。

**方法 1:**
1. 同じバージョンの Office 365 ProPlus があるコンピューターで、タスク スケジューラ (taskschd.msc) を開き、Office 365 自動更新タスクを特定します。 通常は **[タスク スケジューラ ライブラリ]**  > **[Microsoft]** > **[Office]** にあります。
2. 自動更新タスクを右クリックして、 **[プロパティ]** を選択します。
3. **[アクション]** タブに移動して、 **[編集]** をクリックします。 コマンドとすべての引数をコピーします。 
4. Configuration Manager コンソールで、タスク シーケンスを編集します。
5. タスク シーケンスの**ソフトウェア更新プログラムのインストール**手順の前に、新しい**コマンド ラインの実行**手順を追加します。 同じタスク シーケンスの一部として Office 365 ProPlus をインストールする場合は、Office のインストール後にこの手順を実行することを確認します。
6. Office 自動更新のスケジュールされたタスクから収集した引数とコマンドをコピーします。 
7. **[OK]** をクリックします。 

**方法 2:**
1. 同じバージョンの Office 365 ProPlus があるコンピューターで、タスク スケジューラ (taskschd.msc) を開き、Office 365 自動更新タスクを特定します。 通常は **[タスク スケジューラ ライブラリ]**  > **[Microsoft]** > **[Office]** にあります。
2. Configuration Manager コンソールで、タスク シーケンスを編集します。
3. タスク シーケンスの**ソフトウェア更新プログラムのインストール**手順の前に、新しい**コマンド ラインの実行**手順を追加します。 同じタスク シーケンスの一部として Office 365 ProPlus をインストールする場合は、Office のインストール後にこの手順を実行することを確認します。
4. コマンド ライン フィールドに、スケジュールされたタスクを実行するコマンド ラインを入力します。 次の例を見て、引用符で囲まれた文字列が手順 1 で特定したタスクのパスおよび名前と一致していることを確認します。  

    例: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. **[OK]** をクリックします。 

## <a name="update-channels-for-microsoft-365-apps"></a><a name="bkmk_channel"></a> Microsoft 365 アプリのチャネルを更新する
<!--6298093-->
Office 365 ProPlus の名前が **Microsoft 365 Apps for enterprise** に変更されたときに、更新プログラム チャネルの名前も変更されました。 自動展開規則 (ADR) を使用して更新プログラムを展開していて、それらが**タイトル** プロパティに依存している場合は、ADR を変更する必要があります。 それは、Microsoft Update カタログ内の更新プログラム パッケージの名前が変更されているためです。

現在、Office 365 ProPlus の更新プログラム パッケージのタイトルは、次の例に示すように、"Office 365 Client Update" で始まっています。

&nbsp; &nbsp; Office 365 Client Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.20648)

6 月 9 日以降にリリースされる更新プログラム パッケージの場合、タイトルは次の例に示すように "Microsoft 365 Apps Update" で始まります。

&nbsp; &nbsp; Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)
</br>
</br>

|新しいチャネル名|以前のチャネル名|
|--|--|
|半期エンタープライズ チャネル|半期チャネル|
|半期エンタープライズ チャネル (プレビュー)|半期チャネル (対象指定)|
|月間エンタープライズ チャネル|N/A|
|最新チャネル|月次チャネル|
|最新チャネル (プレビュー)|月次チャネル (対象指定)|
|ベータ チャネル|Insider|

ADR の変更方法の詳細については、「[ソフトウェア更新プログラムの自動展開](automatically-deploy-software-updates.md)」を参照してください。 名前の変更の詳細については、「[Office 365 ProPlus の名前の変更](https://docs.microsoft.com/deployoffice/name-change)」を参照してください。


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Configuration Manager から更新プログラムを適用できるように Office 365 クライアントを設定した後で更新チャネルを変更する

Office 365 ProPlus を展開した後、グループ ポリシーまたは Office 展開ツール (ODT) で更新プログラム チャネルを変更できます。 たとえば、半期チャネルから半期チャネル (対象指定) にデバイスを移行できます。 チャネルを変更すると、完全バージョンを再インストールまたはダウンロードしなくても Office は自動的に更新されます。 詳細については、「[組織内のデバイスの Office 365 ProPlus 更新チャネルを変更する](https://docs.microsoft.com//deployoffice/change-update-channels)」を参照してください。


## <a name="next-steps"></a>次のステップ

Configuration Manager で Office 365 クライアント管理ダッシュボードを使って、Office 365 クライアントの情報を確認し、Office 365 アプリを展開します。 詳細については、「[Office 365 クライアント管理ダッシュボード](office-365-dashboard.md)」をご覧ください。
