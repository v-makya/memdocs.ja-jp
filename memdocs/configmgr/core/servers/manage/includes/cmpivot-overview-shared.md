---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 8e95fce122a3e153f2aa391dcd5e40439f8e5820
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704091"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>クエリ

クエリは、用語検索、傾向の識別、パターン分析、データに基づくその他の多くの分析情報の提供に使用することができます。 CMPivot では、表形式の式ステートメントに [Azure Log Analytics](/azure/kusto/query) データ フロー モデルのサブセットを使用します。 表形式の式ステートメントは、通常、クライアント エンティティと表形式のデータ演算子 (フィルターやプロジェクションなど) を組み合わせた構造をしています。 組み合わせはパイプ文字 (|) で表され、表形式のデータの流れを視覚的に左から右に表現する整然とした形式をステートメントに与えています。 各演算子は、"パイプから" の表形式のデータセットと、演算子の本体からの追加入力 (他の表形式のデータ セットを含む) を受け取り、次に続く演算子に表形式のデータ セットを出力します (`entity | operator1 | operator2 | ...`)。

次の例では、エンティティは `CCMRecentlyUsedApplications` (最近使用したアプリケーションへの参照) であり、演算子は where (レコードごとの述語に従ってレコードをフィルター処理して入力から除外する演算子) です。

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>エンティティ

エンティティは、クライアントからのクエリ実行対象とすることができるオブジェクトです。 現在、次のエンティティがサポートされています。


|エンティティ|[説明]|
|---|---|
|AadStatus|Azure Active Directory の状態|
|Administrators|ローカルの Administrators グループのメンバー|
|AppCrash|最新のアプリケーションのクラッシュ レポート|
|AppVClientApplication|AppV クライアント アプリケーション|
|AppVClientPackage|AppV クライアント パッケージ|
|AutoStartSoftware|オペレーティング システムと同時に、またはその直後に自動で起動するソフトウェア|
|BaseBoard|BaseBoard|
|バッテリ|バッテリ|
|Bios|システムの BIOS 情報|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|BitLocker 暗号化の詳細|
|BitLockerPolicy|BitLocker ポリシー|
|BootConfiguration|ブート構成|
|BrowserHelperObject|ブラウザー ヘルパー オブジェクト|
|BrowserUsage|ブラウザー使用状況|
|CcmLog()|Ccm ログ ファイルからの 24 時間以内 (既定) の行|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|最近使用したアプリケーション|
|CCMWebAppInstallInfo|Web アプリケーション|
|CDROM|CD-ROM ドライブ|
|ClientEvents|クライアント イベント|
|ComputerSystem|コンピューター システム|
|ComputerSystemEx|コンピューター システム Ex|
|ComputerSystemProduct|コンピューター システム製品|
|ConnectedDevice|接続済みデバイス|
|接続|デバイスに着信する、またはデバイスから発信する、アクティブな TCP 接続|
|デスクトップ|デスクトップ|
|DesktopMonitor|デスクトップ モニター|
|デバイス|デバイスに関する基本情報|
|ディスク|Windows を実行するコンピューター システム上のローカル記憶装置情報|
|DMA|DMA|
|DMAChannel|DMA チャネル|
|DriverVxD|ドライバー - VxD|
|EmbeddedDeviceInformation|埋め込みデバイス情報|
|環境|環境|
|EPStatus|コンピューター上のマルウェア対策ソフトウェアの状態|
|EventLog()|イベント ログからの 24 時間以内 (既定) のイベント|
|File()|特定のファイルに関する情報|
|FileShare|アクティブなファイル共有の情報|
|ファームウェア|ファームウェア|
|IDEController|IDE コントローラー|
|InstalledExecutable|インストール済み実行可能ファイル|
|InstalledSoftware|デバイスにインストールされているアプリケーション|
|IPConfig|使用可能なインターフェイス、IP アドレス、DNS サーバーなどのネットワーク構成を取得|
|IRQTable|IRQ テーブル|
|キーボード|キーボード|
|LoadOrderGroup|読み込み順序グループ|
|LogicalDisk|論理ディスク|
|MDMDevDetail|デバイス情報|
|メモリ|メモリ|
|モデム|モデム|
|マザーボード|マザーボード|
|NetworkAdapter|ネットワーク アダプター|
|NetworkAdapterConfiguration|ネットワーク アダプター構成|
|NetworkClient|ネットワーク クライアント|
|NetworkLoginProfile|ネットワーク ログイン プロファイル|
|NTEventlogFile|NT イベントログ ファイル|
|Office365ProPlusConfigurations|Office 365 ProPlus の構成|
|OfficeAddin|Office アドイン|
|OfficeClientMetric|Office クライアント メトリック|
|OfficeDeviceSummary|Office デバイス概要|
|OfficeDocumentMetric|Office ドキュメントのメトリック|
|OfficeDocumentSolution|Office ドキュメント ソリューション|
|OfficeMacroError|Office マクロ エラー|
|OfficeProductInfo|Office 製品情報|
|OfficeVbaRuleViolation|Office VBA ルール違反|
|OfficeVbaSummary|Office VBA スキャンのサマリー|
|OperatingSystem|オペレーティング システム|
|OperatingSystemEx|オペレーティング システム Ex|
|OperatingSystemRecoveryConfiguration|オペレーティング システム復旧構成|
|OptionalFeature|オプション機能|
|OS|オペレーティング システムに関する基本情報|
|PageFileSetting|ページ ファイル設定|
|ParallelPort|パラレル ポート|
|パーティション|ディスク パーティション|
|PCMCIAController|PCMCIA コントローラー|
|物理ディスク|物理ディスク|
|PhysicalMemory|物理メモリ|
|PNPDEVICEDRIVER|PNP デバイス ドライバー|
|PointingDevice|ポインティング デバイス|
|PortableBattery|ポータブル バッテリー|
|ポート|ポート|
|PowerCapabilities|電源機能|
|PowerClientOptOutSettings|電源管理の除外設定|
|PowerConfigurations|電源構成|
|PowerManagementDaily|電源管理の日次データ|
|PowerManagementInsomniaReasons|電源管理不可の理由|
|PowerManagementMonthly|電源管理の月次データ|
|PowerSettings|電源設定|
|PrinterConfiguration|プリンター構成|
|PrinterDevice|プリンター デバイス|
|PrintJobs|印刷ジョブ|
|プロセス|オペレーティング システム上のプロセス|
|ProcessModule()|指定されたプロセスによって読み込まれたモジュール|
|プロセッサ|プロセッサ|
|ProtectedVolumeInformation|保護されたボリュームの情報|
|プロトコル|プロトコル|
|QuickFixEngineering|クイック修正エンジニアリング|
|SCSIController|SCSI コントローラー|
|SerialPortConfiguration|シリアル ポート構成|
|SerialPorts|シリアル ポート|
|ServerFeature|サーバー機能|
|サービス|Windows を実行するコンピューター システム上のサービス|
|サービス|サービス|
|共有|共有|
|SMBConfig|デバイスの SMB 構成|
|SMSAdvancedClientPorts|Configuration Manager クライアントのポート|
|SMSAdvancedClientSSLConfigurations|Configuration Manager クライアントの SSL 構成|
|SMSAdvancedClientState|Configuration Manager クライアントの状態|
|SMSDefaultBrowser|既定のブラウザー|
|SMSSoftwareTag|ソフトウェア タグ|
|SMSWindows8Application|Windows アプリ|
|SMSWindows8ApplicationUserInfo|Windows アプリのユーザー情報|
|SoftwareShortcut|ソフトウェア ショートカット|
|SoftwareUpdate|適用可能であるものの、デバイスにインストールされていないソフトウェア更新プログラム|
|SoundDevices|サウンド デバイス|
|SWLicensingProduct|ソフトウェア ライセンス製品|
|SWLicensingService|ソフトウェア ライセンス サービス|
|SystemAccount|システム アカウント|
|SystemBootData|システム ブート データ|
|SystemBootSummary|システム ブート概要|
|SystemConsoleUsage|システム コンソール使用状況|
|SystemConsoleUser|システム コンソール ユーザー|
|SystemDevices|システム デバイス|
|SystemDrivers|システム ドライバー|
|SystemEnclosure|システム格納装置|
|TapeDrive|テープ ドライブ|
|TimeZone|タイム ゾーン|
|TPM|TPM|
|TPMStatus|TPM の状態|
|TSIssuedLicense|TS により発行されたライセンス|
|TSLicenseKeyPack|TS ライセンス キー パック|
|UninterruptiblePowerSupply|無停電電源装置|
|USBController|USB コントローラー|
|USBDevice|USB デバイス|
|ユーザー|デバイスにアクティブに接続しているユーザー アカウント|
|USMFolderRedirectionHealth|フォルダー リダイレクトの正常性|
|USMUserProfile|ユーザー プロファイルの正常性|
|VideoController|ビデオ コントローラー|
|VirtualMachine|仮想マシン|
|VirtualMachine64|仮想マシン (64)|
|ボリューム|ボリューム|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Windows Update エージェントのバージョン|
|WinEvent()|Windows イベント ログからの 24 時間以内 (既定) のイベント|
|WriteFilterState|書き込みフィルターの状態|

## <a name="table-operators"></a>テーブル演算子

テーブル演算子は、データ ストリームのフィルター処理、要約、変換に使用できます。 現在、次の演算子がサポートされています。

|テーブル演算子|[説明]|
|---|---|
|count|そのレコード数を含む単一のレコードを持つテーブルを返します|
|distinct|入力テーブルの指定された列の個別の組み合わせを含むテーブルを生成します|
|join|同じデバイスの行を照合して、2 つのテーブルの行をマージして新しいテーブルを形成します|
|order by|入力テーブルの行の順序を 1 つ以上の列で並べ替えます|
|project|組み込む列を選択し、名前変更または削除して、新しい計算列を挿入します|
|summarize|入力テーブルの内容を集計するテーブルを生成します|
|take|指定された数までの行を返します|
|top|指定された列で並べ替えられた最初の N 個のレコードを返します|
|where|テーブルをフィルター処理して、述語を満たす行のサブセットを取得します|

## <a name="scalar-operators"></a>スカラー演算子

次の表で演算子の概要を示します。

|演算子|[説明]|例
|---|---|---|
|==|等しい|`1 == 1, 'aBc' == 'AbC'`|
|!=|等しくない|`1 != 2, 'abc' != 'abcd'`|
|< |未満|`1 < 2, 'abc' < 'DEF'`|
|> |より大きい|`2 > 1, 'xyz' > 'XYZ'`|
|<=|以下|`1 <= 2, 'abc' <= 'abc'`|
|>=|以上|`2 >= 1, 'abc' >= 'ABC'`|
|+|追加|`2 + 1, now() + 1d`|
|-|減算|`2 - 1, now() - 1h`|
|*|乗算|`2 * 2`|
|/|除算|`2 / 1`|
|%|剰余|`2 % 1`|
|like|左側 (LHS) に右側 (RHS) との一致が含まれています|`'abc' like '%B%'`|
|!like|LHS には RHS に対する一致が含まれていません|`'abc' !like '_d_'`|
|次の値を含む|RHS は LHS のサブシーケンスとして出現します|`'abc' contains 'b'`|
|!contains|RHS は LHS の中に出現しません|`'team' !contains 'i'`|
|startswith|RHS は LHS の冒頭のサブシーケンスです|`'team' startswith 'tea'`|
|!startswith|RHS は LHS の冒頭のサブシーケンスではありません|`'abc' !startswith 'bc'`|
|endswith|RHS は LHS の末尾のサブシーケンスです|`'abc' endswith 'bc'`|
|!endswith|RHS は LHS の末尾のサブシーケンスではありません|`'abc' !endswith 'a'`|
|および|RHS および LHS が真である場合にのみ真になります|`(1 == 1) and (2 == 2)`|
|または|RHS または LHS が真である場合にのみ真になります|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>集計関数

集計関数を集計テーブル演算子と共に使用すると、集計値を計算することができます。 現在、次の集計関数がサポートされています。

|関数|[説明]|
|---|---|
|avg()|グループ全体の値の平均を返します|
|count()|概要作成グループごとのレコード数を返します|
|countif()|述語の評価の結果が true である行数を返します|
|dcount()|グループ内の個別の値の数を返します|
|max()|グループ全体の最大値を返します|
|min()|グループ全体の最小値を返します|
|percentile()|式で定義された母集団の指定したランクに最も近いパーセンタイルの推定値を返します|
|sum()|グループ全体の値の合計を返します|
|sumif()|述語が True に評価される式の合計を返します|

## <a name="scalar-functions"></a>スカラー関数

スカラー関数は、式で使用できます。 現在、次のスカラー関数がサポートされています。

|関数|[説明]|
|---|---|
|ago()|指定された期間を現在の UTC 時刻から減算します|
|bin()|指定のビンのサイズの倍数の日時の数に値を切り捨てます|
|case()|述語の一覧を評価し、その述語を満たす最初の結果式を返します|
|datetime_add()|指定した datepart に対して指定した量を乗算し、指定した datetime に追加して、新しい datetime を計算します|
|datetime_diff()|2 つの日付時刻値の差を計算します|
|iif()|最初の引数を評価し、述語が true または false に評価されるかどうかに応じて、2 番目 (true) または 3 番目 (false) の引数の値を返します|
|indexof()|関数は、入力文字列内で指定された文字列の最初の出現の 0 から始まるインデックスを報告します|
|isnotnull()|唯一の引数を評価し、引数が null 以外の値と評価されるかどうかを示すブール値を返します|
|isnull()|唯一の引数を評価し、引数が null 値と評価されるかどうかを示すブール値を返します|
|now()|現在の UTC 時刻を返します|
|strcat()|1 から 64 の引数を連結します|
|strlen()|入力文字列の文字の長さを返します|
|substring()|いくつかのインデックスから始まり文字列で終わるソース文字列からサブ文字列を抽出します|
|tostring()|入力を文字列形式に変換します|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Configuration Manager からの CMPivot 用の追加のエンティティ、演算子、および関数

> [!Important]
> これらの項目は、CMPivot を Microsoft エンドポイント マネージャー管理センターから実行する場合はサポートされません。

|Type|項目|[説明]|
|--|--|---|
|エンティティ|AccountSID|アカウント SID|
|エンティティ|FileContent()|特定のファイルのコンテンツ|
|エンティティ|NAPClient|NAP クライアント|
|エンティティ|NAPSystemHealthAgent|NAP システム正常性エージェント|
|エンティティ|Registry()|特定のレジストリ キーのすべての値<!--7371183-->|
|テーブル演算子|render|結果をグラフィカル出力としてレンダリングします|