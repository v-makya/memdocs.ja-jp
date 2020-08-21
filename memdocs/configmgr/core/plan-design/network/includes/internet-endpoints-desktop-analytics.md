---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 2ae953f6fb01f42c8140407c551ddeb3a9f39c70
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692683"
---
### <a name="server-connectivity-endpoints"></a>サーバー接続のエンドポイント

サービス接続ポイントでは、次のエンドポイントと通信する必要があります。

| エンドポイント  | 関数  |
|-----------|-----------|
| `https://aka.ms` | サービスを探すために使用されます |
| `https://graph.windows.net` | 階層を (Configuration Manager サーバー ロール上の) Desktop Analytics にアタッチするときに、CommercialId などの設定を自動的に取得するために使用されます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。 |
| `https://*.manage.microsoft.com` | デバイス コレクションのメンバーシップ、展開計画、およびデバイスの準備状態を (Configuration Manager サーバー ロール上の) Desktop Analytics と同期するために使用されます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。 |
| `https://dc.services.visualstudio.com` | クラウドに接続されているサービスの正常性に関する分析情報を得るための、オンプレミス サービス コネクタからの診断データ用。<!--7541816--> |

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
| 3 | `https://watson.telemetry.microsoft.com` | [Windows エラー報告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1803 以前で展開の正常性を監視するために必要です。 |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows エラー報告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降でデバイス正常性レポートに必要です。 |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows エラー報告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows エラー報告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows エラー報告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows エラー報告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows エラー報告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows エラー報告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 バージョン 1809 以降で展開の正常性を監視するために必要です。 |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [オンライン クラッシュ分析 (OCA)](/windows/win32/dxtecharts/crash-dump-analysis)。 Windows 10 バージョン 1809 以降でデバイス正常性レポートに必要です。 |
| 12 | `https://oca.telemetry.microsoft.com`  | [オンライン クラッシュ分析 (OCA)](/windows/win32/dxtecharts/crash-dump-analysis)。 Windows 10 バージョン 1803 以前で展開の正常性を監視するために必要です。 |
| 13 | `https://login.live.com` | Desktop Analytics により信頼性の高いデバイス ID を提供するために必要です。 <br> <br>エンド ユーザーの Microsoft アカウント アクセスを無効にするには、このエンドポイントをブロックするのではなく、ポリシー設定を使用します。 詳しくは、「[エンタープライズでの Microsoft アカウント](/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)」をご覧ください。 |
| 14 | `https://v20.events.data.microsoft.com` | 接続されたユーザー エクスペリエンスと診断コンポーネントのエンドポイント。 |