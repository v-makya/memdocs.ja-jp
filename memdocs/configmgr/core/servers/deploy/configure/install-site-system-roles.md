---
title: サイト システムの役割のインストール
titleSuffix: Configuration Manager
description: サイト システムの役割を、サイト内の既存のサイト システム サーバー、または新しいサイト システム サーバーに追加します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 30b57de75e637aa083070832783647b8ad35b4a7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700533"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Configuration Manager のサイト システム役割のインストール

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager コンソールには、サイト システムの役割をインストールする方法が 2 つあります。

- **サイト システムの役割を追加する**:サイト システムの役割を、サイト内の既存のサイト システム サーバーに追加します。

- **サイト システム サーバーを作成する**:新しいサーバーをサイト システム サーバーとして指定してから、1 つ以上の役割をインストールします。 この方法は、最初のページを除き、「**サイトシステムの役割を追加する**」と同じです。 最初に、サーバーの名前と、サーバーのインストール先となるサイトを指定します。

> [!TIP]
> リモート コンピューターに役割をインストールすると、Configuration Manager によって、サイト サーバーのローカル グループにリモート コンピューターのコンピューター アカウントが追加されます。
>
> ドメイン コントローラーにサイトをインストールする場合のサイト サーバー上のグループは、ローカル グループではなく、ドメイン グループです。 この場合、リモート サイト システムの役割はすぐには機能しません。 サイト システム サーバーを再起動するか、リモート サーバーのコンピューター アカウントのための Kerberos チケットを最新の情報に更新する必要があります。 詳細については、「[使用されるアカウント](../../../plan-design/hierarchy/accounts.md)」を参照してください。

サイト システムの役割をインストールする前に、インストール先のコンピューターが、選択された役割の前提条件を満たしていることを確認するために、Configuration Manager による調査が行われます。

既定では、Configuration Manager がサイト システムの役割をインストールする際には、使用できるディスクの空き領域が最も多く、最初に利用可能な NTFS 形式のディスク ドライブにファイルがインストールされます。 Configuration Manager による特定ドライブへのインストールが行われないようにするには、サイト システム サーバーをインストールする前に、**no_sms_on_drive.sms** と言う名前の空のファイルをドライブのルートに作成します。

Configuration Manager では、**サイト システムのインストール アカウント**を使用して役割をインストールします。 このアカウントは、役割をインストールするときに指定します。 既定では、このアカウントは、サイト サーバー コンピューターのローカル システム アカウントです。 ドメイン ユーザー アカウントを、サイト システムのインストール アカウントとして指定できます。 詳細については、[アカウントに関するページの「サイト システムのインストール アカウント」](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)を参照してください。

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a>既存のサイト システム サーバーに役割をインストールする

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[サイトの構成]** を展開し、 **[サーバーとサイト システムの役割]** ノードを選択します。 新しいサイト システムの役割のインストール先となる既存のサイト システム サーバーを選択します。

1. リボンの **[ホーム]** タブにある **[サーバー]** グループで、 **[サイト システムの役割の追加]** を選択します。

1. **[全般]** ページで設定を確認します。

    > [!TIP]
    >  インターネットからサイト システムの役割にアクセスするには、必ずインターネット完全修飾ドメイン名 (FQDN) を指定します。

1. このサーバー上の役割にインターネット プロキシが必要な場合は、 **[プロキシ]** ページで、プロキシ サーバーの設定を指定します。 詳細については、「[プロキシ サーバーのサポート](../../../plan-design/network/proxy-server-support.md)」を参照してください。

1. **[システムの役割の選択]** ページで、追加するサイト システムの役割を選択します。

1. ウィザードを完了します。 特定のロールには、追加のページが表示される場合があります。 詳細については、[サイト システムの役割の構成オプション](configuration-options-for-site-system-roles.md)に関するページを参照してください。

> [!TIP]
> Windows PowerShell コマンドレットの **New-CMSiteSystemServer** を使用すると、この手順と同じ機能が実行されます。 詳細については、「[New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps)」を参照してください。

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> 新しいサイト システム サーバーに役割をインストールする

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[サイトの構成]** を展開し、 **[サーバーとサイト システムの役割]** ノードを選択します。

1. リボンの **[ホーム]** タブにある **[作成]** グループで、 **[サイト システム サーバーの作成]** を選択します。

1. **[全般]** ページで、サイト システムの全般設定を指定します。

    > [!TIP]
    > インターネットから新しいサイト システムの役割にアクセスするには、必ずインターネット FQDN を指定します。

1. このサーバー上の役割にインターネット プロキシが必要な場合は、 **[プロキシ]** ページで、プロキシ サーバーの設定を指定します。 詳細については、「[プロキシ サーバーのサポート](../../../plan-design/network/proxy-server-support.md)」を参照してください。

1. **[システムの役割の選択]** ページで、追加するサイト システムの役割を選択します。

1. ウィザードを完了します。 特定のロールには、追加のページが表示される場合があります。 詳細については、[サイト システムの役割の構成オプション](configuration-options-for-site-system-roles.md)に関するページを参照してください。

> [!TIP]
> Windows PowerShell コマンドレットの **New-CMSiteSystemServer** を使用すると、この手順と同じ機能が実行されます。 詳細については、「[New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps)」を参照してください。

## <a name="next-steps"></a>次のステップ

- [サイト システムの役割の構成オプション](configuration-options-for-site-system-roles.md)

- [役割の削除](../install/uninstall-sites-and-hierarchies.md#bkmk_role)