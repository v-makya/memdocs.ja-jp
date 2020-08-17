---
title: Microsoft Intune でのアプリの管理とは
titleSuffix: ''
description: Microsoft Intune のプラットフォームでクライアント アプリを管理する機能について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 99dc504f8fc3148463288820dc810bab892e3081
ms.sourcegitcommit: 4f10625e8d12aec294067a1d9138cbce19707560
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87912389"
---
# <a name="what-is-microsoft-intune-app-management"></a>Microsoft Intune アプリの管理とは


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Microsoft Intune を使用すれば、IT 管理者として、会社の従業員が使用するクライアント アプリを管理することができます。 この機能は、デバイス管理とデータ保護に加え用意されています。 管理者の優先事項の 1 つは、エンド ユーザーが仕事を行う上で必要なアプリに確実にアクセスできるようにすることです。 この目標を達成するには以下の理由により、課題があります。
- さまざまなデバイス プラットフォームとアプリの種類が存在する。
- 会社のデバイスとユーザーの個人デバイスの両方で、アプリの管理が必要になる場合がある。
- 社内のネットワークとデータの安全性を確保する必要がある。

また、Intune に登録されていないデバイスでアプリの割り当てと管理が必要になる場合もあります。

## <a name="mobile-application-management-mam-basics"></a>モバイル アプリケーション管理 (MAM) の基本

[Intune モバイル アプリケーション管理](app-lifecycle.md)とは、ユーザーのモバイル アプリの公開、プッシュ、構成、セキュリティ保護、監視、および更新を可能にする一連の Intune 管理機能のことです。

MAM を使用すると、アプリケーション内の組織のデータを管理および保護することができます。 **登録を必要としない MAM** (MAM-WE) を使用すると、機密データが含まれる職場または学校関連のアプリを、**Bring Your Own Device** (BYOD) シナリオにおける個人用デバイスを含む、ほぼすべての[デバイス](app-management.md#app-management-capabilities-by-platform)で管理できます。 Microsoft Office アプリなどの多くの仕事効率化アプリを、Intune MAM で管理することができます。 一般使用が可能な [Microsoft Intune によって保護されたアプリ](apps-supported-intune-apps.md)の公式一覧を参照してください。

Intune MAM では次の 2 つの構成をサポートしています。
- **Intune MDM + MAM**: IT 管理者は、Intune モバイル デバイス管理 (MDM) に登録されているデバイスで MAM とアプリ保護ポリシーを使用したアプリの管理のみを行うことができます。 MDM と MAM を使用してアプリを管理するには、Azure Portal (https://portal.azure.com ) の Intune コンソールを使用する必要があります。
- **デバイス登録なしの MAM**: デバイス登録がない MAM や MAM-WE では、IT 管理者は、Intune MDM に登録されていないデバイス上で MAM とアプリ保護ポリシーを使用してアプリの管理を行うことしかできません。 つまり、サードパーティ EMM プロバイダーに登録されているデバイスで Intune によりアプリを管理できます。 MAM-WE を使用してアプリを管理するには、Azure Portal (https://portal.azure.com ) の Intune コンソールを使用する必要があります。 また、Intune では、サードパーティ製エンタープライズ モビリティ管理 (EMM) プロバイダーに登録されているデバイス上でも、MDM に全く登録されていないデバイス上でもアプリを管理することができます。 BYOD および Microsoft の EMS に関する詳細については、「[Microsoft Enterprise Mobility + Security (EMS) で BYOD を有効にするための技術の決定事項](../fundamentals/byod-technology-decisions.md)」を参照してください。

## <a name="app-management-capabilities-by-platform"></a>プラットフォーム別のアプリ管理機能

Intune では、アプリを実行するデバイス上で必要なアプリを取得するのに役立つさまざまな機能を提供しています。 次の表に、アプリの管理機能の概要を示します。

| アプリの管理機能 | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 | Windows Phone 8.1 |
|-------------------------- | -------------------------- | ---------- | ----- | ---------- | ----------------- |
| デバイスとユーザーにアプリを追加して割り当てる | はい | はい | はい | はい | はい |
| Intune に登録されていないデバイスにアプリを割り当てる | はい | はい | いいえ | いいえ | いいえ |
| アプリ構成ポリシーを使用してアプリのスタートアップ動作を制御する | はい | はい | いいえ | いいえ | いいえ |
| モバイル アプリ プロビジョニング ポリシーを使用して期限切れのアプリを更新する | いいえ | はい | いいえ | いいえ | いいえ |
| アプリ保護ポリシーでアプリ内の会社のデータを保護する | はい | はい | いいえ | いいえ <sup>1</sup> | いいえ |
| インストール済みのアプリから会社のデータのみを削除する (アプリの選択的ワイプ) | はい | はい | いいえ | はい | はい |
| アプリの割り当てを監視する | はい | はい | はい | はい | はい |
| アプリ ストアからのボリューム購入アプリを割り当てて追跡する | いいえ | いいえ | いいえ | はい | いいえ |
| デバイスへのアプリのインストールを強制する (必須) <sup>2</sup> | はい | はい | はい | はい | はい |
| 会社のポータルからデバイスへのオプション インストール (利用可能なインストール) | はい <sup>3</sup> | はい | はい | はい | はい |
| Web 上のアプリへのインストール ショートカット (Web リンク) | はい <sup>4</sup> | はい | はい | はい | はい |
| 社内 (基幹業務) アプリ | はい | はい | はい | はい | いいえ |
| ストアからのアプリ | はい | はい | いいえ | はい | はい |
| アプリを更新する | はい | はい | いいえ | はい | はい |

<sup>1</sup> Windows 10 を実行しているデバイスでアプリを保護するには、[Windows 情報保護](../protect/windows-information-protection-configure.md)の使用を検討してください。<br>
<sup>2</sup> Intune のみで管理されているデバイスに適用されます。<br>
<sup>3</sup> Intune では、Android Enterprise デバイス上にあるマネージド Google Play ストアから入手できるアプリがサポートされます。<br>
<sup>4</sup> Intune では、標準の Android Enterprise デバイス上にアプリへのショートカットを Web リンクとしてインストールする機能は提供されていません。 ただし、[複数アプリ専用の Android Enterprise デバイス](../configuration/device-restrictions-android-for-work.md#device-experience)では、Web リンクのサポートが提供されています。 


## <a name="get-started"></a>作業開始

アプリに関連する情報は、ほとんどが **[アプリ]** ワークロード内にあり、以下の手順でアクセスできます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
3. **[アプリ]** を選択します。

    ![[アプリ] ワークロード ウィンドウ](./media/app-management/apps-workload.png)

アプリ ワークロードでは、一般的なアプリの情報と機能にアクセスするためのリンクが提供されます。 

アプリ ワークロード ナビゲーション メニューの先頭で、一般的に使用されるアプリの詳細が示されます。
- **概要**:テナント名、MDM 機関、テナントの場所、アカウントの状態、アプリのインストール状態、アプリ保護ポリシーの状態を表示するには、このオプションを選択します。
- **すべてのアプリ**:利用可能なすべてのアプリの一覧を表示するには、このオプションを選択します。 このページからアプリを追加できます。 また、各アプリの状態と、各アプリが割り当てられているかどうかも確認できます。 詳しくは、[アプリの追加](apps-add.md)および[アプリの割り当て](apps-deploy.md)に関するページをご覧ください。
- **アプリの監視**
    - **[アプリ ライセンス]** :アプリ ストアのボリューム購入アプリを表示、割り当て、監視します。 詳しくは、[iOS ボリューム購入プログラム (VPP) アプリ](vpp-apps-ios.md)および[ビジネス向け Microsoft Store 一括購入アプリ](windows-store-for-business.md)に関するページをご覧ください。
    - **[検出されたアプリ]** : Intune によって割り当てられたか、デバイスにインストールされたアプリを表示します。 詳細については、「[Intune discovered apps (Intune で検出されたアプリ)](app-discovered-apps.md)」を参照してください。
    - **[アプリ インストールの状態]** : 作成したアプリ割り当ての状態を表示します。 詳しくは、「[Microsoft Intune でアプリの情報と割り当てを監視する](apps-monitor.md#device-and-user-status-graphs)」をご覧ください。
    - **[アプリの保護状態]** :選択したユーザーのアプリ保護ポリシーの状態を表示します。
- **[プラットフォーム別]** : プラットフォームを選択すると、プラットフォーム別に使用可能なアプリが表示されます。
    - Windows
    - iOS
    - macOS
    - Android
- **ポリシー**: 
    - **[アプリ保護ポリシー]** :このオプションを選択すると、アプリに設定を関連付けて、使用される会社のデータを保護できます。 たとえば、アプリの機能による他のアプリとの通信を制限することや、会社のアプリにアクセスしようとするユーザーに PIN の入力を求めることができます。 詳しくは、[アプリ保護ポリシー](app-protection-policies.md)に関するページをご覧ください。
    - **[アプリ構成ポリシー]** :ユーザーがアプリを実行するときに必要となる場合がある設定を指定するには、このオプションを選択します。 詳しくは、[アプリの構成ポリシー](app-configuration-policies-use-ios.md)、[iOS アプリ構成ポリシー](app-configuration-policies-use-ios.md)、および [Android アプリ構成ポリシー](app-configuration-policies-overview.md)に関するページをご覧ください。
    - **[iOS アプリ プロビジョニング プロファイル]** : iOS アプリには、プロビジョニング プロファイルと、証明書によって署名されたコードが含まれます。 証明書の期限が切れると、アプリを実行できなくなります。 Intune には、有効期限が近づいているアプリを持つデバイスに新しいプロビジョニング プロファイルのポリシーを事前に割り当てるツールが用意されています。 詳しくは、[iOS アプリ プロビジョニング プロファイル](app-provisioning-profile-ios.md)に関するページをご覧ください。
    - **[S モードの補足ポリシー]** : マネージド S モード デバイスでの追加アプリケーションの実行を承認するには、このオプションを選択します。 詳しくは、[S モードの補足ポリシー](apps-win32-s-mode.md)に関するページをご覧ください。
    - **[ポリシー セット]** : アプリ、ポリシー、および作成したその他の管理オブジェクトの割り当て可能なコレクションを作成するには、このオプションを選択します。 詳しくは、[ポリシー セット](../fundamentals/policy-sets.md)に関するページをご覧ください。
- **[その他]** :    
    - **[アプリの選択的ワイプ]** :このオプションを選択すると、選択したユーザーのデバイスから会社のデータのみを削除することができます。 詳しくは、[アプリの選択的ワイプ](apps-selective-wipe.md)に関するページをご覧ください。
    - **[アプリのカテゴリ]** :アプリのカテゴリ名を追加、ピン留め、削除します。
    - **[電子書籍]** : 一部のアプリ ストアでは、社内で使用するアプリやブックの複数のライセンスを購入できます。 詳細については、「[Microsoft Intune によるボリューム購入アプリとブックの管理](vpp-apps.md)」を参照してください。
- **[ヘルプとサポート]** :トラブルシューティング、サポートの要求、または Intune の状態の表示を行います。 詳しくは、[問題のトラブルシューティング](../fundamentals/help-desk-operators.md)に関するページをご覧ください。

### <a name="try-the-interactive-guide"></a>対話型ガイドを試す
「[Microsoft Endpoint Manager を使用してモバイル アプリケーションとデスクトップ アプリケーションを管理および保護する](https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager)」の対話型ガイドでは、Microsoft Endpoint Manager 管理センターを使用して、Intune での登録したデバイスの管理、ポリシー準拠の強制、組織のデータの保護を行う方法を説明します。</br></br>

> [!VIDEO https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager]

## <a name="additional-information"></a>追加情報
コンソール内の次の項目では、アプリに関連する機能が提供されます。
- **ビジネス向け Microsoft Store**:ビジネス向け Microsoft ストアとの統合を設定します。 その後、購入済みのアプリケーションを Intune に同期して割り当て、ライセンスの使用状況を追跡できるようになります。 詳しくは、[ビジネス向け Microsoft Store 一括購入アプリ](windows-store-for-business.md)に関するページをご覧ください。
- **[Windows Enterprise 証明書]** :基幹業務アプリを Windows マネージド デバイスに配布するために使うコード署名証明書の状態を適用または表示します。
- **[Windows Symantec 証明書]** :XAP および WP8.x appx ファイルを Windows 10 Mobile デバイスに配布するために必要となる、Symantec コード署名証明書の状態を適用または表示します。
- **[Windows サイドローディング キー]** :Windows サイドローディング キーを追加します。これを使うと、Windows ストアでアプリを公開およびダウンロードするのではなく、アプリを直接デバイスにインストールできます。 詳しくは、[Windows アプリのサイドロード](app-sideload-windows.md)に関するページをご覧ください。
- **[Apple VPP トークン]** : iOS/iPadOS Volume Purchase Program (VPP) のライセンスを適用および表示します。 詳しくは、[iOS/iPadOS 大量購入アプリ](vpp-apps-ios.md)に関するページをご覧ください。
- **[マネージド Google Play]** : マネージド Google Play は、Google のエンタープライズ アプリ ストアであり、Android Enterprise 用の唯一のアプリケーション ソースです。 詳細は、「[Intune で managed Google Play アプリを Android エンタープライズ デバイスに追加する](apps-add-android-for-work.md)」を参照してください。
- **カスタマイズ**:ポータル サイトをカスタマイズして会社のブランドを付与します。 詳しくは、[Intune ポータル サイトの構成](company-portal-app.md)に関するページをご覧ください。

アプリの詳細については、「[Microsoft Intune にアプリを追加する](../apps/apps-add.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

- [アプリを Microsoft Intune に追加する](apps-add.md)
