---
title: Microsoft Intune でエンドポイント セキュリティ ポリシーを使用してファイアウォールを管理する | Microsoft Docs
description: Microsoft Endpoint Manager でエンドポイント セキュリティのファイアウォール ポリシーを使用して、管理するデバイスのポリシーを構成および展開します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 5b33be56975713c801d2ad3fdea17e6303687274
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946914"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのファイアウォール ポリシー

Intune のエンドポイント セキュリティのファイアウォール ポリシーは、macOS や Windows 10 が動作しているデバイスに組み込まれているファイアウォールを構成する場合に使用します。

デバイス構成の Endpoint Protection プロファイルを使用して同じファイアウォール設定を構成できますが、デバイス構成プロファイルには、追加の設定カテゴリがあります。 これらの追加の設定はファイアウォールとは関係がなく、環境に合わせてファイアウォール設定のみを構成するタスクが複雑になる可能性があります。

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) の **[エンドポイント セキュリティ]** ノードにある *[管理]* で、ファイアウォールのためのエンドポイント セキュリティ ポリシーを見つけます。

[ファイアウォール プロファイルの設定](../protect/endpoint-security-Firewall-profile-settings.md)を確認します。

## <a name="prerequisites-for-firewall-profiles"></a>ファイアウォール プロファイルの前提条件

- Windows 10 以降
- サポートされているバージョンの macOS

## <a name="firewall-profiles"></a>ファイアウォール プロファイル

**macOS プロファイル**:

- **macOS ファイアウォール** – macOS 上の組み込みファイアウォールの設定を有効にして構成します。

**Windows 10 プロファイル**:

- **Microsoft Defender ファイアウォール** – セキュリティが強化された Windows Defender ファイアウォールの設定を構成します。 Windows Defender ファイアウォールは、デバイスにホスト ベースの双方向ネットワーク トラフィックのフィルター処理を提供することによって、ローカル デバイスで送受信される承認されていないネットワーク トラフィックをブロックできます。

- **Microsoft Defender ファイアウォール規則** *(プレビュー)* - 特定のポート、プロトコル、アプリケーション、ネットワークを含むきめ細かいファイアウォール規則を定義し、ネットワーク トラフィックを許可またはブロックします。 このプロファイルの各インスタンスでは、最大 150 個のカスタム規則がサポートされています。

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>ファイアウォール規則の結合とポリシーの競合

ポリシーを 1 つだけ使用して複数のファイアウォール ポリシーをデバイスに適用する計画を立てます。 1 つのポリシー インスタンスとポリシーの種類を使用すると、2 つの別のポリシーによって異なる構成が同じ設定に適用されること (およびそれによる競合の発生) を防ぐことができます。 異なる値で同じ設定を管理する 2 つのポリシー インスタンスまたはポリシーの種類間で競合が発生した場合、その設定はデバイスに送信されません。

- このような形のポリシーの競合は **Microsoft Defender ファイアウォール** プロファイルに当てはまるため、このプロファイルは、他の Microsoft Defender ファイアウォール プロファイルと競合したり、デバイスの構成などの別の種類のポリシーによって提供されるファイアウォール構成と競合したりする可能性があります。

  "*Microsoft Defender ファイアウォール*" プロファイルは "*Microsoft Defender ファイアウォール規則*" プロファイルとは競合しません。

**Microsoft Defender ファイアウォール規則** プロファイルを使用すると、同じデバイスに複数の規則プロファイルを適用できます。 ただし、構成が異なっていても同じものに対して異なる規則が存在する場合、両方の規則がデバイスに送信されると、そのデバイスで競合が発生します。

- たとえば、1 つ目の規則がファイアウォール経由で *Teams.exe* をブロックし、2 つ目の規則が *Teams.exe* を許可する場合、両方の規則がクライアントに配信されます。 この結果は、ファイアウォール設定用の他のポリシーによって発生した競合とは異なります。

複数の規則プロファイルの規則が互いに競合していない場合、デバイスでは各プロファイルの規則を結合して、結合されたファイアウォール規則構成をデバイス上に作成します。 この動作により、個々のプロファイルでサポートされている 150 個以上の規則をデバイスに展開できます。

- たとえば、2 つの Microsoft Defender ファイアウォール規則プロファイルがあるとします。 最初のプロファイルは、ファイアウォール経由で *Teams.exe* を許可します。 2 つ目のプロファイルは、ファイアウォール経由で *Outlook.exe* を許可します。 デバイスが両方のプロファイルを受け取ると、ファイアウォール経由で両方のアプリを許可するようにデバイスが構成されます。

## <a name="next-steps"></a>次のステップ

[エンドポイント セキュリティ ポリシーを構成する](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
