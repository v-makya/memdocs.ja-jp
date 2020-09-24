---
title: PKI 証明書で TLS/SSL を使用するようにソフトウェアの更新ポイントを構成するチュートリアル
titleSuffix: Configuration Manager
description: チュートリアル - PKI 証明書で TLS/SSL を使用するように Windows Server Update Services (WSUS) サーバーとソフトウェアの更新ポイントを構成します。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
ms.openlocfilehash: e8359077ac363d2d732b2ffa6712c9b938a2c709
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718930"
---
# <a name="tutorial-configure-a-software-update-point-to-use-tlsssl-with-a-pki-certificate"></a>チュートリアル:PKI 証明書で TLS/SSL を使用するようにソフトウェアの更新ポイントを構成する

*適用対象:Configuration Manager (Current Branch)*

TLS/SSL を使用するように Windows Server Update Services (WSUS) サーバーとそれに対応するソフトウェアの更新ポイント (SUP) を構成すると、攻撃者がクライアントをリモートで侵害して特権を昇格させる能力が低下する可能性があります。 最適なセキュリティ プロトコルが確実に導入されるように、TLS/SSL プロトコルを使用してソフトウェア更新インフラストラクチャをセキュリティで保護することを強くお勧めします。 この記事では、HTTPS を使用するように各 WSUS サーバーとソフトウェアの更新ポイントを構成するために必要な手順について説明します。 WSUS のセキュリティ保護の詳細については、WSUS のドキュメントの記事「[Secure Sockets Layer プロトコルを使用して WSUS をセキュリティで保護する](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)」を参照してください。

このチュートリアルでは、次のことについて説明します。
> [!div class="checklist"]
> * 必要に応じて PKI 証明書を取得する
> * 証明書を WSUS 管理 Web サイトにバインドする
> * SSL を要求するように WSUS Web サービスを構成する
> * SSL を使用するように WSUS アプリケーションを構成する
> * WSUS コンソール接続で SSL を使用できることを確認する
> * WSUS サーバーに対して SSL 通信を要求するようにソフトウェアの更新ポイントを構成する
> * Configuration Manager で機能を確認する

## <a name="considerations-and-limitations"></a>考慮事項と制限事項

WSUS では、TLS/SSL を使用して、クライアント コンピューターとダウンストリーム WSUS サーバーのアップストリーム WSUS サーバーに対する認証が行われます。 また、WSUS では、更新プログラムのメタデータの暗号化にも TLS/SSL が使用されます。 WSUS では、更新プログラムのコンテンツ ファイルには TLS/SSL は使用されません。 コンテンツ ファイルは署名されて、ファイルのハッシュが更新プログラムのメタデータに含められます。 クライアントによってファイルがダウンロードされてインストールされる前に、デジタル署名とハッシュの両方が確認されます。 どちらかのチェックが失敗した場合、更新プログラムはインストールされません。

TLS/SSL を使用して WSUS の展開をセキュリティで保護する場合は、次の制限事項を考慮してください。

- TLS/SSL を使用すると、サーバーのワークロードが増加します。 ネットワーク経由で送信されるすべてのメタデータを暗号化することにより、パフォーマンスがわずかに低下することを予期する必要があります。
- リモート SQL Server データベースで WSUS を使用する場合、WSUS サーバーとデータベース サーバーの間の接続は TLS/SSL によって保護されません。 データベースの接続をセキュリティで保護する必要がある場合は、次の推奨事項を考慮してください。
   - WSUS データベースを WSUS サーバーに移動する。
   - リモート データベース サーバーと WSUS サーバーをプライベート ネットワークに移動する。
   - インターネット プロトコル セキュリティ (IPsec) を展開して、ネットワーク トラフィックをセキュリティで保護する。

TLS/SSL を使用するように WSUS サーバーとそのソフトウェアの更新ポイントを構成するときは、大規模な Configuration Manager 階層の変更を段階的に行うことができます。 これらの変更を段階的に行うことを選択した場合は、階層の最下層から始めて、中央管理サイトで終わるまで、上方に移動していきます。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは、インターネット インフォメーション サービス (IIS) で使用する証明書を取得するための最も一般的な方法について説明します。 どちらの方法を組織で使用するにしても、Configuration Manager のソフトウェアの更新ポイントに対する [PKI 証明書の要件](../../core/plan-design/network/pki-certificate-requirements.md)を証明書が満たしていることを確認します。 どのような証明書でも同じですが、証明機関は、WSUS サーバーと通信するデバイスによって信頼されている必要があります。

- ソフトウェアの更新ポイントの役割がインストールされている WSUS サーバー
- TLS/SSL を有効にする前に、WSUS のメモリ制限のリサイクルと構成の無効化に関する[ベスト プラクティス](/troubleshoot/mem/configmgr/windows-server-update-services-best-practices#disable-recycling-and-configure-memory-limits)に従っていることを確認します。
- 次の 2 つのオプションのいずれか:
   - WSUS サーバーの**個人用**証明書ストアに、適切な PKI 証明書が既に存在します。
   - エンタープライズ ルート証明機関 (CA) に WSUS サーバー用の適切な PKI 証明書を要求して取得できます。
      - 既定では、WebServer 証明書テンプレートを含むほとんどの証明書テンプレートでは、ドメイン管理者に対してのみ発行されます。 ログインしているユーザーがドメイン管理者でない場合は、そのユーザー アカウントに、証明書テンプレートで**登録**アクセス許可を付与する必要があります。

## <a name="obtain-the-certificate-from-the-ca-if-needed"></a><a name="bkmk_pki"></a> 必要に応じて CA から証明書を取得する

WSUS サーバーの**個人用**証明書ストアに適切な証明書が既にある場合は、このセクションをスキップし、[証明書のバインド](#bkmk_bind)に関するセクションから始めてください。 新しい証明書をインストールするために証明書の要求を内部 CA に送信するには、このセクションの手順に従います。
 
1. WSUS サーバーから、管理コマンド プロンプトを開き、`certlm.msc` を実行します。 ローカル コンピューターの証明書を管理するには、ローカル管理者のユーザー アカウントを使用する必要があります。

   ローカル デバイス用の証明書マネージャー ツールが表示されます。

1. **[個人用]** を展開し、 **[証明書]** を右クリックします。
1. **[すべてのタスク]** を選択し、 **[新しい証明書の要求]** を選択します。
1. **[次へ]** を選択して、証明書の登録を開始します。
1. 登録する証明書の種類を選択します。 証明書の目的は **[サーバー認証]** であり、使用する Microsoft 証明書テンプレートは **[Web サーバー]** か、 **[サーバー認証]** で **[拡張キー使用法]** が指定されたカスタム テンプレートです。 証明書を登録するための追加情報の入力を求められる場合があります。 通常は、少なくとも次の情報を指定します。
   - **[共通名]:** **[サブジェクト]** タブにあり、値には WSUS サーバーの FQDN を設定します。
   - **[フレンドリ名]:** **[全般]** タブにあり、値には後で証明書を識別しやすいわかりやすい名前を設定します。
:::image type="content" source="media/certificate-properties.png" alt-text="登録の詳細情報を指定する証明書プロパティ ウィンドウ":::
1. **[登録]** を選択してから **[完了]** を選択して、登録を完了します。
1. 証明書の拇印などの詳細を確認する場合は、証明書を開きます。

> [!TIP]
> WSUS サーバーがインターネットに接続されている場合は、証明書のサブジェクトまたはサブジェクトの別名 (SAN) に外部 FQDN が必要です。

## <a name="bind-the-certificate-to-the-wsus-administration-site"></a><a name="bkmk_bind"></a> 証明書を WSUS 管理サイトにバインドする

WSUS サーバーの個人用証明書ストアに証明書が存在するようになったら、それを IIS の WSUS 管理サイトにバインドします。

1. WSUS サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを起動します。
1. **[サイト]**  >  **[WSUS の管理]** に移動します。
1. アクション メニューから、またはサイトを右クリックして、 **[バインド]** を選択します。
1. **[サイト バインド]** ウィンドウで、**https** の行を選択し、 **[編集...]** を選択します。
   - HTTP のサイト バインドを削除しないでください。 WSUS では、更新プログラムのコンテンツ ファイルに HTTP が使用されます。
1. **[SSL 証明書]** オプションで、WSUS 管理サイトにバインドする証明書を選択します。 証明書のフレンドリ名がドロップダウン メニューに表示されます。 フレンドリ名が指定されていない場合は、証明書の `IssuedTo` フィールドが表示されます。 使用する証明書がわからない場合は、 **[表示]** を選択し、拇印が取得したものと一致していることを確認します。  
   :::image type="content" source="media/edit-site-binding.png" alt-text="SSL 証明書が選択された [サイト バインドの編集] ウィンドウ":::
1. 終わったら **[OK]** を選択し、 **[閉じる]** を選択してサイト バインドを終了します。 次のステップで使用するので、インターネット インフォメーション サービス (IIS) マネージャーは開いたままにします。



## <a name="configure-the-wsus-web-services-to-require-ssl"></a><a name="bkmk_webserv"></a> SSL を要求するように WSUS Web サービスを構成する

1. WSUS サーバーの IIS マネージャーで、 **[サイト]**  >  **[WSUS の管理]** に移動します。
1. WSUS 管理サイトを展開し、WSUS の Web サービスと仮想ディレクトリの一覧を表示します。
1. 次の各 WSUS Web サービスについて:
   - ApiRemoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   次の変更を行います。

      1. **[SSL 設定]** を選択します。
      1. **[SSL が必要]** オプションを有効にします。
      1. **[クライアント証明書]** オプションが **[無視]** に設定されていることを確認します。
      1. **[適用]** を選択します。

コンテンツなどの特定の機能では HTTP を使用する必要があるため、最上位の WSUS 管理サイトでは SSL 設定を設定しないでください。

## <a name="configure-the-wsus-application-to-use-ssl"></a><a name="bkmk_wsusutil"></a> SSL を使用するように WSUS アプリケーションを構成する

SSL を必要とするように Web サービスを設定したら、WSUS アプリケーションでは、変更をサポートするための追加構成をできるように、通知を受け取る必要があります。

1. WSUS サーバーで管理者コマンド プロンプトを開きます。 このコマンドを実行するユーザー アカウントは、WSUS Administrators グループまたはローカルの Administrators グループのいずれかのメンバーである必要があります。
1. WSUS の Tools フォルダーにディレクトリを変更します。  
   `cd "c:\Program Files\Update Services\Tools"`
1. 次のコマンドを使用して、SSL を使用するように WSUS を構成します。

    `WsusUtil.exe configuressl server.contoso.com`
   
   *server.contoso.com* は WSUS サーバーの FQDN です。
1. WsusUtil からは、WSUS サーバーの URL の最後にポート番号が付加されたものが返されます。 ポートは、8531 (既定値) または 443 のいずれかになります。 返された URL が予想したとおりであることを確認します。 何か誤入力した場合は、コマンドを再度実行できます。

   :::image type="content" source="media/wsusutil.png" alt-text="WSUS の HTTPS URL を返す wsusutil configuressl コマンド":::

> [!TIP] 
> WSUS サーバーがインターネットに接続されている場合は、`WsusUtil.exe configuressl` を実行するときに外部 FQDN を指定します。

## <a name="verify-the-wsus-console-can-connect-using-ssl"></a><a name="bkmk_wsus_console"></a> WSUS コンソールが SSL を使用して接続できることを確認する

WSUS コンソールでは、ApiRemoting30 Web サービスが接続に使用されます。 また、Configuration Manager のソフトウェアの更新ポイント (SUP) でも、次のような特定のアクションを実行するよう WSUS に指示するために、同じ Web サービスが使用されます。

- ソフトウェア更新プログラムの同期の開始
- WSUS に対する適切なアップストリーム サーバーの設定 (Configuration Manager の階層内で SUP のサイトが存在する場所に依存)
- 階層の最上位の WSUS サーバーからの同期に対する、製品と分類の追加または削除。
- 期限切れの更新プログラムの削除

WSUS コンソールを開き、WSUS サーバーの ApiRemoting30 Web サービスに対する SSL 接続を使用できることを確認します。 後で、他の Web サービスの一部をテストします。

1. WSUS コンソールを開き、 **[操作]**  >  **[サーバーへ接続]** を選択します。
1. **[サーバー名]** オプションには、WSUS サーバーの FQDN を入力します。
1. WSUSutil からの URL で返された **[ポート番号]** を選択します。
1. 8531 (既定値) または 443 を選択すると、 **[このサーバーへの接続に SSL (Secure Sockets Layer) を使用する]** オプションが自動的に有効になります。
       :::image type="content" source="media/connect-wsus-console.png" alt-text="HTTPS ポート経由で WSUS コンソールに接続する":::
1. Configuration Manager サイト サーバーがソフトウェアの更新ポイントからリモートにある場合は、サイト サーバーから WSUS コンソールを起動し、WSUS コンソールが SSL 経由で接続できることを確認します。
   - リモート WSUS コンソールに接続できない場合は、証明書の信頼、名前解決、またはブロックされているポートのいずれかに問題がある可能性があります。

## <a name="configure-the-software-update-point-to-require-ssl-communication-to-the-wsus-server"></a><a name="bkmk_cm_sup"></a> WSUS サーバーに対して SSL 通信を要求するようにソフトウェアの更新ポイントを構成する

TLS/SSL を使用するように WSUS を設定した後は、対応する Configuration Manager ソフトウェアの更新ポイントでも SSL を要求するように更新する必要があります。 この変更を行うと、Configuration Manager で次のことが行われるようになります。

- ソフトウェアの更新ポイントに対する WSUS サーバーを構成できることを確認します
- この WSUS サーバーに対するスキャンを行うように指示されたら SSL ポートを使用するように、クライアントに指示します。

WSUS サーバーに対して SSL 通信を要求するようにソフトウェアの更新ポイントを構成するには、以下の手順のようにします。 

1. Configuration Manager コンソールを開き、編集する必要があるソフトウェアの更新ポイントに対する中央管理サイトまたはプライマリ サイト サーバーに接続します。
1. **[管理]**  >  **[概要]**  >  **[サイトの構成]**  >  **[サーバーとサイト システムの役割]** の順に移動します。
1. WSUS がインストールされているサイト システム サーバーを選択し、ソフトウェアの更新ポイントのサイト システムの役割を選択します。
1. リボンから、 **[プロパティ]** を選択します。
1. **[WSUS サーバーに対して SSL 通信を必須にする]** オプションを有効にします。

   :::image type="content" source="media/sup-properties.png" alt-text="[WSUS サーバーに対して SSL 通信を必須にする] オプションが示されている SUP プロパティ":::
1. 変更を適用すると、サイトの [**WCM.log**](../../core/plan-design/hierarchy/log-files.md#BKMK_SUPLog) に次のエントリが表示されます。

   ```
   SCF change notification triggered.
   Populating config from SCF
   Setting new configuration state to 1 (WSUS_CONFIG_PENDING)
   ...
   Attempting connection to local WSUS server
   Successfully connected to local WSUS server
   ...
   Setting new configuration state to 2 (WSUS_CONFIG_SUCCESS)
   ```

ログ ファイルの例からは、このシナリオで不要な情報が削除されています。  

## <a name="verify-functionality-with-configuration-manager"></a><a name="bkmk_cm_verify"></a> Configuration Manager で機能を確認する

### <a name="verify-the-site-server-can-sync-updates"></a>サイト サーバーが更新プログラムを同期できることを確認する

1. Configuration Manager コンソールを最上位サイトに接続します。
1. **[ソフトウェア ライブラリ]**  >  **[概要]**  >  **[ソフトウェア更新プログラム]**  >  **[すべてのソフトウェア更新プログラム]** に移動します。
1. リボンから、 **[ソフトウェア更新プログラムの同期]** を選択します。
1. ソフトウェア更新プログラムのサイト全体の同期を開始するかどうかを確認する通知に、 **[はい]** を選択します。
   - WSUS の構成を変更したので、差分同期ではなく、ソフトウェア更新プログラムの完全な同期が実行されます。
1. サイトの **wsyncmgr.log** を開きます。 子サイトを監視している場合は、最初に親サイトの同期が完了するまで待つ必要があります。 ログで次のようなエントリを探して、サーバーの同期が成功したことを確認します。

   ```
   Starting Sync
   ...
   Full sync required due to changes in main WSUS server location.
   ...
   Found active SUP SERVER.CONTOSO.COM from SCF File.
   ...
   https://SERVER.CONTOSO.COM:8531
   ...
   Done synchronizing WSUS Server SERVER.CONTOSO.COM
   ...
   sync: Starting SMS database synchronization
   ...
   Done synchronizing SMS with WSUS Server SERVER.CONTOSO.COM
   ```

### <a name="verify-a-client-can-scan-for-updates"></a>クライアントが更新プログラムをスキャンできることを確認する

SSL を要求するようにソフトウェアの更新ポイントを変更すると、Configuration Manager クライアントは、ソフトウェアの更新ポイントの場所の要求を行うと、更新された WSUS URL を受け取ります。 クライアントをテストすることで、次のことができます。
-  クライアントが WSUS サーバーの証明書を信頼しているかどうかを確認します。 
- WSUS に対して SimpleAuthWebService と ClientWebService が機能しているかどうか。
-  クライアントがスキャン中に EULA を取得した場合、WSUS コンテンツ仮想ディレクトリが機能していること

1. 最近 TLS/SSL を使用するように変更されたソフトウェアの更新ポイントに対してスキャンを行うクライアントを特定します。 クライアントの識別に関するヘルプが必要な場合は、次の PowerShell スクリプトで[スクリプトの実行](../..//apps/deploy-use/create-deploy-scripts.md)を使用します。

   ```powershell
   $Last = (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").LastSuccessScanPath
   $Current= Write-Output (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").CurrentScanPath
   Write-Host "LastGoodSUP- $last"
   Write-Host "CurrentSUP- $current"
   ```

1. テスト クライアントでソフトウェア更新プログラムのスキャン サイクルを実行します。 次の PowerShell スクリプトを使用して、強制的にスキャンを実行できます。

   ```powershell
   Invoke-WMIMethod -Namespace root\ccm -Class SMS_CLIENT -Name TriggerSchedule "{00000000-0000-0000-0000-000000000113}"
   ```

1. クライアントの **ScanAgent.log** を調べて、ソフトウェアの更新ポイントに対するスキャンのメッセージが受信されたことを確認します。

   ```
   Message received: '<?xml version='1.0' ?>
   <UpdateSourceMessage MessageType='ScanByUpdateSource'>
      <ForceScan>TRUE</ForceScan>
      <UpdateSourceIDs>
            <ID>{A1B2C3D4-1234-1234-A1B2-A1B2C3D41234}</ID>
      </UpdateSourceIDs>
    </UpdateSourceMessage>'
   ```

1. **LocationServices.log** を調べて、クライアントが正しい WSUS URL を受け取ったことを確認します。
**LocationServices.log**
   ```
   WSUSLocationReply : <WSUSLocationReply SchemaVersion="1
   ...
   <LocationRecord WSUSURL="https://SERVER.CONTOSO.COM:8531" ServerName="SERVER.CONTOSO.COM"
   ...
   </WSUSLocationReply>
   ```

1. **WUAHandler.log** を調べて、クライアントが正常にスキャンできることを確認します。

   ```
   Enabling WUA Managed server policy to use server: https://SERVER.CONTOSO.COM:8531
   ...
   Successfully completed scan.
   ```

## <a name="next-steps"></a>次のステップ

[ソフトウェア更新プログラムの展開](../deploy-use/deploy-software-updates.md)