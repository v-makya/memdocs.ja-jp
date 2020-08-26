---
title: Application Guard ポリシーの管理
titleSuffix: Configuration Manager
description: Microsoft Defender Application Guard ポリシーを作成および展開する方法について説明します
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3fb7559f624afdb16ef228c61331387c163fbd54
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697111"
---
# <a name="create-and-deploy-microsoft-defender-application-guard-policy"></a>Microsoft Defender Application Guard ポリシーの作成と展開

*適用対象:Configuration Manager (Current Branch)*
<!-- 1351960 -->  
Configuration Manager エンドポイント保護を使用して [Microsoft Defender Application Guard (Application Guard)](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview) ポリシーを作成して展開できます。 これらのポリシーを使用すると、信頼できない Web サイトをオペレーティング システムの他の部分からはアクセスできない安全な分離コンテナーで開くことでユーザーを保護できます。

## <a name="prerequisites"></a>[前提条件]

Microsoft Defender Application Guard ポリシーを作成して展開するには、Windows 10 Fall Creator (1709) の更新プログラムを使用する必要があります。 ポリシーを展開する Windows 10 デバイスは、[ネットワーク分離ポリシー](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard#network-isolation-settings)を使用して構成する必要があります。 詳細については、「[Microsoft Defender Application Guard の概要](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)」を参照してください。

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>ポリシーを作成し、使用可能な設定を参照する

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** を選択します。
2. **[資産とコンプライアンス]** ワークスペースで、 **[概要]**  >  **[Endpoint Protection]**  >  **[Windows Defender Application Guard]** の順に選択します。
3. **[ホーム]** タブの **[作成]** グループで、 **[Windows Defender Application Guard ポリシーの作成]** をクリックします。
4. [記事](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard)を参照として使用して、使用可能な設定を参照および構成することができます。 Configuration Manager では、次のような特定のポリシー設定を設定できます。
   - [ホストの対話設定](#bkmk_HIS)
   - [アプリケーションの動作](#bkmk_ABS)
   - [ファイルの管理](#bkmk_FM)
5. **[ネットワーク定義]** ページでは、企業の ID を指定し、企業ネットワークの境界を定義します。

    > [!NOTE]
    > Windows 10 PC の場合、クライアントでネットワーク分離リストが 1 つだけ保存されます。 2 種類のネットワーク分離リストを作成し、次のクライアントに展開することができます。
    >
    >  - Windows 情報保護から 1 つ
    >  - Microsoft Defender Application Guard の 1 つ
    >
    > 両方のポリシーを展開する場合、ネットワーク分離リストが一致している必要があります。 一致しないリストを同じクライアントに展開すると失敗します。 詳細については、[Windows 情報保護のドキュメント](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)を参照してください。

6. 完了したら、ウィザードを終了し、1 つ以上の Windows 10 1709 デバイスにポリシーを展開します。

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a> ホスト対話の設定

ホスト デバイスと Application Guard コンテナー間の対話を構成します。 Configuration Manager バージョン 1802 より前のバージョンでは、アプリケーションの動作とホスト対話はどちらも **[設定]** タブにあります。

- **クリップボード** - Configuration Manager 1802 より前のバージョンでは [設定] の下
  - 許可されているコンテンツの種類
    - テキスト
    - 画像
- **印刷:**
  - XPS への印刷を有効にする
  - PDF への印刷を有効にする
  - ローカル プリンターへの印刷を有効にする
  - ネットワーク プリンターへの印刷を有効にする
- **グラフィックス:** (Configuration Manager バージョン 1802 以降)
  - 仮想グラフィックス プロセッサ アクセス
- **ファイル:** (Configuration Manager バージョン 1802 以降)
  - ダウンロードしたファイルをホストに保存する

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a> アプリケーションの動作の設定

Application Guard セッション内でアプリケーションの動作を構成します。 Configuration Manager バージョン 1802 より前のバージョンでは、アプリケーションの動作とホスト対話はどちらも **[設定]** タブにあります。

- **コンテンツ:**
  - エンタープライズ サイトはサード パーティ プラグインなどのエンタープライズ以外のコンテンツを読み込める
- **その他:**
  - ユーザーが生成したブラウザー データを保持する
  - 分離された Application Guard セッションでの監査セキュリティ イベント

### <a name="file-management"></a><a name="bkmk_FM"></a> ファイルの管理
<!--3555858-->
Configuration Manager バージョン 1906 以降には、通常は Application Guard で開くファイルをユーザーが信頼できるようにするポリシー設定があります。 正常に完了すると、Application Guard ではなく、ホスト デバイスでファイルが開きます。 Application Guard ポリシーの詳細については、「[Microsoft Defender Application Guard ポリシー設定の構成](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard)」を参照してください。

- **[Allow users to trust files that open in Windows Defender Application Guard] (Windows Defender Application Guard で開かれているファイルをユーザーが信頼できるようにする)** : ファイルを信頼できるものとすることをユーザーに許可します。 ファイルが信頼されている場合は、Application Guard ではなく、ホスト上で開かれます。 Windows 10 バージョン 1809 以降のクライアントに適用されます。
  - **[禁止]:** ファイルを信頼できる (既定) ものとすることをユーザーに許可しません。
  - **[File checked by antivirus]\(ウイルス対策で確認されたファイル\):** ウイルス対策チェック後、ファイルを信頼できるものとすることをユーザーに許可します。
  - **[すべてのファイル]:** あらゆるファイルを信頼できるものとすることをユーザーに許可します。

ファイル管理を有効にすると、クライアントの DCMReporting.log にエラーが記録される場合があります。 以下のエラーは、通常、機能に影響を与えません。 <!--4619457-->

- 互換性のあるデバイスで:
  - FileTrustCriteria_condition が見つかりません
- 互換性のないデバイスで:
  - FileTrustCriteria_condition が見つかりません
  - FileTrustCriteria_condition がマップで見つかりません
  - FileTrustCriteria_condition がダイジェストで見つかりません

Application Guard の設定を編集するには、 **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、 **[Windows Defender Application Guard]** ノードをクリックします。 編集するポリシーを右クリックし、 **[プロパティ]** を選択します。

## <a name="known-issues"></a>既知の問題

Windows 10 バージョン 2004 を実行しているデバイスでは、Microsoft Defender Application Guard のファイルの信頼基準に対するコンプライアンス レポートでエラーが発生します。 この問題が発生する原因は、Windows 10 バージョン 2004 の WMI クラス `MDM_WindowsDefenderApplicationGuard_Settings01` から一部のサブクラスが削除されたことです。 Microsoft Defender Application Guard のその他の設定はすべて適用されますが、ファイルの信頼基準のみ失敗します。 現在、このエラーを避けるための回避策はありません。 <!--7099444,5946790-->

## <a name="next-steps"></a>次のステップ

Microsoft Defender Application Guard の詳細については、以下を参照してください
 - [Microsoft Defender Application Guard の概要](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)。
- [Microsoft Defender Application Guard に関する FAQ](/windows/security/threat-protection/microsoft-defender-application-guard/faq-md-app-guard)。