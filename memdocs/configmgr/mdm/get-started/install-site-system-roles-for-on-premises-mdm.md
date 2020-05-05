---
title: オンプレミス MDM の役割のインストール
titleSuffix: Configuration Manager
description: Configuration Manager で、オンプレミスのモバイルデバイス管理 (MDM) に必要なサイトシステムの役割をインストールします。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724706"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager でオンプレミス MDM のサイトシステムの役割をインストールする

*適用対象:Configuration Manager (Current Branch)*

オンプレミスモバイルデバイス管理 (MDM) を Configuration Manager には、Configuration Manager サイトに次のサイトシステムの役割が必要です。

- 登録ポイント

- 登録プロキシ ポイント

- 配布ポイント

- デバイス管理ポイントは、モバイルデバイスに許可する管理ポイントです。

## <a name="requirements-and-limitations"></a>要件と制限事項

- オンプレミス MDM では、HTTPS 通信用にサイトシステムの役割を有効にする必要があります。 詳細については、「[オンプレミス MDM での信頼された通信用の証明書の設定](set-up-certificates-on-premises-mdm.md)」を参照してください。

- Configuration Manager の現在のブランチは、デバイスからオンプレミス MDM の配布ポイントおよびデバイス管理ポイントへの*イントラネット*接続のみをサポートしています。 ただし、macOS コンピューターも管理する場合、これらのクライアントは同じ役割への*インターネット*接続を必要とします。 配布ポイントとデバイス管理ポイントを構成する場合は、オプションを使用して、**イントラネットとインターネットの接続を許可**します。

- イントラネット接続用に構成する配布ポイントでは、サイトの境界を構成する必要があります。 Configuration Manager は、オンプレミス MDM の IPv4 範囲の境界のみをサポートします。 詳しくは、「[サイト境界と境界グループの定義](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)」をご覧ください。

- デバイス管理ポイントで[データベースレプリカ](../../core/servers/deploy/configure/database-replicas-for-management-points.md)を使用すると、新しく登録されたデバイスは最初に接続に失敗します。 この接続エラーは、正常に接続するために必要な、新しく登録されたデバイスに関する情報がデータベースレプリカにないために発生します。 レプリカは5分ごとに同期されます。 デバイスは、登録後の最初の5分間接続に失敗します。通常、この接続は2回試行されます。 デバイスは正常に接続されます。

## <a name="add-roles"></a>ロールを追加する

Configuration Manager クライアントを使用して管理されているほとんどのデバイスがあるサイトにオンプレミスの MDM を追加する場合は、これらの役割の一部がサイトに既にインストールされている可能性があります。 たとえば、配布ポイントは共通の役割であり、macOS デバイスを管理するには、デバイス管理ポイントが必要です。

サイトに役割を追加する方法の詳細については、「[サイトシステムの役割の追加](../../core/servers/deploy/configure/install-site-system-roles.md)」を参照してください。

## <a name="configure-roles"></a>役割の構成

新規または既存のロールを構成して、モバイルデバイスを管理します。 次の手順に従って、配布ポイントとデバイス管理ポイントをオンプレミスの MDM で正しく機能するように構成します。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サーバーとサイト システムの役割]** ノードを選択します。

1. 構成する配布ポイントまたはデバイス管理ポイントがあるサイトシステムサーバーを選択します。 一覧からサーバーを選択し、[サイトシステムの役割] 詳細ウィンドウで [**サイトシステム**の役割] を選択します。 リボンの [**サイトの役割**] タブで、[**プロパティ**] を選択します。

    > [!TIP]
    > 大規模なサイトでは、ビューのスコープを指定して、特定の役割を持つサーバーのみを表示することができます。 [**サーバーとサイトシステムの役割**] ノードを選択した場合は、リボンの [ホーム] タグで、[**役割を持つサーバー**] を選択します。 次に、サイトで現在利用可能なロールの一覧から、目的のロールを選択します。

    **サイトシステムのプロパティ**の **[全般**] タブで、**名前**が完全修飾ドメイン名 (FQDN) であることを確認します。 プロパティを閉じます。

1. [コンソール] の一覧で、オンプレミスの配布ポイントの役割を持つサーバーを選択します。 [サイトシステムの役割] 詳細ウィンドウで、**配布ポイント**の役割を選択します。 リボンの [**サイトの役割**] タブで、[**プロパティ**] を選択します。 **配布ポイントのプロパティ**の [**通信**] タブで、次のようにします。

    1. [ **HTTPS**] を選択し、[**イントラネットのみの接続を許可する**] を選択します。

        > [!IMPORTANT]
        > Configuration Manager クライアントを使用して macOS コンピューターも管理している場合は、代わりに **[イントラネットとインターネットの接続を許可**する] を使用します。

    1. **モバイルデバイスがこの配布ポイントに接続できるよう**にするオプションを有効にし、プロパティを閉じます。

1. **管理ポイント**サイトシステムの役割のプロパティを開きます。

    1. [**全般**] タブで、[ **HTTPS**] を選択し、[**イントラネットのみの接続を許可する**] を選択します。

        > [!IMPORTANT]
        > Configuration Manager クライアントを使用して macOS コンピューターも管理している場合は、代わりに **[イントラネットとインターネットの接続を許可**する] を使用します。

    1. **モバイルデバイスと Mac コンピューターでこの管理ポイントを使用できるよう**にするオプションを有効にし、プロパティを閉じます。

        > [!NOTE]
        > このオプションを選択すると、管理ポイントが*デバイス*管理ポイントに実質的に変わります。  

## <a name="next-step"></a>次のステップ

モバイルデバイスを管理するための役割を追加して構成したら、サーバーを信頼できるエンドポイントとして構成します。 この信頼により、ロールは管理対象デバイスと通信し、登録することができます。

> [!div class="nextstepaction"]
> [Set up certificates for trusted communications](set-up-certificates-on-premises-mdm.md)
