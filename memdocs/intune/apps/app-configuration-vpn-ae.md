---
title: Android Enterprise デバイス用の VPN の構成
titleSuffix: Microsoft Intune
description: アプリ保護ポリシーを使用して、Android Enterprise デバイス用の VPN を構成します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
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
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347419"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>Android Enterprise デバイス用の VPN の構成

このトピックでは、Android Enterprise デバイス上の VPN クライアントと共に展開できるアプリ構成ポリシーを作成する方法について説明します。 この構成では、企業のリソースにアクセスできるように、選択したアプリケーションのネットワーク トラフィックを許可します。

> [!NOTE]
> Android プラットフォームでは現在、選択したアプリケーションのいずれかが開かれた際の VPN クライアント接続の自動トリガーはサポートされていません。 VPN 接続は最初に手動で開始される必要があります。または、[常時接続 VPN](../configuration/vpn-settings-android-enterprise.md) を使用できます。

構成ポリシーを作成し、VPN アクセスを正常に実現するための前提条件には、選択した VPN クライアントにマネージド アプリケーション構成プロファイルのサポート機能があることが含まれています。 現在、Intune アプリ構成ポリシーがサポートされている VPN クライアントには以下のものがあります。
- Cisco AnyConnect
- Citrix SSO
- F5 Access
- Palo Alto Global Connect
- Pulse Secure
- SonicWall Mobile Connect

VPN エンドポイントへの認証アクセスの方法でクライアント証明書を使用する必要がある場合は、アプリ構成ポリシーに必要な値を設定しやすいように、証明書プロファイルを前もって作成しておく必要があります。

> [!NOTE]
> Android Enterprise の作業プロファイルのシナリオでは SCEP と PKCS の両方の証明書がサポートされていますが、Android Enterprise のデバイス所有者のシナリオでは、現在サポートされているのは SCEP 証明書のみです。 

アプリごとの VPN プロファイルを作成してテストするための基本的なフローは次のとおりです。
1.  ご自分のインフラストラクチャに適した VPN クライアント アプリケーションを選択します。
2.  VPN 接続で使用したい生産性向上アプリのアプリケーション パッケージ ID を特定します。
3.  VPN 接続の認証要件を満たすために必要な証明書プロファイルを展開します。 正常に展開できたことを確認してください。
4.  VPN クライアント アプリケーションを展開します。
5.  それまでの手順で収集した情報を使用して、アプリ構成ベースの VPN プロファイルを準備します。
6.  新しく作成した VPN プロファイルを展開します。
7.  VPN クライアント アプリが VPN サーバー インフラストラクチャに正常に接続できることを確認します。
8.  選択した生産性向上アプリがアクティブなときに、そのトラフィックが VPN に正常に転送されることを確認します。

## <a name="get-the-app-package-id"></a>アプリ パッケージ ID の取得

VPN アクセス権を付与したい各アプリケーションのパッケージ ID を特定します。 一般提供されているアプリケーションの場合は、Google Play ストアで各アプリケーションのパッケージ ID を取得することを検討してください。 各アプリケーションについて表示される URL にパッケージ ID が含まれています。 たとえば、Microsoft Edge ブラウザーの Android バージョンのパッケージ ID は `com.microsoft.emmx` です。 パッケージ ID は URL の一部として含まれています。

![アプリ パッケージ ID の確認の例。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

基幹業務 (LOB) アプリの場合は、ベンダーまたはアプリケーション開発チームに問い合わせて、該当するパッケージ ID を提供するよう依頼してください。

## <a name="certificates"></a>証明書

このトピックでは、お客様の VPN 接続で証明書ベースの認証を使用すること、クライアント認証を成功させるために必要なチェーン内の証明書をすべて正常に展開済みであることを前提としています。 これは通常、クライアント証明書、中間証明書、およびルート証明書になります。
Android Enterprise の証明書を展開する方法の詳細については、最初にトピック「[Microsoft Intune で認証に証明書を使用する](../protect/certificates-configure.md)」を参照してください。

ご自分のクライアント認証証明書プロファイルを展開したら、そのプロファイルの詳細を使用して VPN アプリ構成ポリシーを作成する必要があります。
アプリ構成プロファイルの作成に慣れていない場合は、トピック「[マネージド Android Enterprise デバイス用にアプリ構成ポリシーを追加する](../apps/app-configuration-policies-use-android.md)」を参照してください。
 

## <a name="build-the-vpn-profile"></a>VPN プロファイルの作成

VPN アプリのアプリ構成ポリシーを作成するには、2 つの方法があります。 **構成デザイナー**または **JSON データ**のオプションを使用できます。 **構成デザイナー**の方法で必要な VPN 設定をすべて利用できない場合は、**JSON データ**のオプションが必要です。 JSON のオプションが必要であると判断した場合は、サポートを得るために VPN ベンダーに問い合わせてください。 このトピックでは、両方の方法の例を紹介します。 **JSON データ**と**構成デザイナー**のどちらの方法でも、証明書ベースの認証を正常に実装できます。 **JSON データ**の方法を使用する場合は、最初に**構成デザイナー**を使用して必要なプロファイル値を抽出できます。

> [!NOTE]
> VPN クライアントの構成パラメーターの多くは似ていますが、アプリごとに一意のキーとオプションがあります。 疑問が生じた場合は、VPN ベンダーにお問い合わせください。 

## <a name="use-the-configuration-designer-flow"></a>構成デザイナー フローの使用

1.  最初に、**マネージド デバイス**の新しいアプリ構成ポリシーを追加します。
2.  適切な名前を入力します。
3.  プラットフォームとして **[Android エンタープライズ]** を選択します。
4.  証明書ベースの認証が必要な場合、プロファイルの種類として **[仕事用プロファイルのみ]** または **[デバイスの所有者のみ]** を選択します。 **[Work Owner and Device Owner Profile]\(作業所有者とデバイス所有者のプロファイル\)** は、証明書ベースの認証には対応していません。
5.  ターゲットのアプリとして、展開済みの VPN クライアントを選択します。この例では、前に展開した Cisco AnyConnect VPN クライアントを使用します

  ![アプリ構成ポリシーの作成の例 - 基本。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. 次のページで、構成設定のドロップ ダウンを使用して、 **[構成デザイナーを使用する]** オプションを選択します。

  ![構成デザイナー フローの使用例 - 設定。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. **[追加]** をクリックして、構成キーのリストを表示します。
8.  自分が選択した構成に必要な構成キーをすべて選択します。 この例では、証明書ベースの認証やアプリごとの VPN を含む最小限の設定リストを AnyConnect VPN に使用します。
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. **[接続名]** 、 **[ホスト]** 、 **[プロトコル]** の各キーに適切な値を入力します。

  ![構成デザイナー フローの使用例 - 構成キーの選択。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > これらのキーの名前は、ポリシーを作成する対象の VPN クライアント アプリケーションによって異なります。

10. 先ほど収集したアプリケーション パッケージ ID を **[Per App VPN Allowed Apps]\(アプリごとの VPN が許可されるアプリ\)** キーに入力します。

  ![構成デザイナー フローの使用例 - アプリ パッケージ ID。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. **[KeyChain Certificate Alias]\(キーチェーン証明書のエイリアス\)** キー (省略可能) で、 **[値の種類]** を **[文字列]** から **[証明書]** に切り替えます。これで、VPN 認証に使用される適切なクライアント証明書プロファイルを選択できるようになります。

  ![構成デザイナー フローの使用例 - キーチェーン証明書のエイリアスの更新](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. 次のページで、適切なスコープ タグを選択します。
13. 次のページで、アプリ構成ポリシーの展開先にする適切なグループを入力します。
14. **[作成]** を選択して、ポリシーの作成と展開を完了します。

  ![構成デザイナー フローの使用例 - 確認。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>JSON フローの使用

一時プロファイルを作成します。
1.  最初に、**マネージド デバイス**の新しいアプリ構成ポリシーを追加します。
2.  適切な名前を入力します (このプロファイルは保存されないため、その使用は一時的です)。
3.  プラットフォームとして **[Android エンタープライズ]** を選択します。
4.  ターゲットのアプリとして、自分が展開した VPN クライアントを選択します。
5.  証明書ベースの認証が必要な場合、プロファイルの種類として **[仕事用プロファイルのみ]** または **[デバイスの所有者のみ]** を選択します。 **[Work Owner and Device Owner Profile]\(作業所有者とデバイス所有者のプロファイル\)** は、証明書ベースの認証には対応していません。

  ![JSON フローの使用例 - 基本。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  次のページで、 **[構成設定]** ドロップ ダウンを使用して、 **[構成デザイナーを使用する]** オプションを選択します。

  ![JSON フローの使用例 - 構成設定の形式](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  **[追加]** をクリックして、構成キーのリストを表示します。
8.  **[値の種類]** が **[文字列]** であるいずれかのキーを選択し、 **[OK]** をクリックします。

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  次に、 **[値の種類]** を **[文字列]** から **[証明書]** に変更します。 これにより、VPN 認証に使用される適切なクライアント証明書プロファイルを選択できるようになります。

  ![JSON フローの使用例 - 接続名。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. すぐに **[値の種類]** を **[文字列]** に戻します。 **[構成値]** が `{{cert:GUID}}` という形式のトークンに変更されることに注目してください。
11. 証明書のトークン表現を選択し、別の場所 (テキスト エディターなど) にコピーします。

  ![JSON フローの使用例 - 構成値](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. 作成中のプロファイルを破棄します – ここまでの手順は、証明書トークンを特定することだけを目的としていました。

### <a name="create-the-vpn-profile"></a>VPN プロファイルを作成する

1.  最初に、**マネージド デバイス**の新しいアプリ構成プロファイルを追加します。
2.  適切な名前を入力します。
3.  プラットフォームとして **[Android エンタープライズ]** を選択します。
4.  ターゲットのアプリとして、自分が展開した VPN クライアントを選択します。
5.  証明書ベースの認証が必要な場合、プロファイルの種類として **[仕事用プロファイルのみ]** または **[デバイスの所有者のみ]** を選択します。 **[Work Owner and Device Owner Profile]\(作業所有者とデバイス所有者のプロファイル\)** は、証明書ベースの認証には対応していません。
6.  **[構成設定]** ドロップ ダウンを使用して、 **[JSON データを入力]** オプションを選択します。
7.  JSON は直接編集できるほか、必要に応じて **[JSON テンプレートをダウンロードします]** ボタンを使用してテンプレートをダウンロードし、任意の外部エディターで変更することもできます。 テキスト エディターに**スマート クォート**を使用するオプションがある場合は、取り込み時に JSON が無効なものに変更される可能性があるため、注意してください。

  ![JSON フローの使用例 - JSON の編集。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  どちらの方法を使用する場合も、目的の構成に必要な値を設定したら、JSON 内全体の "STRING_VALUE" または STRING_VALUE の値がある残りの設定をすべて削除する必要があります。

#### <a name="example-json-for-f5-access-vpn"></a>F5 Access VPN 用の JSON の例

F5 Access VPN 用の JSON データの例を次に示します。

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

## <a name="summary"></a>[概要]

Android Enterprise 登録デバイスにアプリ構成ポリシーを使用すると、プラットフォームでそれが直接サポートされていなくても、アプリごとの VPN 動作を利用できます。 

## <a name="additional-information"></a>追加情報

関連情報については、次のトピックを参照してください。
- [マネージド Android Enterprise デバイス用にアプリ構成ポリシーを追加する](../apps/app-configuration-policies-use-android.md)
- [Intune で VPN を構成するための Android Enterprise デバイスの設定](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>次のステップ

- [Intune で VPN サーバーに接続するための VPN プロファイルを作成する](../configuration/vpn-settings-configure.md)
