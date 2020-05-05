---
title: オンプレミス MDM の計画
titleSuffix: Configuration Manager
description: Configuration Manager でモバイルデバイスを管理するためのオンプレミスモバイルデバイス管理の計画
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724696"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager でのオンプレミス MDM の計画

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager でオンプレミスモバイルデバイス管理 (MDM) を実装する計画を立てる際には、いくつかの重要な点を確認する必要があります。

- サポートされているデバイスと OS のバージョン
- 必要なサイト システムの役割
- 安全な通信
- デバイスの登録

> [!IMPORTANT]
> サイトまたはモバイルデバイスが Microsoft Intune に接続していない場合でも、この機能を使用するには Intune ライセンスが必要になります。 詳細については、「 [Microsoft Intune ライセンス](https://docs.microsoft.com/intune/fundamentals/licenses)」を参照してください。

オンプレミスの MDM を処理するために Configuration Manager インフラストラクチャを準備する前に、次の要件を考慮してください。

## <a name="supported-devices"></a><a name="bkmk_devices"></a> サポートされるデバイス  

Configuration Manager の現在のブランチは、Windows 10 を実行しているデバイスのオンプレミスモバイルデバイス管理での登録をサポートしています。 これらのデバイスの種類には、主にノート pc、IoT、および Surface Hub が含まれます。 詳細および特定のエディションの一覧については、「[クライアントとデバイスでサポートされる OS バージョン](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)」を参照してください。

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> サイト システムの役割

オンプレミス MDM には、次のサイトシステムの役割のうち少なくとも1つが必要です。

- **登録プロキシ ポイント** 。登録要求をサポートします。

- **登録ポイント** 。デバイスの登録をサポートします。

- **デバイス管理ポイント** 。ポリシー配信用です。 この役割は管理ポイントの一種であり、モバイルデバイス管理を可能にします。

- **配布ポイント** 。コンテンツ配信用です。

組織のニーズに応じて、これらの役割を1台のサーバーにインストールすることも、別々のサーバーにインストールすることもできます。

> [!NOTE]
> オンプレミスの MDM に使用される各ロールを、信頼されたデバイスと通信するための HTTPS エンドポイントとして構成する必要があります。 詳細については、「 [必要な信頼された通信](#bkmk_trustedComs)」をご覧ください。

一般的な情報については、「[サイトシステムサーバーと役割の計画](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)」を参照してください。

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>信頼できる通信

オンプレミス MDM では、HTTPS 通信用にサイトシステムの役割を有効にする必要があります。 必要に応じて、組織の証明機関 (CA) を使用して、サーバーとデバイス間の信頼関係接続を確立することができます。 また、信頼された機関として公開されている CA を使用することもできます。 どちらの場合も、次の証明書を構成する必要があります。

- 必要なサイトシステムの役割をホストしているサーバー上の IIS の**web サーバー証明書**。 1台のサーバーが複数のサイトシステムの役割をホストしている場合は、そのサーバーの証明書を1つだけ必要とします。 各ロールが個別のサーバー上にある場合は、各サーバーに個別の証明書が必要です。

- Web サーバー証明書を発行する CA の**信頼されたルート証明書**。 サイトシステムの役割に接続する必要があるすべてのデバイスに、このルート証明書をインストールします。

詳細については、「[オンプレミス MDM での信頼された通信用の証明書の設定](../get-started/set-up-certificates-on-premises-mdm.md)」を参照してください。

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>デバイスの登録

オンプレミス MDM のデバイス登録を有効にするには:

- クライアント設定を使用して登録するためのアクセス許可をユーザーに付与する

- 必要な役割をホストしているサイトシステムサーバーとの信頼された通信用にデバイスを構成する

ユーザーが開始した登録の代わりに、一括登録パッケージを設定することもできます。 このパッケージを使用すると、ユーザーの介入なしにデバイスを登録できます。 使用するためにプロビジョニングされる前、または OOBE プロセスの実行後に、デバイスにパッケージを配信します。

詳細については、「[オンプレミス MDM のデバイス登録の設定](../get-started/set-up-device-enrollment-on-premises-mdm.md)」を参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [サイト システムの役割のインストール](../get-started/install-site-system-roles-for-on-premises-mdm.md)
