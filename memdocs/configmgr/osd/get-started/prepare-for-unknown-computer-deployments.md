---
title: 不明なコンピューターの展開の準備
titleSuffix: Configuration Manager
description: Configuration Manager 環境内で Configuration Manager によって管理されていないコンピューターにオペレーティング システムを展開する方法について説明します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708820"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Configuration Manager での不明なコンピューターの展開の準備

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager 環境内でオペレーティング システムを不明なコンピューターに展開するには、このトピックの情報を参考にしてください。 不明なコンピューターとは、Configuration Manager によって管理されていないコンピューターのことです。 これは、Configuration Manager データベースにそれらのコンピューターのレコードがないことを意味します。 不明なコンピューターには次のようなものがあります。  

- Configuration Manager クライアントがインストールされていないコンピューター  

- Configuration Manager にインポートされていないコンピューター  

- Configuration Manager で検出されていないコンピューター  

  以下の展開方法で、不明なコンピューターにオペレーティング システムを展開できます。  

- [PXE を使用したネットワーク経由での Windows の展開](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [起動可能なメディアを使用して、オペレーティング システムを展開する](../deploy-use/create-bootable-media.md)  

- [事前設定されたメディアを使用して、オペレーティング システムを展開する](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>不明なコンピューターの展開のワークフロー  
 以下に、不明なコンピューターにオペレーティング システムを展開する際の基本的なワークフローについて説明します。  

-   展開で使用する不明なコンピューター オブジェクトを選択する。 オペレーティング システムを、 **すべての不明なコンピューター** コレクションの不明なコンピューター オブジェクトのいずれかに展開したり、 **すべての不明なコンピューター** コレクション内のオブジェクトを別のコレクションに追加したりできます。 Configuration Manager では、**すべての不明なコンピューター** コレクション内に 2 つの不明なコンピューター オブジェクトがあります。 ひとつは x86 コンピューター用オブジェクトで、もうひとつは x64 コンピューター用オブジェクトです。  

    > [!NOTE]  
    >  **[不明な x86 コンピューター]** は、x86 のみが可能なコンピューター用オブジェクトです。 **[不明な x64 コンピューター]** は、x86 および x64 が可能なコンピューター用オブジェクトです。 言い換えると、これらのオブジェクトは、展開先コンピューターのアーキテクチャの説明になります。 セットアップ先のコンピューターに展開するオペレーティング システムの説明ではありません。  

-   不明なコンピューターの展開をサポートする PXE 対応配布ポイントを構成するか、メディアを作成する。  

-   オペレーティング システムをインストールするタスク シーケンスを展開する。  

## <a name="unknown-computer-installation-process"></a>不明なコンピューターのインストール プロセス  
 コンピューターが最初に PXE またはメディアから起動されると、 Configuration Manager は、コンピューターのレコードが Configuration Manager データベースに存在するかどうか確認します。 レコードがある場合は、Configuration Manager がさらに、そのレコードに展開されるタスク シーケンスがあるかどうかを確認します。 レコードがない場合は、Configuration Manager は、不明なコンピューター オブジェクトに展開されたタスク シーケンスがあるかどうか確認します。 いずれの場合も、Configuration Manager は、それから次のいずれかのアクションを実行します。  

- タスク シーケンスを使用できる場合は、Configuration Manager はユーザーにタスク シーケンスの実行を求めます。  

- 必要なタスク シーケンスがある場合は、Configuration Manager がそのタスク シーケンスを自動的に実行します。  

- タスク シーケンスがレコードに展開されていない場合は、Configuration Manager は、展開先コンピューターにタスク シーケンスが展開されていないというエラーを生成します。  

  不明なコンピューターが開始された場合、Configuration Manager はそのコンピューターを、不明なコンピューターではなく、プロビジョニングが解除されたコンピューターとして認識します。 これは、そのコンピューターが、不明なコンピューター オブジェクトに展開されたタスク シーケンスを受信できることを意味します。 展開されたタスク シーケンスは、Configuration Manager クライアントを含むオペレーティング システム イメージをインストールします。  

  Configuration Manager クライアントがインストールされた後、コンピューターのレコードが作成され、そのコンピューターが適切な Configuration Manager コレクションのリストに追加されます。 コンピューターがオペレーティング システム イメージまたは Configuration Manager クライアントのインストールに失敗した場合、コンピューターの "不明" のレコードが作成され、コンピューターは**すべてのシステム**コレクションに表示されます。  

> [!NOTE]  
>  オペレーティング システム イメージのインストール時、タスク シーケンスは、不明なコンピューターからコレクション変数を取得できますが、コンピューター変数は取得できません。  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> 不明なコンピューターのサポートの有効化  
 PXE、起動可能なメディア、または事前設定されたメディアを使用してオペレーティング システムを展開する場合、不明なコンピューターのサポートを有効にするには、次をご使用ください。  

-   **PXE**  

     配布ポイントを PXE に有効にするには、 **[PXE]** タブで **[不明なコンピューターのサポートを有効にする]** チェック ボックスをオンにします。 詳細については、「[PXE 要求を受け入れるための配布ポイントの構成](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)」を参照してください。  

-   **起動可能なメディア**  

     タスク シーケンス メディアの作成ウィザードの **[セキュリティ]** ページで、 **[不明なコンピューターのサポートを有効にする]** チェック ボックスをオンにします。 詳細については、[PXE 要求を受け入れるための配布ポイントの構成](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)に関する記事、および「[Configuration Manager で PXE を使用して Windows をネットワーク経由で展開する](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。  

-   **事前設定されたメディア**  

     タスク シーケンス メディアの作成ウィザードの **[セキュリティ]** ページで、 **[不明なコンピューターのサポートを有効にする]** チェック ボックスをオンにします。 詳細については、[Configuration Manager を使用した事前設定されたメディアの作成](../deploy-use/create-prestaged-media.md)に関する記事を参照してください。  
