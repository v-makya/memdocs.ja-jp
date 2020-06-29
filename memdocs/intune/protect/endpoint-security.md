---
title: Microsoft Intune でエンドポイント セキュリティを管理する | Microsoft Docs
description: セキュリティ管理者がエンドポイント セキュリティ ノードを使用して、Microsoft Endpoint Manager でデバイスのセキュリティを管理し、デバイスの問題を修復する方法について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: e3ab2e31aa8a35ef04c150972cd7bb7650e46040
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879705"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Microsoft Intune でエンドポイント セキュリティを管理する

セキュリティ管理者として、Intune の*エンドポイント セキュリティ* ノードを 使用して、デバイスのセキュリティを構成し、デバイスが危険にさらされている場合にデバイスのセキュリティ タスクを管理します。 エンドポイント セキュリティ ポリシーは、デバイスのセキュリティに集中し、リスクを軽減できるように設計されています。 利用可能なタスクを使用して、危険にさらされているデバイスを特定し、それらのデバイスを修復し、準拠した状態、またはさらに安全な状態に復元することができます。

エンドポイント セキュリティ ノードは、デバイスのセキュリティを維持するために Intune で使用できるツールをグループ化します。

- **すべてのマネージド デバイスの状態を確認します**。 デバイス コンプライアンスを高レベルで確認できる [[すべてのデバイス]](#manage-devices) ビューを使用して、特定のデバイスを詳しく調べ、準拠されていないコンプライアンス ポリシーを把握できるので、これらを解決することができます。

- **デバイスのベスト プラクティス セキュリティ構成を確立するセキュリティ ベースラインを展開します**。 Intune には、Windows デバイス用の[セキュリティ ベースライン](#manage-security-baselines)と、Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) や Microsoft Edge などのアプリケーションの増え続ける一覧が含まれています。 セキュリティ ベースラインは Windows 設定の事前構成されたグループであり、これを使うと、関連するセキュリティ チームが推奨する設定と既定値を含んだ既知のグループを適用することができます。

- **焦点を絞ったポリシーを使用して、デバイスのセキュリティ構成を管理します**。  各[エンドポイント セキュリティ ポリシー](#use-policies-to-manage-device-security)は、ウイルス対策、ディスク暗号化、ファイアウォール、Microsoft Defender ATP との統合によって利用できる複数の領域などのデバイス セキュリティの側面に焦点を当てています。

- **コンプライアンス ポリシーを通じてデバイスとユーザーの要件を確立します**。 [コンプライアンス ポリシー](../protect/device-compliance-get-started.md)では、準拠していると見なされるためにデバイスとユーザーが従う必要のあるルールを設定します。 ルールには、OS のバージョン、パスワードの要件、デバイスの脅威レベルなどを含めることができます。

  Azure Active Directory (Azure AD) [条件付きアクセス ポリシー](#configure-conditional-access) を統合してコンプライアンス ポリシーを適用した場合、マネージド デバイスとまだ管理されていないデバイスの両方に対し、企業リソースへのアクセスを制限できます。

- **Intune を Microsoft Defender ATP チームと統合します**。 [Microsoft Defender ATP と統合する](#set-up-integration-with-microsoft-defender-atp)ことにより、[セキュリティ タスク](#review-security-tasks-from-microsoft-defender-atp)にアクセスできます。 セキュリティ タスクは、Microsoft Defender ATP および Intune と密接に結びついているので、セキュリティ チームが危険にさらされているデバイスを特定してから、対処できる Intune 管理者に詳細な修復手順を渡す場合に役立ちます。

この記事の次のセクションでは、管理センターのエンドポイント セキュリティ ノードから行えるさまざまなタスクと、それらを使用するために必要なロールベースのアクセス制御 (RBAC) のアクセス許可について説明します。

## <a name="manage-devices"></a>デバイスの管理

エンドポイント セキュリティ ノードには、 *[すべてのデバイス]* ビューが含まれており、ここでは、Microsoft Endpoint Manager で利用できる、Azure AD からのすべてのデバイスの一覧を確認できます。

このビューから、デバイスが準拠していないポリシーなどの詳細情報を詳しく調べるデバイスを選択できます。 このビューからのアクセスを使用して、デバイスの再起動、マルウェアのスキャンの開始、Windows 10 デバイスでの BitLocker キーのローテーションなど、デバイスの問題を修復することもできます。

詳細については、「[Microsoft Intune でエンドポイント セキュリティを使用してデバイスを管理する](../protect/endpoint-security-manage-devices.md)」をご覧ください。

## <a name="manage-security-baselines"></a>セキュリティ ベースラインを管理する

Intune でのセキュリティ ベースラインは、適切な Microsoft セキュリティ チームによりベスト プラクティスとして推奨される設定の事前に構成されたグループです。 Intune では、Windows 10 デバイス設定、Microsoft Edge、Microsoft Defender Advanced Threat Protection などのセキュリティ ベースラインをサポートしています。

セキュリティ ベースラインを使用して、ユーザーとデバイスを保護するデバイスおよびアプリケーションの設定の*ベスト プラクティス*である構成を即座に展開できます。 セキュリティ ベースラインは、Windows 10 バージョン 1809 以降を実行しているデバイスでサポートされています。

詳細については、「[Intune でのセキュリティ ベースラインを使用した Windows 10 デバイスの構成](../protect/security-baselines.md)」をご覧ください。

セキュリティ ベースラインは、Intune における、デバイスの設定を構成する複数の方法の 1 つです。 設定を管理するときには、デバイスを構成するために環境内で使用されている他の方法を把握して、競合を回避できるようにすることが重要です。 この記事で後述する「[ポリシーの競合を回避する](#avoid-policy-conflicts)」をご覧ください。

## <a name="review-security-tasks-from-microsoft-defender-atp"></a>Microsoft Defender ATP からのセキュリティ タスクを確認する

Intune を Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) と統合する場合、危険にさらされているデバイスを特定し、そのリスクを軽減する手順を提供する Intune での "*セキュリティ タスク*" を確認できます。 その後、これらのリスクが正常に軽減されたときに、これらのタスクを使用して、Microsoft Defender ATP にレポートを返すことができます。

- Microsoft Defender ATP チームは、危険にさらされているデバイスを特定し、その情報をセキュリティ タスクとして Intune チームに渡します。 数回クリックするだけで、リスクにさらされているデバイスと脆弱性を識別し、そのリスクを軽減する方法に関するガイダンスをもたらす Intune のセキュリティ タスクが作成されます。

- Intune 管理者は、セキュリティ タスクを確認してから、Intune 内でこれらのタスクを修復します。 軽減されたら、タスクを完了に設定し、そのステータスを Microsoft Defender ATP チームに返します。

セキュリティ タスクを通じて、両方のチームは、どのデバイスが危険にさらされ、それらのリスクがどのようにいつ修復されるかについて同期が保たれます。

セキュリティ タスクの使用方法の詳細については、「[Intune を使用して Microsoft Defender ATP によって検出された脆弱性を修復する](../protect/atp-manage-vulnerabilities.md)」をご覧ください。

## <a name="use-policies-to-manage-device-security"></a>ポリシーを使用してデバイス セキュリティを管理する

セキュリティ管理者として、エンドポイント セキュリティ ノードの *[管理]* の下にあるセキュリティ ポリシーを使用します。 これらのポリシーを使用すると、デバイスの構成プロファイルやセキュリティ ベースラインから大規模な本文やさまざまな設定を参照するオーバーヘッドなしで、デバイスのセキュリティを構成できます。

![ポリシーの管理](./media/endpoint-security/endpoint-security-policies.png)

これらのセキュリティ ポリシーの使用の詳細については、「[Microsoft Intune でエンドポイント セキュリティ ポリシーを使用してデバイスのセキュリティを管理する](../protect/endpoint-security-policy.md)」をご覧ください。

エンドポイント セキュリティ ポリシーは、デバイスの設定を構成する Intune での複数の方法の 1 つです。 設定を管理するときには、デバイスを構成するために環境内で使用されている他の方法を把握して、競合を回避することが重要です。 この記事で後述する「[ポリシーの競合を回避する](#avoid-policy-conflicts)」をご覧ください。

*デバイス コンプライアンス* ポリシーと*条件付きアクセス* ポリシーは、 *[管理]* の下にもあります。 これらのポリシーの種類は、エンドポイントを構成することに特化したセキュリティ ポリシーではありませんが、デバイスの管理と企業リソースへのアクセスに重要なツールです。

## <a name="use-device-compliance-policy"></a>デバイス コンプライアンス ポリシーを使用する

デバイス コンプライアンス ポリシーを使用して、ネットワークおよび企業リソースへのアクセスを、デバイスとユーザーに許可する条件を作成します。

[使用可能なコンプライアンス設定](../protect/device-compliance-get-started.md#next-steps)はお使いのプラットフォームによって異なりますが、一般的なポリシー ルールには次のものがあります。

- 最低限または特定の OS バージョンがデバイスで実行されていることが必要
- パスワード要件の設定
- Microsoft Defender ATP または他の Mobile Threat Defense パートナーによって決定される、許可される最大のデバイス脅威レベルの指定

ポリシー ルール以外にも、コンプライアンス ポリシーでは次の内容がサポートされています。

- Intune で定義する[場所](../protect/use-network-locations.md)。 コンプライアンス ポリシーで場所を使用すると、ポリシーは、デバイスが職場のネットワークに接続して準拠するように確保できます。
- [コンプライアンス非対応に対するアクション](../protect/actions-for-noncompliance.md)。 これらのアクションは、準拠していないデバイスに適用される時間順のアクションです。 アクションには、コンプライアンス非対応についてデバイス ユーザーに警告する電子メールや通知を送信したり、デバイスをリモートでロックしたり、さらには準拠していないデバイスを廃棄して残っている可能性のある会社データを削除したりするなどがあります。

Intune を Azure AD [条件付きアクセス ポリシー](#configure-conditional-access)と統合してコンプライアンス ポリシーを適用した場合、条件付きアクセスは、コンプライアンス データを使用して、マネージド デバイスと管理されていないデバイスの両方に対し、企業リソースへのアクセスを制限できます。

詳細については、「[Intune を使用して組織内のリソースへのアクセスを許可するように、デバイス上でルールを設定する](../protect/device-compliance-get-started.md)」をご覧ください。

デバイス コンプライアンス ポリシーは、デバイスの設定を構成する Intune での複数の方法の 1 つです。 設定を管理するときには、デバイスを構成するために環境内で使用されている他の方法を把握し、競合を回避することが重要です。 この記事で後述する「[ポリシーの競合を回避する](#avoid-policy-conflicts)」をご覧ください。

## <a name="configure-conditional-access"></a>条件付きアクセスの構成

デバイスと企業リソースを保護するために、Intune で Azure Active Directory (Azure AD) の条件付きアクセス ポリシーを使用できます。

Intune は、デバイス コンプライアンス ポリシーの結果を Azure AD に渡し、Azure AD は続いて条件付きアクセス ポリシーを使用して、企業リソースにアクセスできるデバイスとアプリを制限します。 条件付きアクセス ポリシーは、Intune で管理されていないデバイスのアクセスを制限する場合に役立ちます。 Intune と統合する [Mobile Threat Defense パートナー](../protect/mobile-threat-defense.md)からのコンプライアンスの詳細を使用することもできます。

次に、Intune で条件付きアクセスを使用する一般的な 2 つの方法を示します。

- **デバイスベースの条件付きアクセス**。管理対象の準拠デバイスのみがネットワーク リソースにアクセスできるようにします。
- **アプリベースの条件付きアクセス**。アプリ保護ポリシーを使用して、Intune で管理していないデバイス上のユーザーによるネットワーク リソースへのアクセスを管理します。

Intune での条件付きアクセスの使用の詳細については、[条件付きアクセスと Intune の概要](../protect/conditional-access.md)に関するページをご覧ください。

## <a name="set-up-integration-with-microsoft-defender-atp"></a>Microsoft Defender ATP との統合を設定する

Microsoft Defender ATP と Intune を統合すると、リスクを特定して対応する能力が向上します。

Intune は複数の [Mobile Threat Defense パートナー](../protect/mobile-threat-defense.md)と統合できますが、Microsoft Defender ATP を使用すると、Microsoft Defender ATP と Intune を緊密に統合でき、次のような詳細なデバイス保護オプションにアクセスできます。

- セキュリティ タスク - 危険にさらされているデバイス、それらを修復する方法、およびリスクが軽減されたときの確認に関する、ATP 管理者と Intune 管理者の間でのシームレスな通信。
- クライアントでの Microsoft Defender ATP の合理化されたオンボード。
- Intune コンプライアンス ポリシーで ATP デバイスのリスク信号の使用。
- *改ざん保護*機能へのアクセス。

 Microsoft Defender ATP と Intune の使用の詳細については、「[Intune で条件付きアクセスによる Microsoft Defender ATP のコンプライアンスを強制する](../protect/advanced-threat-protection.md)」をご覧ください。

## <a name="role-based-access-control-requirements"></a>ロールベースのアクセス制御要件

Microsoft Endpoint Manager admin center のエンドポイント セキュリティ ノードでタスクを管理するには、アカウントは次の点を満たす必要があります。

- Intune のライセンスが割り当てられていること。
- **エンドポイント セキュリティ マネージャー**の組み込み Intune ロールで与えられるアクセス許可と同等のロールベースのアクセス制御 (RBAC) のアクセス許可が付与されていること。 Microsoft Endpoint Manager admin center へのアクセス権は、*エンドポイント セキュリティ マネージャー* ロールが付与します。 このロールは、セキュリティ ベースライン、デバイス コンプライアンス、条件付きアクセス、Microsoft Defender ATP などのセキュリティとコンプライアンスの機能を管理する個人が使用できます。

詳細については、「[Microsoft Intune でのロールベースのアクセス制御 (RBAC)](../fundamentals/role-based-access-control.md)」をご覧ください

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>*エンドポイント セキュリティ マネージャー* ロールによって付与されたアクセス許可

Microsoft Endpoint Manager admin center で次のアクセス許可の一覧を表示するには、 **[テナント管理]**  >  **[ロール]**  >  **[すべてのロール]** に移動して、 **[Endpoint Security Manager]\(エンドポイントセキュリティ マネージャー\)**  >  **[プロパティ]** の順に選択します。

**アクセス許可:**

- **Android for Work**
  - 読み取り
- **監査データ**
  - 読み取り
- **業務用デバイスの ID**
  - 読み取り
- **デバイス コンプライアンス ポリシー**
  - 割り当て
  - 作成
  - 削除
  - 読み取り
  - 更新
  - レポートの表示
- **デバイスの構成**
  - 読み取り
- **デバイス登録マネージャー**
  - 読み取り
- **Endpoint Protection レポート**
  - 読み取り
- **登録プログラム**
  - デバイスの読み取り
  - プロファイルの読み取り
  - トークンの読み取り
- **Intune データ ウェアハウス**
  - 読み取り
- **管理対象アプリ**
  - 読み取り
- **マネージド デバイス**
  - 削除
  - 読み取り
  - プライマリ ユーザーの設定
  - 更新
- **モバイル アプリ**
  - 読み取り
- **組織**
  - 読み取り
- **PolicySets**
  - 読み取り
- **リモート アシスタンス**
  - 読み取り
- **リモート タスク**
  - FileVault キーの取得。
- **ロール**
  - 読み取り
- **セキュリティ ベースライン**
  - 割り当て
  - 作成
  - 削除
  - 読み取り
  - 更新
- **セキュリティ タスク**
  - 読み取り
  - 更新
- **通信費**
  - 読み取り
- **使用条件**
  - 読み取り

## <a name="avoid-policy-conflicts"></a>ポリシーの競合を回避する

デバイス用に構成できる設定の多くは、Intune のさまざまな機能で管理できます。 これらの機能には以下が含まれますが、これらに限定されません。

- エンドポイント セキュリティ ポリシー
- セキュリティ ベースライン
- デバイス構成ポリシー
- Windows 10 の登録ポリシー

たとえば、エンドポイント セキュリティ ポリシーにある設定は、デバイス構成ポリシーの*エンドポイント保護*プロファイルと*デバイスの制限*プロファイルにあり、さまざまなセキュリティ ベースラインでも管理される設定のサブセットです。

競合を回避する 1 つの方法は、異なるベースライン、同じベースラインのインスタンス、または異なるポリシーの種類とインスタンスを使用して、1 つのデバイスで同じ設定を管理しないことです。 これには、さまざまなデバイスに構成を展開するために使用する方法を計画する必要があります。 複数のメソッドまたは同じメソッドのインスタンスを使用して同じ設定を構成する場合は、異なる方法が一致しているか、同じデバイスに対して展開されていないかを確認してください。

競合が発生した場合は、Intune の組み込みツールを使用して、競合の原因を特定し、解決することができます。 詳細については、次をご覧ください。

- [Intune でのポリシーとプロファイルのトラブルシューティング](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [セキュリティ ベースラインの監視](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>次のステップ

以下を構成します。

- [セキュリティ ベースライン](../protect/security-baselines.md)
- [コンプライアンス ポリシー](../protect/device-compliance-get-started.md)
- [条件付きアクセス ポリシー](#configure-conditional-access)
- [Microsoft Defender ATP との統合](../protect/advanced-threat-protection.md)
