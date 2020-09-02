---
title: Microsoft Defender Advanced Threat Protection 向けの Intune のセキュリティのベースラインの設定
titleSuffix: Microsoft Intune
description: Microsoft Defender Advanced Threat Protection を管理するために、Intune でサポートされるセキュリティ ベースラインの設定
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: 322e3be8e7421b0c622a8e656a3312791ed7feac
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913445"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Intune 向けの Microsoft Defender Advanced Threat Protection ベースライン設定

Microsoft Intune によってサポートされている Microsoft Defender Advanced Threat Protection ベースライン設定を表示します。 Advanced Threat Protection (ATP) ベースラインの既定値は、ATP の推奨される構成を表しており、他のセキュリティ ベースラインのベースラインの既定値と一致しない場合があります。

::: zone pivot="atp-april-2020"

この記事の詳細は、2020 年 4 月 21 日にリリースされた Microsoft Defender ATP ベースラインのバージョン 4 に適用されます。 以前のバージョンからのこのバージョンのベースラインの変更点を確認するには、このベースラインの *[バージョン]* ウィンドウを表示すると使用可能になる [[ベースラインの比較]](../protect/security-baselines.md#compare-baseline-versions) 操作を使用します。

::: zone-end
::: zone pivot="atp-march-2020"

この記事の詳細は、2020 年 3 月 1 日にリリースされた Microsoft Defender ATP ベースラインのバージョン 3 に適用されます。 以前のバージョンからのこのバージョンのベースラインの変更点を確認するには、このベースラインの *[バージョン]* ウィンドウを表示すると使用可能になる [[ベースラインの比較]](../protect/security-baselines.md#compare-baseline-versions) 操作を使用します。

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


ご使用の環境が [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites) を使用するための前提条件を満たしている場合は、Microsoft Defender Advanced Threat Protection ベースラインを使用できます。

このベースラインは、物理デバイス用に最適化されており、現在は仮想マシン (VM) や VDI エンドポイントでの使用は推奨されていません。 特定のベースライン設定が、仮想化された環境でのリモート対話型セッションに影響を与える可能性があります。 詳細については、Windows ドキュメントの「[Increase compliance to the Microsoft Defender ATP security baseline (Microsoft Defender ATP のセキュリティ ベースラインに対するコンプライアンスの強化)](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline)」をご覧ください。


## <a name="application-guard"></a>Application Guard

詳細については、Windows のドキュメントの「[WindowsDefenderApplicationGuard CSP](/windows/client-management/mdm/windowsdefenderapplicationguard-csp)」を参照してください。  

Microsoft Edge を使用しているとき、ご利用の環境は Windows Defender Application Guard によって、組織で信頼されていないサイトから保護されます。 分離ネットワーク境界のリストに含まれないサイトにユーザーがアクセスすると、そのサイトは Hyper-V 仮想ブラウズ セッションで開きます。 信頼済みサイトは、ネットワーク境界によって定義されます。  

- **Microsoft Edge 向けの Application Guard を有効にする (オプション)**  
  CSP:[Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Edge に対して有効にする** (*既定値*) - Application Guard では未承認のサイトが Hyper-V 仮想ブラウズ コンテナー内で開かれます。
  - **未構成** - サイト (信頼済みおよび信頼されていない) はいずれも仮想化されたコンテナー内ではなくデバイス上で開かれます。  
  
  *[Edge に対して有効にする]* に設定すると、 *[Block external content from non-enterprise approved sites]\(承認された非エンタープライズ サイトからの外部コンテンツをブロックする\)* と *[クリップボードの動作]* を構成できます。

  - **承認された非エンタープライズ サイトからの外部コンテンツをブロックする**  
    CSP:[Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **はい** (*既定値*) - 未承認の Web サイトからのコンテンツの読み込みをブロックします。
    - **[未構成]** - デバイス上で非エンタープライズ サイトを開けるようになります。

  - **[クリップボードの動作]**  
    CSP:[Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    ローカル PC と Application Guard 仮想ブラウザー間で許可するコピー/貼り付け操作を選択します。 次のオプションがあります。
    - **未構成**  
    - **PC とブラウザーの間でのコピー/貼り付けをブロックする** (*既定値*) - 両方ともブロックします。 PC と仮想ブラウザーの間でデータを転送できません。
    - **ブラウザーから PC へのコピー/貼り付けのみを許可する** - PC から仮想ブラウザーにデータを転送できません。
    - **PC からブラウザーへのコピー/貼り付けのみを許可する** - 仮想ブラウザーからホスト PC にデータを転送できません。
    - **PC とブラウザーの間でのコピー/貼り付けを許可する** - コンテンツに対するブロックは存在しません。

- **Windows ネットワーク分離ポリシー**  
  CSP:[ポリシー CSP - NetworkIsolation](/windows/client-management/mdm/policy-csp-networkisolation)

  "*ネットワーク ドメイン*" のリストを指定します。これらは Application Guard がエンタープライズ サイトとして処理するクラウド内でホストされているエンタープライズ リソースです。
  - **構成** (*既定値*)
  - **未構成**

  *[構成]* に設定すると、"*ネットワーク ドメイン*" を定義できるようになります。

  - **ネットワーク ドメイン**  
    **[追加]** を選択し、ドメイン、IP アドレス範囲、およびネットワーク境界を指定します。 既定では *securitycenter.windows.com* が構成されます。

## <a name="bitlocker"></a>BitLocker

詳細については、Windows のドキュメントの「[BitLocker グループ ポリシー設定](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)」を参照してください。

- **ストレージ カードの暗号化が必須 (モバイルのみ)**  
  CSP:[RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  この設定は、Windows Mobile および Mobile Enterprise SKU デバイスにのみ適用されます。
  - **はい** (*既定値*) - モバイル デバイスの場合は、ストレージ カードでの暗号化が必須です。
  - **未構成** - 設定は OS の既定値に戻されます。この場合、ストレージ カードの暗号化は必須ではありません。

  > [!NOTE]
  > [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) と [Windows Phone 8.1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) のサポートは、2020 年 8 月に終了しました。

- **OS および固定データ ドライブのディスク全体の暗号化を有効にする**  
  CSP:[RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  このポリシーが適用される前にドライブが暗号化されている場合、特別にアクションは行われません。 暗号化の方法とオプションがこのポリシーのものと一致する場合、構成からは成功が返されます。 インプレース BitLocker 構成オプションがこのポリシーと一致しない場合、構成からエラーが返される可能性があります。
  
  既に暗号化されているディスクにこのポリシーを適用するには、ドライブの暗号化を解除し、MDM ポリシーを再度適用します。 Windows の既定値では、BitLocker ドライブの暗号化は必要ありませんが、Azure AD Join および Microsoft Account (MSA) では、登録またはログインの自動暗号化が適用され、XTS-AES 128 ビット暗号化で BitLocker が有効にされる可能性があります。

  - **はい** (*既定値*) - BitLocker の使用を強制します。
  - **未構成** - BitLocker は強制されません。

- **BitLocker システム ドライブ ポリシー**  
  [BitLocker グループ ポリシー設定](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **構成** (*既定値*)
  - **未構成**

  *[構成]* に設定すると、 *[Configure encryption method for Operating System drives]\(オペレーティング システム ドライブの暗号化方法の構成\)* を構成できるようになります。

  - **[Configure encryption method for Operating System drives]\(オペレーティング システム ドライブの暗号化方法の構成\)**  
    CSP:[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    この設定は、 *[BitLocker システム ドライブポリシー]* が *[構成]* に設定されている場合に使用できます。  

    システム ドライブの暗号化の方法と暗号強度を構成します。  *XTS - AES 128 ビット* は Windows の既定の暗号化方法であり、推奨される値です。

    - **[未構成]** ("*既定値*")
    - **AES 128 ビット CBC**
    - **AES 256 ビット CBC**
    - **AES 128 ビット XTS**
    - **AES 256 ビット XTS**

- **BitLocker 固定ドライブ ポリシー**  
  [BitLocker グループ ポリシー設定](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **構成** (*既定値*)
  - **未構成**

  *[構成]* に設定すると、 *[Block write access to fixed data-drives not protected by BitLocker]\(BitLocker で保護されていない固定データドライブへの書き込みアクセスをブロックする\)* および *[固定データドライブの暗号化方法の構成]* を構成できるようになります。

  - **[Block write access to fixed data-drives not protected by BitLocker]\(BitLocker で保護されていない固定データドライブへの書き込みアクセスをブロックする\)**  
    CSP:[FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    この設定は、 *[BitLocker 固定ドライブ ポリシー]* が *[構成]* に設定されている場合に使用できます。

    - **未構成** (*既定値*) - 暗号化されていない固定ドライブにデータを書き込むことができます。
    - **はい** - Windows では、BitLocker で保護されていない固定ドライブにデータを書き込むことはできません。 固定ドライブが暗号化されていない場合、書き込みアクセス権が付与される前に、ユーザーはドライブに対して BitLocker セットアップ ウィザードを完了する必要があります。

  - **固定データドライブの暗号化方法の構成**  
    CSP:[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    この設定は、 *[BitLocker 固定ドライブ ポリシー]* が *[構成]* に設定されている場合に使用できます。

    固定データドライブ ディスクの暗号化の方法と暗号強度を構成します。 *XTS - AES 128 ビット* は Windows の既定の暗号化方法であり、推奨される値です。

    - **[未構成]** ("*既定値*")
    - **AES 128 ビット CBC**
    - **AES 256 ビット CBC**
    - **AES 128 ビット XTS**
    - **AES 256 ビット XTS**

- **BitLocker removable drive policy (Bitlocker のリムーバブル ドライブのポリシー)**  
  [BitLocker グループ ポリシー設定](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **構成** (*既定値*)
  - **未構成**

  *[構成]* に設定すると、 *[Configure encryption method for removable data-drives]\(リムーバブル データドライブの暗号化方法の構成\)* および *[Block write access to removable data-drives not protected by BitLocker]\(BitLocker で保護されていないリムーバブル データドライブへの書き込みアクセスをブロックする\)* を構成できるようになります。

  - **[Configure encryption method for removable data-drives]\(リムーバブル データドライブの暗号化方法の構成\)**  
    CSP:[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    この設定は、 *[BitLocker リムーバブル ドライブ ポリシー]* が *[構成]* に設定されている場合に使用できます。

    リムーバブル データドライブ ディスクの暗号化方法と暗号強度を構成します。 *XTS - AES 128 ビット* は Windows の既定の暗号化方法であり、推奨される値です。

    - **未構成**
    - **AES 128 ビット CBC**
    - **AES 256 ビット CBC** (*既定値*)
    - **AES 128 ビット XTS**
    - **AES 256 ビット XTS**

  - **[Block write access to removable data-drives not protected by BitLocker]\(BitLocker で保護されていないリムーバブル データドライブへの書き込みアクセスをブロックする\)**  
    CSP:[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    この設定は、 *[BitLocker リムーバブル ドライブ ポリシー]* が *[構成]* に設定されている場合に使用できます。

    - **未構成** (*既定値*) - 暗号化されていないリムーバブル ドライブにデータを書き込むことができます。  
    - **はい** - Windows では、BitLocker で保護されていないリムーバブル ドライブにデータを書き込むことはできません。 リムーバブル ドライブが暗号化されていない場合、書き込みアクセス権が付与される前に、ユーザーはドライブに対して BitLocker セットアップ ウィザードを完了する必要があります。

## <a name="browser"></a>ブラウザー

- **Require SmartScreen for Microsoft Edge (Microsoft Edge で SmartScreen が必要)**  
  CSP:[Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **はい** (*既定値*) - SmartScreen を使用してフィッシング詐欺にあう可能性や悪意のあるソフトウェアからユーザーを保護しています。
  - **未構成**

- **Block malicious site access (悪意のあるサイトへのアクセスをブロックする)**  
  CSP:[Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **はい** (*既定値*) - ユーザーが Microsoft Defender SmartScreen フィルターの警告を無視できないようにして、サイトへの移動をブロックします。
  - **未構成**

- **Block unverified file download (確認されていないファイルのダウンロードをブロックする)**  
  CSP:[Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **はい** (*既定値*) - ユーザーが Microsoft Defender SmartScreen フィルターの警告を無視できないようにして、確認されていないファイルをダウンロードできないようにします。
  - **未構成**

## <a name="data-protection"></a>データ保護

- **Block direct memory access (ダイレクト メモリ アクセスをブロックする)**  
  CSP:[DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  このポリシー設定は、BitLocker またはデバイスの暗号化が有効な場合にのみ適用されます。

  - **はい** (*既定値*) - ユーザーが Windows にログインするまで、ホット プラグ可能なすべての PCI ダウンストリーム ポートへの直接メモリ アクセス (DMA) が禁止されます。 ユーザーがログインすると、ホスト プラグ PCI ポートに接続されている PCI デバイスが Windows によって列挙されます。 ユーザーがコンピューターをロックするたびに、ユーザーが再ログインするまで、子デバイスが接続されていないホット プラグ PCI ポートで DMA がブロックされます。 コンピューターのロックが解除された際に既に列挙されていたデバイスは、取り外されるまで機能を維持します。
  - **未構成**

## <a name="device-guard"></a>[Device Guard]  

- **Credential Guard を有効にする**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard では、Windows ハイパーバイザーを使用して保護が実現されます。これには、セキュア ブートと DMA 保護が機能する必要があり、そのためにはハードウェア要件が満たされている必要があります。

  - **未構成** - Credential Guard の使用を無効にします。Windows ではこれが既定値です。
  - **UEFI ロックで有効にする** (*既定値*) - Credential Guard を有効にし、それをリモートで無効にできないようにします。UEFI で永続化された構成は手動でクリアする必要があるためです。
  - **UEFI ロックなしで有効にする** - Credential Guard を有効にし、コンピューターへの物理的なアクセスなしにオフにすることを許可します。

## <a name="device-installation"></a>デバイスのインストール

- **Hardware device installation by device identifiers (デバイス識別子を使用してハードウェア デバイスをインストールする)**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  このポリシー設定を使用すると、Windows によるインストールが禁止されているデバイスのプラグ アンド プレイ ハードウェア ID と互換 ID の一覧を指定できます。 このポリシー設定は、Windows がデバイスをインストールできるようにするその他のポリシー設定よりも優先されます。  リモート デスクトップ サーバーでこのポリシー設定を有効にした場合、ポリシー設定は、リモート デスクトップ クライアントからリモート デスクトップ サーバーへの指定されたデバイスのリダイレクトに影響します。

  - **未構成**
  - **ハードウェア デバイスのインストールを許可する** - 他のポリシー設定によって許可または禁止されているとおりに、デバイスをインストールおよび更新することができます。
  - **ハードウェア デバイスのインストールをブロックする** (*既定値*) - ご自分で定義したリスト内に表示されたハードウェア ID または互換性 ID を持つデバイスを Windows でインストールすることはできません。

  *[ハードウェア デバイスのインストールをブロックする]* に設定すると、 *[一致するハードウェア デバイスを削除する]* および *[ブロックされているハードウェア デバイス ID]* を構成できるようになります。

  - **Remove matching hardware devices (一致するハードウェア デバイスを削除する)**

    この設定は *[Hardware device installation by device identifiers]\(デバイス識別子でハードウェア デバイスをインストールする\)* が *[Block hardware device installation]\(ハードウェア デバイスのインストールをブロックする\)* に設定されているときのみ使用できます。
    - **あり**
    - **未構成**

  - **Hardware device identifiers that are blocked (ブロックされているハードウェア デバイス識別子)**  
    
    この設定は *[Hardware device installation by device identifiers]\(デバイス識別子でハードウェア デバイスをインストールする\)* が *[Block hardware device installation]\(ハードウェア デバイスのインストールをブロックする\)* に設定されているときのみ使用できます。

    **[追加]** を選択して、ブロックするハードウェア デバイスの識別子を指定します。

- **Hardware device installation by setup classes (セットアップ クラスを使用してハードウェア デバイスをインストールする)**  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  このポリシー設定を使用すると、Windows によるインストールが禁止されているデバイス ドライバーのデバイス セットアップ クラス GUID (グローバル一意識別子) の一覧を指定できます。 このポリシー設定は、Windows がデバイスをインストールできるようにするその他のポリシー設定よりも優先されます。 リモート デスクトップ サーバーでこのポリシー設定を有効にした場合、ポリシー設定は、リモート デスクトップ クライアントからリモート デスクトップ サーバーへの指定されたデバイスのリダイレクトに影響します。

  - **未構成**
  - **ハードウェア デバイスのインストールを許可する** - Windows では他のポリシー設定によって許可または禁止されているとおりに、デバイスをインストールおよび更新することができます。
  - **ハードウェア デバイスのインストールをブロックする** (*既定値*) - ご自分で定義したリスト内に表示されたセットアップ クラス GUID を持つデバイスを Windows でインストールすることはできません。

  *[ハードウェア デバイスのインストールをブロックする]* に設定すると、 *[一致するハードウェア デバイスを削除する]* および *[ブロックされているハードウェア デバイス ID]* を構成できるようになります。

  - **Remove matching hardware devices (一致するハードウェア デバイスを削除する)**

    この設定は *[Hardware device installation by device identifiers]\(デバイス識別子でハードウェア デバイスをインストールする\)* が *[Block hardware device installation]\(ハードウェア デバイスのインストールをブロックする\)* に設定されているときのみ使用できます。
    - **あり**
    - **未構成**

  - **Hardware device identifiers that are blocked (ブロックされているハードウェア デバイス識別子)**

    この設定は *[Hardware device installation by device identifiers]\(デバイス識別子でハードウェア デバイスをインストールする\)* が *[Block hardware device installation]\(ハードウェア デバイスのインストールをブロックする\)* に設定されているときのみ使用できます。

    **[追加]** を選択して、ブロックするハードウェア デバイスの識別子を指定します。

## <a name="dma-guard"></a>DMA ガード

- **Kernel DMA Protection と互換性のない外部デバイスの列挙**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  このポリシーでは、外部 DMA 対応デバイスに対して追加のセキュリティを提供することができます。 これにより、DMA の再マッピング/デバイス メモリの分離およびサンドボックス化と互換性のない外部 DMA 対応デバイスの列挙をより詳細に制御できます。
  
  このポリシーが有効になるのは、Kernel DMA Protection がシステム ファームウェアによってサポートされていて、それによって有効にされた場合のみです。 カーネル DMA 保護は、製造時にシステムによってサポートされる必要があるプラットフォーム機能です。 システムで Kernel DMA Protection がサポートされているかどうかを確認するには、MSINFO32.exe の概要ページにある Kernel DMA Protection フィールドを調べます。

  - **未構成** - (*既定値*)
  - **すべてブロックする**
  - **すべて許可**

## <a name="endpoint-detection-and-response"></a>エンドポイントの検出と応答

次の設定の詳細については、Windows ドキュメント内の「[WindowsAdvancedThreatProtection CSP](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)」を参照してください。

- **すべてのファイルのサンプル共有**:  
  CSP: [Configuration/SampleSharing](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Microsoft Defender Advanced Threat Protection サンプル共有の構成パラメーターを返すか設定します。  
  
  - **はい** (*既定値*):
  - **未構成**

- **テレメトリの報告頻度を早める**:  
  CSP: [Configuration/TelemetryReportingFrequency](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Microsoft Defender Advanced Threat Protection テレメトリの報告頻度を早めます。  

  - **はい** (*既定値*):
  - **未構成**

## <a name="firewall"></a>ファイアウォール

詳細については、Windows のドキュメントの「[Firewall CSP](/windows/client-management/mdm/firewall-csp)」 (ファイアウォール CSP) を参照してください。

- **ステートフル ファイル転送プロトコル (FTP) を無効にする**  
  CSP:[MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **はい** (*既定値*):
  - **未構成** - ファイアウォールでは FTP を使用して、セカンダリ ネットワーク接続が検査およびフィルター処理されます。これにより、ご利用のファイアウォール規則は無視される可能性があります。

- **セキュリティ アソシエーションが削除されるまでのアイドル状態の秒数**  
CSP:[MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  ネットワーク トラフィックが表示されなくなった後に、セキュリティ アソシエーションを保持する期間を指定します。 構成しない場合、*300* 秒 (既定値) のアイドル期間を経て、セキュリティアソシエーションはシステムによって削除されます。
  
  数値は、**300** から **3600** 秒とする必要があります。

- **事前共有キーのエンコード**  
  CSP:[MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   UTF-8 を必要としない場合、事前共有キーが最初に UTF-8 を使用してエンコードされます。 その後、デバイス ユーザーは別のエンコード方法を選択できます。

  - **未構成**
  - **なし**
  - **UTF8** (*既定値*)

- **証明書失効リスト (CRL) の検証**  
  CSP:[MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  証明書失効リスト (CRL) の検証をどのように適用するかを指定します。  

  - **未構成** (*既定値*) - CRL 検証は無効にされます。
  - **なし**
  - **試行回数**
  - **必要**

- **[パケット キュー]**  
  CSP:[MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  IPsec トンネル ゲートウェイのシナリオで、暗号化された受信とクリア テキストの転送について受信側のソフトウェアのスケーリングを有効にする方法を指定します。 この設定により、パケットの順序が確実に保持されます。

  - **未構成** (*既定値*) - パケット キューはクライアントの既定値に戻され、無効になります。
  - **[無効]**
  - **インバウンドをキューに入れる**
  - **アウトバウンドをキューに入れる**
  - **両方をキューに入れる**

- **ファイアウォール プロファイル プライベート**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **構成** (*既定値*)
  - **未構成**

  *[構成]* に設定すると、次の追加設定を構成できます。

  - **受信接続をブロック**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **はい** (*既定値*):
    - **未構成**

  - **マルチキャスト ブロードキャストへのユニキャスト応答が必要**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **はい** (*既定値*):
    - **未構成**

  - **ステルス モードが必要**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **はい** (*既定値*):
    - **未構成**

  - **送信接続が必要**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **はい** (*既定値*):
    - **未構成**

  - **着信通知をブロック**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **はい** (*既定値*):
    - **未構成**

  - **グループ ポリシーからのグローバル ポート ルールをマージ**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **はい** (*既定値*):
    - **未構成**

  - **ステルス モードをブロック**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **はい** (*既定値*):
    - **未構成**

  - **ファイアウォールの有効化**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **未構成**
    - **［ブロック済み］**
    - **許可** (*既定値*)

  - **グループ ポリシーからの承認されたアプリケーション ルールをマージしない**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **はい** (*既定値*):
    - **未構成**

  - **グループ ポリシーからの接続セキュリティ ルールをマージしない**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **はい** (*既定値*):
    - **未構成**

  - **着信トラフィックが必要**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **はい** (*既定値*):
    - **未構成**

  - **グループ ポリシーからのポリシー ルールをマージしない**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **はい** (*既定値*):
    - **未構成**

- **ファイアウォール プロファイル パブリック**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **構成** (*既定値*)
  - **未構成**

  *[構成]* に設定すると、次の追加設定を構成できます。

  - **受信接続をブロック**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **はい** (*既定値*):
    - **未構成**

  - **マルチキャスト ブロードキャストへのユニキャスト応答が必要**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **はい** (*既定値*):
    - **未構成**

  - **ステルス モードが必要**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **はい** (*既定値*):
    - **未構成**

  - **送信接続が必要**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **はい** (*既定値*):
    - **未構成**

  - **グループ ポリシーからの承認されたアプリケーション ルールをマージしない**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **はい** (*既定値*):
    - **未構成**

  - **着信通知をブロック**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **はい** (*既定値*):
    - **未構成**

  - **グループ ポリシーからのグローバル ポート ルールをマージ**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **はい** (*既定値*):
    - **未構成**

  - **ステルス モードをブロック**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **はい** (*既定値*):
    - **未構成**

  - **ファイアウォールの有効化**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **未構成**
    - **［ブロック済み］**
    - **許可** (*既定値*)

  - **グループ ポリシーからの接続セキュリティ ルールをマージしない**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **はい** (*既定値*):
    - **未構成**

  - **着信トラフィックが必要**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **はい** (*既定値*):
    - **未構成**

  - **グループ ポリシーからのポリシー ルールをマージしない**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **はい** (*既定値*):
    - **未構成**

- **ファイアウォール プロファイル ドメイン**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **マルチキャスト ブロードキャストへのユニキャスト応答が必要**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **グループ ポリシーからの承認されたアプリケーション ルールをマージしない**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **はい** (*既定値*):
    - **未構成**  

  - **着信通知をブロック**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **はい** (*既定値*):
    - **未構成**

  - **グループ ポリシーからのグローバル ポート ルールをマージ**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **はい** (*既定値*):
    - **未構成**

  - **ステルス モードをブロック**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **はい** (*既定値*):
    - **未構成**

  - **ファイアウォールの有効化**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **未構成**
    - **［ブロック済み］**
    - **許可** (*既定値*)

  - **グループ ポリシーからの接続セキュリティ ルールをマージしない**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **はい** (*既定値*):
    - **未構成**

  - **グループ ポリシーからのポリシー ルールをマージしない**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **はい** (*既定値*):
    - **未構成**

## <a name="microsoft-defender"></a>Microsoft Defender

- **Run daily quick scan at (毎日スキャンを実行する時刻)**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   毎日のクイック スキャンを実行する時刻を構成します。 既定では、スキャンの実行は **[午前 2:00]** に設定されます。

- **スケジュールされたスキャンの開始時間**  
  
  既定では、これは **[午前 2:00]** に設定されます。

- **スケジュールされたスキャン用に低い CPU 優先度を構成**  
  CSP: [Defender/EnableLowCPUPriority](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**はい** (*既定値*)
  - **未構成**

- **Office 通信アプリによる子プロセスの作成をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874499)  

  この ASR 規則は、次の GUID を使用して制御されます。26190899-1602-49e8-8b27-eb1d0a1ce869。
  - **未構成** - Windows の既定値が復元され、子プロセスの作成がブロックされることはありません。
  - **ユーザー定義**
  - **有効** (*既定値*) - Office 通信アプリケーションによる子プロセスの作成がブロックされます。
  - **監査モード** - 子プロセスをブロックするのでなく、Windows イベントが発生します。

- **Adobe Reader による子プロセスの作成をブロックする**  
  [攻撃の回避規則を使用した攻撃の回避](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **未構成** - Windows の既定値が復元され、子プロセスの作成がブロックされることはありません。
  - **ユーザー定義**
  - **有効** (*既定値*) - Adobe Reader による子プロセスの作成がブロックされます。
  - **監査モード** - 子プロセスをブロックするのでなく、Windows イベントが発生します。

- **受信メール メッセージをスキャンする**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **はい** (*既定値*) - メールのメールボックスとメール ファイル (PST、DBX、MNX、MIME、BINHEX など) がスキャンされます。
  - **未構成** - 設定はクライアントの既定値に戻され、メール ファイルはスキャンされません。

- **リアルタイム保護を有効にする**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **はい** (*既定値*) - リアルタイム監視が適用されます。ユーザーはこれを無効にすることはできません。
  - **未構成** - 設定はクライアントの既定値 (有効) に戻されますが、ユーザーはこれを変更できます。 リアルタイム監視を無効にするには、カスタム URI を使用します。

- **Number of days (0-90) to keep quarantined malware (検査されたマルウェアを保持する日数 (0-90))**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  項目が削除されるまでの [検疫] フォルダーでの保管日数を構成します。 既定値はゼロ (**0**) です。この場合、検疫されたファイルは削除されません。

- **Defender システム スキャンのスケジュール**  
  CSP:[Defender/ScheduleScanDay](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Defender がデバイスをスキャンする曜日をスケジュールします。 既定では、スキャンは **[ユーザー定義]** になっています。その設定は *[毎日]* にすることも、曜日にすることも、 *[スケジュールされたスキャンはありません]* とすることもできます。

- **クラウド保護のタイムアウトを延長する追加の時間 (0 から 50 秒)**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender ウイルス対策を使用すると、疑わしいファイルが 10 秒間自動的にブロックされ、クラウド内のファイルがスキャンされ、安全であることを確認されます。 この設定では、このタイムアウトに最大 50 秒を追加できます。  既定では、タイムアウトはゼロ (**0**) に設定されます。

- **フル スキャン中に、マップされたネットワーク ドライブをスキャンする**  
  CSP:[Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **はい** (*既定値*) - フルスキャン時に、マップされたネットワーク ドライブが含められます。
  - **未構成** - クライアントはその既定値に戻されます。これにより、マップされたネットワーク ドライブに対するスキャンは無効にされます。

- **Turn on network protection (ネットワーク保護を有効にする)**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **はい** (*既定値*) - Network Inspection System (NIS) で署名によって検出された悪意のあるトラフィックをブロックします。
  - **未構成**

- **すべてのダウンロード ファイルと添付ファイルをスキャンする**  
  CSP:[Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **はい** (*既定値*) - ダウンロードされたファイルと添付ファイルがすべてスキャンされます。 設定はクライアントの既定値 (有効) に戻されますが、ユーザーはこれを変更できます。 この設定を無効にするには、カスタム URI を使用します。
  - **未構成** - 設定はクライアントの既定値 (有効) に戻されますが、ユーザーはこれを変更できます。 この設定を無効にするには、カスタム URI を使用します。

::: zone-end
::: zone pivot="atp-april-2020"

- **アクセス保護をブロックする**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **あり**
  - **[未構成]** ("*既定値*")

::: zone-end
::: zone pivot="atp-march-2020"

- **アクセス保護をブロックする**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **はい** (*既定値*):
  - **未構成**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **ブラウザー スクリプトをスキャンする**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **はい** (*既定値*) - Microsoft Defender のスクリプト スキャン機能が適用され、ユーザーはこれを無効にすることはできません。
  - **未構成** - この設定は、クライアントの既定値 (スクリプト スキャンを有効にする) に戻されます。ただし、ユーザーはこれを無効にすることができます。

- **Microsoft Defender アプリへのユーザー アクセスをブロックする**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **はい** (*既定値*) - Microsoft Defender ユーザー インターフェイス (UI) にアクセスできず、通知は抑制されます。
  - **未構成** [はい] に設定すると、Windows Defender ユーザー インターフェイス (UI) にアクセスできなくなり、通知は抑制されます。 [未構成] に設定すると、設定はクライアントの既定値に戻され、通知は許可されます。

- **スキャンあたりの最大許容 CPU 使用率 (0 から 100%)**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  スキャンに対する CPU の最大使用量をパーセントで指定します。 既定値は **50** です。

- **スキャンの種類**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **ユーザー定義**
  - **[無効]**
  - **クイック スキャン** (*既定値*)
  - **フル スキャン**

- **Enter how often (0-24 hours) to check for security intelligence updates (セキュリティ インテリジェンスの更新を確認する頻度 (0-24 時間) の入力)**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  署名の更新を確認する頻度を時間単位で指定します。 たとえば、値を 1 とすると 1 時間ごとに確認されます。 値が 2 の場合、2 時間ごとに確認されます。

  値が定義されていない場合、デバイスでは、クライアントの既定値である **8** 時間が使用されます。

- **Defender サンプル送信の同意**  
  CSP: [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Microsoft Defender でデータを送信するためのユーザーの同意レベルを確認します。 必要な同意が既に与えられている場合、Microsoft Defender からそれらが送信されます。 それ以外の場合 (かつユーザーが "確認しない" を指定した場合)、( *[クラウドによる保護]* が *[はい]* に設定されている場合は) データを送信する前にユーザーの同意を求める UI が起動します。

  - **安全なサンプルを自動的に送信する** (*既定値*)
  - **[常に確認する]**
  - **送信しない**
  - **すべてのサンプルを自動的に送信する**

- **Cloud-delivered protection level (クラウドによる保護レベル)**  
  CSP:[CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  疑わしいファイルのブロック時とスキャン時に適用する Defender ウイルス対策の度合いを構成します。
  - **未構成** (*既定値*) - 既定の Defender のブロック レベル。
  - **高** - クライアントのパフォーマンスを最適化しながら未知のものを積極的にブロックします。この場合、誤検知の可能性が高くなります。
  - **高+** - 不明なファイルを積極的にブロックし、追加の保護策を適用します。これはクライアントのパフォーマンスに影響を及ぼす可能性があります。
  - **ゼロ トレランス** - 不明な実行可能ファイルをすべてブロックします。

- **アーカイブ ファイルをスキャンする**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **はい** (*既定値*) - ZIP ファイルや CAB ファイルなどのアーカイブ ファイルのスキャンが適用されます。
  - **未構成** - 設定はクライアントの既定値 (アーカイブされたファイルをスキャン) に戻されますが、ユーザーはスキャンを無効にすることができます。

- **動作の監視を有効にする**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **はい** (*既定値*) - 動作の監視が適用され、ユーザーはこれを無効にすることはできません。
  - **未構成** - 設定はクライアントの既定値 (有効) に戻されますが、ユーザーはこれを変更できます。 リアルタイム監視を無効にするには、カスタム URI を使用します。
  
- **フル スキャン中にリムーバブル ドライブをスキャンする**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **はい** (*既定値*) - フル スキャン中に、リムーバブル ドライブ (USB フラッシュ ドライブなど) がスキャンされます。
  - **未構成** - 設定は、クライアントの既定値 (リムーバブル ドライブをスキャン) に戻されますが、ユーザーはこのスキャンを無効にすることができます。
  
- **ネットワーク ファイルをスキャンする**  
  CSP:[Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **はい** (*既定値*) - Microsoft Defender によってネットワーク ファイルがスキャンされます。
  - **未構成** - クライアントはその既定値に戻されます。これにより、ネットワーク ファイルのスキャンが無効にされます。
  
- **Defender potentially unwanted app action (Defender の望ましくないアプリに対するアクション)**  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  望ましくない可能性のあるアプリケーション (PUA) の検出レベルを指定します。 望ましくない可能性のあるソフトウェアをダウンロードするか、デバイスにインストールしようとすると、Defender からユーザーに警告されます。
  - **デバイスの既定**
  - **ブロック** (*既定値*) - 検出された項目はブロックされ、履歴に他の脅威と共に表示されます。
  - **監査** - Defender で、望ましくない可能性のあるアプリケーションが検出されますが、対策は何も行われません。 イベント ビューアーで Defender によって作成されたイベントを検索することで、Defender でアプリケーションに対して実行されたアクションに関する情報を確認できます。

- **Turn on cloud-delivered protection (クラウドによる保護を有効にする)**  
  CSP:[AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  既定では、Windows 10 デスクトップ デバイス上の Defender から、検出された問題に関する情報が Microsoft に送信されます。 Microsoft ではその情報を分析し、お客様や他のユーザーに影響する問題の詳細を把握して、改善されたソリューションを提供しています。

  - **はい** (*既定値*) - クラウドで提供される保護が有効になります。  デバイス ユーザーはこの設定を変更できません。
  - **未構成** - 設定はシステムの既定値に復元されます

- **Office アプリケーションによる他のプロセスへのコード挿入をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872974)

  この ASR 規則は、次の GUID を使用して制御されます。75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ブロック** (*既定値*) - Office アプリケーションは、その他のプロセスへのコードの挿入をブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **Office アプリケーションによる実行可能なコンテンツの作成をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872975)

  この ASR 規則は、次の GUID を使用して制御されます。3B576869-A4EC-4529-8536-B80A7769E899
  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ブロック** (*既定値*) - Office アプリケーションは実行可能なコンテンツの作成をブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。
  
- **JavaScript または VBScript による、ダウンロードされた実行可能なコンテンツの起動をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872979)

   この ASR 規則は、次の GUID を使用して制御されます。D3E037E1-3EB8-44C8-A917-57927947596D
  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ブロック** (*既定値*) - Defender は、インターネットからダウンロードされた JavaScript または VBScript ファイルの実行をブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。
  
- **ネットワーク保護を有効にする**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **未構成** - 設定は Windows の既定値に戻され、無効になります。
  - **ユーザー定義**
  - **有効** - システム上のすべてのユーザーを対象にネットワーク保護が有効にされます。
  - **監査モード** (*既定値*) - 危険なドメインからユーザーがブロックされるのでなく、Windows イベントが発生します。

- **USB から実行された信頼されていない署名なしのプロセスをブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874502)

  この ASR 規則は、次の GUID を使用して制御されます: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ブロック** (*既定値*) - USB ドライブから実行される信頼されていないプロセスおよび無署名プロセスがブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **Windows ローカル セキュリティ機関サブシステム (lsass.exe) からの資格情報の盗難をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=874499)

  この ASR 規則は、次の GUID を使用して制御されます。9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ユーザー定義**
  - **有効** (*既定値*) - lsass.exe を介して資格情報を盗もうとする試みがブロックされます。
  - **監査モード** - 危険なドメインからユーザーはブロックされず、代わりに Windows イベントが発生します。

- **電子メールおよび Web メールのクライアントからの実行可能なコンテンツをブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872980)

  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ブロック** (*既定値*) - 電子メールおよび Web メールのクライアントからダウンロードした実行可能なコンテンツはブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **すべての Office アプリケーションによる子プロセスの作成をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872976)

  この ASR 規則は、次の GUID を使用して制御されます。D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ブロック** (*既定値*)
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **難読化されている可能性のあるスクリプト (js/vbs/ps) の実行をブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872978)

  この ASR 規則は、次の GUID を使用して制御されます。5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ブロック** (*既定値*) - 難読化されたスクリプトの実行が Defender によってブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

- **Office マクロからの Win32 API 呼び出しをブロックする**  
  [悪用からデバイスを保護する](https://go.microsoft.com/fwlink/?linkid=872977)

  この ASR 規則は、次の GUID を使用して制御されます。92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **未構成** - 設定は Windows の既定値 (無効) に戻されます。
  - **ブロック** (*既定値*) - Office マクロは Win32 API 呼び出しの使用をブロックされます。
  - **監査モード** - ブロックするのでなく Windows イベントが発生します。

## <a name="microsoft-defender-security-center"></a>Microsoft Defender セキュリティ センター

- **ユーザーが Exploit Guard 保護インターフェイスを編集することをブロックする**  
  CSP:[WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **はい** (*既定値*) - Microsoft Defender Security Center 内の悪用に対する保護設定の領域に対してユーザーは変更を加えることができなくなります。
  - **未構成** - ローカル ユーザーは悪用に対する保護設定の領域に対して変更を加えることができます。

## <a name="smart-screen"></a>スマート スクリーン

- **ユーザーが SmartScreen 警告を無視できないようにする**  
  CSP:[SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   この設定では、[Windows SmartScreen の有効化] 設定を [はい] にする必要があります。
  - **[はい]** ("*既定*") - SmartScreen は有効になっており、ファイルや悪意のあるアプリに関する警告をユーザーは無視できません。
  - **[未構成]** - ユーザーはファイルや悪意のあるアプリに関する SmartScreen の警告を無視できます。

- **ストアからのアプリのみを要求する**  

  - **はい** (*既定値*):
  - **未構成**

- **Windows SmartScreen を有効にする**  
  CSP:[SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **はい** (*既定値*) - SmartScreen の使用をすべてのユーザーに強制します。
  - **未構成** - 設定を Windows の既定値に戻します。これにより、SmartScreen は有効にされますが、ユーザーはこの設定を変更できます。 SmartScreen を無効にするには、カスタム URI を使用します。

## <a name="windows-hello-for-business"></a>Windows Hello for Business

詳細については、Windows のドキュメントの「[PassportForWork CSP](/windows/client-management/mdm/passportforwork-csp)」を参照してください。

- **Windows Hello for Business をブロックする**  

   Windows Hello for Business は、パスワード、スマート カード、および仮想スマート カードを置き換えることで Windows にサインインする代替方法です。

  - **未構成** - デバイスによって Windows Hello for Business がデバイス プロビジョニングされます。これは Windows の既定値です。
  - **無効** (*既定値*) - デバイスによって Windows Hello for Business がプロビジョニングされます。
  - **有効** - デバイスでは、どのユーザーに対しても Windows Hello for Business がプロビジョニングされません。

  *[無効]* に設定すると、次の設定を構成できます。

  - **[PIN での小文字の使用]**  
    - **許可しない**
    - **必須**
    - **許可** (*既定値*)

  - **[PIN での特殊文字の使用]**
    - **許可しない**
    - **必須**
    - **許可** (*既定値*)

  - **[PIN での大文字の使用]**
    - **許可しない**
    - **必須**
    - **許可** (*既定値*)

::: zone-end

## <a name="next-steps"></a>次のステップ

- [セキュリティ ベースラインに関する詳細](security-baselines.md)
- [競合を回避する](security-baselines.md#avoid-conflicts)
- [Intune でのポリシーとプロファイルのトラブルシューティング](../configuration/troubleshoot-policies-in-microsoft-intune.md)