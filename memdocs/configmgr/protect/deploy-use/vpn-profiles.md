---
title: VPN プロファイル
titleSuffix: Configuration Manager
description: Configuration Manager の VPN プロファイルを使用して、VPN 設定を組織内のユーザーに展開する方法について説明します。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706250"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Configuration Manager の VPN プロファイル

*適用対象:Configuration Manager (Current Branch)*

<!--1283610-->
組織内のユーザーに VPN 設定を展開するには、Configuration Manager の VPN プロファイルを使用します。 これらの設定を展開して、企業ネットワーク上のリソースに接続するために必要なエンド ユーザーの作業を最小化します。  

たとえば、内部ネットワーク上のファイル共有に接続するために必要な設定をすべての Windows 10 デバイスに構成する必要があるとします。 内部ネットワークに接続するために必要な設定が含まれる VPN プロファイルを作成します。 次いで、Windows 10 を実行しているデバイスを使用するすべてのユーザーに、このプロファイルを展開します。 VPN 接続は、これらのユーザーに、使用できるネットワークの一覧として表示されるので、ユーザーは最小限の労力で接続できます。

VPN プロファイルを作成するときに、さまざまなセキュリティ設定を含めることができます。 これらの設定には、Configuration Manager の証明書プロファイルを使ってプロビジョニングする、サーバー評価用の証明書やクライアント認証用の証明書があります。 詳細については、「[Certificate profiles](introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。

> [!Note]
> Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。<!--505213-->  

## <a name="supported-platforms"></a>サポートされているプラットフォーム

次の表では、さまざまなデバイス プラットフォームに対して構成できる VPN プロファイルについて説明します。

|接続の種類|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|はい|いいえ|はい|はい|
|**F5 Edge Client**|はい|いいえ|はい|はい|
|**Dell SonicWALL Mobile Connect**|はい|いいえ|はい|はい|
|**チェック ポイント モバイル VPN**|はい|いいえ|はい|はい|
|**Microsoft SSL (SSTP)**|はい|はい|はい|いいえ|
|**Microsoft 自動**|はい|はい|はい|いいえ|
|**IKEv2**|はい|はい|はい|いいえ|
|**PPTP**|はい|はい|はい|いいえ|
|**L2TP**|はい|はい|はい|いいえ|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [VPN プロファイルの作成方法](create-vpn-profiles.md)

## <a name="see-also"></a>関連項目

- [VPN プロファイルの前提条件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [VPN プロファイルのセキュリティとプライバシー](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
