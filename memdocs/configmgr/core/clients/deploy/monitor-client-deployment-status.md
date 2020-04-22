---
title: クライアントの展開ステータスを監視する
titleSuffix: Configuration Manager
description: Configuration Manager でクライアントの展開ステータスを監視します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80cfa1576ae2cc4505147aee07a247e035b07ada
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693850"
---
# <a name="how-to-monitor-client-deployment-status-in-configuration-manager"></a>Configuration Manager でクライアントの展開ステータスを監視する方法

*適用対象:Configuration Manager (Current Branch)*

サイト全体にクライアントを展開するには時間がかかります。初回インストールが失敗することがあります。 Configuration Manager コンソールには、クライアント展開ステータスをリアルタイムで報告することによって、コレクション内のクライアントの展開を監視する方法が用意されています。  

> [!NOTE]  
>  クライアントの展開を監視するのに最も確実で最善の方法は、Configuration Manager コンソールを (この記事に説明されているとおりに) 使用することです。 コンソールの **[監視]** ワークスペースの **[クライアント ステータス]** セクションに、クライアントの展開ステータスが正確にリアルタイムで表示されます。 Windows Server のサーバー マネージャーや System Center Operations Manager といった他のツールを使用してクライアントの展開を監視することはできますが、通常のクライアント インストールのアクティビティからアラームを受信する可能性があります。 クライアントのインストール プログラム (CCMSetup.exe) がさまざまな環境でどのように実行されるかによって、クライアントの展開の状態を正確に反映していない誤ったアラームと警告がこれらの他のツールによって生成されることがあります。  

 指定したコレクション内で実行されているクライアントの展開について、コンソールの **[監視]** ワークスペースで次のステータスを監視することができます。  

- [準拠]  

- 進行中  

- 非対応  

- Failed  

- Unknown  

  Configuration Manager は、実稼働クライアントや実稼働前クライアント展開について報告します。 Configuration Manager コンソールには、ユーザーが展開の問題を解決するために実行するアクションによって展開の成功率が徐々に改善しているかどうかを確認できるように、指定期間に失敗したクライアントの展開のグラフも表示されます。  

## <a name="to-monitor-client-deployments"></a>クライアントの展開を監視するには  

- Configuration Manager コンソールで、 **[監視]**  >  **[クライアントのステータス]** の順にクリックします。  

- 監視するクライアントのバージョンに応じて、 **[実稼働クライアント展開]** または **[実稼働前クライアント展開]** をクリックします。  

- クライアント展開ステータスとクライアント展開エラーのグラフを確認します。  

- レポートのスコープを変更する場合は、 **[参照...]** をクリックして、別のコレクションを選択します。  

  実稼働前クライアント展開の詳細については、[実稼働前コレクションのクライアント アップグレードをテストする方法](../../../core/clients/manage/upgrade/test-client-upgrades.md)に関するページを参照してください。

  > [!NOTE]
  > 実稼働前コレクションでサイト システムの役割をホストしているコンピューターの展開ステータスは、クライアントが正常に展開された場合でも、**非対応**と報告されることがあります。 クライアントを実稼働環境に昇格すると、展開のステータスが正しく報告されます。   

  展開されたクライアントのステータスを監視するには、[クライアントを監視する方法](../../../core/clients/manage/monitor-clients.md)に関するページを参照してください。  

  Configuration Manager レポートで、サイトのクライアント ステータスについての追加情報を確認できます。 レポートの実行方法の詳細については、[レポートの概要](../../servers/manage/introduction-to-reporting.md)に関するページを参照してください。  
