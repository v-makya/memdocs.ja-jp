---
title: Windows Autopilot のリセット
description: Windows の自動操縦リセットでは、デバイスをビジネス対応状態に戻します。これにより、次のユーザーはサインインして、すばやく簡単に生産性を得ることができます。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 5ec7e9eeb9da46e1d9bc77dcd71e76be4948fc23
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568567"
---
# <a name="windows-autopilot-reset"></a>Windows Autopilot のリセット

- 適用対象: Windows 10 バージョン1709以降 (ローカルリセット)
- 適用対象: Windows 10 バージョン1809以降 (リモートリセット)

Windows の自動操縦リセットでは、デバイスをビジネス対応状態に戻します。これにより、次のユーザーはサインインして、簡単に生産性を向上させることができます。 具体的には、Windows 自動操縦リセット:
- 個人用ファイル、アプリ、および設定を削除します。
- デバイスの元の設定を再適用します。
- Azure AD へのデバイスの id 接続を維持します。
- デバイスの Intune への管理接続を維持します。

Windows 自動操縦リセットプロセスでは、既存のデバイスからの情報が自動的に保持されます。
 
- 地域、言語、およびキーボードを元の値に設定します。
- Wi-fi 接続の詳細。
- 以前にデバイスに適用されたパッケージをプロビジョニングする
- リセットプロセスの開始時に USB ドライブに存在するプロビジョニングパッケージ 
- デバイスのメンバーシップと MDM 登録情報を Azure Active Directory します。

Windows 自動操縦リセットは、この情報が復元されるまでユーザーがデスクトップにアクセスできないようにします。これには、プロビジョニングパッケージの再適用も含まれます。 MDM サービスに登録されているデバイスについては、MDM 同期が完了するまで Windows 自動操縦リセットもブロックされます。 AutoPilot リセットがデバイスで使用されると、デバイスのプライマリ ユーザーが削除されます。 リセット後に初めてサインインしたユーザーがプライマリ ユーザーとして設定されます。
 
 
>[!NOTE]
>自動操縦リセットでは、Hybrid Azure AD 参加済みデバイスはサポートされていません。

## <a name="scenarios"></a>シナリオ

Windows の自動操縦リセットでは、2つのシナリオがサポートされます。

- 組織の IT 担当者または他の管理者によって開始された[ローカルリセット](#reset-devices-with-local-windows-autopilot-reset)。
- [リモートリセット](#reset-devices-with-remote-windows-autopilot-reset) は、Microsoft Intune などの MDM サービスを介して IT 担当者によってリモートで開始されました。

各シナリオでは、追加の要件と構成の詳細が適用されます。

## <a name="reset-devices-with-local-windows-autopilot-reset"></a>ローカルの Windows 自動操縦リセットを使用してデバイスをリセットする 

**適用対象: Windows 10 バージョン1709以降**

このタスクには、Intune サービス管理者ロールが必要です。 詳しくは、「[Intune にユーザーを追加して管理アクセス許可を付与する](/intune/users-add)」をご覧ください。

IT 管理者は、ローカルの Windows 自動操縦リセットを使用して次のことを行うことができます。
- 個人のファイル、アプリ、設定をすばやく削除します。
- ロック画面から Windows 10 デバイスをリセットします。
- 元の設定と管理登録 (Azure Active Directory およびデバイス管理) を適用するデバイスを使用する準備ができました。 ローカル自動操縦リセットを使用すると、デバイスは完全に構成されているか、または既知の承認済みの状態に戻ります。

Windows 10 でローカル自動再設定のリセットを有効にするには

1. [機能に応じたポリシーを有効にする](#enable-local-windows-autopilot-reset)
2. [各デバイスのリセットをトリガーする](#trigger-local-windows-autopilot-reset)

### <a name="enable-local-windows-autopilot-reset"></a>ローカルの Windows 自動再設定のリセットを有効にする

ローカルの Windows 自動操縦のリセットを有効にするには、Disable自動再展開の **資格情報** ポリシーを構成する必要があります。 このポリシーは、 [ポリシー CSP](/windows/client-management/mdm/policy-csp-credentialproviders)、 **Credentialproviders/Disable自動再展開資格情報**に記載されています。 既定では、ローカルの Windows 自動操縦は無効になっています。 この既定では、ローカルの自動操縦リセットが誤ってトリガーされないようにします。

ポリシーは、次のいずれかの方法で設定できます。

- MDM プロバイダー

 - Intune を使用する場合は、次の設定で新しいデバイス構成プロファイルを作成できます。
   - **プラットフォーム**  = **Windows 10**以降
   - **プロファイルの種類**  = **デバイスの制限**
   - **カテゴリ**  = **全般**
   - **自動再展開**  = **許可**します。 ローカルリセットを許可するすべてのデバイスにこの設定を展開します。
 - Intune 以外の MDM プロバイダーを使用している場合は、このポリシーを設定する方法について MDM プロバイダーのドキュメントを確認してください。 

- Windows 構成デザイナー

 [Windows 構成デザイナーを使用](/windows/configuration/provisioning-packages/provisioning-create-package)して、 **> ポリシー > Credentialproviders > Disable自動 redeploymentcredentials**設定を0に設定してから、プロビジョニングパッケージを作成することができます。

- 学校用 PC のセットアップ アプリ

 School Pc のセットアップアプリの最新リリースでは、ローカルの Windows 自動操縦リセットの有効化がサポートされています。

### <a name="trigger-local-windows-autopilot-reset"></a>ローカルの Windows 自動操縦リセットのトリガー

ローカルの Windows 自動操縦リセットは、トリガーを起動して認証する2段階のプロセスです。 この2つの手順を完了すると、プロセスを実行して完了すると、デバイスが再び使用できる状態になります。 

**ローカル自動操縦リセットをトリガーするには**

1. Windows デバイスのロック画面から、**Ctrl + ![Windows キー](images/windows_glyph.png) + R** キーを押します。 

    ![Windows のロック画面で CTRL + Windows キー + R キーを押します。](images/autopilot-reset-lockscreen.png)

    これらのキーストロークにより、ローカルでの自動操縦リセット用のカスタムログイン画面が開きます。 この画面には、次の 2 つの目的があります。
    1. エンドユーザーがローカル自動再起動リセットをトリガーする権限を持っていることを確認します。
    2. Windows 構成デザイナーを使用して作成されたプロビジョニングパッケージがプロセスの一部として使用される場合に備えて、ユーザーに通知します。

        ![ローカルで自動再設定するためのカスタムログイン画面](images/autopilot-reset-customlogin.png)

2. 管理者の資格情報でサインインします。 プロビジョニングパッケージを作成した場合は、USB ドライブに接続し、ローカル自動操縦リセットをトリガーします。

 ローカルの自動操縦リセットがトリガーされると、リセットプロセスが開始されます。 プロビジョニングが完了すると、デバイスがまた使用できる状態になります。

## <a name="reset-devices-with-remote-windows-autopilot-reset"></a>リモートの Windows 自動操縦リセットを使用してデバイスをリセットする

**適用対象: Windows 10 バージョン1809以降**

Microsoft Intune のような MDM サービスを使用して、リモートの Windows 自動操縦リセットプロセスを開始できます。 この方法でリセットすると、IT スタッフが各コンピューターにアクセスしてプロセスを開始する必要がなくなります。

リモートの Windows 自動操縦リセット用にデバイスを有効にするには、デバイスを MDM で管理し、Azure AD に参加させる必要があります。 この機能は、 [自動展開モード](self-deploying.md)を使用して登録されたデバイスではサポートされていません。

### <a name="triggering-a-remote-windows-autopilot-reset"></a>リモートの Windows 自動操縦リセットのトリガー

Intune を使用してリモートの Windows 自動操縦リセットをトリガーするには、次の手順を実行します。
 
1. Intune コンソールの [ **デバイス** ] タブに移動します。 
2. [ **すべてのデバイス** ] ビューで、対象のリセットデバイスを選択し、[ **詳細** ] をクリックしてデバイスの操作を表示します。 
3. [ **自動再設定** ] を選択して、リセットタスクを開始します。 

>[!NOTE]
>Windows 10 ビルド17672以降を実行していないデバイスでは、Microsoft Intune で自動操縦リセットオプションが有効になりません。

>[!IMPORTANT]
>自動再設定の機能はグレー表示されます。 **ただし** 、自動再設定を使用してデバイスをリセットするか、デバイスを手動で sysprep する必要があります。

リセットが完了すると、デバイスは再び使用できる状態になります。
 


## <a name="troubleshooting"></a>トラブルシューティング

Windows 自動操縦リセットでは、 [Windows 回復環境 (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) が正しく構成され、デバイスで有効になっている必要があります。 構成されていない場合は、のようなエラー `Error code: ERROR_NOT_SUPPORTED (0x80070032)` が報告されます。

WinRE が有効になっていることを確認するには、 [REAgentC.exe ツール](/windows-hardware/manufacture/desktop/reagentc-command-line-options) を使用して次のコマンドを実行します。

```
reagentc /enable
```

WinRE を有効にした後に Windows 自動操縦のリセットが失敗した場合、または WinRE を有効にできない場合は、 [Microsoft サポート](https://support.microsoft.com) に問い合わせてください。
