---
title: 共同管理に Azure AD を使用する
titleSuffix: Configuration Manager
description: Azure AD を利用すれば、クラウド環境とオンプレミス環境の両方で、ユーザーの生産性とリソースのセキュリティを改善できます
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a84247482ddece88208e83fec545afc5e953a070
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691290"
---
# <a name="use-azure-ad-for-co-management"></a>共同管理に Azure AD を使用する

クラウドでは、新しい制御レベルとして ID が使用されます。 Azure Active Directory (Azure AD) を利用すれば、クラウド環境とオンプレミス環境の両方にわたってユーザー、デバイス、アプリケーションをリンクできます。 Azure AD にデバイスを登録することで、ユーザーの生産性とリソースのセキュリティを改善できます。 Azure AD にデバイスを登録することは、共同管理とデバイスベースの条件付きアクセスの基礎です。

デバイスベースの条件付きアクセスに関する詳細については、「[方法: 条件付きアクセスを使用してクラウド アプリへのアクセスにマネージド デバイスを要求する](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)」を参照してください。

次のビデオでは、シニア プログラム マネージャーの Sandeep Deo とプロダクト マーケティング マネージャーの Adam Harbour が共同管理のための Azure AD について説明し、デモを行います。

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD は、組織にニーズに合わせて会社所有デバイス向けに 2 つのオプションを用意しています。  

- **Azure AD 参加済みデバイス**:Windows 10 デバイスを Azure AD に参加させますが、オンプレミス Active Directory に参加させる必要はありません  

  - Windows 10 をサポートしています

  - 設定の際、オンプレミス環境に構成を追加する必要はありません  

  - Azure AD でいくつかの設定を有効にすることで、ユーザーは Windows セットアップ エクスペリエンス (OOBE) 経由で Azure AD にデバイスを参加させることができます  

  - 詳細については、「[How to: Azure AD 参加の実装を計画する](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)」を参照してください  

- **Hybrid Azure AD 参加済みのデバイス**:既存のドメイン参加済みデバイスを Azure AD に参加させます  

  - Windows 10、Windows 8.1、Windows 7 をサポートしています

  - AD FS 要求または Azure AD Connect を利用してセットアップします  

  - Windows 10 の場合、コンピューターに関連して参加が行われるため、ユーザーは追加の手順を行う必要がありません  

  - 詳細については、「[方法: Hybrid Azure Active Directory 参加の実装を計画する](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)」をご覧ください  

いずれのオプションでも、ユーザーには同様の機能が提供されます。 ニーズに合わせて自由に選択できます。 たとえば、Active Directory に参加していなくても、Azure AD 参加済みのコンピューターから[オンプレミス リソースにアクセス](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso)できます。

[認証方法](https://docs.microsoft.com/azure/active-directory/hybrid/choose-ad-authn)に関係なく、さまざまな環境で Azure AD にデバイスを参加させることができます。 たとえば、フェデレーション認証やクラウド認証を利用できます。

オンプレミス Active Directory を既に導入している場合、いずれのオプションも簡単にセットアップできます。

## <a name="benefits"></a>利点

デバイスを Azure AD に参加させると、組織に次の利点が与えられます。

### <a name="single-sign-on-to-cloud-resources"></a>クラウド リソースにシングル サインオン

Azure AD に参加しているデバイスでは、一本化した方法であらゆるクラウド リソースとオンプレミス リソースにアクセスできます。 Azure AD に参加している Windows コンピューターにサインインすると、追加のサインイン プロンプトが表示されることなく、すべてのアプリケーションにシングル サインオンします。  

### <a name="windows-hello-for-business"></a>Windows Hello for Business

Windows Hello for Business を利用すると、パスワードなしの強固な認証が Windows 10 に導入されます。 Azure AD にデバイスを参加させると、クラウド リソースとオンプレミス リソースの両方について、ユーザー基盤全体で Windows Hello for Business を有効にすることができます。 Windows Hello for Business を有効にすると、複雑なパスワードを覚えなければならない、うっかりパスワードを公開してしまうといった問題がなくなります。 そのサインイン プロセスは単純ながら安全です。

詳細については、「[Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)」を参照してください。  

### <a name="device-based-conditional-access"></a>デバイスベースの条件付きアクセス

デバイスの状態に基づく条件付きアクセスを有効にし、組織のデータ保護能力を上げます。 デバイスベースの条件付きアクセスには、マネージド デバイスが必要です。 このデバイスは、準拠デバイスか Azure AD 参加済みデバイスでなければなりません。 Azure AD 参加済みデバイスの場合、デバイスを準拠デバイスとして設定するには Intune が必要です。 しかしながら、ハイブリッド Azure AD 参加済みデバイスの場合、デバイスの状態自体を利用し、条件付きアクセスが評価されます。 共同管理には、ハイブリッド Azure AD 参加済みデバイスの場合、Intune 経由で準拠を確認できるという付加的なアドバンテージがあります。 この機能により、デバイスの構成を変えてしまうことがありません。

デバイスベースの条件付きアクセスに関する詳細については、「[方法: 条件付きアクセスを使用してクラウド アプリへのアクセスにマネージド デバイスを要求する](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)」を参照してください。  

### <a name="automatic-device-licensing"></a>デバイス ライセンスの自動付与

Azure AD に参加する Windows 10 デバイスはすべて、ライセンス チェックを受けます。 そのチェックにより、Microsoft クラウド経由で Pro から Enterprise に自動的にアップグレードできます。 関連サブスクリプションをユーザーから削除すると、デバイスはそのライセンスを自動的にダウングレードします。 この機能により、Windows ライセンスを 1 つの制御枠から管理できます。複雑なプロセスまたはオンプレミス システムがありません。

### <a name="self-service-functionality"></a>セルフ サービス機能

セルフ サービス機能には、セルフサービス パスワード リセットと BitLocker 回復キーが含まれています。 Azure AD では、パスワードをリセットしたり、BitLocker 回復キーにアクセスしたりする直接的な選択肢が与えられます。 Azure AD を使用し、Web ブラウザーからではなく、Windows ロック画面から直接、パスワードをリセットできます。 以上の機能により、ユーザーは滞りなくシステムを利用し、組織のヘルプデスク コストを下げることができます。  

詳細については、「[チュートリアル: Azure Active Directory のセルフサービス パスワード リセットを使用して、ユーザーが自分のアカウントのロック解除またはパスワードのリセットを実行できるようにする](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-enable-sspr)」をご覧ください。

### <a name="enterprise-state-roaming"></a>Enterprise State Roaming

Azure AD に参加しているデバイスはすべて、その設定をクラウドに同期できます。 ユーザーがサインインするデバイスはすべて、その全設定を同期するため、生産性が上がります。  

## <a name="value-proposition"></a>価値提案

いずれかの方法で Azure AD にデバイスを参加させることで、デジタル変革が加速します。 Microsoft 365 から与えられる機能が増えます。 使い勝手とデータのセキュリティが向上します。

Azure AD は次のように作業負荷を軽減できます。

- 組織のすべての ID を 1 か所で管理します  

- セルフサービス パスワード リセットを有効にすることでヘルプデスクのコストを削減します。 ユーザーはいつでも自分のデバイスの Windows 10 ロック画面からパスワードをリセットできます。  

## <a name="configure"></a>構成

オンプレミス Active Directory 環境を既に用意しているとき、ドメイン参加済みデバイスを Azure AD に参加させる場合、ハイブリッド Azure AD 参加済みデバイスを構成します。 詳細については、「[方法: ハイブリッド Azure Active Directory 参加の実装を計画する](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)」をご覧ください。

Configuration Manager には、[新しい Windows 10 ドメイン参加済みデバイスを Azure AD に自動的に登録する](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory)ためのクライアント設定があります。 クライアント設定の構成の詳細については、[クライアント設定を構成する方法](../core/clients/deploy/configure-client-settings.md)に関するページをご覧ください。

オンプレミス ドメインには参加させず、デバイスの Azure AD 参加を構成する場合、ご利用の環境での Azure AD 参加の考慮事項を見直してください。 Azure AD 参加を決めたら、組織にニーズに合わせ、さまざまな方法でデプロイできます。 詳細については、以下の記事を参照してください。

- [方法:Azure AD 参加の実装を計画する](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [プロビジョニング オプションを理解する](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  
