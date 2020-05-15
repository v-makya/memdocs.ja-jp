---
title: データ共有を有効にする
titleSuffix: Configuration Manager
description: Desktop Analytics で診断データを共有するためのリファレンスガイド。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0811c695acba4859bf32de535a28ea55cf8eee07
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268744"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Desktop Analytics のためにデータ共有を有効にする

デバイスを Desktop Analytics に登録するには、診断データを Microsoft に送信する必要があります。 お使いの環境でプロキシ サーバーが使用されている場合は、この情報を使用してプロキシを構成します。

## <a name="diagnostic-data-levels"></a>診断データのレベル

![Desktop Analytics の診断データ レベルの図](media/diagnostic-data-levels.png)

Configuration Manager を Desktop Analytics と統合したら、デバイスでの診断データ レベルの管理にもそれを使用します。 最良のエクスペリエンスを実現するには、Configuration Manager をお使いください。

> [!Important]  
> ほとんどの場合、Configuration Manager だけを使ってこれらの設定を構成します。 これらの設定は、ドメイン グループ ポリシー オブジェクトでは適用しないでください。 詳細については、「[競合の解決](enroll-devices.md#conflict-resolution)」をご覧ください。

Desktop Analytics の基本的な機能は、**基本**[診断データのレベル](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels)で動作します。 Configuration Manager で**拡張 (制限付き)** レベルを構成しない場合、Desktop Analytics の次の機能は利用できません。

- アプリの使用状況
- [その他のアプリの分析情報](compat-assessment.md#additional-insights)
- 展開状態データ
- 正常性監視データ

Desktop Analytics で**拡張 (制限付き)** 診断データレベルを有効にして、そこから得られる利点を最大限に高めることをお勧めします。

> [!Tip]
> Configuration Manager での**拡張 (制限付き)** の設定は、Windows 10 バージョン 1709 以降を実行しているデバイスで利用可能な "**拡張診断データを Windows Analytics で必要とされる最小限のものに限定します**" ポリシーと同じ設定です。
>
> Windows 10 バージョン 1703 以前、Windows 8.1、または Windows 7 が実行されているデバイスには、このポリシー設定はありません。 Configuration Manager で**拡張 (制限付き)** の設定を構成すると、これらのデバイスは**基本**レベルに戻されます。
>
> Windows 10 バージョン 1709 が実行されているデバイスには、このポリシー設定があります。 ただし、Configuration Manager で**拡張 (制限付き)** の設定を構成すると、これらのデバイスも**基本**レベルに戻されます。

**拡張 (制限付き)** で Microsoft と共有される診断データについて詳しくは、[Windows 10 の拡張診断データのイベントとフィールド](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)に関する記事をご覧ください。

> [!Important]
> Microsoft は、お客様のプライバシーを管理するためのツールとリソースを提供するために強力なコミットメントを行っています。 そのため、Desktop Analytics では Windows 8.1 デバイスがサポートされていますが、ヨーロッパの国 (EEA およびスイス) に存在する Windows 8.1 デバイスからは Windows 診断データは収集されません。

詳細については、[Desktop Analytics のプライバシー](privacy.md)に関する記事を参照してください。

次の記事も、Windows の診断データ レベルをよく理解するためのよいリソースです。

- [IT 意思決定者向けの Windows 10 と GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> 拡張診断データを制限するように構成されたクライアントでは、最初のフルスキャンで Microsoft クラウドに約 2 MB のデータが送信されます。 毎日のデルタは、1 日あたり 250 から 400 KB で変動します。
>
> 毎日のデルタ スキャンは、午前 3:00 (デバイスのローカル時刻) に行われます。 一部のイベントは、1 日で最初に使用可能な時刻に送信されます。 これらの時刻は構成できません。
>
> 詳しくは、「[組織内の Windows 診断データの構成](https://aka.ms/enterprisetelemetry)」をご覧ください。  

## <a name="endpoints"></a>エンドポイント

データ共有を有効にするには、以下のインターネット エンドポイントを許可するようにプロキシ サーバーを構成します。

> [!Important]  
> プライバシーとデータの整合性を確保するため、診断データ エンドポイントとの通信時に、Windows によって Microsoft SSL 証明書がチェックされます (証明書のピン留め)。 SSL を傍受および検査することはできません。 Desktop Analytics を使用するには、以下のエンドポイントを SSL の検査から除外します。<!-- BUG 4647542 -->

バージョン 2002 以降、Configuration Manager サイトがクラウド サービスに必要なエンドポイントへの接続に失敗すると、クリティカルなステータス メッセージ ID 11488 が生成されます。 サービスに接続できない場合、SMS_SERVICE_CONNECTOR コンポーネントのステータスがクリティカルに変わります。 Configuration Manager コンソールの[コンポーネントのステータス](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) ノードに、詳細なステータスが表示されます。<!-- 5566763 -->

> [!NOTE]
> Microsoft IP アドレス範囲の詳細については、「[Microsoft Public IP Space (Microsoft のパブリック IP スペース)](https://www.microsoft.com/download/details.aspx?id=53602)」を参照してください。 これらのアドレスは定期的に更新されます。 サービス別に細かく分かれておらず、これらの範囲内の任意の IP アドレスを使用できます。

### <a name="server-connectivity-endpoints"></a>サーバー接続のエンドポイント

サービス接続ポイントでは、次のエンドポイントと通信する必要があります。

| エンドポイント  | 関数  |
|-----------|-----------|
| `https://aka.ms` | サービスを探すために使用されます |
| `https://graph.windows.net` | 階層を (Configuration Manager サーバー ロール上の) Desktop Analytics にアタッチするときに、CommercialId などの設定を自動的に取得するために使用されます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。 |
| `https://*.manage.microsoft.com` | デバイス コレクションのメンバーシップ、展開計画、およびデバイスの準備状態を (Configuration Manager サーバー ロール上の) Desktop Analytics と同期するために使用されます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。 |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>ユーザー エクスペリエンスと診断コンポーネントのエンドポイント

クライアント デバイスでは、次のエンドポイントと通信する必要があります。

| エンドポイント  | 関数  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | 接続されたユーザー エクスペリエンスと診断コンポーネントのエンドポイント。 Windows 10 バージョン 1809 以降が実行されているデバイス、または 2018-09 の累積的な更新プログラムがインストールされたバージョン 1803 が実行されているデバイスで使用されます。 |
| `https://v10.events.data.microsoft.com` | 接続されたユーザー エクスペリエンスと診断コンポーネントのエンドポイント。 2018-09 の累積的な更新プログラムがインストールされて "_いない_" Windows 10 バージョン 1803 が実行されているデバイスで使用されます。 |
| `https://v10.vortex-win.data.microsoft.com` | 接続されたユーザー エクスペリエンスと診断コンポーネントのエンドポイント。 Windows 10 バージョン 1709 以前が実行されているデバイスで使用されます。 |
| `https://vortex-win.data.microsoft.com` | 接続されたユーザー エクスペリエンスと診断コンポーネントのエンドポイント。 Windows 7 および Windows 8.1 が実行されているデバイスで使用されます |

### <a name="client-connectivity-endpoints"></a>クライアント接続のエンドポイント

クライアント デバイスでは、次のエンドポイントと通信する必要があります。

| インデックス | エンドポイント  | 関数  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Microsoft にデータを送信するための互換性に関する更新プログラムを有効にします。 |
| 2 | `http://adl.windows.com` | 互換性に関する更新プログラムで Microsoft から最新の互換性データを受信できるようにします。 |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1803 以前で展開の正常性を監視するために必要です。 |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降でデバイス正常性レポートに必要です。 |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [オンライン クラッシュ分析 (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis)。 Windows 10 バージョン 1809 以降でデバイス正常性レポートに必要です。 |
| 12 | `https://oca.telemetry.microsoft.com`  | [オンライン クラッシュ分析 (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis)。 Windows 10 バージョン 1803 以前で展開の正常性を監視するために必要です。 |
| 13 | `https://login.live.com` | Desktop Analytics により信頼性の高いデバイス ID を提供するために必要です。 <br> <br>エンド ユーザーの Microsoft アカウント アクセスを無効にするには、このエンドポイントをブロックするのではなく、ポリシー設定を使用します。 詳しくは、「[エンタープライズでの Microsoft アカウント](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)」をご覧ください。 |
| 14 | `https://v20.events.data.microsoft.com` | 接続されたユーザー エクスペリエンスと診断コンポーネントのエンドポイント。 |

## <a name="proxy-server-authentication"></a>プロキシ サーバー認証

組織でインターネット アクセスにプロキシ サーバー認証を使用している場合は、認証のために診断データがブロックされないようにしてください。 デバイスによるこのデータの送信がプロキシで許可されていない場合、それらのデバイスはデスクトップ分析に表示されません。

### <a name="bypass-recommended"></a>バイパス (推奨)

診断データ エンドポイントへのトラフィックにプロキシ認証が必要ないようにプロキシ サーバーを構成します。 このオプションは、最も包括的な解決策です。 Windows 10 のすべてのバージョンで動作します。  

### <a name="user-proxy-authentication"></a>ユーザー プロキシ認証

サインインしたユーザーのコンテキストをプロキシ認証に使用するようにデバイスを構成します。 この方法では、次の構成が必要です。

- デバイスに、サポートされているバージョンの Windows の最新の品質更新プログラムがインストールされている

- Windows の設定の [ネットワークとインターネット] グループの **[プロキシ設定]** で、ユーザー レベル プロキシ (WinINET プロキシ) を構成します。 従来の [インターネット オプション] コントロール パネルを使用することもできます。

- ユーザーに診断データ エンドポイントにアクセスするためのプロキシ アクセス許可があることを確認します。 このオプションでは、デバイスにプロキシ アクセス許可を持つコンソール ユーザーが存在する必要があるため、この方法をヘッドレス デバイスで使用することはできません。

> [!IMPORTANT]
> ユーザー プロキシ認証の方法は、Microsoft Defender Advanced Threat Protection の使用と互換性がありません。 このような動作が発生するのは、この認証では **DisableEnterpriseAuthProxy** レジストリ キーが `0` に設定されている必要があるのに対し、Microsoft Defender ATP では `1` に設定されている必要があるためです。 詳しくは、[Microsoft Defender ATP でのコンピューターのプロキシとインターネット接続設定の構成](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)に関する記事をご覧ください。

### <a name="device-proxy-authentication"></a>デバイス プロキシ認証

この方法では次のシナリオがサポートされます。

- ユーザーがサインインしない、またはデバイスのユーザーがインターネット アクセスを使用しないヘッドレス デバイス

- Windows 統合認証を使用しない認証プロキシ

- Microsoft Defender Advanced Threat Protection も使用する場合

この方法は、次の構成が必要であるため、最も複雑です。

- デバイスがローカル システム コンテキストで WinHTTP を使用してプロキシ サーバーに接続できることを確認します。 この動作を構成するには、次のいずれかのオプションを使用します。

  - コマンド ライン `netsh winhttp set proxy`

  - Web プロキシ自動検出 (WPAD) プロトコル

  - 透過的プロキシ

  - 次のグループ ポリシー設定を使用して、デバイス全体の WinINET プロキシを構成します。 **(ユーザー別ではなく) コンピューター別にプロキシを設定する** (ProxySettingsPerUser = `1`)

  - ルーティングされた接続、またはネットワーク アドレス変換 (NAT) を使用する接続

- Active Directory のコンピューター アカウントが診断データ エンドポイントにアクセスできるように、プロキシ サーバーを構成します。 この構成では、プロキシ サーバーで Windows 統合認証をサポートする必要があります。  
