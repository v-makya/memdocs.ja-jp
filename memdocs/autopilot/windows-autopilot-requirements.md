---
title: Windows Autopilot の要件
ms.reviewer: ''
manager: laurawi
description: Windows の自動操縦展開のソフトウェア、ネットワーク、ライセンス、および構成要件について通知します。
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
ms.openlocfilehash: e1380a38fb66ce2771d3cf91ecd9117b19ff31c4
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217133"
---
# <a name="windows-autopilot-requirements"></a>Windows Autopilot の要件

**適用対象: Windows 10**

Windows Autopilot は、Microsoft Intune など、Windows 10、Azure Active Directory、MDM サービスで利用可能な特定の機能に依存しています。  Windows の自動操縦を使用してこれらの機能を利用するには、いくつかの要件が満たされている必要があります。

**注**: Windows 自動操縦を現在サポートしている oem の一覧については、「 [windows 自動操縦](https://aka.ms/windowsAutopilot)」の「参加者のデバイス製造元」セクションを参照してください。

## <a name="software-requirements"></a>ソフトウェア要件

- [サポートされているバージョン](https://docs.microsoft.com/windows/release-information/)の Windows 10 半期チャネルが必要です。 Windows 10 Enterprise 2019 長期的なサービスチャネル (LTSC) もサポートされています。
- 次のエディションがサポートされています。
  - Windows 10 Pro
  - Windows 10 Pro Education
  - Windows 10 Pro for Workstations
  - Windows 10 Enterprise
  - Windows 10 Education
  - Windows 10 Enterprise 2019 LTSC

>[!NOTE]
>Windows 自動操縦を展開する手順は、特定の製品とバージョンを参照している場合があります。 これらの製品をこのコンテンツに含めることは、サポートライフサイクルを超えるバージョンのサポートの拡張を意味するものではありません。 Windows 自動操縦では、サポートライフサイクルを超える製品はサポートされていません。 詳しくは、「[Microsoft ライフサイクル ポリシー](https://go.microsoft.com/fwlink/p/?LinkId=208270)」をご覧ください。

## <a name="networking-requirements"></a>ネットワーク要件

Windows の自動操縦は、さまざまなインターネットベースのサービスに依存しています。 自動操縦を正常に機能させるには、これらのサービスへのアクセスを提供する必要があります。 簡単に説明すると、以下の点を確認することで適切な機能を実現できます。

- インターネット DNS 名による DNS 名前解決が行われるようにする
- ポート 80 (HTTP)、443 (HTTPS)、123 (UDP/NTP) を介したすべてのホストへのアクセスを許可する

インターネットアクセスが制限されている環境や、インターネットアクセスを取得する前に認証を必要とする環境では、必要なサービスへのアクセスをホワイトリストに登録するために追加の構成が必要になる場合があります。 

> [!NOTE]
> OOBE.XML では、スマートカードと証明書ベースの認証はサポートされていません。 詳細については、「 [スマートカードと証明書ベースの認証](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication)」を参照してください。

これらの各サービスと固有の要件について詳しくは、以下の詳細を確認してください。

<table><th>サービス<th>Information
<tr><td><b>Windows 自動操縦展開サービス<b><td>ネットワーク接続が確立されると、各 Windows 10 デバイスは Windows 自動操縦展開サービスにアクセスします。  Windows 10 バージョン1903以降では、、の各 Url が使用されます。 https://ztd.dds.microsoft.com https://cs.dds.microsoft.com <br>

<tr><td><b>Windows ライセンス認証<b><td>Windows の自動操縦には、Windows ライセンス認証サービスも必要です。 ライセンス認証サービスにアクセスできる必要がある Url の詳細については、「 <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">Windows のライセンス認証または検証がエラーコード0x8004FE33 で失敗</a> する」を参照してください。<br>

<tr><td><b>Azure Active Directory<b><td>ユーザーの資格情報は Azure Active Directory によって検証され、デバイスを Azure Active Directory に参加させることもできます。 詳細については <a href="https://docs.microsoft.com/office365/enterprise/office-365-ip-web-service">、「Office 365 の IP アドレスと URL Web サービス</a> 」を参照してください。
<tr><td><b>Intune<b><td>認証が完了すると、Azure Active Directory によってデバイスが Intune MDM サービスに登録されます。 ネットワーク通信の要件の詳細については、「 <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">Intune のネットワーク構成の要件と帯域幅</a>」を参照してください。
<tr><td><b>Windows Update<b><td>OOBE プロセス中に加えて Windows 10 OS が完全に構成された後は、Windows Update サービスを利用して必要な更新プログラムが取得されます。 Windows Update に接続するときに問題が発生した場合は、 <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">Windows Update または Microsoft Update に関する接続の問題を解決する方法に関する説明</a>を参照してください。<br>

Windows Update にアクセスできない場合でも、自動操縦プロセスは続行されますが、重要な更新プログラムは使用できません。

<tr><td><b>配信の最適化<b><td>Windows 更新プログラム Microsoft Store、アプリとアプリの更新プログラム、Office 更新プログラム、および Intune Win32 アプリをダウンロードするときに、 <a href="https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization">配信最適化</a> サービスに連絡して、インターネットからのダウンロードを必要とするデバイスがごく少数になるように、コンテンツをピアツーピアで共有できるようにします。<br>

配信最適化サービスにアクセスできない場合でも、自動操縦プロセスは、(ピアツーピアではなく) クラウドから配信の最適化のダウンロードを続行します。

<tr><td><b>ネットワークタイムプロトコル (NTP) の同期<b><td>Windows デバイスが起動すると、デバイスの時刻が正確であることを確認するために、ネットワークタイムサーバーと通信します。 time.windows.com への UDP ポート 123 にアクセスできることを確認します。
<tr><td><b>ドメインネームサービス (DNS)<b><td>すべてのサービスの DNS 名を解決するため、デバイスは DNS サーバーと通信します (通常は DHCP 経由で提供されます)。この DNS サーバーは、インターネット上の名前を解決できる必要があります。
<tr><td><b>診断データ<b><td>Windows 10 1903 以降では、診断データの収集が既定で有効になります。 Windows Analytics および関連する診断機能を無効にする方法については、「 <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">Manage enterprise diagnostics data level</a>」を参照してください。<br>

診断データを送信できない場合でも、自動操縦プロセスは続行されますが、Windows Analytics などの診断データに依存するサービスは機能しません。
<tr><td><b>ネットワーク接続状態インジケーター (NCSI)<b><td>Windows は、デバイスがインターネットにアクセスできることを通知できる必要があります。 詳細については、「 <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">ネットワーク接続状態インジケーター (NCSI)</a>」を参照してください。

<code>www.msftconnecttest.com</code> DNS で解決可能で、HTTP 経由でアクセス可能である必要があります。
<tr><td><b>Windows Notification Services (WNS)<b><td>このサービスを使って、Windows がアプリとサービスから通知を受け取ることができるようにします。 詳細については、「 <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a> 」を参照してください。<br>

WNS サービスを使用できない場合でも、自動操縦プロセスは通知なしで続行されます。
<tr><td><b>Microsoft Store、Microsoft Store for Business<b><td>Microsoft Store 内のアプリは、Intune (MDM) 経由でトリガーしてデバイスにプッシュすることができます。ユーザーが最初にログインするとき、アプリの更新プログラムとその他のアプリも必要になることがあります。 詳細については、「 <a href="https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business">ビジネス向け Microsoft Store および教育機関向けの前提条件</a> (Azure AD と Windows Notification Services も含まれます)」を参照してください。<br>

Microsoft Store にアクセスできない場合でも、Microsoft Store アプリがなくても、自動操縦プロセスは続行されます。

<tr><td><b>Office 365<b><td>Intune デバイス構成の一部として、enterprise 用 Microsoft 365 アプリのインストールが必要になる場合があります。 詳細については、「 <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">office 365 の url と ip アドレスの範囲</a> 」を参照してください (すべての office サービス、DNS 名、ip アドレスが含まれます。また、上記のサービスと重複する可能性がある他のサービスも Azure AD 含まれます)。
<tr><td><b>証明書失効リスト (Crl)<b><td>これらのサービスの一部は、証明書失効リスト (CRL) にサービスで使用される証明書がないか確認する必要もあります。これらの完全な一覧については、「 <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">office 365 の url と IP アドレスの範囲</a> 」と「 <a href="https://aka.ms/o365chains">Office 365 証明書チェーン</a>」をご覧ください。
<tr><td><b>ハイブリッド AAD 参加<b><td>デバイスをハイブリッド AAD に参加させることができます。 ハイブリッド AAD 参加を機能させるには、コンピューターが企業ネットワーク上にある必要があります。 詳細については<a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">、「Windows 自動操縦のユーザー主導モード」を</a>参照してください。
<tr><td><b>自動展開モードと自動操縦用ホワイトグローブ<b><td>Intel、AMD、または Qualcomm によってのみ提供されるファームウェア TPM デバイスでは、起動時に必要なすべての証明書が含まれておらず、最初に使用したときに製造元から取得できる必要があります。 (他の製造元のデバイスを含む) 個別の TPM チップを搭載したデバイスには、これらの証明書がプレインストールされています。 詳細については、 <a href="https://docs.microsoft.com/windows/security/information-protection/tpm/tpm-recommendations">TPM に関する推奨事項</a> を参照してください。 証明書を正常に要求できるように、各ファームウェア TPM プロバイダーでこれらの Url にアクセスできることを確認します。 

  <br>Intel- https://www.intel.com/  <br>Qualcomm- https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1  <br>AMD https://ftpm.amd.com/pki/aia

</table>

## <a name="licensing-requirements"></a>ライセンスの要件

Windows の自動操縦は、Windows 10 および Azure Active Directory で使用できる特定の機能に依存します。 また、Microsoft Intune などの MDM サービスも必要です。 これらの機能は、さまざまなエディションおよびサブスクリプション プログラムを通じて入手できます。

必要な Azure Active Directory (MDM の自動登録と会社のブランド化機能) と MDM 機能を提供するには、次のいずれかが必要です。
- [Premium サブスクリプションの Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1 または F3 サブスクリプション](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 アカデミック A1、A3、または A5 サブスクリプション](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise E3 または E5 サブスクリプション](https://www.microsoft.com/microsoft-365/enterprise)。すべての Windows 10、Office 365、EM + S の機能 (Azure AD と Intune) が含まれています。
- [Enterprise Mobility + Security E3 または E5 サブスクリプション](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)。必要なすべての Azure AD と Intune の機能が含まれています。
- [Intune for Education サブスクリプション](https://docs.microsoft.com/intune-education/what-is-intune-for-education)。必要なすべての Azure AD と Intune の機能が含まれます。
- [Azure Active Directory Premium P1、P2](https://azure.microsoft.com/services/active-directory/) 、 [Microsoft Intune サブスクリプション](https://www.microsoft.com/cloud-platform/microsoft-intune) (または代替 MDM サービス)。

> [!NOTE]
> Microsoft 365 サブスクリプションを使用している場合でも、 [Intune のライセンスをユーザーに割り当てる](https://docs.microsoft.com/intune/fundamentals/licenses-assign)必要があります。

また、次のものも推奨されます (必須ではありません)。
- [Microsoft 365 enterprise 用アプリ](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0)。 Intune (またはその他の MDM サービス) を使用して簡単に展開できます。
- Windows 10 Pro から Windows 10 Enterprise にデバイスを自動的にステップアップする[Windows サブスクリプションのライセンス認証](https://docs.microsoft.com/windows/deployment/windows-10-enterprise-subscription-activation)。

## <a name="configuration-requirements"></a>構成要件

Windows 自動操縦を使用する前に、一般的な自動操縦シナリオをサポートするためにいくつかの構成タスクが必要です。  

- Azure Active Directory の自動登録を構成します。  Microsoft Intune については、「 [Windows 10 の自動登録を有効にする](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) 」を参照してください。  別の MDM サービスを使用している場合は、そのサービスに必要な特定の Url または構成についてベンダーに問い合わせてください。
- Azure Active Directory カスタムブランド化を構成します。  自動操縦プロセス中に組織固有のログオンページを表示するには、表示するイメージとテキストで Azure Active Directory を構成する必要があります。  詳細については [、「クイックスタート: Azure AD のサインインページに会社のブランドを追加する](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) 」を参照してください。  "正方形のロゴ" と "サインインページのテキスト" は、自動操縦の重要な要素であり、Azure Active Directory テナント名 (Azure AD テナントのプロパティで個別に構成されます) であることに注意してください。
- Windows 10 Pro から Windows 10 Enterprise に自動的にステップアップするために、必要に応じて [Windows サブスクリプションのアクティブ化](https://docs.microsoft.com/windows/deployment/windows-10-enterprise-subscription-activation) を有効にします。

その場合、特定のシナリオには追加の要件があります。  一般に、次の2つのタスクがあります。

- デバイス登録。  Windows の自動操縦のシナリオをサポートするには、Windows 自動操縦にデバイスを追加する必要があります。  詳細については、「 [Windows 自動操縦にデバイスを追加する](add-devices.md) 」を参照してください。
- プロファイルの構成。  デバイスが Windows 自動操縦装置に追加されたら、設定のプロファイルを各デバイスに適用する必要があります。  詳細については、「 [自動操縦プロファイルの構成](profiles.md) 」をご覧ください。  このプロファイルの割り当ては、Microsoft Intune が自動化できることに注意してください。詳細については、「 [自動操縦デバイスグループの作成](https://docs.microsoft.com/intune/enrollment-Autopilot#create-an-Autopilot-device-group) 」および「 [デバイスグループへの自動展開プロファイルの割り当て](https://docs.microsoft.com/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group) 」を参照してください。

詳細については、「 [Windows 自動操縦のシナリオ](windows-Autopilot-scenarios.md) 」を参照してください。

これらの手順と関連する手順のチュートリアルについては、次のビデオを参照してください。

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


[Windows 10 を実行するための要件](https://www.microsoft.com/windows/windows-10-specifications)以外に、Windows 10 Autopilot を使用するための追加のハードウェア要件はありません

## <a name="related-topics"></a>関連トピック

[Windows 自動操縦の概要](windows-Autopilot.md)
