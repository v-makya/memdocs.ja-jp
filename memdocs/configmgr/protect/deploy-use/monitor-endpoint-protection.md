---
title: Endpoint Protection の状態を監視する
titleSuffix: Configuration Manager
description: Configuration Manager 階層内の Endpoint Protection を監視する方法を説明します。
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 18bbbfc6486a1e5a784603e6725629d966f6c11a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706280"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Endpoint Protection 状態を監視する方法

*適用対象:Configuration Manager (Current Branch)*

**[監視]** ワークスペースの **[セキュリティ]** の **[Endpoint Protection のステータス]** ノード、 **[資産とコンプライアンス]** ワークスペースの **[Endpoint Protection]** ノード、レポートを使用して、Microsoft Configuration Manager 階層内の Endpoint Protection を監視できます。  

##  <a name="how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a> [Endpoint Protection のステータス] ノードを使用して Endpoint Protection を監視する方法  

1. Configuration Manager コンソールで、 **[監視]** をクリックします。  

2. **[監視]** ワークスペースで **[セキュリティ]** を展開し、 **[Endpoint Protection のステータス]** をクリックします。  

3. **[コレクション]** 一覧で、ステータス情報を確認するコレクションを選択します。  

   > [!IMPORTANT]
   >  コレクションは、次のような場合に選択できます。  
   > 
   > - **[<<em>コレクション名</em>\> のプロパティ]** ダイアログ ボックスの **[アラート]** タブで **[このコレクションを Endpoint Protection ダッシュボードに表示する]** を選択するとき。  
   >   -   Endpoint Protection マルウェア対策ポリシーをコレクションに展開するとき。  
   >   -   Endpoint Protection クライアントの設定をコレクションに対して有効にして展開するとき。  

4. 表示される情報を確認して、 **セキュリティ状態** と **操作状態** セクションです。 一時的なコレクションを作成する任意のステータス リンクをクリックすることができます、 **デバイス** 内のノード、 **資産とコンプライアンス** ワークスペース。 一時コレクションには、選択したステータスのコンピューターが含まれます。  

   > [!IMPORTANT]  
   >  **[Endpoint Protection のステータス]** ノードに表示される情報は、Configuration Manager データベースからまとめられた最終データに基づいていて、最新ではない可能性があります。 最新のデータを取得するには、 **[ホーム]** タブの **[構成基準の概要]** をクリックするか、 **[概要作成スケジュール]** をクリックして、概要構成間隔を調整します。  

##  <a name="how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a> [資産とコンプライアンス] ワークスペースで Endpoint Protection を監視する方法  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** をクリックします。  

2.  **[資産とコンプライアンス]** ワークスペースで、次のいずれかの操作を実行します。  

    -   **[デバイス]** をクリックします。 **デバイス** ボックスの一覧、コンピューターを選択し、クリックして、 **マルウェアの詳細** タブです。  

    -   **[デバイス コレクション]** をクリックします。 **デバイス コレクション** ボックスの一覧で、監視対象のコンピュータを含んでいるコレクションを選択し、、 **ホーム**  タブで、 **コレクション** グループで、 **メンバーの表示**です。  

3.  [<*コレクション名*\>] の一覧で、コンピューターを選択し、 **[マルウェアの詳細]** タブをクリックします。  

##  <a name="how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a> レポートを使用して Endpoint Protection を監視する方法  
 階層にある Endpoint Protection の情報を表示するには、次のレポートを使用します。 Endpoint Protection に問題があれば、これらのレポートを使用して、トラブルシューティングを行うこともできます。 Configuration Manager でのレポートの構成方法について詳しくは、[レポートの概要](../../core/servers/manage/introduction-to-reporting.md)と[ログ ファイル](../../core/plan-design/hierarchy/log-files.md)に関するページを参照してください。 Endpoint Protection レポートは、Endpoint Protection フォルダーにあります。  

|レポート名|[説明]|  
|-----------------|-----------------|  
|**マルウェア対策アクティビティ レポート**|指定したコレクションのマルウェア対策アクティビティを表示します。|  
|**感染したコンピューター**|指定された脅威が検出されたコンピューターの一覧を表示します。|  
|**上位ユーザー (脅威別)**|検出された脅威数が最も多いユーザーの一覧を表示します。|  
|**ユーザーの脅威リスト**|指定されたユーザー アカウントで検出された脅威の一覧を表示します。|  

## <a name="malware-alert-levels"></a>マルウェア アラートのレベル  
 レポートまたは Configuration Manager コンソールに表示される可能性のある Endpoint Protection の各種アラート レベルを、次の表に示します。  

|アラート レベル|[説明]|  
|-----------------|-----------------|  
|**失敗**|Endpoint Protection がマルウェアの修復に失敗しました。 エラーの詳細については、ログを確認します。<br /><br /> **注:** Configuration Manager および Endpoint Protection のログ ファイルの一覧については、[ログ ファイル](../../core/plan-design/hierarchy/log-files.md)のトピックの「Endpoint Protection」セクションを参照してください。|  
|**削除済み**|Endpoint Protection がマルウェアを正常に削除しました。|  
|**検疫済み**|Endpoint Protection がマルウェアを安全な場所に移動したため、マルウェアを削除するか、その実行を許可するまで、実行されることはありません。|  
|**除去済み**|マルウェアは、ウイルスに感染したファイルから消去されました。|  
|**許可されます。**|管理ユーザーを実行するには、そのマルウェアが含まれているソフトウェアの許可を選択します。|  
|**何もしません。**|Endpoint Protection はマルウェアに対して何も実行しませんでした。 これは、マルウェアが検出され、マルウェアが検出された不要になった後に、コンピューターが再起動した場合に発生する可能性があります。たとえば、マップ済みネットワーク ドライブに場合どのマルウェアが検出されたが再接続されなかった場合、コンピューターを再起動するときにします。|  
|**［ブロック済み］**|Endpoint Protection がマルウェアの実行をブロックしました。 これは、マルウェアを格納する、コンピューター上のプロセスが見つかった場合に発生する可能性があります。|
