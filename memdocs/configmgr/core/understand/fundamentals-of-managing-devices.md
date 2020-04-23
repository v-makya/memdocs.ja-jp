---
title: デバイスの管理の基礎
titleSuffix: Configuration Manager
description: Configuration Manager を使用してデバイスを管理する方法について説明します。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707070"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Configuration Manager を使用したデバイス管理の基礎

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager は、大きく分けて 2 つのカテゴリのデバイスを管理できます。

- "*クライアント*" は、Configuration Manager クライアント ソフトウェアのインストール先とするデバイスであり、ワークステーション、ノート PC、サーバー、モバイル デバイスなどがあります。 ハードウェア インベントリのような一部の管理機能には、このクライアント ソフトウェアが必要です。  

- "*マネージド デバイス*" には "*クライアント*" が含まれることもありますが、通常は Configuration Manager クライアント ソフトウェアがインストールされていないモバイル デバイスを指します。 この種のデバイスを管理するには、Configuration Manager に組み込まれているオンプレミスのモバイル デバイス管理を使用します。

また、クライアントの種類だけでなくユーザーに基づいてデバイスをグループ化および識別することもできます。

## <a name="managing-devices-with-the-configuration-manager-client"></a>Configuration Manager クライアントを使用したデバイスの管理

Configuration Manager クライアント ソフトウェアを使用してデバイスを管理するには、2 つの方法があります。 1 つ目の方法は、ネットワーク上でデバイスを探索し、そのデバイスにクライアント ソフトウェアを展開するというものです。 2 つ目の方法は、新しいコンピューターにクライアント ソフトウェアを手動でインストールし、そのコンピューターをネットワークに参加させるときに、サイトにも参加させるというものです。 クライアント ソフトウェアがまだインストールされていないデバイスを探索するには、組み込まれた探索方法のうちの 1 つまたは複数を実行します。 デバイスが探索されたら、いくつかの方法のいずれかで、クライアント ソフトウェアをインストールします。 探索の使用の詳細については、「[System Center Configuration Manager 用の探索の実行](../servers/deploy/configure/run-discovery.md)」をご覧ください。  

Configuration Manager クライアント ソフトウェアを実行するようにサポートされているデバイスを検出したら、いくつかの方法のうちの 1 つを使用して、ソフトウェアをインストールできます。 ソフトウェアがインストールされて、クライアントがプライマリ サイトに割り当てられたら、デバイスの管理を開始できます。 一般的なインストール方法には次のものがあります。

- クライアント プッシュ インストール

- ソフトウェアの更新に基づいたインストール

- グループ ポリシー

- コンピューターへの手動インストール

- 展開する OS イメージの一部としてのクライアントの追加  

クライアントがインストールされたら、コレクションを使用して、デバイス管理タスクを簡略化できます。 コレクションは、デバイスやユーザーをグループとして管理できるように作成されたデバイスまたはユーザーのグループです。 たとえば、Configuration Manager に登録されているすべてのモバイル デバイスに、モバイル デバイス アプリケーションをインストールすることができます。 この場合は、[すべてのモバイル デバイス] コレクションを使用することができます。  

詳細については、次のトピックを参照してください。  

- [デバイス管理ソリューションの選択](../plan-design/choose-a-device-management-solution.md)  

- [クライアント インストール方法](../clients/deploy/plan/client-installation-methods.md)  

- [コレクションの概要](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>クライアント設定

Configuration Manager を最初にインストールすると、階層内のすべてのクライアントは既定のクライアント設定で構成されます (これは変更可能です)。 これらのクライアント設定には、次のような構成オプションがあります。

- デバイスがサイトと通信する頻度。

- クライアントがソフトウェア更新プログラムとその他の管理操作に対してセットアップされているかどうか。

- ユーザーがモバイル デバイスを Configuration Manager による管理対象として登録できるかどうか。  

カスタム クライアント設定を作成し、コレクションに割り当てることができます。 カスタム設定が適用されるようにコレクションのメンバーに構成されます。指定する (番号) 順序で適用されるように複数のカスタム クライアントを作成できます。 競合する設定がある場合は、順序番号が最も小さい設定がその他の設定をオーバーライドします。  

次の図は、カスタム クライアント設定を作成および適用する方法の例を示します。  

![クライアント設定](media/ClientSettings.gif)  

クライアント設定の詳細については、次の記事を参照してください。

- [クライアント設定を構成する方法](../clients/deploy/configure-client-settings.md)
- [クライアント設定について](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Configuration Manager クライアントを使用しないデバイス管理

Configuration Manager では、クライアント ソフトウェアがインストールされていないデバイスの管理、および Intune によって管理されないデバイスの管理をサポートします。 詳細については、[Configuration Manager でのオンプレミス インフラストラクチャによるモバイル デバイスの管理](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)に関する記事、および「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」をご覧ください。  

## <a name="user-based-management"></a>ユーザー ベースの管理

Configuration Manager では、Azure Active Directory および Active Directory Domain Services ユーザーのコレクションをサポートします。 ユーザー コレクションを使用する場合、コレクションのメンバーによって使用されるすべてのコンピューターにソフトウェアをインストールすることができます。 展開するソフトウェアがユーザーのプライマリ デバイスとして指定されているデバイスのみにインストールされるようにするには、ユーザーとデバイスのアフィニティを設定します。 ユーザーは 1 つまたは複数のプライマリ デバイスを持つことができます。  

ユーザーがソフトウェア展開のエクスペリエンスを制御できる 1 つの方法は、クライアント インターフェイスである**ソフトウェア センター**を使用することです。 **ソフトウェア センター**は、クライアント コンピューターに自動的にインストールされ、Windows の **[スタート]** メニューから実行します。 ユーザーは**ソフトウェア センター**を使用して自分のソフトウェアを管理でき、次のタスクを実行できます。  

- ソフトウェアのインストール  

- 勤務時間外にソフトウェアが自動的にインストールされるようにスケジュールする  

- Configuration Manager がデバイスにソフトウェアをインストールできるタイミングを構成する  

- Configuration Manager でリモート コントロールがセットアップされている場合に、リモート コントロールのアクセス設定を構成する  

- 管理者が電源管理オプションを設定している場合、そのオプションを構成する  

- ソフトウェアの参照、インストール、要求

- 優先設定の構成

- 設定時に、ユーザーとデバイスのアフィニティのプライマリ デバイスを指定する

詳細については、以下の記事を参照してください。

- [ソフトウェア センターの計画](../../apps/plan-design/plan-for-software-center.md)
- [ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [ソフトウェア センターのユーザー ガイド](software-center.md)
