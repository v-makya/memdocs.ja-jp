---
title: サイト システムの役割を追加する
titleSuffix: Configuration Manager
description: Configuration Manager サイト システムの役割について説明すると共に、それらの役割を追加してサイトの機能と処理能力を拡張する方法について説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8a4ef1c4377e7b5ffba4ab0f04394ff1253c40df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704900"
---
# <a name="add-site-system-roles-for-configuration-manager"></a>Configuration Manager のサイト システム役割の追加

*適用対象:Configuration Manager (Current Branch)*

サイト システムの役割は、1 つの Configuration Manager サイトにつき複数利用することができます。 サイトにサービスを提供したりデバイスとユーザーを管理したりするうえで必要となるサイトの機能や処理能力は、それぞれの役割によって拡張することになります。 1 つのサイト システム サーバーのそれぞれのサイト システムの役割は、同じサイトにある必要があります。

Configuration Manager では、単一のサイト システム サーバーで、複数のサイトのためにサイト システムの役割を使用することはサポートされません。

> [!TIP]
> サイト システムの役割の基本や、サイト サーバー、サイト システム サーバー、サイト システムの役割の相違点についてあまり詳しくない場合は、「[Configuration Manager の基本](../../../understand/fundamentals.md)」をご覧ください。

以下の記事には、サイト システムの役割をインストールするための手順と、関連する詳細情報が詳述されています。

- [サイト システムの役割のインストール](install-site-system-roles.md):新しいサイト システムの役割をインストールする 2 つのコンソール内ウィザードの使用方法に関する基本的ガイダンス。

- [クラウドベースの配布ポイントのインストール](install-cloud-based-distribution-points-in-microsoft-azure.md):Microsoft Azure を使用して、クライアントに展開するコンテンツをホストします。

- [オンプレミス モバイル デバイス管理 (MDM) のサイト システムの役割のインストール](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md):Configuration Manager オンプレミス MDM を使用して新しいデバイスの管理をサポートする、サイト システムの役割を設定します。

- [サイト システムの役割の構成オプション](configuration-options-for-site-system-roles.md):サイト システムの一部の役割は、ユーザー インターフェイス内で説明可能な詳細情報を必要とする構成をサポートします。

- [サイト システムの役割の削除](../install/uninstall-sites-and-hierarchies.md#bkmk_role):サイト システム サーバーから役割を削除するためのガイダンスと手順。
