---
title: ソフトウェア センターの計画
titleSuffix: Configuration Manager
description: ユーザーが Configuration Manager と対話するために、ソフトウェア センターをどのように構成してブランド化するかを決定します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15da90b12504fdaf7a4dd0a36704391eead877cd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689030"
---
# <a name="plan-for-software-center"></a>ソフトウェア センターの計画

*適用対象:Configuration Manager (Current Branch)*

ユーザーはソフトウェア センターから設定を変更し、アプリケーションを参照して、アプリケーションをインストールします。 Configuration Manager クライアントを Windows デバイスにインストールすると、ソフトウェア センターも自動的にインストールされます。

ソフトウェア センターの他の機能について詳しくは、「[ソフトウェア センターのユーザー ガイド](../../core/understand/software-center.md)」をご覧ください。  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a> ソフトウェア センターの構成  

最新の機能強化を活用するために、Configuration Manager サイトとクライアントをバージョン 1906 以降に更新します。

ソフトウェア センターの以下の機能強化を確認してください。

> [!Important]  
> ソフトウェア センターと管理ポイントがこのように繰り返し改善されるのは、アプリケーション カタログの役割を廃止する目的で行われます。
>
> - Silverlight ユーザー エクスペリエンスは Current Branch バージョン 1806 以降、サポートされません。
> - バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。
> - アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  

### <a name="starting-in-version-1802"></a>バージョン 1802 以降

- **[コンピューター エージェント]** グループのクライアント設定 **[新しいソフトウェア センターを使用する]** は、既定で有効になります。 前のバージョンのソフトウェア センターはサポートされなくなりました。 詳細については、[削除された機能と非推奨の機能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。  

- ユーザーは、Azure Active Directory (Azure AD) に参加しているデバイスで利用可能なアプリケーションを参照してインストールできます。 詳細については、[Azure AD 参加デバイスにユーザーが利用できるアプリケーションを展開する方法](../deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)に関するページを参照してください。  

### <a name="starting-in-version-1806"></a>バージョン 1806 以降

- ソフトウェア センターの **[インストールのステータス]** タブで、アプリケーション カタログ Web サイト リンクの表示を指定します。 詳しくは、「[ソフトウェア センター](../../core/clients/deploy/about-client-settings.md#software-center)」のクライアント設定をご覧ください。  

- ユーザーが利用できるアプリケーションをソフトウェア センターに表示するのにアプリケーション カタログの役割は必要なくなりました。 この変更は、ユーザーにアプリケーションを配布するために必要なサーバー インフラストラクチャを減らすのに役立ちます。 ソフトウェア センターは、この情報を取得するために管理ポイントに依存するようになりました。より大規模な環境を、[境界グループ](../../core/servers/deploy/configure/boundary-groups.md#management-points)に割り当てることでより適切にスケーリングすることができます。<!--1358309-->  

    > [!Note]  
    > 現在、アプリケーション カタログを使用している場合は、Configuration Manager をバージョン 1806 に 更新しても動作し続けます。 アプリケーション カタログの Web サイト ポイントの役割と Web サービス ポイントの役割は "*不要*" になりましたが、まだ "*サポートされています*"。 アプリケーション カタログ "*Web サイト ポイント*" の **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページを参照してください。
    >
    > 将来的にインフラストラクチャからアプリケーション カタログの役割を削除する計画を開始します。 ソフトウェア センターの機能強化を利用して管理ポイントを使用し、Configuration Manager 環境を簡素化します。  

### <a name="starting-in-version-1902"></a>バージョン 1902 以降

- ユーザーとデバイスのアフィニティを構成します。 詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。

### <a name="starting-in-version-1906"></a>バージョン 1906 以降

- ユーザーが入手できるアプリについては、ソフトウェア センターで管理ポイントと通信できるようになりました。 今後、アプリケーション カタログは使用されません。 この変更により、サイトからアプリケーション カタログを簡単に削除できるようになりました。

- 以前は、ソフトウェア センターによって、利用できるサーバーの一覧から最初の管理ポイントが選択されました。 このリリース以降、クライアントにより使用されるものと同じ管理ポイントが使用されます。 この変更により、割り当てられたプライマリ サイトからの管理ポイントでクライアントのものと同じ管理ポイントをソフトウェア センターで使用できるようになりました。

- 管理ポイントには、これらの新機能をサポートするソフトウェア センターのエンドポイントがあります。 これで、5 分ごとにこれらのエンドポイントの正常性が確認されるようになりました。 問題があれば、SMS_MP_CONTROL_MANAGER サイト コンポーネントのステータス メッセージにより報告されます。

- 新しいアプリケーション カタログ ロールをサイトに追加することはできません。 既存のロールは引き続き機能します。 ユーザーが利用できる展開にアプリケーション カタログを使用するのは、既存のクライアントのみです。 更新されたクライアントは、すべての展開の管理ポイントを自動的に使用します。

- ソフトウェア センターには、最大 5 つのカスタム タブを追加できます。 詳細については、[ソフトウェア センターのクライアント設定](../../core/clients/deploy/about-client-settings.md#software-center)に関するページを参照してください。 <!--4063773-->

### <a name="summary-of-infrastructure-requirements-per-version"></a>バージョンごとのインフラストラクチャ要件の概要

特定のバージョンの Configuration Manager に依存するソフトウェア センターの要件を理解するには、次の表を参考にしてください。

| デバイスの種類 | サイトのバージョン | インフラストラクチャ |
|-----------------|--------------|----------------|
| Azure AD 参加済みデバイス<br>(または "クラウド ドメイン参加済み") | 1802 または 1806 | すべてのアプリの展開に対する管理ポイント |
| インターネット上の[ハイブリッド Azure AD 参加済み](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)デバイス | 1802 または 1806 | すべてのアプリの展開に対するクラウド管理ゲートウェイと管理ポイント |
| オンプレミスの Active Directory ドメイン参加済みデバイス | 1802 | ソフトウェア センターを介してユーザーが利用できるアプリに必要なアプリケーション カタログ |
| オンプレミスの Active Directory ドメイン参加済みデバイス | 1806 | すべてのアプリの展開に対する管理ポイント |

> [!Important]  
> Configuration Manager の新機能を利用するには、最初にクライアントを最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。


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

## <a name="branding-software-center"></a>ソフトウェア センターのブランド化

組織のブランド化要件を満たすようにソフトウェア センターの外観を変更します。 この構成はユーザーがソフトウェア センターを信頼するのに役立ちます。

### <a name="configure-software-center-branding"></a>ソフトウェア センターのブランド化を構成する

<!-- 1351224 -->
組織のブランド化要素を追加し、タブの表示を指定することにより、ソフトウェア センターの外観をカスタマイズします。

詳細については、以下の記事を参照してください。

- [ソフトウェア センター](../../core/clients/deploy/about-client-settings.md#software-center) グループのクライアント設定  
- [クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>ブランド化の優先順位

Configuration Manager では、次の優先順位に従って、ソフトウェア センターのカスタム ブランド化が適用されます。  

1. **ソフトウェア センター**のクライアント設定。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#software-center)」を参照してください。  

2. **[コンピューター エージェント]** グループでの **[組織名]** クライアント設定。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#computer-agent)」を参照してください。  

#### <a name="application-catalog-branding-priorities"></a>アプリケーション カタログのブランド化の優先順位

> [!Important]
> アプリケーション カタログの Silverlight ユーザー エクスペリエンスは、Current Branch バージョン 1806 以降サポートされていません。 バージョン 1906 以降では、更新されたクライアントで、ユーザーが利用できるアプリケーション展開の管理ポイントが自動的に使用されます。 また、新しいアプリケーション カタログの役割はインストールできません。 アプリケーション カタログの役割のサポートは、バージョン 1910 で終了します。  

アプリケーション カタログを使用している場合、ブランド化は次の優先順位に従います。  

1. **ソフトウェア センター**のクライアント設定。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#software-center)」を参照してください。  

2. アプリケーション カタログ Web サイト ポイントのプロパティで指定した*組織名*と*色*。 詳細については、[アプリケーション カタログ Web サイト ポイントの構成オプション](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)に関するページをご覧ください。  

3. **[コンピューター エージェント]** グループでの **[組織名]** クライアント設定。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#computer-agent)」を参照してください。  


## <a name="see-also"></a>関連項目

- [ソフトウェア センターのユーザー ガイド](../../core/understand/software-center.md)
- [アプリケーション管理の計画と構成](plan-for-and-configure-application-management.md)
