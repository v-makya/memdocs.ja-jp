---
title: Windows Defender Application Control の管理方法
titleSuffix: Configuration Manager
description: Configuration Manager を使用して Windows Defender Application Control を管理する方法について説明します。
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0dcd519a7703b5de94f779dc5dbe48aa0d34a3bc
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700465"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>Configuration Manager を使用した Windows Defender Application Control の管理

*適用対象:Configuration Manager (Current Branch)*

## <a name="introduction"></a>概要
Windows Defender Application Control は、マルウェアおよびその他の信頼されていないソフトウェアから PC を保護するように設計されています。 承認されているコードのみを実行することで、悪意のあるコードの実行を防ぎます。

Windows Defender アプリケーション制御はソフトウェア ベースのセキュリティ層です。この層で、PC 上での実行を許可するソフトウェアの明示的一覧を強制します。 アプリケーション制御自体には、ハードウェアの前提条件もファームウェアの前提条件もありません。 アプリケーション制御ポリシーを Configuration Manager で展開すると、この記事で説明する Windows バージョンと SKU の最小要件を満たす対象コレクションの PC でポリシーが有効になります。 任意で、Configuration Manager で展開したアプリケーション制御ポリシーのハイパーバイザー ベースの保護を対応ハードウェア上でグループ ポリシーにより有効にできます。

Windows Defender Application Control の詳細については、「[Windows Defender Application Control 展開ガイド](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)」を参照してください。

   > [!NOTE]
   > - Windows 10 バージョン 1709 以降、構成可能なコードの整合性ポリシーは Windows Defender アプリケーション制御と呼ばれます。
   > - Configuration Manager バージョン 1710 以降では、Device Guard ポリシーが Windows Defender Application Control ポリシーに名前変更されました。

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>Configuration Manager での Windows Defender Application Control の使用

Configuration Manager を使用して Windows Defender アプリケーション制御ポリシーを展開できます。 このポリシーを使用すると、コレクション内の PC で Windows Defender Application Control を実行するモードを設定できます。 

次のモードのいずれかを構成できます。

1. **強制の有効化** - 信頼されている実行可能ファイルのみを実行できます。
2. **監査のみ** - すべての実行可能ファイルの実行を許可しますが、信頼されていない実行可能ファイルが実行された場合、ローカル クライアント イベント ログに記録します。

> [!Tip]  
> この機能はバージョン 1702 で[プレリリース機能](../../core/servers/manage/pre-release-features.md)として初めて導入されました。 バージョン 1906 からは、この機能はプレリリース機能ではなくなります。  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Windows Defender Application Control ポリシーを展開するときに実行できるもの

Windows Defender Application Control を使用すると、管理対象の PC で実行できる内容を厳密に制御できます。 この機能は、高いセキュリティが導入され、不要なソフトウェアの実行が許可されない部署の PC で役立ちます。

ポリシーを実行するときは、一般的に、次の実行可能ファイルを実行できます。

- Windows オペレーティング システムのコンポーネント
- ハードウェア デベロッパー センターのドライバー (Windows Hardware Quality Labs の署名あり)
- Windows ストア アプリ
- Configuration Manager クライアント 
- Windows Defender Application Control ポリシーの処理後に PC がインストールした Configuration Manager で展開されたすべてのソフトウェアが処理されます。 
- Windows コンポーネントの更新元:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager
    - 必要に応じて、Microsoft インテリジェント セキュリティ グラフ (ISG) から良い評価を得ているソフトウェア。 ISG には Windows Defender SmartScreen などの Microsoft サービスが含まれています。 デバイスでこのソフトウェアを信頼するためには Windows Defender SmartScreen および Windows 10 バージョン 1709 を実行している必要があります。

>[!IMPORTANT]
>前述のいずれかの更新メカニズムまたはインターネットからインストールされるかどうかに関係なく、インターネットやサードパーティのソフトウェア更新から自動的に更新する Windows に*組み込まれていない*ソフトウェアは上記に含まれていません。 Configuration Manager クライアントで展開されるソフトウェア変更のみを実行できます。

## <a name="before-you-start"></a>開始する前に

Windows Defender Application Control ポリシーを構成または展開する前に、次の情報をお読みください。

- Windows Defender Application Control の管理は、Configuration Manager のプレリリース機能であり、変更される可能性があります。
- Configuration Manager で Windows Defender Application Control を使用するには、管理対象の PC で Windows 10 Enterprise バージョン 1703 以降を実行している必要があります。
- ポリシーがクライアント PC で正常に処理されると、そのクライアント上で、Configuration Manager が管理されたインストーラーとして構成されます。 これを介して展開されるソフトウェアは、ポリシーの処理の後で、自動的に信頼されます。 Windows Defender アプリケーション制御ポリシーの処理前に Configuration Manager によりインストールされたソフトウェアが自動的に信頼されることはありません。
- 展開中に構成可能な、アプリケーション制御ポリシーの既定のコンプライアンスの評価スケジュールは 1 日ごとです。 ポリシー処理で問題が発生した場合、コンプライアンスの評価スケジュールを短く設定すると解消される可能性があります。たとえば、1 時間ごとに設定します。 このスケジュールは、エラーが発生したとき、クライアントが Windows Defender アプリケーション制御ポリシーの処理を再試行する頻度を示します。
- 選択した強制モードに関係なく、Windows Defender Application Control ポリシーを展開すると、クライアント PC は拡張子が .hta の HTML アプリケーションを実行できなくなります。

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Windows Defender Application Control ポリシーの作成方法
1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** をクリックします。
2. **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、 **[Windows Defender Application Control policies]\(Windows Defender アプリケーション制御ポリシー\)** をクリックします。
3. **[ホーム]** タブの **[作成]** グループで **[アプリケーション制御ポリシーの作成]** をクリックします。
4. **アプリケーション制御ポリシーの作成ウィザード**の **[全般]** ページで、次の設定を指定します。
    - **[名前]** - この Windows Defender Application Control ポリシーに一意の名前を入力します。 
    - **[説明]** - 必要に応じて、Configuration Manager コンソールで識別に役立ちそうなポリシーの説明を入力します。
    - **すべてのプロセスに対してこのポリシーを適用できるように、デバイスの再起動を強制する** - クライアント PC でポリシーが処理されたら、 **[コンピューターの再起動]** の **[クライアント設定]** に基づき、そのクライアントで再起動がスケジュールされます。
        - Windows 10 バージョン 1703 以前を実行しているデバイスは、必ず自動的に再起動します。
        - Windows 10 バージョン 1709 以降、デバイスで現在実行しているアプリケーションは、再試行しない限り新しいアプリケーション制御ポリシーが適用されません。 ただし、ポリシーの適用後に起動されるアプリケーションは、新しいアプリケーション制御ポリシーを優先します。 
    - **強制モード** - クライアント PC の Windows Defender Application Control に次の強制モードの 1 つを選択します。
        - **強制の有効化** - 信頼されている実行可能ファイルのみを実行できます。
        - **監査のみ** - すべての実行可能ファイルの実行を許可しますが、信頼されていない実行可能ファイルが実行された場合、ローカル クライアント イベント ログに記録します。
5. **アプリケーション制御ポリシーの作成ウィザード**の **[追加]** タブで、 **[インテリジェント セキュリティ グラフによって信頼されているソフトウェアを認証する]** を選択します。
6. PC 上の特定のファイルまたはフォルダーの信頼を追加する場合は、 **[追加]** をクリックします。 **[信頼できるファイルまたはフォルダーの追加]** ダイアログ ボックスで、信頼するローカル ファイルまたはフォルダー パスを指定できます。 また、接続するアクセス許可があるリモート デバイス上のファイルまたはフォルダー パスを指定することもできます。 Windows Defender アプリケーション制御ポリシー内で特定のファイルまたはフォルダーに信頼を追加すると、次の操作を実行できます。
    - 管理されたインストーラーの動作で問題を解決する
    - Configuration Manager で展開できない基幹業務アプリを信頼する
    - オペレーティング システムの展開イメージに含まれているアプリを信頼する 
8. **［次へ］** をクリックして、ウィザードを完了します。

>[!IMPORTANT]
>信頼するファイルやフォルダーの追加は、1706 以降のバージョンの Configuration Manager クライアントを実行するクライアント PC でのみサポートされます。 いずれかの追加ルールが Windows Defender Application Control ポリシーに含まれており、そのポリシーを、以前のバージョンの Configuration Manager クライアントを実行するクライアント PC に展開した場合、ポリシーは適用されません。 この問題は、これらの古いクライアントをアップグレードすると解決します。 追加ルールを含まないポリシーは、古いバージョンの Configuration Manager クライアントにも適用できます。

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Windows Defender Application Control ポリシーの展開方法
1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** をクリックします。
2. **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、 **[Windows Defender Application Control policies]\(Windows Defender アプリケーション制御ポリシー\)** をクリックします。
3. ポリシーの一覧から展開するポリシーを選択し、 **[ホーム]** タブの **[展開]** グループで **[アプリケーション制御ポリシーの展開]** をクリックします。
4. **[アプリケーション制御ポリシーの展開]** ダイアログ ボックスで、ポリシーを展開するコレクションを選択します。 次に、クライアントがポリシーを評価するときのスケジュールを構成します。 最後に、クライアントが構成されたメンテナンス期間外にポリシーを評価できるかどうかを選択します。
5. 完了したら、 **[OK]** をクリックしてポリシーを展開します。 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Windows Defender Application Control ポリシーの監視方法

「[System Center Configuration Manager でコンプライアンス設定を監視する](../../compliance/deploy-use/monitor-compliance-settings.md)」の記事の情報を使用して、展開したポリシーがすべての PC に正しく適用されていることを監視します。

Windows Defender Application Control ポリシーの処理を監視するには、クライアント PC の次のログ ファイルを使用します。

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

特定のソフトウェアのブロックや監査を検証するには、次のローカル クライアント イベント ログを確認します。

1. 実行可能ファイルをブロックまたは監査するには、 **[アプリケーションとサービス ログ]** 、 >  **[Microsoft]** 、 >  **[Windows]** 、 >  **[Code Integrity]** 、 >  **[Operational]** の順に選択します。
2. Windows インストーラーとスクリプト ファイルをブロックまたは監査するには、 **[アプリケーションとサービス ログ]** 、 >  **[Microsoft]** 、 >  **[Windows]** 、 >  **[AppLocker]** 、 >  **[MSI and Script]** の順に選択します。

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Windows Defender Application Control のセキュリティとプライバシー情報

- このプレリリース版では、運用環境の場合、Windows Defender Application Control ポリシーを **[監査のみ]** 強制モードで展開しないでください。 このモードは機能テストの対象をラボ設定のみとします。
- **[監査のみ]** モードまたは **[強制の有効化]** モードでポリシーを展開しているが、まだ再起動されておらず、ポリシーが適用されていないデバイスは無防備であり、信頼されていないソフトウェアがインストールされます。
そのような状況では、デバイスを再起動しても、 **[強制の有効化]** モードでポリシーを受け入れても、ソフトウェアが引き続き実行される可能性があります。
- Windows Defender Application Control ポリシーが有効であることを確認するには、ラボ環境でデバイスを準備します。 次に、 **[強制の有効化]** ポリシーを展開し、最後に、エンドユーザーにデバイスを配布する前にデバイスを再起動します。
- **[強制の有効化]** でポリシーを展開し、その後、 **[監査のみ]** で同じデバイスにポリシーを展開する行為はお止めください。 この構成により、信頼されていないソフトウェアが実行される可能性があります。
- Configuration Manager を利用し、クライアント PC 上の Windows Defender アプリケーション制御を有効にすると、ローカル管理者権限を持つユーザーがアプリケーション制御ポリシーを回避したり、その他の方法で信頼されていないソフトウェアを実行したりすることをポリシーは防げません。 
- ローカル管理者権限を持つユーザーがアプリケーション制御を無効にすることを防ぐ唯一の方法は、署名付きのバイナリ ポリシーを展開することです。 これはグループ ポリシーで可能ですが、現在のところ、Configuration Manager ではサポートされていません。
- クライアント PC に管理インストーラーとして Configuration Manager を設定するとき、AppLocker ポリシーが使用されます。 AppLocker は管理インストーラーの識別にのみ利用されます。すべての適用は Windows Defender アプリケーション制御で行われます。 

## <a name="next-steps"></a>次のステップ

 [マルウェア対策ポリシーとファイアウォール設定の管理](endpoint-antimalware-firewall.md)