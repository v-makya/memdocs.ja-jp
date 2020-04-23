---
title: アカウントを閉じる方法
titleSuffix: Configuration Manager
description: Azure アカウントから Desktop Analytics を削除する方法
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e1d031588100f3930bf5bf25970f544b91017d77
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706610"
---
# <a name="how-to-close-your-account"></a>アカウントを閉じる方法

環境内に Desktop Analytics をセットアップした後、それを削除する必要がある場合は、このプロセスを使用してアカウントを閉じます。

## <a name="prerequisites"></a>[前提条件]

**グローバル管理者**だけが、Azure portal でアカウントを閉じるか再アクティブ化できます。

## <a name="process-to-offboard"></a>オフボードするためのプロセス

1. Microsoft 365 デバイス管理で、**グローバル管理者**ロールを持つユーザーとして、[Desktop Analytics ポータル](https://aka.ms/desktopanalytics)を開きます。

1. **[グローバル設定]** メニューで、 **[接続済みサービス]** を選択します。 [デバイスの登録] セクションで、 **[オフボード]** オプションを選択します。

1. 続行すると、アカウントが閉じられます。

> [!Important]
> この記事の残りの部分は 90 後、または再アクティブ化する予定がない場合にのみ、続行してください。
>
> 90 日間待機せずにアカウントを完全に閉じる場合は、まずアカウントを[リセット](account-reset.md)してください。

## <a name="reactivate"></a>再アクティブ化する

次の 90 日の間、Desktop Analytics ポータルにアクセスする組織の管理者には、オフボードが選択されたことを示す通知が表示されます。

グローバル管理者は、90 日以内にアカウントを再アクティブ化することができます。 組織の Desktop Analytics を復元するには、 **[戻る]** オプションを選択します。

## <a name="delete-the-solution"></a>ソリューションを削除する

> [!Warning]
> この記事の残りの部分は 90 後、または再アクティブ化する予定がない場合にのみ、続行してください。 これらの他のコンポーネントを削除して切断する場合は、再アクティブ化しようとしないでください。

1. **グローバル管理者**ロールを持つユーザーとして [Azure portal](https://portal.azure.com) にサインインします。

1. **[すべてのリソース]** で、Desktop Analytics ワークスペースの名前を検索します。 この名前は、サービスにサインアップするときに作成したものです。

1. 種類が **[ソリューション]** である `Microsoft365Analytics(YourWorkspaceName)` を削除します。

Desktop Analytics データは、ワークスペースのデータ保持ポリシーに基づいて期限切れになります。 同じワークスペースの他のソリューションは引き続き使用できます。

> [!Important]  
> Log Analytics ワークスペースを他のソリューションと共に使用している場合は、ワークスペースを削除しないでください。

## <a name="remove-user-and-app-access"></a>ユーザーとアプリのアクセス権の削除

1. **グローバル管理者**ロールを持つユーザーとして [Azure portal](https://portal.azure.com) にサインインします。 **[Azure Active Directory]** に移動します。

1. **[ロールと管理者]** で、 **[Desktop Analytics 管理者]** ロールを探します。 そのメンバーを削除します。

1. **[グループ]** で、次のグループのメンバーを削除します。

    - **M365 Analytics Client 管理者 (Log Analytics 所有者)**
    - **M365 Analytics Client 管理者 (Log Analytics 共同作成者)**

1. **[エンタープライズ アプリケーション]** で、次のアプリに対するアクセス許可を削除するか取り消します。

    - `MaLogAnalyticsReader`

    - ConfigMgr アプリ。 このアプリの名前を見つけるには、Configuration Manager コンソールに移動します。 **[管理]** ワークスペースで、 **[クラウド サービス]** を展開し、 **[Azure サービス]** ノードを選択します。 **Desktop Analytics** サービスのプロパティを開き、 **[アプリケーション]** タブに切り替えます。 **[Web アプリ]** がこの Azure アプリです。

        > [!Important]  
        > Azure AD でこのアプリを変更する前に、Configuration Manager の別のサービスでそれを再利用していないことを確認してください。

## <a name="disconnect-configuration-manager"></a>Configuration Manager を切断する

1. **完全な権限を持つ管理者** ロールのユーザーとして Configuration Manager コンソールを開きます。

1. **[管理]** ワークスペースに移動し、 **[クラウド サービス]** を展開し、 **[Azure サービス]** ノードを選択します。

1. Desktop Analytics サービスを削除します。

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>パイロットと運用環境への展開用のコレクションを削除する

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースの **[デバイス コレクション]** を選択します。

1. 使用しなくなったコレクションを削除します。 既定では、コレクションは、 **[展開計画]** フォルダーに配置されます。  

## <a name="reconfigure-clients"></a>クライアントを再構成する

### <a name="unenroll-devices"></a>デバイスの登録を解除する

登録済みのデバイスに関して、次の Windows レジストリキーから CommercialID 値を削除します。

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Windows の診断データの構成

デバイスによる診断データの送信を続行しない場合:

- Windows 10: 診断データ レベルを **[セキュリティ]** に設定します
- Windows 7 SP1 または 8.1: **[商用データ オプトイン キー]** を無効にします

次のいずれかの方法で、これらの値を設定します。

- グループ ポリシー: **[コンピューターの構成]**  >  **[管理用テンプレート]**  >  **[Windows コンポーネント]**  >  **[データの収集とプレビュー ビルド]**
- モバイル デバイス管理 (MDM): [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry) など

詳しくは、「[組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)」をご覧ください。

> [!NOTE]  
> これらの変更を適用すると、デバイスによる診断データの送信は、すぐに停止されます。 Microsoft がワークスペースの分析情報の処理を停止するまでに 24 時間から48 時間かかることがあります。 Microsoft では、このデータを、30 日以内にクラウド サービスから削除します。
