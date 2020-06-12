---
title: Azure AD でのクライアントのインストール
titleSuffix: Configuration Manager
description: 認証のために Azure Active Directory を使用して、Windows 10 デバイスで Configuration Manager クライアントをインストールして割り当てる
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b447e5c8d34a4b8758fa0fd6109113b0675a635
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347017"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる

Azure AD 認証を使用して Windows 10 デバイスで Configuration Manager クライアントをインストールするには、Azure Active Directory (Azure AD) と Configuration Manager を統合します。 クライアントは、HTTPS が有効な管理ポイントまたは拡張 HTTP 用に有効化されたサイト内の任意の管理ポイントと直接通信するイントラネット上に配置することができます。 CMG を通じて、あるいはインターネット ベース管理ポイントでインターネット ベースの通信を行うこともできます。 このプロセスでは Azure AD を使用して、Configuration Manager サイトに対してクライアントを認証します。 Azure AD を使用すると、クライアント認証証明書を構成して使用する必要がなくなります。

一部の顧客にとっては、Azure AD を設定する方が、証明書ベースの認証用に公開キー基盤を設定するよりも簡単な場合があります。 一部の機能ではサイトを Azure AD にオンボードすることが必要ですが、クライアントは必ずしも Azure AD 参加済みである必要はありません。<!-- SCCMDocs issue 1259 --> 詳細については、以下の記事を参照してください。

- [Azure Active Directory の計画](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [共同管理用に Azure AD を使用する](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>始める前に

- Azure AD テナントは前提条件です。  

- デバイスの要件:  

  - Windows 10  

  - Azure AD への参加、純粋なクラウド ドメイン参加、またはハイブリッド Azure AD 参加  

- ユーザーの要件:  

  - サインインしたユーザーは Azure AD の ID である必要があります。

  - ユーザーがフェデレーション ID または同期 ID である場合、Configuration Manager の [Active Directory ユーザー探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)と [Azure AD ユーザー探索](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)の両方を構成する必要があります。 ハイブリッド ID の詳細については、「[ハイブリッド ID 導入戦略の定義](https://docs.microsoft.com/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-identity-adoption-strategy)」を参照してください。<!--497750-->

- 管理ポイント サイト システムの役割に関する[既存の前提条件](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq)に加え、このサーバーでは **ASP.NET 4.5** も有効にします。 ASP.NET 4.5 を有効にするときに自動的に選択される他のすべてのオプションを含めます。  

- 管理ポイントで HTTPS が必要かどうかを判断します。 詳細については、「[HTTPS 用の管理ポイントを有効にする](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)」を参照してください。  

- 必要に応じて、インターネット ベースのクライアントを展開するために[クラウド管理ゲートウェイ](../manage/cmg/plan-cloud-management-gateway.md) (CMG) を設定します。 Azure AD で認証するオンプレミス クライアントの場合、CMG は必要ありません。  

> [!TIP]
> バージョン 2002 以降、<!--5686290--> Configuration Manager では、内部ネットワークに接続することがあまりなく、Azure Active Directory (Azure AD) に参加できず、PKI によって発行された証明書をインストールする方法を持たない、インターネット ベースのデバイスに対するサポートが拡張されています。 詳細については、[CMG のトークンベースの認証](deploy-clients-cmg-token.md)に関する記事をご覧ください。

## <a name="configure-azure-services-for-cloud-management"></a>クラウド管理用の Azure サービスの構成

最初のステップとして、Azure AD には Configuration Manager サイトを接続します。 このプロセスの詳細については、「[Azure サービスの構成](../../servers/deploy/configure/azure-services-wizard.md)」を参照してください。 **クラウド管理**サービスへの接続を作成します。

**クラウド管理**へのオンボーディングの一環として、[Azure AD ユーザー探索](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)を有効にします。

これらの操作が完了すると、Configuration Manager サイトが Azure AD に接続されます。

## <a name="configure-client-settings"></a>クライアント設定を構成する

これらのクライアント設定は、Windows 10 デバイスをハイブリッド参加済みに構成するのに役立ちます。 また、インターネット ベースのクライアントで CMG とクラウド配布ポイントを使用することもできます。

1. **[クラウド サービス]** グループで、次のクライアント設定を構成します。 詳しくは、「[クライアント設定を構成する方法](configure-client-settings.md)」をご覧ください。

    - **クラウド配布ポイントへのアクセスを許可する**:この設定を有効にすると、インターネットベースのデバイスが、構成マネージャー クライアントのインストールに必要なコンテンツを取得できるようになります。 クラウド配布ポイントでコンテンツを使用できない場合、デバイスは CMG からコンテンツを取得できます。 クライアント インストール ブートストラップでは、CMG にフォールバックするまで 4 時間、クラウド配布ポイントを再試行します。<!--495533-->  

    - **[新しい Windows 10 ドメインに参加しているデバイスを自動的に Azure Active Directory に登録する]** : **[はい]** または **[いいえ]** に設定します。 既定の設定は **[はい]** です。 この動作は、Windows 10 バージョン 1709 の既定でもあります。

        > [!TIP]
        > ハイブリッド参加済みデバイスは、オンプレミスの Active Directory ドメインに参加し、Azure AD に登録されます。 詳細については、「[ハイブリッド Azure AD 参加済みデバイス](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid)」を参照してください。<!-- MEMDocs#325 -->

    - **クライアントでクラウド管理ゲートウェイを使用できるようにする** **[はい]** (既定値)、または **[いいえ]** に設定します。  

2. クライアント設定を必要なデバイスのコレクションに展開します。 ユーザー コレクションには、これらの設定を展開しないでください。

デバイスがハイブリッド参加済みであることを確認するには、コマンド プロンプトで `dsregcmd.exe /status` を実行します。 デバイスが Azure AD 参加済みまたはハイブリッド参加済みである場合、結果の **[AzureAdjoined]** フィールドに **[YES]** と表示されます。 詳細については、[dsregcmd コマンド - デバイスの状態](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-device-dsregcmd)に関するページを参照してください。

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Azure AD の ID を使用してクライアントをインストールして登録する

Azure AD の ID を使用してクライアントを手動でインストールするには、まず、「[クライアントの手動インストール方法](deploy-clients-to-windows-computers.md#BKMK_Manual)」の一般的なプロセスを確認します。

> [!Note]  
> デバイスは Azure AD に接続する際にインターネットにアクセスする必要がありますが、インターネット ベースである必要はありません。

次の例は、コマンド ラインの一般的な構造を示しています。`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

詳細については、「[クライアント インストールのプロパティ](about-client-installation-properties.md)」を参照してください。

**/mp** パラメーターと **CCMHOSTNAME** プロパティでは、シナリオに応じて、以下のいずれかを指定します。

- オンプレミスの管理ポイント。 **/mp** パラメーターのみを指定します。 **CCMHOSTNAME** プロパティは必要ありません。
- クラウド管理ゲートウェイ
- インターネット ベースの管理ポイント

**SMSMP** プロパティでは、オンプレミスまたはインターネット ベースの管理ポイントを指定します。

この例では、クラウド管理ゲートウェイを使用します。 サンプルの値が次のように置き換えられます。`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

サイトでは、クラウド管理ゲートウェイ (CMG) に対して Azure AD の追加情報が公開されます。 Azure AD に参加しているクライアントは、ccmsetup プロセスの間に、参加している同じテナントを使用して、CMG からこの情報を取得します。 この動作により、複数の Azure AD テナントがある環境でのクライアントのインストールがさらに簡略化されます。 必要な ccmsetup プロパティは、**CCMHOSTNAME** と **SMSSiteCode** の 2 つだけです。<!--3607731-->

Microsoft Intune で Azure AD の ID を使用してクライアントのインストールを自動化する場合は、「[How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)」 (共同管理用にインターネット ベースのデバイスを準備する方法) を参照してください。

## <a name="next-steps"></a>次のステップ

完了したら、引き続き[クライアントの監視と管理](../manage/monitor-clients.md)ができます。
