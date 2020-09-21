---
title: Microsoft Intune にアップロードする Win32 アプリを準備する
titleSuffix: ''
description: Microsoft Intune にアップロードする Win32 アプリを準備する方法を説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 94626b6cc7e9586ff6b9230206c3e57e6b01b86f
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083799"
---
# <a name="prepare-win32-app-content-for-upload"></a>Win32 アプリ コンテンツのアップロードを準備する

Win32 アプリを Microsoft Intune に 追加する前に、[Microsoft Win32 コンテンツ準備ツール](https://go.microsoft.com/fwlink/?linkid=2065730)を使用してアプリを準備する必要があります。

## <a name="prerequisites"></a>[前提条件]

Win32 アプリの管理を使用する場合は、必ず、次の基準を満たすようにしてください。

- Windows 10 バージョン 1607 以降 (Enterprise、Pro、Education バージョン) を使用します。
- デバイスを Azure Active Directory (Azure AD) に参加させ、自動登録する必要があります。 Intune 管理拡張機能では、Azure AD 参加済み、ハイブリッド ドメイン参加済み、グループ ポリシー登録済みのデバイスがサポートされます。 
  > [!NOTE]
  > グループ ポリシー登録のシナリオの場合、エンド ユーザーはローカル ユーザー アカウントを使用して、Windows 10 デバイスを Azure AD に参加させます。 ユーザーは、Azure AD ユーザー アカウントを使用してデバイスにログオンし、Intune に登録する必要があります。 PowerShell スクリプトまたは Win32 アプリのターゲットがユーザーまたはデバイスである場合、Intune でデバイス上に Intune 管理拡張機能がインストールされます。
- Windows アプリケーションのサイズはアプリごとに 8 GB に制限されています。

## <a name="convert-the-win32-app-content"></a>Win32 アプリのコンテンツを変換する

[Microsoft Win32 コンテンツ準備ツール](https://go.microsoft.com/fwlink/?linkid=2065730)を使用して、Windows クラシック (Win32) アプリを事前処理します。 このツールは、アプリケーション インストール ファイルを *.intunewin* 形式に変換します。 また、このツールは、Intune でアプリケーションのインストール状態を判断するのに必要な属性の一部を検出します。 アプリのインストーラー フォルダーでこのツールを使用した後、Intune コンソールで Win32 アプリを作成できます。

> [!IMPORTANT]
> [Microsoft Win32 コンテンツ準備ツール](https://go.microsoft.com/fwlink/?linkid=2065730)では、 *.intunewin* ファイルの作成時に、すべてのファイルとサブフォルダーを zip 圧縮します。 必ず、Microsoft Win32 コンテンツ準備ツールを、インストーラー ファイルとフォルダーから切り離し、 *.intunewin* ファイルにツールや他の不要なファイルとフォルダーを含めないようにしてください。

[Microsoft Win32 コンテンツ準備ツール](https://go.microsoft.com/fwlink/?linkid=2065730)は、GitHub から .zip ファイルとしてダウンロードできます。 zip ファイルには、*Microsoft-Win32-Content-Prep-Tool-master* という名前のフォルダーが含まれています。 フォルダーには準備ツール、ライセンス、readme、およびリリース ノートが含まれています。 

### <a name="process-flow-to-create-a-intunewin-file"></a>.intunewin ファイルを作成するプロセス フロー

   <img alt="Flow chart of the process to create a .intunewin file." src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="running-the-microsoft-win32-content-prep-tool"></a>Microsoft Win32 コンテンツ準備ツールを実行する

コマンド ウィンドウからパラメーターを指定せずに `IntuneWinAppUtil.exe` を実行する場合、ツールによって、段階的に必要なパラメーターを入力する方法が示されます。 以下の使用可能なコマンド ライン パラメーターに基づいて、コマンドにパラメーターを追加することもできます。

### <a name="available-command-line-parameters"></a>使用可能なコマンド ライン パラメーター 

|    **コマンド ライン パラメーター**    |    **説明**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    ヘルプ    |
|    `-c <setup_folder>`     |    すべてのセットアップ ファイルのフォルダー。 このフォルダー内のすべてのファイルは、 *.intunewin* ファイルに圧縮されます。    |
|    `-s <setup_file>`     |    セットアップ ファイル (*setup.exe*、*setup.msi* など)。    |
|    `-o <output_folder>`     |    生成された *.intunewin* ファイルの出力フォルダー。    |
|    `-q`       |    非表示モードです。    |

### <a name="example-commands"></a>コマンドの例

|    **コマンド例**    |    **説明**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    このコマンドでは、ツールの使用情報が表示されます。    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    このコマンドにより、指定されたソース フォルダーおよびセットアップ ファイルから *.intunewin* ファイルが生成されます。 MSI セットアップ ファイルでは、このツールは Intune に必要な情報を取得します。 `-q` が指定されている場合、コマンドは quiet モードで実行されます。 出力ファイルが既に存在する場合は上書きされます。 また、出力フォルダーが存在しない場合は、自動的に作成されます。    |

*.intunewin* ファイルを生成する場合、参照するために必要なすべてのファイルをセットアップ フォルダーのサブフォルダーに置いてください。 次に、相対パスを使用して特定の必要なファイルを参照します。 次に例を示します。

**セットアップのソース フォルダー:** *c:\testapp\v1.0*<br>
**ライセンス ファイル:** *c:\testapp\v1.0\licenses\license.txt*

相対パス *licenses\license.txt* を使用して *license.txt* ファイルを参照します。

## <a name="next-steps"></a>次のステップ

- [Microsoft Intune に Win32 アプリを追加する](apps-win32-add.md)
