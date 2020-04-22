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
ms.openlocfilehash: 7a670660bcf7b3f5cb8209aaf6d0b59eb0f343e4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691240"
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
    - 次の [Azure AD ハイブリッド ID オプション](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin)のいずれか:  
       - [シームレス シングル サインオン (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) を使った[パスワード ハッシュ同期](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization)
       - [シームレス シングル サインオン (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) を使った[パススルー認証](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta)
       - [フェデレーション SSO (Active Directory フェデレーション サービス (AD FS) を使用)](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium ライセンス
    - ハイブリッド Azure AD 参加を構成する (オプションを 1 つ選択する):
        - マネージド ドメイン用
        - フェデレーション ドメイン用
- ハイブリッド Azure AD 参加のクライアント エージェント設定
- Intune へのデバイスの自動登録を構成する
- Intune ユーザー ライセンスを割り当てる
- Configuration Manager で共同管理を有効にする

このパスのチュートリアルについては、「[Tutorial:Enable co-management for existing Configuration Manager clients](tutorial-co-manage-clients.md)」 (チュートリアル: 既存の Configuration Manager クライアントの共同管理を有効にする) を参照してください。



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a> パス 2:最新のプロビジョニングを使用してブートストラップする

設定には以下が必要です。

1. [拡張 HTTP をセットアップする](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Azure でクラウド サービスを作成する](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [クラウド管理ゲートウェイを使用するように管理ポイントとクライアントを構成する](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Intune を使用して Configuration Manager クライアントを展開する](how-to-prepare-Win10.md)  

> [!Note]  
> このパスのチュートリアルは準備中です。

