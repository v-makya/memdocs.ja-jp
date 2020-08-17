---
title: Intune のエンドポイント セキュリティの攻撃の回避設定 |Microsoft Docs
description: Microsoft Intune のエンドポイント セキュリティの攻撃の回避ポリシー設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: a0d1ee33e3aca6dbb6ff6e349eb9a578aad6ae88
ms.sourcegitcommit: 56a894edd291034510c144c31770cf09e20b2d6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2020
ms.locfileid: "88048074"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティの攻撃の回避ポリシー設定

[エンドポイント セキュリティ ポリシー](../protect/endpoint-security-policy.md)の一部として、Intune のエンドポイント セキュリティ ノードにある "*攻撃の回避*" ポリシーのプロファイルで構成できる設定を確認します。

サポートされているプラットフォームとプロファイルは、次のとおりです。

- **Windows 10 以降**:
  - プロファイル: **[アプリとブラウザーの分離]**
  - プロファイル: **[Web 保護]**
  - プロファイル: **[アプリケーションの制御]**
  - プロファイル: **[攻撃の回避規則]**
  - プロファイル: **[デバイス制御]**
  - プロファイル: **[悪用に対する保護]**

## <a name="app-and-browser-isolation-profile"></a>アプリとブラウザーの分離プロファイル

### <a name="app-and-browser-isolation"></a>アプリとブラウザーの分離

- **Microsoft Edge 向けの Application Guard を有効にする (オプション)**  
  CSP:[AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **[未構成]** ("*既定値*")
  - **Edge に対して有効にする** - Application Guard は未承認サイトを Hyper-V 仮想化ブラウズ コンテナーで開きます。

  *[Edge に対して有効にする]* に設定すると、次の設定を使用できます。
  
  - **[クリップボードの動作]**  
    CSP:[ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    ローカル PC と Application Guard 仮想ブラウザーから、どのようなコピー/貼り付けの操作を許可するかを選択します。
    - **[未構成]** ("*既定値*")
    - **[PC とブラウザーの間でのコピー/貼り付けをブロックする]**
    - **[ブラウザーから PC へのコピー/貼り付けのみを許可する]**
    - **[PC からブラウザーへのコピー/貼り付けのみを許可する]**
    - **[PC とブラウザーの間でのコピー/貼り付けを許可する]**

  - **承認された非エンタープライズ サイトからの外部コンテンツをブロックする**  
    CSP:[BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **[未構成]** ("*既定値*")
    - **はい** - 未承認の Web サイトからのコンテンツの読み込みをブロックします。

  - **Collect logs for events that occur within an Application Guard browsing session (Application Guard ブラウズ セッション内で発生するイベントのログを収集する)**  
    CSP:[AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **[未構成]** ("*既定値*")
    - **はい** - Application Guard 仮想ブラウズ セッション内で発生するイベントのログを収集します。

  - **Allow user-generated browser data to be saved (ユーザーが生成したブラウザー データの保存を許可する)**  
    CSP:[AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **[未構成]** ("*既定値*")
    - **はい** - Application Guard 仮想ブラウズ セッション中に作成されるユーザー データの保存を許可します。 ユーザー データの例としては、パスワード、お気に入り、cookie などがあります。

  - **ハードウェアのグラフィック アクセラレータを有効にする**  
    CSP:[AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **[未構成]** ("*既定値*")
    - **はい** - Application Guard 仮想ブラウズ セッション内で、仮想グラフィックス プロセッシング ユニットを使用して、グラフィックを多用する Web サイトを読み込みます。

  - **Allow users to download files onto the host (ホストへのファイルのダウンロードをユーザーに許可する)**  
    CSP:[SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **[未構成]** ("*既定値*")
    - **はい** - 仮想化されたブラウザーからホスト オペレーティング システムへのファイルのダウンロードをユーザーに許可します。

- **Application Guard でローカル プリンターへの印刷を許可する**  

  - **[未構成]** ("*既定値*")
  - **[はい]** - ローカル プリンターへの印刷を許可します。

- **Application Guard でネットワーク プリンターへの印刷を許可する**  

  - **[未構成]** ("*既定値*")
  - **はい** - ネットワーク プリンターへの印刷を許可します。

- **Application Guard で PDF への出力を許可する**  

  - **[未構成]** ("*既定値*")
  - **はい** - PDF への出力を許可します。

- **Application Guard で XPS への出力を許可する**  

  - **[未構成]** ("*既定値*")
  - **はい** - XPS への出力を許可します。

- **Windows ネットワーク分離ポリシー**  
  
  - **[未構成]** ("*既定値*")
  - **はい** - Windows ネットワーク分離ポリシーを構成します。  
  
  *[はい]* に設定すると、つぎの設定を構成できます。

  - **IP 範囲**  
    ドロップダウンを展開し、 **[追加]** を選択してから、*開始アドレス*、*終了アドレス*の順に指定します。

  - **クラウド リソース**  
    ドロップダウンを展開し、 **[追加]** を選択してから、*IP アドレスまたは FQDN* および*プロキシ*を指定します。

  - **ネットワーク ドメイン**  
   ドロップダウンを展開し、 **[追加]** を選択してから、*ネットワーク ドメイン*を指定します。

  - **プロキシ サーバー**  
    ドロップダウンを展開し、 **[追加]** を選択してから、*プロキシ サーバー*を指定します。

  - **内部プロキシ サーバー**  
    ドロップダウンを展開し、 **[追加]** を選択してから、*内部プロキシ サーバー*を指定します。

  - **ニュートラル リソース**  
    ドロップダウンを展開し、 **[追加]** を選択してから、*ニュートラル リソース*を指定します。

  - **その他のエンタープライズ プロキシ サーバーの自動検出を無効にする**  
    - **[未構成]** ("*既定値*")
    - **はい** - その他のエンタープライズ プロキシ サーバーの自動検出を無効にします。

  - **その他のエンタープライズ IP 範囲の自動検出を無効にする**  
    - **[未構成]** ("*既定値*")
    - **はい** - その他のエンタープライズ IP 範囲の自動検出を無効にします。

## <a name="web-protection-profile"></a>Web 保護プロファイル

### <a name="web-protection"></a>Web 保護

- **ネットワーク保護を有効にする**  
  CSP:[EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **未構成** (*既定値*) - 設定は Windows の既定値に戻され、無効になります。
  - **ユーザー定義**
  - **有効** - システム上のすべてのユーザーを対象にネットワーク保護が有効にされます。
  - **監査モード** - 危険なドメインからユーザーはブロックされず、代わりに Windows イベントが発生します。

- **Require SmartScreen for Microsoft Edge (Microsoft Edge で SmartScreen が必要)**  
  CSP:[Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **はい** - SmartScreen を使用してフィッシング詐欺にあう可能性や悪意のあるソフトウェアからユーザーを保護します。
  - **[未構成]** ("*既定値*")

- **Block malicious site access (悪意のあるサイトへのアクセスをブロックする)**  
  CSP:[Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **はい** - ユーザーが Microsoft Defender SmartScreen フィルターの警告を無視できないようにして、サイトへの移動をブロックします。
  - **[未構成]** ("*既定値*")

- **Block unverified file download (確認されていないファイルのダウンロードをブロックする)**  
  CSP:[Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **はい** - ユーザーが Microsoft Defender SmartScreen フィルターの警告を無視できないようにして、確認されていないファイルをダウンロードできないようにします。
  - **[未構成]** ("*既定値*")

## <a name="application-control-profile"></a>アプリケーションの制御プロファイル

### <a name="microsoft-defender-application-control"></a>Microsoft Defender アプリケーション制御

- **App Locker アプリケーション コントロール**  
  - **[未構成]** ("*既定値*")
  - **コンポーネントとストア アプリの適用**
  - **コンポーネントとストア アプリの監査**
  - **コンポーネント、ストア アプリ、Smartlocker の適用**
  - **コンポーネント、ストア アプリ、Smartlocker の監査** CSP:[AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

- **ユーザーが SmartScreen 警告を無視できないようにする**  
  CSP:[SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **[未構成]** ("*既定*") - ユーザーはファイルや悪意のあるアプリに関する SmartScreen の警告を無視できます。
  - **[はい]** - SmartScreen は有効になっており、ファイルや悪意のあるアプリに関する警告をユーザーは無視できません。

- **Windows SmartScreen を有効にする**  
  CSP:[SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、SmartScreen が有効になりますが、ユーザーはこの設定を変更できます。 SmartScreen を無効にするには、カスタム URI を使用します。
  - **はい** - SmartScreen の使用をすべてのユーザーに強制します。

## <a name="attack-surface-reduction-rules-profile"></a>攻撃の回避規則プロファイル

### <a name="attack-surface-reduction-rules"></a>攻撃の回避規則

- **Windows ローカル セキュリティ機関サブシステム (lsass.exe) からの資格情報の盗難をブロックする**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874499)

  この攻撃の回避 (ASR) 規則は、次の GUID を使用して制御されます。9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ユーザー定義**
  - **有効化** - lsass.exe を介して資格情報を盗もうとする試みがブロックされます。
  - **監査モード** - 危険なドメインからユーザーはブロックされず、代わりに Windows イベントが発生します。

- **Adobe Reader による子プロセスの作成をブロックする**  
  [攻撃の回避規則を使用した攻撃の回避](https://go.microsoft.com/fwlink/?linkid=853979)
  
  この ASR 規則は、次の GUID を使用して制御されます。7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **未構成** (*既定値*) - Windows の既定値が復元され、子プロセスの作成がブロックされなくなります。
  - **ユーザー定義**
  - **有効化** - Adobe Reader による子プロセスの作成がブロックされます。
  - **監査モード** - 子プロセスをブロックするのでなく、Windows イベントが発生します。

- **Office アプリケーションによる他のプロセスへのコード挿入をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872974)

  この ASR 規則は、次の GUID を使用して制御されます。75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - Office アプリケーションによる他のプロセスへのコード挿入がブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **Office アプリケーションによる実行可能なコンテンツの作成をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872975)

  この ASR 規則は、次の GUID を使用して制御されます。3B576869-A4EC-4529-8536-B80A7769E899
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - Office アプリケーションによる実行可能なコンテンツの作成がブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **すべての Office アプリケーションによる子プロセスの作成をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872976)

  この ASR 規則は、次の GUID を使用して制御されます。D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - Office アプリケーションによる子プロセスの作成がブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **Office マクロからの Win32 API 呼び出しをブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872977)

  この ASR 規則は、次の GUID を使用して制御されます。92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - Office マクロの Win32 API 呼び出しの使用がブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **Office 通信アプリによる子プロセスの作成をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874499)  

  この ASR 規則は、次の GUID を使用して制御されます。26190899-1602-49e8-8b27-eb1d0a1ce869。
  - **未構成** (*既定値*) - Windows の既定値が復元され、子プロセスの作成がブロックされなくなります。
  - **ユーザー定義**
  - **有効化** - Office 通信アプリケーションによる子プロセスの作成がブロックされます。
  - **監査モード** - 子プロセスをブロックするのでなく、Windows イベントが発生します。

- **難読化されている可能性のあるスクリプト (js/vbs/ps) の実行をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872978)

  この ASR 規則は、次の GUID を使用して制御されます。5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - 難読化されたスクリプトの実行が Defender によってブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **JavaScript または VBScript による、ダウンロードされた実行可能なコンテンツの起動をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872979)

   この ASR 規則は、次の GUID を使用して制御されます。D3E037E1-3EB8-44C8-A917-57927947596D
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - インターネットからダウンロードされた JavaScript または VBScript ファイルの実行が Defender によってブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **PSExec および WMI コマンドから開始されるプロセス作成をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874500)

  この ASR 規則は、次の GUID を使用して制御されます: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - PSExec または WMI コマンドによるプロセスの作成がブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **USB から実行された信頼されていない署名なしのプロセスをブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874502)

  この ASR 規則は、次の GUID を使用して制御されます: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - USB ドライブから実行される信頼されていないプロセスおよび無署名プロセスがブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **普及、経過時間、または信頼されたリストの条件を満たしていない実行可能ファイルの実行をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874503)

  この ASR 規則は、次の GUID を使用して制御されます。01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック**
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **電子メールおよび Web メールのクライアントからの実行可能なコンテンツをブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872980)

  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ブロック** - 電子メールおよび Web メールのクライアントからダウンロードした実行可能なコンテンツがブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **ランサムウェアに対して高度な保護を使用する**  
   [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874504)

  この ASR 規則は、次の GUID を使用して制御されます: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **未構成** (*既定値*) - 設定が Windows の既定値に戻され、オフになります。
  - **ユーザー定義**
  - **有効化**
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **フォルダーの保護を有効にする**  
  CSP:[EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **未構成** (*既定値*) - この設定は既定値に戻され、読み取りも書き込みもブロックされません。
  - **有効化** - 信頼できないアプリの場合、保護されたフォルダー内のファイルの変更または削除、あるいはディスク セクターへの書き込みの試行が Defender によってブロックされます。 どのアプリケーションが信頼できるかは、Defender によって自動的に判断されます。 あるいは、信頼できるアプリケーションの一覧を独自に定義することもできます。
  - **監査モード** - 信頼できないアプリケーションが制御対象のフォルダーにアクセスしたとき、Windows イベントが発生しますが、ブロックは適用されません。
  - **ディスク変更のブロック** - ディスク セクターへの書き込みの試行のみがブロックされます。
  - **ディスクの変更の監査** - ディスク セクターへの書き込みの試行をブロックするのではなく、Windows イベントが発生します。
  
- **攻撃の回避規則から除外されたファイルとフォルダー**  
  CSP:[AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  ドロップダウンを展開してから、 **[追加]** を選択して、攻撃の回避規則から除外するファイルまたはフォルダーへの**パス**を定義します。

## <a name="device-control-profile"></a>デバイス制御プロファイル

### <a name="device-control"></a>デバイスの制御

- **Hardware device installation by device identifiers (デバイス識別子を使用してハードウェア デバイスをインストールする)**  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  この設定を使用すると、Windows によるインストールが禁止されているデバイスのプラグ アンド プレイ ハードウェア ID と互換 ID の一覧を指定できます。 このポリシー設定は、Windows がデバイスをインストールできるようにするその他のポリシー設定よりも優先されます。  リモート デスクトップ サーバーでこのポリシー設定を有効にした場合、ポリシー設定は、リモート デスクトップ クライアントからリモート デスクトップ サーバーへの指定されたデバイスのリダイレクトに影響します。

  - **未構成**
  - **ハードウェア デバイスのインストールを許可する** - 他のポリシー設定によって許可または禁止されているとおりに、デバイスをインストールおよび更新することができます。
  - **ハードウェア デバイスのインストールをブロックする** (*既定値*) - ご自分で定義したリスト内に表示されたハードウェア ID または互換性 ID を持つデバイスを Windows でインストールすることはできません。

  *[ハードウェア デバイスのインストールをブロックする]* に設定すると、次の設定を構成できます。

  - **Remove matching hardware devices (一致するハードウェア デバイスを削除する)**

    この設定は *[Hardware device installation by device identifiers]\(デバイス識別子でハードウェア デバイスをインストールする\)* が *[Block hardware device installation]\(ハードウェア デバイスのインストールをブロックする\)* に設定されているときのみ使用できます。
    - **あり**
    - **未構成**

  - **Hardware device identifiers that are blocked (ブロックされているハードウェア デバイス識別子)**  

    この設定は *[Hardware device installation by device identifiers]\(デバイス識別子でハードウェア デバイスをインストールする\)* が *[Block hardware device installation]\(ハードウェア デバイスのインストールをブロックする\)* に設定されているときのみ使用できます。

    **[追加]** を選択して、ブロックするハードウェア デバイスの識別子を指定します。

- **Hardware device installation by setup classes (セットアップ クラスを使用してハードウェア デバイスをインストールする)**  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  このポリシー設定を使用すると、Windows によるインストールが禁止されているデバイス ドライバーのデバイス セットアップ クラス GUID (グローバル一意識別子) の一覧を指定できます。 このポリシー設定は、Windows がデバイスをインストールできるようにするその他のポリシー設定よりも優先されます。 リモート デスクトップ サーバーでこのポリシー設定を有効にした場合、ポリシー設定は、リモート デスクトップ クライアントからリモート デスクトップ サーバーへの指定されたデバイスのリダイレクトに影響します。

  - **未構成**
  - **ハードウェア デバイスのインストールを許可する** - Windows では他のポリシー設定によって許可または禁止されているとおりに、デバイスをインストールおよび更新することができます。
  - **ハードウェア デバイスのインストールをブロックする** (*既定値*) - ご自分で定義したリスト内に表示されたセットアップ クラス GUID を持つデバイスを Windows でインストールすることはできません。

  *[ハードウェア デバイスのインストールをブロックする]* に設定すると、 *[一致するハードウェア デバイスを削除する]* および *[ブロックされているハードウェア デバイス ID]* を構成できるようになります。

  - **Remove matching hardware devices (一致するハードウェア デバイスを削除する)**

    この設定は *[Hardware device installation by device identifiers]\(デバイス識別子でハードウェア デバイスをインストールする\)* が *[Block hardware device installation]\(ハードウェア デバイスのインストールをブロックする\)* に設定されているときのみ使用できます。
    - **あり**
    - **未構成**

  - **Hardware device identifiers that are blocked (ブロックされているハードウェア デバイス識別子)**

    この設定は *[Hardware device installation by device identifiers]\(デバイス識別子でハードウェア デバイスをインストールする\)* が *[Block hardware device installation]\(ハードウェア デバイスのインストールをブロックする\)* に設定されているときのみ使用できます。

    **[追加]** を選択して、ブロックするハードウェア デバイスの識別子を指定します。

- **フル スキャン中にリムーバブル ドライブをスキャンする**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **未構成** (*既定値*) - 設定はクライアントの既定値 (リムーバブル ドライブをスキャン) に戻されますが、ユーザーはこのスキャンを無効にすることができます。
  - **はい** - フル スキャン中に、リムーバブル ドライブ (USB フラッシュ ドライブなど) がスキャンされます。

- **Block direct memory access (ダイレクト メモリ アクセスをブロックする)**  
  CSP:[DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)

  このポリシー設定は、BitLocker またはデバイスの暗号化が有効な場合にのみ適用されます。

  - **[未構成]** ("*既定値*")
  - **はい** - ユーザーが Windows にログインするまで、ホット プラグ可能なすべての PCI ダウンストリーム ポートへの直接メモリ アクセス (DMA) が禁止されます。 ユーザーがログインすると、ホスト プラグ PCI ポートに接続されている PCI デバイスが Windows によって列挙されます。 ユーザーがコンピューターをロックするたびに、ユーザーが再ログインするまで、子デバイスが接続されていないホット プラグ PCI ポートで DMA がブロックされます。 コンピューターのロックが解除されたときに既に列挙されていたデバイスは、取り外されるまで機能を維持します。

- **Kernel DMA Protection と互換性のない外部デバイスの列挙**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  このポリシーでは、外部 DMA 対応デバイスに対して追加のセキュリティを提供することができます。 これにより、DMA の再マッピング/デバイス メモリの分離およびサンドボックス化と互換性のない外部 DMA 対応デバイスの列挙をより詳細に制御できます。

  このポリシーが有効になるのは、Kernel DMA Protection がシステム ファームウェアによってサポートされていて、それによって有効にされた場合のみです。 カーネル DMA 保護は、製造時にシステムによってサポートされる必要があるプラットフォーム機能です。 システムで Kernel DMA Protection がサポートされているかどうかを確認するには、MSINFO32.exe の概要ページにある Kernel DMA Protection フィールドを調べます。

  - **未構成** - (*既定値*)
  - **すべてブロックする**
  - **すべて許可**

- **Bluetooth 接続をブロックする**  
  CSP:[Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **[未構成]** ("*既定値*")
  - **はい** - デバイスとの Bluetooth 接続をブロックします。

- **Bluetooth の検出機能をブロックする**  
  CSP:[Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **[未構成]** ("*既定値*")
  - **はい** - このデバイスは他の Bluetooth 対応デバイスで検出されなくなります。

- **Bluetooth の事前ペアリングをブロックする**  
  CSP:[Bluetooth/AllowPrepairing](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

  - **[未構成]** ("*既定値*")
  - **はい** - 特定の Bluetooth デバイスがホスト デバイスと自動的にペアリングできなくなります。

- **Bluetooth 広告をブロックする**  
  CSP:[Bluetooth/AllowAdvertising](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

  - **[未構成]** ("*既定値*")
  - **はい** - デバイスは Bluetooth 広告を送信できなくなります。  

- **Bluetooth の近位接続をブロックする**  
  CSP:[Bluetooth/AllowPromptedProximalConnections](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections) ユーザーがクイック ペアリングやその他の近接通信ベースのシナリオを利用することをブロックします

  - **[未構成]** ("*既定値*")
  - **はい** - デバイス ユーザーがクイック ペアリングやその他の近接通信ベースのシナリオを使用できないようになります。  

  [Bluetooth/AllowPromptedProximalConnections CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Bluetooth を使用できるサービス**  
  CSP:[Bluetooth/ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)。  
  サービスの一覧の詳細については、[ServicesAllowedList 使用ガイド](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) ページを参照してください

  - **追加** - 許可される Bluetooth のサービスとプロファイルの一覧を 16 進数文字列 (例: `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`) で指定します。
  - **インポート** - Bluetooth のサービスとプロファイルの一覧 (`{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}` のような 16 進数文字) が含まれる .csv ファイルをインポートします。

## <a name="exploit-protection-profile"></a>悪用に対する保護プロファイル

### <a name="exploit-protection"></a>悪用に対する保護

- **[XML をアップロードする]**  
  CSP:[ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  IT 管理者が、組織内のすべてのデバイスに対して、目的のシステムとアプリケーションの軽減策オプションを表す構成をプッシュできるようにします。 この構成は XML ファイルで表されます。 [悪用に対する保護] は、拡散と感染のためにエクスプロイトを使用するマルウェアからデバイスを保護するのに役立ちます。 Windows セキュリティ アプリまたは PowerShell を使用して、一連の軽減策 (構成と呼ばれます) を作成します。 次に、この構成を XML ファイルとしてエクスポートし、ネットワーク上の複数のマシンと共有して、すべてのマシンに同じ軽減策設定が適用されるようにすることができます。 既存の EMET 構成 XML ファイルを変換して Exploit Protection 構成 XML にインポートすることもできます。

  **[XML ファイルの選択]** を選択し、アップロードする XML ファイルを指定してから、 **[選択]** をクリックします。
  - **[未構成]** ("*既定値*")
  - **あり**

- **ユーザーが Exploit Guard 保護インターフェイスを編集することをブロックする**  
  CSP:[DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **未構成** (*既定値*) - ローカル ユーザーは悪用に対する保護設定の領域に対して変更を加えることができます。
  - **はい** - Microsoft Defender Security Center 内の悪用に対する保護設定の領域に対してユーザーは変更を加えることができなくなります。

## <a name="next-steps"></a>次のステップ

[ASR のエンドポイント セキュリティ ポリシー](../protect/endpoint-security-asr-policy.md)
