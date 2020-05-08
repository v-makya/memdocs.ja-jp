---
title: 診断結果と使用状況データ
titleSuffix: Configuration Manager
description: Configuration Manager が収集する、それ自体の診断結果と使用状況データについて説明します。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904393"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Configuration Manager の診断結果と使用状況データ

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、それ自体の診断および使用状況データが収集されます。このデータは、今後のリリースでインストールのエクスペリエンス、品質、セキュリティを向上させるために Microsoft によって使用されます。  

診断結果および使用状況データは、それぞれの Configuration Manager 階層で有効になります。 これは、各プライマリ サイトと中央管理サイト (CAS) で毎週実行される SQL Server クエリで構成されます。 階層で CAS が使用されている場合、子プライマリ サイトのデータがその CAS にレプリケートされます。 階層の最上位のサイトでは、[サービス接続ポイント](../../servers/deploy/configure/about-the-service-connection-point.md)で更新プログラムがチェックされるときに、この情報が送信されます。 サービス接続ポイントがオフライン モードの場合は、[サービス接続ツール](../../servers/manage/use-the-service-connection-tool.md)を使用して情報を転送します。

> [!NOTE]  
> Configuration Manager は、サイトの SQL Server データベースからのみデータを収集します。クライアントやサイト サーバーから直接データを収集することはありません。  

詳細については、「[Microsoft のプライバシーに関する声明](https://privacy.microsoft.com/privacystatement)」を参照してください。  

> [!div class="nextstepaction"]
> [Microsoft での診断結果と使用状況データの使用方法](how-diagnostics-and-usage-data-is-used.md)
