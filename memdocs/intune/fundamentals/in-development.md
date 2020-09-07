---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: feb277f30401f31ddb400f5e3f6cd7709fa31c0b
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286239"
---
# <a name="in-development-for-microsoft-intune"></a>Microsoft Intune 用に開発中

お客様の準備と計画をサポートするため、このページでは、開発中でまだリリースされていない Intune UI の更新と機能が一覧表示されます。 このページの情報に加えて: 

- 変更前にお客様による対処が必要であると予測される場合は、Office メッセージ センターに補足の投稿が公開されます。
- 機能の運用が始まると、機能の説明はプレビュー版も一般公開版も、このページから[新機能](whats-new.md)に関するページに移行します。
- このページと[新機能](whats-new.md)に関するページは、定期的に更新されます。 適宜確認してください。
- 戦略的な成果物とタイムラインについては、「[Microsoft 365 のロードマップ](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS)」を参照してください。

> [!NOTE]
> このページには、今後のリリースでの Intune の機能に関する現在の予測が反映されています。 日付と個々の機能は変更される可能性があります。 このページは、開発中のすべての機能を説明しているわけではありません。

**RSS フィード**:ご自身のフィード リーダーに次の URL をコピーして貼り付けることで、このページが更新されたときにわかるようになります。`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**この記事は、上記のタイトルの下に示されている日付に最後に更新されました。**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>アプリ管理

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Android 上のポータル サイトおよび Intune アプリのデバイス アイコンを更新する<!-- 6057023  -->
Microsoft では、より新しい外観を作成し、Microsoft Fluent Design System に準拠するように、Android デバイス上のポータル サイトと Intune アプリのデバイス アイコンを更新しています。 関連する情報については、「[iOS または iPadOS および macOS 用のポータル サイト アプリのアイコンの更新](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-)」を参照してください。 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS ポータル サイトでは、ユーザー アフィニティなしでの Apple の自動デバイス登録がサポートされます<!-- 7282707  --> 
割り当てられたユーザーを必要とせずに Apple の自動デバイス登録を使用して登録されたデバイス上で、iOS ポータル サイトがサポートされます。 エンド ユーザーは、iOS ポータル サイトにサインインして、デバイス アフィニティなしで登録された iOS/iPadOS デバイス上で、自身をプライマリ ユーザーとして確立できます。 自動デバイス登録に関する詳細については、「[Apple の自動デバイス登録を使用して iOS または iPadOS デバイスを自動登録する](../enrollment/device-enrollment-program-enroll-ios.md)」を参照してください。


<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Android Enterprise フル マネージド デバイス (COBO) 用の PKCS 証明書プロファイルを作成する<!-- 4839686 -->
PKCS 証明書プロファイルを作成して、Android Enterprise デバイス所有者および仕事用プロファイルのデバイスに証明書を展開できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Android Enterprise] > [デバイスの所有者のみ]** 、または **[Android Enterprise] > [仕事用プロファイルのみ]** (プラットフォーム) > **[PKCS]** (プロファイル))。

間もなく、Android Enterprise フル マネージド デバイス用の PKCS 証明書プロファイルを作成できるようになります。 Intune の PFX 証明書コネクタが必要です。 SCEP を使用せず、PKCS のみを使用する場合は、新しい PFX コネクタをインストールした後で NDES コネクタを削除できます。 新しい PFX コネクタによって PFX ファイルがインポートされ、すべてのプラットフォームに PKCS 証明書が展開されます。

PKCS 証明書の詳細については、「[Intune で PKCS 証明書を構成して使用する](../protect/certficates-pfx-configure.md)」をご覧ください。

適用対象:
- Android Enterprise フル マネージド (COBO)

### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>iOS および macOS デバイスでのキー サイズが 4096 ビットの証明書のサポート<!-- 7659175   -->
Intune ではまもなく、SCEP 証明書プロファイルについて 4096 ビットのキー サイズの使用がサポートされるようになります ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  > "*プラットフォームを選択*" > "*プロファイル*" =  **[SCEP 証明書]** )。

4096 ビットのキーは、次のプラットフォームでサポートされます。 
- iOS 14 以降
- macOS 11 以降    

### <a name="new-setting-for-password-complexity-for-android-10-and-later---7992114----"></a>Android 10 以降のパスワードの複雑さに関する新しい設定<!-- 7992114  -->
Android 10 以降の新しいオプションをサポートするために、"*デバイスのコンプライアンス*" ポリシーと "*デバイスの制限*" ポリシーの両方に**パスワードの複雑さ**と呼ばれる新しい設定を追加しています ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[デバイスの制限]** および **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシーの作成]** ) この設定を使用すると、パスワードの種類、長さ、品質を考慮したパスワードの強度の測定を管理できます。 

次の複雑さレベルがサポートされます。
- **なし** - パスワードなし
- **低** - パスワードは、次のいずれかを満たします。
  - Pattern
  - 繰り返し (4444) または順序付け (1234、4321、2468) シーケンスを使用した PIN
- **中** - パスワードは、次のいずれかを満たします。
  - 繰り返し (4444) または順序付け (1234、4321、2468) シーケンスを使用せず、長さが 4 文字以上の PIN
  - アルファベット、長さが 4 文字以上
  - 英数字、長さが 4 文字以上
- **高** - パスワードは、次のいずれかを満たします。
  - 繰り返し (4444) または順序付け (1234、4321、2468) シーケンスを使用せず、長さが 8 文字以上の PIN
  - アルファベット、長さが 6 文字
  - 英数字、長さが 6 文字以上

パスワードの複雑さは、Android 10 以降を実行する Samsung Knox デバイスには適用されません。 これらのデバイスでは、パスワードの長さおよびパスワードの種類の設定によって、パスワードの複雑さがオーバーライドされます。

### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355---"></a>COPE プレビュー更新プログラム : 仕事用プロファイルを使用する Android Enterprise 企業所有デバイスに対して、仕事用プロファイルのパスワードに関する要件を作成するための新しい設定<!--7088355 -->
将来の設定により、管理者は、仕事用プロファイルを使用する Android Enterprise 企業所有デバイスに対して、仕事用プロファイルのパスワードに関する要件を設定できるようになります  ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Android Enterprise]** (プラットフォーム) > **[Fully Managed, Dedicated, and Corporate-Owned Work profile]\(フル マネージド、専用、会社所有の仕事用プロファイル\)**  >  **[デバイスの制限]** (プロファイル) > **[仕事用プロファイルのパスワード]** )。

- 必要なパスワードの種類
- パスワードの最小文字数
- パスワードの有効期限が切れるまでの日数
- ユーザーがあるパスワードを再使用できるようになるまでに必要なパスワード数
- デバイスがワイプされるまでのサインイン失敗回数


### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886----"></a>iOS または iPadOS および macOS デバイスでアプリごとの VPN またはオンデマンド VPN の使用に関する新しい設定<!-- 7758772 7758837 7758886  -->
- **ユーザーが自動 VPN を無効にするのを禁止する**: 自動の **アプリごとの VPN** または**オンデマンド VPN** 接続を作成する場合、ユーザーが自動 VPN を有効にしたまま実行し続けることを強制できます。
- **関連付けられたドメイン**: 自動の **アプリごとの VPN** 接続を作成する場合、VPN プロファイルで、VPN 接続を自動的に開始する、関連付けられたドメインを指定することができます。 
- **除外されるドメイン**: **アプリごとの VPN** 接続を作成する場合、アプリごとの VPN が接続されたときに VPN 接続をバイパスできるドメインの一覧を作成できます。

自動 VPN プロファイルは、 **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS/iPadOS]** または **[macOS]** (プラットフォーム) > **[VPN]** (プロファイル) > **[自動 VPN]** で構成できます。

関連付けられたドメインの詳細については、「[関連付けられたドメイン](../configuration/device-features-configure.md#associated-domains)」を参照してください。

構成可能な設定を確認するには、「[iOS/iPadOS デバイスに対するアプリごとの仮想プライベート ネットワーク (VPN) の設定](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile)」を参照してください。

適用対象:
- iOS/iPadOS 14 以降
- macOS Big Sur (macOS 11)

### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356----"></a>COPE プレビュー更新プログラム : 仕事用プロファイルを使用する Android Enterprise 会社所有デバイスの個人プロファイルを構成するための新しい設定<!-- 7086356  -->
仕事用プロファイルを使用する Android Enterprise 会社所有デバイスの場合、個人プロファイルにのみ適用される新しい設定を構成することができます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Android Enterprise]** (プラットフォーム) > **[Fully Managed, Dedicated, and Corporate-Owned Work profile]\(フル マネージド、専用、会社所有の仕事用プロファイル\)**  >  **[デバイスの制限]** (プロファイル) > **[個人プロファイル]** )。

- **[カメラ]** :個人的に使用しているときにカメラへのアクセスをブロックするには、この設定を使用します。
- **[画面キャプチャ]** :個人的に使用しているときに画面キャプチャをブロックするには、この設定を使用します。
- **Allow users to enable app installation from unknown sources in the personal profile \(ユーザーが個人プロファイルで不明なソースからのアプリのインストールを有効化するのを許可する\)** : ユーザーが個人プロファイルで不明のソースからアプリをインストールするのを許可するには、この設定を使用します。 

構成可能な現在の設定を確認するには、[機能を許可または制限するように Android エンタープライズ デバイスを設定する](../configuration/device-restrictions-android-for-work.md)方法に関するページを参照してください。

### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422----"></a>iOS および iPadOS での App Clips のブロック、macOS デバイスでの OS 以外のソフトウェア更新プログラムの延期<!-- 7518422  -->
iOS または iPadOS および macOS デバイスでデバイスの制限プロファイルを作成する場合、新しい設定がいくつかあります。

**iOS/iPadOS 14.0+ Block App Clips \(App Clips のブロック (iOS/iPadOS 14.0 以降)\)**
- iOS/iPadOS 14.0 以降に適用されます。
- デバイス登録またはデバイスの自動登録 (監視対象デバイス) にデバイスを登録する必要があります。
- **[App Clips のブロック]** 設定により、マネージド デバイスで App Clips がブロックされます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS/iPadOS]** (プラットフォーム) > **[デバイスの制限]** (プロファイル) > **[全般]** )。 ブロックされると、ユーザーは、App Clips を追加することも、既存の App Clips をデバイスから削除することもできません。  

**ソフトウェア更新プログラムの延期 (macOS 11 以降)**
- macOS 11 以降に適用されます。 監視対象 macOS デバイスで、デバイスは、ユーザーが承認したデバイス登録されているか、デバイスの自動登録によって登録されている必要があります。
- **[ソフトウェア更新プログラムの延期]** 設定により、OS 以外のソフトウェア更新プログラムのユーザーへの表示が延期されます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[macOS]** (プラットフォーム) > **[デバイスの制限]** (プロファイル) > **[全般]** )。 これらの更新プログラムを延期すると、延期期間が終了するまで、新しくリリースされた更新プログラムはユーザーに表示されません。延期期間は、 **[ソフトウェア更新プログラムの表示を遅らせる]** 設定を使用して構成します。 オペレーティング システム以外のソフトウェア更新プログラムを延期しても、スケジュールされた更新プログラムに影響しません。
- 既存の **[ソフトウェア更新プログラムの延期]** 設定をこの新しい設定と組み合わせます。 新しい設定を使用すると、OS のソフトウェア更新プログラムと OS 以外のソフトウェア更新プログラムを延期できます。 ソフトウェア更新プログラムを延期する日数を設定するには、引き続き **[ソフトウェア更新プログラムの表示を遅らせる]** 設定を使用します。これは両方の設定に適用されます。
- 既存のポリシーの動作は変更されず、影響を受けることも削除されることもありません。 既存のポリシーは、同じ構成で新しい設定に自動的に移行されます。

### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689----"></a>iOS および iPadOS デバイスで Wi-Fi ネットワークの MAC アドレスのランダム化を無効にする<!-- 7758689  -->
iOS/iPadOS 14 以降、既定では、物理 MAC アドレスの代わりにネットワークに接続する場合、デバイスにより、ランダム化された MAC アドレスが提示されます。 MAC アドレスでデバイスを追跡することは困難であるため、この動作はプライバシーのために推奨されます。 さらに、この機能は、ネットワーク アクセス制御 (NAC) などの静的 MAC アドレスに依存する機能を中断します。 

MAC アドレスのランダム化は、Wi-Fi プロファイルでネットワークごとに無効にすることができます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS/iPadOS]** (プラットフォーム) > **[Wi-Fi]** (プロファイル) > **[基本]** または **[エンタープライズ]** (Wi-Fi の種類))。

現在構成可能な設定を確認するには、[iOS および iPadOS デバイス向けの Wi-Fi 設定を追加する](../configuration/wi-fi-settings-ios.md)方法に関するページを参照してください。

適用対象:
- iOS/iPadOS 14 以降

### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>iOS および iPadOS デバイスで IKEv2 VPN 接続の最大伝送速度を設定する<!-- 7758937  -->
iOS/iPadOS 14 以降のデバイスでは、IKEv2 VPN 接続を使用する場合、カスタムの最大伝送速度 (MTU) を構成できます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS/iPadOS]** (プラットフォーム) > **[VPN]** (プロファイル) -> [IKEv2](接続の種類))。

構成可能な設定の詳細については、「[IKEv2 設定](../configuration/vpn-settings-ios.md#ikev2-settings)」を参照してください。

適用対象:
- iOS/iPadOS 14 以降

### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116----"></a>iOS および iPadOS デバイスでの電子メール プロファイル用のアカウントごとの VPN 接続<!-- 7759116  -->
iOS/iPadOS 14 以降、ユーザーが使用しているアカウントに基づいて、ネイティブ メール アプリの電子メール トラフィックを VPN 経由でルーティングできます。 このアカウントベースの VPN 接続に使用する、アプリごとの VPN プロファイルを指定できるようになりました。  ユーザーがメール アプリで組織のアカウントを使用する場合、アプリごとの VPN 接続は自動的に有効になります。

現在構成可能な設定を確認するには、[iOS および iPadOS デバイスの電子メール設定を追加する](../configuration/email-settings-ios.md)方法に関するページを参照してください。

適用対象:
- iOS/iPadOS 14 以降

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>仕事用プロファイルを使用する Android Enterprise デバイスに VPN 接続の種類として NetMotion を使用する<!-- 7764263 -->
VPN プロファイルを作成するときに、VPN 接続の種類として NetMotion を使用できます ( **[デバイス]**  >  **[デバイス構成]**  >  **[プロファイルの作成]**  >  **[Android Enterprise 仕事用プロファイル]** (プラットフォーム) **[VPN]** (プロファイル) > **[NetMotion]** (接続の種類))。

Intune での VPN プロファイルの詳細については、[VPN サーバーに接続するための VPN プロファイルの作成](../configuration/vpn-settings-configure.md)に関する記事をご覧ください。

適用対象:
- Android Enterprise 仕事用プロファイル

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>デバイスの制限プロファイルでのパスワード設定の変更 (Android デバイス管理者向け)<!-- 7662279  --> 
"*Android デバイス管理者*" 向けに、"*デバイスの制限*" および "*コンプライアンス*" ポリシーのパスワード設定にいくつかの変更を導入しています ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[デバイスの制限]** および **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシーの作成]** )。これらの変更は、Intune で、Android バージョン 10 以降の変更に対応して、パスワードの設定が引き続き想定どおりにデバイスに適用されることを確実にするのに役立ちます。
 
変更内容:
- **パスワード**の上位オプションの削除。  
- 設定は、適用されるデバイスに基づいてセクションに再編成されます。
- **[パスワードの種類]** が、パスワードの長さが適用される値に構成されない限り、 **[パスワードの最小文字数]** は使用できません。
- ラベルとサンプル テキストに対する追加の更新。

これらの変更は、設定の UI に適用され、既存のプロファイルには影響しません。 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>デバイスの登録

### <a name="ending-support-for-ios-11--7327321---"></a>iOS 11 のサポートの終了<!--7327321 -->
iOS 14 のリリース後、Intune の登録とポータル サイト アプリでは、iOS バージョン 12 以降がサポートされます。 以前のバージョンはサポートされませんが、ポリシーは引き続き受け取られます。

### <a name="ending-support-for-macos-1012--7327326---"></a>macOS 10.12 のサポートの終了<!--7327326 -->
macOS 11 のリリース後、Intune の登録とポータル サイト アプリでは、macOS バージョン 10.13 以降がサポートされます。 以前のバージョンはサポートされません。


<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics には、デバイスの詳細ログが含まれる<!--6014987  -->
Intune デバイスの詳細ログは、 **[レポート]**  >  **[ログ分析]** で入手できます。 デバイスの詳細を相互に関連付けて、カスタム クエリと Azure ブックを作成することができます。

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>テナントのアタッチ:管理センターのデバイス タイムライン<!--7220536, CM7141381 -->
Configuration Manager で、テナントのアタッチを使用してデバイスを Microsoft Endpoint Manager と同期すると、イベントのタイムラインを確認できるようになります。 このタイムラインにはそのデバイス上での過去の活動が表示され、問題のトラブルシューティングに役立ちます。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline) に関する記事をご覧ください。  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>テナントのアタッチ:管理センターからアプリケーションをインストールする<!-- 7220536, CM6024389 -->
Microsoft エンドポイント管理の管理センターからテナントに接続されたデバイスへのアプリケーションのインストールを、リアルタイムで開始できるようになります。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps) に関する記事をご覧ください。

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>テナントのアタッチ:管理センターからの CMPivot<!--7220536, CM6024392 -->
[CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) の機能を、Microsoft Endpoint Manager admin center に導入できるようになります。 Helpdesk などの追加のペルソナが、ConfigMgr マネージド デバイスそれぞれに対してクラウドからリアルタイムのクエリを開始して、結果を管理センターに返すことができるようになりました。 これにより、CMPivot の従来の利点すべてを利用して、IT 管理者やその他の指定されたペルソナが環境内のデバイスの状態をすばやく評価し、アクションを実行することが可能になります。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot) に関する記事をご覧ください。 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>テナントのアタッチ:管理センターからスクリプトを実行する<!--7220536, CM6234688 -->
Configuration Manager のオンプレミスの[スクリプト実行](../../configmgr/apps/deploy-use/create-deploy-scripts.md)機能を、Microsoft Endpoint Manager admin center に導入できるようになります。 Helpdesk などの追加のペルソナが、Configuration Manager マネージド デバイスそれぞれに対してクラウドから PowerShell スクリプトを実行できるようになります。 これにより、Configuration Manager 管理者によって既に定義され、承認されている PowerShell スクリプトの従来の利点すべてを、この新しい環境でも利用できるようになります。 詳細については、[Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts) に関する記事をご覧ください。 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>ソフトウェア更新プログラムを macOS デバイスに展開する <!-- 3194876 -->
macOS デバイスのグループにソフトウェア更新プログラムを展開できます。 この機能には、クリティカル、ファームウェア、構成ファイル、およびその他の更新プログラムが含まれます。 次のデバイス チェックイン時に更新プログラムを送信したり、週単位でのスケジュールを選択して設定した期間内または期間外に更新プログラムを展開したりできます。 これは、標準の勤務時間外にデバイスを更新する場合や、ヘルプ デスクのスタッフが常時配置されている場合に役立ちます。 また、更新プログラムが展開されるすべての macOS デバイスの詳細なレポートも取得します。 デバイスごとにレポートの詳細を表示して、特定の更新プログラムの状態を確認することができます。

### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228---"></a>COPE プレビュー更新プログラム : 仕事用プロファイルを使用する Android Enterprise 会社所有デバイスの仕事用プロファイルのパスワードをリセットする <!--7217228 -->
将来の管理者アクションでは、管理者は、仕事用プロファイルを使用する Android Enterprise 会社所有デバイスで仕事用プロファイルのパスワードをリセットできます。

### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043---"></a>Azure Active Directory に参加している共同管理デバイスの名前を変更する<!--7728043 -->
Azure AD に参加している共同管理デバイスの名前を変更できるようになります。 このためには、MEM に移動し、 **[デバイス]**  >  **[すべてのデバイス]** の順に選択し、デバイスを選択して、 **[...]**  >  **[デバイスの名前の変更]** の順に選択します。

### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987---"></a>Zebra デバイスの PowerPrecision および PowerPrecision+ Batteries のサポート<!--3724987 -->
デバイスの [ハードウェアの詳細] ページで、PowerPrecision および PowerPrecision+ batteries を使用する Zebra デバイスについて、次の情報を確認できるようになります。
- Zebra で決定された正常性状態の評価 (PowerPrecision+ batteries のみ)
- 使用された完全充電サイクルの数
- デバイスで最後に検出されたバッテリの最終チェックインの日付
- デバイスで最後に検出されたバッテリ パックのシリアル番号

<!-- ***********************************************-->
## <a name="intune-apps"></a>Intune アプリ

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Windows ポータル サイトでの Azure AD Enterprise と Office Online アプリケーションの統合配信<!-- 1817861  -->
2006 リリースでは、[ポータル サイトでの Azure AD Enterprise と Office Online アプリケーションの統合配信](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal)を発表しました。 この機能は、Windows ポータル サイトでサポートされています。 Intune の **[カスタマイズ]** ウィンドウで、**Azure AD Enterprise アプリケーション**と **Office Online アプリケーション**の両方を、Windows ポータル サイトで **[非表示]** または **[表示]** することを選択できます。 各エンド ユーザーには、選択された Microsoft サービスによるアプリケーション カタログ全体が表示されます。 既定では、追加のアプリ ソースがそれぞれ **[非表示]** に設定されるようになります。 この構成設定を見つけるには、[Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[テナント管理]**  >  **[カスタマイズ]** の順に選択します。 関連情報については、「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md)」を参照してください。
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI コンプライアンス レポート テンプレート V2.0<!-- 636958  -->
管理者は、Power BI コンプライアンス レポート テンプレートのバージョンを V1.0 から V2.0 に更新できるようになります。 V2.0 では、設計の改善が組み込まれ、テンプレートの一部として計算とデータが表示される改訂も行われます。 関連情報については、「[Power BI でデータ ウェアハウスに接続する](../developer/reports-proc-get-a-link-powerbi.md)」を参照してください。


### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Windows 10 以降用の新しいおよび改善された Microsoft Defender ウイルス対策レポート<!-- 6018169  -->
**[エンドポイント セキュリティ]**  >  **[ウイルス対策]** で、Windows 10 の Microsoft Defender ウイルス対策に 4 つの新しいレポートを追加しています。
- 2 つの運用レポート ("*マルウェアが検出されたデバイス*" および "*エージェントの状態*")。
- 2 つの組織レポート ("*検出されたマルウェア*" および "*エージェントの状態*")。

たとえば、運用レポートの "*エージェントの状態*" では、デバイス名、ユーザー名、ユーザーの電子メール、UPN と、リアルタイム保護およびネットワーク保護が有効であるかどうかが一見してわかるように表示されます。 これらのレポートが使用できるようになると、より多くの詳細が共有されます。

Intune でのエンドポイント セキュリティの詳細については、「[Microsoft Intune でエンドポイント セキュリティを管理する](../protect/endpoint-security.md)」を参照してください。

### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics-preview--7200950---"></a>グループ ポリシー分析 (プレビュー) を使用してオンプレミスの GPO を分析する<!--7200950 -->
**[デバイス]**  >  **[グループ ポリシー分析 (プレビュー)]** では、エンドポイント マネージャー管理センターでグループ ポリシー オブジェクト (GPO) をインポートできます。 インポートすると、Intune では、GPO を自動的に分析し、Intune に同等の設定があるポリシーを表示します。 また、非推奨の (サポートされなくなった) GPO も表示されます。

適用対象:
- Windows 10 以降

#### <a name="new-windows-10-feature-update-report---6473121-----"></a>新しい Windows 10 の機能更新プログラム レポート<!-- 6473121   -->
**機能更新プログラムのエラー** レポートでは、**Windows 10 の機能更新プログラム** ポリシーがあり、更新が試行されたターゲットのデバイスについてエラーの詳細が提供されます。 [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]**  >  **[監視]**  >  **[機能更新プログラムのエラー]** の順に選択して、このレポートを表示します。

#### <a name="new-windows-10-feature-update-report---6473128----"></a>新しい Windows 10 の機能更新プログラム レポート<!-- 6473128  -->
**Windows の機能更新プログラム** レポートでは、**Windows 10 機能更新** ポリシーがあるターゲットのデバイスについてコンプライアンスの全体的なビューが表示されます。 [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[レポート]**  >  **[Windows 10 の機能更新プログラム (プレビュー)]**  >  **[機能更新プログラムのエラー]** の順に選択して、このレポートのサマリを表示します。 特定のポリシーのレポートを表示するには、 **[レポート]** タブを選択し、**Windows の機能更新プログラム レポート**を開きます。 

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>セキュリティ

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Symantec Endpoint Security および Check Point Sandblast のアプリ保護ポリシーのサポート<!--  4452423, 4731168 -->

2019 年 10 月に、Intune アプリ保護ポリシーに、一部の Microsoft Threat Defense パートナー (MTD パートナー) のデータを利用する機能が追加されました。 Microsoft では以下のパートナーに対して、アプリ保護ポリシーを使用して、デバイスの正常性に基づいてユーザーの企業データをブロックしたり選択的にワイプしたりするためのサポートを追加しています。

- Android、iOS、および iPadOS 上での **Check Point Sandblast**
- Android、iOS、および iPadOS 上での **Symantec Endpoint Security**

MTD パートナーによるアプリ保護ポリシーの利用については、「[Intune で Mobile Threat Defense アプリ保護ポリシーを作成する](../protect/mtd-app-protection-policy.md)」を参照してください。

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP による脆弱性の詳細を含んだエンドポイント マネージャー セキュリティ タスクの作成<!-- 5568193  -->
Microsoft Defender ATP の脅威と脆弱性の管理 (TVM) によって、デバイスの正しく構成されていないセキュリティ設定を検出できます。 管理者は、この情報を使用して、脆弱性のあるデバイスを更新できます。

近日中に、Microsoft Defender ATP によって脆弱性の詳細を含むエンドポイント マネージャー セキュリティ タスク ( **[エンドポイント マネージャー]**  >  **[エンドポイント セキュリティ]**  >  **[セキュリティ タスク]** ) を生成し、影響を受けたデバイスを表示できるようになります。 IT 管理者は、セキュリティ タスクを受け入れ、必要な構成を展開できます。 

セキュリティ タスク詳細については、「[Intune を使用して Microsoft Defender ATP によって検出された脆弱性を修復する](../protect/atp-manage-vulnerabilities.md)」をご覧ください。

### <a name="improved-certificate-deployment-for-android-enterprise----6296499----"></a>Android Enterprise の証明書展開の改善 <!-- 6296499  -->
まもなく、Android Enterprise フル マネージド、専用、会社所有の仕事用プロファイルを実行するデバイスで、デバイスのユーザーがアクセスを許可する必要なく、Outlook 用の S/MIME 証明書を使用できるようになります。 S/MIME 証明書は、デバイス構成用の PKCS インポート済み証明書プロファイルを使用して展開されます ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]**  >  **[Android Enterprise]**  >  **[PKCS インポート済み証明書]** "*フル マネージド、専用、会社所有の仕事用プロファイル*" のカテゴリ)。

### <a name="tri-state-options-for-settings-are-coming-to-endpoint-security-firewall-policy---6586159-----"></a>エンドポイント セキュリティ ファイアウォール ポリシーに追加される設定の 3 つの状態オプション<!-- 6586159   -->
プラットフォーム (Windows または macOS) で追加のオプション ( **[エンドポイント セキュリティ]**  >  **[ファイアウォール]** ) をサポートできる場合、エンドポイント セキュリティ ファイアウォール ポリシーの設定に 3 番目の構成オプションを追加しています。

たとえば、現在、設定で、 **[構成しない]** と **[はい]** が提供されている場合、プラットフォームでサポートされている場合は、オプション **[いいえ]** が追加されます。

### <a name="new-security-baseline-for-office---3150261----"></a>Office の新しいセキュリティ ベースライン<!-- 3150261  -->
*Microsoft Office O365* の設定を管理するための新しいセキュリティ ベースライン ( **[エンドポイント セキュリティ]**  >  **[セキュリティ ベースライン]** ) を追加しています。 ベースラインの設定に、"*アドオン管理*"、"*MIME 処理*" などの Office アプリの構成が含まれるようになります。

### <a name="improved-status-details-in-security-baseline-reports---7221051------"></a>セキュリティ ベースライン レポートの状態の詳細の改善<!-- 7221051    -->
展開されたセキュリティ ベースラインの結果を表示したときに表示される状態の詳細を改善しています ( **[エンドポイント セキュリティ]**  >  **[セキュリティ ベースライン]**  >   "*セキュリティ ベースラインの種類を選択*" (**Windows 10 Security Baselines など)**  >  **[プロファイル]**  >  "*そのプロファイルのインスタンスを選択して状態を表示*"  > "*プロファイル レポートを選択*" (**デバイスの状態**など))。

この改善により、状態に使用する共通のラベルと定義が改善され、状態の意図にさらに適合するようになります。 次に例を示します。
- **[ベースラインと一致]** は、 **[既定の設定と一致]** に更新されます。これにより、デバイス構成が既定の (変更されていない) ベースライン構成と一致する場合を特定する意図がよりわかりやすく説明されます。
- **[正しく構成されていない]** は、より具体的な詳細に分けられます。たとえば、 **[エラー]** 、 **[競合]** 、 **[保留]** などがあります。 新しい状態により、コンソールの他の領域との一貫性が確保されます。

### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374--idstaged---"></a>エンドポイント セキュリティ ロールの RBAC アクセス許可の強化<!--7312374  idstaged -->
Intune の**エンドポイント セキュリティ マネージャー** ロールに、リモート タスクのロールベースのアクセス制御 (RBAC) アクセス許可を追加しています。このロールによって、Microsoft エンドポイント マネージャー管理センターへのアクセスが付与されます。これは、セキュリティ ベースライン、デバイスのコンプライアンス、条件付きアクセス、Microsoft Defender Advanced Threat Protection などのセキュリティとコンプライアンスの機能を管理するユーザーが使用できます。

Intune RBAC ロールのアクセス許可を表示するには、 **[テナント管理者]**  >  **[Intune ロール]**  >  の順に移動し、"*ロールを選択*" して、 >  **[アクセス許可]** を選択します。

リモート タスクの拡張されたアクセス許可には、次のものがあります。

- 今すぐ再起動
- リモート ロック
- BitLockerKeys のローテーション (プレビュー)
- FileVault キーのローテーション
- デバイスの同期
- Microsoft Defender
- 構成マネージャー アクションの開始

### <a name="updates-for-security-baselines---7102146-7103916----"></a>セキュリティ ベースラインの更新<!-- 7102146, 7103916  -->
まもなく、次のセキュリティ ベースラインの更新プログラムをリリースします ( **[エンドポイント セキュリティ]**  >  **[セキュリティ ベースライン]** )。
- **MDM セキュリティ ベースライン** (Windows 10 Security)
- **Microsoft Defender ATP ベースライン**

ベースラインの更新バージョンでは、それぞれの製品チームが推奨するベストプラクティスの構成を維持するのに役立つ最新の設定がサポートされます。

### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503--idstaged----"></a>エンドポイント セキュリティ構成の詳細を使用してデバイスのポリシー競合の原因を特定する<!-- 7567503  idstaged  -->
競合の解消を支援するために、まもなく、セキュリティ ベースライン プロファイルをドリルインして、選択されたデバイスの "*エンドポイント セキュリティ構成*" を表示できるようになります。 そこから、"*競合*" または "*エラー*" を示す設定を選択し、さらにドリルインを続け、競合に関係するプロファイルやポリシーを含む詳細の一覧を表示できます。 その後、競合の原因であるポリシーを選択すると、Intune により、そのポリシーの概要ペインが表示され、そこからポリシーの構成を確認または変更することができるようになります ( **[デバイス]**  >  "*デバイスを選択*"  >  **[エンドポイント セキュリティの構成]**  >  "*プロファイルまたはベースラインを選択*"  >  "*デバイスに適用される設定の一覧から設定を選択*")。

セキュリティ ベースラインをドリルインすると、次のポリシーの種類を、競合の原因として特定できます。
- デバイスの構成ポリシー
- エンドポイント セキュリティ ポリシー

### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-----"></a>デバイスのエンドポイント セキュリティ構成の新しい詳細<!-- 7745029   -->
デバイスのエンドポイント セキュリティ構成の一部として表示できるデバイスの新しい詳細を追加しています ( **[エンドポイント セキュリティ]**  >  **[セキュリティ ベースライン]**  >  "*ベースラインの選択*"  >  **[プロファイル]**  >  "*プロファイルの選択*"  >  **[デバイスの状態]**  >  **[エンドポイント セキュリティ構成]** )。 新しい詳細は次のとおりです。

- **UPN** (ユーザー プリンシパル名): UPN により、デバイス上の特定のユーザーに割り当てられているエンドポイント セキュリティ プロファイルを特定します。 これは、デバイス上の複数のユーザー、およびデバイスに割り当てられているプロファイルまたはベースラインの複数のエントリを区別するのに役立ちます。 
- **最低の状態**: この詳細により、デバイスの最も望ましくない状態を特定します。 この状態が **[成功]** の場合、デバイスにはポリシーの競合もエラーもありません。

### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Android 11 で、デバイス管理者登録されたデバイスへの信頼されたルート証明書の展開を非推奨にする<!--7662775  -->
Android 11 では、信頼されたルート証明書は、"*Android デバイス管理者*" として登録されたデバイスに展開できなくなりました。 Intune は Knox プラットフォームと統合されているため、この変更は、Samsung Knox デバイスに影響しません。 Samsung 以外のデバイスについては、ユーザーは、信頼されたルート証明書をデバイスに手動でインストールする必要があります。 

信頼されたルート証明書をデバイスに手動でインストールすると、SCEP を使用して、デバイスに証明書をプロビジョニングできます。 このシナリオでも、"*信頼された証明書*" ポリシーを作成してデバイスに展開し、そのポリシーを "*SCEP 証明書*" プロファイルにリンクする必要があります。

- 信頼されたルート証明書がデバイス上にある場合、SCEP 証明書プロファイルは正常にインストールされます。 
- 信頼された証明書が見つからない場合、SCEP 証明書プロファイルは失敗します。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。