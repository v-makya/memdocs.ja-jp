---
title: Windows 自動操縦のユーザー主導モード
description: Windows 自動操縦のユーザー主導モードでは、IT 担当者の支援を必要とせずに、デバイスをすぐに使用可能な状態に展開するように構成できます。
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
ms.openlocfilehash: b2c9d3b8741fdae30b42aede8f5c7443e35d8bc7
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251961"
---
# <a name="windows-autopilot-user-driven-mode"></a>Windows Autopilot ユーザードリブン モード

**適用対象: Windows 10 バージョン1809以降**

Windows 自動操縦のユーザー主導モードでは、新しい Windows 10 デバイスを構成して、それらを工場出荷時の状態からすぐに使用可能な状態に自動的に変換することができます。 このプロセスでは、IT 担当者がデバイスに触れている必要はありません。

プロセスは単純で、だれでも完了できます。 デバイスは、簡単な手順で直接、エンドユーザーに配布または配信できます。

1. デバイスのボックスを解除して接続し、電源をオンにします。
2. 言語 (複数の言語がインストールされている場合にのみ必要)、ロケール、およびキーボードを選択します。
3. インターネットにアクセスできるワイヤレスネットワークまたは有線ネットワークに接続します。 ワイヤレスを使用する場合、ユーザーは Wi-fi リンクを確立する必要があります。 
4. 組織アカウントの電子メールアドレスとパスワードを指定します。

プロセスの残りの部分は、デバイスとして次のように自動化されます。
1. 組織に参加します。
2. Intune (または別の MDM サービス) に登録する
3. は、組織によって定義されたとおりに構成されます。

既定のエクスペリエンス (OOBE) では、追加のプロンプトを表示しないようにすることができます。使用可能なオプションについては、「 [自動操縦プロファイルの構成](profiles.md) 」を参照してください。

Windows 自動操縦のユーザー主導モードでは、Azure Active Directory およびハイブリッド Azure Active Directory 参加しているデバイスがサポートされます。 これら2つの結合オプションの詳細については、「 [デバイス id とは](https://docs.microsoft.com/azure/active-directory/devices/overview)」を参照してください。

ユーザー主導のプロセス中に完了したプロセスフローは次のとおりです。

1. ネットワークに接続した後、デバイスは Windows 自動操縦プロファイルをダウンロードします。 プロファイルでは、デバイスに使用する設定を定義します。 たとえば、OOBE 中に抑制するプロンプトを定義します。
2. Windows 10 は、重大な OOBE 更新プログラムをチェックします。 更新プログラムが利用可能な場合は、自動的にインストールされます (必要に応じて再起動します)。
3. ユーザーは Azure Active Directory 資格情報の入力を求められます。 このカスタマイズされたユーザーエクスペリエンスでは、Azure AD のテナント名、ロゴ、サインインテキストが表示されます。
4.  デバイスは、Windows 自動操縦プロファイルの設定に応じて、Azure Active Directory または Active Directory に参加します。
5. デバイスは、Intune (またはその他の構成済み MDM サービス) に登録されます。 組織のニーズに応じて、この登録は次のように行われます。
    - MDM の自動登録を使用した Azure Active Directory 参加プロセス中
    - Active Directory の結合プロセスの前。
6. 構成されている場合、 [登録ステータスページ](enrollment-status.md) (ESP) が表示されます。
7. デバイス構成タスクが完了すると、ユーザーは以前に指定した資格情報を使用して Windows 10 にサインインします。 (デバイスの ESP プロセス中にデバイスが再起動された場合、ユーザーは再起動の間にこれらの詳細が保持されないため、資格情報を再入力する必要があります)。
8. サインインすると、ユーザー対象の構成タスクについて [登録ステータス] ページが表示されます。

このプロセス中に問題が見つかった場合は、 [Windows 自動操縦のトラブルシューティング](troubleshooting.md) に関するドキュメントを参照してください。

使用可能な結合オプションの詳細については、次のセクションを参照してください。

- [Azure Active Directory 参加](#user-driven-mode-for-azure-active-directory-join) は、デバイスをオンプレミスの Active Directory ドメインに参加させる必要がない場合に使用できます。
- [ハイブリッド Azure Active Directory 参加](#user-driven-mode-for-hybrid-azure-active-directory-join) は、Azure Active Directory とオンプレミスの Active Directory ドメインの両方に参加する必要があるデバイスで使用できます。

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Azure Active Directory join のユーザー駆動モード

Windows 自動操縦を使用してユーザー主導の展開を完了するには、次の準備手順に従います。

1. ユーザー主導モードの展開を実行するユーザーが、デバイスを Azure Active Directory に参加させることができることを確認します。 詳細については、Azure Active Directory のドキュメントの [デバイス設定の構成](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal#configure-device-settings) に関するドキュメントを参照してください。
2. 必要な設定を使用して、ユーザー主導モードの自動操縦プロファイルを作成します。 Microsoft Intune では、プロファイルの作成時にこのモードが明示的に選択されます。 Microsoft Store for Business とパートナーセンターでは、ユーザー主導モードが既定値であるため、選択する必要はありません。
3. Intune を使用している場合は Azure Active Directory でデバイスグループを作成し、そのグループに自動操縦プロファイルを割り当てます。

ユーザー主導の展開を使用して展開するデバイスごとに、次の追加の手順が必要になります。

- デバイスが Windows 自動操縦に追加されていることを確認します。 Windows 自動操縦にデバイスを追加するには、次の2つの方法があります。
  - デバイスの購入時に OEM またはパートナーによって自動的に実行する
  - 「 [Windows 自動操縦にデバイスを追加する](add-devices.md)」の説明に従って、手動で収集します。
- 自動操縦プロファイルがデバイスに割り当てられていることを確認します。
 - Intune を使用して動的なデバイスグループを Azure Active Directory する場合は、この割り当てを自動的に行うことができます。
 - Intune を使用して静的デバイスグループを Azure Active Directory する場合は、デバイスをデバイスグループに手動で追加します。
 - 他の方法を使用する場合は (たとえば、ビジネスやパートナーセンターの Microsoft Store)、デバイスに自動操縦プロファイルを手動で割り当てます。


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>ハイブリッド Azure Active Directory 結合のユーザー主導モード

Windows の自動操縦には、デバイスを参加させることが Azure Active Directory 必要があります。 オンプレミスの Active Directory 環境がある場合は、オンプレミスドメインにデバイスを参加させることができます。 デバイスを参加させるには、 [Azure Active Directory (Azure AD) にハイブリッド参加](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)するように自動操縦デバイスを構成する必要があります。 

### <a name="requirements"></a>必要条件

Windows 自動操縦を使用して、ユーザー主導のハイブリッド Azure AD 参加した展開を実行するには:

- ユーザー主導モードの Windows 自動操縦プロファイルを作成する必要があります。 
 - **Hybrid Azure AD** 結合は、自動操縦プロファイルと **同じよう Azure AD に [結合** ] で選択したオプションとして指定する必要があります。
- Intune を使用している場合は、Azure Active Directory のデバイスグループが、そのグループに割り当てられた Windows 自動操縦プロファイルと共に存在している必要があります。
- デバイスでは、Windows 10 バージョン1809以降を実行している必要があります。
- デバイスは、Active Directory ドメインコントローラーにアクセスできる必要があります。 組織のネットワークに接続されている必要があります。 AD ドメインおよび AD ドメインコントローラーの DNS レコードを解決できる必要があります。 ユーザーを認証するために、ドメインコントローラーと通信できる必要があります。
- [ドキュメント「Windows 自動操縦ネットワークの要件](networking-requirements.md)」に従って、デバイスがインターネットにアクセスできる必要があります。
- Active Directory 用の Intune コネクタをインストールする必要があります。
 - 注: Intune コネクタは、オンプレミスの AD 参加を実行します。 そのため、ユーザーはオンプレミスの AD 参加アクセス許可を必要としません。 これは、ユーザーの代わりに [この操作を実行するように](https://docs.microsoft.com/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) コネクタが構成されていることを前提としています。 
- プロキシを使用する場合は、WPAD プロキシ設定オプションを有効にして構成する必要がある。

**デバイス参加の Azure AD**: ハイブリッド Azure AD 参加プロセスでは、システムコンテキストを使用してデバイス Azure AD 参加を実行します。 ユーザーベースの Azure AD 結合アクセス許可の設定の影響を受けません。 既定では、すべてのユーザーがデバイスを Azure AD に参加させることができます。

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>VPN サポートによるハイブリッド Azure Active Directory 参加のためのユーザー主導モード

Active Directory に参加しているデバイスは、多くのアクティビティに対して Active Directory ドメインコントローラーへの接続を必要とします。 これらのアクティビティには、ユーザーのサインイン (ユーザーの資格情報の検証) とグループポリシーアプリケーションが含まれます。 その結果、Windows 自動操縦のユーザー主導 Hybrid Azure AD Join プロセスでは、そのドメインコントローラーに ping を実行して、デバイスが Active Directory ドメインコントローラーに接続できるかどうかを検証します。

このシナリオの VPN サポートを追加すると、接続チェックをスキップするように Hybrid Azure AD Join プロセスを構成できます。 これによって、Active Directory ドメインコントローラーと通信する必要がなくなります。 代わりに、組織のネットワークへの接続を許可するために、ユーザーが Windows にサインインしようとする前に、必要な VPN 構成が提供されます。 


### <a name="requirements"></a>必要条件

VPN サポートの Hybrid Azure AD Join には、次の追加要件が適用されます。

- サポートされている Windows 10 のバージョン:
 - Windows 10 1903 + 12 月10日累積更新プログラム (KB4530684、OS ビルド 18362.535) 以降 
 - Windows 10 1909 + 12 月10日累積更新プログラム (KB4530684、OS ビルド 18363.535) 以降 
 - Windows 10 2004 以降 
- Hybrid Azure AD Join 自動操縦プロファイルで、新しい "ドメイン接続の確認をスキップする" 切り替えを有効にします。
- 次のような VPN 構成。
  - を Intune と共に展開し、ユーザーが Windows ログオン画面から手動で VPN 接続を確立できるようにすることができます。
  - 必要に応じて VPN 接続を自動的に確立するもの。 

必要な特定の VPN 構成は、使用されている VPN ソフトウェアと認証によって異なります。 サードパーティ (Microsoft 以外の) VPN ソリューションでは、通常、Intune 管理拡張機能を使用して、(VPN クライアントソフトウェア自体および特定の接続情報 (たとえば、VPN エンドポイントホスト名) を含む Win32 アプリを展開します。 そのプロバイダーに固有の構成の詳細については、VPN プロバイダーのドキュメントを参照してください。

> [!NOTE]
> VPN 要件は、Windows 自動操縦に固有のものではありません。 たとえば、ユーザーが組織のネットワーク上にいないときに新しいパスワードを使用して Windows にログオンする必要がある場合に、リモートでのパスワードのリセットを有効にする VPN 構成を既に実装している場合は、同じ構成を Windows 自動操縦で使用できます。 ユーザーが資格情報をキャッシュするためにサインインした後は、キャッシュされた資格情報を使用できるため、以降のログオン試行で接続は不要になります。 

VPN ソフトウェアで証明書認証が必要な場合は、必要なコンピューター証明書も Intune を使用して展開する必要があります。 この展開は、Intune 証明書の登録機能を使用して行うことができます。この場合、デバイスに対して証明書プロファイルをターゲットにします。

ユーザー証明書は、ユーザーがログインするまで展開できないため、サポートされていません。 また、ユーザーがサインインするまでインストールされないため、Windows ストアから配信された Microsoft 以外の UWP VPN プラグインはサポートされていません。

### <a name="validation"></a>検証

VPN を使用してハイブリッド Azure AD 参加を試行する前に、ユーザー主導の Hybrid Azure AD Join プロセスを組織のネットワークで実行できることを確認することが重要です。 この確認では、必要な追加の VPN 構成を追加する前にコアプロセスが動作することを確認することで、トラブルシューティングが容易になります。

次に、既にハイブリッド Azure AD 参加している既存のデバイスに、Intune を使用して VPN 構成 (Win32 アプリ、証明書、およびその他の要件) を展開できることを確認します。 たとえば、一部の VPN クライアントは、インストールプロセスの一部として、コンピューターごとの VPN 接続を作成します。 そのため、次のような手順を使用して構成を検証できます。

- PowerShell から、"VpnConnection-AllUserConnection" コマンドを使用して、コンピューターごとの VPN 接続が少なくとも1つ作成されていることを確認します。
- コマンドを使用して VPN 接続を手動で開始しようとしています: RASDIAL.EXE "ConnectionName"
- Windows のログオンページに [VPN 接続] アイコンが表示されることを確認します。
- 会社のネットワークからデバイスを移動し、Windows のログオンページのアイコンを使用して接続を確立します。 資格情報がキャッシュされていないアカウントにサインインします。

自動的に接続される VPN 構成では、検証手順が異なる場合があります。

> [!NOTE]
> このシナリオでは Always On VPN を使用できます。 詳細については、 [ALWAYS ON VPN のデプロイ](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) に関するドキュメントを参照してください。 Intune では、必要なコンピューターごとの VPN プロファイルをまだ展開できないことに注意してください。 

プロセスを検証するには、windows 10 の累積的な更新プログラムが Windows 10 1903 または Windows 10 1909 にインストールされていることを確認します。 最初にから最新の累積をダウンロードすることにより、OOBE 中に更新プログラムを手動でインストールでき https://catalog.update.microsoft.com ます。 次の手順に従います。

1. Shift + F10 キーを押してコマンドプロンプトを開きます。
2. ダウンロードした更新プログラムを含む USB キーを挿入します。
3. コマンドを使用して更新プログラムをインストールします (実際のファイル名に置き換えてください)。 WUSA.EXE <filename> .msu/quiet
4. コマンドを使用してコンピューターを再起動します。 shutdown.exe/r/t 0

または、Windows Update を開始して、最新の更新プログラムをインストールすることもできます。

1. Shift + F10 キーを押してコマンドプロンプトを開きます。
2. コマンド "start ms-settings:" を実行します。
3. [Update & Security] ノードに移動し、更新プログラムを確認します。
4. 更新プログラムのインストール後に再起動します。

### <a name="step-by-step-instructions"></a>詳細な手順

「 [Intune と Windows 自動操縦を使用したハイブリッド Azure AD 参加済みデバイスのデプロイ](https://docs.microsoft.com/intune/windows-autopilot-hybrid)」を参照してください。



