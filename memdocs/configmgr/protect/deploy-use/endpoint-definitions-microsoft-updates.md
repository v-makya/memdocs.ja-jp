---
title: Microsoft からの定義のダウンロード
titleSuffix: Configuration Manager
description: Configuration Manager で Endpoint Protection のマルウェア定義を Microsoft Update からダウンロードできるようにする方法について説明します。
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697240"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Endpoint Protection のマルウェア定義を Microsoft Update からダウンロードできるようにする

*適用対象:Configuration Manager (Current Branch)*

定義ファイルの更新を Microsoft Update からダウンロードするように選択した場合、クライアントによって、マルウェア対策ポリシーのダイアログ ボックスの **[セキュリティ インテリジェンスの更新]** セクションで定義した間隔で Microsoft Update サイトがチェックされます。

 この方法は、クライアントが Configuration Manager サイトに接続されていない場合、またはユーザーから定義ファイルの更新を開始できるようにする場合に役立ちます。

> [!IMPORTANT]
> - この方法を使用して定義ファイルの更新をダウンロードするには、クライアントがインターネット経由で Microsoft Update にアクセスできなければなりません。
> - **[定義の更新]** セクションは、Configuration Manager バージョン 1902 から、 **[セキュリティ インテリジェンスの更新]** に名前変更されました。

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Microsoft マルウェア プロテクション センターを使用して定義ファイルをダウンロードするには
 Microsoft マルウェア プロテクション センターから、定義ファイルの更新をダウンロードできるようにクライアントを構成することができます。 Endpoint Protection クライアントは、別のソースから更新をダウンロードできない場合に、このオプションを使用して定義ファイルの更新をダウンロードします。 この更新方法は、Configuration Manager インフラストラクチャに更新ファイルの配布を妨げる問題がある場合に役立ちます。

> [!IMPORTANT]
>  この方法を使用して定義ファイルの更新をダウンロードするには、クライアントがインターネット経由で Microsoft Update にアクセスできなければなりません。
> 
> 
> [!div class="button"]
> [次のステップ >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [戻る >](endpoint-configure-alerts.md)
