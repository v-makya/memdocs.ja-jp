---
title: Wi-Fi と VPN プロファイルの前提条件
titleSuffix: Configuration Manager
description: Configuration Manager で Wi-Fi プロファイルと VPN プロファイルを管理するための前提条件について説明します。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706070"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager の Wi-Fi および VPN プロファイルの前提条件

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の Wi-Fi プロファイルおよび VPN プロファイルには、製品内の依存関係のみがあります。

証明書プロファイル、Wi-Fi プロファイル、VPN プロファイルなどの会社のリソースのアクセス設定を管理するには、次のセキュリティのアクセス許可が必要です。  

- Wi-Fi とプロファイルのアラートとレポートを表示して管理する: **[アラート]** オブジェクトの **[作成]** 、 **[削除]** 、 **[変更]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。  

- 証明書プロファイルを作成して管理する: **[証明書プロファイル]** オブジェクトの **[作成者ポリシー]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。  

- Wi-Fi プロファイル、証明書プロファイル、VPN プロファイルの展開を管理する: **[コレクション]** オブジェクトの **[構成ポリシーの展開]** 、 **[クライアント ステータス アラートの変更]** 、 **[読み取り]** 、 **[リソースの読み取り]** 。  

- すべての構成ポリシーを管理する: **[構成のポリシー]** オブジェクトの **[作成]** 、 **[削除]** 、 **[変更]** 、 **[読み取り]** 、 **[セキュリティ スコープの設定]** 。  

- Wi-Fi とプロファイルに関連するクエリを実行する: **[クエリ]** オブジェクトの **[読み取り]** アクセス許可。  

- Configuration Manager コンソールで Wi-Fi および VPN プロファイルの情報を表示する: **[サイト]** オブジェクトの **[読み取り]** アクセス許可。  

- Wi-Fi とプロファイルのステータス メッセージを表示する: **[ステータス メッセージ]** オブジェクトの **[読み取り]** アクセス許可。  

- 信頼された証明機関証明書プロファイルを作成および変更する: **[信頼された証明機関証明書プロファイル]** オブジェクトの **[作成者ポリシー]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。  

- VPN プロファイルを作成して管理する: **[VPN プロファイル]** オブジェクトの **[作成者ポリシー]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。  

- Wi-Fi プロファイルを作成して管理する: **[Wi-Fi プロファイル]** オブジェクトの **[作成者ポリシー]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。  

**[会社リソース アクセス マネージャー]** 組み込みセキュリティ ロールには、Configuration Manager で Wi-Fi プロファイルを管理するのに必要な上記のアクセス許可が付与されています。 詳細については、「[セキュリティの構成](../../core/plan-design/security/configure-security.md)」をご覧ください。
