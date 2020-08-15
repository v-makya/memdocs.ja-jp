---
title: Windows 自動操縦に関する既知の問題
ms.reviewer: ''
manager: laurawi
description: Windows の自動操縦展開中に発生する可能性のある既知の問題について通知します。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
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
ms.openlocfilehash: d7c92d2e999ffe9a4e503359a81e6422cd24ee30
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252025"
---
# <a name="windows-autopilot---known-issues"></a>Windows 自動操縦-既知の問題

**適用対象**

- Windows 10

<table>
<th>問題<th>詳細情報

<tr><td>ユーザー対象の登録ステータスプロファイルで指定されたアプリのブロックは、デバイス ESP の間は無視されます。</td>
<td>デバイスの ESP 中にブロックする必要があるアプリの一覧を決定するサービスでは、ユーザー id がわからないため、アプリの一覧を含む正しい ESP プロファイルを特定できません。 回避策として、既定の ESP プロファイル (すべてのユーザーとデバイスをターゲットとする) を有効にし、ブロックしているアプリの一覧をそこに配置します。 今後、この問題を回避するために、デバイスグループに対して ESP プロファイルをターゲットにすることができます。</tr>

<tr><td>そのユーザー名は、別の組織に属しているように見えます。 もう一度サインインするか、別のアカウントを使用してやり直してください。</td>
 <td>HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Provisioning\Diagnostics\AutoPilot. で、すべての情報が正しいことを確認します。 詳細については、「 <a href="troubleshooting.md#windows-10-version-1709-and-above">Windows 自動操縦のトラブルシューティング</a>」を参照してください。</td></tr>

<tr><td>Windows 自動操縦型の Hybrid Azure AD 展開では、Windows 自動操縦プロファイルで指定されている場合でも、ユーザーに管理者権限が付与されることはありません。</td>
<td>この問題は、既に管理者権限を持っているデバイスに別のユーザーがいる場合に発生します。 たとえば、PowerShell スクリプトまたはポリシーによって、Administrators グループのメンバーである追加のローカルアカウントを作成できます。 これが正しく機能するように、Windows の自動操縦プロセスが完了するまで、追加のアカウントを作成しないでください。</tr>

<tr><td>Windows の自動操縦装置プロビジョニングは、リアルタイムクロックが長時間にオフになっているデバイス (数分以上など) で、TPM 構成証明エラーまたは ESP タイムアウトによって失敗する場合があります。</td>
<td>この問題を解決するには、次の手順に従います。 <ol><li>デバイスを起動して、すぐに使えるエクスペリエンス (OOBE) を開始します。
<li>ネットワーク接続 (有線またはワイヤレス) を確立します。
<li>コマンド <b>w32tm/resync/force</b> を実行し、時刻を既定のタイムサーバー (time.windows.com) と同期します。</ol>
</tr>

<tr><td>Windows 10 バージョン1903または1909では、既存のデバイスの windows 自動操縦は機能しません。windows 10 の [使用許諾契約書] 画面など、Windows 自動操縦プロファイルで無効にした画面が表示されます。
<br>&nbsp;<br>
この問題は、Windows 10 バージョン1903および1909によってファイルの AutopilotConfigurationFile.jsが削除されるために発生します。
<td>この問題を解決するには、次の手順に従います。 <ol><li>Configuration Manager タスクシーケンスを編集し、[ <b>Windows のキャプチャの準備</b> ] ステップを無効にします。
<li><b>/Oobe/rebootc:\windows\system32\sysprep\sysprep.exe</b>実行される新しい [<b>コマンドラインの実行]</b>ステップを追加します。</ol>
<a href="https://oofhours.com/2019/09/19/a-challenge-with-windows-autopilot-for-existing-devices-and-windows-10-1903/">詳細情報</a></tr>
 
<tr><td>Windows 10 1903 で TPM の構成証明が失敗するのは、EK 証明書のアキ拡張機能が不足しているためです。 (Windows 10 1903 で追加の検証を行い、TPM EK 証明書に含まれている TCG 仕様に従って、適切な属性があることを確認します。
<td><a href="https://support.microsoft.com/help/4517211/windows-10-update-kb4517211">KB4517211 update</a>をダウンロードしてインストールします。
<tr><td>2019年8月30日 KB4512941 更新プログラム (OS ビルド 18362.329) をインストールすると、次の既知の問題が解決されます。

- 既存のデバイスの Windows 自動操縦機能では、OOBE 中に "アクティビティ" ページが正しく表示されません。 (この問題のため、OOBE 中に余分なページが表示されます)。
- TPM 構成証明の状態が sysprep/generalize によってクリアされていないため、後の OOBE フロー中に TPM 構成証明のエラーが発生しました。 (これは特に一般的な問題ではありませんが、sysprep/generalize を実行していて、再起動または再イメージ化して、自動操縦用のホワイトグローブや自己展開のシナリオに戻るようにデバイスを再イメージ化する場合に、テスト中に実行することができます)。
- デバイスに有効な AIK 証明書があり、EK 証明書がない場合、TPM 構成証明は失敗する可能性があります (この問題は前の項目に関連しています)。
- Windows 自動操縦用のホワイトグローブプロセスで TPM 構成証明が失敗した場合、ランディングページがハングしているように見えます。 (基本的に、ホワイトグローブのランディングページでは、[プロビジョニング] をクリックしてホワイトグローブプロセスを開始すると、エラーが適切に報告されません)。
- TPM 構成証明は、新しい Infineon Tpm (ファームウェアバージョン > 7.69) で失敗します。 (この修正の前に、特定のファームウェアバージョンの一覧のみが受け入れられました)。
- デバイスの名前付けテンプレートでは、15ではなく14文字でコンピューター名が切り捨てられる場合があります。
- 割り当てられたアクセスポリシーによって再起動が発生するため、シングルアプリキオスクデバイスの構成が妨げられる可能性があります。
<td><a href="https://support.microsoft.com/help/4512941">KB4512941 update</a>をダウンロードしてインストールします。 <br><br>更新プログラムを取得するために使用できる特定のリリースチャネルについては、「 <b>この更新プログラムを取得する方法</b> 」を参照してください。
<tr><td>2019年7月26日 KB4505903 更新プログラム (OS ビルド 18362.267) をインストールすると、次の既知の問題が解決されます。

- Windows 自動操縦用のホワイトグローブは、英語以外の OS では機能しないため、"成功" と表示される赤い画面が表示されます。
- Windows の自動操縦では、sysprep、リセット、その他のバリエーションの後に、OOBE 中に AUTOPILOTUPDATE エラーが報告します。 この問題は、通常、OS をリセットした場合、またはカスタムの sysprep イメージを使用した場合に発生します。
- BitLocker 暗号化が正しく構成されていません。 例: BitLocker は、暗号化を開始するためにポリシーを適用した後に予期される通知を受け取りませんでした。
- Microsoft Store から UWP アプリをインストールできないため、Windows の自動操縦中にエラーが発生しています。 Windows の自動操縦 ESP 中にブロックアプリとしてポータルサイトをデプロイしている場合、このエラーが発生することがあります。
- Windows 自動操縦のユーザー主導 Hybrid Azure AD 参加シナリオでは、ユーザーに管理者権限は付与されません。 これは、英語以外の別の OS の問題です。
<td><a href="https://support.microsoft.com/help/4505903">KB4505903 update</a>をダウンロードしてインストールします。 <br><br>更新プログラムを取得するために使用できる特定のリリースチャネルについては、「 <b>この更新プログラムを取得する方法</b> 」を参照してください。
<tr><td>Windows 自動操縦 <a href="self-deploying.md">用自己展開モード</a> が失敗し、エラーコードが発生します。
<td><table>
<tr><td>0x800705B4<td>これは、タイムアウトを示す一般的なエラーです。 自己展開モードでこのエラーが発生する一般的な原因として、デバイスが TPM 2.0 に対応していないことが考えられます (例: 仮想マシン)。 TPM 2.0 に対応していないデバイスは、自己展開モードでは使用できません。
<tr><td>0x801c03ea<td>このエラーは、TPM 構成証明が失敗し、デバイストークンを使用して Azure Active Directory の参加に失敗したことを示します。
<tr><td>0xc1036501<td>Azure AD に複数の MDM 構成があるため、デバイスは MDM の自動登録を行うことができません。 「 <a href="https://oofhours.com/2019/10/01/inside-windows-autopilot-self-deploying-mode/">Windows 自動操縦の自己展開モード</a>」を参照してください。
</table>
<tr><td>白いグローブによって赤い画面が表示され、 <b>Microsoft-Windows-ユーザーのデバイス登録/管理</b>イベントログに<b>HResult エラーコード 0x801C03F3</b>が表示されます。<td>この問題は、Azure AD が、展開しようとしているデバイスの Azure AD デバイスオブジェクトを見つけられない場合に発生する可能性があります。 この問題は、手動でオブジェクトを削除した場合に発生します。 この問題を解決するには、Azure AD、Intune、および自動操縦からデバイスを削除してから、自動操縦を再登録します。これにより、Azure AD デバイスオブジェクトが再作成されます。<br> 
<br>トラブルシューティングログを取得するには、次のように使用します。 <b>Mdmdiagnosticstool.exe-領域の自動操縦;TPM-cab c:\autopilot.cab</b>
<tr><td>白いグローブが赤の画面を表示する<td>ホワイトグローブは VM ではサポートされていません。
<tr><td>Windows 自動操縦デバイスを .csv ファイルからインポート中にエラーが発生した<td>Microsoft Excel で .csv ファイルを編集していないこと、またはメモ帳以外のエディターを使用していないことを確認します。 これらのエディターの中には、ファイル形式が無効になる余分な文字が導入されているものもあります。 
<tr><td>既存のデバイスの Windows 自動操縦は、自動操縦用の OOBE エクスペリエンスに従っていません。<td>Unicode または UTF-8 ではなく、JSON プロファイルファイルが <b>ANSI/ASCII</b> 形式で保存されていることを確認します。
<tr><td>問題が<b>発生</b>した場合は、OOBE 中にページが表示されます。<td>クライアントが、必要なすべての Azure AD/MSA 関連の Url にアクセスできない可能性があります。 詳細については、「 [ネットワーク要件](networking-requirements.md)」を参照してください。
<tr><td>プロビジョニングパッケージを Windows 自動操縦と組み合わせて使用すると、特に PPKG に参加、登録、またはデバイス名の情報が含まれている場合に、問題が発生する可能性があります。<td>PPKGs と Windows 自動操縦を組み合わせて使用することは推奨されません。
</table>

## <a name="related-topics"></a>関連トピック

[Windows 10 での MDM エラーの診断](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Windows 自動操縦のトラブルシューティング](troubleshooting.md)
