---
title: Windows 自動操縦のユーザー主導モード
description: Windows 自動操縦のユーザー主導モードでは、IT 担当者の支援を必要とせずに、デバイスをすぐに使用可能な状態に展開できます。
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
ms.openlocfilehash: b5e7c88272f8da386d25e7e7bca1973026f4407a
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757065"
---
# <a name="windows-autopilot-user-driven-mode"></a>Windows Autopilot ユーザードリブン モード

**適用対象: Windows 10 バージョン1809以降**

Windows 自動操縦のユーザー主導モードは、新しい Windows 10 デバイスを、IT 担当者がデバイスに触れることなく、すぐに使用可能な状態に変換できるように設計されています。  このプロセスは単純なものになるように設計されています。これにより、デバイスは、簡単な指示によって直接エンドユーザーに配布または配信できます。

- デバイスのボックスを解除して接続し、電源をオンにします。
- 言語 (複数の言語がインストールされている場合にのみ必要)、ロケール、およびキーボードを選択します。
- インターネットにアクセスできるワイヤレスネットワークまたは有線ネットワークに接続します。  ワイヤレスを使用する場合、ユーザーは Wi-fi リンクを確立する必要があります。  
- 組織アカウントの電子メールアドレスとパスワードを指定します。

これらの簡単な手順を完了すると、プロセスの残りの部分は自動化され、デバイスが組織に参加し、Intune (または別の MDM サービス) に登録され、組織によって定義されたとおりに完全に構成されます。  既定のエクスペリエンス (OOBE) では、追加のプロンプトを表示しないようにすることができます。使用可能なオプションについては、「[自動操縦プロファイルの構成](profiles.md)」を参照してください。

Windows 自動操縦のユーザー主導モードでは、Azure Active Directory およびハイブリッド Azure Active Directory 参加しているデバイスがサポートされます。  これら2つの結合オプションの詳細については、「[デバイス id とは](https://docs.microsoft.com/azure/active-directory/devices/overview)」を参照してください。

プロセスフローの観点から見ると、ユーザー主導のプロセス中に実行されるタスクは次のとおりです。

- ネットワークに接続されると、デバイスは、使用する必要がある設定 (たとえば、抑制する必要がある OOBE のプロンプトなど) を指定して、Windows 自動操縦プロファイルをダウンロードします。
- Windows 10 は、重大な OOBE の更新プログラムを確認します。 更新プログラムが利用可能な場合は、自動的にインストールされます (必要に応じて再起動します)。
- ユーザーは、Azure AD のテナント名、ロゴ、サインインテキストを表示するカスタマイズされたユーザーエクスペリエンスを使用して、Azure Active Directory 資格情報の入力を求められます。
- デバイスは、Windows 自動操縦プロファイルの設定に基づいて、Azure Active Directory または Active Directory に参加します。
- デバイスは、Intune (またはその他の構成済み MDM サービス) に登録されます。  (この登録は、MDM の自動登録を使用するか、必要に応じて Active Directory 参加プロセスの前に Azure Active Directory 参加プロセスの一部として行われます)。
- 構成されている場合、[登録ステータスページ](enrollment-status.md)(ESP) が表示されます。
- デバイス構成タスクが完了すると、ユーザーは、以前に指定した資格情報を使用して Windows 10 にサインインします。  (注: デバイスの ESP プロセス中にデバイスが再起動された場合、ユーザーは、再起動の間にこれらの詳細が保持されないため、資格情報を再入力する必要があります。)
- サインインすると、ユーザー対象の構成タスクについて [登録ステータス] ページが再び表示されます。

このプロセス中に問題が発生した場合は、 [Windows 自動操縦のトラブルシューティング](troubleshooting.md)に関するドキュメントを参照してください。

使用可能な結合オプションの詳細については、次のセクションを参照してください。

- [Azure Active Directory 参加](#user-driven-mode-for-azure-active-directory-join)は、デバイスをオンプレミスの Active Directory ドメインに参加させる必要がない場合に使用できます。
- [ハイブリッド Azure Active Directory 参加](#user-driven-mode-for-hybrid-azure-active-directory-join)は、Azure Active Directory とオンプレミスの Active Directory ドメインの両方に参加する必要があるデバイスで使用できます。

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Azure Active Directory join のユーザー駆動モード

Windows 自動操縦を使用してユーザー主導の展開を実行するには、次の準備手順を完了する必要があります。

- ユーザー主導モードの展開を実行するユーザーが、デバイスを Azure Active Directory に参加させることができることを確認します。  詳細については、Azure Active Directory のドキュメントの[デバイス設定の構成](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal#configure-device-settings)に関するドキュメントを参照してください。
- 必要な設定を使用して、ユーザー主導モードの自動操縦プロファイルを作成します。  Microsoft Intune では、プロファイルの作成時にこのモードが明示的に選択されます。 Microsoft Store for Business とパートナーセンターでは、ユーザー主導モードが既定値であるため、選択する必要はありません。
- Intune を使用している場合は Azure Active Directory でデバイスグループを作成し、そのグループに自動操縦プロファイルを割り当てます。

ユーザー主導の展開を使用して展開するデバイスごとに、次の追加の手順が必要になります。

- デバイスが Windows 自動操縦に追加されていることを確認します。  この追加は、デバイスの購入時に OEM またはパートナーによって自動的に行うことができます。または、後で手動で処理することもできます。  詳細については、「 [Windows 自動操縦にデバイスを追加する](add-devices.md)」を参照してください。
- 自動操縦プロファイルがデバイスに割り当てられていることを確認します。
  - Intune を使用して動的なデバイスグループを Azure Active Directory する場合は、この割り当てを自動的に行うことができます。
  - Intune を使用して静的デバイスグループを Azure Active Directory する場合は、デバイスをデバイスグループに手動で追加します。
  - 他の方法を使用する場合は (たとえば、ビジネスやパートナーセンターの Microsoft Store)、デバイスに自動操縦プロファイルを手動で割り当てます。


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>ハイブリッド Azure Active Directory 結合のユーザー主導モード

Windows の自動操縦には、デバイスを参加させることが Azure Active Directory 必要があります。 オンプレミスの Active Directory 環境を使用していて、オンプレミスドメインにデバイスを参加させる必要がある場合は、自動操縦デバイスを[Azure Active Directory (Azure AD) にハイブリッド参加](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)するように構成することができます。  

### <a name="requirements"></a>必要条件

Windows 自動操縦を使用して、ユーザー主導のハイブリッド Azure AD 参加した展開を実行するには:

- ユーザー主導モードの Windows 自動操縦プロファイルを作成する必要があります。 
  - **Hybrid Azure AD**結合は、自動操縦プロファイルと**同じよう Azure AD に [結合**] で選択したオプションとして指定する必要があります。
- Intune を使用している場合は、Azure Active Directory のデバイスグループが、そのグループに割り当てられた Windows 自動操縦プロファイルと共に存在している必要があります。
- デバイスでは、Windows 10 バージョン1809以降を実行している必要があります。
- デバイスは Active Directory ドメインコントローラーにアクセスできる必要があるため、組織のネットワークに接続する必要があります (AD ドメインと AD ドメインコントローラーの DNS レコードを解決し、ユーザーを認証するためにドメインコントローラーと通信できます)。
- [ドキュメント「Windows 自動操縦ネットワークの要件](windows-autopilot-requirements.md)」に従って、デバイスがインターネットにアクセスできる必要があります。
- Active Directory 用の Intune コネクタをインストールする必要があります。
  - 注: Intune コネクタはオンプレミスの AD 参加を実行します。そのため、ユーザーは、コネクタがユーザーの代わりに[この操作を実行するように構成](https://docs.microsoft.com/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit)されていることを前提として、オンプレミスの ad 参加アクセス許可は必要ありません。 
- プロキシを使用する場合は、WPAD プロキシ設定オプションを有効にして構成する必要がある。

**デバイス参加の Azure AD**: ハイブリッド Azure AD 参加プロセスでは、システムコンテキストを使用してデバイス Azure AD 参加を実行します。そのため、ユーザーベースの Azure AD 結合アクセス許可の設定による影響はありません。 また、既定では、すべてのユーザーがデバイスを Azure AD に参加させることができるようになります。

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>VPN サポートによるハイブリッド Azure Active Directory 参加のためのユーザー主導モード

Active Directory に参加しているデバイスは、ユーザーのサインイン (ユーザーの資格情報の検証) やグループポリシーアプリケーションなどのさまざまなアクティビティに対して、Active Directory ドメインコントローラーへの接続を必要とします。  その結果、Windows 自動操縦のユーザー主導 Hybrid Azure AD Join プロセスでは、そのドメインコントローラーに ping を実行して、デバイスが Active Directory ドメインコントローラーに接続できるかどうかを検証します。

このシナリオに対する VPN のサポートが追加されたため、Hybrid Azure AD Join 中の接続チェックをスキップするように指定できるようになりました。  これにより、Active Directory ドメインコントローラーと通信する必要がなくなりますが、ユーザーが Windows にサインインする前に、Intune を介して配信される必要な VPN 構成を使用して、組織のネットワークへの接続が可能になるように、デバイスを最初に準備することができます。

### <a name="requirements"></a>必要条件

VPN サポートの Hybrid Azure AD Join には、次の追加要件が適用されます。

- サポートされている Windows 10 のバージョン:
  - Windows 10 1903 + 12 月10日の累積的な更新プログラム (KB4530684、OS ビルド 18362.535) 以降 
  - Windows 10 1909 + 12 月10日の累積的な更新プログラム (KB4530684、OS ビルド 18363.535) 以降  
  - Windows 10 2004 以降 
- Hybrid Azure AD Join 自動操縦プロファイルで、新しい "ドメイン接続の確認をスキップする" 切り替えを有効にします。
- ユーザーが Windows ログオン画面から VPN 接続を手動で確立できるようにする、または必要に応じて VPN 接続を自動的に確立することを可能にする、Intune を使用して展開できる VPN 構成。  

必要な特定の VPN 構成は、使用されている VPN ソフトウェアと認証によって異なります。  サードパーティ (Microsoft 以外の) VPN ソリューションの場合は、通常、Intune 管理拡張機能を使用して、(vpn クライアントソフトウェア自体だけでなく、VPN エンドポイントホスト名などの特定の接続情報を含む) Win32 アプリを展開する必要があります。  そのプロバイダーに固有の構成の詳細については、VPN プロバイダーのドキュメントを参照してください。

> [!NOTE]
> VPN 要件は、Windows 自動操縦に固有のものではありません。 たとえば、ユーザーが組織のネットワーク上にいないときに新しいパスワードを使用して Windows にログオンする必要がある場合に、リモートでのパスワードのリセットを有効にする VPN 構成を既に実装している場合は、同じ構成を Windows 自動操縦で使用できます。  ユーザーが資格情報をキャッシュするためにサインインした後は、キャッシュされた資格情報を使用できるため、以降のログオン試行で接続は不要になります。 

VPN ソフトウェアで証明書認証が必要な場合は、必要なコンピューター証明書も Intune を使用して展開する必要があります。  この展開は、Intune 証明書の登録機能を使用して行うことができます。この場合、デバイスに対して証明書プロファイルをターゲットにします。

ユーザー証明書は、ユーザーがログインするまで展開できないため、サポートされていないことに注意してください。  また、Windows ストアから配信される Microsoft UWP VPN プラグインもサポートされていません。これは、ユーザーがサインインするまでこれらのプラグインがインストールされないためです。

### <a name="validation"></a>検証

VPN を使用してハイブリッド Azure AD 参加を試みる前に、まず、ユーザー主導の Hybrid Azure AD Join プロセスを組織のネットワークで実行できることを確認してから、次に説明する追加の要件を追加することが重要です。  これにより、必要な追加の VPN 構成を追加する前に、コアプロセスが正常に動作することを確認することで、トラブルシューティングが簡単になります。

次に、既にハイブリッド Azure AD 参加している既存のデバイスに、Intune を使用して VPN 構成 (Win32 アプリ、証明書、およびその他の要件) を展開できることを確認します。  たとえば、一部の VPN クライアントでは、インストールプロセスの一部としてコンピューターごとの VPN 接続が作成されるため、次のような手順を使用して構成を検証できます。

- PowerShell から、"VpnConnection-AllUserConnection" コマンドを使用して、コンピューターごとの VPN 接続が少なくとも1つ作成されていることを確認します。
- コマンドを使用して VPN 接続を手動で開始しようとしています: RASDIAL.EXE "ConnectionName"
- Windows のログオンページに [VPN 接続] アイコンが表示されることを確認します。
- 会社のネットワークからデバイスを移動し、Windows ログオンページのアイコンを使用して接続を確立し、キャッシュされた資格情報がないアカウントにサインインします。

自動的に接続される VPN 構成では、検証手順が異なる場合があります。

> [!NOTE]
> このシナリオでは Always On VPN を使用できます。  詳細については、 [ALWAYS ON VPN の展開](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment)に関するドキュメントを参照してください。  Intune では、必要なコンピューターごとの VPN プロファイルをまだ展開できないことに注意してください。 

エンドツーエンドのプロセスを検証するには、windows 10 または Windows 10 1909 10 1903 に必要な Windows 10 の累積的な更新プログラムがインストールされていることを確認します。 この更新プログラムは、最初にから最新の累積をダウンロードし、手動でインストールすることによって、OOBE 中に手動で実行でき https://catalog.update.microsoft.com ます。

- Shift + F10 キーを押してコマンドプロンプトを開きます。
- ダウンロードした更新プログラムを含む USB キーを挿入します。
- コマンドを使用して更新プログラムをインストールします (実際のファイル名に置き換えてください)。 WUSA.EXE <filename> .msu/quiet
- コマンドを使用してコンピューターを再起動します。 shutdown.exe/r/t 0

または、Windows Update を呼び出して、このプロセスを使用して最新の更新プログラムをインストールすることもできます。

- Shift + F10 キーを押してコマンドプロンプトを開きます。
- コマンド "start ms-settings:" を実行します。
- [Update & Security] ノードに移動し、更新プログラムを確認します。
- 更新プログラムのインストール後に再起動します。

### <a name="step-by-step-instructions"></a>ステップ バイ ステップの手順

「 [Intune と Windows 自動操縦を使用したハイブリッド Azure AD 参加済みデバイスのデプロイ](https://docs.microsoft.com/intune/windows-autopilot-hybrid)」を参照してください。



