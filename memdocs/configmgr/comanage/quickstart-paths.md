---
title: 共同管理へのパス
titleSuffix: Configuration Manager
description: 共同管理を設定するための主な 2 つの方法の前提条件について理解します。
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a685e10ecdb2f6fac8d5634fd932facf52fddcb0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694952"
---
# <a name="paths-to-co-management"></a>共同管理へのパス

共同管理を設定するための主な方法は 2 つあります。 各パスの前提条件を理解することが重要です。 それぞれに Azure Active Directory (Azure AD)、Configuration Manager、Microsoft Intune、および Windows 10 のいくつかの組み合わせが必要です。 

1. [既存の Configuration Manager で管理されているデバイスを Intune に自動登録する](#bkmk_path1)  
2. [最新のプロビジョニングを使用して Configuration Manager クライアントをブートストラップする](#bkmk_path2)  

![共同管理パスの図](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a> パス 1:既存のクライアントを自動登録する

このパスを使用すれば、既存の Configuration Manager で管理されているデバイスを Intune にすばやく登録することができます。 Configuration Manager からのこれらのデバイスの管理は、共同管理を有効にする前のものと変わりません。 これで、クラウドベースの利点がすべて得られます。 このパスはユーザーに対して透過的です。

設定には以下が必要です。
- Hybrid Azure AD
    - 次の [Azure AD ハイブリッド ID オプション](/azure/active-directory/hybrid/plan-connect-user-signin)のいずれか:  
       - [シームレス シングル サインオン (SSO)](/azure/active-directory/hybrid/how-to-connect-sso) を使った[パスワード ハッシュ同期](/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization)
       - [シームレス シングル サインオン (SSO)](/azure/active-directory/hybrid/how-to-connect-sso) を使った[パススルー認証](/azure/active-directory/hybrid/how-to-connect-pta)
       - [フェデレーション SSO (Active Directory フェデレーション サービス (AD FS) を使用)](/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium ライセンス
    - ハイブリッド Azure AD 参加を構成する (オプションを 1 つ選択する):
        - マネージド ドメイン用
        - フェデレーション ドメイン用
- ハイブリッド Azure AD 参加のクライアント エージェント設定
- Intune へのデバイスの自動登録を構成する
- Configuration Manager で共同管理を有効にする

このパスのチュートリアルについては、「[Tutorial:Enable co-management for existing Configuration Manager clients](tutorial-co-manage-clients.md)」 (チュートリアル: 既存の Configuration Manager クライアントの共同管理を有効にする) を参照してください。



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a> パス 2:最新のプロビジョニングを使用してブートストラップする

設定には以下が必要です。

1. [拡張 HTTP をセットアップする](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Azure でクラウド サービスを作成する](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [クラウド管理ゲートウェイを使用するように管理ポイントとクライアントを構成する](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Intune を使用して Configuration Manager クライアントを展開する](how-to-prepare-Win10.md)  

このパスのチュートリアルについては、「[Tutorial:新しいインターネットベースのデバイスの共同管理を有効にする](tutorial-co-manage-new-devices.md)」をご覧ください。