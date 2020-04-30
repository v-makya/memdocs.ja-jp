---
title: VPN プロファイルを作成する方法
titleSuffix: Configuration Manager
description: Configuration Manager で VPN プロファイルを作成する方法について説明します。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694250"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Configuration Manager で VPN プロファイルを作成する方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager は、複数の VPN 接続の種類をサポートします。 さまざまなデバイスプラット フォームで使用できる接続の種類の詳細については、[VPN プロファイル](vpn-profiles.md)に関するページを参照してください。

サード パーティの VPN 接続の場合は、VPN プロファイルを展開する前に VPN アプリを配布します。 アプリを展開しないと、ユーザーが VPN に接続しようとしたときに、アプリを展開するように求められます。 詳細については、「[アプリケーションの展開](../../apps/deploy-use/deploy-applications.md)」をご覧ください。

## <a name="create-a-vpn-profile"></a>VPN プロファイルの作成

1. Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースに移動し、 **[コンプライアンス設定]** 、 **[会社のリソースへのアクセス]** の順に展開して、 **[VPN プロファイル]** ノードを選択します。

1. リボンの **[ホーム]** タブの **[作成]** グループで、 **[VPN プロファイルの作成]** を選択します。

1. VPN プロファイルの作成ウィザードの **[全般]** ページで、次の情報を指定します。

    - **名前**:コンソールで VPN プロファイルを識別する一意の名前を入力します。

        > [!NOTE]
        > VPN プロファイル名には、文字 `\/:*?<>|; ` を使用しないでください。 Windows VPN プロファイルは、これらの特殊文字をサポートしません。

    - **説明**:必要に応じて、VPN プロファイルに関する詳細情報を提供する説明を入力します。

    - **VPN プロファイルの種類**:適切なプラットフォームを選択します。

        **Windows 8.1** プラットフォームを選択した場合は、 **[ファイルからインポート]** することもできます。 この操作は、XML ファイルから VPN プロファイル情報をインポートします。 このオプションを選択すると、ウィザードの残りの部分は、 **[サポートされているプラットフォーム]** ページと **[VPN プロファイルのインポート]** ページに簡素化されます。

1. **[サポートされているプラットフォーム]** ページで、この VPN プロファイルでサポートされている OS バージョンを選択します。

1. **[接続]** ページで、次の情報を指定します。

    - **接続の種類**:VPN 接続の種類を選択します。 サポートされている種類の詳細については、[VPN プロファイル](vpn-profiles.md)に関するページを参照してください。

    - **サーバーの一覧**: VPN 接続に使用する新しいサーバーを追加します。 接続の種類によっては、1 つ以上の VPN サーバーを追加し、既定のサーバーを指定することもできます。

    - **[Bypass VPN when connected to company network]\(会社のネットワークに接続されているときは VPN を使用しない\)** :クライアントが内部ネットワークに接続されている場合、VPN を使用しないように構成します。 必要に応じて、接続固有の DNS 名を指定します。

1. ウィザードの **[認証方法]** ページで、接続の種類でサポートされている方法を選択します。 このページの設定および使用可能なオプションは、選択した接続の種類によって異なります。 詳細については、「[認証方法のリファレンス](#bkmk_auth)」を参照してください。

1. VPN でプロキシ サーバーを使用する場合は、 **[プロキシの設定]** ページで、環境に適したいずれかのオプションを選択します。 次に、プロキシの構成情報を指定します。

1. **[アプリケーション]** ページは、Windows 10 プロファイルにのみ適用されます。 この VPN に自動的に接続するデスクトップとユニバーサル アプリを追加します。 アプリの種類によってアプリの識別子が決まります。

    - *デスクトップ アプリ*の場合、アプリのファイル パスを指定します。

    - *ユニバーサル アプリ*の場合、パッケージのファミリ名 (PFN) を指定します。 アプリの PFN を検索する方法については、「[Find a package family name for per-app VPN](find-a-pfn-for-per-app-vpn.md)」(アプリごとの VPN のパッケージ ファミリ名を検索する) を参照してください。

    また、 **[一覧に含まれるアプリだけがこの VPN を使用できる]** ようにオプションを構成することもできます。

    > [!IMPORTANT]
    > アプリごとの VPN を構成するためにコンパイルした、関連付けられたアプリのすべての一覧をセキュリティで保護してください。 承認されていないユーザーによって一覧が変更され、それをアプリごとの VPN のアプリの一覧にインポートした場合、アクセスが許可されていないアプリへの VPN アクセスが認証される可能性があります。

1. **[境界]** ページは Windows 10 プロファイルにのみ適用され、VPN 境界を構成します。 次のオプションを追加できます。

    - **ネットワーク トラフィック規則**: VPN 接続に対して有効にするプロトコル、ローカル ポート、リモート ポート、アドレス範囲を設定します。  

        > [!Note]
        > ネットワーク トラフィック規則を作成しない場合は、すべてのプロトコル、ポート、およびアドレス範囲が有効になります。 規則を作成すると、その規則または追加の規則で指定したプロトコル、ポート、アドレス範囲のみが VPN 接続で使用されます。

    - **DNS 名および DNS サーバー**:デバイスが接続を確立した後に VPN 接続で使用される DNS サーバー。

    - **ルート**:VPN 接続を使用するネットワーク ルート。 60 を超えるルートを作成すると、ポリシーが機能しなくなる場合があります。

1. ウィザードを完了します。

新しい VPN プロファイルは、 **[資産とコンプライアンス]** ワークスペースの **[VPN プロファイル]** ノードに表示されます。

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a>認証方法のリファレンス

使用できる VPN 認証方法は、接続の種類によって異なります。

### <a name="certificates"></a>証明書

RADIUS サーバー (ネットワーク ポリシー サーバーなど) での認証にクライアント証明書を使用する場合は、証明書のサブジェクトの別名をユーザーのプリンシパル名に設定します。

サポートされる接続の種類:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- チェック ポイント モバイル VPN

### <a name="username-and-password"></a>ユーザー名とパスワード

サポートされる接続の種類:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- チェック ポイント モバイル VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

サポートされる接続の種類:

- Microsoft SSL (SSTP)
- Microsoft 自動
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Microsoft 保護された EAP (PEAP)

サポートされる接続の種類:

- Microsoft SSL (SSTP)
- Microsoft 自動
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Microsoft セキュリティで保護されたパスワード (EAP-MSCHAP v2)

サポートされる接続の種類:

- Microsoft SSL (SSTP)
- Microsoft 自動
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>スマート カードまたはその他の証明書

サポートされる接続の種類:

- Microsoft SSL (SSTP)
- Microsoft 自動
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

サポートされる接続の種類:

- Microsoft SSL (SSTP)
- Microsoft 自動
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>コンピューターの証明書を使う

サポートされる接続の種類:

- IKEv2

### <a name="additional-authentication-options"></a>追加の認証オプション

Windows クライアント バージョンでサポートされている場合は、認証方法を**構成**するためのオプションを使用できます。 このオプションを選択すると、認証方法を構成するための Windows のプロパティ ウィンドウが開きます。

選択したオプションに応じて、次のような詳細情報の指定を求められる場合があります。

- **ログオンごとにユーザー資格情報を保存する**: ユーザーが接続するたびに資格情報を入力する必要がないように、ユーザー資格情報が保存されます。  

- **[クライアント認証用のクライアント証明書の選択]** : VPN 接続を認証するための、以前に作成したクライアント SCEP 証明書プロファイルを選択します。 詳細については、[PFX 証明書プロファイルの作成](create-certificate-profiles.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

- サード パーティの VPN 接続の場合は、VPN プロファイルを展開する前に VPN アプリを配布します。 アプリを展開しないと、ユーザーが VPN に接続しようとしたときに、アプリを展開するように求められます。 詳細については、「[アプリケーションの展開](../../apps/deploy-use/deploy-applications.md)」をご覧ください。

- VPN プロファイルを展開します。 詳細については、[プロファイルの展開方法](deploy-wifi-vpn-email-cert-profiles.md)に関するページを参照してください。
