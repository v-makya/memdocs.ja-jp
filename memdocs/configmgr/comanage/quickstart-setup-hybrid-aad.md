---
title: ハイブリッド Azure AD をセットアップする
titleSuffix: Configuration Manager
description: ご利用の環境に現在、ドメイン参加済みの Windows 10 デバイスがある場合は、共同管理を有効にする前にハイブリッド Azure AD を設定します
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 405303b3988e8c853ba30e8fb6d620d782b0474e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694901"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>共同管理用にハイブリッド Azure AD を設定する

オンプレミスの Active Directory に参加している Windows 10 デバイスがある場合は、Configuration Manager で共同管理を有効にする前に、まず、これらのデバイスを Azure Active Directory (Azure AD) に参加させます。 このプロセスをハイブリッド Azure AD 参加といいます。 

次のビデオでは、シニア プログラム マネージャーの Sandeep Deo とプロダクト マーケティング マネージャーの Adam Harbour が、Azure AD でのデバイスの構成について説明し、デモを行っています。

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

ハイブリッド Azure AD 参加プロセスでは、オンプレミスのドメイン参加済みデバイスを Azure AD に自動的に登録します。 このプロセスについて詳しくは、以下の記事をご覧ください。
- [Azure Active Directory のデバイス管理の概要](/azure/active-directory/device-management-introduction) 
- [ハイブリッド Azure AD 参加を計画する方法](/azure/active-directory/devices/hybrid-azuread-join-plan)

ハイブリッド Azure AD 参加は、共同管理用の重要な基礎の 1 つです。 このプロセスは、一部の顧客にとって困難な場合があります。例を以下に示します。
- 組織でサード パーティの ID ソリューションが使用されている 
- Active Directory フェデレーション サービス (ADFS) の設定の複雑さ

これらの課題を解決する際に、何らかのガイダンスを使用する場合があります。 この記事は遅延を軽減するのに役立ちます。


## <a name="how-to-do-it"></a>実行方法

デバイスは、保護する必要がある ID を作成するときのユーザーに似ています。 いつでもどこでもデバイスの ID を保護できるようにするには、Azure AD にそのデバイスの ID を取り込む必要があります。

使用するドメインの種類に基づいて、主な 2 つの実行方法があります。 次のドメインの種類のいずれかに対して、ハイブリッド Azure AD 参加を構成します。  
- [フェデレーション ドメイン](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [マネージド ドメイン](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

上記の 2 つの方法では最適なエクスペリエンスが提供されます。 完全な手動プロセスを含む詳細については、次の記事を参照してください。
- [ハイブリッド Azure AD 参加済みデバイスを手動で構成する](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [ハイブリッド Azure AD の ADFS パススルー認証](/windows-server/identity/ad-fs/ad-fs-overview)。Azure AD 検出が含まれます  

トラブルシューティングのガイダンスについては、[Windows 10 ハイブリッド Azure AD 参加のトラブルシューティング ガイド](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)に関するページを参照してください。



## <a name="case-study"></a>導入事例

ネットワーク内に 100,000 人を超えるユーザーが存在するヨーロッパの大規模なソフトウェア会社では、ハイブリッド Azure AD 参加の有効化に向けて、詳細かつ段階的なアプローチを取りました。

計画段階では、ハイブリッド Azure AD 参加が共同管理をサポートする重要な要素であるため、Configuration Manager 管理者は ID チームと共に作業を行いました。 このソフトウェア会社には多くの ADFS 規則があり、その一部は複雑なものでした。 この課題に対処するために、ID チームでは、ハイブリッド Azure AD 参加を有効にする前に既存の ADFS 規則を確認しました。 また、IT チームは、Azure AD Connect を最新バージョンにアップグレードすることにしました。 Azure AD Connect では、現在、ハイブリッド Azure AD 参加を有効にするための自動化されたプロセス フローが提供されています。

実稼働前の環境での正常なデプロイおよびテストの後に、この顧客は実稼働環境の不動産全体でハイブリッド Azure AD 参加を有効にしました。 1 週間以内に、すべての Windows 10 デバイスの共同管理を行いました。



## <a name="contact-fasttrack"></a>FastTrack への問い合わせ

プロセスの任意の時点で Azure AD の設定サポートが必要な場合は、[Microsoft FastTrack](https://Microsoft.com/FastTrack/) に移動し、サインインしてサポートを要求してください。 

詳細については、[FastTrack からのサポートの取得](quickstart-fasttrack.md)に関するページを参照してください。