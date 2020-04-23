---
title: データとサイト インフラストラクチャの保護
titleSuffix: Configuration Manager
description: Configuration Manager で組織のリソースを漏洩や悪意のある攻撃から保護する方法について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708600"
---
# <a name="protect-data-and-site-infrastructure"></a>データとサイト インフラストラクチャの保護

*適用対象:Configuration Manager (Current Branch)*

ユーザーが組織のリソースに安全にアクセスできるようにする必要があります。 インフラストラクチャとデータの両方を、漏洩や悪意のある攻撃から保護します。 Configuration Manager を使用してアクセスを有効にし、組織のリソースを保護します。  

- [Endpoint Protection](../deploy-use/endpoint-protection.md) では、クライアント コンピューターの次の Microsoft Defender ポリシーを管理できます。

  - Microsoft Defender マルウェア対策
  - Microsoft Defender ファイアウォール
  - Microsoft Defender Advanced Threat Protection
  - Microsoft Defender Exploit Guard
  - Microsoft Defender Application Guard
  - Microsoft Defender アプリケーション制御

  > [!TIP]
  > Microsoft Endpoint Manager クラウド サービスを使用して共同管理されている Windows 10 デバイスのエンドポイント保護を管理するには、[**Endpoint Protection** ワークロード](../../comanage/workloads.md#endpoint-protection)を Intune に切り替えます。 詳細については、[Microsoft Intune のエンドポイント保護](https://docs.microsoft.com/intune/endpoint-protection-windows-10)に関するページを参照してください。

- BitLocker ドライブ暗号化 (BDE) を使用して、オンプレミスの Windows クライアントに格納されているデータを保護します。 Configuration Manager には、Microsoft BitLocker Administration and Monitoring (MBAM) の代わりに使用できる完全な BitLocker ライフサイクル管理機能が用意されています。 詳細については、「[BitLocker 管理の計画](../plan-design/bitlocker-management.md)」を参照してください。

- 従来のパスワードの代わりに、Windows Hello for Business を使用して Windows 10 デバイスで代替サインイン方法を有効にします。 詳細については、[Windows Hello for Business の設定](../deploy-use/windows-hello-for-business-settings.md) に関するページを参照してください。

- VPN プロファイルを使って VPN 接続を有効にして、ユーザーがリソースに接続するための作業を最小限に抑えます。 詳細については、[VPN プロファイル](../deploy-use/vpn-profiles.md)に関するページをご覧ください。  

- Wi-Fi プロファイルには、組織内のデバイスのワイヤレス ネットワーク設定を管理するのに役立つ一連のツールとリソースが用意されています。 この設定を展開することにより、エンド ユーザーがワイヤレス ネットワークに接続するときの作業を最小限に抑えます。 詳細については、[Wi-Fi プロファイル](../deploy-use/create-wifi-profiles.md)に関するページをご覧ください。  

- ユーザーがリソースに接続するために必要な証明書を使用してデバイスをプロビジョニングします。 詳細については、「[Certificate profiles](../deploy-use/introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  
