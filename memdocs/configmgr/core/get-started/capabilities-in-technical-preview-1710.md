---
title: Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1710 で使用できる機能について説明します。
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e408bbe7ea88d70c5a9d02368c2d820584cae2b8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694442"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Configuration Manager の Technical Preview 1710 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1710 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**この Technical Preview の既知の問題:**
- **Windows 10、バージョン 1709 (Fall Creators Update とも呼ばれます) のサポート**。  この Windows リリース以降、Windows メディアには複数のエディションが含まれます。 オペレーティング システム アップグレード パッケージまたはオペレーティング システム イメージを使用するようにタスク シーケンスを構成する場合は、必ず [Configuration Manager による使用をサポートしているエディション](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)を選択してください。
- **サイト サーバーがパッシブ モードの場合、新しいプレビュー バージョンへの更新に失敗します**。 [プライマリ サイト サーバーがパッシブ モード](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)であるプレビュー バージョンを実行する場合は、プレビュー サイトをこの新しいプレビュー バージョンに正常に更新するため、あらかじめパッシブ モードのサイト サーバーをアンインストールしておく必要があります。 パッシブ モードのサイト サーバーは、サイトの更新を完了したあとに再インストールできます。

  パッシブ モードのサイト サーバーをアンインストールするには、次の手順を実行します。
  1. コンソールで **[管理]**  >  **[概要]**  >  **[サイトの構成]**  >  **[サーバーとサイト システムの役割]** の順に移動し、パッシブ モードのサイト サーバーを選択します。
  2. **[サイト システムの役割]** ウィンドウで、 **[サイト サーバー]** の役割を右クリックし、 **[役割の削除]** を選択します。
  3. パッシブ モードのサイト サーバーを右クリックし、 **[削除]** を選択します。
  4. サイト サーバーのアンインストール後に、アクティブなプライマリ サイト サーバーで **CONFIGURATION_MANAGER_UPDATE** のサービスを再起動します。

**このバージョンでお試しいただける新機能を次に示します。**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Configuration Manager から PowerShell スクリプトを展開するための機能強化
このリリースでは、展開する PowerShell スクリプトで次の機能強化の使用がサポートされるようになりました。 
- **セキュリティ スコープ**。  スクリプトのオーサリングと実行を制御するため、スクリプトでセキュリティ スコープを使用するようになりました。 これは、ユーザー グループを表すタグを割り当てることで行います。 セキュリティ スコープの使用の詳細については、「[Configuration Manager のロール ベース管理の構成](../../core/servers/deploy/configure/configure-role-based-administration.md)」を参照してください。
- **リアルタイム監視**。 スクリプトの実行を監視するときに、スクリプトの実行時にリアルタイムで行われるようになりました。
- **パラメーターの検証**。 スクリプト内の各パラメーターには、そのパラメーターに検証を追加するための **[Script Parameter Properties]\(スクリプト パラメーター プロパティ\)** ダイアログがあります。 検証を追加した後に、その検証を満たしていないパラメーターの値を入力すると、エラーが発生します。

PowerShell スクリプトの展開は、Technical Preview [Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console) で初めて導入されました。 [Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) および [Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) で機能強化がさらに追加されました。


### <a name="try-it-out"></a>試してみましょう。

スクリプトの実行機能を使用して試すには、[スクリプトの作成と実行](../../apps/deploy-use/create-deploy-scripts.md)に関するページを参照してください。



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Windows 10 拡張データを制限し、Windows Analytics デバイスの正常性に関連したデータのみを送信するようにする
<!-- 1356148 -->

今回のリリースでは、Windows 10 診断データ コレクション レベルを **[拡張 (制限付き)]** に設定できるようになりました。 この設定を行うと、デバイスから **[拡張]** レベルのデータのすべてを報告されなくても、Windows 10 バージョン 1709 以降で、ご利用の環境のデバイスに関する、アクションにつながる有用な情報を得ることができます。

[拡張 (制限付き)] レベルには、基本レベルから収集されたメトリックと共に、Windows Analytics に関連する **[拡張]** レベルから収集されたデータのサブセットも含まれます。


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>ソフトウェア センターで 250x250 を超えるアイコンが変形しなくなります  
<!-- 1356194 -->

今回のリリース以降、ソフトウェア センターではアイコンのサイズが 250 x 250 を超えてもアイコンが変形しなくなります。 そのようなアイコンはソフトウェア センターではぼやけて表示されます。 最大 512x512 のピクセル寸法でアイコンを設定でき、変形することなく表示されます。

### <a name="try-it-out"></a>試してみましょう。
ソフトウェア センターで、アプリのアイコンを追加してみましょう。 追加方法については、[アプリケーションの作成](../../apps/deploy-use/create-applications.md)に関する記事をご覧ください。


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>ソフトウェア センターから共同管理対象デバイスのコンプライアンスを確認する
<!-- 1356374 -->
今回のリリースでは、条件付きアクセスが Intune によって管理されている場合でも、ユーザーはソフトウェア センターを使用して共同管理対象 Windows 10 デバイスのコンプライアンスを確認できます。 詳細については、「[Windows 10 デバイスの共同管理](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)」をご覧ください。


## <a name="support-for-exploit-guard"></a>Exploit Guard のサポート
今回のリリースでは、Windows Defender Exploit Guard のサポートが追加されます。 Exploit Guard の 4 つすべてのコンポーネントを管理するポリシーを構成し、展開できます。 これらのコンポーネントには次のものが含まれます。
-   攻撃の回避
-   フォルダー アクセスの制御
-   悪用に対する保護
-   ネットワーク保護

Exploit Guard ポリシーのコンプライアンス データは、Configuration Manager コンソールを使用して展開できます。

Exploit Guard と特定のコンポーネントおよび規則の詳細については、Windows ドキュメント ライブラリの「[Windows Defender Exploit Guard](/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard)」をご覧ください。

### <a name="prerequisites"></a>[前提条件]
マネージド デバイスでは、Windows 10 1709 Fall Creators Update 以降を実行し、構成するコンポーネントと規則に応じて次の要件を満たす必要があります。

|Exploit Guard コンポーネント |追加の前提条件|
|------------------------|------------------------|
| 攻撃の回避  | デバイスで [Windows Defender AV のリアルタイム保護]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)を有効にする必要があります。  |
| フォルダー アクセスの制御  | デバイスで [Windows Defender AV のリアルタイム保護]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)を有効にする必要があります。   |
| 悪用に対する保護  | なし  |
| ネットワーク保護  |  デバイスで [Windows Defender AV のリアルタイム保護]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)を有効にする必要があります。  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Exploit Guard ポリシーを作成する  <!--1355468 -->
1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[Endpoint Protection]** の順に移動し、 **[Windows Defender Exploit Guard]** をクリックします。
2. **[ホーム]** タブの **[作成]** グループで、 **[Create Exploit Policy]\(Exploit Policy の作成\)** をクリックします。
3. **構成項目の作成ウィザード** の **[全般]** ページで、構成項目の名前と、必要に応じて説明を入力します。
4. 次に、このポリシーで管理する Exploit Guard コンポーネントを選択します。 選択したコンポーネントごとに、追加の詳細を構成できます。
   - **攻撃の回避:** ブロックまたは監査する Office に関連する脅威、スクリプトに関連する脅威、メールに関連する脅威について構成します。 この規則から特定のファイルまたはフォルダーを除外することもできます。
   - **フォルダー アクセスの制御:** ブロックまたは監査を構成してから、このポリシーをバイパスできるアプリを追加します。  既定では保護されない追加のフォルダーを指定することもできます。
   - **悪用に対する保護:** システム プロセスとアプリの悪用を緩和するための設定が記述された XML ファイルを指定します。 これらの設定は、Windows 10 デバイス上の Windows Defender Security Center アプリからエクスポートできます。
   - **ネットワーク保護:** 疑わしいドメインへのアクセスをブロックまたは監査するネットワーク保護を設定します。
5. ポリシーを作成するウィザードを完了します。このポリシーはあとでデバイスに展開できます。

### <a name="deploy-an-exploit-guard-policy"></a>Exploit Guard ポリシーを展開する     
Exploit Guard ポリシーを作成したら、Deploy Exploit Guard Policy ウィザードを使用してポリシーを展開します。 そのためには、Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[Endpoint Protection]** の順に移動し、 **[Deploy Exploit Guard Policy]\(Exploit Guard ポリシーの展開\)** をクリックします。

## <a name="limited-support-for-cng-certificates"></a>CNG 証明書の制限付きサポート
<!-- 1356191 -->
このリリース以降では、次のシナリオに [Cryptography API:Next Generation (CNG)](/windows/win32/seccng/cng-features) 証明書テンプレートを使用できるようになりました。

- HTTPS 管理ポイントを使用したクライアントの登録と通信。   
- HTTPS 配布ポイントを使用したソフトウェアの配布とアプリケーションの展開。   
- オペレーティング システムの展開。  
- クライアント メッセージ SDK (最新の更新プログラム) と ISV プロキシ。   
- クラウド管理ゲートウェイの構成。  

CNG 証明書を使用するには、証明機関 (CA) が対象コンピューターに CNG 証明書テンプレートを提供する必要があります。  テンプレートの詳細は、シナリオによって異なります。ただし、次のプロパティは必須です。

- **[互換性]** タブ

    - **[証明機関]** が Windows Server 2008 以降である必要があります。 (Windows Server 2012 推奨)

    - **[証明書の受信者]** が Windows Vista/Server 2008 以降である必要があります。 (Windows 8/Windows Server 2012 推奨)

- **[暗号化]** タブ

    - **[プロバイダーのカテゴリ]** が **[キー格納プロバイダー]** である必要があります。  (必須)

最適な結果を得るには、Active Directory の情報から [サブジェクト名] を構築することをおすすめします。  **[サブジェクト名の形式]** の [DNS 名] を使用し、代替サブジェクト名にその DNS 名を含めます。  それ以外の場合は、デバイスを証明書プロファイルに登録するときに、この情報を提供する必要があります。


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>再起動を待機しているコンピューターに関する説明を改善   <!--1356283 -->
[Technical Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console) では、Configuration Manager コンソールから、再起動を待機しているデバイスを特定する機能が追加されました。

この Technical Preview 以降、再起動を要求するプロセスまたはアクションに関する追加の詳細情報がコンソールに表示されるようになります。

## <a name="device-guard-policy-changes----1355092---"></a>Device Guard ポリシーの変更 <!-- 1355092 -->
1710 Technical Preview ビルドで、Device Guard ポリシーに関連する次の 3 つの変更が加えられました。

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Device Guard ポリシーを Windows Defender Application Control ポリシーという名前に変更
Device Guard ポリシーは、Windows Defender Application Control ポリシーという名前に変更されました。 そのため、たとえば、**Device Guard ポリシーの作成ウィザード**は **Windows Defender Application Control ポリシーの作成ウィザード**になります。

### <a name="restart-is-not-required-to-apply-policies"></a>ポリシー適用のための再起動は不要
Windows バージョン 1709 Fall Creators Update 以降、この新しいバージョンを使用するデバイスでは、Windows Defender Application Control ポリシーを適用するための再起動は必要なくなりました。

再起動は既定です。

#### <a name="try-it-out"></a>試してみましょう。  

再起動をオフにする場合は、次の手順に従います。

1.  **[Create Windows Defender Application Control Policy]\(Windows Defender Application Control ポリシーの作成\)** ウィザードを開きます。
2.  **[全般]** ページで、 **[すべてのプロセスに対してこのポリシーを適用できるように、デバイスの再起動を強制する]** のチェック ボックスをオフにします。
3.  ウィザードが完了するまで **[次へ]** をクリックします。

以前のバージョンの Windows では、強制的に自動で再起動されます。

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>インテリジェント セキュリティ グラフから信頼されているソフトウェアの自動実行

管理者は、Microsoft インテリジェント セキュリティ グラフ (ISG) から良い評価を得て信頼されているソフトウェアを、ロックダウンされたデバイスで実行することを許可できます。 ISG は Windows Defender SmartScreen などの Microsoft サービスで構成されています。

デバイスでソフトウェアを信頼するためには Windows Defender SmartScreen を実行している必要があります。

#### <a name="try-it-out"></a>試してみましょう。  

Windows Defender SmartScreen を実行しているデバイスで、信頼されているソフトウェアを実行するには、次の手順に従います。

1.  **[Create Windows Defender Application Control Policy]\(Windows Defender Application Control ポリシーの作成\)** ウィザードを開きます。
2.  **[追加]** ページで、 **[インテリジェント セキュリティ グラフによって信頼されているソフトウェアを認証する]** のチェック ボックスをオンにします。
3.  **[信頼されているファイルまたはフォルダー]** ボックスに、信頼させるファイルとフォルダーを追加します。
4.  ウィザードが完了するまで **[次へ]** をクリックします。

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Windows Defender Application Guard ポリシーの構成と展開 <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) は、信頼できない Web サイトをオペレーティング システムの他の部分からはアクセスできない安全な分離コンテナーで開くことでユーザーを保護する Windows の新機能です。 この Technical Preview では、設定する Configuration Manager のコンプライアンス設定を使用して、この機能を構成し、コレクションに展開するためのサポートが追加されました。 この機能は、64 ビット版の Windows 10 Creators Update のプレビューでリリースされます。 この機能を今すぐテストするには、この更新プログラムのプレビュー バージョンを使用している必要があります。

### <a name="before-you-start"></a>開始する前に
Windows Defender Application Guard ポリシーを作成して展開するには、ネットワーク分離ポリシーを使用して、ポリシーを展開する Windows 10 デバイスを構成する必要があります。 詳細については、後述のブログ記事をご覧ください。 この機能は、最新の Windows 10 Insider Build でのみ動作します。 これをテストするには、クライアントが最新の Windows 10 Insider Build で実行されている必要があります。

### <a name="try-it-out"></a>試してみましょう。

Windows Defender Application Guard の基本を理解するには、[こちらのブログ記事](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)をご覧ください。

ポリシーを作成し、使用可能な設定を参照するには、次の手順を実行します。
1. **Configuration Manager** コンソールで、 **[資産とコンプライアンス]** を選択します。
2. **[資産とコンプライアンス]** ワークスペースで、 **[概要]**  >  **[Endpoint Protection]**  >  **[Windows Defender Application Guard]** の順に選択します。
3. **[ホーム]** タブの **[作成]** グループで、 **[Windows Defender Application Guard ポリシーの作成]** をクリックします。
4. ブログ記事を参照として使用して、使用可能な設定を参照および構成して、機能を試すことができます。
5. 今回のリリースでは、ウィザードに新しく [ネットワーク定義] ページを追加しました。 このページでは、企業の ID を指定し、企業ネットワークの境界を定義します。

    > [!NOTE]
    > Windows 10 PC の場合、クライアントでネットワーク分離リストが 1 つだけ保存されます。 今回のリリースでは、2 種類のネットワーク分離リスト (Windows 情報保護のリストと Windows Defender Application Guard のリスト) を作成し、クライアントに展開できます。 両方のポリシーを展開する場合、ネットワーク分離リストが一致している必要があります。 一致しないリストを同じクライアントに展開すると失敗します。

    ネットワーク定義の指定方法について詳しくは、Windows 情報保護のドキュメントの「[Windows 情報保護 (WIP) を使用したエンタープライズ データの保護](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)」を参照してください。

6. 完了したら、ウィザードを終了し、1 つ以上の Windows 10 デバイスにポリシーを展開します。

### <a name="further-reading"></a>参考資料

Windows Defender Application Guard の詳細については、[このブログ記事](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)を参照してください。 また、Windows Defender Application Guard のスタンドアロン モードの詳細については、[このブログ記事](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)を参照してください。

## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。