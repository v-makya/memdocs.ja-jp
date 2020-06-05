---
title: Microsoft Intune で Windows 8.1 デバイスでの VPN 設定を構成する - Azure | Microsoft Docs
description: Microsoft Intune で、Windows 8.1 が実行されているデバイスに対して、仮想プライベート ネットワーク (VPN) 構成設定を使用して VPN 構成プロファイルを追加または作成します。これには、接続の詳細、IP または FQDN アドレスを含めるプロキシ設定、および TCP ポートが含まれます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556355"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Microsoft Intune で Windows 8.1 デバイスでの VPN 設定を追加する

この記事では、Windows 8.1 を実行するデバイスでの VPN 接続の構成に使用できる Intune 設定を示します。

選択した設定によっては、次の一覧に記載されている値の一部を構成できない場合があります。

## <a name="before-you-begin"></a>始める前に

[Windows 8.1 VPN デバイス構成プロファイルを作成します](vpn-settings-configure.md)。

## <a name="base-vpn-settings"></a>基本 VPN 設定

- **[接続名]** :この接続の名前を入力します。 ユーザーがデバイスで使用可能な VPN 接続の一覧を参照するときに、この名前が表示されます。 たとえば、「`Contoso VPN`」と入力します。
- **サーバー**: デバイスの接続先となる 1 台以上の VPN サーバーを追加します。 サーバーを追加するときは、次の情報を入力します。
  - **説明**:**Contoso VPN サーバー**など、サーバーを表す名前を入力します。
  - **[IP アドレスまたは FQDN]** :デバイスの接続先となる VPN サーバーの IP アドレスまたは完全修飾ドメイン名 (FQDN) を入力します。 たとえば、「`192.168.1.1`」や「`vpn.contoso.com`」と入力します。
  - **[既定のサーバー]** : **[True]** にするとこのサーバーを、デバイスが接続を確立するために使用する既定のサーバーとして設定します。 1 台のサーバーのみを既定のサーバーとして設定してください。
  - **インポート**: 「説明, IP アドレスまたは FQDN, 既定のサーバー」という形式のサーバーのリストを含む、コンマ区切りのファイルを参照します。 **[OK]** を選んで、これらのサーバーを **[サーバー]** 一覧にインポートします。
  - **エクスポート**:サーバーのリストをコンマ区切り値 (csv) ファイルにエクスポートします。

- **接続の種類**:VPN 接続の種類を選択します。 次のようなオプションがあります。
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **[ログイン グループまたはドメイン]** (SonicWall Mobile Connect のみ):接続するログイン グループまたはドメインの名前を入力します。

- **[ロール]** (Pulse Secure のみ):この接続にアクセスできるユーザー ロールの名前を入力します。 ユーザー ロールを使用して、個人の設定とオプションを定義し、特定のアクセス機能を有効または無効にします。

- **[領域]** (Pulse Secure のみ):使用する認証領域の名前を入力します。 認証領域とは、接続の種類が [Pulse Secure] の場合に使用される認証リソースのグループを表します。

- **[カスタム XML]** :VPN 接続を構成する任意のカスタム XML コマンドを入力します。

  **Pulse Secure の例**:

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **CheckPoint Mobile VPN の例**:

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **SonicWall Mobile Connect の例**:

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **F5 Edge Client の例**:

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  カスタム XML コマンドの作成方法については、製造元の VPN ドキュメントをご覧ください。

- **[分割トンネリング]** : **[有効]** を選択すると、トラフィックに応じてデバイスに使用する接続が決定されるようになります。 たとえば、ホテルにいるユーザーは、業務ファイルへのアクセスに VPN 接続を使用しますが、通常の Web 閲覧にはホテルの標準ネットワークを使用します。 VPN 接続がアクティブなときにすべてのトラフィックに VPN トンネルが使用されるようにするには、 **[無効]** に設定します。

## <a name="proxy-settings"></a>プロキシの設定

- **[自動構成スクリプト]** :ファイルを使用してプロキシ サーバーを構成します。 構成ファイルを含む**プロキシ サーバー URL** を入力します。 たとえば、「`http://proxy.contoso.com`」と入力します。
- **[アドレス]** :プロキシ サーバーのアドレスを入力します (IP アドレスや `vpn.contoso.com` など)。
- **[ポート番号]** :プロキシ サーバーが使用する TCP ポート番号を入力します。
- **[自動的にプロキシ設定を検出する]** :VPN サーバーが接続にプロキシ サーバーを必要とする場合は、デバイスで接続の設定を自動的に検出するかどうかを選択します。 次のようなオプションがあります。
  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **有効**: 接続の設定を自動的に検出します。
  - **無効**:接続の設定は自動的に検出されません。
- **[ローカル アドレスにはプロキシ サーバーを使用しない]** :ローカル アドレスに対してプロキシ サーバーを使用するかどうか選択します。 次のようなオプションがあります。
  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **有効**: ローカル アドレスにはプロキシ サーバーを使用しません。
  - **無効**:ローカル アドレスにプロキシ サーバーを使用します。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Android](vpn-settings-android.md)、[Android エンタープライズ](vpn-settings-android-enterprise.md)、[macOS](vpn-settings-macos.md)、および [Windows 10](vpn-settings-windows-10.md) デバイスに対して VPN 設定を構成します。
