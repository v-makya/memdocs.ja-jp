---
title: PFX 証明書プロファイルインポート
titleSuffix: Configuration Manager
description: Configuration Manager で PFX ファイルをインポートして、暗号化されたデータ交換をサポートするユーザー固有の証明書を生成する方法について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef8c1656c12ead992d5305cdf86b1ab8fcfcb836
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608432"
---
# <a name="import-pfx-certificate-profiles"></a>PFX 証明書プロファイルインポート

*適用対象:Configuration Manager (Current Branch)*

外部証明書から資格情報をインポートして証明書プロファイルを作成する方法について説明します。 この記事では、personal information exchange (PFX) 証明書プロファイルに関する特定の情報について説明します。 これらのプロファイルを作成して構成する方法の詳細については、「 [証明書プロファイル](../../protect/deploy-use/introduction-to-certificate-profiles.md)」を参照してください。

Configuration Manager は、さまざまな種類のデバイスと OS バージョンに対応するさまざまな種類の証明書ストアをサポートしています。 たとえば、Windows 10 と Windows 10 Mobile です。 詳細については、「 [証明書プロファイルの前提条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)」を参照してください。

Configuration Manager を使用して証明書の資格情報をインポートし、PFX ファイルをデバイスにプロビジョニングします。 これらのファイルを使用して、暗号化されたデータ交換をサポートするユーザー固有の証明書を生成できます。

> [!TIP]  
> このプロセスの詳細な手順については、 [Configuration Manager で PFX 証明書プロファイルを作成して展開する方法に](/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager)関するブログ投稿を参照してください。  

## <a name="create-a-profile"></a>プロファイルの作成

1. Configuration Manager コンソールで、[ **資産とコンプライアンス** ] ワークスペースにアクセスし、[ **コンプライアンス設定**]、[ **会社リソースのアクセス**] の順に展開して、[ **証明書プロファイル**] を選択します。

1. リボンの **[ホーム]** タブの **[作成]** グループで、**[証明書プロファイルの作成]** を選択します。

1. **証明書プロファイルの作成ウィザード**の **[全般**] ページで、次の情報を指定します。  

    - **名前**: 証明書プロファイルの固有な名前を入力します。 最大 256 文字を使用できます。  

    - **説明**: Configuration Manager コンソールで証明書を識別するのに役立つ、証明書プロファイルの概要を示す説明を入力します。 最大 256 文字を使用できます。  

1. [ **Personal Information Exchange-PKCS #12 (PFX) の設定-インポート**] を選択します。 このオプションは、既存の証明書から情報をインポートして、証明書プロファイルを作成します。

    > [!NOTE]
    > **Create**オプションは、接続されているオンプレミスの証明機関 (CA) からユーザーの代わりに証明書を要求します。 その後、このプロセスは証明書を PFX ファイルとしてクライアントに安全に配信します。 詳細については、「 [証明機関を使用した PFX 証明書プロファイルの作成](create-pfx-certificate-profiles.md)」を参照してください。

1. **証明書プロファイルの作成ウィザード**の [ **PFX 証明書**] ページで、デバイスのキー格納プロバイダー (KSP) を指定します。

    - **トラステッド プラットフォーム モジュール (TPM) にインストールする (存在する場合)**  
    - **トラステッドプラットフォームモジュール (TPM) にインストールする (それ以外は失敗)**
    - **Windows Hello for Business にインストールする (それ以外は失敗)**
    - **ソフトウェア キー記憶域プロバイダーにインストールする**

1. [ **サポートさ** れているプラットフォーム] ページで、サポートされているデバイスプラットフォームを選択します。

1. ウィザードを完了します。

## <a name="deploy-the-profile"></a>プロファイルのデプロイ

証明書プロファイルを作成してプロビジョニングすると、[ **証明書プロファイル** ] ノードで使用できるようになります。 デプロイ方法の詳細については、「 [リソースアクセスプロファイルのデプロイ](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)」を参照してください。

## <a name="assign-primary-users"></a>プライマリユーザーの割り当て

PFX 証明書をインストールする必要がある Windows 10 デバイスで、ターゲットユーザーをプライマリユーザーとして割り当てます。 詳細については、「 [ユーザーとデバイスのアフィニティ](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。

## <a name="provision-a-create-pfx-script"></a>PFX スクリプトの作成をプロビジョニングする

PFX 証明書をインポートするには、次の Configuration Manager PowerShell コマンドレットを使用して PFX 作成スクリプトをプロビジョニングします。

- [取得-CMClientCertificatePfx](/powershell/module/configurationmanager/get-cmclientcertificatepfx)
- [インポート-CMClientCertificatePfx](/powershell/module/configurationmanager/import-cmclientcertificatepfx)
- [CMClientCertificatePfx を削除します。](/powershell/module/configurationmanager/remove-cmclientcertificatepfx)

### <a name="example-script"></a>サンプル スクリプト

PFX ファイルをユーザーの証明書プロファイルにプロビジョニングするには、Configuration Manager コンソールを使用してコンピューターで PowerShell を開きます。 変数を環境の値で変更します。

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>関連項目

[新しい証明書プロファイルを作成する](../../protect/deploy-use/create-certificate-profiles.md)

[証明機関を使用して PFX 証明書プロファイルを作成する](create-pfx-certificate-profiles.md)

[Wi-Fi、VPN、電子メール、および証明書プロファイルの展開](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)