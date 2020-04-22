---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697930"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a> ハードウェア インベントリのレポート

<!--5468413-->
ハードウェア インベントリに依存しているレポートを実行しようとすると、エラーが返されます。 たとえば、BitLocker レポートでは、次のようなエラーが返されます。

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

**dataldr.log** ファイルに次のエラーが表示される場合もあります。

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

ハードウェア インベントリに依存しているコンソール ダッシュボードも影響を受ける可能性があります。

この問題は、特定のハードウェア インベントリ テーブルでデータベース スキーマが変更されたことが原因で発生します。

#### <a name="workaround"></a>回避策

回避策として、データベースから既存の属性を削除します。 これにより、dataloader サイト コンポーネントで新しい属性を作成できます。 サイト データベース サーバーで次の SQL スクリプトを実行して、テーブル スキーマを修正します。

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
