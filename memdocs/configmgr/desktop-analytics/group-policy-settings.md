---
title: グループ ポリシー設定
titleSuffix: Configuration Manager
description: Configuration Manager と Desktop Analytics で使用される Windows のローカル ポリシーとグループ ポリシーの設定について説明します。
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0224d9faecb9ff17afc2af3a57ba222023b5a3d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701740"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Desktop Analytics のグループ ポリシーの設定

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager と Desktop Analytics で使用される Windows のローカル ポリシーとグループ ポリシーの設定について詳しく説明します。

Configuration Manager は、デバイスを Desktop Analytics に登録すると、Windows ポリシーを設定してデバイスを構成します。 ほとんどの場合、Configuration Manager だけを使ってこれらの設定を構成します。

## <a name="windows-settings"></a>Windows の設定

Configuration Manager によって、次のレジストリ キーの一方または両方で Windows ポリシーが設定されます。

- グループ ポリシー オブジェクト (**GPO**): `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- **ローカル** ポリシー設定: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| ポリシー | パス | 適用対象 | 値 |
|--------|------|------------|-------|
| **CommercialId** | ローカル | すべての Windows バージョン | デバイスが Desktop Analytics に表示されるようにするために、ご自分の組織の商用 ID を使用して構成します。 |
| **AllowTelemetry**  | GPO | Windows 10 | 使用する診断データについて、 **[基本]** の場合は `1` を、 **[拡張]** の場合は `2` を、 **[完全]** の場合は `3` を設定します。 Desktop Analytics には、少なくとも基本の診断データが必要です。 Microsoft では、Desktop Analytics で [拡張 (制限付き)] レベルを使うことをお勧めします。 詳しくは、「[組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization)」をご覧ください。 |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10 バージョン 1803 以降 | この設定は、AllowTelemetry 設定が `2` の場合にのみ適用されます。 これにより、Microsoft に送信される拡張診断データのイベントが、Desktop Analytics に必要なイベントのみに制限されます。 詳細については、「[拡張診断データの制限ポリシーを使用して収集される Windows 10 診断データのイベントとフィールド](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields)」をご覧ください。 |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10 バージョン 1803 以降 | デバイスがデバイス名を送信できるようにします。 既定では、デバイス名は Microsoft に送信されません。 デバイス名を送信しない場合、それは Desktop Analytics で "不明" として表示されます。 詳細については、「[デバイス名](enroll-devices.md#device-name)」をご覧ください。 |
| **CommercialDataOptIn** | ローカル | Windows 8.1 以前 | Desktop Analytics では値 `1` が必要です。 詳細については、[Windows 7 での商用データのオプトイン](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\))に関する記事をご覧ください。 |
| **RequestAllAppraiserVersions** | 両方 | Windows 8.1 以前 | Desktop Analytics では、データ収集を正常に機能させるために値 `1` が必要です。 |
| **DisableEnterpriseAuthProxy** | GPO | すべての Windows バージョン | 環境で、インターネット アクセスのために Windows 統合認証を使用するユーザー認証済みプロキシが必要な場合、データ収集を正常に機能させるために、Desktop Analytics で値 `0` が必要です。 詳細については、「[プロキシ サーバー認証](enable-data-sharing.md#proxy-server-authentication)」をご覧ください。 |

> [!IMPORTANT]
> ほとんどの場合、Configuration Manager だけを使ってこれらの設定を構成します。 これらの設定は、ドメイン グループ ポリシー オブジェクトでは適用しないでください。 詳細については、「[競合の解決](enroll-devices.md#conflict-resolution)」をご覧ください。

### <a name="settings-from-upgrade-readiness"></a>Upgrade Readiness からの設定

Windows Analytics では、Upgrade Readiness スクリプトを使用して次のポリシーも設定されます。

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

デバイスで Upgrade Readiness オンボード スクリプトを実行した場合は、これらのポリシー設定がまだ存在する可能性があります。 レガシ スクリプトは使用しないでください。 デバイスを Desktop Analytics に登録する前に、これらの以前のポリシー設定を削除してください。

## <a name="group-policy-settings"></a>グループ ポリシー設定

通常は、構成マネージャー コレクションを使用して、Desktop Analytics の設定と登録の対象を設定します。 コレクションに対してデバイスを含めたり除外したりするには、ダイレクト メンバーシップまたはクエリを使用します。 詳しくは、「[コレクションを作成する方法](../core/clients/manage/collections/create-collections.md)」をご覧ください。

Configuration Manager によって、ターゲット コレクションで商用 ID と診断データ設定が構成されます。 デバイスのグループごとに異なる診断データ設定を構成する必要がある場合は、グループ ポリシー設定を使用して Configuration Manager の設定を上書きします。 たとえば、一部のデバイスでは**拡張 (制限付き)** レベルを設定し、他のデバイスでは**基本**レベルを設定する必要があります。 一部のデバイスで、異なる[プロキシ サーバー認証](enable-data-sharing.md#proxy-server-authentication)設定を使用する場合があります。

関連するグループ ポリシー設定は、次のパスにあります。 **[コンピューターの構成]**  >  **[管理用テンプレート]**  >  **[Windows コンポーネント]**  >  **[データの収集とプレビュー ビルド]** 。

グループ ポリシー設定では、次のキーのレジストリ設定のみが変更されます: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> グループ ポリシー設定を使用して複雑なシナリオに対応する場合は、構成の競合を引き起こす可能性があるポリシー設定に特に注意してください。 *値がまだ存在していない場合にのみ*、Configuration Manager によって [Windows の設定](#windows-settings)が構成されます。 グループ ポリシーの設定は Configuration Manager の設定よりも優先されるため、グループ ポリシーの構成によっては、Desktop Analytics で問題が発生する可能性があります。

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Desktop Analytics で Configuration Manager の設定と競合する可能性のあるグループ ポリシー設定

次の表に、Configuration Manager が Desktop Analytics に登録するデバイスで設定される Windows 設定と競合する可能性が最も高いグループ ポリシー設定を示します。

| 表示名 | レジストリ値 | Desktop Analytics に登録されたデバイスへの影響 |
|--------------|----------------|-------------------------------------------------|
| **[Configure the Commercial ID]\(商用 ID を構成する\)** | CommercialId | このポリシーを別の値に設定すると、Configuration Manager によって設定された商用 ID が上書きされます。 ID が同じでない場合は、構成されたデバイスが Desktop Analytics で表示されないことがあります。 |
| **[利用統計情報の許可]** | AllowTelemetry | このポリシーを別の値に設定すると、ターゲット コレクションに対して Configuration Manager で設定したグローバル診断データ レベルが上書きされます。 |
| **[Limit Enhanced diagnostic data to the minimum required by Windows Analytics]\(拡張診断データを Windows Analytics で必要とされる最小値に制限する\)** | LimitEnhancedDiagnosticDataWindowsAnalytics | このポリシーは、以前の AllowTelemetry 設定に依存します。 このポリシーにより、Configuration Manager またはグループ ポリシーで設定したレベルに応じて、デバイスの診断データ レベルが**拡張**または**拡張 (制限付き)** に変更される場合があります。 このポリシーは、AllowTelemetry が `2` (**拡張**) に設定されている場合にのみ適用されます。 |
| **[Allow device name to be sent in Windows diagnostic data]\(Windows 診断データでのデバイス名の送信を許可する\)** | AllowDeviceNameInTelemetry | Configuration Manager でデバイス名を送信することを選択した場合、このポリシーを [無効] に構成することで、その選択を上書きできます。 この設定を無効にすると、Desktop Analytics でデバイス名は "不明" と表示されます。 詳細については、「[デバイス名](enroll-devices.md#device-name)」をご覧ください。 |
| **[Configure Authenticated Proxy usage for the Connected User Experience and Telemetry service]\(接続ユーザー エクスペリエンスとテレメトリ サービスでの認証済みプロキシの使用を構成する\)** | DisableEnterpriseAuthProxy | Configuration Manager でデバイスでのユーザー認証済みプロキシの使用 (`0`) を構成した場合、このポリシーを **[Disable Authenticated Proxy usage]\(認証済みプロキシの使用を無効にする\)** (`1`) に構成すると、デバイスはユーザーのコンテキストではなく、システムのコンテキストで診断データを送信します。 システムのコンテキストのプロキシでデバイスを構成していない場合、またはデバイスがこのプロキシに対して認証できない場合、Windows は Desktop Analytics に診断データを送信できません。 |

> [!NOTE]
> レガシ ポリシーの **[Configure Connected User Experiences and Telemetry]\(接続ユーザーのエクスペリエンスと利用統計情報を構成する\)** (TelemetryProxy) により、Windows は、ユーザー (WinINET) またはデバイス (WinHTTP) のプロキシを使用する代わりに、専用プロキシに診断データを転送できます。 一部の Windows コンポーネントは、このポリシーをサポートしていません。 このポリシーを使用すると、Desktop Analytics でデータ品質の問題が発生する可能性があります。

#### <a name="behavior-of-disabled-settings"></a>無効な設定の動作

これらのグループ ポリシー設定を **[無効]** に構成すると、システムの動作にさまざまな影響があります。

- **CommercialId** ポリシーを無効にすると、Windows によってこのレジストリ値が削除されます。 ローカル ポリシーのレジストリ パスに設定されている商用 ID の Configuration Manager 設定がデバイスに適用されます。

- Configuration Manager によってグループ ポリシーと同じレジストリの場所に設定されたポリシーの場合、グループ ポリシーで設定を無効にすると、Windows によってそのレジストリ値が削除されます。 Configuration Manager は、次回のポリシー処理サイクルでこのレジストリ値を再び設定しますが、その後、Windows は、次回のグループ ポリシーの更新時にこのレジストリ値を削除します。 このように構成が絶えず変わることが原因で、Desktop Analytics で望ましくない動作を招く可能性があります。

  - これらのグループ ポリシー設定を **[未構成]** に設定すると、Windows は値を 1 回削除しますが、続けて削除されることはありません。 この構成により、Configuration Manager の値を想定どおりに適用できます。

### <a name="group-policy-settings-to-customize-the-user-experience"></a>ユーザー エクスペリエンスをカスタマイズするためのグループ ポリシー設定

これらのグループ ポリシー設定は、Configuration Manager および Desktop Analytics では必要ありません。 Windows 診断データを使用してユーザーのエクスペリエンスを構成するために、グループ ポリシーでこれらを構成できます。

| 表示名 | レジストリ値 | Desktop Analytics に登録されたデバイスへの影響 |
|--------------|----------------|-------------------------------------------------|
| **[Configure telemetry opt-in change notifications]\(テレメトリのオプトイン変更通知を構成する\)** | DisableTelemetryOptInChangeNotification | Windows 10 バージョン 1803 以降では、診断データ レベルが変更されると、Windows によってユーザーに通知が送られます。 通知を無効にするには、このポリシーを使用します。 |
| **[Configure telemetry opt-in setting user interface]\(テレメトリのオプトイン設定のユーザー インターフェイスを構成する\)** | DisableTelemetryOptInSettingsUx | 診断データのレベルを構成する場合は、デバイスに対して上限を設定します。 Windows 10 バージョン 1803 以降では、ユーザーは下位レベルを設定できます。 ユーザーが診断レベルを変更できないようにするには、このポリシーを使用します。 詳しくは、「[組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)」をご覧ください。 |
| **[Disable deleting diagnostic data]\(診断データの削除を無効にする\)** | DisableDeviceDelete | Windows 10 バージョン 1809 以降では、ユーザーは **[Diagnostic & feedback]\(診断とフィードバック\)** 設定ページから診断データを削除できます。 Microsoft がデバイスから収集した診断データを削除できないようにするには、このポリシーを使用します。 |
| **[Disable diagnostic data viewer]\(診断データ ビューアーを無効にする\)** | DisableDiagnosticDataViewer | Windows 10 バージョン 1809 以降では、ユーザーは **[Diagnostic & feedback]\(診断とフィードバック\)** 設定ページから診断データ ビューアーを有効にし、開くことができます。 Windows 設定の診断データ ビューアーを無効にし、Microsoft がデバイスから収集した診断データがこのビューアーで表示されないようにするには、このポリシーを使用します。|
