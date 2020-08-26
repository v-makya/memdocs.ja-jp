---
title: ソフトウェア センターの計画
titleSuffix: Configuration Manager
description: ユーザーが Configuration Manager と対話するために、ソフトウェア センターをどのように構成してブランド化するかを決定します。
ms.date: 08/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 802dbaa4188199e555a5cc0143ed599ad454e27e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695173"
---
# <a name="plan-for-software-center"></a>ソフトウェア センターの計画

*適用対象:Configuration Manager (Current Branch)*

ユーザーはソフトウェア センターから設定を変更し、アプリケーションを参照して、アプリケーションをインストールします。 Configuration Manager クライアントを Windows デバイスにインストールすると、ソフトウェア センターも自動的にインストールされます。

ソフトウェア センターの他の機能について詳しくは、「[ソフトウェア センターのユーザー ガイド](../../core/understand/software-center.md)」をご覧ください。  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a> ソフトウェア センターの構成  

ソフトウェア センターの最新の機能を活用するために、Configuration Manager サイトとクライアントをバージョン 1906 以降に更新します。

> [!IMPORTANT]
> ソフトウェア センターと管理ポイントがこのように繰り返し改善されるのは、アプリケーション カタログの役割を廃止する目的で行われます。
>
> - Silverlight ユーザー エクスペリエンスは Current Branch バージョン 1806 以降、サポートされません。
> - バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。
> - アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。

- **[コンピューター エージェント]** グループのクライアント設定 **[新しいソフトウェア センターを使用する]** は、既定で有効になります。 前のバージョンのソフトウェア センターはサポートされなくなりました。 詳細については、[削除された機能と非推奨の機能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。

- ソフトウェア センターの **[インストールのステータス]** タブで、アプリケーション カタログ Web サイト リンクの表示を指定します。 詳しくは、「[ソフトウェア センター](../../core/clients/deploy/about-client-settings.md#software-center)」のクライアント設定をご覧ください。

- バージョン 1906 以降では、ソフトウェア センターに最大 5 つのカスタム タブを追加できます。 詳細については、[ソフトウェア センターのクライアント設定](../../core/clients/deploy/about-client-settings.md#software-center)に関するページを参照してください。 <!--4063773-->

- ユーザーはソフトウェア センターでユーザーとデバイスのアフィニティを構成できます。 詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。

- バージョン 2006 以降では、Intune アプリと Configuration Manager アプリの両方に対して Intune ポータル サイトを使用するように、共同管理デバイスを構成できます。 詳細については、「[共同管理デバイスでポータル サイト アプリを使用する](../../comanage/company-portal.md)」を参照してください。<!--CMADO-3601237,INADO-4297660-->

> [!IMPORTANT]
> Configuration Manager の新機能を利用するには、最初にクライアントを最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。

### <a name="software-center-and-user-available-applications"></a>ソフトウェア センターとユーザーが利用できるアプリケーション

- ユーザーが利用できるアプリケーションをソフトウェア センターに表示するためにアプリケーション カタログの役割は必要ありません。 この動作は、ユーザーにアプリケーションを配布するために必要なサーバー インフラストラクチャを減らすのに役立ちます。 ソフトウェア センターは、この情報を取得するために管理ポイントに依存します。これにより、より大規模な環境を、[境界グループ](../../core/servers/deploy/configure/boundary-groups.md#management-points)に割り当てることでより適切にスケーリングすることができます。<!--1358309-->

- ユーザーは、Azure Active Directory (Azure AD) に参加しているデバイスで利用可能なアプリケーションを参照してインストールできます。 バージョン 2006 以降では、ドメインに参加しているインターネットベースのデバイスでユーザーが利用できるアプリを取得できます。 詳細については、[ユーザーが利用できるアプリケーションの展開](../deploy-use/deploy-applications.md#deploy-user-available-applications)に関するページを参照してください。

- バージョン 1906 以降では、ユーザーが利用可能であるとされているアプリに関して、ソフトウェア センターは管理ポイントと通信します。 今後、アプリケーション カタログは使用されません。 この変更により、サイトからアプリケーション カタログを簡単に削除できるようになりました。

- 以前は、ソフトウェア センターによって、利用できるサーバーの一覧から最初の管理ポイントが選択されました。 バージョン 1906 以降では、クライアントにより使用されるものと同じ管理ポイントが使用されます。 この変更により、割り当てられたプライマリ サイトからの管理ポイントでクライアントのものと同じ管理ポイントをソフトウェア センターで使用できるようになりました。

## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a> ダイアログ ウィンドウでトースト通知を置き換える

<!--3555947-->
再起動や必須の展開に関する Windows のトースト通知が表示されないことがあります。 また、リマインダーを再通知するエクスペリエンスが表示されません。 クライアントが期限に達すると、この動作が原因でユーザー エクスペリエンスが低下する可能性があります。

バージョン 1902 以降では、[ソフトウェアの変更が必要](#software-changes-are-required)な場合、または展開で[再起動が必要](#restart-required)な場合に、より頻繁に表示されるダイアログ ウィンドウを使用できるようになりました。

### <a name="software-changes-are-required"></a>ソフトウェアの変更が必要

必要に応じて今後の期限を指定して[アプリケーションを展開する](../deploy-use/deploy-applications.md)ときに、ソフトウェアの展開ウィザードの **[ユーザー エクスペリエンス]** ページで、次のユーザー通知オプションを選択します。

- **すべての通知をソフトウェア センターで表示し、ユーザーにもすべて通知する**
- **[When software changes are required, show a dialog window to the user instead of a toast notification]\(ソフトウェアの変更が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する\)**

この展開設定を構成すると、このシナリオのユーザー エクスペリエンスが変わります。

次のトースト通知から:

!["ソフトウェアの変更が必要です" というトースト通知](media/3555947-required-toast.png)  

次のダイアログ ウィンドウに変更:

![必須のソフトウェアの変更に関するダイアログ ウィンドウ](media/3555947-required-dialog.png)


### <a name="restart-required"></a>再起動が必要

クライアント設定の [[コンピューターの再起動]](../../core/clients/deploy/about-client-settings.md#computer-restart) グループで、次のオプションを有効にします。 **[When a deployment requires a restart, show a dialog window to the user instead of a toast notification]\(展開で再起動が必要な場合、トースト通知ではなくダイアログ ウィンドウをユーザーに表示する\)** 。  

このクライアント設定を構成すると、すべての必要な展開のユーザー エクスペリエンスが変更されます。これには次の種類の再起動が必要です。

- [アプリケーション](../deploy-use/deploy-applications.md)。
- [タスク シーケンス](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [ソフトウェア更新プログラム](../../sum/deploy-use/deploy-software-updates.md)

次のトースト通知から:

!["再起動が必要" というトースト通知](media/3555947-restart-toast.png)  

次のダイアログ ウィンドウに変更:

!["コンピューターを再起動してください" というダイアログ ウィンドウ](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> Configuration Manager 1902 の場合、特定の状況下では、ダイアログ ボックスでトースト通知が置き換えられません。 この問題を解決するには、[Configuration Manager バージョン 1902 の更新プログラムのロールアップ](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)をインストールします。 <!--4404715-->

## <a name="brand-software-center"></a>ソフトウェア センターのブランド化

組織のブランド化要件を満たすようにソフトウェア センターの外観を変更します。 この構成はユーザーがソフトウェア センターを信頼するのに役立ちます。

### <a name="configure-software-center-branding"></a>ソフトウェア センターのブランド化を構成する

<!-- 1351224 -->
組織のブランド化要素を追加し、タブの表示を指定することにより、ソフトウェア センターの外観をカスタマイズします。

詳細については、次の記事を参照してください。

- [ソフトウェア センター](../../core/clients/deploy/about-client-settings.md#software-center) グループのクライアント設定  
- [クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>ブランド化の優先順位

Configuration Manager では、次の優先順位に従って、ソフトウェア センターのカスタム ブランド化が適用されます。  

1. **ソフトウェア センター**のクライアント設定。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#software-center)」を参照してください。  

2. **[コンピューター エージェント]** グループでの **[組織名]** クライアント設定。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#computer-agent)」を参照してください。  

#### <a name="application-catalog-branding-priorities"></a>アプリケーション カタログのブランド化の優先順位

> [!IMPORTANT]
> アプリケーション カタログの Silverlight ユーザー エクスペリエンスは、Current Branch バージョン 1806 以降では、サポートされません。 バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  

アプリケーション カタログを使用している場合、ブランド化は次の優先順位に従います。  

1. **ソフトウェア センター**のクライアント設定。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#software-center)」を参照してください。  

2. アプリケーション カタログ Web サイト ポイントのプロパティで指定した*組織名*と*色*。 詳細については、[アプリケーション カタログ Web サイト ポイントの構成オプション](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)に関するページをご覧ください。  

3. **[コンピューター エージェント]** グループでの **[組織名]** クライアント設定。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#computer-agent)」を参照してください。  

## <a name="see-also"></a>関連項目

- [ソフトウェア センターのユーザー ガイド](../../core/understand/software-center.md)

- [アプリケーション管理の計画と構成](plan-for-and-configure-application-management.md)

- [共同管理デバイスでポータル サイト アプリを使用する](../../comanage/company-portal.md)
