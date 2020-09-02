---
title: Microsoft Intune で Microsoft Defender ATP を使用する - Azure | Microsoft Docs
description: Intune で Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を使用して (設定と構成も含みます)、Intune デバイスを ATP にオンボードしてから、Intune デバイス コンプライアンスを使用したデバイスの ATP リスク評価と、条件付きアクセス ポリシーを使用して、ネットワーク リソースを保護します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1420bf03fe236decba0345e299eb5d5893f96c93
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915111"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Intune で条件付きアクセスによる Microsoft Defender ATP のコンプライアンスを強制する

Mobile Threat Defense ソリューションとして Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を Microsoft Intune と統合できます。 統合することで、セキュリティ侵害を防止し、組織内での侵害の影響を抑えることができます。

Microsoft Defender ATP は、Windows 10 以降を実行しているデバイスと Android デバイスで動作します。

正しく設定するには、以下の構成を同時に使用します。

- **Intune と Microsoft Defender ATP の間にサービス間接続を確立する**。 この接続により、Microsoft Defender ATP では、Intune で管理するサポート対象デバイスからコンピューターのリスクに関するデータを収集できるようになります。
- **デバイス構成プロファイルを使用して、デバイスを Microsoft Defender ATP にオンボードする**。 デバイスをオンボードして、Microsoft Defender ATP と通信を行い、そのリスク レベルを評価するのに役立つデータを提供するようにそれらを構成します。
- **デバイス コンプライアンス ポリシーを使用して、許可するリスクのレベルを設定する**。 リスク レベルは Microsoft Defender ATP によって報告されます。 許可されたリスク レベルを超えるデバイスは、非準拠として識別されます。
- **条件付きアクセス ポリシーを使用**して、ユーザーが非準拠のデバイスから企業リソースにアクセスできないようにする。

Intune を Microsoft Defender ATP と統合する場合、Microsoft Defender ATP の脅威と脆弱性の管理 (TVM) を利用し、[Intune を使って TVM によって識別されたエンドポイントの脆弱性を修復](atp-manage-vulnerabilities.md)できます。

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Intune で Microsoft Defender ATP を使用する例

以下の例は、これらのソリューションを連携させて組織を保護するしくみを説明するのに役立ちます。 この例では、Microsoft Defender ATP と Intune は既に統合されています。

誰かが、組織内のユーザーに、悪意のあるコードが埋め込まれた Word の添付ファイルを送信する、というイベントを考えてみましょう。

- そのユーザーは添付ファイルを開き、コンテンツを有効にします。
- 昇格された特権への攻撃が始まります。リモート コンピューターからの攻撃者は犠牲者のデバイスへの管理者権限を持ちます。
- その後、攻撃者はそのユーザーの他のデバイスにリモートでアクセスします。 このセキュリティ違反が組織全体に影響する可能性があります。

Microsoft Defender ATP は、このシナリオのようなセキュリティ イベントを解決するのに役立ちます。

- この例では、Microsoft Defender ATP によって、デバイスで異常なコードが実行され、プロセスの特権エスカレーションが発生し、悪意のあるコードが挿入され、不審なリモート シェルが発行されたことが検出されます。
- デバイスからのこのようなアクションに基づいて、Microsoft Defender ATP により[そのデバイスは危険度が高いと分類され](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity)、Microsoft Defender セキュリティ センターのポータルに疑わしいアクティビティに関する詳細なレポートが追加されます。

Mobile Threat Defense ソリューションとして Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を Microsoft Intune と統合できます。 統合することで、セキュリティ侵害を防止し、組織内での侵害の影響を抑えることができます。

リスク レベルが "*中*" または "*高*" であるデバイスを非準拠として分類する Intune デバイス コンプライアンス ポリシーを使用しているため、侵害されたデバイスは非準拠として分類されます。 この分類により、条件付きアクセス ポリシーが適用されて、そのデバイスから企業リソースへのアクセスがブロックされます。

Android を実行するデバイスの場合、Intune ポリシーを使用して、Android に対する Microsoft Defender ATP の構成を変更することができます。 詳細については、[Microsoft Defender ATP の Web 保護](../protect/advanced-threat-protection-manage-android.md)に関する記事をご覧ください。

## <a name="prerequisites"></a>[前提条件]

Intune で Microsoft Defender ATP を使用する場合は、以下が構成済みであり、使用できる状態であることを確認してください。

- Enterprise Mobility + Security E3 および Windows E5 (または Microsoft 365 Enterprise E5) のライセンス済みテナント
- [Intune で管理されている](../enrollment/windows-enroll.md) Windows 10 デバイスまたは Android デバイス (Azure AD にも参加している) を含む Microsoft Intune 環境
- Microsoft Defender セキュリティ センター (ATP ポータル) にアクセスできる [Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) 環境

> [!NOTE]
> Microsoft Defender ATP は、iOS/iPadOS および Android の Intune アプリ保護ポリシーではサポートされていません。

## <a name="next-steps"></a>次のステップ

- Microsoft Defender ATP を Intune に接続し、デバイスをオンボードして、条件付きアクセス ポリシーを構成するには、「[Intune で Microsoft Defender ATP を構成する](../protect/advanced-threat-protection-configure.md)」をご覧ください。

Intune のドキュメントで詳細を確認します。

- [ATP の脆弱性の管理を使用したセキュリティ タスクを使ってデバイスの問題を修復する](atp-manage-vulnerabilities.md)
- [デバイス コンプライアンス ポリシーの概要](device-compliance-get-started.md)

Microsoft Defender ATP のドキュメントで詳細を確認します。

- [Microsoft Defender ATP の条件付きアクセス](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP のリスク ダッシュボード](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)