---
title: Intune 用 Microsoft Defender ウイルス対策の Windows 10 ウイルス対策ポリシーの設定 | Microsoft Docs
description: Windows 10 の Microsoft Defender ウイルス対策プロファイルの設定一覧を参照してください。 これらの設定は、Microsoft Intune のエンドポイント セキュリティ ウイルス対策ポリシーの一部として構成できます。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: ff5c8208cb1ee9357c501a3c457bc346879b241d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906703"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Microsoft Intune の Windows 10 Microsoft Defender ウイルス対策ポリシーの設定

[エンドポイント セキュリティ ポリシー](../protect/endpoint-security-policy.md)の一部として Microsoft Intune で Windows 10 用の Microsoft Defender ウイルス対策プロファイルに構成できる、エンドポイント セキュリティ ウイルス対策ポリシー設定を確認します。

## <a name="cloud-protection"></a>クラウド保護

これらの設定は、次のプロファイルで使用できます。

- Microsoft Defender ウイルス対策

**設定**:

- **Turn on cloud-delivered protection (クラウドによる保護を有効にする)**  
  CSP:[AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  既定では、Windows 10 デスクトップ デバイス上の Defender から、検出された問題に関する情報が Microsoft に送信されます。 Microsoft ではその情報を分析し、お客様や他のユーザーに影響する問題の詳細を把握して、改善されたソリューションを提供しています。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - クラウドで提供される保護が有効になります。  デバイス ユーザーはこの設定を変更できません。

- **Cloud-delivered protection level (クラウドによる保護レベル)**  
  CSP:[CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  疑わしいファイルのブロック時とスキャン時に適用する Defender ウイルス対策の度合いを構成します。
  - **未構成** (*既定値*) - 既定の Defender のブロック レベル。
  - **高** - クライアントのパフォーマンスを最適化しながら未知のものを積極的にブロックします。この場合、誤検知の可能性が高くなります。
  - **高+** - 不明なファイルを積極的にブロックし、追加の保護策を適用します。これはクライアントのパフォーマンスに影響を及ぼす可能性があります。
  - **ゼロ トレランス** - 不明な実行可能ファイルをすべてブロックします。

- **Defender クラウド延長タイムアウト (秒単位)**  
  CSP:[CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender ウイルス対策を使用すると、疑わしいファイルが 10 秒間自動的にブロックされ、その間にクラウド内でそれらがスキャンされて、安全であることが確認されます。 このタイムアウトに最大 50 秒を追加できます。

## <a name="microsoft-defender-antivirus-exclusions"></a>Windows Defender ウイルス対策の除外

これらの設定は、次のプロファイルで使用できます。

- Microsoft Defender ウイルス対策
- Windows Defender ウイルス対策の除外

**設定**:

このグループの各設定について、設定を展開し、 **[追加]** を選択して、除外の値を指定できます。

- **Defender の除外されるプロセス**  
  CSP:[ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  スキャン中に無視するプロセスによって開かれるファイルの一覧を指定します。 プロセス自体はスキャンから除外されません。

- **スキャンおよびリアルタイム保護から除外するファイル拡張子**  
  CSP:[ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  スキャン中に無視するファイルの種類について拡張子の一覧を指定します。

- **Defender の除外されるファイルとフォルダー**  
  CSP:[ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  スキャン中に無視するファイルとディレクトリ パスの一覧を指定します。

## <a name="real-time-protection"></a>リアルタイム保護

これらの設定は、次のプロファイルで使用できます。

- Microsoft Defender ウイルス対策

**設定**:

- **リアルタイム保護を有効にする**  
  CSP:[AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  リアルタイム監視機能を使用するには、Windows 10 デスクトップ デバイス上に Defender が必要です。
  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - リアルタイム監視の使用を強制します。 デバイス ユーザーはこの設定を変更できません。

- **Enable on access protection (常時保護を有効にする)**  
  CSP:[AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  オンデマンドではなく、継続的にアクティブなウイルス対策を構成します。

  - **未構成** (*既定値*) - このポリシーを選択しても、デバイス上のこの設定の状態は変更されません。 デバイス上の既存の状態は変更されません。
  - **いいえ** - デバイス上で常時保護をブロックします。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - デバイス上で常時保護がアクティブになります。

- **受信ファイルと送信ファイルの監視**  
  CSP:[Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  この設定を構成して、どの NTFS ファイルとプログラムの動作を監視するかを決定します。
  - **すべてのファイルを監視する** (*既定*)
  - **受信ファイルのみを監視する**
  - **送信ファイルのみを監視する**

- **動作の監視を有効にする**  
  CSP:[AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  既定では、Windows 10 デスクトップ デバイス上の Defender には動作監視機能が使用されます。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - リアルタイム動作の監視の使用を強制します。 デバイス ユーザーはこの設定を変更できません。

- **Turn on network protection (ネットワーク保護を有効にする)**  
  CSP:[EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  インターネット上のフィッシング詐欺、悪用ホスト サイト、および悪意のあるコンテンツにアクセスしないように、アプリを使用するデバイス ユーザーを保護します。 保護には、サード パーティ製のブラウザーが危険なサイトに接続するのを防ぐことが含まれます。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - ネットワーク保護は有効になります。 デバイス ユーザーはこの設定を変更できません。

- **すべてのダウンロード ファイルと添付ファイルをスキャンする**  
  CSP:[EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  ダウンロードしたすべてのファイルと添付ファイルをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - すべてのダウンロードされたファイルと添付ファイルが Defender によってスキャンされます。 デバイス ユーザーはこの設定を変更できません。

- **Scan scripts that are used in Microsoft browsers (Microsoft のブラウザーで使用されているスクリプトをスキャンする)**  
  CSP:[AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  スクリプトをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - Defender によってスクリプトがスキャンされます。 デバイス ユーザーはこの設定を変更できません。

- **ネットワーク ファイルをスキャンする**  
  CSP:[AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  ネットワーク ファイルをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - ネットワーク ファイルのスキャンを有効にします。 デバイス ユーザーはこの設定を変更できません。

- **Scan emails (メールをスキャンする)**  
  CSP:[AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  着信メールをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - メールのスキャンを有効にします。 デバイス ユーザーはこの設定を変更できません。

## <a name="remediation"></a>修復

これらの設定は、次のプロファイルで使用できます。

- Microsoft Defender ウイルス対策

**設定**:

- **Number of days (0-90) to keep quarantined malware (検査されたマルウェアを保持する日数 (0-90))**  
  CSP:[DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  検査された項目がシステムによって自動的に削除されるまで保持される日数を 0 から 90 の範囲で指定します。 値を 0 にすると、項目は隔離されたままになり、自動的に削除されません。

- **サンプル送信の同意**  

  - **[未構成]** ("*既定値*")
  - **安全なサンプルを自動的に送信する**
  - **[常に確認する]**
  - **送信しない**
  - **すべてのサンプルを自動的に送信する**

- **Action to take on potentially unwanted apps (望ましくない可能性のあるアプリに対して実行するアクション)**  
  CSP:[PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  望ましくない可能性のあるアプリケーション (PUA) の検出レベルを指定します。 望ましくない可能性のあるソフトウェアをダウンロードするか、デバイスにインストールしようとすると、Defender からユーザーに警告されます。

  - **未構成** (*既定値*) - 設定はシステムの既定値 (PUA の保護が無効) に復元されます。
  - **無効化**
  - **有効** - 検出された項目はブロックされ、履歴に他の脅威と共に表示されます。
  - **監査モード** - Defender で、望ましくない可能性のあるアプリケーションが検出されますが、対策は何も行われません。 イベント ビューアーで Defender によって作成されたイベントを検索することで、Defender でアプリケーションに対して実行されたアクションに関する情報を確認できます。

- **Actions for detected threats (検出された脅威に対するアクション)**  
  CSP:[ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  マルウェアの脅威レベルに基づいて、Defender で検出されたマルウェアに対して実行されるアクションを指定します。
  
  Defender では、検出されたマルウェアが次の重大度レベルのいずれかに分類されます。
  - **重要度レベル低**
  - **"中程度" の重大度**
  - **重要度レベル高**
  - **"重大" の重大度**

  各レベルに対して実行するアクションを指定します。 各重大度レベルの既定値は *[未構成]* です。

  - **未構成**
  - **クリーン** - サービスによってファイルの回復とウイルス駆除が試行されます。
  - **検査** - 検査するファイルが移動されます。
  - **削除** - デバイスからファイルが削除されます。
  - **許可**- ファイルを許可し、他の操作は実行しません。
  - **ユーザー定義** - デバイス ユーザーが実行するアクションを決定します。
  - **ブロック** - ファイルの実行はブロックされます。

## <a name="scan"></a>スキャン

これらの設定は、次のプロファイルで使用できます。

- Microsoft Defender ウイルス対策

**設定**:

- **アーカイブ ファイルをスキャンする**  
  CSP:[AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  ZIP ファイルや CAB ファイルなどのアーカイブ ファイルをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はクライアントの既定値に戻ります。つまり、アーカイブ ファイルはスキャンされますが、ユーザーは設定を無効にすることができます。
詳細情報
  - **いいえ** - ファイルのアーカイブはスキャンされません。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - アーカイブ ファイルのスキャンを有効にします。 デバイス ユーザーはこの設定を変更できません。

- **Use low CPU priority for scheduled scans (スケジュールされたスキャン用に低い CPU 優先度を使用する)**  
  CSP:[EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  スケジュールされたスキャン用に CPU 優先度を構成します。
  - **未構成** (*既定値*) - 設定はシステムの既定値に戻ります。つまり、CPU の優先度は変更されません。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - スケジュールされたスキャン中に低い CPU 優先度が使用されます。 デバイス ユーザーはこの設定を変更できません。

- **Disable catch-up full scan (キャッチアップ フル スキャンを無効にする)**  
  CSP:[DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  スケジュールされたフル スキャンのキャッチアップ スキャンを構成します。 キャッチアップ スキャンとは、定期的にスケジュールされたスキャンが実行されなかった場合に開始されるスキャンです。 スケジュールされたスキャンが実行されなかった理由は、通常、スキャンの予定時刻にコンピューターの電源が切られていたためです。

  - **未構成** (*既定値*) - 設定はクライアントの既定値に戻されます。つまり、フル スキャンのキャッチアップ スキャンは有効になりますが、ユーザーはそれを無効にすることができます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - スケジュールされたフル スキャンのキャッチアップ スキャンが適用され、ユーザーがそれを無効にすることはできません。 2 回続けてスキャンの予定時刻にコンピューターがオフラインになっていた場合は、次回のコンピューターへのサインイン時にキャッチアップ スキャンが開始されます。 スケジュールされたスキャンが構成されていない場合は、キャッチアップ スキャンは実行されません。 デバイス ユーザーはこの設定を変更できません。

- **Disable catchup quick scan (キャッチアップ クイック スキャンを無効にする)**  
  CSP:[DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  スケジュールされたクイック スキャンのキャッチアップ スキャンを構成します。 キャッチアップ スキャンとは、定期的にスケジュールされたスキャンが実行されなかった場合に開始されるスキャンです。 スケジュールされたスキャンが実行されなかった理由は、通常、スキャンの予定時刻にコンピューターの電源が切られていたためです。

  - **未構成** (*既定値*) - 設定はクライアントの既定値に戻されます。つまり、キャッチアップ クイック スキャンは有効になりますが、ユーザーはそれを無効にすることができます。
  - **いいえ** - 設定は無効になります。 デバイス ユーザーはこの設定を変更できません。
  - **はい** - スケジュールされたクイック スキャンのキャッチアップ スキャンが適用され、ユーザーがそれを無効にすることはできません。 2 回続けてスキャンの予定時刻にコンピューターがオフラインになっていた場合は、次回のコンピューターへのサインイン時にキャッチアップ スキャンが開始されます。 スケジュールされたスキャンが構成されていない場合は、キャッチアップ スキャンは実行されません。 デバイス ユーザーはこの設定を変更できません。

- **CPU usage limit per scan (スキャンごとの CPU 使用率の制限)**  
  CSP:[AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Defender スキャンの平均 CPU 負荷率を 0 から 100 の割合で指定します。

- **フル スキャン中にマップされたネットワーク ドライブをスキャンする**  
  CSP:[AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  マップされたネットワーク ドライブをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。つまり、マップされたネットワーク ドライブのスキャンは無効になります。
  - **いいえ** - 設定は無効になります。 デバイスのユーザーは設定を変更できません。
  - **はい** - マップされたネットワーク ドライブのスキャンを有効にします。 デバイス ユーザーはこの設定を変更できません。

- **Run daily quick scan at (毎日スキャンを実行する時刻)**  
  CSP:[ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Defender クイック スキャンを実行する時刻を選択します。
  既定では、この設定は**未構成**です

- **スキャンの種類**  
  CSP:[ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Defender で実行するスキャンの種類を選択します。

  - **未構成** (*既定値*)
  - **クイック スキャン**
  - **フル スキャン**

- **Day of week to run a scheduled scan (スケジュールされたスキャンを実行する曜日)**  
  - **未構成** (*既定値*)

- **Time of day to run a scheduled scan (スケジュールされたスキャンを実行する時刻)**  
  - **未構成** (*既定値*)

- **Check for signature updates before running scan (スキャンを実行する前に署名の更新を確認する)**  
  - **未構成** (*既定値*)
  - **いいえ**
  - **あり**

## <a name="updates"></a>更新プログラム

これらの設定は、次のプロファイルで使用できます。

- Microsoft Defender ウイルス対策

**設定**:

- **Enter how often (0-24 hours) to check for security intelligence updates (セキュリティ インテリジェンスの更新を確認する頻度 (0-24 時間) の入力)**  
  CSP:[SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  署名の確認に使用する間隔を 0 から 24 (時間単位) の範囲で指定します。 値を 0 にすると、新しい署名は確認されなくなります。 値が 2 の場合、2 時間ごとに確認されます。

- **定義ファイルの更新をダウンロードするためのファイル共有を定義する**  
  CSP:[SignatureUpdateFallbackOrder](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

  定義ファイルの更新を取得するダウンロード元の場所として、UNC ファイル共有など、場所を管理します。 指定した更新元の 1 つから定義ファイルの更新が正しくダウンロードされたら、リストの残りの更新元には接続されません。

  個別の場所を**追加**したり、.csv ファイルとして場所の一覧を**インポート**したりすることができます。

- **定義ファイルの更新をダウンロードするためのソースの順序を定義する**  
  CSP:[SignatureUpdateFileSharesSources](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)

  定義ファイルの更新を取得する目的で、指定したダウンロード元に接続する順序を指定します。 指定した更新元の 1 つから定義ファイルの更新が正しくダウンロードされたら、リストの残りの更新元には接続されません。

## <a name="user-experience"></a>ユーザー側の表示と操作

これらの設定は、次のプロファイルで使用できます。

- Microsoft Defender ウイルス対策

**設定**:

- **Allow user access to Microsoft Defender app (Microsoft Defender アプリへのユーザー アクセスを許可する)**  
  CSP:[AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **未構成** (*既定値*) - この設定を選択すると、UI と通知が許可されるクライアントの既定値に戻ります。
  - **いいえ** - Defender ユーザー インターフェイス (UI) にアクセスできず、通知は抑制されます。
  - **あり**