---
title: アプリケーションの管理タスク
titleSuffix: Configuration Manager
description: Configuration Manager アプリケーションおよび展開の種類を管理します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0896204fa994643064676b55b20d63d349c4098b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689300"
---
# <a name="management-tasks-for-configuration-manager-applications"></a>Configuration Manager アプリケーションの管理タスク

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager アプリケーションと展開の種類を管理する方法を説明します。  

アプリケーションと展開の種類の作成については、「[Create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md)」 (System Center Configuration Manager でアプリケーションを作成する) を参照してください。  

> [!IMPORTANT]  
>  アプリケーションの種類または展開の種類によっては、使用できない管理オプションがあります。  

##  <a name="manage-applications"></a>アプリケーションを管理する  
 **[ソフトウェア ライブラリ]** ワークスペースで、 **[アプリケーション管理]**  >  **[アプリケーション]** の順に展開し、管理するパッケージを選んで、管理タスクを選びます。  

|タスク|詳細|  
|----------|-------------|  
|**アクセス アカウントの管理**|**[アクセス アカウントの管理]** ダイアログ ボックスを開くと、選択したアプリケーションに関連付けられたコンテンツへのアクセス許可のレベルを指定できます。|  
|**事前設定コンテンツ ファイルの作成**|**事前設定コンテンツ ファイルの作成ウィザード**を開始します。このウィザードは、コンテンツのリモート配布ポイントへの配布を管理するのに役立ちます。 スケジュールおよび調整によってリモート配布ポイントの問題が有効に解決できない場合は、配布ポイントにコンテンツを事前設定することができます。<br /><br /> 「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。|  
|**リビジョン履歴**|**[アプリケーションのリビジョン履歴]** ダイアログ ボックスが開きます。このダイアログ ボックスでは、このアプリケーションに加えられたリビジョンのプロパティを確認したり、古いアプリケーション リビジョンを削除したり、このアプリケーションの旧バージョンを復元したりすることができます。<br /><br /> 「[アプリケーションを修正して置き換える方法](../../apps/deploy-use/revise-and-supersede-applications.md)」を参照してください。|  
|**展開の種類の作成**|**展開の種類の作成ウィザード**が開き、選択したアプリケーションに新しい展開の種類を追加できます。<br /><br /> 「[Create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md)」 (System Center Configuration Manager でアプリケーションを作成する) を参照してください。|  
|**統計情報の更新**|**[監視]** ワークスペースの、 **[展開]** ノードに表示されるこのアプリケーションの展開に関する情報を更新します。<br /><br /> 「[Configuration Manager コンソールからのアプリケーションの監視](../../apps/deploy-use/monitor-applications-from-the-console.md)」を参照してください。|  
|**復帰**|**[インベントリから削除]** 管理タスクを使ってインベントリから削除されたアプリケーションを元に戻します。|  
|**削除**|アプリケーションをインベントリから削除すると、展開に使用することはできなくなりますが、このアプリケーション自体やその展開は削除されません。 クライアント コンピューターにインストールされたアプリケーションの既存のコピーが削除されることはありません。 アプリケーションのすべてのリビジョンは 60 日後に Configuration Manager から削除されます。 ただし、インストール済みのアプリケーションのコピーは削除されません。<br /><br /> アプリケーションを削除するには、まずインベントリから削除し、次にその展開をすべて削除し、さらに他の展開によるアプリケーションの参照を削除してから、アプリケーションのすべてのリビジョンを削除します。<br /><br /> 「[アプリケーションを修正して置き換える方法](../../apps/deploy-use/revise-and-supersede-applications.md)」を参照してください。|  
|**エクスポート**|**アプリケーションのエクスポート ウィザード**が開きます。このウィザードは選択したアプリケーションを .zip ファイルにエクスポートするので、これをアーカイブしたり、別のサイトにインストールしたりできます。 アプリケーションのコンテンツをエクスポートすると、そのコンテンツを含むフォルダーが作成されます。<br /><br /> さらに、アプリケーションの依存関係や、置き換え関係、そのアプリケーションと依存関係の条件やコンテンツもエクスポートできます。<br /><br /> Windows PowerShell コマンドレットの **Export-CMApplication** は、同じ機能を実行します。 詳細については、Microsoft System Center 2012 Configuration Manager SP1 コマンドレット リファレンス ドキュメントの「[Export-CMApplication](https://go.microsoft.com/fwlink/p/?LinkID=258880)」を参照してください。|  
|**削除**|現在選択しているアプリケーションを削除します。<br /><br /> ほかのアプリケーションが依存している場合、アクティブな展開がある場合、または依存タスク シーケンスがある場合は、そのアプリケーションを削除できません。|  
|**展開のシミュレート**|**アプリケーション展開のシミュレーション ウィザード**を開きます。このウィザードを使うと、アプリケーションをインストールしたり、アンインストールせずに、コンピューターへのアプリケーションの展開結果をテストできます。<br /><br /> 「[Simulate application deployments with System Center Configuration Manager](../../apps/deploy-use/simulate-application-deployments.md)」 (System Center Configuration Manager でアプリケーションの展開をシミュレーションする) を参照してください。|  
|**展開**|**ソフトウェアの展開ウィザード** を開きます。このウィザードを使うと、階層内のコンピューターのグループに対して選択したアプリケーションを展開できます。<br /><br /> 「[Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)」 (System Center Configuration Manager でアプリケーションを展開する) を参照してください。|  
|**コンテンツの配布**|**コンテンツの配布ウィザード**を開きます。このウィザードを使うと、階層内の配布ポイントに選択したアプリケーションのコンテンツをコピーできます。<br /><br /> 「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。|  
|**関係の表示**|選択したアプリケーションと他のアプリケーションの関係図が表示されます。 次のいずれかを選択します。<br><br><ul><li>**依存関係** – 選択したアプリケーションに依存しているアプリケーションや、選択したアプリケーションが依存しているアプリケーションが表示されます。</li><li>**置き換え** – 選択したアプリケーションによって置き換えられるアプリケーションと、選択したアプリケーションを置き換えるアプリケーションが表示されます。</li><li>**グローバル条件** – このアプリケーションが参照するグローバル条件が表示されます。</li></ol><br /> 「[How to revise and supersede applications in System Center Configuration Manager](../../apps/deploy-use/revise-and-supersede-applications.md)」 (System Center Configuration Manager でアプリケーションを修正して置き換える方法) および「[How to create global conditions in System Center Configuration Manager](../../apps/deploy-use/create-global-conditions.md)」 (System Center Configuration Manager でグローバル条件を作成する方法) を参照してください。|  
|**アプリケーションのコピー**|Configuration Manager アプリケーションをコピーまたは複製して、新しいアプリケーションを作成します。 このアクションは、何かをテストする場合や、類似のアプリケーションを作成する必要がある場合に便利です。 サイトでは、 **-copy** を名前に付けて、新しいアプリケーションが作成されます。 サイトでは、ほとんどのメタデータが新しいアプリケーションにコピーされますが、展開はコピーされません。|

##  <a name="manage-deployment-types"></a>展開の種類を管理する  
 **[ソフトウェア ライブラリ]** ワークスペースで、 **[アプリケーション管理]** を展開し、 **[アプリケーション]** を選択してから、管理する展開の種類のアプリケーションを選択します。 詳細ウィンドウで **[展開の種類]** タブを選び、管理する展開の種類を選んで、管理タスクを選びます。  

|タスク|詳細|  
|----------|-------------|  
|**優先順位を上げる**|選択した展開の種類の優先順位を上げます。 展開の種類は順番に評価されます。 展開の種類が特定の要件を満たしている場合はそれが実行され、優先順位一覧に表示された他の展開の種類は評価されません。|  
|**優先順位を下げる**|選択した展開の種類の優先順位を下げます。|  
|**削除**|選択した展開の種類を削除します。<br><br>別のアプリケーションの展開の種類によって参照されている展開の種類は、削除できません。<br>展開の種類を削除するにはまず、他の展開の種類に含まれる展開の種類の依存関係をすべて削除する必要があります。<br>さらに、削除する展開の種類を参照する展開の種類を含むすべてのアプリケーションの、以前のリビジョンも削除する必要があります。|  
|**コンテンツの更新**|選択した展開の種類のコンテンツを更新します。<br /><br /> 仮想アプリケーションを含む展開の種類に対してウィザードを使用する場合、**コンテンツの更新ウィザード**が開始されます。 このウィザードを使うと、選択した仮想アプリケーションの公開オプションと要件の規則を変更できます。 詳細については、「[Create applications](../../apps/deploy-use/create-applications.md)」 (アプリケーションを作成する) を参照してください。<br /><br /> 展開の種類のコンテンツを更新すると、アプリケーションの新しいリビジョンが作成されます。 これにより、新しいアプリケーションと共にクライアント デバイスが更新される場合があります。|  
