---
title: PFX 証明書プロファイルの作成
titleSuffix: Configuration Manager
description: Configuration Manager で PFX ファイルを使用して、暗号化されたデータ交換をサポートするユーザー固有の証明書を生成する方法について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724576"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>証明機関を使用して PFX 証明書プロファイルを作成する

*適用対象:Configuration Manager (Current Branch)*

資格情報に証明機関を使用する証明書プロファイルを作成する方法について説明します。 この記事では、personal information exchange (PFX) 証明書プロファイルに関する特定の情報について説明します。 これらのプロファイルを作成して構成する方法の詳細については、「[証明書プロファイル](../../protect/deploy-use/introduction-to-certificate-profiles.md)」を参照してください。

Configuration Manager では、証明機関によって発行された資格情報を使用して PFX 証明書プロファイルを作成できます。 証明機関として Microsoft または Entrust を選択できます。 PFX ファイルをユーザーデバイスに展開すると、暗号化されたデータ交換をサポートするためのユーザー固有の証明書が生成されます。

既存の証明書ファイルから証明書の資格情報をインポートするには、「 [PFX 証明書プロファイルをインポート](import-pfx-certificate-profiles.md)する」を参照してください。

## <a name="prerequisites"></a>前提条件

証明書プロファイルの作成を開始する前に、必要な前提条件が満たされていることを確認してください。 詳細については、「[証明書プロファイルの前提条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)」を参照してください。 たとえば、PFX 証明書プロファイルの場合は、[証明書登録ポイント](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point)サイトシステムの役割が必要です。

## <a name="create-a-profile"></a>プロファイルを作成する  

1. Configuration Manager コンソールで、[**資産とコンプライアンス**] ワークスペースにアクセスし、[**コンプライアンス設定**]、[**会社リソースのアクセス**] の順に展開して、[**証明書プロファイル**] を選択します。

1. リボンの **[ホーム]** タブの **[作成]** グループで、**[証明書プロファイルの作成]** を選択します。

1. **証明書プロファイルの作成ウィザード**の **[全般**] ページで、次の情報を指定します。  

    - **名前**: 証明書プロファイルの固有な名前を入力します。 最大 256 文字を使用できます。  

    - **説明**: Configuration Manager コンソールで証明書を識別するのに役立つ、証明書プロファイルの概要を示す説明を入力します。 最大 256 文字を使用できます。  

1. [ **Personal Information Exchange-PKCS #12 (PFX) 設定-作成**] を選択します。 このオプションは、接続されているオンプレミスの証明機関 (CA) からのユーザーの代理で証明書を要求します。 証明機関 ( **Microsoft**または**Entrust Datacard**) を選択します。

    > [!NOTE]
    > **インポート**オプションでは、既存の証明書から情報を取得して、証明書プロファイルを作成します。 詳細については、[PFX 証明書プロファイルのインポート](import-pfx-certificate-profiles.md)に関するページを参照してください。

1. [**サポートされているプラットフォーム**] ページで、この証明書プロファイルでサポートされている OS バージョンを選択します。 Configuration Manager のバージョンでサポートされている OS バージョンの詳細については、「[クライアントとデバイスでサポートされる os バージョン](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)」を参照してください。

1. [**証明機関**] ページで、証明書登録ポイント (CRP) を選択して PFX 証明書を処理します。

    1. [**プライマリサイト**]: CA の CRP ロールを含むサーバーを選択します。
    1. [**証明機関**]: 関連する CA を選択します。

    詳細については、[「証明書インフラストラクチャ」](../../protect/deploy-use/certificate-infrastructure.md) をご覧ください。

[ **PFX 証明書**] ページの設定は、 **[全般**] ページで選択した CA によって異なります。

- [Microsoft CA](#bkmk_microsoft)
- [Entrust Datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>Microsoft CA の**PFX 証明書**の設定を構成する

1. **証明書テンプレート名**として、証明書テンプレートを選択します。

1. S/MIME 署名または暗号化に証明書プロファイルを使用するには、**証明書の使用**を有効にします。

    このオプションを有効にすると、対象ユーザーに関連付けられているすべての PFX 証明書がすべてのデバイスに配信されます。 このオプションを有効にしない場合、各デバイスは一意の証明書を受け取ります。  

1. **[サブジェクト名の形式]** を **[共通名]** または **[完全な識別名]** に設定します。 どちらを使用すればよいかわからない場合は、CA 管理者に問い合わせてください。

1. [**サブジェクトの別名**] で、CA に適した**電子メールアドレス**と**ユーザープリンシパル名 (UPN)** を有効にします。

1. **更新しきい値**: 有効期限が切れるまでの残り時間の割合に基づいて、証明書を自動的に更新するかどうかを決定します。

1. **[証明書の有効期間]** に証明書の有効期間を設定します。

1. 証明書登録ポイントで Active Directory の資格情報が指定されている場合は**Active Directory の発行**を有効にします。

1. 1つまたは複数の Windows 10 でサポートされているプラットフォームを選択した場合:

    1. **Windows 証明書ストア**を**ユーザー**に設定します。 ([**ローカルコンピューター** ] オプションでは証明書は展開されず、選択しないでください)。

    1. 次のいずれかの**キー記憶域プロバイダー (KSP)** を選択します。

        - **トラステッド プラットフォーム モジュール (TPM) にインストールする (存在する場合)**  
        - **トラステッドプラットフォームモジュール (TPM) にインストールする (それ以外は失敗)**
        - **Windows Hello for Business にインストールする (それ以外は失敗)**
        - **ソフトウェア キー記憶域プロバイダーにインストールする**

1. ウィザードを完了します。

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>Entrust Datacard CA の**PFX 証明書**の設定を構成する

1. **デジタル ID 構成**については、構成プロファイルを選択します。 Entrust 管理者は、デジタル ID 構成オプションを作成します。

1. S/MIME 署名または暗号化に証明書プロファイルを使用するには、**証明書の使用**を有効にします。

    このオプションを有効にすると、対象ユーザーに関連付けられているすべての PFX 証明書がすべてのデバイスに配信されます。 このオプションを有効にしない場合、各デバイスは一意の証明書を受け取ります。  

1. Entrust の**サブジェクト名の形式**のトークンを Configuration Manager フィールドにマップするには、[**書式**] を選択します。

    **[Certificate Name Formatting]\(証明書名の形式\)** に、Entrust デジタル ID 構成変数の一覧が表示されます。 各 Entrust 変数に対して、適切な Configuration Manager フィールドを選択します。

1. サポートされている LDAP 変数に Entrust**サブジェクト代替名**トークンをマップするには、[**形式**] を選択します。

    **[Certificate Name Formatting]\(証明書名の形式\)** に、Entrust デジタル ID 構成変数の一覧が表示されます。 各 Entrust 変数に対して、適切な LDAP 変数を選択します。

1. **更新しきい値**: 有効期限が切れるまでの残り時間の割合に基づいて、証明書を自動的に更新するかどうかを決定します。

1. **[証明書の有効期間]** に証明書の有効期間を設定します。

1. 証明書登録ポイントで Active Directory の資格情報が指定されている場合は**Active Directory の発行**を有効にします。

1. 1つまたは複数の Windows 10 でサポートされているプラットフォームを選択した場合:

    1. **Windows 証明書ストア**を**ユーザー**に設定します。 ([**ローカルコンピューター** ] オプションでは証明書は展開されず、選択しないでください)。

    1. 次のいずれかの**キー記憶域プロバイダー (KSP)** を選択します。

        - **トラステッド プラットフォーム モジュール (TPM) にインストールする (存在する場合)**  
        - **トラステッドプラットフォームモジュール (TPM) にインストールする (それ以外は失敗)**
        - **Windows Hello for Business にインストールする (それ以外は失敗)**
        - **ソフトウェア キー記憶域プロバイダーにインストールする**

1. ウィザードを完了します。

## <a name="deploy-the-profile"></a>プロファイルのデプロイ

証明書プロファイルを作成したら、[**証明書プロファイル**] ノードで使用できるようになります。 デプロイ方法の詳細については、「[リソースアクセスプロファイルのデプロイ](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)」を参照してください。

## <a name="see-also"></a>関連項目

[新しい証明書プロファイルを作成する](../../protect/deploy-use/create-certificate-profiles.md)

[PFX 証明書プロファイルインポート](import-pfx-certificate-profiles.md)

[、VPN、電子メール、および証明書プロファイルの展開](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
