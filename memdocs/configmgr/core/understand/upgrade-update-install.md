---
title: アップグレード、更新、およびインストールについて
titleSuffix: Configuration Manager
description: Configuration Manager のインフラストラクチャを管理するときのインストール、更新、およびアップグレードという用語の相違点について説明します。
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706720"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>サイトと階層のインフラストラクチャでのアップグレード、更新、およびインストールについて

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のサイトと階層のインフラストラクチャの管理において、"*アップグレード*"、"*更新*"、"*インストール*" という用語は、3 つの異なる概念を説明するために使用されます。

## <a name="upgrade"></a>Upgrade

*アップグレード*または*インプレース アップグレード*は、Configuration Manager 2012 のサイトまたは階層を Configuration Manager Current Branch を実行するサイトまたは階層に変換する際に使用されます。

System Center 2012 Configuration Manager を Configuration Manager Current Branch にアップグレードする場合は、サイトおよびサイト サーバーをホストするために同じサーバーを引き続き使用し、Configuration Manager の既存のデータおよび構成を維持します。  これは、新しいハードウェアにインストールされている新しい Configuration Manager Current Branch サイトを使用しているときに、マネージド デバイスに関する構成およびデータを保持する方法である[移行](../migration/migrate-data-between-hierarchies.md)とは異なります。

詳細については、「[Configuration Manager へのアップグレード](../servers/deploy/install/upgrade-to-configuration-manager.md)」を参照してください。



## <a name="update"></a>更新
*更新*は、Configuration Manager のコンソール内の更新プログラム、および Configuration Manager コンソール内から配信できない更新プログラムであるアウトオブバンドの更新プログラムのインストールに使用されます。 以降のバージョンが実行されるように、コンソール内の更新プログラムでは、Current Branch サイト (またはテクニカル プレビュー サイト) のバージョンを変更できます。 たとえば、サイトでバージョン 1806 を実行している場合は、バージョン 1810 用の更新プログラムをインストールできます。 更新プログラムではサイトのバージョンを変更しなくても、既知の問題に対する修正プログラムをインストールすることもできます。      

通常、更新プログラムではセキュリティ修正プログラム、品質の向上、新機能が既存の展開に追加されます。 Technical Preview ブランチを使用する場合、更新プログラムでは Technical Preview の最新バージョンをインストールできます。
- コンソール内の更新プログラムをインストールするタイミングの選択を、階層の最上位サイトからします。
- コンソール内から利用できる更新プログラムはすべてインストールできます。 たとえば、サイトでバージョン 1802 を実行しているとき、1806 と 1810 の両方が提供されている場合、バージョン 1810 のインストールを検討してください。各バージョンには、前のリリース バージョンで最初に利用可能になった機能が含まれているためです。
- 新しい更新プログラムが最上位サイトでインストールを完了すると、子プライマリ サイトは自動的にプロセスを開始して更新します。 ただし、[サービス ウィンドウ](../servers/manage/service-windows.md)を設定し、更新のタイミングを制御することができます。
- セカンダリ サイトは更新プログラムを自動的にインストールしません。 代わりに、Configuration Manager コンソール内から手動で更新プログラムを開始します。

詳細については、「[Configuration Manager の更新プログラム](../servers/manage/updates.md)」、および「[Configuration Manager の Technical Preview](../get-started/technical-preview.md)」を参照してください。



## <a name="install"></a>[インストール]
*インストール*は、最初から新しい Configuration Manager の階層を作成する際、または追加のサイトを既存の階層に追加する際に使用されます。  

新しいプライマリ サイトまたは中央管理サイトをインストールする場合、使用する setup.exe の場所と関連するソース ファイルは、インストール シナリオによって異なります。

詳細については、[サイトのインストールの準備](../servers/deploy/install/prepare-to-install-sites.md)に関するページを参照してください。
