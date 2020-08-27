---
title: Windows Autopilot ネットワーク要件
ms.reviewer: ''
manager: laurawi
description: Windows の自動操縦展開のネットワーク要件について通知します。
keywords: mdm、セットアップ、windows、windows 10、oobe、管理、展開、自動操縦、ztd、ゼロタッチ、パートナー、msfb、intune
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
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 3c24610a2ac10dfae6a8ba73062edf29188938ea
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907990"
---
# <a name="windows-autopilot-networking-requirements"></a>Windows Autopilot ネットワーク要件

**適用対象: Windows 10**

Windows の自動操縦は、さまざまなインターネットベースのサービスに依存しています。 自動操縦を正常に機能させるには、これらのサービスへのアクセスを提供する必要があります。 最も単純なケースでは、次の条件を満たすことで適切な機能を有効にすることができます。

- インターネット DNS 名のドメインネームサービス (DNS) の名前解決を確認する
- ポート 80 (HTTP)、443 (HTTPS)、123 (UDP/NTP) を介したすべてのホストへのアクセスを許可する

次のような環境で、必要なサービスへのアクセスを許可するために、追加の構成が必要になる場合があります。
- インターネットへのアクセスが制限されています。
- インターネットアクセスを取得するには、認証が必要です。 

> [!NOTE]
> OOBE.XML では、スマートカードと証明書ベースの認証はサポートされていません。 詳細については、「 [スマートカードと証明書ベースの認証](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication)」を参照してください。

これらの各サービスと固有の要件について詳しくは、以下の詳細を確認してください。

<table><th>サービス<th>情報
<tr><td><b>Windows 自動操縦展開サービス<b><td>ネットワーク接続が確立されると、各 Windows 10 デバイスは Windows 自動操縦展開サービスにアクセスします。 Windows 10 バージョン1903以降では、、の各 Url が使用されます。 https://ztd.dds.microsoft.com https://cs.dds.microsoft.com <br>

<tr><td><b>Windows ライセンス認証<b><td>Windows の自動操縦には Windows ライセンス認証サービスが必要です。 アクティベーションサービスにアクセスできる必要がある Url の詳細について <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">は、「Windows のライセンス認証」または「検証がエラーコード0x8004FE33 で失敗</a>する」を参照してください。<br>

<tr><td><b>Azure Active Directory<b><td>ユーザーの資格情報は Azure Active Directory によって検証され、デバイスを Azure Active Directory に参加させることもできます。 詳細については、「 <a href="https://docs.microsoft.com/office365/enterprise/office-365-ip-web-service">Office 365 の IP アドレスと URL Web サービス</a>」を参照してください。
<tr><td><b>Intune<b><td>認証が完了すると、Azure Active Directory によってデバイスが Intune モバイルデバイス管理 (MDM) サービスに登録されます。 ネットワーク通信の要件の詳細については、「 <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">Intune のネットワーク構成の要件と帯域幅</a>」を参照してください。
<tr><td><b>Windows Update<b><td>OOBE プロセス中および Windows 10 OS 構成後に、Windows Update サービスは必要な更新プログラムを取得します。 Windows Update に接続するときに問題が発生した場合は、 <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">Windows Update または Microsoft Update に関する接続の問題を解決する方法に関する説明</a>を参照してください。<br>

Windows Update にアクセスできない場合でも、自動操縦プロセスは続行されますが、重要な更新プログラムは使用できません。

<tr><td><b>配信の最適化<b><td>自動操縦は、アプリと更新プログラムをダウンロードするときに <a href="/windows/deployment/update/waas-delivery-optimization">配信最適化</a> サービスに問い合わせます。 この連絡先は、少数のデバイスのみがインターネットからダウンロードする必要があるように、コンテンツのピアツーピア共有を確立します。
- Windows 更新プログラム - Microsoft Store アプリとアプリの更新プログラム - Office 更新プログラム - Intune Win32 アプリ<br>

配信最適化サービスにアクセスできない場合でも、自動操縦プロセスは、(ピアツーピアではなく) クラウドから配信の最適化のダウンロードを続行します。

<tr><td><b>ネットワークタイムプロトコル (NTP) の同期<b><td>Windows デバイスが起動すると、デバイスの時刻が正しいことを確認するために、ネットワークタイムサーバーと通信します。 time.windows.com への UDP ポート 123 にアクセスできることを確認します。
<tr><td><b>ドメインネームサービス (DNS)<b><td>すべてのサービスの DNS 名を解決するため、デバイスは DNS サーバーと通信します (通常は DHCP 経由で提供されます)。 この DNS サーバーは、インターネット上の名前を解決できる必要があります。
<tr><td><b>診断データ<b><td>Windows 10 1903 以降では、診断データの収集が既定で有効になります。 Windows Analytics および関連する診断機能を無効にする方法については、「 <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">Manage enterprise diagnostics data level</a>」を参照してください。<br>

診断データを送信できない場合でも、自動操縦プロセスは続行されます。 ただし、Windows Analytics などの診断データに依存するサービスは機能しません。
<tr><td><b>ネットワーク接続状態インジケーター (NCSI)<b><td>Windows は、デバイスがインターネットにアクセスできることを通知できる必要があります。 詳細については、「 <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">ネットワーク接続状態インジケーター (NCSI)</a>」を参照してください。

<code>www.msftconnecttest.com</code> DNS で解決可能で、HTTP 経由でアクセス可能である必要があります。
<tr><td><b>Windows Notification Services (WNS)<b><td>このサービスを使って、Windows がアプリとサービスから通知を受け取ることができるようにします。 詳細については、「 <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a>」を参照してください。<br>

WNS サービスが使用できない場合でも、自動操縦プロセスは通知なしで続行されます。
<tr><td><b>Microsoft Store、Microsoft Store for Business<b><td>Microsoft Store 内のアプリは、Intune (MDM) 経由でトリガーしてデバイスにプッシュすることができます。ユーザーが最初にログインするとき、アプリの更新プログラムとその他のアプリも必要になることがあります。 詳細については、「 <a href="/microsoft-store/prerequisites-microsoft-store-for-business">ビジネス向け Microsoft Store および教育機関向けの前提条件</a> (Azure AD と Windows Notification Services も含まれます)」を参照してください。<br>

Microsoft Store にアクセスできない場合でも、自動操縦プロセスは Microsoft Store アプリなしで続行されます。

<tr><td><b>Office 365<b><td>Intune デバイス構成の一部として、enterprise 用 Microsoft 365 アプリのインストールが必要になる場合があります。 詳細については、「 <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">Office 365 の url と IP アドレス範囲</a>」を参照してください。 この記事には、すべての Office サービス、DNS 名、IP アドレスが含まれています。 また、上記のサービスと重複する可能性のある Azure AD およびその他のサービスも含まれています。
<tr><td><b>証明書失効リスト (Crl)<b><td>これらのサービスの一部は、証明書失効リスト (CRL) にサービスで使用される証明書がないか確認する必要もあります。完全な一覧については、「 <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">office 365 の url と IP アドレスの範囲</a> 」と「 <a href="https://aka.ms/o365chains">Office 365 証明書チェーン</a>」を参照してください。
<tr><td><b>ハイブリッド Azure AD 参加<b><td>デバイスは、ハイブリッド Azure AD 参加できます。 ハイブリッド Azure AD 参加するには、コンピューターが企業ネットワーク上にある必要があります。 詳細については<a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">、「Windows 自動操縦のユーザー主導モード」を</a>参照してください。
<tr><td><b>自動展開モードと自動操縦用ホワイトグローブ<b><td>Intel、AMD、または Qualcomm によってのみ提供されるファームウェア TPM デバイスは、起動時に必要なすべての証明書を含みません。また、最初に使用するときに製造元から取得できる必要があります。 (他の製造元のデバイスを含む) 個別の TPM チップを搭載したデバイスには、これらの証明書がプレインストールされています。 詳細については、「 <a href="https://docs.microsoft.com/windows/security/information-protection/tpm/tpm-recommendations">TPM の推奨事項</a>」を参照してください。 各ファームウェア TPM プロバイダーについて、証明書が正常に要求されるように、これらの Url にアクセスできることを確認します。

 <br>Intel <code>https://ekop.intel.com/ekcertservice</code>
 <br>Qualcomm <code>https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1</code>
 <br>AMD <code>https://ftpm.amd.com/pki/aia</code>

</table>

**次の手順**

[Windows Autopilot のライセンス要件](licensing-requirements.md)