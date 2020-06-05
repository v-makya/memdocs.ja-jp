---
title: ファイルを含める
description: インクルード ファイル
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347258"
---
## <a name="apple-device-network-information"></a>Apple デバイス ネットワークの情報

|**使用目的**|**ホスト名 (IP アドレス/サブネット)**|**プロトコル**|**ポート**|
|------------|-----------|------------|-----------|
|Apple サーバーからコンテンツを取得して表示する|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|APNS サーバーとの通信|#-courier.push.apple.com<br>'#' は、0 から 50 の乱数です。|TCP|5223 および 443|
|各種の関数には、インターネット、iTunes Store、macOS アプリ ストア、iCloud、メッセージングなどへのアクセスが含まれます。|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 または 443|

詳細については、次をご覧ください。

- [Apple ソフトウェア製品に使用される TCP ポートと UDP ポート](https://support.apple.com/HT202944)
- [macOS、iOS/iPadOS、iTunes のサーバー ホスト接続と iTunes のバックグラウンド プロセスについて](https://support.apple.com/HT201999)
- [macOS および iOS/iPadOS クライアントで Apple プッシュ通知が届かない場合](https://support.apple.com/HT203609)