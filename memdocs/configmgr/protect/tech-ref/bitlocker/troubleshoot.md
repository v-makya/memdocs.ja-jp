---
title: BitLocker のトラブルシューティング
titleSuffix: Configuration Manager
description: Configuration Manager での BitLocker の管理に関する問題をトラブルシューティングする方法について説明します
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708610"
---
# <a name="troubleshoot-bitlocker"></a>BitLocker のトラブルシューティング

*適用対象:Configuration Manager (Current Branch)*

この記事の情報は、Configuration Manager での BitLocker の管理に関する問題をトラブルシューティングするのに役立ちます。

## <a name="server-error-in-self-service"></a>セルフサービスでのサーバー エラー

セルフサービス ポータル (`https://webserver.contoso.com/SelfService`) を初めて開こうとすると、次のエラー メッセージが表示されます。

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

この問題を解決するには、Web サーバーに **Microsoft ASP.NET MVC 4.0** の[前提条件](../../plan-design/bitlocker-management.md#prerequisites)がインストールされていることを確認してください。

## <a name="see-also"></a>関連項目

BitLocker イベント ログの使用の詳細については、「[BitLocker イベント ログ](about-event-logs.md)」を参照してください。

イベント ログ エントリの既知のエラーと考えられる原因の一覧については、次の記事を参照してください。

- [クライアント イベント ログ](client-event-logs.md)
- [サーバー イベント ログ](server-event-logs.md)

クライアントから BitLocker 管理ポリシーに準拠していないと報告される理由については、「[非コンプライアンス コード](non-compliance-codes.md)」をご覧ください。
