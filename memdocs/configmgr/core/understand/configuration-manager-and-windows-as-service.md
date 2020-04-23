---
title: Configuration Manager とサービスとしての Windows
titleSuffix: Configuration Manager
description: サービスとしての Windows をサポートするために Configuration Manager の Current Branch を導入する場合の基本情報について説明します。
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701250"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager とサービスとしての Windows

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、Windows 10 の機能更新プログラムを包括的に制御できます。 サービス モデルとして Windows を完全に導入するには、Configuration Manager の Current Branch モデルを導入する必要もあります。 Windows 10 を最新の状態に保つには、最適なエクスペリエンスを実現するために Configuration Manager を最新の状態に保つ必要があります。 Windows 10 の魅力的な新しい企業の機能を最大限に活用するには、新しいバージョンの Configuration Manager が必要です。 この記事は、Configuration Manager の Current Branch を導入するために必要な主な記事のランディング ページとして提供されています。 Configuration Manager の Current Branch を準備してからサービスとしての Windows に進みます。

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Configuration Manager の Current Branch の導入に関する主な記事

| 記事        | [説明]          | 
| ------------- |-------------|
|[Configuration Manager Current Branch の概要](../plan-design/changes/whats-new-incremental-versions.md)|Configuration Manager (Current Branch) の新しいサービス モデルの要点を簡単に説明します。|
|[サポート ライフサイクル](../servers/manage/current-branch-versions-supported.md)|新しいサポートおよびサービス モデルについて説明します。|
|[削除された項目と非推奨の項目](../plan-design/changes/deprecated/removed-and-deprecated.md)|Configuration Manager の使用に影響する可能性のある将来の変更について早期に注意するものです。|
|[Configuration Manager Current Branch の更新](../servers/manage/updates.md)|Configuration Manager に機能更新プログラムを適用するための簡単なコンソール内の方式について説明します。|
|[利用可能な更新プログラムの取得](../servers/manage/install-in-console-updates.md#get-available-updates)|新しい Configuration Manager の機能更新プログラムを取得するために利用できる 2 つのモードについて説明します。|
|[更新プログラムのチェックリスト](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|更新プログラムのバージョン固有のチェックリスト (適用可能な場合) を提供します。| 
|[新しい Configuration Manager の機能更新プログラムのインストール](../servers/manage/install-in-console-updates.md#bkmk_install)|機能更新プログラムの簡単なインストール手順について説明します。|
|[Windows 10 のサポート](../plan-design/configs/support-for-windows-10.md)|Windows 10 (および ADK) バージョンのサポート マトリックスを提供します。|
|[Configuration Manager の Technical Preview](../get-started/technical-preview.md)|ConfigMgr テクニカル プレビュー プログラムに関する情報を提供します。|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>サービスとしての Windows の導入に関する主な記事

| 記事        | [説明]          |
| ------------- |-------------|
|[サービスとしての Windows の管理](../../osd/deploy-use/manage-windows-as-a-service.md)|サービス プランを使用して Windows 10 の機能更新プログラムを展開する方法について説明します。|
|[タスク シーケンスによる Windows 10 のアップグレード](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|追加の推奨事項で Windows 10 をアップグレードするためのタスク シーケンスの作成に関する詳細。|
|[段階的展開](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|段階的展開は、複数のコレクションでのタスク シーケンスの調整および順序付けされたロールアウトを自動化します。|  
|[Windows 10 更新プログラムの配信の最適化](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Configuration Manager を使用して、Windows 10 を最新の状態に保つための更新プログラムのコンテンツを管理します。|
|[Desktop Analytics の使用](../../desktop-analytics/overview.md)|Desktop Analytics を使用すると、Windows 10 にアップグレードするため、環境内のデバイスの対応性を評価および分析することができます。|
|[Windows Update for Business 統合 (オプション)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Configuration Manager を使用して、Windows Update for Business (WUfB) ポリシーを定義して展開する方法について説明します。|
|[Microsoft Intune と Windows Update for Business での共同管理の使用 (オプション)](../../comanage/overview.md)|共同管理の概要を示します。|


## <a name="related-articles"></a>関連記事

- [System Center 2012 Configuration Manager から Configuration Manager Current Branch へのインプレース アップグレード](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Configuration Manager Current Branch への移行を計画する](../migration/planning-for-migration.md)
