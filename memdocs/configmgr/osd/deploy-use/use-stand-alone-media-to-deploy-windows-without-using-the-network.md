---
title: スタンドアロン メディアを使用した Windows の展開
titleSuffix: Configuration Manager
description: 帯域幅が制限されている場合にコンピューターを更新、インストール、またはアップグレードするオプションとして、Configuration Manager のスタンドアロン メディアを使用して Windows を展開します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124654"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>ネットワークではなくスタンドアロン メディアを使用した Windows の展開

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のスタンドアロン メディアには、コンピューター上に OS を展開するために必要なものがすべて含まれています。 このメディアには、ブート イメージ、OS イメージ、タスク シーケンス ポリシー、アプリケーション、ドライバーなどが含まれています。 スタンドアロン メディアによる展開では、次のような状況でオペレーティング システムを展開できます。

- OS イメージまたはその他の大きなパッケージをネットワークを通じてコピーするのが実用的ではない環境

- ネットワーク接続がない、または低帯域幅のネットワーク接続の環境

次の OS 展開シナリオでは、スタンドアロン メディアを使用します。

- [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)

- [Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md)

いずれかの OS の展開シナリオの手順を完了します。 その後、次のセクションを使用して、スタンドアロン メディアの準備と作成を行います。

## <a name="unsupported-task-sequence-actions"></a>サポートされていないタスク シーケンス アクション

スタンドアロン メディアを使用する場合、タスク シーケンスの次のアクションは Configuration Manager でサポートされません。

- [ドライバーの自動適用](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers)のステップ。 ドライバー カタログからのデバイス ドライバーの自動適用はサポートされていません。 特定の一連のドライバーを Windows セットアップで使用できるようにするには、[[ドライバー パッケージの適用]](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) ステップを使用します。

- ソフトウェア更新プログラムのインストール

- OS 展開前のソフトウェアのインストール

- ユーザーとデバイスのアフィニティのための展開先のコンピューターとユーザーの関連付け

- [[パッケージのインストール]](../understand/task-sequence-steps.md#BKMK_InstallPackage) ステップを使用した動的なパッケージのインストール

- [[アプリケーションのインストール]](../understand/task-sequence-steps.md#BKMK_InstallApplication) ステップを使用した動的なアプリケーションのインストール

> [!NOTE]
> OS を展開するタスク シーケンスに **[パッケージのインストール]** ステップが含まれる場合に、中央管理サイト (CAS) でスタンドアロン メディアを作成すると、エラーが発生する可能性があります。 CAS には、タスク シーケンスの実行時に、ソフトウェア配布エージェントを有効にするために必要なクライアント構成ポリシーがありません。 **CreateTsMedia.log** ファイルに次のエラーが表示される場合があります。
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> **[パッケージのインストール]** ステップを含むスタンドアロン メディアの場合は、ソフトウェア配布エージェントが有効になっているプライマリ サイトでスタンドアロン メディアを作成します。
>
> または、タスク シーケンスを編集して、[[Windows と ConfigMgr のセットアップ]](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) ステップの後に [[コマンド ラインの実行]](../understand/task-sequence-steps.md#BKMK_RunCommandLine) ステップを追加します。 最初の **[パッケージのインストール]** ステップが実行される前に、この **[コマンド ラインの実行]** ステップによって、以下の WMI コマンドが実行されてソフトウェア配布エージェントが有効になります。
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>展開の設定の構成

スタンドアロン メディアを使用して OS の展開プロセスを開始する場合、OS をメディアから使用できるように展開を構成します。 展開の **[展開の設定]** ページの **[利用できるようにする項目]** の設定で、次のいずれかのオプションを選択します。

- Configuration Manager クライアント、メディア、PXE

- メディアと PXE のみ

- メディアと PXE のみ (非表示)

## <a name="create-the-standalone-media"></a>スタンドアロン メディアの作成

スタンドアロン メディアとして USB フラッシュ ドライブと CD/DVD セットのどちらかを指定できます。 メディアが起動されるコンピューターでは、起動可能なドライブとして選択するオプションがサポートされている必要があります。 詳細については、「[スタンドアロン メディアの作成](create-stand-alone-media.md)」を参照してください。

## <a name="install-the-os-from-standalone-media"></a>スタンドアロン メディアから OS をインストールする

OS をインストールするには、スタンドアロン メディアをコンピューターに挿入し、電源をオンにします。

## <a name="next-steps"></a>次のステップ

[OS 展開のユーザー エクスペリエンス](../understand/user-experience.md#task-sequence-wizard)
