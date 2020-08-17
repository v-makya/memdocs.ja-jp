---
title: ファイルを含める
description: インクルード ファイル
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/10/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: af506f9eee80d167b42827f93958fc2a3a5741a4
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051632"
---
以下の通知では、今後の Intune の変更と機能に備えるために役立つ重要な情報が提供されます。

### <a name="microsoft-intune-ends-support-for-windows-phone-81-and-windows-10-mobile---3544938-3544909---"></a>Microsoft Intune での Windows Phone 8.1 と Windows 10 Mobile のサポートが終了<!-- 3544938, 3544909 -->
Windows Phone 8.1 に対する Microsoft のメインストリーム サポートは 2017 年 7 月に終了し、拡張サポートは 2019 年 6 月に終了しました。 Windows Phone 8.1 用のポータル サイト アプリは、2017 年 10 月から維持モードになっています。 さらに、2020 年 2 月 20 日に、Windows Phone 8.1 に対する Microsoft Intune のサポートが終了しました。 

Windows 10 Mobile の Microsoft メインストリーム サポートは、2019 年 12 月に終了しました。 サポートの声明に記載されているように、Windows 10 Mobile のユーザーは、新しいセキュリティ更新プログラム、セキュリティ以外の修正プログラム、無償のサポート オプション、Microsoft からのオンライン技術コンテンツ更新プログラムを受け取ることができなくなります。 Microsoft Intune は、すべてのモバイル OS のサポートに基づいて、2020 年 8 月 10 日に Windows 10 Mobile アプリと Windows 10 Mobile オペレーティング システムの両方のポータル サイトのサポートを終了します。

8 月 10 日の時点で、Windows Phone 8.1 と Windows 10 Mobile デバイスの登録は失敗し、Windows Mobile のプロファイルの種類は Intune UI から削除されます。 登録済みのデバイスは Intune サービスにチェックインされなくなり、デバイスとポリシーのデータが削除されます。

### <a name="end-of-support-for-legacy-pc-management"></a>従来の PC 管理のサポート終了

従来の PC 管理は 2020 年 10 月 15 日にサポートが終了します。 デバイスを Windows 10 にアップグレードし、Intune による管理が継続されるようにモバイル デバイス管理 (MDM) デバイスとして再登録してください。

[詳細情報](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>Intune のすべての管理を Microsoft Endpoint Manager 管理センターに移行する
今年 3 月に掲載された MC208118 で、Microsoft Endpoint Manager での Intune 管理のための新しい簡単な URL ([https://endpoint.microsoft.com](https://endpoint.microsoft.com)) が発表されました。 Microsoft Endpoint Manager は、Microsoft Intune と Configuration Manager を含む統合プラットフォームです。 **2020 年 8 月 1 日以降**、[https://portal.azure.com](https://portal.azure.com) での Intune の管理を削除します。代わりに、すべてのエンドポイント管理に [https://endpoint.microsoft.com](https://endpoint.microsoft.com) をご使用になることをお勧めします。 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>Android デバイス管理者のサポートの縮小<!--7371518-->
Android デバイス管理者の管理は、Android デバイスを管理する方法の 1 つとして Android 2.2 でリリースされました。 その後、Android 5 で、より最新の管理フレームワークである [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (Google Mobile Services に確実に接続できるデバイス向け) がリリースされました。 Google は、新しい Android リリースでのデバイス管理者の管理サポートを縮小して、管理を移行することを奨励しています。

#### <a name="how-does-this-affect-me"></a>ユーザーへの影響
Google によるこれらの変更により、2020 年第 4 四半期には、影響を受ける、デバイス管理者によって管理されているデバイスに対して広範な管理機能がお使いいただけなくなります。 

> [!NOTE]
> 以前、この日付は 2020 年第 3 四半期と伝えられていましたが、[Google の最新情報](https://www.blog.google/products/android-enterprise/da-migration/)によると、第 4 四半期まで引き延ばされました。

##### <a name="device-types-that-will-be-impacted"></a>影響を受けるデバイスの種類
デバイス管理者のサポート縮小によって影響を受けるデバイスは、次の 3 つの条件すべてに該当するデバイスです。
- デバイス管理者の管理に登録されている。
- Android 10 以降が実行されている。
- Samsung デバイスではない。

次のいずれかに該当するデバイスは影響を受けません。
- デバイス管理者の管理に登録されていない。
- Android 10 より下のバージョンの Android が実行されている。
- Samsung デバイスである。 Samsung Knox デバイスは、この時間枠内に影響を受けることはありません。これは、Intune と Knox プラットフォームとの統合によって延長サポートが提供されるためです。 このため、Samsung デバイスについては、デバイス管理者の管理を移行するまで時間的な余裕があり、十分な計画を立てることができます。

##### <a name="settings-that-will-be-impacted"></a>影響を受ける設定
[Google がデバイス管理者のサポートを縮小](https://developers.google.com/android/work/device-admin-deprecation)することによって、次の設定の構成が、影響を受けるデバイスに適用されなくなります。

###### <a name="configuration-profile-device-restriction-settings"></a>構成プロファイルのデバイス制限の設定

- **カメラ**のブロック
- **[パスワードの最小文字数]** の設定
- **[デバイスがワイプされるまでのサインイン失敗回数]** の設定 (パスワードを設定していないデバイスは該当しませんが、パスワードを設定しているデバイスは該当します)
- **[パスワードの有効期限 (日数)]** の設定
- **[必要なパスワードの種類]** の設定
- **[以前のパスワードを再利用できないようにする]** の設定
- **Smart Lock などの信頼できるエージェント**のブロック

###### <a name="compliance-policy-settings"></a>コンプライアンス ポリシーの設定

- **[必要なパスワードの種類]** の設定
- **[パスワードの最小文字数]** の設定
- **[パスワードの有効期限が切れるまでの日数]** の設定
- **[再使用を禁止するパスワード世代数]** の設定


![[Android コンプライアンス ポリシー] ページのスクリーンショット](../fundamentals/media/notices/android-compliance-settings.png)

###### <a name="additional-impacts-based-on-android-os-version"></a>Android OS のバージョンに基づくその他の影響

**Android 10**: Google では、管理者によって管理され、Android 10 以降が実行されているすべてのデバイス (Samsung を含む) に対して、ポータル サイトなどのデバイス管理者の管理エージェントを使ってデバイス識別子の情報にアクセスする機能を制限しています。 この制限により、Android 10 以降にデバイスを更新すると、次の Intune 機能が影響を受けます。
- VPN のネットワーク アクセス制御が機能しなくなる
- IMEI またはシリアル番号を使用した企業所有のデバイスの識別で、デバイスが企業所有として自動的にマークされなくなる
- Intune で IT 管理者に IMEI とシリアル番号が表示されなくなる

**Android 11**: Microsoft では、現在、デバイス管理者によって管理されているデバイスに影響があるかどうかを評価するために、最新の開発者向けベータ リリースで Android 11 のサポートのテストを行っています。

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>影響を受けるデバイスの影響を受ける設定のユーザー エクスペリエンス

影響を受ける構成設定:
- 既に登録済みで、設定が既に適用されているデバイスについては、影響を受ける構成設定が引き続き適用されます。
- 新たに登録されるデバイス、新しく割り当てられる設定、更新された設定については、影響を受ける構成設定が適用されません (ただし、他のすべての構成設定は適用されます)。

影響を受けるコンプライアンス設定:
- 既に登録済みで、設定が既に適用されているデバイスについては、影響を受けるコンプライアンス設定が、コンプライアンス違反の理由として [デバイスの更新設定] ページに表示され、デバイスはコンプライアンスに準拠しなくなります。さらに、設定アプリでは、パスワード要件が引き続き適用されます。
- 新たに登録されるデバイス、新しく割り当てられる設定、更新された設定については、影響を受けるコンプライアンス設定が、コンプライアンス違反の理由として [デバイスの更新設定] ページに表示され、デバイスはコンプライアンスに対応していませんが、設定アプリでは、より厳格なパスワード要件が適用されることはありません。

#### <a name="cause-of-impact"></a>影響の原因 
デバイスへの影響が出始めるのは、2020 年第 4 四半期からです。 そのときに、([Google の要求に応じて](https://www.blog.google/products/android-enterprise/da-migration/)) ポータル サイト API のターゲットをレベル 28 からレベル 29 に上げるポータル サイト アプリの更新があります。 

その時点で、ユーザーが次の両方のアクションを完了すると、デバイス管理者によって管理されるデバイスで、Samsung 製以外のものは影響を受けることになります。
- Android 10 以降に更新する。
- ポータル サイト アプリを、API レベル 29 を対象とするバージョンに更新する。

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>この変更に対して必要な準備
2020 年第 4 四半期に始まる機能の縮小を回避するために、次のことをお勧めします。
- **新規登録**: 新しいデバイスを [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理 (利用可能な場合) および[アプリ保護ポリシー](../apps/app-protection-policies.md)にオンボードします。 新しいデバイスをデバイス管理者の管理にオンボードしないようにしてください。 
- **以前に登録されたデバイス**: デバイス管理者によって管理されているデバイスが Android 10 以降を実行している場合、または Android 10 以降に更新する可能性がある場合 (特に Samsung デバイスではない場合)、そのデバイスをデバイス管理者の管理から [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理または[アプリ保護ポリシー](../apps/app-protection-policies.md)に移行します。 [Android デバイスをデバイス管理者から仕事用プロファイル管理に移動する](../enrollment/android-move-device-admin-work-profile.md)には、合理化されたフローを利用できます。

#### <a name="additional-information"></a>追加情報
- [Android デバイスをデバイス管理者から仕事用プロファイル管理に移動する](../enrollment/android-move-device-admin-work-profile.md)
- [Android Enterprise 仕事用プロファイル デバイスの登録を設定する](../enrollment/android-work-profile-enroll.md)
- [Android Enterprise 専用デバイスの登録を設定する](../enrollment/android-kiosk-enroll.md)
- [Android Enterprise フル マネージド デバイスの Intune 登録を設定する](../enrollment/android-fully-managed-enroll.md)
- [アプリ保護ポリシーを作成して割り当てる方法](../apps/app-protection-policies.md)
- [Google Mobile Services のない環境で Intune を使用する方法](../apps/manage-without-gms.md)
- [Android エンタープライズ デバイス上のアプリケーション保護ポリシーと仕事用プロファイルの概要](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [デバイス管理者機能の廃止について知っておく必要があることに関する Google のブログ](https://www.blog.google/products/android-enterprise/da-migration/)
- [デバイス管理者から Android Enterprise への移行に関する Google のガイダンス](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [非推奨のデバイス管理者 API に関する Google のドキュメント](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>変更の計画: Apple の iOS/iPadOS 向け Automated Device Enrollment のための Intune 登録フローの更新
7 月のポータル サイト リリースでは、Apple の Automated Device Enrollment (旧称 DEP) の iOS/iPadOS 登録フローを変更する予定です。 登録フローの変更は、[ユーザー アフィニティに登録する] フローでのみ発生します。 以前は、構成の一部として [ポータル サイトのインストール] を [いいえ] に設定しても、ユーザーはストアからポータル サイト アプリをインストールでき、その後、登録がトリガーされ、ユーザーは適切なシリアル番号を追加することができました。 この次回のポータル サイト リリースでは、そのシリアル番号確認画面を削除する予定です。 代わりに、対応するアプリ構成ポリシーを作成し、ポータル サイトと一緒に送信して、ユーザーが無事に登録できるようにするか、または構成の一部として [ポータル サイトのインストール] を [はい] に設定することをお勧めします。 
 - 詳細については、[こちら](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629)の投稿記事を参照してください。
