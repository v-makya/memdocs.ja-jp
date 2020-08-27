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
ms.openlocfilehash: b8737646946e1c575ddb8ebdd26397712c412e20
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908570"
---
# <a name="adding-devices-to-windows-autopilot"></a>Windows 自動操縦にデバイスを追加する

**適用対象**

- Windows 10

Windows 自動操縦を使用してデバイスを展開する前に、デバイスを Windows 自動操縦展開サービスに登録する必要があります。 これは、デバイスを購入した OEM、リセラー、またはディストリビューターによって実行されるのが理想的ですが、ハードウェア id を収集して手動でアップロードすることによって、組織がこれを行うこともできます。

## <a name="oem-registration"></a>OEM 登録

OEM から直接デバイスを購入すると、その OEM はデバイスを Windows 自動操縦展開サービスに自動的に登録することができます。  現在この機能をサポートしている Oem の一覧については、「 [Windows 自動操縦情報」ページ](https://aka.ms/windowsautopilot)の「参加者のデバイスの製造元および再販業者」セクションを参照してください。

OEM が組織に代わってデバイスを登録する前に、組織は OEM のアクセス許可を付与する必要があります。  このプロセスは OEM によって開始され、Azure AD のグローバル管理者によって組織から付与されます。  [お客様の同意ページ](registration-auth.md#oem-authorization)の「お客様の同意」セクションを参照してください。

> [!Note]
> ハードウェアハッシュは、OEM デバイス製造プロセスの一部として生成されますが、お客様または CSP パートナーに直接提供する必要はありません。  代わりに、OEM はデバイスを顧客の代理として登録する必要があります。  デバイスが CSP パートナーによって登録されている場合、Oem はデバイス登録プロセスをサポートするために、これらのパートナーに PKID 情報を提供することができます。

## <a name="reseller-distributor-or-partner-registration"></a>リセラー、代理店、またはパートナー登録

お客様は、リセラー、代理店、またはその他のパートナーからデバイスを購入できます。  これらの再販業者、販売代理店、パートナーは、 [クラウドソリューションパートナー (CSP) プログラム](https://partner.microsoft.com/cloud-solution-provider)の一部である限り、お客様に代わってデバイスを登録することができます。  

Oem と同様、CSP パートナーには、組織に代わってデバイスを登録するためのアクセス許可を付与する必要があります。  これは、 [お客様の同意ページ](registration-auth.md#csp-authorization)で説明されている手順に従います。  CSP パートナーが組織との関係を確立する要求を開始し、組織のグローバル管理者によって承認されます。  CSP パートナーは、承認が完了すると、web サイトから直接、または同じタスクを自動化できる利用可能な Api を介して、 [パートナーセンター](https://partner.microsoft.com/pcv/dashboard/overview)を使用してデバイスを追加します。

CSP パートナーと組織の間の関係を確立するときに、Windows の自動操縦によって委任された管理者のアクセス許可は必要ありません。  全体管理者によって実行される承認プロセスの一環として、全体管理者は [委任された管理アクセス許可を含める] チェックボックスをオフにすることができます。

> [!Note]
> リセラー、代理店、またはパートナーは、新しい Windows デバイスを起動してハードウェアハッシュを取得することもできますが (顧客に提供するため、またはパートナーが直接登録するため)、この方法はお勧めしません。  代わりに、これらのパートナーは、デバイスのパッケージ化 (バーコード) から取得した PKID 情報を使用するか、OEM または上流のパートナー (たとえば、ディストリビューター) から電子的に取得したデバイスを登録する必要があります。

## <a name="automatic-registration-of-existing-devices"></a>既存のデバイスの自動登録

既存のデバイスが、サポートされているバージョンの Windows 10 半期チャネルを既に実行していて、Intune などの MDM サービスに登録されている場合、MDM サービスはデバイスにハードウェア ID (ハードウェアハッシュとも呼ばれます) を要求できます。  その後、デバイスを Windows 自動操縦に自動的に登録することができます。

Microsoft Intune でこの操作を行う方法については、「すべての対象デバイスを自動操縦に変換する」設定を説明している「 [自動操縦展開プロファイルの作成](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) 」を参照してください。 

また、 [既存のデバイスに対して Windows 自動操縦](existing-devices.md) を使用する場合は、デバイスを Windows 自動操縦装置に事前登録する必要がないことに注意してください。  代わりに、すべての Windows 自動操縦プロファイル設定を含む構成ファイル (AutopilotConfigurationFile.js) が使用されます。デバイスは、"すべての対象デバイスを自動操縦に変換する" 設定を使用して、Windows 自動操縦に登録できます。

## <a name="manual-registration"></a>手動登録

デバイスの手動登録を実行するには、まずハードウェア ID (ハードウェアハッシュとも呼ばれます) をキャプチャする必要があります。  このプロセスが完了すると、生成されたハードウェア ID を Windows 自動操縦サービスにアップロードできます。  このプロセスでは、ハードウェア ID を取得するためにデバイスを Windows 10 で起動する必要があるため、これは主にテストと評価のシナリオに使用されます。

> [!Note]
> お客様は、ハードウェアハッシュを使用してのみデバイスを登録できます。  その他の方法 (PKID、タプル) は、前のセクションで説明したように、Oem または CSP パートナーから入手できます。

## <a name="device-identification"></a>デバイスの識別

Windows 自動展開サービスにデバイスを定義するには、デバイスの一意のハードウェア ID をキャプチャしてサービスにアップロードする必要があります。 この手順は、ハードウェアベンダー (OEM、リセラー、またはディストリビューター) によって実行されるのが理想的ですが、デバイスを組織に自動的に関連付けることもできます。また、実行中の Windows 10 インストール内からデバイスを収集するプロセスを使用して行うこともできます。

ハードウェア ID (一般にハードウェアハッシュとも呼ばれます) には、デバイスの製造元、モデル、デバイスのシリアル番号、ハードドライブのシリアル番号など、デバイスを一意に識別するために使用できる多くの属性が含まれています。

ハードウェアハッシュには、生成された時点の詳細も含まれているため、生成されるたびに変更されることに注意してください。 Windows 自動操縦展開サービスがデバイスとの照合を試みると、そのような変更や、新しいハードドライブなどの大幅な変更が考慮され、それでも正常に一致することができます。 ただし、マザーボード交換などのハードウェアの大幅な変更は一致しないため、新しいハッシュを生成してアップロードする必要があります。

### <a name="collecting-the-hardware-id-from-existing-devices-using-microsoft-endpoint-configuration-manager"></a>Microsoft エンドポイントを使用して既存のデバイスからハードウェア ID を収集する Configuration Manager

Microsoft Endpoint Configuration Manager は、既存の Windows 10 デバイスのハードウェアハッシュを自動的に収集します。 詳細については、「 [Windows 自動操縦の Configuration Manager から情報を収集](/configmgr/comanage/how-to-prepare-win10#windows-autopilot)する」を参照してください。 ハッシュ情報は Configuration Manager から CSV ファイルに抽出できます。

> [!Note]
> Intune に CSV ファイルをアップロードする前に、最初の行にデバイスのシリアル番号、Windows 製品 ID、ハードウェアハッシュ、グループタグ、割り当てられたユーザーが含まれていることを確認してください。 CSV ファイルの先頭にヘッダー情報がある場合は、そのヘッダー情報を削除してください。 詳細について [は、「Intune での Windows デバイスの登録」を](/intune/enrollment/enrollment-autopilot)参照してください。

### <a name="collecting-the-hardware-id-from-existing-devices-using-powershell"></a>PowerShell を使用した既存のデバイスからのハードウェア ID の収集

既存のデバイスのハードウェア ID またはハードウェアハッシュは、デバイスがサポートされているバージョンの Windows 10 半期チャネルを実行している限り、Windows Management Instrumentation (WMI) を介して利用できます。 この情報と、デバイスのシリアル番号 (コンピューターが属するコンピューターを一目で確認するのに役立ちます) を収集するために、Get-WindowsAutoPilotInfo.ps1 という名前の PowerShell スクリプト [ が PowerShell ギャラリー web サイトに公開されて](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)います。

このスクリプトを使用するには、PowerShell ギャラリーからダウンロードし、各コンピューターで実行するか、PowerShell ギャラリーから直接インストールすることができます。 ローカルコンピューターからハードウェアハッシュを直接インストールしてキャプチャするには、管理者特権の Windows PowerShell プロンプトから次のコマンドを使用します。

```powershell
md c:\\HWID
Set-Location c:\\HWID
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

WMI アクセス許可が適用されていて、そのリモートコンピューターの Windows ファイアウォール経由で WMI にアクセスできる限り、コマンドをリモートで実行することもできます。 スクリプトの実行の詳細については、 [WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) スクリプトのヘルプ ("get-help Get-WindowsAutoPilotInfo.ps1" を使用) を参照してください。

>[!IMPORTANT]
>ハードウェア ID をキャプチャし、自動操縦用デバイスプロファイルを作成する前に、デバイスをインターネットに接続しないでください。 これには、ハードウェア ID の収集、のアップロードも含まれます。MSfB または Intune に CSV を、プロファイルを割り当て、プロファイルの割り当てを確認します。 このプロセスが完了する前にデバイスをインターネットに接続すると、デバイスは、明示的が削除されるまでデバイスに保存されている空のプロファイルをダウンロードします。 Windows 10 バージョン1809では、OOBE を再起動することで、キャッシュされたプロファイルをクリアできます。 以前のバージョンでは、保存されたプロファイルをクリアする唯一の方法は、OS の再インストール、PC の再イメージ化、または **sysprep/generalize/oobe**の実行です。 <br>
>Intune でプロファイルの準備が完了したら、デバイスがインターネットに接続されている必要があります。

>[!NOTE]
>OOBE を再起動する回数が多すぎると、復旧モードに入り、自動操縦の構成を実行できません。 このシナリオは、OOBE.XML によって、言語、地域、キーボードレイアウトなど、同じページに複数の構成オプションが表示されている場合に識別できます。 通常の OOBE では、これらはそれぞれ個別のページに表示されます。 次の値のキーは、OOBE の再試行の数を追跡します。 <br>
>**HKCU\ software \\ Microsoft \\ Windows \\ CurrentVersion \\ useroobe** <br>
>OOBE が何度も再起動されていないことを確認するには、この値を1に変更します。

## <a name="registering-devices"></a>デバイスの登録

<img src="./images/image2.png" width="511" height="249" alt="process" />


ハードウェア Id は、既存のデバイスからキャプチャされた後、さまざまな方法でアップロードできます。 使用可能な各メカニズムの詳細なドキュメントを参照してください。

-   [Microsoft Intune](enrollment-autopilot.md)。  これは、すべてのお客様に推奨されるメカニズムです。
    - Microsoft Endpoint Manager 管理センターは、Intune のデバイス登録に使用されます。
-   [パートナーセンター](https://msdn.microsoft.com/partner-center/autopilot)。  これは、ユーザーに代わってデバイスを登録するために CSP パートナーによって使用されます。
-   [& Office 365 管理者を Microsoft 365 Business](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa)します。 通常、これは、Microsoft 365 Business を使用してデバイスを管理する中小企業 (Smb) によって使用されます。
-   [ビジネス向け Microsoft Store](/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles)。  アプリと設定の管理には、既に MSfB を使用している可能性があります。

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
<td><a href="https://docs.microsoft.com/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 Business</a></td>
<td>はい-最大で1000</td>
<td>はい<b><sup>3</sup></b></td>
<td>4K HH</td>
</tr>

</table>

><b><sup>1</sup></b>使用する Microsoft 推奨プラットフォーム<br>
><b><sup>2</sup></b>Intune のライセンスが必要です<br>
><b><sup>3</sup></b>機能の機能は制限されています<br>
><b><sup>4</sup></b>デバイスプロファイルの割り当ては、今後数か月の間、MSfB とパートナーセンターから廃止される予定です。<br>


デバイス Id の詳細については、次のトピックも参照してください。
- [デバイスの識別](#device-identification)
- [Windows 自動操縦用デバイスのガイドライン](autopilot-device-guidelines.md)
- [顧客アカウントへのデバイスの追加](/partner-center/autopilot)


## <a name="summary"></a>まとめ

Windows 自動操縦を使用して新しいデバイスを展開する場合は、次の手順を実行する必要があります。

1.  [デバイスを登録](#registering-devices)します。 この手順は、デバイスを購入した OEM、リセラー、またはディストリビューターによって実行されるのが理想的ですが、ハードウェア id を収集して手動でアップロードすることで、組織が行うこともできます。
2.  デバイス[プロファイルを構成](profiles.md)して、デバイスの展開方法と表示するユーザーエクスペリエンスを指定します。
3.  デバイスを起動します。 デバイスがインターネットにアクセスできるネットワークに接続されている場合、デバイスが登録されているかどうか、およびデバイスが登録されているかどうかを確認するために、Windows 自動展開サービスに連絡します。これは、エンドユーザーエクスペリエンスをカスタマイズするために使用される、 [登録ステータスページ](enrollment-status.md)などのプロファイル設定をダウンロードします。

## <a name="other-configuration-settings"></a>その他の構成設定

- [Bitlocker 暗号化設定](bitlocker.md): 自動暗号化を開始する前に適用する bitlocker 暗号化設定を構成できます。