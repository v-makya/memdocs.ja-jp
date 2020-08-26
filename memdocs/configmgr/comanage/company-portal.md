---
title: ポータル サイトのアプリ
titleSuffix: Configuration Manager
description: 共同管理デバイスで Intune ポータル サイト アプリを使用するための、一貫したユーザー エクスペリエンスが提供されます。
ms.date: 08/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 535b91b82e024431e4221824b4623b6ffc17b286
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700876"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>共同管理デバイスでポータル サイト アプリを使用する

*適用対象:Configuration Manager (Current Branch)*

<!--CMADO-3601237,INADO-4297660-->

バージョン 2006 以降では、Intune ポータル サイトが、Microsoft エンドポイント マネージャー用のクロスプラットフォームのアプリ ポータル エクスペリエンスになっています。 ポータル サイトも使用するように共同管理デバイスを構成することで、すべてのデバイスで一貫したユーザー エクスペリエンスを実現できます。

Intune ポータル サイトでは、次の操作がサポートされています。

- 共同管理デバイスでポータル サイト アプリを起動し、Azure Active Directory (Azure AD) シングル サインオン (SSO) を使用してサインインする。
- ポータル サイトで、Intune アプリと共に、利用可能およびインストールされている Configuration Manager アプリを表示する。
- ポータル サイトから利用可能な Configuration Manager アプリをインストールし、インストールの状態に関する情報を受け取る。

:::image type="content" source="media/3601237-company-portal.png" alt-text="Configuration Manager からのアプリが表示されたポータル サイト" lightbox="media/3601237-company-portal.png":::

ポータル サイトの動作は、お使いの共同管理ワークロードの構成によって異なります。

| ワークロード | 設定 | 動作 |
|----------|---------|----------|
| クライアント アプリ | **Configuration Manager** | Configuration Manager クライアント アプリのみが表示されます |
| クライアント アプリ | **パイロット Intune** または **Intune** | Configuration Manager と Intune クライアント アプリの両方が表示されます |
| Office クイック実行アプリ | **Configuration Manager** | Configuration Manager の Office クイック実行アプリのみが表示されます |
| Office クイック実行アプリ | **パイロット Intune** または **Intune** | Intune の Office クイック実行アプリのみが表示されます |

詳細については、以下の記事を参照してください。

- [アプリのワークロードの図](workloads.md#diagram-for-app-workloads)

- [Configuration Manager のワークロードを Intune に切り替える方法](how-to-switch-workloads.md)

## <a name="prerequisites"></a>前提条件

- Configuration Manager Current Branch バージョン 2006 以降

- Windows 10 バージョン 1803 以降:

  - [共同管理](how-to-enable.md)に登録済み

  - [Intune のインターネット エンドポイント](../../intune/fundamentals/intune-endpoints.md)へのアクセス

- これらのデバイスにサインインするユーザー アカウントには、次の構成が必要です。

  - Azure AD ID

  - Intune ライセンスが割り当て済み

## <a name="configure-and-deploy"></a>構成して展開する

### <a name="configuration-manager-client-settings"></a>Configuration Manager のクライアント設定

ユーザーが Intune ポータル サイトからのみ通知を受け取れるようにするには、Configuration Manager のクライアント設定を構成します。 デバイス設定の **[ソフトウェア センター]** グループで、 **[ユーザー ポータルを選択]** を **[ポータル サイト]** に変更します。

クライアント設定の詳細については、以下の記事を参照してください。

- [クライアント設定を構成する方法](../core/clients/deploy/configure-client-settings.md)
- [クライアント設定について](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>Intune ポータル サイト アプリを展開する

- ユーザーは、[Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab) から Intune ポータル サイト アプリを手動でインストールできます。

- 共同管理デバイス上のアプリを要求するため、展開プロセスでは[クライアント アプリ](workloads.md#client-apps)共同管理ワークロードの状態が利用されます。

  - クライアント アプリのワークロードで Configuration Manager が使用されている場合は、[Configuration Manager を使用してアプリケーションを作成および展開します](../apps/get-started/create-and-deploy-an-application.md)。 [ビジネス向け Microsoft Store](https://www.microsoft.com/business-store) から、オフライン Intune ポータル サイト アプリをダウンロードします。

  - クライアント アプリのワークロードで Intune が使用されている場合は、Configuration Manager を使用して展開するか、[Microsoft Intune を使用して Windows 10 の Intune ポータル サイト アプリを追加する](../../intune/apps/store-apps-company-portal-app.md)ことができます。

組織用の Intune ポータル サイトのブランド化に関する詳細については、[Intune ポータル サイト アプリのカスタマイズ方法](../../intune/apps/company-portal-app.md)に関する記事を参照してください。

## <a name="use-the-company-portal"></a>Intune ポータル サイトを使用する

1. [スタート] メニューから Intune ポータル サイトを起動します。 現在サインインしているユーザーは、Azure AD ID に基づいて Intune ポータル サイトに自動的にサインインされます。

1. **[アプリ]** ページを選択します。 Configuration Manager アプリが一覧に表示されます。

1. Configuration Manager から展開されたアプリの 1 つを選択します。

    - **[概要]** タブに、サイズ、バージョン、発行日など、アプリの詳細が表示されます。

    - Configuration Manager がこのアプリの管理サービスであることを確認するには、 **[追加情報]** タブに切り替えます。

    - アプリをインストールするには、 **[インストール]** を選択します。 Intune ポータル サイトにインストールの状態が表示され、完了すると通知が表示されます。

    - アプリが既にインストールされている場合は、 **[アンインストール]** を選択してアプリを削除します。

    - 追加の操作 ( **[修復]** や **[共有]** など) を使用するには、省略記号 [`...`] を選択します。

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="Intune ポータル サイトに詳細情報が表示されている Configuration Manager アプリ" lightbox="media/3601237-company-portal-app-details.png":::

    - Configuration Manager Web アプリをインストールした後、省略記号メニューを選択し、 **[ブラウザーで開く]** を選択して Web アプリを起動ます。

    - Configuration Manager アプリケーションのインストールが既知のエラー コードで失敗する場合は、失敗状態のリンクを選択してエラー コードを検索します。

[ポータル サイト] にクライアントの設定を変更した場合、ユーザーが Configuration Manager の通知を選択すると、Intune ポータル サイトが起動されます。 Intune ポータル サイトでサポートされていないシナリオに対する通知の場合、通知を選択するとソフト ウェアセンターが起動されます。

Configuration Manager アプリのインストールに関する問題のトラブルシューティングについては、Intune ポータル サイトの **[ヘルプとサポート]** セクションに移動します。 **[問い合わせ]** オプションを使用すると、要求の一部として Configuration Manager のログ ファイルを送信できます。

## <a name="frequently-asked-questions-faq"></a>よく寄せられる質問 (FAQ)

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>Intune ポータル サイトでは、Configuration Manager からソフトウェア更新プログラムとして展開されたアプリケーションがサポートされますか?

はい。 ソフトウェア更新プログラム機能を使用してアプリを展開した場合、クライアントでは、ユーザー エクスペリエンスが Intune ポータル サイトかソフトウェア センターかにかかわらず、同じように扱われます。

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>ユーザーは Intune ポータル サイトで Configuration Manager アプリの修復、アンインストール、更新を行うことができますか?

はい。 これらの追加操作をサポートするように Configuration Manager アプリを構成した場合、Intune ポータル サイトでは修復、アンインストール、更新がサポートされます。

## <a name="known-issues"></a>既知の問題

現在、Intune ポータル サイトでは、ソフトウェア センターの次の機能は利用できません。

- 一部のアプリ情報 (再起動が必要な場合や、インストールの推定所要時間など)

- [アプリ グループ](../apps/deploy-use/create-app-groups.md)

その他の既知の問題:

- Configuration Manager と Intune の両方から同じアプリを展開すると、Intune ポータル サイトに 2 回表示されます。

- Intune ポータル サイトを検索すると、常に Intune アプリが Configuration Manager アプリの前に表示されます。

## <a name="next-steps"></a>次のステップ

[Configuration Manager のワークロードを Intune に切り替える方法](how-to-switch-workloads.md)

[Intune ポータル サイト アプリをカスタマイズする方法](../../intune/apps/company-portal-app.md)
