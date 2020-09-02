---
title: Microsoft Intune で Microsoft Defender ATP を構成する - Azure | Microsoft Docs
description: Intune で Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を構成します。これには、ATP への接続、デバイスのオンボード、リスク レベルへのコンプライアンスの割り当て、条件付きアクセス ポリシーなどが含まれます。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9c3e456722d0b747a07c3f7040edc2cdf28f264
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909586"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>Intune で Microsoft Defender ATP を構成する

この記事に記載されている情報と手順は、Microsoft Defender ATP と Intune の統合を構成する場合に役立ちます。 構成には、次の一般的な手順が含まれます。

- テナントに対して Microsoft Defender ATP を有効にする
- Windows および Android を実行するデバイスをオンボードする
- コンプライアンス ポリシーを使用してデバイスのリスク レベルを設定する
- 条件付きアクセス ポリシーを使用して、想定したリスク レベルを超えるデバイスをブロックする

開始する前に、お使いの環境で、Intune と共に Microsoft Defender ATP を使用するための[前提条件](../protect/advanced-threat-protection.md#prerequisites)が満たされている必要があります。

## <a name="enable-microsoft-defender-atp-in-intune"></a>Intune で Microsoft Defender ATP を有効にする

実行する最初の手順は、Intune と Microsoft Defender ATP の間にサービス間接続を設定することです。 設定には、Microsoft Defender セキュリティ センターと Intune の両方に対する管理アクセス権が必要です。

Microsoft Defender ATP を有効にする必要があるのは、テナントごとに 1 回だけです。

### <a name="to-enable-microsoft-defender-atp"></a>Microsoft Defender ATP を有効にするには

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[Microsoft Defender ATP]** の順に選択し、 **[Microsoft Defender セキュリティ センターを開く]** を選択します。

   ![選択して Microsoft Defender セキュリティ センターを開く](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. **Microsoft Defender セキュリティ センター**で次の操作を行います。
   1. **[設定]**  >  **[高度な機能]** の順に選択します。
   2. **Microsoft Intune の接続**については、次のように **[オン]** を選択します。

      ![Intune への接続を有効にする](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

   3. **[環境設定の保存]** を選択します。

4. Microsoft Endpoint Manager admin center で **[Microsoft Defender ATP]** に戻ります。 組織のニーズに応じて、 **[MDM コンプライアンスポリシー設定]** で:
   - **[バージョン 10.0.15063 以上の Windows デバイスを Microsoft Defender ATP に接続します]** を **[オン]** に設定します
   - **[バージョン 6.0.0 以上の Android デバイスを Microsoft Defender ATP に接続します]** を **[オン]** に設定します

5. **[保存]** を選択します。

> [!TIP]
> 新しいアプリケーションを Intune Mobile Threat Defense に統合し、Intune への接続を有効にすると、Intune によって Azure Active Directory 内に従来の条件付きアクセス ポリシーが作成されます。 統合する各 MTD アプリ ([Microsoft Defender ATP](advanced-threat-protection.md) や追加の [MTD パートナー](mobile-threat-defense.md#mobile-threat-defense-partners)のいずれかなど) によって、新しい従来の条件付きアクセス ポリシーが作成されます。 これらのポリシーは無視してもかまいませんが、編集、削除、または無効にすることはできません。
>
> 従来のポリシーを削除した場合は、その作成に使用された Intune への接続を削除してから、それを再設定する必要があります。 これにより、従来のポリシーが再作成されます。 MTD アプリ用の従来のポリシーを、条件付きアクセス用の新しいポリシーの種類に移行することは、サポートされていません。
>
> MTD アプリ用の従来の条件付きアクセス ポリシーは:
>
> - デバイスが Azure AD に登録され、MTD パートナーと通信する前にデバイス ID を持っていることを要求するために、Intune MTD によって使用されます。 ID は、デバイスが Intune に正常に自身の状態を報告できるようにするために必要です。
> - 他のクラウド アプリやリソースには影響しません。
> - MTD の管理を支援するために作成する条件付きアクセス ポリシーとは異なります。
> - 既定では、評価に使用する他の条件付きアクセス ポリシーとは対話しません。
>
> 従来の条件付きアクセス ポリシーを表示するには、[Azure](https://portal.azure.com/#home) で **[Azure Active Directory]**  >  **[条件付きアクセス]**  >  **[クラシック ポリシー]** の順に移動します。

## <a name="onboard-devices"></a>デバイスのオンボード

Intune で Microsoft Defender ATP のサポートを有効にした場合、Intune と Microsoft Defender ATP の間にサービス間接続が確立されます。 次に、Intune で管理するデバイスを Microsoft Defender ATP にオンボードできます。これによって、デバイスのリスク レベルに関するデータを収集できます。

### <a name="onboard-windows-devices"></a>Windows デバイスのオンボード

Intune と Microsoft Defender ATP の間の接続を確立したときに、Microsoft Defender ATP から Intune に対して Microsoft Defender ATP のオンボード構成パッケージが渡されました。 Microsoft Defender ATP のデバイス構成プロファイルを使用して、この構成パッケージを Windows デバイスに展開します。

構成パッケージによってデバイスが構成され、[Microsoft Defender ATP サービス](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)と通信を行ってファイルのスキャンや脅威の検出が実行されます。 またデバイスは、作成するコンプライアンス ポリシーに基づいて、Microsoft Defender ATP にデバイスのリスク レベルを報告するように構成されます。

構成パッケージを使用してデバイスをオンボードした後は、再度これを行う必要はありません。 [グループ ポリシーまたは Microsoft Endpoint Configuration Manager](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints) を使用して、デバイスをオンボードすることもできます。

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>デバイス構成プロファイルを作成して Windows デバイスをオンボードする

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. **[プラットフォーム]** では、 **[Windows 10 以降]** を選択します。
4. **[プロファイルの種類]** では、 **[Microsoft Defender ATP (Windows 10 デスクトップ)]** を選択してから、 **[作成]** を選択します。
5. **[基本]** ページで、プロファイルの "*名前*" と "*説明*" (必要に応じて) を入力して、 **[次へ]** を選択します。
6. **[構成設定]** ページで、以下を構成します。

   - **[Microsoft Defender ATP クライアント構成パッケージの種類]** : **[Onboard]\(オンボード\)** を選択し、プロファイルに構成パッケージを追加します。 **[Offboard]** \(オフボード\) を選択し、プロファイルから構成パッケージを削除します。
  
     > [!NOTE]
     > Microsoft Defender ATP との接続を適切に確立している場合、Intune によって自動的に構成プロファイルが**オンボード**され、 **[Microsoft Defender ATP クライアント構成パッケージの種類]** 設定は使用できなくなります。
  
   - **[すべてのファイルのサンプル共有]** : **[有効にする]** では、サンプルを収集し、Microsoft Defender ATP と共有できるようになります。 たとえば、疑わしいファイルがある場合、それを Microsoft Defender ATP に送信して詳しく分析できます。 **[未構成]** では、いかなるサンプルも Microsoft Defender ATP と共有されません。
   - **[テレメトリの報告頻度を早める]** :高リスクのデバイスがある場合は、この設定を **[有効にする]** を選択し、Microsoft Defender ATP サービスに対してより頻繁にテレメトリを報告させることができます。

     これらの Microsoft Defender ATP の設定について詳しくは、[Microsoft Endpoint Configuration Manager を使用する Windows 10 コンピューターのオンボード](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm)に関する記事をご覧ください。

7. **[次へ]** を選択して、 **[スコープ タグ]** ページを開きます。 スコープ タグは省略可能です。 **[次へ]** を選択して続行します。

8. **[割り当て]** ページで、このプロファイルを受け取るグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

   **[次へ]** を選択します。

9. **[確認および作成]** ページで、完了したら、 **[作成]** を選択します。 作成したプロファイルのポリシーの種類を選択すると、新しいプロファイルが一覧に表示されます。
 **[OK]** 、 **[作成]** の順に選択して変更内容を保存します。これで、プロファイルが作成されます。

### <a name="onboard-android-devices"></a>Android デバイスをオンボードする

Intune と Microsoft Defender ATP の間にサービス間接続を確立した後は、Microsoft Defender ATP に Android デバイスをオンボードできます。 オンボードによって Defender ATP と通信するようにデバイスが構成され、その後、デバイスのリスク レベルに関するデータが収集されます。

Windows デバイスの場合とは異なり、Android を実行するデバイス用の構成パッケージはありません。 代わりに、Microsoft Defender ATP のドキュメントに含まれている [Android 用 Microsoft Defender ATP の概要](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android)に関する記事を参照して、Android 用の前提条件とオンボード手順を確認してください。

Android を実行するデバイスの場合、Intune ポリシーを使用して、Android に対する Microsoft Defender ATP を変更することもできます。 詳細については、[Microsoft Defender ATP の Web 保護](../protect/advanced-threat-protection-manage-android.md)に関する記事をご覧ください。

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>デバイスのリスク レベルを設定するコンプライアンス ポリシーを作成して割り当てる

Windows デバイスと Android デバイスのどちらでも、コンプライアンス ポリシーによって、デバイスに対して許容可能と見なすリスク レベルが決まります。

コンプライアンス ポリシーの作成に慣れていない場合は、「*Microsoft Intune でコンプライアンス ポリシーを作成する*」の記事の「[ポリシーを作成する](../protect/create-compliance-policy.md#create-the-policy)」の手順を参照してください。 次の情報は、コンプライアンス ポリシーの一部として Microsoft Defender ATP を構成する場合に固有のものです。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシー]**  >  **[ポリシーの作成]** を選択します。

3. **[プラットフォーム]** については、ドロップダウン ボックスを使用して、次のいずれかのオプションを選択します。
   - **Windows 10 以降**
   - **Android デバイス管理者**
   - **Android エンタープライズ**

   次に、 **[作成]** を選択し、 **[ポリシーの作成]** 構成ウィンドウを開きます。

4. 後でこのポリシーを識別するのに役立つ **[名前]** を指定します。 **[説明]** を指定することもできます。
  
5. **[コンプライアンス設定]** タブで、 **[Microsoft Defender ATP]** グループを展開し、オプションの **[デバイスは、次のマシン リスク スコア以下であることが必要]** を目的のレベルに設定します。

   脅威レベルの分類は、[Microsoft Defender ATP によって決定されます](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue)。

   - **[クリア]** :このレベルはセキュリティ上最も安全です。 デバイスには既存のいかなる脅威も存在できず、引き続き会社のリソースにアクセスできます。 いずれかの脅威が見つかった場合、デバイスは非準拠と評価されます。 (Microsoft Defender ATP ユーザーの値は *[セキュア]* です)。
   - **低**:低レベルの脅威が存在する場合にのみ、デバイスは準拠しています。 脅威レベルが中または高のデバイスは非準拠になります。
   - **中**: デバイスに存在する脅威が低または中の場合、デバイスは準拠しています。 高レベルの脅威が検出された場合は、デバイスは非準拠と判定されます。
   - **高**: 最も安全性の低いレベルであり、すべての脅威レベルが許容されます。 脅威レベルが高、中または低のデバイスは準拠していると見なされます。

6. 該当するグループへのポリシーの割り当てを含め、ポリシーの構成を完了します。


## <a name="create-a-conditional-access-policy"></a>条件付きアクセス ポリシーを作成する

条件付きアクセス ポリシーでは Microsoft Defender ATP からのデータを使用して、お客様が設定した脅威レベルを超えるデバイスによるリソースへのアクセスをブロックすることができます。 デバイスから企業リソース (SharePoint や Exchange Online など) へのアクセスをブロックできます。

> [!TIP]
> 条件付きアクセスは、Azure Active Directory (Azure AD) テクノロジです。 Microsoft Endpoint Manager admin center で検出される "*条件付きアクセス*" ノードは、*Azure AD* からのノードです。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[条件付きアクセス]**  >  **[新しいポリシー]** の順に選択します。

3. ポリシーの**名前**を入力して、 **[ユーザーとグループ]** を選択します。 含めるオプションまたは除外するオプションを使用して、ポリシーのグループを追加し、 **[完了]** を選択します。

4. **[クラウド アプリ]** を選択し、保護するアプリを選びます。 たとえば、 **[アプリを選択]** を選び、 **[Office 365 SharePoint Online]** と **[Office 365 Exchange Online]** を選択します。

   **[完了]** を選択して変更を保存します。

5. **[条件]**  >  **[クライアント アプリ]** の順に選択して、アプリとブラウザーにポリシーを適用します。 たとえば、 **[はい]** を選択し、 **[ブラウザー]** と **[モバイル アプリとデスクトップ クライアント]** を有効にします。

   **[完了]** を選択して変更を保存します。

6. **[許可]** を選択し、デバイスのコンプライアンスに基づいて条件付きアクセスを適用します。 たとえば、 **[アクセスの許可]**  >  **[デバイスは準拠しているとしてマーク済みである必要があります]** の順に選択します。

    **[選択]** を選んで変更を保存します。

7. **[ポリシーを有効にする]** 、 **[作成]** の順に選択して変更を保存します。

## <a name="next-steps"></a>次のステップ

- [Android に対する Microsoft Defender ATP 設定の構成](../protect/advanced-threat-protection-manage-android.md)
- [リスク レベルのコンプライアンスを監視する](../protect/advanced-threat-protection-monitor.md)

Intune のドキュメントで詳細を確認します。

- [ATP の脆弱性の管理を使用したセキュリティ タスクを使ってデバイスの問題を修復する](atp-manage-vulnerabilities.md)
- [デバイス コンプライアンス ポリシーの概要](device-compliance-get-started.md)

Microsoft Defender ATP のドキュメントで詳細を確認します。

- [Microsoft Defender ATP の条件付きアクセス](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP のリスク ダッシュボード](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)