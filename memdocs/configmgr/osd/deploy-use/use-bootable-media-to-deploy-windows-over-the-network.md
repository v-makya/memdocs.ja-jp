---
title: 起動可能なメディアを使用したネットワーク経由での Windows の展開
titleSuffix: Configuration Manager
description: Configuration Manager での起動可能なメディアによる展開を使用して、セットアップ先のコンピューターの起動時に OS を展開します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124758"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager で起動可能なメディアを使用してネットワーク経由で Windows を展開する

*適用対象:Configuration Manager (Current Branch)*

起動可能なメディアには、ブート イメージとタスク シーケンスへのポインターのみが含まれます。 これにより、OS イメージとその他の参照されるコンテンツがネットワークからダウンロードされます。 起動可能なメディアにはあまりコンテンツが含まれていないため、メディアを交換しなくても、タスク シーケンスとほとんどのコンテンツを更新できます。

次のシナリオでは、ブート メディアを使用して、ネットワーク経由でオペレーティング システムを展開します。

- [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)

- [既存のコンピューターの置き換えと設定の転送](replace-an-existing-computer-and-transfer-settings.md)

いずれかの OS の展開シナリオの手順を完了してから、次のセクションを使用して、起動可能なメディアを使用し、OS を展開します。

## <a name="configure-deployment-settings"></a>展開の設定の構成

起動可能なメディアを使用して OS の展開プロセスを開始する場合、OS をメディアから使用できるように、タスク シーケンスの展開を構成します。 このオプションは、展開の **[展開の設定]** タブで設定します。 **[利用できるようにする項目]** の設定では、次のいずれかのオプションを選択します。

- Configuration Manager クライアント、メディア、PXE

- メディアと PXE のみ

- メディアと PXE のみ (非表示)

詳細については、「 [Deploy a task sequence](deploy-a-task-sequence.md)」をご覧ください。

## <a name="create-the-bootable-media"></a>起動可能なメディアを作成する

起動可能なメディアを作成するときに、USB フラッシュ ドライブまたは CD/DVD セットのどちらかを指定します。 起動可能なドライブに選ぶオプションは、メディアを起動するコンピューターがサポートするものでなければなりません。 詳細については、「[起動可能なメディアの作成](create-bootable-media.md)」を参照してください。

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a> 起動可能なメディアから OS をインストールする

OS をインストールするには、起動可能なメディアを挿入し、コンピューターの電源を入れます。

## <a name="support-for-cloud-based-content"></a>クラウドベースのコンテンツのサポート

<!--6209223-->

バージョン 2006 以降では、起動可能なメディアによってクラウドベースのコンテンツをダウンロードできます。 たとえば、デバイスを再イメージ化するために、リモート オフィスのユーザーに USB キーを送ることがあります。 または、ローカルの PXE サーバーがあるオフィスでも、デバイスでクラウド サービスの優先順位をできるだけ高くしたいことがあります。 今では、大規模な OS 展開コンテンツをダウンロードするために WAN にさらに負荷をかけるのではなく、ブート メディアや PXE 展開で、クラウドベースのソースからコンテンツを取得することができるようになりました。 たとえば、コンテンツの共有が可能なクラウド管理ゲートウェイ (CMG) などがあります。

> [!NOTE]
> デバイスには、管理ポイントへのイントラネット接続が引き続き必要になります。

タスク シーケンスを実行すると、クラウドベースのソースからコンテンツがダウンロードされます。 クライアントで **smsts.log** を確認します。

### <a name="prerequisites"></a>前提条件

- **[Cloud Services]** グループで、 **[クラウド配布ポイントへのアクセスを許可する]** クライアント設定を有効にします。 このクライアント設定がターゲット クライアントに展開されていることを確認します。 詳細については、クライアント設定に関するページの「[クラウド サービス](../../core/clients/deploy/about-client-settings.md#cloud-services)」を参照してください。

- クライアントが含まれている境界グループの場合:

  - コンテンツが有効な CMG またはクラウド配布ポイント サイト システムを関連付けます。 詳細については、「[境界グループを構成する](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config)」を参照してください。

  - 次のオプションを有効にします: **[オンプレミスのソースよりクラウド ベースのソースを優先する]** オプションを有効にします。 詳細については、「[ピアのダウンロードの境界グループのオプション](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)」を参照してください。

- タスク シーケンスによって参照されるコンテンツを、コンテンツが有効な CMG またはクラウド配布ポイントに配布します。

## <a name="next-steps"></a>次のステップ

[OS 展開のユーザー エクスペリエンス](../understand/user-experience.md#task-sequence-wizard)
