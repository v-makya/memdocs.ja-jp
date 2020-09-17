---
title: デバイスの追加
ms.reviewer: ''
manager: laurawi
description: Windows 自動操縦にデバイスを追加する方法
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
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
ms.openlocfilehash: 776cc47865853ae9b52218c0b2257840aea09219
ms.sourcegitcommit: 2339c927b6576db8878f34f167a9a45c5dc9f58d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90689333"
---
# <a name="adding-devices-to-windows-autopilot"></a>Windows 自動操縦にデバイスを追加する

**適用対象**

- Windows 10

Windows 自動操縦を使用してデバイスを展開する前に、デバイスを Windows 自動操縦展開サービスに登録する必要があります。 この登録は、デバイスを購入した OEM、リセラー、またはディストリビューターによって実行されるのが理想的です。 ただし、ハードウェア id を収集して手動でアップロードすることで、組織内で登録を行うこともできます。

## <a name="oem-registration"></a>OEM 登録

OEM からデバイスを購入すると、その OEM はデバイスを Windows 自動操縦装置に自動的に登録することができます。 登録をサポートしている Oem の一覧については、「 [Windows 自動操縦」ページ](https://aka.ms/windowsautopilot)の「参加者のデバイスの製造元および再販業者」セクションを参照してください。

OEM が組織のデバイスを登録する前に、組織は OEM のアクセス許可を付与する必要があります。 OEM は、このプロセスを開始します。このプロセスは、Azure AD のグローバル管理者によって組織から付与されます。 [お客様の同意ページ](registration-auth.md#oem-authorization)の「お客様の同意」セクションを参照してください。

> [!Note]
> ハードウェアハッシュ (ハードウェア Id とも呼ばれます) は、OEM デバイス製造プロセスの一部として生成されますが、お客様または CSP パートナーに直接提供することはできません。 代わりに、OEM はデバイスを顧客の代理として登録する必要があります。 デバイスが CSP パートナーによって登録されている場合、Oem はデバイス登録プロセスをサポートするために、これらのパートナーに PKID 情報を提供することができます。

## <a name="reseller-distributor-or-partner-registration"></a>リセラー、代理店、またはパートナー登録

お客様は、リセラー、代理店、またはその他のパートナーからデバイスを購入できます。 これらの再販業者、販売代理店、パートナーは、 [クラウドソリューションパートナー (CSP) プログラム](https://partner.microsoft.com/cloud-solution-provider)の一部である限り、お客様にデバイスを登録できます。 

Oem と同様に、CSP パートナーは、組織のデバイスを登録するためのアクセス許可を付与する必要があります。 [お客様の同意ページ](registration-auth.md#csp-authorization)で説明されているプロセスを使用できます。 CSP パートナーが組織との関係を要求します。 組織の全体管理者が要求を承認します。 承認後、CSP パートナーは、web サイトから直接、または同じタスクを自動化できる利用可能な Api を介して、 [パートナーセンター](https://partner.microsoft.com/pcv/dashboard/overview)を使用してデバイスを追加します。

Surface デバイスの場合、Microsoft サポートはデバイスの登録に役立ちます。  詳細については、「 [Windows 自動操縦の Surface Registration サポート](https://docs.microsoft.com/surface/surface-autopilot-registration-support)」を参照してください。

CSP パートナーと組織の間の関係を確立するときに、Windows 自動操縦の管理者権限は必要ありません。 グローバル管理者の承認プロセスの一環として、[委任された管理アクセス許可を含める] チェックボックスをオフにすることができます。

> [!Note]
> リセラー、販売代理店、またはパートナーは、新しい Windows デバイスを起動してハードウェアハッシュを取得することができますが (顧客に提供したり、パートナーが直接登録したりするため)、この方法はお勧めできません。 代わりに、これらのパートナーは、デバイスのパッケージ化 (バーコード) から取得した PKID 情報を使用するか、OEM または上流のパートナー (たとえば、ディストリビューター) から電子的に取得したデバイスを登録する必要があります。

## <a name="automatic-registration-of-existing-devices"></a>既存のデバイスの自動登録

次の場合は、既存のデバイスを自動的に登録できます。
- サポートされているバージョンの Windows 10 半期チャネルを実行しています。
- Intune などの MDM サービスに登録されている。

両方の要件を満たすデバイスの場合、MDM サービスはデバイスにハードウェアハッシュを要求できます。 その後、デバイスを Windows 自動操縦に自動的に登録できます。

Microsoft Intune でこの操作を行う方法については、「すべての対象デバイスを自動操縦に変換する」設定を説明している「 [自動操縦展開プロファイルの作成](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) 」を参照してください。 

Intune の **すべての対象デバイスを自動操縦する設定に変換** することで、このようなデバイスを Windows に自動的に変換できます。 詳しくは、「[Autopilot Deployment プロファイルを作成する](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile)」をご覧ください。 

[既存のデバイスに対して Windows 自動操縦](existing-devices.md)を使用する場合、デバイスを Windows 自動操縦装置に事前登録する必要はありません。 代わりに、すべての Windows 自動操縦プロファイルの設定を含む構成ファイル (AutopilotConfigurationFile.js) が使用されます。 デバイスは、[すべての対象となるデバイスを自動操縦に変換する] 設定を使用して、Windows 自動操縦に登録できます。

## <a name="manual-registration"></a>手動登録

デバイスを手動で登録するには、まずハードウェアハッシュをキャプチャする必要があります。 このプロセスが完了すると、生成されたハードウェアハッシュを Windows 自動操縦サービスにアップロードできます。 このプロセスでは、ハードウェアハッシュを取得するためにデバイスを Windows 10 で起動する必要があるため、手動登録は主にテストおよび評価シナリオに使用されます。

> [!Note]
> お客様は、ハードウェアハッシュを使用してのみデバイスを登録できます。 その他の方法 (PKID、タプル) は、前のセクションで説明したように、Oem または CSP パートナーから入手できます。

## <a name="device-identification"></a>デバイスの識別

Windows 自動操縦装置を使用してデバイスを識別するには、デバイスの固有のハードウェアハッシュをキャプチャしてサービスにアップロードする必要があります。 この手順は、ハードウェアベンダー (OEM、リセラー、またはディストリビューター) によって、デバイスと組織の関連付けが自動的に行われる場合に最適です。 また、実行中の Windows 10 インストール内からデバイスを収集するプロセスを使用して、デバイスを識別することもできます。

ハードウェアハッシュには、デバイスの詳細が含まれています。
- manufacturer
- model
- デバイスのシリアル番号
- ハードドライブのシリアル番号
- ID が生成された日時の詳細
- デバイスを一意に識別するために使用できるその他の多くの属性

生成されたタイミングに関する詳細が含まれているため、生成されるたびにハードウェアハッシュが変更されます。 Windows 自動操縦展開サービスがデバイスとの照合を試みると、そのような変更が考慮されます。 また、新しいハードドライブなどの大きな変更を考慮し、正常に一致させることもできます。 ただし、マザーボード交換など、ハードウェアに大きな変更を加えても、新しいハッシュを生成してアップロードする必要があります。

### <a name="collecting-the-hardware-hash-from-existing-devices-using-microsoft-endpoint-configuration-manager"></a>Microsoft エンドポイントを使用して既存のデバイスからハードウェアハッシュを収集する Configuration Manager

Microsoft Endpoint Configuration Manager は、既存の Windows 10 デバイスのハードウェアハッシュを自動的に収集します。 詳細については、「 [Windows 自動操縦の Configuration Manager から情報を収集](/configmgr/comanage/how-to-prepare-win10#windows-autopilot)する」を参照してください。 ハッシュ情報は Configuration Manager から CSV ファイルに抽出できます。

> [!Note]
> Intune に CSV ファイルをアップロードする前に、最初の行にデバイスのシリアル番号、Windows 製品 ID、ハードウェアハッシュ、グループタグ、割り当てられたユーザーが含まれていることを確認してください。 CSV ファイルの先頭にヘッダー情報がある場合は、そのヘッダー情報を削除してください。 詳細について [は、「Intune での Windows デバイスの登録」を](/intune/enrollment/enrollment-autopilot)参照してください。

### <a name="collecting-the-hardware-hash-from-existing-devices-using-powershell"></a>PowerShell を使用した既存のデバイスからのハードウェアハッシュの収集

既存のデバイスのハードウェアハッシュは、そのデバイスでサポートされているバージョンの Windows 10 半期チャネルが実行されている限り、Windows Management Instrumentation (WMI) を介して利用できます。 PowerShell スクリプト ([Get-WindowsAutoPilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)) を使用して、デバイスのハードウェアハッシュとシリアル番号を取得できます。 シリアル番号は、ハードウェアハッシュが属するデバイスをすばやく確認するのに役立ちます。

このスクリプトを使用するには、次のいずれかの方法を使用できます。
- PowerShell ギャラリーからダウンロードし、各コンピューターで実行します。
- PowerShell ギャラリーから直接インストールします。

ローカルコンピューターからハードウェアハッシュを直接インストールしてキャプチャするには、管理者特権の Windows PowerShell プロンプトから次のコマンドを使用します。

```powershell
md c:\\HWID
Set-Location c:\\HWID
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

次の両方に該当する場合は、コマンドをリモートで実行できます。
- WMI アクセス許可が適用されています
- WMI は、リモートコンピューターの Windows ファイアウォールを介してアクセスできます。

スクリプトの実行の詳細につい [ては、](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) 「get-help Get-WindowsAutoPilotInfo.ps1」を参照してください。

>[!IMPORTANT]
>ハードウェアハッシュをキャプチャし、自動操縦用デバイスプロファイルを作成する前に、デバイスをインターネットに接続しないでください。 これには、ハードウェアハッシュの収集、のアップロードも含まれます。MSfB または Intune に CSV を、プロファイルを割り当て、プロファイルの割り当てを確認します。 このプロセスが完了する前にデバイスをインターネットに接続すると、デバイスは、明示的が削除されるまでデバイスに保存されている空のプロファイルをダウンロードします。 Windows 10 バージョン1809では、OOBE を再起動することで、キャッシュされたプロファイルをクリアできます。 以前のバージョンでは、保存されたプロファイルをクリアする唯一の方法は、OS の再インストール、PC の再イメージ化、または **sysprep/generalize/oobe**の実行です。 <br>
>Intune でプロファイルの準備が完了したら、デバイスがインターネットに接続されている必要があります。

>[!NOTE]
>OOBE を再起動する回数が多すぎると、復旧モードに入り、自動操縦の構成を実行できません。 このシナリオは、OOBE.XML によって、言語、地域、キーボードレイアウトなど、同じページに複数の構成オプションが表示されている場合に識別できます。 通常の OOBE では、これらはそれぞれ個別のページに表示されます。 次の値のキーは、OOBE の再試行の数を追跡します。 <br>
>**HKCU\ software \\ Microsoft \\ Windows \\ CurrentVersion \\ useroobe** <br>
>OOBE が何度も再起動されていないことを確認するには、この値を1に変更します。

## <a name="registering-devices"></a>デバイスの登録

<img src="./images/image2.png" width="511" height="249" alt="process" />


既存のデバイスからハードウェアハッシュをキャプチャした後は、次のいずれかの方法でアップロードできます。

- [Microsoft Intune](enrollment-autopilot.md)。 これは、すべてのお客様に推奨されるメカニズムです。
  - Microsoft Endpoint Manager 管理センターは、Intune のデバイス登録に使用されます。
- [パートナーセンター](https://msdn.microsoft.com/partner-center/autopilot)。 これは、ユーザーに代わってデバイスを登録するために CSP パートナーによって使用されます。
- [& Office 365 管理者を Microsoft 365 Business](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa)します。通常、これは、Microsoft 365 Business を使用してデバイスを管理する中小企業 (Smb) によって使用されます。
- [ビジネス向け Microsoft Store](/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles)。 アプリと設定の管理には、既に MSfB を使用している可能性があります。

各プラットフォームの機能の概要については、以下を参照してください。<br>
<br>
<table>
<tr>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">プラットフォーム/ポータル</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">デバイスを登録しますか?</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">プロファイルの作成/割り当て</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">許容される DeviceID</font></td>
</tr>

<tr>
<td>OEM Direct API</td>
<td>はい-最大で1000</td>
<td>NO</td>
<td>タプルまたは PKID</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/partner-center/autopilot">パートナー センター</a></td>
<td>はい-最大で1000</td>
<td>はい<b><sup>34</sup></b></td>
<td>タプルまたは PKID または 4K HH</td>
</tr>

<tr>
<td><a href="enrollment-autopilot.md">Intune</a></td>
<td>はい-500 時に最大<b><sup>1</sup></b></td> 
<td>はい<b><sup>12</sup></b></td> 
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles">ビジネス向け Microsoft ストア</a></td>
<td>はい-最大で1000</td>
<td>はい<b><sup>4</sup></b></td>
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 Business Premium</a></td>
<td>はい-最大で1000</td>
<td>はい<b><sup>3</sup></b></td>
<td>4K HH</td>
</tr>

</table>

><b><sup>1</sup></b>使用する Microsoft 推奨プラットフォーム<br>
><b><sup>2</sup></b>Intune のライセンスが必要です<br>
><b><sup>3</sup></b>機能の機能は制限されています<br>
><b><sup>4</sup></b>デバイスプロファイルの割り当ては、今後数か月の間、MSfB とパートナーセンターから廃止される予定です。<br>

デバイス Id の詳細については、次のトピックを参照してください。
- [デバイスの識別](#device-identification)
- [Windows 自動操縦用デバイスのガイドライン](autopilot-device-guidelines.md)
- [顧客アカウントへのデバイスの追加](/partner-center/autopilot)


## <a name="summary"></a>まとめ

Windows 自動操縦を使用して新しいデバイスを展開する場合は、次の手順を実行する必要があります。

1. [デバイスを登録](#registering-devices)します。 理想的には、この手順は、デバイスを購入した OEM、リセラー、またはディストリビューターによって実行されます。 ただし、ハードウェア id を収集して手動でアップロードすることで、組織が登録を行うこともできます。
2. [デバイスプロファイルを構成](profiles.md)します。 デバイスの展開方法と、表示するユーザーエクスペリエンスを指定します。
3. デバイスを起動します。 デバイスがインターネットにアクセスできるネットワークに接続されている場合、デバイスが登録されているかどうかを確認するために、Windows 自動展開サービスに連絡します。 登録されている場合は、エンドユーザーエクスペリエンスをカスタマイズするために使用される、 [登録ステータスページ](enrollment-status.md)などのプロファイル設定がダウンロードされます。

## <a name="next-steps"></a>次の手順

[Bitlocker 暗号化設定](bitlocker.md): 自動暗号化を開始する前に適用する bitlocker 暗号化設定を構成できます。
