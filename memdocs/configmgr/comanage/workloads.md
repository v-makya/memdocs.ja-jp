---
title: 共同管理ワークロード
titleSuffix: Configuration Manager
description: Configuration Manager から Microsoft Intune に切り替えることができるワークロードについて学習します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 0425b937062acd96b8df66df38ec53a04e91b4de
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995230"
---
# <a name="co-management-workloads"></a>共同管理ワークロード

ワークロードを切り替える必要はありません。準備ができたときに個別に行うこともできます。 Configuration Manager では、Intune に切り替えないワークロードを含む、他のすべてのワークロードと、共同管理でサポートされない Configuration Manager の他のすべての機能が引き続き管理されます。

ワークロードを Intune に切り替えても、後で気が変わった場合は、Configuration Manager に戻すことができます。

共同管理では次のワークロードがサポートされます。

- [コンプライアンス ポリシー](#compliance-policies)  

- [Windows Update のポリシー](#windows-update-policies)  

- [リソースのアクセス ポリシー](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [デバイス構成](#device-configuration)  

- [Office クイック実行アプリ](#office-click-to-run-apps)  

- [クライアント アプリ](#client-apps)  

## <a name="compliance-policies"></a>コンプライアンス ポリシー

コンプライアンス ポリシーは、デバイスが条件付きアクセス ポリシーによって "準拠している" と見なされるために遵守する必要がある規則および設定を定義します。 また、コンプライアンス ポリシーを使用して、条件付きアクセスとは別に、デバイスのコンプライアンスに関する問題を監視および修復します。 Configuration Manager バージョン 1910 より、コンプライアンス ポリシー評価の規則として、カスタム構成基準の評価を追加できるようになりました。 詳細については、「[コンプライアンス ポリシー評価の一部としてカスタム構成基準を含める](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)」を参照してください。

Intune 機能の詳細については、「[デバイス コンプライアンス ポリシー](/intune/device-compliance-get-started)」を参照してください。  

## <a name="windows-update-policies"></a>Windows Update のポリシー

Windows Update for Business ポリシーでは、Windows Update for Business によって直接管理されている Windows 10 デバイスの Windows 10 機能更新プログラムまたは品質更新プログラムに対し、遅延ポリシーを構成できます。

Intune 機能の詳細については、[Windows Update for Business 遅延ポリシーの構成](/intune/windows-update-for-business-configure)に関するページを参照してください。  

## <a name="resource-access-policies"></a>リソースのアクセス ポリシー

リソースのアクセス ポリシーで、デバイスに対する VPN、Wi-Fi、電子メール、および証明書の設定を構成します。

Intune 機能の詳細については、[リソース アクセス プロファイルの展開](/intune/device-profiles)に関するページを参照してください。

> [!Note]  
> リソース アクセス ワークロードもデバイス構成の一部です。 これらのポリシーは、[デバイス構成](#device-configuration)ワークロードを切り替えると、Intune によって管理されます。

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

Endpoint Protection ワークロードには、マルウェア対策保護機能の Windows Defender スイートが含まれます。

- Windows Defender マルウェア対策
- Windows Defender Application Guard  
- Windows Defender ファイアウォール  
- Windows Defender SmartScreen  
- Windows 暗号化
- Windows Defender Exploit Guard  
- Windows Defender Application Control  
- Windows Defender セキュリティ センター  
- Windows Defender Advanced Threat Protection (現在は Microsoft Defender Threat Protection という名称です)

Intune 機能の詳細については、[Microsoft Intune のエンドポイント保護](/intune/endpoint-protection-windows-10)に関するページを参照してください。

> [!Note]  
> このワークロードを切り替えると、Intune ポリシーによって上書きされるまで、Configuration Manager ポリシーはデバイスに残ります。 この動作により、移行中にデバイスが確実に保護ポリシーを保持することができます。
>
> Endpoint Protection ワークロードもデバイス構成の一部です。 [デバイス構成](#device-configuration)ワークロードを切り替えた場合も同じ動作が適用されます。<!-- SCCMDocs.nl-nl issue #4 --> デバイス構成ワークロードを切り替えると、Endpoint Protection ワークロードには含まれていない Windows Information Protection 機能のポリシーも組み込まれます。<!-- 4184095 -->
>
> Intune デバイス構成のデバイス制限プロファイルの種類の一部である Microsoft Defender ウイルス対策の設定は、Endpoint Protection スライダーの範囲に含まれていません。 Endpoint Protection スライダーを有効にして共同管理デバイスの Microsoft Defender ウイルス対策を管理するには、 **[Microsoft Endpoint Manager 管理センター]**  >  **[エンドポイント セキュリティ]**  >  **[ウイルス対策]** で新しいウイルス対策ポリシーを使用します。 新しいポリシーの種類には、使用可能な新しいオプションと改善されたオプションがあり、デバイス制限プロファイルで使用できるのと同じ設定がすべてサポートされています。 <!--6609171-->
>
> Windows 暗号化機能には、BitLocker 管理が含まれています。 共同管理を使用したこの機能の動作の詳細については、「[BitLocker 管理の展開](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune)」を参照してください。<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>デバイスの構成

<!--1357903-->

デバイス構成ワークロードには、組織内のデバイスを管理する設定が含まれます。 このワークロードを切り替えると、**リソース アクセス** ワークロードと**エンドポイント保護**ワークロードも移動されます。

Intune がデバイス構成機関であっても、Configuration Manager から共同管理デバイスに引き続き設定を展開できます。 この例外は、組織で必要な設定を構成するために使用できるかもしれませんが、Intune ではまだ利用できません。 この例外は、[Configuration Manager の構成基準](../compliance/deploy-use/create-configuration-baselines.md)で指定します。 ベースラインを作成するときに、 **[Always apply this baseline even for co-managed clients]\(共同管理クライアントにもこのベースラインを常に適用する\)** のオプションを有効にします。 これは後で、既存のベースラインのプロパティの **[全般]** タブで変更することができます。  

Intune 機能の詳細については、「[Microsoft Intune でのデバイス プロファイルの作成](/intune/device-profile-create)」を参照してください。  

> [!NOTE]
> デバイス構成ワークロードを切り替えると、Endpoint Protection ワークロードには含まれていない Windows Information Protection 機能のポリシーも組み込まれます。<!-- 4184095 -->

## <a name="office-click-to-run-apps"></a>Office クイック実行アプリ

<!--1357841-->

このワークロードでは、共同管理デバイス上の Microsoft 365 Apps が管理されます。

- ワークロードを移動した後は、デバイスの **Intune ポータル サイト**にアプリが表示されます  

- デバイスが再起動されない場合、Office 更新プログラムがクライアントに表示されるまでに約 24 時間かかる場合があります  

- **Office 365 アプリケーションがデバイス上の Intune で管理されているか**という新しいグローバル条件があります。 この条件は、新しい Microsoft 365 アプリケーションの要件として既定で追加されます。 このワークロードを移行すると、共同管理されたクライアントでアプリケーションの要件が満たされなくなります。 そのため、Configuration Manager で展開される Microsoft 365 がインストールされません。  

Intune 機能の詳細については、「[Microsoft Intune を使用して Windows 10 デバイスに Microsoft 365 アプリを割り当てる](https://docs.microsoft.com/intune/apps-add-office365)」をご覧ください。

## <a name="client-apps"></a>クライアント アプリ

<!--1357892-->

Intune を使用して、共同管理されている Windows 10 デバイス上のクライアント アプリと PowerShell スクリプトを管理します。 このワークロードを移行すると、Intune から展開された使用可能なアプリが、すべてポータル サイトで使用可能になります。 Configuration Manager から展開するアプリは、ソフトウェア センターで使用できます。

Intune 機能の詳細については、「[Microsoft Intune アプリの管理とは](/intune/app-management)」を参照してください。

> [!Tip]  
> この機能はバージョン 1806 で[プレリリース機能](../core/servers/manage/pre-release-features.md)として初めて導入されました。 バージョン 2002 以降、プレリリース機能ではなくなりました。  
>
> この機能は機能の一覧に**共同管理デバイス向けモバイル アプリ**として表示される場合があります。<!-- 5849669 -->

バージョン 1910 以降、Configuration Manager 配布ポイントで Microsoft Connected Cache を有効にすると、Microsoft Intune Win32 アプリを共同管理クライアントに提供できるようになりました。 詳細については、「[Configuration Manager における Microsoft 接続済みキャッシュ](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune)」を参照してください。

## <a name="diagram-for-app-workloads"></a>アプリのワークロードの図

:::image type="content" source="media/co-management-apps.svg" alt-text="共同管理アプリのワークロードの図" lightbox="media/co-management-apps.svg":::

> [!TIP]
> バージョン 2006 以降の Intune ポータル サイトは、Configuration Manager アプリも表示されるように構成できます。 このアプリ ポータル エクスペリエンスを変更すると、上の図で説明した動作が変更されます。 詳細については、「[共同管理デバイスでポータル サイト アプリを使用する](company-portal.md)」を参照してください。<!--CMADO-3601237,INADO-4297660-->

## <a name="known-issues"></a>既知の問題

Endpoint Protection ワークロードを Intune に移行すると、クライアントが Configuration Manager と Microsoft Defender によって設定されたポリシーを引き続き受け入れる可能性があります。 <!--5024559-->

この問題を回避するには、次の手順を使用して、Intune ポリシーがクライアントによって受信された後に ConfigSecurityPolicy.exe を使用して CleanUpPolicy.xml を適用します。

1. 次のテキストをコピーして `CleanUpPolicy.xml` として保存します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```

1. 管理者特権を使用してコマンド プロンプトを開いて `ConfigSecurityPolicy.exe` を実行します。 通常、この実行可能ファイルは、次のいずれかのディレクトリにあります。
   - C:\Program Files\Windows Defender
   - C:\Program Files\Microsoft Security Client

1. コマンド プロンプトで、xml ファイルを渡してポリシーをクリーンアップします。 たとえば、`ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml` となります。  

## <a name="next-steps"></a>次のステップ

[ワークロードを切り替える方法](how-to-switch-workloads.md)
