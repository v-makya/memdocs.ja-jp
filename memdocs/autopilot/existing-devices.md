---
title: 既存のデバイスの Windows 自動操縦展開
description: Windows 自動操縦による最新のデスクトップ展開を使用すると、既存のデバイスに Windows 10 の最新バージョンを簡単に展開できます。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: fc13a3a73e5e043d01bf5c7a3d310c496714caee
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908394"
---
# <a name="windows-autopilot-deployment-for-existing-devices"></a>既存のデバイスの Windows 自動操縦展開

**適用対象: Windows 10**

Windows 自動操縦による最新のデスクトップ展開を使用すると、既存のデバイスに Windows 10 の最新バージョンを簡単に展開できます。 作業に必要なアプリが自動的にインストールされます。 仕事用プロファイルが同期されているので、すぐに作業を再開できます。

このトピックでは、windows 自動操縦を使用して、Windows 7 また Windows 8.1 はドメインに参加しているコンピューターを、Azure Active Directory または Active Directory (Hybrid Azure AD Join) に参加している Windows 10 デバイスに変換する方法について説明します。

>[!NOTE]
>既存のデバイスの Windows 自動操縦機能では、ユーザー主導の Azure Active Directory と Hybrid Azure AD プロファイルのみがサポートされます。 自己展開プロファイルはサポートされていません。

## <a name="prerequisites"></a>前提条件

- 現在サポートされているバージョンの Microsoft Endpoint Configuration Manager current branch または technical preview ブランチ。 
- [WINDOWS ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) 1803 以降
    - Configuration Manager サポートの詳細については、「 [Windows 10 ADK のサポート](/configmgr/core/plan-design/configs/support-for-windows-10#windows-10-adk)」を参照してください。
- 割り当てられた Microsoft Intune ライセンス
- Azure Active Directory Premium
- オペレーティングシステムイメージとして Configuration Manager にインポートされた Windows 10 バージョン1809以降
  - **重要**: Configuration Manager の組み込みの**windows 自動操縦**タスクシーケンステンプレートで windows 10 1903 を使用している場合は、「[既知の問題](known-issues.md)」を参照してください。 現時点では、このタスクシーケンスの手順の1つは、Windows 10 バージョン1903で適切に動作するように編集する必要があります。

## <a name="procedures"></a>手順

### <a name="configure-the-enrollment-status-page-optional"></a>[登録ステータス] ページを構成する (省略可能)

必要に応じて、Intune を使用して自動操縦の [登録ステータスページ](enrollment-status.md) を設定できます。

[登録および状態] ページを有効にして構成するには、次のようにします。

1. [Azure portal で Intune を](https://aka.ms/intuneportal)開きます。
2. **Intune > デバイスの登録**にアクセスして Windows の登録を > し、[登録ステータスページをセットアップ](/intune/windows-enrollment-status)します。 
3. **Azure Active Directory > モビリティ (mdm および MAM) Microsoft Intune >** にアクセスして、[自動 MDM 登録を構成](/configmgr/mdm/deploy-use/enroll-hybrid-windows#enable-windows-10-automatic-enrollment)し、一部またはすべてのユーザーに対して mdm ユーザースコープを構成します。 

次の例を参照してください。

![[登録ステータス] ページ](images/esp-config.png)<br><br>
![mdm](images/mdm-config.png)

### <a name="create-the-json-file"></a>JSON ファイルの作成 

>[!TIP]
>Windows Server 2012/2012 R2 または Windows 7/8.1 を実行しているコンピューターで次のコマンドを実行するには、まず [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616)をダウンロードしてインストールする必要があります。

1. インターネットに接続されている Windows PC またはサーバーで、管理者特権の Windows PowerShell コマンドウィンドウを開きます。
2. 次の行を入力して、必要なモジュールをインストールします。

    #### <a name="install-required-modules"></a>必要なモジュールをインストールする

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module AzureAD -Force
    Install-Module WindowsAutopilotIntune -Force
    Install-Module Microsoft.Graph.Intune -Force
    ```
    
3. 次の行を入力し、Intune の管理者資格情報を入力します。
   - 指定したユーザーアカウントに十分な管理者権限があることを確認してください。

     ```powershell
     Connect-MSGraph
     ```
     アカウントのユーザーとパスワードは、標準の Azure AD フォームを使用して要求されます。 ユーザー名とパスワードを入力し、[ **サインイン**] をクリックします。 
     <br>次の例を参照してください。

     ![Azure AD 認証](images/pwd.png)

     Intune Graph Api を初めて使用する場合は、Microsoft Intune PowerShell の読み取りと書き込みのアクセス許可も有効にするように求められます。 これらのアクセス許可を有効にするには、次の手順を実行します。
   - **代理または組織の同意**を選択する
   - **[Accept]\(受け入れる\)** をクリックします

4. 次に、指定した Intune テナントで使用可能なすべての自動操縦プロファイルを JSON 形式で取得して表示します。

    #### <a name="retrieve-profiles-in-autopilot-for-existing-devices-json-format"></a>既存のデバイスの JSON 形式の自動操縦でプロファイルを取得する

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    ```

    次のサンプル出力を参照してください (長い行を表示するには、下部にある水平スクロールバーを使用します)。
    <pre style="overflow-y: visible">
    PS C:\> Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    {
        "CloudAssignedTenantId":  "1537de22-988c-4e93-b8a5-83890f34a69b",
        "CloudAssignedForcedEnrollment":  1,
        "Version":  2049,
        "Comment_File":  "Profile Autopilot Profile",
        "CloudAssignedAadServerData":  "{\"ZeroTouchConfig\":{\"CloudAssignedTenantUpn\":\"\",\"ForcedEnrollment\":1,\"CloudAssignedTenantDomain\":\"M365x373186.onmicrosoft.com\"}}",
        "CloudAssignedTenantDomain":  "M365x373186.onmicrosoft.com",
        "CloudAssignedDomainJoinMethod":  0,
        "CloudAssignedOobeConfig":  28,
        "ZtdCorrelationId":  "7F9E6025-1E13-45F3-BF82-A3E8C5B59EAC"
    }</pre>

    各プロファイルは、中かっこ **{}** 内にカプセル化されます。 前の例では、1つのプロファイルが表示されています。     

    JSON ファイルで使用されるプロパティの説明については、次の表を参照してください。


   |                          プロパティ                          |                                                                                                                                                                        説明                                                                                                                                                                         |
   |------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                 バージョン (number、optional)                 |                                                                                                                 JSON ファイルの形式を識別するバージョン番号。  Windows 10 1809 の場合、指定するバージョンは2049である必要があります。                                                                                                                  |
   |           CloudAssignedTenantId (guid、必須)           |                                                                                      使用する必要がある Azure Active Directory テナント ID。  これはテナントの GUID であり、テナントの [プロパティ] にあります。  値には中かっこを含めないでください。                                                                                       |
   |        CloudAssignedTenantDomain (文字列、必須)        |                                                                                                                                  使用する必要がある Azure Active Directory テナント名 (例: tenant.onmicrosoft.com)。                                                                                                                                  |
   |         CloudAssignedOobeConfig (number, required)         |                                                                           これは、構成された自動操縦設定を示すビットマップです。 値は次のとおりです: SkipCortanaOptIn = 1、OobeUserNotLocalAdmin = 2、SkipExpressSettings = 4、SkipOemRegistration = 8、SkipEula = 16                                                                           |
   |      CloudAssignedDomainJoinMethod (number, required)      |                                                                                                                                    このプロパティは、デバイスが Azure Active Directory に参加するか Active Directory (Hybrid Azure AD Join) するかを指定します。  値は次のとおりです: Active AD Join = 0、Hybrid Azure AD Join = 1                                                        |
   |      CloudAssignedForcedEnrollment (number, required)      |                                                                                                                         デバイスで AAD 参加と MDM 登録が必要であることを指定します。  <br>0 = 必須ではありません。 1 = 必須です。                                                                                                                         |
   |             ZtdCorrelationId (guid、必須)              | 登録プロセスの一部として Intune に提供される一意の GUID (中かっこなし)。 ZtdCorrelationId は、"OfflineAutoPilotEnrollmentCorrelator" として登録メッセージに含められます。 この属性は、オフライン登録によるゼロタッチプロビジョニングで登録されたデバイスで登録が行われている場合にのみ表示されます。 |
   | CloudAssignedAadServerData (エンコードされた JSON 文字列、必須) |                                                  ブランド化に使用される埋め込み JSON 文字列。 AAD corp ブランド化が有効になっている必要があります。 <br> 値の例: "CloudAssignedAadServerData": "{ \" ZeroTouchConfig \" : { \" CloudAssignedTenantUpn \" : \" \" , \" CloudAssignedTenantDomain \" : \" tenant.onmicrosoft.com \" }}"                                                   |
   |         CloudAssignedDeviceName (文字列、省略可能)         |                                                                          コンピューターに自動的に割り当てられる名前。  これは、自動操縦プロファイルの一部として Intune で構成できる命名パターン規則に従います。また、使用する明示的な名前を指定することもできます。                                                                           |


5. 自動操縦プロファイルは、ASCII または ANSI 形式で JSON ファイルとして保存する必要があります。 Windows PowerShell の既定値は Unicode 形式であるため、コマンドの出力をファイルにリダイレクトする場合は、ファイル形式も指定する必要があります。 たとえば、Windows PowerShell を使用してファイルを ASCII 形式で保存するには、ディレクトリを作成し (例: C:\ 自動操縦)、次のようにプロファイルを保存します (コマンド文字列全体を表示するには、下部にある水平スクロールバーを使用します)。

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON | Out-File c:\Autopilot\AutopilotConfigurationFile.json -Encoding ASCII
    ```
    **重要**: ファイル名は、ASCII/ANSI としてエンコードされていることに加えて、 **AutopilotConfigurationFile.js** という名前にする必要があります。 

    必要に応じて、プロファイルをテキストファイルに保存し、メモ帳で編集することができます。 メモ帳で、[名前を付け **て保存** ] を **選択し、** [ **エンコード**] の横にあるドロップダウンリストから [ANSI] を選択する必要があります。 次の例を参照してください。

    ![メモ帳 JSON](images/notepad.png)

    ファイルを保存したら、Microsoft エンドポイント Configuration Manager パッケージソースとして適切な場所にファイルを移動します。

    >[!IMPORTANT]
    >複数の JSON プロファイルファイルを使用できますが、OOBE が自動操縦エクスペリエンスに従うためには、それぞれ ** にAutopilotConfigurationFile.js** という名前を付ける必要があります。 また、ファイルは ANSI としてエンコードする必要があります。 <br><br>**Unicode または utf-8 エンコードを使用してファイルを保存するか、別のファイル名を付けて保存すると、Windows 10 OOBE は自動操縦エクスペリエンスに従いません**。<br>


### <a name="create-a-package-containing-the-json-file"></a>JSON ファイルを含むパッケージを作成する

1. Configuration Manager で、 **Library\Overview\Application**に移動します。
2. リボンで、[**パッケージの作成**] をクリックします。
3. **パッケージとプログラムの作成ウィザード**で、次の**パッケージ**と**プログラムの種類**の詳細を入力します。<br>
    - <u>名前</u>:**既存のデバイス構成の自動**実行
    - [ **このパッケージにソースファイルを含める** ] チェックボックスをオンにします。
    - <u>ソースフォルダー</u>: [ **参照** ] をクリックし、ファイルの AutopilotConfigurationFile.jsを含む UNC パスを指定します。 
    - **[OK]** をクリックし、 **[次へ]** をクリックします。
    - <u>プログラムの種類</u>:**プログラムを作成**しない
4. **[次へ]** を 2 回クリックし、**[閉じる]** をクリックします。

**注**: 後日 Intune でユーザー主導の自動操縦プロファイルの設定を変更した場合は、JSON ファイルを更新して、関連付けられている Configuration Manager パッケージを再配布する必要もあります。

### <a name="create-a-target-collection"></a>ターゲットコレクションを作成する

>[!NOTE]
>既存のコレクションを再利用するように選択することもできます。

1. **[資産と Compliance\Overview\Device コレクション**] に移動します。
2. リボンで [**作成**] をクリックし、[**デバイスコレクションの作成**] をクリックします。
3. **デバイスコレクションの作成ウィザード**で、次の**全般的な**詳細を入力します。
   - <u>名前</u>:**既存のデバイスコレクションの自動**実行
   - Comment: (省略可能)
   - <u>限定コレクション</u>: [**参照**] をクリックし、[**すべてのシステム**] を選択します。

     >[!NOTE]
     >必要に応じて、限定コレクションに別のコレクションを使用することもできます。 アップグレードするデバイスは、選択したコレクションで ConfigMgr エージェントを実行している必要があります。

4. [ **次へ**] をクリックし、次の **メンバーシップ規則** の詳細を入力します。
   - [ **規則の追加** ] をクリックし、ターゲットテスト用の Windows 7 デバイスを新しいコレクションに追加するには、直接またはクエリベースの収集ルールを指定します。
   - たとえば、ワイプして再読み込みするコンピューターのホスト名が PC-01 であり、属性として名前を使用する場合は、[ **> > 規則の追加**] をクリックして、[次へ] > [次へ] をクリックし、[**値**] の横に「 **PC-01** 」と入力します。 [**次へ**] をクリックし、[**リソース**] の下にある [ **PC-01** ] を選択します。 次の例を参照してください。

     ![](images/pc-01a.png)
     Resource2 という名前の resource1.resx ![](images/pc-01b.png)

5. 既定の設定を使用してデバイスコレクションの作成を続行します。
    - このコレクションで増分更新を使用する: 選択されていません
    - このコレクションの完全な更新をスケジュールする: 既定
    - [**次へ**] を2回クリックし、[**閉じる**] をクリックします。

### <a name="create-an-autopilot-for-existing-devices-task-sequence"></a>既存のデバイスの自動操縦タスクシーケンスを作成する

>[!TIP]
>次の手順では、Windows 10 1803 以降のブートイメージが必要です。 Configuration Manager ベンダーの [ソフトウェアライブラリ]、[オペレーティングシステム]、[ **ブートイメージ** ] の順に選択し、使用可能なブートイメージを確認し、 **OS のバージョン** が 10.0.17134.1 (Windows 10 バージョン 1803) 以降であることを確認します。

1. Configuration Manager コンソールで、[ソフトウェアライブラリ]、[概要]、[**オペレーティングシステム \ タスクシーケンス**] の順に移動します。
2. [ホーム] リボンで、[**タスクシーケンスの作成**] をクリックします。
3. [**既存のイメージパッケージをインストールする**] を選択し、[**次へ**] をクリックします。
4. タスクシーケンスの作成ウィザードで、次の情報を入力します。
   - <u>タスクシーケンス名</u>:**既存のデバイスの自動**実行
   - <u>ブートイメージ</u>: [ **参照** ] をクリックし、Windows 10 ブートイメージ (1803 以降) を選択します。
   - [ **次へ**] をクリックし、[Windows のインストール] ページで [ **参照** ] をクリックして、windows 10 **イメージパッケージ** と **イメージインデックス**バージョン1803以降を選択します。
   - [ **オペレーティングシステムをインストールする前に対象のコンピュータのパーティションを設定してフォーマットする** ] チェックボックスをオンにします。
   - [ **BitLocker で使用するタスクシーケンスを構成する** ] チェックボックスをオンまたはオフにします。 これは省略可能です。
   - <u>プロダクトキー</u> と <u>サーバーライセンスモード</u>: 必要に応じて、プロダクトキーとサーバーライセンスモードを入力します。
   - <u>ローカル管理者パスワードをランダムに生成し、すべてのサポートプラットフォームでアカウントを無効にします (推奨)</u>: 省略可能。
   - <u>アカウントを有効にし、ローカル管理者パスワードを指定</u>します (省略可能)。
   - [ **次へ**] をクリックし、[ネットワークの構成] ページで [ワーク **グループに参加** ] を選択し、[ **ワークグループ**] の横に名前 (例: ワークグループ) を指定します。

     > [!IMPORTANT]
     > [既存のデバイスの自動操縦] タスクシーケンスでは、システム準備ツール (sysprep) を使用する [ **Windows のキャプチャの準備** ] アクションが実行されます。 ターゲットコンピューターがドメインに参加している場合、この操作は失敗します。
     
     >[!IMPORTANT]
     > システム準備ツール (sysprep) は、/Generalize パラメーターを使用して実行されます。これは、Windows 10 バージョン1903および1909では、自動操縦プロファイルファイルが削除され、マシンは自動操縦フェーズではなく、OOBE フェーズで起動します。 この問題を解決するには、 [Windows 自動操縦に関する既知の問題](known-issues.md)を参照してください。

5. [ **次へ**] をクリックし、もう一度 [ **次へ** ] をクリックして、[Configuration Manager のインストール] ページの既定の設定をそのまま使用します。
6. [状態移行] ページで、次の情報を入力します。
   - [ **ユーザー設定とファイルをキャプチャ** する] チェックボックスをオフにします。
   - [ **ネットワーク設定のキャプチャ** ] チェックボックスをオフにします。
   - [ **Microsoft Windows の設定をキャプチャ** する] チェックボックスをオフにします。
   - **[次へ]** をクリックします。

     >[!NOTE]
     >Windows PE では、[既存のデバイスの自動操縦] タスクシーケンスは完了するため、ユーザー状態移行ツールキット (USMT) のデータ移行はサポートされていません。これは、ユーザー状態を新しい OS に復元する方法がないためです。  また、ユーザー状態移行ツールキット (USMT) は、Azure AD に参加しているデバイスをサポートしていません。

7. [更新プログラムを含める] ページで、使用可能な3つのオプションのいずれかを選択します。 この選択は省略可能です。
8. [アプリケーションのインストール] ページで、必要に応じてアプリケーションを追加します。 これは省略可能です。
9. [ **次へ**] をクリックして設定を確認し、[ **次へ**] をクリックして、[ **閉じる**] をクリックします。
10. [既存のデバイスの自動操縦] タスクシーケンスを右クリックし、[ **編集**] をクリックします。
11. タスクシーケンスエディターの [ **オペレーティングシステムのインストール** ] グループで、[ **Windows 設定の適用** ] アクションをクリックします。
12. [ **追加** ] をクリックし、[ **新しいグループ**] をクリックします。
13. **既存のデバイス構成について**、グループ**名**を**新しいグループ**から自動操縦に変更します。
14. [ **追加**] をクリックし、[ **全般**] をポイントして、[ **コマンドラインの実行**] をクリックします。
15. [ **コマンドラインの実行** ] ステップが、[ **既存のデバイスの自動構成** ] グループの下に入れ子になっていることを確認します。
16. [**既存のデバイス構成ファイルの自動操縦を適用**する] の**名前**を変更し、[**コマンドライン**] テキストボックスに次のコードを貼り付けて、[**適用**] をクリックします。
    ```
    cmd.exe /c xcopy AutopilotConfigurationFile.json %OSDTargetSystemDrive%\windows\provisioning\Autopilot\ /c
    ```
    -  **AutopilotConfigurationFile.jsに** は、前に作成した既存のデバイスパッケージの自動操縦に存在する JSON ファイルの名前を指定する必要があります。

17. [ **既存のデバイスの自動操縦の適用] 構成ファイル** のステップで、[ **パッケージ** ] チェックボックスをオンにし、[ **参照**] をクリックします。
18. 前の手順で作成した **既存のデバイス構成パッケージの自動操縦** を選択し、[ **OK]** をクリックします。 このセクションの最後に例が表示されます。
19. [ **オペレーティングシステムのセットアップ** ] グループで、[ **Windows と Configuration Manager のセットアップ** ] タスクをクリックします。
20. [ **追加** ] をクリックし、[ **新しいグループ**] をクリックします。
21. **新しいグループ**の**名前**を変更し**て、自動操縦用にデバイスを準備**する
22. [ **自動操縦用デバイスの準備** ] グループがタスクシーケンスの最後の手順であることを確認します。 必要に応じて [ **下へ移動** ] ボタンを使用します。
23. [ **自動操縦用デバイスの準備** ] グループを選択し、[ **追加**] をクリックして [ **イメージ** ] をポイントし、[ **ConfigMgr クライアントのキャプチャの準備**] をクリックします。
24. 2番目の手順を追加するには、[ **追加**] をクリックし、[ **イメージ**] をポイントし、[ **Windows のキャプチャの準備**] をクリックします。 この手順では、次の設定を使用します。
    - <u>大容量記憶装置ドライバーの一覧を自動的に作成</u>する: **未選択**
    - <u>アクティブ化フラグをリセットしません</u>: 選択され**ていませ**ん
    - <u>この操作の実行後にコンピューターをシャットダウンする</u>: **オプション**

    ![自動操縦タスクシーケンス](images/ap-ts-1.png)

25. [ **OK** ] をクリックして、タスクシーケンスエディターを閉じます。

> [!NOTE]
> Windows 10 1903 および1909では、の **AutopilotConfigurationFile.jsは [** **windows のキャプチャの準備** ] ステップによって削除されます。 詳細と回避策については、「 [Windows 自動操縦-既知の問題](known-issues.md) 」を参照してください。

### <a name="deploy-content-to-distribution-points"></a>配布ポイントへのコンテンツの展開

次に、タスクシーケンスに必要なすべてのコンテンツが配布ポイントに展開されていることを確認します。

1. [ **既存のデバイスの自動操縦** ] タスクシーケンスを右クリックし、[ **コンテンツの配布**] をクリックします。
2. [ **次へ**] をクリックし、 **配布するコンテンツを確認**して、[ **次へ**] をクリックします。
3. [コンテンツの配布の指定] ページで、[ **追加** ] をクリックして、 **配布ポイント** または **配布ポイントグループ**を指定します。
4. 配布ポイントの追加ウィザードまたは配布ポイントグループの追加ウィザードで、タスクシーケンスの実行時に JSON ファイルを取得できるようにするコンテンツの宛先を指定します。
5. コンテンツの配布の指定が完了したら、[ **次へ** ] を2回クリックし、[ **閉じる**] をクリックします。

### <a name="deploy-the-os-with-autopilot-task-sequence"></a>自動操縦タスクシーケンスを使用して OS を展開する

1. [ **既存のデバイスの自動** 入力] タスクシーケンスを右クリックし、[ **展開**] をクリックします。
2. ソフトウェアの展開ウィザードで、次の**全般的な****設定と展開の設定**の詳細を入力します。
    - <u>タスクシーケンス</u>:  **既存のデバイスに対して自動**実行します。
    - <u>コレクション</u>: [ **参照** ] をクリックし、[ **既存のデバイスコレクション** ] (または希望する別のコレクション) の [自動操縦] を選択します。
    - [ **次へ** ] をクリックして、 **展開設定**を指定します。
    - <u>操作</u>: **インストール**します。
    - <u>目的</u>: **使用可能**。 必要に応じて、[**使用可能**な代わりに**必須**] を選択できます。 これは、誤った構成による影響を起因テストの際にはお勧めしません。
    - <u>次のものを使用できるように</u>します。 **Configuration Manager クライアントのみ**です。 注: テストのコンテキストに関連するオプションをここで選択します。 ターゲットクライアントに Configuration Manager エージェントまたは Windows がインストールされていない場合は、PXE またはブートメディアを含むオプションを選択する必要があります。
    - [ **次へ** ] をクリックして、 **スケジュール** の詳細を指定します。
    - <u>この展開が使用可能になる日時をスケジュールする</u>: オプション
    - <u>この展開の有効期限を設定する</u>: オプション
    - [ **次へ** ] をクリックして、 **ユーザーエクスペリエンス** の詳細を指定します。
    - <u>タスクシーケンスの進行状況の表示</u>: 選択されました。
    - <u>ソフトウェアのインストール</u>: 選択されていません。
    - <u>[システムの再起動 (インストールの完了に必要な場合)</u>]: 選択されていません。
    - <u>期限またはメンテナンス期間中にコミットが変更された (再起動が必要)</u>: オプション。
    - <u>クライアントのタスクシーケンスをインターネット上で実行できるように</u>する: オプション
    - [ **次** へ] をクリックして、 **アラート** の詳細を指定します。
    - <u>しきい値が次の値より大きい場合に展開アラートを作成</u>する: 省略可能。
    - [ **次** へ] をクリックして、 **配布ポイント** の詳細を指定します。
    - <u>展開オプション</u>: **実行中のタスクシーケンスで必要になったときに、ローカルでコンテンツをダウンロード**します。
    - <u>ローカルの配布ポイントが使用できない場合は、リモートの配布ポイントを使用</u>します (省略可能)。
    - <u>[既定のサイト境界グループの配布ポイントをクライアントが使用できるようにする]</u>: (省略可能)
    - [ **次へ**] をクリックして設定を確認し、[ **次へ**] をクリックして、[ **閉じる**] をクリックします。

### <a name="complete-the-client-installation-process"></a>クライアントのインストールプロセスを完了する

1. 対象の Windows 7 または Windows 8.1 クライアントコンピューターでソフトウェアセンターを開きます。 これを行うには、[スタート] ボタンをクリックし、検索ボックスに「 **software** 」と入力するか、Windows PowerShell またはコマンドプロンプトで次のように入力します。

    ```
    C:\Windows\CCM\SCClient.exe
    ```

2. [ソフトウェアライブラリ] で、[ **既存のデバイスの自動操縦** ] を選択し、[ **インストール**] をクリックします。 次の例を参照してください。

    ![](images/sc.png)Resource2 という名前の resource2 ![](images/sc1.png)

タスクシーケンスは、コンテンツをダウンロードし、再起動して、ドライブをフォーマットし、Windows 10 をインストールします。 その後、デバイスが自動操縦用に準備されます。 タスクシーケンスが完了すると、デバイスは OOBE で起動し、自動操縦エクスペリエンスを提供します。

![更新-1 ](images/up-1.png)
 ![ 更新-2 ](images/up-2.png)
 ![ 更新-3](images/up-3.png)

>[!NOTE]
>デバイスを Active Directory (Hybrid Azure AD Join) に参加させる場合は、"すべてのデバイス" を対象とするドメイン参加デバイス構成プロファイルを作成する必要があります (グループベースのターゲット設定を実行するコンピューターには、Azure Active Directory デバイスオブジェクトが存在しないため)。  詳細については、「 [ハイブリッド Azure Active Directory のユーザー駆動モード](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join) 」を参照してください。

### <a name="register-the-device-for-windows-autopilot"></a>Windows 自動操縦用デバイスの登録

自動操縦によってプロビジョニングされたデバイスは、最初の起動時にガイド付きの OOBE 自動操縦エクスペリエンスのみを受け取ります。 Windows 10 に更新したら、デバイスを登録して、PC がリセットされたときに自動操縦機能を使用できるようにする必要があります。 割り当てられたグループの自動登録を有効にするには、[ **すべての対象デバイスを自動操縦に変換する** ] 設定を使用します。 詳しくは、「[Autopilot Deployment プロファイルを作成する](enrollment-autopilot.md#create-an-autopilot-deployment-profile)」をご覧ください。

「 [Windows 自動操縦にデバイスを追加する](add-devices.md)」も参照してください。

## <a name="speeding-up-the-deployment-process"></a>展開プロセスの高速化

デプロイプロセスから約20分後に削除するには、 [既存のデバイスの Windows 自動操縦を高速化](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices)するための手順を含む Michael/ehau のブログを参照してください。