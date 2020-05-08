---
title: Configuration Manager とは
titleSuffix: Configuration Manager
description: Microsoft Endpoint Configuration Manager の基本を説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c3be302ecefad36d7be8617a4cc9354db1b685
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906072"
---
# <a name="what-is-configuration-manager"></a>Configuration Manager とは

*適用対象:Configuration Manager (Current Branch)*

バージョン 1910 以降、Configuration Manager は Microsoft Endpoint Manager の一部になりました。

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager は、すべてのデバイスを管理するための統合ソリューションです。 Microsoft は、複雑な移行を行わず、ライセンスを簡素化して、Configuration Manager と Intune を統合しました。 既存の Configuration Manager の投資を引き続き活用しながら、Microsoft クラウドの機能をご自分のペースで利用できます。

次の Microsoft 管理ソリューションは、すべて **Microsoft Endpoint Manager** ブランドの一部になりました。

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- [デバイス管理の管理コンソール](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)に含まれるその他の機能

詳細については、「[Microsoft Endpoint Configuration Manager のよくあるご質問](microsoft-endpoint-manager-faq.md)」を参照してください。

## <a name="introduction"></a>概要

Configuration Manager を使用すると、次のシステム管理作業に役立ちます。

- 手動のタスクを削減し、価値の高いプロジェクトに重点を置くことができるようにすることによって、IT スタッフの生産性と効率を向上させる。  
- ハードウェアとソフトウェアの投資を最大限活かす。  
- 適切なタイミングで適切なソフトウェアを提供することによってユーザーの生産性を高める。  

Configuration Manager で以下を有効にすると、より効果的な IT サービスを提供するのに役立ちます。

- アプリケーション、ソフトウェア更新プログラム、オペレーティング システムの安全でスケーラブルな展開。
- マネージド デバイスに対するリアルタイムのアクション。
- オンプレミスとインターネットベースのデバイスの、クラウドを利用した分析と管理。
- コンプライアンス設定の管理。  
- サーバー、デスクトップ、ラップトップの包括的な管理。

Configuration Manager は、多くの Microsoft テクノロジやソリューションと共に拡張し、機能します。 たとえば、Configuration Manager は以下と統合されています。  

- Microsoft Intune (さまざまなモバイル デバイス プラットフォームを協働管理)
- Microsoft Azure (クラウド サービスをホストして管理サービスを拡張)
- Windows Server Update Services (WSUS) (ソフトウェアの更新を管理)
- 証明書サービス
- Exchange Server および Exchange Online
- グループ ポリシー
- DNS
- Windows 自動展開キット (Windows ADK) およびユーザー状態移行ツール (USMT)
- Windows 展開サービス (WDS)
- リモート デスクトップおよびリモート アシスタンス

Configuration Manager は以下も使用します。  

- セキュリティ、サービスの場所、構成、管理対象のユーザーとデバイスの探索に、Active Directory Domain Services と Azure Active Directory を使用します。  
- Microsoft SQL Server を分散型の変更管理データベースとして使用し、SQL Server Reporting Services (SSRS) と統合することで、管理アクティビティを監視および追跡するためのレポートを作成できます。  
- 管理機能を提供するサイト システムの役割、およびインターネット インフォメーション サービス (IIS) の Web サービスを使用します。
- 配信の最適化、Windows Low Extra Delay Background Transport (LEDBAT)、バックグラウンド インテリジェント転送サービス (BITS)、BranchCache、その他のピア キャッシュ テクノロジを使用して、ネットワーク上のコンテンツやデバイス間の管理を支援します。

運用環境で Configuration Manager を適切に使用するには、管理機能の計画とテストを十分に行います。 Configuration Manager は強力な管理アプリケーションのため、組織内のすべてのコンピューターに影響する可能性があります。 ビジネス要件に沿って十分な計画を行ってから Configuration Manager を展開および管理すれば、Configuration Manager で管理オーバーヘッドと総所有コストを削減することができます。  

## <a name="user-interfaces"></a>ユーザー インターフェイス

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> Configuration Manager コンソール

Configuration Manager をインストールしたら、Configuration Manager コンソールを使用して、サイトとクライアントを構成し、管理タスクを実行および監視します。 このコンソールは管理の中核であり、このコンソールで複数のサイトを管理できます。  

追加のコンピューターに Configuration Manager コンソールをインストールし、Configuration Manager の役割に基づいた管理権限で、アクセスを制限したり、コンソールで管理ユーザーが表示できる内容を制限したりできます。  

詳細については、[Configuration Manager コンソールの使用](../servers/manage/admin-console.md)に関する記事を参照してください。

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a> ソフトウェア センター

**ソフトウェア センター**は、Configuration Manager クライアントを Windows デバイスにインストールするとインストールされるアプリケーションです。 ユーザーはソフトウェア センターを使用して、展開されるソフトウェアの要求とインストールを行います。 ソフトウェア センターにより、ユーザーは次のアクションを行うことができます。  

- アプリケーション、ソフトウェア更新プログラム、新しい OS バージョンの参照とインストール
- 自身のソフトウェア要求履歴の表示
- 組織のポリシーに対するデバイスのコンプライアンスの表示

追加のビジネス要件を満たすため、ソフトウェアセンターにカスタム タブを表示することもできます。

詳細については、「[Security Center のユーザー ガイド](software-center.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

Configuration Manager をインストールする前に、基本的な概念と用語を理解するようにしてください。

- System Center 2012 Configuration Manager についてよく理解している場合は、「[System Center 2012 から Configuration Manager の変更点](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md)」を参照してください。

- Configuration Manager の技術の概要については、「[Configuration Manager の基本](fundamentals.md)」を参照してください。

基本的な概念を理解している場合は、このドキュメント ライブラリを使用すると、Configuration Manager を適切に展開して使用するのに役立ちます。 次の記事から始めてください。

- [Configuration Manager の特徴と機能](../plan-design/changes/features-and-capabilities.md)  
- [デバイス管理ソリューションの選択](../plan-design/choose-a-device-management-solution.md)  
- [独自のラボ環境を構築して Configuration Manager を評価する](../get-started/set-up-your-lab.md)
- [Configuration Manager の使用に関するヘルプの検索](find-help.md)  
