---
title: Microsoft Intune での証明書プロファイルの作成 - Azure | Microsoft Docs
description: Microsoft Intune で Simple Certificate Enrollment Protocol (SCEP) 証明書または Public Key Cryptography Standards (PKCS) 証明書と証明書プロファイルを使用する方法について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1db36b0ea3d2ba691811958a01043a606b4681a
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251974"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>Microsoft Intune で認証に証明書を使用する

Intune で証明書を使用し、VPN、Wi-Fi、電子メール プロファイルを介してアプリケーションや企業リソースに対してユーザーが本人であることを確認します。 接続の認証に証明書を使用すると、エンド ユーザーはユーザー名とパスワードを入力する必要がなくなり、アクセスがシームレスになります。 証明書は、S/MIME を使用した電子メールの署名と暗号化にも使用されます。

## <a name="intune-supported-certificates-and-usage"></a>Intune でサポートされている証明書と使用方法

| Type              | 認証 | S/MIME 署名 | S/MIME 暗号化  |
|--|--|--|--|
| 公開キー暗号化標準 (PKCS) のインポートされた証明書 |  | ![サポート](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png)|
| PKCS#12 (または PFX)    | ![サポート](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png) |  |
| Simple Certificate Enrollment Protocol (SCEP)  | ![サポート](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png) | |

このような証明書を配備するには、証明書プロファイルを作成し、デバイスに割り当てます。

作成する証明書プロファイルは、1 つにつきプラットフォームを 1 つサポートします。 たとえば、PKCS 証明書を使用する場合、Android 用の PKCS 証明書プロファイルと iOS/iPadOS 用の別の PKCS 証明書プロファイルを別々に作成します。 この 2 つのプラットフォームに SCEP 証明書も使用する場合、Android 用に 1 つ、iOS/iPadOS 用に 1 つ、SCEP 証明書プロファイルを作成します。

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>Microsoft の証明機関を使用する場合の一般的な考慮事項

Microsoft の証明機関 (CA) を使用する場合:

- SCEP 証明書プロファイルを使用するには、Intune で使用する[ネットワーク デバイス登録サービス (NDES) サーバーを設定する](certificates-scep-configure.md#set-up-ndes)必要があります。
- 次の証明書プロファイルの種類を使用するには、[Microsoft Intune 証明書コネクタをインストールする](certificates-scep-configure.md#install-the-intune-certificate-connector)必要があります。
  - SCEP 証明書プロファイル
  - PKCS 証明書プロファイル

- PKCS のインポートされた証明書を使用するには:
  - [PFX Certificate Connector for Microsoft Intune をインストールします](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune)。
  - 証明機関から証明書をエクスポートし、Microsoft Intune にインポートします。 「[PFXImport PowerShell プロジェクト](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell)」を参照してください。

- 次のメカニズムで証明書を展開します。
  - [信頼された証明書プロファイル](certificates-configure.md#create-trusted-certificate-profiles): 信頼されたルート CA 証明書をルートまたは中間 (発行) CA からデバイスに展開するため
  - SCEP 証明書プロファイル
  - PKCS 証明書プロファイル
  - PKCS のインポートされた証明書プロファイル

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>サードパーティの証明機関を使用する場合の一般的な考慮事項

サードパーティ (Microsoft 以外) の証明機関 (CA) を使用する場合:

- SCEP 証明書プロファイルを作成するには:
  - [サポートされているパートナーのいずれか](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners)からのサードパーティの CA との統合を設定します。 設定には、サードパーティの CA からの指示に従って、CA と Intune の統合を完了することも含まれます。
  - SCEP 証明書チャレンジの検証を行うために Intune に権限を委任する[アプリケーションを Azure AD で作成します](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration)。

- PKCS のインポートされた証明書では、[PFX Certificate Connector for Microsoft Intune をインストールする](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune)必要があります。

- 次のメカニズムで証明書を展開します。
  - [信頼された証明書プロファイル](certificates-configure.md#create-trusted-certificate-profiles): 信頼されたルート CA 証明書をルートまたは中間 (発行) CA からデバイスに展開するため
  - SCEP 証明書プロファイル
  - PKCS 証明書プロファイル *([Digicert PKI プラットフォーム](certificates-digicert-configure.md)でのみサポートされています)*
  - PKCS のインポートされた証明書プロファイル

## <a name="supported-platforms-and-certificate-profiles"></a>サポートされているプラットフォームと証明書プロファイル

| プラットフォーム              | 信頼された証明書プロファイル | PKCS 証明書プロファイル | SCEP 証明書プロファイル | PKCS のインポートされた証明書プロファイル  |
|--|--|--|--|---|
| Android デバイス管理者 | ![サポート](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png)|  ![サポート](./media/certificates-configure/green-check.png) |
| Android エンタープライズ <br> - フル マネージド (デバイスの所有者)   | ![サポート](./media/certificates-configure/green-check.png) |   | ![サポート](./media/certificates-configure/green-check.png) |  ![サポート](./media/certificates-configure/green-check.png)  |
| Android エンタープライズ <br> - 専用 (デバイスの所有者)   | ![サポート](./media/certificates-configure/green-check.png)  | ![サポート](./media/certificates-configure/green-check.png) | ![サポートされています](./media/certificates-configure/green-check.png)  | ![サポート](./media/certificates-configure/green-check.png)|
| Android エンタープライズ <br> - 会社所有の仕事用プロファイル   | ![サポート](./media/certificates-configure/green-check.png)  |  | ![サポート](./media/certificates-configure/green-check.png)  | ![サポート](./media/certificates-configure/green-check.png)  |
| Android エンタープライズ <br> - 仕事用プロファイル    | ![サポート](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png) | ![サポートされています](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![サポート](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png) | ![サポートされています](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png) |
| macOS                 | ![サポート](./media/certificates-configure/green-check.png) |  ![サポートされています](./media/certificates-configure/green-check.png) |![サポート](./media/certificates-configure/green-check.png)|![サポート](./media/certificates-configure/green-check.png)|
| Windows 8.1 以降 |![サポート](./media/certificates-configure/green-check.png)  |  |![サポート](./media/certificates-configure/green-check.png) |   |
| Windows 10 以降  | ![サポート](./media/certificates-configure/green-check.png) | ![サポートされています](./media/certificates-configure/green-check.png) | ![サポートされています](./media/certificates-configure/green-check.png) | ![サポート](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>信頼されたルート CA 証明書をエクスポートする

PKCS、SCEP、PKCS のインポートされた証明書を使用するには、デバイスでルート証明機関を信頼する必要があります。 信頼を確立するには、信頼されたルート CA 証明書だけでなく、中間または発行元の証明機関の証明書も公開証明書 (.cer) としてエクスポートします。 このような証明書は、発行元 CA か、発行元 CA を信頼する任意のデバイスから取得できます。

証明書をエクスポートするには、証明機関のドキュメントを参照してください。 公開証明書は .cer ファイルとしてエクスポートする必要があります。  秘密キー (.pfx ファイル) をエクスポートしないでください。

[信頼された証明書プロファイルを作成](#create-trusted-certificate-profiles)し、その証明書をデバイスに配備するとき、この .cer ファイルを使用します。

## <a name="create-trusted-certificate-profiles"></a>信頼された証明書プロファイルを作成する

SCEP、PKCS、または PKCS のインポートされた証明書プロファイルを作成する前に、信頼された証明書プロファイルを作成して展開します。 他の種類の証明書プロファイルを受信するグループと同じグループに信頼された証明書プロファイルを展開すると、各デバイスで CA の正当性を認識できるようになります。 これには、VPN、Wi-Fi、電子メールなどのプロファイルが含まれます。

SCEP 証明書プロファイルでは、信頼された証明書プロファイルが直接参照されます。 PKCS 証明書プロファイルでは、信頼された証明書プロファイルが直接参照されず、CA をホストするサーバーが直接参照されます。 PKCS のインポートされた証明書プロファイルでは、信頼された証明書プロファイルが直接参照されませんが、デバイス上で利用されることがあります。 信頼された証明書プロファイルをデバイスに配備することで、この信頼が確立されます。 デバイスでルート CA が信頼されない場合、SCEP または PKCS 証明書プロファイル ポリシーは失敗します。

SCEP、PKCS、PKCS のインポートされた証明書プロファイルの場合と同様に、サポートするデバイス プラットフォームごとに別個の信頼された証明書プロファイルを作成します。

> [!IMPORTANT]
> *Windows 10 以降*のプラットフォーム用に作成する信頼されたルート プロファイルは、Microsoft Endpoint Manager admin center には *Windows 8.1 以降*のプラットフォーム用のプロファイルとして表示されます。 
>
> これは、信頼された証明書プロファイルのプラットフォームの表示に関する既知の問題です。 プロファイルには Windows 8.1 以降のプラットフォームが表示されますが、Windows 10 以降で機能します。

> [!NOTE]
> Intune の "*信頼された証明書*" プロファイルは、ルート証明書または中間証明書を提供するためにのみ使用できます。 このような証明書を展開する目的は、信頼チェーンを確立することです。 信頼された証明書プロファイルを使用してルート証明書または中間証明書以外の証明書を配信することは、Microsoft ではサポートされていません。 Intune ポータルで信頼された証明書プロファイルを選択する場合は、ルート証明書または中間証明書と見なされない証明書のインポートがブロックされることがあります。 このプロファイルの種類を使用して、ルート証明書でも中間証明書でもない証明書をインポートして展開できたとしても、iOS や Android など、異なるプラットフォーム間で予期しない結果が発生する可能性があります。

### <a name="to-create-a-trusted-certificate-profile"></a>信頼された証明書プロファイルを作成するには

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動します。

   ![Intune に移動して信頼済み証明書用に新しいプロファイルを作成する](./media/certificates-configure/certificates-configure-profile-new.png)

3. 次のプロパティを入力します。
   - **[プラットフォーム]** :このプロファイルを受信するデバイスのプラットフォームを選択します。
   - **[プロファイル]** : **[信頼された証明書]** を選択します。
  
4. **[作成]** を選択します。

5. **[Basics]\(基本\)** で次のプロパティを入力します。
   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「*会社全体の信頼済み証明書プロファイル*」は適切なプロファイル名です。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** で、以前にエクスポートした信頼されたルート CA 証明書の .cer ファイルを指定します。 

   Windows 8.1 および Windows 10 デバイスの場合のみ、信頼された証明書の**保存先ストア**を以下から選択します。

   - **コンピューター証明書ストア - ルート**
   - **コンピューター証明書ストア - 中間**
   - **ユーザー証明書ストア - 中間**

   ![プロファイルを作成し、信頼済み証明書をアップロードする](./media/certificates-configure/certificates-configure-profile-fill.png)

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

   **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. (*Windows 10 のみに適用*) **[適用性ルール]** で、適用性ルールを指定してこのプロファイルの割り当てを調整します。 デバイスの OS エディションまたはバージョンに基づいて、プロファイルを割り当てるかどうかを選択できます。

  詳細については、「*Microsoft Intune でのデバイス プロファイルの作成*」の「[適用性ルール](../configuration/device-profile-create.md#applicability-rules)」を参照してください。

12. **[確認と作成]** で、設定を確認します。 [作成] を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="additional-resources"></a>その他のリソース

- [デバイス プロファイルを割り当てる](../configuration/device-profile-assign.md)  
- [S/MIME を使用して電子メールに署名し、暗号化する](certificates-s-mime-encryption-sign.md)  
- [サード パーティの証明機関を使用する](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>次のステップ

使用する各プラットフォーム用に SCEP、PKCS、または PKCS のインポートされた証明書プロファイルを作成します。 続行するには、次の記事をご覧ください。

- [Intune を使用して SCEP 証明書をサポートするようにインフラストラクチャを構成する](certificates-scep-configure.md)  
- [Intune で PKCS 証明書を構成して管理する](certficates-pfx-configure.md)  
- [PKCS のインポートされた証明書プロファイルを作成する](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
