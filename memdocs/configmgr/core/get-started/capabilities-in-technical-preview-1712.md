---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1712 で使用できる機能について説明します。
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705080"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Configuration Manager の Technical Preview 1712 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1712 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 

このバージョンの Technical Preview をインストールする前に、「[Configuration Manager の Technical Preview](technical-preview.md)」を確認してください。 この記事により、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法についての理解を深めることができます。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**この Technical Preview の既知の問題:**
- **サイト サーバーがパッシブ モードの場合、新しいプレビュー バージョンへの更新に失敗します**。 [プライマリ サイト サーバーがパッシブ モード](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)の場合は、この新しいプレビュー バージョンに更新する前にパッシブ モードのサイト サーバーをアンインストールする必要があります。 パッシブ モードのサイト サーバーは、サイトの更新を完了したあとに再インストールできます。

  パッシブ モードのサイト サーバーをアンインストールするには、次の手順を実行します。
  1. Configuration Manager コンソールで **[管理]**  >  **[概要]**  >  **[サイトの構成]**  >  **[サーバーとサイト システムの役割]** の順に移動し、パッシブ モードのサイト サーバーを選択します。
  2. **[サイト システムの役割]** ウィンドウで、 **[サイト サーバー]** の役割を右クリックし、 **[役割の削除]** を選択します。
  3. パッシブ モードのサイト サーバーを右クリックし、 **[削除]** を選択します。
  4. サイト サーバーのアンインストール後に、アクティブなプライマリ サイト サーバーで **CONFIGURATION_MANAGER_UPDATE** のサービスを再起動します。
  <!--sms489412-->


**このバージョンでお試しいただける新機能を次に示します。**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>置き換えられたアプリケーションを自動的にアップグレードしない
<!-- 1351266 -->
[皆さまからのフィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior)を基に、このリリースでは、置き換えられたアプリケーションを自動的にアップグレードしないようにアプリケーションの展開を構成することができます。 展開を作成する際に、**ソフトウェアの展開ウィザード**の **[展開設定]** ページで、**利用可能な**インストールまたは**必須**インストールのために、 **[このアプリケーションの置き換えられるバージョンを自動的にアップグレードする]** のオプションを有効または無効にできるようになりました。


## <a name="install-multiple-applications-in-software-center"></a>ソフトウェア センターで複数のアプリケーションをインストールする
<!-- 1357126 -->
エンド ユーザーまたはデスクトップ技術者がデバイスに複数のアプリケーションをインストールする必要がある場合、ソフトウェア センターで複数の選択されたアプリケーションのインストールがサポートされるようになりました。 1 つのインストールが完了するのを待ってから次のインストールを開始するのではないため、ユーザーの効率を上げることができます。

**[アプリケーション]** タブで複数選択モードを使用する場合は、次の条件で、ソフトウェア センターで複数選択できるアプリを判別します。
- アプリがユーザーに表示される
- アプリがまだインストールされていない
- 管理者の承認が必要ないか、既に付与されている
- アプリの状態が使用可能である (たとえば、まだコンテンツがダウンロードされていない)

### <a name="try-it-out"></a>試してみましょう。
**Configuration Manager コンソールで:** (利用可能または必須) インストール対象の複数のアプリケーションをユーザーまたはデバイスに展開します (期限は将来の日付)。 管理者の承認は必要ありません。 詳細については、「[アプリケーションの展開](../../apps/deploy-use/deploy-applications.md)」をご覧ください。

**ソフトウェア センターで次の操作を行います**。
 1. **[アプリケーション]** タブは既定で開きます。 
 2. リスト ビューで複数選択モードに入るには、右上隅にある新しいアイコン ![ソフトウェア センターの複数選択アイコン](media/software-center-multi-select-apps.png) をクリックします。
 3. リストのアプリの左側にあるチェック ボックスをオンにして、インストールする 2 つ以上のアプリを選択します。
 4. **[選択項目のインストール]** ボタンをクリックします。

これで、アプリは通常どおり、連続してインストールされます。


## <a name="client-based-pxe-responder-service"></a>クライアント ベースの PXE レスポンダー サービス
<!-- 1357148 -->
お客様の共通の課題は、サーバー インフラストラクチャがほとんど、またはまったくないリモート/ブランチ オフィスでの PXE サービスの提供です。 配布ポイントの役割ではクライアントのオペレーティング システムはサポートされますが、Windows 展開サービスへの依存関係により、PXE を有効にすることはできません。

新しいクライアント設定では、Configuration Manager クライアントで PXE レスポンダー サービスを有効にできるようになりました。 PXE 対応のブート イメージは、PXE レスポンダーのクライアント キャッシュになければなりません。

### <a name="try-it-out"></a>試してみましょう。
テスト環境に既存の PXE 対応配布ポイントまたはその他の PXE サーバーがないことを確認してください。ある場合は、このクライアントの PXE レスポンダーと競合する可能性があります。

Configuration Manager コンソールで、次の操作を行います。
1. **[ソフトウェア ライブラリ]** ワークスペースの **[オペレーティング システム]** 、 **[タスク シーケンス]** で: カスタム テンプレートを使用してタスク シーケンスを作成します。
   1. **[追加]** をクリックして、 **[全般]** を選択してから **[タスク シーケンス変数の設定]** ステップを選択します。 タスク シーケンス変数として「**SMSTSPersistContent**」と入力し、**TRUE** の値を入力します。
   1. **[追加]** をクリックして、 **[ソフトウェア]** を選択してから **[パッケージ コンテンツのダウンロード]** ステップを選択します。 金色のアスタリスクをクリックしてから、PXE 対応ブート イメージを選択します。 x86 と x64 の両方のブート イメージを含めます。 **Configuration Manager クライアント キャッシュ**に配置するようにステップを構成します。
   1. **[追加]** をクリックして、 **[全般]** を選択してから **[タスク シーケンス変数の設定]** ステップを選択します。 タスク シーケンス変数として「**SMSTSPreserveContent**」を入力し、**TRUE** の値を入力します。
2. **[管理]** ワークスペースの **[クライアント設定]** で: カスタム クライアント デバイス設定ポリシーを作成します。
   1. **[クライアント キャッシュ設定]** グループを選択します。
   1. **[完全な OS 上の Configuration Manager クライアントでコンテンツを共有できるようにする]** 設定を **[はい]** に設定します。
   1. **[PXE レスポンダー サービスを有効にする]** 設定を **[はい]** に設定します。
   1. **[自己署名入り証明書を作成するか、PKI クライアント証明書をインポートします]** 設定では、 **[証明書を提供]** をクリックします。 テスト環境に PKI がある場合は、 **[証明書のインポート]** を選択します。それ以外の場合は、 **[OK]** をクリックして自己署名証明書を作成します。 
   1. 必要に応じて、テスト環境用に残りの設定を構成します (特定のネットワークまたはセキュリティの要件がある場合を除き、既定の設定が動作します)。
3. PXE レスポンダーとなるターゲット クライアントのコレクションにタスク シーケンスとカスタム クライアント設定を展開します。 ポリシーが適用され、タスク シーケンスが実行されるまで待ちます。
4. 通常どおり、PXE/ネットワーク ブートに対して同じサブネットで別のクラスターを起動します。

### <a name="known-issues"></a>既知の問題
- ブート イメージを追加すると、タスク シーケンス エディターに **[パッケージ コンテンツのダウンロード]** ステップの赤いエラー アイコンが表示されますが、タスク シーケンスは正常に保存されます。 エディターでこのタスク シーケンスをもう一度開くと、参照されているオブジェクトが見つからないことを示す無害な警告も表示されます。 <!-- sms427542 -->
- [パッケージ コンテンツのダウンロード] ステップからのブート イメージは、カスタム タスク シーケンスの参照リストには表示されません。 また、 **[コンテンツの配布]** アクションは使用できません。 <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Configuration Manager クライアント インストールにおける変更  
皆さまからのフィードバックを反映し、[Silverlight がクライアントに自動でインストールされないようになりました。](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Surface デバイス ダッシュボードに対する変更
Surface ダッシュボードに、オペレーティング システムのバージョンではなく、Surface デバイスのファームウェア バージョンが表示されるようになりました。 コンソールでは、 **[監視]**  >  **[Surface Devices]\(Surface デバイス\)** の順に進みます。 次の項目を表示できます。
- Surface の割合
- Surface モデルの割合
- 上位 5 つのファームウェアのバージョン
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボードの機能拡張 
Office 365 クライアント管理ダッシュボードに、グラフ セクションが選択されたときに関連するデバイスのリストが表示されるようになりました。 コンソールで、 **[ソフトウェア ライブラリ]**  > **[概要]**  > **[Office 365 クライアント管理]** の順に移動します。 ダッシュボードは右側に表示されます。 グラフから条件を選択すると、デバイスのリストが表示されます。  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager コンソールの機能拡張 
Configuration Manager コンソールについて、皆さまからのフィードバックを基に、次のような機能拡張を行いました。

- [[デバイス] リストにプライマリ ユーザーが表示されます](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user):[資産とコンプライアンス]、[デバイス] の下の [デバイス] リストに既定でプライマリ ユーザーが表示されるようになりました。 最後にログオンしたユーザーを省略可能な列として追加することもできます。 <!-- 1357280 -->
- [名前変更されたコレクションが既存のコレクション メンバーシップ規則に表示されます](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections):コレクションが別のコレクションのメンバーである場合、その名前を変更すると、メンバーシップの規則に従って新しい名前が更新されます。<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>オペレーティング システムの展開に関する機能拡張
オペレーティング システムの展開について、次のような機能拡張を行いました。一部は皆さまからのフィードバックに基づくものです。
- [ブート イメージの既定のログ ビューアー](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a):Windows PE では、cmtrace.exe の起動時に、このプログラムをログ ファイルの既定のビューアーにするかどうかを選択するように求められることがなくなりました。 <!-- SMS 500897 -->
- パッケージ コンテンツのダウンロード ステップ:ブート イメージをこのタスク シーケンス ステップに追加できるようになりました。


## <a name="windows-10-feedback-hub-app-integration"></a>Windows 10 フィードバック Hub アプリの統合

皆さまからのフィードバックをお待ちしています。Windows 10 に組み込まれている[フィードバック Hub アプリ](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)を使用してフィードバックをお送りいただけるようになりました。 **新しいフィードバックを追加する**場合は、必ず、 **[エンタープライズ管理]** カテゴリを選択してから、以下のサブカテゴリのいずれかを選択してださい。
- Configuration Manager クライアント
- Configuration Manager コンソール
- Configuration Manager OS の展開
- Configuration Manager サーバー

Configuration Manager の新しい機能のアイデアについて投票する場合は、引き続き [User Voice ページ](https://configurationmanager.uservoice.com/)をご利用ください。


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[Configuration Manager の Technical Preview](technical-preview.md)」をご覧ください。    
