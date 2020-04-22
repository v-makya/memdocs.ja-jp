---
title: Windows 10 デバイスの共同管理
titleSuffix: Configuration Manager
description: Configuration Manager と Microsoft Intune の両方を使用して Windows 10 デバイスを同時に管理する方法について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/24/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: e06dc0d40eb6359d11ef31045989d7ed398b3687
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691000"
---
# <a name="what-is-co-management"></a>共同管理とは

<!-- 1350871 -->
共同管理は、既存の Configuration Manager の展開を Microsoft 365 のクラウドにアタッチするための主要な方法の 1 つです。 条件付きアクセスなど、クラウドを利用した追加機能のロックを解除するために役立ちます。

共同管理によって、Configuration Manager と Microsoft Intune の両方を使って Windows 10 デバイスを同時に管理することができます。 新しい機能を追加して、Configuration Manager 内の既存の投資をクラウドにアタッチできます。 共同管理を使用すると、組織に最適なテクノロジ ソリューションを柔軟に使用できます。

Windows 10 デバイスに Configuration Manager クライアントがあり、Intune に登録されている場合は、両方のサービスの恩恵を受けられます。 ワークロードがある場合、そのワークロードを制御して、機関を Configuration Manager から Intune に切り替えます。 Configuration Manager では、Intune に切り替えないワークロードを含む、他のすべてのワークロードと、共同管理でサポートされない Configuration Manager の他のすべての機能が引き続き管理されます。

また、個別のデバイス コレクションを使用してワークロードを試験運用することもできます。 試験運用を使用すると、大規模なグループを切り替える前に、デバイスのサブセットを使用して Intune 機能をテストできます。

![共同管理の概要図](media/co-management-overview.svg)

[図をフル サイズで表示する](media/co-management-overview.svg)

> [!Note]  
> Windows 10 デバイスを Configuration Manager と Microsoft Intune の両方で同時に管理するとき、この構成は*共同管理*と呼ばれます。 Configuration Manager でデバイスを管理し、サード パーティ製 MDM サービスに登録するとき、この構成は*共存*と呼ばれます。 1 台のデバイスに 2 つの管理機関を与えることは、2 つの間が適切に調整されなければ難しくなることがあります。 共同管理の場合、競合がないように Configuration Manager と Intune の間で[ワークロード](#workloads)が分散されます。 サード パーティ サービスとはこのやりとりがないため、共存の管理機能には制限があります。 詳細については、「[サード パーティ製 MDM と Configuration Manager の共存](coexistence.md)」を参照してください。

## <a name="paths-to-co-management"></a>共同管理へのパス

共同管理を達成するには、主に 2 つのパスがあります。  

- **既存の Configuration Manager クライアント**:既に Configuration Manager クライアントである Windows 10 デバイスを持っています。 ハイブリッド Azure AD を設定し、それらを Intune に登録します。  

- **新しいインターネットベースのデバイス**:Azure AD に参加し、自動的に Intune に登録する新しい Windows 10 デバイスを持っています。 共同管理状態にするには、Configuration Manager クライアントをインストールします。  

パスの詳細については、「[共同管理へのパス](quickstart-paths.md)」を参照してください。

## <a name="benefits"></a>利点

既存の Configuration Manager クライアントを共同管理に登録すると、すぐに次のような恩恵を受けられます。  

- 条件付きアクセスとデバイス コンプライアンス  

- Intune ベースのリモート操作 (例: 再起動、リモート制御、出荷時設定へのリセットなど)

- デバイスの正常性を一元的に把握  

- ユーザー、デバイス、およびアプリを Azure Active Directory (Azure AD) とリンク  

- Windows Autopilot による最新のプロビジョニング  

- リモート操作

共同管理からすぐに得られる価値の詳細については、「[クラウドの共同管理を使用した接続](quickstarts.md)」のクイック スタート シリーズを参照してください。

共同管理では、複数のワークロードに対して Intune を使用して調整することもできます。 詳細については、「[ワークロード](#workloads)」セクションを参照してください。

## <a name="prerequisites"></a>[前提条件]

共同管理には、次の領域に前提条件があります。

- [ライセンス](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [アクセス許可と役割](#permissions-and-roles)  

### <a name="licensing"></a>ライセンス

- Azure AD Premium

    > [!Note]  
    > Enterprise Mobility + Security (EMS) のサブスクリプションには、Azure Active Directory Premium と Microsoft Intune の両方が含まれています。

- 管理者が Intune ポータルにアクセスするために必要な、少なくとも 1 つの Intune ライセンス。

    > [!Tip]
    > テナントへのサインインに使用するアカウントには必ず Intune ライセンスを割り当ててください。 そうしないと、サインインが失敗し、"User not recognized (ユーザーが認識されません)" というエラー メッセージが表示されます。
    >
    > ユーザーに対して個別の Intune または EMS ライセンスを購入して割り当てる必要はなくなりました。 詳細については、「[Configuration Manager のブランチとライセンスに関してよく寄せられる質問](../core/understand/product-and-licensing-faq.md#bkmk_mem)」を参照してください。

### <a name="configuration-manager"></a>Configuration Manager

共同管理には、Configuration Manager バージョン 1710 以降が必要です。

Configuration Manager バージョン 1806 以降では、複数の Configuration Manager インスタンスを 1 つの Intune テナントに接続できます。 <!--1357944-->  

共同管理を有効にすることだけであれば、Azure AD を使用してサイトをオンボードする必要はありません。 [2 つ目のパス シナリオ](#paths-to-co-management)の場合、インターネットベースの Configuration Manager クライアントには、[クラウド管理ゲートウェイ](../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) が必要です。 CMG では、[クラウド管理のためにサイトが Azure AD にオンボードされている](../core/servers/deploy/configure/azure-services-wizard.md)必要があります。

### <a name="azure-ad"></a>Azure AD

- Windows 10 デバイスは、Azure AD に参加している必要があります。 次のいずれかの種類です。  

  - [ハイブリッド Azure AD 参加済み](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)。デバイスがオンプレミスの Active Directory に参加し、Azure Active Directory に参加している場合。  

  - [Azure AD のみに参加](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)。 (この種類は "クラウド ドメイン参加済み" とも呼ばれます)<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [Intune をセットアップする](https://docs.microsoft.com/intune/setup-steps)  

- [Windows 10 の自動登録を有効にする](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

デバイスを Windows 10 バージョン 1709 以降にアップグレードする 詳細については、[サービスとしての Windows の導入](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)に関する記事を参照してください。

> [!IMPORTANT]
> Windows 10 モバイル デバイスでは共同管理はサポートされません。

### <a name="permissions-and-roles"></a>アクセス許可と役割

<!--SCCMDocs issue #667-->
| 操作 | 必要な役割 |
|----|----|
| Configuration Manager でクラウド管理ゲートウェイを設定する | Azure の**サブスクリプション マネージャー** |
| Configuration Manager から Azure AD アプリを作成する | Azure AD の**全体管理者** |
| Configuration Manager で Azure AD アプリをインポートする | Configuration Manager の**完全な権限を持つ管理者**<br>その他の Azure 役割は必要はありません |
| Configuration Manager で共同管理を有効にする | Azure AD ユーザー<br>**すべての**スコープの権限を含め、Configuration Manager の**完全な権限を持つ管理者**<!--SCCMDoc issue 626--> |

Azure の役割について詳しくは、[さまざまな役割](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles)に関するページをご覧ください。

Configuration Manager の役割の詳細については、「[ロール ベース管理の基礎](../core/understand/fundamentals-of-role-based-administration.md)」を参照してください。

## <a name="workloads"></a>ワークロード

ワークロードを切り替える必要はありません。準備ができたときに個別に行うこともできます。 Configuration Manager では、Intune に切り替えないワークロードを含む、他のすべてのワークロードと、共同管理でサポートされない Configuration Manager の他のすべての機能が引き続き管理されます。

共同管理では次のワークロードがサポートされます。

- コンプライアンス ポリシー  

- Windows Update のポリシー  

- リソースのアクセス ポリシー  

- Endpoint Protection  

- デバイスの構成  

- Office クイック実行アプリ  

- クライアント アプリ  

詳細については、「[ワークロード](workloads.md)」を参照してください。

## <a name="monitor-co-management"></a>共同管理の監視

共同管理ダッシュボードを利用すれば、お使いの環境で共同管理しているコンピューターを確認できます。 各種グラフを見ることで、対処が必要なデバイスを特定できます。

![共同管理ダッシュボードのスクリーンショット](media/co-management-dashboard.png)

詳細については、[共同管理の監視方法](how-to-monitor.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

- [共同管理のすぐに得られる価値と基本の詳細](quickstarts.md)  

- [チュートリアル:既存の Configuration Manager クライアントの共同管理を有効にする](tutorial-co-manage-clients.md)  
