---
title: バージョン 2006 の新機能
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch のバージョン 2006 で導入された変更点および新機能について説明します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f624a207b5e9afded9b86312d1608a35005355f6
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179343"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch のバージョン 2006 の新機能

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 2006 はコンソール内の更新プログラムとして利用できます。 バージョン 1810 以降が実行されているサイトで、この更新プログラムを適用します。 <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->この記事では、Configuration Manager バージョン 2006 での変更点と新機能をまとめます。

この更新プログラムをインストールするための最新のチェックリストを常に確認してください。 詳細については「[更新プログラム 2006 をインストールするためのチェックリスト](../../servers/manage/checklist-for-installing-update-2006.md)」を参照してください。 サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist)に関するページも確認してください。

Configuration Manager の新機能をすべて利用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

<!-- commenting this for now as it doesn't work 7422960
> [!TIP]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`
 -->

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a>Microsoft Endpoint Manager テナントのアタッチ

### <a name="install-applications-from-the-admin-center"></a>管理センターからアプリケーションをインストールする
<!--7518897, 6024389-->
Microsoft エンドポイント マネージャーの管理センターから、テナントに接続されたデバイスへのアプリケーションのインストールを、リアルタイムで開始できます。 Configuration Manager バージョン 2006 以降では、デバイスで使用できるアプリケーションの一覧に、デバイスの現在ログオンしているユーザーに展開されたアプリケーションも含まれます。 詳細については、「[テナントのアタッチ:管理センターからアプリケーションをインストールする](../../../tenant-attach/applications.md)」。  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a> テナント接続のオンボード中に以前に作成した Azure AD アプリケーションをインポートする
<!--6479246-->
新しいオンボードの際、管理者は、テナント接続へのオンボード中に以前に作成したアプリケーションを指定できます。 詳細については、「[Microsoft Endpoint Manager テナントのアタッチ: デバイスの同期とデバイスのアクション](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app)」を参照してください。

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> エンドポイント分析

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>既定で有効になっているエンドポイント分析データの収集
<!--7065447, 7741111-->
**[Enable Endpoint analytics data collection]\(エンドポイント分析データの収集を有効にする\)** クライアント設定が既定で有効化されるようになりました。 この設定により、マネージド エンドポイントで、スタートアップ パフォーマンスの分析情報などのデータを Configuration Manager サイト サーバーに送信できるようになります。 この変更は、ローカル データの収集のみに影響します。 エンドポイント分析データは、[Configuration Manager でデータ アップロードを有効化](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload)しないと、Microsoft Endpoint Manager 管理センターにアップロードされません。 新しい既定値は、既定のクライアント設定と、バージョン 2006 へのアップグレード後に作成されたカスタム クライアント設定に適用されます。

- バージョン 2002 からバージョン 2006 にアップグレードする場合、既存のカスタム クライアント設定値が保持されます。 Configuration Manager バージョン 2002 では、 **[Enable Endpoint analytics data collection]\(エンドポイント分析データの収集を有効にする\)** の既定値は **[いいえ]** です。
- Configuration Manager バージョン 1910 以前からバージョン 2006 にアップグレードする場合、設定のグループ **[コンピューター エージェント]** を含む既存のカスタム クライアント設定では、 **[Enable Endpoint analytics data collection]\(エンドポイント分析データの収集を有効にする\)** の新しい既定値 **[はい]** が継承されます。

詳しくは、[Configuration Manager でのエンドポイント分析データ収集の有効化](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload)に関する記事をご覧ください。

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> サイトのインフラストラクチャ

### <a name="vpn-boundary-type"></a> VPN 境界の種類

<!--7020519-->

リモート クライアントの管理を簡略化するため、VPN の新しい境界の種類を作成できるようになりました。 これまでは、VPN クライアントの境界を、IP アドレスかサブネットに基づいて作成する必要がありました。 この構成は、サブネット構成や VPN の設計が原因で、困難な場合や不可能な場合がありました。

今回、クライアントが場所の要求を送信すると、そのネットワーク構成に関する追加情報が含まれるようになりました。 この情報に基づいて、サーバーはクライアントが VPN 上にあるかどうかを判断します。

詳細については、[境界の定義](../../servers/deploy/configure/boundaries.md)に関する記事を参照してください。

### <a name="management-insights-to-optimize-for-remote-workers"></a>リモート ワーカーに合わせた最適化を行うための管理分析情報

<!--6982226-->

このリリースでは、管理分析情報の新しいグループ、**リモート ワーカーに合わせた最適化**が追加されています。 これらの分析情報は、リモート ワーカー向けにより良いエクスペリエンスを作成し、インフラストラクチャの負荷を軽減するのに役立ちます。 このリリースの分析情報では、主に VPN に焦点が当てられています。

- **VPN 境界グループの定義**
- **クラウド ベースのコンテンツ ソースを優先するように VPN に接続されたクライアントを構成する**
- **VPN 接続されたクライアントのピア ツー ピアのコンテンツ共有を無効にする**

詳細については、[管理分析情報](../../servers/manage/management-insights.md)に関するページを参照してください。

### <a name="improved-support-for-windows-virtual-desktop"></a> Windows Virtual Desktop のサポートの改善

<!--6527576-->

**Windows 10 Enterprise マルチセッション** プラットフォームが、要件の規則や適用性の一覧があるオブジェクトでサポートされている OS バージョンの一覧に表示されます。

Configuration Manager による Windows Virtual Desktop のサポートの詳細については、[クライアントとデバイスに対してサポートされる OS のバージョン](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)に関する記事をご覧ください。

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>イントラネット クライアントで CMG ソフトウェアの更新ポイントを使用できる
<!--7102873-->
イントラネット クライアントは、境界グループに割り当てられたときに、CMG ソフトウェアの更新ポイントにアクセスできるようになりました。 詳細については、[境界グループの構成](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup)に関するページを参照してください。

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> クラウド接続の管理

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>Microsoft Azure China 21Vianet を使用した共同管理
<!--7133238-->
共同管理を有効にするときに、Azure の環境として Azure China Cloud を選択できるようになりました。 詳細については、「[How to enable co-management](../../../comanage/how-to-enable.md)」 (共同管理を有効にする方法) を参照してください。

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Azure AD アプリの秘密鍵の有効期限切れ通知

<!--6386392-->

お使いのサイトをクラウドに接続するように Azure サービスを構成すると、Configuration Manager コンソールに次の状況で通知が表示されるようになりました。

- 1 つ以上の Azure AD アプリの秘密鍵の有効期限が間もなく切れる
- 1 つ以上の Azure AD アプリの秘密鍵が期限切れになっている

詳細については、[秘密鍵の更新](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew)に関するページを参照してください。

### <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics クラウド サービスの毎月の変更については、「[Desktop Analytics の新機能](../../../desktop-analytics/whats-new.md)」を参照してください。

#### <a name="change-to-diagnostic-data-labels"></a>診断データ ラベルへの変更

<!-- 7363467 -->

Windows 診断データのデスクトップ分析要件に合わせるために、これらの設定に新しいラベルが用意されました。

| バージョン 2006 以降 | バージョン 2002 以前 |
|---------|---------|
| 必須 | Basic |
| 省略可能 (制限あり) | 拡張 (制限あり) |
| 該当なし | 拡張 |
| Optional | [完全] |

以前に**拡張**レベルでデバイスを構成したことがある場合、バージョン 2006 にアップグレードすると、それらは**省略可能 (制限あり)** に戻ります。 その後、Microsoft に送信されるデータが少なくなります。 この変更は、Desktop Analytics に表示される内容には影響しません。

詳細については、「[Desktop Analytics のためにデータ共有を有効にする](../../../desktop-analytics/enable-data-sharing.md)」を参照してください。

## <a name="real-time-management"></a><a name="bkmk_real"></a> リアルタイムの管理

### <a name="improvements-to-cmpivot"></a>CMPivot の改善
<!--6518631-->
CMPivot に加えられた改良点は次のとおりです。

- コンソールおよび CMPivot スタンドアロンの CMPivot が統合されました。
- 個々のデバイスまたは複数のデバイスから CMPivot を実行する際、コレクションを選択または作成する必要がなくなりました。
- CMPivot クエリの結果から、個々のデバイスまたは複数のデバイスを選択し、指定された範囲で個別に CMPivot インスタンスを起動できるようになりました。

詳細については、「[バージョン 2006 以降の CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_2006)」を参照してください。

## <a name="client-management"></a><a name="bkmk_client"></a> クライアント管理

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a> 従量制課金接続でのクライアントのインストールとアップグレード

<!--6976145-->

これまでは、デバイスが従量制課金接続に接続されていた場合、新しいクライアントはインストールされませんでした。 すべてのクライアント通信を許可している場合、既存のクライアントのみがアップグレードされました。 従量制課金ネットワークで頻繁にローミングされるデバイスは、管理されていないことやクライアント バージョンが古いことがありました。 このリリース以降、クライアントのインストールとアップグレードは、クライアント設定 **[従量制ネットワーク接続でのクライアントの通信方法]** を **[許可]** または **[Limit]\(制限\)** に設定した場合に機能します。 この設定により、クライアントを最新の状態に維持しながら、従量制課金ネットワークでクライアントの通信を管理できます。

新しいクライアント インストールの動作を定義するため、新しい ccmsetup パラメーター **/AllowMetered** が用意されました。 従量制課金ネットワークでのクライアント通信を ccmsetup に許可すると、コンテンツのダウンロード、サイトへの登録、初期ポリシーのダウンロードが実行されます。 それ以降のクライアント通信は、そのポリシーのクライアント設定の構成に従います。

詳細については、以下の記事を参照してください。

- [クライアント設定について](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [クライアント インストール パラメーターとプロパティについて](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>デバイスの再起動の管理の改善

<!--3601213-->

Configuration Manager には、デバイスの再起動を管理したり、通知を再起動したりするための多くのオプションが用意されています。 デバイスの再起動が展開で要求されても自動的に実行されないように、クライアント設定を構成できるようになりました。 この設定により、固有の状況をより細かく制御できます。 既定では、クライアント設定 **[Configuration Manager can force a device to restart]\(Configuration Manager でデバイスの再起動を強制できる\)** が有効になっているため、Configuration Manager は強制的にデバイスを再起動できます。 この設定は、再起動が必要なアプリケーション、ソフトウェア更新プログラム、およびパッケージの展開にのみ適用されます。

詳細については、「[デバイス再起動の通知](../../clients/deploy/device-restart-notifications.md)」を参照してください。

## <a name="application-management"></a><a name="bkmk_app"></a> アプリケーション管理

### <a name="improvements-to-available-apps-via-cmg"></a>CMG を介した利用可能なアプリの改善

<!--6935376-->
このリリースでは、ソフトウェア センターと Azure Active Directory (Azure AD) 認証に関する問題が修正されました。 イントラネット上で検出されているものの、クラウド管理ゲートウェイ (CMG) を介して通信しているクライアントの場合、ソフトウェア センターではこれまで Windows 認証が使用されていました。 ユーザーの使用可能なアプリの一覧を取得しようとすると、失敗していました。 今後、Azure Active Directory に参加しているデバイスでは、Azure AD ID が使用されます。 これらのデバイスは、クラウド参加もハイブリッド参加も可能です。

詳細については、「[ユーザーが利用できるアプリを展開する](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)」を参照してください。

### <a name="microsoft-365-apps-for-enterprise"></a>Microsoft 365 Apps for enterprise
<!--6298093-->
Office 365 ProPlus は、2020 年 4 月 21 日に、Microsoft 365 Apps for enterprise に名前が変更されました。 バージョン 2006 以降、次のような変更が加えられました。

- 新しい名前を使用するため、Configuration Manager コンソールが更新されました。
  - この変更には、Microsoft 365 アプリの更新プログラム チャネル名も含まれます。
- バナー通知がコンソールに追加され、1 つ以上の自動展開規則により Microsoft 365 アプリの更新プログラムの**タイトル**条件で古いチャネル名が参照された場合、ユーザーに通知が表示されるようになりました。

詳細については、[Microsoft 365 Apps のチャネル名](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel)に関する記事と「[Microsoft 365 Apps の準備ダッシュボード](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash)」を参照してください。

## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS の展開

### <a name="task-sequence-media-support-for-cloud-based-content"></a> クラウドベース コンテンツに対するタスク シーケンス メディアのサポート

<!--6209223-->

タスク シーケンス メディアでクラウドベース コンテンツをダウンロードできるようになりました。 たとえば、デバイスを再イメージ化するために、リモート オフィスのユーザーに USB キーを送ることがあります。 または、ローカルの PXE サーバーがあるオフィスでも、デバイスでクラウド サービスの優先順位をできるだけ高くしたいことがあります。 今では、大規模な OS 展開コンテンツをダウンロードするために WAN にさらに負荷をかけるのではなく、ブート メディアや PXE 展開で、クラウドベースのソースからコンテンツを取得することができるようになりました。 たとえば、コンテンツの共有が可能なクラウド管理ゲートウェイ (CMG) などがあります。

> [!NOTE]
> デバイスには、管理ポイントへのイントラネット接続が引き続き必要になります。

詳細については、「[起動可能なメディアを使用したネットワーク経由での Windows の展開](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content)」を参照してください。

### <a name="improvements-to-task-sequences-via-cmg"></a> CMG を介したタスク シーケンスの改善

このリリースには、クラウド管理ゲートウェイ (CMG) を介して通信するデバイスにタスク シーケンスを展開するための、次の改善が含まれています。

- OS の展開のサポート<!--6997525-->:OS を展開するためにブート イメージを使用するタスク シーケンスの場合、CMG を介して通信するデバイスに展開することができます。 ユーザーは、ソフトウェア センターからタスク シーケンスを開始する必要があります。 詳細については、[CMG の計画に関するページの「仕様」](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications)を参照してください。

- このリリースでは、Configuration Manager Current Branch バージョン 2002 からの 2 つの[既知の問題](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg)が修正されました。<!-- 6983320 --> 次の状況で、CMG を介して通信するデバイス上でタスク シーケンスを実行できるようになりました。

  - [一括登録トークン](../../clients/deploy/deploy-clients-cmg-token.md)を使用して登録したワークグループ デバイス

  - [拡張 HTTP](../hierarchy/enhanced-http.md) 用にサイトを構成し、管理ポイントが HTTP に設定されている場合

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>BitLocker タスク シーケンス ステップの強化

<!--6995601-->

**BitLocker の有効化**および **BitLocker の事前プロビジョニング**のタスク シーケンス ステップで、ディスクの暗号化モードを指定できるようになりました。 既定で、これらのステップでは、OS バージョンの既定の暗号化方法が引き続き使用されます。

**BitLocker の有効化**のステップにも、 **[TPM がないか、TPM が有効ではない場合は、コンピューターでこの手順はスキップされます]** の設定が含まれるようになりました。 この設定を有効にすると、このステップでは TPM がないか初期化されていない TPM がないデバイスにエラーが記録され、タスク シーケンスが続行されます。 この設定により、BitLocker を完全にはサポートできないデバイスでも、タスク シーケンスの動作が管理しやすくなります。

詳しくは、「[タスク シーケンスのステップ](../../../osd/understand/task-sequence-steps.md)」をご覧ください。

### <a name="management-insight-rules-for-os-deployment"></a>OS 展開のマネジメント インサイト規則

<!--6982275-->

タスク シーケンスのポリシーのサイズが 32 MB を超えると、クライアントは大きなポリシーを処理できません。 その後、クライアントはタスク シーケンスの展開の実行に失敗します。 このリリースには、タスク シーケンスのポリシー サイズを管理するのに役立つ次の管理分析情報が含まれています。

- **タスク シーケンスが大きいと、最大ポリシー サイズを超える要因になる可能性がある**

- **タスク シーケンスのポリシーの合計サイズがポリシーの制限を超過している**

> [!TIP]
> これらの規則は **[オペレーティング システムの展開]** の新しいグループに含まれています。 **[未使用のブート イメージ]** の既存の規則も、このグループに含まれるようになりました。

詳細については、[管理分析情報](../../servers/manage/management-insights.md#operating-system-deployment)に関するページを参照してください。

### <a name="improvements-to-os-deployment"></a>OS 展開の機能強化

このリリースには、OS 展開に対する次の追加の機能強化が含まれています。

- タスク シーケンス変数を使用して、[[ディスクのフォーマットとパーティション作成]](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) ステップのターゲットを指定できます。 この新しい変数オプションでは、動的な動作を含むより複雑なタスク シーケンスがサポートされます。 たとえば、カスタム スクリプトでディスクを検出し、ハードウェアの種類に基づいて変数を設定することができます。 その後、このステップの複数のインスタンスを使用して、さまざまなハードウェアの種類とパーティションを構成できます。<!--6610288-->

- [準備の確認](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness)ステップに、デバイスが UEFI を使用しているかどうかを確認するためのチェックが含まれるようになりました。 また、新しい読み取り専用タスク シーケンス変数 **_TS_CRUEFI** も含まれています。<!--6452769-->

- [タスク シーケンスの進行状況のウィンドウ](../../../osd/understand/user-experience.md#task-sequence-progress)を有効にして、より詳細な進行状況の情報を表示した場合に、無効なグループの有効なステップがカウントされなくなりました。 この変更により、進行状況をより正確に見積もることができます。<!--6448412-->

- 以前は、デバイスを Windows 10 にアップグレードするタスク シーケンスの間、最終的な Windows 構成フェーズのいずれかで、コマンド プロンプト ウィンドウが開いていました。 このウィンドウは、Windows の out-of-box experience (OOBE) より手前に表示され、ユーザーはこれを操作してアップグレード プロセスを中断することができました。 今回、Configuration Manager の SetupCompleteTemplate.cmd および SetupRollbackTemplate.cmd スクリプトに、このコマンド プロンプト ウィンドウを非表示にするための変更が含まれています。<!--2837795-->

- 一部のお客様は **IProgressUI::ShowMessage** メソッドを使用してカスタム タスク シーケンス インターフェイスを構築しますが、これによってユーザーの応答の値は返されません。 このリリースでは [IProgressUI::ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md) メソッドが追加されています。 この新しいメソッドは既存のメソッドに似ていますが、新しい整数の結果変数 **pResult** も含まれています。<!--6448458-->

## <a name="protection"></a>保護

### <a name="cmg-support-for-endpoint-protection-policies"></a>CMG によるエンドポイント保護ポリシーのサポート

<!--4773948-->

クラウド管理ゲートウェイ (CMG) ではエンドポイント保護ポリシーがサポートされていますが、デバイスではオンプレミスのドメイン コントローラーにアクセスする必要がありました。 このリリース以降、CMG を介して通信するクライアントでは、Active Directory へのアクティブな接続なしで、すぐにエンドポイント保護ポリシーを適用できます。

詳細については、[Configuration Manager の機能の CMG サポート](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features)に関する記事をご覧ください。

### <a name="bitlocker-management-support-for-hierarchies"></a>階層用の BitLocker 管理サポート

<!-- 5925693 -->

中央管理サイトに BitLocker セルフサービス ポータルと管理と監視用 Web サイトをインストールできるようになりました。

詳細については、「[BitLocker ポータルのセットアップ](../../../protect/deploy-use/bitlocker/setup-websites.md)」を参照してください。

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager コンソール

### <a name="community-hub-and-github"></a>コミュニティ ハブと GitHub
<!--3555935, 3555936, deep link included 4224406-->

" *(2020 年 6 月に初めて導入)* "

IT 管理者のコミュニティには、長年にわたる豊富な知識が蓄積されています。 スクリプトやレポートなどの項目を最初から作り直す代わりに、私たちは、ユーザーが互いに共有できる Configuration Manager **コミュニティ ハブ**を構築しました。 他のユーザーの作業を活用することで、作業時間を節約できます。 コミュニティ ハブでは、他のユーザーの作業を基礎にし、他のユーザーはあなたの作業を基礎にすることで、創造力が促進されます。 GitHub には、既に共有のために作成された業界標準のプロセスとツールがあります。 そこで、コミュニティ ハブでは、この新しいコミュニティを推進するための基本要素として、これらのツールが Configuration Manager コンソールで直接活用されます。 最初のリリースでは、コミュニティ ハブで利用できるコンテンツは、Microsoft によってのみアップロードされます。 

詳細については、「[コミュニティ ハブと GitHub](../../servers/manage/community-hub.md)」をご覧ください。

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> コミュニティ ハブの項目への直接リンク
<!--4224406-->
直接リンクを使用して、Configuration Manager コンソールのコミュニティ ハブ ノードの項目に簡単に移動し、参照できます。 詳細については、「[コミュニティ ハブの項目への直接リンク](../../servers/manage/community-hub.md#bkmk_deeplink)」を参照してください。

### <a name="notifications-from-microsoft"></a>Microsoft からの通知
<!--3953121-->
Configuration Manager コンソールで Microsoft から通知を受け取ることができるようになりました。 これらの通知は、新機能または更新された機能、Configuration Manager および関連付けられているサービスに対する変更、修復するために操作が必要な問題に関する最新情報を入手するのに役立ちます。

詳しくは、「[Microsoft からメッセージを受信するようにサイトを構成する](../../servers/manage/admin-console-notifications.md#bkmk_msft)」を参照してください。

### <a name="power-bi-sample-reports"></a>Power BI サンプル レポート
<!--5679791-->

" *(2020 年 6 月に初めて導入)* "

Power BI Report Server を Configuration Manager のレポートと統合すると、サンプルの Power BI レポートを使用できるようになります。 次のサンプル レポートをダウンロードしてインストールします。

- ソフトウェア更新の対応状態
- ソフトウェア更新プログラムの展開ステータス

詳細については、「[Power BI サンプル レポートのインストール](../../servers/manage/powerbi-sample-reports.md)」を参照してください。

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> 非推奨のオペレーティング システム

[削除された項目と非推奨の項目](deprecated/removed-and-deprecated.md)で実装される前のサポートに関する変更点について説明します。

バージョン 1906 で最初に発表されたように、バージョン 2006 では次のクライアント OS バージョンのサポートが廃止されます。  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise

## <a name="other-updates"></a>その他の更新内容

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

Configuration Manager 向け Windows PowerShell コマンドレットの変更に関する詳細については、[PowerShell バージョン 2006 のリリース ノート](https://docs.microsoft.com/powershell/sccm/2006-release-notes?view=sccm-ps)を参照してください。

管理サービスの REST API の変更に関する詳細については、[管理サービスのリリース ノート](../../../develop/adminservice/release-notes.md#bkmk_2006)を参照してください。

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4556203).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>次のステップ

現時点では、バージョン 2006 は早期更新リングに対してリリースされます。 この更新プログラムをインストールするには、オプトインする必要があります。 詳しくは、「[早期更新リング](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring)」をご覧ください。

<!-- As of May 11, 2020, version 2006 is globally available for all customers to install. -->

このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラムのインストール](../../servers/manage/updates.md)に関する記事および「[2006 に更新するためのチェックリスト](../../servers/manage/checklist-for-installing-update-2006.md)」をご覧ください。

> [!TIP]
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用します。
>
> 詳細については、下記のリンクをクリックしてください。
>
> - [新しいサイトのインストール](../../servers/deploy/install/installing-sites.md)
> - [基準バージョンと更新プログラムのバージョン](../../servers/manage/updates.md#bkmk_Baselines)

既知の重大な問題については、[リリース ノート](../../servers/deploy/install/release-notes.md)を参照してください。

サイトを更新した後は、[更新後のチェックリスト](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist)に関するページも確認してください。
