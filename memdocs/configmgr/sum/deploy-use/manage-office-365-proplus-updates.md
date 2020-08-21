---
title: Microsoft 365 Apps 更新プログラムの管理
titleSuffix: Configuration Manager
description: Configuration Manager によって WSUS カタログからサイト サーバーに Microsoft 365 Apps クライアントの更新プログラムが同期されたら、更新プログラムをクライアントに展開できるようになります。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 907c8d63d68ee4f34b9d22be24f32ffb1878b715
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696176"
---
# <a name="manage-microsoft-365-apps-with-configuration-manager"></a>Configuration Manager での Microsoft 365 Apps の管理

*適用対象:Configuration Manager (Current Branch)*

> [!Note]
> 2020 年 4 月 21 日以降、Office 365 ProPlus は、**Microsoft 365 Apps for enterprise** に名前が変更されます。 詳細については、「[Office 365 ProPlus の名前の変更](/deployoffice/name-change)」を参照してください。 コンソールの更新中は、Configuration Manager コンソールやサポート ドキュメントに古い名前へのリファレンスが表示される場合があります。

Configuration Manager では、次の方法で Microsoft 365 Apps を管理できます。

- [Microsoft 365 Apps を展開する](#bkmk_deploy):[Office 365 クライアント管理ダッシュボード](office-365-dashboard.md)から Microsoft 365 Apps インストーラーを起動すると、Microsoft 365 Apps の最初のインストール操作をより簡単にすることができます。 ウィザードに従って、Microsoft 365 Apps のインストール設定を構成し、Office Content Delivery Network (CDN) からファイルをダウンロードして、コンテンツを含むスクリプト アプリケーションを作成して展開することができます。

- [Microsoft 365 Apps 更新プログラムを展開する](#bkmk_update):ソフトウェア更新プログラム管理ワークフローを使用して、Microsoft 365 Apps クライアントの更新プログラムを管理できます。 Microsoft が Office Content Delivery Network (CDN) に新しい Microsoft 365 Apps 更新プログラムを公開する際には、Windows Server Update Services (WSUS) にも更新プログラム パッケージを公開します。 Configuration Manager によって WSUS カタログからサイト サーバーに Microsoft 365 Apps クライアント更新プログラムが同期されたら、更新プログラムをクライアントに展開できるようになります。

   > [!NOTE]
   > Configuration Manager バージョン 2002 以降では、接続されていない環境に Microsoft 365 Apps 更新プログラムをインポートできます。 詳細については、「[切断されているソフトウェアの更新ポイントからの Microsoft 365 Apps 更新プログラムの同期](../get-started/synchronize-office-updates-disconnected.md)」を参照してください。   

- [Microsoft 365 Apps 更新プログラムのダウンロード対象言語を追加する](#bkmk_o365_lang):Microsoft 365 Apps でサポートされている任意の言語を、Configuration Manager で更新プログラムをダウンロードする際の対象言語として追加できます。 つまり、Microsoft 365 Apps でその言語がサポートされている限り、Configuration Manager でサポートする必要はありません。 バージョン 1610 より前の Configuration Manager では、Microsoft 365 Apps クライアントに構成されているのと同じ言語の更新プログラムをダウンロードして展開する必要があります。

- [更新チャネルを変更する](#bkmk_channel):グループ ポリシーを使用して、レジストリ キー値の変更を Microsoft 365 Apps クライアントに配信して、更新プログラム チャネルを変更することができます。

Microsoft 365 Apps クライアントの情報を確認し、これらの Microsoft 365 Apps 管理アクションのいくつかを開始するには、[Office 365 クライアント管理ダッシュボード](office-365-dashboard.md)を使用します。

## <a name="deploy-microsoft-365-apps"></a><a name="bkmk_deploy"></a>Microsoft 365 Apps を展開する
最初の Microsoft 365 Apps のインストールのために、Office 365 クライアント管理ダッシュボードから Microsoft 365 Apps インストーラーを起動します。 ウィザードに従って、Microsoft 365 Apps のインストール設定を構成し、Office Content Delivery Network (CDN) からファイルをダウンロードして、そのファイルのスクリプト アプリケーションを作成して展開することができます。 Microsoft 365 Apps がクライアントにインストールされて [Microsoft 365 Apps 自動更新タスク](/deployoffice/overview-update-process-microsoft-365-apps)が実行されるまでは、Microsoft 365 Apps 更新プログラムは適用できません。 テスト目的で、更新タスクを手動で実行することができます。

以前のバージョンの Configuration Manager では、次の手順に従って、最初にクライアントに Microsoft 365 Apps をインストールする必要があります。
- Office 展開ツール (ODT) をダウンロードします。
- Microsoft 365 Apps のインストール ソース ファイルを、必要なすべての言語パックを含めてダウンロードします。
- Microsoft 365 Apps の正しいバージョンとチャネルを指定する Configuration.xml を生成します。
- レガシ パッケージまたはスクリプト アプリケーションのどちらかを作成して展開し、クライアントが Microsoft 365 Apps アプリをインストールできるようにします。

### <a name="requirements"></a>要件
- インストーラーを実行するコンピューターは、インターネットにアクセスできる必要があります。  
- インストーラーを実行するユーザーには、ウィザードで示されるコンテンツの場所の共有に対する**読み取り**および**書き込み**アクセス権が必要です。
- 404 ダウンロード エラーが発生した場合は、次のファイルをユーザーの %temp% フォルダーにコピーします。
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1806-or-higher"></a>Configuration Manager バージョン 1806 以降を使用して Microsoft 365 Apps を展開する 
Configuration Manager 1806 以降では、Office カスタマイズ ツールが Configuration Manager コンソール内のインストーラーと統合されています。 Microsoft 365 Apps の展開を作成するときに、最新の管理性設定を動的に構成できます。 <!--1358149-->

1. Configuration Manager コンソールで **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[Office 365 クライアント管理]** に移動します。
2. 右上のウィンドウで **[Office 365 インストーラー]** をクリックします。 インストール ウィザードが開きます。
3. **[アプリケーションの設定]** ページでアプリの名前と説明を入力し、ファイルをダウンロードする場所を入力して、 **[次へ]** をクリックします。 場所は &#92;&#92;*server*&#92;*share* として指定する必要があります。
4. **[Office の設定]** ページで、 **[Office カスタマイズ ツールに移動します]** をクリックします。 これにより、[Office カスタマイズ ツール クイック実行](https://config.office.com)が開きます。
5. Microsoft 365 Apps のインストールに必要な設定を構成します。 構成が完了したら、ページの右上にある **[送信]** をクリックします。 
6. **[展開]** ページで、今すぐ展開するか後で展開するかを決定します。 後で展開することを選択した場合は、 **[ソフトウェア ライブラリ]**  >  **[アプリケーション管理]**  >  **[アプリケーション]** でアプリケーションを検索できます。  
7. **[概要]** ページで、設定を確認します。 
8. ウィザードが完了したら、 **[次へ]** をクリックし、 **[閉じる]** をクリックします。 

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1802-and-prior"></a>Configuration Manager バージョン 1802 以前を使用して Microsoft 365 Apps を展開する

1. Configuration Manager コンソールで **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[Office 365 クライアント管理]** に移動します。
2. 右上のウィンドウで **[Office 365 インストーラー]** をクリックします。 インストール ウィザードが開きます。
3. **[アプリケーションの設定]** ページでアプリの名前と説明を入力し、ファイルをダウンロードする場所を入力して、 **[次へ]** をクリックします。 場所は &#92;&#92;*server*&#92;*share* として指定する必要があります。
4. **[クライアント設定のインポート]** ページで、Microsoft 365 Apps クライアントの設定を既存の XML 構成ファイルからインポートするか、手動で設定を指定するかを選択します。 完了したら、 **[次へ]** をクリックします。  

    既存の構成ファイルを使用する場合は、ファイルの場所を入力し、ステップ 7 に進みます。 場所は &#92;&#92;*server*&#92;*share*&#92;*filename*.XML の形式で指定する必要があります。
    > [!IMPORTANT]    
    > XML 構成ファイルには、[Office 2016 でサポートされている言語](/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016)のみを含める必要があります。

5. **[クライアント製品]** ページで、使用する Microsoft 365 Apps スイートを選択します。 含めるアプリケーションを選択します。 含める必要がある追加の製品を選択し、 **[次へ]** をクリックします。
6. **[クライアント設定]** ページで、含める設定を選び、 **[次へ]** をクリックします。
7. **[展開]** ページで、アプリケーションを展開するかどうかを選び **[次へ]** をクリックします。 <br/>ウィザードでパッケージを展開しないことを選択した場合は、ステップ 9 に進みます。
8. 一般的なアプリケーション展開の場合と同様に、ウィザードの残りのページを構成します。 詳細については、「[アプリケーションの作成手順と展開手順](../../apps/get-started/create-and-deploy-an-application.md)」を参照してください。
9. ウィザードを完了します。
10. アプリケーションは **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[アプリケーション管理]**  >  **[アプリケーション]** から展開または編集することができます。

インストーラーを使用して Microsoft 365 Apps を作成して展開すると、既定では、Configuration Manager で Microsoft 365 Apps 更新プログラムが管理されません。 Microsoft 365 Apps クライアントで Configuration Manager から更新プログラムを受信できるようにするには、[Configuration Manager で Microsoft 365 更新プログラムを展開する方法についての説明](#bkmk_update)を参照してください。

Microsoft 365 Apps を展開したら、それを維持するための自動展開規則を作成できます。 Microsoft 365 Apps 用の自動展開規則を作成するには、[Office 365 クライアント管理ダッシュボード](office-365-dashboard.md)で **[ADR の作成]** をクリックします。 製品を選択するときに **[Office 365 クライアント]** を選択します。 詳細については、「[ソフトウェア更新プログラムの自動展開](automatically-deploy-software-updates.md)」を参照してください。


## <a name="drill-through-required-microsoft-365-apps-updates"></a>必要な Microsoft 365 Apps 更新プログラムをドリルスルーする
<!--4224414-->
*(バージョン 1906 で導入)*

特定の Microsoft 365 アプリのソフトウェア更新プログラムが必要なデバイスを確認するため、コンプライアンスに関する統計情報をドリルダウンできます。 デバイスの一覧を表示するには、更新プログラムとデバイスが属するコレクションを表示するアクセス許可が必要です。 デバイスの一覧にドリルダウンするには、次のようにします。

1. **[ソフトウェア ライブラリ]**  >  **[Office 365 クライアント管理]**  >  **[Office 365 の更新プログラム]** の順に移動します。
1. 少なくとも 1 つのデバイスによって必要とされる任意の更新プログラムを選択します。
1. **[概要]** タブを表示して、 **[統計情報]** で円グラフを見つけます。
1. 円グラフの横にある **[View Required]\(必須の表示\)** ハイパーリンクを選択して、デバイスの一覧にドリルダウンします。
1. このアクションによって、更新プログラムが必要なデバイスを確認できる **[デバイス]** の下の一時ノードに移動されます。 一覧から新しいコレクションを作成するなど、ノードに対して操作を行うこともできます。


## <a name="deploy-microsoft-365-apps-updates"></a><a name="bkmk_update"></a>Microsoft 365 Apps 更新プログラムを展開する

Configuration Manager で Microsoft 365 Apps 更新プログラムを展開するには、次の手順を使用します。

1. Configuration Manager を使用して Microsoft 365 Apps クライアントの更新プログラムを管理するための[要件を確認](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates)します (この記事の、**Configuration Manager を使用して Microsoft 365 Apps クライアントの更新プログラムを管理するための要件**に関するセクションを参照してください)。  

2. Microsoft 365 Apps クライアントの更新プログラムを同期するための[ソフトウェアの更新ポイントを構成](../get-started/configure-classifications-and-products.md)します。 分類の**更新プログラム**を設定して、製品の **Office 365 クライアント**を選択します。 分類の**更新プログラム**を使用するには、ソフトウェア更新ポイントの構成後にソフトウェア更新プログラムを同期します。
3. Microsoft 365 Apps クライアントで Configuration Manager から更新プログラムを受信できるようにします。 クライアントを有効にするには、Configuration Manager クライアント設定またはグループ ポリシーを使用します。

    **方法 1**:Configuration Manager バージョン 1606 以降では、Configuration Manager のクライアント設定を使用して、Microsoft 365 Apps クライアント エージェントを管理できます。 この設定を構成し、Microsoft 365 Apps 更新プログラムを展開すると、Configuration Manager クライアント エージェントは Microsoft 365 Apps クライアント エージェントと通信し、配布ポイントから更新プログラムをダウンロードしてインストールします。 Configuration Manager は、Microsoft 365 Apps クライアントの設定のインベントリを取得します。    

      1. Configuration Manager コンソールで、 **[管理]**  >  **[概要]**  >  **[クライアント設定]** の順にクリックします。  

      2. クライアント エージェントを有効にする適切なデバイスの設定を開きます。 既定とカスタムのクライアント設定の詳細については、[クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)に関するページをご覧ください。  

      3. **[ソフトウェアの更新]** を選択し、 **[Office 365 クライアント エージェントの管理を有効にする]** の設定に **[はい]** を設定します。  

    **方法 2**:Office 展開ツールまたはグループ ポリシーを使用して、[Microsoft 365 Apps クライアントで Configuration Manager から更新プログラムを受信できるようにします](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient)。  

4. クライアントに [Microsoft 365 Apps 更新プログラムを展開します](deploy-software-updates.md)。

> [!NOTE]  
>
> Microsoft 365 Apps が最近インストールされた場合、そのインストール方法によっては、更新プログラム チャネルがまだ設定されていない可能性があります。 その場合、展開された更新プログラムは適用外として検出されます。 Microsoft 365 Apps をインストールするときに、[スケジュールされた自動更新タスク](/deployoffice/overview-of-the-update-process-for-office-365-proplus)が作成されます。 この状況では、更新チャネルを設定し、更新プログラムが適用可能として検出されるようにするために、このタスクを少なくとも 1 回実行する必要があります。
>
> Microsoft 365 Apps が最近インストールされ、展開された更新プログラムが検出されない場合は、クライアント上で、テストのために Office 自動更新タスクを手動で起動してから、[ソフトウェア更新プログラムの展開評価サイクル](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process)を開始できます。 タスク シーケンスでこれを実行する手順について詳しくは、「[タスク シーケンスでの Microsoft 365 Apps の更新](manage-office-365-proplus-updates.md#bkmk_ts)」を参照してください。

## <a name="restart-behavior-and-client-notifications-for-microsoft-365-apps-updates"></a>Microsoft 365 Apps 更新プログラムの動作とクライアント通知を再起動する
Microsoft 365 Apps クライアントに更新プログラムを展開する場合、再起動の動作とクライアント通知は、Configuration Manager のバージョンによって異なります。 次の表に、クライアントが Microsoft 365 Apps 更新プログラムを受け取るときのエンド ユーザー エクスペリエンスに関する情報を示します。

|Configuration Manager バージョン |エンド ユーザー エクスペリエンス|  
|----------------|---------------------|
|1706、1710|クライアントは、ポップアップとアプリ内通知、および更新プログラムをインストールする前にカウント ダウン ダイアログを受け取ります。|
|1802| クライアントは、ポップアップとアプリ内通知、および更新プログラムをインストールする前にカウント ダウン ダイアログを受け取ります。 </br>クライアントの更新プログラムの適用時に Microsoft 365 Apps が実行中の場合、Microsoft 365 Apps は強制的に閉じられません。 代わりに、更新プログラムのインストールでシステムの再起動が必要であることが示されます <!--510006-->|


> [!Important]
>
>Configuration Manager バージョン 1706 では、次の詳細に注意してください。
>
>- 今後 48 時間以内に期限に達し、コンテンツの更新がダウンロードされていることを通知するアイコンが、必要なアプリのタスク バーの通知領域に表示されます。 
>- 今後 7.5 時間以内に期限に達し、更新プログラムがダウンロードされている必要なアプリに対し、カウントダウン ダイアログが表示されます。 ユーザーは、期限に達する前に、カウントダウン ダイアログを 3 回まで延期することができます。 延期すると、2 時間後にもう一度カウントダウンが表示されます。 延期しない場合は、30 分のカウントダウンの終了後、更新プログラムがインストールされます。
>- ユーザーが通知領域内のアイコンをクリックするまで、ポップアップ通知が表示されない場合があります。 さらに、通知領域に最小限のスペースがある場合、ユーザーが通知領域を開くか展開しない限り、通知アイコンが表示されない場合があります。 
>- 通知とカウントダウン ダイアログは、ユーザーがデバイスでアクティブに作業していない間に開始する場合があります。 たとえば、デバイスが一晩中ロックされている場合、デバイス上で実行中の Microsoft 365 Apps を強制的に閉じて更新プログラムをインストールすることができます。 アプリを閉じる前に、Office はデータ損失を防ぐため、アプリ データを保存します。 
>- 期限が過去またはできるだけ早く開始するように設定されている場合は、実行中の Microsoft 365 Apps が通知なく強制的に閉じられる場合があります。 
>- ユーザーが期限前に Microsoft 365 Apps 更新プログラムをインストールすると、期限に達したときに、Configuration Manager によって、更新プログラムがインストールされていることが確認されます。 デバイスで更新プログラムが検出されない場合、更新プログラムがインストールされます。 
>- アプリ内通知バーは、更新プログラムがダウンロードされる前に実行されているアプリでは表示されません。 更新プログラムをダウンロードすると、アプリ内通知は新しく開いたアプリに対してのみ表示されます。
>- サービス ウィンドウによってトリガーされるか、営業時間外にスケジュールされている Microsoft 365 Apps 更新プログラムの場合、実行中の Office アプリを強制的に閉じて、通知せずに更新プログラムをインストールすることが可能です。 
>- 詳細については、「[Microsoft 365 アプリのエンドユーザーによる更新の通知](/deployoffice/end-user-update-notifications-microsoft-365-apps)」を参照してください。


## <a name="add-languages-for-microsoft-365-apps-update-downloads"></a><a name="bkmk_o365_lang"></a>Microsoft 365 Apps 更新プログラムのダウンロード対象言語を追加する
Microsoft 365 Apps でサポートされている任意の言語を、Configuration Manager で更新プログラムをダウンロードする際の対象言語として追加できます。

### <a name="download-updates-for-additional-languages-in-version-1902"></a>バージョン 1902 で追加言語の更新プログラムをダウンロードする
<!--3555955-->

Configuration Manager 1902 以降、更新のワークフローは、**Windows Update** では 38 の言語に分割される一方、**Office 365 クライアント更新**では多数の言語が追加されます。

必要な言語を選択するには、次の場所にある **[言語の選択]** ページを使用します。
- 自動展開規則の作成ウィザード
- ソフトウェアの更新の展開ウィザード
- ソフトウェア更新プログラムのダウンロード ウィザード
- 自動展開規則のプロパティ

**[言語の選択]** ページで、 **[Office 365 Client Update]\(Office 365 クライアント更新プログラム\)** を選択してから、 **[編集]** をクリックします。 Microsoft 365 Apps に必要な言語を追加し、 **[OK]** をクリックします。

![Microsoft 365 Apps の言語追加のスクリーンショット](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>バージョン 1810 およびそれ以前で追加言語の更新プログラムをダウンロードするためのサポートを追加するには

以下の手順は、中央管理サイトまたはスタンドアロンのプライマリ サイトにあるソフトウェアの更新ポイントで実行してください。

> [!IMPORTANT]  
> Microsoft 365 Apps 更新プログラムの言語追加の構成は、サイト全体に適用される設定です。 次の手順に従って言語を追加すると、すべての Microsoft 365 Apps 更新プログラムが、ソフトウェア更新プログラムのダウンロード ウィザードまたはソフトウェア更新プログラムの展開ウィザードの **[言語の選択]** ページで選択した言語に加えて、その言語でもダウンロードされます。

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
11. これで、Microsoft 365 Apps 更新プログラムをダウンロードすると、ウィザードで選択した言語とこの手順で構成した言語で更新プログラムがダウンロードされるようになります。 正しい言語の更新プログラムがダウンロードされたことを確認するには、その更新プログラムのパッケージ ソースにアクセスし、その言語コードを名前に含んだファイルを探します。  
    ![Filenames with additional languages](../media/5-verification.png)

## <a name="updating-microsoft-365-apps-in-a-task-sequence"></a><a name="bkmk_ts"></a>タスク シーケンスでの Microsoft 365 Apps の更新
タスク シーケンスの[ソフトウェア更新プログラムのインストール](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)手順を使用して Microsoft 365 Apps 更新プログラムをインストールすると、展開された更新プログラムが適用外として検出されることがあります。  これは、スケジュールされている Office 自動更新タスクが一度も実行されていない場合に発生する可能性があります (「[Deploy Microsoft 365 Apps 更新プログラムを展開する](manage-office-365-proplus-updates.md#bkmk_update)」の注を参照してください)。 たとえば、この手順を実行する直前に Microsoft 365 Apps をインストールした場合に、これが発生する可能性があります。

展開された更新プログラムが正しく検出されるように、更新チャネルを確実に設定するためには、次の方法のいずれかを使います。

**方法 1:**
1. 同じバージョンの Microsoft 365 Apps があるコンピューターで、タスク スケジューラ (taskschd.msc) を開き、Microsoft 365 Apps 自動更新タスクを見つけます。 通常は **[タスク スケジューラ ライブラリ]**  > **[Microsoft]** > **[Office]** にあります。
2. 自動更新タスクを右クリックして、 **[プロパティ]** を選択します。
3. **[アクション]** タブに移動して、 **[編集]** をクリックします。 コマンドとすべての引数をコピーします。 
4. Configuration Manager コンソールで、タスク シーケンスを編集します。
5. タスク シーケンスの**ソフトウェア更新プログラムのインストール**手順の前に、新しい**コマンド ラインの実行**手順を追加します。 同じタスク シーケンスの一部として Microsoft 365 Apps をインストールする場合は、Office のインストール後にこの手順が実行されるようにします。
6. Office 自動更新のスケジュールされたタスクから収集した引数とコマンドをコピーします。 
7. **[OK]** をクリックします。 

**方法 2:**
1. 同じバージョンの Microsoft 365 Apps があるコンピューターで、タスク スケジューラ (taskschd.msc) を開き、Microsoft 365 Apps 自動更新タスクを見つけます。 通常は **[タスク スケジューラ ライブラリ]**  > **[Microsoft]** > **[Office]** にあります。
2. Configuration Manager コンソールで、タスク シーケンスを編集します。
3. タスク シーケンスの**ソフトウェア更新プログラムのインストール**手順の前に、新しい**コマンド ラインの実行**手順を追加します。 同じタスク シーケンスの一部として Microsoft 365 Apps をインストールする場合は、Office のインストール後にこの手順が実行されるようにします。
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

ADR の変更方法の詳細については、「[ソフトウェア更新プログラムの自動展開](automatically-deploy-software-updates.md)」を参照してください。 名前の変更の詳細については、「[Office 365 ProPlus の名前の変更](/deployoffice/name-change)」を参照してください。


## <a name="change-the-update-channel-after-you-enable-microsoft-365-apps-clients-to-receive-updates-from-configuration-manager"></a>Configuration Manager から更新プログラムを受信できるように Microsoft 365 Apps クライアントを設定した後で更新プログラム チャネルを変更する

Microsoft 365 Apps を展開した後、グループ ポリシーまたは Office 展開ツール (ODT) を使用して更新プログラム チャネルを変更できます。 たとえば、半期チャネルから半期チャネル (対象指定) にデバイスを移行できます。 チャネルを変更すると、完全バージョンを再インストールまたはダウンロードしなくても Office は自動的に更新されます。 詳細については、「[組織のデバイスの Microsoft 365 Apps 更新プログラム チャネルを変更する](//deployoffice/change-update-channels)」を参照してください。


## <a name="next-steps"></a>次のステップ

Configuration Manager 内の Office 365 クライアント管理ダッシュボードを使用して Microsoft 365 Apps クライアントの情報を確認し、Microsoft 365 Apps を展開します。 詳細については、「[Office 365 クライアント管理ダッシュボード](office-365-dashboard.md)」をご覧ください。