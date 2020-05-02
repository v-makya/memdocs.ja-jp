---
title: ファイルを含める
description: インクルード ファイル
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183052"
---
以下の通知では、今後の Intune の変更と機能に備えるために役立つ重要な情報が提供されます。

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Windows 10 Mobile 終了のための Microsoft Intune のサポート<!--3544938-->
Windows 10 Mobile の Microsoft メインストリーム サポートは、2019 年 12 月に終了しました。 このサポートの声明に記載されているように、Windows 10 Mobile のユーザーは、新しいセキュリティ更新プログラム、セキュリティ以外の修正プログラム、無償のサポート オプション、Microsoft からのオンライン技術コンテンツ更新プログラムを受け取ることができなくなります。 Microsoft Intune は、すべてのモバイル OS のサポートに基づいて、2020 年 8 月 10 日に Windows 10 Mobile アプリと Windows 10 Mobile オペレーティング システムの両方のポータル サイトのサポートを終了することになりました。

#### <a name="how-does-this-affect-me"></a>ユーザーへの影響
Windows 10 Mobile のデバイスが組織に展開されている場合、今から 2020 年 8 月 10 日まで、新しいデバイスを登録したり、ポリシーとアプリを追加または削除したり、管理設定を更新したりできます。 8 月 10 日以降は、新しい登録が停止され、最終的に Intune UI から Windows 10 Mobile の管理が削除されます。 デバイスが Intune サービスにチェックインされなくなり、デバイスとポリシーのデータが削除されます。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>この変更に対して必要な準備
Intune レポートをチェックして、影響を受ける可能性のあるデバイスまたはユーザーを確認できます。 **[デバイス]**  >  **[すべてのデバイス]** の順に移動し、OS でフィルター処理します。 さらに列を追加して、Windows 10 Mobile を稼働しているデバイスを持つ組織内のユーザーの特定に役立てることができます。 エンド ユーザーに対して、デバイスのアップグレードや、会社にアクセスするためのデバイスの使用中止を要求してください。


### <a name="end-of-support-for-legacy-pc-management"></a>従来の PC 管理のサポート終了

従来の PC 管理は 2020 年 10 月 15 日にサポートが終了します。 デバイスを Windows 10 にアップグレードし、Intune による管理が継続されるようにモバイル デバイス管理 (MDM) デバイスとして再登録してください。

[詳細情報](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Android デバイス管理者のサポートの縮小<!--5857738-->
Android デバイス管理者 ("従来の" Android 管理とも呼ばれ、Android 2.2 でリリースされました) は、Android デバイスを管理する方法の 1 つです。 しかし、[Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (Android 5.0 でリリース) では、強化された管理機能を使用できるようになりました。 Google では、より豊富で安全な最新のデバイス管理に移行するための努力の一環として、新しい Android リリースでのデバイス管理者のサポートを縮小させています。

#### <a name="how-does-this-affect-me"></a>ユーザーへの影響
Google によるこのような変更により、Intune ユーザーは次のような影響を受けます。  
- Intune では、Android 10 以降を実行している、デバイス管理者が管理する Android デバイスのフル サポートは、2020 年度第 2 四半期までのみ提供できます。 この時以降、Android 10 以降を実行している、デバイス管理者が管理するデバイスは、まったく管理できなくなります。 具体的には、影響を受けるデバイスが新しいパスワード要件を受け取ることはありません。
    - Samsung Knox デバイスは、この時間枠内に影響を受けることはありません。これは、Intune と Knox プラットフォームとの統合によって延長サポートが提供されるためです。 これにより、デバイス管理者の管理の移行を計画する時間を増やすことができます。    
- デバイス管理者が管理する Android デバイスで、Android 10 より前の Android バージョンのままであるものは影響を受けません。デバイス管理者で引き続き完全に管理できます。    
- Google では、Android 10 以降を稼働しているすべてのデバイスに対して、ポータル サイトのようなデバイス管理者の管理エージェントを使ってデバイス識別子の情報にアクセスする機能を制限しています。 この制限により、Android 10 以降にデバイスを更新すると、次の Intune 機能が影響を受けます。  
    - VPN のネットワーク アクセス制御が機能しなくなる。   
    - IMEI またはシリアル番号を使用した企業所有のデバイスの識別で、デバイスが企業所有として自動的にマークされなくなる。  
    - Intune で IT 管理者に IMEI とシリアル番号が表示されなくなる。 
        > [!NOTE]
        > これが影響を与えるのは、デバイス管理者が管理するデバイスで Android 10 以降のもののみです。Android Enterprise として管理されているデバイスには影響しません。 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>この変更に対して必要な準備
2020 年度第 3 四半期に予定されている機能の縮小を回避するために、次のことをお勧めします。
- 新しいデバイスをデバイス管理者の管理にオンボードしない。
- デバイスが Android 10 への更新プログラムを受け取ることが予想される場合は、それをデバイス管理者の管理から外し、Android Enterprise 管理、アプリ保護ポリシーのいずれかまたは両方に移行する。

#### <a name="additional-information"></a>追加情報
- [デバイス管理者から Android Enterprise への移行に関する Google のガイダンス](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [デバイス管理者 API の廃止計画に関する Google のドキュメント](https://developers.google.com/android/work/device-admin-deprecation)