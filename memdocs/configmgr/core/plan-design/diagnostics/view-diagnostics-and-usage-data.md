---
title: 診断データを表示する
titleSuffix: Configuration Manager
description: 診断および使用状況データを表示して、Configuration Manager 階層に機密情報が含まれていないことを確認します。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 993a3549ddca4c2b5ae1dbbfc0346f28b9c3083e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692740"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Configuration Manager の診断と使用状況データを表示する方法

*適用対象:Configuration Manager (Current Branch)*

診断と使用状況データを Configuration Manager 階層から表示し、機密情報や個人情報が含まれていないことを確認できます。 サイトでは、診断データがまとめられ、サイト データベースの **TEL_TelemetryResults** テーブルに格納されます。 データはプログラムで利用できるように、かつ効率的になるようにフォーマットされます。

この記事の情報は、Microsoft に送信されるデータを寸分の違いなく提示するものです。 データ分析など、その他の用途は意図されていません。  

## <a name="view-data-in-database"></a>データベース内のデータを表示する

このテーブルの内容を表示し、送信される正確なデータを表示するには、次の SQL コマンドを使用します。  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>データをエクスポートする

サービス接続ポイントがオフライン モードの場合、サービス接続ツールを使用し、現在のデータをコンマ区切り値 (CSV) ファイルにエクスポートします。 サービス接続ポイントで **-Export** パラメーターを使用してサービス接続ツールを実行します。

詳細については、[サービス接続ツールの使用](../../servers/manage/use-the-service-connection-tool.md)に関するページを参照してください。

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a> 一方向のハッシュ

一部のデータは、任意の英数字の文字列で構成されています。 Configuration Manager では SHA-256 アルゴリズムを使用し、一方向のハッシュが作成されます。 このプロセスにより、機密の可能性があるデータを Microsoft が収集することはありません。 ハッシュされたデータは、関連付けと比較のために利用できます。

たとえば、サイト データベースのテーブルの名前を収集するのではなく、テーブル名ごとに一方向のハッシュがキャプチャされます。 この動作により、あらゆるカスタム テーブル名が非表示になります。 Microsoft はその後、既定の SQL テーブル名を同じく一方向でハッシュします。 2 つのクエリの結果を比較すると、製品既定から測った、データベース スキーマの偏差が決定されます。 この情報はその後、SQL スキーマの変更が必要な更新プログラムの向上に役立てられます。  

生データを表示すると、共通のハッシュ値がデータの各行に表示されます。 このハッシュは階層 ID です。 この値は、顧客またはソースを特定せずに、同じ階層内のデータを関連付けるのに使用されます。

### <a name="how-the-one-way-hash-works"></a>一方向ハッシュのしくみ

1. 階層 ID は、SQL Management Studio で Configuration Manager データベースに対して SQL クエリを実行することで取得します。

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. 次の Windows PowerShell スクリプトを使用し、階層 ID を一方向でハッシュします。  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. スクリプトの出力を生データの GUID と比較します。 このプロセスからは、データを隠すしくみがわかります。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [診断と使用状況データのレベル](levels-overview.md)
