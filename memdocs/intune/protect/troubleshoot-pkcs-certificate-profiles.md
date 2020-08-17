---
title: Microsoft Intune で PKCS 証明書プロファイルを使用して証明書をプロビジョニングする場合のトラブルシューティング | Microsoft Docs
description: デバイスによって秘密キーと公開キーのペア (PKCS) のプロファイルを使用して、Intune に使用する証明書を要求する場合のトラブルシューティングを行います。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c6f2eb7d6174c706cdd8a3910df1d0ddc2e6ef0
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110683"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>Microsoft Intune での PKCS 証明書の展開のトラブルシューティング

この記事の情報は、Microsoft Intune で秘密キーと公開キーのペア (PKCS) 証明書を展開する際のいくつかの一般的な問題を解決するうえで役立ちます。 トラブルシューティングを行う前に、「[Intune で PKCS 証明書を構成して使用する](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca)」に記載されている次のタスクを完了していることを確認します。

- [PKCS 証明書プロファイルを使用する場合の要件](../protect/certficates-pfx-configure.md#requirements)を確認する
- エンタープライズ証明機関 (CA) からルート証明書をエクスポートする
- 証明機関で証明書テンプレートを構成する
- Intune Certificate Connector をインストールして構成する
- 信頼された証明書プロファイルを作成して展開し、ルート証明書を展開する
- PKCS 証明書プロファイルを作成して展開する

PKCS 証明書プロファイルに関する問題の最も一般的な原因は、PKCS 証明書プロファイルの構成に関連しています。 プロファイルの構成を見直して、サーバー名または完全修飾ドメイン名 (FQDN) に入力ミスがないことを確認し、 **[証明機関]** および **[証明機関名]** が正しいことを確認します。

- **証明機関**:証明機関のコンピューターの内部 FQDN。 たとえば、server1.domain.local。
- **証明機関名**:証明機関 MMC に表示される証明機関名。 **[証明機関 (ローカル)]** 下を確認してください

CA 上で [certutil コマンドライン プログラム](https://docs.microsoft.com/windows-server/administration/windows-commands/certutil)を使用して、[証明機関] および [証明機関名] の正しい名前を確認できます。

## <a name="pkcs-communication-overview"></a>PKCS 通信の概要

次の図は、Intune での PKCS 証明書展開プロセスの基本的な概要を示しています。

> [!div class="mx-imgBorder"]
> ![PKCS 証明書プロファイルのフロー](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. 管理者は、Intune で PKCS 証明書プロファイルを作成します。
2. Intune サービスでは、オンプレミスの Intune Certificate Connector によってユーザー用の新しい証明書が作成されるように、要求が行われます。
3. Intune Certificate Connector によって、Microsoft 証明機関に対して PFX BLOB と要求が送信されます。
4. 証明機関によって発行が行われ、Intune Certificate Connector に PFX ユーザー証明書が送り返されます。
5. Intune Certificate Connector によって、暗号化された PFX ユーザー証明書が Intune にアップロードされます。
6. Intune によって、PFX ユーザー証明書の暗号化が解除されてから、デバイス管理証明書を使用するデバイスに対して、再暗号化が行われます。  その後、Intune によって PFX ユーザー証明書がデバイスに送信されます。
7. デバイスから Intune へ証明書の状態が報告されます。

## <a name="data-and-log-files"></a>データおよびログ ファイル

通信と証明書のプロビジョニング ワークフローに関する問題を特定するには、サーバー インフラストラクチャとデバイスの両方のログ ファイルを確認します。 後述する PKCS 証明書プロファイルのトラブルシューティングに関するセクションでは、このセクションで触れているログ ファイルについて取り上げています。

- [インフラストラクチャとサーバーのログ](#logs-for-on-premises-infrastructure)

デバイスのログは、デバイスのプラットフォームによって異なります。

- [iOS と iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>オンプレミス インフラストラクチャのログ
  
証明書の展開に PKCS 証明書プロファイルの使用をサポートするオンプレミス インフラストラクチャには、Microsoft Intune Certificate Connector、Windows サーバー上で実行される NDES、および証明機関などがあります。

これらのロールのログ ファイルには、Windows イベント ビューアー、証明書コンソールと、Intune Certificate Connector、NDES、またはオンプレミス インフラストラクチャの一部である他のロールと操作に固有のさまざまなログ ファイルが含まれます。

- **NDESConnector_date_time.svclog**:

  このログには、Microsoft Intune Certificate Connector から Intune クラウド サービスへの通信が示されます。 このログ ファイルを表示するには、[サービス トレース ビューアー ツール](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe)を使用できます。

  関連するレジストリ キー:*HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  場所: *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs* の NDES をホストするサーバー上

- **CertificateRegistrationPoint_date_time.svclog**:

  このログには、証明書の要求を受信および確認する NDES ポリシー モジュールが示されます。 このログ ファイルを表示するには、[サービス トレース ビューアー ツール](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe)を使用できます。

  場所: *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs* の NDES をホストするサーバー上

- **NDESPlugin.log**:

  このログには、証明書登録ポイントへ証明書要求を渡す処理と、それらの要求の結果の検証が示されます。

  場所: *%program_files%\Microsoft Intune\NDESPolicyModule\logs* の NDES をホストするサーバー上

- **Windows アプリケーション ログ**:

  場所:NDES をホストするサーバー上:**eventvwr.msc** を実行して Windows イベント ビューアーを開きます

### <a name="logs-for-android-devices"></a>Android デバイスのログ

Android を実行するデバイスの場合は、**Android ポータル サイト** アプリ ログ ファイル **OMADM.log** を使用します。 ログを収集して確認する前に、[[詳細なログ記録]](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) が有効であることを確認してから、問題を再現します。

デバイスから OMADM.logs を収集する方法については、「[USB ケーブルを使用してログをアップロードして電子メールを送信する](../user-help/send-logs-to-your-it-admin-using-cable-android.md)」を参照してください。

サポートする[ログをアップロードして電子メールで送信する](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app)こともできます。

### <a name="logs-for-ios-and-ipados-devices"></a>iOS および iPadOS デバイスのログ

iOS/iPadOS を実行するデバイスの場合、デバッグログと、Mac コンピューター上で実行される **Xcode** を使用します。

1. iOS/iPadOS デバイスを Mac に接続し、 **[アプリケーション]**  >  **[ユーティリティ]** に移動してコンソール アプリを開きます。

2. **[アクション]** で、 **[Include Info Messages]\(情報メッセージを含める\)** と **[Include Debug Messages]\(デバッグ メッセージを含める\)** を選択します。

   ![ログ オプションを選択する](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. 問題を再現し、次のようにログをテキスト ファイルに保存します。
   1. **[編集]**  >  **[すべて選択]** を選択して現在の画面のすべてのメッセージを選択し、 **[編集]**  >  **[コピー]** を選択してメッセージをクリップボードにコピーします。
   2. TextEdit アプリケーションを開き、コピーしたログを新しいテキスト ファイルに貼り付けて、ファイルを保存します。

iOS および iPadOS デバイスのポータル サイト ログには、PKCS 証明書プロファイルに関する情報は含まれていません。

### <a name="logs-for-windows-devices"></a>Windows デバイスのログ

Windows を実行するデバイスの場合、Windows イベント ログを使用して、Intune で管理するデバイスの登録またはデバイス管理の問題を診断します。

デバイスで、 **[イベント ビューアー]**  >  **[アプリケーションとサービス ログ]**  >  **[Microsoft]**  >  **[Windows]**  >  **[DeviceManagement-Enterprise-Diagnostics-Provider]** を開きます。

![Windows イベント ログ](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="antivirus-exclusions"></a>ウイルス対策の除外

次の場合に、NDES または Certificate Connector をホストするサーバーでウイルス対策の除外を追加することを検討してください。

- 証明書の要求はサーバーまたは Intune Certificate Connector に届いているが、正常に処理されていない 
- 証明書の発行が遅い

除外対象となる可能性がある場所の例を次に示します。

- *%program_files%* \Microsoft Intune\PfxRequest
- *%program_files%* \Microsoft Intune\CertificateRequestStatus
- *%program_files%* \Microsoft Intune\CertificateRevocationStatus

## <a name="common-errors"></a>一般的なエラー

以下のセクションではそれぞれ、次の一般的なエラーに対応しています。

- [RPC サーバーを使用できません 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [登録ポリシー サーバーが見つかりません 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [送信が保留中です](#the-submission-is-pending)
- [パラメーターが正しくありません 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [ポリシー モジュールによって拒否されました](#denied-by-policy-module)
- [証明書プロファイルが保留中としてスタックしています](#certificate-profile-stuck-as-pending)
- [エラー -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>RPC サーバーを使用できません 0x800706ba

PFX 展開中は、信頼されたルート証明書がデバイス上に表示されますが、PFX 証明書はデバイス上には表示されません。 NDESConnector ログ ファイルには、 **RPC サーバーを使用できません。0x800706ba** という文字列が含まれます。次の例の 1 行目に表示されています。

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>原因 1 - Intune での CA の構成が正しくない

この問題は、PKCS 証明書プロファイルによって間違ったサーバーが指定されているか、CA の名前または FQDN に入力ミスが含まれている場合に発生する可能性があります。 CA は、プロファイルの次のプロパティで指定されています。

- Certification authまたはity
- 証明機関名

**解決方法**:

次の設定を確認して、正しくない場合は修正します。

- **[証明機関]** プロパティには、CA サーバーの内部 FQDN が表示されます。
- **[証明機関名]** プロパティには、CA の名前が表示されます。

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>原因 2 - 以前の CA 証明書で署名された要求に対する証明書の更新が、CA によってサポートされていない

PKCS 証明書プロファイル上の CA のFQDN と名前が正しい場合、証明機関のサーバー上にある Windows アプリケーション ログを確認します。 次の例に示すような **Event ID 128** を探します。

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

CA 証明書が更新された場合は、オンライン証明書状態プロトコル (OCSP) 応答の署名証明書に署名が行われる必要があります。 署名されると、OCSP 応答の署名証明書によって、失効状態を確認することで他の証明書の検証が行われます。 既定では、この署名は有効になっていません。

**解決方法**:

証明書の署名を手動で適用します。

1. CA サーバー上で、管理者特権でのコマンド プロンプトを開き、コマンド **certutil-setreg ca\UseDefinedCACertInRequest 1** を実行します
2. Certificate Services サービスを再起動します。

Certificate Services サービスが再起動されると、デバイスでは証明書の受信が可能になります。

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>登録ポリシー サーバーが見つかりません 0x80094015

次の例に示すように、**登録ポリシー サーバーが見つかりません** と **0x80094015** が表示されます。

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>原因 - 証明書の登録ポリシーのサーバー名

この問題は、Intune NDES コネクタをホストするコンピューターによって、証明書の登録ポリシー サーバーを見つけられない場合に発生します。

**解決方法**:

NDES コネクタをホストするコンピューター上で、証明書の登録ポリシー サーバーの名前を手動で構成します。 名前を構成するには、[Add-CertificateEnrollmentPolicyServer](https://docs.microsoft.com/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps) PowerShell コマンドレットを使用します。

### <a name="the-submission-is-pending"></a>送信が保留中です

PKCS 証明書プロファイルをモバイル デバイスに展開した後、証明書が取得されず、NDESConnector ログに、次の例に示すように、**送信が保留中です**という文字列が含まれます。

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

加えて、証明機関のサーバー上の **[保留中の要求]** フォルダー内で、PFX 要求を確認できます。

> [!div class="mx-imgBorder"]
> ![証明機関の [保留中の要求] フォルダーのスクリーンショット](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>原因 - 要求処理の構成が正しくない

この問題は、オプションの **[管理者が証明書を発行するまで、証明書の要求状態を保留にする]** が、 **[プロパティ]**  >  **[ポリシー モジュール]**  >  **[プロパティ]** ダイアログ ボックスで選択されている場合に発生します。

> [!div class="mx-imgBorder"]
> ![[ポリシー モジュール] のプロパティのスクリーンショット](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**解決方法**:

[ポリシー モジュール] のプロパティを編集して、次に設定します: **[証明書テンプレートに操作が設定されている場合はそれに従い、設定されていない場合は自動的に証明書を発行する]** 。

### <a name="the-parameter-is-incorrect-0x80070057"></a>パラメーターが正しくありません 0x80070057

Intune Certificate Connector がインストールされ正常に構成されている場合に、デバイスでは PKCS 証明書が受信されず、次の例に示すように、NDESConnector ログに **パラメーターが正しくありません。0x80070057** という文字列が含まれます。

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>原因 - PKCS プロファイルの構成

この問題は、Intune での PKCS プロファイルが正しく構成されていない場合に発生します。 次に、一般的な誤った構成を示します。

- プロファイルには、正しくない CA の名前が含まれています。
- サブジェクト代替名 (SAN) は電子メール アドレス用に構成されていますが、対象ユーザーにはまだ有効な電子メール アドレスがありません。 この組み合わせが生じると、SAN は、無効である null 値になります。

**解決方法**:

PKCS プロファイルの次の構成を確認して、デバイス上でポリシーが更新されるまで待機します。

- CA の名前を使って構成されている
- 正しいユーザー グループに割り当てられている
- グループ内のユーザーに有効な電子メール アドレスがある

詳細については、「[Intune で PKCS 証明書を構成して使用する](../protect/certficates-pfx-configure.md)」をご覧ください。

### <a name="denied-by-policy-module"></a>ポリシー モジュールによって拒否されました

デバイスによって信頼されたルート証明書が受信されても、PFX 証明書が受信されず、NDESConnector ログには、次の例に示すように **タスクの送信に失敗しました。ポリシー モジュールによって拒否されました**という文字列が表示されます。

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>原因 – 証明書テンプレートに対するコンピューター アカウントのアクセス許可

この問題は、Intune Certificate Connector をホストするサーバーのコンピューター アカウントに、証明書テンプレートに対するアクセス許可がない場合に発生します。

**解決方法**:

1. 管理特権があるアカウントでエンタープライズ CA にサインインします。
2. **[証明機関]** コンソールで、 **[証明書テンプレート] を右クリックして [管理] を選択**します。
3. 証明書テンプレートを探して、テンプレートの **[プロパティ]** ダイアログ ボックスを開きます。
4. **[セキュリティ]** タブを選択して、Microsoft Intune Certificate Connector をインストールしたサーバー用のコンピューター アカウントを追加します。 そのアカウントに、 **[読み取り]** と **[登録]** のアクセス許可を付与します。
5. **[適用]**  >  **[OK]** の順に選択して証明書テンプレートを保存し、 **[証明書テンプレート]** コンソールを閉じます。
6. **[証明機関]** コンソールで **[証明書テンプレート]** を右クリックして、 **[新規作成]**  >  **[発行する証明書テンプレート]** をクリックします。
7. 変更したテンプレートを選択して、 **[OK]** をクリックします。

詳細については、「[CA 上で証明書テンプレートを構成する](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca)」を参照してください。

### <a name="certificate-profile-stuck-as-pending"></a>証明書プロファイルが保留中としてスタックしています

Microsoft Endpoint Manager admin center では、PKCS 証明書プロファイルは、**保留中**の状態では展開できません。 NDESConnector ログ ファイルには、明らかなエラーはありません。
この問題の原因は、ログでは明確に特定されないため、次のような原因を探ります。

#### <a name="cause-1---unprocessed-request-files"></a>原因 1 - 未処理の要求ファイル

処理に失敗した理由を示すエラーについて、要求ファイルを確認します。

1. NDES コネクタをホストするコンピューター上で、ファイル エクスプローラーを使用して **%programfiles%\Microsoft Intune\PfxRequest** に移動します。
2. 任意のテキスト エディターを使用して、 **[失敗]** および **[Processing]\(処理中\)** フォルダー内のファイルを確認します。

   > [!div class="mx-imgBorder"]
   > ![PfxRequest フォルダーを確認する](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. これらのファイル内で、エラーを示しているか、または問題を提示しているエントリを探します。 要求の処理に失敗した理由の手掛かりと、それらの問題の解決策のために、Web ベースの検索を使用してエラー メッセージを調べます。

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>原因 2 - PKCS 証明書プロファイルの構成の誤り

**[失敗]** 、 **[Processing]\(処理中\)** 、または **[成功]** フォルダー内に要求ファイルが見つからない場合、PKCS 証明書プロファイルに誤った証明書が関連付けられていることが原因の可能性があります。 たとえば、プロファイルに下位 CA が関連付けられていたり、誤ったルート証明書が使用されていたりします。

**解決方法**:

1. 信頼された証明書プロファイルを確認して、エンタープライズ CA からデバイスへのルート証明書を展開済みであることを確かめます。
2. PKCS 証明書プロファイルを確認して、正しい CA、証明書の種類、およびルート証明書をデバイスに展開する信頼された証明書プロファイルが参照されていることを確かめます。

詳細については、Microsoft Intune で[認証に証明書を使用する](../protect/certificates-configure.md)方法に関する記事を参照してください。

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>エラー -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

PKCS 証明書の展開に失敗し、発行元 CA 上の証明書コンソールに、次の例に示すように、 **-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED** という文字列を含むメッセージが表示されます。

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>原因- [要求に含まれる] が誤った構成になっている

この問題は、証明書テンプレートの **[プロパティ]** ダイアログ ボックスにある **[サブジェクト名]** 上で、 **[要求に含まれる]** オプションが有効になっていない場合に発生します。

> [!div class="mx-imgBorder"]
> ![NDES プロパティを構成する](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**解決方法**:

テンプレートを編集して、構成の問題を解決します。

1. 管理特権があるアカウントでエンタープライズ CA にサインインします。
2. **[証明機関]** コンソールで **[証明書テンプレート]** を右クリックして **[管理]** を選択します。
3. 証明書テンプレートの [プロパティ] ダイアログ ボックスを開きます。
4. **[サブジェクト名]** タブで **[要求に含まれる]** を選択します
5. **[OK]** を選択して証明書テンプレートを保存してから、 **[証明書テンプレート]** コンソールを閉じます。
6. **[証明機関]** コンソールで、 **[テンプレート]** を右クリック  >  **[新規作成]**  >  **[発行する証明書テンプレート]** の順にクリックします。
7. 変更したテンプレートを選択して、 **[OK]** を選びます。

## <a name="next-steps"></a>次のステップ

引き続き解決策を必要としているか、Intune に関するより詳しい情報を探している場合は、[Microsoft Intune フォーラム](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)に質問を投稿してください。 多くのサポート エンジニア、MVP、および開発チームのメンバーがフォーラムをよく利用しているため、支援を受ける機会が得られます。

Microsoft Intune 製品サポート チームにサポート リクエストを開くには、「[Microsoft Intune のサポートを受ける方法](../fundamentals/get-support.md)」を参照してください。
PKCS 証明書の展開に関する詳細については、次の記事を参照してください。

- [Intune で PKCS 証明書を構成して使用する](../protect/certficates-pfx-configure.md)
- [Microsoft Intune でデバイスの証明書プロファイルを構成する](../protect/certificates-configure.md)
- [Microsoft Intune で SCEP 証明書と PKCS 証明書を削除する](../protect/remove-certificates.md)
