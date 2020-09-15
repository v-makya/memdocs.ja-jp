---
title: Microsoft Intune でエンドポイント セキュリティ ポリシーを使用して攻撃の回避設定を管理する | Microsoft Docs
description: Microsoft Intune でエンドポイント セキュリティの攻撃の回避ポリシー設定を使用して管理する、デバイスのポリシーを構成および展開する
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/3/2020
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
ms.openlocfilehash: 303acae2eba275907b70fcc52660217568913c62
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432525"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Intune でのエンドポイント セキュリティの攻撃の回避ポリシー

Windows 10 デバイスで Defender ウイルス対策が使用されている場合は、攻撃の回避のために Intune エンドポイント セキュリティ ポリシーを使用して、デバイスのこれらの設定を管理することができます。

攻撃の回避ポリシーは、サイバー攻撃および攻撃に対する組織の脆弱な場所を最小化することで、攻撃を回避するのに役立ちます。 詳細については、Windows の脅威に対する保護のドキュメントの「[攻撃面の縮小の概要]( /windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction)」を参照してください。

[Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)の **[エンドポイント セキュリティ]** ノードにある *[管理]* で、攻撃の回避のためのエンドポイント セキュリティ ポリシーを見つけます。 各攻撃の回避 "*プロファイル*" では、Windows 10 デバイスの特定の領域の設定が管理されます。

[攻撃の回避プロファイルの設定](../protect/endpoint-security-asr-profile-settings.md)を確認します。

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>攻撃の回避プロファイルの前提条件

- Windows 10 以降
- Defender ウイルス対策は、デバイスのプライマリ ウイルス対策である必要があります。

## <a name="attack-surface-reduction-profiles"></a>攻撃の回避プロファイル

**Windows 10 プロファイル**:

- **アプリとブラウザーの分離** – Defender ATP の一部として、Windows Defender Application Guard (Application Guard) の設定を管理します。 Application Guard を使用すると、以前の攻撃や新たに出現した攻撃を防ぐことができ、エンタープライズ定義サイトを信頼できないものとして分離し、信頼できるサイト、クラウドリソース、および内部ネットワークを定義することができます。

  詳細については、Microsoft Defender ATP ドキュメントの「[Application Guard](/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview)」を参照してください。

- **Web 保護** – Microsoft Defender ATP で Web 保護のために管理できる設定により、Web 脅威からコンピューターを保護するようにネットワーク保護が構成されます。 Web 保護では、Microsoft Edge、および Chrome や Firefox などの一般的なサードパーティ製ブラウザーと統合することで、Web プロキシを使用せずに Web の脅威を防いだり、遠隔またはオンプレミスでコンピューターを保護したりできます。 Web 保護では、次の項目へのアクセスが防止されます。
  - フィッシング サイト
  - マルウェア ベクトル
  - エクスプロイト サイト
  - 信頼されていないサイトまたは低評判のサイト
  - カスタム インジケーター一覧でブロックしたサイト

  詳細については、Microsoft Defender ATP ドキュメントの「[Web 保護](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview)」を参照してください。

- **アプリケーション制御** - アプリケーション制御設定を使用すると、ユーザーが実行できるアプリケーションと System Core (カーネル) で実行されるコードを制限することで、セキュリティの脅威を軽減できます。 署名されていないスクリプトと MSI をブロックし、Windows PowerShell を制約付き言語モードで実行するように制限するための設定を管理します。

  詳細については、Microsoft Defender ATP ドキュメントの[アプリケーション制御](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)に関するページを参照してください。
  
    > [!NOTE]
    > この設定を使用する場合、現在の AppLocker CSP の動作では、ポリシーが展開されたときに、エンド ユーザーに対してコンピューターの再起動を求めるメッセージが表示されます。

- **攻撃の回避規則** – マルウェアおよび悪意のあるアプリでコンピューターに感染させるために通常使用される動作を対象とする、攻撃の回避規則の設定を構成します。次にその一部を示します。
  - ファイルのダウンロードまたは実行を試みる、Office アプリまたは Web メールで使用される実行可能ファイルおよびスクリプト。
  - 難読化されたスクリプトまたは疑わしいスクリプト。
  - アプリで日常業務中に通常は開始されない動作。攻撃面を減少させると、攻撃者が攻撃を実行する手段が少なくなります。

  詳細については、Microsoft Defender ATP ドキュメントの[攻撃の回避規則](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)に関するページを参照してください。

- **デバイス制御** – デバイス制御の設定を使用して、リムーバブル メディアを保護するための階層型アプローチ用にデバイスを構成することができます。 Microsoft Defender ATP では、承認されていない周辺機器の脅威によってデバイスが侵害されるのを防ぐために、複数の監視機能と制御機能が提供されています。

  詳細については、Microsoft Defender ATP ドキュメントの「[Microsoft Defender ATP を使用して USB デバイスとその他のリムーバブル メディアを制御する方法](/windows/security/threat-protection/device-control/control-usb-devices-using-intune)」を参照してください。

- **Exploit Protection** - Exploit Protection 設定は、エクスプロイトを使用してデバイスを感染および拡散させるマルウェアから保護するのに役立ちます。 Exploit Protection は、オペレーティング システムまたは個々のアプリに適用できるさまざまな軽減策で構成されています。

  詳細については、Microsoft Defender ATP ドキュメントの「[Exploit Protection を有効にする](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection)」を参照してください。

## <a name="next-steps"></a>次のステップ

[エンドポイント セキュリティ ポリシーを構成する](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
