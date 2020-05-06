---
title: Microsoft Intune での Windows 10 デバイス向けの保護設定 - Azure | Microsoft Docs
description: Windows 10 デバイスで、エンドポイント保護設定を使用または構成して、Microsoft Defender の機能を有効にします。これには、Application Guard、ファイアウォール、SmartScreen、暗号化と BitLocker、Exploit Guard、Application Control、Security Center、Microsoft Intune のローカル デバイスのセキュリティが含まれます。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/23/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3af7c91b-8292-4c7e-8d25-8834fcf3517a
ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: fedca34aaf390dfec655e3166f3a153af93a7ce0
ms.sourcegitcommit: 7b3eed763b394075766ea080968889a8538bfe56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82506592"
---
# <a name="windows-10-and-later-settings-to-protect-devices-using-intune"></a>Intune を使用してデバイスを保護するための Windows 10 (以降) の設定

Microsoft Intune には、デバイスの保護に役立つ多くの設定が含まれています。 この記事では、Windows 10 以降のデバイスで有効にして構成できるすべての設定について説明します。 これらの設定は、BitLocker や Windows Defender を含む、セキュリティを制御するための Intune のエンドポイント保護構成プロファイルで作成されます。  

Microsoft Defender ウイルス対策を構成するには、[Windows 10 のデバイス制限](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)に関するページを参照してください。  

## <a name="before-you-begin"></a>始める前に  

[エンドポイント保護デバイス構成プロファイルを作成](endpoint-protection-configure.md)します。  

構成サービス プロバイダー (CSP) の詳細については、「[構成サービス プロバイダーのリファレンス](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference)」を参照してください。  

## <a name="microsoft-defender-application-guard"></a>Microsoft Defender Application Guard  

Microsoft Edge を使用しているとき、ご利用の環境は Windows Defender Application Guard によって、組織で信頼されていないサイトから保護されます。 分離ネットワーク境界のリストに含まれないサイトにユーザーがアクセスすると、そのサイトは Hyper-V 仮想ブラウズ セッションで開きます。 信頼済みサイトはネットワーク境界によって定義され、デバイス構成で構成されます。  

Application Guard は Windows 10 (64 ビット) デバイスでのみ使用可能です。 このプロファイルを使用すると、Application Guard をアクティブ化するための Win32 コンポーネントがインストールされます。  

- **[Application Guard]**  
  **既定値**:未構成  
   Application Guard CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)  

  - **[Edge に対して有効にする]** - この機能をオンにすると、信頼されていないサイトが Hyper-V 仮想ブラウズ コンテナーで開かれます。  
  - **[未構成]** - デバイス上で任意のサイト (信頼されたおよび信頼されていない) を開くことができます。  

- **[クリップボードの動作]**  
  **既定値**:未構成  
   Application Guard CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)  

  ローカル PC と Application Guard 仮想ブラウザー間で許可するコピー/貼り付け操作を選択します。  
  - **未構成**  
  - **[PC からブラウザーへのコピー/貼り付けのみを許可する]**  
  - **[ブラウザーから PC へのコピー/貼り付けのみを許可する]**  
  - **[PC とブラウザーの間でのコピー/貼り付けを許可する]**  
  - **[PC とブラウザーの間でのコピー/貼り付けをブロックする]**  

- **[クリップボードの内容]**  
  この設定は、 *[クリップボードの動作]* が "*許可*" 設定の中のいずれかに設定されている場合にのみ使用できます。  
  **既定値**:未構成  
  Application Guard CSP: [Settings/ClipboardFileType](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardfiletype)  

  許可されているクリップボードの内容を選択します。  
  - **未構成**  
  - **Text**  
  - **[イメージ]**  
  - **[テキストとイメージ]**  

- **[エンタープライズ サイトの外部コンテンツ]**  
  **既定値**:未構成  
  Application Guard CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)  

  - **[ブロック]** - 未承認の Web サイトからのコンテンツの読み込みをブロックします。  
  - **[未構成]** - デバイス上で非エンタープライズ サイトを開けるようになります。  
 
- **[仮想ブラウザーから印刷]**  
  **既定値**:未構成  
  Application Guard CSP: [Settings/PrintingSettings](https://go.microsoft.com/fwlink/?linkid=872354)  

  - **[許可]** - 仮想ブラウザーから選択されたコンテンツの印刷を許可します。  
  - **[未構成]** すべての印刷機能を無効にします。  

  印刷を "*許可*" した場合は、次の設定を構成できます。
  - **[印刷の種類]** 次のオプションの 1 つまたは複数を選択します。  
    - PDF  
    - XPS  
    - ローカル プリンター
    - ネットワーク プリンター  

- **[ログの収集]**  
  **既定値**:未構成  
  Application Guard CSP: [Audit/AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)  

  - **[許可]** - Application Guard ブラウズ セッション内で発生するイベントのログが収集されます。  
  - **[未構成]** - ブラウズ セッション内でログは収集されません。  

- **[ユーザーが生成したブラウザー データを保持する]**  
  **既定値**:未構成  
  Application Guard CSP: [Settings/AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)  

  - **[許可]** - Application Guard 仮想ブラウズ セッション中に作成されるユーザー データ (パスワード、お気に入り、Cookie など) が保存されます。  
  - **[未構成]** - デバイスを再起動するか、ユーザーがサインアウトすると、ユーザーがダウンロードしたファイルやデータが破棄されます。  

- **[グラフィック アクセラレータ]**  
 **既定値**:未構成  
  Application Guard CSP: [Settings/AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)  
      
  - **[有効]** - 仮想グラフィックス処理ユニットにアクセスできるようにすることで、グラフィックを大量に利用する Web サイトや動画の読み込みが速くなります。  
  - **[未構成]** グラフィックスにデバイスの CPU を使用します。仮想グラフィックス処理ユニットは使用しません。  

- **[ホスト ファイル システムにファイルをダウンロードする]**  
  **既定値**:未構成  
  Application Guard CSP: [Settings/SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)  

  - **[有効]** - ユーザーは仮想ブラウザーからホスト オペレーティング システムにファイルをダウンロードできます。  
  - **[未構成]** - デバイスにローカルでファイルが保存されます。ホスト ファイル システムにはダウンロードされません。  

## <a name="microsoft-defender-firewall"></a>Microsoft Defender ファイアウォール  
 
### <a name="global-settings"></a>グローバル設定  

これらの設定はすべてのネットワークの種類に適用されます。  

- **[ファイル転送プロトコル]**  
  **既定値**:未構成  
   Firewall CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **[ブロック]** - ステートフル FTP が無効になります。  
  - **[未構成]** - ファイアウォールでステートフル FTP フィルタリングを行い、セカンダリ接続を許可します。  

- **[セキュリティ アソシエーションが削除されるまでのアイドル時間]**  
  **既定値**:*未構成*  
   Firewall CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)  

   セキュリティ アソシエーションが削除されるまでのアイドル時間を秒単位で指定します。   

- **[事前共有キーのエンコード]**  
  **既定値**:未構成  
   Firewall CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)  

   - **[有効]** - UTF-8 を使用して事前共有キーをエンコードします。  
   - **[未構成]** - ローカル ストア値を使用して事前共有キーをエンコードします。  

- **[IPsec の除外]**  
  **既定値**:*選択済み 0*  
   Firewall CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

   IPsec から除外するトラフィックの種類を次の中から 1 つまたは複数選択します。  
   - **[近隣ノードは IPv6 ICMP の種類コードを検出する]**  
   - **[ICMP]**  
   - **[ルーターは IPv6 ICMP の種類コードを検出する]**  
   - **[Both IPv4 and IPv6 DHCP network traffic]\(IPv4 と IPv6 DHCP の両方のネットワーク トラフィック\)**  

- **証明書失効リストの検証**  
  **既定値**:未構成  
  Firewall CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)  

  デバイスで証明書失効リストを確認する方法を選択します。 次のオプションがあります。  
  - **[CRL の検証を無効にする]**  
  - **[証明書が失効した場合にのみ CRL の検証を失敗する]**  
  - **[何かのエラーが発生したら CRL の検証を失敗する]**  
 

- **[状況に応じてキー モジュールごとに認証セットを一致させる]**  
  **既定値**:未構成  
  Firewall CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)  
  
  - **[有効]** - キー モジュールでは、サポートされていない認証スイートのみが無視されます。  
  - **[未構成]** - 認証セットに指定されているすべての認証スイートをサポートしていない場合、キー モジュールは認証セット全体を無視します。  


- **[パケット キュー]**  
  **既定値**:未構成  
  Firewall CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)  

  IPsec トンネル ゲートウェイのシナリオで暗号化された受信とクリア テキストの転送について、受信側のソフトウェア スケーリングを有効にする方法を指定します。 この設定により、パケットの順序が確実に保持されます。 次のオプションがあります。  
  - **未構成**  
  - **[すべてのパケットのキューを無効にする]**  
  - **[暗号化された受信パケットのみをキューに入れる]**  
  - **[転送の場合にのみ、暗号化の解除を実行した後のパケットをキューに入れる]**  
  - **[受信パケットと送信パケットの両方を構成する]**  

### <a name="network-settings"></a>ネットワークの設定  

この記事では次の設定はそれぞれ 1 回だけしか示されていませんが、これらはすべて、次の 3 種類のネットワークに適用されます。  
- **ドメイン (社内) ネットワーク**  
- **プライベート (検出可能な) ネットワーク**  
- **パブリック (検出不可能な) ネットワーク**  

#### <a name="general-settings"></a>全般設定  

- **Microsoft Defender ファイアウォール**  
  **既定値**:未構成  
  Firewall CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)  
  
  - **[有効]** - ファイアウォールと高度なセキュリティが有効になります。 
  - **[未構成]** - 他のポリシー設定に関係なく、すべてのネットワーク トラフィックが許可されます。  

- **ステルス モード**  
  **既定値**:未構成  
  Firewall CSP: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)  
  - **未構成**  
  - **[ブロック]** - ファイアウォールがステルス モードで動作しないようにブロックされます。 ステルス モードをブロックすることで、 **[IPsec secured packet exemption]\(IPsec 保護パケットの除外\)** もブロックできます。  
  - **[許可]** - ファイアウォールはステルス モードで動作します。これはプローブ要求に対する応答を阻止するのに役立ちます。  

- **[IPsec でセキュリティ保護されたパケットのステルス モードでの適用除外]**  
  **既定値**:未構成  
  Firewall CSP: [DisableStealthModeIpsecSecuredPacketExemption](https://go.microsoft.com/fwlink/?linkid=872560)  

  *[ステルス モード]* が *[ブロック]* に設定されている場合、このオプションは無視されます。  

  - **未構成**  
  - **[ブロック]** - IPSec でセキュリティ保護されたパケットでは、除外対象を受け取りません。  
  - **[許可]** - 除外を有効にします。 ファイアウォールのステルス モードは、IPsec によってセキュリティ保護されている要請していないネットワーク トラフィックにホスト コンピューターが応答することを阻止してはなりません。  

- **[シールド]**  
  **既定値**:未構成  
  Firewall CSP: [[シールド]](https://go.microsoft.com/fwlink/?linkid=872561)  
    - **未構成**  
    - **[ブロック]** - Microsoft Defender ファイアウォールがオンになっていて、この設定が *[ブロック]* に設定されている場合、他のポリシー設定に関係なく、すべての着信トラフィックがブロックされます。 
    - **[許可]** - *[許可]* に設定すると、この設定はオフにされます。着信トラフィックは他のポリシー設定に基づいて許可されます。

- **[マルチキャスト ブロードキャストへのユニキャスト応答]**  
  **既定値**:未構成  
  Firewall CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)  
  
  通常、マルチキャスト メッセージまたはブロードキャスト メッセージへのユニキャスト応答を受信する必要はありません。 これらの応答は、サービス拒否 (DOS) 攻撃、または既知のライブ コンピューターをプローブしようとしている攻撃者を示す可能性があります。  
  - **未構成**  
  - **[ブロック]** - マルチキャスト ブロードキャストへのユニキャスト応答を無効にします。  
  - **[許可]** - マルチキャスト ブロードキャストへのユニキャスト応答を許可します。  

- **[受信の通知]**  
  **既定値**:未構成  
  Firewall CSP: [DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=8725630)  

  - **未構成**  
  - **[ブロック]** - アプリがポート上でのリッスンをブロックされたときに使用する通知を非表示にします。  
  - **[未構成]** - この設定が有効になります。アプリがポートでのリッスンをブロックされたとき、ユーザーに通知が表示される場合があります。  

- **[送信接続の既定のアクション]**  
  **既定値**:未構成  
  Firewall CSP: [DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)  
  
  送信接続に対してファイアウォールが実行する既定のアクションを構成します。 この設定は、Windows バージョン 1809 以降に適用されます。  

  - **未構成**  
  - **[ブロック]** - 既定のファイアウォール アクションは、ブロックしないように明示的に指定されていない限り、送信トラフィックに対して実行されません。  
  - **[許可]** - 送信接続に対して既定のファイアウォール アクションが実行されます。  

- **[受信接続の既定のアクション]**  
  **既定値**:未構成  
  Firewall CSP: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)  
 
  - **未構成**  
  - **[ブロック]** - 受信接続に対して既定のファイアウォール アクションが実行されません。  
  - **[許可]** - 受信接続に対して既定のファイアウォール アクションが実行されます。  

#### <a name="rule-merging"></a>規則のマージ  

- **[ローカル ストアからの Microsoft Defender ファイアウォール規則の承認された適用]**  
  **既定値**:未構成  
  Firewall CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)  

  - **未構成**  
  - **[未構成]** - ローカル ストアにある承認済みのアプリケーション ファイアウォール規則が無視され、適用されません。  
  - **[許可]** -
    **[有効]** を選択すると、ローカル ストアにあるファイアウォール規則が認識され、適用されます。  

- **[ローカル ストアからのグローバル ポート Microsoft Defender ファイアウォール規則]**  
  **既定値**:未構成  
  Firewall CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)  

  - **未構成**  
  - **[ブロック]** - ローカル ストア内のグローバル ポート ファイアウォール規則は無視され、適用されません。  
  - **[許可]** - ローカル ストアのグローバル ポート ファイアウォール規則の適用が認識され、適用されます。  

- **[ローカル ストアからの Microsoft Defender ファイアウォール規則]**  
  **既定値**:未構成  
  Firewall CSP: [AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)  

  - **未構成**  
  - **[ブロック]** - ローカル ストアからのファイアウォール規則は無視され、適用されません。
  - **[有効]** - ローカル ストアのファイアウォール規則の適用が認識され、適用されます。  

- **[ローカル ストアからの IPsec 規則]**  
  **既定値**:未構成  
  Firewall CSP: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)  

  - **未構成**  
  - **[ブロック]** - スキーマと接続セキュリティ規則のバージョンに関係なく、ローカル ストアの接続セキュリティ規則は無視され、適用されません。  
  - **[有効]** - スキーマや接続セキュリティ規則のバージョンに関係なく、ローカル ストアからの接続セキュリティ規則が適用されます。  

### <a name="firewall-rules"></a>ファイアウォール規則  

1 つまたは複数のカスタム ファイアウォール規則を**追加**することができます。 詳細については、「[Windows 10 デバイスのカスタム ファイアウォール規則を追加する](endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices)」を参照してください。  

カスタム ファイアウォール規則では、次のオプションがサポートされています。  

#### <a name="general-settings"></a>[全般設定]:  

- **名前**  
  **既定値**: *[名前なし]*  

  使用する規則にフレンドリ名を指定します。 規則の一覧にはこの名前が表示されるので、識別しやすくなります。  

- **説明**  
  **既定値**: *[説明なし]*  

  規則の説明を入力します。  

- **[方向]**    
  **既定値**:未構成  
  Firewall CSP: [FirewallRules/*FirewallRuleName*/Direction](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#direction)  
  
  この規則を**受信**または**送信**トラフィックに適用するかどうかを指定します。 **[未構成]** として設定すると、送信トラフィックに規則が自動的に適用されます。  

- **操作**  
  **既定値**:未構成  
  Firewall CSP: [FirewallRules/*FirewallRuleName*/Action](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#action)、および [FirewallRules/*FirewallRuleName*/Action/Type](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#type)  

  **[許可]** または **[ブロック]** から選択します。 **[未構成]** として設定した場合、既定では規則によってトラフィックが許可されます。  

- **[ネットワークの種類]**  
  **既定値**:0 件選択済み  
  Firewall CSP: [FirewallRules/*FirewallRuleName*/Profiles](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#profiles)  

  この規則が属するネットワークの種類を最大 3 種類まで選択します。 オプションには、 **[ドメイン]** 、 **[プライベート]** 、 **[パブリック]** があります。  ネットワークの種類を選択しなかった場合、3 種類のネットワークすべてに規則が適用されます。  

#### <a name="application-settings"></a>アプリケーションの設定  

- **アプリケーション**  
  **既定値**:すべて  

  アプリまたはプログラム用の接続を制御します。 次のいずれかのオプションを選択してから、追加の構成を完了します。  
  - **[パッケージ ファミリ名]** – パッケージ ファミリ名を指定します。 パッケージ ファミリ名を検索するには、PowerShell コマンド **Get-AppxPackage** を使用します。   
    Firewall CSP: [FirewallRules/*FirewallRuleName*/App/PackageFamilyName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#packagefamilyname)  
 
  - **[ファイル パス]** – クライアント デバイス上のアプリへのファイル パス (絶対パスまたは相対パス) を指定する必要があります。 次に例を示します。C:\Windows\System\Notepad.exe or %WINDIR%\Notepad.exe.  
    Firewall CSP: [FirewallRules/*FirewallRuleName*/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)  

  - **[Windows サービス]** – トラフィックを送信または受信するアプリケーションではなくサービスである場合に、Windows サービスの短い名前を指定します。 サービスの短い名前を検索するには、PowerShell コマンド **Get-Service** を使用します。  
    Firewall CSP: [FirewallRules/*FirewallRuleName*/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)  

  - **[すべて]** – *追加の構成はありません*。  

#### <a name="ip-address-settings"></a>IP アドレスの設定  

この規則を適用するローカル アドレスとリモート アドレスを指定します。  

- **[ローカル アドレス]**     
  **既定値**: [任意のアドレス]  
  Firewall CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  

  **[任意のアドレス]** または **[指定されたアドレス]** を選択します。  

  *[指定されたアドレス]* を使用する場合は、1 つまたは複数のアドレスを、規則の対象となるローカル アドレスのコンマ区切りリストとして追加します。 有効なトークンは次のとおりです。  
  - *任意*のローカル アドレスには、アスタリスク "*" を使用します。 アスタリスクを使用する場合は、それを、使用する唯一のトークンとする必要があります。  
  - サブネットを指定するには、サブネット マスクまたはネットワーク プレフィックス表記のいずれかを使用します。 サブネット マスクとネットワーク プレフィックスのどちらも指定しない場合、サブネット マスクの既定値は 255.255.255.255 となります。  
  - 有効な IPv6 アドレス。  
  - IPv4 アドレス範囲。"開始アドレス - 終了アドレス" の形式とし、スペースは含めません。  
  - IPv6 アドレス範囲。"開始アドレス - 終了アドレス" の形式とし、スペースは含めません。  

- **[リモート アドレス]**  
  **既定値**: [任意のアドレス]  
  Firewall CSP: [FirewallRules/*FirewallRuleName*/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  
 
  **[任意のアドレス]** または **[指定されたアドレス]** を選択します。  

  *[指定されたアドレス]* を使用する場合は、規則の対象となるリモート アドレスのコンマ区切りリストとして 1 つまたは複数のアドレスを追加します。 トークンは大文字と小文字が区別されません。 有効なトークンは次のとおりです。  
  - *任意*のリモート アドレスには、アスタリスク "*" を使用します。 アスタリスクを使用する場合は、それを、使用する唯一のトークンとする必要があります。  
  - "Defaultgateway"  
  - "DHCP"  
  - "DNS"  
  - "WINS"  
  - "Intranet" (Windows バージョン 1809 以降でサポート)  
  - "RmtIntranet" (Windows バージョン 1809 以降でサポート)  
  - "Internet" (Windows バージョン 1809 以降でサポート)  
  - "Ply2Renders" (Windows バージョン 1809 以降でサポート)  
  - "LocalSubnet" は、ローカル サブネット上の任意のローカル アドレスを示します。  
  - サブネットを指定するには、サブネット マスクまたはネットワーク プレフィックス表記のいずれかを使用します。 サブネット マスクとネットワーク プレフィックスのどちらも指定しない場合、サブネット マスクの既定値は 255.255.255.255 となります。  
  - 有効な IPv6 アドレス。  
  - IPv4 アドレス範囲。"開始アドレス - 終了アドレス" の形式とし、スペースは含めません。  
  - IPv6 アドレス範囲。"開始アドレス - 終了アドレス" の形式とし、スペースは含めません。  

#### <a name="port-and-protocol-settings"></a>ポートとプロトコルの設定  
この規則を適用するローカル ポートとリモート ポートを指定します  

- **プロトコル**  
  **既定値**:任意  
  Firewall CSP: [FirewallRules/*FirewallRuleName*/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)  
  次の中から選択し、必要な構成を完了します。  
  - **[すべて]** – 追加の構成はありません。  
  - **TCP** – ローカルおよびリモートのポートを構成します。 両方のオプションで、すべてのポートまたは指定されたポートがサポートされます。 コンマ区切りのリストを使用して、指定されたポートを入力します。  
    - **ローカル ポート** -    ファイアウォール CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **リモート ポート** -   Firewall CSP: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **[UDP]** – ローカルおよびリモートのポートを構成します。 両方のオプションで、すべてのポートまたは指定されたポートがサポートされます。 コンマ区切りのリストを使用して、指定されたポートを入力します。  
    - **ローカル ポート** -    ファイアウォール CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **リモート ポート** -   Firewall CSP: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **[カスタム]** – 0 から 255 までのカスタム **プロトコル**番号を指定します。  

#### <a name="advanced-configuration"></a>詳細構成  
- **[インターフェイスの種類]**  
  **既定値**:0 件選択済み  
  Firewall CSP: [FirewallRules/*FirewallRuleName*/InterfaceTypes](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#interfacetypes)  

  次のオプションから選択します。  
  - **[リモート アクセス]**  
  - **[ワイヤレス]**  
  - **[ローカル エリア ネットワーク]**  

- **[以下のユーザーのみに接続を許可する]**  
  **既定値**:すべてのユーザー *(リストが指定されていない場合、既定ではすべての使用となります)*  
  Firewall CSP: [FirewallRules/*FirewallRuleName*/LocalUserAuthorizationList](https://aka.ms/intunefirewallauthorizedusers)  

  この規則に対して承認されたローカル ユーザーのリストを指定します。 この規則が Windows サービスに適用される場合、承認されたユーザーのリストを指定することはできません。  


## <a name="microsoft-defender-smartscreen-settings"></a>Windows Defender SmartScreen 設定  
 
デバイスに Microsoft Edge をインストールする必要があります。  

- **[アプリとファイルの SmartScreen]**  
  **既定値**:未構成  
   SmartScreen CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)  

  - **[未構成]** - SmartScreen の使用を無効にします。  
  - **[有効]** - ファイルやアプリの実行のために Windows SmartScreen を有効にします。 SmartScreen はクラウドをベースとする、フィッシング/マルウェア対策のためのコンポーネントです。  

- **[確認されていないファイルの実行]**  
  **既定値**:未構成  
   SmartScreen CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **[未構成]** - この機能は無効になります。エンド ユーザーは未検証のファイルを実行できます。  
  - **[ブロック]** - Windows SmartScreen で検証されていないファイルをエンド ユーザーが実行することをブロックします。  

## <a name="windows-encryption"></a>Windows 暗号化  
 
### <a name="windows-settings"></a>Windows の設定  

- **デバイスの暗号化**  
  **既定値**:未構成  
  BitLocker CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)  

  - **[必要]** - デバイスの暗号化を有効にするようにユーザーに求めます。 Windows のエディションとシステム構成によっては、次のことがユーザーに求められる場合があります。  
    - 別のプロバイダーの暗号化が有効になっていないことを確認する。  
    - BitLocker ドライブ暗号化をオフにし、再び BitLocker をオンにする。  
  - **未構成**  
  
  別の暗号化方式がアクティブになっている場合に Windows の暗号化を有効にすると、デバイスが不安定になる可能性があります。  

- **[メモリ カードの暗号化 (モバイルのみ)]**  
  "*この設定は、Windows 10 モバイルにのみ適用されます。* "  
  **既定値**:未構成  
  BitLocker CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)  

  - デバイスで使用するリムーバブル メモリ カードの暗号化を**要求**します。  
  - **[未構成]** - メモリ カードの暗号化は要求されません。暗号化をオンにするようにユーザーに求めることはありません。  

### <a name="bitlocker-base-settings"></a>BitLocker の基本設定  

基本設定は、すべての種類のデータ ドライブに対するユニバーサル BitLocker の設定です。 これらの設定では、エンド ユーザーがすべての種類のデータ ドライブで変更できるドライブ暗号化タスクまたは構成オプションを管理します。  

- **[他のディスクの暗号化に対する警告]**  
  **既定値**:未構成  
  BitLocker CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)  

  - **[ブロック]** - 別のディスク暗号化サービスがデバイスに存在する場合の警告プロンプトが無効になります。  
  - **[未構成]** - 他のディスク暗号化に関する警告を表示することができます。  

  > [!TIP]  
  > Azure AD 参加済みであると共に Windows 1809 以降を実行しているデバイスに BitLocker を自動的かつサイレントにインストールするには、この設定を *[ブロック]* に設定する必要があります。 詳細については、「[デバイスで BitLocker をサイレント モードで有効にする](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices)」を参照してください。

  *[ブロック]* に設定した場合は、次の設定を構成できます。  

  - **[Azure AD 参加中の暗号化の有効化を標準ユーザーに許可する]**  
    *この設定は、Azure Active Directory 参加済み (Azure ADJ) のデバイスにのみ適用され、前の設定 [`Warning for other disk encryption`] に依存します。*  
    **既定値**:未構成  
    BitLocker CSP: [AllowStandardUserEncryption](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp#allowstandarduserencryption)

     - **[許可]** - 標準ユーザー (管理者以外) はサインイン時に BitLocker 暗号化を有効にすることができます。  
     - **[未構成]** - デバイス上で BitLocker 暗号化を有効にすることを管理者にのみ許可します。  

  > [!TIP]  
  > Azure AD 参加済みであると共に Windows 1809 以降を実行しているデバイスに BitLocker を自動的かつサイレントにインストールするには、この設定を *[許可]* に設定する必要があります。 詳細については、「[デバイスで BitLocker をサイレント モードで有効にする](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices)」を参照してください。

- **[暗号化方法の構成]**  
  **既定値**:未構成  
  BitLocker CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **[有効]** - オペレーティング システム、データ、リムーバブル ドライブ用の暗号化アルゴリズムを構成します。  
  - **[未構成]** - BitLocker は XTS-AES 128 ビットを既定の暗号化手法として使用するか、他の設定スクリプトによって指定される暗号化手法を使用します。  

  " *[有効]* " に設定すると、次の設定を構成できます。  

  - **[オペレーティング システム ドライブの暗号化]**  
    **既定値**:XTS-AES 128 ビット  
   
    オペレーティング システム ドライブ用の暗号化の方法を選択します。 XTS-AES アルゴリズムの使用をお勧めします。  
    - **AES-CBC 128 ビット**  
    - **AES-CBC 256 ビット**  
    - **XTS-AES 128 ビット**  
    - **XTS-AES 256 ビット**  

  - **[固定データ ドライブの暗号化]**  
    **既定値**:AES-CBC 128 ビット  
   
    固定 (組み込み) のデータ ドライブ用の暗号化の方法を選択します。 XTS-AES アルゴリズムの使用をお勧めします。  
    - **AES-CBC 128 ビット**  
    - **AES-CBC 256 ビット**  
    - **XTS-AES 128 ビット**  
    - **XTS-AES 256 ビット**  

  - **[リムーバブル データドライブの暗号化]**  
    **既定値**:AES-CBC 128 ビット  

    リムーバブル データ ドライブ用の暗号化の方法を選択します。 Windows 10 を実行していないデバイスでリムーバブル ドライブを使用する場合は、AES-CBC アルゴリズムの使用をお勧めします。  
    - **AES-CBC 128 ビット**  
    - **AES-CBC 256 ビット**  
    - **XTS-AES 128 ビット**  
    - **XTS-AES 256 ビット**  

### <a name="bitlocker-os-drive-settings"></a>BitLocker OS ドライブ設定  

これらの設定はオペレーティング システムのデータ ドライブにのみ適用されます。  

- **[起動時の追加認証]**  
  **既定値**:未構成  
  BitLocker CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)  

  - **[必要]** - トラステッド プラットフォーム モジュール (TPM) の使用を含む、コンピューター スタートアップの認証要件を構成します。  
  - **[未構成]** - TPM を使用するデバイス上で基本オプションのみを構成します。  

  " *[必要]* " に設定すると、次の設定を構成できます。  

  - **互換性のない TPM チップでの BitLocker**  
    **既定値**:未構成  

    - **[ブロック]** - 互換性のある TPM チップがデバイスにないときに BitLocker の使用を無効にします。  
    - **[未構成]** - 互換性のある TPM チップなしでも BitLocker を使用できます。 BitLocker には、パスワードまたはスタートアップ キーが必要になることがあります。  

  - **[互換性のある TPM スタートアップ]**  
    **既定値**: [TPM を許可する]  

    TPM を許可するか、要求するか、または許可しないかを構成します。  

    - **[TPM を許可する]**  
    - **[TPM を許可しない]**  
    - **[TPM を要求する]**  

  - **[互換性のある TPM スタートアップ PIN]**  
    **既定値**: [TPM でスタートアップ PIN を許可する]  

    TPM チップ搭載のスタートアップ PIN の使用を許可するか、許可しないか、または必須とするかを選びます。 スタートアップ PIN を有効にするには、エンド ユーザーによる操作が必要です。  

    - **[TPM でスタートアップ PIN を許可する]**  
    - **[TPM でスタートアップ PIN を許可しない]**  
    - **[TPM でスタートアップ PIN を要求する]**

    > [!TIP]
    > Azure AD 参加済みであると共に Windows 1809 以降を実行しているデバイスに BitLocker を自動的かつサイレントにインストールするには、この設定を *[TPM でスタートアップ PIN を要求する]* に設定することはできません。 詳細については、「[デバイスで BitLocker をサイレント モードで有効にする](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices)」を参照してください。

  - **[互換性のある TPM スタートアップ キー]**  
    **既定値**: [TPM でスタートアップ キーを許可する]  

    TPM チップ搭載のスタートアップ キーの使用を許可するか、許可しないか、または必須とするかを選びます。 スタートアップ キーを有効にするには、エンド ユーザーによる操作が必要です。  

    - **[TPM でスタートアップ キーを許可する]**  
    - **[TPM でスタートアップ キーを許可しない]**  
    - **[TPM でスタートアップ キーを要求する]**  

    > [!TIP]
    > Azure AD 参加済みであると共に Windows 1809 以降を実行しているデバイスに BitLocker を自動的かつサイレントにインストールするには、この設定を *[TPM でスタートアップ キーを要求する]* に設定することはできません。 詳細については、「[デバイスで BitLocker をサイレント モードで有効にする](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices)」を参照してください。

  - **[互換性のある TPM スタートアップ キーと PIN]**  
    **既定値**: [TPM でスタートアップ キーと PIN を許可する]  

    TPM チップ搭載のスタートアップ キーおよび PIN の使用を許可するか、許可しないか、または必須とするかを選びます。 スタートアップ キーとスタートアップ PIN を有効にするには、エンド ユーザーによる操作が必要です。  
    - **[TPM でスタートアップ キーと PIN を許可する]**  
    - **[TPM でスタートアップ キーと PIN を許可しない]**  
    - **[TPM でスタートアップ キーと PIN を要求する]**   

    > [!TIP]  
    > Azure AD 参加済みであると共に Windows 1809 以降を実行しているデバイスに BitLocker を自動的かつサイレントにインストールするには、この設定を *[TPM でスタートアップ キーと PIN を要求する]* に設定することはできません。 詳細については、「[デバイスで BitLocker をサイレント モードで有効にする](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices)」を参照してください。

- **[PIN の長さの最小値]**  
    **既定値**:未構成  
    BitLocker CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)   

    - **[有効]** TPM スタートアップ PIN の最小長を構成します。  
    - **[未構成]** - ユーザーは長さが 6 から 20 桁のスタートアップ PIN を構成できます。  

  " *[有効]* " に設定すると、次の設定を構成できます。  

  - **[最小文字数]**  
    **既定値**: *[未構成]* BitLocker CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)  

    スタートアップ PIN に必要な文字数を、**4**-**20** の範囲で入力します。  

- **[OS ドライブの回復]**  
  **既定値**:未構成   
  BitLocker CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)  

  - **[有効]** - 必要なスタートアップ情報が利用できない場合に BitLocker で保護されたオペレーティング システム ドライブを回復させる方法を制御します。  
  - **[未構成]** - BitLocker の回復については既定の回復オプションがサポートされます。 既定では、DRA が許可され、回復パスワードと回復キーを含む回復オプションがユーザーによって選択されます。回復情報は AD DS にバックアップされません。  

  " *[有効]* " に設定すると、次の設定を構成できます。  

  - **[証明書ベースのデータ回復エージェント]**  
    **既定値**:未構成  
     
    - **[ブロック]** - データ回復エージェントと、BitLocker で保護されている OS ドライブとの併用を阻止します。  
    - **[未構成]** - BitLocker で保護されているオペレーティング システム ドライブでデータ回復エージェントを使用できるようにします。  

  - **[ユーザーによる回復パスワードの作成]**  
    **既定値**: [48 桁の回復パスワードを許可する]  

    48 桁の回復パスワードの生成をユーザーに許可するか、必須にするか、許可しないかを選びます。  
    - **[48 桁の回復パスワードを許可する]**  
    - **[48 桁の回復パスワードを許可しない]**  
    - **[48 桁の回復パスワードを要求する]**  

  - **[ユーザーによる回復キーの作成]**  
    **既定値**: [256 ビットの回復キーを許可する]  

    256 ビットの回復キーの生成をユーザーに許可するか、必須にするか、許可しないかを選びます。  
    - **[256 ビットの回復キーを許可する]**  
    - **[256 ビットの回復キーを許可しない]**  
    - **[256 ビットの回復キーを要求する]**  

  - **[BitLocker セットアップ ウィザードの回復オプション]**  
    **既定値**:未構成  

    - **[ブロック]** - ユーザーには回復オプションが表示されず、変更できません。 に設定すると 
    - **[未構成]** - BitLocker をオンにしたとき、ユーザーに回復オプションが表示され、変更できます。 
 
  - **[BitLocker 回復情報を Azure Active Directory に保存]**  
    **既定値**:未構成  

    - **[有効]** - Azure Active Directory (Azure AD) に BitLocker 回復情報が保存されます。  
    - **[未構成]** - BitLocker 回復情報は AAD に格納されません。  

  - **[Azure Active Directory に保存する BitLocker 回復情報]**  
    **既定値**: [回復パスワードとキー パッケージをバックアップする]  

    BitLocker 回復情報のどの部分を Azure AD に保存するかを構成します。 次の中から選択します。  
    - **回復パスワードとキー パッケージをバックアップする**  
    - **回復パスワードのみバックアップする**  

  - **クライアント主導の回復パスワードの交換**  
    **既定値**: [Azure AD 参加済みデバイスに対して有効にされたキー交換]  
    BitLocker CSP: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    この設定では、OS ドライブの回復後 (bootmgr または WinRE のいずれかを使用) に、クライアント主導の回復パスワードのローテーションが開始されます。  

    - 未構成  
    - キーの回転が無効  
    - Azure AD 参加済みデバイスに対して有効にされたキー交換  
    - Azure AD とハイブリッド参加済みデバイスに対して有効にされたキー交換  

  - **[BitLocker を有効にする前に Azure Active Directory で回復情報を保存]**  
    **既定値**:未構成  
 
     コンピューターから Azure Active Directory に BitLocker 回復情報が正常にバックアップされない場合に、ユーザーが BitLocker を有効にできないようにします。  

    - **[要求]** - BitLocker 回復情報が Azure AD に正常に保存されていない限り、ユーザーが BitLocker をオンにできないようにします。  
    - **[未構成]** - 回復情報が Azure AD に正常に保存されていない場合でも、ユーザーは BitLocker をオンにできます。  

- **[プリブート回復メッセージと URL]**  
  **既定値**:未構成  
  BitLocker CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)  

  - **[有効]** - プリブート キー回復画面に表示されるメッセージと URL を構成します。  
  - **[未構成]** - この機能が無効になります。  
  
  " *[有効]* " に設定すると、次の設定を構成できます。  
  - **[プリブート回復メッセージ]**  
    **既定値**: [既定の回復メッセージと URL を使用する]   
 
    プリブート回復メッセージをユーザーに表示する方法を構成します。 次の中から選択します。  
    - **既定の回復メッセージと URL を使用する**  
    - **空の回復メッセージと URL を使用する**  
    - **カスタム回復メッセージを使用する**  
    - **カスタム回復 URL を使用する**  

### <a name="bitlocker-fixed-data-drive-settings"></a>BitLocker 固定データ ドライブの設定  

これらの設定は、固定データ ドライブに特に適用されます。  

- **[BitLocker によって保護されていない固定データ ドライブへの書き込みアクセス]**  
  **既定値**:未構成  
  BitLocker CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  

  - **[ブロック]** - BitLocker で保護されていないデータ ドライブへの読み取り専用アクセスを与えます。  
  - **[未構成]** - 既定では、暗号化されていないデータ ドライブに対する読み取りおよび書き込みアクセスが可能です。  

- **[固定ドライブの回復]**  
  **既定値**:未構成  
  BitLocker CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)  

  - **[有効]** - 必要なスタートアップ情報が利用できないときに BitLocker で保護されている固定ドライブを回復させる方法を制御します。  
  - **[未構成]** - この機能が無効になります。  

  " *[有効]* " に設定すると、次の設定を構成できます。  

  - **[データ回復エージェント]**  
    **既定値**:未構成  
 
    - **[ブロック]** - BitLocker で保護されている固定ドライブのポリシー エディターでデータ回復エージェントを使用できないようにします。 
    - **[未構成]** - BitLocker で保護されている固定ドライブでデータ回復エージェントを使用できます。  

  - **[ユーザーによる回復パスワードの作成]**  
    **既定値**: [48 桁の回復パスワードを許可する]  

    48 桁の回復パスワードの生成をユーザーに許可するか、必須にするか、許可しないかを選びます。  
    - **[48 桁の回復パスワードを許可する]**  
    - **[48 桁の回復パスワードを許可しない]**  
    - **[48 桁の回復パスワードを要求する]**  

  - **[ユーザーによる回復キーの作成]**  
    **既定値**: [256 ビットの回復キーを許可する]

    256 ビットの回復キーの生成をユーザーに許可するか、必須にするか、許可しないかを選びます。
    - **[256 ビットの回復キーを許可する]**  
    - **[256 ビットの回復キーを許可しない]**  
    - **[256 ビットの回復キーを要求する]**  

  - **[BitLocker セットアップ ウィザードの回復オプション]**  
    **既定値**:未構成  

    - **[ブロック]** - ユーザーには回復オプションが表示されず、変更できません。 に設定すると 
    - **[未構成]** - BitLocker をオンにしたとき、ユーザーに回復オプションが表示され、変更できます。
 
  - **[BitLocker 回復情報を Azure Active Directory に保存]**  
    **既定値**:未構成  

    - **[有効]** - Azure Active Directory (Azure AD) に BitLocker 回復情報が保存されます。  
    - **[未構成]** - BitLocker 回復情報は AAD に格納されません。

  - **[Azure Active Directory に保存する BitLocker 回復情報]**  
    **既定値**: [回復パスワードとキー パッケージをバックアップする]  

    BitLocker 回復情報のどの部分を Azure AD に保存するかを構成します。 次の中から選択します。  
    - **回復パスワードとキー パッケージをバックアップする**  
    - **回復パスワードのみバックアップする**  

  - **[BitLocker を有効にする前に Azure Active Directory で回復情報を保存]**  
    **既定値**:未構成  
 
    コンピューターから Azure Active Directory に BitLocker 回復情報が正常にバックアップされない場合に、ユーザーが BitLocker を有効にできないようにします。  

    - **[要求]** - BitLocker 回復情報が Azure AD に正常に保存されていない限り、ユーザーが BitLocker をオンにできないようにします。  
    - **[未構成]** - 回復情報が Azure AD に正常に保存されていない場合でも、ユーザーは BitLocker をオンにできます。  

### <a name="bitlocker-removable-data-drive-settings"></a>BitLocker リムーバブル データ ドライブの設定  

これらの設定は、リムーバブル データ ドライブに特に適用されます。  

- **[BitLocker によって保護されていないリムーバブル データ ドライブへの書き込みアクセス]**  
  **既定値**:未構成  
  BitLocker CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  

  - **[ブロック]** - BitLocker で保護されていないデータ ドライブへの読み取り専用アクセスを与えます。  
  - **[未構成]** - 既定では、暗号化されていないデータ ドライブに対する読み取りおよび書き込みアクセスが可能です。  

  " *[有効]* " に設定すると、次の設定を構成できます。  

  - **[別の組織で構成されたデバイスへの書き込みアクセス]**  
    **既定値**:未構成  

    - **[ブロック]** - 別の組織で構成されたデバイスへの書き込みアクセスをブロックします。  
    - **[未構成]** - 書き込みアクセスを拒否します。  
 
## <a name="microsoft-defender-exploit-guard"></a>Microsoft Defender Exploit Guard  

[悪用に対する保護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/exploit-protection)を使用して、従業員が使用するアプリに対する攻撃を管理し、回避することができます。  

### <a name="attack-surface-reduction"></a>攻撃の回避  

攻撃の回避規則は、マルウェアがコンピューターを悪意のあるコードに感染させるためによく使用する動作を防止するのに役立ちます。  

#### <a name="attack-surface-reduction-rules"></a>[攻撃の回避規則]  

- **Windows ローカル セキュリティ機関サブシステムからの資格情報の盗難にフラグを設定する**  
  **既定値**:未構成  
  規則: [Windows ローカル セキュリティ機関サブシステム (lsass.exe) からの資格情報の盗難をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-credential-stealing-from-the-windows-local-security-authority-subsystem)

  コンピューターを感染させるために、悪用目的のマルウェアによって一般的に使用されるアクションとアプリを防ぐのに役立ちます。  

  - **未構成**  
  - **[有効]** - Windows ローカル セキュリティ機関サブシステム (lsass.exe) からの資格情報の盗難にフラグを設定します。  
  - **[監査のみ]**  

- **[Adobe Reader (ベータ版) からのプロセスの作成]**  
  **既定値**:未構成  
  規則: [Adobe Reader による子プロセスの作成をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-adobe-reader-from-creating-child-processes)  

  - **未構成**  
  - **[有効]** - Adobe Reader から作成された子プロセスをブロックします。  
  - **[監査のみ]**  

#### <a name="rules-to-prevent-office-macro-threats"></a>Office マクロの脅威を防止するための規則  

Office アプリによる次の操作をブロックします。  

- **他のプロセス内に挿入する Office アプリ (例外なし)**  
  **既定値**:未構成  
  規則: [Office アプリケーションによる他のプロセスへのコード挿入をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-injecting-code-into-other-processes)  

  - **未構成**  
  - **[ブロック]** - Office アプリが他のプロセスに挿入することをブロックします。  
  - **[監査のみ]**  

- **実行可能なコンテンツを作成する Office アプリ/マクロ**  
  **既定値**:未構成  
  規則: [Office アプリケーションによる実行可能なコンテンツの作成をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-creating-executable-content)  

  - **未構成**  
  - **[ブロック]** - Office アプリとマクロが、実行可能なコンテンツを作成することをブロックします。  
  - **[監査のみ]**  

- **子プロセスを起動する Office アプリ**  
  **既定値**:未構成  
  規則: [すべての Office アプリケーションによる子プロセスの作成をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-all-office-applications-from-creating-child-processes)  

  - **未構成**  
  - **[ブロック]** - Office アプリが子プロセスを起動することをブロックします。  
  - **[監査のみ]**  
  
- **Office のマクロ コードからの Win32 のインポート**  
  **既定値**:未構成  
  規則: [Office マクロからの Win32 API 呼び出しをブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-win32-api-calls-from-office-macros)  

  - **未構成**  
  - **[ブロック]** - Office でマクロ コードから Win32 をインポートすることをブロックします。  
  - **[監査のみ]**  
  
- **[Office 通信製品からプロセスの作成]**  
  **既定値**:未構成  
  規則: [Office 通信アプリケーションによる子プロセスの作成をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-communication-application-from-creating-child-processes)  

  - **未構成**  
  - **[有効]** - Office の通信アプリからの子プロセスの作成をブロックします。  
  - **[監査のみ]**  

#### <a name="rules-to-prevent-script-threats"></a>スクリプトの脅威を防止するための規則  

スクリプトの脅威を防止するために以下をブロックします。  

- **難読化された js/vbs/ps/マクロ コード**  
  **既定値**:未構成  
  規則: [難読化された可能性のあるスクリプトの実行をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-execution-of-potentially-obfuscated-scripts)    

  - **未構成**  
  - **[ブロック]** - 難読化された js/vbs/ps/マクロ コードをブロックします。  
  - **[監査のみ]**  

- **インターネットからダウンロードしたペイロードを実行する js/vbs (例外なし)**  
  **既定値**:未構成  
  規則: [JavaScript または VBScript による、ダウンロードされた実行可能なコンテンツの起動をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-javascript-or-vbscript-from-launching-downloaded-executable-content)  

  - **未構成**  
  - **[ブロック]** - js/vbs が、インターネットからダウンロードしたペイロードを実行することをブロックします。  
  - **[監査のみ]**  

- **PSExec および WMI コマンドからのプロセス作成**  
  **既定値**:未構成  
  規則: [PSExec および WMI コマンドから開始されるプロセス作成をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-process-creations-originating-from-psexec-and-wmi-commands)  

  - **未構成**  
  - **[ブロック]** - PSExec および WMI コマンドから開始されるプロセス作成をブロックします。  
  
  - **[監査のみ]**  

- **USB から実行された信頼されていない署名なしのプロセス**  
  **既定値**:未構成  
  規則: [USB から実行された信頼されていない署名なしのプロセスをブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-untrusted-and-unsigned-processes-that-run-from-usb)    

  - **未構成**  
  - **[ブロック]** - USB から実行された信頼されていない署名なしのプロセスをブロックします。  
  - **[監査のみ]**  
  
- **普及、経過時間、または信頼されたリストの条件を満たしていない実行可能ファイル**  
  **既定値**:未構成  
  規則: [普及、経過時間、または信頼されたリストの条件を満たしていない実行可能ファイルの実行をブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-files-from-running-unless-they-meet-a-prevalence-age-or-trusted-list-criterion)    

  - **未構成**  
  - **[ブロック]** - 普及、経過時間、または信頼されたリストの条件を満たしていない実行可能ファイルの実行をブロックします。  
  - **[監査のみ]**  

#### <a name="rules-to-prevent-email-threats"></a>電子メールの脅威を防止するための規則  

電子メールの脅威を防止するために以下をブロックします。  

- **電子メール (Web メール/メール クライアント) からドロップされた実行可能なコンテンツ (exe、dll、ps、js、vbs など) の実行 (例外なし)**  
  **既定値**:未構成  
  規則: [電子メール クライアントと Web メールからの実行可能なコンテンツをブロックする](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-content-from-email-client-and-webmail)  

  - **未構成**  
  - **[ブロック]** - 電子メール (Web メール/メール クライアント) からドロップされた実行可能なコンテンツ (exe、dll、ps、js、vbs など) の実行をブロックします。  
  - **[監査のみ]**  

#### <a name="rules-to-protect-against-ransomware"></a>ランサムウェアから保護するための規則  

- **高度なランサムウェア防止**  
  既定:未構成  
  規則: [ランサムウェアに対して高度な保護を使用する](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#use-advanced-protection-against-ransomware)  

  - **未構成**  
  - **[有効]** - 積極的なランサムウェア防止を使います。  
  - **[監査のみ]**  

#### <a name="attack-surface-reduction-exceptions"></a>攻撃の回避の例外

- **[攻撃の回避規則から除外されたファイルとフォルダー]**  
  Defender CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)  

  - 攻撃の回避規則から除外するファイルとフォルダーが格納されている .csv ファイルを**インポート**します。  
  - ローカル ファイルまたはフォルダーを手動で**追加**します。  

> [!IMPORTANT]  
> LOB Win32 アプリを適切にインストールして実行できるようにするには、マルウェア対策設定で、以下のディレクトリをスキャン対象から除外する必要があります。  
> **X64 クライアント コンピューターの場合**:  
> *C:\Program Files (x86)\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>  
> **X86 クライアント コンピューターの場合**:  
> *C:\Program Files\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>
> 詳細については、「[現在サポートされているバージョンの Windows を搭載しているエンタープライズ コンピューターでウイルス スキャンを行う場合の推奨事項](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers)」を参照してください。


### <a name="controlled-folder-access"></a>フォルダー アクセスの制御  

ランサムウェアなど、悪意のあるアプリおよび脅威からの[重要なデータの保護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/controlled-folders)に役立ちます。  

- **[フォルダーの保護]**  
  **既定値**:未構成  
  Defender CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)  

  ファイルおよびフォルダーを、悪意のあるアプリによる未承認の変更から保護します。  

  - **未構成**  
  - **有効化**  
  - **[監査のみ]**  
  - **[ディスク変更のブロック]**  
  - **[ディスク変更の監査]**  

  *[未構成]* 以外の構成を選択した場合は、次の構成を行うことができます。  
  - **[保護されたフォルダーへのアクセス権を持つアプリの一覧]**  
    Defender CSP: [ControlledFolderAccessAllowedApplications](https://go.microsoft.com/fwlink/?linkid=872616)  

    - アプリの一覧が格納されている .csv ファイルを**インポート**します。  
    - アプリをこの一覧に手動で**追加**します。  

  - **[保護する必要がある追加フォルダーの一覧]**  
    Defender CSP: [ControlledFolderAccessProtectedFolders](https://go.microsoft.com/fwlink/?linkid=872617)  

    - フォルダーの一覧が格納されている .csv ファイルを**インポート**します。  
    - フォルダーをこの一覧に手動で**追加**します。  

### <a name="network-filtering"></a>ネットワーク フィルター  

評価が低い IP アドレスまたはドメインへの任意のアプリからの送信接続をブロックします ネットワーク フィルタリングは、監査モードとブロック モードの両方でサポートされています。  

- **[ネットワークの保護]**  
  **既定値**:未構成  
  Defender CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)  

  この設定の目的は、インターネット上のフィッシング詐欺、悪用ホスティング サイト、悪意のあるコンテンツにアクセスするアプリからエンド ユーザーを保護することです。 また、サードパーティのブラウザーが危険なサイトに接続するのを防ぐことができます。  

  - **[未構成]** - この機能が無効になります。 ユーザーとアプリは危険なドメインへの接続をブロックされません。 管理者は、このアクティビティを Microsoft Defender セキュリティ センターで確認することはできません。  
  - **[有効]** - ネットワーク保護を有効にし、ユーザーとアプリによる危険なドメインへの接続をブロックします。 管理者は、このアクティビティを Microsoft Defender セキュリティ センターで確認できます。  
  - **[監査のみ]** : - ユーザーとアプリは危険なドメインへの接続をブロックされません。 管理者は、このアクティビティを Microsoft Defender セキュリティ センターで確認できます。  

### <a name="exploit-protection"></a>悪用に対する保護  

- **[XML をアップロードする]**  
  **既定値**:*未構成*  

  悪用に対する保護を使用して、[デバイスを悪用から保護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)するには、必要なシステムとアプリケーションの軽減策設定を含む XML ファイルを作成します。 XML ファイルを作成するには、次の 2 つの方法があります。  

  - *PowerShell* - *Get-ProcessMitigation*、*Set-ProcessMitigation*、*ConvertTo-ProcessMitigationPolicy* のうちの 1 つ以上の PowerShell コマンドレットを使います。 これらのコマンドレットは、軽減策設定を構成し、それらの XML 表現をエクスポートします。  

  - "*Microsoft Defender セキュリティ センターの UI*" - Microsoft Defender セキュリティ センターで [アプリとブラウザー コントロール] をクリックしてから、結果画面の一番下までスクロールして Exploit Protection を見つけます。 まず、[システム設定] と [プログラム設定] タブを使用して、軽減策設定を構成します。 次に、画面の一番下にある [設定のエクスポート] リンクを見つけ、それらの XML 表現をエクスポートします。  

- **[悪用に対する保護インターフェイスのユーザー編集]**  
  **既定値**:未構成  
  ExploitGuard CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=872887)  


  - **[ブロック]** - メモリ、制御フロー、およびポリシーの制限を構成するための XML ファイルをアップロードします。 XML ファイル内の設定を使って、アプリケーションが悪用されるのをブロックできます。  
  - **[未構成]** - カスタム構成は使用されません。  

## <a name="microsoft-defender-application-control"></a>Microsoft Defender アプリケーション制御  

Microsoft Defender アプリケーション制御によって監査する必要がある、または実行しても差し支えないという信頼を Microsoft Defender アプリケーション制御から得られる追加のアプリを選択します。 Windows コンポーネントと Windows ストアのすべてのアプリは、実行しても差し支えないという信頼を自動的に得ます。  


- **[アプリケーション制御コード整合性ポリシー]**  
  **既定値**:未構成  
   CSP: [AppLocker CSP](https://go.microsoft.com/fwlink/?linkid=874543)  

  - **[強制]** - ユーザーのデバイス用のアプリケーション制御コード整合性ポリシーを選択します。  
  
    一度デバイスで有効にすると、アプリケーション制御はモードを " *[強制]* " から " *[監査のみ]* " に変更することのみで無効にできます。 モードを *[強制]* から *[未構成]* に変更すると、アプリケーション制御が引き続き割り当てられたデバイスに強制されます。  

  - **[未構成]** - アプリケーション制御はデバイスに追加されません。 ただし、以前に追加された設定は、割り当てられたデバイスに引き続き適用されます。 
 
  - **[監査のみ]** - アプリケーションはブロックされません。 すべてのイベントがローカル クライアントのログに記録されます。  

## <a name="microsoft-defender-credential-guard"></a>Microsoft Defender Credential Guard  

Windows Defender Credential Guard によって、資格情報盗難攻撃から保護されます。 特権のあるシステム ソフトウェアだけがアクセスできるように、シークレットを分離します。  

- **[Credential Guard]**  
  **既定値**:無効化  
  [DeviceGuard CSP](https://go.microsoft.com/fwlink/?linkid=872424)  

  - **[無効]** - 以前に Credential Guard が **[UEFI ロックなしで有効にする]** オプションで有効になっていた場合、Credential Guard をリモートで無効にします。  

  - **[UEFI ロックで有効にする]** - レジストリ キーまたはグループ ポリシーを使って Credential Guard をリモートで無効にできないようにします。  

    > [!NOTE]
    > この設定を使った場合、後で Credential Guard を無効にするときは、グループ ポリシーを **[無効]** に設定する必要があります。 また、UEFI の構成情報を各コンピューターから物理的にクリアします。 UEFI の構成が保持されている限り、Credential Guard は有効になっています。  

  - **[UEFI ロックなしで有効にする]** - グループ ポリシーを使って Credential Guard をリモートで無効にできるようにします。 この設定を使うデバイスは、Windows 10 バージョン 1511 以降を実行している必要があります。  

  Credential Guard を "*有効*" にすると、次の必要な機能も有効になります。  
  
  - **仮想化ベースのセキュリティ** (VBS)  
    次の再起動中にオンになります。 仮想化ベースのセキュリティは、Windows ハイパーバイザーを使ってセキュリティ サービスのサポートを提供します。  
  - **ディレクトリ メモリ アクセスによるセキュア ブート**  
    セキュア ブートと直接メモリ アクセス (DMA) の保護による VBS が有効になります。 DMA 保護は、ハードウェアのサポートを必要とし、正しく構成されたデバイスでのみ有効にされます。  

## <a name="microsoft-defender-security-center"></a>Microsoft Defender セキュリティ センター  

Microsoft Defender セキュリティ センターは、個々の機能とは別のアプリまたはプロセスとして動作します。 アクション センターで通知を表示します。 コレクターまたは 1 つの場所として機能し、状態の表示、各機能の一部の構成を実行します。 詳細については、[Microsoft Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-security-center/windows-defender-security-center) に関するドキュメントを参照してください。  

### <a name="microsoft-defender-security-center-app-and-notifications"></a>Microsoft Defender セキュリティ センターのアプリと通知  

Microsoft Defender セキュリティ センターのアプリのさまざまな領域に対するエンド ユーザー アクセスをブロックします。 セクションを非表示にすると、関連する通知もブロックされます。  

- **ウイルスと脅威の防止**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)  

  Microsoft Defender セキュリティ センターの [ウイルスと脅威の防止] 領域をエンド ユーザーに表示にするかどうかを構成します。 このセクションを非表示にすると、[ウイルスと脅威の防止] に関連する通知もすべてブロックされます。  

  - **未構成**  
  - **非表示**  

- **[ランサムウェア防止]**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)  

  Microsoft Defender セキュリティ センターの [ランサムウェア防止] 領域をエンド ユーザーに表示にするかどうかを構成します。 このセクションを非表示にすると、[ランサムウェア防止] に関連する通知もすべてブロックされます。  

  - **未構成**  
  - **非表示**  

- **[アカウント保護]**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)  

  Microsoft Defender セキュリティ センターの [アカウント保護] 領域をエンド ユーザーに表示にするかどうかを構成します。 このセクションを非表示にすると、[アカウント保護] に関連する通知もすべてブロックされます。  

  - **未構成**  
  - **非表示**  

- **ファイアウォールとネットワーク保護**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)  

  Microsoft Defender セキュリティ センターの [ファイアウォールとネットワーク保護] 領域をエンド ユーザーに表示にするかどうかを構成します。 このセクションを非表示にすると、[ファイアウォールとネットワーク保護] に関連する通知もすべてブロックされます。  

  - **未構成**  
  - **非表示**  

- **[アプリとブラウザーの制御]**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)  

  Microsoft Defender セキュリティ センターの [アプリとブラウザーの制御] 領域をエンド ユーザーに表示にするかどうかを構成します。 このセクションを非表示にすると、[アプリとブラウザーの制御] に関連する通知もすべてブロックされます。  

  - **未構成**  
  - **非表示**  

- **[ハードウェアの保護]**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)  

  Microsoft Defender セキュリティ センターの [ハードウェアの保護] 領域をエンド ユーザーに表示にするかどうかを構成します。 このセクションを非表示にすると、[ハードウェアの保護] に関連する通知もすべてブロックされます。  

  - **未構成**  
  - **非表示**  

- **デバイスのパフォーマンスと正常性**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)  

  Microsoft Defender セキュリティ センターの [デバイスのパフォーマンスと正常性] 領域をエンド ユーザーに表示にするかどうかを構成します。 このセクションを非表示にすると、[デバイスのパフォーマンスと正常性] に関連する通知もすべてブロックされます。  
  
  - **未構成**  
  - **非表示**  

- **ファミリー オプション**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)  

  Microsoft Defender セキュリティ センターの [ファミリー オプション] 領域をエンド ユーザーに表示にするかどうかを構成します。 このセクションを非表示にすると、[ファミリー オプション] に関連する通知もすべてブロックされます。  
  
  - **未構成**  
  - **非表示**  

- **[アプリの表示領域からの通知]**  
  **既定値**:未構成  
  WindowsDefenderSecurityCenter CSP: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)  

  エンド ユーザーに表示する通知を選択します。 重大ではない通知には、スキャンが完了したときの通知など、Microsoft Defender ウイルス対策アクティビティの概要が含まれます。 その他のすべての通知は重要とみなされます。  

  - **未構成**  
  - **[重大ではない通知のブロック]**  
  - **[すべての通知のブロック]**  

- **[システム トレイの Windows セキュリティ センター アイコン]**  
  **既定値**:未構成  

  通知領域コントロールの表示を構成します。 この設定を有効にするには、ユーザーがサインアウトしてからサインインするか、コンピューターを再起動する必要があります。  
  
  - **未構成**  
  - **非表示**  

- **[TPM のクリア ボタン]**  
  **既定値**:未構成  

  TPM のクリア ボタンの表示を構成します。  
  
  - **未構成**  
  - **無効化**  

- **[TPM ファームウェア更新に関する警告]**  
  **既定値**:未構成  
  
  脆弱性のあるファームウェアが検出された場合は、TPM ファームウェア更新プログラムの表示を構成します。  

  - **未構成**  
  - **非表示**  

- **[改ざん保護]**  
  **既定値**:未構成

  デバイスで [改ざん保護] をオンまたはオフにします。 [改ざん保護] を使用するには、[Microsoft Defender Advanced Threat Protection を Intune と統合](advanced-threat-protection.md)し、[Enterprise Mobility + Security E5 ライセンス](../fundamentals/licenses.md)を用意する必要があります。  
  - **[未構成]** - デバイスの設定に変更は加えられません。
  - **[有効]** - [改ざん保護] がオンになり、デバイスに制限が適用されます。
  - **[無効]** - [改ざん保護] がオフになり、制限は適用されません。

### <a name="it-contact-information"></a>IT の連絡先情報  

Microsoft Defender セキュリティ センターのアプリとアプリ通知に表示する IT の連絡先情報を指定します。  

**[アプリと通知に表示]** 、 **[アプリにのみ表示]** 、 **[通知にのみ表示]** または **[Don't display]\(表示しない\)** を選択できます。 **IT 組織名**と、以下の連絡先オプションの 1 つ以上を入力します。  


- **IT の連絡先情報**  
  **既定値**: [表示しない]  
  WindowsDefenderSecurityCenter CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)  
  
  IT の連絡先情報をエンド ユーザーに表示する場所を構成します。  
  
  - **[アプリと通知に表示]**  
  - **[アプリにのみ表示]**  
  - **[通知にのみ表示]**  
  - **[表示しない]**  

  表示するように構成した場合、次の設定を構成できます。  

  - **IT の組織名**  
    **既定値**:*未構成*  
    WindowsDefenderSecurityCenter CSP: [CompanyName](https://go.microsoft.com/fwlink/?linkid=873677)  

  - **IT 部門の電話番号または Skype ID**  
    **既定値**:*未構成*  
    WindowsDefenderSecurityCenter CSP: [Phone](https://go.microsoft.com/fwlink/?linkid=873678) 

  - **IT 部門の電子メール アドレス**  
    **既定値**:*未構成*  
    WindowsDefenderSecurityCenter CSP: [電子メール](https://go.microsoft.com/fwlink/?linkid=873679)  

  - **IT サポート用 Web サイトの URL**  
    **既定値**:*未構成*  
    WindowsDefenderSecurityCenter CSP: [URL](https://go.microsoft.com/fwlink/?linkid=873680)  
 
## <a name="local-device-security-options"></a>ローカル デバイスのセキュリティ オプション  

これらのオプションを使って、Windows 10 デバイス上のローカル セキュリティ設定を構成します。  

### <a name="accounts"></a>[アカウント]  

- **[新しい Microsoft アカウントを追加する]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [Accounts_BlockMicrosoftAccounts](https://go.microsoft.com/fwlink/?linkid=867916)  


  - **[ブロック]** - ユーザーはデバイスに新しい Microsoft アカウントを追加できません。  
  - **[未構成]** ユーザーはデバイスで Microsoft アカウントを使用できます。  

- **[パスワードを使用せずにリモート ログオンする]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867890)  


   - **[ブロック]** - デバイスのキーボードを使用してローカル アカウントと空のパスワードでのみサインインを許可します。  
   - **[未構成]** - 物理デバイス以外の場所からローカル アカウントと空のパスワードでサインインを許可します。  

#### <a name="admin"></a>管理者  

- **[ローカル管理者アカウント]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867850)  


  - **[ブロック]** ローカル管理者アカウントを使用できないようにします。  
  - **未構成**  

- **[管理者アカウントの名前を変更する]**  
  **既定値**:*未構成*  
  LocalPoliciesSecurityOptions CSP: [Accounts_RenameAdministratorAccount](https://go.microsoft.com/fwlink/?linkid=867917)  
 

  アカウント "管理者" のセキュリティ識別子 (SID) に関連付ける別のアカウント名を定義します。  

 #### <a name="guest"></a>ゲスト  

- **[Guest アカウント]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [LocalPoliciesSecurityOptions](https://go.microsoft.com/fwlink/?linkid=867853)  

  - **[ブロック]** - Guest アカウントを使用できないようにします。  
  - **未構成**  

- **[Guest アカウント名の変更]**  
  **既定値**:*未構成*  
  LocalPoliciesSecurityOptions CSP: [Accounts_RenameGuestAccount](https://go.microsoft.com/fwlink/?linkid=867918)  
  
  アカウント "Guest" のセキュリティ識別子 (SID) に関連付ける別のアカウント名を定義します。  

### <a name="devices"></a>デバイス  

- **[ログオンなしでデバイスを装着解除する]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [Devices_AllowUndockWithoutHavingToLogon](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-devices-allowundockwithouthavingtologon)  

  - **[ブロック]** - ユーザーはデバイスにサインインし、デバイスを取り外すアクセス許可を受ける必要があります。
  - **[未構成]** - ユーザーは装着しているポータブル デバイス本体の取り出しボタンを押すことでデバイスを安全に取り外すことができます。

- **[共有プリンターのプリンター ドライバーをインストールする]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [Devices_PreventUsersFromInstallingPrinterDriversWhenConnectingToSharedPrinters](https://go.microsoft.com/fwlink/?linkid=867921)  


  - **[有効]** - 任意のユーザーが共有プリンターに接続する過程でプリンター ドライバーをインストールできます。  
  - **[未構成]** - 管理者だけが共有プリンターに接続する過程でプリンター ドライバーをインストールできます。  

- **[CD-ROM へのアクセスをローカル アクティブ ユーザーに制限する]**  
  **既定値**:未構成  
  CSP:[Devices_RestrictCDROMAccessToLocallyLoggedOnUserOnly](https://go.microsoft.com/fwlink/?linkid=867922)  


  - **[有効]** - 対話的にログインしたユーザーだけが CD-ROM メディアを使用できます。 このポリシーが有効なとき、誰も対話的にログオンしていなければ、ネットワーク経由で CD-ROM にアクセスできます。  
  - **[未構成]** - 誰でも CD-ROM にアクセスできます。  

- **[リムーバブル メディアのフォーマットと取り出し]**  
  **既定値**:Administrators  
  CSP:[Devices_AllowedToFormatAndEjectRemovableMedia](https://go.microsoft.com/fwlink/?linkid=867920)  
 

  リムーバブル NTFS メディアをフォーマットして取り出すことができるユーザーを定義します。  
  - **未構成**  
  - **Administrators**  
  - **Administrators と Power Users**  
  - **Administrators と Interactive Users**  

### <a name="interactive-logon"></a>対話型ログオン  

- **スクリーン セーバーがアクティブになるまでのロック画面の非アクティブ時間 (分)**  
  **既定値**:*未構成*  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_MachineInactivityLimit](https://go.microsoft.com/fwlink/?linkid=867891)  


  時間を分単位で入力します。デスクトップの対話型サインイン画面で操作のないままこの時間を経過すると、スクリーン セーバーが起動します。 (**0** - **99999**)  

- **[ログオンに Ctrl+Alt+Del が必要]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_DoNotRequireCTRLALTDEL](https://go.microsoft.com/fwlink/?linkid=867951)  


  - **[有効]** - ユーザーが Windows にログオンするには、先に Ctrl + Alt + Del キーを押す必要があります。
  - **[未構成]** - ユーザーがサインインするときに Ctrl + Alt + Del キーを押す必要はありません。

- **スマート カードを取り外したときの動作**  
  **既定値**:ワークステーションをロックする   
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_SmartCardRemovalBehavior](https://go.microsoft.com/fwlink/?linkid=868437)  
    
  ログオンしているユーザーのスマート カードがスマート カード リーダーから取り出されたときの動作を決定します。 次のようなオプションがあります。  

  - **[ワークステーションをロックする]** - スマート カードが取り出されると、ワークステーションがロックされます。 このオプションを利用すると、スマート カードを持って場所を離れ、なおかつ、保護されたセッションを維持できます。  
  - **[何もしない]**  
  - **[ログオフを強制する]** - スマート カードが取り出されると、ユーザーは自動的にログオフされます。  
  - **[リモート デスクトップ サービス セッションであれば、切断する]** - スマート カードを取り出すと、ユーザーをログオフさせずにセッションを切断します。 このオプションを利用すると、後でスマート カードを挿入し、セッションを再開できます。あるいは、スマート カード リーダーを装備した別のコンピューターにスマート カードを挿入し、セッションを再開できます。もう一度サインインする必要はありません。 セッションがローカルの場合、このポリシーの機能は [ワークステーションをロックする] と同じになります。  

#### <a name="display"></a>ディスプレイ  

- **[ロック画面上のユーザー情報]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_DisplayUserInformationWhenTheSessionIsLocked](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-displayuserinformationwhenthesessionislocked)  

  セッションがロックされているときに表示されるユーザー情報を構成します。 構成しないと、ユーザーの表示名、ドメイン、およびユーザー名が表示されます。  

  - **未構成**  
  - **ユーザーの表示名、ドメイン、ユーザー名**  
  - **ユーザーの表示名のみ**  
  - **ユーザー情報を表示しない**  

- **[最後にサインインしたユーザーを表示しない]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_DoNotDisplayLastSignedIn](https://go.microsoft.com/fwlink/?linkid=868437)  
  
  
  - **[有効]** - ユーザー名を非表示にします。  
  - **[未構成]** - 最後のユーザー名を表示します。  

- **[サインイン時にユーザー名を表示しない]** 
  **既定値**: 未構成  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_DoNotDisplayUsernameAtSignIn](https://go.microsoft.com/fwlink/?linkid=867959)  

  
  - **[有効]** - ユーザー名を非表示にします。  
  - **[未構成]** - 最後のユーザー名を表示します。  

- **[Logon message title]\(ログオン メッセージのタイトル\)**  
  **既定値**:*未構成*  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_MessageTitleForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867964)  

  サインインしようとしているユーザーへのメッセージのタイトルを設定します。  

- **[Logon message text]\(ログオン メッセージのテキスト\)**  
  **既定値**:*未構成*  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_MessageTextForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867962)  

  サインインしようとしているユーザーへのメッセージのテキストを設定します。  
  
### <a name="network-access-and-security"></a>ネットワーク アクセスとセキュリティ

- **[名前付きパイプと共有への匿名アクセス]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [NetworkAccess_RestrictAnonymousAccessToNamedPipesAndShares](https://go.microsoft.com/fwlink/?linkid=868432)  

  - **[未構成]** - 匿名アクセスを共有と名前付きパイプの設定に制限します。 匿名でアクセスできる設定に適用されます。  
  - **[ブロック]** - このポリシーを無効にします。それにより匿名アクセスを使用できるようになります。  

- **[SAM アカウントの匿名の列挙]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSAMAccounts](https://go.microsoft.com/fwlink/?linkid=868434)  
  
  - **[未構成]** - 匿名ユーザーが SAM アカウントを列挙できます。  
  - **[ブロック]** - SAM アカウントの匿名の列挙を禁止します。  

- **[SAM アカウントと共有の匿名の列挙]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares](https://go.microsoft.com/fwlink/?linkid=868435)  

  - **[未構成]** - 匿名ユーザーがドメイン アカウントとネットワーク共有の名前を列挙できます。  
  - **[ブロック]** - SAM アカウントと共有の匿名の列挙を禁止します。 

- **[パスワードの変更時に LAN Manager ハッシュ値を保存する]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_DoNotStoreLANManagerHashValueOnNextPasswordChange](https://go.microsoft.com/fwlink/?linkid=868431)  
   
  次にパスワードを変更したときに、パスワードのハッシュ値を保存するかどうかを判断します。 
  - **[未構成]** - ハッシュ値は保存されません。  
  - **[ブロック]** - LAN Manager (LM) によって、新しいパスワードのハッシュ値が格納されます。  

- **[PKU2U 認証要求]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_AllowPKU2UAuthenticationRequests](https://go.microsoft.com/fwlink/?linkid=867892)  

  - **[未構成]** - PU2U 要求を許可します。  
  - **[ブロック]** - デバイスに対する PKU2U 認証要求をブロックします。  

- **[ソフトウェア アセット管理へのリモート RPC 接続を制限する]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [NetworkAccess_RestrictClientsAllowedToMakeRemoteCallsToSAM](https://go.microsoft.com/fwlink/?linkid=867893)  
  
  - **[未構成]** - 既定のセキュリティ記述子を使用します。これにより、SAM へのリモート RPC 呼び出しをユーザーとグループに許可することができます。
  - **[許可]** - セキュリティ アカウント マネージャー (SAM) へのリモート RPC 呼び出し (これにより、ユーザー アカウントとパスワードが格納される) をユーザーとグループが行うことを拒否します。 また、 **[許可]** により、セキュリティ記述子定義言語の既定 (SDDL) の文字列を編集して、このようなユーザーおよびグループによるソフトウェア アセット管理へのリモート呼び出しを明示的に許可または拒否することもできます。  

    - **セキュリティ記述子**  
      **既定値**:*未構成*  
    
- **[Minimum Session Security For NTLM SSP Based Clients]\(NTLM SSP ベースのクライアント向け最小セッション セキュリティ\)**  
  **既定値**:なし  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedClients](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)  
  
  このセキュリティ設定を使用すると、サーバーで 128 ビット暗号化および/または NTLMv2 セッション セキュリティのネゴシエーションが必要になるようにすることができます。  

  - **なし**  
  - **[NTLMv2 セッション セキュリティが必要]**  
  - **[128 ビット暗号化を要求する]**  
  - **[NTLMv2 and 128-bit encryption]\(NTLMv2 および 128 ビットの暗号化\)**  
 
- **[Minimum Session Security For NTLM SSP Based Server]\(NTLM SSP ベースのサーバー向け最小セッション セキュリティ\)**  
  **既定値**:なし  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedServers](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)  

  このセキュリティ設定では、ネットワーク ログオンに使用されるチャレンジ/レスポンス認証プロトコルが決定されます。  

  - **なし**  
  - **[NTLMv2 セッション セキュリティが必要]**  
  - **[128 ビット暗号化を要求する]**  
  - **[NTLMv2 and 128-bit encryption]\(NTLMv2 および 128 ビットの暗号化\)**  

- **[LAN Manager 認証レベル]**  
  **既定値**:LM および NTLM  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_LANManagerAuthenticationLevel](https://aka.ms/policy-csp-localpoliciessecurityoptions-lanmanagerauthenticationlevel)  


  - **LM および NTLM**  
  - **LM、NTLM、および NTLMv2**  
  - **[NTLM]**  
  - **[NTLMv2]**  
  - **[LM ではなく NTLMv2]**  
  - **[LM や NTLM ではなく NTLMv2]**  
  
- **[安全でないゲスト ログオン]**  
  **既定値**:未構成  
  LanmanWorkstation CSP: [LanmanWorkstation](https://aka.ms/policy-csp-lanmanworkstation-enableinsecureguestlogons)  

  この設定を有効にした場合、安全でないゲストのログオンは SMB クライアントによって拒否されます。  

  - **未構成**  
  - **[ブロック]** - 安全でないゲストのログオンは SMB クライアントによって拒否されます。  

### <a name="recovery-console-and-shutdown"></a>回復コンソールとシャットダウン  

- **[シャットダウン時に仮想メモリのページ ファイルをクリアする]**  
  **既定値**:未構成  
   LocalPoliciesSecurityOptions CSP: [Shutdown_ClearVirtualMemoryPageFile](https://go.microsoft.com/fwlink/?linkid=867914)  


  - **[有効]** - デバイスの電源を切るときに仮想メモリのページ ファイルが消去されます。  
  - **[未構成]** - 仮想メモリは消去されません。  

- **[Shut down without log on]\(ログオンせずにシャットダウン\)**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [Shutdown_AllowSystemToBeShutDownWithoutHavingToLogOn](https://go.microsoft.com/fwlink/?linkid=867912)  

  
  - **[ブロック]** - Windows サインイン画面でシャットダウン オプションが非表示になります。 ユーザーはデバイスにサインインし、それからシャットダウンする必要があります。  
  - **[未構成]** - ユーザーに Windows サインイン画面からデバイスをシャットダウンすることを許可します。  

### <a name="user-account-control"></a>ユーザー アカウント制御  

- **[セキュリティで保護された場所を使用しない UIA 整合性]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867897)  
  
  - **[ブロック]** - ファイル システム内のセキュリティで保護されている場所にあるアプリは、UIAccess 整合性でのみ実行されます。  
  - **[未構成]** - アプリが置かれているファイル システム内の場所がセキュリティで保護されていない場合でも、アプリを UIAccess 整合性で実行できます。  

- **[ファイルおよびレジストリの書き込みエラーをユーザーごとの場所に仮想化する]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations](https://go.microsoft.com/fwlink/?linkid=867900)  

  - **[有効]** - 保護されている場所にデータを書き込むアプリケーションは失敗します。  
  - **[ブロック]** - ファイル システムとレジストリに関して、アプリケーションの書き込みエラーが実行時に、ユーザーに定義されている場所にリダイレクトされます。  

- **[署名および検証された実行可能ファイルのみを昇格]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867965)  

  - **[有効]** - 実行可能ファイルを実行する前に PKI 証明書パス検証が強制されます。  
  - **[未構成]** - 実行ファイルの実行前に PKI 証明書パス検証が強制されません。  

#### <a name="uia-elevation-prompt-behavior"></a>[UIA 昇格時のプロンプトの動作]  

- **[管理者の昇格時のプロンプト]**  
  **既定値**:非 Windows バイナリに対して同意を要求します  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_BehaviorOfTheElevationPromptForAdministrators](https://go.microsoft.com/fwlink/?linkid=867895)  

  管理者承認モードの管理者に対する昇格時のプロンプトの動作を定義します。  

  - **未構成**  
  - **プロンプトを表示せずに昇格する**  
  - **セキュリティで保護されたデスクトップで資格情報を要求する**  
  - **資格情報を要求する**  
  - **同意を要求する**  
  - **[非 Windows バイナリで同意を要求する]**  


- **[標準ユーザーの昇格時のプロンプト]**  
  **既定値**:資格情報を要求する  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_BehaviorOfTheElevationPromptForStandardUsers](https://go.microsoft.com/fwlink/?linkid=867896)  

  標準ユーザーに対する昇格時のプロンプトの動作を定義します。  

  - **未構成**  
  - **昇格要求を自動的に拒否する**  
  - **セキュリティで保護されたデスクトップで資格情報を要求する**  
  - **資格情報を要求する**  

- **[昇格時のプロンプトをユーザーの対話型のデスクトップにルーティング]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_SwitchToTheSecureDesktopWhenPromptingForElevation](https://go.microsoft.com/fwlink/?linkid=867899)  


  - **[有効]** - すべての昇格要求が、セキュリティで保護されたデスクトップではなく、対話ユーザーのデスクトップに送られます。 管理者と標準ユーザーに対するプロンプト動作ポリシーの設定が使用されます。  
  - **[未構成]** - 管理者と標準ユーザーのプロンプト動作ポリシーの設定に関係なく、すべての昇格要求がセキュリティで保護されたデスクトップに送られます。

- **[アプリのインストールでの昇格時のプロンプト]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_DetectApplicationInstallationsAndPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867901)  

   - **[無効]** - アプリケーション インストール パッケージは検出されず、昇格は求められません。
   - **[未構成]** - アプリケーション インストール パッケージで管理者特権が必要なとき、管理ユーザーの名前とパスワードの入力がユーザーに求められます。

- **[セキュリティで保護されたデスクトップを使用しない UIA 昇格時のプロンプト]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_AllowUIAccessApplicationsToPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867894)  

- **[有効]** - UIAccess アプリで、セキュリティで保護されたデスクトップを使わずに昇格を要求できます。  
- **[未構成]** - 昇格プロンプトではセキュリティで保護されたデスクトップが使用されます。  

#### <a name="admin-approval-mode"></a>管理者承認モード  

- **[ビルトイン Administrator の管理者承認モード]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_UseAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867902)  

  - **[有効]** - ビルトイン Administrator アカウントで管理者承認モードを使用できます。 ある操作で特権の昇格が必要になると、その操作を承認するようにユーザーに求めます。  
  - **[未構成]** - 完全管理者特権ですべてのアプリが実行されます。  

- **[すべての管理者を管理者承認モードで実行する]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_RunAllAdministratorsInAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867898)  


  - **[有効]** - 管理者承認モードを有効にします。  
  - **[未構成]** - 管理者承認モードと関連するすべての UAC ポリシー設定が無効になります。  

### <a name="microsoft-network-client"></a>Microsoft ネットワーク クライアント  

- **[通信にデジタル署名を行う (サーバーが同意した場合)]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [MicrosoftNetworkClient_DigitallySignCommunicationsIfServerAgrees](https://go.microsoft.com/fwlink/?linkid=868423)  

  SMB クライアントで SMB パケット署名をネゴシエートするかどうかを決定します。  
  - **[ブロック]** - SMB クライアントでは SMB パケットの署名がネゴシエートされません。
  - **[未構成]** - Microsoft ネットワーク クライアントは、セッションのセットアップ時に SMB パケットの署名を実行するようサーバーに要求します。 サーバーでパケットの署名が有効になっている場合、パケットの署名がネゴシエートされます。  

- **[暗号化されていないパスワードをサード パーティの SMB サーバーに送信する]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [MicrosoftNetworkClient_SendUnencryptedPasswordToThirdPartySMBServers](https://go.microsoft.com/fwlink/?linkid=868426)  


  - **[有効]** - サーバー メッセージ ブロック (SMB) リダイレクターで、認証時にパスワードの暗号化をサポートしていない Microsoft 以外の SMB サーバーにプレーンテキストのパスワードを送信できます。  
  - **[未構成]** - プレーンテキスト パスワードの送信をブロックします。 パスワードは暗号化されます。  

- **[通信にデジタル署名を行う (常時)]**  
  **既定値**:未構成  
  LocalPoliciesSecurityOptions CSP: [MicrosoftNetworkClient_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868425)  


  - **[有効]** - Microsoft ネットワーク クライアントは、Microsoft ネットワーク サーバーが SMB パケットの署名に同意しない限り、そのサーバーと通信しません。  
  - **[未構成]** - クライアントとサーバーの間で SMB パケットの署名がネゴシエートされます。  

### <a name="microsoft-network-server"></a>Microsoft ネットワーク サーバー  
  
- **[通信にデジタル署名を行う (クライアントが同意した場合)]**  
  **既定値**:未構成  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsIfClientAgrees](https://go.microsoft.com/fwlink/?linkid=868429)  

  - **[有効]** - Microsoft ネットワーク サーバーは、クライアントから要求されたら、SMB パケットの署名をネゴシエートします。 つまり、クライアントでパケットの署名が有効になっている場合、パケットの署名がネゴシエートされます。  
  - **[未構成]** - SMB クライアントでは SMB パケットの署名がネゴシエートされません。  

- **[通信にデジタル署名を行う (常時)]**  
  **既定値**:未構成  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868428)  

  - **[有効]** - Microsoft ネットワーク サーバーは、Microsoft ネットワーク クライアントが SMB パケットの署名に同意しない限り、そのクライアントと通信しません。  
  - **[未構成]** - クライアントとサーバーの間で SMB パケットの署名がネゴシエートされます。  

## <a name="xbox-services"></a>Xbox サービス

- **[Xbox セーブ データ タスク]**  
  **既定値**:未構成  
  CSP: [TaskScheduler/EnableXboxGameSaveTask](https://go.microsoft.com/fwlink/?linkid=875480)  
   
  この設定では、Xbox セーブ データ タスクが [有効] または [無効] のどちらであるかを決定します。  
  - **Enabled**
  - **未構成**

- **[Xbox Accessory Management Service]**  
  **既定値**:手動  
  CSP: [SystemServices/ConfigureXboxAccessoryManagementServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875481)  

  この設定では、Accessory Management Service の開始の種類を決定します。  
  - **[手動]**
  - **自動**
  - **[無効]**

- **[Xbox Live Auth Manager サービス]**  
  **既定値**:手動  
  CSP: [SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875482)  
 
  この設定では、Live Auth Manager Service サービスの開始の種類を決定します。  
  - **[手動]**
  - **自動**
  - **[無効]**
 
- **[Xbox Live セーブ データ サービス]**  
  **既定値**:手動  
  CSP: [SystemServices/ConfigureXboxLiveGameSaveServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875483)  

  この設定では、Live セーブ データ サービスの開始の種類を決定します。  
  - **[手動]**
  - **自動**
  - **[無効]**

- **[Xbox Live ネットワーク サービス]**  
  **既定値**:手動  
  CSP: [SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875484)  

  この設定では、ネットワーク サービスの開始の種類を決定します。  
  - **[手動]**
  - **自動**
  - **[無効]**

## <a name="next-steps"></a>次のステップ

プロファイルは作成されましたが、まだ何も行われていません。 次に、[プロファイルを割り当て](../configuration/device-profile-assign.md)、[その状態を監視](../configuration/device-profile-monitor.md)します。  

[macOS](endpoint-protection-macos.md) デバイス上でエンドポイント保護設定を構成します。  
