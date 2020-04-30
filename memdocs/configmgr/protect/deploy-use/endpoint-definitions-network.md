---
title: ネットワーク共有からの定義のダウンロード
titleSuffix: Configuration Manager
description: Microsoft から最新の定義ファイルの更新を手動でダウンロードし、これらの定義をダウンロードするようにクライアントを構成する方法について説明します。
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697230"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>Endpoint Protection のマルウェア定義をネットワーク共有からダウンロードできるようにする

*適用対象:Configuration Manager (Current Branch)*

 Microsoft から最新の定義ファイルの更新を手動でダウンロードし、ネットワーク上の共有フォルダーからこれらの定義をダウンロードするようにクライアントを構成できます。 この更新ソースを使用する場合、ユーザーは定義ファイルの更新も開始できます。

> [!NOTE]
>  クライアントは、定義ファイルの更新をダウンロードするために、共有フォルダーへの読み取りアクセス権が必要です。

 定義とエンジンの更新プログラムをダウンロードしてファイル共有に保存する方法の詳細については、「[Install the latest Microsoft antimalware and antispyware software](https://www.microsoft.com/wdsi/definitions)」 (最新の Microsoft マルウェア対策およびスパイウェア対策ソフトウェアのインストール) をご覧ください。

## <a name="to-configure-definition-downloads-from-a-file-share"></a>ファイル共有からの定義ファイルのダウンロードを構成するには

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** をクリックします。

2.  **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、 **[マルウェア対策ポリシー]** をクリックします。

3.  **[既定のマルウェア対策ポリシー]** プロパティ ページを開くか、新しいマルウェア対策ポリシーを作成します。 マルウェア対策ポリシーを作成する方法の詳細については、「[System Center Configuration Manager で Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)」を参照してください。

4.  マルウェア対策プロパティ ダイアログ ボックスの **[セキュリティ インテリジェンスの更新]** セクションで **[ソースの設定]** をクリックします。
    - **[定義の更新]** セクションは、Configuration Manager バージョン 1902 から、 **[セキュリティ インテリジェンスの更新]** に名前変更されました。

5.  **[定義ファイルの更新ソースの構成]** ダイアログ ボックスで、 **[UNC ファイル共有から更新する]** を選びます。

6.  **[OK]** をクリックして **[定義ファイルの更新ソースの構成]** ダイアログ ボックスを閉じます。

7.  **[パスの設定]** をクリックします。 次に、 **[定義更新プログラム用 UNC パスの構成]** ダイアログ ボックスで、ネットワーク共有上の定義ファイルの更新ファイルの場所を示す UNC パスを 1 つまたは複数追加します。

8.  **[OK]** をクリックして **[定義更新プログラム用 UNC パスの構成]** ダイアログ ボックスを閉じます。


> [!div class="button"]
> [次のステップ >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [戻る >](endpoint-configure-alerts.md)
