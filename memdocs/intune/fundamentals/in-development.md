---
title: 開発中 - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune の開発中の機能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764205"
---
# <a name="in-development-for-microsoft-intune"></a>Microsoft Intune 用に開発中

お客様の準備と計画をサポートするため、このページでは、開発中でまだリリースされていない Intune UI の更新と機能が一覧表示されます。 このページの情報に加えて: 

- 変更前にお客様による対処が必要であると予測される場合は、Office メッセージ センターに補足の投稿が公開されます。
- 機能の運用が始まると、機能の説明はプレビュー版も一般公開版も、このページから[新機能](whats-new.md)に関するページに移行します。
- このページと[新機能](whats-new.md)に関するページは、定期的に更新されます。 適宜確認してください。
- 戦略的な成果物とタイムラインについては、「[Microsoft 365 のロードマップ](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS)」を参照してください。

> [!NOTE]
> このページには、今後のリリースでの Intune の機能に関する現在の予測が反映されています。 日付と個々の機能は変更される可能性があります。 このページは、開発中のすべての機能を説明しているわけではありません。

**RSS フィード**:ご自身のフィード リーダーに次の URL をコピーして貼り付けることで、このページが更新されたときにわかるようになります。`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**この記事は、上記のタイトルの下に示されている日付に最後に更新されました。**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>アプリ管理

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Android 用ポータル サイトで仕事用プロファイルの登録後にアプリを取得する方法がユーザーに示されるようになる <!-- 6103999  -->
ユーザーがアプリをより簡単に見つけてインストールできるように、ポータル サイトのアプリ内ガイダンスを改善しています。  仕事用プロファイルの管理に登録した後、バッジ付きバージョンの Google Play で推奨されるアプリを見つけられることを示すメッセージがユーザーに表示されます。 また、ユーザーには、左側のポータル サイト ドロアーで新しい **[アプリの取得]** リンクが表示されます。 これらの新規および改善されたエクスペリエンスの場所を空けるために、 **[アプリ]** タブが削除されます。 

<!-- ***********************************************-->
## <a name="device-configuration"></a>デバイスの構成

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Windows プラットフォーム用のデバイス構成プロファイルの設定と値が更新される<!-- 4091122 -->
Windows プラットフォーム用のデバイス構成プロファイルを作成する場合 ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** > プラットフォームの任意の **Windows** オプション)、一部の設定とその値は CSP とは異なるため、混乱を招く可能性があります。 設定の名前とその値はわかりやすくするために更新されます。

適用対象:

- Windows 10 以降のデバイス構成プロファイル
- Windows Holographic for Business のデバイス構成プロファイル
- Windows 8.1 のデバイス構成プロファイル
- Windows Phone 8.1 のデバイス構成プロファイル

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection デバイス構成ポリシーの新しい FileVault 設定<!-- 5459801   -->
[macOS Endpoint Protection](../protect/endpoint-protection-macos.md) テンプレート内の FileVault カテゴリに、次の新しい設定を追加しています: 回復キーを非表示にする ( **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動し、"*プラットフォーム*" として **[macOS]** を選択してから、"*プロファイルの種類*" として **[Endpoint Protection]** を選ぶ)。 この設定により、FileVault 2 の暗号化中は、エンド ユーザーに対して個人用キーが非表示になります。 デバイス ユーザーは、iOS ポータル サイト アプリから、または暗号化された macOS デバイス用のポータル Web サイトから、いつでも自分の個人用回復キーを表示することができます。 個人用回復キーを表示するには、[デバイスの詳細] に移動し、 *[回復キーの取得]* をクリックします。

この設定は、以前に作成されたポリシーでは使用できません。 この設定を利用するように構成するには、FileVault ポリシーを再作成する必要があります。 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>デバイスの登録

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>個人所有デバイスでは、VPN を使用して展開できる<!--5015344 -->
この機能は延期される可能性があります。

### <a name="shared-ipads-for-business--6367326---"></a>法人向け共有 iPad<!--6367326 -->
Intune と Apple Business Manager を使用して、複数の従業員がデバイスを共有できるように共有 iPad を簡単かつ安全に設定できるようになります。 Apple の [共有 iPad](https://developer.apple.com/education/shared-ipad/) では、ユーザー データを保持しながら、複数のユーザーに対してパーソナライズされたエクスペリエンスが提供されます。 ユーザーは、管理対象 Apple ID を使用して、組織内の共有 iPad にサインインした後、アプリ、データ、設定にアクセスできます。 共有 iPad はフェデレーション ID と連動します。

この機能を表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >  **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** の順に移動し、トークンを選択して**、 **[プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS]** の順に移動します。 **[管理の設定]** ページで、 **[ユーザー アフィニティを使用しないで登録する]** を選択すると、 **[共有 iPad]** オプションが表示されます。

**適用対象:** iPadOS 13.4 以降。 このリリースでは、ユーザーが管理対象 Apple ID を使用せずにデバイスにアクセスできるように、共有 iPad での一時的なセッションのサポートが追加されました。 ログアウト時に、デバイスではすべてのユーザー データが消去されるため、デバイスをすぐに使用できる状態になり、デバイスのワイプは不要になります。 

<!-- ***********************************************-->
## <a name="device-management"></a>デバイス管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>PowerShell スクリプトによる BYOD デバイスのサポート<!-- 1862833  -->
PowerShell スクリプトでは、Intune で Azure AD に登録されたデバイスがサポートされるようになります。 PowerShell の詳細については、「[Intune で Windows 10 デバイスに対して PowerShell スクリプトを使用する](../apps/intune-management-extension.md)」を参照してください。 この機能では、Windows 10 Home Edition を実行するデバイスはサポートされません。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics には、デバイスの詳細ログが含まれる<!--6014987  -->
Intune デバイスの詳細ログは、 **[レポート]**  >  **[ログ分析]** で入手できます。 デバイスの詳細を相互に関連付けて、カスタム クエリと Azure ブックを作成することができます。


<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>監視とトラブルシューティング

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI コンプライアンス レポート テンプレート V2.0<!-- 636958  -->
管理者は、Power BI コンプライアンス レポート テンプレートのバージョンを V1.0 から V2.0 に更新できるようになります。 V2.0 では、設計が改善され、テンプレートの一部として表示される計算とデータが変更されます。 関連情報については、「[Power BI でデータ ウェアハウスに接続する](../developer/reports-proc-get-a-link-powerbi.md)」を参照してください。

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>セキュリティ


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>エンドポイント セキュリティでポリシーを複製する<!-- 5892558   -->
Microsoft Endpoint Manager admin center のエンドポイント セキュリティ ノードで作成したポリシーを選択し、複製してコピーを作成できるようになります。  複製できるようになるポリシーには、以下について作成するものが含まれます。 

- ウイルス対策
- ディスクの暗号化
- ファイアウォール
- エンドポイントの検出と応答
- 攻撃の回避
- アカウント保護

複製によって元のポリシーのコピーが作成されます。その後、名前を変更して編集することができます。 コピーには元の割り当ては含まれません。

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>エンドポイント セキュリティ ファイアウォール ポリシーの新しいプロファイル<!-- 5653324   -->
プレビューとして、Intune のエンドポイント セキュリティのファイアウォール ポリシーに、Windows 10 以降用のプロファイルをさらに追加しています ( **[エンドポイント セキュリティ]**  >  **[ファイアウォール]**  >  **[ポリシーの作成]** > **[Windows 10 以降]** を選択)。 

この新しいプロファイルの各インスタンスでは、最大 150 のカスタム "*Microsoft Defender ファイアウォール規則*" がサポートされます。 Microsoft Defender ファイアウォール規則プロファイルを使用すると、Windows 10 のポートとアプリケーションを許可またはブロックするための詳細な Windows ファイアウォール規則を定義できます。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>関連項目

最近の開発状況について詳しくは、「[Microsoft Intune の新機能](whats-new.md)」をご覧ください。



