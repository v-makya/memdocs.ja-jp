---
title: 'ブート イメージのカスタマイズ '
titleSuffix: Configuration Manager
description: Configuration Manager または展開イメージのサービスと管理 (DISM) コマンドライン ツールを使用して、ブート イメージをカスタマイズするいくつかの方法について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc679ec7e73e9d43902ad70e09fb2a01c95eed65
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906879"
---
# <a name="customize-boot-images-with-configuration-manager"></a>Configuration Manager を使用してブート イメージを管理する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の各バージョンが、Windows アセスメントおよびデプロイメント キット (Windows ADK) の特定のバージョンをサポートしています。 ブート イメージが、サポートされているバージョンの Windows ADK の Windows PE バージョンに基づいている場合は、Configuration Manager コンソールから利用したり、カスタマイズしたりできます。 それ以外のブート イメージは、別の方法でカスタマイズする必要があります。たとえば、Windows AIK と Windows ADK に含まれている、展開イメージのサービスと管理 (DISM) コマンドライン ツールなどを使います。  

 サポートされている Windows ADK のバージョン、Configuration Manager コンソールからカスタマイズできるブート イメージのベースとなる Windows PE バージョン、DISM でカスタマイズした後で Configuration Manager に追加できるブート イメージのベースとなる Windows PE バージョンは次のとおりです。  

- **Windows ADK バージョン**  

   Windows 10 用 Windows ADK  

- **Configuration Manager コンソールでカスタマイズできる Windows PE ブート イメージのバージョン**  

   Windows PE 10  

- **Configuration Manager コンソールでカスタマイズできない Windows PE ブート イメージのバージョン**  

   Windows PE 3.1<sup>1</sup> および Windows PE 5  

   <sup>1</sup> Windows PE 3.1 のブートイメージしか Configuration Manager に追加することができません。 Windows AIK for Windows 7 (Windows PE 3 の構築用) を Windows AIK Supplement for Windows 7 SP1 (Windows PE 3.1 の構築用) にアップグレードしてください。 Windows AIK Supplement for Windows 7 SP1 は、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=5188)からダウンロードできます。  

   たとえば、Configuration Manager を使っている場合は、Windows 10 用 Windows ADK (Windows PE 10 に基づく) で構築したブート イメージを Configuration Manager コンソールでカスタマイズできます。 一方、Windows PE 5 のブート イメージはサポートされていますが、このブート イメージをカスタマイズするには、別のコンピューターにある Windows 8 用 Windows ADK に付属している DISM を使わなければなりません。 その後、ブート イメージを Configuration Manager コンソールに追加できます。  

  以下のセクションでは、次の Windows PE パッケージを使用して、Configuration Manager で必要とするオプションのコンポーネントをブート イメージに追加する方法を説明します。  

- **WinPE-WMI**: Windows Management Instrumentation (WMI) のサポートを追加します。  

- **WinPE-Scripting**: Windows スクリプト ホスト (WSH) のサポートを追加します。  

- **WinPE-WDS-Tools**: Windows 展開サービス ツールをインストールします。  

  その他の Windows PE パッケージも追加できます。 ブート イメージに追加できるオプションのコンポーネントの詳細については、[WinPE: パッケージの追加 (オプション コンポーネント リファレンス)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference) に関するページを参照してください。

> [!NOTE]
>追加したツールを含むカスタマイズされたブート イメージから WinPE を起動するときは、WinPE からコマンド プロンプトを開き、それを実行するツールのファイル名を入力できます。 これらのツールの場所は、パス変数に自動的に追加されます。 ブート イメージ プロパティの **[カスタマイズ]** タブで **[コマンド サポートを有効にする (テストのみ)]** 設定が選択されている場合は、コマンド プロンプトのみを追加できます。

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Windows PE 5 を使用するブート イメージのカスタマイズ  
 Windows PE 5 を使用するブート イメージをカスタマイズするには、Windows ADK をインストールし、DISM コマンドライン ツールを使ってブート イメージをマウントして、オプションのコンポーネントとドライバーを追加してから、ブート イメージへの変更をコミットします。 ブート イメージをカスタマイズする手順は、次のとおりです。  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Windows PE 5 を使用するブート イメージをカスタマイズするには  

1. コンピューターに Windows ADK をインストールします。このコンピューターは、他のバージョンの Windows ADK や Windows AIK、Configuration Manager のコンポーネントがインストールされていないコンピューターでなければなりません。  

2. Windows 8.1 用 Windows ADK を [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=39982)からダウンロードしてください。  

3. Windows ADK のインストール フォルダー (例: <*インストール パス*>\Windows Kits\\<*バージョン*>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<*x86 または amd64*>\\<*ロケール*>) から、ブート イメージ (wimpe.wim) を、ブート イメージのカスタマイズ作業を行うコンピューターの宛先フォルダーにコピーします。 ここでは、C:\WinPEWAIK というフォルダーを使います。  

4. DISM を使って、ブート イメージをローカルの Windows PE フォルダーにマウントします。 たとえば、次のコマンドを入力します。  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    ここで、C:\WinPEWAIK はブート イメージが含まれているフォルダー、C:\WinPEMount はマウントするフォルダーです。  

   > [!NOTE]
   >  詳細については、[DISM (展開イメージのサービスと管理) リファレンス](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management)に関するページを参照してください。

5. ブート イメージをマウントしたら、DISM を使って、ブート イメージにオプションのコンポーネントを追加します。 Windows PE 5 では、64 ビットのオプションのコンポーネントは <*インストール パス*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs にあります。  

   > [!NOTE]
   >  この手順では、オプション コンポーネントの次の場所が使用されます。C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs。 実際のパスは、インストールした Windows ADK のバージョンと選択したインストール オプションによって異なります。  

    次のように入力して、オプションのコンポーネントをインストールします。  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** " *<ロケール\>* " **\WinPE-SecureStartup_** " *<ロケール\>* " **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** " *<ロケール\>* " **\WinPE-WMI_** " *<ロケール\>* " **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** " *<ロケール\>* " **\WinPE-Scripting** " *<ロケール\>* " **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** " *<ロケール\>* " **\WinPE-WDS-Tools_** " *<ロケール\>* " **.cab"**  

    ここで C:\WinPEMount はマウントしたフォルダーで、ロケールはコンポーネントのロケールです。 たとえば、 **en-us** ロケールの場合、次のように入力します。  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

   > [!TIP]
   >  ブート イメージに追加できるオプションのコンポーネントの詳細については、「[Windows PE オプション コンポーネント リファレンス](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference)」をご覧ください。

6. 必要に応じて、DISM を使って特定のドライバーをブート イメージに追加します。 このためには、次のように入力します。  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** "*ドライバー .inf ファイルへのパス*" **>**  

    ここで、C:\WinPEMount はマウントしたフォルダーです。  

7. 次のように入力して、ブート イメージのマウントを解除して、変更をコミットします。  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    ここで、C:\WinPEMount はマウントしたフォルダーです。  

8. 変更したブート イメージを Configuration Manager に追加して、タスク シーケンスで使用できるようにします。 このためには、次の手順に従って、ブート イメージをインポートします。  

   1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。  

   2. **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開し、 **[ブート イメージ]** をクリックします。  

   3. **[ホーム]** タブの **[作成]** グループで、 **[ブート イメージの追加]** をクリックし、ブート イメージの追加ウィザードを開始します。  

   4. **[データ ソース]** ページで以下のオプションを指定し、 **[次へ]** をクリックします。  

      - **[パス]** ボックスで、ブート イメージ ファイルのパスを指定します。 このパスは、UNC 形式の有効なネットワーク パスでなければなりません。 例:  **\\\\<** <em>servername</em> **>\\<** <em>WinPEWAIK share</em> **>\winpe.wim**.  

      - **[ブート イメージ]** ドロップダウン リストで、インポートするブート イメージを選択します。 WIM ファイルに複数のブート イメージが含まれている場合は、それぞれのイメージが一覧表示されます。  

   5. **[全般]** ページで、以下のオプションを指定して **[次へ]** をクリックします。  

      -   **[名前]** ボックスで、ブート イメージの一意の名前を指定します。  

      -   **[バージョン]** ボックスで、ブート イメージのバージョン番号を指定します。  

      -   **[コメント]** ボックスで、ブート イメージの使用方法について簡単な説明を指定します。  

   6. ウィザードを完了します。  

9. Windows PE のデバッグとトラブルシューティングを行えるように、ブート イメージのコマンド シェルを有効にします。 このためには、次の手順に従います。  

   1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。  

   2. **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開し、 **[ブート イメージ]** をクリックします。  

   3. ブート イメージの一覧で、上の手順で追加したブート イメージを見つけて、そのイメージのパッケージ ID を確認します。 ブート イメージのパッケージ ID は、 **[イメージ ID]** 列に表示されています。  

   4. コマンド プロンプトで **wbemtest** と入力して、Windows Management Instrumentation テストを開きます。  

   5. **[名前空間]** に **\\\\<** <em>SMS プロバイダー コンピューター</em> **>\root\sms\site_<** <em>sitecode</em> **>** と入力し、 **[接続]** をクリックします。  

   6. **[インスタンスを開く]** をクリックし、**sms_bootimagepackage.packageID="<packageID\>"** と入力して、 **[OK]** をクリックします。 パッケージ ID には、手順 3 で確認した ID を入力してください。  

   7. **[オブジェクトの更新]** をクリックして、 **[プロパティ]** ウィンドウの **[EnableLabShell]** をクリックします。  

   8. **[プロパティの編集]** をクリックし、値を **[TRUE]** に変更し、 **[プロパティの保存]** をクリックします。  

   9. **[オブジェクトの保存]** をクリックし、Windows Management Instrumentation Tester を終了します。  

10. タスク シーケンスでブート イメージを使用するには、配布ポイント、配付ポイント グループ、配付ポイントに関連付けられているコレクションにブート イメージを配付する必要があります。 ブート イメージを配付するには、次の手順に従います。  

    1.  Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。  

    2.  **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開し、 **[ブート イメージ]** をクリックします。  

    3.  手順 3 で確認したブート イメージ ID をクリックします。  

    4.  **[ホーム]** タブの **[展開]** グループで、 **[配布ポイントの更新]** をクリックします。  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Windows PE 3.1 を使用するブート イメージのカスタマイズ  
 WinPE 3.1 を使用するブート イメージをカスタマイズするには、Windows AIK と Windows AIK Supplement for Windows 7 SP1 をインストールし、DISM コマンドライン ツールを使ってブート イメージをマウントして、オプションのコンポーネントとドライバーを追加してから、ブート イメージへの変更をコミットします。 ブート イメージをカスタマイズする手順は、次のとおりです。  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Windows PE 3.1 を使用するブート イメージをカスタマイズするには  

1. コンピューターに Windows AIK をインストールします。このコンピューターは、他のバージョンの Windows ADK や Windows AIK、Configuration Manager のコンポーネントがインストールされていないコンピューターでなければなりません。 Windows AIK は、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=5753)からダウンロードしてください。  

2. 手順 1 のコンピューターに Windows AIK Supplement for Windows 7 SP1 をインストールします。 Windows AIK Supplement for Windows 7 SP1 は、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=5188)からダウンロードできます。  

3. Windows AIK のインストール フォルダー (例: <*インストール パス*>\Windows AIK\Tools\PETools\amd64\\) から、ブート イメージ (wimpe.wim) を、ブート イメージのカスタマイズ作業を行うコンピューターのフォルダーにコピーします。 ここでは、C:\WinPEWAIK というフォルダーを使います。  

4. DISM を使って、ブート イメージをローカルの Windows PE フォルダーにマウントします。 たとえば、次のコマンドを入力します。  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    ここで、C:\WinPEWAIK はブート イメージが含まれているフォルダー、C:\WinPEMount はマウントするフォルダーです。  

   > [!NOTE]
   > 詳細については、[DISM (展開イメージのサービスと管理) リファレンス](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management)に関するページを参照してください。

5. ブート イメージをマウントしたら、DISM を使って、ブート イメージにオプションのコンポーネントを追加します。 たとえば、Windows PE 3.1 では、オプションのコンポーネントは、<*インストール パス*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\ にあります。  

   > [!NOTE]
   >  この手順では、オプション コンポーネントの次の場所が使用されます。C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs。 実際のパスは、インストールした Windows AIK のバージョンと選択したインストール オプションによって異なります。  

    次のように入力して、オプションのコンポーネントをインストールします。  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** " *<ロケール\>* " **\winpe-wmi_** " *<ロケール\>* " **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** " *<ロケール\>* " **\winpe-scripting_** " *<ロケール\>* " **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** " *<ロケール\>* " **\winpe-wds-tools_** " *<ロケール\>* " **.cab"**  

    ここで C:\WinPEMount はマウントしたフォルダーで、ロケールはコンポーネントのロケールです。 たとえば、 **en-us** ロケールの場合、次のように入力します。  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

   > [!TIP]
   >  ブート イメージに追加できる他のパッケージの詳細については、「[パッケージを Windows PE イメージに追加する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd799312(v=ws.10))」をご覧ください。

6. 必要に応じて、DISM を使って特定のドライバーをブート イメージに追加します。 このためには、次のように入力します。  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** "*ドライバー .inf ファイルへのパス*" **>**  

    ここで、C:\WinPEMount はマウントしたフォルダーです。  

7. 次のように入力して、ブート イメージのマウントを解除して、変更をコミットします。  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    ここで、C:\WinPEMount はマウントしたフォルダーです。  

8. 変更したブート イメージを Configuration Manager に追加して、タスク シーケンスで使用できるようにします。 このためには、次の手順に従って、ブート イメージをインポートします。  

   1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。  

   2. **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開し、 **[ブート イメージ]** をクリックします。  

   3. **[ホーム]** タブの **[作成]** グループで、 **[ブート イメージの追加]** をクリックし、ブート イメージの追加ウィザードを開始します。  

   4. **[データ ソース]** ページで以下のオプションを指定し、 **[次へ]** をクリックします。  

      - **[パス]** ボックスで、ブート イメージ ファイルのパスを指定します。 このパスは、UNC 形式の有効なネットワーク パスでなければなりません。 例:  **\\\\<** <em>servername</em> **>\\<** <em>WinPEWAIK share</em> **>\winpe.wim**.  

      - **[ブート イメージ]** ドロップダウン リストで、インポートするブート イメージを選択します。 WIM ファイルに複数のブート イメージが含まれている場合は、それぞれのイメージが一覧表示されます。  

   5. **[全般]** ページで、以下のオプションを指定して **[次へ]** をクリックします。  

      -   **[名前]** ボックスで、ブート イメージの一意の名前を指定します。  

      -   **[バージョン]** ボックスで、ブート イメージのバージョン番号を指定します。  

      -   **[コメント]** ボックスで、ブート イメージの使用方法について簡単な説明を指定します。  

   6. ウィザードを完了します。  

9. Windows PE のデバッグとトラブルシューティングを行えるように、ブート イメージのコマンド シェルを有効にします。 このためには、次の手順に従います。  

   1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。  

   2. **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開し、 **[ブート イメージ]** をクリックします。  

   3. ブート イメージの一覧で、上の手順で追加したブート イメージを見つけて、そのイメージのパッケージ ID を確認します。 ブート イメージのパッケージ ID は、 **[イメージ ID]** 列に表示されています。  

   4. コマンド プロンプトで **wbemtest** と入力して、Windows Management Instrumentation テストを開きます。  

   5. **[名前空間]** に **\\\\<** <em>SMS プロバイダー コンピューター</em> **>\root\sms\site_<** <em>sitecode</em> **>** と入力し、 **[接続]** をクリックします。  

   6. **[インスタンスを開く]** をクリックし、**sms_bootimagepackage.packageID="<packageID\>"** と入力して、 **[OK]** をクリックします。 パッケージ ID には、手順 3 で確認した ID を入力してください。  

   7. **[オブジェクトの更新]** をクリックして、 **[プロパティ]** ウィンドウの **[EnableLabShell]** をクリックします。  

   8. **[プロパティの編集]** をクリックし、値を **[TRUE]** に変更し、 **[プロパティの保存]** をクリックします。  

   9. **[オブジェクトの保存]** をクリックし、Windows Management Instrumentation Tester を終了します。  

10. タスク シーケンスでブート イメージを使用するには、配布ポイント、配付ポイント グループ、配付ポイントに関連付けられているコレクションにブート イメージを配付する必要があります。 ブート イメージを配付するには、次の手順に従います。  

    1.  Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。  

    2.  **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開し、 **[ブート イメージ]** をクリックします。  

    3.  手順 3 で確認したブート イメージ ID をクリックします。  

    4.  **[ホーム]** タブの **[展開]** グループで、 **[配布ポイントの更新]** をクリックします。  
