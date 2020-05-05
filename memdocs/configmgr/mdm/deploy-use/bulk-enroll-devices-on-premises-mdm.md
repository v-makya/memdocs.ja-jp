---
title: デバイスを一括で登録する方法
titleSuffix: Configuration Manager
description: Configuration Manager のオンプレミスモバイルデバイス管理 (MDM) を使用して、自動化された方法でデバイスを一括登録します。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfe2d395187f8af86e2d09156a45f7398a5bc670
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724616"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Configuration Manager でオンプレミス MDM を使用してデバイスを一括登録する方法

*適用対象:Configuration Manager (Current Branch)*

オンプレミスモバイルデバイス管理 (MDM) Configuration Manager での一括登録は、デバイスを登録するための自動化された方法です。 もう1つの方法はユーザー登録で、ユーザーはデバイスを登録するために資格情報を入力する必要があります。 一括登録では、登録パッケージを使用して、登録時にデバイスを認証します。 パッケージは、登録をサポートするための証明書と Wi-fi プロファイルを含むことができる、ppkg ファイルです。

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> 証明書プロファイルの作成

信頼されたルート証明書をデバイスに自動的にインストールするには、証明書プロファイルを含めます。 このルート証明書は、オンプレミス MDM に必要なデバイスとサイトシステムの役割の間の信頼された通信に必要です。

オンプレミス MDM 用にサイトを準備するときに、信頼されたルート証明書をエクスポートします。 この証明書は、登録パッケージの証明書プロファイルで使用します。 信頼されたルート証明書を取得する方法の詳細については、「[エクスポートする信頼されたルート証明書](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)」を参照してください。

エクスポートした証明書を使用して、証明書プロファイルを作成します。 詳細については、「[証明書プロファイルを作成する方法](../../protect/deploy-use/create-certificate-profiles.md)」を参照してください。

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a> Wi-Fi プロファイルの作成

一括登録パッケージのもう1つのコンポーネントは、Wi-fi プロファイルです。 このプロファイルにより、デバイスが登録をサポートするためのネットワーク接続を確立できるようになります。

Configuration Manager で Wi-fi プロファイルを作成する方法の詳細については、「 [wi-fi プロファイルを作成する方法](../../protect/deploy-use/create-wifi-profiles.md)」を参照してください。

### <a name="wi-fi-profile-limitations"></a>Wi-fi プロファイルの制限事項

オンプレミス MDM 一括登録用の Wi-fi プロファイルを作成する場合は、次の制限事項を確認してください。

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>オンプレミス MDM の wi-fi セキュリティ構成

Configuration Manager の現在のブランチは、オンプレミス MDM に対して次の Wi-fi セキュリティ構成のみをサポートしています。

- セキュリティの種類: **[WPA2 Enterprise]** または **[WPA2 Personal]**

- 暗号化の種類: **[AES]** または **[TKIP]**

- EAP の種類: **[スマート カードまたは他の証明書]** または **[PEAP]**

#### <a name="proxy-server"></a>プロキシ サーバー

Configuration Manager には、Wi-fi プロファイルのプロキシサーバー情報の設定がありますが、デバイスを登録するときにプロキシは構成されません。 一括登録されたデバイスでプロキシサーバーを設定する必要がある場合は、次のようにします。

- デバイスを登録した後で、構成項目を使用して設定を展開します。

- Windows イメージと構成デザイナー (ICD) を使用して2番目のパッケージを作成し、一括登録パッケージと共に展開します。

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> 登録プロファイルの作成

登録プロファイルを使用すると、デバイスの登録に必要な設定を指定できます。 これらの設定には、[証明書プロファイル](#bkmk_createCert)と[wi-fi プロファイル](#CreateWifi)が含まれます。

1. Configuration Manager コンソールで、[**資産とコンプライアンス**] ワークスペースにアクセスし、[**すべての企業所有のデバイス**]、[ **Windows**] の順に展開して、[**登録プロファイル**] ノードを選択します。

1. リボンで、[**登録プロファイルの作成**] を選択します。

1. 登録プロファイルの作成ウィザードの **[全般**] ページで、次の情報を指定します。

    - **名前**: プロファイルを識別する一意の名前

    - **説明**: オプションのフィールドで、プロファイルの詳細を説明します。

    - **管理機関**: オン**プレミス**のみを選択

1. [**サイトの割り当て**] ページで、デバイス管理ポイントが含まれている**管理サイトコード**を選択します。

1. [**登録プロキシポイントの選択**] ページで、[**イントラネットのみ**] を選択し、1つまたは複数の登録プロキシポイントを選択します。 デバイスはこれらのサーバーを使用して登録プロセスを開始します。

1. [**信頼されたルート証明書の選択**] ページで、信頼されたルート証明書を含む証明書プロファイルを選択します。

1. [ **Wi-fi プロファイル**] ページで、デバイスが接続するために必要なネットワーク設定が含まれている wi-fi プロファイルを選択します。

    > [!TIP]
    > 登録パッケージに Wi-fi プロファイルを使用していない場合は、この手順をスキップしてください。

1. ウィザードを完了します。

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a>登録パッケージを作成する

登録パッケージ (ppkg) は、オンプレミス MDM のデバイスを一括登録するために使用するファイルです。 このファイルを Configuration Manager で作成します。 Windows ICD で同様の種類のパッケージを作成できますが、オンプレミス MDM のデバイスの登録に使用できるのは Configuration Manager で作成したパッケージだけです。 Windows ICD で作成したパッケージは、登録に必要なユーザープリンシパル名 (UPN) のみを提供できます。実際の登録プロセスを開始することはできません。

登録パッケージを作成するプロセスには、Windows 10 用 Windows アセスメント & デプロイメント キット (ADK) が必要です。 Configuration Manager コンソールを実行しているコンピューターで、最新バージョンの Windows ADK をインストールします。 **イメージングおよび構成デザイナー (ICD)** 機能と依存関係を選択します。 (このバージョンは、Configuration Manager サイトによる OS の展開に使用されるバージョンと一致する必要はありません)。詳細については、「windows [ADK For windows 10 のダウンロード](https://docs.microsoft.com/windows-hardware/get-started/adk-install)」を参照してください。

1. Configuration Manager コンソールで、[**資産とコンプライアンス**] ワークスペースにアクセスし、[**すべての企業所有のデバイス**]、[ **Windows**] の順に展開して、[**登録プロファイル**] ノードを選択します。

1. 既存の登録プロファイルを選択します。 リボンで、[**エクスポート**] を選択します。

1. [登録パッケージのエクスポート] ウィンドウで、次の情報を指定します。

    - **有効期間**(日): 既定では、登録パッケージの有効期限が2週間 (14 日) に設定されて Configuration Manager ます。 有効期限が切れた後、デバイスの登録にパッケージを使用することはできません。 1 ~ 30 の整数を入力してください。

    - **パッケージファイル**: ローカルまたはネットワークのファイルパスと、ppkg ファイルの名前を指定します。

    - [**パッケージの暗号化**]: このオプションを有効にすると、パッケージをパスワードで保護できます。 パッケージをエクスポートすると、生成されたパスワードが Configuration Manager に表示されます。 パスワードをコピーし、安全な場所に保存します。 エクスポートされた登録パッケージは、パスワードなしでは使用できません。

        > [!IMPORTANT]
        > Configuration Manager はパスワードを保存しないので、カスタマイズまたは変更することはできません。 パスワードを表示するウィンドウを閉じると、パスワードを取得する方法はありません。

1. **[エクスポート]** を選択します。 Configuration Manager は、Windows ADK を使用して登録パッケージを作成します。

Configuration Manager は、有効な登録パッケージを追跡します。 コンソールで、[**登録プロファイル**] ノードを展開し、[エクスポートされた**パッケージ**] を選択します。

> [!TIP]
> Configuration Manager コンソールから登録パッケージを削除した場合、デバイスを登録するために使用することはできません。 この方法は、他のユーザーが一括登録に使用しない登録パッケージを管理する場合に使用します。

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a>デバイスの一括登録

パッケージを使用して、デバイスの既定のエクスペリエンス (OOBE) プロセスの前または後にデバイスを登録できます。 登録パッケージは、相手先ブランド供給 (OEM) のプロビジョニングパッケージの一部として含めることもできます。

一括登録のためにパッケージを使用するには、デバイスに物理的に配信する必要があります。 ニーズに応じてさまざまな方法があります。次に例を示します。

- ファイルシステムからコピーする

- 電子メールに添付する

- 近距離無線通信 (NFC) 接続を経由したコピー

- メモリカードからのコピー

- バーコードをスキャン

- テザリングされたデバイスからのコピー

- OEM プロビジョニングパッケージに含める

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>一括登録パッケージを使用してデバイスを登録する

1. デバイスで、ppkg ファイルを開きます。 必要に応じて、管理者として実行します。

1. パッケージが信頼できる発行元のものかどうかを確認するメッセージが表示されたら、[**はい]** を選択します。

登録プロセスが開始されます。

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a>登録の確認

### <a name="verify-bulk-enrollment-on-the-device"></a>デバイスでの一括登録を確認する

1. デバイスで、[**設定**] を開きます。

1. [**アカウント**] を選択し、[**職場または学校にアクセス**する] を選択します。 登録が成功すると、[会社の**アプリ**] の下にアカウントが表示されます。

1. アカウントを選択し、[**同期**] を選択します。この操作により、Configuration Manager で管理が開始されます。

### <a name="verify-enrollment-in-the-console"></a>コンソールで登録を確認する

Configuration Manager コンソールを使用して、デバイスが正常に登録されていることを確認します。 Configuration Manager コンソールで、**[資産とコンプライアンス]** ワークスペースに移動し、**[デバイス]** を選択します。 デバイスの一覧で、登録されているデバイスを参照または検索します。
