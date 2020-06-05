---
title: Intune 用 Windows セキュリティ エクスペリエンスの Windows 10 ウイルス対策ポリシーの設定 | Microsoft Docs
description: Microsoft Intune における Windows セキュリティ アプリ向けエンドポイント セキュリティのウイルス対策ポリシーの設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 089303b76f674d47767afdff72341d09f7f227d4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431736"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Microsoft Intune における Windows セキュリティ エクスペリエンス プロファイルの設定

[エンドポイント セキュリティ ポリシー](../protect/endpoint-security-policy.md)の一部として Microsoft Intune で Windows 10 の **Windows セキュリティ エクスペリエンス** プロファイル向けに構成できるウイルス対策ポリシー設定を確認します。

**Windows セキュリティ**

- **[改ざん保護を有効にして Microsoft Defender が無効にならないようにします]**  
  [改ざん防止機能によってセキュリティ設定の変更を防止する](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **[未構成]** ("*既定値*") - *[有効]* または *[無効]* 状態がクライアントに存在する場合、 *[未構成]* を展開しても設定に影響を与えません。 
  - **[有効]** - 改ざん保護の制限を有効にします。 状態を有効または無効から変更するには、その逆の設定を展開して有効にします。
  - **[無効]** - 改ざん保護の制限を無効にします。 状態を有効または無効から変更するには、その逆の設定を展開して有効にします。

- **[Windows セキュリティ アプリの [ウイルスと脅威の防止] 領域を非表示にする]**  
  CSP:[DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザー アクセスと通知が許可されます。
  - **[はい]** - Windows セキュリティ アプリの [ウイルスと脅威の防止] 領域がエンドユーザーに表示されません。 ウイルスと脅威の防止に関連した通知は表示されません。

  - **[Windows セキュリティ アプリの [ランサムウェア攻撃後のデータ回復] オプションを非表示にする]**  
    CSP: [](https://go.microsoft.com/fwlink/?linkid=873664)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザー アクセスと通知が許可されます。
  - **[はい]** - Windows セキュリティ アプリの [ランサムウェア攻撃後のデータ回復] 領域がエンドユーザーに表示されません。 ランサムウェアに関連した通知は表示されません。

- **[Windows セキュリティ アプリの [アカウント保護] 領域を非表示にする]**  
  CSP:[DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザー アクセスと通知が許可されます。
  - **[はい]** - Windows セキュリティ アプリの [アカウント保護] 領域がエンドユーザーに表示されません。 アカウント保護に関連した通知は表示されません。

- **[Hide the Firewall and network protection area in the Windows Security app]\(Windows セキュリティ アプリの [ファイアウォールとネットワーク保護] 領域を非表示にする\)**  
  CSP:[DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザー アクセスと通知が許可されます。
  - **[はい]** - Windows セキュリティの [ファイアウォールとネットワーク保護] 領域がエンドユーザーに表示されません。 ファイアウォールとネットワーク保護に関連した通知は表示されません。

- **[Windows セキュリティ アプリの [アプリとブラウザーの制御] 領域を非表示にする]**  
  CSP:[DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザー アクセスと通知が許可されます。
  - **[はい]** - Windows セキュリティの [アプリとブラウザーの制御] 領域がエンドユーザーに表示されません。 アプリとブラウザーの制御に関連した通知は表示されません。

- **[Windows セキュリティ アプリの [デバイスのセキュリティ] 領域を非表示にする]**  
  CSP:[DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザー アクセスと通知が許可されます。
  - **[はい]** - Windows セキュリティ アプリの [ハードウェア保護] 領域がエンドユーザーに表示されません。 ハードウェア保護に関連した通知は表示されません。
  
- **[Hide the Device performance and health area in the Windows Security app]\(Windows セキュリティ アプリの [デバイスのパフォーマンスと正常性] 領域を非表示にする\)**  
  CSP:[DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザー アクセスと通知が許可されます。
  - **[はい]** - Windows セキュリティ アプリの [デバイスのパフォーマンスと正常性] 領域がエンドユーザーに表示されません。 デバイスのパフォーマンスと正常性に関連した通知は表示されません。

- **[Windows セキュリティ アプリの [ファミリー オプション] 領域を非表示にする]**  
  CSP:[DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザー アクセスと通知が許可されます。
  - **[はい]** - Windows セキュリティ アプリの [ファミリー オプション] 領域がエンドユーザーに表示されません。 また、ファミリー オプションに関連した通知は表示されません。

- **[Windows セキュリティ アプリの通知]**  
  CSP: [](https://go.microsoft.com/fwlink/?linkid=873675)

  前述のすべての機能設定に関するユーザーへの Windows セキュリティの通知をブロックするには、この設定を使用します。 または、前述の設定を使用して機能ごとに Windows セキュリティ アプリの通知を管理することもできます。

  - **[未構成]** ("*既定値*") - 別の設定で制御されていない Windows セキュリティ アプリのすべての通知が許可されます。
  - **[重大ではない通知のブロック]** - スキャンの完了などの通知がブロックされます。
  - **[すべての通知のブロック]** - すべての Windows セキュリティ機能に関して、重大な通知も重大でない通知もブロックされます。

- **[通知領域の Windows セキュリティ アイコンを非表示にする]**  
  CSP:[HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  この設定を有効にするには、ユーザーがサインアウトしてからサインインするか、コンピューターを再起動する必要があります。
  - **[未構成]** ("*既定値*") - この設定によりクライアントは既定値に戻され、アイコンが表示されます。
  - **[はい]** - Windows セキュリティ アイコンがユーザーのシステム トレイに表示されなくなります。
  
- **[Windows セキュリティ アプリの [TPM のクリア] オプションを無効にする]**  
  CSP:[DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ボタンへのアクセスが許可されます。
  - **[はい]** - Windows セキュリティ アプリの TPM のクリア ボタンへのアクセスを無効にします。

- **[Prompt users to update TPM firmware if vulnerability is discovered]\(脆弱性が検出された場合に TPM ファームウェアの更新をユーザーに求める\)**  
  CSP:[DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **[未構成]** ("*既定値*") - この設定はクライアントの既定値に戻り、ユーザーに求めなくなります。
  - **[はい]** - TPM ファームウェアで潜在的な脆弱性が検出された場合にエンドユーザーにメッセージを表示することを Windows に許可します。 その後、ファームウェアの更新を実行して脆弱性を解決することをお勧めします。

- **[Organization's support contact information]\(組織のサポート連絡先情報\)**  
  CSP:[EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  IT 組織情報を Windows セキュリティ アプリと通知のどこに表示するかを宣言します。
  - **[未構成]** ("*既定値*")
  - **[アプリと通知に表示]**
  - **[アプリにのみ表示]**
  - **[通知にのみ表示]**