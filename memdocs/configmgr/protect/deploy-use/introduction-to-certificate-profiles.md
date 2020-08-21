---
title: 証明書プロファイルの概要
titleSuffix: Configuration Manager
description: Configuration Manager の証明書プロファイルを Active Directory 証明書サービスと共に使用する方法について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3598c95d1431915431d96b16c10c7c913741fe3d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699995"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Configuration Manager の証明書プロファイルの概要

*適用対象:Configuration Manager (Current Branch)*

証明書プロファイルは、Active Directory 証明書サービスおよびネットワーク デバイス登録サービス (NDES) ロールと共に使用されます。 ユーザーが組織のリソースに簡単にアクセスできるように、マネージド デバイスに認証証明書を作成して展開します。 たとえば、証明書プロファイルを作成して展開し、ユーザーが VPN 接続およびワイヤレス接続に必要な証明書を提供することができます。

証明書プロファイルでは、Wi-Fi ネットワークや VPN サーバーなど組織のリソースにアクセスするために、ユーザー デバイスを自動的に構成できます。 ユーザーは、手動で証明書をインストールしたり、帯域外プロセスを使用したりすることなく、これらのリソースにアクセスできます。 証明書プロファイルを使用すると、公開キー基盤 (PKI) でサポートされているさらに安全な設定を使用できるため、リソースをセキュリティで保護するために役立ちます。 たとえば、マネージド デバイスに必要な証明書を展開しているため、すべての Wi-Fi 接続と VPN 接続に対してサーバー認証を要求します。

証明書プロファイルが提供する管理機能:  

- 異なる OS の種類とバージョンを実行しているデバイスの証明機関 (CA) からの証明書の登録と更新。 これらの証明書を Wi-Fi 接続と VPN 接続に使用できます。  

- 信頼されたルート CA 証明書と中間 CA 証明書の展開。 これらの証明書では、サーバー認証が必要な場合に VPN 接続のデバイスと Wi-Fi 接続のデバイスで信頼関係のチェーンを構成します。  

- インストールされている証明書を監視してレポートします。  

**例 1**:すべての従業員が、複数のオフィスにある Wi-Fi ホットスポットに接続する必要があります。 簡単なユーザー接続を有効にするには、最初に Wi-Fi への接続に必要な証明書を展開します。 次に、証明書を参照する Wi-Fi プロファイルを展開します。  

**例 2**:PKI が配置されています。 より柔軟でセキュリティで保護された方法で証明書を展開する必要があります。 ユーザーは、セキュリティを低下させることなく、個人のデバイスから組織のリソースにアクセスする必要があります。 特定のデバイス プラットフォーム用にサポートされている設定とプロトコルを使用して、証明書プロファイルを構成します。 デバイスは、インターネットに接続された登録サーバーに対してこれらの証明書を自動的に要求することができます。 その後、デバイスが組織のリソースにアクセスできるように、これらの証明書を使用するように VPN プロファイルを構成します。  

## <a name="types"></a>種類

次の 3 種類の証明書プロファイルがあります。  

- **信頼された CA 証明書**: 信頼されたルート CA 証明書または中間 CA 証明書を展開します。 デバイスでサーバーを認証する必要がある場合、これらの証明書で信頼関係のチェーンが形成されます。  

- **Simple Certificate Enrollment Protocol (SCEP)** :SCEP プロトコルを使用して、デバイスまたはユーザーの証明書を要求します。 この種類には、Windows Server 2012 R2 以降を実行するサーバー上のネットワーク デバイス登録サービス (NDES) ロールが必要です。

    **Simple Certificate Enrollment Protocol (SCEP)** の証明書プロファイルを作成するには、最初に**信頼された CA 証明書**プロファイルを作成します。

- **Personal information exchange (.pfx)** :デバイスまたはユーザーの .pfx (別名、PKCS #12) 証明書を要求します。<!--1321368--> PFX 証明書プロファイルを作成するには、次の 2 つの方法があります。

  - 既存の証明書から[資格情報をインポートする](../../mdm/deploy-use/import-pfx-certificate-profiles.md)
  - 要求を処理するための[証明機関を定義する](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

  > [!Note]  
  > Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。<!--505213-->  

  **Personal information exchange (.pfx)** 証明書の証明機関として Microsoft または Entrust を使用できます。

## <a name="requirements"></a>要件

SCEP を使用する証明書プロファイルを展開するには、証明書登録ポイントをサイト システム サーバーにインストールします。 また、NDES 用のポリシー モジュール (Configuration Manager ポリシー モジュール) を Windows Server 2012 R2 以降を実行するサーバーにインストールします。 このサーバーには、Active Directory 証明書サービスの役割が必要です。 また、証明書が必要なデバイスにアクセスできる動作中の NDES も必要です。 デバイスでインターネットからの証明書を登録する必要がある場合は、NDES サーバーにインターネットからアクセスできる必要があります。 たとえば、インターネットから NDES サーバーへのトラフィックを安全に有効にするには、[Azure アプリケーション プロキシ](/azure/active-directory/manage-apps/application-proxy)を使用できます。

PFX 証明書には、証明書登録ポイントも必要です。 また、証明書の証明機関 (CA) と関連するアクセス資格情報も指定します。 証明機関として Microsoft または Entrust のいずれかを指定できます。  

Configuration Manager で証明書を展開するためのネットワーク デバイス登録サービスとポリシー モジュールのしくみについては、「[Using a Policy Module with the Network Device Enrollment Service](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\))」 (ポリシー モジュールとネットワーク デバイス登録サービスの使用) を参照してください。

要件に応じて、Configuration Manager では、さまざまなデバイスの種類やオペレーティング システム上で異なる証明書ストアへの証明書の展開をサポートします。 次のデバイスとオペレーティング システムがサポートされています。  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> Windows Phone 8.1 と Windows 10 Mobile を管理するには、Configuration Manager オンプレミス MDM を使用します。 詳細については、「[オンプレミス MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」を参照してください。

Configuration Manager の一般的なシナリオは、Wi-Fi および VPN サーバーを認証するために、信頼されたルート CA 証明書をインストールすることです。 一般的な接続では、次のプロトコルを使用します。

- 認証プロトコル:EAP-TLS、EAP-TTLS、および PEAP
- VPN トンネリング プロトコル:IKEv2、L2TP/IPsec、および Cisco IPsec

デバイスが SCEP 証明書プロファイルを使用して証明書を要求するには、そのデバイスにエンタープライズ ルート CA 証明書がインストールされている必要があります。  

さまざまな環境や接続要件に合わせてカスタマイズされた証明書を要求するように、SCEP 証明書プロファイルに設定を指定できます。 **証明書プロファイルの作成ウィザード** には、登録パラメーター用のページが 2 つあります。 1 つ目の **[SCEP 登録]** には、登録要求の設定と証明書のインストール先の場所が含まれています。 もう 1 つの **[証明書のプロパティ]** は、要求する証明書自体を説明するページです。  

## <a name="deploy"></a>デプロイ

SCEP 証明書プロファイルを展開すると、Configuration Manager クライアントがポリシーを処理します。 次に、管理ポイントから SCEP チャレンジ パスワードを要求します。 デバイスは公開キーと秘密キーのペアを作成し、証明書署名要求 (CSR) を生成します。 この要求を NDES サーバーに送信します。 NDES サーバーは、NDES ポリシー モジュールを使用して、証明書登録ポイントのサイト システムに要求を転送します。 証明書登録ポイントは、要求を検証し、SCEP チャレンジ パスワードを確認して、要求が改ざんされていないことを確認します。 その後、要求を承認または拒否します。 承認されると、NDES サーバーは署名のために署名要求を接続された証明機関 (CA) に送信します。 CA は要求に署名し、要求元のデバイスに証明書を返します。

ユーザーまたはデバイスのコレクションに証明書プロファイルを展開します。 各証明書の保存先ストアを指定できます。 適用規則によって、デバイスが証明書をインストールできるかどうかが決まります。

証明書プロファイルをユーザー コレクションに展開する場合は、[ユーザーとデバイスのアフィニティ](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)によって、証明書をインストールするユーザーのデバイスが決まります。 ユーザー証明書を使用して証明書プロファイルをデバイス コレクションに展開すると、既定では、各ユーザーのプライマリ デバイスによって証明書がインストールされます。 ユーザーの任意のデバイス上に証明書をインストールするには、**証明書プロファイルの作成ウィザード**の **[SCEP 登録]** ページでこの動作を変更します。 デバイスがワークグループに含まれている場合、Configuration Manager はユーザー証明書を展開しません。  

## <a name="monitor"></a>モニター

コンプライアンスの結果やレポートを表示し、証明書プロファイルの展開を監視できます。 詳細については、「[証明書プロファイルを監視する方法](monitor-certificate-profiles.md)」を参照してください。

## <a name="automatic-revocation"></a>自動失効

Configuration Manager で、証明書プロファイルを使用して展開したユーザー証明書とコンピューター証明書は次のような場合に自動的に失効します。  

- デバイスが Configuration Manager の管理下のインベントリから削除された場合。  

- デバイスが Configuration Manager の階層からブロックされた場合。  

証明書を失効させるために、サイト サーバーが、証明書の発行元の証明機関に失効コマンドを送信します。 この失効の理由は、「 **運用停止** 」です。

> [!NOTE]
> 証明書を適切に失効させるには、階層内の最上位サイトのコンピューター アカウントに、CA で**証明書の発行と管理**を行うためのアクセス許可が必要です。
>
> セキュリティを強化するために、CA の CA マネージャーを制限することもできます。 次に、サイトの SCEP プロファイルに使用する特定の証明書テンプレートに対してのみ、このアカウントのアクセス許可を与えます。

## <a name="next-steps"></a>次のステップ

- [証明書プロファイルの作成](create-certificate-profiles.md)

- [証明書インフラストラクチャの構成](certificate-infrastructure.md)