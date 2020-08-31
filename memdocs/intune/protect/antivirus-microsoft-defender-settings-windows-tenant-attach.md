---
title: テナントにアタッチされたデバイスの Microsoft Defender ウイルス対策からの Windows 10 ウイルス対策ポリシー設定 | Microsoft Docs
description: Configuration Manager によって管理される Windows 10 デバイスの Microsoft Defender ウイルス対策プロファイルの設定の一覧を確認してください。 Configuration Manager のテナントのアタッチを構成した後、これらの設定を Microsoft Intune のエンドポイント セキュリティのウイルス対策ポリシーの一部として構成できます。
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
ms.openlocfilehash: 966c3f21505cbbe1573abd47fb7081c5e97cc3c1
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823559"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Microsoft Intune のテナントにアタッチされたデバイスの Microsoft Defender ウイルス対策ポリシーの設定

Intune の **[Microsoft Defender Antivirus Policy (ConfigMgr)]\(Microsoft Defender ウイルス対策ポリシー (ConfigMgr)\)** プロファイルで管理できる Microsoft Defender ウイルス対策設定を確認してください。 プロファイルは、Intune の[エンドポイント セキュリティのウイルス対策ポリシー](../protect/endpoint-security-antivirus-policy.md)を構成するときに使用できます。このポリシーは、[テナントのアタッチ](../protect/tenant-attach-intune.md) シナリオを構成したときに、Configuration Manager で管理するデバイスに展開されます。

## <a name="cloud-protection"></a>クラウド保護

- **Turn on cloud-delivered protection (クラウドによる保護を有効にする)**  
  CSP:[AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  既定では、Windows 10 デスクトップ デバイス上の Defender から、検出された問題に関する情報が Microsoft に送信されます。 Microsoft ではその情報を分析し、お客様や他のユーザーに影響する問題の詳細を把握して、改善されたソリューションを提供しています。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **許可されていません。** Microsoft Active Protection Service を無効にします。
  - **[許可]** 。  Microsoft Active Protection Service を有効にします。

- **Cloud-delivered protection level (クラウドによる保護レベル)**  
  CSP:[CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  疑わしいファイルのブロック時とスキャン時に適用する Defender ウイルス対策の度合いを構成します。
  - **未構成** (*既定値*) - 既定の Defender のブロック レベル。
  - **高** - クライアントのパフォーマンスを最適化しながら未知のものを積極的にブロックします。この場合、誤検知の可能性が高くなります。
  - **高+** - 不明なファイルを積極的にブロックし、追加の保護策を適用します。これはクライアントのパフォーマンスに影響を及ぼす可能性があります。
  - **ゼロ トレランス** - 不明な実行可能ファイルをすべてブロックします。

- **Defender クラウド延長タイムアウト (秒単位)**  
  CSP:[CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender ウイルス対策を使用すると、疑わしいファイルが 10 秒間自動的にブロックされ、クラウド内のファイルがスキャンされ、安全であることを確認されます。 この設定では、このタイムアウトに最大 50 秒を追加できます。

## <a name="microsoft-defender-antivirus-exclusions"></a>Windows Defender ウイルス対策の除外

このグループの各設定について、設定を展開し、 **[追加]** を選択して、除外の値を指定できます。

- **Defender の除外されるプロセス**  
  CSP:[ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  スキャン中に無視するプロセスによって開かれるファイルの一覧を指定します。 プロセス自体はスキャンから除外されません。

- **スキャンおよびリアルタイム保護から除外するファイル拡張子**  
  CSP:[ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  スキャン中に無視するファイルの種類について拡張子の一覧を指定します。

- **Defender の除外されるファイルとフォルダー**  
  CSP:[ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  スキャン中に無視するファイルとディレクトリ パスの一覧を指定します。

## <a name="real-time-protection"></a>リアルタイム保護

- **リアルタイム保護を有効にする**  
  CSP:[AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  リアルタイム監視機能を使用するには、Windows 10 デスクトップ デバイス上に Defender が必要です。
  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます
  - **許可されていません。** リアルタイム監視サービスを無効にします。
  - **[許可]** 。 リアルタイム監視サービスを有効にして実行します。

- **Enable on access protection (常時保護を有効にする)**  
  CSP:[AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  オンデマンドではなく、継続的にアクティブなウイルス対策を構成します。

  - **未構成** (*既定値*) - このポリシーを選択しても、デバイス上のこの設定の状態は変更されません。 デバイス上の既存の状態は変更されません。
  - **許可されていません。** リアルタイム監視サービスを無効にします。
  - **[許可]** 。

- **受信ファイルと送信ファイルの監視**  
  CSP:[Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  この設定を構成して、どの NTFS ファイルとプログラムの動作を監視するかを決定します。
  - **すべてのファイルを監視します (双方向)。** (*既定値*)
  - **受信ファイルを監視します。**
  - **送信ファイルを監視します。**

- **動作の監視を有効にする**  
  CSP:[AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  既定では、Windows 10 デスクトップ デバイス上の Defender には動作監視機能が使用されます。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **許可されていません。** 動作の監視を無効にします。
  - **[許可]** 。 リアルタイム動作の監視を有効にします。

- **侵入防止システムを許可する**  
  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **許可されていません。**
  - **[許可]** 。

- **すべてのダウンロード ファイルと添付ファイルをスキャンする**  
  CSP:[EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  ダウンロードしたすべてのファイルと添付ファイルをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **許可されていません。**
  - **[許可]** 。

- **Scan scripts that are used in Microsoft browsers (Microsoft のブラウザーで使用されているスクリプトをスキャンする)**  
  CSP:[AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  スクリプトをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **許可されていません。**
  - **[許可]** 。

- **ネットワーク ファイルをスキャンする**  
  CSP:[AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  ネットワーク ファイルをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **許可されていません。** ネットワーク ファイルのスキャンを無効にします。
  - **[許可]** 。 ネットワーク ファイルをスキャンします。

- **Scan emails (メールをスキャンする)**  
  CSP:[AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  着信メールをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **許可されていません。** メールのスキャンを無効にします。
  - **[許可]** 。 メールのスキャンを有効にします。

## <a name="remediation"></a>修復

- **Number of days (0-90) to keep quarantined malware (検査されたマルウェアを保持する日数 (0-90))**  
  CSP:[DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  検査された項目がシステムによって自動的に削除されるまで保持される日数を 0 から 90 の範囲で指定します。 値を 0 にすると、項目は隔離されたままになり、自動的に削除されません。

- **サンプル送信の同意**  

  - **[未構成]** ("*既定値*")
  - **[常に確認する]** 。
  - **[安全なサンプルを自動的に送信する]** 。
  - **[送信しない]** 。
  - **[すべてのサンプルを自動的に送信する]** 。

- **Action to take on potentially unwanted apps (望ましくない可能性のあるアプリに対して実行するアクション)**  
  CSP:[PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  望ましくない可能性のあるアプリケーション (PUA) の検出レベルを指定します。 望ましくない可能性のあるソフトウェアをダウンロードするか、デバイスにインストールしようとすると、Defender からユーザーに警告されます。

  - **未構成** (*既定値*) - 設定はシステムの既定値 (PUA の保護が無効) に復元されます。
  - **PUA の保護がオフになります。** Windows Defender によって、望ましくない可能性のあるアプリケーションから保護されません。
  - **PUA の保護がオンになります。** 検出された項目はブロックされます。 これらはその他の脅威と共に履歴に表示されます。
  - **[監査モード]** 。 Defender で、望ましくない可能性のあるアプリケーションが検出されますが、対策は何も行われません。 イベント ビューアーで Defender によって作成されたイベントを検索することで、Defender でアプリケーションに対して実行されたアクションに関する情報を確認できます。

- **コンピューターをクリーンアップする前に、システム復元ポイントを作成する**  
  - **はい** (*既定値*):
  - **いいえ**
  - **未構成**

- **Actions for detected threats (検出された脅威に対するアクション)**  
  CSP:[ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  マルウェアの脅威レベルに基づいて、Defender で検出されたマルウェアに対して実行されるアクションを指定します。
  
  Defender では、検出されたマルウェアが次の重大度レベルのいずれかに分類されます。
  - **低レベルの脅威**
  - **中レベルの脅威**
  - **高レベルの脅威**
  - **重大な脅威**

  各レベルに対して実行するアクションを指定します。 各重大度レベルの既定値は *[未構成]* です。

  - **[未構成]** ("*既定値*")
  - **クリーン** - サービスによってファイルの回復とウイルス駆除が試行されます。
  - **検査** - 検査するファイルが移動されます。
  - **削除** - デバイスからファイルが削除されます。
  - **許可**- ファイルを許可し、他の操作は実行しません。
  - **ユーザー定義** - デバイス ユーザーが実行するアクションを決定します。
  - **ブロック** - ファイルの実行はブロックされます。

## <a name="scan"></a>スキャン

- **アーカイブ ファイルをスキャンする**  
  CSP:[AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  ZIP ファイルや CAB ファイルなどのアーカイブ ファイルをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はクライアントの既定値に戻ります。つまり、アーカイブ ファイルはスキャンされますが、ユーザーはスキャンを無効にすることができます。
詳細情報
  - **[許可しない]** 。アーカイブ ファイルのスキャンを無効にします。
  - **[許可]** 。 アーカイブ ファイルをスキャンします。

- **スケジュールされたスキャン用に低い CPU 優先度を有効にする**  
  CSP:[EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  スケジュールされたスキャン用に CPU 優先度を構成します。
  - **未構成** (*既定値*) - 設定はシステムの既定値に戻ります。つまり、CPU の優先度は変更されません。
  - **Disabled**
  - **Enabled**

- **Disable catch-up full scan (キャッチアップ フル スキャンを無効にする)**  
  CSP:[DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  スケジュールされたフル スキャンのキャッチアップ スキャンを構成します。 キャッチアップ スキャンとは、定期的にスケジュールされたスキャンが実行されなかった場合に開始されるスキャンです。 スケジュールされたスキャンが実行されなかった理由は、通常、スキャンの予定時刻にコンピューターの電源が切られていたためです。

  - **未構成** (*既定値*) - 設定はクライアントの既定値に戻されます。つまり、フル スキャンのキャッチアップ スキャンは有効になりますが、ユーザーはそれを無効にすることができます。
  - **Disabled**
  - **Enabled**

- **Disable catchup quick scan (キャッチアップ クイック スキャンを無効にする)**  
  CSP:[DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  スケジュールされたクイック スキャンのキャッチアップ スキャンを構成します。 キャッチアップ スキャンとは、定期的にスケジュールされたスキャンが実行されなかった場合に開始されるスキャンです。 スケジュールされたスキャンが実行されなかった理由は、通常、スキャンの予定時刻にコンピューターの電源が切られていたためです。

  - **未構成** (*既定値*) - 設定はクライアントの既定値に戻されます。つまり、キャッチアップ クイック スキャンは有効になりますが、ユーザーはそれを無効にすることができます。
  - **Disabled**
  - **Enabled**

- **CPU usage limit (0-100 percent) per scan (スキャンあたりの CPU 使用率の制限 (0-100%))**  
  CSP:[AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Defender スキャンの平均 CPU 負荷率を 0 から 100 の割合で指定します。

- **Enable mapped network drives be scanned during a full scan (フル スキャン中にマップされたネットワーク ドライブをスキャンできるようにする)**  
  CSP:[AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  マップされたネットワーク ドライブをスキャンするように Defender を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。つまり、マップされたネットワーク ドライブのスキャンは無効になります。
  - **許可されていません。** マップされたネットワーク ドライブのスキャンを無効にします。
  - **[許可]** 。 マップされたネットワーク ドライブをスキャンします。

- **Run daily quick scan at (毎日スキャンを実行する時刻)**  
  CSP:[ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Defender クイック スキャンを実行する時刻を選択します。
  既定では、このオプションは **[未構成]** です。

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
  - **Disabled**
  - **Enabled**

- **スケジュールされたスキャンとセキュリティ インテリジェンスの更新の開始時刻をランダム化する**  
  -**未構成** - (*既定値*) - **[はい]** 
  - **[いいえ]**

- **フル スキャン中にリムーバブル ドライブをスキャンする**
  - **未構成** (*既定値*)
  - **許可されていません。** リムーバブル ドライブのスキャンを無効にします。
  - **[許可]** 。 リムーバブル ドライブをスキャンします。

## <a name="updates"></a>更新プログラム

- **Enter how often (0-24 hours) to check for security intelligence updates (セキュリティ インテリジェンスの更新を確認する頻度 (0-24 時間) の入力)**  
  CSP:[SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  署名の確認に使用する間隔を 0 から 24 (時間単位) の範囲で指定します。 値を 0 にすると、新しい署名は確認されなくなります。 値が 2 の場合、2 時間ごとに確認されます。

- **定義更新のフォールバック順序 (デバイス)**

- **定義更新ファイル共有ソース (デバイス)**

- **セキュリティ インテリジェンスの場所 (デバイス)**  

## <a name="user-experience"></a>ユーザー エクスペリエンス

- **Microsoft Defender アプリへのユーザー アクセスをブロックする**  
  - **未構成** (*既定値*)
  - **許可されていません。** ユーザーが UI にアクセスできないようにします。
  - **[許可]** 。 ユーザーが UI にアクセスできるようにします。

- **ユーザーがフル スキャン、セキュリティ インテリジェンスの更新、または Windows Defender オフラインを実行する必要がある場合に、クライアント コンピューターに通知メッセージを表示する**  
  - **未構成** (*既定値*)
  - **はい**
  - **いいえ**

- **クライアントのユーザー インターフェイスを無効にする**  
  - **未構成** (*既定値*)
  - **はい**
  - **いいえ**

- **Allow users to view full History results (すべてのユーザーがすべての履歴結果を表示できるようにする)**
  - **未構成** (*既定値*)
  - **はい**
  - **いいえ**