---
title: Windows アプリケーションを作成する
titleSuffix: Configuration Manager
description: Configuration Manager での Windows アプリケーションの作成と展開について詳しく説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 77fee5931046bc706f965a9a5d738f5a7e2223f4
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819628"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Configuration Manager で Windows アプリケーションを作成する

*適用対象:Configuration Manager (Current Branch)*

[アプリケーションを作成する](../deploy-use/create-applications.md)ための Configuration Manager の他の要件と手順に加えて、Windows デバイス用アプリケーションを作成および展開するときには次の考慮事項について検討します。  

## <a name="general-considerations"></a><a name="bkmk_general"></a> 一般的な考慮事項  

Configuration Manager では、Windows 8.1 および Windows 10 デバイスの Windows アプリ パッケージ (.appx) 形式とアプリバンドル (.appxbundle) 形式の展開がサポートされています。

Configuration Manager コンソールでアプリケーションを作成するときは、アプリケーション インストール ファイルの **[種類]** として **[Windows アプリケーション パッケージ (\*.appx、\*.appxbundle、\* msix、\*.msixbundle)]** を選択します。 一般にアプリを作成する方法の詳細については、[アプリケーションの作成](../deploy-use/create-applications.md)に関するページを参照してください。 MSIX 形式の詳細については、「[Support for MSIX format](#bkmk_msix)」 (MSIX 形式のサポート) を参照してください。

> [!Note]  
> Configuration Manager の新機能を利用するには、最初にクライアントを最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a> デバイス上のすべてのユーザーに対して Windows アプリ パッケージをプロビジョニングする
<!--1358310-->
デバイス上のすべてのユーザーに対して、Windows アプリ パッケージを含むアプリケーションをプロビジョニングします。 このシナリオの 1 つの一般的な例では、ある学校の生徒が使用するすべてのデバイスに、Minecraft:Education Edition などの、ビジネス向け Microsoft Store および教育機関向け Microsoft Store からアプリをプロビジョニングします。 これまでは、Configuration Manager では、これらのアプリケーションのユーザーごとのインストールのみがサポートされていました。 新しいデバイスにサインインした後、学生はアプリにアクセスするまで待機する必要があります。 これからは、すべてのユーザー用のデバイスにアプリがプロビジョニングされている場合、より迅速に生産性を高めることができます。

> [!Important]  
> 予期しない結果になる場合があるため、1 つのデバイス上で同じ Windows アプリ パッケージの異なるバージョンのインストール、プロビジョニング、および更新を行う際には注意してください。 この動作は、Configuration Manager を使用してアプリをプロビジョニングするが、ユーザーに Microsoft Store からのアプリの更新を許可する場合に発生する可能性があります。 詳細については、[ビジネス向け Microsoft Store からアプリを管理する](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)場合の「次のステップ」のガイダンスを参照してください。  

オフライン アプリを構成マネージャー クライアントを使用した Windows 10 デバイスに展開する場合、Configuration Manager の展開の外部のアプリケーションをユーザーが更新できないようにしてください。 オフライン アプリの更新の制御は、教室などのマルチ ユーザー環境で特に重要です。 詳細については、「[Configuration Manager を使用してビジネス向けおよび教育機関向け Microsoft Store のアプリを管理する](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)」を参照してください。<!-- MEMDocs#316 -->

Configuration Manager では、Windows 10 のすべてのサポート対象バージョンでのアプリのプロビジョニングがサポートされています。<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

この機能に対して Windows アプリ展開の種類を構成するには、オプション **[このアプリケーションをデバイス上のすべてのユーザーにプロビジョニングする]** を有効にします。 詳細については、「[Create applications](../deploy-use/create-applications.md)」 (アプリケーションを作成する) を参照してください。

> [!Note]  
> ユーザーが既にサインオンしているデバイスからプロビジョニングされたアプリケーションをアンインストールする必要がある場合は、2 つのアンインストール展開を作成する必要があります。 1 つ目のアンインストール展開は、デバイスを含むデバイス コレクションを対象とします。 2 つ目のアンインストール展開は、アプリケーションがプロビジョニングされているデバイスに既にサインオンしているユーザーを含むユーザー コレクションを対象とします。 デバイスのプロビジョニングされているアプリをアンインストールしても、Windows では、現在、そのユーザーのアプリはアンインストールされません。

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a> MSIX 形式のサポート
<!--1357427-->

Configuration Manager では、Windows 10 のアプリ パッケージ (.msix) 形式とアプリ バンドル (.msixbundle) 形式がサポートされます。 Windows 10 バージョン 1809 以降で、これらの形式がサポートされています。

- MSIX の概要については、「[A closer look at MSIX](/archive/blogs/sgern/a-closer-look-at-msix)」(MSIX を詳しく調べる) をご覧ください。  

- 新しい MSIX アプリを作成する方法については、「[MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376)」(Insider ビルド 17682 で導入された MSIX のサポート) をご覧ください。  

### <a name="convert-applications-to-msix"></a>アプリケーションを MSIX に変換する
<!--3607729, fka 1359029-->

既存の Windows インストーラー (.msi) アプリケーションを MSIX 形式に変換します。

#### <a name="prerequisites-for-msix"></a>MSIX の前提条件

- Windows 10 バージョン 1809 以降を実行している参照デバイス  

- ローカル管理者権限を持つユーザーとしてこのデバイスの Windows にサインインします  

- 次のアプリをこのデバイスにアンインストールします  

  - Configuration Manager コンソール  

  - Microsoft Store から [MSIX Packaging Tool](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) をインストールします  

  - [MSIX Packaging Tool ドライバー](/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)をインストールします<!--SCCMDocs-pr issue #3091-->  

このデバイスには、他のアプリやサービスをインストールしないでください。 これは参照システムです。

#### <a name="process-to-convert-applications-to-msix-format"></a>アプリケーションを MSIX 形式に変換するプロセス

1. 管理者特権で Configuration Manager コンソールにアクセスし、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** ノードを選択します。  

2. 展開の種類が Windows インストーラー (.msi) であるアプリケーションを選択します。  

    > [!Note]  
    > 参照デバイスからアプリケーションのソース コンテンツにアクセスできる必要があります。  
    >
    > アプリケーションの名前に特殊文字が含まれていてはなりません。 Configuration Manager では、出力ファイルの名前としてアプリ名が使用されます。  
    >
    > このアプリケーションを参照デバイスに事前にインストールしないでください。  

3. リボンの **[Convert to .MSIX]\(.MSIX に変換\)** を選択します。

ウィザードが完了すると、MSIX Packaging Tool によって、ウィザードで指定した場所に MSIX ファイルが作成されます。 このプロセスの間に、Configuration Manager によって参照デバイスにアプリケーションがサイレント モードでインストールされます。

プロセスが失敗した場合、概要ページに詳細情報を含むログ ファイルが示されます。 ユーザー状態のキャプチャに関するエラーがある場合は、Windows からサインアウトします。 もう一度サインインすると、この問題が解決する可能性があります。

この MSIX アプリを使用するには、クライアントによって信頼されるように、最初にデジタル署名する必要があります。 このプロセスについて詳しくは、以下の記事をご覧ください。

- [MSIX – MSIX Packaging Tool – MSIX パッケージの署名](/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package)
- [SignTool を使用してアプリ パッケージに署名する方法](/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

アプリに署名した後、Configuration Manager でアプリケーションに新しい展開の種類を作成します。 詳細については、「[アプリケーションの展開の種類を作成する](../deploy-use/create-applications.md#bkmk_create-dt)」を参照してください。

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a> タスク シーケンスの展開の種類

<!--3555953-->

> [!Note]  
> このバージョンの Configuration Manager では、タスク シーケンスの展開の種類はプレリリース機能です。 これを有効にする場合は、「[プレリリース機能](../../core/servers/manage/pre-release-features.md)」を参照してください。  

バージョン 2002 以降では、アプリケーション モデルを介してタスク シーケンスを使用し、複雑なアプリケーションをインストールできます。 アプリのインストールまたはアンインストールのいずれかのために、タスク シーケンスの展開の種類をアプリに追加します。 この展開の種類によって、以下の動作を提供します。

<!-- - Deploy an app task sequence to a user collection -->

- ソフトウェア センターにアイコンでアプリ タスク シーケンスを表示する。 ユーザーは、このアイコンによってアプリ タスク シーケンスを見つけて識別しやすくなります。

- ローカライズされた情報を含むアプリ タスク シーケンスのメタデータを追加で定義する

アプリには、OS 展開のタスク シーケンスを除く展開の種類しか追加できません。 影響の大きいタスク シーケンス、OS 展開のタスク シーケンス、OS アップグレード タスク シーケンスはサポートされていません。 <!--A user-targeted deployment still runs in the user context of the local System account.-->

この展開の種類をアプリに追加するときには、 **[タスク シーケンス]** ページでプロパティを構成します。 詳細については、「[展開の種類の **[タスク シーケンス]** オプション](../deploy-use/create-applications.md#bkmk_dt-ts)」を参照してください。

バージョン 2006 以降では、次の Windows PowerShell コマンドレットを使用して、タスク シーケンスの展開の種類を追加および構成してください。

- [Add-CMTaskSequenceDeploymentType](/powershell/module/configurationmanager/add-cmtasksequencedeploymenttype?view=sccm-ps)
- [Set-CMTaskSequenceDeploymentType](/powershell/module/configurationmanager/set-cmtasksequencedeploymenttype?view=sccm-ps)

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>タスク シーケンスの展開の種類に関する前提条件

カスタム タスク シーケンスの作成:

- OS 展開の手順を除くもののみを使用します。たとえば、**パッケージのインストール**、**コマンド ラインの実行**、**PowerShell スクリプトの実行**です。 サポートされているすべての手順を含む詳細については、「[OS 以外の展開用タスク シーケンスの作成](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)」を参照してください。

- タスク シーケンスのプロパティの **[ユーザー通知]** タブでは、影響の大きいタスク シーケンスのオプションは選択しないでください。

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

アプリケーションを作成するときに、タスク シーケンスの展開の種類を追加するには、ユーザー アカウントに、タスク シーケンスを読み取るためのアクセス許可が必要です。<!-- 6348976 --> 次のいずれかのオプションを使用して、これらのアクセス許可を構成します。

- アプリ管理者のユーザー アカウントを、組み込みの **読み取り専用アナリスト** ロールに追加します。 このロールで、すべての Configuration Manager オブジェクトを表示できます。

- 組み込みの **アプリケーション管理者** ロールをコピーしてカスタム ロールを作成します。 **タスク シーケンス パッケージ** オブジェクトに対する**読み取り**アクセス許可を追加します。

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>タスク シーケンスの展開の種類に関する既知の問題

- ユーザー コレクションにアプリ タスク シーケンスを展開することは、まだできません

- このタスク シーケンスで**アプリケーションのインストール** ステップを使用しないでください。 アプリをインストールするには、[パッケージのインストール](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) ステップを使用します。

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a> ユニバーサル Windows プラットフォーム (UWP) アプリのサポート  

Windows 10 デバイスで基幹業務アプリをインストールする場合、サイドローディング キーは不要です。 ただし、Windows でサイドローディングを有効にするには、レジストリ キー `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` の値を **1** にする必要があります。  

このレジストリ キーを構成しないと、アプリをデバイスに初めて展開するときに、Configuration Manager によってこの値が自動的に **1** に設定されます。 この値を **0** に設定した場合、Configuration Manager は値を自動的に変更できず、基幹業務アプリの展開は失敗します。  

UWP 基幹業務アプリにデジタル署名します。 アプリを展開する各デバイスで信頼されているコード署名証明書を使用します。 ユーザーの組織の PKI の証明書を使用するか、または Windows によってパブリック ルート証明書が既に信頼されているサード パーティ プロバイダーから証明書を購入します。  

モバイル アプリ パッケージに署名するには、次の表を参考にして、使用するコード署名証明書の種類を決定します。

| パッケージ  | Symantec  | Symantec 以外  |
|---------|---------|---------|
| Windows 10 Mobile デバイス上のユニバーサル **.appx** パッケージ | はい | はい |
| **.xap** パッケージ | はい | いいえ |
| Windows 10 Mobile デバイスにインストールするために Windows Phone 8.1 用にビルドされた **.appx** パッケージ | はい | いいえ |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a> MDM 登録済みの Windows 10 デバイスに Windows インストーラー アプリを展開する  

**MDM を介した Windows インストーラー (\*.msi)** の展開種類では、Windows インストーラー ベースのアプリを作成して、Windows 10 を実行する MDM 登録済みデバイスに展開できます。  

この展開の種類を使用するときは、次の点を考慮してください。

- 拡張子が MSI のファイルを 1 つだけアップロードします。  

- Configuration Manager では、アプリの検出にファイルの製品コードと製品バージョンが使われます。  

- Windows では、アプリの既定の再起動動作が使われます。 Configuration Manager では、アプリの再起動動作は制御されません。  

- ユーザー単位の MSI パッケージは単一のユーザーにインストールされます。  

- コンピューター単位の MSI パッケージはデバイスのすべてのユーザーにインストールされます。  

- Configuration Manager ではアプリの更新プログラムがサポートされます。 各バージョンの MSI 製品コードは同じである必要があります。