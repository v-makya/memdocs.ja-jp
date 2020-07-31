---
title: Microsoft Intune で Android Enterprise デバイス用の VPN またはアプリごとの VPN を構成する | Microsoft Docs
titleSuffix: Microsoft Intune
description: Microsoft Intune でアプリ構成ポリシーを使用して、Android Enterprise デバイス用の VPN プロファイルまたはアプリごとの VPN プロファイルを追加または作成します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262899"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>Microsoft Intune で Android Enterprise デバイスに対して VPN ポリシーまたはアプリごとの VPN ポリシーを使用する

仮想プライベート ネットワーク (VPN) を使用すると、ユーザーが自宅、ホテル、カフェなどから組織のリソースにリモートでアクセスできます。 Microsoft Intune では、アプリ構成ポリシーを使用して、Android Enterprise デバイスで VPN クライアント アプリを構成することができます。 次に、このポリシーを、その VPN 構成と共に組織内のデバイスに展開します。

また、特定のアプリによって使用される VPN ポリシーを作成することもできます。 この機能は、アプリごとの VPN と呼ばれます。 アプリがアクティブであれば、VPN に接続し、VPN 経由でリソースにアクセスできます。 アプリがアクティブでない場合、VPN は使用されません。

この機能は、以下に適用されます。

- Android エンタープライズ

VPN クライアント アプリのアプリ構成ポリシーを作成するには、2 つの方法があります。

- 構成デザイナー
- JSON データ

この記事では、両方のオプションを使用してアプリごとの VPN および VPN アプリ構成ポリシーを作成する方法について説明します。

> [!NOTE]
> VPN クライアントの構成パラメーターの多くは似ています。 ただし、各アプリには一意のキーとオプションがあります。 不明な点がある場合は、ご自身の VPN ベンダーにお問い合わせください。

## <a name="before-you-begin"></a>始める前に

- Android では、アプリが開いたときに VPN クライアント接続が自動的にトリガーされることはありません。 VPN 接続は手動で開始する必要があります。 または、[Always On VPN](../configuration/vpn-settings-android-enterprise.md) を使用して接続を開始することもできます。

- 次の VPN クライアントでは、Intune アプリ構成ポリシーがサポートされています。

  - Cisco AnyConnect
  - Citrix SSO
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - SonicWall Mobile Connect

- Intune で VPN ポリシーを作成する場合は、さまざまなキーを選択して構成を行います。 これらのキー名は、さまざまな VPN クライアント アプリによって異なります。 そのため、お客様の環境のキー名は、この記事の例とは異なる場合があります。

- 構成デザイナーと JSON データでは、証明書ベースの認証を正常に使用できます。 VPN 認証にクライアント証明書が必要な場合は、VPN ポリシーを作成する前に証明書プロファイルを作成します。 VPN アプリ構成ポリシーでは、証明書プロファイルの値が使用されます。

  Android Enterprise 仕事用プロファイル デバイスでは、SCEP および PKCS 証明書がサポートされています。 Android Enterprise のフル マネージド、専用、会社所有の仕事用プロファイル デバイスでは、SCEP 証明書のみがサポートされています。 詳細については、「[Microsoft Intune で認証に証明書を使用する](../protect/certificates-configure.md)」をご覧ください。

## <a name="per-app-vpn-overview"></a>アプリごとの VPN の概要

アプリごとの VPN を作成してテストする場合、その基本的なフローには次の手順が含まれます。

1. VPN クライアント アプリケーションを選択します。 「[始める前に](#before-you-begin)」(この記事内) に、サポートされているアプリの一覧が記載されています。
2. VPN 接続を使用するアプリのアプリケーション パッケージ ID を取得します。 「[アプリ パッケージ ID の取得](#get-the-app-package-id)」(この記事内) にその方法が記載されています。
3. 証明書を使用して VPN 接続を認証する場合は、VPN ポリシーを展開する前に証明書プロファイルを作成して展開します。 証明書プロファイルが正常に展開されることを確認します。 詳細については、「[Microsoft Intune で認証に証明書を使用する](../protect/certificates-configure.md)」をご覧ください。
4. Intune に [VPN クライアント アプリケーション](apps-add-android-for-work.md)を追加し、ユーザーとデバイスにアプリを展開します。
5. VPN アプリ構成ポリシーを作成します。 ポリシーでアプリ パッケージ ID と証明書情報を使用します。
6. 新しい VPN ポリシーを展開します。
7. VPN クライアント アプリが VPN サーバーと正常に接続されていることを確認します。
8. アプリがアクティブになったら、アプリからのトラフィックが正常に VPN を通過していることを確認します。

## <a name="get-the-app-package-id"></a>アプリ パッケージ ID の取得

VPN を使用する各アプリケーションのパッケージ ID を取得します。 一般公開されているアプリケーションの場合は、Google Play ストアでアプリ パッケージ ID を取得できます。 各アプリケーションについて表示される URL にパッケージ ID が含まれています。

次の例の場合、Microsoft Edge ブラウザー アプリのパッケージ ID は `com.microsoft.emmx` です。 このパッケージ ID は URL に含まれています。

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="Google Play ストアの URL からアプリ パッケージ ID を取得します。":::

基幹業務 (LOB) アプリの場合は、ベンダーまたはアプリケーション開発者からパッケージ ID を取得します。

## <a name="certificates"></a>証明書

この記事では、VPN 接続で証明書ベースの認証を使用することを前提としています。 また、クライアントの正常な認証に必要なチェーン内のすべての証明書を、お客様が正常に展開していることも前提としています。 通常、この証明書チェーンには、クライアント証明書、中間証明書、およびルート証明書が含まれます。

証明書の詳細については、「[Microsoft Intune で認証に証明書を使用する](../protect/certificates-configure.md)」をご覧ください。

クライアント認証の証明書プロファイルを展開すると、証明書プロファイルに証明書トークンが作成されます。 このトークンは、VPN アプリ構成ポリシーを作成するために使用されます。

アプリ構成ポリシーの作成に慣れていない場合は、「[マネージド Android Enterprise デバイス用にアプリ構成ポリシーを追加する](app-configuration-policies-use-android.md)」をご覧ください。

## <a name="use-the-configuration-designer"></a>構成デザイナーを使用する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド デバイス]** の順に選択します。
3. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 適切なポリシー名の例:「**アプリ構成ポリシー:Android Enterprise 仕事用プロファイル デバイス用の Cisco AnyConnect VPN ポリシー**」。
    - **説明**:ポリシーの説明を入力します。 この設定は省略可能ですが、推奨されます。
    - **[プラットフォーム]** : **[Android エンタープライズ]** を選択します。
    - **[プロファイルの種類]** :次のようなオプションがあります。
      - **[すべてのプロファイルの種類]** :このオプションでは、ユーザー名とパスワードの認証がサポートされます。 証明書ベースの認証を使用する場合は、このオプションを使用しないでください。
      - **[フル マネージド、専用、会社所有の仕事用プロファイルのみ]** :このオプションでは、証明書ベースの認証と、ユーザー名とパスワードの認証がサポートされます。
      - **[仕事用プロファイルのみ]** :このオプションでは、証明書ベースの認証と、ユーザー名とパスワードの認証がサポートされます。
    - **対象アプリ**:前に追加した VPN クライアント アプリを選択します。 次の例では、Cisco AnyConnect VPN クライアント アプリが使用されています。

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="Microsoft Intune でアプリ構成ポリシーを作成し、VPN またはアプリごとの VPN を構成する":::

4. **[次へ]** を選択します。
5. **[設定]** で、次のプロパティを入力します。

    - **[構成設定の形式]** : **[構成デザイナーを使用する]** を選択します。

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="構成デザイナーを使用して Microsoft Intune でアプリ構成 VPN ポリシーを作成する - 例。":::

    - **[追加]** :構成キーの一覧が表示されます。 構成に必要なすべての構成キーを選択し、 **[OK]** を選択します。

      次の例では、証明書ベースの認証やアプリごとの VPN など、AnyConnect VPN 用の最小限のリストが選択されています。
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="構成デザイナーを使用して Microsoft Intune で VPN アプリ構成ポリシーに構成キーを追加する - 例。":::

    - **構成値**:選択した構成キーの値を入力します。 キー名は使用している VPN クライアント アプリによって異なることを忘れないでください。 この例で選択したキーの場合、次のようにします。

      - **[Per App VPN Allowed Apps]\(アプリごとの VPN が許可されるアプリ\)** :先ほど収集したアプリケーション パッケージ ID を入力します。 次に例を示します。

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="構成デザイナーを使用して Microsoft Intune で VPN アプリ構成ポリシーに許可されるアプリ パッケージ ID を入力する - 例。":::

      - **[KeyChain Certificate Alias]\(キーチェーン証明書のエイリアス\)** (省略可能): **[値の種類]** を **[文字列]** から **[証明書]** に変更します。 VPN 認証に使用するクライアント証明書プロファイルを選択します。 次に例を示します。

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="構成デザイナーを使用して Microsoft Intune で VPN アプリ構成ポリシーのキーチェーン クライアント証明書のエイリアスを変更する - 例。":::

      - **Protocol**:VPN の **[SSL]** または **[IPsec]** トンネル プロトコルを選択します。
      - **[接続名]** :VPN 接続のユーザー フレンドリ名を入力します。 ユーザーのデバイスには、この接続名が表示されます。 たとえば、「`ContosoVPN`」と入力します。
      - **[ホスト]** : ヘッドエンド ルーターのホスト名 URL を入力します。 たとえば、「`vpn.contoso.com`」と入力します。

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="構成デザイナーを使用した Microsoft Intune での VPN アプリ構成ポリシーのプロトコル、接続名、ホスト名の例":::

6. **[次へ]** を選択します。
7. **[割り当て]** で、VPN アプリ構成ポリシーを割り当てるグループを選択します。

    **[次へ]** を選択します。

8. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、ポリシーがグループに展開されます。 ポリシーは、アプリ構成ポリシーの一覧にも表示されます。

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="Microsoft Intune で構成デザイナーフローを使用してアプリ構成ポリシーを確認する例。":::

## <a name="use-json"></a>JSON を使用する

**構成デザイナー**で使用されるすべての必須 VPN 設定が満たせない、またはわからない場合は、このオプションを使用します。 ヘルプが必要な場合は、ご自身の VPN ベンダーにお問い合わせください。

### <a name="get-the-certificate-token"></a>証明書トークンを取得する

この手順では、一時ポリシーを作成します。 このポリシーは保存されません。 証明書トークンをコピーすることが目的です。 JSON を使って VPN ポリシーを作成する際に、このトークンを使用します (次のセクション)。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド デバイス]** を選択します。
2. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:任意の名前を入力します。 このポリシーは一時的なものであり、保存されません。
    - **[プラットフォーム]** : **[Android エンタープライズ]** を選択します。
    - **[プロファイルの種類]** : **[仕事用プロファイルのみ]** を選択します。
    - **対象アプリ**:前に追加した VPN クライアント アプリを選択します。

3. **[次へ]** を選択します。
4. **[設定]** で、次のプロパティを入力します。

    - **[構成設定の形式]** : **[構成デザイナーを使用する]** を選択します。
    - **[追加]** :構成キーの一覧が表示されます。 **[値の種類]** が **[文字列]** である任意のキーを選択します。 **[OK]** を選択します。

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="構成デザイナーを使用して、Microsoft Intune VPN アプリ構成ポリシーで値の種類が文字列であるキーを選択する":::

5. **[値の種類]** を **[文字列]** から **[証明書]** に変更します。 この手順により、VPN を認証する正しいクライアント証明書プロファイルを選択できます。

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="Microsoft Intune で VPN アプリ構成ポリシーの接続名を変更する例":::

6. すぐに **[値の種類]** を **[文字列]** に戻します。 **[構成値]** がトークン `{{cert:GUID}}` に変更されます。

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="Microsoft Intune の VPN アプリ構成ポリシーで構成値に証明書トークンが表示される":::

7. この証明書トークンをコピーし、テキスト エディターなどの別のファイルに貼り付けます。

8. このポリシーを破棄します。 保存しないでください。 唯一の目的は、証明書トークンをコピーして貼り付けることです。

### <a name="create-the-vpn-policy-using-json"></a>JSON を使用して VPN ポリシーを作成する

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド デバイス]** を選択します。

2. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 適切なポリシー名の例:「**アプリ構成ポリシー:会社全体の Android Enterprise 仕事用プロファイル デバイス用の JSON Cisco AnyConnect VPN ポリシー**」。
    - **説明**:ポリシーの説明を入力します。 この設定は省略可能ですが、推奨されます。
    - **[プラットフォーム]** : **[Android エンタープライズ]** を選択します。
    - **[プロファイルの種類]** :次のようなオプションがあります。
      - **[すべてのプロファイルの種類]** :このオプションでは、ユーザー名とパスワードの認証がサポートされます。 証明書ベースの認証を使用する場合は、このオプションを使用しないでください。
      - **[フル マネージド、専用、会社所有の仕事用プロファイルのみ]** :このオプションでは、証明書ベースの認証と、ユーザー名とパスワードの認証がサポートされます。
      - **[仕事用プロファイルのみ]** :このオプションでは、証明書ベースの認証と、ユーザー名とパスワードの認証がサポートされます。
    - **対象アプリ**:前に追加した VPN クライアント アプリを選択します。 

3. **[次へ]** を選択します。
4. **[設定]** で、次のプロパティを入力します。

    - **[構成設定の形式]** : **[JSON データの入力]** を選択します。 JSON は直接編集できます。
    - **[JSON テンプレートをダウンロードします]** :このオプションを使用すると、テンプレートをダウンロードして任意の外部エディターで更新できます。 **スマート クォート**を使用するテキスト エディターの場合は注意してください。無効な JSON が作成される可能性があるためです。

    構成に必要な値を入力した後、`"STRING_VALUE"` または `STRING_VALUE` を持つすべての設定を削除します。

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="JSON フローの使用例 - JSON の編集。":::

5. **[次へ]** を選択します。
6. **[割り当て]** で、VPN アプリ構成ポリシーを割り当てるグループを選択します。

    **[次へ]** を選択します。

7. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、ポリシーがグループに展開されます。 ポリシーは、アプリ構成ポリシーの一覧にも表示されます。

#### <a name="json-example-for-f5-access-vpn"></a>F5 Access VPN 用の JSON の例

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="additional-information"></a>追加情報

- [マネージド Android Enterprise デバイス用にアプリ構成ポリシーを追加する](app-configuration-policies-use-android.md)
- [Intune で VPN を構成するための Android Enterprise デバイスの設定](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>次のステップ

- [Intune で VPN サーバーに接続するための VPN プロファイルを作成する](../configuration/vpn-settings-configure.md)
