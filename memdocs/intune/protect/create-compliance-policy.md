---
title: Microsoft Intune でデバイス コンプライアンス ポリシーを作成する - Azure | Microsoft Docs
description: デバイス コンプライアンス ポリシーの作成、状態と重大度レベルの概要、InGracePeriod 状態の使用、条件付きアクセスの使用、割り当てポリシーなしのデバイスの処理、Microsoft Intune の Azure portal とクラシック ポータルのコンプライアンスの違い
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: de23dc438ac176383cf5f5fbfac4da22f91bd4b2
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988814"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Microsoft Intune でコンプライアンス ポリシーを作成する

Intune を使用して組織のリソースを保護する場合、デバイスのコンプライアンス ポリシーは重要な機能です。 Intune では、最低限の OS バージョンなど、デバイスがコンプライアンス準拠と見なされるために満たす必要がある規則と設定を作成できます。 デバイスが準拠していない場合は、[条件付きアクセス](conditional-access.md)を使用してデータとリソースへのアクセスをブロックできます。

また、コンプライアンス非準拠の場合は、通知メールをユーザーに送信するなどの対応を実行できます。 コンプライアンス ポリシーの役割と使用方法の概要については、[デバイスのコンプライアンスの概要](device-compliance-get-started.md)に関するページを参照してください。

この記事の内容:

- コンプライアンス ポリシーを作成する前提条件と手順を示します。
- ユーザーおよびデバイス グループにポリシーを割り当てる方法を示します。
- ポリシーを "フィルター処理" するためのスコープのタグ、準拠していないデバイスに対して実行できる手順など、追加の機能について説明します。
- デバイスでポリシーの更新を受信した際のチェックインの更新サイクル時間を示します。

## <a name="before-you-begin"></a>始める前に

デバイス コンプライアンス ポリシーを使う場合、次のことを確認します。

- 以下のサブスクリプションを使用します。

  - Intune
  - 条件付きアクセスを使用する場合は、Azure Active Directory (AD) Premium Edition が必要です。 「[Azure Active Directory の価格](https://azure.microsoft.com/pricing/details/active-directory/)」には、さまざまなエディションで入手できる機能を一覧表示しています。 Intune のコンプライアンスには、Azure AD は必要ありません。

- サポートされているプラットフォームを使用します。

  - Android デバイス管理者
  - Android エンタープライズ
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Intune にデバイスを登録します (コンプライアンスの状態を確認するために必要です)。

- 1 人のユーザーにデバイスを登録するか、またはプライマリ ユーザーなしで登録します。 複数のユーザーに登録されたデバイスはサポートされていません。

## <a name="create-the-policy"></a>ポリシーを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシー]**  >  **[ポリシーの作成]** を選択します。

3. 次のオプションから、このポリシーの **[プラットフォーム]** を選択します。
   - *Android デバイス管理者*
   - *Android エンタープライズ*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows Phone 8.1*
   - *Windows 8.1 以降*
   - *Windows 10 以降*

    *Android Enterprise* の場合は、 **[ポリシーの種類]** も選択します。
     - *Android デバイス所有者のコンプライアンス ポリシー*
     - *Android 仕事用プロファイルのコンプライアンス ポリシー*

    次に、 **[作成]** を選択し、 **[ポリシーの作成]** 構成ウィンドウを開きます。

4. **[基本]** タブで、後で識別しやすいように **[名前]** を指定します。 たとえば、適切なポリシー名は、**iOS/iPadOS の脱獄されたデバイスを非準拠としてマークする**などです。

   **[説明]** を指定することもできます。
  
5. **[コンプライアンス設定]** タブで、使用できるカテゴリを展開し、ポリシーの設定を構成します。  次の記事では、各プラットフォームの設定について説明しています。
   - [Android デバイス管理者](compliance-policy-create-android.md)
   - [Android エンタープライズ](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows Phone 8.1、Windows 8.1 以降](compliance-policy-create-windows-8-1.md)
   - [Windows 10 以降](compliance-policy-create-windows.md)  

6. **[場所]** タブでは、デバイスの場所に基づいてコンプライアンスを強制できます。 既存の場所から選択します。 使用できる場所がまだない場合は、[場所 (ネットワーク フェンス) の使用](use-network-locations.md)に関するページを参照してください。
   > [!TIP]
   > **[場所]** は、*Android デバイス管理者*プラットフォームでのみ使用できます。

7. **[コンプライアンス非対応に対するアクション]** タブで、このコンプライアンス ポリシーを満たさないデバイスに自動的に適用する一連のアクションを指定します。

   複数のアクションを追加し、一部のアクションのスケジュールと追加の詳細を構成できます。 たとえば、既定のアクションである *[デバイスに非準拠のマークを付ける]* のスケジュールを 1 日後に発生するように変更できます。 次に、デバイスが準拠していない場合にユーザーにメールを送信して、その状態を警告するアクションを追加できます。 非準拠のままになっているデバイスをロックするかインベントリから削除するアクションを追加することもできます。

   構成できるアクションについては、ユーザーに送信する通知メールを作成する方法など、[非準拠デバイスに対してアクションを追加する](actions-for-noncompliance.md)方法に関するページを参照してください。

   [場所] を使用し、コンプライアンス ポリシーに少なくとも 1 つの場所を追加する例もあります。 このケースでは、少なくとも 1 つの場所を選択すると、コンプライアンス非対応に対する既定のアクションが適用されます。 選択した場所のいずれにもデバイスが接続されていない場合、デバイスは準拠していないと見なされます。 ユーザーに 1 日などの猶予期間を与えるようにスケジュールを構成できます。

8. **[スコープ タグ]** タブで、タグを選択して、ポリシーを `US-NC IT Team` や `JohnGlenn_ITDepartment` などの特定のグループにフィルター処理します。 設定を追加したら、コンプライアンス ポリシーにスコープのタグを追加することもできます。 

   スコープ タグの使用の詳細については、[スコープのタグを使用してポリシーをフィルター処理する](../fundamentals/scope-tags.md)方法に関するページを参照してください。

9. **[割り当て]** タブで、グループにポリシーを割り当てます。  

   **[+ 含めるグループを選択]** を選択し、ポリシーを 1 つ以上のグループに割り当てます。 次の手順の後でポリシーを保存すると、これらのグループにポリシーが適用されます。 

10. **[確認および作成]** タブで設定を確認し、コンプライアンス ポリシーを保存する準備ができたら **[作成]** を選択します。  

    ポリシーの対象となるユーザーまたはデバイスは、Intune にチェックインするときにコンプライアンスが評価されます。

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>サイクル時間の更新

Intune では、複数の更新サイクルを使用して、コンプライアンス ポリシーの更新が確認されます。 登録してすぐのデバイスでは、チェックインの実行頻度が高くなります。 「[ポリシーとプロファイルの更新サイクル](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)」に、おおよその更新間隔が一覧表示されています。

ユーザーはいつでもポータル サイト アプリを起動し、デバイスを同期して、ポリシーの更新をすぐに確認できます。

### <a name="assign-an-ingraceperiod-status"></a>InGracePeriod 状態を割り当てる

コンプライアンス ポリシーの InGracePeriod 状態は値の 1 つです。 この値は、デバイスの猶予期間、およびそのコンプライアンス ポリシーのデバイスの実際の状態の組み合わせによって決まります。

具体的には、デバイスに割り当てられているコンプライアンス ポリシーが NonCompliant 状態になっている場合、次のようになります。

- デバイスに猶予期間が割り当てられていない場合、コンプライアンス ポリシーに割り当てられる値は NonCompliant です。
- デバイスに割り当てられている猶予期間が期限切れになっている場合、コンプライアンス ポリシーに割り当てられる値は NonCompliant です。
- デバイスに将来の猶予期間が割り当てられている場合、コンプライアンス ポリシーに割り当てられる値は InGracePeriod です。

次の表はこれらの点をまとめたものです。

|実際のコンプライアンス状態|割り当てられた猶予期間の値|有効なコンプライアンス状態|
|---------|---------|---------|
|NonCompliant |猶予期間が割り当てられていない |NonCompliant |
|NonCompliant |昨日の日付|NonCompliant|
|NonCompliant |明日の日付|InGracePeriod|

デバイスのコンプライアンス ポリシーの監視の詳細については、「[Intune デバイス コンプライアンス対応ポリシーの監視](compliance-policy-monitor.md)」を参照してください。

### <a name="assign-a-resulting-compliance-policy-status"></a>コンプライアンス ポリシーの結果の状態を割り当てる

デバイスに複数のコンプライアンス ポリシーがあり、デバイスの 2 つ以上の割り当て済みコンプライアンス ポリシーが異なるコンプライアンス状態になっている場合、1 つの結果のコンプライアンス状態が割り当てられます。 この割り当ては、各コンプライアンス状態に割り当てられている概念的な重大度レベルを基にしています。 各コンプライアンス状態には、次の重大度レベルがあります。

|状態  |重大度  |
|---------|---------|
|Unknown     |1|
|NotApplicable     |2|
|[準拠]|3|
|InGracePeriod|4|
|NonCompliant|5|
|エラー|6|

デバイスに複数のコンプライアンス ポリシーがある場合、すべてのポリシーの最も高い重大度がそのデバイスに割り当てられます。

たとえば、デバイスに 3 つのコンプライアンス ポリシーが割り当てられていて、1 つが不明状態 (重大度 = 1)、1 つが準拠状態 (重大度 = 3)、1 つが InGracePeriod 状態 (重要度 = 4) であるとします。 この中で重大度レベルが最も高いのは、InGracePeriod 状態です。 したがって、3 つのポリシーすべてのコンプライアンス状態が InGracePeriod となります。

## <a name="next-steps"></a>次のステップ

[ポリシーを監視します](compliance-policy-monitor.md)。
