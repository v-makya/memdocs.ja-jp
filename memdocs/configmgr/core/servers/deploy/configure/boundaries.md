---
title: 境界を定義する
titleSuffix: Configuration Manager
description: 管理するデバイスを含めることができる、イントラネット上のネットワークの場所を定義する方法について説明します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13312c20edbda290daaa0d51908adeb7ab4a6860
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700063"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Configuration Manager の境界としてネットワークの場所を定義する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の境界は、管理対象のデバイスが含まれる、ネットワーク上の場所です。 Active Directory サイトやネットワーク IP アドレスなど、さまざまな種類の境界を作成できます。 Configuration Manager クライアントにより同様のネットワークの場所が特定されると、そのデバイスは境界の一部になります。

Configuration Manager では、次の種類の境界がサポートされています。

- IP サブネット
- Active Directory サイト
- IPv6 プレフィックス
- IP アドレスの範囲
- VPN (バージョン 2006 以降)

個別の境界を手動で作成することも、[Active Directory フォレストの探索](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)を使用することもできます。 この探索方法では、IP サブネットと Active Directory サイトの境界が自動的に検出、作成されます。 Active Directory フォレストの探索によって、Active Directory サイトのスーパーネットが特定されると、Configuration Manager によりスーパーネットが IP アドレスの範囲の境界に変換されます。

デバイスが想定した境界内にない場合は、ネットワークの場所を境界として定義していないことが原因である可能性があります。 デバイスのネットワークの場所が不明な場合は、デバイスで次の Windows コマンドを使用して確認します。

- IP アドレス: `ipconfig`
- Active Directory サイト: `nltest /dsgetsite`
- VPN: `ipconfig /all`

## <a name="boundary-types"></a>境界の種類

### <a name="ip-subnet"></a>IP サブネット

IP サブネットの境界の種類では、**サブネット ID** が必要です。 たとえば、「 `169.254.0.0` 」のように入力します。 **ネットワーク** (既定のゲートウェイ) と **サブネット マスク**の値を指定すると、Configuration Manager によって **サブネット ID** が自動的に計算されます。 境界を保存すると、Configuration Manager でサブネット ID 値のみが保存されます。

> [!NOTE]
> Configuration Manager では、境界としてスーパーネットを直接入力できません。 代わりに、境界の種類として IP アドレスの範囲を使用してください。

### <a name="active-directory-site"></a>Active Directory サイト

**Active Directory サイト**の境界の種類の場合、サイト名を指定します。 名前を入力するか、サイト サーバーのローカル フォレストを参照できます。

境界の Active Directory サイトを指定すると、Active Directory サイトのメンバーである各 IP サブネットが境界に含まれます。 Active Directory で Active Directory サイトの構成が変更されると、この境界に含まれているネットワークの場所も変更されます。  

Active Directory サイトの境界は、純粋な Azure Active Directory (Azure AD) デバイス (別称: クラウド ドメイン参加デバイス) に対しては機能しません。 オンプレミスでローミングする場合、Active Directory サイト タイプの境界のみを作成すると、これらのデバイスは境界内になりません。

> [!TIP]
> デバイスの現在の Active Directory サイトを確認するには、Windows コマンド `nltest /dsgetsite` を使用します。
>
> クライアントがクラウド ドメイン参加済みかどうかを調べるには、Windows コマンド `dsregcmd /status` を使用します。 詳細については、[dsregcmd コマンド - デバイスの状態](/azure/active-directory/devices/troubleshoot-device-dsregcmd)に関するページを参照してください。

### <a name="ipv6-prefix"></a>IPv6 プレフィックス

**IPv6 プレフィックス**境界タイプの場合、**接頭辞**を指定します。 たとえば、「 `2001:1111:2222:3333` 」のように入力します。

### <a name="ip-address-range"></a>IP アドレスの範囲

**IP アドレス範囲**の境界タイプの場合、範囲として**開始 IP アドレス**と**終了 IP アドレス**を指定します。 範囲には、1 つの IP サブネットまたは複数の IP サブネットの一部を含めることができます。 スーパーネットに対応するには、1 つの IP アドレス範囲の境界タイプを使用します。

このタイプでは、単一 IP アドレスに 1 つの境界を定義することもできます。 開始 IP アドレスと終了 IP アドレスを同じ値に設定します。 この構成は、一意のデバイスまたはテスト環境に役立つ場合があります。

### <a name="vpn"></a>VPN

<!--7020519-->

バージョン 2006 以降では、リモート クライアントの管理を簡略化するため、VPN 用の境界の種類を作成できます。 クライアントによる場所の要求の送信時に、そのネットワーク構成に関する追加情報が含まれます。 この情報に基づいて、サーバーはクライアントが VPN 上にあるかどうかを判断します。 Configuration Manager によってその境界内のクライアントを関連付けるには、デバイスを VPN に接続します。

VPN 境界を構成する方法には、いくつかあります。

- **[Auto detect VPN]\(VPN の自動検出\)** :Configuration Manager により Point-to-Point トンネリング プロトコル (PPTP) を使用するすべての VPN ソリューションが検出されます。 使用する VPN が検出されない場合は、他のオプションのいずれかを使用します。 コンソールの一覧の境界値は `Auto:On` になります。

- **[接続名]** :デバイスでの VPN 接続の名前を指定します。 これは、VPN 接続用の Windows のネットワーク アダプターの名前です。 Configuration Manager では文字列の最初の 250 文字が照合されますが、ワイルドカード文字または部分文字列はサポートされていません。 コンソールの一覧の境界値は `Name:<name>` になります。`<name>` はお客様が指定した接続名です。

  たとえば、デバイス上で `ipconfig` コマンドを実行し、1 つのセクションが `PPP adapter ContosoVPN:` で始まっていたとします。 **[接続名]** として文字列 `ContosoVPN` を使用します。 これは `Name:CONTOSOVPN` として一覧に表示されます。

- **[Connection description]\(接続の説明\)** :VPN 接続の説明を指定します。 Configuration Manager では文字列の最初の 243 文字が照合されますが、ワイルドカード文字または部分文字列はサポートされていません。 コンソールの一覧の境界値は `Description:<description>` になります。`<description>` はお客様が指定した接続の説明です。

  たとえば、デバイス上で `ipconfig /all` コマンドを実行し、1 つの接続に次の行が含まれていたとします: `Description . . . . . . . . . . . : ContosoMainVPN`。 **[Connection description]\(接続の説明\)** として文字列 `ContosoMainVPN` を使用します。 これは `Description:CONTOSOMAINVPN` として一覧に表示されます。

> [!IMPORTANT]
> この機能を最大限に活用するには、サイトを更新した後、クライアントも最新バージョンに更新します。 新しい機能は、サイトとコンソールを更新すると、Configuration Manager コンソールに表示されます。 完全なシナリオは、クライアントのバージョンも最新になるまで機能しません。
>
> OS の展開中にこの VPN 境界を使用するには、ブート イメージも更新して、最新のクライアント バイナリが含まれるようにする必要があります。

## <a name="create-a-boundary"></a>境界の作成

1. Configuration Manager コンソールで **[管理]** ワークスペースに移動し、 **[階層の構成]** を展開して、 **[境界]** ノードを選択します。

1. リボンの **[ホーム]** タブにある **[作成]** グループで、 **[境界の作成]** を選択します。

1. **[境界の作成]** ウィンドウの **[全般]** タブで、次の情報を指定します。

    - **説明**:フレンドリ名または参照によって境界を識別します。

        > [!NOTE]
        > Configuration Manager により、その種類と範囲に基づいて、境界に自動的に名前が付けられます。 名前を変更することはできません。

    - **種類**:作成する境界の種類を選択します。 種類に必要な追加情報を指定します。 詳しくは、「[境界の種類](#boundary-types)」を参照してください。

1. **[境界グループ]** タブに切り替えます。サイトに既に境界グループがある場合は、この新しい境界を 1 つ以上のグループにすぐに追加できます。

1. **[OK]** を選択して新しい境界を保存します。

## <a name="configure-a-boundary"></a>境界の構成

> [!TIP]
> 境界を作成すると、境界の種類と範囲に基づいて Configuration Manager により自動的に名前が付けられます。 この名前は変更できません。 Configuration Manager コンソールで境界を識別しやすいように説明を入力できます。

1. Configuration Manager コンソールで **[管理]** ワークスペースに移動し、 **[階層の構成]** を展開して、 **[境界]** ノードを選択します。

1. 変更する境界を選択します。 リボンの **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** を選択します。

1. 境界の **[プロパティ]** ウィンドウの **[全般]** タブで、次の設定を構成できます。

    - **[説明]** を編集します。
    - 境界の **[Type]\(種類\)** を変更します。
    - そのネットワークの場所を編集して、境界の範囲を変更します。 たとえば、Active Directory サイトの境界の場合、新しい Active Directory サイト名を指定できます。

1. その境界に関連付けられているサイト システムを確認するには、 **[サイト システム]** タブに切り替えます。この構成は、境界のプロパティから変更することはできません。

    > [!TIP]
    > サーバーが境界のサイト システムの一覧に表示されるようにするには、それをこの境界を含む少なくとも 1 つの境界グループのサイト システム サーバーとして関連付けます。 この構成は、境界グループの **[参照]** タブで行います。 詳しくは、「[サイトの割り当てを構成し、サイト システム サーバーを選択する](boundary-group-procedures.md#bkmk_references)」を参照してください。

1. この境界の境界グループ メンバーシップを変更するには、 **[境界グループ]** タブを選択します。

    - この境界を 1 つまたは複数の境界グループに追加するには、 **[追加]** を選択します。 境界グループを 1 つまたは複数選択して、 **[OK]** を選択してください。

    - この境界を境界グループから削除するには、境界グループを選択して、 **[削除]** を選択します。

1. **[OK]** を選択して境界のプロパティを閉じ、構成を保存します。

## <a name="next-steps"></a>次のステップ

各境界は階層内のすべてのサイトで利用できます。 境界を作成したら、1 つ以上の[境界グループ](boundary-groups.md)に境界を追加します。