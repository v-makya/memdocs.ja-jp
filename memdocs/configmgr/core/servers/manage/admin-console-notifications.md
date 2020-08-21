---
title: Configuration Manager コンソールの通知
titleSuffix: Configuration Manager
description: Configuration Manager コンソールからのアプリケーションの監視について説明します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129547"
---
# <a name="configuration-manager-console-notifications"></a>Configuration Manager コンソールの通知

*適用対象:Configuration Manager (Current Branch)*

<!--3556016, fka 1318035-->
Configuration Manager バージョン 1902 以降では、特定のイベントの発生に関して Configuration Manager コンソールから通知が行われます。 このイベント通知の一部を、Configuration Manager サイトに対して構成できます。

- 構成不可能なイベント通知には次のものがあります。
   - Configuration Manager 自体の更新プログラムが利用可能になったとき
   - ライフサイクルおよびメンテナンス イベントが環境で発生したとき
- 構成可能なイベント通知には次のものがあります。
   - [重要ではないサイトの正常性の変更](#bkmk_noncrit)
   - [Microsoft からのメッセージ](#bkmk_msft) (バージョン 2006 以降)

この通知は、コンソール ウィンドウの上部のリボンの下のバーに表示されます。 これにより Configuration Manager の更新プログラムが利用可能になったときに、以前のエクスペリエンスが置き換えられます。 これらのコンソール内通知には引き続き重要な情報が表示されますが、コンソールでの作業には干渉しません。 重要な通知は消去できません。 コンソールのタイトル バーの新しい通知領域に、すべての通知が表示されます。

![コンソール内の通知バーとフラグ](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a>重要ではない通知を表示するようにサイトを構成する

サイトのプロパティで、重要でない通知を表示するように各サイトを構成することができます。

1. **[管理]** ワークスペースで、 **[サイトの構成]** を展開してから **[サイト]** ノードを選択します。
1. 重要ではない通知に構成するサイトを選択します。
1. リボンで、 **[プロパティ]** を選択します。
1. **[アラート]** タブで、 **[重大ではないサイト ヘルスの変更についてのコンソール通知を有効にする]** オプションを選択します。
   - この設定を有効にすると、すべてのコンソール ユーザーに重要、警告、および情報の通知が表示されます。 既定では、この設定は有効になっています。  
   - この設定を無効にすると、コンソール ユーザーには重要な通知のみが表示されます。  

ほとんどのコンソール通知はセッションごとです。 ユーザーがクエリを起動すると、コンソールによってクエリが評価されます。 通知に変更を表示するには、コンソールを再起動します。 ユーザーが重要でない通知を破棄すると、コンソールを再起動したときにその通知がまだ有効な場合は、再度通知されます。

次の通知は、5 分ごとに再評価します。

- サイトがメンテナンス モードにある  
- サイトが回復モードにある  
- サイトがアップグレード モードにある  

通知は、ロール ベース管理のアクセス許可に従います。 たとえば、ユーザーが Configuration Manager 更新プログラムを表示するアクセス許可を持っていない場合、これらの通知は表示されません。

一部の通知には、関連するアクションがあります。 たとえば、コンソールのバージョンがサイトのバージョンと一致しない場合は、 **[コンソールの新しいバージョンをインストールします]** を選択します。 このアクションにより、コンソールのインストーラーが起動されます。

バージョン 2006 以降では、サイトをクラウドに接続するように Azure サービスを構成すると、[秘密鍵の更新](../deploy/configure/azure-services-wizard.md#bkmk_renew)アクションに関する通知が表示されるようになります。<!--6386392--> サイトでは、次のアラートの状態が 1 時間に 1 回評価されます。

- 1 つ以上の Azure AD アプリの秘密鍵の有効期限が間もなく切れる
- 1 つ以上の Azure AD アプリの秘密鍵が期限切れになっている

次の通知は、Technical Preview Branch に最適です。  

- 評価版の有効期限まで 30 日以内 (警告): 現在の日付は、評価版の有効期限まで 30 日を切っています  
- 評価版の有効期限切れ (重要): 現在の日付は、評価版の有効期限を過ぎています  
- コンソールのバージョンの不一致 (重要) コンソールのバージョンがサイトのバージョンと一致しません  
- サイトのアップグレードが利用可能 (警告): 使用可能な新しい更新プログラム パッケージがあります  

詳細とトラブルシューティングに役立つ情報については、コンソール コンピューター上の **SmsAdminUI.log** ファイルをご覧ください。 既定では、このログ ファイルは次のパスに配置されています。`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log`

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a>Microsoft からメッセージを受信するようにサイトを構成する
 <!--3953121-->

バージョン 2006 以降では、Configuration Manager コンソールで Microsoft からの通知を受信することを選択できます。 これらの通知は、新機能または更新された機能、Configuration Manager および関連付けられているサービスに対する変更、修復するために操作が必要な問題に関する最新情報を入手するのに役立ちます。

### <a name="configure-notification-settings-for-microsoft-messages"></a>Microsoft からのメッセージの通知設定を構成する

1. **[管理]**  >  **[サイトの構成]**  >  **[サイト]** の順に移動します。
1. サイトを右クリックし、 **[プロパティ]** をクリックします。
1. **[アラート]** タブで、 **[Receive messages from Microsoft] (Microsoft からメッセージを受信)** を選択して通知を有効にします。 受信しない場合は、次のいずれかの通知の選択を解除できます。  
   - **回避または修正**:組織に影響を与える既知の問題により、ユーザーによる操作が必要になる可能性があります。
   - **変更の計画**: Configuration Manager に対する変更により、ユーザーによる操作が必要になる可能性があります。
   - **最新の情報を入手**:利用可能な新機能または更新された機能に関する情報を提供します。

     [ ![サイトのプロパティの Microsoft からの通知オプション](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>次のステップ

- [コンソールの使用](admin-console.md)
- [コンソールのヒント](admin-console-tips.md)
- [ユーザー補助機能](../../understand/accessibility-features.md)
