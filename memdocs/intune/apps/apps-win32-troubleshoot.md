---
title: Microsoft Intune の Win32 アプリのトラブルシューティング
titleSuffix: ''
description: Microsoft Intune に関する Win32 アプリの問題をトラブルシューティングするための最も一般的な方法について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bbdc929f5d3a9703f3d299b8e3a68dd624c450c2
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083915"
---
# <a name="troubleshoot-win32-app-issues"></a>Win32 アプリの問題をトラブルシューティングする

Microsoft Intune で使用される Win32 アプリのトラブルシューティングを行うには、いくつかの方法があります。 この記事では、トラブルシューティングの詳細と、Win32 アプリの問題の解決に役立つ情報を提供します。 詳しくは、「[Win32 アプリのインストールのトラブルシューティング](troubleshoot-app-install.md#win32-app-installation-troubleshooting)」をご覧ください。

> [!NOTE]
> このアプリの管理機能では、Windows アプリケーションの 32 ビットと 64 ビットの両方のオペレーティング システム アーキテクチャがサポートされます。

> [!IMPORTANT]
> Win32 アプリを展開する場合、特に複数ファイルの Win32 アプリ インストーラーがある場合は、[Intune 管理拡張機能](../apps/intune-management-extension.md)の方法を排他的に使用することを検討してください。 AutoPilot 登録中に Win32 アプリと基幹業務 (LOB) アプリのインストールを混在させると、アプリのインストールが失敗する場合があります。 PowerShell スクリプトまたは Win32 アプリがユーザーまたはデバイスに割り当てられると、Intune 管理拡張機能が自動的にインストールされます。

## <a name="app-troubleshooting-details"></a>アプリのトラブルシューティングの詳細

アプリの作成日時、変更日時、対象とされた日時、デバイスに配信された日時など、インストールに関する問題を表示できます。 [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) では、 **[トラブルシューティング + サポート]** ペインでこれらの情報とその他の詳細を提供しています。 詳細については、「[アプリのトラブルシューティングの詳細](troubleshoot-app-install.md#app-troubleshooting-details)」をご覧ください。

## <a name="troubleshooting-app-issues-by-using-logs"></a>ログを使用したアプリの問題のトラブルシューティング

ログの詳細を表示すると、発生している問題の原因を特定して解決するのに役立ちます。 [Intune に表示されているログ](apps-win32-troubleshoot.md#logs-displayed-in-intune)を表示するか、[CMTrace を使用して表示されるログ](apps-win32-troubleshoot.md#logs-displayed-through-cmtrace)を表示するかを選択できます。 

### <a name="logs-displayed-in-intune"></a>Intune に表示されるログ

Win32 アプリでインストールの問題が発生した場合は、Intune でアプリの **[インストールの詳細]** ペインにある **[ログの収集]** オプションを選択できます。 詳しくは、「[Win32 アプリのインストールのトラブルシューティング](troubleshoot-app-install.md#win32-app-installation-troubleshooting)」をご覧ください。

### <a name="logs-displayed-through-cmtrace"></a>CMTrace を使用して表示されるログ

クライアント コンピューター上のエージェント ログは、通常 *C:\ProgramData\Microsoft\IntuneManagementExtension\Logs* にあります。 *CMTrace.exe* を使用してこれらのログ ファイルを表示できます。 詳細については、「[CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace)」を参照してください。

![クライアント コンピューター上のエージェント ログのスクリーンショット](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> LOB Win32 アプリを適切にインストールして実行できるようにするには、マルウェア対策設定で、以下のディレクトリをスキャン対象から除外する必要があります。<p>
> **x64 クライアント コンピューターの場合**:<br>
> *C:\Program Files (x86)\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>  
> **x86 クライアント コンピューターの場合**:<br>
> *C:\Program Files\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>
> 詳細については、「[現在サポートされているバージョンの Windows を搭載しているエンタープライズ コンピューターでウイルス スキャンを行う場合の推奨事項](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers)」を参照してください。

## <a name="detecting-the-win32-app-file-version-by-using-powershell"></a>PowerShell を使用して Win32 アプリ ファイルのバージョンを検出する

Win32 アプリ ファイルのバージョンを検出するのが難しい場合は、以下の PowerShell コマンドの使用または変更を検討してください。

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

上記の PowerShell コマンドで、`<path to binary file>` 文字列を、Win32 アプリ ファイルへのパスに置き換えます。 パスの例は次のようになります。

`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

また、`<file version of successfully detected file>` 文字列を、検出する必要があるファイルのバージョンに置き換えます。 ファイル バージョン文字列の例は、次のようになります。

`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Win32 アプリのバージョン情報を取得する必要がある場合は、次の PowerShell コマンドを使用できます。

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

上記の PowerShell コマンドで、`<path to binary file>` をファイル パスに置き換えます。

## <a name="additional-troubleshooting-areas-to-consider"></a>検討すべき追加のトラブルシューティング領域
- ターゲットを確認して、エージェントがデバイスにインストールされていることを確認します。 グループを対象とする Win32 アプリ、またはグループを対象とする PowerShell スクリプトにより、セキュリティ グループのエージェント インストール ポリシーが作成されます。
- OS のバージョンを確認します: Windows 10 1607 以降  
- Windows 10 SKU を確認します。 Windows 10 S (S モードを有効にして実行されている Windows バージョン) では、MSI のインストールはサポートされていません。

Win32 アプリのトラブルシューティングについて詳しくは、「[Win32 アプリ インストールのトラブルシューティング](troubleshoot-app-install.md#win32-app-installation-troubleshooting)」を参照してください。 ARM64 デバイスでのアプリの種類の詳細については、「[ARM64 デバイスでサポートされているアプリの種類](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices)」をご覧ください。

## <a name="next-steps"></a>次のステップ

- [アプリのインストールに関する問題のトラブルシューティング](troubleshoot-app-install.md)
