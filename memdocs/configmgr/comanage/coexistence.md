---
title: サード パーティ製 MDM の共存
titleSuffix: Configuration Manager
description: Configuration Manager でサード パーティ製 MDM を使用する方法について説明します
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 055d79c56417135e2b08a31bc05a3ca30b5fd581
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695105"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>サード パーティ製 MDM と Configuration Manager の共存

Windows 10 デバイスを Configuration Manager と Microsoft Intune の両方で同時に管理するとき、この機能は[共同管理](overview.md)と呼ばれます。 Configuration Manager でデバイスを管理し、サード パーティ製 MDM サービスに登録するとき、この機能は*共存*と呼ばれます。 1 台のデバイスに 2 つの管理機関を与えることは、2 つの間が適切に調整されなければ難しくなることがあります。 共同管理の場合、競合がないように Configuration Manager と Intune の間で[ワークロード](workloads.md)が分散されます。 サード パーティ サービスとはこのやりとりがないため、共存の管理機能には制限があります。

Configuration Manager クライアントは、Azure Active Directory に参加しており、Windows 10 バージョン 1709 以降を実行しているデバイス上でサード パーティ製 MDM サービスと共存できます。 そのデバイスは次の種類のいずれかになります。

- [Azure AD のみに参加](/azure/active-directory/devices/azureadjoin-plan)。 (この種類は "クラウド ドメイン参加済み" とも呼ばれます)  

- [Hybrid ドメイン参加済み](/azure/active-directory/devices/hybrid-azuread-join-plan): デバイスがオンプレミスの Active Directory に参加し、Azure Active Directory に登録されている場合。  

> [!Note]  
> [個人所有デバイス](/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device)はサポートされません。  

サード パーティ製 MDM サービスでもデバイスが管理されていることが Configuration Manager クライアントで検出されると、Configuration Manager では、特定のワークロードの場所が自動的に無効になります。 この動作により、MDM サービスはこれらの機能を引き継ぐことができます。 クライアント上で設定が競合し、デバイスやユーザー エクスペリエンスに悪影響を与える可能性も防ぎます。 このケースでは、Configuration Manager の次のワークロードが無効になります。

- VPN、Wi-Fi、電子メール、証明書設定のリソース アクセス ポリシー
- 旧パッケージを含む、アプリケーション管理
- ソフトウェア更新プログラムのスキャンとインストール
- Windows Defender のマルウェア対策保護機能スイートであるエンドポイント保護
- 条件付きアクセスのコンプライアンス ポリシー
- デバイスの構成
- Office クイック実行管理

Configuration Manager クライアントでは、次の読み取り専用操作を続行することで、サード パーティ管理機関との競合が回避されます。

- ハードウェアとソフトウェアのインベントリ
- 資産インテリジェンス
- ソフトウェア使用状況測定
- 電源管理レポート

Configuration Manager と Intune の共同管理の長所については、[共同管理の長所](overview.md#benefits)に関するページを参照してください。