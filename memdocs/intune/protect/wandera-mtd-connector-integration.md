---
title: Wandera モバイル脅威保護と Intune との統合を設定する
titleSuffix: Intune on Azure
description: Microsoft Intune で Wandera モバイル脅威保護ソリューションを設定し、モバイル デバイスから会社のリソースへのアクセスを制御する方法。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: b227148a6e16f7c9f8d62cb58eeb628afbd84123
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86872020"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Wandera モバイル脅威保護を Intune と統合する  

Wandera Mobile Threat Defense ソリューションを Intune と統合するには、以下の手順を実行します。  

## <a name="before-you-begin"></a>始める前に  

Wandera を Intune と統合する手順を開始する前に、次の前提条件を満たしていることを確認してください。

- Intune のサブスクリプション
- Azure Active Directory 管理者の資格情報と、次のアクセス許可を付与できる割り当てられたロール:

    - サインインし、ユーザー プロファイルを読む
    - サインインしたユーザーとしてディレクトリにアクセスする
    - ディレクトリ データの読み込み
    - Intune にデバイスのリスク情報を送信する
 
- 有効な Wandera サブスクリプション
    - スーパー管理者特権を持つ管理者アカウント

## <a name="integration-overview"></a>統合の概要

Wandera と Intune 間の Mobile Threat Defense 統合を有効にするには、次の操作が必要です。

- Wandera の UEM Connect サービスを有効にして、Azure および Intune と情報を同期させます。 これには、Mobile Threat Defense (MTD) デバイス脅威レベルと共に、ユーザーとデバイスのライフ サイクル管理 (LCM) メタデータが含まれます。
- Wandera でアクティブ化プロファイルを作成して、デバイスの登録の動作を定義します。
- 管理対象の iOS および Android デバイスに Wandera を無線で展開します。
- iOS および Android のアンマネージド デバイスで MAM-WE を使用してエンド ユーザーのセルフサービス用に Wandera を構成します。

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Wandera Mobile Threat Defense の統合を設定する

Wandera と Intune 間の統合を設定するために、Wandera スタッフのサポートは必要ありません。数分で簡単に実現できます。

### <a name="enable-support-for-wandera-in-intune"></a>Intune での Wandera のサポートを有効にする

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[Mobile Threat Defense]**  >  **[追加]** を選択します。
3. **[コネクタの追加]** ページで、ドロップダウンを使用して **[Wandera]** を選択します。 次いで **[作成]** を選択します。  
4. [Mobile Threat Defense] ウィンドウで、コネクタの一覧から **[Wandera]** MTD コネクタを選択し、 **[コネクタの編集]** ウィンドウを開きます。 **[Open the Wandera admin console]\(Wandera 管理コンソールを開く\)** を選択して [RADAR](https://radar.wandera.com/login) (Wandera の管理コンソール) を開き、サインインします。 
5. Wandera RADAR コンソールで、 **[統合] > [UEM Integration]\(UEM 統合\)** の順に移動し、 **[UEM Connect]\(UEM Connect\)** タブを選択します。[EMM Vendor]\(EMM ベンダー\) ドロップダウンを使用して、 **[Microsoft Intune]** を選択します。
6. 次のような画面が表示され、統合を完了するために必要なアクセス許可の付与が示されます。

   ![統合とアクセス許可](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. [Intune User]\(Intune ユーザー\) と [Device Sync]\(デバイスの同期\) の横にある [Grant]\(許可\) をクリックして、Wandera が Azure と Intune のライフ サイクル管理 (LCM) を実行することに同意します。
8. プロンプトが表示されたら、Azure 管理者の資格情報を選択または入力します。 要求されたアクセス許可を確認して、[組織の代理として同意する] チェックボックスをオンにします。 最後に、[同意する] をクリックして、LCM 統合を承認します。

   ![アクセス許可に同意する](./media/wandera-mtd-connector-integration/permissions.png)

9. RADAR 管理コンソールに自動的に戻ります。  承認が成功した場合は、[Grant]\(許可\) ボタンの横に緑色のティックが表示されます。
10. 一覧表示された残りの統合について、[Grant]\(許可\) ボタンをクリックして、それぞれの横に緑色のティックが表示されるまで同意プロセスを繰り返します。

11. Intune コンソールに戻り、Wandera MTD コネクタの編集を再開します。 使用可能な切り替えを [オン] に設定して、構成を [保存] します。

    ![Wandera の有効化](./media/wandera-mtd-connector-integration/enable-wandera.png)

これで Intune と Wandera が接続されました。

## <a name="create-activation-profiles-in-wandera"></a>Wandera でアクティブ化プロファイルを作成する

Intune ベースの展開は、RADAR で定義される Wandera アクティブ化プロファイルを使用して容易に行うことができます。  各アクティブ化プロファイルでは、認証要件、サービス機能、初期のグループ メンバーシップなどの特定の構成オプションを定義します。

Wandera でアクティブ化プロファイルを作成した後、それを Intune のユーザーとデバイスに "割り当て" ます。  アクティブ化プロファイルは、デバイス プラットフォームおよび管理戦略間で共通ですが、次の手順では、これらの違いに基づいて Intune を構成する方法を明示します。

以下の手順では、Intune を介してターゲット デバイスに展開する Wandera でアクティブ化プロファイルが作成されていることを前提としています。 Wandera アクティブ化プロファイルの作成と使用の詳細については、[アクティブ化プロファイル ガイド](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links)を参照してください。

> [!NOTE]
> Intune または MAM-WE を介して展開するためのアクティブ化プロファイルを作成する場合、最大のセキュリティ、プラットフォーム間の互換性、合理化されたエンド ユーザー エクスペリエンスを確保するために、[関連付けられたユーザー] を必ず [Authenticated by Identity Provider]\(ID プロバイダーによる認証済み\) > [Azure Active Directory] オプションに設定してください。

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>無線による MDM マネージド デバイスへの Wandera の展開

Intune で管理されている iOS および Android デバイスの場合、Wandera を無線で展開して、迅速なプッシュベースのアクティブ化を実現することができます。 このセクションを読み進む前に、必要なアクティブ化プロファイルが既に作成されていることを確認してください。 マネージド デバイスに Wandera を展開するには、次の操作が必要です。
- Wandera 構成プロファイルを Intune に追加し、ターゲット デバイスに割り当てる。
- Wandera アプリとそれぞれのアプリ構成を Intune に追加し、ターゲット デバイスに割り当てる。

### <a name="configure-and-deploy-ios-configuration-profiles"></a>iOS 構成プロファイルを構成して展開する 

このセクションでは、**必須**の iOS デバイスの構成ファイルをダウンロードし、MDM を経由して無線で Intune マネージド デバイスに配信します。

1. **RADAR**で、展開するアクティブ化プロファイルに進み ([デバイス] > [アクティブ化])、 **[展開戦略] タブ、[マネージド デバイス]、[Microsoft エンドポイント マネージャー]** の順にクリックします。
2. ご使用のデバイス フリーと構成に基づいて、 **[Apple iOS Supervised]\(監視下の Apple iOS \)** セクションまたは **[Apple iOS Unsupervised]\(監視されていない Apple iOS\)** セクションを展開します。
3. 次の手順で、提供された構成プロファイルをダウンロードし、それらをアップロードする準備を行います。
4. **Microsoft Intune 管理コンソール**を開き、 **[デバイス] > [iOS/iPadOS] > [構成プロファイル]** の順に移動します。  **[プロファイルの作成]** をクリックします。
5. 表示されたパネルで、 **[プラットフォーム]** の下の **[iOS/iPadOS]** を選択し、[プロファイル] の下の **[カスタム]** を選択します。 **[作成]** をクリックします。
6. **[名前]** フィールドに、構成のわかりやすいタイトルを入力します。RADAR でアクティブ化プロファイルに付けた名前と同じ名前にするのが理想的です。 こうすることにより、将来簡単に相互参照できます。 または、必要に応じて、アクティブ化プロファイル コードを指定します。 名前にサフィックスを付けて、監視下のデバイスまたは監視されていないデバイスのどちらの構成であるかを示すことをお勧めします。
7. 必要に応じて、 **[説明]** を入力して、構成の目的または用途について他の管理者に詳細を提供します。 **[次へ]** をクリックします。
8. **[ファイルの選択]** をクリックし、手順 3 でダウンロードした適切なアクティブ化プロファイルに対応するダウンロード済みの構成ファイルを見つけます。 監視下のプロファイルと監視されていないプロファイルの両方をダウンロードした場合は、適切なプロファイルを選択するようにしてください。 **[次へ]** をクリックします。
   <!-- image placeholder - ending future availability -->
9.  Intune RBAC プラクティスで必要とされる **[スコープ タグ]** を定義します。  **[次へ]** をクリックします。
10. Wandera をインストールする必要があるユーザーまたはデバイスのグループに、構成ファイルを**割り当て**ます。  テスト グループから開始し、アクティブ化が正常に機能していることを検証した後に展開することをお勧めします。 **[次へ]** をクリックします。
11. 構成が正しいかどうかを確認し、必要に応じて編集した後、 **[作成]** をクリックして、構成ファイルを作成し、展開します。

> [!NOTE]
> 監視下の iOS デバイスについては、Wandera は拡張された展開プロファイルを提供します。 監視下のデバイスと監視されていないデバイスが混在するフリートを使用している場合は、必要に応じて、他方のプロファイルの種類に対して上記の手順を繰り返します。 Intune を介して展開される将来のすべてのアクティブ化プロファイルについても、これらの同じ手順に従う必要があります。 監視下および監視されていない iOS デバイスが混在するフリートを使用しており、監視下モードベースのポリシーの割り当てについて支援が必要な場合は、Wandera サポートにお問い合わせください。 

## <a name="deploying-wandera-to-mam-we-devices"></a>MAM-WE デバイスへの Wandera の展開
Intune で管理されていない MAM-WE デバイスの場合、Wandera は、統合された認証ベースのオンボード エクスペリエンスを利用して、MAM 対応アプリ内の会社のデータをアクティブ化し、保護します。 

以降のセクションでは、エンド ユーザーが会社のデータにアクセスする前に Wandera をシームレスにアクティブ化できるように Wandera と Intune を構成する方法について説明します。 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>Wandera アクティブ化プロファイルで Azure デバイス プロビジョニングを構成する
MAM-WE で使用されるアクティブ化プロファイルでは、[関連付けられたユーザー] を [Authenticated by Identity Provider]\(ID プロバイダーによる認証済み\) > [Azure Active Directory] オプションに設定する必要があります。
1. **Wandera RADAR** ポータルで、[デバイス] > [アクティブ化] の登録で MAM-WE デバイスによって使用されるアクティブ化プロファイルを、既存の中から選択するか、新規に作成します。 
2. **[展開戦略] タブ、[アンマネージド デバイス]** の順にクリックし、 **[Azure Device Provisioning]\(Azure デバイス プロビジョニング\)** セクションまでスクロールします。
3. ご使用の **Azure AD テナント ID** を適切なテキスト フィールドに入力します。 テナント ID を用意していない場合は、 **[Get my Tenant ID]\(テナント ID を取得する\)** リンクをクリックして、新しいタブで Azure AD を開きます。ここで、この値をクリップボードに簡単にコピーできます。
4. (省略可能) **[グループ ID]** を指定して、ユーザーのアクティブ化を特定のグループに制限します。
   - 1 つ以上の **[グループ ID]** を定義する場合、MAM-WE をアクティブ化するユーザーは、このアクティブ化プロファイルを使用してアクティブ化するように指定された 1 つ以上のグループのメンバーである必要があります。
   - Azure テナント ID が同じで、グループ ID が異なる構成の複数のアクティブ化プロファイルを設定できます。 これにより、Azure グループのメンバーシップに基づいてデバイスを Wandera に登録することができ、アクティブ化するときに機能をグループ別に区別することができます。
   - グループ ID が指定されていない "既定" のアクティブ化プロファイルを 1 つだけ構成することができます。  このグループは、別のアクティブ化プロファイルとの関連付けを使用して、認証済みのユーザーがグループのメンバーではない場合のすべてのアクティブ化に使用できる汎用グループとして機能します。
5. ページの右上隅にある **[保存]** をクリックします。

## <a name="next-steps"></a>次のステップ
- RADAR に読み込まれた Wandera アクティブ化プロファイルを使用して、Intune でクライアント アプリを作成し、Wandera アプリを Android および iOS/iPadOS デバイスに展開します。 Wandera アプリ構成では、プッシュされたデバイス構成ファイルを補完するために不可欠な機能が提供されるため、すべての展開で使用することをお勧めします。 Wandera アプリに固有の手順とカスタムの詳細については、[MTD アプリの追加](mtd-apps-ios-app-configuration-policy-add-assign.md)に関する記事をご覧ください。 
- Wandera をエンドポイント マネージャーに統合したので、構成の調整、レポートの表示、モバイル デバイス フリート全体でのより広範囲の展開を行うことができるようになりました。 詳細な構成ガイドについては、Wandera のドキュメントの「[Support Center Getting Started Guide](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started)」 (サポート センター入門ガイド) を参照してください。
