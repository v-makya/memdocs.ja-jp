---
title: オペレーティング システムの展開の準備
titleSuffix: Configuration Manager
description: Configuration Manager でのオペレーティング システムの展開の準備方法について学習します
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708840"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Configuration Manager で OS を展開する準備を行う

*適用対象:Configuration Manager (Current Branch)*

オペレーティング システムを展開する前に、Configuration Manager でいくつかの作業を行う必要があります。 OS を展開する準備を行う場合は、次の記事を使用してください。  

-   [ブート イメージの管理](manage-boot-images.md)  

-   [OS イメージの管理](manage-operating-system-images.md)  

-   [OS アップグレード パッケージの管理](manage-operating-system-upgrade-packages.md)  

-   [ドライバーの管理](manage-drivers.md)  

-   [ユーザー状態の管理](manage-user-state.md)  

-   [不明なコンピューターの展開の準備](prepare-for-unknown-computer-deployments.md)  

-   [展開先のコンピューターにユーザーを関連付ける](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>OS イメージのサイズ  

OS イメージのサイズは大きくなります。 たとえば、Windows 7 のイメージ サイズは 3 GB 以上です。 イメージのサイズや、OS を同時に展開するコンピューターの数は、ネットワーク パフォーマンスや利用可能な帯域幅に影響します。 必ず、ネットワーク パフォーマンスのテストを行ってください。 影響をテストすることで、イメージの展開によって受ける可能性のある影響と、展開を完了するのにかかる時間を適切に判断できます。 ネットワーク パフォーマンスに影響する Configuration Manager の操作には、配布ポイントへのイメージの配布、サイト間でのイメージの配布、クライアントへのイメージのダウンロードが含まれます。  

また、OS イメージをホストする配布ポイントに十分なディスク容量を必ず設けるようにしてください。  

詳細については、「[Additional planning considerations for distribution points](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning)」(配布ポイントの計画に関する追加の考慮事項) を参照してください。


### <a name="client-cache-size"></a>クライアントのキャッシュ サイズ  

Configuration Manager クライアントでコンテンツをダウンロードする際は、バックグラウンド インテリジェント転送サービス (BITS) が使用可能であれば、このサービスが自動的に使用されます。 OS をインストールするタスク シーケンスを展開する際は、タスク シーケンスが実行される前に、Configuration Manager クライアントでローカル キャッシュに完全なイメージがダウンロードされるように、展開に関するオプションを設定することができます。  

Configuration Manager クライアントで OS イメージをダウンロードする必要はあるが、キャッシュに十分な領域がない場合、クライアントでそのキャッシュの領域をクリアすることができます。 キャッシュ内の他のパッケージが確認され、最も古いパッケージのいずれかを削除することで、イメージを格納するのに十分なディスク領域を確保できるかどうかが判断されます。 パッケージを削除しても十分な容量を確保できない場合、クライアントでイメージがダウンロードされず、展開は失敗します。 この動作は、キャッシュに大きなパッケージが保存されており、キャッシュにそれを保持するように設定した場合に起こる可能性があります。 パッケージを削除するとキャッシュに十分なディスク容量を確保できる場合は、クライアントはそれらを削除し、イメージをダウンロードしてキャッシュに保存します。  

Configuration Manager クライアントの既定のキャッシュ サイズでは、ほとんどの場合、OS イメージの展開に十分な容量を確保できません。 クライアント キャッシュに完全なイメージをダウンロードする予定の場合は、展開するイメージのサイズに合わせて、ダウンロード先のコンピューターにおけるクライアントのキャッシュ サイズを調整します。  

詳細については、[クライアント キャッシュの構成](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)に関するページを参照してください。  


