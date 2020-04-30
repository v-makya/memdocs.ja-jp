---
title: Technical Preview 1707
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1707 で使用できる機能について説明します。
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ddae3e4c4cf31cb05376bfa437d722f16652fad
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705140"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Configuration Manager の Technical Preview 1707 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1707 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**この Technical Preview の既知の問題:**
- **サイト サーバーがパッシブ モードの場合、プレビュー バージョン 1707 への更新に失敗します**。 プレビュー バージョン 1706 を実行し、[プライマリ サイト サーバーがパッシブ モード](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)の場合、プレビュー サイトをバージョン 1707 に正常に更新するには、パッシブ モードのサイト サーバーをアンインストールする必要があります。 パッシブ モードのサイト サーバーは、サイトでバージョン 1707 が実行された後に再インストールできます。

  パッシブ モードのサイト サーバーをアンインストールするには、次の手順を実行します。
  1. コンソールで **[管理]**  >  **[概要]**  >  **[サイトの構成]**  >  **[サーバーとサイト システムの役割]** の順に移動し、パッシブ モードのサイト サーバーを選択します。
  2. **[サイト システムの役割]** ウィンドウで、 **[サイト サーバー]** の役割を右クリックし、 **[役割の削除]** を選択します。
  3. パッシブ モードのサイト サーバーを右クリックし、 **[削除]** を選択します。
  4. サイト サーバーのアンインストール後に、アクティブなプライマリ サイト サーバーで **CONFIGURATION_MANAGER_UPDATE** のサービスを再起動します。



**このバージョンでお試しいただける新機能を次に示します。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>クライアント ピア キャッシュで、Windows 10 と Office 365 の高速インストール ファイルに対応
<!-- 1352486 -->
今回のリリースから、ピア キャッシュで、Windows 10 のコンテンツ高速インストール ファイルと Office 365 の更新ファイルを配信できるようになりました。 追加の構成は必要ありません。

## <a name="surface-device-dashboard"></a>Surface デバイス ダッシュボード
<!--1355788-->
Surface デバイス ダッシュボードに、お使いの環境で検出された Surface デバイスに関する情報が表示されます。 コンソールでは、 **[監視]**  >  **[Surface Devices]\(Surface デバイス\)** の順に進みます。 次を表示できます。
- Surface の割合
- Surface モデルの割合
- 上位 5 つのオペレーティング システム バージョン

**Surface モデル** グラフのセクションをクリックすると、デバイスの完全一覧が表示されます。  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Windows Defender Application Guard ポリシーの構成と展開
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) は、信頼できない Web サイトをオペレーティング システムの他の部分からはアクセスできない安全な分離コンテナーで開くことでユーザーを保護する Windows の新機能です。 この Technical Preview では、設定する Configuration Manager のコンプライアンス設定を使用して、この機能を構成し、コレクションに展開するためのサポートが追加されました。 この機能は、Windows 10 Fall Creator's Update (コードネーム: RS3) の 64 ビット バージョンのプレビューでリリースされます。 この機能を今すぐテストするには、この更新プログラムのプレビュー バージョンを使用している必要があります。

### <a name="before-you-start"></a>開始する前に

Windows Defender Application Guard ポリシーを作成して展開するには、ネットワーク分離ポリシーを使用して、ポリシーを展開する Windows 10 デバイスを構成する必要があります。 詳しくは、[このブログ投稿](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)をご覧ください。 この機能は、最新の Windows 10 Insider Build でのみ動作します。 これをテストするには、クライアントが最新の Windows 10 Insider Build で実行されている必要があります。

### <a name="try-it-out"></a>試してみましょう。

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>ポリシーを作成し、使用可能な設定を参照するには、次の手順を実行します。

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** を選択します。
2. **[資産とコンプライアンス]** ワークスペースで、 **[概要]**  >  **[Endpoint Protection]**  >  **[Windows Defender Application Guard]** の順に選択します。
3. **[ホーム]** タブの **[作成]** グループで、 **[Windows Defender Application Guard ポリシーの作成]** をクリックします。
4. ブログ記事を参照として使用して、使用可能な設定を参照および構成して、機能を試すことができます。
5. 今回のリリースでは、ウィザードに新しく **[ネットワーク定義]** ページを追加しました。 このページでは、企業の ID を指定し、企業ネットワークの境界を定義します。<br>Windows 10 PC の場合、クライアントでネットワーク分離リストが 1 つだけ保存されます。 今回のリリースでは、2 種類のネットワーク分離リスト (Windows 情報保護のリストと Windows Defender Application Guard のリスト) を作成し、クライアントに展開できます。 両方のポリシーを展開する場合、ネットワーク分離リストが一致している必要があります。 一致しないリストを同じクライアントに展開すると失敗します。
ネットワーク定義の指定方法については、[Windows 情報保護のドキュメント](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)を参照してください。

6. 完了したら、ウィザードを終了し、1 つ以上の Windows 10 デバイスにポリシーを展開します。

### <a name="further-reading"></a>参考資料
Windows Defender Application Guard の詳細については、[このブログ記事](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)を参照してください。 また、Windows Defender Application Guard のスタンドアロン モードの詳細については、[このブログ記事](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)を参照してください。

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Configuration Manager から PowerShell スクリプトを展開するときにパラメーターを追加する

<!-- 1236459 --->

前回の Technical Preview では、[Configuration Manager コンソールから PowerShell スクリプトを作成し、実行](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)できる新しい機能を導入しました。
今回の Technical Preview では、この機能をさらに拡張しています。 Configuration Manager で PowerShell スクリプトを読み込み、スクリプトの作成ウィザードであらゆるパラメーターを表示するようになりました。 スクリプトの実行時に使用されるパラメーター値をウィザードで指定できます。 あるいは、パラメーターは空のまま残すことができます。 その場合、スクリプトの実行時にパラメーター値を指定する必要があります。
今回の Technical Preview では、スクリプトで必要なパラメーターを指定する必要があります。 今後のリリースでは、スクリプト パラメーターの指定は省略可能になる予定です。

### <a name="try-it-out"></a>試してみましょう。

1. 指示に従い、[Configuration Manager コンソールから PowerShell スクリプトを作成し、実行](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)してください。
2. **スクリプトの作成ウィザード**の新しい **[スクリプト パラメーター]** ページで、パラメーターを選択し、 **[編集]** をクリックします。
3. 選択したパラメーターのパラメーター値を指定し、 **[OK]** をクリックします。
4. ウィザードを完了します。

スクリプトを実行すると、設定したパラメーター値があればそれが使用されます。
