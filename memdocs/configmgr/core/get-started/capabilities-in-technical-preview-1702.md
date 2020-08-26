---
title: Technical Preview 1702 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1702 で使用できる機能について説明します。
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 7a4c42891276b36fd888f0f70495bdcd504f23a1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693014"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Configuration Manager の Technical Preview 1702 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1702 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    


**このバージョンでお試しいただける新機能を次に示します。**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Configuration Manager コンソールからフィードバックを送信する

このプレビューでは、Configuration Manager コンソールの新しいフィードバック オプションを紹介します。 このフィードバック オプションを使用すると、Configuration Manager UserVoice フィードバック Web サイトから開発チームにフィードバックを直接送信できます。  

> **[フィードバック]** オプションは、次の場所に表示されます。
> -  各ノードのリボンの [ホーム] タブの左端。  
>    ![リボン](./media/feedback-home.png)

-  コンソールのオブジェクトを右クリックしたとき。   
    ![右クリック オプション](./media/feedback-option.png)   

**[フィードバック]** を選択すると、ブラウザーが開いて https://configurationmanager.uservoice.com/forums/300492-ideas の Configuration Manager UserVoice フィードバック Web サイトが表示されます。
##  <a name="changes-for-updates-and-servicing"></a>更新プログラムとサービスの変更
このプレビューで導入された更新内容は次のとおりです。

**簡単になった更新プログラムの選択**  
次の更新時に、お使いのインフラストラクチャで複数の更新プログラムが適用対象になった場合、最新の更新プログラムのみがダウンロードされます。 たとえば、現在のサイト バージョンが、リリースされている最新バージョンよりも 2 つ以上古い場合、その最新の更新プログラム バージョンのみが自動的にダウンロードされます。  

リリース済みのその他の更新プログラムが最新バージョンではない場合でも、ダウンロードしてインストールすることができます。 ただし、その更新プログラムは新しい更新プログラムで置き換えられたという警告が表示されます。 *[ダウンロード可能]* と表示される更新プログラムをダウンロードするには、コンソールで更新プログラムを選択し、 **[ダウンロード]** をクリックします。

**古い更新プログラムのクリーンアップの改善**   
サイト サーバー上の 'EasySetupPayload' フォルダーから不要なダウンロードを削除する自動クリーンアップ機能を追加しました。  


## <a name="peer-cache-improvements"></a>ピア キャッシュの改善
今回のリリース以降、ピア キャッシュ ソース コンピューターが次のいずれかの条件を満たす場合、ピア キャッシュ ソース コンピューターはコンテンツの要求を拒否するようになります。  
-  バッテリ低下モードの場合。
-  コンテンツの要求時に CPU 負荷が 80% を超えている場合。
-  ディスク I/O の *AvgDiskQueueLength* が 10 を超えている場合。
-  新たにコンピューターに接続できない場合。   

これらの設定を構成するには、Configuration Manager SDK を使用するときに、ピア ソース機能 (*SMS_WinPEPeerCacheConfig*) に対してクライアント エージェントの構成クラスを使用します。

コンピューターがコンテンツの要求を拒否すると、要求元のコンピューターは、使用できるコンテンツ ソース場所のプール内にある代替ソースのコンテンツを引き続きシークします。   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a> Azure Active Directory Domain Services を使用してデバイス、ユーザー、グループを管理する

この Technical Preview バージョンでは、Azure Active Directory (AD) Domain Services マネージド ドメインに参加しているデバイスを管理できます。 また、Configuration Manager のさまざまな探索方法を使用して、そのドメイン内のデバイス、ユーザー、およびグループを探索することもできます。

Technical Preview サイトのインフラストラクチャ、クライアント、および Azure AD Domain Services ドメインは、すべて Azure で実行される必要があります。


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Azure AD を使用するように Configuration Manager を設定する
Configuration Manager で Azure AD を使用するには、以下が必要です。
- Azure のサブスクリプション。
- Azure AD と Domain Services (DS)。
- Azure AD に参加している Azure VM 上で実行されている Configuration Manager サイト。
- 同じ Azure AD 環境で実行されている Configuration Manager クライアント。

Azure AD Domain Services を構成する方法については、「[Azure AD ドメイン サービスの使用開始](/azure/active-directory-domain-services/create-instance)」を参照してください。

### <a name="discover-resources"></a>リソースの探索
Azure AD 内で実行するように Configuration Manager を設定したら、次の Active Directory 探索方法を使用して Azure AD のリソースを検索できます。  
- Active Directory システムの探索
- Active Directory ユーザー検出
- Active Directory グループの探索  

使用する方法ごとに、オンプレミス Active Directory の場合に一般的なコンテナーではなく、Azure AD OU 構造を検索するように LDAP クエリを編集します。 そのためには、Azure サブスクリプションの Active Directory を検索するようにクエリを指定する必要があります。  

次の例では、*contoso.onmicrosoft.com* の Azure AD を使用しています。
- **システムの探索**   
  Azure AD は、**AADDC Computers** OU 以下にデバイスを格納します。  次を構成します。  
  - *LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **ユーザーの探索** AAD は **AADDC Users** OU 以下にユーザーを格納します。  次を構成します。
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **グループの探索**  
Azure AD にはグループを格納する OU がありません。 その代わり、システム クエリまたはユーザー クエリと同じ一般的な構造を使用し、探索するグループを含む OU を示すように LDAP クエリを構成します。

Azure AD の詳細については、以下を参照してください。  
- 「[Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds)」(azure.microsoft.com)。
- 「[Active Directory Domain Services のドキュメント](/azure/active-directory-domain-services)」(docs.microsoft.com)。

## <a name="conditional-access-device-compliance-policy-improvements"></a>条件付きアクセス デバイス コンプライアンス ポリシーの改善

ユーザーがアプリのコンプライアンス非対応リストに含まれているアプリを使用している場合、新しいデバイスのコンプライアンス ポリシー ルールを使用して、条件付きアクセスをサポートする会社のリソースへのアクセスをブロックできます。 アプリのコンプライアンス非対応リストは、管理者が新しい準拠ルール **[インストールできないアプリ]** の追加時に定義できます。 このルールを使用するには、管理者がコンプライアンス非対応リストにアプリを追加するときに、**アプリ名**、**アプリ ID**、**アプリの発行元** (省略可能) を入力する必要があります。 この設定は、iOS および Android デバイスにのみ適用されます。

また、組織はこの設定を使用して、セキュリティで保護されていないアプリを介したデータ漏えいを軽減し、特定のアプリ経由の過度なデータ使用を防ぐことができます。

### <a name="try-it-out"></a>試してみましょう

**シナリオ:** 社外に会社データを送信してデータ漏えいを引き起こしている可能性があるアプリ、または過度なデータ使用を引き起こしているアプリを特定します。次に、このようなアプリをアプリのコンプライアンス非準拠リストに追加する[条件付きアクセス デバイス コンプライアンス ポリシーを作成します](../../mdm/understand/what-happened-to-hybrid.md)。 これによって、ユーザーがブロックされたアプリを削除するまで、条件付きアクセスをサポートする会社のリソースに対するアクセスはブロックされます。

## <a name="antimalware-client-version-alert"></a>マルウェア対策クライアントのバージョンのアラート
このプレビュー バージョン以降、管理対象のクライアントの 20% 超 (既定) が期限切れバージョンのマルウェア対策クライアント (つまり Windows Defender または Endpoint Protection クライアント) を使用している場合、Configuration Manager Endpoint Protection でアラートが発生します。

### <a name="try-it-out"></a>試してみましょう
クライアント設定ポリシーを使用して、すべてのデスクトップとサーバー クライアントで Endpoint Protection を有効にします。 **[資産とコンプライアンス]**  >  **[概要]**  >  **[デバイス]**  >  **[All Desktops and Serve Clients (すべてのデスクトップとサービス クライアント)]** の順に選択して、 **[マルウェア対策クライアント バージョン]** と **[Endpoint Protection Deployment Status (Endpoint Protection の展開ステータス)]** を確認できます。 アラートを確認するには、 **[監視]** ワークスペースの **[アラート]** を表示します。 20% を超える管理対象クライアントが期限切れバージョンのマルウェア対策ソフトウェアを実行している場合、"マルウェア対策クライアント バージョンが期限切れです" のアラートが表示されます。 このアラートは、 **[監視]**  >  **[概要]** タブには表示されません。期限切れのマルウェア対策クライアントを更新するには、マルウェア対策クライアントのソフトウェア更新プログラムを有効にします。

アラートを生成するパーセント値を構成するには、 **[監視]**  >  **[アラート]**  >  **[すべてのアラート]** を展開し、 **[期限切れのマルウェア対策クライアント]** をダブルクリックし、 **[管理されたクライアントのうち、期限切れのバージョンのマルウェア対策クライアントを使用しているものが次の割合を超えたら、アラートを生成する]** オプションを変更します。

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Windows Update for Business 更新プログラムのコンプライアンス評価
コンプライアンス ポリシーの更新ルールを構成して、条件付きアクセス評価の一部として Windows Update for Business の評価結果を含めることができるようになりました。
> [!IMPORTANT]
> Windows Update for Business 更新プログラムのコンプライアンス評価を使用するには、Windows 10 Insider Preview Build 15019 以降を使用している必要があります。

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Windows 10 の更新プログラム管理を Windows Update for Business に許可する
Windows Update for Business 更新プログラムのコンプライアンス評価情報を収集するには、次の手順で、Windows 10 の更新プログラム管理を Windows Update for Business に明示的に許可するクライアント エージェント設定を構成します。
1. Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]** に移動します。
2. クライアント設定のプロパティで、 **[ソフトウェア更新プログラム]** を開き、 **[Windows Update for Business で Windows 10 の更新プログラムを管理する]** 設定で **[はい]** を選択します。

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Windows Update for Business 評価のコンプライアンス ポリシーを作成する
1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[コンプライアンス設定]**  >  **[コンプライアンス ポリシー]** の順にクリックします。
2. **[コンプライアンス ポリシーの作成]** をクリックするか、既存のコンプライアンス ポリシーを選択して変更します。
3. [全般] ページで、名前と説明を入力し、 **[Configuration Manager クライアントで管理されるデバイスのコンプライアンス規則]** を選択し、レポートのコンプライアンスコンプライアンス非対応の重要度を設定し、 **[次へ]** をクリックします。
4. [サポートされているプラットフォーム] ページの **[Windows 10]** を選択し、 **[次へ]** をクリックします。
5. [ルール] ページの **[新規]** をクリックし、 **[条件]** の **[Require Windows Update for Business compliance (Windows Update for Business コンプライアンスが必要)]** をオンにします。 **[値]** 設定は **[真]** に自動的に設定されます。

**[資産とコンプライアンス]** ワークスペースの **[コンプライアンス ポリシー]** ノードに新しいポリシーが表示されます。

### <a name="deploy-a-compliance-policy"></a>コンプライアンス ポリシーの展開
1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[コンプライアンス設定]** の順にクリックし、 **[コンプライアンス ポリシー]** をクリックします。
2. **[ホーム]** タブの **[展開]** グループで、 **[展開]** をクリックします。
3. **[コンプライアンス ポリシーの展開]** ダイアログ ボックスで、 **[参照]** をクリックして、ポリシーを展開するユーザー コレクションを選択します。
   さらに、ポリシーが準拠していない場合にアラートを生成するオプションや、ポリシーのコンプライアンスを評価するスケジュールを構成するオプションを選択できます。
4. 終了したら、 **[OK]** をクリックします。

### <a name="monitor-the-compliance-policy"></a>コンプライアンス ポリシーの監視
コンプライアンス ポリシーを作成すると、Configuration Manager コンソールでコンプライアンス結果を監視できます。 詳細については、「[Monitor the compliance policy](../../mdm/understand/what-happened-to-hybrid.md)」(コンプライアンス ポリシーの監視) を参照してください。


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>ソフトウェア センターの設定と影響の大きいタスク シーケンスの通知メッセージの改善
このリリースでは、影響の大きい展開タスク シーケンスのソフトウェア センター設定と通知メッセージについて、次の点などが改善されています。

- タスク シーケンスのプロパティで、危険性が高い展開として、オペレーティング システム以外のタスク シーケンスを含め、任意のタスク シーケンスを構成できます。 特定の条件を満たす任意のタスク シーケンスは、影響度大として自動的に定義されます。 詳細については、「[System Center Configuration Manager の危険度の高い展開を管理するための設定](../servers/manage/settings-to-manage-high-risk-deployments.md)」を参照してください。
- タスク シーケンスのプロパティでは、影響の大きい展開について既定の通知メッセージを使用するか、独自のカスタム通知メッセージを作成することができます。
- タスク シーケンスのプロパティでは、ソフトウェア センターのプロパティ (再起動を必須にする、タスク シーケンスのダウンロード サイズ、推定実行時間など) を構成できます。
- インプレース アップグレードの既定の影響の大きい展開のメッセージには、アプリ、データ、および設定が自動的に移行されると表示されるようになりました。 以前のバージョンでは、オペレーティング システムのインストールに関する既定のメッセージには、すべてのアプリ、データ、および設定が失われると表示されていましたが、これはインプレース アップグレードの場合は該当しない内容でした。

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>タスク シーケンスを影響の大きいタスク シーケンスとして設定する
次の手順を使用して、影響の大きいタスク シーケンスとして設定します。
> [!NOTE]
> 特定の条件を満たす任意のタスク シーケンスは、影響度大として自動的に定義されます。 詳細については、「[System Center Configuration Manager の危険度の高い展開を管理するための設定](../servers/manage/settings-to-manage-high-risk-deployments.md)」を参照してください。

1. Configuration Manager コンソールの **[ソフトウェア ライブラリ]**  >  **[オペレーティング システム]**  >  **[タスク シーケンス]** の順に選択します。
2. 編集するタスク シーケンスを選択し、 **[プロパティ]** をクリックします。
3. **[ユーザー通知]** タブの **[これは、インパクトのあるタスク シーケンスです]** をオンにします。

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>危険度の高い展開のカスタム通知を作成する
1. Configuration Manager コンソールの **[ソフトウェア ライブラリ]**  >  **[オペレーティング システム]**  >  **[タスク シーケンス]** の順に選択します。
2. 編集するタスク シーケンスを選択し、 **[プロパティ]** をクリックします。
3. **[ユーザー通知]** タブの **[カスタム テキストを使用する]** をオンにします。
   > [!NOTE]
   >  **[これは、インパクトのあるタスク シーケンスです]** がオンの場合にのみ、ユーザー通知テキストを設定できます。

4. 次の設定を構成します (各テキスト ボックスは最大 255 文字です)。

   **ユーザー通知の見出しテキスト**:ソフトウェア センターのユーザー通知に表示する青色のテキストを指定します。 たとえば、既定のユーザー通知では、このセクションに "このコンピューターのオペレーティング システムをアップグレードすることを確認します" のようなテキストが表示されます。

   **ユーザー通知のメッセージ テキスト**:カスタム通知の本文を入力する 3 つのテキスト ボックスがあります。
   - 1 つ目のテキスト ボックス:ユーザーの手順など、テキストのメインの本文を指定します。 たとえば、既定のユーザー通知では、このセクションには "オペレーティング システムのアップグレードには時間がかかります。また、コンピューターが数回再起動される場合があります" のようなテキストが表示されます。
   - 2 つ目のテキスト ボックス:メインの本文の下に表示される太字のテキストを指定します。 たとえば、既定のユーザー通知では、このセクションに "このインプレース アップグレードでは、新しいオペレーティング システムがインストールされ、アプリ、データ、設定が自動的に移行されます" のようなテキストが表示されます。
   - 3 つ目のテキスト ボックス:太字のテキストの下の最終行を指定します。 たとえば、既定のユーザー通知では、このセクションに "インストールを開始するには、開始するには [インストール]、 それ以外の場合は [キャンセル] をクリックしてください" のようなテキストが表示されます。   

   たとえば、プロパティでは次のようなカスタム通知を構成できます。

   ![タスク シーケンスのカスタム通知](./media/user-notification.png)

   エンドユーザーがソフトウェア センターからインストールを開くときに、次の通知メッセージが表示されます。

   ![タスク シーケンスのカスタム通知](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>ソフトウェア センターのプロパティを構成する
ソフトウェア センターに表示されるタスク シーケンスの詳細を構成するには、次の手順を実行します。 これは参考目的のみの情報です。  
1. Configuration Manager コンソールの **[ソフトウェア ライブラリ]**  >  **[オペレーティング システム]**  >  **[タスク シーケンス]** の順に選択します。
2. 編集するタスク シーケンスを選択し、 **[プロパティ]** をクリックします。
3. **[全般]** タブでは、ソフトウェア センターの次の設定を使用できます。
   - **再起動が必要**:インストール時に再起動が必要かどうかをユーザーに通知します。
   - **ダウンロード サイズ (MB)** :タスク シーケンスについてソフトウェア センターに表示するサイズ (MB) を指定します。  
   - **推定実行時間 (分)** : タスク シーケンスについてソフトウェア センターに表示する推定実行時間を分単位で指定します。


## <a name="check-for-running-executable-files-before-installing-an-application"></a>アプリケーションをインストールする前に実行中の実行可能ファイルを確認する

展開の種類の **[ *\<deployment type name>* のプロパティ]** ダイアログ ボックスの [インストールの処理] タブで、実行可能ファイルが実行中の場合、その展開の種類のインストールをブロックする実行可能ファイルの 1 つを指定できるようになりました。 ユーザーは、その展開の種類をインストールするには、実行中の実行可能ファイルを終了する必要があります (または、展開の目的が必須の場合は自動的に終了することができます)。

### <a name="try-it-out"></a>試してみましょう

1. Configuration Manager の展開の種類のプロパティで、 **[インストールの処理]** タブを選択します。
2. **[追加]** を選択して、確認する 1 つまたは複数の実行可能ファイル名を追加します。 ユーザーがリストのアプリケーションを特定しやすくなるように、表示名を追加することもできます。
3. 展開の目的を必須にする場合、必要に応じて、ソフトウェアの展開ウィザードで **[[展開の種類プロパティ] ダイアログ ボックスの [インストールの処理] タブで指定した実行中の実行可能ファイルをすべて自動的に閉じる]** をオンにすることもできます。

アプリケーションの展開が **[使用可能]** で、エンド ユーザーがアプリケーションをインストールしようとすると、インストールを続行する前に、指定した実行中の実行可能ファイルを終了するようにユーザーに求めます。

アプリケーションの展開が **[必須]** で、オプション **[[展開の種類プロパティ] ダイアログ ボックスの [インストールの処理] タブで指定した実行中の実行可能ファイルをすべて自動的に閉じる]** がオンの場合、アプリケーションのインストール期限に達したときに、指定した実行可能ファイルが自動的に閉じられることを通知するダイアログ ボックスが表示されます。 これらのダイアログは **[クライアント設定]**  >  **[コンピューター エージェント]** でスケジュールできます。 これらのメッセージをエンド ユーザーに表示しない場合は、展開のプロパティの **[ユーザー エクスペリエンス]** タブで **[すべての通知をソフトウェア センターで非表示にし、ユーザーにも通知しない]** をオンにします。

アプリケーションの展開が **[必須]** で、オプション **[[展開の種類プロパティ] ダイアログ ボックスの [インストールの処理] タブで指定した実行中の実行可能ファイルをすべて自動的に閉じる]** がオフの場合、指定したアプリケーションの 1 つまたは複数が実行中の場合、アプリのインストールは失敗します。

## <a name="create-pfx-certificates-with-s-mime-support"></a>S/MIME サポートを含む PFX 証明書を作成する

S/MIME をサポートする PFX 証明書プロファイルを作成できるようになりました。  この証明書は、ユーザーが登録したデバイス全体で S/MIME の暗号化と復号化に使用できます。

また、複数の証明書登録ポイントのサイト システムの役割に対して複数の証明機関 (CA) を指定し、証明書プロファイルの一部として要求を処理する CA を割り当てることできるようになりました。

iOS デバイスでは、PFX 証明書プロファイルを電子メール プロファイルに割り当てて、S/MIME 暗号化を有効にすることができます。  これで、iOS のネイティブ電子メール クライアントで S/MIME を有効にして、正しい S/MIME 暗号化証明書を関連付けることができます。

Configuration Manager の証明書の詳細については、「[証明書プロファイルの概要]( /sccm/protect/deploy-use/introduction-to-certificate-profiles)」を参照してください。


## <a name="new-compliance-settings-for-ios-devices"></a>iOS デバイスの新しいコンプライアンス設定

iOS デバイスの構成アイテムで使用できる新しい設定が追加されました。 これらの設定は、以前はスタンドアロン構成での Microsoft Intune にありましたが、Intune を Configuration Manager で使用する際にも使用できるようになりました。 これらの設定の詳細については、「[Microsoft Intune の iOS ポリシー設定](../../../intune/configuration/device-restrictions-ios.md)」を参照してください。

- **管理対象アプリから iCloud にデータを同期**
- **ハンドオフして別のデバイスで作業を継続**
- **iCloud の写真共有**
- **iCloud フォトライブラリ**
- **新しいエンタープライズ アプリ作成者を信頼**
- **'アダルト' のフラグが付いているコンテンツをユーザーが iBook ストアからダウンロードすることを許可する** (監視モードのみ)
- **ペアリングされている Apple Watch で手首検出の使用を強制する**
- **AirPlay 送信要求のパスワード**
- **アカウント設定の変更** (監視モードのみ)
- **アプリの携帯データ ネットワークの使用設定に対する変更** (監視モードのみ)
- **すべてのコンテンツと設定を消去** (監視モードのみ)
- **デバイスに対する制限の構成** (監視モードのみ)
- **iOS デバイスとペアリングできるデバイスをホスト ペアリングで制御** (監視モードのみ)
- **構成プロファイルと証明書のインストール** (監視モードのみ)
- **デバイス名の変更** (監視モードのみ)
- **パスコードの変更** (監視モードのみ)
- **Apple Watch のペアリング** (監視モードのみ)
- **通知設定の変更** (監視モードのみ)
- **壁紙の変更** (監視モードのみ)
- **診断の送信の設定変更** (監視モードのみ)
- **Bluetooth の変更** (監視モードのみ)
- **AirDrop** (監視モードのみ)
- **Siri を使用して、ユーザーが生成したインターネットのコンテンツに対してクエリを実行** (監視モードのみ)
- **Siri の不適切な単語フィルター** (監視モードのみ)
- **Spotlight 検索でインターネットから結果を返す** (監視モードのみ)
- **単語の定義の検索** (監視モードのみ)
- **予測表示キーボード** (監視モードのみ)
- **自動修正** (監視モードのみ)
- **キーボード スペル チェック** (監視モードのみ)
- **キーボード ショートカット** (監視モードのみ)
  <!--- - **Enterprise app trust settings modification** --->
- **Apple Configurator と iTunes を使ったアプリのインストールのみ** (監視モードのみ)
- **アプリの自動ダウンロード** (監視モードのみ)
- **"友達を探す" アプリの設定の変更** (監視モードのみ)
- **iBooks ストアへのアクセス** (監視モードのみ)
- **メッセージ アプリ** (監視モードのみ)
- **ポッドキャスト** (監視モードのみ)
- **Apple Music** (監視モードのみ)
- **iTunes Radio** (監視モードのみ)
- **Apple News** (監視モードのみ)
- **Game Center** (監視モードのみ)
- **Airdrop を管理対象外として扱う**

## <a name="android-for-work-support"></a>Android for Work のサポート

Technical Preview バージョン 1702 以降、Google アカウントをハイブリッド MDM テナントにバインドできます。 バインドすると、以下を実行できるようになります。

- [サポートされる Android デバイス](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)を Android for Work として登録し、その登録したデバイスに仕事用プロファイルを作成する
- Play for Work ストアでアプリを承認し、Configuration Manager コンソールと同期して、デバイスの仕事用プロファイルに展開する
- 構成アイテムを作成して展開し、そのデバイスの仕事用プロファイルとパスワード設定を構成する
- Android デバイスと同様の手順で Android for Work デバイスのコンプライアンス ポリシー アイテムとリソース アクセス プロファイルを作成して展開する
- Android for Work デバイスの選択的ワイプを実行する

デバイスを登録すると、Android for Work は Intune が管理できるデバイスに仕事用プロファイルを作成します。 この仕事用プロファイルは、Android デバイス上の個人用プロファイルと同時に存在します。 ユーザーは仕事用プロファイル アプリと個人用プロファイル アプリを簡単に切り替えることができます。 管理者は、個人用プロファイルのアイテムを管理できません。 個人のアプリとデータは管理対象外のままです。 Configuration Manager では仕事用プロファイルとそのコンテンツを完全に制御し、デバイスから削除することができます。

Android for Work は Android とは別のプラットフォームです。仕事用プロファイルをサポートする Android デバイスに使用する管理の形式を決定する必要があります。

### <a name="try-it-out"></a>試してみましょう。
以下のセクションでは、Android for Work の管理について説明します。

#### <a name="enable-android-for-work-management"></a>Android for Work の管理を有効にする
1. [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp ) で、Android for Work 管理者アカウントとして使用する Google アカウントを作成します。このアカウントは、この Intune テナントのすべての Android for Work 管理タスクに関連付けられます。 これは、Android デバイスを管理する管理者間で共有する Google アカウントにすることができます。 これは、組織が Play for Work コンソールでアプリを管理および発行するときに使用する Google アカウントです。 このアカウントを使用して、Play for Work ストアのアプリを承認し、アカウント名とパスワードを追跡します。
2. Android の登録を有効にするには、Google アカウントを Configuration Manager で管理される Intune テナントにバインドします。
   1. **[管理]**  >  **[概要]**  >  **[Cloud Services]**  >  **[Microsoft Intune サブスクリプション]** の順に選択し、Intune サブスクリプションを選択します。
   2. リボンの **[プラットフォームの構成]**  >  **[Android]** をクリックし、 **[Android の登録を有効にする]** をオンにします。
   3. リボンの **[プラットフォームの構成]**  >  **[Android for Work]** をクリックします。
   4. ダイアログ ボックスの **[Intune コンソールで Android for Work を構成する]** をクリックします。 Web ブラウザーで Intune コンソールが開きます。
   5. Intune 管理者の資格情報を使用して Intune ポータルにログインします。
   6. **[構成]** をクリックして Google Play の Android for Work Web サイトを開きます。
   7. Google のサインイン コンポーネントで、手順 1 の Google アカウントの資格情報を入力し、会社情報を入力します。
3. Intune ポータルに戻ると、Android for Work が有効になり、Android for Work デバイスの 3 つの登録オプションが表示されます。
   - **すべてのデバイスを Android として管理する** - (無効) Android for Work をサポートするデバイスを含め、すべての Android デバイスが従来の Android デバイスとして登録されます。
   - **サポートされているデバイスを Android for Work として管理する** - (有効) Android for Work をサポートするすべてのデバイスが Android for Work デバイスとして登録されます。 Android for Work をサポートしない Android デバイスは、従来の Android デバイスとして登録されます。
   - **これらのグループに所属するユーザーのサポートされているデバイスのみを Android for Work として管理する** - (テスト) Android for Work の管理を特定のユーザー グループを対象にしてみましょう。 Android for Work をサポートするデバイスを登録した、選択したグループのメンバーのみが、Android for Work デバイスとして登録されます。 それ以外は Android デバイスとして登録されます。
  
> [!NOTE]
> ある既知の問題では、 **[これらのグループに所属するユーザーのサポートされているデバイスのみを Android for Work として管理する]** オプションが期待どおり動作しません。 指定の Azure AD グループにあるユーザーのデバイスが Android for Work ではなく Android として登録されます。 Android for Work をテストするには、 **[Manage all supported devices as Android for Work (サポートされているすべてのデバイスを Android for Work として管理する)]** を利用する必要があります。


  Android for Work の登録を有効にするには、下の 2 つのオプションのいずれかを選択する必要があります。 **[これらのグループに所属するユーザーのサポートされているデバイスのみを Android for Work として管理する]** オプションの場合、まず Azure Active Directory セキュリティ グループを設定する必要があります。

バインドが完了すると、アカウント名と組織名が Intune ポータルに表示されます。完了すると、両方のブラウザーを閉じることができます。

#### <a name="approve-and-deploy-android-for-work-apps"></a>Android for Work アプリの承認と展開
Play for Work ストアのアプリを承認し、Configuration Manager コンソールと同期し、管理対象の Android for Work デバイスに展開するには、次の手順を実行します。 アプリをユーザーの仕事用プロファイルに展開するには、Play for Work でアプリを承認し、アプリを Configuration Manager コンソールと同期する必要があります。

1. ブラウザーを開き、 https://play.google.com/work に移動します。
2. Intune テナントにバインドした Google 管理者アカウントを使用してサインインします。
3. 環境に展開するアプリを参照し、各アプリについて **[承認]** をクリックします。
4. Configuration Manager コンソールで **[管理者]**  >  **[概要]**  >  **[クラウド サービス]**  >  **[Android for Work]** の順にクリックし、 **[同期]** をクリックします。
5. アプリが同期されるまで 10 分間待ってから **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[アプリケーション管理]**  >  **[ストア アプリのライセンス情報]** の順に選択します。
6. Play for Work から同期したアプリをクリックしてから **[アプリケーションの作成]** をクリックします。
7. ウィザードを完了し、 **[閉じる]** をクリックします。
8. **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[アプリケーション管理]**  >  **[アプリケーション]** の順に選択し、Android for Work アプリを選択して、通常どおりに展開します。

Play for Work アプリを Configuration Manager と同期するには、少なくとも 1 つのアプリを Play for Work Web サイトで承認する必要があります。

#### <a name="enroll-an-android-for-work-device"></a>Android for Work デバイスを登録する
Android for Work デバイスの登録方法は、Android の登録方法と似ています。 モバイル デバイスで Android 用のポータル サイト アプリをダウンロードして実行します。 登録プロセスの一環で仕事用プロファイルを作成するように求められます。  仕事用プロファイルを完了したら、管理対象バージョンのポータル サイトに切り替える必要があります。 管理対象のポータル サイトには、右下に小さなオレンジ色のブリーフケースのタグが付いています。

#### <a name="create-and-deploy-a-configuration-item"></a>構成アイテムの作成と展開
Android for Work には、構成アイテムに 2 つの設定グループがあります。
- パスワード
- 仕事用プロファイル

Android 6 以降を実行するデバイスでは、仕事用プロファイル間で共有するコンテンツだけでなく、次の構成アイテムも構成できます。
- 特定のアクセス許可を求めるアプリの動作
- 仕事用プロファイル内のアプリの通知をロック画面に表示するかどうか

この機能を試すには、標準のワークフローで構成アイテムを作成し、 **[全般]** ページで **[Android for Work]** を選択し、各設定グループの設定を構成し、構成アイテムを基準に追加して、通常どおりに展開します。 これらの設定は、Android for Work として登録されたデバイスにのみ適用され、Android として登録されたデバイスには適用されません。

#### <a name="perform-selective-wipe"></a>選択的なワイプを実行する
管理者は仕事用プロファイルのみを管理するので、Android for Work として登録されたデバイスに対してのみ、選択的なワイプを実行できます。 そのため、個人用プロファイルはワイプから保護されます。 Android for Work デバイスで選択的なワイプを実行すると、すべてのアプリとデータを含む仕事用プロファイルが削除され、デバイスの登録が削除されます。

Android for Work デバイスで選択的なワイプを実行するには、Configuration Manager コンソールで通常の[選択的なワイプ プロセス](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)を使用します。

#### <a name="known-issues-for-android-for-work"></a>Android for Work の既知の問題
**Android for Work 電子メール プロファイルで同期スケジュールを設定すると、展開に失敗する** Android for Work 電子メール プロファイルの ConfigMgr UI のオプションの 1 つが "スケジュール" です。 他のプラットフォームでは、管理者はスケジュールを設定し、展開先のモバイル デバイスに電子メールやその他の電子メール アカウント データを同期できます。 ただし、Android for Work 電子メール プロファイルの場合は動作しません。"未構成" 以外のオプションを選択すると、プロファイルはいかなるデバイスにも展開されません。