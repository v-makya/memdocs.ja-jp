---
title: Microsoft Intune 用のエンドポイント セキュリティのファイアウォール規則移行ツール - Azure | Microsoft Docs
description: Microsoft Intune 用エンドポイント セキュリティのファイアウォール規則移行ツールの使用方法について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465003"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>エンドポイント セキュリティのファイアウォール規則移行ツールの概要

多くの組織は、最新のクラウドベースの管理を利用するために、セキュリティ構成を Microsoft エンドポイント マネージャーに移行しようと考えています。

エンドポイント マネージャーのエンドポイント セキュリティでは、Windows ファイアウォールの構成とファイアウォール規則のきめ細かな管理のための充実した管理エクスペリエンスが提供されます。

多くの組織では、Windows ファイアウォール規則を管理するためのグループ ポリシーが既に策定されています。 何百ものファイアウォール規則を手動で作成するのは面倒であるため、最新の管理に移行するのは困難な場合があります。

お客様がファイアウォール規則の構成をエンドポイント マネージャーのエンドポイント セキュリティ ポリシーに移行するのを支援するために、**エンドポイント セキュリティのファイアウォール規則移行ツール**が開発されました。

お客様は、参照または構成済み Windows 10 クライアントで**エンドポイント セキュリティのファイアウォール規則移行ツール**を実行して、エンドポイント マネージャーでエンドポイント セキュリティのファイアウォール規則ポリシーを自動的に作成することができます。 これらの規則が作成されると、管理者は、それを Azure AD グループに割り当てて、MDM および共同管理のクライアントを構成することができます。

[エンドポイント セキュリティのファイアウォール規則移行ツール](https://aka.ms/EndpointSecurityFWRuleMigrationTool)をダウンロードしてください。<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>ツールの使用方法

このツールは、参照コンピューターで実行され、現在の Windows ファイアウォール規則の構成を移行します。 ツールを実行すると、デバイス上にあるすべての有効なファイアウォール規則がエクスポートされ、収集された規則を使用して新しい Intune ポリシーが自動的に作成されます。

1. ローカルの管理者特権を使用して、参照コンピューターにログオンします。
2. ファイル `Export-FirewallRules.zip` をダウンロードして解凍します。 <br>
   この zip ファイルには、スクリプト ファイル `Export-FirewallRules.ps1` が含まれています。 
3. コンピューター上で `Export-FirewallRules.ps1` スクリプトを実行します。 <br>
   このスクリプトでは、実行に必要なすべての前提条件がダウンロードされます。 プロンプトが表示されたら、適切な Intune サービス管理者の資格情報を入力します。 必要なアクセス許可の詳細については、「[必要なアクセス許可](#required-permissions)」を参照してください。
4. プロンプトが表示されたら、ポリシー名を指定します。 <br>
   このポリシーは、 **[エンドポイント セキュリティ]**  >  **[ファイアウォール]** ペインの[[Microsoft エンドポイント マネージャー]](https://go.microsoft.com/fwlink/?linkid=2109431) に表示されます。 

    > [!IMPORTANT]
    > ポリシー名は、テナントに対して一意である必要があります。

    150 を超えるファイアウォール規則が見つかった場合、複数のポリシーが作成されます。

    > [!NOTE]
    > 既定では、有効なファイアウォール規則のみが移行され、GPO によって作成されたファイアウォール規則のみが移行されます。 これらの既定値を変更するためのスイッチが用意されています。 詳細については、「[スイッチ](#switches)」を参照してください。
    >
    > 検出されたファイアウォール規則の個数によっては、ツールの実行に時間がかかることがあります。

5. 完了すると、ツールによって、自動的に移行できなかったファイアウォール規則のカウントが出力されます。 詳細については、「[サポートされていない構成](#unsupported-configuration)」を参照してください。

## <a name="switches"></a>スイッチ

次のスイッチ (パラメーター) を使用して、ツールの既定の機能を変更することができます。

- `IncludeLocalRules` - このスイッチを使用すると、エクスポートに、ローカルで作成された、および既定のすべての Windows ファイアウォール規則が含まれます。 このスイッチを有効にすると、多くの規則が含まれる可能性があることにご注意ください。 
- `IncludedDisabledRules` - このスイッチを使用すると、エクスポートに、有効および無効のすべての Windows ファイアウォール規則が含まれます。 このスイッチを有効にすると、多くの規則が含まれる可能性があることにご注意ください。

## <a name="unsupported-configuration"></a>サポートされていない構成

Windows では MDM がサポートされていないため、次のレジストリベースの設定はサポートされていません。 これらの設定は一般的ではありませんが、これらの設定を必要とする場合は、標準のサポート チャネルを通じて、そのニーズをログに記録してください。

|     GPO フィールド    |     理由    |
|-|-|
|      TYPE-VALUE =/ "Security=" IFSECURE-VAL    |     Windows MDM でサポートされていない IPSec 関連の設定    |
|      TYPE-VALUE =/ "Security2_9=" IFSECURE2-9-VAL    |     Windows MDM でサポートされていない IPSec 関連の設定    |
|      TYPE-VALUE =/ "Security2=" IFSECURE2-10-VAL     |     Windows MDM でサポートされていない IPSec 関連の設定    |
|      TYPE-VALUE =/ "IF=" IF-VAL    |     インターフェイス ID (LUID) は管理できません    |
|      TYPE-VALUE =/ "Defer=" DEFER-VAL    |     グループ ポリシーまたは Windows MDM を介して公開されないインバウンド NAT Traversal 関連    |
|      TYPE-VALUE =/ "LSM=" BOOL-VAL    |     グループ ポリシーまたは Windows MDM を介して公開されない Loose Source Mapped    |
|      TYPE-VALUE =/ "Platform=" PLATFORM-VAL    |     グループ ポリシーまたは Windows MDM を介して公開されない OS のバージョン管理    |
|      TYPE-VALUE =/ "RMauth=" STR-VAL    |     Windows MDM でサポートされていない IPSec 関連の設定    |
|      TYPE-VALUE =/ "RUAuth=" STR-VAL    |     Windows MDM でサポートされていない IPSec 関連の設定    |
|      TYPE-VALUE =/ "AuthByPassOut=" BOOL-VAL    |     Windows MDM でサポートされていない IPSec 関連の設定    |
|      TYPE-VALUE =/ "LOM=" BOOL-VAL    |     グループ ポリシーまたは Windows MDM を介して公開されない Local Only Mapped    |
|      TYPE-VALUE =/ "Platform2=" PLATFORM-OP-VAL    |     グループ ポリシーまたは Windows MDM を介して公開されない冗長設定    |
|      TYPE-VALUE =/ "PCross=" BOOL-VAL    |     グループ ポリシーまたは Windows MDM を介して公開されないプロファイル交差の許可    |
|      TYPE-VALUE =/ "LUOwn=" STR-VAL    |     MDM で適用できないローカル ユーザーの所有者 SID    |
|      TYPE-VALUE =/ "TTK=" TRUST-TUPLE-KEYWORD-VAL    |     グループ ポリシーまたは Windows MDM を介して公開されない、トラフィックと信頼タプル キーワードの一致    |
|      TYPE-VALUE =/ “TTK2_22=” TRUST-TUPLE-KEYWORD-VAL2-22    |     グループ ポリシーまたは Windows MDM を介して公開されない、トラフィックと信頼タプル キーワードの一致    |
|      TYPE-VALUE =/ “TTK2_27=” TRUST-TUPLE-KEYWORD-VAL2-27    |     グループ ポリシーまたは Windows MDM を介して公開されない、トラフィックと信頼タプル キーワードの一致    |
|      TYPE-VALUE =/ “TTK2_28=” TRUST-TUPLE-KEYWORD-VAL2-28    |     グループ ポリシーまたは Windows MDM を介して公開されない、トラフィックと信頼タプル キーワードの一致    |
|      TYPE-VALUE =/ "NNm=" STR-ENC-VAL    |     Windows MDM でサポートされていない IPSec 関連の設定    |
|      TYPE-VALUE =/ "SecurityRealmId=" STR-VAL    |     Windows MDM でサポートされていない IPSec 関連の設定    |

## <a name="unsupported-setting-values"></a>サポートされていない設定値
次の設定値は、移行ではサポートされていません。

**ポート**
- `PlayToDiscovery` は、ローカルまたはリモート ポート範囲としてサポートされていません。

**アドレス範囲**
- `LocalSubnet6` は、ローカルまたはリモート アドレス範囲としてサポートされていません。 
- `LocalSubnet4` は、ローカルまたはリモート アドレス範囲としてサポートされていません。
- `PlatToDevice` は、ローカルまたはリモート アドレス範囲としてサポートされていません。

ツールを実行すると、正常に移行されなかった規則を含むレポートが生成されます。 これらの規則は、`C:\<folder needed>` で検出された `RulesError.csv` を表示することによって確認できます。 

## <a name="required-permissions"></a>必要なアクセス許可
エンドポイント セキュリティ マネージャー、Intune サービス管理者、またはグローバル管理者のユーザーは、Windows ファイアウォール規則をエンドポイント セキュリティ ポリシーに移行できます。 または、セキュリティ ベースラインのアクセス許可が、 **[削除]** 、 **[読み取り]** 、 **[割り当て]** 、 **[作成]** 、 **[更新]** の付与が適用されるように設定されている場合、カスタム ロールを使用できます。 詳細については、[Intune に対する管理者アクセス許可の付与](../fundamentals/users-add.md#grant-admin-permissions)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

- ルールを Azure AD グループに割り当てて、MDM および共同管理のクライアントを構成します。 詳細については、「[ユーザーとデバイスを整理するためのグループを追加する](../fundamentals/groups-add.md)」を参照してください。
