---
title: クライアントをアップグレードする
titleSuffix: Configuration Manager
description: Configuration Manager でクライアントをアップグレードする方法について説明します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 40fc094d6c1a1acbd31f1d26e6fe6617972f8da5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696240"
---
# <a name="upgrade-clients-in-configuration-manager"></a>Configuration Manager でクライアントをアップグレードする

*適用対象:Configuration Manager (Current Branch)*

Windows コンピューター、UNIX/Linux サーバー、Mac コンピューターで Configuration Manager クライアント ソフトウェアをアップグレードするには、さまざまな方法があります。 各方法の利点と欠点の詳細について以下に説明します。  

> [!TIP]  
>  Configuration Manager の以前のバージョン \(Configuration Manager 2007 または System Center 2012 Configuration Manager など\) から、サーバー インフラストラクチャをアップグレードする場合は、Configuration Manager クライアントをアップグレードする前に、現在のすべてのブランチの更新プログラムのインストールを含む、サーバーのアップグレードを完了することをお勧めします。 これにより、クライアント ソフトウェアの最新バージョンも使用できます。  

## <a name="group-policy-installation"></a>グループ ポリシーによるインストール  
 **サポートされるクライアント プラットフォーム:** Windows  

#### <a name="advantages"></a>長所  

- クライアントをアップグレードする前に、コンピューターが検出されている必要はありません。  

- 新しいクライアントのインストールまたは更新で使用できます。  

- コンピューターは、Active Directory ドメイン サービスに公表されたクライアント インストール プロパティを読み取ることができます。  

- 目的のクライアント コンピューターのインストール アカウントを構成してメンテナンスを行う必要はありません。  

#### <a name="disadvantages"></a>短所  

- 多数のクライアントをアップグレードする場合、大量のネットワーク トラフィックを発生させる可能性があります。  

- Active Directory スキーマが Configuration Manager 向けに拡張されていない場合、[グループ ポリシー設定](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP)を使用してサイト内のコンピューターにクライアント インストール プロパティを追加する必要があります。  


## <a name="logon-script-installation"></a>ログオン スクリプトによるインストール  
 **サポートされるクライアント プラットフォーム:** Windows  

#### <a name="advantages"></a>長所  

- クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

- 新しいクライアントのインストールまたは更新で使用できます。  

- CCMSetup のコマンド ライン プロパティを使用してサポートします。  

#### <a name="disadvantages"></a>短所  

- 多数のクライアントをアップグレードする場合、短時間で大量のネットワーク トラフィックを発生させる可能性があります。  

- ユーザーがネットワークに頻繁にログオンしない場合は、すべてのクライアント コンピューターでアップグレードするのに長時間かかる場合があります。  

  詳細については、「[ログオン スクリプトを使用した Configuration Manager クライアントのインストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript)」を参照してください。  

## <a name="manual-installation"></a>手動インストール  
 **サポートされるクライアント プラットフォーム:** Windows、UNIX/Linux、Mac OS X  

#### <a name="advantages"></a>長所  

- クライアントをアップグレードする前に、コンピューターが検出されている必要はありません。  

- テストの目的で役立ちます。  

- CCMSetup のコマンド ライン プロパティを使用してサポートします。  

#### <a name="disadvantages"></a>短所  

- 自動化されていないため、時間を削減できます。  

  詳細については、以下のトピックを参照してください。  

- [Configuration Manager クライアントの手動インストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Linux および UNIX サーバーのクライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Mac コンピューター上のクライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>アップグレード インストール (アプリケーション管理)  
 **サポートされるクライアント プラットフォーム:** Windows  

> [!NOTE]  
>  この方法では、Configuration Manager 2007 クライアントをアップグレードすることはできません。 このシナリオでは、Configuration Manager 2007 サイトからのパッケージとして Configuration Manager クライアントを展開したり、自動クライアント アップグレードを使用して、最新バージョンのクライアントを含むパッケージを自動的に作成して展開したりできます。  

#### <a name="advantages"></a>長所  

- CCMSetup のコマンド ライン プロパティを使用してサポートします。  

#### <a name="disadvantages"></a>短所  

- 大規模なコレクションに対してクライアントを配布する場合、ネットワーク トラフィックの量が増大する可能性があります。  

- サイトで探索または割り当てられたコンピューター上のクライアント ソフトウェアをアップグレードするときのみ使用できます。  

  詳細については、「[パッケージとプログラムを使用した Configuration Manager クライアントのインストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp)」を参照してください。  

## <a name="automatic-client-upgrade"></a>自動クライアント アップグレード  

> [!NOTE]  
> Configuration Manager 2007 クライアントを Configuration Manager Current Branch クライアントにアップグレードするために使用できます。 Configuration Manager 2007 クライアントは Configuration Manager サイトに割り当てることができますが、自動クライアント アップグレード以外の操作は実行できません。  

 **サポートされるクライアント プラットフォーム:** Windows  

#### <a name="advantages"></a>長所  

- 指定した期間ランダム化されるため、大規模なクライアントのアップグレードに適しているのは自動アップグレードのみです。 他の方法は大規模なアップグレードには遅すぎるか、ランダム化がありません。 

    > [!Note]
    > クライアントのパイロット テストは、まったくランダム化されないので大規模には適していません。  
- サイト内のクライアントを自動的に最新バージョンに保つのに使用できます。  

- 最小限の管理が必要です。  

#### <a name="disadvantages"></a>短所  

- クライアント ソフトウェアのアップグレードにのみ使用できます。新しいクライアントのインストールには使用できません。  

- サイトに関連付けられた階層内のすべてのクライアントに対して適用します。 コレクションでスコープを設定することはできません。  

- スケジュール オプションは限定されています。  

  詳細については、「[Windows コンピューター用クライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)」を参照してください。  

## <a name="client-testing"></a>クライアントのテスト  
 **サポートされるクライアント プラットフォーム:** Windows  

#### <a name="advantages"></a>長所  

- 小規模な実稼働前環境コレクションで新しいクライアント バージョンをテストするために使用できます。  

- テストが完了すると、実稼働前環境のクライアントは実稼働環境に昇格され、Configuration Manager サイト全体で自動的にアップグレードされます。  

#### <a name="disadvantages"></a>短所  

- クライアント ソフトウェアのアップグレードにのみ使用できます。新しいクライアントのインストールには使用できません。  

  [実稼働前コレクションのクライアント アップグレードをテストする方法](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
