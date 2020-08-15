---
title: Windows 自動操縦のトラブルシューティング
description: Windows 自動操縦の展開プロセス中に発生した問題の処理方法について説明します。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: c89731edddd94da99e114cf98c10547c096ebb53
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252015"
---
# <a name="troubleshooting-windows-autopilot"></a>Windows 自動操縦のトラブルシューティング

**適用対象: Windows 10**

Windows の自動操縦は、Windows デバイスのライフサイクルのすべての部分を簡略化するように設計されていますが、問題が発生する可能性が常にあります。 トラブルシューティングに役立つ次の情報を確認してください。

## <a name="troubleshooting-process"></a>トラブルシューティングプロセス

ユーザー主導または自己展開型のデバイス展開を実行しているかどうかにかかわらず、トラブルシューティングプロセスはほぼ同じです。 特定のデバイスのフローを理解すると役に立ちます。

1. ネットワーク接続が確立されます。 接続には、ワイヤレス (Wi-fi) 接続またはワイヤード (イーサネット) 接続を使用できます。
2. Windows 自動操縦プロファイルがダウンロードされます。 ワイヤード (有線) 接続を使用する場合、またはワイヤレス接続を手動で確立する場合、プロファイルは、ネットワーク接続が確立されるとすぐに、自動操縦展開サービスからダウンロードされます。
3. ユーザー認証が行われます。 ユーザー主導の展開を実行する場合、ユーザーは Azure Active Directory の資格情報を入力します。これは検証されます。
4. Azure Active Directory 結合が発生します。 ユーザー主導のデプロイの場合、デバイスは指定されたユーザー資格情報を使用して Azure AD に参加します。 自己展開のシナリオでは、ユーザーの資格情報を指定せずにデバイスが結合されます。
5. MDM の自動登録が行われます。 Azure AD 参加プロセスの一部として、デバイスは Azure AD で構成された MDM サービス (たとえば、Microsoft Intune) に登録されます。
6. 設定が適用されます。 [ [登録ステータス] ページ](enrollment-status.md) が構成されている場合は、[登録ステータス] ページが表示されている間、ほとんどの設定が適用されます。 構成されていない場合、または使用できない場合は、ユーザーがサインインした後に設定が適用されます。

トラブルシューティングのために実行する主なアクティビティは次のとおりです。

- 構成: Azure Active Directory と Microsoft Intune (または同等の MDM サービス) は、「 [Windows 自動構成の要件](configuration-requirements.md)」で指定したとおりに構成されていますか。
- ネットワーク接続: デバイスは、「 [Windows 自動操縦ネットワーク要件](networking-requirements.md)」に記載されているサービスにアクセスできますか。
- 自動操縦装置 (OOBE) の動作: 予期しない既定のエクスペリエンス画面のみが表示されていました。 Azure AD の資格情報ページでは、組織固有の詳細情報が想定どおりにカスタマイズされていますか。
- Azure AD 参加の問題: デバイスは Azure Active Directory に参加できましたか?
- MDM の登録に関する問題: デバイスは Microsoft Intune (または同等の MDM サービス) に登録できましたか?

## <a name="troubleshooting-autopilot-device-import"></a>自動操縦用デバイスのインポートのトラブルシューティング

### <a name="clicking-import-after-selecting-csv-does-nothing-400-error-appears-in-network-trace-with-error-body-cannot-convert-the-literal-devicehash-to-the-expected-type-edmbinary"></a>[CSV] を選択した後に [インポート] をクリックしても何も起こりません。 "400" エラーがネットワークトレースにエラー本文と共に表示される **"リテラル ' [DEVICEHASH] ' を必要な型 ' Edm. Binary ' に変換できません**"

このエラーは、デバイスハッシュが正しくフォーマットされていないことを示しています。 収集されたハッシュが破損していると、このエラーが発生する可能性があります。 1つの可能性として、ハッシュ自体 (有効な場合でも) はデコードされません。

デバイスハッシュは Base64 です。 デバイスレベルでは、埋め込まれていない Base64 としてエンコードされますが、自動操縦では Base64 が埋め込まれると想定されています。 通常、ペイロードには埋め込みが不要で、プロセスは動作します。 ただし、ペイロードが正しく作成されず、埋め込みが必要になる場合があります。 この場合は、上記のエラーが表示されます。 PowerShell の Base64 デコーダーでも、埋め込みの Base64 が必要であるため、このデコーダーを使用して、ハッシュが適切に埋め込まれていることを検証できます。

ハッシュの末尾の "A" 文字は実質的に空のデータです。 Base64 の各文字は6ビットで、Base64 のは6ビットが0と等しくなります。 **を削除する**か、末尾にを追加しても、実際のペイロードデータは変更されません。

この問題を解決するには、ハッシュを変更し、PowerShell がハッシュのデコードに成功するまで新しい値をテストする必要があります。 ほとんどの場合、結果は判読できません。 "Base-64 char 配列または文字列の長さが無効です" というエラーがスローされないことを探しているだけです。 

Base64 をテストするには、次の PowerShell を使用できます。
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("DEVICE HASH"))
```

そのため、例として (これはデバイスハッシュではなく、テストに適した非埋め込みの Base64 に適合しています)。
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("Q29udG9zbwAAA"))
```

ここで、パディングルールを使用します。 埋め込み文字は "=" です。 埋め込み文字は、ハッシュの最後にのみ使用できます。また、埋め込み文字は最大2つにすることができます。 基本的なロジックを次に示します。

- ハッシュのデコードに失敗しますか。
 - [はい]: 最後の2文字 "=" です。
   - はい: "=" を1つの "A" 文字に置き換えてから、もう一度やり直してください。
   - いいえ: 末尾に "=" 文字をもう1つ追加してから、もう一度やり直してください
 - いいえ: そのハッシュは有効です

前の例のハッシュでロジックをループすると、次のような順列が得られます。
- Q29udG9zbwAAA
- Q29udG9zbwAAA =
- Q29udG9zbwAAA = =
- Q29udG9zbwAAAA
- Q29udG9zbwAAAA =
- **Q29udG9zbwAAAA = =** (有効な埋め込みがある)

収集したハッシュをこの新しい埋め込みハッシュで置き換えてから、もう一度インポートしてみてください。

## <a name="troubleshooting-autopilot-oobe-issues"></a>自動操縦用 OOBE の問題のトラブルシューティング

OOBE に予期しない自動操縦動作が含まれている場合は、デバイスが自動操縦プロファイルを受信したかどうかを確認すると便利です。 その場合は、プロファイルに含まれている設定を確認します。 Windows 10 のリリースによっては、さまざまなメカニズムを使用できます。

### <a name="windows-10-version-1803-and-above"></a>Windows 10 バージョン1803以降

Windows 10 バージョン1803以降では、イベントログエントリが追加されます。 Og エントリを使用して、自動操縦プロファイル設定と OOBE フローに関連する詳細を確認できます。 これらのエントリはイベントビューアーを使用して表示できます。 詳細については、「 **アプリケーションとサービスのログ– > Microsoft – > Windows – > >** 」1903を参照してください。 バージョン1903以降については、「 **アプリケーションとサービスのログ– > Microsoft – > Windows – > ModernDeployment – > 自動操縦**」を参照してください。 シナリオとプロファイルの構成によっては、次のイベントが記録される場合があります。

| イベント ID | Type | 説明 |
|----------|------|-------------| 
| 100 | 警告 | "自動操縦ポリシー [名前] が見つかりませんでした。" 通常、このエラーは一時的な問題であり、デバイスは自動操縦プロファイルがダウンロードされるのを待機しています。 |
| 101 | Info | "AutopilotGetPolicyDwordByName succeeded: policy name = [setting name];ポリシー値 = [値]。 " このメッセージは、数値の OOBE 設定の取得と処理を自動操縦することを示しています。 |
| 103 | Info | "AutopilotGetPolicyStringByName succeeded: policy name = [name];値 = [値]。 " このメッセージは、Azure AD のテナント名など、OOBE 設定文字列の取得と処理を自動で行うことを示しています。 |
| 109 | Info | "AutopilotGetOobeSettingsOverride succeeded: OOBE 設定 [設定名];state = [state]。 " このメッセージは、状態に関連する OOBE 設定の取得および処理を自動実行することを示しています。 |
| 111 | Info | "AutopilotRetrieveSettings は成功しました。" このメッセージは、OOBE の動作を制御する自動操縦プロファイルに格納されている設定が正常に取得されたことを意味します。 |
| 153 | Info | "AutopilotManager は [元の状態] から [新しい状態] に変更された状態を報告しました。" 通常、このメッセージは "ProfileState_Unknown" を "ProfileState_Available" にする必要があります。 この場合は、プロファイルが利用可能で、デバイスにダウンロードされたことを示します。 そのため、デバイスは自動操縦を使用して展開する準備ができています。 |
| 160 | Info | "AutopilotRetrieveSettings の取得を開始しています。" このメッセージは、自動操縦が、必要な自動操縦プロファイル設定をダウンロードする準備ができていることを示しています。 |
| 161 | Info | "AutopilotManager の設定の取得に成功しました。" 自動操縦プロファイルが正常にダウンロードされました。 |
| 163 | Info | "AutopilotManager によって検出されたダウンロードは必要ではなく、デバイスは既にプロビジョニングされています。 デバイスをクリーニングまたはリセットして、これを変更してください。 " このメッセージは、デバイスに自動操縦プロファイルがあることを示しています。通常は、 **Sysprep/Generalize** プロセスによってのみ削除されます。 |
| 164 | Info | "AutopilotManager によって検出されたインターネットを使用してポリシーをダウンロードすることができます。" |
| 171 | エラー | "AutopilotManager で TPM id を設定できませんでした。 HRESULT = [エラーコード]。 " このメッセージは、自己展開モードプロセスを完了するために必要な TPM 構成証明を実行するときに問題が発生したことを示します。 | 
| 172 | エラー | "AutopilotManager は、使用可能な自動操縦プロファイルを設定できませんでした。 HRESULT = [エラーコード]。 " このエラーは、通常、イベント ID 171 に関連しています。 |

イベントログエントリに加えて、以下のレジストリおよび ETW トレースオプションは、Windows 10 バージョン1803以降で動作します。

### <a name="windows-10-version-1709-and-above"></a>Windows 10 バージョン1709以降

自動操縦展開サービスから受け取った自動操縦プロファイル設定は、デバイスのレジストリに格納されます。 この情報については、 **HKLM\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot**を参照してください。 使用できるレジストリエントリは次のとおりです。

| [値] | 説明 |
|-------|-------------|
| AadTenantId | ユーザーがサインインした Azure AD テナントの GUID。 このエントリがデバイスの登録に使用されたテナントと一致しない場合、ユーザーはエラーを受け取ります。 |
| CloudAssignedTenantDomain | デバイスが登録されている Azure AD テナント (例、"contosomn.onmicrosoft.com")。 デバイスが自動操縦に登録されていない場合、この値は空白になります。 |
| CloudAssignedTenantId | デバイスが登録されている Azure AD テナントの GUID。 GUID は、CloudAssignedTenantDomain レジストリ値のテナントドメインに対応します。 デバイスが自動操縦に登録されていない場合、この値は空白になります。|
| IsAutopilotDisabled | 1に設定すると、このレジストリ値は、デバイスが自動操縦に登録されていないことを示します。 この状態は、ネットワーク接続またはファイアウォールの問題またはネットワークのタイムアウトが原因で、自動操縦プロファイルをダウンロードできなかったことを示している可能性もあります。 |
| TenantMatched 照合 | ユーザーのテナント ID が、デバイスが登録されているテナント ID と一致する場合、このエントリは1に設定されます。 このレジストリ値が0の場合、ユーザーにはエラーが表示され、最初からやり直すように強制されます。 |
| CloudAssignedOobeConfig | 構成された自動操縦設定を示すビットマップ。 値は次のとおりです: SkipCortanaOptIn = 1、OobeUserNotLocalAdmin = 2、SkipExpressSettings = 4、SkipOemRegistration = 8、SkipEula = 16 |

### <a name="windows-10-semi-annual-channel-supported-versions"></a>Windows 10 半期チャネルでサポートされるバージョン

[サポートされているバージョン](https://docs.microsoft.com/windows/release-information/)の Windows 10 半期チャネルを実行しているデバイスでは、ETW トレースを使用して、自動操縦と関連コンポーネントから詳細情報を取得できます。 ETW トレースファイルは、Windows パフォーマンスアナライザーまたは同様のツールを使用して表示できます。 詳細については、 [高度なトラブルシューティングのブログ](https://blogs.technet.microsoft.com/mniehaus/2017/12/13/troubleshooting-windows-autopilot-level-300400/)を参照してください。

## <a name="troubleshooting-azure-ad-join-issues"></a>Azure AD 参加に関する問題のトラブルシューティング

デバイスを Azure AD に参加させる最も一般的な問題は Azure AD のアクセス許可に関連しています。 ユーザーがデバイスを Azure AD に参加できるように [、正しい構成が適用さ](configuration-requirements.md) れていることを確認します。 エラーは、ユーザーが参加を許可されているデバイスの数を超えた場合にも発生する可能性があります。 この制限は Azure AD で構成されます。

インポート時に Azure AD デバイスが作成されます。 重要なのは、このオブジェクトは削除されないことです。 オブジェクトは、グループのメンバーシップとターゲット (プロファイルを含む) のために、Azure AD で自動操縦のアンカーとして機能します。 削除すると、結合エラーが発生する可能性があります。 このオブジェクトが削除された場合は、この自動操縦ハッシュを削除して再インポートし、関連付けられているオブジェクトを再作成できるようにすることで、問題を解決できます。

エラーコード801C0003 は、通常、"問題が発生しました" というエラーページで報告されます。 このエラーは、Azure AD 参加に失敗したことを示します。

## <a name="troubleshooting-intune-enrollment-issues"></a>Intune の登録に関する問題のトラブルシューティング

Intune の登録に関する問題については、 [このサポート技術情報の記事](https://support.microsoft.com/help/4089533/troubleshooting-windows-device-enrollment-problems-in-microsoft-intune) を参照してください。 一般的な問題には次のものがあります。
- ユーザーに割り当てられたライセンスが正しくないか、存在しません。
- ユーザーに登録されているデバイスが多すぎます。

エラーコード80180018は、通常、"問題が発生しました" というエラーページで報告されます。 このエラーは、MDM の登録に失敗したことを意味します。

エラーが発生してすぐに自動再起動が失敗する場合 **。管理者アカウントでサインインして、手動で理由とリセットを確認**してください。詳細については、「 [自動操縦リセットのトラブルシューティング](https://docs.microsoft.com/education/windows/autopilot-reset#troubleshoot-autopilot-reset) 」を参照してください。

## <a name="profile-download"></a>プロファイルのダウンロード

インターネットに接続された Windows 10 デバイスが起動すると、自動操縦サービスへの接続が試行され、自動操縦プロファイルがダウンロードされます。 注: 空のプロファイルが PC にローカルにキャッシュされないように、この段階にプロファイルが存在することが重要です。 Windows 10 バージョン1803以前で現在キャッシュされているローカルプロファイルを削除するには、 **sysprep/generalize/oobe**を使用して os を再一般化し、os を再インストールするか、PC を再イメージ化する必要があります。 Windows 10 バージョン1809以降では、PC を再起動することによって新しいプロファイルを取得できます。

プロファイルをダウンロードする場合は、PC で実行されている Windows 10 のバージョンによって異なります。 次の表を参照してください。

| Windows 10 のバージョン | プロファイルのダウンロード動作 |
| --- | --- |
| 1709 | このプロファイルは、OOBE ネットワーク接続ページの後にダウンロードされます。 このページは、ワイヤード (有線) 接続を使用しているときは表示されません。 この場合、EULA 画面の前にプロファイルがダウンロードされます。 |
| 1803 | プロファイルは、できるだけ早くダウンロードされます。 ワイヤード (有線) の場合は、OOBE の開始時にダウンロードされます。 ワイヤレスの場合は、[ネットワーク接続] ページの後にダウンロードされます。 |
| 1809 | プロファイルは、できるだけ早く (1803 と同じ)、再起動のたびに再度ダウンロードされます。 |

OOBE 中にコンピューターを再起動する必要がある場合は、次のようにします。
- Shift + F10 キーを押してコマンドプロンプトを開きます。
- すぐに再起動するには、 **shutdown/r/t 0** を入力してください。直ちにシャットダウンするには、 **/s/t 0 をシャットダウン** してください。

詳細については、「 [Windows セットアップ コマンド ライン オプション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)」を参照してください。

## <a name="related-topics"></a>関連トピック

[Windows 自動操縦-既知の問題](known-issues.md)<br>
[Windows 10 での MDM エラーの診断](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
